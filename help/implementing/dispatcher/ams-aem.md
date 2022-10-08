---
title: Migrazione della configurazione Dispatcher da AMS a AEM as a Cloud Service
description: Migrazione della configurazione Dispatcher da AMS a AEM as a Cloud Service
feature: Dispatcher
exl-id: ff7397dd-b6e1-4d08-8e2d-d613af6b81b3
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '1447'
ht-degree: 17%

---

# Migrazione della configurazione Dispatcher da AMS a AEM as a Cloud Service {#Dispatcher-in-the-cloud}

## Differenze principali tra AMS Dispatcher e AEM as a Cloud Service {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

La configurazione di Apache e Dispatcher in AEM as a Cloud Service è abbastanza simile a quella di AMS. Le principali differenze sono:

* In AEM as a Cloud Service, alcune direttive Apache potrebbero non essere utilizzate (ad esempio `Listen` o `LogLevel`)
* In AEM as a Cloud Service, è possibile inserire solo alcuni elementi della configurazione di Dispatcher nei file di inclusione e la loro denominazione è importante. Ad esempio, le regole di filtro da riutilizzare tra host diversi devono essere inserite in un file denominato `filters/filters.any`. Per ulteriori informazioni, consulta la pagina di riferimento .
* In AEM as a Cloud Service esiste una convalida aggiuntiva per impedire la scrittura di regole di filtro utilizzando `/glob` per evitare problemi di sicurezza. Da `deny *` saranno utilizzati anziché `allow *` (che non può essere utilizzato), i clienti trarranno vantaggio dall’esecuzione del Dispatcher localmente e dall’esecuzione di prove ed errori, dalla ricerca dei registri per sapere esattamente quali percorsi i filtri del Dispatcher bloccano per poterli aggiungere.

## Linee guida per la migrazione della configurazione del dispatcher da AMS a AEM as a Cloud Service

La struttura di configurazione del Dispatcher presenta differenze tra Managed Services e AEM as a Cloud Service. Di seguito è riportata una guida dettagliata su come migrare dalla configurazione di AMS Dispatcher versione 2 a AEM as a Cloud Service.

## Come convertire una configurazione AMS in una configurazione Dispatcher di AEM as a Cloud Service

