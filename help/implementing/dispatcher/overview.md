---
title: Dispatcher in Cloud
description: 'Dispatcher in Cloud '
translation-type: tm+mt
source-git-commit: 64475ec492863f713a7cefaedc4c0782014682ae

---


# Dispatcher in Cloud {#Dispatcher-in-the-cloud}

## Configurazione e test Apache e Dispatcher {#apache-and-dispatcher-configuration-and-testing}

In questa sezione viene descritto come strutturare AEM come configurazioni di Apache e Dispatcher del servizio Cloud, nonché come convalidarlo ed eseguirlo localmente prima di distribuirlo negli ambienti Cloud. Inoltre, descrive il debug negli ambienti Cloud. Per ulteriori informazioni sul dispatcher, consultate la documentazione [del dispatcher](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/dispatcher.html)AEM.

>[!NOTE]
>Gli utenti Windows dovranno utilizzare Windows 10 Professional o altre distribuzioni che supportano Docker. Questo è un prerequisito per l&#39;esecuzione e il debug del dispatcher su un computer locale. Le sezioni seguenti includono comandi che utilizzano le versioni Mac o Linux dell&#39;SDK, ma l&#39;SDK di Windows può essere utilizzato in modo simile.

## Strumenti Dispatcher {#dispatcher-sdk}

Gli strumenti Dispatcher fanno parte di AEM nel suo complesso come SDK per servizi cloud e forniscono:

* una struttura di file di vaniglia contenente i file di configurazione da includere in un progetto di speditore di lievito;
* Collaborazione per consentire ai clienti di convalidare localmente una configurazione dispatcher;
* Un&#39;immagine Docker che riproduce localmente il dispatcher.

## Download ed estrazione degli strumenti {#extracting-the-sdk}

Gli strumenti Dispatcher possono essere scaricati da un file zip sul portale [Software Distribution](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html) . L&#39;accesso agli elenchi dell&#39;SDK è limitato a quelli con AEM Managed Services o AEM come ambienti di servizio cloud. Qualsiasi nuova configurazione disponibile nella nuova versione del dispatcher Tools può essere utilizzata per distribuire agli ambienti Cloud in cui è in esecuzione tale versione di AEM nel Cloud o in una versione successiva.

**Per macOS e Linux**, scaricate lo script shell in una cartella del computer, rendetelo eseguibile ed eseguitelo. Estrarre automaticamente i file Dispatcher Tools sotto la directory in cui `version` è memorizzato (dove si trova la versione del dispatcher Tools).

```bash
$ chmod +x DispatcherSDKv<version>.sh
$ ./DispatcherSDKv<version>.sh
Verifying archive integrity...  100%   All good.
Uncompressing DispatcherSDKv<version>  100% 
```

**Per Windows**, scaricate l’archivio ZIP ed estraetelo.

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

Questo file è incluso dall&#39;interno del `dispatcher_vhost.conf` file. È possibile modificare il livello del dispatcher e riscrivere nuovamente il livello di registro in questo file.

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

È possibile avere uno o più di questi file e contengono farm che corrispondono ai nomi host e consentono al modulo dispatcher di gestire ogni farm con regole diverse. I file vengono creati nella `available_farms` directory e attivati con un collegamento simbolico nella `enabled_farms` directory. Da questi `.farm` file saranno inclusi altri file come filtri, regole della cache e altri.

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

Regole di riscrittura predefinite adatte a un progetto standard. Se avete bisogno di personalizzazione, modificate `rewrite.rules`. Nella personalizzazione, potete comunque includere prima le regole predefinite, a seconda delle vostre esigenze.

* `conf.dispatcher.d/available_farms/default.farm`

Contiene una farm di dispatcher di esempio. Per la vostra farm, create una copia di questo file, personalizzatelo, passate a `conf.d/enabled_farms` e create un collegamento simbolico alla vostra copia personalizzata.

* `conf.dispatcher.d/cache/default_invalidate.any`

