---
title: Convalida e debug tramite gli strumenti di Dispatcher
description: Convalida e debug tramite gli strumenti di Dispatcher
feature: Dispatcher
source-git-commit: 5545f7c271137050d522904bfa94e20f0286e059
workflow-type: tm+mt
source-wordcount: '2414'
ht-degree: 1%

---

# Convalida e debug tramite gli strumenti di Dispatcher {#Dispatcher-in-the-cloud}

## Introduzione {#apache-and-dispatcher-configuration-and-testing}

>[!NOTE]
>Per ulteriori informazioni su Dispatcher nel cloud e su come scaricare gli strumenti di Dispatcher, consulta la pagina [Dispatcher nel cloud](/help/implementing/dispatcher/disp-overview.md) . Se la configurazione del dispatcher è in modalità legacy, consulta la [documentazione sulla modalità legacy](/help/implementing/dispatcher/validation-debug-legacy.md).

Le sezioni seguenti descrivono la struttura del file in modalità flessibile, la convalida locale, il debug e la migrazione dalla modalità legacy alla modalità flessibile.

Questo articolo presuppone che la configurazione del dispatcher del progetto includa il file `opt-in/USE_SOURCES_DIRECTLY`, il che fa sì che l&#39;SDK e il runtime convalidino e distribuiscano la configurazione in un modo migliore rispetto alla modalità legacy, rimuovendo le limitazioni relative al numero e alle dimensioni dei file.

