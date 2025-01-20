---
Title: Authoring a Form
Description: This article provides information on various form authoring platforms, including the Universal Editor, document-based authoring, and Adaptive Forms editors (Core Components and Foundation Components).
Keywords: Universal Editor for WYSIWYG authoring, document-based authoring, Adaptive Forms editors, Adaptive Forms editors for Core Components authoring, Adaptive Forms editors for Foundation Components authoring
feature: Edge Delivery Services
Role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: bdc0e51a8b16df432f1f1aeabed11135fb8c8e0c
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 0%

---


# Creazione di un modulo

Adobe Experience Manager offre e supporta più editor per la creazione di un modulo. Puoi utilizzare:
* Editor universale (per l’authoring WYSIWYG)
* Microsoft Excel o Google Sheets (noto come authoring basato su documento)
* Editor Forms adattivi (per l’authoring basato su componenti core o di base)

**[immagine da aggiungere]**

## Editor universale (per l’authoring WYSIWYG)

Universal Editor è un editor visivo versatile che offre una funzionalità WYSIWYG (What-you-see-is-what-you-get) per garantire un’esperienza di creazione dei moduli intuitiva. Si consiglia di utilizzare l’Editor universale durante la creazione di nuovi moduli, in quanto offre un design moderno e intuitivo e una comoda interfaccia con metodo di trascinamento della selezione.

