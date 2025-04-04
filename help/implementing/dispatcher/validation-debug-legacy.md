---
title: Convalida e debug con gli strumenti di Dispatcher (legacy)
description: Convalida e debug con gli strumenti di Dispatcher (legacy)
feature: Dispatcher
hidefromtoc: true
exl-id: dc04d035-f002-42ef-9c2e-77602910c2ec
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '2337'
ht-degree: 1%

---

# Convalida e debug con gli strumenti di Dispatcher (legacy)  {#Dispatcher-tools-legacy}

## Introduzione {#apache-and-dispatcher-configuration-and-testing}

>[!NOTE]
>Per ulteriori informazioni su Dispatcher nel cloud e su come scaricare Dispatcher Tools, visita la pagina [Dispatcher nel cloud](/help/implementing/dispatcher/disp-overview.md).

Le sezioni seguenti descrivono la struttura del file in modalità legacy, la convalida locale, il debug e le modalità di migrazione dalla modalità legacy alla [modalità flessibile](/help/implementing/dispatcher/validation-debug.md).

Questo articolo presuppone che la configurazione Dispatcher del progetto non includa il file opt-in/USE_SOURCES_DIRECT. Di conseguenza, presenta limitazioni relative al numero e alle dimensioni dei file, ad esempio:

* un singolo file di riscrittura che deve essere utilizzato anziché file specifici del sito.
* la somma del contenuto dei file personalizzabili deve essere inferiore a 1 MB.

A partire dalla versione 2021.7.0 di Cloud Manager, i nuovi programmi Cloud Manager generano strutture di progetto Maven con AEM archetipo 28 e versioni successive, che includono il file precedentemente menzionato.

