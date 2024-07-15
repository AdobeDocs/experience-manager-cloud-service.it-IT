---
title: Migrazione della configurazione Dispatcher da AMS a AEM as a Cloud Service
description: Migrazione della configurazione Dispatcher da AMS a AEM as a Cloud Service
feature: Dispatcher
exl-id: ff7397dd-b6e1-4d08-8e2d-d613af6b81b3
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 7%

---

# Migrazione della configurazione Dispatcher da AMS a AEM as a Cloud Service {#Dispatcher-in-the-cloud}

## Differenze principali tra AMS Dispatcher e AEM as a Cloud Service {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

La configurazione di Apache e Dispatcher in AEM as a Cloud Service è molto simile a quella di AMS. Le principali differenze sono le seguenti:

* In AEM as a Cloud Service è possibile che alcune direttive Apache non vengano utilizzate (ad esempio, `Listen` o `LogLevel`)
* In AEM as a Cloud Service, solo alcune parti della configurazione Dispatcher possono essere inserite in file di inclusione e la loro denominazione è importante. Ad esempio, le regole di filtro che si desidera riutilizzare su host diversi devono essere inserite in un file denominato `filters/filters.any`. Per ulteriori informazioni, consulta la pagina di riferimento.
* In AEM as a Cloud Service è disponibile una convalida aggiuntiva per non consentire la scrittura di regole di filtro con `/glob` per evitare problemi di sicurezza. Poiché viene utilizzato `deny *` anziché `allow *` (che non può essere utilizzato), i clienti traggono vantaggio dall&#39;esecuzione locale di Dispatcher e dall&#39;esecuzione di tentativi ed errori, dall&#39;analisi dei registri per sapere esattamente quali percorsi i filtri di Dispatcher stanno bloccando per poter essere aggiunti.
* In AEM as a Cloud Service, attualmente si consiglia vivamente di [dare il consenso per utilizzare la modalità di origine flessibile della configurazione del dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug), ad esempio per utilizzare le pipeline di configurazione a livello web o per avere una maggiore flessibilità sul numero e sulla struttura dei file di configurazione.

## Linee guida per la migrazione della configurazione del dispatcher da AMS ad AEM as a Cloud Service

La struttura di configurazione di Dispatcher presenta delle differenze tra Managed Services e AEM as a Cloud Service. Di seguito è riportata una guida dettagliata su come migrare dalla configurazione AMS Dispatcher versione 2 ad AEM as a Cloud Service.

## Come convertire una configurazione AMS in una configurazione AEM as a Cloud Service Dispatcher

