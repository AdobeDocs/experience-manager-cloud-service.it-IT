---
title: Rendering lato server e SPA
description: L’utilizzo del rendering lato server (SSR) nell’SPA può accelerare il caricamento iniziale della pagina e quindi passare un ulteriore rendering al client.
exl-id: be409559-c7ce-4bc2-87cf-77132d7c2da1
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1498'
ht-degree: 0%

---

# Rendering lato server e SPA{#spa-and-server-side-rendering}

Le applicazioni a pagina singola (SPA) possono offrire all’utente un’esperienza ricca e dinamica che reagisce e si comporta in modo familiare, spesso come un’applicazione nativa. [Ciò si ottiene affidandosi al client per caricare il contenuto in primo piano e poi fare il pesante sollevamento dell&#39;interazione dell&#39;utente](introduction.md#how-does-a-spa-work) riducendo al minimo la quantità di comunicazione necessaria tra client e server, rendendo l’app più reattiva.

Tuttavia, questo può portare a tempi di caricamento iniziali più lunghi, soprattutto se l’SPA è grande e ricco di contenuti. Per ottimizzare i tempi di caricamento, è possibile eseguire il rendering di alcuni contenuti lato server. L’utilizzo del rendering lato server (SSR) può accelerare il caricamento iniziale della pagina e quindi trasmettere un ulteriore rendering al client.

## Quando utilizzare SSR {#when-to-use-ssr}

SSR non è richiesto per tutti i progetti. Sebbene l’AEM supporti completamente la SSR JS per l’SPA, l’Adobe sconsiglia di attuarla sistematicamente per ogni progetto.

Quando si decide di implementare SSR, è necessario innanzitutto stimare la complessità, l&#39;impegno e i costi aggiuntivi che la SSR rappresenta in modo realistico per il progetto, inclusa la manutenzione a lungo termine. Un’architettura SSR dovrebbe essere scelta solo quando il valore aggiunto supera chiaramente i costi stimati.

In genere, SSR fornisce un valore quando è presente un &quot;sì&quot; chiaro a una delle seguenti domande:

* **SEO:** SSR è ancora necessario per la corretta indicizzazione del sito da parte dei motori di ricerca che generano traffico? Tieni presente che i crawler del motore di ricerca principale ora valutano JS.
* **Velocità pagina:** SSR fornisce un miglioramento della velocità misurabile in ambienti reali e contribuisce all&#39;esperienza complessiva dell&#39;utente?

Solo quando ad almeno una di queste due domande viene risposto con un chiaro &quot;sì&quot; per il progetto, Adobe consiglia di implementare SSR. Le sezioni seguenti descrivono come eseguire questa operazione utilizzando Adobe I/O Runtime, parte di [App Builder](https://developer.adobe.com/app-builder).

## Adobe I/O Runtime {#adobe-i-o-runtime}

Se [sono certi che il tuo progetto richieda l&#39;implementazione di SSR](#when-to-use-ssr), la soluzione consigliata da Adobe è l’utilizzo di Adobe I/O Runtime.

Per ulteriori informazioni su Adobe I/O Runtime, consulta

* [https://developer.adobe.com/runtime](https://developer.adobe.com/runtime) : panoramica della funzione Runtime di App Builder
* [https://developer.adobe.com/app-builder](https://developer.adobe.com/app-builder) - per informazioni dettagliate sul prodotto App Builder completo
* [https://developer.adobe.com/runtime/docs/](https://developer.adobe.com/runtime/docs) - documentazione dettagliata

Le sezioni seguenti descrivono come Adobe I/O Runtime può essere utilizzato per implementare SSR per l’SPA in due modelli diversi:

* [Flusso di comunicazione basato sull’AEM](#aem-driven-communication-flow)
* [Flusso di comunicazione basato su Adobe I/O Runtime](#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>L’Adobe consiglia un’area di lavoro Adobe I/O Runtime separata per ogni ambiente (stage, prod, test, ecc.). Ciò consente di implementare i modelli SDLC (System Development Life Cycle) tipici con versioni diverse di una singola applicazione distribuite in ambienti diversi.  Consulta il documento [CI/CD per applicazioni App Builder](https://developer.adobe.com/app-builder/docs/guides/deployment/ci_cd_for_firefly_apps/) per ulteriori informazioni.
>
>Un’area di lavoro separata non è necessaria per ogni istanza (Author, Publish) a meno che non vi siano differenze nell’implementazione runtime per tipo di istanza.

## Configurazione Remote Renderer {#remote-content-renderer-configuration}

L’AEM deve sapere dove è possibile recuperare i contenuti renderizzati in remoto. Indipendentemente da [il modello che si sceglie di implementare per SSR,](#adobe-i-o-runtime) sarà necessario specificare a AEM come accedere a questo servizio di rendering remoto.

Questa operazione viene eseguita tramite **RemoteContentRenderer - Servizio OSGi di Configuration Factory**. Cerca la stringa &quot;RemoteContentRenderer&quot; nella console di configurazione della console Web all&#39;indirizzo `http://<host>:<port>/system/console/configMgr`.

![Configurazione rendering](assets/renderer-configuration.png)

Per la configurazione sono disponibili i seguenti campi:

* **Schema percorso contenuto** : espressione regolare che corrisponde a una parte del contenuto, se necessario
* **URL endpoint remoto** : URL dell’endpoint responsabile della generazione del contenuto
   * Utilizza il protocollo HTTPS protetto se non si trova nella rete locale.
* **Intestazioni di richiesta aggiuntive** - Intestazioni aggiuntive da aggiungere alla richiesta inviata all’endpoint remoto
   * Pattern: `key=value`
* **Timeout richiesta** - Timeout della richiesta dell&#39;host remoto in millisecondi

>[!NOTE]
>
>Indipendentemente da se scegli di implementare [Flusso di comunicazione basato sull&#39;AEM](#aem-driven-communication-flow) o [Flusso basato su Adobe I/O Runtime](#adobe-i-o-runtime-driven-communication-flow) è necessario definire una configurazione del renderer del contenuto remoto.

>[!NOTE]
>
>Questa configurazione utilizza [Rendering contenuto remoto,](#remote-content-renderer) che dispone di opzioni di estensione e personalizzazione aggiuntive.

## Flusso di comunicazione basato sull’AEM {#aem-driven-communication-flow}

Quando si utilizza SSR, il [flusso di lavoro di interazione dei componenti](introduction.md#interaction-with-the-spa-editor) dell’SPA nell’AEM include una fase in cui il contenuto iniziale dell’app viene generato su Adobe I/O Runtime.

1. Il browser richiede il contenuto SSR all’AEM.
1. L&#39;AEM pubblica il modello su Adobe I/O Runtime.
1. Adobe I/O Runtime restituisce il contenuto generato.
1. AEM fornisce le HTML restituite da Adobe I/O Runtime tramite il modello HTL del componente pagina back-end.

![ADOBE I/O AEM basato su SSE CMS](assets/ssr-cms-drivenaemnode-adobeio.png)

## Flusso di comunicazione basato su Adobe I/O Runtime {#adobe-i-o-runtime-driven-communication-flow}

La sezione precedente descrive l’implementazione standard e consigliata del rendering lato server per quanto riguarda l’SPA nell’AEM, in cui l’AEM esegue il bootstrapping e la trasmissione dei contenuti.

In alternativa, SSR può essere implementato in modo che Adobe I/O Runtime sia responsabile dell&#39;avvio, invertendo efficacemente il flusso di comunicazione.

Entrambi i modelli sono validi e supportati dall’AEM. Tuttavia, si dovrebbero considerare i vantaggi e gli svantaggi di ciascuno prima di implementare un particolare modello.

<table>
 <tbody>
  <tr>
   <th><strong>Bootstrap</strong></th>
   <th><strong>Vantaggi</strong></th>
   <th><strong>Svantaggi</strong></th>
  </tr>
  <tr>
   <th><strong>tramite AEM</strong><br /> </th>
   <td>
    <ul>
     <li>L'AEM gestisce le librerie di iniezione dove necessario</li>
     <li>Le risorse devono essere mantenute solo sull'AEM<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Possibilmente non familiare allo sviluppatore SPA<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>tramite Adobe I/O Runtime<br /> </strong></th>
   <td>
    <ul>
     <li>Più familiare agli sviluppatori SPA<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Le risorse Clientlib richieste dall’applicazione, come CSS e JavaScript, dovranno essere rese disponibili dallo sviluppatore AEM tramite <code><a href="/help/implementing/developing/introduction/clientlibs.md">allowProxy</a></code> proprietà<br /> </li>
     <li>Le risorse devono essere sincronizzate tra AEM e Adobe I/O Runtime<br /> </li>
     <li>Per abilitare la creazione dell'SPA, potrebbe essere necessario un server proxy per Adobe I/O Runtime</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Pianificazione per SSR {#planning-for-ssr}

In genere, è necessario eseguire il rendering lato server solo di una parte dell’applicazione. L’esempio comune è il contenuto visualizzato sopra la piega al caricamento iniziale della pagina, di cui viene eseguito il rendering sul lato server. In questo modo si risparmia tempo distribuendo al client contenuti già sottoposti a rendering. Quando l’utente interagisce con l’SPA, il contenuto aggiuntivo viene riprodotto dal client.

Se stai valutando l’implementazione del rendering lato server per l’SPA, devi verificare quali parti dell’app sono necessarie.

## Sviluppo di un SPA utilizzando la SSR {#developing-an-spa-using-ssr}

Il rendering dei componenti SPA poteva essere eseguito dal client (nel browser) o dal lato server. Quando viene eseguito il rendering lato server, le proprietà del browser come le dimensioni della finestra e la posizione non sono presenti. Pertanto, i componenti dell’SPA devono essere isomorfi, senza supporre dove vengono resi.

Per utilizzare SSR, devi distribuire il codice in AEM e su Adobe I/O Runtime, che è responsabile del rendering lato server. La maggior parte del codice è lo stesso, tuttavia le attività specifiche del server differiscono.

## SSR per l’SPA nell’AEM {#ssr-for-spas-in-aem}

La SSR per l’SPA nell’AEM richiede Adobe I/O Runtime, che è chiamato per il rendering del lato server del contenuto dell’app. All’interno dell’HTL dell’app, viene chiamata una risorsa su Adobe I/O Runtime per eseguire il rendering del contenuto.

Proprio come l’AEM supporta i framework SPA Angular e React pronti all’uso, è supportato anche il rendering lato server, ad Angular per le app React. Per ulteriori dettagli, consulta la documentazione NPM per entrambi i framework.

## Rendering contenuto remoto {#remote-content-renderer}

Il [Configurazione rendering contenuto remoto](#remote-content-renderer-configuration) che è necessario per utilizzare SSR con il tuo SPA in AEM si inserisce in un servizio di rendering più generalizzato che può essere esteso e personalizzato per soddisfare le tue esigenze.

### Servizio RemoteContentRendering {#remotecontentrenderingservice}

`RemoteContentRenderingService` è un servizio OSGi per recuperare il contenuto di cui è stato eseguito il rendering su un server remoto, ad esempio da Adobe I/O. Il contenuto inviato al server remoto si basa sul parametro di richiesta passato.

`RemoteContentRenderingService` può essere inserito tramite inversione delle dipendenze in un modello Sling personalizzato o in un servlet quando è necessaria un’ulteriore manipolazione del contenuto.

Questo servizio è utilizzato internamente da [RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet).

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

Il `RemoteContentRendererRequestHandlerServlet` può essere utilizzato per impostare a livello di programmazione la configurazione della richiesta. `DefaultRemoteContentRendererRequestHandlerImpl`, l’implementazione predefinita del gestore di richieste fornita, ti consente di creare più configurazioni OSGi in modo da poter mappare una posizione nella struttura del contenuto a un endpoint remoto.

Per aggiungere un gestore di richieste personalizzato, implementa `RemoteContentRendererRequestHandler` di rete. Assicurarsi di impostare `Constants.SERVICE_RANKING` proprietà del componente a un numero intero maggiore di 100, che corrisponde alla classificazione `DefaultRemoteContentRendererRequestHandlerImpl`.

```javascript
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### Configurare la configurazione OSGi del gestore predefinito {#configure-default-handler}

La configurazione del gestore predefinito deve essere configurata come descritto nella sezione [Configurazione rendering contenuto remoto](#remote-content-renderer-configuration).

### Utilizzo di Remote Content Renderer {#usage}

Per recuperare un servlet e restituire parte del contenuto che può essere inserito nella pagina:

1. Verificare che il server remoto sia accessibile.
1. Aggiungi uno dei seguenti snippet al modello HTL di un componente AEM.
1. Facoltativamente, crea o modifica le configurazioni OSGi.
1. Sfogliare il contenuto del sito

Di solito, il modello HTL di un componente pagina è il destinatario principale di tale funzione.

```html
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### Requisiti {#requirements}

I servlet utilizzano Sling Model Exporter per serializzare i dati del componente. Per impostazione predefinita, entrambe le opzioni `com.adobe.cq.export.json.ContainerExporter` e `com.adobe.cq.export.json.ComponentExporter` sono supportati come adattatori del modello Sling. Se necessario, puoi aggiungere le classi a cui la richiesta deve essere adattata utilizzando `RemoteContentRendererServlet` e l&#39;implementazione `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`. Le classi aggiuntive devono estendere `ComponentExporter`.
