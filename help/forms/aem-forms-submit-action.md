---
title: Come si configura un’azione di invio per un modulo adattivo?
description: Un modulo adattivo fornisce più azioni di invio. Un’azione di invio definisce il modo in cui un modulo adattivo viene elaborato dopo l’invio. Puoi utilizzare le azioni di invio integrate o crearne di personalizzate.
feature: Adaptive Forms, Foundation Components, Edge Delivery Services, Core Components
role: User, Developer
source-git-commit: c0df3c6eaf4e3530cca04157e1a5810ebf5b4055
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 12%

---


# Azioni di invio supportate da Adaptive Forms

I moduli adattivi consentono di creare moduli coinvolgenti e reattivi, che si rivelano, inoltre, dinamici e adattivi. Offrono un’interfaccia utente intuitiva e un set di componenti pronti all’uso per la progettazione e la gestione efficiente dei moduli. Puoi configurare diverse azioni di invio per inviare i dati del modulo a servizi come OneDrive, SharePoint, Workfront Fusion e altro ancora.

Un&#39;azione di invio viene attivata quando un utente fa clic sul pulsante **[!UICONTROL Invia]** in un modulo adattivo. Forms as a Cloud Service fornisce diverse azioni di invio pronte all’uso. Le azioni di invio incorporate consentono di:

* Inviare facilmente i dati del modulo tramite e-mail
* Avvia flussi di lavoro Microsoft® Power Automate o AEM durante la trasmissione dei dati.
* Trasmette direttamente i dati del modulo a Microsoft® SharePoint Server, Microsoft® Azure Blob Storage o Microsoft® OneDrive.
* Invia facilmente i dati a un’origine dati configurata utilizzando il modello dati del modulo (FDM).
* Invia in modo semplice i dati a un endpoint REST.

## Azioni di invio supportate da Adaptive Forms

AEM Forms offre le seguenti azioni di invio predefinite:

