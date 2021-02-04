---
title: Introduzione SPA e Procedura dettagliata
description: Questo articolo introduce i concetti di SPA e illustra come utilizzare un'applicazione SPA di base per la creazione, mostrando come si collega all'Editor SPA sottostante.
translation-type: tm+mt
source-git-commit: e1db93e8f4cf8ef881b274879e800c9993753a66
workflow-type: tm+mt
source-wordcount: '1986'
ht-degree: 0%

---


# Introduzione SPA e Procedura dettagliata {#spa-introduction}

Le applicazioni a pagina singola (SPA) possono offrire esperienze coinvolgenti agli utenti di siti Web. Gli sviluppatori desiderano essere in grado di creare siti utilizzando SPA framework e gli autori desiderano modificare i contenuti all&#39;interno di AEM per un sito creato utilizzando tali framework.

SPA Editor offre una soluzione completa per SPA di supporto in AEM. Questo articolo descrive l’utilizzo di un’applicazione SPA di base per l’authoring e mostra come si collega all’editor SPA AEM sottostante.

## Introduzione {#introduction}

### Articolo Obiettivo {#article-objective}

In questo articolo vengono introdotti i concetti di base di SPA prima di guidare il lettore attraverso una procedura dettagliata dell&#39;editor SPA, utilizzando una semplice applicazione SPA per illustrare la modifica di base dei contenuti. Viene quindi descritto come creare la pagina e come l’applicazione SPA si collega e interagisce con l’editor SPA AEM.

L&#39;obiettivo di questa introduzione e di questa procedura dettagliata è dimostrare a uno sviluppatore AEM perché SPA rilevanti, come funzionano in generale, come un SPA viene gestito dall&#39;Editor SPA AEM e come è diverso da un&#39;applicazione AEM standard.

La procedura dettagliata si basa sulla funzionalità standard AEM e sull&#39;app di esempio WKND SPA Project. Per seguire, [scaricare e installare l&#39;app di progetto WKND SPA di esempio da GitHub qui.](https://github.com/adobe/aem-guides-wknd-spa)

>[!CAUTION]
>
>Questo documento utilizza l&#39; [app progetto WKND SPA](https://github.com/adobe/aem-guides-wknd-spa) solo a scopo dimostrativo. Non deve essere utilizzato per nessun progetto.

>[!TIP]
>
>Qualsiasi progetto AEM deve sfruttare il [AEM Project Archetype](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/archetype/overview.html), che supporta SPA progetti utilizzando React o Angular e sfrutta l&#39;SDK SPA.

### Cos&#39;è un SPA? {#what-is-a-spa}

Un’applicazione a pagina singola (SPA) è diversa da una pagina tradizionale in quanto viene sottoposta a rendering sul lato client ed è principalmente guidata da Javascript, basandosi sulle chiamate Ajax per caricare i dati e aggiornare dinamicamente la pagina. La maggior parte o tutto il contenuto viene recuperato una volta in un singolo caricamento di pagina con risorse aggiuntive caricate in modo asincrono in base alle esigenze, in base all&#39;interazione dell&#39;utente con la pagina.

Questo riduce la necessità di aggiornare le pagine e offre all&#39;utente un&#39;esperienza semplice, rapida e più simile a un&#39;esperienza app nativa.

AEM SPA Editor consente agli sviluppatori front-end di creare SPA che possono essere integrati in un sito AEM, consentendo agli autori dei contenuti di modificare i contenuti SPA con la stessa facilità con cui si trovano altri contenuti AEM.

### Perché un SPA? {#why-a-spa}

Essendo più veloce, fluido e simile a un&#39;applicazione nativa, un SPA diventa un&#39;esperienza molto interessante non solo per il visitatore della pagina Web, ma anche per gli esperti di marketing e gli sviluppatori a causa della natura del funzionamento SPA.

![SPA](assets/spa-benefits.png)

#### Visitatori {#visitors}

* I visitatori desiderano esperienze simili a quelle native quando interagiscono con i contenuti.
* Esistono dati chiari che più veloce sarà una pagina, più probabile sarà una conversione.