Per creare i moduli tramite l’Editor universale, vengono utilizzati i modelli di Edge Delivery Services disponibili nell’ambiente AEM. Questi moduli ereditano il loro aspetto dalle configurazioni nell’archivio GitHub dei Edge Delivery Services. [È stata stabilita una connessione tra l&#39;ambiente AEM e l&#39;archivio GitHub dei Edge Delivery Services](/help/edge/docs/forms/publishing-forms.md) per consentire la pubblicazione di questi moduli sui Edge Delivery Services.

Per i passaggi dettagliati su come eseguire l&#39;authoring utilizzando l&#39;editor universale, fare riferimento all&#39;articolo [Authoring dei contenuti con l&#39;editor universale](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/universal-editor/authoring).

## Microsoft Excel o Google Sheets (noto come authoring basato su documento)

Puoi creare i moduli utilizzando l’authoring basato su documenti con file Microsoft Excel o Google Sheets, che consentono di sfruttare i solidi ecosistemi e API di Google Sheets, Microsoft Excel e Microsoft SharePoint. Questo approccio è particolarmente utile per la creazione di moduli semplici senza servizi di invio avanzati.

Per iniziare a creare un modulo utilizzando Microsoft Excel o Google Sheets, [imposta un progetto AEM utilizzando AEM Forms boilerplate](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) e clona l&#39;archivio GitHub corrispondente nel computer locale. AEM Forms Edge Delivery fornisce una funzione chiamata Blocco di Forms adattivo, che semplifica il processo di creazione dei moduli per l’acquisizione e l’archiviazione dei dati. Per informazioni su come creare e pubblicare moduli tramite il blocco Forms adattivo sui Edge Delivery Services, consulta [Creazione di un modulo](/help/edge/docs/forms/create-forms.md).

## Editor Forms adattivi (per l’authoring basato su componenti core o di base)

Puoi creare moduli coinvolgenti, reattivi e dinamici. L’editor di moduli adattivi fornisce una procedura guidata intuitiva che consente di creare rapidamente Forms adattivo. La procedura guidata per i moduli semplifica la navigazione tra schede, consentendo di selezionare modelli preconfigurati per componenti di base o principali, temi, modelli di dati e opzioni di invio per creare un modulo in modo efficiente.

[La creazione di moduli con i componenti core](/help/forms/creating-adaptive-form-core-components.md) consente di sfruttare i componenti di acquisizione dati standardizzati che possono essere personalizzati, riducendo i tempi di sviluppo e i costi di manutenzione per le esperienze di registrazione digitale. Questi moduli possono essere pubblicati utilizzando il blocco Forms adattivo sui Edge Delivery Services o tramite l’istanza Publish dell’AEM.

[Per la creazione di moduli con i componenti di Foundation](/help/forms/create-an-adaptive-form.md) vengono utilizzati componenti di acquisizione dati classici. Questi moduli possono essere pubblicati solo utilizzando l’istanza Publish dell’AEM.

Puoi anche pubblicare i moduli creati con Editor Forms adattivi sui Edge Delivery Services stabilendo [connessione tra l&#39;ambiente AEM e l&#39;archivio GitHub dei Edge Delivery Services](/help/edge/docs/forms/publishing-forms.md).

## Come scegliere tra vari tipi di creazione di moduli?

La tabella seguente illustra le funzioni e i casi d’uso per ogni editor di authoring, per aiutarti a scegliere quello giusto in base ai tuoi requisiti e alle tue esigenze di invio dei moduli.

| **Editor creazione moduli** | **Approccio chiave** | **Caratteristiche** | **Metodo di pubblicazione** | **Casi d&#39;uso** |
|--------|-----------|-------|-------|------------------------------------------------|
| **Authoring basato su documenti** | Sfrutta strumenti familiari come Google Docs e Microsoft Office per la creazione di moduli. | Forms è progettato utilizzando fogli di calcolo, con dati inviati direttamente a fogli Google o fogli Microsoft Excel. </br> </br> Questi moduli sono più veloci da creare e distribuire. Per sviluppare componenti e stili personalizzati per questi moduli non è necessaria alcuna conoscenza preventiva dell’AEM. | Questi moduli sono pubblicati su Edge Delivery Services e hanno un punteggio Google Lighthouse molto alto. </br> </br> Il punteggio elevato consente un rendering più rapido e SEO migliore. | Questi moduli sono ideali per la creazione rapida di prototipi o per moduli di base in cui non sono necessari servizi di invio avanzati. </br> </br> Questi moduli sono particolarmente adatti per sondaggi, registrazioni o moduli di feedback che richiedono l&#39;archiviazione dei dati nei fogli di calcolo. Questi moduli vengono pubblicati sui servizi di Edge Delivery |
| **Editor universale** </br> </br> Se si sta creando un nuovo modulo, utilizzare Editor universale per creare i moduli. | Offre un’interfaccia WYSIWYG per la creazione intuitiva dei moduli. | I Forms sono progettati tramite un&#39;interfaccia di trascinamento intuitiva. </br> </br> Questi moduli prendono in prestito aspetto dall&#39;archivio GitHub dei Edge Delivery Services configurati per il modulo corrispondente. | Questi moduli sono pubblicati su Edge Delivery Services e hanno un punteggio Google Lighthouse molto alto. </br> </br> Il punteggio elevato consente un rendering più rapido e SEO migliore. | Questi moduli sono ideali per la creazione di moduli per pagine e siti del servizio Edge Delivery. Questi scenari di moduli coinvolgono moduli complessi, flussi di lavoro complessi, azioni personalizzate o integrazioni con sistemi esterni |
| **Editor Forms adattivi** | Fornisce un approccio guidato per avviare rapidamente l’authoring dei moduli utilizzando modelli, stili e campi predefiniti. | Utilizza questi editor per creare moduli basati su Componenti core o moduli basati su Componenti base. | Questi moduli possono essere pubblicati su Edge Delivery Services o tramite istanze Publish AEM. | Utilizza questi editor per creare moduli basati su Componenti core o moduli basati su Componenti base. Ideale per scenari che richiedono moduli complessi, flussi di lavoro complessi, azioni personalizzate o integrazioni con sistemi esterni. |


>[!NOTE]
>
>
> Se nell’editor universale mancano funzioni precedentemente disponibili nell’editor di Forms adattivo, puoi richiederle inviando un’e-mail a mailto:aem-forms-ea@adobe.com utilizzando il tuo indirizzo e-mail ufficiale.

## Articolo correlato

* [Authoring basato su documenti con Microsoft Excel o Google Sheets](/help/edge/docs/forms/create-forms.md)
* [Editor universale per l&#39;authoring di WYSIWYG](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)
* [Creare un modulo adattivo (componenti di base)](/help/forms/creating-adaptive-form.md)
* [Creare un modulo adattivo (componenti core)](/help/forms/create-an-adaptive-form.md)

## Consulta anche

{{see-more-forms-eds}}