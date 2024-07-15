---
title: Convalida e debug con gli strumenti di Dispatcher
description: Scopri la convalida locale, il debug, la struttura del file in modalità flessibile e come migrare dalla modalità legacy alla modalità flessibile.
feature: Dispatcher
exl-id: 9e8cff20-f897-4901-8638-b1dbd85f44bf
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '3028'
ht-degree: 1%

---

# Convalida e debug con gli strumenti di Dispatcher {#Dispatcher-in-the-cloud}

## Introduzione {#apache-and-dispatcher-configuration-and-testing}

>[!NOTE]
>Per ulteriori informazioni su Dispatcher nel cloud e su come scaricare Dispatcher Tools, visita la pagina [Dispatcher nel cloud](/help/implementing/dispatcher/disp-overview.md). Se la configurazione di Dispatcher è in modalità legacy, consulta la [documentazione sulla modalità legacy](/help/implementing/dispatcher/validation-debug-legacy.md).

Le sezioni seguenti descrivono la struttura del file in modalità flessibile, la convalida locale, il debug e la migrazione dalla modalità precedente alla modalità flessibile.

In questo articolo si presuppone che la configurazione Dispatcher del progetto includa il file `opt-in/USE_SOURCES_DIRECTLY`. Questo file fa sì che l’SDK e il runtime convalidino e distribuiscano la configurazione in modo migliore rispetto alla modalità precedente, rimuovendo le limitazioni relative al numero e alle dimensioni dei file.

Se la configurazione di Dispatcher non include il file menzionato in precedenza, l&#39;Adobe consiglia di migrare dalla modalità legacy alla modalità flessibile come descritto nella sezione [Migrazione dalla modalità legacy alla modalità flessibile](#migrating).

## Struttura del file {#flexible-mode-file-structure}

La struttura della sottocartella Dispatcher del progetto è la seguente:

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

Puoi avere uno o più di questi file. Contengono `<VirtualHost>` voci che corrispondono ai nomi host e consentono ad Apache di gestire ogni traffico di dominio con regole diverse. I file vengono creati nella directory `available_vhosts` e abilitati con un collegamento simbolico nella directory `enabled_vhosts`. Dai file `.vhost` sono inclusi altri file, ad esempio riscritture e variabili.

>[!NOTE]
>
>In modalità flessibile, è necessario utilizzare percorsi relativi invece di percorsi assoluti.

Verificare che almeno un host virtuale sia sempre disponibile che corrisponda agli alias server `\*.local`, `localhost` e `127.0.0.1` necessari per l&#39;annullamento della validità di Dispatcher. Gli alias del server `*.adobeaemcloud.net` e `*.adobeaemcloud.com` sono necessari anche in almeno una configurazione vhost e sono necessari per i processi di Adobe interni.

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
> Quando si lavora con collegamenti simbolici in Windows, è necessario eseguire l&#39;operazione in un prompt dei comandi con privilegi elevati, nel Sottosistema Windows per Linux o avere il privilegio [Crea collegamenti simbolici](https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/create-symbolic-links) assegnato.

* `conf.d/rewrites/rewrite.rules`

Il file è incluso all&#39;interno dei file `.vhost`. Include un set di regole di riscrittura per `mod_rewrite`.

* `conf.d/variables/custom.vars`

Il file è incluso all&#39;interno dei file `.vhost`. Puoi aggiungere definizioni per le variabili Apache in questa posizione.

* `conf.d/variables/global.vars`

Il file è incluso nel file `dispatcher_vhost.conf`. Puoi modificare il Dispatcher e riscrivere il livello di registro in questo file.

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

Puoi avere uno o più di questi file, che contengono farm con nomi host corrispondenti e consentono al modulo Dispatcher di gestire ogni farm con regole diverse. I file vengono creati nella directory `available_farms` e abilitati con un collegamento simbolico nella directory `enabled_farms`. Dai file `.farm`, sono inclusi altri file come filtri, regole di cache e altri.

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
> Quando si lavora con collegamenti simbolici in Windows, è necessario eseguire l&#39;operazione in un prompt dei comandi con privilegi elevati, nel Sottosistema Windows per Linux o avere il privilegio [Crea collegamenti simbolici](https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/create-symbolic-links) assegnato.

* `conf.dispatcher.d/cache/rules.any`

Il file è incluso all&#39;interno dei file `.farm`. Specifica le preferenze di caching.