#### Marketing {#marketers}

* Gli esperti di marketing desiderano offrire esperienze ricche e native per consentire ai visitatori di interagire pienamente con i contenuti.
* La personalizzazione può rendere queste esperienze ancora più coinvolgenti.

#### Sviluppatori {#developers}

* Gli sviluppatori desiderano una netta separazione tra contenuti e presentazioni.
* La separazione pulita rende il sistema più estensibile e consente uno sviluppo front-end indipendente.

### Come funziona un SPA? {#how-does-a-spa-work}

L&#39;idea principale alla base di un SPA è che le chiamate a un server e le dipendenze vengono ridotte al fine di ridurre i ritardi causati dalla latenza del server, in modo che il SPA si avvicini alla reattività di un&#39;applicazione nativa.

In una pagina Web sequenziale tradizionale, vengono caricati solo i dati necessari per la pagina immediata. Questo significa che quando il visitatore si sposta in un’altra pagina, il server viene chiamato per le risorse aggiuntive. Potrebbero essere necessarie chiamate aggiuntive quando il visitatore interagisce con gli elementi sulla pagina. Queste chiamate multiple possono dare un senso di ritardo o ritardo, in quanto la pagina deve essere in grado di soddisfare le richieste del visitatore.

![Esperienze sequenziali e fluide](assets/spa-sequential-vs-fluid.png)

Per un&#39;esperienza più fluida, che si avvicina alle aspettative di un visitatore dalle app native per dispositivi mobili, un SPA carica tutti i dati necessari per il visitatore al primo caricamento. Anche se inizialmente l&#39;operazione potrebbe richiedere un po&#39; più di tempo, elimina la necessità di ulteriori chiamate server.

Rendering sul lato client, gli elementi di pagina reagiscono più rapidamente e le interazioni con la pagina da parte del visitatore sono immediate. Eventuali dati aggiuntivi che potrebbero essere necessari vengono denominati in modo asincrono per massimizzare la velocità della pagina.

>[!TIP]
>
>Per informazioni tecniche sul funzionamento SPA in AEM, consultate gli articoli:
>* [Guida introduttiva alle SPA in AEM Utilizzo di React](getting-started-react.md)
>* [Guida introduttiva alle SPA in AEM Utilizzo di Angular](getting-started-angular.md)

>
>
Per informazioni più dettagliate sulla progettazione, l’architettura e il flusso di lavoro tecnico dell’editor SPA, consultate l’articolo:
>* [Panoramica](editor-overview.md) dell’editor SPA.


## Esperienza di modifica dei contenuti con SPA {#content-editing-experience-with-spa}

