---
title: Dispatcher nel cloud
description: 'Dispatcher nel cloud '
feature: Dispatcher
exl-id: 6d78026b-687e-434e-b59d-9d101349a707
translation-type: tm+mt
source-git-commit: f6c700f82bc5a1a3edf05911a29a6e4d32dd3f72
workflow-type: tm+mt
source-wordcount: '4211'
ht-degree: 6%

---

# Dispatcher nel cloud {#Dispatcher-in-the-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispoverview"
>title="Dispatcher nel cloud"
>abstract="Questa sezione descrive come strutturare il AEM come configurazioni di Cloud Service Apache e Dispatcher, nonché come convalidarlo ed eseguirlo localmente prima di distribuirlo negli ambienti Cloud. Descrive anche il debug negli ambienti Cloud."

## Configurazione e test di Apache e Dispatcher {#apache-and-dispatcher-configuration-and-testing}

Questa sezione descrive come strutturare il AEM come configurazioni di Cloud Service Apache e Dispatcher, nonché come convalidarlo ed eseguirlo localmente prima di distribuirlo negli ambienti Cloud. Descrive anche il debug negli ambienti Cloud. Per ulteriori informazioni su Dispatcher, consulta la [AEM documentazione di Dispatcher](https://docs.adobe.com/content/help/it-IT/experience-manager-dispatcher/using/dispatcher.html).

>[!NOTE]
>Gli utenti Windows devono utilizzare Windows 10 Professional o altre distribuzioni che supportano Docker. Questo è un prerequisito per l’esecuzione e il debug di Dispatcher su un computer locale. Le sezioni seguenti includono comandi che utilizzano le versioni Mac o Linux dell&#39;SDK, ma l&#39;SDK di Windows può essere utilizzato in modo simile.

## Strumenti del dispatcher {#dispatcher-sdk}

Gli strumenti di Dispatcher fanno parte del AEM generale come SDK per Cloud Service e forniscono:

* Una struttura di file vaniglia contenente i file di configurazione da includere in un progetto Maven per Dispatcher.
* Possibilità per i clienti di verificare che la configurazione di Dispatcher includa solo AEM come direttive supportate dal Cloud Service.        Inoltre, il tooling verifica che la sintassi sia corretta in modo che apache possa avviarsi con successo.
* Immagine Docker che porta il Dispatcher localmente.

## Download ed estrazione degli strumenti {#extracting-the-sdk}

Gli strumenti Dispatcher, parte del [AEM come Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md), possono essere scaricati da un file zip dal portale [Distribuzione software](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html) . Qualsiasi nuova configurazione disponibile in quella nuova versione di Dispatcher Tools, può essere utilizzata per distribuire negli ambienti Cloud in cui è in esecuzione la versione di AEM nel Cloud o una versione successiva.

Decomprimi l’SDK, che crea i bundle degli strumenti Dispatcher per macOS/Linux e Windows.

**Per macOS/Linux**, esegui l’artefatto dello strumento Dispatcher e eseguilo. Estrae automaticamente i file degli strumenti del Dispatcher sotto la directory in cui è stato memorizzato (dove `version` è la versione degli strumenti del Dispatcher).

```bash
$ chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
$ ./aem-sdk-dispatcher-tools-<version>-unix.sh
Verifying archive integrity...  100%   All good.
Uncompressing aem-sdk-dispatcher-tools-<version>-unix.sh 100%
```

**Per Windows**, estrarre l’archivio zip Dispatcher Tooling.

## Struttura dei file {#file-structure}

La struttura della sottocartella Dispatcher del progetto è descritta di seguito e deve essere copiata nella cartella Dispatcher del progetto Maven:

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

Di seguito è riportata una spiegazione dei file importanti che possono essere modificati:

**File personalizzabili**

I file seguenti sono personalizzabili e verranno trasferiti all’istanza Cloud durante la distribuzione:

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

Puoi avere uno o più di questi file. Contengono voci `<VirtualHost>` che corrispondono ai nomi host e consentono ad Apache di gestire il traffico di ogni dominio con regole diverse. I file vengono creati nella directory `available_vhosts` e abilitati con un collegamento simbolico nella directory `enabled_vhosts`. Dai file `.vhost` verranno inclusi altri file come le riscritture e le variabili.

* `conf.d/rewrites/rewrite.rules`

Questo file è incluso all&#39;interno dei file `.vhost`. Dispone di un set di regole di riscrittura per `mod_rewrite`.

>[!NOTE]
>
>Attualmente, è necessario utilizzare un singolo file di riscrittura anziché file specifici per il sito. Di regola, la somma dei contenuti dei file personalizzabili deve essere inferiore a 1 MB.

* `conf.d/variables/custom.vars`

Questo file è incluso all&#39;interno dei file `.vhost`. Puoi inserire le definizioni per le variabili Apache in questa posizione.

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

>[!NOTE]
>
>L’AEM come archetipo di Cloud Service Maven genera la stessa struttura di file di configurazione del Dispatcher.

Le sezioni seguenti descrivono come convalidare la configurazione localmente in modo da poter superare il gate di qualità associato in Cloud Manager durante la distribuzione di una versione interna.

## Convalida locale delle direttive supportate nella configurazione di Dispatcher {#local-validation-of-dispatcher-configuration}

Lo strumento di convalida è disponibile nell&#39;SDK in `bin/validator` come binario per Mac OS, Linux o Windows, consentendo ai clienti di eseguire la stessa convalida che Cloud Manager eseguirà durante la creazione e la distribuzione di una versione.

Viene richiamato come: `validator full [-d folder] [-w allowlist] zip-file | src folder`

Lo strumento verifica che la configurazione del Dispatcher utilizzi le direttive appropriate supportate da AEM as a Cloud Service tramite la scansione di tutti i file con pattern `conf.d/enabled_vhosts/*.vhost`.

In Windows, la convalida del dispatcher fa distinzione tra maiuscole e minuscole. Di conseguenza, la convalida della configurazione può non riuscire se non si rispetta la capitalizzazione del percorso in cui si trova la configurazione, ad esempio:

```
bin\validator.exe full src
Cloud manager validator 2.0.xx
2021/03/15 18:15:40 Dispatcher configuration validation failed:
  conf.dispatcher.d\available_farms\default.farm:15: parent directory outside server root: c:\k\a\aem-dispatcher-sdk-windows-symlinks-testing3\dispatcher\src
  
```

Evita questo errore copiando e incollando il percorso da Esplora risorse e quindi dal prompt dei comandi utilizzando un comando `cd` in quel percorso.

Le direttive consentite nei file di configurazione Apache possono essere elencate eseguendo il comando di inserire nell&#39;elenco Consentiti della convalida:

```
$ validator allowlist
Cloud manager validator 2.0.4
 
Allowlisted directives:
  <Directory>
  ...
  
```

La tabella seguente mostra i moduli Apache supportati:

| Nome modulo | Pagina di riferimento |
|---|---|
| `core` | [https://httpd.apache.org/docs/2.4/mod/core.html](https://httpd.apache.org/docs/2.4/mod/core.html) |
| `mod_access_compat` | [https://httpd.apache.org/docs/2.4/mod/mod_access_compat.html](https://httpd.apache.org/docs/2.4/mod/mod_access_compat.html) |
| `mod_alias` | [https://httpd.apache.org/docs/2.4/mod/mod_alias.html](https://httpd.apache.org/docs/2.4/mod/mod_alias.html) |
| `mod_allowmethods` | [https://httpd.apache.org/docs/2.4/mod/mod_allowmethods.html](https://httpd.apache.org/docs/2.4/mod/mod_allowmethods.html) |
| `mod_authn_core` | [https://httpd.apache.org/docs/2.4/mod/mod_authn_core.html](https://httpd.apache.org/docs/2.4/mod/mod_authn_core.html) |
| `mod_authn_file` | [https://httpd.apache.org/docs/2.4/mod/core.html](https://httpd.apache.org/docs/2.4/mod/mod_authn_file.html) |
| `mod_authz_core` | [https://httpd.apache.org/docs/2.4/mod/core.html](https://httpd.apache.org/docs/2.4/mod/mod_authz_core.html) |
| `mod_authz_groupfile` | [https://httpd.apache.org/docs/2.4/mod/mod_authz_groupfile.html](https://httpd.apache.org/docs/2.4/mod/mod_authz_groupfile.html) |
| `mod_deflate` | [https://httpd.apache.org/docs/2.4/mod/mod_deflate.html](https://httpd.apache.org/docs/2.4/mod/mod_deflate.html) |
| `mod_dir` | [https://httpd.apache.org/docs/2.4/mod/mod_dir.html](https://httpd.apache.org/docs/2.4/mod/mod_dir.html) |
| `mod_env` | [https://httpd.apache.org/docs/2.4/mod/mod_env.html](https://httpd.apache.org/docs/2.4/mod/mod_env.html) |
| `mod_filter` | [https://httpd.apache.org/docs/2.4/mod/mod_filter.html](https://httpd.apache.org/docs/2.4/mod/mod_filter.html) |
| `mod_headers` | [https://httpd.apache.org/docs/2.4/mod/mod_headers.html](https://httpd.apache.org/docs/2.4/mod/mod_headers.html) |
| `mod_mime` | [https://httpd.apache.org/docs/2.4/mod/mod_mime.html](https://httpd.apache.org/docs/2.4/mod/mod_mime.html) |
| `mod_remoteip` | [https://httpd.apache.org/docs/2.4/mod/mod_remoteip.html](https://httpd.apache.org/docs/2.4/mod/mod_remoteip.html) |
| `mod_reqtimeout` | [https://httpd.apache.org/docs/2.4/mod/mod_reqtimeout.html](https://httpd.apache.org/docs/2.4/mod/mod_reqtimeout.html) |
| `mod_rewrite` | [https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html](https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html) |
| `mod_security` | [https://modsecurity.org/](https://modsecurity.org/) |
| `mod_setenvif` | [https://httpd.apache.org/docs/2.4/mod/mod_setenvif.html](https://httpd.apache.org/docs/2.4/mod/mod_setenvif.html) |
| `mod_substitute` | [https://httpd.apache.org/docs/2.4/mod/mod_substitute.html](https://httpd.apache.org/docs/2.4/mod/mod_substitute.html) |
| `mod_userdir` | [https://httpd.apache.org/docs/2.4/mod/mod_userdir.html](https://httpd.apache.org/docs/2.4/mod/mod_userdir.html) |

I clienti non possono aggiungere moduli arbitrari, tuttavia è possibile considerare moduli aggiuntivi da includere nel prodotto in futuro. I clienti possono trovare l’elenco delle direttive disponibili per una determinata versione di Dispatcher eseguendo il comando di inserire nell&#39;elenco Consentiti convalida nell’SDK, come descritto in precedenza.

L’inserire nell&#39;elenco Consentiti contiene un elenco di direttive Apache consentite in una configurazione cliente. Se una direttiva non viene inserita nell&#39;elenco Consentiti, lo strumento registra un errore e restituisce un codice di uscita diverso da zero. Se sulla riga di comando non viene fornito alcun inserì nell&#39;elenco Consentiti (che è il modo in cui dovrebbe essere invocato), lo strumento utilizza un inserì nell&#39;elenco Consentiti predefinito che Cloud Manager utilizzerà per la convalida prima di distribuire agli ambienti Cloud.

Inoltre, esamina ulteriormente tutti i file con il pattern `conf.dispatcher.d/enabled_farms/*.farm` e verifica che:

* Non esiste una regola di filtro che utilizza l&#39;autorizzazione tramite `/glob` (per ulteriori informazioni, consulta [CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957))
* Non viene visualizzata alcuna funzione di amministrazione. Ad esempio, puoi accedere a percorsi quali `/crx/de or /system/console`.

Quando viene eseguito contro l’artefatto maven o la sottodirectory `dispatcher/src`, gli errori di convalida vengono segnalati:

```
$ validator full dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

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

## Convalida locale della sintassi di configurazione del Dispatcher in modo che apache httpd possa iniziare {#local-validation}

Una volta stabilito che la configurazione del modulo Dispatcher include solo direttive supportate, verifica che la sintassi sia corretta in modo che Apache possa avviarsi. Per eseguire il test, il docker deve essere installato localmente. E notate che non è necessario che AEM sia in funzione.

Utilizza lo script `validate.sh` come mostrato di seguito:

```
$ validate.sh src/dispatcher
Phase 1: Dispatcher validator
2019/06/19 16:02:55 No issues found
Phase 1 finished
Phase 2: httpd -t validation in docker image
Running script /docker_entrypoint.d/10-create-docroots.sh
Running script /docker_entrypoint.d/20-wait-for-backend.sh
Waiting until aemhost is available
aemhost resolves to xx.xx.xx.xx
Running script /docker_entrypoint.d/30-allowed-clients.sh
# Dispatcher configuration: (/etc/httpd/conf.dispatcher.d/dispatcher.any)
/farms {
...
}
Syntax OK
Phase 2 finished
```

Lo script esegue le seguenti operazioni:

1. Esegue la convalida dalla sezione precedente per garantire che siano incluse solo le direttive supportate. Se la configurazione non è valida, lo script non riesce.
2. Esegue il `httpd -t command` per verificare se la sintassi è corretta in modo che apache httpd possa iniziare. In caso di esito positivo, la configurazione dovrebbe essere pronta per la distribuzione.
3. Controlla che il sottoinsieme dei file di configurazione dell’SDK di Dispatcher, che sono destinati ad essere immutabili come descritto nella [sezione Struttura file](#file-structure), non sia stato modificato. Questo è un nuovo controllo, introdotto con AEM versione SDK v2021.1.4738 che include anche Dispatcher Tools versione 2.0.36. Prima di questo aggiornamento, i clienti potrebbero aver erroneamente supposto che eventuali modifiche SDK locali di tali file immutabili sarebbero state applicate anche all&#39;ambiente Cloud.

Durante l’implementazione di Cloud Manager, verrà eseguito anche il controllo `httpd -t syntax` e tutti gli errori verranno inclusi nel registro di Cloud Manager `Build Images step failure`.

## Verifica locale della configurazione di Apache e Dispatcher {#testing-apache-and-dispatcher-configuration-locally}

È inoltre possibile testare localmente la configurazione di Apache e Dispatcher. Richiede che il docker sia installato localmente e che la configurazione passi la convalida come descritto sopra.

Esegui lo strumento di convalida (nota che è diverso dal `validator.sh` menzionato in precedenza) utilizzando il parametro `-d` che restituisce una cartella con tutti i file di configurazione di Dispatcher. Quindi esegui lo script `docker_run.sh`, passando la cartella come argomento. Fornendo il numero di porta (qui: 8080) per esporre l’endpoint del Dispatcher, viene avviato un contenitore Docker, che esegue il Dispatcher con la configurazione.

```
$ validator full -d out src/dispatcher
2019/06/19 16:02:55 No issues found
$ docker_run.sh out docker.for.mac.localhost:4503 8080
Running script /docker_entrypoint.d/10-create-docroots.sh
Running script /docker_entrypoint.d/20-wait-for-backend.sh
Waiting until aemhost is available
aemhost resolves to xx.xx.xx.xx
Running script /docker_entrypoint.d/30-allowed-clients.sh
Starting httpd server
...
```

Viene avviato il Dispatcher in un contenitore con il relativo backend che punta a un&#39;istanza AEM in esecuzione sul computer Mac OS locale alla porta 4503.

## Debug della configurazione di Apache e Dispatcher {#debugging-apache-and-dispatcher-configuration}

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

## Differenze principali tra AMS Dispatcher e AEM come Cloud Service {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

Come descritto nella pagina di riferimento precedente, la configurazione di Apache e Dispatcher in AEM come Cloud Service è abbastanza simile a quella di AMS. Le principali differenze sono:

* In AEM come Cloud Service, alcune direttive Apache potrebbero non essere utilizzate (ad esempio `Listen` o `LogLevel`)
* In AEM come Cloud Service, è possibile inserire solo alcuni elementi della configurazione di Dispatcher nei file di inclusione e la loro denominazione è importante. Ad esempio, le regole di filtro da riutilizzare tra host diversi devono essere inserite in un file denominato `filters/filters.any`. Per ulteriori informazioni, consulta la pagina di riferimento .
* In AEM come Cloud Service esiste una convalida aggiuntiva per impedire che le regole di filtro scritte utilizzando `/glob` impediscano problemi di sicurezza. Poiché verrà utilizzato `deny *` anziché `allow *` (che non può essere utilizzato), i clienti trarranno vantaggio dall’esecuzione del Dispatcher localmente e dall’esecuzione di prove ed errori, guardando i registri per sapere esattamente quali percorsi i filtri del Dispatcher bloccano per poterli aggiungere.

## Linee guida per la migrazione della configurazione del dispatcher da AMS a AEM come Cloud Service

La struttura di configurazione del Dispatcher presenta differenze tra Managed Services e AEM come Cloud Service. Di seguito è riportata una guida passo passo su come migrare dalla configurazione di AMS Dispatcher versione 2 a AEM come Cloud Service.

## Come convertire una configurazione AMS in una configurazione Dispatcher di AEM as a Cloud Service

La sezione seguente fornisce istruzioni dettagliate su come convertire una configurazione AMS. Si assume
che disponi di un archivio con una struttura simile a quella descritta in [Configurazione del Dispatcher di Cloud Manager](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

### Estrarre l’archivio e rimuovere un eventuale prefisso

Estrai l’archivio in una cartella e assicurati che le sottocartelle immediate inizino con `conf`, `conf.d`,
`conf.dispatcher.d` e `conf.modules.d`. Se non lo fanno, spostali verso l&#39;alto nella gerarchia.

### Eliminare le sottocartelle e i file non utilizzati

Rimuovi le sottocartelle `conf` e `conf.modules.d`, nonché i file corrispondenti a `conf.d/*.conf`.

### Eliminare tutti gli host virtuali non relativi alla pubblicazione

Rimuovere i file host virtuali in `conf.d/enabled_vhosts` con `author`, `unhealthy`, `health`,
`lc` o `flush` nel nome. Tutti i file host virtuali in `conf.d/available_vhosts` che non sono
è possibile rimuovere anche i collegamenti a .

### Rimuovere o impostare come commento le sezioni di host virtuali che non fanno riferimento alla porta 80

Se i file host virtuali contengono ancora sezioni che fanno riferimento esclusivamente a porte diverse dalla porta 80, ad esempio:

```
<VirtualHost *:443>
...
</VirtualHost>
```

rimuovile o impostale come commenti. Le istruzioni di queste sezioni non verranno elaborate, ma se le mantieni potresti comunque finire per modificarle senza alcun effetto, il che creerebbe confusione.

### Verificare la directory rewrites

Accedi alla directory `conf.d/rewrites`.

Rimuovi i file denominati `base_rewrite.rules` e `xforwarded_forcessl_rewrite.rules` e ricorda di
rimuovere le istruzioni `Include` nei file host virtuali che vi fanno riferimento.

Se ora `conf.d/rewrites` contiene un singolo file, deve essere rinominato in `rewrite.rules` e non
dimenticare di adattare le istruzioni `Include` che fanno riferimento a tale file anche nei file host virtuali.

Se tuttavia la cartella contiene più file specifici dell’host virtuale, il loro contenuto deve essere
copiato nell&#39;istruzione `Include` che fa riferimento a essi nei file host virtuali.

### Verificare la directory variables

Accedi alla directory `conf.d/variables`.

Rimuovi tutti i file denominati `ams_default.vars` e ricorda di rimuovere le istruzioni `Include` nella versione virtuale
file host che fanno riferimento a essi.

Se ora `conf.d/variables` contiene un singolo file, deve essere rinominato in `custom.vars` e non
dimenticare di adattare le istruzioni `Include` che fanno riferimento a tale file anche nei file host virtuali.

Se tuttavia la cartella contiene più file specifici dell’host virtuale, il loro contenuto deve essere
copiato nell&#39;istruzione `Include` che fa riferimento a essi nei file host virtuali.

### Rimuovi inseriti nell&#39;elenco Consentiti

Rimuovi la cartella `conf.d/whitelists` e rimuovi le istruzioni `Include` nei file host virtuali che fanno riferimento a
alcuni file presenti nella sottocartella.

### Sostituire le variabili non più disponibili

In tutti i file host virtuali:

Rinomina `PUBLISH_DOCROOT` in `DOCROOT`
Rimuovi le sezioni che fanno riferimento a variabili denominate `DISP_ID`, `PUBLISH_FORCE_SSL` o `PUBLISH_WHITELIST_ENABLED`

### Controllare lo stato eseguendo la convalida

Esegui la convalida del Dispatcher nella directory con il sottocomando `httpd` :

```
$ validator httpd .
```

Se si verificano degli errori relativi a file di inclusione mancanti, verifica di aver rinominato correttamente tali file.

Se vengono visualizzate direttive Apache che non sono inserite nell&#39;elenco Consentiti, rimuovile.

### Eliminare tutte le farm non relative alla pubblicazione

Rimuovi i file di farm in `conf.dispatcher.d/enabled_farms` con `author`, `unhealthy`, `health`,
`lc` o `flush` nel nome. Tutti i file di farm in `conf.dispatcher.d/available_farms` che non sono
è possibile rimuovere anche i collegamenti a .

### Rinominare i file di farm

Tutte le farm in `conf.d/enabled_farms` devono essere rinominate in modo che corrispondano al pattern `*.farm`, ad esempio
il file farm denominato `customerX_farm.any` deve essere rinominato `customerX.farm`.

### Verificare la cache

Accedi alla directory `conf.dispatcher.d/cache`.

Rimuovi eventuali file con prefisso `ams_`.

Se ora `conf.dispatcher.d/cache` è vuoto, copia il file `conf.dispatcher.d/cache/rules.any`
dalla configurazione standard di Dispatcher a questa cartella. Dispatcher standard
La configurazione si trova nella cartella `src` di questo SDK. Non dimenticarti di adattare le
Istruzioni `$include` che fanno riferimento ai file di regole `ams_*_cache.any` nei file di farm
anche.

Se invece `conf.dispatcher.d/cache` ora contiene un singolo file con suffisso `_cache.any`,
deve essere rinominato in `rules.any` e non dimenticare di adattare le istruzioni `$include`
riferimento a tale file anche nei file di farm.

Se tuttavia la cartella contiene più file specifici della farm con tale pattern, il relativo contenuto
devono essere copiati nell&#39;istruzione `$include` che fa riferimento a essi nei file di farm.

Rimuovi i file con suffisso `_invalidate_allowed.any`.

Copia il file `conf.dispatcher.d/cache/default_invalidate_any` dal valore predefinito
AEM nella configurazione del Cloud Dispatcher in tale posizione.

In ciascun file di farm, rimuovi eventuali contenuti nella sezione `cache/allowedClients` e sostituiscili
con:

```
$include "../cache/default_invalidate.any"
```

### Verificare la directory clientheaders

Accedi alla directory `conf.dispatcher.d/clientheaders`.

Rimuovi eventuali file con prefisso `ams_`.

Se ora `conf.dispatcher.d/clientheaders` contiene un singolo file con suffisso `_clientheaders.any`,
deve essere rinominato in `clientheaders.any` e non dimenticare di adattare le istruzioni `$include`
riferimento a tale file anche nei file di farm.

Se tuttavia la cartella contiene più file specifici della farm con tale pattern, il relativo contenuto
devono essere copiati nell&#39;istruzione `$include` che fa riferimento a essi nei file di farm.

Copia il file `conf.dispatcher/clientheaders/default_clientheaders.any` dal valore predefinito
AEM come configurazione Cloud Service di Dispatcher in tale posizione.

In ciascun file di farm, sostituisci qualsiasi istruzione di inclusione clientheader di questo tipo:

```
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"
```

con l’istruzione:

```
$include "../clientheaders/default_clientheaders.any"
```

### Verificare la directory filters

Accedi alla directory `conf.dispatcher.d/filters`.

Rimuovi eventuali file con prefisso `ams_`.

Se ora `conf.dispatcher.d/filters` contiene un singolo file, è necessario rinominarlo in
`filters.any` e non dimenticare di adattare le istruzioni `$include` che fanno riferimento a tali istruzioni
anche nei file di farm.

Se tuttavia la cartella contiene più file specifici della farm con tale pattern, il relativo contenuto
devono essere copiati nell&#39;istruzione `$include` che fa riferimento a essi nei file di farm.

Copia il file `conf.dispatcher/filters/default_filters.any` dal valore predefinito
AEM come configurazione Cloud Service di Dispatcher in tale posizione.

In ciascun file di farm, sostituisci le istruzioni di inclusione dei filtri come segue:

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

con l’istruzione:

```
$include "../filters/default_filters.any"
```

### Verificare la directory renders

Accedi alla directory `conf.dispatcher.d/renders`.

Rimuovi tutti i file presenti nella cartella.

Copia il file `conf.dispatcher.d/renders/default_renders.any` dal valore predefinito
AEM come configurazione Cloud Service di Dispatcher in tale posizione.

In ciascun file di farm, rimuovi eventuali contenuti nella sezione `renders` e sostituiscili
con:

```
$include "../renders/default_renders.any"
```

### Verificare la directory virtualhosts

Rinomina la directory `conf.dispatcher.d/vhosts` in `conf.dispatcher.d/virtualhosts` e inseriscila.

Rimuovi eventuali file con prefisso `ams_`.

Se ora `conf.dispatcher.d/virtualhosts` contiene un singolo file, è necessario rinominarlo in
`virtualhosts.any` e non dimenticare di adattare le istruzioni `$include` che fanno riferimento a tali istruzioni
anche nei file di farm.

Se tuttavia la cartella contiene più file specifici della farm con tale pattern, il relativo contenuto
devono essere copiati nell&#39;istruzione `$include` che fa riferimento a essi nei file di farm.

Copia il file `conf.dispatcher/virtualhosts/default_virtualhosts.any` dal valore predefinito
AEM come configurazione Cloud Service di Dispatcher in tale posizione.

In ciascun file di farm, sostituisci le istruzioni di inclusione dei filtri come segue:

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

con l’istruzione:

```
$include "../virtualhosts/default_virtualhosts.any"
```

### Controllare lo stato eseguendo la convalida

Esegui il AEM come convalida del Dispatcher di Cloud Service nella directory, con il sottocomando `dispatcher` :

```
$ validator dispatcher .
```

Se si verificano degli errori relativi a file di inclusione mancanti, verifica di aver rinominato correttamente tali file.

Se vengono visualizzati errori relativi a una variabile `PUBLISH_DOCROOT` non definita, rinominala in `DOCROOT`.

Per qualsiasi altro errore, consulta la sezione Risoluzione di problemi della documentazione relativa allo strumento di convalida.

### Verifica la configurazione con un’implementazione locale (richiede l’installazione di Docker)

Utilizzando lo script `docker_run.sh` nel AEM come strumenti del Dispatcher di Cloud Service, puoi verificare che
la configurazione non contiene altri errori che potrebbero verificarsi solo in
distribuzione:

### Passaggio 1: Genera informazioni di distribuzione con la convalida

```
validator full -d out .
```


In questo modo viene convalidata la configurazione completa e vengono generate le informazioni di implementazione in/`out`

### Passaggio 2: Avvia Dispatcher in un’immagine docker con tali informazioni di distribuzione

Con il server di pubblicazione AEM in esecuzione sul computer macOS, in ascolto sulla porta 4503,
puoi avviare Dispatcher davanti a tale server come segue:

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

In questo modo verrà avviato il contenitore e Apache sarà esposto sulla porta locale 8080.

### Utilizza la nuova configurazione del Dispatcher

Congratulazioni! Se la convalida non segnala più alcun problema e la
il contenitore docker si avvia senza errori o avvisi, sei
pronto per spostare la configurazione in una sottodirectory `dispatcher/src`
dell’archivio git.

**I clienti che utilizzano la versione 1 della configurazione di AMS Dispatcher devono contattare il supporto clienti per aiutarli a migrare dalla versione 1 alla versione 2, in modo da seguire le istruzioni di cui sopra.**