* `conf.dispatcher.d/clientheaders/clientheaders.any`

Il file è incluso all&#39;interno dei file `.farm`. Specifica le intestazioni di richiesta da inoltrare al backend.

* `conf.dispatcher.d/filters/filters.any`

Il file è incluso all&#39;interno dei file `.farm`. Ha una serie di regole che modificano il tipo di traffico da filtrare e non lo rendono al backend.

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

Il file è incluso all&#39;interno dei file `.farm`. Dispone di un elenco di nomi host o percorsi URI a cui deve corrispondere la corrispondenza glob. Questa corrispondenza determina il backend da utilizzare per distribuire una richiesta.

* `opt-in/USE_SOURCES_DIRECTLY`

Questo file consente una configurazione di Dispatcher più flessibile e rimuove le limitazioni precedenti relative al numero e alle dimensioni dei file. Inoltre, l’SDK e il runtime possono convalidare e distribuire la configurazione in modo migliorato.

I file di cui sopra fanno riferimento ai file di configurazione immutabili elencati di seguito. Le modifiche ai file immutabili non vengono elaborate da Dispatcher in ambienti Cloud.

**File di configurazione immutabili**

Questi file fanno parte del framework di base e applicano standard e best practice. I file sono considerati immutabili perché la loro modifica o eliminazione locale non ha alcun impatto sulla distribuzione, in quanto non vengono trasferiti nell’istanza Cloud.

Si consiglia che i file di cui sopra facciano riferimento ai file immutabili elencati di seguito, seguiti da eventuali istruzioni o sostituzioni aggiuntive. Quando la configurazione Dispatcher viene distribuita in un ambiente cloud, viene utilizzata la versione più recente dei file immutabili, indipendentemente dalla versione utilizzata nello sviluppo locale.

* `conf.d/available_vhosts/default.vhost`

Contiene un host virtuale di esempio. Per il tuo host virtuale, crea una copia di questo file, personalizzalo, passa a `conf.d/enabled_vhosts` e crea un collegamento simbolico alla tua copia personalizzata.
Non copiare il file default.vhost direttamente in `conf.d/enabled_vhosts`.

Verificare che sia sempre disponibile un host virtuale che corrisponda agli alias server `\*.local`, `localhost` e `127.0.0.1` necessari per l&#39;annullamento della validità di Dispatcher. Gli alias del server `*.adobeaemcloud.net` e `*.adobeaemcloud.com` sono necessari per i processi di Adobe interni.

* `conf.d/dispatcher_vhost.conf`

Parte del framework di base, utilizzato per illustrare come vengono inclusi gli host virtuali e le variabili globali.

* `conf.d/rewrites/default_rewrite.rules`

Le regole di riscrittura predefinite sono idonee per un progetto standard. Se è necessario eseguire la personalizzazione, modificare `rewrite.rules`. Nella personalizzazione, puoi comunque includere prima le regole predefinite, se soddisfano le tue esigenze.

* `conf.dispatcher.d/available_farms/default.farm`

Contiene una farm di Dispatcher di esempio. Per la tua farm, crea una copia di questo file, personalizzalo, passa a `conf.d/enabled_farms` e crea un collegamento simbolico alla tua copia personalizzata.

* `conf.dispatcher.d/cache/default_invalidate.any`

Parte del framework di base, viene generato all&#39;avvio. È **necessario** includere il file in ogni farm definita nella sezione `cache/allowedClients`.

* `conf.dispatcher.d/cache/default_rules.any`

Regole di cache predefinite adatte a un progetto standard. Se è necessario eseguire la personalizzazione, modificare `conf.dispatcher.d/cache/rules.any`. Nella personalizzazione, puoi comunque includere prima le regole predefinite, se soddisfano le tue esigenze.

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

Intestazioni di richiesta predefinite per l’inoltro al backend, adatte a un progetto standard. Se è necessario eseguire la personalizzazione, modificare `clientheaders.any`. Nella personalizzazione, puoi comunque includere prima le intestazioni di richiesta predefinite, se soddisfano le tue esigenze.

* `conf.dispatcher.d/dispatcher.any`

Parte del framework di base, utilizzato per illustrare come vengono incluse le farm di Dispatcher.

* `conf.dispatcher.d/filters/default_filters.any`

Filtri predefiniti adatti a un progetto standard. Se è necessario eseguire la personalizzazione, modificare `filters.any`. Nella personalizzazione, puoi comunque includere prima i filtri predefiniti, se soddisfano le tue esigenze.