Parte del framework di base, viene generato all&#39;avvio. È **necessario** includere questo file in ogni farm definita, nella `cache/allowedClients` sezione.

* `conf.dispatcher.d/cache/default_rules.any`

Regole di cache predefinite adatte a un progetto standard. Se avete bisogno di personalizzazione, modificate `conf.dispatcher.d/cache/rules.any`. Nella personalizzazione, potete comunque includere prima le regole predefinite, a seconda delle vostre esigenze.

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
>AEM come archetipo di cloud service genererà la stessa struttura di file di configurazione del dispatcher.

Le sezioni seguenti descrivono come convalidare la configurazione localmente in modo che possa superare il gate di qualità associato in Cloud Manager durante la distribuzione di una versione interna.

## Convalida locale della configurazione del dispatcher {#local-validation-of-dispatcher-configuration}

Lo strumento di convalida è disponibile nell’SDK `bin/validator` come binario Mac OS, Linux o Windows, per consentire ai clienti di eseguire la stessa convalida che Cloud Manager eseguirà durante la creazione e la distribuzione di una versione.

Viene richiamato come: `validator full [-d folder] [-w whitelist] zip-file | src folder`

Lo strumento convalida la configurazione Apache e dispatcher. Consente di analizzare tutti i file con il pattern `conf.d/enabled_vhosts/*.vhost` e di verificare che vengano utilizzate solo le direttive inserite nella lista bianca. Le direttive consentite nei file di configurazione Apache possono essere elencate eseguendo il comando whitelist del validatore:

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

I clienti non possono aggiungere moduli arbitrari, ma in futuro potrebbero essere presi in considerazione moduli aggiuntivi per l&#39;inclusione nel prodotto. I clienti possono trovare l&#39;elenco delle direttive disponibili per una determinata versione del dispatcher eseguendo la whitelist di convalida nell&#39;SDK, come descritto nella documentazione di Dispatcher Tools.

La whitelist contiene un elenco di direttive Apache consentite in una configurazione cliente. Se una direttiva non è elencata, lo strumento registra un errore e restituisce un codice di uscita diverso da zero. Se sulla riga di comando non viene visualizzata alcuna whitelist (che rappresenta il modo in cui dovrebbe essere richiamata), lo strumento utilizza una whitelist predefinita che Cloud Manager utilizzerà per la convalida prima di distribuirla negli ambienti Cloud.

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

Lo strumento di convalida segnala solo l&#39;uso vietato di direttive Apache che non sono state inserite nella lista bianca. Non segnala problemi sintattici o semantici con la configurazione Apache, in quanto tali informazioni sono disponibili solo per i moduli Apache in un ambiente in esecuzione.

Se non vengono segnalati errori di convalida, la configurazione è pronta per la distribuzione.

Di seguito sono illustrate le tecniche di risoluzione dei problemi per il debug di errori di convalida comuni generati dallo strumento:

**impossibile individuare una`conf.dispatcher.d`sottocartella nell&#39;archivio**

L&#39;archivio deve contenere cartelle `conf.d` e `conf.dispatcher.d`. Nota: **non** utilizzare il prefisso `etc/httpd` nell&#39;archivio.

**impossibile trovare alcuna fattoria in`conf.dispatcher.d/enabled_farms`**

Le farm abilitate devono trovarsi nella sottocartella indicata.

**il file incluso (...) deve essere denominato:...**

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

**file incluso in posizione sconosciuta:...**

Nella configurazione della farm sono presenti quattro sezioni in cui è possibile includere il proprio file: `/clientheaders`, `filters`, `/rules` nella `/cache` sezione e `/virtualhosts`. I file inclusi devono essere denominati come segue:

| Sezione | Includi nome file |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

In alternativa, è possibile includere la versione **predefinita** di tali file, i cui nomi sono preceduti dalla parola `default_`, ad esempio `../filters/default_filters.any`.

**include istruzione in (...), al di fuori di qualsiasi posizione nota:...**

A parte le sei sezioni menzionate nei paragrafi precedenti, non è consentito utilizzare l&#39; `$include` istruzione, ad esempio:

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**i client/rendering consentiti non sono inclusi da:...**

