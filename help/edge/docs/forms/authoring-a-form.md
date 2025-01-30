---
Title: Authoring a Form
Description: This article provides information on various form authoring platforms, including the Universal Editor, document-based authoring, and Adaptive Forms editors (Core Components and Foundation Components).
Keywords: Universal Editor for WYSIWYG authoring, document-based authoring, Adaptive Forms editors, Adaptive Forms editors for Core Components authoring, Adaptive Forms editors for Foundation Components authoring
feature: Edge Delivery Services
Role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: bdc0e51a8b16df432f1f1aeabed11135fb8c8e0c
workflow-type: ht
source-wordcount: '877'
ht-degree: 100%

---


# Creazione di un modulo

Adobe Experience Manager offre e supporta più editor per la creazione di un modulo. Puoi utilizzare:
* Editor universale (per l’authoring WYSIWYG)
* Microsoft Excel o Fogli Google (noto come authoring basato su documento)
* Editor di moduli adattivi (per l’authoring basato su componenti core o di base)

**[immagine da aggiungere]**

## Editor universale (per l’authoring WYSIWYG)

L’editor universale è un editor visivo versatile che offre una funzionalità what-you-see-is-what-you-get (WYSIWYG) per garantire un’esperienza di creazione dei moduli intuitiva. Si consiglia di utilizzare l’editor universale durante la creazione di nuovi moduli, in quanto offre un design moderno e intuitivo e una comoda interfaccia tramite trascinamento.

Per creare i moduli tramite l’Editor universale, vengono utilizzati i modelli di Edge Delivery Services disponibili nell’ambiente AEM. Questi moduli ereditano l’aspetto dalle configurazioni nell’archivio GitHub di Edge Delivery Services. È stata stabilita [una connessione tra l’ambiente AEM e l’archivio GitHub di Edge Delivery Services](/help/edge/docs/forms/publishing-forms.md) per consentire la pubblicazione di questi moduli su Edge Delivery Services.

Per informazioni dettagliate su come effettuare l’authoring con l’Editor universale, consulta l’articolo [Authoring dei contenuti con l’Editor universale.](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/sites/authoring/universal-editor/authoring)

## Microsoft Excel o Fogli Google (noto come authoring basato su documento)

Puoi creare i moduli utilizzando l’authoring basato su documenti con file Microsoft Excel o Fogli Google, che consentono di sfruttare i solidi ecosistemi e le API di Fogli Google, Microsoft Excel e Microsoft SharePoint. Questo approccio è particolarmente utile per la creazione di moduli semplici senza servizi di invio avanzati.

Per iniziare a creare un modulo utilizzando Microsoft Excel o Fogli Google, [imposta un progetto AEM utilizzando AEM Forms standard](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) e clona l’’archivio GitHub corrispondente nel computer locale. AEM Forms Edge Delivery fornisce una funzione chiamata Blocco di moduli adattivi, che semplifica il processo di creazione dei moduli per l’acquisizione e l’archiviazione dei dati. Per informazioni su come creare e pubblicare moduli tramite il blocco di moduli adattivi su Edge Delivery Services, consulta [Creare un modulo](/help/edge/docs/forms/create-forms.md).

## Editor di moduli adattivi (per l’authoring basato su componenti core o di base)

Puoi creare moduli coinvolgenti, reattivi e dinamici. L’editor di moduli adattivi fornisce una procedura guidata intuitiva che consente di creare rapidamente moduli adattivi. La procedura guidata per i moduli semplifica la navigazione tra schede, consentendo di selezionare modelli preconfigurati per componenti core o di base, temi, modelli di dati e opzioni di invio per creare un modulo in modo efficiente.

[La creazione di moduli con i componenti core](/help/forms/creating-adaptive-form-core-components.md) consente di sfruttare i componenti di acquisizione dei dati standardizzati che possono essere personalizzati, riducendo i tempi di sviluppo e i costi di manutenzione per le esperienze di registrazione digitale. Questi moduli possono essere pubblicati utilizzando il Blocco dei moduli adattivi su Edge Delivery Services o tramite l’istanza di pubblicazione di AEM.

