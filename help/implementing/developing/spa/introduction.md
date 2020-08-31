---
title: Introduzione e introduzione SPA
description: Questo articolo introduce i concetti di SPA e illustra come utilizzare un'applicazione SPA di base per l'authoring, mostrando il suo rapporto con l'Editor SPA AEM sottostante.
translation-type: tm+mt
source-git-commit: 78ce5113d97b0fa2e0172598d374c924f4306395
workflow-type: tm+mt
source-wordcount: '1930'
ht-degree: 0%

---


# Introduzione e introduzione SPA {#spa-introduction}

Le applicazioni SPA (Single Page Applications) possono offrire esperienze coinvolgenti agli utenti di siti Web. Gli sviluppatori desiderano essere in grado di creare siti utilizzando i framework SPA e gli autori desiderano modificare i contenuti all&#39;interno AEM per un sito creato utilizzando tali framework.

L&#39;editor SPA offre una soluzione completa per supportare gli SPA in AEM. Questo articolo descrive l’utilizzo di un’applicazione SPA di base per l’authoring e mostra il rapporto con l’Editor SPA AEM sottostante.

## Introduzione {#introduction}

### Articolo Obiettivo {#article-objective}

Questo articolo introduce i concetti di base degli SPA prima di guidare il lettore attraverso una panoramica dettagliata dell&#39;editor SPA, utilizzando una semplice applicazione SPA per dimostrare l&#39;editing di base dei contenuti. Viene quindi descritto come creare la pagina e come l&#39;applicazione SPA si collega e interagisce con l&#39;editor AEM SPA.

L&#39;obiettivo di questa introduzione e di questa panoramica è dimostrare a uno sviluppatore AEM perché le SPA sono rilevanti, come funzionano in generale, come una SPA viene gestita dall&#39;editor AEM SPA e come è diversa da un&#39;applicazione AEM standard.

La procedura dettagliata si basa sulla funzionalità standard AEM e sull&#39;app di esempio WKND SPA Project. Per seguire, [scaricate e installate l&#39;app di esempio WKND SPA Project da GitHub qui.](https://github.com/adobe/aem-guides-wknd-spa)

>[!CAUTION]
>
>Questo documento utilizza l&#39;app [WKND SPA Project](https://github.com/adobe/aem-guides-wknd-spa) solo a scopo dimostrativo. Non deve essere utilizzato per nessun progetto.

>[!TIP]
>
>Qualsiasi progetto AEM dovrebbe sfruttare il [AEM Project Archetype](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/archetype/overview.html), che supporta i progetti SPA utilizzando React o Angular e sfrutta l’SDK SPA.

### Che cos&#39;è un SPA? {#what-is-a-spa}

Un&#39;applicazione a pagina singola (SPA) differisce da una pagina tradizionale in quanto viene sottoposta a rendering sul lato client ed è principalmente guidata da Javascript, basandosi sulle chiamate Ajax per caricare i dati e aggiornare dinamicamente la pagina. La maggior parte o tutto il contenuto viene recuperato una volta in un singolo caricamento di pagina con risorse aggiuntive caricate in modo asincrono in base alle esigenze, in base all&#39;interazione dell&#39;utente con la pagina.

Questo riduce la necessità di aggiornare le pagine e offre all&#39;utente un&#39;esperienza semplice, rapida e più simile a un&#39;esperienza app nativa.

AEM SPA Editor consente agli sviluppatori front-end di creare SPA che possono essere integrati in un sito AEM, consentendo agli autori di modificare i contenuti SPA con la stessa facilità con cui si trovano altri contenuti AEM.

### Perché una SPA? {#why-a-spa}

Grazie a un&#39;applicazione nativa più veloce, fluida e semplice, l&#39;SPA diventa un&#39;esperienza molto interessante non solo per il visitatore della pagina Web, ma anche per gli esperti di marketing e gli sviluppatori, a causa della natura del funzionamento degli SPA.

![Vantaggi SPA](assets/spa-benefits.png)

#### Visitatori {#visitors}

* I visitatori desiderano esperienze simili a quelle native quando interagiscono con i contenuti.
* Esistono dati chiari che più veloce sarà una pagina, più probabile sarà una conversione.

#### Marketing {#marketers}

