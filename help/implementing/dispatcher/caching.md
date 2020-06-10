---
title: Memorizzazione nella cache di AEM come servizio cloud
description: 'Memorizzazione nella cache di AEM come servizio cloud '
translation-type: tm+mt
source-git-commit: 9d99a7513a3a912b37ceff327e58a962cc17c627
workflow-type: tm+mt
source-wordcount: '1358'
ht-degree: 0%

---


# Introduzione {#intro}

Il traffico passa attraverso la CDN a un livello di server Web Apache, che supporta i moduli incluso il dispatcher. Per migliorare le prestazioni, il dispatcher viene utilizzato principalmente come cache per limitare l’elaborazione sui nodi di pubblicazione.
È possibile applicare delle regole alla configurazione del dispatcher per modificare eventuali impostazioni predefinite di scadenza della cache, con conseguente caching alla rete CDN. Il dispatcher rispetta anche le intestazioni di scadenza della cache risultanti se `enableTTL` è abilitato nella configurazione del dispatcher, il che implica che aggiornerà contenuto specifico anche al di fuori del contenuto che viene ripubblicato.

Questa pagina descrive inoltre come la cache del dispatcher viene invalidata, nonché come funziona il caching a livello di browser per quanto riguarda le librerie lato client.

## Caching {#caching}

### HTML/Testo {#html-text}

* per impostazione predefinita, è memorizzata nella cache dal browser per cinque minuti, in base all’intestazione del controllo cache emesso dal livello apache. Anche la CDN rispetta questo valore.
* può essere ignorato per tutto il contenuto HTML/Testo definendo la `EXPIRATION_TIME` variabile in `global.vars` AEM come strumenti Dispatcher SDK di Servizi cloud.
* possono essere sostituiti a un livello di granulosità più sottile dalle seguenti direttive apache mod_header:

```
<LocationMatch "\.(html)$">
        Header set Cache-Control "max-age=200"
</LocationMatch>
```

È necessario assicurarsi che un file con `src/conf.dispatcher.d/cache` la regola seguente (che si trova nella configurazione predefinita):

```
/0000
{ /glob "*" /type "allow" }
```

* Per evitare che un contenuto specifico venga memorizzato nella cache, impostate l&#39;intestazione Cache-Control su &quot;private&quot;. Ad esempio, quanto segue impedisce che il contenuto HTML in una directory denominata &quot;myfolder&quot; venga memorizzato nella cache:

```
<LocationMatch "\/myfolder\/.*\.(html)$">.  // replace with the right regex
    Header set Cache-Control “private”
</LocationMatch>
```

* Altri metodi, incluso il progetto [AEM ACS](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/)dispatcher-ttl, non sostituiranno correttamente i valori.

### Librerie lato client (js, css) {#client-side-libraries}

