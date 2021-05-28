---
title: Introduzione SPA e Procedura dettagliata
description: Questo articolo introduce i concetti di un SPA e spiega come utilizzare un'applicazione SPA di base per l'authoring, mostrando come si relaziona con l'Editor SPA sottostante.
exl-id: 8dad48d5-fa90-467c-8bec-e4b76e057f80
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1984'
ht-degree: 1%

---

# Introduzione SPA e procedura dettagliata {#spa-introduction}

Le applicazioni a pagina singola (SPA) possono offrire esperienze coinvolgenti agli utenti di siti web. Gli sviluppatori desiderano poter creare siti utilizzando framework SPA e gli autori desiderano modificare facilmente i contenuti all’interno di AEM per un sito creato utilizzando tali framework.

SPA Editor offre una soluzione completa per il supporto dei SPA in AEM. Questo articolo illustra l’utilizzo di un’applicazione di SPA di base per l’authoring e illustra come si relaziona con l’editor di SPA di AEM sottostante.

## Introduzione {#introduction}

### Obiettivo dell&#39;articolo {#article-objective}

Questo articolo introduce i concetti di base di SPA prima di guidare il lettore attraverso una procedura dettagliata dell’editor di SPA utilizzando una semplice applicazione SPA per illustrare le modifiche di base dei contenuti. Viene quindi descritto come creare la pagina e come l’applicazione SPA si relaziona e interagisce con l’editor di SPA AEM.

L&#39;obiettivo di questa introduzione e di questa procedura dettagliata è dimostrare a uno sviluppatore AEM perché SPA sono rilevanti, come funzionano in generale, come un SPA viene gestito dall&#39;editor di SPA AEM e come è diverso da un&#39;applicazione AEM standard.