* Gli esperti di marketing desiderano offrire esperienze ricche e native per consentire ai visitatori di interagire pienamente con i contenuti.
* La personalizzazione può rendere queste esperienze ancora più coinvolgenti.

#### Sviluppatori {#developers}

* Gli sviluppatori desiderano una netta separazione tra contenuti e presentazioni.
* La separazione pulita rende il sistema più estensibile e consente uno sviluppo front-end indipendente.

### Come funziona una SPA? {#how-does-a-spa-work}

L&#39;idea principale alla base di uno SPA è che le chiamate e la dipendenza da un server vengono ridotte al fine di minimizzare i ritardi causati dalla latenza del server, in modo che l&#39;SPA si avvicini alla reattività di un&#39;applicazione nativa.

In una pagina Web sequenziale tradizionale, vengono caricati solo i dati necessari per la pagina immediata. Questo significa che quando il visitatore si sposta in un’altra pagina, il server viene chiamato per le risorse aggiuntive. Potrebbero essere necessarie chiamate aggiuntive quando il visitatore interagisce con gli elementi sulla pagina. Queste chiamate multiple possono dare un senso di ritardo o ritardo, in quanto la pagina deve essere in grado di soddisfare le richieste del visitatore.

![Esperienze sequenziali e fluide](assets/spa-sequential-vs-fluid.png)

Per un&#39;esperienza più fluida, che si avvicina alle aspettative di un visitatore dalle app native per dispositivi mobili, un&#39;app SPA carica tutti i dati necessari per il visitatore al primo caricamento. Anche se inizialmente l&#39;operazione potrebbe richiedere un po&#39; più di tempo, elimina la necessità di ulteriori chiamate server.

Rendering sul lato client, gli elementi di pagina reagiscono più rapidamente e le interazioni con la pagina da parte del visitatore sono immediate. Eventuali dati aggiuntivi che potrebbero essere necessari vengono denominati in modo asincrono per massimizzare la velocità della pagina.

>[!TIP]
>
>Per informazioni tecniche sulle modalità di funzionamento delle ZPS in AEM, consultate gli articoli:
>* [Guida introduttiva alle app SPA in AEM Utilizzo di React](getting-started-react.md)
>* [Guida introduttiva alle app SPA in AEM Utilizzo di Angular](getting-started-angular.md)

>
>
Per un&#39;occhiata più dettagliata alla progettazione, all&#39;architettura e al flusso di lavoro tecnico dell&#39;editor SPA, consultate l&#39;articolo:
>* [Panoramica](editor-overview.md)dell&#39;editor SPA.


## Esperienza di editing dei contenuti con SPA {#content-editing-experience-with-spa}

Quando si crea un&#39;app SPA per sfruttare l&#39;editor AEM SPA, l&#39;autore del contenuto non nota alcuna differenza quando si modifica e si crea contenuto. È disponibile una funzionalità AEM comune e non sono necessarie modifiche al flusso di lavoro dell’autore.

1. Modificate l&#39;app WKND SPA Project in AEM.

   `http://localhost:4502/editor.html/content/wknd-spa-react/us/en/home.html`

   ![Home del progetto SPA WKND](assets/wknd-home.png)

1. Selezionate un componente di testo e notate che una barra degli strumenti è simile a quella di qualsiasi altro componente. Seleziona **Modifica**.

   ![Seleziona componente testo](assets/wknd-text.png)

1. Modificate il contenuto come normale all’interno AEM e tenete presente che le modifiche sono persistenti.

   ![Modifica testo](assets/wknd-edit-text.png)

1. Usate il Browser risorse per trascinare una nuova immagine in un componente immagine.

   ![Trascinamento di una risorsa immagine](assets/wkdn-drop-image.png)

1. La modifica è persistente.

   ![Immagine persistente](assets/wknd-change-persisted.png)

Sono supportati ulteriori strumenti di authoring, come il trascinamento di componenti aggiuntivi sulla pagina, la ridisposizione dei componenti e la modifica del layout, come in qualsiasi applicazione AEM non SPA.