[La creazione di moduli con i componenti base](/help/forms/create-an-adaptive-form.md) utilizza componenti di acquisizione di dati classici. Questi moduli possono essere pubblicati solo utilizzando l’istanza di pubblicazione di AEM.

Puoi anche pubblicare i moduli creati con l’editor di moduli adattivi su Edge Delivery Services stabilendo una [connessione tra l’ambiente AEM e l’archivio GitHub di Edge Delivery Services](/help/edge/docs/forms/publishing-forms.md).

## Come scegliere tra i vari tipi di creazione dei moduli?

La tabella seguente illustra le funzioni e i casi d’uso per ogni editor di authoring, per aiutarti a scegliere quello giusto in base ai tuoi requisiti e alle tue esigenze di invio dei moduli.

| **Editor per la creazione moduli** | **Approccio chiave** | **Funzioni** | **Metodo di pubblicazione** | **Casi d’uso** |
|--------|-----------|-------|-------|------------------------------------------------|
| **Authoring basato su documenti** | Sfrutta strumenti familiari come Documenti Google e Microsoft Office per la creazione di moduli. | I moduli sono progettati utilizzando fogli di calcolo, con dati inviati direttamente a Fogli Google o fogli di Microsoft Excel. </br> </br> Questi moduli sono più veloci da creare e distribuire. Per sviluppare componenti e stili personalizzati per questi moduli non è necessaria alcuna conoscenza preliminare di AEM. | Questi moduli sono pubblicati su Edge Delivery Services e hanno un punteggio Google Lighthouse molto alto. </br> </br> Il punteggio elevato consente un rendering più rapido e una SEO migliore. | Questi moduli sono ideali per la creazione rapida di prototipi o per moduli di base in cui non sono necessari servizi di invio avanzati. </br> </br> Questi moduli sono particolarmente adatti per sondaggi, registrazioni o moduli di feedback che richiedono l’archiviazione dei dati nei fogli di calcolo. Questi moduli vengono pubblicati su Edge Delivery Services |
| **Editor universale**  </br> </br> Se stai creando un modulo nuovo, utilizza Editor universale per creare i moduli. | Offre un’interfaccia WYSIWYG per la creazione intuitiva dei moduli. | I moduli sono progettati tramite un’interfaccia di trascinamento intuitiva. </br> </br> Questi moduli prendono in prestito l’aspetto dall’archivio GitHub di Edge Delivery Services configurato per il modulo corrispondente. | Questi moduli sono pubblicati su Edge Delivery Services e hanno un punteggio Google Lighthouse molto alto. </br> </br> Il punteggio elevato consente un rendering più rapido e una SEO migliore. | Questi moduli sono ideali per la creazione di moduli per siti e pagine di Edge Delivery Service. Questi scenari di moduli coinvolgono moduli e flussi di lavoro complessi, azioni personalizzate o integrazioni con sistemi esterni |
| **Editor moduli adattivi** | Fornisce un approccio guidato per avviare rapidamente la creazione di moduli utilizzando modelli, stili e campi predefiniti. | Utilizza questi editor per creare moduli basati su Componenti core o moduli basati su Componenti base. | Questi moduli possono essere pubblicati su Edge Delivery Services o tramite istanze di pubblicazione di AEM. | Utilizza questi editor per creare moduli basati su Componenti core o moduli basati su Componenti base. Ideali per scenari che richiedono moduli e flussi di lavoro complessi, azioni personalizzate o integrazioni con sistemi esterni. |


>[!NOTE]
>
>
> Se nell’editor universale mancano funzioni precedentemente disponibili nell’editor di moduli adattivi, si possono richiedere inviando un’e-mail a mailto:aem-forms-ea@adobe.com utilizzando il proprio indirizzo e-mail ufficiale.

## Articolo correlato

* [Creazione basata su documenti con Microsoft Excel o Fogli Google](/help/edge/docs/forms/create-forms.md)
* [Editor universale per l’authoring WYSIWYG](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)
* [Creare un modulo adattivo (componenti di base)](/help/forms/creating-adaptive-form.md)
* [Creare un modulo adattivo (componenti core)](/help/forms/create-an-adaptive-form.md)

## Consulta anche

{{see-more-forms-eds}}