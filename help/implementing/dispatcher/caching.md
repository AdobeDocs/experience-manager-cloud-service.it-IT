---
title: Memorizzazione in cache in AEM as a Cloud Service
description: Memorizzazione in cache in AEM as a Cloud Service
feature: Dispatcher
exl-id: 4206abd1-d669-4f7d-8ff4-8980d12be9d6
source-git-commit: 762c30f83a15aba24b56a8d4a6059b371b87aae2
workflow-type: tm+mt
source-wordcount: '2833'
ht-degree: 2%

---

# Introduzione {#intro}

Il traffico passa attraverso la rete CDN a un livello di server web Apache, che supporta moduli tra cui Dispatcher. Per migliorare le prestazioni, Dispatcher viene utilizzato principalmente come cache per limitare l’elaborazione sui nodi di pubblicazione.
È possibile applicare regole alla configurazione del Dispatcher per modificare eventuali impostazioni di scadenza della cache predefinite, con conseguente memorizzazione in cache nella rete CDN. Tieni presente che Dispatcher rispetta anche le intestazioni di scadenza della cache risultanti se `enableTTL` è abilitato nella configurazione di Dispatcher e aggiornerà contenuti specifici anche al di fuori del contenuto ripubblicato.

Questa pagina descrive anche come la cache di Dispatcher viene invalidata e come funziona la memorizzazione in cache a livello di browser per quanto riguarda le librerie lato client.

## Memorizzazione in cache {#caching}

### HTML/Testo {#html-text}

* per impostazione predefinita, è stata memorizzata nella cache dal browser per cinque minuti, in base alla `cache-control` intestazione emessa dal livello Apache. Anche la CDN rispetta questo valore.
* l’impostazione predefinita per la memorizzazione in cache di HTML/Text può essere disabilitata definendo `DISABLE_DEFAULT_CACHING` variabile in `global.vars`:

```
Define DISABLE_DEFAULT_CACHING
```

Ciò può essere utile, ad esempio, quando la logica di business richiede una regolazione precisa dell’intestazione di pagina (con un valore basato sul giorno del calendario), in quanto per impostazione predefinita l’intestazione di pagina è impostata su 0. Detto questo, **prestare attenzione quando si disattiva la memorizzazione in cache predefinita.**

