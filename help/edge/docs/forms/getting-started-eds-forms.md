---
title: Guida introduttiva di Forms su AEM Edge Delivery Services
description: Scopri come creare e distribuire moduli ad alte prestazioni su Adobe Experience Manager Edge Delivery Services, con particolare attenzione all’approccio di authoring di Universal Editor.
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: e1ead9342fadbdf82815f082d7194c9cdf6d799d
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 1%

---


# Guida introduttiva di Forms su AEM Edge Delivery Services

<span class="preview"> Questa è una funzionalità pre-release disponibile tramite il nostro <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=it#new-features">canale pre-release</a>. </span>

Adobe Experience Manager (AEM) Edge Delivery Services (EDS) consente di offrire esperienze web estremamente veloci e altamente scalabili dall’edge di. Questa guida spiega **come creare e pubblicare moduli per tali esperienze**, con una chiara gerarchia di consigli:

1. **Editor universale (UE): scelta migliore per la maggior parte dei team**
2. **Authoring basato su documenti (documenti/fogli): ideale per moduli semplici e veloci**
3. **Authoring dei documenti (DA) - Utilizzare per incorporare i moduli nelle pagine create da DA**

Entro la fine sarà possibile scegliere il metodo di authoring corretto, comprendere le opzioni di invio e seguire i passaggi successivi verso i moduli pronti per la produzione.



## Scelta di un metodo di authoring

| Team e requisiti | Metodo consigliato | Perché |
|--------------------|--------------------|-----|
| Gli addetti al marketing e i designer hanno bisogno di controllo visivo, logica condizionale o integrazioni AEM | **Editor universale** | Trascinamento della selezione, regole avanzate, invii a FSS o AEM Publish |
| Autori di contenuti che già lavorano in Word/Google Docs/Sheets; acquisizione dati semplice su foglio di calcolo/e-mail | **Authoring basato su documenti** | Strumenti familiari, percorso più veloce per i moduli di base |
| Pagine del sito Web generate in **Document Authoring (DA)** | **Incorpora** un modulo UE o basato su documenti nella pagina DA | DA non genera i moduli |


## Metodi di authoring in dettaglio

### Editor universale

Universal Editor è uno strumento di authoring visivo e con trascinamento per gli esperti di marketing e i designer che combina velocità e potenza di livello enterprise:

* Editing WYSIWYG in tempo reale e anteprime dei dispositivi.
* Regole avanzate e interfaccia utente di convalida: non è richiesto alcun codice.
* Integrazione diretta con risorse AEM, flussi di lavoro e Form Data Model (FDM).
* Comodo passaggio per gli sviluppatori di componenti personalizzati in Vanilla JS/CSS.
* Destinazioni di invio flessibili: inizia semplice con **Forms Submission Service (FSS)** o passa a **AEM Publish submit actions** in base alle tue esigenze.

> **Consiglio**: avvia ogni nuovo progetto modulo con Universal Editor a meno che il team non sia interamente incentrato sul documento e il modulo non sia molto semplice.


### Authoring basato su documenti (documenti/fogli)

L&#39;authoring basato su documenti è particolarmente adatto per la creazione di moduli semplici e a bassa complessità, utilizzando strumenti familiari come Microsoft Word, Google Docs o Google Sheets. Questo metodo è ideale per i team di contenuti che richiedono un modo rapido e semplice di creare moduli.

* Definisci i campi modulo all’interno di una tabella (Docs) o come righe (Sheets).
* Supporta la convalida di campo di base e Google reCAPTCHA per la protezione da posta indesiderata.
* Gli invii di moduli vengono gestiti esclusivamente tramite il servizio di invio Forms.
* Pubblicazione immediata: qualsiasi modifica apportata nel documento di origine viene immediatamente riportata sul sito senza richiedere una pipeline di distribuzione.


### Incorporazione di Forms nell’authoring dei documenti (DA)

L’authoring dei documenti (DA) è progettato per creare contenuti di pagina strutturati e non supporta la creazione di moduli nativi. Per aggiungere un modulo a una pagina creata da, eseguire la procedura seguente:

1. Creare il modulo utilizzando **Universal Editor** (scelta consigliata) o l&#39;authoring basato su documenti.
2. Pubblicare il modulo per generare un URL univoco, ad esempio `/forms/contact-us`.
3. Nella pagina DA, inserisci un blocco **Incorpora modulo** e specifica l&#39;URL del modulo pubblicato.

<!-- 
## Feature Comparison

| Capability | Universal Editor | Document-Based | Document Authoring |
|------------|-----------------|----------------|--------------------|
| Visual drag-and-drop | ✅ | – | – |
| Advanced rules editor | ✅ | Limited | – |
| Attachments | ✅ | EA | – |
| reCAPTCHA Enterprise | ✅ | ✅ | Depends on embed |
| Submit to spreadsheet/email | ✅ (FSS) | ✅ (FSS) | Via embed |
| Submit to AEM workflows/FDM | ✅ | – | Via UE embed |
| Custom components (JS/CSS) | ✅ | ✅ | Via embed |
| Localization via Sites | ✅ | Manual | Via embed |

-->

## Passaggi successivi

1. **Inizia con l&#39;editor universale:** Per iniziare a creare i moduli, consulta la [guida introduttiva all&#39;editor universale](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md).
2. **Configura invio modulo:** Seleziona e imposta il metodo di invio preferito. Per istruzioni sulla configurazione, consulta [Forms Submission Service](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md) o AEM Publish submit actions.
3. **Applica best practice:** Rivedi [best practice per la progettazione dei moduli](/help/edge/docs/forms/universal-editor/best-practices-eds-forms.md) per garantire accessibilità e prestazioni.
4. **Utilizzare l&#39;authoring basato su documenti:** Per creare moduli con Microsoft Excel o Google Sheets, seguire la [esercitazione sull&#39;authoring basato su documenti](/help/edge/docs/forms/tutorial.md).
5. **Incorpora Forms nell&#39;authoring dei documenti:** Se stai creando pagine nell&#39;authoring dei documenti, consulta l&#39;[esercitazione DA](https://www.aem.live/developer/da-tutorial) per istruzioni sull&#39;incorporamento dei moduli pubblicati.

> **È ora possibile creare il primo modulo ad alte prestazioni con AEM Edge Delivery Services.**