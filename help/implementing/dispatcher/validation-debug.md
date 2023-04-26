---
title: Convalida e debug con gli strumenti di Dispatcher
description: Convalida e debug con gli strumenti di Dispatcher
feature: Dispatcher
exl-id: 9e8cff20-f897-4901-8638-b1dbd85f44bf
source-git-commit: a56b0ed1efff7b8d04e65921ee9dd25ae7030dbd
workflow-type: tm+mt
source-wordcount: '2865'
ht-degree: 1%

---

# Convalida e debug con gli strumenti di Dispatcher {#Dispatcher-in-the-cloud}

## Introduzione {#apache-and-dispatcher-configuration-and-testing}

>[!NOTE]
>Per ulteriori informazioni su Dispatcher nel cloud e su come scaricare gli strumenti di Dispatcher, consulta la sezione [Dispatcher nel cloud](/help/implementing/dispatcher/disp-overview.md) pagina. Se la configurazione del dispatcher è in modalità legacy, consulta [documentazione sulla modalità legacy](/help/implementing/dispatcher/validation-debug-legacy.md).

Le sezioni seguenti descrivono la struttura del file in modalità flessibile, la convalida locale, il debug e la migrazione dalla modalità legacy alla modalità flessibile.

Questo articolo presuppone che la configurazione del dispatcher del tuo progetto includa il file `opt-in/USE_SOURCES_DIRECTLY`, che consente all’SDK e al runtime di convalidare e distribuire la configurazione in modo migliore rispetto alla modalità legacy, rimuovendo le limitazioni relative al numero e alle dimensioni dei file.