* può essere ignorato per tutto il contenuto di HTML/Testo definendo la variabile `EXPIRATION_TIME` variabile in `global.vars` mediante gli strumenti AEM SDK Dispatcher.
* può essere sostituito a un livello di grana più preciso, compreso il controllo della CDN e della cache del browser in modo indipendente, con i seguenti Apache `mod_headers` direttive:

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header set Cache-Control "max-age=200"
        Header set Surrogate-Control "max-age=3600"
        Header set Age 0
   </LocationMatch>
   ```

   >[!NOTE]
   >L&#39;intestazione Surrogate-Control si applica alla rete CDN gestita da Adobe. Se utilizzi un [CDN gestito dal cliente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html?lang=en#point-to-point-CDN), potrebbe essere necessaria un’intestazione diversa a seconda del provider CDN.

   Fai attenzione quando imposti intestazioni di controllo cache globale o quelle che corrispondono a un’ampia regex in modo che non vengano applicate al contenuto che devi mantenere privato. Valuta l’utilizzo di più direttive per garantire che le regole vengano applicate in modo dettagliato. Detto questo, AEM as a Cloud Service rimuoverà l’intestazione della cache se rileva che è stata applicata a ciò che rileva come non possa essere memorizzata nella cache da Dispatcher, come descritto nella documentazione di Dispatcher. Per forzare AEM ad applicare sempre le intestazioni di memorizzazione in cache, è possibile aggiungere il **sempre** come segue:

   ```
   <LocationMatch "^/content/.*\.(html)$">
        Header unset Cache-Control
        Header unset Expires
        Header always set Cache-Control "max-age=200"
        Header set Age 0
   </LocationMatch>
   ```

   È necessario assicurarsi che un file in `src/conf.dispatcher.d/cache` ha la seguente regola (che si trova nella configurazione predefinita):

   ```
   /0000
   { /glob "*" /type "allow" }
   ```

* Per evitare che contenuti specifici vengano memorizzati nella cache **alla rete CDN**, imposta l&#39;intestazione Cache-Control su *privato*. Ad esempio, quanto segue impedisce il contenuto HTML in una directory denominata **sicuro** dalla memorizzazione in cache nel CDN:

   ```
      <LocationMatch "/content/secure/.*\.(html)$">.  // replace with the right regex
      Header unset Cache-Control
      Header unset Expires
      Header always set Cache-Control “private”
     </LocationMatch>
   ```

* Mentre il contenuto HTML impostato su privato non verrà memorizzato nella cache della rete CDN, può essere memorizzato nella cache del dispatcher se [Memorizzazione in cache sensibile alle autorizzazioni](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=it) è configurato in modo efficiente, garantendo che solo gli utenti autorizzati possano ricevere il contenuto.

   >[!NOTE]
   >Gli altri metodi, compresi i [Progetto ACS Commons AEM dispatcher-ttl](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), non sovrascriverà correttamente i valori.

   >[!NOTE]
   >Tieni presente che Dispatcher potrebbe comunque memorizzare in cache il contenuto in base alla propria [regole di cache](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17497.html). Per rendere il contenuto davvero privato, è necessario assicurarsi che non sia memorizzato nella cache da Dispatcher.

### Librerie lato client (js, css) {#client-side-libraries}

* Quando si utilizza AEM framework di libreria lato client, il codice JavaScript e CSS viene generato in modo tale che i browser possano memorizzarlo nella cache a tempo indefinito, poiché qualsiasi modifica si manifesta come nuovo file con un percorso univoco.  In altre parole, HTML che fa riferimento alle librerie client verrà prodotto in base alle esigenze, in modo che i clienti possano vedere nuovi contenuti mentre vengono pubblicati. Il controllo della cache è impostato su &quot;immutabile&quot; o su 30 giorni per i browser meno recenti che non rispettano il valore &quot;immutabile&quot;.
* vedi la sezione [Librerie lato client e coerenza delle versioni](#content-consistency) per ulteriori dettagli.

### Immagini e contenuti di dimensioni sufficienti per essere archiviati in BLOB {#images}

Il comportamento predefinito per i programmi creati dopo la metà di maggio 2022 (in particolare, per gli ID di programma superiori a 65000) è quello di memorizzare in cache per impostazione predefinita, nel rispetto anche del contesto di autenticazione della richiesta. I programmi precedenti (ID programma uguale o inferiore a 65000) non memorizzano in cache il contenuto BLOB per impostazione predefinita.

In entrambi i casi, le intestazioni di memorizzazione in cache possono essere sostituite a un livello più granulare nel livello Apache/Dispatcher utilizzando l’ `mod_headers` direttive, ad esempio:

```
   <LocationMatch "^/content/.*\.(jpeg|jpg)$">
     Header set Cache-Control "max-age=222"
     Header set Age 0
   </LocationMatch>