* `conf.dispatcher.d/renders/default_renders.any`

Parte del framework di base, questo file viene generato all’avvio. È **necessario** includere il file in ogni farm definita nella sezione `renders`.

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

Globbing host predefinito adatto a un progetto standard. Se è necessario eseguire la personalizzazione, modificare `virtualhosts.any`. Nella personalizzazione non è consigliabile includere il globbing host predefinito, in quanto corrisponde a **ogni** richiesta in ingresso.

## Moduli Apache supportati {#apache-modules}

Consulta [Moduli Apache Supportati](/help/implementing/dispatcher/disp-overview.md#supported-directives).

## Convalida locale {#local-validation-flexible-mode}

>[!NOTE]
>
>Le sezioni seguenti includono comandi che utilizzano le versioni Mac o Linux® dell’SDK, ma l’SDK di Windows può essere utilizzato anche in modo simile.

Utilizza lo script `validate.sh` come illustrato di seguito:

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
2. Esegue il comando `httpd -t` per verificare se la sintassi è corretta in modo che Apache httpd possa avviarsi. In caso di esito positivo, la configurazione deve essere pronta per la distribuzione.
3. Verifica che il sottoinsieme dei file di configurazione dell&#39;SDK di Dispatcher, che devono essere immutabili come descritto nella [sezione struttura file](##flexible-mode-file-structure), non sia stato modificato e corrisponda alla versione SDK corrente.

Durante una distribuzione Cloud Manager, viene eseguito anche il controllo della sintassi `httpd -t` e gli eventuali errori vengono inclusi nel registro di Cloud Manager `Build Images step failure`.

>[!NOTE]
>
>Consulta la sezione [Ricaricamento e convalida automatici](#automatic-loading) per un&#39;alternativa efficiente all&#39;esecuzione di `validate.sh` dopo ogni modifica della configurazione.

### Fase 1 {#first-phase}

Se una direttiva non viene inserita nell&#39;elenco Consentiti, lo strumento registra un errore e restituisce un codice di uscita diverso da zero. Inoltre, esegue un&#39;ulteriore scansione di tutti i file con il pattern `conf.dispatcher.d/enabled_farms/*.farm` e verifica che:

* Non esiste alcuna regola di filtro che utilizza allow tramite `/glob` (vedi [CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957)) per ulteriori dettagli.
* Nessuna funzione di amministrazione è esposta. Ad esempio, l&#39;accesso a percorsi quali `/crx/de or /system/console`.

Lo strumento di convalida segnala solo l’utilizzo vietato delle direttive Apache che non sono state inserite nell&#39;elenco Consentiti. Non segnala problemi sintattici o semantici relativi alla configurazione di Apache, in quanto queste informazioni sono disponibili solo per i moduli Apache in un ambiente in esecuzione.

Di seguito sono illustrate le tecniche di risoluzione dei problemi per il debug degli errori di convalida comuni generati dallo strumento:

**Impossibile individuare una sottocartella `conf.dispatcher.d` nell&#39;archivio**

L’archivio deve contenere le cartelle `conf.d` e `conf.dispatcher.d`. Nota: **non** utilizzare il
prefisso `etc/httpd` nell’archivio.

**Impossibile trovare una farm in`conf.dispatcher.d/enabled_farms`**

Le farm abilitate devono trovarsi nella sottocartella indicata.

**Il nome del file incluso (...) deve essere: ...**

Nella configurazione della farm sono presenti due sezioni che **devono** includere
file specifico: `/renders` e `/allowedClients` nella sezione `/cache`. Tali
Le sezioni devono avere il seguente aspetto:

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

Nella configurazione della farm sono disponibili quattro sezioni in cui è possibile includere i propri file: `/clientheaders`, `filters`, `/rules` nella sezione `/cache` e `/virtualhosts`. I file inclusi devono essere denominati come segue:

| Sezione | Includi nome file |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

In alternativa, è possibile includere la versione **default** di tali file, i cui nomi sono preceduti dalla parola `default_`, ad esempio `../filters/default_filters.any`.

**Istruzione Include in (...), all&#39;esterno di qualsiasi percorso noto: ...**

A parte le sei sezioni menzionate nei paragrafi precedenti, non è consentito
per utilizzare l&#39;istruzione `$include`, ad esempio, l&#39;errore verrà generato nel modo seguente:

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**I client/rendering consentiti non sono inclusi da: ...**

Questo errore viene generato quando non si specifica un&#39;inclusione per `/renders` e `/allowedClients` nella sezione `/cache`. Consulta la
**il file incluso (...) deve essere denominato: ...** sezione per ulteriori informazioni.

**Il filtro non deve utilizzare il modello glob per consentire le richieste**

Non è sicuro consentire richieste con una regola di stile `/glob`, che viene confrontata con la riga di richiesta completa, ad esempio,

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

Questa istruzione consente richieste per `css` file, ma consente anche richieste a **qualsiasi** risorsa seguita dalla stringa di query `?a=.css`. È pertanto vietato utilizzare tali filtri (cfr. anche CVE-2016-0957).

**Il file incluso (...) non corrisponde ad alcun file noto**

Per impostazione predefinita, è possibile specificare due tipi di file nella configurazione dell’host virtuale Apache: riscritture e variabili.

| Tipo | Includi nome file |
|-----------|---------------------------------|
| Riscrittura | `conf.d/rewrites/rewrite.rules` |
| Variabili | `conf.d/variables/custom.vars` |

In modalità flessibile è possibile includere anche altri file, purché si trovino in sottodirectory (a qualsiasi livello) della directory `conf.d` con il prefisso seguente.

| Includi prefisso della directory superiore del file |
|-------------------------------------|
| `conf.d/includes` |
| `conf.d/modsec` |
| `conf.d/rewrites` |

Ad esempio, è possibile includere un file in una directory creata nella directory `conf.d/includes` nel modo seguente:

```
Include conf.d/includes/mynewdirectory/myincludefile.conf
```

In alternativa, è possibile includere la versione **default** delle regole di riscrittura, il cui nome è `conf.d/rewrites/default_rewrite.rules`.
Nota: non esiste una versione predefinita dei file delle variabili.

**Rilevato layout di configurazione obsoleto, abilitazione della modalità di compatibilità**

Questo messaggio indica che la configurazione ha il layout versione 1 obsoleto, contenente un elemento
Configurazione Apache e file con prefissi `ams_`. Questa configurazione è ancora supportata per le versioni precedenti
è necessario passare al nuovo layout.

Anche la prima fase può essere **eseguita separatamente**, anziché dallo script wrapper `validate.sh`.

Quando viene eseguito in base all&#39;artefatto Maven o alla sottodirectory `dispatcher/src`, vengono segnalati errori di convalida:

```
$ validator full -relaxed dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

In Windows, la convalida di Dispatcher distingue tra maiuscole e minuscole. Di conseguenza, potrebbe non essere possibile convalidare la configurazione se non si rispetta la combinazione di maiuscole e minuscole del percorso in cui si trova la configurazione, ad esempio:

```
bin\validator.exe -relaxed full src
Cloud manager validator 2.0.xx
2021/03/15 18:15:40 Dispatcher configuration validation failed:
  conf.dispatcher.d\available_farms\default.farm:15: parent directory outside server root: c:\k\a\aem-dispatcher-sdk-windows-symlinks-testing3\dispatcher\src
```

Evitare questo errore copiando e incollando il percorso da Esplora risorse e quindi al prompt dei comandi utilizzando un comando `cd` nel percorso.

### Fase 2 {#second-phase}

Questa fase controlla la sintassi di Apache avviando Apache HTTPD in un contenitore docker. Docker deve essere installato localmente, ma non è necessario che l’AEM sia in esecuzione.

>[!NOTE]
>
>Gli utenti di Windows devono utilizzare Windows 10 Professional o altre distribuzioni che supportano Docker. Questo requisito è un prerequisito per l&#39;esecuzione e il debug di Dispatcher in un computer locale.
>Per macOS e Windows, l’Adobe consiglia di utilizzare Docker Desktop.

Questa fase può anche essere eseguita in modo indipendente tramite `bin/docker_run.sh src/dispatcher host.docker.internal:4503 8080`.

Durante una distribuzione Cloud Manager, viene eseguito anche il controllo della sintassi `httpd -t` e tutti gli errori vengono inclusi nel registro errori del passaggio Immagini build di Cloud Manager.

### Fase 3 {#third-phase}

Se si verifica un errore in questa fase, significa che Adobe ha modificato uno o più file immutabili. In tal caso, è necessario sostituire i file immutabili corrispondenti con la nuova versione distribuita nella directory `src` dell&#39;SDK. L’esempio di registro seguente illustra questo problema:

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

I file immutabili locali possono essere aggiornati eseguendo lo script `bin/update_maven.sh src/dispatcher` nella cartella Dispatcher, dove `src/dispatcher` è la directory di configurazione di Dispatcher. Questo script aggiorna anche qualsiasi file `pom.xml` nella directory padre in modo che anche i controlli di immutabilità Maven vengano aggiornati.

## Debug della configurazione di Apache e Dispatcher {#debugging-apache-and-dispatcher-configuration}

È possibile eseguire Apache Dispatcher localmente utilizzando `./bin/docker_run.sh src/dispatcher docker.for.mac.localhost:4503 8080`.

Come indicato in precedenza, Docker deve essere installato localmente e non è necessario che l’AEM sia in esecuzione. Gli utenti di Windows devono utilizzare Windows 10 Professional o altre distribuzioni che supportano Docker. Questo requisito è un prerequisito per l&#39;esecuzione e il debug di Dispatcher in un computer locale.

La strategia seguente può essere utilizzata per aumentare l&#39;output del registro per il modulo Dispatcher e visualizzare i risultati della valutazione `RewriteRule` sia negli ambienti locali che in quelli cloud.

I livelli di registro per questi moduli sono definiti dalle variabili `DISP_LOG_LEVEL` e `REWRITE_LOG_LEVEL`. È possibile impostarli nel file `conf.d/variables/global.vars`. La parte pertinente è la seguente:

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

Se Dispatcher viene eseguito localmente, i registri vengono stampati direttamente nell&#39;output del terminale. Nella maggior parte dei casi, si desidera che questi registri siano in DEBUG, operazione che può essere eseguita passando il livello di debug come parametro durante l’esecuzione di Docker. Ad esempio: `DISP_LOG_LEVEL=Debug ./bin/docker_run.sh src docker.for.mac.localhost:4503 8080`.

I registri per gli ambienti cloud vengono esposti tramite il servizio di registrazione disponibile in Cloud Manager.

>[!NOTE]
>
>Per gli ambienti su AEM as a Cloud Service, debug è il livello di dettaglio massimo. Il livello del registro di traccia non è supportato, pertanto è consigliabile evitare di impostarlo quando si lavora in ambienti cloud.

### Ricaricamento e convalida automatici {#automatic-reloading}

>[!NOTE]
>
>A causa di una limitazione del sistema operativo Windows, questa funzione è disponibile solo per gli utenti macOS e Linux®.

Anziché eseguire la convalida locale (`validate.sh`) e avviare il contenitore docker (`docker_run.sh`) ogni volta che la configurazione viene modificata, è possibile eseguire in alternativa lo script `docker_run_hot_reload.sh`. Lo script controlla eventuali modifiche alla configurazione, la ricarica automaticamente ed esegue nuovamente la convalida. Utilizzando questa opzione, è possibile risparmiare molto tempo durante il debug.

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

### Inserimento di variabili di ambiente personalizzate {#environment-variables}

È possibile utilizzare le variabili di ambiente personalizzate con l’SDK del dispatcher impostandole in un file separato e facendo riferimento a esse nella variabile di ambiente `ENV_FILE` prima di avviare il dispatcher locale.

Un file con variabili di ambiente personalizzate sarà simile al seguente:

```
COMMERCE_ENDPOINT=commerce-host
AEM_HTTP_PROXY_HOST=host.docker.internal
AEM_HTTP_PROXY_PORT=8000
```

Può essere utilizzato nell’SDK del dispatcher locale con i seguenti comandi:

```
export ENV_FILE=custom.env
./bin/docker_run.sh src/dispatcher docker.for.mac.localhost:4503 8080
```

## Diverse configurazioni di Dispatcher per ambiente {#different-dispatcher-configurations-per-environment}

Attualmente, la stessa configurazione di Dispatcher viene applicata a tutti gli ambienti su AEM as a Cloud Service. Il runtime include una variabile di ambiente `ENVIRONMENT_TYPE` che contiene la modalità di esecuzione corrente (sviluppo, stage o produzione) e un valore &quot;define&quot;. &quot;define&quot; può essere `ENVIRONMENT_DEV`, `ENVIRONMENT_STAGE` o `ENVIRONMENT_PROD`. Nella configurazione di Apache, la variabile può essere utilizzata direttamente in un’espressione. In alternativa, è possibile utilizzare la &quot;definizione&quot; per generare la logica:

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

In alternativa, puoi utilizzare le variabili di ambiente Cloud Manager nella configurazione httpd/dispatcher, ma non i segreti dell’ambiente. Questo metodo è particolarmente importante se un programma ha più ambienti di sviluppo e alcuni di questi hanno valori diversi per la configurazione di httpd/dispatcher. La stessa sintassi ${VIRTUALHOST} verrebbe utilizzata come nell&#39;esempio precedente, ma non verrebbero utilizzate le dichiarazioni Define nel file di variabili precedente. Per istruzioni sulla configurazione delle variabili dell&#39;ambiente Cloud Manager, leggere la [documentazione di Cloud Manager](/help/implementing/cloud-manager/environment-variables.md).

Quando si esegue il test della configurazione in locale, è possibile simulare diversi tipi di ambiente passando la variabile `DISP_RUN_MODE` direttamente allo script `docker_run.sh`:

```
$ DISP_RUN_MODE=stage docker_run.sh src docker.for.mac.localhost:4503 8080
```

La modalità di esecuzione predefinita quando non viene passato un valore per DISP_RUN_MODE è &quot;dev&quot;.
Per un elenco completo delle opzioni e delle variabili disponibili, eseguire lo script `docker_run.sh` senza argomenti.

## Visualizzazione della configurazione del Dispatcher utilizzata dal contenitore Docker {#viewing-dispatcher-configuration-in-use-by-docker-container}

Con configurazioni specifiche per l’ambiente, può essere difficile determinare l’aspetto della configurazione Dispatcher effettiva. Dopo aver avviato il contenitore docker con `docker_run.sh`, è possibile scaricarlo come segue:

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

Con la versione di Cloud Manager 2021.7.0, i nuovi programmi Cloud Manager generano strutture di progetto Maven con [archetipo AEM 28](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) o versione successiva, che include il file **opt-in/USE_SOURCES_DIRECT**. Elimina le limitazioni precedenti della [modalità legacy](/help/implementing/dispatcher/validation-debug-legacy.md) relative al numero e alla dimensione dei file, consentendo inoltre all&#39;SDK e al runtime di convalidare e distribuire la configurazione in modo migliorato. Se la configurazione del Dispatcher non dispone di questo file, si consiglia vivamente di eseguire la migrazione. Utilizza i seguenti passaggi per garantire una transizione sicura:

1. **Test locale.** Utilizzando l&#39;SDK degli strumenti di Dispatcher più recente, aggiungere la cartella e il file `opt-in/USE_SOURCES_DIRECTLY`. Segui le istruzioni di &quot;convalida locale&quot; in questo articolo per verificare che Dispatcher funzioni localmente.
1. **Test di sviluppo cloud:**
   * Eseguire il commit del file `opt-in/USE_SOURCES_DIRECTLY` in un ramo Git distribuito dalla pipeline non di produzione in un ambiente di sviluppo Cloud.
   * Utilizza Cloud Manager per eseguire la distribuzione in un ambiente di sviluppo Cloud.
   * Effettua il test completo. È fondamentale verificare che la configurazione di Apache e Dispatcher si comporti come previsto prima di distribuire le modifiche agli ambienti superiori. Controlla tutti i comportamenti relativi alla configurazione personalizzata. Se ritieni che la configurazione Dispatcher implementata non rifletta la configurazione personalizzata, invia una segnalazione all’assistenza clienti.

   >[!NOTE]
   >
   >In modalità flessibile, è necessario utilizzare percorsi relativi invece di percorsi assoluti.
1. **Distribuisci in produzione:**
   * Eseguire il commit del file `opt-in/USE_SOURCES_DIRECTLY` in un ramo Git distribuito dalla pipeline di produzione negli ambienti di staging e produzione Cloud.
   * Utilizza Cloud Manager per eseguire la distribuzione nell’ambiente di staging.
   * Effettua il test completo. È fondamentale verificare che la configurazione di Apache e Dispatcher si comporti come previsto prima di distribuire le modifiche agli ambienti superiori. Controlla tutti i comportamenti relativi alla configurazione personalizzata j. Se ritieni che la configurazione Dispatcher implementata non rifletta la configurazione personalizzata, invia una segnalazione all’assistenza clienti.
   * Utilizza Cloud Manager per continuare la distribuzione in produzione.
