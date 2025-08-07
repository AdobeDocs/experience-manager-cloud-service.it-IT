---
title: Guida introduttiva ai moduli in AEM Edge Delivery Services
description: Scopri come creare e distribuire moduli con prestazioni elevate in Adobe Experience Manager Edge Delivery Services, con particolare attenione all’approccio di authoring dell’editor universale.
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 100%

---


# Guida introduttiva ai moduli in AEM Edge Delivery Services

<span class="preview">Si tratta di una funzione pre-release accessibile tramite il <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=it#new-features">canale pre-release</a>. </span>

Adobe Experience Manager (AEM) Edge Delivery Services (EDS) consente di offrire esperienze web estremamente veloci e altamente scalabili dall’edge. Questa guida spiega **come creare e pubblicare moduli per tali esperienze**, con una chiara gerarchia di consigli:

1. **Editor universale (UE): la migliore scelta per la maggior parte dei team**
2. **Authoring basato su documenti (documenti/fogli): ideale per moduli semplici e veloci**
3. **Authoring di documenti (DA): da utilizzare per incorporare i moduli nelle pagine create da DA**

Alla fine, sarai in grado di scegliere il metodo di authoring adatto, comprendere le opzioni di invio e seguire i passaggi successivi verso i moduli pronti per la produzione.



## Scelta di un metodo di authoring

| Team &amp; requisiti | Metodo consigliato | Perché |
|--------------------|--------------------|-----|
| Gli addetti al marketing e i designer hanno bisogno di controllo visivo, logica condizionale o integrazioni AEM | **Editor universale** | Trascinamento, regole avanzate, invii a FSS o AEM Publish |
| Autori di contenuti che già lavorano in Word/Google Docs/Sheets; acquisizione semplice dei dati su foglio di calcolo/e-mail | **Authoring basato su documenti** | Strumenti noti, percorso più veloce per moduli di base |
| Pagine del sito web generate in **Document Authoring (DA)** | **Incorpora** un modulo UE o basato su documenti nella pagina DA | DA non genera i moduli autonomamente |


## Metodi di authoring in dettaglio

### Editor universale

L’editor universale è uno strumento di authoring visivo e di trascinamento per gli addetti al marketing e i designer che combina velocità e potenza di livello enterprise:

- Editing WYSIWYG in tempo reale e anteprime dei dispositivi.
- Regole avanzate e interfaccia utente di convalida: non è richiesto alcun codice.
- Integrazione diretta con AEM Assets, flussi di lavoro e modello dati modulo (FDM).
- Passaggio semplice per sviluppatori di componenti personalizzati in Vanilla JS/CSS.
- Destinazioni di invio flessibili: inizia in modo semplice con il **servizio di invio moduli (FSS)** o passa alle **azioni di invio AEM Publish** in base alle tue esigenze.

> **Consiglio**: avvia ogni nuovo progetto di modulo con l’editor universale a meno che il team non sia interamente incentrato sul documento e il modulo non sia molto semplice.


### Authoring basato su documenti (documenti/fogli)

L’authoring basato su documenti è particolarmente adatto per la creazione di moduli semplici e a bassa complessità, utilizzando strumenti noti come Microsoft Word, Google Docs o Google Sheets. Questo metodo è ideale per i team di contenuti che richiedono un modo rapido e diretto per creare moduli.

- Definisci i campi modulo all’interno di una tabella (Docs) o come righe (Sheets).
- Supporta la convalida del campo di base e Google reCAPTCHA per la protezione da posta indesiderata.
- Gli invii di moduli vengono gestiti esclusivamente tramite il servizio di invio moduli.
- Pubblicazione immediata: qualsiasi modifica apportata nel documento di origine viene immediatamente riportata sul sito senza richiedere una pipeline di distribuzione.


### Incorporamento di moduli in Document Authoring (DA)

Document Authoring (DA) è progettato per la creazione di contenuti di pagina strutturati e non supporta la creazione di moduli nativi. Per aggiungere un modulo a una pagina creata da DA, segui i passaggi seguenti:

1. Crea il modulo utilizzando l’**editor universale** (consigliato) o l’authoring basato su documenti.
2. Pubblica il modulo per generare un URL univoco (ad esempio, `/forms/contact-us`).
3. Nella pagina DA, inserisci un blocco **Incorpora modulo** e specifica l’URL del modulo pubblicato.

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

1. **Inizia con l’editor universale:** per iniziare a creare i moduli, consulta la [guida introduttiva all’editor universale](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md).
2. **Configura invio modulo:** seleziona e imposta il metodo di invio preferito. Per istruzioni sulla configurazione, consulta [Servizio di invio dei moduli](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md) o Azioni di invio di AEM Publish.
3. **Applica best practice:** rivedi le [best practice per la progettazione dei moduli](/help/edge/docs/forms/universal-editor/best-practices-eds-forms.md) per garantire accessibilità e prestazioni.
4. **Utilizza l’authoring basato su documenti:** per creare moduli tramite Microsoft Excel o Google Sheets, segui il [tutorial sull’authoring basato su documenti](/help/edge/docs/forms/tutorial.md).
5. **Incorpora moduli nell’authoring dei documenti:** se stai creando pagine nell’authoring dei documenti, consulta il [tutorial DA](https://www.aem.live/developer/da-tutorial) per ricevere istruzioni sull’incorporamento dei moduli pubblicati.

> **Ora puoi creare il primo modulo ad alte prestazioni con AEM Edge Delivery Services.**