Di conseguenza, se la configurazione del dispatcher non include il file di cui sopra, è **altamente raccomandato** per passare dalla modalità legacy alla modalità flessibile, come descritto in [Migrazione dalla modalità legacy alla modalità flessibile](#migrating) sezione .

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

Di seguito è riportata una spiegazione dei file importanti che possono essere modificati:

**File personalizzabili**

I file seguenti sono personalizzabili e verranno trasferiti all’istanza Cloud durante la distribuzione:

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

Puoi avere uno o più di questi file. Contengono `<VirtualHost>` voci che corrispondono ai nomi host e consentono ad Apache di gestire il traffico di ogni dominio con regole diverse. I file vengono creati nella `available_vhosts` e attivato con un collegamento simbolico nel `enabled_vhosts` directory. Da `.vhost` verranno inclusi file, altri file come riscritture e variabili.

>[!NOTE]
>
>In modalità flessibile è necessario utilizzare percorsi relativi invece di percorsi assoluti.

Assicurati che sia sempre disponibile almeno un host virtuale corrispondente a ServerAlias `\*.local`, `localhost` e `127.0.0.1` necessari per l’invalidazione del dispatcher. Alias del server `*.adobeaemcloud.net` e `*.adobeaemcloud.com` sono inoltre necessarie in almeno una configurazione vhost e sono necessarie per i processi di Adobe interni.

Se vuoi far corrispondere l&#39;host esatto perché hai più file vhost puoi seguire l&#39;esempio seguente:

```
<VirtualHost *:80>
	ServerName	"example.com"
	# Put names of which domains are used for your published site/content here
	ServerAlias	 "*example.com" "\*.local" "localhost" "127.0.0.1" "*.adobeaemcloud.net" "*.adobeaemcloud.com"
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

* `conf.d/rewrites/rewrite.rules`

Questo file è incluso all&#39;interno del `.vhost` file. Ha una serie di regole di riscrittura per `mod_rewrite`.

* `conf.d/variables/custom.vars`

Questo file è incluso all&#39;interno del `.vhost` file. Puoi aggiungere definizioni per le variabili Apache in questa posizione.

* `conf.d/variables/global.vars`

Questo file è incluso dall&#39;interno del `dispatcher_vhost.conf` file. Puoi modificare il tuo livello di Dispatcher e riscrivere il livello di registro in questo file.

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

Puoi avere uno o più di questi file, che contengono farm che corrispondono ai nomi host e consentono al modulo Dispatcher di gestire ogni farm con regole diverse. I file vengono creati nella `available_farms` e attivato con un collegamento simbolico nel `enabled_farms` directory. Da `.farm` verranno inclusi file, altri file come filtri, regole di cache e altri.

* `conf.dispatcher.d/cache/rules.any`

Questo file è incluso all&#39;interno del `.farm` file. Specifica le preferenze di memorizzazione in cache.

* `conf.dispatcher.d/clientheaders/clientheaders.any`

Questo file è incluso all&#39;interno del `.farm` file. Specifica quali intestazioni di richiesta devono essere inoltrate al backend.

* `conf.dispatcher.d/filters/filters.any`

Questo file è incluso all&#39;interno del `.farm` file. Ha un set di regole che cambiano il traffico da filtrare e non arrivare al backend.

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

Questo file è incluso all&#39;interno del `.farm` file. Contiene un elenco di nomi host o percorsi URI che devono essere associati dalla corrispondenza glob. Questo determina quale backend utilizzare per elaborare una richiesta.

* `opt-in/USE_SOURCES_DIRECTLY`

Questo file consente una configurazione più flessibile del dispatcher e rimuove le limitazioni precedenti relative al numero e alle dimensioni dei file. Inoltre, fa sì che l&#39;SDK e il runtime convalidino e distribuiscano la configurazione in modo migliore.

I file di cui sopra fanno riferimento ai file di configurazione immutabili elencati di seguito. Le modifiche ai file immutabili non verranno elaborate dai Dispatcher negli ambienti Cloud.

**File di configurazione immutabili**

Questi file fanno parte del framework di base e applicano gli standard e le best practice. I file sono considerati immutabili perché modificarli o eliminarli localmente non avranno alcun impatto sulla distribuzione, in quanto non verranno trasferiti all’istanza Cloud.

Si consiglia che i file di cui sopra facciano riferimento ai file immutabili elencati di seguito, seguiti da eventuali istruzioni o sostituzioni aggiuntive. Quando la configurazione di Dispatcher viene distribuita in un ambiente cloud, verrà utilizzata la versione più recente dei file immutabili, indipendentemente dalla versione utilizzata nello sviluppo locale.

* `conf.d/available_vhosts/default.vhost`

Contiene un esempio di host virtuale. Per il tuo host virtuale, crea una copia di questo file, personalizzalo, vai a `conf.d/enabled_vhosts` e crea un collegamento simbolico alla copia personalizzata.
Non copiare il file default.vhost direttamente in `conf.d/enabled_vhosts`.

Assicurati che un host virtuale sia sempre disponibile e che corrisponda a ServerAlias `\*.local`, `localhost` e `127.0.0.1` necessari per l’invalidazione del dispatcher. Alias del server `*.adobeaemcloud.net` e `*.adobeaemcloud.com` sono necessarie per i processi di Adobe interni.

* `conf.d/dispatcher_vhost.conf`

Parte del framework di base, utilizzato per illustrare il modo in cui vengono inclusi gli host virtuali e le variabili globali.

* `conf.d/rewrites/default_rewrite.rules`

Regole di riscrittura predefinite adatte a un progetto standard. Se hai bisogno di personalizzazione, modifica `rewrite.rules`. Nella personalizzazione, puoi comunque includere prima le regole predefinite, se sono adatte alle tue esigenze.

* `conf.dispatcher.d/available_farms/default.farm`

Contiene un esempio di farm del Dispatcher. Per la tua farm, crea una copia di questo file, personalizzalo, vai a `conf.d/enabled_farms` e crea un collegamento simbolico alla copia personalizzata.

* `conf.dispatcher.d/cache/default_invalidate.any`

Parte del framework di base, viene generato all&#39;avvio. Lei è **obbligatorio** per includere questo file in ogni farm definita, nella `cache/allowedClients` sezione .

* `conf.dispatcher.d/cache/default_rules.any`

Regole di cache predefinite adatte a un progetto standard. Se hai bisogno di personalizzazione, modifica `conf.dispatcher.d/cache/rules.any`. Nella personalizzazione, puoi comunque includere prima le regole predefinite, se sono adatte alle tue esigenze.

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

Intestazioni di richiesta predefinite da inoltrare al backend, adatte a un progetto standard. Se hai bisogno di personalizzazione, modifica `clientheaders.any`. Nella personalizzazione, puoi comunque includere prima le intestazioni di richiesta predefinite, se sono adatte alle tue esigenze.

* `conf.dispatcher.d/dispatcher.any`

Parte del framework di base, utilizzato per illustrare come sono incluse le farm del Dispatcher.

* `conf.dispatcher.d/filters/default_filters.any`

Filtri predefiniti adatti a un progetto standard. Se hai bisogno di personalizzazione, modifica `filters.any`. Nella personalizzazione, puoi comunque includere prima i filtri predefiniti, se soddisfano le tue esigenze.

* `conf.dispatcher.d/renders/default_renders.any`

Parte del framework di base, questo file viene generato all&#39;avvio. Lei è **obbligatorio** per includere questo file in ogni farm definita, nella `renders` sezione .

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

Globbing host predefinito adatto per un progetto standard. Se hai bisogno di personalizzazione, modifica `virtualhosts.any`. Nella personalizzazione, non è necessario includere il globbing host predefinito, in quanto corrisponde a **ogni** richiesta in arrivo.

## Moduli Apache supportati {#apache-modules}

Vedi [Moduli Apache supportati](/help/implementing/dispatcher/disp-overview.md#supported-directives).

## Convalida locale {#local-validation-flexible-mode}

>[!NOTE]
>
>Le sezioni seguenti includono comandi che utilizzano le versioni Mac o Linux dell&#39;SDK, ma l&#39;SDK di Windows può essere utilizzato anche in modo simile.

Utilizza la `validate.sh` script come mostrato di seguito:

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
2. Esegue il `httpd -t` per verificare se la sintassi è corretta in modo che apache httpd possa avviarsi. In caso di esito positivo, la configurazione dovrebbe essere pronta per la distribuzione.
3. Controlla che il sottoinsieme dei file di configurazione dell’SDK di Dispatcher, destinati ad essere immutabili come descritto in [Sezione struttura file](##flexible-mode-file-structure), non è stato modificato e corrisponde alla versione SDK corrente.

Durante l’implementazione di Cloud Manager, la variabile `httpd -t` verrà eseguito anche il controllo della sintassi e eventuali errori verranno inclusi in Cloud Manager `Build Images step failure` registro.

>[!NOTE]
>
>Consulta la sezione [Ricaricamento e convalida automatici](#automatic-loading) sezione per un&#39;alternativa efficiente all&#39;esecuzione `validate.sh` dopo ogni modifica della configurazione.

### Fase 1 {#first-phase}

Se una direttiva non viene inserita nell&#39;elenco Consentiti, lo strumento registra un errore e restituisce un codice di uscita diverso da zero. Inoltre, scansiona ulteriormente tutti i file con pattern `conf.dispatcher.d/enabled_farms/*.farm` e controlla che:

* Non esiste una regola di filtro che utilizza l&#39;autorizzazione tramite `/glob` (vedi [CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957) per ulteriori dettagli.
* Non viene visualizzata alcuna funzione di amministrazione. Ad esempio, l’accesso a percorsi come `/crx/de or /system/console`.

Lo strumento di convalida segnala solo l’uso non consentito di direttive Apache che non sono state inserite nell&#39;elenco Consentiti. Non segnala problemi sintattici o semantici con la configurazione Apache, in quanto queste informazioni sono disponibili solo per i moduli Apache in un ambiente in esecuzione.

Di seguito sono riportate le tecniche di risoluzione dei problemi per il debug di errori di convalida comuni generati dallo strumento:

**impossibile individuare un `conf.dispatcher.d` sottocartella nell’archivio**

L’archivio deve contenere le cartelle `conf.d` e `conf.dispatcher.d`. Nota: **non** utilizzare il
prefisso `etc/httpd` nell’archivio.

**impossibile trovare aziende agricole in`conf.dispatcher.d/enabled_farms`**

Le farm abilitate devono trovarsi nella sottocartella indicata.

**il file incluso (..) deve essere denominato: ...**

Nella configurazione della farm sono disponibili due sezioni: **deve** includere un file specifico: `/renders` e `/allowedClients` in `/cache` sezione . Tali sezioni devono avere il seguente aspetto:

```
/renders {
    $include "../renders/default_renders.any"
}
```

e:

```
/allowedClients {
    $include "../cache/default_invalidate.any"
}
```

**file incluso in posizione sconosciuta: ...**

Nella configurazione della farm sono presenti quattro sezioni in cui puoi includere i tuoi file: `/clientheaders`, `filters`, `/rules` in `/cache` sezione e `/virtualhosts`. I file inclusi devono essere denominati come segue:

| Sezione | Nome file di inclusione |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

In alternativa, puoi includere il **default** versione di tali file, i cui nomi sono preceduti dalla parola `default_`ad esempio, `../filters/default_filters.any`.

**include l&#39;istruzione in (...), al di fuori di qualsiasi posizione nota: ...**

Oltre alle sei sezioni menzionate nei paragrafi precedenti, non è consentito utilizzare il `$include` ad esempio, il seguente genera questo errore:

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**i client/rendering consentiti non sono inclusi in: ...**

Questo errore viene generato quando non si specifica un&#39;inclusione per `/renders` e `/allowedClients` in `/cache` sezione . Consulta la sezione
**il file incluso (..) deve essere denominato: ...** per ulteriori informazioni.

**Il filtro non deve utilizzare il pattern glob per consentire le richieste**

Non è sicuro consentire le richieste con un `/glob` regola di stile, che viene confrontata con la riga di richiesta completa, ad esempio,

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

Questa istruzione ha lo scopo di consentire le richieste di `css` , ma consente anche alle richieste di **qualsiasi** risorsa seguita dalla stringa query `?a=.css`. È pertanto vietato utilizzare tali filtri (cfr. anche CVE-2016-0957).

**il file incluso (...) non corrisponde ad alcun file noto**

Per impostazione predefinita, è possibile specificare due tipi di file nella configurazione dell&#39;host virtuale Apache come include: riscrive e variabili.

| Tipo | Nome file di inclusione |
|-----------|---------------------------------|
| Riscrittura | `conf.d/rewrites/rewrite.rules` |
| Variabili | `conf.d/variables/custom.vars` |

In modalità flessibile è possibile includere anche altri file, purché si trovino in sottodirectory (a qualsiasi livello) di `conf.d` directory con il prefisso seguente.

| Includi prefisso della directory superiore del file |
|-------------------------------------|
| `conf.d/includes` |
| `conf.d/modsec` |
| `conf.d/rewrites` |

Ad esempio, puoi includere un file in una directory appena creata in `conf.d/includes` come segue:

```
Include conf.d/includes/mynewdirectory/myincludefile.conf
```

In alternativa, puoi includere il **default** versione delle regole di riscrittura il cui nome è `conf.d/rewrites/default_rewrite.rules`.
Tieni presente che non esiste una versione predefinita dei file delle variabili.

**Rilevato layout di configurazione obsoleto, abilitazione della modalità di compatibilità**

Questo messaggio indica che la configurazione dispone di un layout 1 obsoleto, contenente una configurazione Apache completa e file con `ams_` prefissi. Anche se questo è ancora supportato per la compatibilità con le versioni precedenti, dovresti passare al nuovo layout.

Si prega di notare che la prima fase può anche essere **eseguire separatamente**, anziché dal wrapper `validate.sh` script.

Quando viene eseguito contro il tuo artefatto Maven o il tuo `dispatcher/src` la sottodirectory segnalerà gli errori di convalida:

```
$ validator full -relaxed dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

In Windows, la convalida del dispatcher fa distinzione tra maiuscole e minuscole. Di conseguenza, la convalida della configurazione può non riuscire se non si rispetta la capitalizzazione del percorso in cui si trova la configurazione, ad esempio:

```
bin\validator.exe -relaxed full src
Cloud manager validator 2.0.xx
2021/03/15 18:15:40 Dispatcher configuration validation failed:
  conf.dispatcher.d\available_farms\default.farm:15: parent directory outside server root: c:\k\a\aem-dispatcher-sdk-windows-symlinks-testing3\dispatcher\src
```

Evitare questo errore copiando e incollando il percorso da Esplora risorse e quindi dal prompt dei comandi utilizzando un `cd` in quel percorso.

### Fase 2 {#second-phase}

Questa fase controlla la sintassi apache avviando Apache HTTPD in un contenitore docker. Il Docker deve essere installato localmente, ma non è necessario eseguire AEM.

>[!NOTE]
>
>Gli utenti Windows devono utilizzare Windows 10 Professional o altre distribuzioni che supportano Docker. Questo è un prerequisito per l’esecuzione e il debug di Dispatcher su un computer locale.
>Per Windows e macOS si consiglia di utilizzare Docker Desktop.

Questa fase può anche essere eseguita in modo indipendente `bin/docker_run.sh src/dispatcher host.docker.internal:4503 8080`.

Durante l’implementazione di Cloud Manager, la variabile `httpd -t` viene inoltre eseguito il controllo della sintassi e eventuali errori verranno inclusi nel registro degli errori del passaggio Build Images di Cloud Manager.

### Fase 3 {#third-phase}

Se si verifica un errore in questa fase, significa che Adobe ha modificato uno o più file immutabili e devi sostituire i corrispondenti file immutabili con la nuova versione consegnata nella `src` della directory dell&#39;SDK. Il seguente esempio di log illustra questo problema:

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

Questa fase può anche essere eseguita in modo indipendente `bin/docker_immutability_check.sh src/dispatcher`.

I file immutabili locali possono essere aggiornati eseguendo il `bin/update_maven.sh src/dispatcher` nella cartella del dispatcher, dove `src/dispatcher` è la directory di configurazione del dispatcher. Questo aggiornerà anche qualsiasi file pom.xml nella directory principale in modo che vengano aggiornati anche i controlli di immutabilità maven.

## Debug della configurazione di Apache e Dispatcher {#debugging-apache-and-dispatcher-configuration}

Tieni presente che puoi eseguire apache dispatcher localmente utilizzando `./bin/docker_run.sh src/dispatcher docker.for.mac.localhost:4503 8080`.

Come indicato in precedenza, Docker deve essere installato localmente e non è necessario che AEM sia in esecuzione. Gli utenti Windows devono utilizzare Windows 10 Professional o altre distribuzioni che supportano Docker. Questo è un prerequisito per l’esecuzione e il debug di Dispatcher su un computer locale.

La seguente strategia può essere utilizzata per aumentare l’output di log per il modulo Dispatcher e visualizzare i risultati del `RewriteRule` in ambienti sia locali che cloud.

I livelli di registro per tali moduli sono definiti dalle variabili `DISP_LOG_LEVEL` e `REWRITE_LOG_LEVEL`. Possono essere impostati nel file `conf.d/variables/global.vars`. La sua parte pertinente è la seguente:

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

Quando si esegue Dispatcher localmente, i registri vengono stampati direttamente nell’output del terminale. Nella maggior parte dei casi, si desidera che questi log siano in DEBUG, che può essere fatto passando il livello Debug come parametro durante l&#39;esecuzione di Docker. Esempio: `DISP_LOG_LEVEL=Debug ./bin/docker_run.sh src docker.for.mac.localhost:4503 8080`.

I registri per gli ambienti cloud sono esposti tramite il servizio di registrazione disponibile in Cloud Manager.

>[!NOTE]
>
>Per AEM ambienti as a Cloud Service, il debug è il livello massimo di verbosità. Il livello di registro di traccia non è supportato, pertanto evita di impostarlo quando si lavora in ambienti cloud.

### Ricaricamento e convalida automatici {#automatic-reloading}

>[!NOTE]
>
>A causa di una limitazione del sistema operativo Windows, questa funzione è disponibile solo per gli utenti macOS e Linux.

Invece di eseguire la convalida locale (`validate.sh`) e avvio del contenitore docker (`docker_run.sh`) ogni volta che la configurazione viene modificata, puoi in alternativa eseguire il `docker_run_hot_reload.sh` script.  Lo script controlla eventuali modifiche alla configurazione e la ricaricherà automaticamente ed eseguirà nuovamente la convalida. Utilizzando questa opzione è possibile risparmiare molto tempo durante il debug.

È possibile eseguire lo script utilizzando il seguente comando: `./bin/docker_run_hot_reload.sh src/dispatcher host.docker.internal:4503 8080`

Tieni presente che le prime righe di output avranno un aspetto simile a quello per cui verrebbe eseguito `docker_run.sh`ad esempio:

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

Attualmente, la stessa configurazione del Dispatcher viene applicata a tutti gli ambienti AEM as a Cloud Service. Il runtime avrà una variabile di ambiente `ENVIRONMENT_TYPE` che contiene la modalità di esecuzione corrente (dev, stage o prod) e una definizione. La definizione può essere `ENVIRONMENT_DEV`, `ENVIRONMENT_STAGE` o `ENVIRONMENT_PROD`. Nella configurazione di Apache, la variabile può essere utilizzata direttamente in un’espressione. In alternativa, è possibile utilizzare la definizione per generare la logica:

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

Nella configurazione del Dispatcher è disponibile la stessa variabile di ambiente. Se è necessaria una maggiore logica, definisci le variabili come mostrato nell’esempio precedente e utilizzale nella sezione Configurazione di Dispatcher :

```
/virtualhosts {
  { "${VIRTUALHOST}" }
}
```

In alternativa, puoi utilizzare le variabili di ambiente Cloud Manager nella configurazione httpd/dispatcher, anche se non i segreti dell’ambiente. Questo metodo è particolarmente importante se un programma dispone di più ambienti di sviluppo e alcuni di questi ambienti di sviluppo hanno valori diversi per la configurazione httpd/dispatcher. La stessa sintassi ${VIRTUALHOST} verrebbe utilizzata come nell&#39;esempio precedente, tuttavia non verranno utilizzate le dichiarazioni Define nel file delle variabili di cui sopra. Leggi la sezione [Documentazione di Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) per istruzioni su come configurare le variabili di ambiente di Cloud Manager.

Quando verifichi la configurazione localmente, puoi simulare diversi tipi di ambiente passando la variabile `DISP_RUN_MODE` al `docker_run.sh` script direttamente:

```
$ DISP_RUN_MODE=stage docker_run.sh src docker.for.mac.localhost:4503 8080
```

La modalità di esecuzione predefinita quando non si passa un valore per DISP_RUN_MODE è &quot;dev&quot;.
Per un elenco completo delle opzioni e delle variabili disponibili, esegui lo script `docker_run.sh` senza argomenti.

## Visualizzazione della configurazione del Dispatcher in uso dal contenitore Docker {#viewing-dispatcher-configuration-in-use-by-docker-container}

Con configurazioni specifiche per l’ambiente, può essere difficile determinare l’aspetto della configurazione effettiva di Dispatcher. Dopo aver avviato il contenitore docker con `docker_run.sh` può essere oggetto di dumping come segue:

* Determina l&#39;ID del contenitore docker in uso:

```
$ docker ps
CONTAINER ID       IMAGE
d75fbd23b29        adobe/aem-ethos/dispatcher-publish:...
```

* Esegui la seguente riga di comando con l’ID contenitore:

```
$ docker exec d75fbd23b29 httpd-test
# Dispatcher configuration: (/etc/httpd/conf.dispatcher.d/dispatcher.any)
/farms {
  /publishfarm {
    /clientheaders {
...
```

## Migrazione dalla modalità legacy alla modalità flessibile {#migrating}

Con la versione 2021.7.0 di Cloud Manager, i nuovi programmi Cloud Manager generano strutture di progetto Maven con [AEM archetipo 28](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) o superiore, che include il file **opt-in/USE_SOURCES_DIRECTLY**. Questo elimina le limitazioni precedenti del [modalità legacy](/help/implementing/dispatcher/validation-debug-legacy.md) circa il numero e le dimensioni dei file, con conseguente miglioramento della convalida e distribuzione della configurazione da parte dell’SDK e del runtime. Se la configurazione del dispatcher non dispone di questo file, ti consigliamo vivamente di eseguire la migrazione. Utilizza i seguenti passaggi per garantire una transizione sicura:

1. **Test locale.** Utilizzando l’SDK degli strumenti del dispatcher più recenti, aggiungi la cartella e il file `opt-in/USE_SOURCES_DIRECTLY`. Segui le istruzioni di &quot;convalida locale&quot; in questo articolo per verificare che il dispatcher funzioni localmente.
1. **Test di sviluppo cloud:**
   * Commit del file `opt-in/USE_SOURCES_DIRECTLY` a un ramo git distribuito dalla pipeline non di produzione in un ambiente di sviluppo Cloud.
   * Utilizza Cloud Manager per distribuire in un ambiente di sviluppo Cloud.
   * Esegui il test completo. È fondamentale verificare che la configurazione di apache e dispatcher si comporti come previsto prima di distribuire le modifiche agli ambienti più elevati. Controlla tutti i comportamenti relativi alla tua configurazione personalizzata! Invia un ticket di assistenza clienti se ritieni che la configurazione del dispatcher implementato non rifletta la configurazione personalizzata.

   >[!NOTE]
   >
   >In modalità flessibile è necessario utilizzare percorsi relativi invece di percorsi assoluti.
1. **Distribuzione in produzione:**
   * Commit del file `opt-in/USE_SOURCES_DIRECTLY` a un ramo Git distribuito dalla pipeline di produzione nell’area di lavoro e negli ambienti di produzione di Cloud.
   * Utilizza Cloud Manager per distribuire in staging.
   * Esegui il test completo. È fondamentale verificare che la configurazione di apache e dispatcher si comporti come previsto prima di distribuire le modifiche agli ambienti più elevati. Controlla tutti i comportamenti relativi alla tua configurazione personalizzata! Invia un ticket di assistenza clienti se ritieni che la configurazione del dispatcher implementato non rifletta la configurazione personalizzata.
   * Utilizza Cloud Manager per continuare la distribuzione in produzione.
