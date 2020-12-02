---
title: Memorizzazione in cache in AEM as a Cloud Service
description: 'Memorizzazione in cache in AEM as a Cloud Service '
translation-type: tm+mt
source-git-commit: 0e414de936267cb4648c3078720b198e00c4a3cb
workflow-type: tm+mt
source-wordcount: '1479'
ht-degree: 1%

---


# Introduzione {#intro}

Il traffico passa attraverso la CDN a un livello di server Web Apache, che supporta i moduli incluso il dispatcher. Per migliorare le prestazioni, il dispatcher viene utilizzato principalmente come cache per limitare l’elaborazione sui nodi di pubblicazione.
È possibile applicare delle regole alla configurazione del dispatcher per modificare eventuali impostazioni predefinite di scadenza della cache, con conseguente caching alla rete CDN. Tenere presente che il dispatcher rispetta anche le intestazioni di scadenza della cache risultanti se `enableTTL` è abilitato nella configurazione del dispatcher, il che implica che aggiornerà contenuto specifico anche al di fuori del contenuto in fase di ripubblicazione.

Questa pagina descrive inoltre come la cache del dispatcher viene invalidata, nonché come funziona il caching a livello di browser per quanto riguarda le librerie lato client.

## Cache {#caching}

### HTML/Testo {#html-text}

* per impostazione predefinita, è memorizzata nella cache dal browser per cinque minuti, in base all’intestazione del controllo cache emesso dal livello apache. Anche la CDN rispetta questo valore.
* può essere ignorato per tutto il contenuto HTML/Testo definendo la variabile `EXPIRATION_TIME` in `global.vars` utilizzando il AEM come strumenti di Cloud Service SDK Dispatcher.
* possono essere sostituiti a un livello di granulosità più sottile dalle seguenti direttive apache mod_header:

   ```
   <LocationMatch "\.(html)$">
        Header set Cache-Control "max-age=200"
        Header set Age 0
   </LocationMatch>
   ```

   Fate attenzione quando impostate intestazioni di controllo cache globali o che corrispondono a un&#39;area ampia, in modo che non vengano applicate al contenuto che intendete mantenere privato. Valutare la possibilità di utilizzare più direttive per garantire che le regole siano applicate in modo preciso. Detto questo, AEM come Cloud Service rimuovere l&#39;intestazione della cache se rileva che è stata applicata a ciò che rileva come non possa essere memorizzata nella cache dal dispatcher, come descritto nella documentazione del dispatcher. Per obbligare AEM ad applicare sempre la memorizzazione nella cache, è possibile aggiungere l&#39;opzione &quot;always&quot; come segue:

   ```
   <LocationMatch "\.(html)$">
        Header always set Cache-Control "max-age=200"
        Header set Age 0
   </LocationMatch>
   ```

   È necessario assicurarsi che un file in `src/conf.dispatcher.d/cache` disponga della regola seguente (che si trova nella configurazione predefinita):

   ```
   /0000
   { /glob "*" /type "allow" }
   ```

* Per evitare che un contenuto specifico venga memorizzato nella cache, impostate l&#39;intestazione Cache-Control su *private*. Ad esempio, quanto segue impedisce al contenuto HTML in una directory denominata **myfolder** di essere memorizzato nella cache:

   ```
      <LocationMatch "/myfolder/.*\.(html)$">.  // replace with the right regex
      Header set Cache-Control “private”
     </LocationMatch>
   ```

   >[!NOTE]
   >Gli altri metodi, incluso il progetto [dispatcher-ttl AEM ACS Commons Project](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), non sostituiranno correttamente i valori.

### Librerie lato client (js,css) {#client-side-libraries}