Questo errore viene generato quando non si specifica un&#39;inclusione per `/renders` e `/allowedClients` nella `/cache` sezione. **Vedere il nome del** file incluso (...):... per ulteriori informazioni.

**il filtro non deve usare il pattern GSM per consentire le richieste**

Non è sicuro consentire le richieste con una regola di `/glob` stile, che viene confrontata con la riga di richiesta completa, ad esempio

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

Questa istruzione consente le richieste di `css` file, ma consente anche le richieste a **qualsiasi** risorsa seguita dalla stringa di query `?a=.css`. È pertanto vietato utilizzare tali filtri (cfr. anche CVE-2016-0957).

**il file incluso (...) non corrisponde ad alcun file noto**

Nella configurazione host virtuale Apache sono disponibili due tipi di file che possono essere specificati come include: riscrittura e variabili.
I file inclusi devono essere denominati come segue:

| Tipo | Includi nome file |
|-----------|---------------------------------|
| Riscrittura | `conf.d/rewrites/rewrite.rules` |
| Variabili | `conf.d/variables/custom.vars` |

In alternativa, potete includere la versione **predefinita** delle regole di riscrittura, il cui nome è `conf.d/rewrites/default_rewrite.rules`.
Si noti che non esiste una versione predefinita dei file delle variabili.

**Rilevato layout di configurazione obsoleto, abilitazione della modalità di compatibilità**

Questo messaggio indica che la configurazione ha il layout obsoleto della versione 1, contenente una configurazione completeApache e file con `ams_` prefissi. Anche se questo è ancora supportato per la compatibilità con le versioni precedenti, è necessario passare al nuovo layout.

## Verifica locale della configurazione Apache e Dispatcher {#testing-apache-and-dispatcher-configuration-locally}

È inoltre possibile testare localmente la configurazione Apache e Dispatcher. Richiede che Docker sia installato localmente e che la configurazione superi la convalida come descritto sopra.

Utilizzando il parametro &quot;`-d`&quot;, il validatore genera una cartella con tutti i file di configurazione necessari al dispatcher.

Quindi, lo `docker_run.sh` script può puntare a tale cartella, avviando il contenitore con la configurazione.

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

La seguente strategia può essere utilizzata per aumentare l&#39;output di registro per il modulo dispatcher e vedere il risultato della `RewriteRule` valutazione negli ambienti locali e cloud.

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

Quando si esegue il dispatcher localmente, i file di registro vengono stampati anche direttamente nell&#39;output del terminale. Nella maggior parte dei casi, questi registri devono essere in DEBUG, che può essere realizzato trasmettendo il livello Debug come parametro quando si esegue Docker. Esempio:

`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`

I registri per gli ambienti cloud saranno esposti tramite il servizio di registrazione disponibile in Cloud Manager.

## Diverse configurazioni del dispatcher per ambiente {#different-dispatcher-configurations-per-environment}

Al momento, la stessa configurazione del dispatcher viene applicata a tutti AEM come ambienti di servizio cloud. Il runtime avrà una variabile di ambiente `ENVIRONMENT_TYPE` che contiene la modalità di esecuzione corrente (dev, stage o prod) e una definizione. La definizione può essere `ENVIRONMENT_DEV`, `ENVIRONMENT_STAGE` o `ENVIRONMENT_PROD`. Nella configurazione Apache, la variabile può essere utilizzata direttamente in un&#39;espressione. In alternativa, è possibile utilizzare la definizione per creare logica:

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

Durante il test della configurazione localmente, potete simulare diversi tipi di ambiente trasferendo la variabile `DISP_RUN_MODE` allo `docker_run.sh` script direttamente:

```
$ DISP_RUN_MODE=stage docker_run.sh out docker.for.mac.localhost:4503 8080
```

La modalità di esecuzione predefinita quando non viene passato un valore per DISP_RUN_MODE è &quot;dev&quot;.
Per un elenco completo delle opzioni e delle variabili disponibili, eseguire lo script `docker_run.sh` senza argomenti.