È **vivamente consigliato** effettuare la migrazione dalla modalità legacy alla modalità flessibile come descritto nella sezione sulla migrazione [Migrazione dalla modalità legacy alla modalità flessibile](#migrating-flexible). L’utilizzo della modalità flessibile consente inoltre all’SDK e al runtime di convalidare e distribuire la configurazione in modo migliorato.

## Struttura del file {#legacy-mode-file-structure}

La struttura della sottocartella Dispatcher del progetto (in modalità legacy) è la seguente:

```bash
./
├── conf.d
│   ├── available_vhosts
│   │   └── default.vhost
│   ├── dispatcher_vhost.conf
│   ├── enabled_vhosts
│   │   ├── README
│   │   └── default.vhost -> ../available_vhosts/default.vhost
│   └── rewrites
│   │   ├── default_rewrite.rules
│   │   └── rewrite.rules
│   └── variables
|       ├── custom.vars
│       └── global.vars
└── conf.dispatcher.d
    ├── available_farms
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
    │   └── default.farm -> ../available_farms/default.farm
    ├── filters
    │   ├── default_filters.any
    │   └── filters.any
    ├── renders
    │   └── default_renders.any
    └── virtualhosts
        ├── default_virtualhosts.any
        └── virtualhosts.any
```

Di seguito è riportata una spiegazione dei file rilevanti che possono essere modificati:

**File personalizzabili**

I seguenti file sono personalizzabili e vengono trasferiti nell’istanza Cloud al momento dell’implementazione:

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

Puoi avere uno o più di questi file. Contengono `<VirtualHost>` voci che corrispondono ai nomi host e consentono ad Apache di gestire ogni traffico di dominio con regole diverse. I file vengono creati nella directory `available_vhosts` e abilitati con un collegamento simbolico nella directory `enabled_vhosts`. Dai file `.vhost` sono inclusi altri file, ad esempio riscritture e variabili.

* `conf.d/rewrites/rewrite.rules`

Questo file è incluso nei tuoi file `.vhost`. Include un set di regole di riscrittura per `mod_rewrite`.

>[!NOTE]
>
>Attualmente, è necessario utilizzare un singolo file di riscrittura anziché file specifici del sito. Di norma, la somma del contenuto dei file personalizzabili deve essere inferiore a 1 MB.

* `conf.d/variables/custom.vars`

Questo file è incluso nei tuoi file `.vhost`. Puoi aggiungere definizioni per le variabili Apache in questa posizione.

* `conf.d/variables/global.vars`

Il file è incluso nel file `dispatcher_vhost.conf`. Puoi modificare il Dispatcher e riscrivere il livello di registro in questo file.

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

Puoi avere uno o più di questi file, che contengono farm con nomi host corrispondenti e consentono al modulo Dispatcher di gestire ogni farm con regole diverse. I file vengono creati nella directory `available_farms` e abilitati con un collegamento simbolico nella directory `enabled_farms`. Dai file `.farm`, sono inclusi altri file come filtri, regole di cache e altri.

* `conf.dispatcher.d/cache/rules.any`

Questo file è incluso nei tuoi file `.farm`. Specifica le preferenze di caching.

* `conf.dispatcher.d/clientheaders/clientheaders.any`

Questo file è incluso nei tuoi file `.farm`. Specifica le intestazioni di richiesta da inoltrare al backend.

* `conf.dispatcher.d/filters/filters.any`

Questo file è incluso nei tuoi file `.farm`. Ha una serie di regole che modificano il tipo di traffico da filtrare e non lo rendono al backend.

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

Questo file è incluso nei tuoi file `.farm`. Dispone di un elenco di nomi host o percorsi URI a cui deve corrispondere la corrispondenza glob. Questa corrispondenza determina il backend da utilizzare per distribuire una richiesta.

I file di cui sopra fanno riferimento ai file di configurazione immutabili elencati di seguito. Le modifiche ai file immutabili non vengono elaborate da Dispatcher in ambienti Cloud.

**File di configurazione immutabili**

Questi file fanno parte del framework di base e applicano standard e best practice. I file sono considerati immutabili perché la loro modifica o eliminazione locale non ha alcun impatto sulla distribuzione, in quanto non vengono trasferiti nell’istanza Cloud.

Si consiglia che i file di cui sopra facciano riferimento ai file immutabili elencati di seguito, seguiti da eventuali istruzioni o sostituzioni aggiuntive. Quando la configurazione Dispatcher viene distribuita in un ambiente cloud, viene utilizzata la versione più recente dei file immutabili, indipendentemente dalla versione utilizzata nello sviluppo locale.

* `conf.d/available_vhosts/default.vhost`

Contiene un host virtuale di esempio. Per il tuo host virtuale, crea una copia di questo file, personalizzalo, passa a `conf.d/enabled_vhosts` e crea un collegamento simbolico alla tua copia personalizzata.

* `conf.d/dispatcher_vhost.conf`

Parte del framework di base, utilizzato per illustrare come vengono inclusi gli host virtuali e le variabili globali.

* `conf.d/rewrites/default_rewrite.rules`

Regole predefinite per la riscrittura adatte a un progetto standard. Se è necessario eseguire la personalizzazione, modificare `rewrite.rules`. Nella personalizzazione, puoi comunque includere prima le regole predefinite, se soddisfano le tue esigenze.

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

## Convalida locale {#local-validation-legacy-mode}

>[!NOTE]
>Le sezioni seguenti includono comandi che utilizzano le versioni Mac o Linux® dell’SDK, ma l’SDK di Windows può essere utilizzato anche in modo simile.

Utilizza lo script `validate.sh` come illustrato di seguito:

```
$ validate.sh src/dispatcher
Phase 1: Dispatcher validator
Cloud manager validator 2.0.32
Phase 1 finished
Phase 2: httpd -t validation in docker image
values.csv found in deployment folder: /tmp/dispatcher_validation_1625150390 - using files listed there
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

Lo script esegue le operazioni seguenti:

1. Esegue la convalida. Se la configurazione non è valida, lo script non riesce.
2. Esegue il comando `httpd -t` per verificare se la sintassi è corretta in modo che Apache httpd possa avviarsi. In caso di esito positivo, la configurazione deve essere pronta per la distribuzione.
3. Verifica che il sottoinsieme dei file di configurazione dell&#39;SDK di Dispatcher, che devono essere immutabili come descritto nella [sezione sulla struttura dei file](##legacy-mode-file-structure), non sia stato modificato. Questo controllo è una nuova versione, introdotta con la versione v2021.1.4738 dell’SDK per AEM che include anche la versione 2.0.36 degli strumenti Dispatcher. Prima di questo aggiornamento, i clienti potevano erroneamente supporre che eventuali modifiche SDK locali di tali file immutabili sarebbero state applicate anche all’ambiente Cloud.

Durante una distribuzione Cloud Manager, viene eseguito anche il controllo della sintassi `httpd -t` e gli eventuali errori vengono inclusi nel registro di Cloud Manager `Build Images step failure`.

### Fase 1 {#first-phase}

Se una direttiva non viene inserita nell&#39;elenco Consentiti, lo strumento registra un errore e restituisce un codice di uscita diverso da zero. Inoltre, esegue un&#39;ulteriore scansione di tutti i file con il pattern `conf.dispatcher.d/enabled_farms/*.farm` e verifica che:

* Non esiste alcuna regola di filtro che utilizza allow tramite `/glob` (vedi [CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957) per ulteriori dettagli.
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

Nella configurazione della farm sono disponibili quattro sezioni in cui è possibile includere il proprio file: `/clientheaders`, `filters`, `/rules` nella sezione `/cache` e `/virtualhosts`. I file inclusi devono essere denominati come segue:

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

Nella configurazione dell’host virtuale Apache sono disponibili due tipi di file che possono essere specificati come inclusivi: riscritture e variabili.
I file inclusi devono essere denominati come segue:

| Tipo | Includi nome file |
|-----------|---------------------------------|
| Riscrittura | `conf.d/rewrites/rewrite.rules` |
| Variabili | `conf.d/variables/custom.vars` |

>[!TIP]
>
>Per poter includere più file in modo molto meno limitato, è possibile passare alla modalità di configurazione flessibile di Dispatcher. Per ulteriori informazioni sulla modalità flessibile, vedere [Convalida e debug con gli strumenti di Dispatcher](/help/implementing/dispatcher/validation-debug.md).

In alternativa, è possibile includere la versione **default** delle regole di riscrittura, il cui nome è `conf.d/rewrites/default_rewrite.rules`.
Nota: non esiste una versione predefinita dei file delle variabili.

**Rilevato layout di configurazione obsoleto, abilitazione della modalità di compatibilità**

Questo messaggio indica che la configurazione ha il layout versione 1 obsoleto, contenente un elemento
Configurazione Apache e file con prefissi `ams_`. Questa configurazione è ancora supportata per le versioni precedenti
è necessario passare al nuovo layout.

Anche la prima fase può essere **eseguita separatamente**, anziché dallo script wrapper `validate.sh`.

Quando viene eseguito in base all&#39;artefatto Maven o alla sottodirectory `dispatcher/src`, vengono segnalati errori di convalida:

```
$ validator full dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

In Windows, la convalida di Dispatcher distingue tra maiuscole e minuscole. Di conseguenza, potrebbe non essere possibile convalidare la configurazione se non si rispetta la combinazione di maiuscole e minuscole del percorso in cui si trova la configurazione, ad esempio:

```
bin\validator.exe full src
Cloud manager validator 2.0.xx
2021/03/15 18:15:40 Dispatcher configuration validation failed:
  conf.dispatcher.d\available_farms\default.farm:15: parent directory outside server root: c:\k\a\aem-dispatcher-sdk-windows-symlinks-testing3\dispatcher\src
  
```

Evitare questo errore copiando e incollando il percorso da Esplora risorse e quindi al prompt dei comandi utilizzando un comando `cd` nel percorso.

### Fase 2 {#second-phase}

Questa fase controlla la sintassi di Apache avviando Docker in un’immagine. Docker deve essere installato localmente, ma non è necessario che l’AEM sia in esecuzione.

>[!NOTE]
>Gli utenti di Windows devono utilizzare Windows 10 Professional o altre distribuzioni che supportano Docker. Questo prerequisito è necessario per eseguire il debug di Dispatcher in un computer locale.

Questa fase può anche essere eseguita in modo indipendente tramite `validator full -d out src/dispatcher`, che genera una directory &quot;out&quot; necessaria per il comando successivo `bin/docker_run.sh out host.docker.internal:4503 8080`.

Durante una distribuzione Cloud Manager, viene eseguito il controllo della sintassi `httpd -t` e tutti gli errori vengono inclusi nel registro errori del passaggio Immagini di compilazione di Cloud Manager.

### Fase 3 {#third-phase}

Se si verifica un errore in questa fase, significa che Adobe ha modificato uno o più file immutabili. In tal caso, è necessario sostituire i file immutabili corrispondenti con la nuova versione distribuita nella directory `src` dell&#39;SDK. Il seguente esempio di registro illustra questo problema:

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

Questa fase può anche essere eseguita in modo indipendente tramite `validator full -d out src/dispatcher`, che genera una directory &quot;out&quot;, necessaria per il comando successivo `bin/docker_immutability_check.sh out`.

## Debug della configurazione di Apache e Dispatcher {#debugging-apache-and-dispatcher-configuration}

È possibile eseguire Apache Dispatcher localmente utilizzando `./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`.

Come indicato in precedenza, Docker deve essere installato localmente e non è necessario che l’AEM sia in esecuzione. Gli utenti di Windows devono utilizzare Windows 10 Professional o altre distribuzioni che supportano Docker. Questo prerequisito è necessario per eseguire il debug di Dispatcher in un computer locale.

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

Se Dispatcher viene eseguito localmente, i registri vengono stampati direttamente nell&#39;output del terminale. Nella maggior parte dei casi, si desidera che questi registri siano in DEBUG, operazione che può essere eseguita passando il livello di debug come parametro durante l’esecuzione di Docker. Ad esempio: `DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`.

I registri per gli ambienti cloud vengono esposti tramite il servizio di registrazione disponibile in Cloud Manager.

## Diverse configurazioni di Dispatcher per ambiente {#different-dispatcher-configurations-per-environment}

Attualmente, la stessa configurazione di Dispatcher viene applicata a tutti gli ambienti su AEM as a Cloud Service. Il runtime dispone di una variabile di ambiente `ENVIRONMENT_TYPE` che contiene la modalità di esecuzione corrente (dev, stag o prod) e una definizione. La definizione può essere `ENVIRONMENT_DEV`, `ENVIRONMENT_STAGE` o `ENVIRONMENT_PROD`. Nella configurazione di Apache, la variabile può essere utilizzata direttamente in un’espressione. In alternativa, è possibile utilizzare la definizione per generare la logica:

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

Quando si esegue il test della configurazione in locale, è possibile simulare diversi tipi di ambiente passando la variabile `DISP_RUN_MODE` direttamente allo script `docker_run.sh`:

```
$ DISP_RUN_MODE=stage docker_run.sh out docker.for.mac.localhost:4503 8080
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

## Migrazione dalla modalità legacy alla modalità flessibile {#migrating-flexible}

Con la versione di Cloud Manager 2021.7.0, i nuovi programmi Cloud Manager generano strutture di progetto Maven con archetipo AEM 28 o versione successiva, che include il file **opt-in/USE_SOURCES_DIRECT**. Le limitazioni precedenti della modalità legacy riguardo al numero e alle dimensioni dei file vengono rimosse, consentendo all’SDK e al runtime di convalidare e distribuire la configurazione in modo migliorato. Se la configurazione del Dispatcher non dispone di questo file, si consiglia vivamente di eseguire la migrazione. Utilizzare i metodi descritti nella pagina [modalità flessibile](/help/implementing/dispatcher/validation-debug.md#migrating).