* utilizzando AEM framework di libreria lato client, i codici JavaScript e CSS vengono generati in modo tale che i browser possano memorizzarli nella cache in modo indefinito, poiché qualsiasi modifica si manifesta come nuovo file con un percorso univoco.  In altre parole, il codice HTML che fa riferimento alle librerie client verrà prodotto come necessario, in modo che i clienti possano provare nuovi contenuti mentre vengono pubblicati. Il controllo della cache è impostato su &quot;immutabile&quot; o su 30 giorni per i browser meno recenti che non rispettano il valore &quot;immutabile&quot;.
* per ulteriori informazioni, vedere la sezione [Librerie lato client e coerenza delle versioni](#content-consistency).

### Immagini e contenuti sufficientemente grandi memorizzati in archivio BLOB {#images}

* per impostazione predefinita, non memorizzato nella cache
* può essere impostato su un livello di granulosità più fine dalle seguenti direttive apache `mod_headers`:

   ```
      <LocationMatch "^\.*.(jpeg|jpg)$">
        Header set Cache-Control "max-age=222"
        Header set Age 0
      </LocationMatch>
   ```

   Consultate la discussione nella sezione html/testo precedente per fare attenzione a non memorizzare troppo nella cache e a forzare AEM applicare sempre la cache con l&#39;opzione &quot;always&quot;.

   È necessario assicurarsi che un file in `src/conf.dispatcher.d/`cache abbia la seguente regola (che si trova nella configurazione predefinita):

   ```
   /0000
   { /glob "*" /type "allow" }
   ```

   Accertatevi che le risorse da mantenere private anziché nella cache non facciano parte dei filtri di direttiva LocationMatch.

   >[!NOTE]
   >Gli altri metodi, incluso il progetto [dispatcher-ttl AEM ACS Commons Project](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), non sostituiranno correttamente i valori.

### Altri tipi di file di contenuto nell&#39;archivio nodi {#other-content}

* nessuna cache predefinita
* il valore predefinito non può essere impostato con la variabile `EXPIRATION_TIME` utilizzata per i tipi di file html/text
* la scadenza della cache può essere impostata con la stessa strategia LocationMatch descritta nella sezione html/text specificando il regex appropriato

## Annullamento validità cache del dispatcher {#disp}

In generale, non sarà necessario annullare la validità della cache del dispatcher. È invece necessario fare affidamento sul dispatcher che aggiorna la cache quando il contenuto viene ripubblicato e la CDN rispetta le intestazioni di scadenza della cache.

### Annullamento della validità della cache del dispatcher durante l&#39;attivazione/disattivazione {#cache-activation-deactivation}

Come nelle versioni precedenti di AEM, la pubblicazione o l’annullamento della pubblicazione di pagine eliminerà il contenuto dalla cache del dispatcher. Se si sospetta un problema di caching, i clienti devono ripubblicare le pagine in questione.

Quando l’istanza di pubblicazione riceve una nuova versione di una pagina o di una risorsa dall’autore, utilizza l’agente di eliminazione per annullare i percorsi appropriati nel dispatcher. Il percorso aggiornato viene rimosso dalla cache del dispatcher, insieme ai relativi elementi principali, fino a un livello (è possibile configurarlo con [statfileslevel](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level).

### Annullamento della validità della cache del dispatcher esplicito {#explicit-invalidation}

In generale, non sarà necessario annullare manualmente il contenuto nel dispatcher, ma è possibile, se necessario, come descritto di seguito.

Prima di AEM come Cloud Service, esistevano due modi per invalidare la cache del dispatcher.

1. Richiamate l&#39;agente di replica, specificando l&#39;agente di eliminazione del dispatcher di pubblicazione
2. Chiamata diretta all&#39;API `invalidate.cache` (ad esempio, `POST /dispatcher/invalidate.cache`)

L&#39;approccio `invalidate.cache` dell&#39;API del dispatcher non sarà più supportato, in quanto riguarda solo un nodo dispatcher specifico. AEM come Cloud Service opera a livello di servizio, non a livello di singolo nodo, pertanto le istruzioni di annullamento della convalida nella pagina [Invalidazione delle pagine memorizzate nella cache da AEM](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/page-invalidate.html) non sono più valide per AEM come Cloud Service.
Utilizzare invece l&#39;agente di flush di replica. Questa operazione può essere eseguita utilizzando l&#39;API Replication. La documentazione relativa alle API di replica è disponibile [qui](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/Replicator.html) e per un esempio di svuotamento della cache, vedere la [pagina di esempio delle API](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) nello specifico l&#39; `CustomStep` esempio che emette un&#39;azione di replica di tipo ACTIVATE per tutti gli agenti disponibili. L&#39;endpoint dell&#39;agente di flush non è configurabile ma preconfigurato per puntare al dispatcher, associato al servizio di pubblicazione che esegue l&#39;agente di flush. L&#39;agente di flush può in genere essere attivato da eventi OSGi o flussi di lavoro.

Il diagramma presentato di seguito illustra questo punto.

![](assets/cdnd.png "CDNCDN")

In caso di problemi di cancellazione della cache del dispatcher, contattare l&#39; [assistenza clienti](https://helpx.adobe.com/support.ec.html) che, se necessario, può cancellare la cache del dispatcher.

La  CDN gestita dal Adobe rispetta i TTL e pertanto non è necessario scaricarla. Se si sospetta un problema, [contattare il supporto clienti](https://helpx.adobe.com/support.ec.html) che può cancellare una cache CDN gestita dal Adobe  secondo necessità.

## Librerie lato client e coerenza delle versioni {#content-consistency}

Le pagine sono composte da HTML, JavaScript, CSS e immagini. I clienti sono invitati a utilizzare il framework [Client-Side Libraries (clientlibs)](/help/implementing/developing/introduction/clientlibs.md) per importare risorse Javascript e CSS in pagine HTML, tenendo conto delle dipendenze tra librerie JS.

Il framework clientlibs fornisce la gestione automatica delle versioni, consentendo agli sviluppatori di archiviare le modifiche apportate alle librerie JS nel controllo del codice sorgente e rendendo disponibile l&#39;ultima versione al momento del rilascio da parte del cliente. In caso contrario, gli sviluppatori dovrebbero modificare manualmente il codice HTML con i riferimenti alla nuova versione della libreria, il che è particolarmente costoso se molti modelli HTML condividono la stessa libreria.

Quando le nuove versioni delle librerie vengono rilasciate in produzione, le pagine HTML di riferimento vengono aggiornate con nuovi collegamenti alle versioni libreria aggiornate. Una volta scaduta la cache del browser per una determinata pagina HTML, non c&#39;è alcun problema che le vecchie librerie vengano caricate dalla cache del browser, dal momento che la pagina aggiornata (da AEM) ora fa riferimento alle nuove versioni delle librerie. In altre parole, una pagina HTML aggiornata includerà tutte le versioni libreria più recenti.

Il meccanismo di questo è un hash serializzato, che viene aggiunto al collegamento della libreria client, garantendo un URL univoco con le versioni affinché il browser memorizzi nella cache CSS/JS. L&#39;hash serializzato viene aggiornato solo quando il contenuto della libreria client cambia. Ciò significa che, se si verificano aggiornamenti non correlati (ovvero nessuna modifica al css/js sottostante della libreria client) anche con una nuova distribuzione, il riferimento rimane lo stesso, garantendo meno interruzioni nella cache del browser.

### Abilitazione delle versioni Longcache delle librerie lato client - AEM come avvio rapido dell&#39;SDK di Cloud Service {#enabling-longcache}

clientlib predefinite in una pagina HTML sono simili a quelle dell&#39;esempio seguente:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

Quando la funzione di controllo delle versioni di clientlib rigorose è abilitata, nella libreria client viene aggiunta una chiave hash a lungo termine come selettore. Di conseguenza, il riferimento clientlib sarà simile al seguente:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

Il controllo delle versioni clientlib rigorose è attivato per impostazione predefinita in tutti i AEM come ambienti di Cloud Service.

Per abilitare il controllo delle versioni di clientlib rigorose nell’SDK Quickstart locale, effettua le seguenti operazioni:

1. Passare a Gestione configurazione OSGi `<host>/system/console/configMgr`
1. Trovate la configurazione OSGi per  Adobe Granite HTML Library Manager:
   * Selezionare la casella di controllo per abilitare il controllo delle versioni rigorose
   * Nel campo con l&#39;etichetta Chiave cache lato client a lungo termine, immettere il valore di /.*;hash
1. Salva le modifiche. Non è necessario salvare questa configurazione nel controllo del codice sorgente, poiché AEM come Cloud Service attiverà automaticamente questa configurazione negli ambienti di sviluppo, fase e produzione.
1. Ogni volta che il contenuto della libreria client viene modificato, viene generata una nuova chiave hash e il riferimento HTML verrà aggiornato.
