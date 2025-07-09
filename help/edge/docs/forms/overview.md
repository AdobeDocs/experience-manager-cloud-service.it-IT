---
title: Panoramica di Edge Delivery Services per AEM Forms
description: Scopri come utilizzare Edge Delivery Services per creare e distribuire moduli ad alte prestazioni con AEM Forms, consentendo uno sviluppo rapido e una raccolta dati semplificata.
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: 1ddf97f56e5a9b7c95959da47a748f5a6d128e43
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 8%

---


# Edge Delivery Services per AEM Forms


Edge Delivery Services per AEM Forms è un set di servizi componibili per un ambiente di sviluppo rapido in cui nuovi moduli possono essere aggiornati, pubblicati e lanciati rapidamente dagli autori. Questi servizi forniscono esperienze di moduli di eccezionale e forte impatto che determinano coinvolgimento e conversioni. Queste esperienze di moduli sono facili da creare e sviluppare.

* **Esperienze più veloci:** Forms vengono forniti da una rete CDN (Content Delivery Network) globale, per garantirne il caricamento rapido da parte degli utenti.
* **Sviluppo rapido:** Un processo di sviluppo semplificato consente aggiornamenti più rapidi. Le modifiche possono essere pubblicate senza attendere lunghe build della pipeline.
* **Authoring flessibile:** è possibile scegliere tra vari strumenti per la creazione di moduli, tra cui l&#39;authoring basato su documenti (Microsoft Word, Google Docs/Sheets) o un editor WYSIWYG visivo (Universal Editor).

## Come funziona

Con Edge Delivery Services, la struttura e il contenuto del modulo possono risiedere in origini come AEM as a Cloud Service, Microsoft SharePoint o Google Drive. Questo contenuto viene pubblicato su una rete CDN globale. Quando un utente visita il sito, il modulo viene servito direttamente dal server Edge CDN più vicino per ottenere prestazioni ottimali.