* [Invia e-mail](/help/forms/configure-submit-action-send-email.md)
* [Richiama un flusso Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
* [Invia a SharePoint](/help/forms/configure-submit-action-sharepoint.md)
* [Richiama Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
* [Inviare mediante il modello di dati modulo (FDM)](/help/forms/using-form-data-model.md)
* [Invia ad Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md)
* [Invia a endpoint REST](/help/forms/configure-submit-action-restpoint.md)
* [Invia a OneDrive](/help/forms/configure-submit-action-onedrive.md)
* [Richiama un flusso di lavoro AEM](/help/forms/configure-submit-action-workflow.md)
* [Invia a Marketo enagage](/help/forms/submit-adaptive-form-to-marketo-engage.md)
* [Invia a Adobe Experience Platform (AEP)](/help/forms/aem-forms-aep-connector.md)
* [Invia a foglio di calcolo](/help/forms/forms-submission-service.md)

È inoltre possibile inviare un modulo adattivo ad altre configurazioni di archiviazione:

* [Collegare un modulo adattivo all’applicazione Salesforce](/help/forms/aem-forms-salesforce-integration.md)
* [Collegare un modulo adattivo a Microsoft](/help/forms/ms-dynamics-odata-configuration.md)

## Supporto delle azioni di invio tra i tipi di authoring

La tabella seguente mostra quali azioni di invio sono supportate in base al metodo di authoring dei moduli utilizzato in AEM Forms:

| Azione invio | [Componenti di base](/help/forms/configuring-submit-actions.md) | [Componenti core](/help/forms/configure-submit-actions-core-components.md) | [Editor universale](/help/forms/configure-submit-action-eds-forms.md#submit-actions-supported-by-adaptive-forms-created-in-universal-editor) | [Forms basato su documenti](/help/forms/configure-submit-action-eds-forms.md#supported-submit-actions-for-document-based-forms) |
|----------------------------|------------------------|------------------|------------------|------------------------|
| Inviare un’e-mail | ✅ supportati | ✅ supportati | ✅ supportati |                        |
| Flusso di Power Automate | ✅ supportati | ✅ supportati | ✅ supportati |                        |
| Invia a SharePoint | ✅ supportati | ✅ supportati | ✅ supportati |                        |
| Workfront Fusion | ✅ supportati | ✅ supportati | ✅ supportati |                        |
| Invia tramite FDM | ✅ supportati | ✅ supportati | ✅ supportati |                        |
| Invia ad AEP | ✅ supportati | ✅ supportati | ✅ supportati |                        |
| Archiviazione BLOB di Azure | ✅ supportati | ✅ supportati | ✅ supportati |                        |
| Invia all’endpoint REST | ✅ supportati | ✅ supportati | ✅ supportati |                        |
| Invia a Marketo Engage | ✅ supportati | ✅ supportati | ✅ supportati |                        |
| Invia a OneDrive | ✅ supportati | ✅ supportati | ✅ supportati |                        |
| Richiama il flusso di lavoro AEM | ✅ supportati | ✅ supportati | ✅ supportati |                        |
| Invia a foglio di calcolo |                        |                  | ✅ supportati | ✅ supportati |


## Riconvalida lato server in modulo adattivo

In genere, in qualsiasi sistema di acquisizione dati online, gli sviluppatori inseriscono alcune convalide JavaScript sul lato client per applicare alcune regole di business. Tuttavia, nei browser moderni, gli utenti finali possono ignorare tali convalide ed effettuare manualmente gli invii utilizzando varie tecniche, ad esempio la Console per la creazione di strumenti di browser Web. Tali tecniche sono valide anche per Adaptive Forms. Uno sviluppatore di moduli può creare diverse logiche di convalida, ma tecnicamente gli utenti finali possono ignorarle e inviare dati non validi al server. I dati non validi violano le regole business applicate da un autore di moduli.

La funzione di riconvalida lato server consente inoltre di eseguire le convalide fornite da un autore di Forms adattivo durante la progettazione di un modulo adattivo sul server. Impedisce qualsiasi possibile compromissione dell’invio dei dati e delle violazioni delle regole aziendali rappresentate in termini di convalide dei moduli.


### Cosa convalidare su Server?

Tutte le convalide di campo pronte all’uso di un modulo adattivo che vengono rieseguite sul server sono:

* Obbligatorio
* Clausola di convalida immagine
* Espressione di convalida

Utilizza **[!UICONTROL Riconvalida sul server]** in Contenitore modulo adattivo nella barra laterale per abilitare o disabilitare la convalida lato server per il modulo corrente.

![Abilitazione della convalida lato server](assets/revalidate-on-server.png)

**Abilitazione della convalida lato server**

Se l&#39;utente finale ignora tali convalide e invia i moduli, il server esegue nuovamente la convalida. Se la convalida non riesce alla fine del server, la transazione di invio viene interrotta. All’utente viene nuovamente presentato il modulo originale. I dati acquisiti e inviati vengono presentati all’utente come un errore.

>[!NOTE]
>
>La convalida lato server convalida il modello del modulo. Ti consigliamo di creare una libreria client separata per le convalide e non combinarla con altri elementi come lo stile di HTML e la manipolazione DOM nella stessa libreria client.

<!--### Supporting Custom functions in Validation Expressions {#supporting-custom-functions-in-validation-expressions-br}

At times, if there are **complex validation rules**, the exact validation script reside in custom functions and author calls these custom functions from field validation expression. To make this custom function library known and available while performing server-side validations, the form author can configure the name of AEM client library under the **[!UICONTROL Basic]** tab of Adaptive Form Container properties as shown below.

![Supporting Custom functions in Validation Expressions](assets/clientlib-cat.png)

Supporting Custom functions in Validation Expressions

Author can configure customJavaScript library per Adaptive Form. In the library, only keep the reusable functions, which have dependency on jquery and underscore.js third-party libraries.

Refer to the following articles to learn how to create custom functions for:

* [Adaptive Forms based on Foundation Components](/help/forms/rule-editor.md#custom-functions-in-rule-editor)
* [Adaptive Forms based on Core Components](/help/forms/create-and-use-custom-functions.md)
* [Adaptive Forms authored using Document-Based Authoring](/help/edge/docs/forms/rules-forms.md#create-a-custom-function)
* [Adaptive Forms created using the Universal Editor](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md#create-a-custom-function)

## Error handling on Submit Action {#error-handling-on-submit-action}

As a part of AEM security and hardening guidelines, configure custom error pages such as 400.jsp, 404.jsp, and 500.jsp. These handlers are called, when on submitting a form 400, 404, or 500 errors appear. The handlers are also called when these error codes are triggered on the Publish node. You can also create JSP pages for other HTTP error codes.

When you prefill a form data model (FDM), or schema based Adaptive Form with XML or JSON data complaint to a schema that is data does not contain `<afData>`, `<afBoundData>`, and `</afUnboundData>` tags, then the data of unbounded fields of the Adaptive Form is lost. The schema can be an XML schema, JSON schema, or a Form Data Model (FDM). Unbounded fields are Adaptive Form fields without the `bindref` property.-->

## Consulta anche

{{af-submit-action}}