* utilizzando il framework di libreria lato client di AEM, il codice JavaScript e CSS viene generato in modo tale che i browser possano memorizzarlo nella cache in modo indefinito, dal momento che qualsiasi modifica si verifica come nuovi file con un percorso univoco.  In altre parole, il codice HTML che fa riferimento alle librerie client verrà prodotto come necessario, in modo che i clienti possano provare nuovi contenuti mentre vengono pubblicati. Il controllo della cache è impostato su &quot;immutabile&quot; o su 30 giorni per i browser meno recenti che non rispettano il valore &quot;immutabile&quot;.
* per ulteriori dettagli, consultate la sezione [Librerie lato client e coerenza](#content-consistency) delle versioni.

### Immagini e contenuti sufficientemente grandi memorizzati in archivio BLOB {#images}

* per impostazione predefinita, non memorizzato nella cache
* può essere fissato a un livello di grana più fine dalle seguenti `mod_headers` direttive apache:

```
<LocationMatch "^.*.jpeg$">
    Header set Cache-Control "max-age=222"
</LocationMatch>
```

È necessario assicurarsi che un file in src/conf.dispatcher.d/cache abbia la seguente regola (che si trova nella configurazione predefinita):

```
/0000
{ /glob "*" /type "allow" }
```

Accertatevi che le risorse da mantenere private anziché nella cache non facciano parte dei filtri di direttiva LocationMatch.

* Altri metodi, incluso il progetto [AEM ACS](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/)dispatcher-ttl, non sostituiranno correttamente i valori.

### Altri tipi di file di contenuto nell&#39;archivio nodi {#other-content}

* nessuna cache predefinita
* impossibile impostare il valore predefinito con la `EXPIRATION_TIME` variabile utilizzata per i tipi di file html/text
* la scadenza della cache può essere impostata con la stessa strategia LocationMatch descritta nella sezione html/text specificando il regex appropriato

## Annullamento validità cache del dispatcher {#disp}

In generale, non dovrebbe essere necessario annullare la validità della cache del dispatcher. È invece necessario fare affidamento sul dispatcher, che aggiorna la cache quando il contenuto viene ripubblicato, e sul CDN che rispetta le intestazioni di scadenza della cache.

### Annullamento della validità della cache del dispatcher durante l&#39;attivazione/disattivazione {#cache-activation-deactivation}

Come nelle versioni precedenti di AEM, la pubblicazione o l’annullamento della pubblicazione di pagine eliminerà il contenuto dalla cache del dispatcher. Se si sospetta un problema di caching, i clienti devono ripubblicare le pagine in questione.

Quando l’istanza di pubblicazione riceve una nuova versione di una pagina o di una risorsa dall’autore, utilizza l’agente di eliminazione per annullare i percorsi appropriati nel dispatcher. Il percorso aggiornato viene rimosso dalla cache del dispatcher, insieme ai relativi elementi principali, fino a un livello (è possibile configurarlo con [statfileslevel](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level)).

### Annullamento della validità della cache del dispatcher esplicito {#explicit-invalidation}

In generale, non sarà necessario annullare manualmente il contenuto nel dispatcher, ma è possibile, se necessario, come descritto di seguito.

Prima di AEM come servizio cloud, erano disponibili due modi per annullare la validità della cache del dispatcher.

1. Richiamate l&#39;agente di replica, specificando l&#39;agente di eliminazione del dispatcher di pubblicazione
2. Chiamata diretta dell&#39; `invalidate.cache` API (ad esempio, `POST /dispatcher/invalidate.cache`)

L&#39;approccio `invalidate.cache` API del dispatcher non sarà più supportato in quanto si rivolge solo a un nodo dispatcher specifico. Poiché AEM come servizio cloud opera a livello di servizio, non a livello di singolo nodo, le istruzioni di annullamento della validità contenute nella pagina [Invalidazione delle pagine cache da AEM](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/page-invalidate.html) non sono più valide per AEM come servizio cloud.
Utilizzare invece l&#39;agente di flush di replica. Questa operazione può essere eseguita utilizzando l&#39;API Replication. La documentazione API di replica è disponibile [qui](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/Replicator.html) e per un esempio di svuotamento della cache, consultate la pagina [di esempio](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) API, in particolare l&#39; `CustomStep` esempio che emette un&#39;azione di replica di tipo ACTIVATE a tutti gli agenti disponibili. L&#39;endpoint dell&#39;agente di flush non è configurabile ma preconfigurato per puntare al dispatcher, associato al servizio di pubblicazione che esegue l&#39;agente di flush. L&#39;agente di flush può in genere essere attivato da eventi OSGi o flussi di lavoro.

Il diagramma presentato di seguito illustra questo punto.

![](assets/cdnd.png "CDNCDN")

In caso di problemi di cancellazione della cache del dispatcher, contattare il supporto [](https://helpx.adobe.com/support.ec.html) clienti che, se necessario, può cancellare la cache del dispatcher.

La rete CDN gestita da Adobe rispetta i TTL e non è quindi necessario scaricarla. Se si sospetta un problema, [contattate il supporto](https://helpx.adobe.com/support.ec.html) clienti che potrà cancellare una cache CDN gestita da Adobe in base alle esigenze.

## Librerie lato client e coerenza delle versioni {#content-consistency}

Le pagine sono composte da HTML, JavaScript, CSS e immagini. I clienti sono invitati a sfruttare il framework Client-Side Libraries (clientlibs) per importare risorse Javascript e CSS in pagine HTML, tenendo conto delle dipendenze tra librerie JS.

Il framework clientlibs fornisce la gestione automatica delle versioni, consentendo agli sviluppatori di archiviare le modifiche apportate alle librerie JS nel controllo del codice sorgente e rendendo disponibile l&#39;ultima versione al momento del rilascio da parte del cliente. In caso contrario, gli sviluppatori dovrebbero modificare manualmente il codice HTML con i riferimenti alla nuova versione della libreria, il che è particolarmente costoso se molti modelli HTML condividono la stessa libreria.

Quando le nuove versioni delle librerie vengono rilasciate in produzione, le pagine HTML di riferimento vengono aggiornate con nuovi collegamenti alle versioni libreria aggiornate. Una volta scaduta la cache del browser per una determinata pagina HTML, non c&#39;è motivo di preoccuparsi che le vecchie librerie vengano caricate dalla cache del browser, dal momento che la pagina aggiornata (da AEM) ora fa riferimento alle nuove versioni delle librerie. In altre parole, una pagina HTML aggiornata includerà tutte le versioni libreria più recenti.

Il meccanismo di questo è un hash serializzato, che viene aggiunto al collegamento della libreria client, garantendo un URL univoco con le versioni affinché il browser memorizzi nella cache CSS/JS. L&#39;hash serializzato viene aggiornato solo quando il contenuto della libreria client cambia. Ciò significa che, se si verificano aggiornamenti non correlati (ovvero nessuna modifica al css/js sottostante della libreria client) anche con una nuova distribuzione, il riferimento rimane lo stesso, garantendo meno interruzioni nella cache del browser.

### Abilitazione delle versioni Longcache delle librerie lato client - AEM come servizio cloud - Avvio rapido SDK {#enabling-longcache}

clientlib predefinite in una pagina HTML sono simili a quelle dell&#39;esempio seguente:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

Quando la funzione di controllo delle versioni di clientlib rigorose è abilitata, nella libreria client viene aggiunta una chiave hash a lungo termine come selettore. Di conseguenza, il riferimento clientlib sarà simile al seguente:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

Il controllo delle versioni clientlib rigorose è abilitato per impostazione predefinita in tutti gli ambienti AEM come servizio cloud.

Per abilitare il controllo delle versioni di clientlib rigorose nell’SDK Quickstart locale, effettua le seguenti operazioni:

1. Passa a Gestione configurazione OSGi `<host>/system/console/configMgr`
1. Trovate il file di configurazione OSGi per Adobe Granite HTML Library Manager:
   * Selezionare la casella di controllo per abilitare il controllo delle versioni rigorose
   * Nel campo con l&#39;etichetta Chiave cache lato client a lungo termine, immettere il valore di /.*;hash
1. Salva le modifiche. Non è necessario salvare questa configurazione nel controllo del codice sorgente, in quanto AEM come servizio cloud attiverà automaticamente questa configurazione negli ambienti di sviluppo, fase e produzione.
1. Ogni volta che il contenuto della libreria client viene modificato, viene generata una nuova chiave hash e il riferimento HTML verrà aggiornato.