La sezione seguente fornisce istruzioni dettagliate su come convertire una configurazione AMS. Presuppone che
di disporre di un archivio con una struttura simile a quella descritta in [Configurazione di Cloud Manager Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

### Estrarre l’archivio e rimuovere un eventuale prefisso

Estrarre l&#39;archivio in una cartella e assicurarsi che le sottocartelle immediate inizino con `conf`, `conf.d`,
`conf.dispatcher.d` e `conf.modules.d`. In caso contrario, spostarli verso l&#39;alto nella gerarchia.

### Eliminare le sottocartelle e i file inutilizzati

Rimuovere le sottocartelle `conf` e `conf.modules.d` e i file corrispondenti a `conf.d/*.conf`.

### Eliminare tutti gli host virtuali non relativi alla pubblicazione

Rimuovi qualsiasi file host virtuale in `conf.d/enabled_vhosts` con `author`, `unhealthy`, `health`,
`lc` o `flush` nel suo nome. Tutti i file host virtuali in `conf.d/available_vhosts` che non
possono essere rimossi anche i collegamenti a.

### Rimuovere o impostare come commento le sezioni di host virtuali che non fanno riferimento alla porta 80

Se nei file host virtuali sono ancora presenti sezioni che fanno riferimento esclusivamente a porte diverse dalla porta 80, ad esempio:

```
<VirtualHost *:443>
...
</VirtualHost>
```

rimuovile o impostale come commenti. Le istruzioni in queste sezioni non verranno elaborate, ma se
se li mantieni, potresti comunque finire per modificarli senza alcun effetto, il che creerebbe confusione.

### Controlla riscritture

Immettere la directory `conf.d/rewrites`.

Rimuovi i file denominati `base_rewrite.rules` e `xforwarded_forcessl_rewrite.rules` e ricorda di
rimuovere `Include` istruzioni nei file host virtuali che vi fanno riferimento.

Se `conf.d/rewrites` contiene ora un singolo file, deve essere rinominato in `rewrite.rules` e non
dimentica di adattare le istruzioni `Include` che fanno riferimento a tale file anche nei file host virtuali.

Se tuttavia la cartella contiene più file virtuali specifici dell’host, il loro contenuto deve essere
copiato nell&#39;istruzione `Include` che vi fa riferimento nei file host virtuali.

### Controlla variabili

Immettere la directory `conf.d/variables`.

Rimuovi qualsiasi file denominato `ams_default.vars` e ricorda di rimuovere `Include` istruzioni nel file virtuale
ospita i file che vi fanno riferimento.

Se `conf.d/variables` contiene ora un singolo file, deve essere rinominato in `custom.vars` e non
dimentica di adattare le istruzioni `Include` che fanno riferimento a tale file anche nei file host virtuali.

Se tuttavia la cartella contiene più file virtuali specifici dell’host, il loro contenuto deve essere
copiato nell&#39;istruzione `Include` che vi fa riferimento nei file host virtuali.

### Inserire nell&#39;elenco Consentiti Rimuovi

Rimuovi la cartella `conf.d/whitelists` e le istruzioni `Include` nei file host virtuali che fanno riferimento a
alcuni file in tale sottocartella.

### Sostituisci le variabili non più disponibili

In tutti i file host virtuali:

Rinomina `PUBLISH_DOCROOT` in `DOCROOT`
Rimuovere le sezioni che fanno riferimento a variabili denominate `DISP_ID`, `PUBLISH_FORCE_SSL` o `PUBLISH_WHITELIST_ENABLED`

### Controllare lo stato eseguendo la convalida

Esegui la convalida Dispatcher nella directory, con il sottocomando `httpd`:

```
$ validator httpd .
```

Se vengono visualizzati errori relativi a file di inclusione mancanti, verifica di averli rinominati correttamente
file.

Se vengono visualizzate direttive Apache non inserite nell&#39;elenco Consentiti, rimuovile.

### Eliminare tutte le farm non relative alla pubblicazione

Rimuovi qualsiasi file di farm in `conf.dispatcher.d/enabled_farms` contenente `author`, `unhealthy`, `health`,
`lc` o `flush` nel suo nome. Tutti i file di farm in `conf.dispatcher.d/available_farms` che non sono
possono essere rimossi anche i collegamenti a.

### Rinominare i file farm

Tutte le farm in `conf.dispatcher.d/enabled_farms` devono essere rinominate in modo da corrispondere al pattern `*.farm`, ad esempio
il file farm denominato `customerX_farm.any` deve essere rinominato `customerX.farm`.

### Verifica cache

Immettere la directory `conf.dispatcher.d/cache`.

Rimuovi eventuali file con prefisso `ams_`.

Se `conf.dispatcher.d/cache` è vuoto, copiare il file `conf.dispatcher.d/cache/rules.any`
dalla configurazione standard di Dispatcher a questa cartella. Il Dispatcher standard
La configurazione si trova nella cartella `src` di questo SDK. Non dimenticare di adattare
`$include` istruzioni che fanno riferimento ai file di regole `ams_*_cache.any` nei file di farm
anche.

Se invece `conf.dispatcher.d/cache` ora contiene un singolo file con suffisso `_cache.any`,
deve essere rinominato in `rules.any` e non dimenticare di adattare le istruzioni `$include`
riferimento a tale file anche nei file di farm.

Se tuttavia la cartella contiene più file specifici della farm con tale pattern, il loro contenuto
deve essere copiato nell&#39;istruzione `$include` che vi fa riferimento nei file di farm.

Rimuovere i file con suffisso `_invalidate_allowed.any`.

Copia il file `conf.dispatcher.d/cache/default_invalidate_any` dal valore predefinito
AEM nella configurazione Cloud Dispatcher in quella posizione.

In ciascun file di farm, rimuovere il contenuto della sezione `cache/allowedClients` e sostituirlo
con:

```
$include "../cache/default_invalidate.any"
```

### Verifica intestazioni client

Immettere la directory `conf.dispatcher.d/clientheaders`.

Rimuovi eventuali file con prefisso `ams_`.

Se `conf.dispatcher.d/clientheaders` contiene ora un singolo file con suffisso `_clientheaders.any`,
deve essere rinominato in `clientheaders.any` e non dimenticare di adattare le istruzioni `$include`
riferimento a tale file anche nei file di farm.

Se tuttavia la cartella contiene più file specifici della farm con tale pattern, il loro contenuto
deve essere copiato nell&#39;istruzione `$include` che vi fa riferimento nei file di farm.

Copia il file `conf.dispatcher/clientheaders/default_clientheaders.any` dal valore predefinito
la configurazione di AEM as a Cloud Service Dispatcher in quella posizione.

In ciascun file di farm, sostituisci qualsiasi istruzione di inclusione clientheader di questo tipo:

```
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"
```

con l’istruzione:

```
$include "../clientheaders/default_clientheaders.any"
```

### Controlla filtro

Immettere la directory `conf.dispatcher.d/filters`.

Rimuovi eventuali file con prefisso `ams_`.

Se `conf.dispatcher.d/filters` ora contiene un singolo file, deve essere rinominato in
`filters.any` e non dimenticare di adattare le istruzioni `$include` che fanno riferimento a tale
anche nei file di farm.

Se tuttavia la cartella contiene più file specifici della farm con tale pattern, il loro contenuto
deve essere copiato nell&#39;istruzione `$include` che vi fa riferimento nei file di farm.

Copia il file `conf.dispatcher/filters/default_filters.any` dal valore predefinito
la configurazione di AEM as a Cloud Service Dispatcher in quella posizione.

In ciascun file di farm, sostituisci eventuali istruzioni di inclusione di questo tipo:

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

con l’istruzione:

```
$include "../filters/default_filters.any"
```

### Controlla rendering

Immettere la directory `conf.dispatcher.d/renders`.

Rimuovi tutti i file presenti nella cartella.

Copia il file `conf.dispatcher.d/renders/default_renders.any` dal valore predefinito
la configurazione di AEM as a Cloud Service Dispatcher in quella posizione.

In ciascun file di farm, rimuovere il contenuto della sezione `renders` e sostituirlo
con:

```
$include "../renders/default_renders.any"
```

### Controlla gli host virtuali

Rinominare la directory `conf.dispatcher.d/vhosts` in `conf.dispatcher.d/virtualhosts` e immetterla.

Rimuovi eventuali file con prefisso `ams_`.

Se `conf.dispatcher.d/virtualhosts` ora contiene un singolo file, deve essere rinominato in
`virtualhosts.any` e non dimenticare di adattare le istruzioni `$include` che fanno riferimento a tale
anche nei file di farm.

Se tuttavia la cartella contiene più file specifici della farm con tale pattern, il loro contenuto
deve essere copiato nell&#39;istruzione `$include` che vi fa riferimento nei file di farm.

Copia il file `conf.dispatcher/virtualhosts/default_virtualhosts.any` dal valore predefinito
la configurazione di AEM as a Cloud Service Dispatcher in quella posizione.

In ciascun file di farm, sostituisci eventuali istruzioni di inclusione di questo tipo:

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

con l’istruzione:

```
$include "../virtualhosts/default_virtualhosts.any"
```

### Controllare lo stato eseguendo la convalida

Esegui la convalida di AEM as a Cloud Service Dispatcher nella directory, con il sottocomando `dispatcher`:

```
$ validator dispatcher .
```

Se vengono visualizzati errori relativi a file di inclusione mancanti, verifica di averli rinominati correttamente
file.

Se vengono visualizzati errori relativi a una variabile `PUBLISH_DOCROOT` non definita, rinominala in `DOCROOT`.

Per ogni altro errore, consulta la sezione Risoluzione dei problemi del
documentazione relativa allo strumento di convalida.

### Verifica la configurazione con una distribuzione locale (richiede l’installazione di Docker)

Utilizzando lo script `docker_run.sh` negli strumenti Dispatcher di AEM as a Cloud Service, puoi verificare che
la configurazione non contiene altri errori che verrebbero visualizzati solo in
distribuzione:

### Passaggio 1: generare le informazioni di distribuzione con la convalida

```
validator full -d out .
```

In questo modo viene convalidata la configurazione completa e vengono generate le informazioni di distribuzione in `out`

### Passaggio 2: avvia Dispatcher in un’immagine docker con tali informazioni di distribuzione

Con il server di pubblicazione AEM in esecuzione sul computer macOS, in ascolto sulla porta 4503,
è possibile eseguire start the Dispatcher davanti al server nel modo seguente:

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

In questo modo verrà avviato il contenitore e Apache sarà esposto sulla porta locale 8080.

### Usa la nuova configurazione Dispatcher

Congratulazioni Se la convalida non segnala più alcun problema e il
il contenitore docker si avvia senza errori o avvisi.
pronto per spostare la configurazione in una sottodirectory `dispatcher/src`
dell’archivio Git.

**I clienti che utilizzano la versione 1 della configurazione di AMS Dispatcher devono contattare l&#39;assistenza clienti per aiutarli a migrare dalla versione 1 alla versione 2, in modo da poter seguire le istruzioni precedenti.**