La procedura dettagliata si basa sulle funzionalità AEM standard e sull’app di esempio WKND SPA Project . Per seguire, [scarica e installa l&#39;app di esempio WKND SPA Project da GitHub qui.](https://github.com/adobe/aem-guides-wknd-spa)

>[!CAUTION]
>
>Questo documento utilizza l&#39; [app di progetto WKND SPA](https://github.com/adobe/aem-guides-wknd-spa) solo a scopo dimostrativo. Non deve essere utilizzato per alcun lavoro di progetto.

>[!TIP]
>
>Qualsiasi progetto AEM deve sfruttare il [AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html), che supporta SPA progetti utilizzando React o Angular e sfrutta l&#39;SDK SPA.

### Cos&#39;è un SPA? {#what-is-a-spa}

Un’applicazione a pagina singola (SPA) differisce da una pagina convenzionale in quanto viene sottoposta a rendering lato client ed è principalmente guidata da Javascript, basandosi sulle chiamate Ajax per caricare i dati e aggiornare dinamicamente la pagina. La maggior parte o tutto il contenuto viene recuperato una volta in un singolo caricamento di pagina con risorse aggiuntive caricate in modo asincrono in base alle esigenze, in base all’interazione dell’utente con la pagina.

Questo riduce la necessità di aggiornare le pagine e presenta all’utente un’esperienza fluida, rapida e più simile a un’esperienza nativa per le app.

L’editor di SPA AEM consente agli sviluppatori front-end di creare SPA che possono essere integrati in un sito AEM, consentendo agli autori di contenuti di modificare il contenuto SPA con la stessa facilità con cui sono presenti altri contenuti AEM.

### Perché un SPA? {#why-a-spa}

Essendo più veloce, fluida e più simile a un&#39;applicazione nativa, un SPA diventa un&#39;esperienza molto attraente non solo per il visitatore della pagina web, ma anche per gli esperti di marketing e gli sviluppatori a causa della natura del funzionamento di SPA.

![SPA](assets/spa-benefits.png)

#### Visitatori {#visitors}

* I visitatori desiderano esperienze di tipo nativo quando interagiscono con i contenuti.
* Ci sono dati chiari che più veloce sarà una pagina, più probabile sarà una conversione.

#### Addetti al marketing {#marketers}

* Gli esperti di marketing desiderano offrire esperienze avanzate e di tipo nativo per invitare i visitatori a interagire pienamente con i contenuti.
* La personalizzazione può rendere queste esperienze ancora più coinvolgenti.

#### Sviluppatori {#developers}

* Gli sviluppatori vogliono una netta separazione tra contenuti e presentazioni.
* La separazione pulita rende il sistema più estensibile e consente uno sviluppo front-end indipendente.

### Come funziona un SPA? {#how-does-a-spa-work}

L&#39;idea principale alla base di un SPA è che le chiamate a e la dipendenza da un server vengono ridotte al fine di ridurre al minimo i ritardi causati dalla latenza del server, in modo che il SPA si avvicini alla reattività di un&#39;applicazione nativa.

In una pagina web tradizionale sequenziale, vengono caricati solo i dati necessari per la pagina immediata. Questo significa che quando il visitatore si sposta su un’altra pagina, il server viene chiamato per le risorse aggiuntive. Potrebbero essere necessarie chiamate aggiuntive mentre il visitatore interagisce con gli elementi della pagina. Queste chiamate multiple possono dare un senso di ritardo o ritardo in quanto la pagina deve soddisfare le richieste del visitatore.

![Esperienze sequenziali e fluide](assets/spa-sequential-vs-fluid.png)

Per un’esperienza più fluida, che si avvicina a ciò che un visitatore si aspetta dalle app native per dispositivi mobili, un SPA carica tutti i dati necessari al visitatore al primo caricamento. Anche se inizialmente l&#39;operazione potrebbe richiedere un po&#39; più di tempo, elimina la necessità di ulteriori chiamate server.

Effettuando il rendering sul lato client, gli elementi di pagina reagiscono più rapidamente e le interazioni con la pagina da parte del visitatore sono immediate. Eventuali dati aggiuntivi che potrebbero essere necessari vengono chiamati in modo asincrono per massimizzare la velocità della pagina.

>[!TIP]
>
>Per informazioni tecniche sul funzionamento SPA in AEM, vedere gli articoli:
>* [Guida introduttiva a SPA in AEM con React](getting-started-react.md)
* [Guida introduttiva a SPA in AEM Utilizzo di Angular](getting-started-angular.md)

Per un’analisi più approfondita della progettazione, dell’architettura e del flusso di lavoro tecnico dell’editor di SPA, consulta l’articolo:
* [Panoramica dell’editor di SPA](editor-overview.md).


## Esperienza di modifica dei contenuti con SPA {#content-editing-experience-with-spa}

Quando viene creata una SPA per sfruttare l’Editor SPA AEM, l’autore del contenuto non nota alcuna differenza durante la modifica e la creazione di contenuti. È disponibile una funzionalità AEM comune e non è necessaria alcuna modifica al flusso di lavoro dell’autore.

1. Modifica l’app WKND SPA Project in AEM.

   `http://localhost:4502/editor.html/content/wknd-spa-react/us/en/home.html`

   ![Pagina principale del progetto SPA WKND](assets/wknd-home.png)

1. Seleziona un componente testo e osserva che la barra degli strumenti è simile a quella di qualsiasi altro componente. Seleziona **Modifica**.

   ![Seleziona componente testo](assets/wknd-text.png)

1. Modifica il contenuto come normale in AEM e osserva che le modifiche sono persistenti.

   ![Modifica testo](assets/wknd-edit-text.png)

1. Utilizza il browser Risorse per trascinare una nuova immagine in un componente immagine.

   ![Eliminazione di una risorsa immagine](assets/wkdn-drop-image.png)

1. La modifica viene mantenuta.

   ![Immagine persistente](assets/wknd-change-persisted.png)

Sono supportati ulteriori strumenti di authoring, come il trascinamento e il rilascio di componenti aggiuntivi sulla pagina, la ridisposizione dei componenti e la modifica del layout, come in qualsiasi applicazione AEM non SPA.

>[!NOTE]
L’Editor SPA non modifica il DOM dell’applicazione. Il SPA stesso è responsabile del DOM.
Per vedere come funziona, continua con la sezione successiva di questo articolo [App SPA e l&#39;editor SPA AEM](#spa-apps-and-the-aem-spa-editor).

## App SPA e editor SPA AEM {#spa-apps-and-the-aem-spa-editor}

L’esperienza di come si comporta un SPA per l’utente finale e quindi l’analisi della pagina di SPA aiuta a comprendere meglio come funziona un’app SAP con l’editor di SPA in AEM.

### Utilizzo di un&#39;applicazione SPA {#using-an-spa-application}

1. Carica l&#39;applicazione WKND SPA Project sul server di pubblicazione o utilizzando l&#39;opzione **Visualizza come pubblicato** dal menu **Informazioni pagina** nell&#39;editor pagina.

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.html`

   ![Anteprima della pagina principale del progetto SPA WKND](assets/wknd-preview.png)

   Osserva la struttura delle pagine, inclusa la navigazione verso pagine figlie, menu e schede articolo.

1. Passa a una pagina figlia utilizzando il menu e controlla che la pagina venga caricata immediatamente senza la necessità di un aggiornamento.

   ![Progetto WKND SPA pagina 1](assets/wknd-page1.png)

1. Apri gli strumenti di sviluppo incorporati del browser e monitora l’attività di rete mentre navighi nelle pagine figlie.

   ![Attività di rete](assets/wknd-network-activity.png)

   C&#39;è molto poco traffico mentre si passa da una pagina all&#39;altra nell&#39;app. La pagina non viene ricaricata e vengono richieste solo le nuove immagini.

   Il SPA gestisce il contenuto e il routing interamente sul lato client.

Quindi, se la pagina non viene ricaricata durante la navigazione tra le pagine figlie, come viene caricata?

La sezione successiva, [Caricamento di un&#39;applicazione SPA](#loading-a-spa-application), approfondisce la procedura di caricamento del SPA e spiega come caricare il contenuto in modo sincrono e asincrono.

### Caricamento di un&#39;applicazione SPA {#loading-a-spa-application}

1. Se non è già stato caricato, carica l&#39;app WKND SPA Project sul server di pubblicazione o utilizzando l&#39;opzione **Visualizza come pubblicato** dal menu **Informazioni pagina** nell&#39;editor pagina.

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.html`

   ![Anteprima progetto SPA WKND](assets/wknd-preview.png)

1. Utilizza lo strumento incorporato del browser per visualizzare l’origine della pagina.
1. Il contenuto della sorgente è limitato.
   * La pagina non ha alcun contenuto all’interno del suo corpo. È composto principalmente da fogli di stile e una chiamata a vari script come `clientlib-react.min.js`.
   * Questi script sono i driver principali di questa applicazione e sono responsabili del rendering di tutti i contenuti.

1. Utilizza gli strumenti incorporati del browser per ispezionare la pagina. Visualizzare il contenuto del DOM completamente caricato.

   ![DOM del progetto di SPA WKND](assets/wknd-dom.png)

1. Passa alla scheda Rete in Ispettore e ricarica la pagina.

   Le richieste di immagini vengono ignorate. Le risorse principali caricate per la pagina sono la pagina stessa, CSS, il JavaScript di React, le sue dipendenze e i dati JSON per la pagina.

   ![Attività di rete del progetto SPA WKND](assets/wknd-network.png)

1. Carica il `home.model.json` in una nuova scheda.

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.model.json`

   ![JSON della pagina principale del progetto SPA WKND](assets/wknd-json.png)

   L’editor di SPA AEM sfrutta [AEM Content Services](/help/assets/content-fragments/content-fragments.md) per distribuire l’intero contenuto della pagina come modello JSON.

   Implementando interfacce specifiche, i modelli Sling forniscono le informazioni necessarie al SPA. La consegna dei dati JSON viene delegata verso il basso a ciascun componente (dalla pagina, al paragrafo, al componente, ecc.).

   Ogni componente sceglie ciò che espone e come viene riprodotto (lato server con HTL o lato client con React o Angular). Questo articolo si concentra sul rendering lato client con React.

1. Il modello può anche raggruppare le pagine in modo che vengano caricate in modo sincrono, riducendo il numero di ricaricamenti di pagina necessari.

   Nell’esempio dell’app di progetto WKND SPA, le pagine `home`, `page-1`, `page-2` e `page-3` vengono caricate in modo sincrono, in quanto i visitatori visitano solitamente tutte le pagine.

   Questo comportamento non è obbligatorio ed è completamente definibile.

   ![Raggruppamento elementi di progetto SPA WKND](assets/wknd-pages.png)

1. Per visualizzare questa differenza di comportamento, ricaricare la pagina `home` e cancellare l&#39;attività di rete del controllo. Passa a `page-1` nel menu della pagina e osserva che l’unica attività di rete è una richiesta per l’immagine di `page-1`. `page-1` non è necessario caricare.

   ![WKND SPA Project page-1 attività di rete](assets/wknd-page1-network.png)

### Interazione con l&#39;editor SPA {#interaction-with-the-spa-editor}

Utilizzando l’applicazione di esempio WKND SPA Project , è chiaro come l’app si comporta e viene caricata quando viene pubblicata, sfruttando i servizi di contenuto per la distribuzione di contenuti JSON e il caricamento asincrono delle risorse.

Inoltre, per l’autore dei contenuti, la creazione di contenuti tramite un editor di SPA è semplice all’interno di AEM.

Nella sezione seguente esploreremo il contratto che consente all’editor di SPA di correlare i componenti all’interno del SPA a componenti AEM e ottenere questa esperienza di modifica senza soluzione di continuità.

1. Carica l&#39;applicazione WKND SPA Project nell&#39;editor e passa alla modalità **Preview** .

   `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`

1. Utilizzando gli strumenti di sviluppo incorporati del browser, esamina il contenuto della pagina. Con lo strumento di selezione, seleziona un componente modificabile nella pagina e visualizza i dettagli dell’elemento.

   Il componente ha un nuovo attributo di dati `data-cq-data-path`.

   ![Ispezione degli elementi del progetto WKND SPA](assets/wknd-inspector.png)

   Esempio

   `data-cq-data-path="/content/wknd-spa-react/us/en/home/jcr:content/root/responsivegrid/text`

   Questo percorso consente il recupero e l&#39;associazione dell&#39;oggetto di configurazione del contesto di modifica di ciascun componente.

   Questo è l’unico attributo di markup necessario affinché l’editor riconosca questo come componente modificabile all’interno del SPA. In base a questo attributo, l’Editor SPA determinerà quale configurazione modificabile è associata al componente, in modo che la cornice, la barra degli strumenti e così via corretta. è caricato.

   Vengono inoltre aggiunti alcuni nomi di classe specifici per i segnaposto di contrassegno e per la funzionalità di trascinamento della risorsa.

   >[!NOTE]
   Questo comportamento è diverso dalle pagine di rendering lato server in AEM, dove è inserito un elemento `cq` per ciascun componente modificabile.
   Questo approccio nell’editor di SPA elimina la necessità di inserire elementi personalizzati, basandosi solo su un attributo di dati aggiuntivo, semplificando il markup per lo sviluppatore front-end.

## Cefalea e senza testa in AEM {#headful-headless}

SPA può essere abilitato con livelli flessibili di integrazione all&#39;interno di AEM, compresi SPA sviluppati e mantenuti al di fuori di AEM. Inoltre, SPA può essere sfruttato all’interno di AEM, utilizzando anche AEM per fornire contenuti ad endpoint aggiuntivi senza problemi.

>[!TIP]
Per ulteriori informazioni, consulta il documento [Headful and Headless in AEM](/help/implementing/developing/headful-headless.md) .

## Passaggi successivi {#next-steps}

Ora che comprendi l’esperienza di modifica SPA in AEM e come un SPA si relaziona con l’Editor SPA, approfondisci più approfonditamente il modo in cui viene generato un SPA.

* [La Guida introduttiva a SPA in AEM con ](getting-started-react.md) Reactmostra come viene creato un SPA di base per lavorare con l’Editor SPA in AEM utilizzando React
* [La Guida introduttiva a SPA in AEM utilizzo di ](getting-started-angular.md) Angularmostra come viene creato un SPA di base per lavorare con l’Editor SPA in AEM utilizzando Angular
* [SPA Editor ](editor-overview.md) Overview approfondisce il modello di comunicazione tra AEM e SPA.
* [Lo sviluppo di SPA per ](developing.md) AEM descrive come coinvolgere gli sviluppatori front-end nello sviluppo di un SPA per AEM e come SPA interagire con l’architettura AEM.