Quando un SPA è creato per sfruttare l&#39;editor SPA AEM, l&#39;autore del contenuto non nota alcuna differenza quando si modifica e si crea contenuto. È disponibile una funzionalità AEM comune e non sono necessarie modifiche al flusso di lavoro dell’autore.

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
>L&#39;Editor SPA non modifica il DOM dell&#39;applicazione. Il SPA stesso è responsabile del DOM.
>
>Per vedere come funziona, andate alla sezione successiva di questo articolo [SPA App e all&#39;editor SPA AEM](#spa-apps-and-the-aem-spa-editor).

## SPA App e l&#39;editor SPA AEM {#spa-apps-and-the-aem-spa-editor}

L&#39;esperienza di come un SPA si comporta per l&#39;utente finale e quindi l&#39;analisi della pagina SPA aiuta a comprendere meglio come un&#39;app SAP funziona con l&#39;Editor SPA in AEM.

### Utilizzo di un&#39;applicazione SPA {#using-an-spa-application}

1. Caricate l&#39;applicazione WKND SPA Project sul server di pubblicazione o utilizzando l&#39;opzione **Visualizza come pubblicato** dal menu **Informazioni pagina** nell&#39;editor pagina.

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.html`

   ![Anteprima della pagina principale del progetto SPA WKND](assets/wknd-preview.png)

   Prendete nota della struttura delle pagine, inclusa la navigazione verso pagine figlie, menu e schede articolo.

1. Passa a una pagina figlia utilizzando il menu e verifica che la pagina venga caricata immediatamente senza che sia necessario effettuare un aggiornamento.

   ![WKND SPA Project pagina 1](assets/wknd-page1.png)

1. Aprite gli strumenti di sviluppo integrati del browser e monitorate l&#39;attività di rete mentre vi spostate nelle pagine figlie.

   ![Attività di rete](assets/wknd-network-activity.png)

   Il traffico si riduce notevolmente quando si passa da una pagina all&#39;altra nell&#39;app. La pagina non viene ricaricata e vengono richieste solo le nuove immagini.

   Il SPA gestisce il contenuto e il routing interamente sul lato client.

Quindi, se la pagina non viene ricaricata durante la navigazione tra le pagine figlie, come viene caricata?

La sezione successiva, [Caricamento di un&#39;applicazione SPA](#loading-a-spa-application), approfondisce la procedura di caricamento del SPA e spiega come caricare il contenuto in modo sincrono e asincrono.

### Caricamento di un&#39;applicazione SPA {#loading-a-spa-application}

1. Se non è già stato caricato, caricate l&#39;app WKND SPA Project sul server di pubblicazione o utilizzando l&#39;opzione **Visualizza come pubblicato** dal menu **Informazioni pagina** nell&#39;editor pagina.

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.html`

   ![Anteprima progetto WKND SPA](assets/wknd-preview.png)

1. Utilizzate lo strumento incorporato del browser per visualizzare l’origine della pagina.
1. Il contenuto dell&#39;origine è limitato.
   * La pagina non ha alcun contenuto all’interno del suo corpo. È costituito principalmente da fogli di stile e da una chiamata a vari script come `clientlib-react.min.js`.
   * Questi script sono i driver principali di questa applicazione e sono responsabili del rendering di tutto il contenuto.

1. Utilizzate gli strumenti integrati del browser per ispezionare la pagina. Visualizzare il contenuto del DOM completamente caricato.

   ![DOM of WKND SPA Project](assets/wknd-dom.png)

1. Passate alla scheda Rete in Ispettore e ricaricate la pagina.

   Ignorando le richieste di immagini, tenete presente che le risorse principali caricate per la pagina sono la pagina stessa, CSS, il JavaScript React, le sue dipendenze e i dati JSON per la pagina.

   ![WKND SPA Attività di rete del progetto](assets/wknd-network.png)

1. Caricate la `home.model.json` in una nuova scheda.

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.model.json`

   ![JSON della home page del progetto WKND SPA](assets/wknd-json.png)

   L&#39;editor SPA AEM utilizza [AEM Content Services](/help/assets/content-fragments/content-fragments.md) per distribuire l&#39;intero contenuto della pagina come modello JSON.

   Implementando interfacce specifiche, Sling Models fornisce le informazioni necessarie al SPA. La consegna dei dati JSON viene delegata verso il basso a ciascun componente (dalla pagina al paragrafo, al componente, ecc.).

   Ciascun componente sceglie le funzioni esposte e di rendering (lato server con HTL o lato client con React o Angular). Questo articolo è incentrato sul rendering lato client con React.

1. Il modello può anche raggruppare le pagine in modo che vengano caricate in modo sincrono, riducendo il numero di ricariche di pagina necessarie.

   Nell&#39;esempio dell&#39;app progetto WKND SPA, le pagine `home`, `page-1`, `page-2` e `page-3` vengono caricate in modo sincrono, dal momento che i visitatori visitano generalmente tutte queste pagine.

   Questo comportamento non è obbligatorio ed è completamente definibile.

   ![WKND SPA Raggruppamento di elementi del progetto](assets/wknd-pages.png)

1. Per visualizzare questa differenza di comportamento, ricaricare la pagina `home` e cancellare l&#39;attività di rete della finestra di ispezione. Andate a `page-1` nel menu della pagina e vedete che l&#39;unica attività di rete è una richiesta per l&#39;immagine di `page-1`. `page-1` non deve essere caricato.

   ![WKND SPA Project page-1 attività di rete](assets/wknd-page1-network.png)

### Interazione con l&#39;editor SPA {#interaction-with-the-spa-editor}

Utilizzando l&#39;applicazione di esempio WKND SPA Project, è chiaro il funzionamento dell&#39;app e come viene caricata quando viene pubblicata, sfruttando i servizi di contenuto per la distribuzione di contenuto JSON e il caricamento asincrono delle risorse.

Inoltre, per l&#39;autore del contenuto, la creazione di contenuto tramite un editor SPA è perfettamente all&#39;interno di AEM.

Nella sezione seguente verrà illustrato il contratto che consente all’editor SPA di correlare i componenti all’interno del SPA a AEM componenti e di ottenere questa esperienza di modifica senza soluzione di continuità.

1. Caricate l&#39;applicazione WKND SPA Project nell&#39;editor e passate alla modalità **Preview**.

   `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`

1. Utilizzando gli strumenti di sviluppo incorporati del browser, controllate il contenuto della pagina. Con lo strumento selezione, selezionate un componente modificabile sulla pagina e visualizzate il dettaglio dell’elemento.

   Il componente ha un nuovo attributo di dati `data-cq-data-path`.

   ![Analisi degli elementi del progetto WKND SPA](assets/wknd-inspector.png)

   Esempio

   `data-cq-data-path="/content/wknd-spa-react/us/en/home/jcr:content/root/responsivegrid/text`

   Questo percorso consente il recupero e l&#39;associazione dell&#39;oggetto di configurazione del contesto di modifica di ciascun componente.

   Questo è l&#39;unico attributo di markup richiesto all&#39;editor per riconoscere questo come componente modificabile all&#39;interno del SPA. In base a questo attributo, l’Editor SPA determinerà quale configurazione modificabile è associata al componente, in modo che il frame, la barra degli strumenti e così via siano corretti. è caricato.

   Alcuni nomi di classe specifici vengono aggiunti anche per i segnaposto di marketing e per la funzionalità di trascinamento della risorsa.

   >[!NOTE]
   >
   >Questo comportamento è diverso dalle pagine sottoposte a rendering sul lato server in AEM, dove è inserito un elemento `cq` per ciascun componente modificabile.
   >
   >Questo approccio nell&#39;Editor SPA elimina la necessità di inserire elementi personalizzati, basandosi solo su un attributo di dati aggiuntivo, semplificando il markup per lo sviluppatore frontend.

## Cuffia e testa senza testa in AEM {#headful-headless}

SPA può essere abilitata con livelli flessibili di integrazione all&#39;interno AEM, compresi SPA sviluppati e mantenuti al di fuori di AEM. Inoltre, SPA può essere sfruttato all&#39;interno di AEM e utilizzare AEM per distribuire contenuti ad endpoint aggiuntivi senza problemi.

>[!TIP]
>
>Per ulteriori informazioni, vedere il documento [Cuffia e Senza testa in AEM](/help/implementing/developing/headful-headless.md).

## Passaggi successivi {#next-steps}

Ora che avete compreso l&#39;esperienza di modifica SPA in AEM e come un SPA si collega all&#39;Editor SPA, approfondisci la conoscenza di come un SPA è costruito.

* [Guida introduttiva alle SPA in AEM con ](getting-started-react.md) Reactmostra come è stato creato un SPA di base per lavorare con l’Editor SPA in AEM con React
* [Guida introduttiva alle SPA in AEM con ](getting-started-angular.md) Angularmostra come è stato creato un SPA di base per lavorare con SPA Editor in AEM con Angular
* [SPA Editor ](editor-overview.md) Overviewfinder approfondisce il modello di comunicazione tra AEM e SPA.
* [Lo sviluppo di SPA per ](developing.md) AEM descrive come coinvolgere gli sviluppatori front-end nello sviluppo di un SPA per AEM e come SPA interagire con AEM architettura.
