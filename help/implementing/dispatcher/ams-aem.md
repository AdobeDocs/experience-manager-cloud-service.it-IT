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

## Differenze principali tra Dispatcher AMS e AEM as a Cloud Service {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

La configurazione di Apache e Dispatcher in AEM as a Cloud Service è abbastanza simile a quella di AMS. Le principali differenze sono le seguenti:

* In AEM as a Cloud Service è possibile che alcune direttive Apache non vengano utilizzate (ad esempio, `Listen` o `LogLevel`)
* In AEM as a Cloud Service, solo alcune parti della configurazione di Dispatcher possono essere inserite in file di inclusione e la loro denominazione è importante. Ad esempio, le regole di filtro che desideri riutilizzare tra host diversi devono essere inserite in un file denominato `filters/filters.any`. Per ulteriori informazioni, consulta la pagina di riferimento.
* In AEM as a Cloud Service è disponibile una convalida aggiuntiva per non consentire la scrittura di regole di filtro tramite `/glob` per evitare problemi di sicurezza. Perché `deny *` viene utilizzato anziché `allow *` (che non può essere utilizzato), i clienti traggono vantaggio dall’esecuzione locale di Dispatcher e dall’esecuzione di tentativi ed errori, esaminando i registri per sapere esattamente quali percorsi i filtri di Dispatcher stanno bloccando per poter essere aggiunti.
* Nell’AEM as a Cloud Service è attualmente altamente raccomandato di [consenso per utilizzare la modalità di origine flessibile della configurazione di dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug) Ad esempio, per utilizzare le pipeline di configurazione a livello web o per avere una maggiore flessibilità sul numero e sulla struttura dei file di configurazione.

## Linee guida per la migrazione della configurazione del dispatcher da AMS a AEM as a Cloud Service

La struttura di configurazione del Dispatcher presenta delle differenze tra Managed Services e AEM as a Cloud Service. Di seguito è riportata una guida dettagliata su come migrare dalla versione 2 della configurazione del Dispatcher AMS a AEM as a Cloud Service.

## Come convertire una configurazione AMS in una configurazione AEM as a Cloud Service Dispatcher

