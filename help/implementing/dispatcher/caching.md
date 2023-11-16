---
title: Memorizzazione in cache in AEM as a Cloud Service
description: Scopri le nozioni di base sul caching in AEM as a Cloud Service
feature: Dispatcher
exl-id: 4206abd1-d669-4f7d-8ff4-8980d12be9d6
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '2874'
ht-degree: 2%

---

# Introduzione {#intro}

Il traffico passa attraverso la rete CDN a un livello di server web Apache, che supporta moduli tra cui Dispatcher. Per migliorare le prestazioni, Dispatcher viene utilizzato principalmente come cache per limitare l’elaborazione sui nodi di pubblicazione.
È possibile applicare delle regole alla configurazione di Dispatcher per modificare eventuali impostazioni di scadenza predefinite della cache, con conseguente memorizzazione nella cache della rete CDN. Dispatcher rispetta anche le intestazioni di scadenza della cache risultanti se `enableTTL` è abilitato nella configurazione di Dispatcher, il che significa che aggiorna contenuti specifici anche al di fuori di quelli ripubblicati.

Questa pagina descrive anche come viene invalidata la cache di Dispatcher e come funziona il caching a livello di browser per quanto riguarda le librerie lato client.

## Memorizzazione in cache {#caching}

### HTML/Text {#html-text}

* per impostazione predefinita, viene memorizzato nella cache dal browser per cinque minuti, in base al `cache-control` intestazione emessa dal livello Apache. Anche la rete CDN rispetta questo valore.
* l’impostazione predefinita di HTML/Text caching può essere disabilitata definendo `DISABLE_DEFAULT_CACHING` variabile in `global.vars`:

```
Define DISABLE_DEFAULT_CACHING
```

Questo metodo è utile, ad esempio, quando la logica di business richiede l’ottimizzazione dell’intestazione age (con un valore basato sul giorno del calendario) perché per impostazione predefinita l’intestazione age è impostata su 0. Detto questo, **prestare attenzione quando si disattiva il caching predefinito.**