## Visualizzazione della configurazione del dispatcher in uso dal contenitore Docker {#viewing-dispatcher-configuration-in-use-by-docker-container}

Con configurazioni specifiche dell&#39;ambiente, può essere difficile determinare l&#39;aspetto della configurazione effettiva del dispatcher. Dopo aver avviato il contenitore docker con `docker_run.sh` esso può essere scaricato come segue:

* Determinare l&#39;ID contenitore docker in uso:

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

## Differenze principali tra il dispatcher AMS e AEM come servizio cloud {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

Come descritto nella pagina di riferimento precedente, la configurazione Apache e Dispatcher in AEM come servizio cloud è abbastanza simile a quella di AMS. Le principali differenze sono:

* In AEM come servizio cloud, alcune direttive Apache potrebbero non essere utilizzate (ad esempio `Listen` o `LogLevel`)
* In AEM come servizio cloud, è possibile inserire solo alcuni elementi della configurazione del dispatcher, che includono file e la loro denominazione è importante. Ad esempio, le regole del filtro che si desidera riutilizzare tra host diversi devono essere inserite in un file denominato `filters/filters.any`. Per ulteriori informazioni, consultate la pagina di riferimento.
* In AEM come servizio cloud è disponibile una funzione di convalida aggiuntiva per rifiutare le regole del filtro scritte con `/glob` per evitare problemi di sicurezza. Poiché `deny *` verranno utilizzati invece di `allow *` (che non possono essere utilizzati), i clienti trarranno vantaggio dall&#39;esecuzione locale del Dispatcher e dall&#39;esecuzione di tentativi ed errori, dall&#39;analisi dei registri per sapere esattamente quali percorsi i filtri del Dispatcher bloccano per poter aggiungere tali percorsi.

## Linee guida per la migrazione della configurazione del dispatcher da AMS ad AEM come servizio cloud

La struttura di configurazione del dispatcher presenta differenze tra i servizi gestiti e AEM come servizio cloud. Presentato di seguito, è una guida dettagliata su come migrare dalla configurazione di AMS Dispatcher versione 2 ad AEM come servizio cloud.

## Come convertire un AMS in un AEM come configurazione del dispatcher di servizi cloud

