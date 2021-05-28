---
title: Memorizzazione in cache in AEM as a Cloud Service
description: 'Memorizzazione in cache in AEM as a Cloud Service '
feature: Dispatcher
exl-id: 4206abd1-d669-4f7d-8ff4-8980d12be9d6
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1528'
ht-degree: 1%

---

# Introduzione {#intro}

Il traffico passa attraverso la CDN a un livello di server web Apache, che supporta moduli incluso il dispatcher. Per migliorare le prestazioni, il dispatcher viene utilizzato principalmente come cache per limitare l’elaborazione sui nodi di pubblicazione.
Le regole possono essere applicate alla configurazione del dispatcher per modificare eventuali impostazioni di scadenza della cache predefinite, con conseguente memorizzazione in cache nella CDN. Tieni presente che il dispatcher rispetta anche le intestazioni di scadenza della cache risultanti se `enableTTL` è abilitato nella configurazione del dispatcher, il che implica che aggiornerà contenuti specifici anche al di fuori del contenuto in fase di ripubblicazione.

Questa pagina descrive anche come la cache del dispatcher viene invalidata, nonché come funziona la memorizzazione in cache a livello di browser per quanto riguarda le librerie lato client.

## Memorizzazione in cache {#caching}

### HTML/Testo {#html-text}

* per impostazione predefinita, è stata memorizzata nella cache dal browser per cinque minuti, in base all&#39; `cache-control` intestazione emessa dal livello apache. Anche la CDN rispetta questo valore.
* l&#39;impostazione predefinita per la memorizzazione in cache HTML/testo può essere disabilitata definendo la variabile `DISABLE_DEFAULT_CACHING` in `global.vars`:

```
Define DISABLE_DEFAULT_CACHING
```

Ciò può essere utile, ad esempio, quando la logica di business richiede una regolazione precisa dell’intestazione di pagina (con un valore basato sul giorno del calendario), in quanto per impostazione predefinita l’intestazione di pagina è impostata su 0. Detto questo, **si prega di prestare attenzione quando si disattiva la memorizzazione in cache predefinita.**

* può essere ignorato per tutti i contenuti HTML/testo definendo la variabile `EXPIRATION_TIME` in `global.vars` utilizzando l’AEM come strumenti di Dispatcher SDK per Cloud Service.
* possono essere sovrascritti a un livello più granulare dalle seguenti direttive mod_headers apache:

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header set Cache-Control "max-age=200"
        Header set Age 0
   </LocationMatch>
   ```

   Fai attenzione quando imposti le intestazioni di controllo cache globale o quelle che corrispondono a un’area estesa in modo che non vengano applicate al contenuto che potresti voler mantenere privato. Valuta l’utilizzo di più direttive per garantire che le regole vengano applicate in modo dettagliato. Detto questo, AEM come Cloud Service rimuoverà l’intestazione della cache se rileva che è stata applicata a ciò che rileva come non può essere memorizzata nella cache dal dispatcher, come descritto nella documentazione del dispatcher. Per forzare AEM ad applicare sempre la memorizzazione in cache, è possibile aggiungere l’opzione &quot;sempre&quot; come segue:

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header always set Cache-Control "max-age=200"
        Header set Age 0
   </LocationMatch>
   ```

   È necessario assicurarsi che un file in `src/conf.dispatcher.d/cache` abbia la seguente regola (che si trova nella configurazione predefinita):

   ```
   /0000
   { /glob "*" /type "allow" }
   ```

* Per evitare che un contenuto specifico venga memorizzato nella cache, imposta l&#39;intestazione Cache-Control su *private*. Ad esempio, quanto segue impedisce la memorizzazione nella cache del contenuto HTML in una directory denominata **myfolder**:

   ```
      <LocationMatch "/content/myfolder/.*\.(html)$">.  // replace with the right regex
      Header set Cache-Control “private”
     </LocationMatch>
   ```

   >[!NOTE]
   >Gli altri metodi, incluso il [progetto ACS Commons AEM dispatcher-ttl](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), non sostituiranno correttamente i valori.

### Librerie lato client (js, css) {#client-side-libraries}