La sezione seguente fornisce istruzioni dettagliate su come convertire una configurazione AMS. Si parte dal presupposto che tu disponga di un archivio con una struttura simile a quella descritta in [Configurazione del Dispatcher di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

### Estrarre l’archivio e rimuovere un eventuale prefisso

Estrai l’archivio in una cartella e assicurati che le sottocartelle immediate inizino con `conf`, `conf.d`,
`conf.dispatcher.d` e `conf.modules.d`. Se non lo fanno, spostali verso l&#39;alto nella gerarchia.

### Eliminare le sottocartelle e i file non utilizzati

Rimuovere le sottocartelle `conf` e `conf.modules.d`, nonché i file corrispondenti `conf.d/*.conf`.

### Eliminare tutti gli host virtuali non relativi alla pubblicazione

Rimuovi i file host virtuali in `conf.d/enabled_vhosts` che `author`, `unhealthy`, `health`,
`lc` o `flush` a nome. Tutti i file host virtuali in `conf.d/available_vhosts` che non sono collegati a possono essere rimossi.

### Rimuovere o impostare come commento le sezioni di host virtuali che non fanno riferimento alla porta 80

Se i file host virtuali contengono ancora sezioni che fanno riferimento esclusivamente a porte diverse dalla porta 80, ad esempio:

```
<VirtualHost *:443>
...
</VirtualHost>
```

rimuovile o impostale come commenti. Le istruzioni di queste sezioni non verranno elaborate, ma se le mantieni potresti comunque finire per modificarle senza alcun effetto, il che creerebbe confusione.

### Verificare la directory rewrites

Immettere la directory `conf.d/rewrites`.

Rimuovi i file denominati `base_rewrite.rules` e `xforwarded_forcessl_rewrite.rules` e ricorda di rimuovere `Include` istruzioni nei file host virtuali che vi fanno riferimento.

Se `conf.d/rewrites` ora contiene un singolo file, deve essere rinominato in `rewrite.rules` e non dimenticare di adattare il `Include` istruzioni che fanno riferimento a tale file anche nei file host virtuali.

Se tuttavia la cartella contiene più file specifici dell’host virtuale, il loro contenuto deve essere copiato nel `Include` istruzioni che fanno riferimento a tali file nei file host virtuali.

### Verificare la directory variables

Immettere la directory `conf.d/variables`.

Rimuovi i file denominati `ams_default.vars` e ricorda di rimuovere `Include` istruzioni nei file host virtuali che vi fanno riferimento.

Se `conf.d/variables` ora contiene un singolo file, deve essere rinominato in `custom.vars` e non dimenticare di adattare il `Include` istruzioni che fanno riferimento a tale file anche nei file host virtuali.

Se tuttavia la cartella contiene più file specifici dell’host virtuale, il loro contenuto deve essere copiato nel `Include` istruzioni che fanno riferimento a tali file nei file host virtuali.

### Rimuovi inseriti nell&#39;elenco Consentiti

Rimuovi la cartella `conf.d/whitelists` e rimuovere `Include` istruzioni nei file host virtuali che fanno riferimento ad alcuni file presenti nella sottocartella.

### Sostituire le variabili non più disponibili

In tutti i file host virtuali:

Rinomina `PUBLISH_DOCROOT` a `DOCROOT`
Rimuovi le sezioni che fanno riferimento a variabili denominate `DISP_ID`, `PUBLISH_FORCE_SSL` o `PUBLISH_WHITELIST_ENABLED`

### Controllare lo stato eseguendo la convalida

Esegui la convalida del Dispatcher nella directory con il `httpd` sottocomando:

```
$ validator httpd .
```

Se si verificano degli errori relativi a file di inclusione mancanti, verifica di aver rinominato correttamente tali file.

Se vengono visualizzate direttive Apache che non sono inserite nell&#39;elenco Consentiti, rimuovile.

### Eliminare tutte le farm non relative alla pubblicazione

Rimuovi i file di farm in `conf.dispatcher.d/enabled_farms` che `author`, `unhealthy`, `health`,
`lc` o `flush` a nome. Tutti i file di farm in `conf.dispatcher.d/available_farms` che non sono collegati a possono essere rimossi.

### Rinominare i file di farm

Tutte le aziende agricole `conf.d/enabled_farms` deve essere rinominato per corrispondere al pattern `*.farm`ad esempio un file farm denominato `customerX_farm.any` deve essere rinominato `customerX.farm`.

### Verificare la cache

Immettere la directory `conf.dispatcher.d/cache`.

Rimuovi eventuali file con prefisso `ams_`.

Se `conf.dispatcher.d/cache` è ora vuoto, copia il file `conf.dispatcher.d/cache/rules.any`
dalla configurazione standard di Dispatcher a questa cartella. La configurazione standard di Dispatcher si trova nella cartella `src` di questo SDK. Non dimenticarti di adattare le
`$include` dichiarazioni che fanno riferimento al `ams_*_cache.any` file di regole anche nei file di farm.

Se invece `conf.dispatcher.d/cache` ora contiene un singolo file con suffisso `_cache.any`, deve essere rinominato in `rules.any` e non dimenticare di adattare il `$include` istruzioni che fanno riferimento a tale file anche nei file di farm.

Se tuttavia la cartella contiene più file specifici della farm con tale pattern, il relativo contenuto deve essere copiato nella cartella `$include` nei file farm.

Rimuovi i file con il suffisso `_invalidate_allowed.any`.

Copia il file `conf.dispatcher.d/cache/default_invalidate_any` dal AEM predefinito nella configurazione del Cloud Dispatcher a tale posizione.

In ciascun file di farm, rimuovi eventuali contenuti `cache/allowedClients` e sostituiscilo con:

```
$include "../cache/default_invalidate.any"
```

### Verificare la directory clientheaders

Immettere la directory `conf.dispatcher.d/clientheaders`.

Rimuovi eventuali file con prefisso `ams_`.

Se `conf.dispatcher.d/clientheaders` ora contiene un singolo file con suffisso `_clientheaders.any`, deve essere rinominato in `clientheaders.any` e non dimenticare di adattare il `$include` istruzioni che fanno riferimento a tale file anche nei file di farm.

Se tuttavia la cartella contiene più file specifici della farm con tale pattern, il relativo contenuto deve essere copiato nella cartella `$include` nei file farm.

Copia il file `conf.dispatcher/clientheaders/default_clientheaders.any` dalla configurazione di Dispatcher as a Cloud Service AEM predefinita a quella posizione.

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

Immettere la directory `conf.dispatcher.d/filters`.

Rimuovi eventuali file con prefisso `ams_`.

Se `conf.dispatcher.d/filters` ora contiene un singolo file a cui deve essere rinominato
`filters.any` e non dimenticare di adattare il `$include` istruzioni che fanno riferimento a tale file anche nei file di farm.

Se tuttavia la cartella contiene più file specifici della farm con tale pattern, il relativo contenuto deve essere copiato nella cartella `$include` nei file farm.

Copia il file `conf.dispatcher/filters/default_filters.any` dalla configurazione di Dispatcher as a Cloud Service AEM predefinita a quella posizione.

In ciascun file di farm, sostituisci le istruzioni di inclusione dei filtri come segue:

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

Copia il file `conf.dispatcher.d/renders/default_renders.any` dalla configurazione di Dispatcher as a Cloud Service AEM predefinita a quella posizione.

In ciascun file di farm, rimuovi eventuali contenuti `renders` e sostituiscilo con:

```
$include "../renders/default_renders.any"
```

### Verificare la directory virtualhosts

Rinomina la directory `conf.dispatcher.d/vhosts` a `conf.dispatcher.d/virtualhosts` e inseriscilo.

Rimuovi eventuali file con prefisso `ams_`.

Se `conf.dispatcher.d/virtualhosts` ora contiene un singolo file a cui deve essere rinominato
`virtualhosts.any` e non dimenticare di adattare il `$include` istruzioni che fanno riferimento a tale file anche nei file di farm.

Se tuttavia la cartella contiene più file specifici della farm con tale pattern, il relativo contenuto deve essere copiato nella cartella `$include` nei file farm.

Copia il file `conf.dispatcher/virtualhosts/default_virtualhosts.any` dalla configurazione di Dispatcher as a Cloud Service AEM predefinita a quella posizione.

In ciascun file di farm, sostituisci le istruzioni di inclusione dei filtri come segue:

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

con l’istruzione:

```
$include "../virtualhosts/default_virtualhosts.any"
```

### Controllare lo stato eseguendo la convalida

Esegui la convalida del Dispatcher as a Cloud Service AEM nella directory, con `dispatcher` sottocomando:

```
$ validator dispatcher .
```

Se si verificano degli errori relativi a file di inclusione mancanti, verifica di aver rinominato correttamente tali file.

Se vengono visualizzati errori relativi a una variabile `PUBLISH_DOCROOT` non definita, rinominala in `DOCROOT`.

Per qualsiasi altro errore, consulta la sezione Risoluzione di problemi della documentazione relativa allo strumento di convalida.

### Verifica la configurazione con un’implementazione locale (richiede l’installazione di Docker)

Utilizzo dello script `docker_run.sh` in AEM strumenti Dispatcher as a Cloud Service, puoi verificare che la configurazione non contenga altri errori che potrebbero verificarsi solo nella distribuzione:

### Passaggio 1: Genera informazioni di distribuzione con la convalida

```
validator full -d out .
```


In questo modo viene convalidata la configurazione completa e vengono generate le informazioni di implementazione in/`out`

### Passaggio 2: Avvia Dispatcher in un’immagine docker con tali informazioni di distribuzione

Con il server di pubblicazione AEM in esecuzione sul computer macOS, in ascolto sulla porta 4503, puoi avviare Dispatcher davanti a tale server come segue:

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

In questo modo verrà avviato il contenitore e Apache sarà esposto sulla porta locale 8080.

### Utilizza la nuova configurazione del Dispatcher

Congratulazioni! Se la funzione di convalida non segnala più alcun problema e il contenitore docker si avvia senza errori o avvisi, puoi spostare la configurazione in un `dispatcher/src` sottodirectory dell’archivio git.

**I clienti che utilizzano la versione 1 della configurazione di AMS Dispatcher devono contattare il supporto clienti per aiutarli a migrare dalla versione 1 alla versione 2, in modo da seguire le istruzioni di cui sopra.**