La sezione seguente fornisce istruzioni dettagliate su come convertire una configurazione AMS. Presuppone di disporre di un archivio con una struttura simile a quella descritta nella configurazione del dispatcher di [Cloud Manager](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

### Estrarre l&#39;archivio e rimuovere un eventuale prefisso

Estrarre l&#39;archivio in una cartella e assicurarsi che le sottocartelle immediate inizino con `conf`, `conf.d`e`conf.dispatcher.d` `conf.modules.d`. In caso contrario, spostateli nella gerarchia.

### Eliminare le sottocartelle e i file non utilizzati

Rimuovere sottocartelle `conf` e `conf.modules.d`, nonché i file corrispondenti `conf.d/*.conf`.

### Eliminazione di tutti gli host virtuali non pubblicati

Rimuovete qualsiasi file host virtuale in `conf.d/enabled_vhosts` cui sia presente `author`, `unhealthy`, `health`o`lc` `flush` nel nome. È inoltre possibile rimuovere tutti i file host virtuali in `conf.d/available_vhosts` cui non è stato eseguito il collegamento.

### Rimuovere o commentare sezioni di host virtuali che non fanno riferimento alla porta 80

Se i file host virtuali contengono ancora sezioni che fanno riferimento esclusivamente a porte diverse dalla porta 80, ad esempio

```
<VirtualHost *:443>
...
</VirtualHost>
```

rimuovete o commentateli. Le istruzioni in queste sezioni non vengono elaborate, ma se le si mantiene intorno, si potrebbe comunque finire per modificarle senza alcun effetto, il che crea confusione.

### Verifica riscrittura

Enter directory `conf.d/rewrites`.

Rimuovete tutti i file denominati `base_rewrite.rules` e `xforwarded_forcessl_rewrite.rules` ricordate di rimuovere le istruzioni `Include` nei file host virtuali che vi fanno riferimento.

Se `conf.d/rewrites` ora contiene un singolo file, deve essere rinominato `rewrite.rules` e non dimenticare di adattare le `Include` istruzioni che fanno riferimento a tale file anche nei file host virtuali.

Se tuttavia la cartella contiene più file specifici dell&#39;host virtuale, il relativo contenuto deve essere associato all&#39; `Include` istruzione che li fa riferimento nei file host virtuali.

### Verifica variabili

Enter directory `conf.d/variables`.

Rimuovete qualsiasi file denominato `ams_default.vars` e ricordate di rimuovere `Include` le istruzioni nei file virtualhost che vi fanno riferimento.

Se `conf.d/variables` ora contiene un singolo file, deve essere rinominato `custom.vars` e non dimenticare di adattare le `Include` istruzioni che fanno riferimento a tale file anche nei file host virtuali.

Se tuttavia la cartella contiene più file specifici dell&#39;host virtuale, il relativo contenuto deve essere associato all&#39; `Include` istruzione che li fa riferimento nei file host virtuali.

### Rimuovi whitelist

Rimuovete la cartella `conf.d/whitelists` e rimuovete `Include` le istruzioni nei file host virtuali che fanno riferimento ad alcuni file nella sottocartella.

### Sostituisce qualsiasi variabile non più disponibile

In tutti i file host virtuali:

Rinomina `PUBLISH_DOCROOT` in `DOCROOT`Rimuovi sezioni che fanno riferimento a variabili denominate `DISP_ID`, `PUBLISH_FORCE_SSL` oppure `PUBLISH_WHITELIST_ENABLED`

### Controllare lo stato eseguendo la convalida

Eseguire il dispatcher validator nella directory, con il `httpd` sottocomando:

```
$ validator httpd .
```

Se si verificano errori relativi ai file di inclusione mancanti, verificate di aver rinominato correttamente tali file.

Se vengono visualizzate delle direttive Apache che non sono inserite nella white list, rimuoverle.

### Eliminazione di tutte le farm non pubblicate

Rimuovete qualsiasi file della farm in `conf.dispatcher.d/enabled_farms` cui sia presente `author`, `unhealthy`, `health`o`lc` `flush` nel nome. È inoltre possibile rimuovere tutti i file della farm in `conf.dispatcher.d/available_farms` cui non è stato eseguito il collegamento.

### Rinominare i file della farm

Tutte le farm in `conf.d/enabled_farms` devono essere rinominate in modo da corrispondere al pattern, `*.farm`pertanto, ad esempio, il file afarm chiamato `customerX_farm.any` deve essere rinominato `customerX.farm`.

### Controlla cache

Enter directory `conf.dispatcher.d/cache`.

Rimuovete eventuali file con prefisso `ams_`.

Se `conf.dispatcher.d/cache` è vuoto, copiate il file `conf.dispatcher.d/cache/rules.any`dalla configurazione del dispatcher standard in questa cartella. La configurazione del dispatcher standard si trova nella cartella `src` di questo SDK. Non dimenticare di adattare le`$include` istruzioni relative ai file delle `ams_*_cache.any` regole anche nei file della farm.

Se invece `conf.dispatcher.d/cache` ora contiene un singolo file con suffisso `_cache.any`, è necessario rinominarlo `rules.any` e non dimenticare di adattare le `$include` istruzioni relative a tale file anche nei file della farm.

Se tuttavia la cartella contiene più file specifici della farm con tale pattern, il relativo contenuto deve essere copiato nell&#39; `$include` istruzione che li fa riferimento nei file della farm.

Rimuovete qualsiasi file con il suffisso `_invalidate_allowed.any`.

Copiate il file `conf.dispatcher.d/cache/default_invalidate_any` da AEM predefinito nella configurazione del dispatcher di Cloud a tale posizione.

In ciascun file della farm, rimuovete qualsiasi contenuto della `cache/allowedClients` sezione e sostituitelo con:

```
$include "../cache/default_invalidate.any"
```

### Verifica intestazioni client

Enter directory `conf.dispatcher.d/clientheaders`.

Rimuovete eventuali file con prefisso `ams_`.

Se `conf.dispatcher.d/clientheaders` ora contiene un singolo file con suffisso `_clientheaders.any`, è necessario rinominarlo `clientheaders.any` e non dimenticare di adattare le `$include` istruzioni relative a tale file anche nei file della farm.

Se tuttavia la cartella contiene più file specifici della farm con tale pattern, il relativo contenuto deve essere copiato nell&#39; `$include` istruzione che li fa riferimento nei file della farm.

Copiate il file `conf.dispatcher/clientheaders/default_clientheaders.any` dall’applicazione predefinita AEM come configurazione del dispatcher del servizio cloud in tale posizione.

In ciascun file farm, sostituite le istruzioni include di tipo client che abbiano il seguente aspetto:

```
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"
```

con l&#39;istruzione:

```
$include "../clientheaders/default_clientheaders.any"
```

### Filtro controllo

Enter directory `conf.dispatcher.d/filters`.

Rimuovete eventuali file con prefisso `ams_`.

Se `conf.dispatcher.d/filters` ora contiene un singolo file deve essere rinominato`filters.any` e non dimenticare di adattare le `$include` istruzioni che fanno riferimento a tale file anche nei file della farm.

Se tuttavia la cartella contiene più file specifici della farm con tale pattern, il relativo contenuto deve essere copiato nell&#39; `$include` istruzione che li fa riferimento nei file della farm.

Copiate il file `conf.dispatcher/filters/default_filters.any` dall’applicazione predefinita AEM come configurazione del dispatcher del servizio cloud in tale posizione.

In ciascun file farm, sostituire eventuali istruzioni di filtro con le seguenti:

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

con l&#39;istruzione:

```
$include "../filters/default_filters.any"
```

### Controllare i rendering

Enter directory `conf.dispatcher.d/renders`.

Rimuovete tutti i file presenti nella cartella.

Copiate il file `conf.dispatcher.d/renders/default_renders.any` dall’applicazione predefinita AEM come configurazione del dispatcher del servizio cloud in tale posizione.

In ciascun file della farm, rimuovete qualsiasi contenuto della `renders` sezione e sostituitelo con:

```
$include "../renders/default_renders.any"
```

### Controllare i virtualhost

Rinominare la directory `conf.dispatcher.d/vhosts` in `conf.dispatcher.d/virtualhosts` e immetterla.

Rimuovete eventuali file con prefisso `ams_`.

Se `conf.dispatcher.d/virtualhosts` ora contiene un singolo file deve essere rinominato`virtualhosts.any` e non dimenticare di adattare le `$include` istruzioni che fanno riferimento a tale file anche nei file della farm.

Se tuttavia la cartella contiene più file specifici della farm con tale pattern, il relativo contenuto deve essere copiato nell&#39; `$include` istruzione che li fa riferimento nei file della farm.

Copiate il file `conf.dispatcher/virtualhosts/default_virtualhosts.any` dall’applicazione predefinita AEM come configurazione del dispatcher del servizio cloud in tale posizione.

In ciascun file farm, sostituire eventuali istruzioni di filtro con le seguenti:

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

con l&#39;istruzione:

```
$include "../virtualhosts/default_virtualhosts.any"
```

### Controllare lo stato eseguendo la convalida

Eseguite AEM come strumento di convalida del dispatcher dei servizi cloud nella directory, con il `dispatcher` sottocomando:

```
$ validator dispatcher .
```

Se si verificano errori relativi ai file di inclusione mancanti, verificate di aver rinominato correttamente tali file.

Se vengono visualizzati errori relativi a una variabile non definita, rinominarla `PUBLISH_DOCROOT`in `DOCROOT`.

Per ogni altro errore, consultate la sezione Risoluzione dei problemi della documentazione sullo strumento di convalida.

### Verificare la configurazione con una distribuzione locale (richiede l&#39;installazione di Docker)

Utilizzando lo script `docker_run.sh` in AEM come strumenti di dispatcher dei servizi cloud, puoi verificare che la configurazione non contenga altri errori che potrebbero solo verificarsi come dislocazione:

### Passaggio 1: Generazione di informazioni sulla distribuzione con il validatore

```
validator full -d out .
```

In questo modo viene convalidata la configurazione completa e vengono generate le informazioni sulla distribuzione in `out`

### Passaggio 2: Avviare il dispatcher in un&#39;immagine docker con tali informazioni di distribuzione

Con il server di pubblicazione AEM in esecuzione sul computer MacOS, in ascolto sulla porta 4503, potete avviare il dispatcher davanti al server come segue:

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

Verrà avviato il contenitore ed esporre Apache sulla porta locale 8080.

### Utilizza la nuova configurazione dispatcher

Congratulazioni! Se la funzione di convalida non segnala più alcun problema e il contenitore docker viene avviato senza errori o avvisi, è possibile spostare la configurazione in una `dispatcher/src` sottodirectory del repository git.

**I clienti che utilizzano la configurazione AMS Dispatcher versione 1 devono contattare l&#39;assistenza clienti per effettuare la migrazione dalla versione 1 alla versione 2, in modo da seguire le istruzioni riportate sopra.**

## Dispatcher e CDN {#dispatcher-cdn}

Il flusso di dati è il seguente:

1. URL inserito nel browser
2. Richiesta effettuata alla CDN mappata in DNS a tale dominio
3. Se il contenuto è completamente memorizzato nella cache su CDN, CDN lo trasmette al browser
4. Se il contenuto non è completamente memorizzato nella cache, la rete CDN richiama (proxy inverso) al dispatcher
5. Se il contenuto è completamente memorizzato nella cache del dispatcher, il dispatcher lo invia alla CDN
6. Se il contenuto non è completamente memorizzato nella cache, il dispatcher richiama (proxy inverso) alla pubblicazione AEM
7. Contenuto riprodotto dal browser

### CDN {#cdn}

AEM offre due opzioni:

1. CDN gestito - CDN out-of-the-box di AEM.
2. CDN non gestito - Il cliente porta la propria CDN ed è interamente responsabile della gestione.

La prima opzione è altamente consigliata e Adobe non è responsabile del risultato di eventuali errori di configurazione quando si utilizza la seconda opzione.

#### CDN gestito {#managed-cdn}

Dopo che Adobe ha fornito la CDN, è necessario creare un CNAME, mappando i domini dell&#39;applicazione su un dominio controllato da Adobe ospitato nel dominio CDN gestito.

La rete CDN funge da firewall per applicazioni Web layer 7, che richiede la terminazione SSL, pertanto richiede un certificato SSL firmato dal cliente. Durante la fase di pre-rilascio, è necessario fornire il certificato ad Adobe attraverso processi manuali.

Al momento di GA, devi caricare il certificato in Cloud Manager, che a sua volta lo caricherà nella rete CDN. Quando i certificati SSL scadono, riceverete una notifica per consentirvi di aggiornare i certificati in Cloud Manager.

#### CDN non gestito {#unmanaged-cdn}

Puoi gestire la tua CDN, a condizione:

1. Esiste una CDN.
2. Lo gestirà.
3. L’applicazione non effettua chiamate API estese alla rete CDN che non sono già incluse nell’architettura AEM.
4. AEM come servizio cloud è in grado di stabilire che il sistema end-to-end funziona correttamente.
5. Dovrete fornire ad Adobe la whitelist degli URL CDN per consentirne l&#39;utilizzo.

Adobe fornirà un URL AEM Cloud da usare come origine della CDN.


#### Annullamento validità cache CDN {#CDN-cache-invalidation}

L&#39;annullamento della validità della cache segue le regole seguenti:

* In generale, il contenuto HTML viene memorizzato nella cache CDN per 5 minuti, in base all&#39;intestazione del controllo cache emesso dal dispatcher.
* Le librerie client (JavaScript e CSS) vengono memorizzate nella cache in modo indefinito utilizzando il controllo cache impostato su immutabile o su 30 giorni per i browser meno recenti che non rispettano il valore immutabile. Le librerie client vengono servite in un percorso univoco che cambia se cambiano le librerie client. In altre parole, l&#39;HTML che fa riferimento alle librerie client verrà prodotto come necessario, in modo da poter sperimentare il nuovo contenuto mentre viene pubblicato.
* Per impostazione predefinita, le immagini non sono memorizzate nella cache.

## Annullamento della validità della cache del dispatcher esplicito {#explicit-invalidation}

Prima di AEM come servizio cloud, erano disponibili 2 modi per annullare la validità della cache del dispatcher.

1. Richiamate l&#39;API di replica, specificando l&#39;agente di eliminazione del dispatcher di pubblicazione
2. Chiamata diretta dell&#39; `invalidate.cache` API (ad esempio POST /dispatcher/invalidate.cache)

L&#39; `invalidate.cache` approccio non sarà più supportato, in quanto riguarda solo un nodo dispatcher specifico.
AEM come servizio cloud opera a livello di servizio, non a livello di singolo nodo, pertanto le istruzioni di annullamento della validità contenute nella documentazione [Dispatcher Help](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/dispatcher.html) non sono più precise.
È invece necessario utilizzare l&#39;approccio API di replica. [La documentazione](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/Replicator.html) API è disponibile e per un esempio di cancellazione della cache, consultate la pagina [di esempio](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) API e in particolare l&#39;esempio CustomStep che emette un&#39;azione di replica di tipo ACTIVATE a tutti gli agenti disponibili.

Il diagramma seguente illustra questo.

<!-- [CDN](assets/cdn.png "CDN") -->

<!-- See [Apache and Dispatcher Configuration and Testing](../developing/introduction/developer-experience.md#apache-and-dispatcher-configuration-and-testing) for instructions on how a developer can configure apache and the dispatcher module. -->

### Annullamento della validità della cache del dispatcher durante l&#39;attivazione/disattivazione {#cache-activation-deactivation}

L’annullamento della validità con attivazione della pubblicazione è uguale a quello del quickstart:
Quando l’istanza di pubblicazione riceve una nuova versione di una pagina o di una risorsa dall’autore (tramite la coda di replica e pipeline), utilizza l’agente di svuotamento per annullare i percorsi appropriati nel dispatcher. Il percorso aggiornato viene rimosso dalla cache del dispatcher, insieme ai relativi elementi principali, fino a un livello che è possibile configurare con [statfileslevel](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level).

### Massima libertà di stampa e coerenza delle versioni {#content-consistency}

* Le pagine sono costituite da HTML, JavaScript, CSS e immagini.
* È consigliabile sfruttare il framework clientlibs per importare risorse Javascript e CSS in pagine HTML, tenendo conto delle dipendenze tra librerie JS.
* È disponibile la gestione automatica delle versioni, che consente agli sviluppatori di archiviare le modifiche apportate alle librerie JS nel controllo del codice sorgente, e l&#39;ultima versione sarà disponibile quando viene premuto un rilascio. In caso contrario, gli sviluppatori dovrebbero modificare manualmente il codice HTML con riferimenti alla nuova versione della libreria, il che è particolarmente costoso se molti modelli HTML condividono la stessa libreria.
* Quando le nuove versioni delle librerie vengono rilasciate in produzione, le pagine HTML di riferimento vengono aggiornate con nuovi collegamenti alle versioni libreria aggiornate. Una volta scaduta la cache del browser per una determinata pagina HTML, non c&#39;è motivo di preoccuparsi che le vecchie librerie vengano caricate dalla cache del browser, dal momento che la pagina aggiornata (da AEM) ora fa riferimento alle nuove versioni delle librerie. In altre parole, una pagina HTML aggiornata includerà tutte le versioni libreria più recenti.
