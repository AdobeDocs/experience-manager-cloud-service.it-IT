---
title: Convalida e debug con gli strumenti di Dispatcher
description: Scopri la convalida locale, il debug, la struttura del file in modalità flessibile e come migrare dalla modalità legacy alla modalità flessibile.
feature: Dispatcher
exl-id: 9e8cff20-f897-4901-8638-b1dbd85f44bf
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '2990'
ht-degree: 1%

---

# Convalida e debug con gli strumenti di Dispatcher {#Dispatcher-in-the-cloud}

## Introduzione {#apache-and-dispatcher-configuration-and-testing}

>[!NOTE]
>Per ulteriori informazioni su Dispatcher nel cloud e su come scaricare gli strumenti di Dispatcher, vedi [Dispatcher nel cloud](/help/implementing/dispatcher/disp-overview.md) pagina. Se la configurazione del Dispatcher è in modalità legacy, consulta [documentazione della modalità legacy](/help/implementing/dispatcher/validation-debug-legacy.md).

Le sezioni seguenti descrivono la struttura del file in modalità flessibile, la convalida locale, il debug e la migrazione dalla modalità precedente alla modalità flessibile.

Questo articolo presuppone che la configurazione del Dispatcher del progetto includa il file `opt-in/USE_SOURCES_DIRECTLY`. Questo file fa sì che l’SDK e il runtime convalidino e distribuiscano la configurazione in modo migliore rispetto alla modalità precedente, rimuovendo le limitazioni relative al numero e alle dimensioni dei file.