* utilizzando AEM framework di libreria lato client, i codici JavaScript e CSS vengono generati in modo tale che i browser possano memorizzarli nella cache a tempo indefinito, poiché qualsiasi modifica si manifesta come nuovi file con un percorso univoco.  In altre parole, l’HTML che fa riferimento alle librerie client verrà prodotto in base alle esigenze, in modo che i clienti possano vedere nuovi contenuti mentre vengono pubblicati. Il controllo della cache è impostato su &quot;immutabile&quot; o su 30 giorni per i browser meno recenti che non rispettano il valore &quot;immutabile&quot;.
* per ulteriori informazioni, consulta la sezione [Librerie lato client e coerenza delle versioni](#content-consistency) .

### Immagini e contenuti sufficientemente grandi archiviati in BLOB {#images}

* per impostazione predefinita, non memorizzato nella cache
* può essere impostato a un livello più granulare dalle seguenti direttive apache `mod_headers`:

   ```
      <LocationMatch "^/content/.*\.(jpeg|jpg)$">
        Header set Cache-Control "max-age=222"
        Header set Age 0
      </LocationMatch>
   ```

   Consulta la discussione nella sezione html/text di cui sopra per fare attenzione a non memorizzare la cache troppo su larga scala e anche su come forzare AEM ad applicare sempre la memorizzazione in cache con l&#39;opzione &quot;sempre&quot;.

   È necessario garantire che un file sotto `src/conf.dispatcher.d/`cache abbia la seguente regola (che si trova nella configurazione predefinita):

   ```
   /0000
   { /glob "*" /type "allow" }
   ```

   Assicurati che le risorse da mantenere private anziché memorizzate nella cache non facciano parte dei filtri di direttiva LocationMatch.

   >[!NOTE]
   >Gli altri metodi, incluso il [progetto ACS Commons AEM dispatcher-ttl](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), non sostituiranno correttamente i valori.

### Altri tipi di file di contenuto nell&#39;archivio nodi {#other-content}

* nessuna memorizzazione in cache predefinita
* il valore predefinito non può essere impostato con la variabile `EXPIRATION_TIME` utilizzata per i tipi di file html/text
* la scadenza della cache può essere impostata con la stessa strategia LocationMatch descritta nella sezione html/text specificando il regex appropriato

## Annullamento della validità della cache del dispatcher {#disp}

In generale, non sarà necessario annullare la validità della cache del dispatcher. Al contrario, dovresti affidarti all’aggiornamento della cache del dispatcher quando il contenuto viene ripubblicato e la CDN che rispetta le intestazioni di scadenza della cache.

### Annullamento della validità della cache del dispatcher durante l’attivazione/disattivazione {#cache-activation-deactivation}

Come nelle versioni precedenti di AEM, la pubblicazione o l’annullamento della pubblicazione di pagine cancella il contenuto dalla cache del dispatcher. Se si sospetta un problema di caching, i clienti devono ripubblicare le pagine in questione.

Quando l’istanza di pubblicazione riceve una nuova versione di una pagina o di una risorsa dall’autore, utilizza l’agente di eliminazione per annullare la validità dei percorsi appropriati sul proprio dispatcher. Il percorso aggiornato viene rimosso dalla cache del dispatcher, insieme ai relativi genitori, fino a un livello (puoi configurarlo con [statfileslevel](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level).

### Annullamento esplicito della validità della cache del dispatcher {#explicit-invalidation}

In generale, non sarà necessario annullare manualmente la validità del contenuto nel dispatcher, ma è possibile se necessario, come descritto di seguito.

Prima di AEM come Cloud Service, c&#39;erano due modi per invalidare la cache del dispatcher.

1. Richiama l’agente di replica, specificando l’agente di eliminazione del dispatcher di pubblicazione
2. Chiamata diretta dell’ API `invalidate.cache` (ad esempio, `POST /dispatcher/invalidate.cache`)

L’approccio API del dispatcher `invalidate.cache` non sarà più supportato in quanto si rivolge solo a un nodo specifico del dispatcher. AEM come Cloud Service funziona a livello di servizio, non a livello di singolo nodo, pertanto le istruzioni di invalidazione nella pagina [Invalidazione delle pagine in cache da AEM](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html) non sono più valide per AEM come Cloud Service .
È invece necessario utilizzare l&#39;agente di scaricamento della replica. Questa operazione può essere eseguita utilizzando l’API di replica. La documentazione sulle API di replica è disponibile [qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service-javadoc/com/day/cq/replication/Replicator.html) e per un esempio di scaricamento della cache, consulta la [pagina di esempio API](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) in particolare l’ esempio `CustomStep` che invia un’azione di replica di tipo ACTIVATE a tutti gli agenti disponibili. L’endpoint dell’agente di scaricamento non è configurabile ma preconfigurato per puntare al dispatcher, con corrispondenza con il servizio di pubblicazione che esegue l’agente di scaricamento. L’agente di scaricamento può in genere essere attivato da eventi o flussi di lavoro OSGi.

Il diagramma che segue illustra questo aspetto.

![](assets/cdnd.png "CDNCDN")

Se si teme che la cache del dispatcher non venga cancellata, contatta il [supporto clienti](https://helpx.adobe.com/support.ec.html) che può scaricare la cache del dispatcher se necessario.

La rete CDN gestita da Adobe rispetta i TTL e non è quindi necessario scaricarla. Se si sospetta un problema, [contatta il supporto clienti](https://helpx.adobe.com/support.ec.html) che può eseguire il flush di una cache CDN gestita da Adobe, se necessario.

## Librerie lato client e coerenza delle versioni {#content-consistency}

Le pagine sono composte da HTML, JavaScript, CSS e immagini. Invitiamo i clienti a sfruttare il framework [Librerie lato client (clientlibs)](/help/implementing/developing/introduction/clientlibs.md) per importare risorse Javascript e CSS nelle pagine HTML, tenendo conto delle dipendenze tra le librerie JS.

Il framework clientlibs fornisce una gestione automatica della versione, il che significa che gli sviluppatori possono archiviare le modifiche alle librerie JS nel controllo del codice sorgente e che la versione più recente sarà resa disponibile quando un cliente invia il rilascio. In caso contrario, gli sviluppatori dovranno modificare manualmente l’HTML con i riferimenti alla nuova versione della libreria, il che è particolarmente oneroso se molti modelli HTML condividono la stessa libreria.

Quando le nuove versioni delle librerie vengono rilasciate in produzione, le pagine HTML di riferimento vengono aggiornate con nuovi collegamenti alle versioni della libreria aggiornate. Una volta scaduta la cache del browser per una determinata pagina HTML, non c&#39;è alcun problema che le vecchie librerie vengano caricate dalla cache del browser, poiché la pagina aggiornata (da AEM) ora è garantita per fare riferimento alle nuove versioni delle librerie. In altre parole, una pagina HTML aggiornata includerà tutte le versioni della libreria più recenti.

Il meccanismo di questo è un hash serializzato, che viene aggiunto al collegamento della libreria client, garantendo un URL univoco con versione affinché il browser memorizzi nella cache CSS/JS. L’hash serializzato viene aggiornato solo quando il contenuto della libreria client cambia. Ciò significa che se si verificano aggiornamenti non correlati (cioè nessuna modifica al css/js sottostante della libreria client) anche con una nuova distribuzione, il riferimento rimane lo stesso, garantendo una minore interruzione della cache del browser.

### Abilitazione delle versioni Longcache delle librerie lato client - AEM come Cloud Service SDK Quickstart {#enabling-longcache}

Le inclusioni clientlib predefinite su una pagina HTML hanno un aspetto simile al seguente:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

Quando il controllo delle versioni di clientlib è abilitato, una chiave hash a lungo termine viene aggiunta come selettore alla libreria client. Di conseguenza, il riferimento a clientlib sarà simile al seguente:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

Il controllo delle versioni clientlib restrittive è abilitato per impostazione predefinita in tutti gli ambienti AEM come Cloud Service.

Per abilitare il controllo delle versioni di clientlib restrittive nell’SDK Quickstart locale, esegui le seguenti azioni:

1. Passa a Gestione configurazione OSGi `<host>/system/console/configMgr`
1. Trova la configurazione OSGi per Adobe Granite HTML Library Manager:
   * Seleziona la casella di controllo per abilitare il controllo delle versioni restrittive .
   * Nel campo con etichetta Chiave cache lato client a lungo termine, immetti il valore di /.*;hash
1. Salva le modifiche. Nota che non è necessario salvare questa configurazione nel controllo del codice sorgente in quanto AEM come Cloud Service abiliterà automaticamente questa configurazione negli ambienti di sviluppo, stage e produzione.
1. Ogni volta che il contenuto della libreria client viene modificato, viene generata una nuova chiave hash e il riferimento HTML viene aggiornato.