![Diagramma semplificato dell&#39;architettura con origini di contenuto, una rete CDN e l&#39;utente.](/help/forms/assets/eds-simplified-architecture.png)
**Architettura Edge Delivery Services semplificata con Forms**

I dati inviati dagli utenti possono essere inviati a varie destinazioni, da un semplice foglio di calcolo a un potente backend di AEM per un’ulteriore elaborazione.

## Scelta di un metodo di authoring

Sono disponibili diversi modi per creare moduli per i siti Edge Delivery Services. Il metodo migliore dipende dalle competenze del team, dalla complessità del modulo e dai requisiti del progetto.

![Struttura decisionale per la scelta di un metodo di creazione dei moduli.](/help/forms/assets/eds-authoring-selection.png)
**Struttura delle decisioni per l&#39;authoring dei moduli**

### Authoring basato su documenti

Questo metodo consente di [creare moduli con Microsoft Word o Google Docs/Sheets](/help/edge/docs/forms/create-forms.md). È possibile definire campi modulo, etichette e tipi in un documento utilizzando un formato tabella specifico. Edge Delivery Services converte il documento in un modulo HTML interattivo.

**Caratteristiche:**

* Creazione in strumenti familiari: fogli Word, Google Docs o Google.
* Definisci campi come input di testo, e-mail, elenchi a discesa, caselle di controllo e pulsanti di scelta.
* Impostare regole di convalida di base, ad esempio campi obbligatori.
* Integra Google reCAPTCHA per la protezione da posta indesiderata.
* Supporto per il caricamento di file.
* Invia i dati direttamente a un foglio di calcolo o a un indirizzo e-mail.
* Estendi con codice personalizzato tramite GitHub per componenti e stili avanzati.

**Ideale per:**

* Team che utilizzano principalmente gli editor di documenti per la creazione di contenuti.
* Creazione rapida di moduli semplici o moderatamente complessi.
* Raccolta dati semplice su foglio di calcolo o e-mail.

Gli invii da moduli basati su documenti vengono in genere gestiti dal [Servizio di invio AEM Forms](/help/forms/forms-submission-service.md), che indirizza i dati a un foglio di calcolo o a un indirizzo e-mail configurato.

### Authoring nell’Editor universale

[Universal Editor fornisce un&#39;interfaccia moderna di WYSIWYG](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) per la creazione di moduli con un&#39;esperienza di trascinamento della selezione.

**Caratteristiche:**

* Creazione di moduli visiva e con trascinamento della selezione con una libreria di componenti predefiniti.
* Configura la convalida in tempo reale e la logica di business complessa (ad esempio, mostra/nascondi campi in base alle selezioni dell’utente).
* Anteprima live per diversi dispositivi.
* Integrazione approfondita con funzioni di AEM as a Cloud Service come Frammenti di contenuto, Flussi di lavoro di AEM e autorizzazioni utente.
* Creazione e modifica di moduli basati sull’intelligenza artificiale tramite &quot;Experience Builder&quot;.

**Ideale per:**

* Creazione di moduli complessi con logica condizionale, pannelli in più passaggi o personalizzazione.
* Team (ad esempio, esperti di marketing, utenti aziendali) che preferiscono gli strumenti visivi.
* Progetti che richiedono una forte integrazione con il backend AEM per l’elaborazione dei dati e i flussi di lavoro.

Forms creato con Universal Editor può utilizzare il [Servizio di invio Forms](/help/forms/forms-submission-service.md) o essere configurato per utilizzare [azioni di invio fornite OOTB per la gestione avanzata dei dati](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md), ad esempio l&#39;invio di dati a un flusso di lavoro AEM, un endpoint REST o a un database.

### Incorporazione di Forms nelle pagine di authoring dei documenti

[Document Authoring (DA)](https://www.aem.live/developer/da-tutorial) è un servizio ospitato da Adobe per la gestione dei contenuti dei siti Web per Edge Delivery Services. Sebbene DA non sia uno strumento per la creazione di moduli, è possibile utilizzarlo per creare pagine Web e quindi incorporare moduli creati con altri metodi.

**Funzionamento:**

1. **Creare il modulo:** Creare il modulo utilizzando l&#39;authoring basato su documenti o l&#39;editor universale.
2. **Pubblica il modulo:** Assicurati che il modulo sia pubblicato e accessibile al proprio URL.
3. **Incorpora in DA:** Nella pagina di authoring dei documenti, aggiungi un blocco che fa riferimento all&#39;URL del modulo per incorporarlo.

Questo approccio è pensato per i team che utilizzano l’authoring dei documenti come sistema principale di gestione dei contenuti per i siti Edge Delivery Services.

## Confronto dei metodi di authoring

| Criteri | Authoring basato su documenti | Editor universale (WYSIWYG) | Forms nell’authoring dei documenti (DA) |
|----------------------------------|---------------------------------------|-----------------------------------------|-------------------------------------------|
| **Strumento di authoring primario** | Word/Google Docs/Fogli | Browser (AEM Universal Editor) | N/D (i Forms sono *embedded*) |
| **Livello abilità team** | Conoscenza degli editor di documenti | Comodità degli strumenti Web visivi | Utilizza DA per il contenuto della pagina |
| **Complessità tipica del modulo** | Da semplice a moderato | Da moderato a complesso, di livello Enterprise | Dipende dal modulo incorporato |
| **Opzioni invio** | Servizio di invio Forms (a foglio/e-mail) | Servizio di invio Forms, pubblicazione AEM (flusso di lavoro, modello dati modulo, integrazioni di terze parti) | Segue la configurazione del modulo incorporato |
| **Integrazione back-end di AEM** | Minimo | Alta (con invio pubblicazione AEM) | Indirettamente, tramite modulo Editor universale incorporato |
| **Ottimo per...** | Creazione rapida di moduli semplici da parte di team di contenuti, acquisizione rapida dei dati. | Esperti di marketing e utenti aziendali che necessitano di controllo visivo, moduli complessi o un’integrazione approfondita con AEM. | Siti in cui il contenuto principale viene gestito in DA. |

<!-- 
## Detailed Feature Comparison

| **Capability**                        | **Universal Editor (WYSIWYG)** | **Document-based Authoring** | **Document Authoring (DA)** |
|-----------------------------------------|-------------------------------|-----------------------------|-----------------------------|
| **Unified Composition with Sites**    | ✅                            |                              | ✅ (with embedded forms)     |
| **Embedding Form Support**            | ✅                            | ✅                          | ✅ (embed from Universal Editor or Docs)   |
| **Rules (Dynamic Behavior)**          | Advanced rules editor with custom functions | Limited: Show/hide, compute value, custom functions | Depends on embedded form     |
| **Attachment Support**                | ✅                            | ℹ️ (Early Access)           | Depends on embedded form     |
| **CAPTCHA Support**                   | reCAPTCHA Enterprise          | reCAPTCHA Enterprise       | Depends on embedded form     |
| **Submission Features**               | REST, Email, FDM, Workflow, SharePoint, OneDrive, Azure Blob, Power Automate, Workfront Fusion (EA) | Only Spreadsheet            | Follows embedded form's setup |
| **Data Schema**                       | FDM, Custom                   | Custom                      | Based on embedded form       |
| **Pre-fill**                          | 💡 (via Wizard)               | ✅                          | Depends on embedded form     |
| **Fragments**                         | ✅                            | ✅                          | Depends on embedded form     |
| **Visual Rule Editor**                | ✅                            |                              |                              |
| **Localization**                      | 💡 (via Sites)                | ℹ️ (Excel/Sheets manual)    | Depends on embedded form     |
| **Template Support**                  | Only Initial Content          |                              |                              |
| **Theme**                             | ℹ️ (at project level)         | ℹ️ (at project level)        | ℹ️ (based on hosting site)    |
| **Custom Component**                  | ✅                            | ✅                          | ✅ (if embedded component supports it) |
| **Experimentation**                   | ✅                            | ✅                          | Depends on embed context     |
| **Submit Action**                     | ✅                            | Only Spreadsheet            | Based on embedded form       |
-->



## Passaggi successivi

* [Creare un modulo con authoring basato su documenti](/help/edge/docs/forms/tutorial.md)
* [Scopri Universal Editor per Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [Configurare le azioni di invio dei moduli](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)
* [Informazioni su Document Authoring (DA)](https://www.aem.live/developer/da-tutorial)