Di conseguenza, se la configurazione del dispatcher non include il file di cui sopra, è **altamente consigliato** migrare dalla modalità legacy alla modalità flessibile come descritto nella sezione [Migrazione dalla modalità legacy alla modalità flessibile](#migrating) .

## Struttura del file {#flexible-mode-file-structure}

La struttura della sottocartella Dispatcher del progetto è la seguente:

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
│── opt-in
│   └── USE_SOURCES_DIRECTLY
└── conf.dispatcher.d
    ├── available_farms
    │   └── default.farm
    ├── cache
    │   ├── default_invalidate.any
    │   ├── default_rules.any
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
    │   ├── default_virtualhosts.any
    │   └── virtualhosts.any
    
```

Di seguito è riportata una spiegazione dei file importanti che possono essere modificati:

**File personalizzabili**

I file seguenti sono personalizzabili e verranno trasferiti all’istanza Cloud durante la distribuzione:

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

Puoi avere uno o più di questi file. Contengono voci `<VirtualHost>` che corrispondono ai nomi host e consentono ad Apache di gestire il traffico di ogni dominio con regole diverse. I file vengono creati nella directory `available_vhosts` e abilitati con un collegamento simbolico nella directory `enabled_vhosts`. Dai file `.vhost` verranno inclusi altri file come le riscritture e le variabili.

* `conf.d/rewrites/rewrite.rules`

Questo file è incluso all&#39;interno dei file `.vhost`. Dispone di un set di regole di riscrittura per `mod_rewrite`.

* `conf.d/variables/custom.vars`

Questo file è incluso all&#39;interno dei file `.vhost`. Puoi aggiungere definizioni per le variabili Apache in questa posizione.

* `conf.d/variables/global.vars`

Questo file è incluso all&#39;interno del file `dispatcher_vhost.conf`. Puoi modificare il tuo livello di Dispatcher e riscrivere il livello di registro in questo file.

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

Puoi avere uno o più di questi file, che contengono farm che corrispondono ai nomi host e consentono al modulo Dispatcher di gestire ogni farm con regole diverse. I file vengono creati nella directory `available_farms` e abilitati con un collegamento simbolico nella directory `enabled_farms`. Dai file `.farm` verranno inclusi altri file come filtri, regole di cache e altri.

* `conf.dispatcher.d/cache/rules.any`

Questo file è incluso all&#39;interno dei file `.farm`. Specifica le preferenze di memorizzazione in cache.

* `conf.dispatcher.d/clientheaders/clientheaders.any`

Questo file è incluso all&#39;interno dei file `.farm`. Specifica quali intestazioni di richiesta devono essere inoltrate al backend.

* `conf.dispatcher.d/filters/filters.any`

Questo file è incluso all&#39;interno dei file `.farm`. Ha un set di regole che cambiano il traffico da filtrare e non arrivare al backend.

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

Questo file è incluso all&#39;interno dei file `.farm`. Contiene un elenco di nomi host o percorsi URI che devono essere associati dalla corrispondenza glob. Questo determina quale backend utilizzare per elaborare una richiesta.

* `opt-in/USE_SOURCES_DIRECTLY`

Questo file consente una configurazione più flessibile del dispatcher e rimuove le limitazioni precedenti relative al numero e alle dimensioni dei file. Inoltre, fa sì che l&#39;SDK e il runtime convalidino e distribuiscano la configurazione in modo migliore.

I file di cui sopra fanno riferimento ai file di configurazione immutabili elencati di seguito. Le modifiche ai file immutabili non verranno elaborate dai Dispatcher negli ambienti Cloud.

**File di configurazione immutabili**

Questi file fanno parte del framework di base e applicano gli standard e le best practice. I file sono considerati immutabili perché modificarli o eliminarli localmente non avranno alcun impatto sulla distribuzione, in quanto non verranno trasferiti all’istanza Cloud.

Si consiglia che i file di cui sopra facciano riferimento ai file immutabili elencati di seguito, seguiti da eventuali istruzioni o sostituzioni aggiuntive. Quando la configurazione di Dispatcher viene distribuita in un ambiente cloud, verrà utilizzata la versione più recente dei file immutabili, indipendentemente dalla versione utilizzata nello sviluppo locale.

* `conf.d/available_vhosts/default.vhost`

Contiene un esempio di host virtuale. Per il tuo host virtuale, crea una copia di questo file, personalizzalo, vai a `conf.d/enabled_vhosts` e crea un collegamento simbolico alla tua copia personalizzata.

* `conf.d/dispatcher_vhost.conf`

Parte del framework di base, utilizzato per illustrare il modo in cui vengono inclusi gli host virtuali e le variabili globali.

* `conf.d/rewrites/default_rewrite.rules`

Regole di riscrittura predefinite adatte a un progetto standard. Se hai bisogno di personalizzazione, modifica `rewrite.rules`. Nella personalizzazione, puoi comunque includere prima le regole predefinite, se sono adatte alle tue esigenze.

* `conf.dispatcher.d/available_farms/default.farm`

Contiene un esempio di farm del Dispatcher. Per la tua farm, crea una copia di questo file, personalizzalo, vai a `conf.d/enabled_farms` e crea un collegamento simbolico alla tua copia personalizzata.

* `conf.dispatcher.d/cache/default_invalidate.any`

Parte del framework di base, viene generato all&#39;avvio. Sei **obbligatorio** per includere questo file in ogni farm definita, nella sezione `cache/allowedClients` .

* `conf.dispatcher.d/cache/default_rules.any`

Regole di cache predefinite adatte a un progetto standard. Se hai bisogno di personalizzazione, modifica `conf.dispatcher.d/cache/rules.any`. Nella personalizzazione, puoi comunque includere prima le regole predefinite, se sono adatte alle tue esigenze.

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

Intestazioni di richiesta predefinite da inoltrare al backend, adatte a un progetto standard. Se hai bisogno di personalizzazione, modifica `clientheaders.any`. Nella personalizzazione, puoi comunque includere prima le intestazioni di richiesta predefinite, se sono adatte alle tue esigenze.

* `conf.dispatcher.d/dispatcher.any`

Parte del framework di base, utilizzato per illustrare come sono incluse le farm del Dispatcher.

* `conf.dispatcher.d/filters/default_filters.any`

Filtri predefiniti adatti a un progetto standard. Se hai bisogno di personalizzazione, modifica `filters.any`. Nella personalizzazione, puoi comunque includere prima i filtri predefiniti, se soddisfano le tue esigenze.

* `conf.dispatcher.d/renders/default_renders.any`

Parte del framework di base, questo file viene generato all&#39;avvio. Sei **obbligatorio** per includere questo file in ogni farm definita, nella sezione `renders` .

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

Globbing host predefinito adatto per un progetto standard. Se hai bisogno di personalizzazione, modifica `virtualhosts.any`. Nella tua personalizzazione, non devi includere il globbing host predefinito, in quanto corrisponde a **ogni** richiesta in arrivo.

## Moduli Apache supportati {#apache-modules}

Consulta [Moduli Apache supportati](/help/implementing/dispatcher/disp-overview.md#supported-directives).

## Convalida locale {#local-validation-flexible-mode}

>[!NOTE]
>Le sezioni seguenti includono comandi che utilizzano le versioni Mac o Linux dell&#39;SDK, ma l&#39;SDK di Windows può essere utilizzato anche in modo simile.

Utilizza lo script `validate.sh` come mostrato di seguito:

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
2. Esegue il comando `httpd -t` per verificare se la sintassi è corretta in modo che apache httpd possa avviarsi. In caso di esito positivo, la configurazione dovrebbe essere pronta per la distribuzione.
3. Controlla che il sottoinsieme dei file di configurazione dell’SDK di Dispatcher, che sono destinati ad essere immutabili come descritto nella [sezione Struttura file](##flexible-mode-file-structure), non sia stato modificato.

Durante un’implementazione di Cloud Manager, verrà eseguito anche il controllo di sintassi `httpd -t` e tutti gli errori verranno inclusi nel registro di Cloud Manager `Build Images step failure`.

### Fase 1 {#first-phase}

Se una direttiva non viene inserita nell&#39;elenco Consentiti, lo strumento registra un errore e restituisce un codice di uscita diverso da zero. Inoltre, esamina ulteriormente tutti i file con il pattern `conf.dispatcher.d/enabled_farms/*.farm` e verifica che:

* Non esiste una regola di filtro che utilizza l&#39;autorizzazione tramite `/glob` (consulta [CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957) per ulteriori dettagli.
* Non viene visualizzata alcuna funzione di amministrazione. Ad esempio, puoi accedere a percorsi quali `/crx/de or /system/console`.

Lo strumento di convalida segnala solo l’uso non consentito di direttive Apache che non sono state inserite nell&#39;elenco Consentiti. Non segnala problemi sintattici o semantici con la configurazione Apache, in quanto queste informazioni sono disponibili solo per i moduli Apache in un ambiente in esecuzione.

Di seguito sono riportate le tecniche di risoluzione dei problemi per il debug di errori di convalida comuni generati dallo strumento:

**impossibile individuare una  `conf.dispatcher.d` sottocartella nell&#39;archivio**

L’archivio deve contenere le cartelle `conf.d` e `conf.dispatcher.d`. Nota: **non** utilizzare il
prefisso `etc/httpd` nell’archivio.

**impossibile trovare aziende agricole in`conf.dispatcher.d/enabled_farms`**

Le farm abilitate devono trovarsi nella sottocartella indicata.

**il file incluso (..) deve essere denominato: ...**

Nella configurazione della farm sono presenti due sezioni che **devono includere
file specifico: `/renders` e `/allowedClients` nella sezione `/cache`.** Tali
le sezioni devono essere le seguenti:

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

Nella configurazione della farm sono presenti quattro sezioni in cui puoi includere il tuo file: `/clientheaders`, `filters`, `/rules` nelle sezioni `/cache` e `/virtualhosts`. I file inclusi devono essere denominati come segue:

| Sezione | Nome file di inclusione |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

In alternativa, è possibile includere la versione **predefinita** di tali file, i cui nomi sono preceduti dalla parola `default_`, ad esempio `../filters/default_filters.any`.

**include l&#39;istruzione in (...), al di fuori di qualsiasi posizione nota: ...**

Oltre alle sei sezioni menzionate nei paragrafi precedenti, non è consentito
per utilizzare l’istruzione `$include`, ad esempio, il seguente genera questo errore:

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**i client/rendering consentiti non sono inclusi in: ...**

Questo errore viene generato quando non si specifica un&#39;inclusione per `/renders` e `/allowedClients` nella sezione `/cache`. Consulta la sezione
**il file incluso (...) deve essere denominato: ...Sezione** per ulteriori informazioni.

**Il filtro non deve utilizzare il pattern glob per consentire le richieste**

Non è sicuro consentire le richieste con una regola di stile `/glob` che viene confrontata con l’intera riga di richiesta, ad esempio

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

Questa istruzione ha lo scopo di consentire le richieste per i file `css`, ma consente anche le richieste a **qualsiasi risorsa** seguita dalla stringa query `?a=.css`. È pertanto vietato utilizzare tali filtri (cfr. anche CVE-2016-0957).

**il file incluso (...) non corrisponde ad alcun file noto**

Nella configurazione dell’host virtuale Apache sono disponibili due tipi di file che è possibile specificare come include: riscrive e variabili.
I file inclusi devono essere denominati come segue:

| Tipo | Nome file di inclusione |
|-----------|---------------------------------|
| Riscrittura | `conf.d/rewrites/rewrite.rules` |
| Variabili | `conf.d/variables/custom.vars` |

In alternativa, è possibile includere la versione **predefinita** delle regole di riscrittura, il cui nome è `conf.d/rewrites/default_rewrite.rules`.
Tieni presente che non esiste una versione predefinita dei file delle variabili.

**Rilevato layout di configurazione obsoleto, abilitazione della modalità di compatibilità**

Questo messaggio indica che la configurazione presenta un layout della versione 1 obsoleto, contenente un
Configurazione di Apache e file con prefissi `ams_`. Anche se questo è ancora supportato per le versioni precedenti
compatibilità, è necessario passare al nuovo layout.

Tieni presente che la prima fase può anche essere **eseguita separatamente**, anziché dallo script wrapper `validate.sh`.

Quando viene eseguito contro l’artefatto maven o la sottodirectory `dispatcher/src`, gli errori di convalida vengono segnalati:

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

Evita questo errore copiando e incollando il percorso da Esplora risorse e quindi dal prompt dei comandi utilizzando un comando `cd` in quel percorso.

### Fase 2 {#second-phase}

Questa fase controlla la sintassi Apache avviando Docker in un&#39;immagine. Il Docker deve essere installato localmente, ma non è necessario eseguire AEM.

>[!NOTE]
>Gli utenti Windows devono utilizzare Windows 10 Professional o altre distribuzioni che supportano Docker. Questo è un prerequisito per l’esecuzione e il debug di Dispatcher su un computer locale.

Questa fase può anche essere eseguita in modo indipendente tramite `bin/docker_run.sh src/dispatcher host.internal.docker:4503 8080`.

Durante un’implementazione di Cloud Manager, verrà eseguito anche il controllo di sintassi `httpd -t` e gli eventuali errori verranno inclusi nel registro degli errori del passaggio Build Images di Cloud Manager.

### Fase 3 {#third-phase}

Se si verifica un errore in questa fase, significa che Adobe ha modificato uno o più file immutabili e devi sostituire i corrispondenti file immutabili con la nuova versione consegnata nella directory `src` dell&#39;SDK. Il seguente esempio di log illustra questo problema:

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

## Debug della configurazione di Apache e Dispatcher {#debugging-apache-and-dispatcher-configuration}

Tieni presente che puoi eseguire il dispatcher Apache localmente utilizzando `./bin/docker_run.sh src/dispatcher docker.for.mac.localhost:4503 8080`.

Come indicato in precedenza, Docker deve essere installato localmente e non è necessario che AEM sia in esecuzione. Gli utenti Windows devono utilizzare Windows 10 Professional o altre distribuzioni che supportano Docker. Questo è un prerequisito per l’esecuzione e il debug di Dispatcher su un computer locale.

La seguente strategia può essere utilizzata per aumentare l’output di registro per il modulo Dispatcher e visualizzare i risultati della valutazione `RewriteRule` sia negli ambienti locali che in quelli cloud.

I livelli di registro per tali moduli sono definiti dalle variabili `DISP_LOG_LEVEL` e `REWRITE_LOG_LEVEL`. Possono essere impostati nel file `conf.d/variables/global.vars`. La sua parte pertinente è la seguente:

```
# Log level for the dispatcher
#
# Possible values are: Error, Warn, Info, Debug and Trace1
# Default value: Warn
#
# Define DISP_LOG_LEVEL Warn
 
# Log level for mod_rewrite
#
# Possible values are: Error, Warn, Info, Debug and Trace1 - Trace8
# Default value: Warn
#
# To debug your RewriteRules, it is recommended to raise your log
# level to Trace2.
#
# More information can be found at:
# https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging
#
# Define REWRITE_LOG_LEVEL Warn
```

Quando si esegue Dispatcher localmente, i registri vengono stampati direttamente nell’output del terminale. Nella maggior parte dei casi, si desidera che questi log siano in DEBUG, che può essere fatto passando il livello Debug come parametro durante l&#39;esecuzione di Docker. Esempio: `DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`.

I registri per gli ambienti cloud sono esposti tramite il servizio di registrazione disponibile in Cloud Manager.

## Diverse configurazioni del Dispatcher per ambiente {#different-dispatcher-configurations-per-environment}

Attualmente, la stessa configurazione del Dispatcher viene applicata a tutti i AEM come ambienti di Cloud Service. Il runtime dispone di una variabile di ambiente `ENVIRONMENT_TYPE` che contiene la modalità di esecuzione corrente (dev, stage o prod) e di una definizione. La definizione può essere `ENVIRONMENT_DEV`, `ENVIRONMENT_STAGE` o `ENVIRONMENT_PROD`. Nella configurazione di Apache, la variabile può essere utilizzata direttamente in un’espressione. In alternativa, è possibile utilizzare la definizione per generare la logica:

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

Quando esegui il test della configurazione localmente, puoi simulare diversi tipi di ambiente passando direttamente la variabile `DISP_RUN_MODE` allo script `docker_run.sh` :

```
$ DISP_RUN_MODE=stage docker_run.sh out docker.for.mac.localhost:4503 8080
```

La modalità di esecuzione predefinita quando non si passa un valore per DISP_RUN_MODE è &quot;dev&quot;.
Per un elenco completo delle opzioni e delle variabili disponibili, eseguire lo script `docker_run.sh` senza argomenti.

## Visualizzazione della configurazione del Dispatcher in uso dal contenitore Docker {#viewing-dispatcher-configuration-in-use-by-docker-container}

Con configurazioni specifiche per l’ambiente, può essere difficile determinare l’aspetto della configurazione effettiva di Dispatcher. Dopo aver avviato il contenitore docker con `docker_run.sh`, può essere scaricato come segue:

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

Con la versione 2021.7.0 di Cloud Manager, i nuovi programmi di Cloud Manager generano strutture di progetto Maven con [AEM archetipo 28](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en) o superiore, che include il file **opt-in/USE_SOURCES_DIRECTLY**. Questo rimuove le limitazioni precedenti della [modalità legacy](/help/implementing/dispatcher/validation-debug-legacy.md) relative al numero e alle dimensioni dei file, causando anche una migliore convalida e distribuzione della configurazione da parte dell&#39;SDK e del runtime. Se la configurazione del dispatcher non dispone di questo file, ti consigliamo vivamente di eseguire la migrazione. Utilizza i seguenti passaggi per garantire una transizione sicura:

1. **Test locale.** Utilizzando l’SDK degli strumenti del dispatcher più recenti, aggiungi la cartella e il file  `opt-in/USE_SOURCES_DIRECTLY`. Segui le istruzioni di &quot;convalida locale&quot; in questo articolo per verificare che il dispatcher funzioni localmente.
2. **Test di sviluppo cloud:**
   * Invia il file `opt-in/USE_SOURCES_DIRECTLY` a un ramo git distribuito dalla pipeline non di produzione in un ambiente di sviluppo Cloud.
   * Utilizza Cloud Manager per distribuire in un ambiente di sviluppo Cloud.
   * Esegui il test completo. È fondamentale verificare che la configurazione di apache e dispatcher si comporti come previsto prima di distribuire le modifiche agli ambienti più elevati. Controlla tutti i comportamenti relativi alla tua configurazione personalizzata! Invia un ticket di assistenza clienti se ritieni che la configurazione del dispatcher implementato non rifletta la configurazione personalizzata.
3. **Distribuzione in produzione:**
   * Conferma il file `opt-in/USE_SOURCES_DIRECTLY` a un ramo git distribuito dalla pipeline di produzione nell’area di visualizzazione e negli ambienti di produzione di Cloud.
   * Utilizza Cloud Manager per distribuire in staging.
   * Esegui il test completo. È fondamentale verificare che la configurazione di apache e dispatcher si comporti come previsto prima di distribuire le modifiche agli ambienti più elevati. Controlla tutti i comportamenti relativi alla tua configurazione personalizzata! Invia un ticket di assistenza clienti se ritieni che la configurazione del dispatcher implementato non rifletta la configurazione personalizzata.
   * Utilizza Cloud Manager per continuare la distribuzione in produzione.