```

Quando modifichi le intestazioni di memorizzazione in cache a livello di Dispatcher, presta attenzione a non memorizzare in cache troppo ampiamente, consulta la discussione nella sezione HTML/testo [sopra](#html-text). Inoltre, assicurati che le risorse destinate a essere mantenute private (anziché memorizzate nella cache) non facciano parte del `LocationMatch` filtri di direttiva.

#### Nuovo comportamento predefinito di memorizzazione in cache {#new-caching-behavior}

Il livello AEM imposterà le intestazioni della cache a seconda che l’intestazione della cache sia già stata impostata e il valore del tipo di richiesta. Tieni presente che se non è stata impostata alcuna intestazione di controllo cache, il contenuto pubblico viene memorizzato nella cache e il traffico autenticato è impostato su privato. Se è stata impostata un’intestazione di controllo cache, le intestazioni della cache vengono lasciate intatte.

| L&#39;intestazione di controllo cache esiste? | Tipo di richiesta | AEM imposta le intestazioni di cache su |
|------------------------------|---------------|------------------------------------------------|
| No | pubblico | Controllo cache: pubblico, max-age=600, immutabile |
| No | autenticato | Controllo cache: privato, max-age=600, immutabile |
| Sì | qualsiasi | invariato |

Sebbene non sia consigliato, è possibile modificare il nuovo comportamento predefinito in modo che segua il comportamento precedente (ID programma uguale o inferiore a 65000) impostando la variabile di ambiente Cloud Manager. `AEM_BLOB_ENABLE_CACHING_HEADERS` su false.

#### Comportamento precedente della memorizzazione in cache predefinito {#old-caching-behavior}

Per impostazione predefinita, il livello AEM non memorizza in cache il contenuto BLOB.

>[!NOTE]
>È consigliabile modificare il comportamento predefinito precedente in modo che sia coerente con il nuovo comportamento (ID programma superiori a 65000) impostando la variabile di ambiente Cloud Manager AEM_BLOB_ENABLE_CACHING_HEADERS su true. Se il programma è già attivo, verifica che dopo le modifiche il contenuto si comporti come previsto.

Al momento, le immagini in memoria BLOB contrassegnate come private non possono essere memorizzate nella cache del dispatcher utilizzando [Memorizzazione in cache sensibile alle autorizzazioni](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=it). L&#39;immagine viene sempre richiesta dall&#39;origine AEM e distribuita se l&#39;utente è autorizzato.

>[!NOTE]
>Gli altri metodi, compresi i [Progetto ACS Commons AEM dispatcher-ttl](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), non sovrascriverà correttamente i valori.

### Altri tipi di file di contenuto nell&#39;archivio nodi {#other-content}

* nessuna memorizzazione in cache predefinita
* impossibile impostare il valore predefinito con `EXPIRATION_TIME` variabile utilizzata per i tipi di file html/text
* la scadenza della cache può essere impostata con la stessa strategia LocationMatch descritta nella sezione html/text specificando il regex appropriato

### Ulteriori ottimizzazioni {#further-optimizations}

* Evitare di utilizzare `User-Agent` come parte del `Vary` intestazione. Le versioni precedenti dell’impostazione predefinita di Dispatcher (prima dell’archetipo versione 28) includevano questo elemento e consigliamo di rimuoverlo utilizzando i passaggi seguenti.
   * Individua i file vhost in `<Project Root>/dispatcher/src/conf.d/available_vhosts/*.vhost`
   * Rimuovi o commenta la riga: `Header append Vary User-Agent env=!dont-vary` da tutti i file vhost, ad eccezione di default.vhost, che è di sola lettura
* Utilizza la `Surrogate-Control` intestazione per controllare la memorizzazione in cache CDN indipendente dalla memorizzazione in cache del browser
* Valuta applicazione [`stale-while-revalidate`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-while-revalidate) e [`stale-if-error`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-if-error) direttive per consentire l’aggiornamento in background ed evitare errori di cache, mantenendo il contenuto veloce e fresco per gli utenti.
   * Esistono molti modi per applicare queste direttive, ma aggiungendo 30 minuti `stale-while-revalidate` a tutte le intestazioni di controllo cache è un buon punto di partenza.
* Di seguito sono riportati alcuni esempi di vari tipi di contenuto, che possono essere utilizzati come guida per l’impostazione delle regole di memorizzazione nella cache. Considera attentamente e verifica la configurazione e i requisiti specifici:

   * Memorizza in cache risorse della libreria client mutabili per 12h e aggiornamento in background dopo 12h.

      ```
      <LocationMatch "^/etc\.clientlibs/.*\.(?i:json|png|gif|webp|jpe?g|svg)$">
         Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200,public" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * Memorizza in cache le risorse della libreria client immutabili a lungo termine (30 giorni) con aggiornamento in background per evitare MISS.

      ```
      <LocationMatch "^/etc\.clientlibs/.*\.(?i:js|css|ttf|woff2)$">
         Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * Memorizza in cache le pagine HTML per 5 minuti con aggiornamento in background 1h sul browser e 12h su CDN. Le intestazioni Cache-Control verranno sempre aggiunte, pertanto è importante garantire che le pagine html corrispondenti in /content/* siano destinate a essere pubbliche. In caso contrario, considera l&#39;utilizzo di un regex più specifico.

      ```
      <LocationMatch "^/content/.*\.html$">
         Header unset Cache-Control
         Header always set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
         Header always set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * Memorizza in cache i servizi di contenuti/modello Sling risposte json per 5min con aggiornamento in background 1h sul browser e 12h su CDN.

      ```
      <LocationMatch "^/content/.*\.model\.json$">
         Header set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
         Header set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * Memorizza in cache gli URL immutabili dal componente immagine di base a lungo termine (30 giorni) con aggiornamento in background per evitare MISS.

      ```
      <LocationMatch "^/content/.*\.coreimg.*\.(?i:jpe?g|png|gif|svg)$">
         Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

   * Memorizza in cache risorse mutabili dal DAM come immagini e video per 24 ore e aggiornamento in background dopo 12 ore per evitare MISS

      ```
      <LocationMatch "^/content/dam/.*\.(?i:jpe?g|gif|js|mov|mp4|png|svg|txt|zip|ico|webp|pdf)$">
         Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
         Header set Age 0
      </LocationMatch>
      ```

### Comportamento della richiesta di HEAD {#request-behavior}

Quando viene ricevuta una richiesta di HEAD al CDN di Adobe per una risorsa che è **not** memorizzata nella cache, la richiesta viene trasformata e ricevuta dal Dispatcher e/o dall’istanza AEM come richiesta di GET. Se la risposta è memorizzabile nella cache, le richieste successive di HEAD verranno servite dalla rete CDN. Se la risposta non è memorizzabile in cache, le richieste successive di HEAD verranno trasmesse all’istanza di Dispatcher e/o AEM per un periodo di tempo che dipende dal `Cache-Control` TTL.

### Parametri della campagna di marketing {#marketing-parameters}

Gli URL dei siti web includono frequentemente i parametri delle campagne di marketing utilizzati per monitorare il successo di una campagna. Per utilizzare in modo efficace la cache del dispatcher, ti consigliamo di configurare le `ignoreUrlParams` proprietà come [documentato qui](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#ignoring-url-parameters).

La `ignoreUrlParams` deve essere rimossa la funzione e deve fare riferimento al file `conf.dispatcher.d/cache/marketing_query_parameters.any`. Puoi modificare il file rimuovendo il commento dalle righe corrispondenti ai parametri rilevanti per i tuoi canali di marketing. Puoi aggiungere anche altri parametri.

```
/ignoreUrlParams {
{{ /0001 { /glob "*" /type "deny" }}}
{{ $include "../cache/marketing_query_parameters.any"}}
}
```

## Annullamento della validità della cache del dispatcher {#disp}

In generale, non sarà necessario annullare la validità della cache del Dispatcher. Dovresti invece affidarti all’aggiornamento della cache da parte di Dispatcher quando il contenuto viene ripubblicato e la CDN che rispetta le intestazioni di scadenza della cache.

### Annullamento della validità della cache del dispatcher durante l’attivazione/disattivazione {#cache-activation-deactivation}

Come nelle versioni precedenti di AEM, la pubblicazione o l’annullamento della pubblicazione di pagine cancella il contenuto dalla cache di Dispatcher. Se si sospetta un problema di caching, è necessario ripubblicare le pagine in questione e assicurarsi che sia disponibile un host virtuale che corrisponda al `ServerAlias` localhost, necessario per l’annullamento della validità della cache del Dispatcher.

>[!NOTE]
>Per una corretta invalidazione del dispatcher, assicurati che le richieste da &quot;127.0.0.1&quot;, &quot;localhost&quot;, &quot;.local&quot;, &quot;.adobeaemcloud.com&quot; e &quot;.adobeaemcloud.net&quot; siano tutte soddisfatte e gestite da una configurazione vhost in modo che tali richieste possano essere servite. A tale scopo è possibile eseguire la corrispondenza globale &quot;*&quot; in una configurazione vhost catch-all seguendo il pattern nel riferimento [archetipo AEM](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/dispatcher.cloud/src/conf.d/available_vhosts/default.vhost) o assicurando che l&#39;elenco precedentemente menzionato sia catturato da uno dei vhosts.

Quando l’istanza di pubblicazione riceve una nuova versione di una pagina o di una risorsa dall’autore, utilizza l’agente di eliminazione per annullare la validità dei percorsi appropriati sul suo Dispatcher. Il percorso aggiornato viene rimosso dalla cache di Dispatcher, insieme ai relativi elementi principali, fino a un livello (puoi configurarlo con il [statfileslevel](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level)).

## Annullamento esplicito della validità della cache del Dispatcher {#explicit-invalidation}

L’Adobe consiglia di basarsi su intestazioni di cache standard per controllare il ciclo di vita della distribuzione dei contenuti. Tuttavia, se necessario, è possibile annullare la validità del contenuto direttamente in Dispatcher.

Il seguente elenco contiene scenari in cui si potrebbe voler annullare esplicitamente la validità della cache (ascoltando facoltativamente il completamento dell’annullamento della validità):

* Dopo aver pubblicato contenuti quali frammenti di esperienza o frammenti di contenuto, annullare la validità di contenuti pubblicati e memorizzati nella cache che fanno riferimento a tali elementi.
* Notifica di un sistema esterno quando le pagine di riferimento sono state invalidate correttamente.

Esistono due approcci per annullare esplicitamente la validità della cache:

* L’approccio preferito è l’utilizzo di Sling Content Distribution (SCD) dall’autore.
* Utilizzando l’API di replica per richiamare l’agente di replica di svuotamento del dispatcher di pubblicazione.

Gli approcci differiscono in termini di disponibilità del livello, capacità di deduplicare eventi e garanzia di elaborazione degli eventi. La tabella seguente riassume queste opzioni:

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>N/D</th>
    <th>Disponibilità dei livelli</th>
    <th>Deduplication </th>
    <th>Garanzia </th>
    <th>Azione </th>
    <th>Impatto </th>
    <th>Descrizione </th>
  </tr>  
  <tr>
    <td>API Sling Content Distribution (SCD)</td>
    <td>Autore</td>
    <td>Possibile utilizzando l’API Discovery o abilitando <a href="https://github.com/apache/sling-org-apache-sling-distribution-journal/blob/e18f2bd36e8b43814520e87bd4999d3ca77ce8ca/src/main/java/org/apache/sling/distribution/journal/impl/publisher/DistributedEventNotifierManager.java#L146-L149">modalità di deduplicazione</a>.</td>
    <td>Almeno una volta.</td>
    <td>
     <ol>
       <li>AGGIUNGI</li>
       <li>ELIMINA</li>
       <li>INVALIDARE</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>Livello Gerarchico/Statale</li>
       <li>Livello Gerarchico/Statale</li>
       <li>Solo risorsa di livello</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>Pubblica il contenuto e invalida la cache.</li>
       <li>Rimuove il contenuto e invalida la cache.</li>
       <li>Annulla la validità del contenuto senza pubblicarlo.</li>
     </ol>
     </td>
  </tr>
  <tr>
    <td>API di replica</td>
    <td>Pubblicazione</td>
    <td>Impossibile, evento generato in ogni istanza di pubblicazione.</td>
    <td>Il massimo sforzo.</td>
    <td>
     <ol>
       <li>ATTIVA</li>
       <li>DISATTIVA</li>
       <li>ELIMINA</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>Livello Gerarchico/Statale</li>
       <li>Livello Gerarchico/Statale</li>
       <li>Livello Gerarchico/Statale</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>Pubblica il contenuto e invalida la cache.</li>
       <li>Dal livello Author/Publish : consente di rimuovere il contenuto e di invalidare la cache.</li>
       <li><p><strong>Dal livello di authoring</strong> - Rimuove il contenuto e invalida la cache (se attivata dal livello di authoring di AEM sull’agente di pubblicazione).</p>
           <p><strong>Dal livello di pubblicazione</strong> - Annulla la validità solo della cache (se attivata dal livello di pubblicazione AEM sull’agente di scaricamento scaricamento scaricabile solo risorsa).</p>
       </li>
     </ol>
     </td>
  </tr>
  </tbody>
</table>

Le due azioni direttamente collegate all’annullamento della validità della cache sono: Annullamento della validità dell’API Sling Content Distribution (SCD) e Disattivazione dell’API di replica.

Inoltre, dal tavolo osserviamo che:

* L’API SCD è necessaria quando ogni evento deve essere garantito, ad esempio, la sincronizzazione con un sistema esterno che richiede una conoscenza accurata. Se al momento della chiamata di annullamento della validità è presente un evento di upscaling del livello di pubblicazione, viene generato un evento aggiuntivo quando ogni nuova pubblicazione elabora l’annullamento della validità.

* L’utilizzo dell’API di replica non è un caso d’uso comune, ma deve essere utilizzato nei casi in cui il trigger per annullare la validità della cache proviene dal livello di pubblicazione e non dal livello di authoring. Questo potrebbe essere utile se il TTL del dispatcher è configurato.

In conclusione, se desideri annullare la validità della cache del Dispatcher, l’opzione consigliata è quella di utilizzare l’azione Annulla validità API SCD da Author. Inoltre, puoi anche ascoltare l’evento in modo da poter attivare ulteriori azioni a valle.

### Distribuzione di contenuti Sling (SCD) {#sling-distribution}

>[!NOTE]
>Utilizzando le istruzioni riportate di seguito, verifica il codice personalizzato in un ambiente AEM Cloud Service Dev e non localmente.

Quando si utilizza l’azione SCD di Author, il pattern di implementazione è il seguente:

1. Dall’autore, scrivi un codice personalizzato per richiamare la distribuzione del contenuto sling [API](https://sling.apache.org/documentation/bundles/content-distribution.html), passando l’azione di annullamento della validità con un elenco di percorsi:

```
@Reference
private Distributor distributor;

ResourceResolver resolver = ...; // the resource resolver used for authorizing the request
String agentName = "publish";    // the name of the agent used to distribute the request

String pathToInvalidate = "/content/to/invalidate";
DistributionRequest distributionRequest = new SimpleDistributionRequest(DistributionRequestType.INVALIDATE, false, pathToInvalidate);
distributor.distribute(agentName, resolver, distributionRequest);
```

* (Facoltativo) Ascolta un evento che riflette la risorsa invalidata per tutte le istanze di Dispatcher:


```
package org.apache.sling.distribution.journal.shared;

import org.apache.sling.discovery.DiscoveryService;
import org.apache.sling.distribution.journal.impl.event.DistributionEvent;
import org.osgi.service.component.annotations.Component;
import org.osgi.service.component.annotations.Reference;
import org.osgi.service.event.Event;
import org.osgi.service.event.EventHandler;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import static org.apache.sling.distribution.DistributionRequestType.INVALIDATE;
import static org.apache.sling.distribution.event.DistributionEventProperties.DISTRIBUTION_PATHS;
import static org.apache.sling.distribution.event.DistributionEventProperties.DISTRIBUTION_TYPE;
import static org.apache.sling.distribution.event.DistributionEventTopics.AGENT_PACKAGE_DISTRIBUTED;
import static org.osgi.service.event.EventConstants.EVENT_TOPIC;

@Component(immediate = true, service = EventHandler.class, property = {
        EVENT_TOPIC + "=" + AGENT_PACKAGE_DISTRIBUTED
})
public class InvalidatedHandler implements EventHandler {
    private static final Logger LOG = LoggerFactory.getLogger(InvalidatedHandler.class);

    @Reference
    private DiscoveryService discoveryService;

    @Override
    public void handleEvent(Event event) {

        String distributionType = (String) event.getProperty(DISTRIBUTION_TYPE);

        if (INVALIDATE.name().equals(distributionType)) {
            boolean isLeader = discoveryService.getTopology().getLocalInstance().isLeader();
            // process the OSGi event on the leader author instance
            if (isLeader) {
                String[] paths = (String[]) event.getProperty(DISTRIBUTION_PATHS);
                String packageId = (String) event.getProperty(DistributionEvent.PACKAGE_ID);
                invalidated(paths, packageId);
            }
        }
    }

    private void invalidated(String[] paths, String packageId) {
        // custom logic
        LOG.info("Successfully applied package with id {}, paths {}", packageId, paths);
    }
}
```

<!-- Optionally, instead of using the isLeader approach, one could add an OSGi configuration for the PID org.apache.sling.distribution.journal.impl.publisher.DistributedEventNotifierManager and property deduplicateEvent=true. But we'll stick with just one strategy and not mention it (double-check this).**review this**-->

* (Facoltativo) Esegui logica di business nel `invalidated(String[] paths, String packageId)` metodo precedente.

>[!NOTE]
>
>La rete CDN Adobe non viene scaricata quando Dispatcher viene invalidato. La rete CDN gestita da Adobe rispetta i TTL e non è quindi necessario scaricarla.

### API di replica {#replication-api}

Di seguito è riportato il pattern di implementazione quando si utilizza l’azione di disattivazione API di replica:

1. Sul livello di pubblicazione, chiama l’API di replica per attivare l’agente di replica di svuotamento del dispatcher di pubblicazione.

L’endpoint dell’agente di svuotamento non è configurabile ma è preconfigurato per puntare a Dispatcher, con corrispondenza con il servizio di pubblicazione in esecuzione accanto all’agente di svuotamento.

L’agente di flush può in genere essere attivato dal codice personalizzato in base agli eventi o ai flussi di lavoro OSGi.

```
String[] paths = …
ReplicationOptions options = new ReplicationOptions();
options.setSynchronous(true);
options.setFilter( new AgentFilter {
  public boolean isIncluded (Agent agent) {
   return agent.getId().equals(“flush”);
  }
});

Replicator.replicate (session,ReplicationActionType.DELETE,paths, options);
```

<!-- In general, it will not be necessary to manually invalidate content in the dispatcher, but it is possible if needed.

>[!NOTE]
>Prior to AEM as a Cloud Service, there were two ways of invalidating the dispatcher cache.
>
>1. Invoke the replication agent, specifying the publish dispatcher flush agent
>2. Directly calling the `invalidate.cache` API (for example, `POST /dispatcher/invalidate.cache`)
>
>The dispatcher's `invalidate.cache` API approach will no longer be supported since it addresses only a specific dispatcher node. AEM as a Cloud Service operates at the service level, not the individual node level and so the invalidation instructions in the [Invalidating Cached Pages From AEM](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html) page are not longer valid for AEM as a Cloud Service.

The replication flush agent should be used. This can be done using the [Replication API](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/replication/Replicator.html). The flush agent endpoint is not configurable but pre-configured to point to the dispatcher, matched with the publish service running the flush agent. The flush agent can typically be triggered by OSGi events or workflows.

<!-- Need to find a new link and/or example -->
<!-- 
and for an example of flushing the cache, see the [API example page](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) (specifically the `CustomStep` example issuing a replication action of type ACTIVATE to all available agents). 

The diagram presented below illustrates this.

![CDN](assets/cdnd.png "CDN")

If there is a concern that the dispatcher cache isn't clearing, contact [customer support](https://helpx.adobe.com/support.ec.html) who can flush the dispatcher cache if necessary.

The Adobe-managed CDN respects TTLs and thus there is no need fo it to be flushed. If an issue is suspected, [contact customer support](https://helpx.adobe.com/support.ec.html) support who can flush an Adobe-managed CDN cache as necessary. -->

## Librerie lato client e coerenza delle versioni {#content-consistency}

Le pagine sono composte da HTML, Javascript, CSS e immagini. I clienti sono incoraggiati a sfruttare [Framework delle librerie lato client (clientlibs)](/help/implementing/developing/introduction/clientlibs.md) importare risorse Javascript e CSS nelle pagine HTML, tenendo conto delle dipendenze tra le librerie JS.

Il framework clientlibs fornisce una gestione automatica della versione, il che significa che gli sviluppatori possono archiviare le modifiche alle librerie JS nel controllo del codice sorgente e che la versione più recente sarà resa disponibile quando un cliente invia il rilascio. In caso contrario, gli sviluppatori dovranno modificare manualmente HTML con i riferimenti alla nuova versione della libreria, il che è particolarmente oneroso se molti modelli di HTML condividono la stessa libreria.

Quando le nuove versioni delle librerie vengono rilasciate in produzione, le pagine HTML di riferimento vengono aggiornate con nuovi collegamenti alle versioni della libreria aggiornate. Una volta scaduta la cache del browser per una determinata pagina HTML, non c&#39;è alcun problema che le vecchie librerie vengano caricate dalla cache del browser, poiché la pagina aggiornata (da AEM) ora è garantita per fare riferimento alle nuove versioni delle librerie. In altre parole, una pagina HTML aggiornata includerà tutte le versioni della libreria più recenti.

Il meccanismo di questo è un hash serializzato, che viene aggiunto al collegamento della libreria client, garantendo un URL univoco con versione affinché il browser memorizzi nella cache CSS/JS. L’hash serializzato viene aggiornato solo quando il contenuto della libreria client cambia. Ciò significa che se si verificano aggiornamenti non correlati (cioè nessuna modifica al css/js sottostante della libreria client) anche con una nuova distribuzione, il riferimento rimane lo stesso, garantendo una minore interruzione della cache del browser.

### Abilitazione delle versioni Longcache delle librerie lato client - AEM Quickstart SDK as a Cloud Service {#enabling-longcache}

Le inclusioni clientlib predefinite su una pagina HTML hanno un aspetto simile al seguente:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

Quando il controllo delle versioni di clientlib è abilitato, una chiave hash a lungo termine viene aggiunta come selettore alla libreria client. Di conseguenza, il riferimento a clientlib sarà simile al seguente:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

Il controllo delle versioni clientlib restrittive è abilitato per impostazione predefinita in tutti gli ambienti as a Cloud Service AEM.

Per abilitare il controllo delle versioni di clientlib restrittive nell’SDK Quickstart locale, esegui le seguenti azioni:

1. Passa a Gestione configurazione OSGi `<host>/system/console/configMgr`
1. Trova la configurazione OSGi per Adobe Granite HTML Library Manager:
   * Seleziona la casella di controllo per abilitare il controllo delle versioni restrittive .
   * Nel campo con etichetta Chiave cache lato client a lungo termine, immetti il valore di /.*;hash
1. Salva le modifiche. Non è necessario salvare questa configurazione nel controllo del codice sorgente, in quanto AEM as a Cloud Service abilita automaticamente questa configurazione negli ambienti di sviluppo, stage e produzione.
1. Ogni volta che il contenuto della libreria client viene modificato, viene generata una nuova chiave hash e il riferimento di HTML verrà aggiornato.
