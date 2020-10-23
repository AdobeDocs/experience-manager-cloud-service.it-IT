---
title: Dispatcher nel cloud
description: 'Dispatcher nel cloud '
translation-type: tm+mt
source-git-commit: 95e89bc665ee228da0a25a57a3a917a6b4c379ad
workflow-type: tm+mt
source-wordcount: '4073'
ht-degree: 9%

---


# Dispatcher nel cloud {#Dispatcher-in-the-cloud}

## Apache and Dispatcher configuration and testing {#apache-and-dispatcher-configuration-and-testing}

Questa sezione descrive come strutturare il AEM come configurazioni di Cloud Service Apache e Dispatcher, nonché come convalidarlo ed eseguirlo localmente prima di distribuirlo negli ambienti Cloud. Inoltre, descrive il debug negli ambienti Cloud. Per ulteriori informazioni sul dispatcher, consulta la [AEM documentazione](https://docs.adobe.com/content/help/it-IT/experience-manager-dispatcher/using/dispatcher.html)del dispatcher.

>[!NOTE]
>
>Gli utenti Windows dovranno utilizzare Windows 10 Professional o altre distribuzioni che supportano Docker. Questo è un prerequisito per l&#39;esecuzione e il debug del dispatcher su un computer locale. Le sezioni seguenti includono comandi che utilizzano le versioni Mac o Linux dell&#39;SDK, ma l&#39;SDK di Windows può essere utilizzato in modo simile.

>[!WARNING]
>
>Utenti Windows: la versione corrente di AEM come Cloud Service di strumenti Dispatcher locali (v2.0.20) è incompatibile con Windows. Contattate [Adobe](https://daycare.day.com/home.html) per ricevere gli aggiornamenti sulla compatibilità di Windows.

## Strumenti Dispatcher {#dispatcher-sdk}

Gli strumenti Dispatcher fanno parte del AEM generale come SDK per Cloud Service e forniscono:

* Una struttura di file di vaniglia contenente i file di configurazione da includere in un progetto maven per dispatcher.
* Un pool per consentire ai clienti di verificare che la configurazione del dispatcher includa solo AEM come direttive supportate dal Cloud Service.        Inoltre, il tooling convalida che la sintassi sia corretta, in modo che apache possa avviarsi correttamente.
* Un&#39;immagine Docker che riproduce localmente il dispatcher.

## Download ed estrazione degli strumenti {#extracting-the-sdk}

Gli strumenti Dispatcher, parte del [AEM come SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)di Cloud Service, possono essere scaricati da un file zip nel portale di distribuzione [](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html) software. Qualsiasi nuova configurazione disponibile nella nuova versione di dispatcher Tools può essere utilizzata per distribuire agli ambienti Cloud in cui è in esecuzione la versione di AEM nel cloud o versioni successive.

Decomprimete l&#39;SDK, che include gli strumenti Dispatcher per MacOS/Linux e Windows.

**Per macOS/Linux**, esegui l’artifact dello strumento dispatcher ed eseguilo. Estrarre automaticamente i file Dispatcher Tools sotto la directory in cui `version` è memorizzato (dove si trova la versione del dispatcher Tools).

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

Potete avere uno o più di questi file. Contiene `<VirtualHost>` voci che corrispondono ai nomi host e consentono ad Apache di gestire ogni traffico di dominio con regole diverse. I file vengono creati nella `available_vhosts` directory e attivati con un collegamento simbolico nella `enabled_vhosts` directory. Da questi `.vhost` file, verranno inclusi altri file come le riscritture e le variabili.

* `conf.d/rewrites/rewrite.rules`

Questo file è incluso dall&#39;interno `.vhost` dei file. Ha una serie di regole di riscrittura per `mod_rewrite`.

>[!NOTE]
>
>Al momento, è necessario utilizzare un singolo file di riscrittura anziché file specifici del sito. La dimensione del file deve essere inferiore a 1 MB.

* `conf.d/variables/custom.vars`

Questo file è incluso dall&#39;interno `.vhost` dei file. In questa posizione potete inserire le definizioni per le variabili Apache.

* `conf.d/variables/global.vars`

Questo file è incluso dall&#39;interno del `dispatcher_vhost.conf` file. È possibile modificare il livello del dispatcher e riscrivere di nuovo il livello di registro in questo file.

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

È possibile avere uno o più di questi file, che contengono farm che corrispondono ai nomi host e consentono al modulo dispatcher di gestire ogni farm con regole diverse. I file vengono creati nella `available_farms` directory e attivati con un collegamento simbolico nella `enabled_farms` directory. Da questi `.farm` file saranno inclusi altri file come filtri, regole della cache e altri.

* `conf.dispatcher.d/cache/rules.any`

Questo file è incluso dall&#39;interno `.farm` dei file. Specifica le preferenze di memorizzazione nella cache.

* `conf.dispatcher.d/clientheaders/clientheaders.any`

Questo file è incluso dall&#39;interno `.farm` dei file. Specifica quali intestazioni di richiesta devono essere inoltrate al back-end.

* `conf.dispatcher.d/filters/filters.any`

Questo file è incluso dall&#39;interno `.farm` dei file. Ha una serie di regole che modificano il traffico da filtrare e non arrivare al backend.

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

Questo file è incluso dall&#39;interno `.farm` dei file. Contiene un elenco di nomi host o di percorsi URI che devono essere associati dalla corrispondenza di tipo GSM. Questo determina il backend da utilizzare per distribuire una richiesta.

I file di cui sopra fanno riferimento ai file di configurazione immutabili elencati di seguito. Le modifiche ai file immutabili non verranno elaborate dai dispatcher negli ambienti Cloud.

**File di configurazione immutabili**

Questi file fanno parte del framework di base e applicano gli standard e le best practice. I file sono considerati immutabili perché modificarli o eliminarli localmente non avranno alcun impatto sulla distribuzione, in quanto non verranno trasferiti nell’istanza di Cloud.

Si consiglia che i file di cui sopra facciano riferimento ai file immutabili elencati di seguito, seguiti da eventuali istruzioni o sostituzioni aggiuntive. Quando la configurazione del dispatcher viene distribuita in un ambiente cloud, verrà utilizzata la versione più recente dei file immutabili, indipendentemente dalla versione utilizzata nello sviluppo locale.

* `conf.d/available_vhosts/default.vhost`

Contiene un esempio di host virtuale. Per il vostro host virtuale, create una copia di questo file, personalizzatelo, passate a `conf.d/enabled_vhosts` e create un collegamento simbolico alla vostra copia personalizzata.

* `conf.d/dispatcher_vhost.conf`

Parte del framework di base, utilizzata per illustrare il modo in cui gli host virtuali e le variabili globali sono inclusi.

* `conf.d/rewrites/default_rewrite.rules`

Regole di riscrittura predefinite adatte a un progetto standard. Se avete bisogno di personalizzazione, modificate `rewrite.rules`. Nella personalizzazione, potete comunque includere prima le regole predefinite, se sono adatte alle vostre esigenze.

* `conf.dispatcher.d/available_farms/default.farm`

Contiene una farm di dispatcher di esempio. Per la vostra farm, create una copia di questo file, personalizzatelo, passate a `conf.d/enabled_farms` e create un collegamento simbolico alla vostra copia personalizzata.

* `conf.dispatcher.d/cache/default_invalidate.any`

Parte del framework di base, viene generato all&#39;avvio. È **necessario** includere questo file in ogni farm definita, nella `cache/allowedClients` sezione.

* `conf.dispatcher.d/cache/default_rules.any`

Regole predefinite per la cache adatte a un progetto standard. Se avete bisogno di personalizzazione, modificate `conf.dispatcher.d/cache/rules.any`. Nella personalizzazione, potete comunque includere prima le regole predefinite, se sono adatte alle vostre esigenze.

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

Intestazioni di richiesta predefinite da inoltrare al back-end, adatte a un progetto standard. Se avete bisogno di personalizzazione, modificate `clientheaders.any`. Nella personalizzazione, potete comunque includere per primo le intestazioni di richiesta predefinite, a seconda delle vostre esigenze.

* `conf.dispatcher.d/dispatcher.any`

Parte del framework di base, utilizzata per illustrare il modo in cui vengono incluse le farm dispatcher.

* `conf.dispatcher.d/filters/default_filters.any`

Filtri predefiniti adatti per un progetto standard. Se avete bisogno di personalizzazione, modificate `filters.any`. Nella personalizzazione, potete comunque includere prima i filtri predefiniti, a seconda delle vostre esigenze.

* `conf.dispatcher.d/renders/default_renders.any`

Parte del framework di base, questo file viene generato all&#39;avvio. È **necessario** includere questo file in ogni farm definita, nella `renders` sezione.

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

Globo host predefinito adatto a un progetto standard. Se avete bisogno di personalizzazione, modificate `virtualhosts.any`. Nella personalizzazione, non devi includere il globbing host predefinito, in quanto corrisponde a **ogni** richiesta in entrata.

>[!NOTE]
>
>Il AEM come archetipo Cloud Service maven genererà la stessa struttura di file di configurazione del dispatcher.

Le sezioni seguenti descrivono come convalidare la configurazione localmente in modo che possa superare il gate di qualità associato in Cloud Manager durante la distribuzione di una versione interna.

## Convalida locale delle direttive supportate nella configurazione del dispatcher {#local-validation-of-dispatcher-configuration}

Lo strumento di convalida è disponibile nell’SDK `bin/validator` come binario Mac OS, Linux o Windows, per consentire ai clienti di eseguire la stessa convalida che Cloud Manager eseguirà durante la creazione e la distribuzione di una versione.

Viene richiamato come: `validator full [-d folder] [-w whitelist] zip-file | src folder`

Lo strumento verifica che la configurazione del dispatcher utilizzi le direttive appropriate supportate da AEM come servizio Cloud, eseguendo la scansione di tutti i file con il pattern `conf.d/enabled_vhosts/*.vhost`. Le direttive consentite nei file di configurazione Apache possono essere elencate eseguendo il comando di inserì nell&#39;elenco Consentiti  convalida:

```
$ validator whitelist
Cloud manager validator 2.0.4
 
Whitelisted directives:
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
| `mod_auth_basic` | [https://httpd.apache.org/docs/2.4/mod/mod_auth_basic.html](https://httpd.apache.org/docs/2.4/mod/mod_auth_basic.html) |
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

* Non esiste una regola del filtro che utilizza la funzione `/glob` (per ulteriori informazioni, consultate [CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957) )
* Nessuna funzione di amministrazione esposta. Ad esempio, l&#39;accesso a percorsi come `/crx/de or /system/console`.

Se eseguito contro il tuo artefatto del cielo o la tua `dispatcher/src` sottodirectory, segnalerà gli errori di convalida:

```
$ validator full dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-whitelisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

Lo strumento di convalida segnala solo l&#39;uso vietato di direttive Apache che non sono state inserite nell&#39;elenco Consentiti. Non segnala problemi sintattici o semantici con la configurazione Apache, in quanto tali informazioni sono disponibili solo per i moduli Apache in un ambiente in esecuzione.

Di seguito sono illustrate le tecniche di risoluzione dei problemi per il debug di errori di convalida comuni generati dallo strumento:

**impossibile individuare una `conf.dispatcher.d` sottocartella nell&#39;archivio**

L’archivio deve contenere le cartelle `conf.d` e `conf.dispatcher.d`. Nota: **non** utilizzare il
prefisso `etc/httpd` nell’archivio.

**impossibile trovare alcuna fattoria in`conf.dispatcher.d/enabled_farms`**

Le farm abilitate devono trovarsi nella sottocartella indicata.

**il file incluso (...) deve essere denominato: ...**

Nella configurazione della farm sono presenti due sezioni che **devono** includere un file specifico: `/renders` e `/allowedClients` nella `/cache` sezione. Queste sezioni devono avere il seguente aspetto:

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

Nella configurazione della farm sono presenti quattro sezioni in cui è possibile includere il proprio file: `/clientheaders`, `filters`, `/rules` nella `/cache` sezione e `/virtualhosts`. I file inclusi devono essere denominati come segue:

| Sezione | Includi nome file |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

In alternativa, è possibile includere la versione **predefinita** di tali file, i cui nomi sono preceduti dalla parola `default_`, ad esempio `../filters/default_filters.any`.

**include l&#39;istruzione in (...), al di fuori di qualsiasi posizione nota: ...**

A parte le sei sezioni menzionate nei paragrafi precedenti, non è consentito utilizzare l&#39; `$include` istruzione, ad esempio:

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**i client/i rendering consentiti non sono inclusi da: ...**

Questo errore viene generato quando non si specifica un&#39;inclusione per `/renders` e `/allowedClients` nella `/cache` sezione. Vedere il nome del **file incluso (...): ...** per ulteriori informazioni.

**il filtro non deve usare il pattern GSM per consentire le richieste**

Non è sicuro consentire le richieste con una regola di `/glob` stile, che viene confrontata con la riga di richiesta completa, ad esempio

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

Questa istruzione consente le richieste di `css` file, ma consente anche le richieste a **qualsiasi** risorsa seguita dalla stringa di query `?a=.css`. È pertanto vietato utilizzare tali filtri (cfr. anche CVE-2016-0957).

**il file incluso (...) non corrisponde ad alcun file noto**

Nella configurazione dell&#39;host virtuale Apache sono disponibili due tipi di file che possono essere specificati come include: riscrittura e variabili.
I file inclusi devono essere denominati come segue:

| Tipo | Includi nome file |
|-----------|---------------------------------|
| Riscrittura | `conf.d/rewrites/rewrite.rules` |
| Variabili | `conf.d/variables/custom.vars` |

In alternativa, potete includere la versione **predefinita** delle regole di riscrittura, il cui nome è `conf.d/rewrites/default_rewrite.rules`.
Si noti che non esiste una versione predefinita dei file delle variabili.

**Rilevato layout di configurazione obsoleto, abilitazione della modalità di compatibilità**

Questo messaggio indica che la configurazione ha il layout obsoleto della versione 1, contenente una configurazione completeApache e file con `ams_` prefissi. Anche se questo è ancora supportato per la compatibilità con le versioni precedenti, è necessario passare al nuovo layout.

## Convalida locale della sintassi di configurazione del dispatcher in modo che apache httpd possa avviare {#local-validation}

Una volta stabilito che la configurazione del modulo dispatcher include solo direttive supportate, è necessario verificare che la sintassi sia corretta in modo che apache possa avviarsi. Per testarlo, il docker deve essere installato localmente. E notate che non è necessario AEM essere in funzione.

Utilizzate lo `validate.sh` script come mostrato di seguito:

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
2. Viene eseguito il test `httpd -t command` per verificare se la sintassi è corretta in modo che apache httpd possa iniziare. In caso di esito positivo, la configurazione dovrebbe essere pronta per la distribuzione

## Verifica locale della configurazione Apache e Dispatcher {#testing-apache-and-dispatcher-configuration-locally}

È inoltre possibile testare localmente la configurazione Apache e Dispatcher. Richiede che il docker venga installato localmente e che la configurazione superi la convalida come descritto in precedenza.

Eseguire lo strumento di convalida (notare che è diverso da quello `validator.sh` indicato in precedenza) utilizzando il `-d` parametro che produce una cartella con tutti i file di configurazione del dispatcher. Eseguire quindi lo `docker_run.sh` script, passando la cartella come argomento. Fornendo il numero di porta (qui: 8080) per esporre l&#39;endpoint del dispatcher, viene avviato un contenitore Docker che esegue il dispatcher con la configurazione.

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

La seguente strategia può essere utilizzata per aumentare l&#39;output di registro per il modulo dispatcher e vedere i risultati della `RewriteRule` valutazione negli ambienti locali e cloud.

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

Al momento, la stessa configurazione del dispatcher viene applicata a tutti i AEM come ambienti di Cloud Service. Il runtime avrà una variabile di ambiente `ENVIRONMENT_TYPE` che contiene la modalità di esecuzione corrente (dev, stage o prod) e una definizione. La definizione può essere `ENVIRONMENT_DEV`, `ENVIRONMENT_STAGE` o `ENVIRONMENT_PROD`. Nella configurazione Apache, la variabile può essere utilizzata direttamente in un&#39;espressione. In alternativa, è possibile utilizzare la definizione per creare logica:

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

Quando si esegue il test della configurazione localmente, è possibile simulare diversi tipi di ambiente trasferendo la variabile `DISP_RUN_MODE` allo `docker_run.sh` script direttamente:

```
$ DISP_RUN_MODE=stage docker_run.sh out docker.for.mac.localhost:4503 8080
```

La modalità di esecuzione predefinita quando non viene passato un valore per DISP_RUN_MODE è &quot;dev&quot;.
Per un elenco completo delle opzioni e delle variabili disponibili, eseguire lo script `docker_run.sh` senza argomenti.

## Visualizzazione della configurazione del dispatcher in uso dal contenitore Docker {#viewing-dispatcher-configuration-in-use-by-docker-container}

Con configurazioni specifiche per l&#39;ambiente, può essere difficile determinare l&#39;aspetto della configurazione effettiva del dispatcher. Dopo aver avviato il contenitore docker con `docker_run.sh` esso può essere scaricato come segue:

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
* In AEM come Cloud Service c&#39;è una convalida supplementare per non consentire le regole di filtro scritte utilizzando `/glob` per prevenire problemi di sicurezza. Poiché `deny *` verranno utilizzati invece di `allow *` (che non possono essere utilizzati), i clienti trarranno vantaggio dall&#39;esecuzione locale del Dispatcher e dall&#39;esecuzione di tentativi ed errori, dall&#39;analisi dei registri per sapere esattamente quali percorsi i filtri del Dispatcher bloccano per poter aggiungere tali percorsi.

## Linee guida per la migrazione della configurazione del dispatcher da AMS a AEM come Cloud Service

La struttura di configurazione del dispatcher presenta differenze tra Managed Services e AEM come Cloud Service. Presentato di seguito, è una guida dettagliata su come migrare dalla configurazione di AMS Dispatcher versione 2 a AEM come Cloud Service.

## Come convertire un AMS in un AEM come configurazione del dispatcher di servizi cloud

La sezione seguente fornisce istruzioni dettagliate su come convertire una configurazione AMS. It assumes
that you have an archive with a structure similar to the one described in [Cloud Manager dispatcher configuration](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

### Estrarre l’archivio e rimuovere un eventuale prefisso

Estrarre l&#39;archivio in una cartella e assicurarsi che le sottocartelle immediate inizino con `conf`, `conf.d`e`conf.dispatcher.d` `conf.modules.d`. In caso contrario, spostateli nella gerarchia.

### Eliminare le sottocartelle e i file non utilizzati

Remove subfolders `conf` and `conf.modules.d`, as well as files matching `conf.d/*.conf`.

### Eliminare tutti gli host virtuali non relativi alla pubblicazione

Rimuovete qualsiasi file host virtuale in `conf.d/enabled_vhosts` cui sia presente `author`, `unhealthy`, `health`o`lc` `flush` nel nome. All virtual host files in `conf.d/available_vhosts` that are not
linked to can be removed as well.

### Rimuovere o impostare come commento le sezioni di host virtuali che non fanno riferimento alla porta 80

Se i file host virtuali contengono ancora sezioni che fanno riferimento esclusivamente a porte diverse dalla porta 80, ad esempio

```
<VirtualHost *:443>
...
</VirtualHost>
```

rimuovile o impostale come commenti. Le istruzioni di queste sezioni non verranno elaborate, ma se le mantieni potresti comunque finire per modificarle senza alcun effetto, il che creerebbe confusione.

### Verificare la directory rewrites

Enter directory `conf.d/rewrites`.

Remove any file named `base_rewrite.rules` and `xforwarded_forcessl_rewrite.rules` and remember to
remove `Include` statements in the virtual host files referring to them.

If `conf.d/rewrites` now contains a single file, it should be renamed to `rewrite.rules` and don&#39;t
forget to adapt the `Include` statements referring to that file in the virtual host files as well.

If the folder however contains multiple, virtual host specific files, their contents should be
copied to the `Include` statement referring to them in the virtual host files.

### Verificare la directory variables

Enter directory `conf.d/variables`.

Remove any file named `ams_default.vars` and remember to remove `Include` statements in the virtual
host files referring to them.

If `conf.d/variables` now contains a single file, it should be renamed to `custom.vars` and don&#39;t
forget to adapt the `Include` statements referring to that file in the virtual host files as well.

If the folder however contains multiple, virtual host specific files, their contents should be
copied to the `Include` statement referring to them in the virtual host files.

### Rimuovere  inseriti nell&#39;elenco Consentiti

Remove the folder `conf.d/whitelists` and remove `Include` statements in the virtual host files referring to
some file in that subfolder.

### Sostituire le variabili non più disponibili

In tutti i file host virtuali:

Rinomina `PUBLISH_DOCROOT` in `DOCROOT`Rimuovi sezioni che fanno riferimento a variabili denominate `DISP_ID`, `PUBLISH_FORCE_SSL` oppure `PUBLISH_WHITELIST_ENABLED`

### Controllare lo stato eseguendo la convalida

Run the dispatcher validator in your directory, with the `httpd` subcommand:

```
$ validator httpd .
```

Se si verificano degli errori relativi a file di inclusione mancanti, verifica di aver rinominato correttamente tali file.

Se vengono visualizzate delle direttive Apache che non vengono inserite nell&#39;elenco Consentiti, rimuoverle.

### Eliminare tutte le farm non relative alla pubblicazione

Remove any farm file in `conf.dispatcher.d/enabled_farms` that has `author`, `unhealthy`, `health`,
`lc` or `flush` in its name. All farm files in `conf.dispatcher.d/available_farms` that are not
linked to can be removed as well.

### Rinominare i file di farm

All farms in `conf.d/enabled_farms` must be renamed to match the pattern `*.farm`, so e.g. a
farm file called `customerX_farm.any` should be renamed `customerX.farm`.

### Verificare la cache

Enter directory `conf.dispatcher.d/cache`.

Rimuovi eventuali file con prefisso `ams_`.

If `conf.dispatcher.d/cache` is now empty, copy the file `conf.dispatcher.d/cache/rules.any`
from the standard dispatcher configuration to this folder. The standard dispatcher
configuration can be found in the folder `src` of this SDK. Don&#39;t forget to adapt the
`$include` statements referring to the `ams_*_cache.any` rule files  in the farm files
as well.

If instead `conf.dispatcher.d/cache` now contains a single file with suffix `_cache.any`,
it should be renamed to `rules.any` and don&#39;t forget to adapt the `$include` statements
referring to that file in the farm files as well.

If the folder however contains multiple, farm specific files with that pattern, their contents
should be copied to the `$include` statement referring to them in the farm files.

Remove any file that has the suffix `_invalidate_allowed.any`.

Copiate il file `conf.dispatcher.d/cache/default_invalidate_any` da AEM predefinito nella configurazione del dispatcher di Cloud a tale posizione.

In each farm file, remove any contents in the `cache/allowedClients` section and replace it
with:

```
$include "../cache/default_invalidate.any"
```

### Verificare la directory clientheaders

Enter directory `conf.dispatcher.d/clientheaders`.

Rimuovi eventuali file con prefisso `ams_`.

If `conf.dispatcher.d/clientheaders` now contains a single file with suffix `_clientheaders.any`,
it should be renamed to `clientheaders.any` and don&#39;t forget to adapt the `$include` statements
referring to that file in the farm files as well.

If the folder however contains multiple, farm specific files with that pattern, their contents
should be copied to the `$include` statement referring to them in the farm files.

Copiate il file `conf.dispatcher/clientheaders/default_clientheaders.any` da defaultAEM come configurazione dispatcher di Cloud Service in tale posizione.

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

Enter directory `conf.dispatcher.d/filters`.

Rimuovi eventuali file con prefisso `ams_`.

If `conf.dispatcher.d/filters` now contains a single file it should be renamed to
`filters.any` and don&#39;t forget to adapt the `$include` statements referring to that
file in the farm files as well.

If the folder however contains multiple, farm specific files with that pattern, their contents
should be copied to the `$include` statement referring to them in the farm files.

Copiate il file `conf.dispatcher/filters/default_filters.any` da defaultAEM come configurazione dispatcher di Cloud Service in tale posizione.

In ciascun file di farm, sostituisci eventuali istruzioni di inclusione di questo tipo:

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

con l’istruzione:

```
$include "../filters/default_filters.any"
```

### Verificare la directory renders

Enter directory `conf.dispatcher.d/renders`.

Rimuovi tutti i file presenti nella cartella.

Copiate il file `conf.dispatcher.d/renders/default_renders.any` da defaultAEM come configurazione dispatcher di Cloud Service in tale posizione.

In each farm file, remove any contents in the `renders` section and replace it
with:

```
$include "../renders/default_renders.any"
```

### Verificare la directory virtualhosts

Rename the directory `conf.dispatcher.d/vhosts` to `conf.dispatcher.d/virtualhosts` and enter it.

Rimuovi eventuali file con prefisso `ams_`.

If `conf.dispatcher.d/virtualhosts` now contains a single file it should be renamed to
`virtualhosts.any` and don&#39;t forget to adapt the `$include` statements referring to that
file in the farm files as well.

If the folder however contains multiple, farm specific files with that pattern, their contents
should be copied to the `$include` statement referring to them in the farm files.

Copiate il file `conf.dispatcher/virtualhosts/default_virtualhosts.any` da defaultAEM come configurazione dispatcher di Cloud Service in tale posizione.

In ciascun file di farm, sostituisci eventuali istruzioni di inclusione di questo tipo:

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

con l’istruzione:

```
$include "../virtualhosts/default_virtualhosts.any"
```

### Controllare lo stato eseguendo la convalida

Eseguire il AEM come convalida dispatcher Cloud Service nella directory, con il `dispatcher` sottocomando:

```
$ validator dispatcher .
```

Se si verificano degli errori relativi a file di inclusione mancanti, verifica di aver rinominato correttamente tali file.

Se vengono visualizzati errori relativi a una variabile `PUBLISH_DOCROOT` non definita, rinominala in `DOCROOT`.

Per qualsiasi altro errore, consulta la sezione Risoluzione di problemi della documentazione relativa allo strumento di convalida.

### Verificare la configurazione con una distribuzione locale (richiede l&#39;installazione di Docker)

Using the script `docker_run.sh` in the AEM as a Cloud Service Dispatcher Tools, you can test that
your configuration does not contain any other error that would only show up in
deployment:

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

Congratulazioni! If the validator no longer reports any issue and the
docker container starts up without any failures or warnings, you&#39;re
ready to move your configuration to a `dispatcher/src` subdirectory
of your git repository.

**I clienti che utilizzano la configurazione AMS Dispatcher versione 1 devono contattare l&#39;assistenza clienti per effettuare la migrazione dalla versione 1 alla versione 2, in modo da seguire le istruzioni riportate sopra.**
