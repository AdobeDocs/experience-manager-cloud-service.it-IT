---
title: Migrazione della configurazione del Dispatcher da AMS a AEM come Cloud Service
description: 'Migrazione della configurazione del Dispatcher da AMS a AEM come Cloud Service '
feature: Dispatcher
source-git-commit: 4be76f19c27aeab84de388106a440434a99a738c
workflow-type: tm+mt
source-wordcount: '1447'
ht-degree: 14%

---

# Migrazione della configurazione del Dispatcher da AMS a AEM come Cloud Service {#Dispatcher-in-the-cloud}

## Differenze principali tra AMS Dispatcher e AEM come Cloud Service {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

La configurazione di Apache e Dispatcher in AEM as a Cloud Service è abbastanza simile a quella di AMS. Le principali differenze sono:

* In AEM come Cloud Service, alcune direttive Apache potrebbero non essere utilizzate (ad esempio `Listen` o `LogLevel`)
* In AEM come Cloud Service, è possibile inserire solo alcuni elementi della configurazione di Dispatcher nei file di inclusione e la loro denominazione è importante. Ad esempio, le regole di filtro da riutilizzare tra host diversi devono essere inserite in un file denominato `filters/filters.any`. Per ulteriori informazioni, consulta la pagina di riferimento .
* In AEM come Cloud Service esiste una convalida aggiuntiva per impedire che le regole di filtro scritte utilizzando `/glob` impediscano problemi di sicurezza. Poiché verrà utilizzato `deny *` anziché `allow *` (che non può essere utilizzato), i clienti trarranno vantaggio dall’esecuzione del Dispatcher localmente e dall’esecuzione di prove ed errori, guardando i registri per sapere esattamente quali percorsi i filtri del Dispatcher bloccano per poterli aggiungere.

## Linee guida per la migrazione della configurazione del dispatcher da AMS a AEM come Cloud Service

La struttura di configurazione del Dispatcher presenta differenze tra Managed Services e AEM come Cloud Service. Di seguito è riportata una guida passo passo su come migrare dalla configurazione di AMS Dispatcher versione 2 a AEM come Cloud Service.

## Come convertire una configurazione AMS in una configurazione Dispatcher di AEM as a Cloud Service

La sezione seguente fornisce istruzioni dettagliate su come convertire una configurazione AMS. Si assume
che disponi di un archivio con una struttura simile a quella descritta in [Configurazione del Dispatcher di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

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
