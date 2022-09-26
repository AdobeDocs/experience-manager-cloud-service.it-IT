---
title: Rendering lato SPA e server
description: L’utilizzo del rendering lato server (SSR) nel SPA può accelerare il caricamento iniziale della pagina e quindi passare ulteriori rendering al client.
exl-id: be409559-c7ce-4bc2-87cf-77132d7c2da1
source-git-commit: cc50520d7ee2bb3e7d1491154d531aa84ac9e956
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 0%

---

# Rendering lato SPA e server{#spa-and-server-side-rendering}

Le applicazioni a pagina singola (SPA) possono offrire all’utente un’esperienza ricca e dinamica che reagisce e si comporta in modo familiare, spesso come un’applicazione nativa. [Questo si ottiene facendo affidamento sul client per caricare il contenuto in anticipo e poi fare il sollevamento pesante dell&#39;interazione dell&#39;utente di gestione](introduction.md#how-does-a-spa-work) riducendo al minimo la quantità di comunicazione necessaria tra client e server, rendendo l&#39;app più reattiva.

Tuttavia, questo può causare tempi di caricamento iniziali più lunghi, soprattutto se il SPA è grande e ricco di contenuti. Per ottimizzare i tempi di caricamento, è possibile eseguire il rendering di alcuni contenuti lato server. L’utilizzo del rendering lato server (SSR) può accelerare il caricamento iniziale della pagina e quindi passare ulteriori rendering al client.

## Quando utilizzare SSR {#when-to-use-ssr}

SSR non è richiesto per tutti i progetti. Anche se AEM supporta completamente JS SSR per SPA, Adobe consiglia di non implementarlo sistematicamente per ogni progetto.

Quando si decide di implementare SSR, è innanzitutto necessario stimare la complessità, lo sforzo e i costi aggiuntivi che l’SSR rappresenta realisticamente per il progetto, inclusa la manutenzione a lungo termine. È opportuno scegliere un’architettura SSR solo quando il valore aggiunto supera chiaramente i costi stimati.

SSR di solito fornisce un certo valore quando c&#39;è un chiaro &quot;sì&quot; a una delle seguenti domande:

* **SEO:** SSR è ancora effettivamente necessario per il tuo sito per essere indicizzato correttamente dai motori di ricerca che portano traffico? Tieni presente che i principali crawler del motore di ricerca ora valutano JS.
* **Velocità pagina:** L’SSR fornisce un miglioramento della velocità misurabile negli ambienti reali e aggiunge all’esperienza complessiva dell’utente?

Solo quando almeno una di queste due domande riceve una risposta con un chiaro &quot;sì&quot; per il progetto, l’Adobe consiglia di implementare SSR. Le sezioni seguenti descrivono come eseguire questa operazione utilizzando Adobe I/O Runtime, parte di [App Builder](https://developer.adobe.com/app-builder).

## Adobe I/O Runtime {#adobe-i-o-runtime}

Se [sono sicuro che il tuo progetto richiede l’implementazione di SSR](#when-to-use-ssr), la soluzione consigliata di Adobe è l’utilizzo di Adobe I/O Runtime.

Per ulteriori informazioni su Adobe I/O Runtime, consulta

* [https://developer.adobe.com/runtime](https://developer.adobe.com/runtime) - Panoramica della funzione Runtime di App Builder
* [https://developer.adobe.com/app-builder](https://developer.adobe.com/app-builder) - per informazioni dettagliate sul prodotto App Builder completo
* [https://developer.adobe.com/runtime/docs/](https://developer.adobe.com/runtime/docs) - per la documentazione dettagliata

Nelle sezioni seguenti viene illustrato come Adobe I/O Runtime può essere utilizzato per implementare SSR per la tua SPA in due modelli diversi:

* [Flusso di comunicazione AEM](#aem-driven-communication-flow)
* [Flusso di comunicazione basato su Adobe I/O Runtime](#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>Adobe consiglia un’area di lavoro Adobe I/O Runtime separata per ambiente (stage, prod, test, ecc.). Ciò consente modelli tipici del ciclo di vita dello sviluppo dei sistemi (SDLC) con diverse versioni di una singola applicazione implementate in ambienti diversi.  Vedere il documento [CI/CD per applicazioni di App Builder](https://developer.adobe.com/app-builder/docs/guides/deployment/ci_cd_for_firefly_apps/) per ulteriori informazioni.
>
>Un’area di lavoro separata non è necessaria per istanza (autore, pubblicazione) a meno che non vi siano differenze nell’implementazione di runtime per tipo di istanza.

## Configurazione del modulo di rendering remoto {#remote-content-renderer-configuration}

AEM sapere dove è possibile recuperare il contenuto di cui è stato eseguito il rendering in remoto. Indipendentemente dal [quale modello si sceglie di implementare per SSR,](#adobe-i-o-runtime) dovrai specificare come AEM accedere a questo servizio di rendering remoto.

Questo avviene tramite il **RemoteContentRenderer - Servizio OSGi di Configuration Factory**. Cerca la stringa &quot;RemoteContentRenderer&quot; nella console Configurazione console Web Console in `http://<host>:<port>/system/console/configMgr`.

![Configurazione del renderer](assets/renderer-configuration.png)

Per la configurazione sono disponibili i campi seguenti:

* **Pattern di percorso del contenuto** - Espressione regolare per far corrispondere una parte del contenuto, se necessario
* **URL endpoint remoto** - URL dell’endpoint responsabile della generazione del contenuto
   * Utilizzare il protocollo HTTPS protetto se non nella rete locale.
* **Intestazioni di richiesta aggiuntive** - Intestazioni aggiuntive da aggiungere alla richiesta inviata all&#39;endpoint remoto
   * Pattern: `key=value`
* **Timeout richiesta** - Timeout della richiesta host remoto in millisecondi

>[!NOTE]
>
>Indipendentemente da se scegli di implementare il [Flusso di comunicazione AEM](#aem-driven-communication-flow) o [flusso basato su Adobe I/O Runtime,](#adobe-i-o-runtime-driven-communication-flow) è necessario definire una configurazione di rendering del contenuto remoto.

>[!NOTE]
>
>Questa configurazione sfrutta la [Modulo di rendering remoto dei contenuti,](#remote-content-renderer) che dispone di opzioni di estensione e personalizzazione aggiuntive.

## Flusso di comunicazione AEM {#aem-driven-communication-flow}

Quando utilizzi SSR, la [flusso di lavoro di interazione dei componenti](introduction.md#interaction-with-the-spa-editor) di SPA in AEM include una fase in cui il contenuto iniziale dell’app viene generato su Adobe I/O Runtime.

1. Il browser richiede il contenuto SSR da AEM.
1. AEM il modello pubblicato su Adobe I/O Runtime.
1. Adobe I/O Runtime restituisce il contenuto generato.
1. AEM serve il HTML restituito da Adobe I/O Runtime tramite il modello HTL del componente della pagina di back-end.

![Adobe I/O AEM basato su SSE CMS](assets/ssr-cms-drivenaemnode-adobeio.png)

## Flusso di comunicazione basato su Adobe I/O Runtime {#adobe-i-o-runtime-driven-communication-flow}

La sezione precedente descrive l’implementazione standard e consigliata del rendering lato server per quanto riguarda la SPA in AEM, dove AEM esegue il bootstrap e il serving del contenuto.

In alternativa, SSR può essere implementato in modo che Adobe I/O Runtime sia responsabile del bootstrap, invertendo efficacemente il flusso di comunicazione.

Entrambi i modelli sono validi e supportati da AEM. Tuttavia, è opportuno considerare i vantaggi e gli svantaggi di ciascuno prima di implementare un particolare modello.

<table>
 <tbody>
  <tr>
   <th><strong>Bootstrap</strong></th>
   <th><strong>Vantaggi</strong></th>
   <th><strong>Svantaggi</strong></th>
  </tr>
  <tr>
   <th><strong>via AEM</strong><br /> </th>
   <td>
    <ul>
     <li>AEM gestisce l’inserimento delle librerie laddove necessario</li>
     <li>Le risorse devono essere mantenute solo su AEM<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Probabilmente non familiare allo sviluppatore SPA<br /> </li>
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
     <li>Le risorse clientlib richieste dall’applicazione, come CSS e JavaScript, dovranno essere rese disponibili dallo sviluppatore AEM tramite il <code><a href="/help/implementing/developing/introduction/clientlibs.md">allowProxy</a></code> property<br /> </li>
     <li>Le risorse devono essere sincronizzate tra AEM e Adobe I/O Runtime<br /> </li>
     <li>Per abilitare l'authoring del SPA, potrebbe essere necessario un server proxy per Adobe I/O Runtime</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Pianificazione del SSR {#planning-for-ssr}

Generalmente solo una parte di un&#39;applicazione deve essere sottoposta a rendering sul lato server. L’esempio comune è il contenuto che verrà visualizzato sopra la piega al caricamento iniziale della pagina viene rappresentato sul lato server. Questo consente di risparmiare tempo distribuendo al client contenuti già sottoposti a rendering. Quando l’utente interagisce con il SPA, il client esegue il rendering del contenuto aggiuntivo.

Quando consideri l&#39;implementazione del rendering lato server per il tuo SPA, devi verificare quali parti dell&#39;app saranno necessarie.

## Sviluppo di un SPA utilizzando SSR {#developing-an-spa-using-ssr}

È possibile eseguire il rendering dei componenti SPA dal lato client (nel browser) o server. Quando viene eseguito il rendering sul lato server, le proprietà del browser, ad esempio le dimensioni e la posizione della finestra, non sono presenti. Pertanto, SPA componenti dovrebbero essere isomorfi, senza prendere in considerazione dove saranno resi.

Per sfruttare SSR, dovrai distribuire il codice in AEM e su Adobe I/O Runtime, responsabile del rendering lato server. La maggior parte del codice sarà la stessa, ma le attività specifiche del server saranno diverse.

## SSR per SPA in AEM {#ssr-for-spas-in-aem}

SSR per SPA in AEM richiede Adobe I/O Runtime, che è chiamato per il rendering del lato server del contenuto dell’app. All’interno dell’HTL dell’app, viene chiamata una risorsa su Adobe I/O Runtime per eseguire il rendering del contenuto.

Proprio come AEM supporta i framework Angular e React SPA pronti all’uso, anche il rendering lato server è supportato per le app Angular e React. Per ulteriori informazioni, consulta la documentazione NPM per entrambi i framework.

## Renderer di contenuti remoti {#remote-content-renderer}

La [Configurazione del modulo di rendering del contenuto remoto](#remote-content-renderer-configuration) che è necessario utilizzare SSR con il tuo SPA in AEM tocco in un servizio di rendering più generalizzato che può essere esteso e personalizzato per soddisfare le tue esigenze.

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` è un servizio OSGi per recuperare il contenuto di cui è stato eseguito il rendering su un server remoto, ad esempio da Adobe I/O. Il contenuto inviato al server remoto si basa sul parametro della richiesta trasmesso.

`RemoteContentRenderingService` può essere inserito dall’inversione della dipendenza in un modello Sling personalizzato o in un servlet quando è necessaria un’ulteriore manipolazione del contenuto.

Questo servizio è utilizzato internamente dal [RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet).

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

La `RemoteContentRendererRequestHandlerServlet` può essere utilizzato per impostare programmaticamente la configurazione della richiesta. `DefaultRemoteContentRendererRequestHandlerImpl`, l’implementazione predefinita del gestore delle richieste fornita, consente di creare più configurazioni OSGi per mappare una posizione nella struttura del contenuto a un endpoint remoto.

Per aggiungere un gestore di richieste personalizzato, implementa `RemoteContentRendererRequestHandler` interfaccia. Assicurati di impostare il `Constants.SERVICE_RANKING` proprietà del componente a un numero intero superiore a 100, che è la classificazione del `DefaultRemoteContentRendererRequestHandlerImpl`.

```javascript
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### Configurare la configurazione OSGi del gestore predefinito {#configure-default-handler}

La configurazione del gestore predefinito deve essere configurata come descritto nella sezione [Configurazione del modulo di rendering del contenuto remoto](#remote-content-renderer-configuration).

### Utilizzo del modulo di rendering del contenuto remoto {#usage}

Per ottenere un servlet di recupero e restituire alcuni contenuti che possono essere inseriti nella pagina:

1. Verificare che il server remoto sia accessibile.
1. Aggiungi uno dei seguenti snippet al modello HTL di un componente AEM.
1. Facoltativamente, crea o modifica le configurazioni OSGi.
1. Sfoglia il contenuto del sito

Di solito, il modello HTL di un componente pagina è il destinatario principale di tale funzione.

```html
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### Requisiti  {#requirements}

I servlet sfruttano l’esportatore di modelli Sling per serializzare i dati dei componenti. Per impostazione predefinita, entrambe le `com.adobe.cq.export.json.ContainerExporter` e `com.adobe.cq.export.json.ComponentExporter` sono supportate come schede di rete Sling Model. Se necessario, puoi aggiungere classi alle quali la richiesta deve essere adattata utilizzando il `RemoteContentRendererServlet` e l&#39;attuazione `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`. Le classi aggiuntive devono estendere il `ComponentExporter`.
