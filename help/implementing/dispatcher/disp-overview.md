---
title: Dispatcher nel cloud
description: 'Dispatcher nel cloud '
translation-type: tm+mt
source-git-commit: 4d58ccf972f5bf2a48b228755f93166c17bcb4b0
workflow-type: tm+mt
source-wordcount: '4050'
ht-degree: 9%

---


# Dispatcher nel cloud {#Dispatcher-in-the-cloud}

## Configurazione e test Apache e Dispatcher {#apache-and-dispatcher-configuration-and-testing}

Questa sezione descrive come strutturare il AEM come configurazioni di Cloud Service Apache e Dispatcher, nonché come convalidarlo ed eseguirlo localmente prima di distribuirlo negli ambienti Cloud. Inoltre, descrive il debug negli ambienti Cloud. Per ulteriori informazioni sul dispatcher, consultare la [documentazione del dispatcher di AEM](https://docs.adobe.com/content/help/it-IT/experience-manager-dispatcher/using/dispatcher.html).

>[!NOTE]
>Gli utenti Windows dovranno utilizzare Windows 10 Professional o altre distribuzioni che supportano Docker. Questo è un prerequisito per l&#39;esecuzione e il debug del dispatcher su un computer locale. Le sezioni seguenti includono comandi che utilizzano le versioni Mac o Linux dell&#39;SDK, ma l&#39;SDK di Windows può essere utilizzato in modo simile.

## Strumenti Dispatcher {#dispatcher-sdk}

Gli strumenti Dispatcher fanno parte del AEM generale come SDK per Cloud Service e forniscono:

* Una struttura di file di vaniglia contenente i file di configurazione da includere in un progetto maven per dispatcher.
* Un pool per consentire ai clienti di verificare che la configurazione del dispatcher includa solo AEM come direttive supportate dal Cloud Service.        Inoltre, il tooling convalida che la sintassi sia corretta, in modo che apache possa avviarsi correttamente.
* Un&#39;immagine Docker che riproduce localmente il dispatcher.

## Download ed estrazione degli strumenti {#extracting-the-sdk}

Gli strumenti Dispatcher, parte del [AEM come Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md), possono essere scaricati da un file zip sul portale [Distribuzione software](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html). Qualsiasi nuova configurazione disponibile nella nuova versione di dispatcher Tools può essere utilizzata per distribuire agli ambienti Cloud in cui è in esecuzione la versione di AEM nel cloud o versioni successive.

Decomprimete l&#39;SDK, che include gli strumenti Dispatcher per MacOS/Linux e Windows.

**Per macOS/Linux**, esegui l’artifact dello strumento dispatcher ed eseguilo. Estrarre automaticamente i file Dispatcher Tools sotto la directory in cui è stato memorizzato (dove `version` è la versione degli strumenti del dispatcher).

```bash
$ chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
$ ./aem-sdk-dispatcher-tools-<version>-unix.sh
Verifying archive integrity...  100%   All good.
Uncompressing aem-sdk-dispatcher-tools-<version>-unix.sh 100%
```

**Per Windows**, estrarre l&#39;archivio ZIP Dispatcher Tooling.

## Struttura file {#file-structure}

La struttura della sottocartella dispatcher del progetto è descritta di seguito e deve essere copiata nella cartella del dispatcher del progetto maven:

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

I file seguenti sono personalizzabili e verranno trasferiti nell&#39;istanza di Cloud al momento della distribuzione:

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

Potete avere uno o più di questi file. Contiene `<VirtualHost>` voci che corrispondono ai nomi host e consentono ad Apache di gestire ogni traffico di dominio con regole diverse. I file vengono creati nella directory `available_vhosts` e attivati con un collegamento simbolico nella directory `enabled_vhosts`. Dai file `.vhost` saranno inclusi altri file come le riscritture e le variabili.

* `conf.d/rewrites/rewrite.rules`

Questo file è incluso all&#39;interno dei `.vhost` file. Contiene un set di regole di riscrittura per `mod_rewrite`.

>[!NOTE]
>
>Al momento, è necessario utilizzare un singolo file di riscrittura anziché file specifici del sito. La dimensione del file deve essere inferiore a 1 MB.

* `conf.d/variables/custom.vars`

Questo file è incluso all&#39;interno dei `.vhost` file. In questa posizione potete inserire le definizioni per le variabili Apache.

* `conf.d/variables/global.vars`

Questo file è incluso dall&#39;interno del file `dispatcher_vhost.conf`. È possibile modificare il livello del dispatcher e riscrivere di nuovo il livello di registro in questo file.

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

È possibile avere uno o più di questi file, che contengono farm che corrispondono ai nomi host e consentono al modulo dispatcher di gestire ogni farm con regole diverse. I file vengono creati nella directory `available_farms` e attivati con un collegamento simbolico nella directory `enabled_farms`. Dai file `.farm` saranno inclusi altri file come filtri, regole della cache e altri.

* `conf.dispatcher.d/cache/rules.any`

Questo file è incluso all&#39;interno dei `.farm` file. Specifica le preferenze di memorizzazione nella cache.

* `conf.dispatcher.d/clientheaders/clientheaders.any`

Questo file è incluso all&#39;interno dei `.farm` file. Specifica quali intestazioni di richiesta devono essere inoltrate al back-end.

* `conf.dispatcher.d/filters/filters.any`

Questo file è incluso all&#39;interno dei `.farm` file. Ha una serie di regole che modificano il traffico da filtrare e non arrivare al backend.

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

Questo file è incluso all&#39;interno dei `.farm` file. Contiene un elenco di nomi host o di percorsi URI che devono essere associati dalla corrispondenza di tipo GSM. Questo determina il backend da utilizzare per distribuire una richiesta.

I file di cui sopra fanno riferimento ai file di configurazione immutabili elencati di seguito. Le modifiche ai file immutabili non verranno elaborate dai dispatcher negli ambienti Cloud.

**File di configurazione immutabili**

Questi file fanno parte del framework di base e applicano gli standard e le best practice. I file sono considerati immutabili perché modificarli o eliminarli localmente non avranno alcun impatto sulla distribuzione, in quanto non verranno trasferiti nell’istanza di Cloud.

Si consiglia che i file di cui sopra facciano riferimento ai file immutabili elencati di seguito, seguiti da eventuali istruzioni o sostituzioni aggiuntive. Quando la configurazione del dispatcher viene distribuita in un ambiente cloud, verrà utilizzata la versione più recente dei file immutabili, indipendentemente dalla versione utilizzata nello sviluppo locale.

* `conf.d/available_vhosts/default.vhost`

Contiene un esempio di host virtuale. Per l’host virtuale, create una copia del file, personalizzatela, passate a `conf.d/enabled_vhosts` e create un collegamento simbolico alla copia personalizzata.

* `conf.d/dispatcher_vhost.conf`

Parte del framework di base, utilizzata per illustrare il modo in cui gli host virtuali e le variabili globali sono inclusi.

* `conf.d/rewrites/default_rewrite.rules`

Regole di riscrittura predefinite adatte a un progetto standard. Se avete bisogno di personalizzazione, modificate `rewrite.rules`. Nella personalizzazione, potete comunque includere prima le regole predefinite, se sono adatte alle vostre esigenze.

* `conf.dispatcher.d/available_farms/default.farm`

Contiene una farm di dispatcher di esempio. Per la vostra farm, create una copia di questo file, personalizzatelo, andate a `conf.d/enabled_farms` e create un collegamento simbolico alla vostra copia personalizzata.

* `conf.dispatcher.d/cache/default_invalidate.any`

Parte del framework di base, viene generato all&#39;avvio. **obbligatorio** per includere questo file in ogni farm definita, nella sezione `cache/allowedClients`.

* `conf.dispatcher.d/cache/default_rules.any`

Regole predefinite per la cache adatte a un progetto standard. Se avete bisogno di personalizzazione, modificate `conf.dispatcher.d/cache/rules.any`. Nella personalizzazione, potete comunque includere prima le regole predefinite, se sono adatte alle vostre esigenze.

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

Intestazioni di richiesta predefinite da inoltrare al back-end, adatte a un progetto standard. Se avete bisogno di personalizzazione, modificate `clientheaders.any`. Nella personalizzazione, potete comunque includere per primo le intestazioni di richiesta predefinite, a seconda delle vostre esigenze.

* `conf.dispatcher.d/dispatcher.any`

Parte del framework di base, utilizzata per illustrare il modo in cui vengono incluse le farm dispatcher.

* `conf.dispatcher.d/filters/default_filters.any`

Filtri predefiniti adatti per un progetto standard. Se avete bisogno di personalizzazione, modificate `filters.any`. Nella personalizzazione, potete comunque includere prima i filtri predefiniti, a seconda delle vostre esigenze.

* `conf.dispatcher.d/renders/default_renders.any`

Parte del framework di base, questo file viene generato all&#39;avvio. **obbligatorio** per includere questo file in ogni farm definita, nella sezione `renders`.

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

Globo host predefinito adatto a un progetto standard. Se avete bisogno di personalizzazione, modificate `virtualhosts.any`. Nella personalizzazione, non devi includere la globbing host predefinita, in quanto corrisponde a **ogni** richiesta in arrivo.

>[!NOTE]
>
>Il AEM come archetipo Cloud Service maven genererà la stessa struttura di file di configurazione del dispatcher.

Le sezioni seguenti descrivono come convalidare la configurazione localmente in modo che possa superare il gate di qualità associato in Cloud Manager durante la distribuzione di una versione interna.

## Convalida locale delle direttive supportate nella configurazione del dispatcher {#local-validation-of-dispatcher-configuration}

Lo strumento di convalida è disponibile nell&#39;SDK in `bin/validator` come binario Mac OS, Linux o Windows, consentendo ai clienti di eseguire la stessa convalida che Cloud Manager eseguirà durante la creazione e la distribuzione di una versione.

Viene richiamato come: `validator full [-d folder] [-w allowlist] zip-file | src folder`

Lo strumento verifica che la configurazione del dispatcher utilizzi le direttive appropriate supportate da AEM come servizio Cloud, eseguendo la scansione di tutti i file con il pattern `conf.d/enabled_vhosts/*.vhost`. Le direttive consentite nei file di configurazione Apache possono essere elencate eseguendo il comando di inserì nell&#39;elenco Consentiti  convalida:

```
$ validator allowlist
Cloud manager validator 2.0.4
 
Allowlisted directives:
  <Directory>
  ...
  
```

La tabella seguente mostra i moduli apache supportati:

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

I clienti non possono aggiungere moduli arbitrari, ma in futuro potrebbero essere presi in considerazione moduli aggiuntivi per l&#39;inclusione nel prodotto. I clienti possono trovare l&#39;elenco delle direttive disponibili per una determinata versione del dispatcher eseguendo il comando di inserì nell&#39;elenco Consentiti  convalida nell&#39;SDK, come descritto in precedenza.

Il inserire nell&#39;elenco Consentiti  contiene un elenco di direttive Apache consentite in una configurazione cliente. Se una direttiva non viene inserita nell&#39;elenco Consentiti, lo strumento registra un errore e restituisce un codice di uscita diverso da zero. Se non viene  inserì nell&#39;elenco Consentiti sulla riga di comando (che è il modo in cui dovrebbe essere invocato), lo strumento utilizza un inserire nell&#39;elenco Consentiti  predefinito che Cloud Manager utilizzerà per la convalida prima della distribuzione negli ambienti Cloud.

Inoltre, analizza ulteriormente tutti i file con il pattern `conf.dispatcher.d/enabled_farms/*.farm` e verifica che:

* Nessuna regola del filtro utilizzata per l&#39;utilizzo tramite `/glob` (per ulteriori informazioni, vedere [CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957))
* Nessuna funzione di amministrazione esposta. Ad esempio, l&#39;accesso a percorsi come `/crx/de or /system/console`.

Se eseguito contro il tuo artifact di superficie o la tua sottodirectory `dispatcher/src`, segnalerà gli errori di convalida:

```
$ validator full dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

Lo strumento di convalida segnala solo l&#39;uso vietato di direttive Apache che non sono state inserite nell&#39;elenco Consentiti. Non segnala problemi sintattici o semantici con la configurazione Apache, in quanto tali informazioni sono disponibili solo per i moduli Apache in un ambiente in esecuzione.

Di seguito sono illustrate le tecniche di risoluzione dei problemi per il debug di errori di convalida comuni generati dallo strumento:

**impossibile individuare una  `conf.dispatcher.d` sottocartella nell&#39;archivio**

L’archivio deve contenere le cartelle `conf.d` e `conf.dispatcher.d`. Nota: **non** utilizzare il
prefisso `etc/httpd` nell’archivio.

**impossibile trovare alcuna fattoria in`conf.dispatcher.d/enabled_farms`**

Le farm abilitate devono trovarsi nella sottocartella indicata.

**il file incluso (...) deve essere denominato: ...**

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

Nella configurazione della farm sono presenti quattro sezioni in cui è possibile includere il proprio file: `/clientheaders`, `filters`, `/rules` nella sezione `/cache` e `/virtualhosts`. I file inclusi devono essere denominati come segue:

| Sezione | Includi nome file |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

In alternativa, è possibile includere la versione **predefinita** di tali file, i cui nomi sono preceduti dalla parola `default_`, ad esempio `../filters/default_filters.any`.

**include l&#39;istruzione in (...), al di fuori di qualsiasi posizione nota: ...**

Oltre alle sei sezioni menzionate nei paragrafi precedenti, non è consentito
per utilizzare l&#39;istruzione `$include`, ad esempio, il seguente errore genererebbe:

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**i client/i rendering consentiti non sono inclusi da: ...**

Questo errore viene generato quando non si specifica un&#39;inclusione per `/renders` e `/allowedClients` nella sezione `/cache`. Consulta
**il file incluso (...) deve essere denominato: ...** per ulteriori informazioni.

**il filtro non deve usare il pattern GSM per consentire le richieste**

Non è sicuro consentire le richieste con una regola di stile `/glob`, che viene confrontata con l&#39;intera riga di richiesta, ad esempio

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

Questa istruzione ha lo scopo di consentire le richieste per i file `css`, ma consente anche le richieste per **qualsiasi risorsa** seguita dalla stringa di query `?a=.css`. È pertanto vietato utilizzare tali filtri (cfr. anche CVE-2016-0957).

**il file incluso (...) non corrisponde ad alcun file noto**

Nella configurazione dell&#39;host virtuale Apache sono disponibili due tipi di file che possono essere specificati come include: riscrittura e variabili.
I file inclusi devono essere denominati come segue:

| Tipo | Includi nome file |
|-----------|---------------------------------|
| Riscrittura | `conf.d/rewrites/rewrite.rules` |
| Variabili | `conf.d/variables/custom.vars` |

In alternativa, è possibile includere la versione **predefinita** delle regole di riscrittura, il cui nome è `conf.d/rewrites/default_rewrite.rules`.
Si noti che non esiste una versione predefinita dei file delle variabili.

**Rilevato layout di configurazione obsoleto, abilitazione della modalità di compatibilità**

Questo messaggio indica che la configurazione ha un layout obsoleto della versione 1, contenente un
Configurazione Apache e file con `ams_` prefissi. Anche se questo è ancora supportato per le versioni precedenti
compatibilità per passare al nuovo layout.

## Convalida locale della sintassi di configurazione del dispatcher in modo che apache httpd possa avviare {#local-validation}

Una volta stabilito che la configurazione del modulo dispatcher include solo direttive supportate, è necessario verificare che la sintassi sia corretta in modo che apache possa avviarsi. Per testarlo, il docker deve essere installato localmente. E notate che non è necessario AEM essere in funzione.

Utilizzate lo script `validate.sh` come illustrato di seguito:

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

1. Esegue la convalida dalla sezione precedente per garantire che siano incluse solo le direttive supportate. Se la configurazione non è valida, lo script non riuscirà.
2. Viene eseguito il `httpd -t command` per verificare se la sintassi è corretta in modo che apache possa iniziare. In caso di esito positivo, la configurazione dovrebbe essere pronta per la distribuzione

Durante la distribuzione di Cloud Manager, verrà eseguito anche il controllo `httpd -t syntax`, che verrà incluso nel registro di Cloud Manager `Build Images step failure`.

## Verifica della configurazione Apache e Dispatcher localmente {#testing-apache-and-dispatcher-configuration-locally}

È inoltre possibile testare localmente la configurazione Apache e Dispatcher. Richiede che il docker venga installato localmente e che la configurazione superi la convalida come descritto in precedenza.

Eseguire lo strumento di convalida (notare che è diverso dal `validator.sh` indicato in precedenza), utilizzando il parametro `-d` che produce una cartella con tutti i file di configurazione del dispatcher. Eseguire quindi lo script `docker_run.sh`, trasmettendo la cartella come argomento. Fornendo il numero di porta (qui: 8080) per esporre l&#39;endpoint del dispatcher, viene avviato un contenitore Docker che esegue il dispatcher con la configurazione.

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

Questo avvia il dispatcher in un contenitore con il relativo backend che punta a un&#39;istanza AEM in esecuzione sul computer Mac OS locale alla porta 4503.

## Debug della configurazione Apache e Dispatcher {#debugging-apache-and-dispatcher-configuration}

La seguente strategia può essere utilizzata per aumentare l&#39;output di registro per il modulo dispatcher e vedere i risultati della valutazione `RewriteRule` sia in ambiente locale che in ambiente cloud.

I livelli di registro per tali moduli sono definiti dalle variabili `DISP_LOG_LEVEL` e `REWRITE_LOG_LEVEL`. Possono essere impostati nel file `conf.d/variables/global.vars`. La sua parte relativa segue:

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

Quando si esegue il dispatcher localmente, i file di registro vengono stampati direttamente nell&#39;output del terminale. Nella maggior parte dei casi, si desidera che questi registri siano in DEBUG, che può essere fatto passando il livello Debug come parametro quando si esegue Docker. Esempio: `DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`.

I registri per gli ambienti cloud sono esposti tramite il servizio di registrazione disponibile in Cloud Manager.

## Diverse configurazioni del dispatcher per ambiente {#different-dispatcher-configurations-per-environment}

Al momento, la stessa configurazione del dispatcher viene applicata a tutti i AEM come ambienti di Cloud Service. Il runtime dispone di una variabile di ambiente `ENVIRONMENT_TYPE` che contiene la modalità di esecuzione corrente (dev, stage o prod) e una definizione. La definizione può essere `ENVIRONMENT_DEV`, `ENVIRONMENT_STAGE` o `ENVIRONMENT_PROD`. Nella configurazione Apache, la variabile può essere utilizzata direttamente in un&#39;espressione. In alternativa, è possibile utilizzare la definizione per creare logica:

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

Nella configurazione Dispatcher, è disponibile la stessa variabile di ambiente. Se è necessaria una maggiore logica, definite le variabili come illustrato nell’esempio precedente e utilizzatele nella sezione di configurazione del dispatcher:

```
/virtualhosts {
  { "${VIRTUALHOST}" }
}
```

Quando si esegue il test della configurazione localmente, è possibile simulare diversi tipi di ambiente passando la variabile `DISP_RUN_MODE` allo script `docker_run.sh` direttamente:

```
$ DISP_RUN_MODE=stage docker_run.sh out docker.for.mac.localhost:4503 8080
```

La modalità di esecuzione predefinita quando non viene passato un valore per DISP_RUN_MODE è &quot;dev&quot;.
Per un elenco completo delle opzioni e delle variabili disponibili, eseguire lo script `docker_run.sh` senza argomenti.

## Visualizzazione della configurazione del dispatcher in uso da parte del contenitore Docker {#viewing-dispatcher-configuration-in-use-by-docker-container}

Con configurazioni specifiche per l&#39;ambiente, può essere difficile determinare l&#39;aspetto della configurazione effettiva del dispatcher. Dopo aver avviato il contenitore docker con `docker_run.sh`, è possibile scaricarlo come segue:

* Determinare l&#39;ID del contenitore docker in uso:

```
$ docker ps
CONTAINER ID       IMAGE
d75fbd23b29        adobe/aem-ethos/dispatcher-publish:...
```

* Esegui la riga di comando seguente con l&#39;ID contenitore:

```
$ docker exec d75fbd23b29 httpd-test
# Dispatcher configuration: (/etc/httpd/conf.dispatcher.d/dispatcher.any)
/farms {
  /publishfarm {
    /clientheaders {
...
```

## Differenze principali tra il dispatcher AMS e AEM come Cloud Service {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

Come descritto nella pagina di riferimento precedente, la configurazione Apache e Dispatcher in AEM come Cloud Service è abbastanza simile a quella di AMS. Le principali differenze sono:

* In AEM come Cloud Service, alcune direttive Apache non possono essere utilizzate (ad esempio `Listen` o `LogLevel`)
* In AEM come Cloud Service, solo alcuni elementi della configurazione del Dispatcher possono essere inseriti include file e la loro denominazione è importante. Ad esempio, le regole del filtro che si desidera riutilizzare tra host diversi devono essere inserite in un file denominato `filters/filters.any`. Per ulteriori informazioni, consultate la pagina di riferimento.
* In AEM come Cloud Service esiste una convalida aggiuntiva per impedire che le regole del filtro scritte utilizzando `/glob` impediscano problemi di sicurezza. Poiché `deny *` verrà utilizzato invece di `allow *` (che non può essere utilizzato), i clienti potranno eseguire il Dispatcher localmente ed eseguire tentativi ed errori, controllando i registri per sapere esattamente quali percorsi i filtri del Dispatcher stanno bloccando per poter aggiungere tali percorsi.

## Linee guida per la migrazione della configurazione del dispatcher da AMS a AEM come Cloud Service

La struttura di configurazione del dispatcher presenta differenze tra Managed Services e AEM come Cloud Service. Presentato di seguito, è una guida dettagliata su come migrare dalla configurazione di AMS Dispatcher versione 2 a AEM come Cloud Service.

## Come convertire un AMS in un AEM come configurazione del dispatcher di servizi cloud

La sezione seguente fornisce istruzioni dettagliate su come convertire una configurazione AMS. Prende in considerazione
di disporre di un archivio con una struttura simile a quella descritta in [Configurazione dispatcher di Cloud Manager](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

### Estrarre l’archivio e rimuovere un eventuale prefisso

Estrarre l&#39;archivio in una cartella e assicurarsi che le sottocartelle immediate inizino con `conf`, `conf.d`,
`conf.dispatcher.d` e `conf.modules.d`. In caso contrario, spostateli nella gerarchia.

### Eliminare le sottocartelle e i file non utilizzati

Rimuovere le sottocartelle `conf` e `conf.modules.d`, nonché i file corrispondenti a `conf.d/*.conf`.

### Eliminare tutti gli host virtuali non relativi alla pubblicazione

Rimuovere qualsiasi file host virtuale in `conf.d/enabled_vhosts` con `author`, `unhealthy`, `health`,
`lc` o `flush` nel nome. Tutti i file host virtuali in `conf.d/available_vhosts` che non sono
collegato a può essere rimosso anche.

### Rimuovere o impostare come commento le sezioni di host virtuali che non fanno riferimento alla porta 80

Se i file host virtuali contengono ancora sezioni che fanno riferimento esclusivamente a porte diverse dalla porta 80, ad esempio

```
<VirtualHost *:443>
...
</VirtualHost>
```

rimuovile o impostale come commenti. Le istruzioni di queste sezioni non verranno elaborate, ma se le mantieni potresti comunque finire per modificarle senza alcun effetto, il che creerebbe confusione.

### Verificare la directory rewrites

Immettere la directory `conf.d/rewrites`.

Rimuovere qualsiasi file denominato `base_rewrite.rules` e `xforwarded_forcessl_rewrite.rules` e ricordare
rimuovere le istruzioni `Include` nei file host virtuali che vi fanno riferimento.

Se ora `conf.d/rewrites` contiene un singolo file, è necessario rinominarlo in `rewrite.rules` e non
dimenticare di adattare le istruzioni `Include` relative a tale file anche nei file host virtuali.

Tuttavia, se la cartella contiene più file specifici dell&#39;host virtuale, il relativo contenuto deve essere
copiato nell&#39;istruzione `Include` che li fa riferimento nei file host virtuali.

### Verificare la directory variables

Immettere la directory `conf.d/variables`.

Rimuovere qualsiasi file denominato `ams_default.vars` e ricordare di rimuovere le istruzioni `Include` nella
file host che fanno riferimento a tali file.

Se ora `conf.d/variables` contiene un singolo file, è necessario rinominarlo in `custom.vars` e non
dimenticare di adattare le istruzioni `Include` relative a tale file anche nei file host virtuali.

Tuttavia, se la cartella contiene più file specifici dell&#39;host virtuale, il relativo contenuto deve essere
copiato nell&#39;istruzione `Include` che li fa riferimento nei file host virtuali.

### Rimuovere  inseriti nell&#39;elenco Consentiti

Rimuovere la cartella `conf.d/whitelists` e rimuovere le istruzioni `Include` nei file host virtuali che fanno riferimento a
alcuni file in quella sottocartella.

### Sostituire le variabili non più disponibili

In tutti i file host virtuali:

Rinomina `PUBLISH_DOCROOT` in `DOCROOT`
Rimuovere le sezioni relative alle variabili denominate `DISP_ID`, `PUBLISH_FORCE_SSL` o `PUBLISH_WHITELIST_ENABLED`

### Controllare lo stato eseguendo la convalida

Eseguire il dispatcher validator nella directory, con il sottocomando `httpd`:

```
$ validator httpd .
```

Se si verificano degli errori relativi a file di inclusione mancanti, verifica di aver rinominato correttamente tali file.

Se vengono visualizzate delle direttive Apache che non vengono inserite nell&#39;elenco Consentiti, rimuoverle.

### Eliminare tutte le farm non relative alla pubblicazione

Rimuovere qualsiasi file farm in `conf.dispatcher.d/enabled_farms` con `author`, `unhealthy`, `health`,
`lc` o `flush` nel nome. Tutti i file della farm in `conf.dispatcher.d/available_farms` che non sono
collegato a può essere rimosso anche.

### Rinominare i file di farm

Tutte le farm in `conf.d/enabled_farms` devono essere rinominate in modo da corrispondere al pattern `*.farm`, per esempio un
il file della farm denominato `customerX_farm.any` deve essere rinominato `customerX.farm`.

### Verificare la cache

Immettere la directory `conf.dispatcher.d/cache`.

Rimuovi eventuali file con prefisso `ams_`.

Se `conf.dispatcher.d/cache` è ora vuoto, copiate il file `conf.dispatcher.d/cache/rules.any`
dalla configurazione del dispatcher standard a questa cartella. dispatcher standard
La configurazione si trova nella cartella `src` di questo SDK. Non dimenticare di adattare le
`$include` istruzioni relative ai file di regola `ams_*_cache.any` nei file della farm
anche.

Se invece `conf.dispatcher.d/cache` ora contiene un singolo file con suffisso `_cache.any`,
deve essere rinominato in `rules.any` e non dimenticare di adattare le istruzioni `$include`
fare riferimento a tale file anche nei file della farm.

Se la cartella contiene tuttavia più file specifici della farm con tale pattern, il relativo contenuto
deve essere copiata nell&#39;istruzione `$include` che fa riferimento ad esse nei file della farm.

Rimuovere qualsiasi file con suffisso `_invalidate_allowed.any`.

Copiare il file `conf.dispatcher.d/cache/default_invalidate_any` dall&#39;impostazione predefinita
AEM nella configurazione del dispatcher di Cloud in tale posizione.

In ciascun file della farm, rimuovete qualsiasi contenuto nella sezione `cache/allowedClients` e sostituitelo
con:

```
$include "../cache/default_invalidate.any"
```

### Verificare la directory clientheaders

Immettere la directory `conf.dispatcher.d/clientheaders`.

Rimuovi eventuali file con prefisso `ams_`.

Se ora `conf.dispatcher.d/clientheaders` contiene un singolo file con suffisso `_clientheaders.any`,
deve essere rinominato in `clientheaders.any` e non dimenticare di adattare le istruzioni `$include`
fare riferimento a tale file anche nei file della farm.

Se la cartella contiene tuttavia più file specifici della farm con tale pattern, il relativo contenuto
deve essere copiata nell&#39;istruzione `$include` che fa riferimento ad esse nei file della farm.

Copiare il file `conf.dispatcher/clientheaders/default_clientheaders.any` dall&#39;impostazione predefinita
AEM come configurazione del dispatcher di Cloud Service in quella posizione.

In ciascun file di farm, sostituisci le istruzioni di inclusione clientheader di questo tipo:

```
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"
```

con l’istruzione:

```
$include "../clientheaders/default_clientheaders.any"
```

### Verificare la directory filters

Immettere la directory `conf.dispatcher.d/filters`.

Rimuovi eventuali file con prefisso `ams_`.

Se ora `conf.dispatcher.d/filters` contiene un singolo file, è necessario rinominarlo in
`filters.any` e non dimenticare di adattare le istruzioni `$include` relative a tale
anche nei file della farm.

Se la cartella contiene tuttavia più file specifici della farm con tale pattern, il relativo contenuto
deve essere copiata nell&#39;istruzione `$include` che fa riferimento ad esse nei file della farm.

Copiare il file `conf.dispatcher/filters/default_filters.any` dall&#39;impostazione predefinita
AEM come configurazione del dispatcher di Cloud Service in quella posizione.

In ciascun file di farm, sostituisci eventuali istruzioni di inclusione di questo tipo:

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

con l’istruzione:

```
$include "../filters/default_filters.any"
```

### Verificare la directory renders

Immettere la directory `conf.dispatcher.d/renders`.

Rimuovi tutti i file presenti nella cartella.

Copiare il file `conf.dispatcher.d/renders/default_renders.any` dall&#39;impostazione predefinita
AEM come configurazione del dispatcher di Cloud Service in quella posizione.

In ciascun file della farm, rimuovete qualsiasi contenuto nella sezione `renders` e sostituitelo
con:

```
$include "../renders/default_renders.any"
```

### Verificare la directory virtualhosts

Rinominare la directory `conf.dispatcher.d/vhosts` in `conf.dispatcher.d/virtualhosts` e immetterla.

Rimuovi eventuali file con prefisso `ams_`.

Se ora `conf.dispatcher.d/virtualhosts` contiene un singolo file, è necessario rinominarlo in
`virtualhosts.any` e non dimenticare di adattare le istruzioni `$include` relative a tale
anche nei file della farm.

Se la cartella contiene tuttavia più file specifici della farm con tale pattern, il relativo contenuto
deve essere copiata nell&#39;istruzione `$include` che fa riferimento ad esse nei file della farm.

Copiare il file `conf.dispatcher/virtualhosts/default_virtualhosts.any` dall&#39;impostazione predefinita
AEM come configurazione del dispatcher di Cloud Service in quella posizione.

In ciascun file di farm, sostituisci eventuali istruzioni di inclusione di questo tipo:

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

con l’istruzione:

```
$include "../virtualhosts/default_virtualhosts.any"
```

### Controllare lo stato eseguendo la convalida

Eseguire il AEM come convalida del dispatcher di Cloud Service nella directory, con il sottocomando `dispatcher`:

```
$ validator dispatcher .
```

Se si verificano degli errori relativi a file di inclusione mancanti, verifica di aver rinominato correttamente tali file.

Se vengono visualizzati errori relativi a una variabile `PUBLISH_DOCROOT` non definita, rinominala in `DOCROOT`.

Per qualsiasi altro errore, consulta la sezione Risoluzione di problemi della documentazione relativa allo strumento di convalida.

### Verificare la configurazione con una distribuzione locale (richiede l&#39;installazione di Docker)

Utilizzando lo script `docker_run.sh` nel AEM come strumenti del dispatcher di Cloud Service, è possibile verificare che
la configurazione non contiene altri errori che vengono visualizzati solo in
implementazione:

### Passaggio 1: Generazione di informazioni sulla distribuzione con il validatore

```
validator full -d out .
```


In questo modo viene convalidata la configurazione completa e vengono generate le informazioni di implementazione in/`out`

### Passaggio 2: Avviare il dispatcher in un&#39;immagine docker con tali informazioni di distribuzione

Con il server di pubblicazione AEM in esecuzione sul computer macOS, in ascolto sulla porta 4503, puoi avviare il dispatcher prima di tale server come segue:

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

In questo modo verrà avviato il contenitore e Apache sarà esposto sulla porta locale 8080.

### Utilizza la nuova configurazione dispatcher

Congratulazioni! Se il validatore non segnala più alcun problema e la
Il contenitore docker viene avviato senza errori o avvertenze.
pronta per spostare la configurazione in una sottodirectory `dispatcher/src`
del repository Git.

**I clienti che utilizzano la configurazione AMS Dispatcher versione 1 devono contattare l&#39;assistenza clienti per effettuare la migrazione dalla versione 1 alla versione 2, in modo da seguire le istruzioni riportate sopra.**