La sezione seguente fornisce istruzioni dettagliate su come convertire una configurazione AMS. Si presuppone che tu disponga di un archivio con una struttura simile a quella descritta in [Configurazione del Dispatcher di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

### Estrarre l’archivio e rimuovere un eventuale prefisso

Estrai l’archivio in una cartella e assicurati che le sottocartelle immediate inizino con `conf`, `conf.d`,
`conf.dispatcher.d` e `conf.modules.d`. In caso contrario, spostarli verso l&#39;alto nella gerarchia.

### Eliminare le sottocartelle e i file inutilizzati

Rimuovi sottocartelle `conf` e `conf.modules.d`, e i file corrispondenti `conf.d/*.conf`.

### Eliminare tutti gli host virtuali non relativi alla pubblicazione

Rimuovi eventuali file host virtuali in `conf.d/enabled_vhosts` che ha `author`, `unhealthy`, `health`,
`lc` o `flush` nel suo nome. Tutti i file host virtuali in `conf.d/available_vhosts` possono essere rimossi anche quelli non collegati a.

### Rimuovere o impostare come commento le sezioni di host virtuali che non fanno riferimento alla porta 80

Se nei file host virtuali sono ancora presenti sezioni che fanno riferimento esclusivamente a porte diverse dalla porta 80, ad esempio:

```
<VirtualHost *:443>
...
</VirtualHost>
```

rimuovile o impostale come commenti. Le istruzioni in queste sezioni non verranno elaborate, ma se le mantieni potresti comunque finire per modificarle senza alcun effetto, il che creerebbe confusione.

### Controlla riscritture

Inserisci directory `conf.d/rewrites`.

Rimuovi qualsiasi file denominato `base_rewrite.rules` e `xforwarded_forcessl_rewrite.rules` e ricorda di rimuovere `Include` nei file host virtuali che vi fanno riferimento.

Se `conf.d/rewrites` ora contiene un singolo file, deve essere rinominato in `rewrite.rules` e non dimenticare di adattare il `Include` istruzioni che fanno riferimento a tale file anche nei file host virtuali.

Tuttavia, se la cartella contiene più file virtuali specifici dell’host, il loro contenuto deve essere copiato nel `Include` nei file host virtuali.

### Controlla variabili

Inserisci directory `conf.d/variables`.

Rimuovi qualsiasi file denominato `ams_default.vars` e ricorda di rimuovere `Include` nei file host virtuali che vi fanno riferimento.

Se `conf.d/variables` ora contiene un singolo file, deve essere rinominato in `custom.vars` e non dimenticare di adattare il `Include` istruzioni che fanno riferimento a tale file anche nei file host virtuali.

Tuttavia, se la cartella contiene più file virtuali specifici dell’host, il loro contenuto deve essere copiato nel `Include` nei file host virtuali.

### Inserire nell&#39;elenco Consentiti Rimuovi

Rimuovi la cartella `conf.d/whitelists` e rimuovere `Include` istruzioni nei file host virtuali che fanno riferimento ad alcuni file in tale sottocartella.

### Sostituisci le variabili non più disponibili

In tutti i file host virtuali:

Rinomina `PUBLISH_DOCROOT` a `DOCROOT`
Rimuovi le sezioni che fanno riferimento a variabili denominate `DISP_ID`, `PUBLISH_FORCE_SSL` o `PUBLISH_WHITELIST_ENABLED`

### Controllare lo stato eseguendo la convalida

Esegui la convalida del Dispatcher nella directory, con `httpd` sottocomando:

```
$ validator httpd .
```

Se vengono visualizzati errori relativi a file di inclusione mancanti, verifica di averli rinominati correttamente.

Se vengono visualizzate direttive Apache non inserite nell&#39;elenco Consentiti, rimuovile.

### Eliminare tutte le farm non relative alla pubblicazione

Rimuovi eventuali file di farm in `conf.dispatcher.d/enabled_farms` che ha `author`, `unhealthy`, `health`,
`lc` o `flush` nel suo nome. Tutti i file farm in `conf.dispatcher.d/available_farms` possono essere rimossi anche quelli non collegati a.

### Rinominare i file farm

Tutte le farm in `conf.dispatcher.d/enabled_farms` deve essere rinominato per corrispondere al pattern `*.farm`, quindi, ad esempio, un file farm denominato `customerX_farm.any` deve essere rinominato `customerX.farm`.

### Verifica cache

Inserisci directory `conf.dispatcher.d/cache`.

Rimuovi eventuali file con prefisso `ams_`.

Se `conf.dispatcher.d/cache` è ora vuoto, copia il file `conf.dispatcher.d/cache/rules.any`
dalla configurazione standard di Dispatcher a questa cartella. La configurazione standard del Dispatcher si trova nella cartella `src` di questo SDK. Non dimenticare di adattare
`$include` dichiarazioni che fanno riferimento alla `ams_*_cache.any` file delle regole anche nei file della farm.

Se invece `conf.dispatcher.d/cache` ora contiene un singolo file con suffisso `_cache.any`, deve essere rinominato in `rules.any` e non dimenticare di adattare il `$include` istruzioni che fanno riferimento a tale file anche nei file di farm.

Tuttavia, se la cartella contiene più file specifici della farm con tale pattern, il loro contenuto deve essere copiato nella cartella `$include` nei file di farm.

Rimuovi eventuali file con il suffisso `_invalidate_allowed.any`.

Copiare il file `conf.dispatcher.d/cache/default_invalidate_any` dall’AEM predefinito nella configurazione di Cloud Dispatcher a quella posizione.

In ciascun file di farm, rimuovi eventuali contenuti nel `cache/allowedClients` e sostituirla con:

```
$include "../cache/default_invalidate.any"
```

### Verifica intestazioni client

Inserisci directory `conf.dispatcher.d/clientheaders`.

Rimuovi eventuali file con prefisso `ams_`.

Se `conf.dispatcher.d/clientheaders` ora contiene un singolo file con suffisso `_clientheaders.any`, deve essere rinominato in `clientheaders.any` e non dimenticare di adattare il `$include` istruzioni che fanno riferimento a tale file anche nei file di farm.

Tuttavia, se la cartella contiene più file specifici della farm con tale pattern, il loro contenuto deve essere copiato nella cartella `$include` nei file di farm.

Copiare il file `conf.dispatcher/clientheaders/default_clientheaders.any` dalla configurazione di Dispatcher as a Cloud Service per l’AEM predefinita a quella posizione.

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

Inserisci directory `conf.dispatcher.d/filters`.

Rimuovi eventuali file con prefisso `ams_`.

Se `conf.dispatcher.d/filters` ora contiene un singolo file in cui deve essere rinominato
`filters.any` e non dimenticare di adattare il `$include` istruzioni che fanno riferimento a tale file anche nei file di farm.

Tuttavia, se la cartella contiene più file specifici della farm con tale pattern, il loro contenuto deve essere copiato nella cartella `$include` nei file di farm.

Copiare il file `conf.dispatcher/filters/default_filters.any` dalla configurazione di Dispatcher as a Cloud Service per l’AEM predefinita a quella posizione.

In ciascun file di farm, sostituisci eventuali istruzioni di inclusione di questo tipo:

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

con l’istruzione:

```
$include "../filters/default_filters.any"
```

### Controlla rendering

Inserisci directory `conf.dispatcher.d/renders`.

Rimuovi tutti i file presenti nella cartella.

Copiare il file `conf.dispatcher.d/renders/default_renders.any` dalla configurazione di Dispatcher as a Cloud Service per l’AEM predefinita a quella posizione.

In ciascun file di farm, rimuovi eventuali contenuti nel `renders` e sostituirla con:

```
$include "../renders/default_renders.any"
```

### Controlla gli host virtuali

Rinomina la directory `conf.dispatcher.d/vhosts` a `conf.dispatcher.d/virtualhosts` e inseriscilo.

Rimuovi eventuali file con prefisso `ams_`.

Se `conf.dispatcher.d/virtualhosts` ora contiene un singolo file in cui deve essere rinominato
`virtualhosts.any` e non dimenticare di adattare il `$include` istruzioni che fanno riferimento a tale file anche nei file di farm.

Tuttavia, se la cartella contiene più file specifici della farm con tale pattern, il loro contenuto deve essere copiato nella cartella `$include` nei file di farm.

Copiare il file `conf.dispatcher/virtualhosts/default_virtualhosts.any` dalla configurazione di Dispatcher as a Cloud Service per l’AEM predefinita a quella posizione.

In ciascun file di farm, sostituisci eventuali istruzioni di inclusione di questo tipo:

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

con l’istruzione:

```
$include "../virtualhosts/default_virtualhosts.any"
```

### Controllare lo stato eseguendo la convalida

Esegui la convalida del Dispatcher as a Cloud Service per l’AEM nella directory, con `dispatcher` sottocomando:

```
$ validator dispatcher .
```

Se vengono visualizzati errori relativi a file di inclusione mancanti, verifica di averli rinominati correttamente.

Se vengono visualizzati errori relativi a una variabile `PUBLISH_DOCROOT` non definita, rinominala in `DOCROOT`.

Per ogni altro errore, consulta la sezione Risoluzione dei problemi nella documentazione relativa allo strumento di convalida.

### Verifica la configurazione con una distribuzione locale (richiede l’installazione di Docker)

Utilizzo dello script `docker_run.sh` negli Strumenti di Dispatcher as a Cloud Service dall’AEM, puoi verificare che la configurazione non contenga altri errori che potrebbero verificarsi solo durante la distribuzione:

### Passaggio 1: generare le informazioni di distribuzione con la convalida

```
validator full -d out .
```

In questo modo viene convalidata la configurazione completa e vengono generate le informazioni di distribuzione in `out`

### Passaggio 2: avvia Dispatcher in un’immagine docker con tali informazioni di distribuzione

Con il server di pubblicazione AEM in esecuzione sul computer macOS, in ascolto sulla porta 4503, puoi avviare il Dispatcher prima di tale server nel modo seguente:

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

In questo modo verrà avviato il contenitore e Apache sarà esposto sulla porta locale 8080.

### Utilizza la nuova configurazione di Dispatcher

Congratulazioni Se la funzione di convalida non segnala più alcun problema e il contenitore docker si avvia senza errori o avvisi, puoi spostare la configurazione in un `dispatcher/src` sottodirectory dell’archivio Git.

**I clienti che utilizzano la versione 1 della configurazione del Dispatcher AMS devono contattare l’assistenza clienti per aiutarli a migrare dalla versione 1 alla versione 2, in modo da poter seguire le istruzioni precedenti.**
