---
title: Rendering SPA e lato server
description: L’utilizzo del rendering lato server (SSR) nell’area dell’app può accelerare il caricamento iniziale della pagina e quindi passare al client un ulteriore rendering.
translation-type: tm+mt
source-git-commit: c2c338061d72ae6c5054d18308a2ea1038eaea39
workflow-type: tm+mt
source-wordcount: '1451'
ht-degree: 0%

---


# Rendering SPA e lato server{#spa-and-server-side-rendering}

Le applicazioni SPA (Single Page Applications) possono offrire all&#39;utente un&#39;esperienza ricca e dinamica che reagisce e si comporta in modo familiare, spesso come un&#39;applicazione nativa. [Ciò si ottiene affidandosi al client per caricare i contenuti in primo piano e quindi sfruttando l&#39;interazione](introduction.md#how-does-a-spa-work) con l&#39;utente, riducendo al minimo la quantità di comunicazione necessaria tra il client e il server, rendendo l&#39;app più reattiva.

Tuttavia, questo può comportare tempi di caricamento iniziali più lunghi, soprattutto se l&#39;SPA è grande e ricco di contenuti. Per ottimizzare i tempi di caricamento, è possibile eseguire il rendering di parte del contenuto sul lato server. L’utilizzo del rendering lato server (SSR) può accelerare il caricamento iniziale della pagina e quindi passare al client un ulteriore rendering.

## Quando utilizzare SSR {#when-to-use-ssr}

SSR non è richiesto per tutti i progetti. Sebbene AEM supportare completamente JS SSR per SPA,  Adobe non consiglia di implementarlo sistematicamente per ogni progetto.

Quando si decide di implementare SSR è necessario prima stimare quale ulteriore complessità, sforzo e costo supplementare SSR rappresenta realisticamente per il progetto, inclusa la manutenzione a lungo termine. L&#39;architettura SSR dovrebbe essere scelta solo quando il valore aggiunto supera chiaramente i costi stimati.

SSR di solito fornisce un certo valore quando esiste un chiaro &quot;sì&quot; a una delle seguenti domande:

* **SEO:** Il servizio SSR è ancora effettivamente richiesto affinché il sito venga indicizzato correttamente dai motori di ricerca che generano traffico? Tenere presente che i principali crawler del motore di ricerca ora valutano JS.
* **Velocità pagina:** La SSR offre un miglioramento misurabile della velocità negli ambienti reali e contribuisce all&#39;esperienza complessiva dell&#39;utente?

Solo quando almeno una di queste due domande riceve una risposta con un chiaro &quot;sì&quot; per il progetto,  Adobe consiglia di implementare SSR. Le sezioni seguenti descrivono come eseguire questa operazione utilizzando Adobe I/O Runtime.

## Adobe I/O Runtime {#adobe-i-o-runtime}