>[!NOTE]
>
>L’editor SPA non modifica il DOM dell’applicazione. La stessa SPA è responsabile del DOM.
>
>Per vedere come funziona, continuate con la sezione successiva di questo articolo App [SPA e AEM Editor](#spa-apps-and-the-aem-spa-editor)SPA.

## App SPA e AEM SPA Editor {#spa-apps-and-the-aem-spa-editor}

L&#39;esperienza di come uno SPA si comporta per l&#39;utente finale e quindi l&#39;analisi della pagina SPA aiuta a comprendere meglio come un&#39;app SAP funziona con l&#39;editor SPA in AEM.

### Utilizzo di un&#39;applicazione SPA {#using-an-spa-application}

1. Caricate l’applicazione WKND SPA Project sul server di pubblicazione o utilizzando l’opzione **Visualizza come pubblicato** dal menu Informazioni **** pagina nell’editor pagina.

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.html`

   ![Anteprima della pagina principale del progetto SPA WKND](assets/wknd-preview.png)

   Prendete nota della struttura delle pagine, inclusa la navigazione verso pagine figlie, menu e schede articolo.

1. Passa a una pagina figlia utilizzando il menu e verifica che la pagina venga caricata immediatamente senza che sia necessario effettuare un aggiornamento.

   ![Progetto SPA WKND pagina 1](assets/wknd-page1.png)

1. Aprite gli strumenti di sviluppo integrati del browser e monitorate l&#39;attività di rete mentre vi spostate nelle pagine figlie.

   ![Attività di rete](assets/wknd-network-activity.png)

   Il traffico si riduce notevolmente quando si passa da una pagina all&#39;altra nell&#39;app. La pagina non viene ricaricata e vengono richieste solo le nuove immagini.

   L&#39;SPA gestisce i contenuti e l&#39;indirizzamento interamente sul lato client.

Quindi, se la pagina non viene ricaricata durante la navigazione tra le pagine figlie, come viene caricata?

La sezione successiva, [Caricamento di un&#39;applicazione](#loading-a-spa-application)SPA, approfondisce la procedura di caricamento dell&#39;SPA e spiega come è possibile caricare il contenuto in modo sincrono e asincrono.

### Caricamento di un&#39;applicazione SPA {#loading-an-spa-application}

1. Se non è già stato caricato, caricate l’applicazione We.Retail Journal sul server di pubblicazione o utilizzando l’opzione **Visualizza come pubblicato** dal menu Informazioni **** pagina nell’editor pagina.

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.html`

   ![Anteprima progetto SPA WKND](assets/wknd-preview.png)

1. Utilizzate lo strumento incorporato del browser per visualizzare l’origine della pagina.
1. Il contenuto dell&#39;origine è limitato.

   ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8"/>
        <title>WKND SPA React Home Page</title>
   
        <meta name="template" content="spa-page-template"/>
        <meta name="viewport" content="width=device-width, initial-scale=1"/>
   
    <link rel="stylesheet" href="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-base.min.css" type="text/css">
   
    <meta name="theme-color" content="#000000"/>
    <link rel="icon" href="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-react/resources/favicon.ico"/>
    <link rel="apple-touch-icon" href="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-react/resources/logo192.png"/>
    <link rel="manifest" href="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-react/resources/manifest.json"/>
   
    <!-- AEM page model -->
    <meta property="cq:pagemodel_root_url" content="/content/wknd-spa-react/us/en.model.json"/>
    <link href="//fonts.googleapis.com/css?family=Source+Sans+Pro:400,600|Asar&display=swap" rel="stylesheet"/>
    <meta property="cq:datatype" content="JSON"/>
    <meta property="cq:wcmmode" content="edit"/>
   
    <link rel="stylesheet" href="/libs/cq/gui/components/authoring/editors/clientlibs/internal/page.min.css" type="text/css">
    <link rel="stylesheet" href="/etc.clientlibs/wcm/foundation/clientlibs/main.min.css" type="text/css">
    <script type="text/javascript" src="/libs/cq/gui/components/authoring/editors/clientlibs/internal/messaging.min.js"></script>
    <script type="text/javascript" src="/libs/cq/gui/components/authoring/editors/clientlibs/utils.min.js"></script>
    <script type="text/javascript" src="/libs/granite/author/deviceemulator/clientlibs.min.js"></script>
    <script type="text/javascript" src="/libs/cq/gui/components/authoring/editors/clientlibs/internal/page.min.js"></script>
    <script type="text/javascript" src="/etc.clientlibs/wcm/foundation/clientlibs/main.min.js"></script>
    <script type="text/javascript" src="/etc.clientlibs/clientlibs/granite/jquery.min.js"></script>
    <script type="text/javascript" src="/etc.clientlibs/clientlibs/granite/utils.min.js"></script>
    <script type="text/javascript" src="/etc.clientlibs/clientlibs/granite/jquery/granite.min.js"></script>
    <script type="text/javascript" src="/etc.clientlibs/foundation/clientlibs/jquery.min.js"></script>
    <script type="text/javascript" src="/etc.clientlibs/foundation/clientlibs/shared.min.js"></script>
   
    <!--cq{"decorated":false,"type":"cq/cloudconfig/components/scripttags/header","path":"/content/wknd-spa-react/us/en/home/jcr:content/cloudconfig-header","structurePath":"/content/wknd-spa-react/us/en/home/jcr:content/cloudconfig-header","selectors":null,"servlet":"Script /libs/cq/cloudconfig/components/scripttags/header/header.html","totalTime":2,"selfTime":2}-->
   
    <link rel="stylesheet" href="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-react.min.css" type="text/css">
   
    </head>
   
    <body class="page basicpage">
        <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="spa-root"></div>
   
    <script type="text/javascript" src="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-react.min.js"></script>
   
    <script type="text/javascript" src="/etc.clientlibs/core/wcm/components/commons/site/clientlibs/container.min.js"></script>
    <script type="text/javascript" src="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-base.min.js"></script>
   
    <script type="text/javascript" src="/libs/cq/gui/components/authoring/editors/clientlibs/internal/pagemodel/messaging.min.js"></script>
   
    <link rel="stylesheet" href="/etc.clientlibs/wknd-spa-react/clientlibs/clientlib-author.min.css" type="text/css">
   
    <!--cq{"decorated":true,"type":"cq/cloudserviceconfigs/components/servicecomponents","path":"/content/wknd-spa-react/us/en/home/jcr:content/cloudservices","selectors":null,"servlet":"Script /libs/cq/cloudserviceconfigs/components/servicecomponents/servicecomponents.jsp","totalTime":2,"selfTime":2}-->
   
    <!--cq{"decorated":false,"type":"cq/cloudconfig/components/scripttags/footer","path":"/content/wknd-spa-react/us/en/home/jcr:content/cloudconfig-footer","structurePath":"/content/wknd-spa-react/us/en/home/jcr:content/cloudconfig-footer","selectors":null,"servlet":"Script /libs/cq/cloudconfig/components/scripttags/footer/footer.html","totalTime":2,"selfTime":2}-->
   
    </body>
    </html>
    <!--cq{"decorated":false,"type":"wknd-spa-react/components/page","path":"/content/wknd-spa-react/us/en/home/jcr:content","selectors":null,"servlet":"Script /apps/spa-project-core/components/page/page.html","totalTime":39,"selfTime":33}-->
   ```

   La pagina non ha alcun contenuto all’interno del suo corpo. È costituito principalmente da fogli di stile e da una chiamata a vari script come `clientlib-react.min.js`.

   Questi script sono i driver principali di questa applicazione e sono responsabili del rendering di tutto il contenuto.

1. Utilizzate gli strumenti integrati del browser per ispezionare la pagina. Visualizzare il contenuto del DOM completamente caricato.

   ![DOM of WKND SPA Project](assets/wknd-dom.png)

1. Passate alla scheda Rete in Ispettore e ricaricate la pagina.

   Ignorando le richieste di immagini, tenete presente che le risorse principali caricate per la pagina sono la pagina stessa, CSS, il JavaScript React, le sue dipendenze e i dati JSON per la pagina.

   ![Attività di rete del progetto SPA WKND](assets/wknd-network.png)

1. Caricate il file `home.model.json` in una nuova scheda.

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.model.json`

   ![JSON della home page del progetto SPA WKND](assets/wknd-json.png)

   AEM SPA Editor sfrutta [AEM Content Services](/help/assets/content-fragments/content-fragments.md) per distribuire l&#39;intero contenuto della pagina come modello JSON.

   Implementando interfacce specifiche, Sling Models fornisce le informazioni necessarie alla SPA. La consegna dei dati JSON viene delegata verso il basso a ciascun componente (dalla pagina al paragrafo, al componente, ecc.).

   Ciascun componente sceglie le funzioni esposte e di rendering (lato server con HTL o lato client con React o Angular). Questo articolo è incentrato sul rendering lato client con React.

1. Il modello può anche raggruppare le pagine in modo che vengano caricate in modo sincrono, riducendo il numero di ricariche di pagina necessarie.

   Nell&#39;esempio di We.Retail Journal, le pagine `home`, `page-1`, `page-2`e `page-3` le pagine vengono caricate in modo sincrono, poiché i visitatori di solito visitano tutte queste pagine.

   Questo comportamento non è obbligatorio ed è completamente definibile.

   ![Raggruppamento di elementi del progetto SPA WKND](assets/wknd-pages.png)

1. Per visualizzare questa differenza di comportamento, ricaricare la `home` pagina e cancellare l&#39;attività di rete della finestra di ispezione. Andate `page-1` nel menu della pagina e vedete che l&#39;unica attività di rete è una richiesta per l&#39;immagine di `page-1`. `page-1` non deve essere caricato.

   ![WKND SPA Project page-1 attività di rete](assets/wknd-page1-network.png)

### Interazione con l&#39;editor SPA {#interaction-with-the-spa-editor}

Utilizzando l&#39;applicazione di esempio WKND SPA Project, è chiaro come l&#39;app si comporta e viene caricata quando viene pubblicata, sfruttando i servizi di contenuto per la distribuzione di contenuto JSON e il caricamento asincrono delle risorse.

Inoltre, per l&#39;autore dei contenuti, la creazione di contenuti tramite un editor SPA è semplice all&#39;interno AEM.

Nella sezione seguente verrà illustrato il contratto che consente all&#39;editor SPA di collegare componenti all&#39;interno dell&#39;SPA per AEM componenti e ottenere questa esperienza di editing senza problemi.

1. Caricate l&#39;applicazione WKND SPA Project nell&#39;editor e passate alla modalità **Anteprima** .

   `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`

1. Utilizzando gli strumenti di sviluppo incorporati del browser, controllate il contenuto della pagina. Con lo strumento selezione, selezionate un componente modificabile sulla pagina e visualizzate il dettaglio dell’elemento.

   Il componente ha un nuovo attributo dati `data-cq-data-path`.

   ![Analisi degli elementi del progetto SPA WKND](assets/wknd-inspector.png)

   Esempio

   `data-cq-data-path="/content/wknd-spa-react/us/en/home/jcr:content/root/responsivegrid/text`

   Questo percorso consente il recupero e l&#39;associazione dell&#39;oggetto di configurazione del contesto di modifica di ciascun componente.

   Si tratta dell’unico attributo di markup richiesto all’editor per riconoscere questo componente come modificabile all’interno dell’area di protezione speciale. In base a questo attributo, l&#39;editor SPA determinerà quale configurazione modificabile è associata al componente, in modo che il frame, la barra degli strumenti e così via siano corretti. è caricato.

   Alcuni nomi di classe specifici vengono aggiunti anche per i segnaposto di marketing e per la funzionalità di trascinamento della risorsa.

   >[!NOTE]
   >
   >Questo comportamento è diverso dalle pagine sottoposte a rendering sul lato server in AEM, dove è inserito un `cq` elemento per ciascun componente modificabile.
   >
   >Questo approccio nell&#39;editor SPA elimina la necessità di inserire elementi personalizzati, basandosi solo su un attributo di dati aggiuntivo, semplificando il markup per lo sviluppatore frontend.

## Passaggi successivi {#next-steps}

Ora che avete compreso l&#39;esperienza di editing SPA in AEM e come l&#39;SPA si collega all&#39;editor SPA, scoprite meglio come è stata creata una SPA.

* [Guida introduttiva alle app SPA in AEM con React](getting-started-react.md) mostra come una piattaforma SPA di base sia stata creata per lavorare con l&#39;editor SPA in AEM utilizzando React
* [Guida introduttiva alle app SPA in AEM con Angular](getting-started-angular.md) mostra come una piattaforma SPA di base sia progettata per lavorare con l&#39;editor SPA in AEM con Angular
* [SPA Editor Overview](editor-overview.md) approfondisce il modello di comunicazione tra AEM e SPA.
* [Lo sviluppo di SPA per AEM](developing.md) descrive come coinvolgere gli sviluppatori front-end nello sviluppo di una SPA per AEM e come le SPA interagiscono con AEM architettura.