* può essere ignorato per tutto il contenuto HTML/Text definendo `EXPIRATION_TIME` variabile in `global.vars` utilizzando gli strumenti di Dispatcher SDK as a Cloud Service dell’AEM.
* può essere ignorato a un livello più granulare, incluso il controllo indipendente della CDN e della cache del browser, con il seguente Apache `mod_headers` direttive:

  ```
  <LocationMatch "^/content/.*\.(html)$">
       Header set Cache-Control "max-age=200"
       Header set Surrogate-Control "max-age=3600"
       Header set Age 0
  </LocationMatch>
  ```

  >[!NOTE]
  >L’intestazione Surrogate-Control si applica alla rete CDN gestita dall’Adobe. Se si utilizza un [CDN gestita dal cliente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html?lang=en#point-to-point-CDN), potrebbe essere necessaria un’intestazione diversa a seconda del provider CDN.

  Presta attenzione quando imposti intestazioni di controllo cache globale o intestazioni di cache simili che corrispondono a un’ampia regola, in modo che non vengano applicate a contenuti che devono essere mantenuti privati. Valuta l’utilizzo di più direttive per garantire che le regole vengano applicate in modo granulare. Detto questo, AEM as a Cloud Service rimuove l’intestazione della cache se rileva che è stata applicata a ciò che rileva come non memorizzabile in cache da Dispatcher, come descritto nella documentazione di Dispatcher. Per forzare l’AEM ad applicare sempre le intestazioni di caching, è possibile aggiungere **`always`** opzione come segue:

  ```
  <LocationMatch "^/content/.*\.(html)$">
       Header unset Cache-Control
       Header unset Expires
       Header always set Cache-Control "max-age=200"
       Header set Age 0
  </LocationMatch>
  ```

  Assicurati che un file in `src/conf.dispatcher.d/cache` ha la seguente regola (nella configurazione predefinita):

  ```
  /0000
  { /glob "*" /type "allow" }
  ```

* Per evitare che un contenuto specifico venga memorizzato nella cache **alla rete CDN**, imposta l’intestazione Cache-Control su *privato*. Ad esempio, quanto segue impedisce il contenuto HTML in una directory denominata **protetto** dalla memorizzazione nella cache nella rete CDN:

  ```
     <LocationMatch "/content/secure/.*\.(html)$">.  // replace with the right regex
     Header unset Cache-Control
     Header unset Expires
     Header always set Cache-Control "private"
    </LocationMatch>
  ```

* Anche se il contenuto HTML impostato su privato non viene memorizzato nella cache della rete CDN, può essere memorizzato nella cache in Dispatcher se [Memorizzazione in cache sensibile alle autorizzazioni](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=it) è configurato, in modo che solo gli utenti autorizzati possano ricevere il contenuto.

  >[!NOTE]
  >Gli altri metodi, tra cui [Progetto Dispatcher-ttl AEM ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), non sostituisce correttamente i valori.

  >[!NOTE]
  >Dispatcher potrebbe comunque memorizzare in cache il contenuto in base al proprio [regole di caching](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17497.html?lang=it). Per rendere il contenuto veramente privato, assicurati che non venga memorizzato in cache da Dispatcher.

### Librerie lato client (js,css) {#client-side-libraries}

* Quando si utilizza il framework libreria AEM lato client, il codice JavaScript e CSS viene generato in modo tale che i browser possano memorizzarlo nella cache indefinitamente, poiché eventuali modifiche si manifestano come nuovi file con un percorso univoco. In altre parole, i HTML che fanno riferimento alle librerie client vengono prodotti in base alle esigenze, affinché i clienti possano visualizzare nuovi contenuti durante la pubblicazione. Il controllo cache è impostato su &quot;immutabile&quot; o 30 giorni per i browser più vecchi che non rispettano il valore &quot;immutabile&quot;.
* vedi la sezione [Librerie lato client e coerenza delle versioni](#content-consistency) per ulteriori dettagli.

### Immagini e qualsiasi contenuto di dimensioni sufficienti per essere archiviato nell&#39;archivio BLOB {#images}

Il comportamento predefinito per i programmi creati dopo metà maggio 2022 (in particolare, per gli ID programma superiori a 65000) consiste nella memorizzazione in cache per impostazione predefinita, nel rispetto anche del contesto di autenticazione della richiesta. I programmi meno recenti (ID di programma uguali o inferiori a 65000) non memorizzano in cache il contenuto BLOB per impostazione predefinita.

In entrambi i casi, le intestazioni di memorizzazione in cache possono essere ignorate su un livello a grana più fine a livello di Apache/Dispatcher utilizzando Apache `mod_headers` direttive, ad esempio:

```
   <LocationMatch "^/content/.*\.(jpeg|jpg)$">
     Header set Cache-Control "max-age=222"
     Header set Age 0
   </LocationMatch>
```

Quando modifichi le intestazioni di memorizzazione in cache a livello di Dispatcher, presta attenzione a non creare una cache troppo ampia. Consulta la discussione nella sezione HTML/testo [sopra](#html-text). Inoltre, assicurati che le risorse destinate a essere mantenute private (anziché memorizzate in cache) non facciano parte del `LocationMatch` filtri direttiva.

Le risorse JCR (più grandi di 16 KB) memorizzate nell’archivio BLOB vengono solitamente servite come reindirizzamenti 302 dall’AEM. Questi reindirizzamenti vengono intercettati e seguiti da CDN e il contenuto viene distribuito direttamente dall’archivio BLOB. Su queste risposte è possibile personalizzare solo un set limitato di intestazioni. Ad esempio, per personalizzare `Content-Disposition` utilizza le direttive dispatcher nel modo seguente:

```
<LocationMatch "\.(?i:pdf)$">
  ForceType application/pdf
  Header set Content-Disposition inline
  </LocationMatch>
```

L’elenco delle intestazioni che possono essere personalizzate nelle risposte BLOB è:

```
content-security-policy
x-frame-options
x-xss-protection
x-content-type-options
x-robots-tag
access-control-allow-origin
content-disposition
permissions-policy
referrer-policy
x-vhost
content-disposition
cache-control
vary
```

#### Nuovo comportamento di caching predefinito {#new-caching-behavior}

Il livello AEM imposta le intestazioni della cache a seconda che l’intestazione della cache sia già stata impostata e il valore del tipo di richiesta. Se non è impostata alcuna intestazione di controllo della cache, il contenuto pubblico viene memorizzato nella cache e il traffico autenticato viene impostato su privato. Se è impostata un’intestazione di controllo cache, le intestazioni della cache vengono lasciate intatte.

| L’intestazione di controllo cache esiste già? | Tipo di richiesta | AEM imposta le intestazioni della cache su |
|------------------------------|---------------|------------------------------------------------|
| No | pubblico | Cache-Control: public, max-age=600, immutabile |
| No | autenticato | Cache-Control: private, max-age=600, immutabile |
| Sì | qualsiasi | invariato |

Sebbene non sia consigliato, è possibile modificare il nuovo comportamento predefinito in modo che segua il comportamento precedente (ID programma uguali o inferiori a 65000) impostando la variabile di ambiente Cloud Manager `AEM_BLOB_ENABLE_CACHING_HEADERS` su false.

#### Comportamento di memorizzazione nella cache predefinito precedente {#old-caching-behavior}

Per impostazione predefinita, il livello AEM non memorizza in cache il contenuto BLOB.

>[!NOTE]
>Modifica il comportamento predefinito precedente in modo che sia coerente con il nuovo comportamento (ID programma superiori a 65000) impostando la variabile di ambiente AEM_BLOB_ENABLE_CACHING_HEADERS di Cloud Manager su true. Se il programma è già attivo, assicurati di verificare che dopo le modifiche il contenuto si comporti come previsto.

Ora, le immagini nell’archiviazione BLOB contrassegnate come private non possono essere memorizzate nella cache in Dispatcher utilizzando [Memorizzazione in cache sensibile alle autorizzazioni](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=it). L’immagine viene sempre richiesta all’origine dell’AEM e trasmessa se l’utente è autorizzato.

>[!NOTE]
>Gli altri metodi, tra cui [progetto dispatcher-ttl AEM ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/dispatcher-ttl/), non sostituire correttamente i valori.

### Altri tipi di file di contenuto nell’archivio nodi {#other-content}

* nessuna memorizzazione predefinita nella cache
* impossibile impostare il valore predefinito con `EXPIRATION_TIME` variabile utilizzata per i tipi di file html/testo
* La scadenza della cache può essere impostata con la stessa strategia LocationMatch descritta nella sezione html/text specificando il valore regex appropriato

### Ulteriori ottimizzazioni {#further-optimizations}

* Evita di utilizzare `User-Agent` nell&#39;ambito del `Vary` intestazione. Le versioni precedenti della configurazione predefinita di Dispatcher (prima dell’archetipo versione 28) la includevano ed Adobe consiglia di rimuoverla seguendo i passaggi seguenti.
   * Individuare i file vhost in `<Project Root>/dispatcher/src/conf.d/available_vhosts/*.vhost`
   * Rimuovi o commenta la riga: `Header append Vary User-Agent env=!dont-vary` da tutti i file vhost, tranne default.vhost, che è di sola lettura
* Utilizza il `Surrogate-Control` intestazione per controllare la memorizzazione nella cache CDN indipendentemente dalla memorizzazione nella cache del browser
* Valuta l’applicazione [`stale-while-revalidate`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-while-revalidate) e [`stale-if-error`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control#stale-if-error) direttive per consentire l’aggiornamento in background ed evitare mancati riscontri nella cache, mantenendo i contenuti veloci e aggiornati per gli utenti.
   * Esistono molti modi per applicare queste direttive, ma con l&#39;aggiunta di un `stale-while-revalidate` a tutte le intestazioni di controllo cache è un buon punto di partenza.
* Seguono alcuni esempi per vari tipi di contenuto, che possono essere utilizzati come guida durante la configurazione di regole di caching personalizzate. Valuta e verifica attentamente la configurazione e i requisiti specifici:

   * Memorizza nella cache le risorse della libreria client mutabili per 12 ore e aggiorna in background dopo 12 ore.

     ```
     <LocationMatch "^/etc\.clientlibs/.*\.(?i:json|png|gif|webp|jpe?g|svg)$">
        Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200,public" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

   * Memorizza nella cache le risorse della libreria client immutabili a lungo termine (30 giorni) con aggiornamento in background per evitare errori irreversibili.

     ```
     <LocationMatch "^/etc\.clientlibs/.*\.(?i:js|css|ttf|woff2)$">
        Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

   * Memorizza nella cache le pagine HTML per cinque minuti con aggiornamento in background di un’ora sul browser e di 12 ore sulla rete CDN. Le intestazioni Cache-Control vengono sempre aggiunte, pertanto è importante assicurarsi che le pagine HTML corrispondenti in /content/* siano destinate a essere pubbliche. In caso contrario, considera l’utilizzo di un’espressione regex più specifica.

     ```
     <LocationMatch "^/content/.*\.html$">
        Header unset Cache-Control
        Header always set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
        Header always set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

   * Memorizza nella cache le risposte JSON di esportazione del modello Sling/Content Services per cinque minuti con aggiornamento in background di un’ora sul browser e di 12 ore sulla rete CDN.

     ```
     <LocationMatch "^/content/.*\.model\.json$">
        Header set Cache-Control "max-age=300,stale-while-revalidate=3600" "expr=%{REQUEST_STATUS} < 400"
        Header set Surrogate-Control "stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

   * Memorizza nella cache gli URL immutabili del componente immagine principale a lungo termine (30 giorni) con aggiornamento in background per evitare errori irreversibili.

     ```
     <LocationMatch "^/content/.*\.coreimg.*\.(?i:jpe?g|png|gif|svg)$">
        Header set Cache-Control "max-age=2592000,stale-while-revalidate=43200,stale-if-error=43200,public,immutable" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

   * Memorizza nella cache le risorse mutabili da DAM come immagini e video per 24 ore e aggiorna lo sfondo dopo 12 ore per evitare errori irreversibili.

     ```
     <LocationMatch "^/content/dam/.*\.(?i:jpe?g|gif|js|mov|mp4|png|svg|txt|zip|ico|webp|pdf)$">
        Header set Cache-Control "max-age=43200,stale-while-revalidate=43200,stale-if-error=43200" "expr=%{REQUEST_STATUS} < 400"
        Header set Age 0
     </LocationMatch>
     ```

### Comportamento richiesta HEAD {#request-behavior}

Quando viene ricevuta una richiesta HEAD al CDN di Adobe per una risorsa che è **non** memorizzata nella cache, la richiesta viene trasformata e ricevuta dall’istanza di Dispatcher e/o AEM come richiesta di GET. Se la risposta è memorizzabile in cache, le richieste HEAD successive vengono servite dalla rete CDN. Se la risposta non è memorizzabile in cache, le richieste HEAD successive vengono passate al Dispatcher, all’istanza AEM o a entrambi, per un periodo di tempo che dipende da `Cache-Control` TTL.

### Parametri della campagna di marketing {#marketing-parameters}

Gli URL del sito web includono spesso parametri della campagna di marketing utilizzati per monitorare il successo di una campagna.

Per gli ambienti creati a ottobre 2023 o versioni successive, per memorizzare in cache meglio le richieste, la rete CDN rimuoverà i parametri di query comuni relativi al marketing, in particolare quelli che corrispondono al seguente pattern regex:

```
^(utm_.*|gclid|gdftrk|_ga|mc_.*|trk_.*|dm_i|_ke|sc_.*|fbclid)$
```

Inviare un ticket di supporto se si desidera disabilitare questo comportamento.

Per gli ambienti creati prima di ottobre 2023, si consiglia di configurare i `ignoreUrlParams` proprietà come [documentato qui](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#ignoring-url-parameters).


## Annullamento della validità della cache di Dispatcher {#disp}

In generale, non è necessario invalidare la cache di Dispatcher. Al contrario, quando il contenuto viene ripubblicato e la rete CDN rispetta le intestazioni di scadenza della cache, dovrai fare affidamento sull’aggiornamento della cache da parte di Dispatcher.

### Annullamento della validità della cache del Dispatcher durante l’attivazione/disattivazione {#cache-activation-deactivation}

Come per le versioni precedenti dell’AEM, la pubblicazione o l’annullamento della pubblicazione di pagine cancella il contenuto dalla cache di Dispatcher. Se si sospetta un problema di caching, è necessario ripubblicare le pagine in questione e assicurarsi che sia disponibile un host virtuale che corrisponda al `ServerAlias` localhost, richiesto per l’annullamento della validità della cache di Dispatcher.

>[!NOTE]
>Per un’invalidazione corretta del Dispatcher, assicurati che le richieste da &quot;127.0.0.1&quot;, &quot;localhost&quot;, &quot;.local&quot;, &quot;.adobeaemcloud.com&quot; e &quot;.adobeaemcloud.net&quot; corrispondano e siano gestite da una configurazione vhost in modo che la richiesta possa essere servita. Puoi eseguire questa operazione facendo corrispondere il valore globale &quot;*&quot; in una configurazione vhost catch-all seguendo il pattern indicato nella sezione [Archetipo AEM](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/dispatcher.cloud/src/conf.d/available_vhosts/default.vhost). In alternativa, puoi assicurarti che l’elenco precedentemente menzionato sia stato acquisito da uno dei host.

Quando l’istanza Publish riceve una nuova versione di una pagina o di una risorsa dall’autore, utilizza l’agente di svuotamento per invalidare i percorsi appropriati nel proprio Dispatcher. Il percorso aggiornato viene rimosso dalla cache di Dispatcher, insieme ai relativi elementi principali, fino a un livello (puoi configurare questo livello con [statfileslevel](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level)).

## Annullamento esplicito della validità della cache di Dispatcher {#explicit-invalidation}

L’Adobe consiglia di fare affidamento sulle intestazioni di cache standard per controllare il ciclo di vita della distribuzione dei contenuti. Tuttavia, se necessario, è possibile annullare la validità del contenuto direttamente in Dispatcher.

L’elenco seguente contiene scenari in cui potresti voler invalidare esplicitamente la cache (mentre facoltativamente stai in ascolto del completamento dell’invalidazione):

* Dopo la pubblicazione di contenuti come frammenti di esperienza o frammenti di contenuto, invalidando il contenuto pubblicato e memorizzato nella cache che fa riferimento a tali elementi.
* Notifica a un sistema esterno quando le pagine di riferimento sono state invalidate correttamente.

Esistono due approcci per invalidare esplicitamente la cache:

* L’approccio preferito è quello di utilizzare la Distribuzione dei contenuti Sling (SCD) dell’ambiente Author.
* L’altro approccio consiste nell’utilizzare l’API di replica per richiamare l’agente di svuotamento del Dispatcher per la pubblicazione.

Gli approcci sono diversi in termini di disponibilità dei livelli, possibilità di deduplicare gli eventi e garanzia di elaborazione degli eventi. La tabella seguente riassume queste opzioni:

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>N/D</th>
    <th>Disponibilità a livello</th>
    <th>Deduplicazione </th>
    <th>Garanzia </th>
    <th>Azione </th>
    <th>Impatto </th>
    <th>Descrizione </th>
  </tr>  
  <tr>
    <td>API Sling Content Distribution (SCD)</td>
    <td>Autore</td>
    <td>Possibile utilizzando Discovery API o abilitando <a href="https://github.com/apache/sling-org-apache-sling-distribution-journal/blob/e18f2bd36e8b43814520e87bd4999d3ca77ce8ca/src/main/java/org/apache/sling/distribution/journal/impl/publisher/DistributedEventNotifierManager.java#L146-L149">modalità di deduplicazione</a>.</td>
    <td>Almeno una volta.</td>
    <td>
     <ol>
       <li>AGGIUNGI</li>
       <li>ELIMINA</li>
       <li>INVALIDA</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>Gerarchico/Livello Stat</li>
       <li>Gerarchico/Livello Stat</li>
       <li>Livella solo risorsa</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>Pubblica il contenuto e invalida la cache.</li>
       <li>Rimuove il contenuto e invalida la cache.</li>
       <li>Invalida il contenuto senza pubblicarlo.</li>
     </ol>
     </td>
  </tr>
  <tr>
    <td>API di replica</td>
    <td>Pubblicazione</td>
    <td>Impossibile, evento generato su ogni istanza di pubblicazione.</td>
    <td>Ottimo lavoro.</td>
    <td>
     <ol>
       <li>ATTIVA</li>
       <li>DISATTIVA</li>
       <li>ELIMINA</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>Gerarchico/Livello Stat</li>
       <li>Gerarchico/Livello Stat</li>
       <li>Gerarchico/Livello Stat</li>
     </ol>
     </td>
    <td>
     <ol>
       <li>Pubblica il contenuto e invalida la cache.</li>
       <li>Dal livello di authoring/pubblicazione: rimuove il contenuto e invalida la cache.</li>
       <li><p><strong>Dal livello di authoring</strong> : rimuove il contenuto e invalida la cache (se attivata dal livello di authoring AEM sull’agente di pubblicazione).</p>
           <p><strong>Dal livello di pubblicazione</strong> - Invalida solo la cache (se attivata dal livello di pubblicazione AEM nell’agente Flush o Resource-only-flush).</p>
       </li>
     </ol>
     </td>
  </tr>
  </tbody>
</table>

Le due azioni direttamente correlate all’invalidamento della cache sono Invalidate API SCD (Sling Content Distribution) e Deactivate API della replica.

Inoltre, dalla tabella, puoi osservare che:

* L’API SCD è necessaria quando ogni evento deve essere garantito, ad esempio la sincronizzazione con un sistema esterno che richiede una conoscenza accurata. Se è presente un evento di upscaling del livello di pubblicazione al momento della chiamata di invalidazione, viene generato un evento aggiuntivo quando ogni nuova pubblicazione elabora l’invalidazione.

* L’utilizzo dell’API di replica non è un caso d’uso comune, ma può essere utilizzato nei casi in cui il trigger per invalidare la cache proviene dal livello di pubblicazione e non dal livello di authoring. Questo metodo potrebbe essere utile se Dispatcher TTL è configurato.

In conclusione, se desideri annullare la validità della cache di Dispatcher, l’opzione consigliata è quella di utilizzare l’azione Invalida API SCD di Author. Inoltre, puoi anche ascoltare l’evento in modo da poter quindi attivare ulteriori azioni a valle.

### Distribuzione dei contenuti Sling (SCD) {#sling-distribution}

>[!NOTE]
>Quando utilizzi le istruzioni presentate di seguito, testa il codice personalizzato in un ambiente di sviluppo AEM Cloud Service e non localmente.

Quando utilizzi l’azione SCD di Author, il modello di implementazione è il seguente:

1. Dall’autore, scrivi il codice personalizzato per richiamare la distribuzione del contenuto sling [API](https://sling.apache.org/documentation/bundles/content-distribution.html), passando l’azione di invalidazione con un elenco di percorsi:

```
@Reference
private Distributor distributor;

ResourceResolver resolver = ...; // the resource resolver used for authorizing the request
String agentName = "publish";    // the name of the agent used to distribute the request

String pathToInvalidate = "/content/to/invalidate";
DistributionRequest distributionRequest = new SimpleDistributionRequest(DistributionRequestType.INVALIDATE, false, pathToInvalidate);
distributor.distribute(agentName, resolver, distributionRequest);
```

* (Facoltativamente) Ascolta un evento che riflette la risorsa da invalidare per tutte le istanze di Dispatcher:


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

* (Facoltativamente) Eseguire la logica di business in `invalidated(String[] paths, String packageId)` metodo precedente.

>[!NOTE]
>
>Il CDN di Adobe non viene scaricato quando Dispatcher viene invalidato. La rete CDN gestita dall’Adobe rispetta i TTL e quindi non è necessario scaricarla.

### API di replica {#replication-api}

Di seguito è riportato il modello di implementazione per l’utilizzo dell’azione di disattivazione dell’API di replica:

1. Sul livello di pubblicazione, chiama l’API di replica per attivare l’agente di svuotamento del Dispatcher per la pubblicazione.

L’endpoint dell’agente di svuotamento non è configurabile, ma è preconfigurato per puntare a Dispatcher e corrisponde al servizio di pubblicazione in esecuzione insieme all’agente di svuotamento.

L’agente di svuotamento può in genere essere attivato da codice personalizzato basato su eventi o flussi di lavoro OSGi.

```
String[] paths = …
ReplicationOptions options = new ReplicationOptions();
options.setSynchronous(true);
options.setFilter( new AgentFilter {
  public boolean isIncluded (Agent agent) {
   return agent.getId().equals("flush");
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

If there is a concern that the dispatcher cache is not clearing, contact [customer support](https://helpx.adobe.com/support.ec.html) who can flush the dispatcher cache if necessary.

The Adobe-managed CDN respects TTLs and thus there is no need fo it to be flushed. If an issue is suspected, [contact customer support](https://helpx.adobe.com/support.ec.html) support who can flush an Adobe-managed CDN cache as necessary. -->

## Librerie lato client e coerenza delle versioni {#content-consistency}

Le pagine sono composte da HTML, JavaScript, CSS e immagini. I clienti sono incoraggiati a utilizzare [Framework librerie lato client (clientlibs)](/help/implementing/developing/introduction/clientlibs.md) per importare risorse JavaScript e CSS nelle pagine HTML, tenendo conto delle dipendenze tra le librerie JS.

Il framework clientlibs fornisce la gestione automatica delle versioni. Ciò significa che gli sviluppatori possono archiviare le modifiche alle librerie JS nel controllo del codice sorgente e che l’ultima versione è disponibile quando un cliente invia la propria versione. Senza questo flusso di lavoro, gli sviluppatori devono modificare manualmente HTML con riferimenti alla nuova versione della libreria, il che è particolarmente oneroso se la stessa libreria condivide molti modelli di HTML.

Quando vengono rilasciate in produzione le nuove versioni delle librerie, le pagine HTML di riferimento vengono aggiornate con nuovi collegamenti alle versioni aggiornate della libreria. Dopo la scadenza della cache del browser per una determinata pagina HTML, non c’è alcun problema che le vecchie librerie vengano caricate dalla cache del browser. Il motivo è che ora è garantito che la pagina aggiornata (da AEM) faccia riferimento alle nuove versioni delle librerie. In altre parole, una pagina HTML aggiornata include tutte le versioni più recenti della libreria.

Il meccanismo alla base di questa funzionalità è un hash serializzato, che viene aggiunto al collegamento della libreria client. Garantisce un URL univoco con versione affinché il browser possa memorizzare in cache i file CSS/JS. L’hash serializzato viene aggiornato solo quando cambia il contenuto della libreria client. Ciò significa che se si verificano aggiornamenti non correlati (ovvero, nessuna modifica ai css/js sottostanti della libreria client) anche con una nuova distribuzione, il riferimento rimane lo stesso. A sua volta, assicura meno interruzioni alla cache del browser.

### Abilitazione delle versioni Longcache delle librerie lato client: QuickStart per SDK as a Cloud Service per AEM {#enabling-longcache}

Le inclusioni clientlib predefinite in una pagina HTML hanno un aspetto simile al seguente:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.css" type="text/css">
```

Quando è abilitato il controllo rigoroso delle versioni di clientlib, viene aggiunta una chiave hash a lungo termine come selettore alla libreria client. Di conseguenza, il riferimento clientlib è simile al seguente:

```
<link rel="stylesheet" href="/etc.clientlibs/wkndapp/clientlibs/clientlib-base.lc-7c8c5d228445ff48ab49a8e3c865c562-lc.css" type="text/css">
```

Il controllo delle versioni rigorose di clientlib è abilitato per impostazione predefinita in tutti gli ambienti AEM as a Cloud Service.

Per abilitare il controllo rigoroso delle versioni clientlib nel Quickstart dell’SDK locale, effettua le seguenti operazioni:

1. Passa a Gestione configurazione OSGi `<host>/system/console/configMgr`
1. Trova la configurazione OSGi, ad Adobe Granite HTML Library Manager:
   * Seleziona la casella di controllo per abilitare il controllo delle versioni rigorose
   * Nel campo etichettato **Chiave cache lato client a lungo termine**, immetti il valore di /.*;hash
1. Salva le modifiche. Non è necessario salvare questa configurazione nel controllo del codice sorgente perché AEM as a Cloud Service la abilita automaticamente negli ambienti di sviluppo, staging e produzione.
1. Ogni volta che il contenuto della libreria client viene modificato, viene generata una nuova chiave hash e il riferimento HTML viene aggiornato.