Se [sei sicuro che il progetto richiede l&#39;implementazione di SSR](#when-to-use-ssr),  Adobe  soluzione consigliata è utilizzare Adobe I/O Runtime.

Per maggiori informazioni su Adobe I/O Runtime, consulta

* [https://www.adobe.io/apis/experienceplatform/runtime.html](https://www.adobe.io/apis/experienceplatform/runtime.html) - per una panoramica del servizio
* [https://www.adobe.io/apis/experienceplatform/runtime/docs.html](https://www.adobe.io/apis/experienceplatform/runtime/docs.html) - per una documentazione dettagliata sulla piattaforma

Nelle sezioni seguenti viene illustrato come Adobe I/O Runtime può essere utilizzato per implementare SSR per la propria SPA in due modelli diversi:

* [Flusso di comunicazione AEM](#aem-driven-communication-flow)
* [Flusso di comunicazione basato su Adobe I/O Runtime](#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
> Adobe consiglia un’istanza Adobe I/O Runtime separata per ogni ambiente AEM (autore, pubblicazione, area di visualizzazione, ecc.).

## Configurazione del rendering remoto {#remote-renderer-configuration}

AEM sapere dove è possibile recuperare il contenuto sottoposto a rendering remoto. Indipendentemente dal modello [che si sceglie di implementare per SSR,](#adobe-i-o-runtime) sarà necessario specificare AEM modalità di accesso a questo servizio di rendering remoto.

Questa operazione viene eseguita tramite il servizio **RemoteContentRenderer - Configuration Factory OSGi service**. Cercate la stringa &quot;RemoteContentRenderer&quot; nella console Configurazione console Web all’indirizzo `http://<host>:<port>/system/console/configMgr`.

![Configurazione rendering](assets/renderer-configuration.png)

I campi seguenti sono disponibili per la configurazione:

* **Percorso** contenuto - Espressione regolare per far corrispondere una parte del contenuto, se necessario
* **URL** endpoint remoto - URL dell&#39;endpoint responsabile della generazione del contenuto
   * Utilizzare il protocollo HTTPS protetto se non nella rete locale.
* **Intestazioni** di richiesta aggiuntive - Intestazioni aggiuntive da aggiungere alla richiesta inviata all&#39;endpoint remoto
   * Pattern: `key=value`
* **Timeout** richiesta - Timeout richiesta host remoto in millisecondi

>[!NOTE]
>
>Indipendentemente dalla scelta di implementare il flusso [di comunicazione basato su](#aem-driven-communication-flow) AEM o il flusso basato su [Adobe I/O Runtime,](#adobe-i-o-runtime-driven-communication-flow) è necessario definire una configurazione di rendering del contenuto remoto.
>
>Questa configurazione deve essere definita anche se scegli di [utilizzare un server Node.js personalizzato.](#using-node-js)

>[!NOTE]
>
>Questa configurazione sfrutta il modulo di rendering dei contenuti [remoti,](#remote-content-renderer) che offre ulteriori opzioni di estensione e personalizzazione.

## Flusso di comunicazione AEM {#aem-driven-communication-flow}

Quando si utilizza SSR, il flusso di lavoro [di interazione dei](introduction.md#workflow) componenti dell&#39;app in AEM include una fase in cui il contenuto iniziale dell&#39;app viene generato su Adobe I/O Runtime.

1. Il browser richiede il contenuto SSR da AEM.
1. AEM postare il modello su Adobe I/O Runtime.
1. Adobe I/O Runtime restituisce il contenuto generato.
1. AEM serve l’HTML restituito da Adobe I/O Runtime tramite il modello HTL del componente della pagina di back-end.

![I/O AEM Adobe SSE CMS](assets/ssr-cms-drivenaemnode-adobeio.png)

## Flusso di comunicazione basato su Adobe I/O Runtime {#adobe-i-o-runtime-driven-communication-flow}

La sezione precedente descrive l&#39;implementazione standard e consigliata del rendering lato server per quanto riguarda gli SPA in AEM, dove AEM eseguire il bootstrap e la trasmissione dei contenuti.

In alternativa, SSR può essere implementato in modo che Adobe I/O Runtime sia responsabile del bootstrap, invertendo efficacemente il flusso di comunicazione.

Entrambi i modelli sono validi e supportati da AEM. Tuttavia, è opportuno considerare i vantaggi e gli svantaggi di ciascuno di essi prima di implementare un particolare modello.

<table>
 <tbody>
  <tr>
   <th><strong>Avvio</strong></th>
   <th><strong>Vantaggi</strong></th>
   <th><strong>Svantaggi</strong></th>
  </tr>
  <tr>
   <th><strong>via AEM</strong><br /> </th>
   <td>
    <ul>
     <li>AEM gestisce l'inserimento delle librerie laddove necessario</li>
     <li>Le risorse devono essere mantenute solo su AEM<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Potrebbe non essere familiare allo sviluppatore SPA<br /> </li>
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
     <li>Le risorse Clientlib richieste dall'applicazione, come CSS e JavaScript, dovranno essere rese disponibili dallo sviluppatore AEM tramite la <code>allowProxy</code> proprietà<br /> </li>
     <li>Le risorse devono essere sincronizzate tra AEM e Adobe I/O Runtime<br /> </li>
     <li>Per abilitare la creazione dell'SPA, potrebbe essere necessario un server proxy per Adobe I/O Runtime</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Pianificazione per SSR {#planning-for-ssr}

In genere, è necessario eseguire il rendering solo di una parte dell&#39;applicazione sul lato server. L’esempio comune è rappresentato dal contenuto che verrà visualizzato al di sopra della piega al caricamento iniziale della pagina, rappresentato sul lato server. Questo consente di risparmiare tempo distribuendo al client contenuti già sottoposti a rendering. Quando l&#39;utente interagisce con l&#39;app, il contenuto aggiuntivo viene rappresentato dal client.

Considerando l&#39;implementazione del rendering lato server per l&#39;app SPA, è necessario verificare quali parti dell&#39;app saranno necessarie.

## Sviluppo di una SPA con SSR {#developing-an-spa-using-ssr}

I componenti SPA possono essere sottoposti a rendering dal lato client (nel browser) o server. Sul lato server di cui è stato eseguito il rendering, le proprietà del browser, ad esempio la dimensione della finestra e la posizione, non sono presenti. Pertanto, i componenti SPA dovrebbero essere isomorfi, senza fare alcuna ipotesi su dove saranno sottoposti a rendering.

Per sfruttare SSR, dovrete distribuire il codice sia in AEM che in Adobe I/O Runtime, responsabile per il rendering lato server. La maggior parte del codice sarà uguale, ma le attività specifiche del server saranno diverse.

## SSR per SPA in AEM {#ssr-for-spas-in-aem}

SSR per le app SPA in AEM richiede Adobe I/O Runtime, che viene chiamato per il rendering del lato server del contenuto dell&#39;app. All’interno dell’HTL dell’app, viene chiamata una risorsa su Adobe I/O Runtime per eseguire il rendering del contenuto.

Come AEM supporta i framework Angular e React SPA out-of-the-box, anche il rendering lato server è supportato per le app Angular e React. Per ulteriori informazioni, consulta la documentazione di NPM per entrambi i framework.

## Modulo di rendering contenuti remoto {#remote-content-renderer}

La configurazione [](#remote-content-renderer-configuration) Remote Content Renderer necessaria per utilizzare SSR con l&#39;SPA in AEM tocca un servizio di rendering più generalizzato che può essere esteso e personalizzato in base alle proprie esigenze.

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` è un servizio OSGi per recuperare il contenuto su un server remoto, ad esempio da  I/O Adobe. Il contenuto inviato al server remoto si basa sul parametro di richiesta passato.

`RemoteContentRenderingService` può essere iniettato dall&#39;inversione di dipendenza in un modello Sling personalizzato o servlet quando è richiesta ulteriore manipolazione del contenuto.

Questo servizio viene utilizzato internamente da [RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet).

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

L&#39; `RemoteContentRendererRequestHandlerServlet` opzione può essere utilizzata per impostare in modo programmatico la configurazione della richiesta. `DefaultRemoteContentRendererRequestHandlerImpl`, l&#39;implementazione del gestore di richieste predefinito fornita, consente di creare più configurazioni OSGi per mappare una posizione nella struttura del contenuto a un endpoint remoto.

Per aggiungere un gestore di richieste personalizzato, implementate l&#39; `RemoteContentRendererRequestHandler` interfaccia. Accertatevi di impostare la proprietà del `Constants.SERVICE_RANKING` componente su un numero intero superiore a 100, che corrisponde alla classifica del `DefaultRemoteContentRendererRequestHandlerImpl`.

```
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### Configurare la configurazione OSGi del gestore predefinito {#configure-default-handler}

La configurazione del gestore predefinito deve essere configurata come descritto nella sezione Configurazione [del modulo di rendering dei contenuti](#remote-content-renderer-configuration)remoti.

### Utilizzo del modulo di rendering dei contenuti remoti {#usage}

Per ottenere un servlet fetch e restituire il contenuto che può essere inserito nella pagina:

1. Verificare che il server remoto sia accessibile.
1. Aggiungete uno dei seguenti snippet al modello HTL di un componente AEM.
1. Facoltativamente, potete creare o modificare le configurazioni OSGi.
1. Sfogliare il contenuto del sito

In genere, il modello HTL di un componente di pagina è il destinatario principale di tale funzione.

```
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### Requisiti {#requirements}

I servlet sfruttano Sling Model Exporter per serializzare i dati dei componenti. Per impostazione predefinita, sia i modelli `com.adobe.cq.export.json.ContainerExporter` che `com.adobe.cq.export.json.ComponentExporter` sono supportati come adattatori Sling Model. Se necessario, è possibile aggiungere classi che la richiesta deve essere adattata all&#39;utilizzo `RemoteContentRendererServlet` e all&#39;implementazione di `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`. Le classi aggiuntive devono estendere l&#39; `ComponentExporter`.