Se la configurazione del Dispatcher non include il file indicato in precedenza, l’Adobe consiglia di migrare dalla modalità legacy alla modalità flessibile come descritto nella [Migrazione dalla modalità legacy alla modalità flessibile](#migrating) sezione.

## Struttura del file {#flexible-mode-file-structure}

La struttura della sottocartella di Dispatcher del progetto è la seguente:

```bash
./
├── conf.d
│   ├── available_vhosts
│   │   ├── my_site.vhost # Created by customer
│   │   └── default.vhost
│   ├── dispatcher_vhost.conf
│   ├── enabled_vhosts
│   │   ├── README
│   │   └── my_site.vhost -> ../available_vhosts/my_site.vhost  # Created by customer
│   └── rewrites
│   │   ├── default_rewrite.rules
│   │   └── rewrite.rules
│   └── variables
|       ├── custom.vars
│       └── global.vars
│── opt-in
│   └── USE_SOURCES_DIRECTLY
└── conf.dispatcher.d
    ├── available_farms
    │   ├── my_farm.farm # Created by customer
    │   └── default.farm
    ├── cache
    │   ├── default_invalidate.any
    │   ├── default_rules.any
    │   ├── marketing_query_parameters.any
    │   └── rules.any
    ├── clientheaders
    │   ├── clientheaders.any
    │   └── default_clientheaders.any
    ├── dispatcher.any
    ├── enabled_farms
    │   ├── README
    │   └── my_farm.farm -> ../available_farms/my_farm.farm  # Created by customer
    ├── filters
    │   ├── default_filters.any
    │   └── filters.any
    ├── renders
    │   └── default_renders.any
    └── virtualhosts
    │   ├── default_virtualhosts.any
    │   └── virtualhosts.any
    
```

Di seguito è riportata una spiegazione dei file rilevanti che possono essere modificati:

**File personalizzabili**

I seguenti file sono personalizzabili e vengono trasferiti nell’istanza Cloud al momento dell’implementazione:

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

Puoi avere uno o più di questi file. Contengono `<VirtualHost>` voci che corrispondono ai nomi host e consentono ad Apache di gestire ogni traffico di dominio con regole diverse. I file vengono creati in `available_vhosts` e abilitati con un collegamento simbolico nel `enabled_vhosts` directory. Dalla sezione `.vhost` sono inclusi file e altri file, ad esempio riscritture e variabili.

>[!NOTE]
>
>In modalità flessibile, è necessario utilizzare percorsi relativi invece di percorsi assoluti.

Verificare che sia sempre disponibile almeno un host virtuale corrispondente a ServerAlias `\*.local`, `localhost`, e `127.0.0.1` necessari per l’annullamento della validità di Dispatcher. Alias del server `*.adobeaemcloud.net` e `*.adobeaemcloud.com` sono necessarie anche in almeno una configurazione vhost e sono necessarie per i processi di Adobe interni.

Se desideri trovare la corrispondenza esatta con l’host perché disponi di più file vhost, puoi seguire l’esempio seguente:

```
<VirtualHost *:80>
    ServerName    "example.com"
    # Put names of which domains are used for your published site/content here
    ServerAlias     "*example.com" "\*.local" "localhost" "127.0.0.1" "*.adobeaemcloud.net" "*.adobeaemcloud.com"
    # Use a document root that matches the one in conf.dispatcher.d/default.farm
    DocumentRoot "${DOCROOT}"
    # URI dereferencing algorithm is applied at Sling's level, do not decode parameters here
    AllowEncodedSlashes NoDecode
    # Add header breadcrumbs for help in troubleshooting which vhost file is chosen
    <IfModule mod_headers.c>
        Header add X-Vhost "publish-example-com"
    </IfModule>
  ...
</VirtualHost>
```

* `conf.d/enabled_vhosts/<CUSTOMER_CHOICE>.vhost`

Questa cartella contiene collegamenti simbolici relativi a file in conf.dispatcher.d/available_hosts.

Comandi di esempio necessari per creare questi collegamenti simbolici:

Apple macOS, Linux e WSL

```
ln -s ../available_vhosts/wknd.vhost wknd.vhost
```

Microsoft Windows

```
mklink wknd.vhost ..\available_vhosts\wknd.vhost
```

>[!NOTE]
>
> Quando si lavora con collegamenti simbolici in Windows, è necessario eseguire il comando in un prompt dei comandi con privilegi elevati, nel Sottosistema Windows per Linux oppure [Creare collegamenti simbolici](https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/create-symbolic-links) privilegio assegnato.

* `conf.d/rewrites/rewrite.rules`

Il file è incluso dall’interno del tuo `.vhost` file. Ha una serie di regole di riscrittura per `mod_rewrite`.

* `conf.d/variables/custom.vars`

Il file è incluso dall’interno del tuo `.vhost` file. Puoi aggiungere definizioni per le variabili Apache in questa posizione.

* `conf.d/variables/global.vars`

Il file viene incluso dall&#39;interno di `dispatcher_vhost.conf` file. Puoi modificare il Dispatcher e riscrivere il livello di registro in questo file.

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

Puoi avere uno o più di questi file, che contengono farm con nomi host corrispondenti e consentono al modulo Dispatcher di gestire ogni farm con regole diverse. I file vengono creati in `available_farms` e abilitati con un collegamento simbolico nel `enabled_farms` directory. Dalla sezione `.farm` sono inclusi file, altri file come filtri, regole di cache e altri.

* `conf.dispatcher.d/enabled_farms/<CUSTOMER_CHOICE>.farm`

Questa cartella contiene collegamenti simbolici relativi ai file in conf.dispatcher.d/available_farms.

Comandi di esempio necessari per creare questi collegamenti simbolici:

Apple macOS, Linux e WSL

```
ln -s ../available_farms/wknd.farm wknd.farm
```

Microsoft Windows

```
mklink wknd.farm ..\available_farms\wknd.farm
```

>[!NOTE]
>
> Quando si lavora con collegamenti simbolici in Windows, è necessario eseguire il comando in un prompt dei comandi con privilegi elevati, nel Sottosistema Windows per Linux oppure [Creare collegamenti simbolici](https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/create-symbolic-links) privilegio assegnato.

* `conf.dispatcher.d/cache/rules.any`

Il file è incluso dall’interno del tuo `.farm` file. Specifica le preferenze di caching.

* `conf.dispatcher.d/clientheaders/clientheaders.any`

Il file è incluso dall’interno del tuo `.farm` file. Specifica le intestazioni di richiesta da inoltrare al backend.

* `conf.dispatcher.d/filters/filters.any`

Il file è incluso dall’interno del tuo `.farm` file. Ha una serie di regole che modificano il tipo di traffico da filtrare e non lo rendono al backend.

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

Il file è incluso dall’interno del tuo `.farm` file. Dispone di un elenco di nomi host o percorsi URI a cui deve corrispondere la corrispondenza glob. Questa corrispondenza determina il backend da utilizzare per distribuire una richiesta.

* `opt-in/USE_SOURCES_DIRECTLY`

Questo file consente una configurazione di Dispatcher più flessibile e rimuove le limitazioni precedenti relative al numero e alle dimensioni dei file. Inoltre, l’SDK e il runtime possono convalidare e distribuire la configurazione in modo migliorato.

I file di cui sopra fanno riferimento ai file di configurazione immutabili elencati di seguito. Le modifiche ai file immutabili non vengono elaborate da Dispatcher in ambienti Cloud.

**File di configurazione immutabili**

Questi file fanno parte del framework di base e applicano standard e best practice. I file sono considerati immutabili perché la loro modifica o eliminazione locale non ha alcun impatto sulla distribuzione, in quanto non vengono trasferiti nell’istanza Cloud.

Si consiglia che i file di cui sopra facciano riferimento ai file immutabili elencati di seguito, seguiti da eventuali istruzioni o sostituzioni aggiuntive. Quando la configurazione di Dispatcher viene distribuita in un ambiente cloud, viene utilizzata la versione più recente dei file immutabili, indipendentemente dalla versione utilizzata nello sviluppo locale.

* `conf.d/available_vhosts/default.vhost`

Contiene un host virtuale di esempio. Per il tuo host virtuale, crea una copia di questo file, personalizzalo, vai a `conf.d/enabled_vhosts` e crea un collegamento simbolico alla copia personalizzata.
Non copiare il file default.vhost direttamente in `conf.d/enabled_vhosts`.

Verificare che sia sempre disponibile un host virtuale corrispondente a ServerAlias `\*.local`, `localhost`, e `127.0.0.1` necessari per l’annullamento della validità di Dispatcher. Alias del server `*.adobeaemcloud.net` e `*.adobeaemcloud.com` sono necessarie per i processi di Adobe interni.

* `conf.d/dispatcher_vhost.conf`

Parte del framework di base, utilizzato per illustrare come vengono inclusi gli host virtuali e le variabili globali.

* `conf.d/rewrites/default_rewrite.rules`

Le regole di riscrittura predefinite sono idonee per un progetto standard. Se hai bisogno di personalizzazione, modifica `rewrite.rules`. Nella personalizzazione, puoi comunque includere prima le regole predefinite, se soddisfano le tue esigenze.

* `conf.dispatcher.d/available_farms/default.farm`

Contiene un esempio di farm di Dispatcher. Per la tua farm, crea una copia di questo file, personalizzalo, vai a `conf.d/enabled_farms` e crea un collegamento simbolico alla copia personalizzata.

* `conf.dispatcher.d/cache/default_invalidate.any`

Parte del framework di base, viene generato all&#39;avvio. Sei **obbligatorio** per includere questo file in ogni farm definita, nel `cache/allowedClients` sezione.

* `conf.dispatcher.d/cache/default_rules.any`

Regole di cache predefinite adatte a un progetto standard. Se hai bisogno di personalizzazione, modifica `conf.dispatcher.d/cache/rules.any`. Nella personalizzazione, puoi comunque includere prima le regole predefinite, se soddisfano le tue esigenze.

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

Intestazioni di richiesta predefinite per l’inoltro al backend, adatte a un progetto standard. Se hai bisogno di personalizzazione, modifica `clientheaders.any`. Nella personalizzazione, puoi comunque includere prima le intestazioni di richiesta predefinite, se soddisfano le tue esigenze.

* `conf.dispatcher.d/dispatcher.any`

Parte del framework di base, utilizzato per illustrare come vengono incluse le farm di Dispatcher.

* `conf.dispatcher.d/filters/default_filters.any`

Filtri predefiniti adatti a un progetto standard. Se hai bisogno di personalizzazione, modifica `filters.any`. Nella personalizzazione, puoi comunque includere prima i filtri predefiniti, se soddisfano le tue esigenze.

* `conf.dispatcher.d/renders/default_renders.any`

Parte del framework di base, questo file viene generato all’avvio. Sei **obbligatorio** per includere questo file in ogni farm definita, nel `renders` sezione.

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

Globbing host predefinito adatto a un progetto standard. Se hai bisogno di personalizzazione, modifica `virtualhosts.any`. Nella personalizzazione, non devi includere il globbing host predefinito, in quanto corrisponde a **ogni** richiesta in ingresso.

## Moduli Apache supportati {#apache-modules}

Consulta [Moduli Apache supportati](/help/implementing/dispatcher/disp-overview.md#supported-directives).

## Convalida locale {#local-validation-flexible-mode}

>[!NOTE]
>
>Le sezioni seguenti includono comandi che utilizzano le versioni Mac o Linux® dell’SDK, ma l’SDK di Windows può essere utilizzato anche in modo simile.

Utilizza il `validate.sh` script come mostrato di seguito:

```
$ validate.sh src/dispatcher
opt-in USE_SOURCES_DIRECTLY marker file detected
Phase 1: Dispatcher validator
Cloud manager validator 2.0.32
Phase 1 finished
Phase 2: httpd -t validation in docker image
values.csv not found in deployment folder: /Users/foo/src - using files in 'conf.d' and 'conf.dispatcher.d' subfolders directly
processing configuration subfolder: conf.d
processing configuration subfolder: conf.dispatcher.d
Running script /docker_entrypoint.d/10-check-environment.sh
Running script /docker_entrypoint.d/20-create-docroots.sh
Running script /docker_entrypoint.d/30-wait-for-backend.sh
Waiting until localhost is available
localhost resolves to ::1
Running script /docker_entrypoint.d/40-generate-allowed-clients.sh
Running script /docker_entrypoint.d/50-check-expiration.sh
Running script /docker_entrypoint.d/60-check-loglevel.sh
Running script /docker_entrypoint.d/70-check-forwarded-host-secret.sh
# Dispatcher configuration: (/etc/httpd/conf.dispatcher.d/dispatcher.any)
/farms {

... 

}
Syntax OK
Phase 2 finished
Phase 3: Immutability check
reading immutable file list from /etc/httpd/immutable.files.txt

...

no immutable file has been changed - check is SUCCESSFUL
Phase 3 finished
```

Lo script prevede le tre fasi seguenti:

1. Esegue la convalida. Se la configurazione non è valida, lo script non riesce.
2. Esegue il `httpd -t` per verificare se la sintassi è corretta in modo che Apache httpd possa avviarsi. In caso di esito positivo, la configurazione deve essere pronta per la distribuzione.
3. Verifica che il sottoinsieme dei file di configurazione dell’SDK di Dispatcher, destinati a essere immutabili come descritto in [Sezione struttura file](##flexible-mode-file-structure), non è stato modificato e non corrisponde alla versione SDK corrente.

Durante l’implementazione di Cloud Manager, il `httpd -t` viene eseguito anche il controllo della sintassi e gli eventuali errori vengono inclusi in Cloud Manager `Build Images step failure` log.

>[!NOTE]
>
Consulta la [Ricaricamento e convalida automatici](#automatic-loading) per un&#39;alternativa efficiente all&#39;esecuzione `validate.sh` dopo ogni modifica della configurazione.

### Fase 1 {#first-phase}

Se una direttiva non viene inserita nell&#39;elenco Consentiti, lo strumento registra un errore e restituisce un codice di uscita diverso da zero. Inoltre, esegue un&#39;ulteriore scansione di tutti i file con pattern `conf.dispatcher.d/enabled_farms/*.farm` e verifica che:

* Non esiste alcuna regola di filtro che utilizza allow tramite `/glob` (vedere [CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957)) per ulteriori dettagli.
* Nessuna funzione di amministrazione è esposta. Ad esempio, l’accesso a percorsi quali `/crx/de or /system/console`.

Lo strumento di convalida segnala solo l’utilizzo vietato delle direttive Apache che non sono state inserite nell&#39;elenco Consentiti. Non segnala problemi sintattici o semantici relativi alla configurazione di Apache, in quanto queste informazioni sono disponibili solo per i moduli Apache in un ambiente in esecuzione.

Di seguito sono illustrate le tecniche di risoluzione dei problemi per il debug degli errori di convalida comuni generati dallo strumento:

**Impossibile individuare un `conf.dispatcher.d` sottocartella nell’archivio**

L’archivio deve contenere le cartelle `conf.d` e `conf.dispatcher.d`. Nota: **non** utilizzare il
prefisso `etc/httpd` nell’archivio.

**Impossibile trovare una farm in`conf.dispatcher.d/enabled_farms`**

Le farm abilitate devono trovarsi nella sottocartella indicata.

**Il nome del file incluso (...) deve essere: ...**

Nella configurazione della farm sono disponibili due sezioni: **deve** includi un file specifico: `/renders` e `/allowedClients` nel `/cache` sezione. Tali sezioni devono essere visualizzate come segue:

```
/renders {
    $include "../renders/default_renders.any"
}
```

E:

```
/allowedClients {
    $include "../cache/default_invalidate.any"
}
```

**File incluso in una posizione sconosciuta: ...**

Nella configurazione della farm sono disponibili quattro sezioni in cui è possibile includere i file: `/clientheaders`, `filters`, `/rules` in `/cache` sezione e `/virtualhosts`. I file inclusi devono essere denominati come segue:

| Sezione | Includi nome file |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

In alternativa, è possibile includere **predefinito** versione di tali file, i cui nomi sono preceduti dalla parola `default_`ad esempio: `../filters/default_filters.any`.

**Includi istruzione in (...), all&#39;esterno di qualsiasi posizione nota: ...**

Oltre alle sei sezioni menzionate nei paragrafi precedenti, non è consentito utilizzare `$include` L&#39;istruzione seguente, ad esempio, genererebbe questo errore:

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**I client/rendering consentiti non sono inclusi da: ...**

Questo errore viene generato quando non si specifica un valore di inclusione per `/renders` e `/allowedClients` nel `/cache` sezione. Consulta la
**il nome del file incluso (...) deve essere: ...** per ulteriori informazioni.

**Il filtro non deve utilizzare il modello glob per consentire le richieste**

Non è sicuro consentire richieste con un `/glob` regola di stile, corrispondente alla riga di richiesta completa, ad esempio

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

Questa istruzione ha lo scopo di consentire le richieste di `css` ma consente anche di richiedere **qualsiasi** risorsa seguita dalla stringa di query `?a=.css`. È pertanto vietato utilizzare tali filtri (cfr. anche CVE-2016-0957).

**Il file incluso (...) non corrisponde ad alcun file noto**

Per impostazione predefinita, è possibile specificare due tipi di file nella configurazione dell’host virtuale Apache: riscritture e variabili.

| Tipo | Includi nome file |
|-----------|---------------------------------|
| Riscrittura | `conf.d/rewrites/rewrite.rules` |
| Variabili | `conf.d/variables/custom.vars` |

In modalità flessibile, è possibile includere anche altri file, purché si trovino in sottodirectory (a qualsiasi livello) di `conf.d` directory con il prefisso seguente.

| Includi prefisso della directory superiore del file |
|-------------------------------------|
| `conf.d/includes` |
| `conf.d/modsec` |
| `conf.d/rewrites` |

Ad esempio, puoi includere un file in una directory creata in `conf.d/includes` come segue:

```
Include conf.d/includes/mynewdirectory/myincludefile.conf
```

In alternativa, è possibile includere **predefinito** versione delle regole di riscrittura, il cui nome è `conf.d/rewrites/default_rewrite.rules`.
Nota: non esiste una versione predefinita dei file delle variabili.

**Rilevato layout di configurazione obsoleto, abilitazione della modalità di compatibilità**

Questo messaggio indica che la configurazione ha il layout versione 1 obsoleto, contenente una configurazione Apache completa e file con `ams_` prefissi. Anche se questa configurazione è ancora supportata per la compatibilità con le versioni precedenti, è necessario passare al nuovo layout.

La prima fase può anche essere **esegui separatamente**, anziché dall&#39;involucro `validate.sh` script.

Quando esegui su un artefatto Maven o `dispatcher/src` sottodirectory, segnala gli errori di convalida:

```
$ validator full -relaxed dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

In Windows, la convalida del Dispatcher distingue tra maiuscole e minuscole. Di conseguenza, potrebbe non essere possibile convalidare la configurazione se non si rispetta la combinazione di maiuscole e minuscole del percorso in cui si trova la configurazione, ad esempio:

```
bin\validator.exe -relaxed full src
Cloud manager validator 2.0.xx
2021/03/15 18:15:40 Dispatcher configuration validation failed:
  conf.dispatcher.d\available_farms\default.farm:15: parent directory outside server root: c:\k\a\aem-dispatcher-sdk-windows-symlinks-testing3\dispatcher\src
```

Evitare questo errore copiando e incollando il percorso da Esplora risorse e quindi al prompt dei comandi utilizzando un `cd` in tale percorso.

### Fase 2 {#second-phase}

Questa fase controlla la sintassi di Apache avviando Apache HTTPD in un contenitore docker. Docker deve essere installato localmente, ma non è necessario che l’AEM sia in esecuzione.

>[!NOTE]
>
Gli utenti di Windows devono utilizzare Windows 10 Professional o altre distribuzioni che supportano Docker. Questo requisito è un prerequisito per l’esecuzione e il debug di Dispatcher su un computer locale.
Per macOS e Windows, l’Adobe consiglia di utilizzare Docker Desktop.

Questa fase può anche essere eseguita in modo indipendente tramite `bin/docker_run.sh src/dispatcher host.docker.internal:4503 8080`.

Durante l’implementazione di Cloud Manager, il `httpd -t` Viene eseguito anche il controllo della sintassi e tutti gli errori vengono inclusi nel registro degli errori del passaggio Immagini build di Cloud Manager.

### Fase 3 {#third-phase}

Se si verifica un errore in questa fase, significa che Adobe ha modificato uno o più file immutabili. In questo caso, devi sostituire i file immutabili corrispondenti con la nuova versione distribuita in `src` dell’SDK. L’esempio di registro seguente illustra questo problema:

```
Phase 3: Immutability check
reading immutable file list from /etc/httpd/immutable.files.txt
(...)
checking existing 'conf.dispatcher.d/clientheaders/default_clientheaders.any' for changes
immutable file 'conf.dispatcher.d/clientheaders/default_clientheaders.any' has been changed:
--- /etc/httpd/conf.dispatcher.d/clientheaders/default_clientheaders.any
+++ /etc/httpd-actual/conf.dispatcher.d/clientheaders/default_clientheaders.any
@@ -40,4 +40,3 @@
"Sling-uploadmode"
"x-requested-with"
"If-Modified-Since"
-"Authorization"
** error: immutable file 'conf.dispatcher.d/clientheaders/default_clientheaders.any' has been changed!
  
```

Questa fase può anche essere eseguita in modo indipendente tramite `bin/docker_immutability_check.sh src/dispatcher`.

È possibile aggiornare i file immutabili locali eseguendo il comando `bin/update_maven.sh src/dispatcher` nella cartella di Dispatcher, dove `src/dispatcher` è la directory di configurazione del Dispatcher. Questo script aggiorna anche qualsiasi `pom.xml` nella directory principale in modo che vengano aggiornati anche i controlli di immutabilità Maven.

## Debug della configurazione di Apache e Dispatcher {#debugging-apache-and-dispatcher-configuration}

Puoi eseguire Apache Dispatcher localmente utilizzando `./bin/docker_run.sh src/dispatcher docker.for.mac.localhost:4503 8080`.

Come indicato in precedenza, Docker deve essere installato localmente e non è necessario che l’AEM sia in esecuzione. Gli utenti di Windows devono utilizzare Windows 10 Professional o altre distribuzioni che supportano Docker. Questo requisito è un prerequisito per l’esecuzione e il debug di Dispatcher su un computer locale.

La seguente strategia può essere utilizzata per aumentare l’output del registro per il modulo Dispatcher e visualizzare i risultati della `RewriteRule` valutazione in ambienti locali e cloud.

I livelli di registro per tali moduli sono definiti dalle variabili `DISP_LOG_LEVEL` e `REWRITE_LOG_LEVEL`. Possono essere impostati nel file `conf.d/variables/global.vars`. La parte pertinente è la seguente:

```
# Log level for the dispatcher
#
# Possible values are: error, warn, info, debug and trace1
# Default value: warn
#
# Define DISP_LOG_LEVEL warn
 
# Log level for mod_rewrite
#
# Possible values are: error, warn, info, debug and trace1 - trace8
# Default value: warn
#
# To debug your RewriteRules, it is recommended to raise your log
# level to trace2.
#
# More information can be found at:
# https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging
#
# Define REWRITE_LOG_LEVEL warn
```

Quando Dispatcher viene eseguito localmente, i registri vengono stampati direttamente nell’output del terminale. Nella maggior parte dei casi, si desidera che questi registri siano in DEBUG, operazione che può essere eseguita passando il livello di debug come parametro durante l’esecuzione di Docker. Esempio: `DISP_LOG_LEVEL=Debug ./bin/docker_run.sh src docker.for.mac.localhost:4503 8080`.

I registri per gli ambienti cloud vengono esposti tramite il servizio di registrazione disponibile in Cloud Manager.

>[!NOTE]
>
Per gli ambienti su AEM as a Cloud Service, debug è il livello di dettaglio massimo. Il livello del registro di traccia non è supportato, pertanto è consigliabile evitare di impostarlo quando si lavora in ambienti cloud.

### Ricaricamento e convalida automatici {#automatic-reloading}

>[!NOTE]
>
A causa di una limitazione del sistema operativo Windows, questa funzione è disponibile solo per gli utenti macOS e Linux®.

Invece di eseguire la convalida locale (`validate.sh`) e avvio del contenitore docker (`docker_run.sh`) ogni volta che la configurazione viene modificata, in alternativa è possibile eseguire il comando `docker_run_hot_reload.sh` script. Lo script controlla eventuali modifiche alla configurazione, la ricarica automaticamente ed esegue nuovamente la convalida. Utilizzando questa opzione, è possibile risparmiare molto tempo durante il debug.

È possibile eseguire lo script utilizzando il comando seguente: `./bin/docker_run_hot_reload.sh src/dispatcher host.docker.internal:4503 8080`

Le prime righe di output sono simili a quelle eseguite per `docker_run.sh`. Ad esempio:

```
~ bin/docker_run_hot_reload.sh src host.docker.internal:8081 8082
opt-in USE_SOURCES_DIRECTLY marker file detected
Running script /docker_entrypoint.d/10-check-environment.sh
Running script /docker_entrypoint.d/15-check-pod-name.sh
Running script /docker_entrypoint.d/20-create-docroots.sh
Running script /docker_entrypoint.d/30-wait-for-backend.sh
Waiting until host.docker.internal is available
host.docker.internal resolves to 192.168.65.2
Running script /docker_entrypoint.d/40-generate-allowed-clients.sh
Running script /docker_entrypoint.d/50-check-expiration.sh
Running script /docker_entrypoint.d/60-check-loglevel.sh
Running script /docker_entrypoint.d/70-check-forwarded-host-secret.sh
Running script /docker_entrypoint.d/80-frontend-domain.sh
Running script /docker_entrypoint.d/zzz-import-sdk-config.sh
WARN Mon Jul  4 09:53:54 UTC 2022: Pseudo symlink conf.d seems to point to a non-existing file!
INFO Mon Jul  4 09:53:55 UTC 2022: Copied customer configuration to /etc/httpd.
INFO Mon Jul  4 09:53:55 UTC 2022: Start testing
Cloud manager validator 2.0.43
2022/07/04 09:53:55 No issues found
INFO Mon Jul  4 09:53:55 UTC 2022: Testing with fresh base configuration files.
INFO Mon Jul  4 09:53:55 UTC 2022: Apache httpd informationServer version: Apache/2.4.54 (Unix)
```

## Diverse configurazioni del Dispatcher per ambiente {#different-dispatcher-configurations-per-environment}

Attualmente, a tutti gli ambienti AEM as a Cloud Service viene applicata la stessa configurazione di Dispatcher. Il runtime ha una variabile di ambiente `ENVIRONMENT_TYPE` che contiene la modalità di esecuzione corrente (sviluppo, stage o produzione) e un &quot;define&quot;. La &quot;definizione&quot; può essere `ENVIRONMENT_DEV`, `ENVIRONMENT_STAGE`, o `ENVIRONMENT_PROD`. Nella configurazione di Apache, la variabile può essere utilizzata direttamente in un’espressione. In alternativa, è possibile utilizzare la &quot;definizione&quot; per generare la logica:

```
# Simple usage of the environment variable
ServerName ${ENVIRONMENT_TYPE}.company.com
 
# When more logic is required
<IfDefine ENVIRONMENT_STAGE>
  # These statements are for stage
  Define VIRTUALHOST stage.example.com
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  # These statements are for production
  Define VIRTUALHOST prod.example.com
</IfDefine>
```

Nella configurazione di Dispatcher, è disponibile la stessa variabile di ambiente. Se è necessaria più logica, definisci le variabili come mostrato nell’esempio precedente e quindi utilizzale nella sezione di configurazione di Dispatcher:

```
/virtualhosts {
  { "${VIRTUALHOST}" }
}
```

In alternativa, puoi utilizzare le variabili di ambiente Cloud Manager nella configurazione httpd/dispatcher, anche se non i segreti dell’ambiente. Questo metodo è particolarmente importante se un programma ha più ambienti di sviluppo e alcuni di questi hanno valori diversi per la configurazione di httpd/dispatcher. Lo stesso ${VIRTUALHOST} La sintassi viene utilizzata come nell’esempio precedente, ma non le dichiarazioni Define nel file delle variabili di cui sopra. Leggi le [Documentazione di Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) per istruzioni sulla configurazione delle variabili di ambiente Cloud Manager.

Quando esegui il test della configurazione locale, puoi simulare diversi tipi di ambiente trasmettendo la variabile `DISP_RUN_MODE` al `docker_run.sh` script direttamente:

```
$ DISP_RUN_MODE=stage docker_run.sh src docker.for.mac.localhost:4503 8080
```

La modalità di esecuzione predefinita quando non viene passato un valore per DISP_RUN_MODE è &quot;dev&quot;.
Per un elenco completo delle opzioni e delle variabili disponibili, esegui lo script `docker_run.sh` senza argomenti.

## Visualizzazione della configurazione del Dispatcher utilizzata dal contenitore Docker {#viewing-dispatcher-configuration-in-use-by-docker-container}

Con configurazioni specifiche per l’ambiente, può essere difficile determinare l’aspetto della configurazione effettiva di Dispatcher. Dopo aver avviato il contenitore docker con `docker_run.sh`, può essere scaricato come segue:

* Determina l’ID del contenitore docker in uso:

```
$ docker ps
CONTAINER ID       IMAGE
d75fbd23b29        adobe/aem-ethos/dispatcher-publish:...
```

* Esegui la seguente riga di comando con tale ID contenitore:

```
$ docker exec d75fbd23b29 httpd-test
# Dispatcher configuration: (/etc/httpd/conf.dispatcher.d/dispatcher.any)
/farms {
  /publishfarm {
    /clientheaders {
...
```

## Migrazione dalla modalità legacy alla modalità flessibile {#migrating}

Con la versione 2021.7.0 di Cloud Manager, i nuovi programmi Cloud Manager generano strutture di progetto Maven con [Archetipo AEM 28](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) o superiore, che include il file **opt-in/USE_SOURCES_DIRECT**. Elimina le limitazioni precedenti del [modalità legacy](/help/implementing/dispatcher/validation-debug-legacy.md) intorno al numero e alle dimensioni dei file, consentendo all’SDK e al runtime di convalidare e distribuire la configurazione in modo migliorato. Se la configurazione del Dispatcher non dispone di questo file, si consiglia vivamente di eseguire la migrazione. Utilizza i seguenti passaggi per garantire una transizione sicura:

1. **Test locale.** Utilizzando il più recente SDK per strumenti di Dispatcher, aggiungi la cartella e il file `opt-in/USE_SOURCES_DIRECTLY`. Segui le istruzioni di &quot;convalida locale&quot; riportate in questo articolo per verificare che Dispatcher funzioni localmente.
1. **Test di sviluppo cloud:**
   * Esegue il commit del file `opt-in/USE_SOURCES_DIRECTLY` a un ramo Git distribuito dalla pipeline non di produzione in un ambiente di sviluppo Cloud.
   * Utilizza Cloud Manager per la distribuzione in un ambiente di sviluppo Cloud.
   * Effettua il test completo. È fondamentale verificare che la configurazione di Apache e Dispatcher si comporti come previsto prima di distribuire le modifiche agli ambienti superiori. Controlla tutti i comportamenti relativi alla configurazione personalizzata. Se ritieni che la configurazione di Dispatcher implementata non rifletta la configurazione personalizzata, invia una segnalazione all’assistenza clienti.

   >[!NOTE]
   >
   In modalità flessibile, è necessario utilizzare percorsi relativi invece di percorsi assoluti.
1. **Distribuisci in produzione:**
   * Esegue il commit del file `opt-in/USE_SOURCES_DIRECTLY` a un ramo Git distribuito dalla pipeline di produzione negli ambienti di staging e produzione Cloud.
   * Utilizza Cloud Manager per la distribuzione nell’ambiente di staging.
   * Effettua il test completo. È fondamentale verificare che la configurazione di Apache e Dispatcher si comporti come previsto prima di distribuire le modifiche agli ambienti superiori. Controlla tutti i comportamenti relativi alla configurazione personalizzata j. Se ritieni che la configurazione di Dispatcher implementata non rifletta la configurazione personalizzata, invia una segnalazione all’assistenza clienti.
   * Utilizza Cloud Manager per continuare la distribuzione in produzione.
