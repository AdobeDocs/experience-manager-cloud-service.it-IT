---
title: Come si configura un’azione di invio per un modulo adattivo?
description: Un modulo adattivo fornisce più azioni di invio. Un’azione di invio definisce il modo in cui un modulo adattivo viene elaborato dopo l’invio. Puoi utilizzare le azioni di invio incorporate o crearne di personalizzate
keywords: come selezionare l’azione di invio per un modulo adattivo, collegare un modulo adattivo a un elenco di sharepoint, collegare un modulo adattivo a una raccolta documenti di sharepoint, collegare un modulo adattivo a un modello di dati modulo (FDM)
feature: Adaptive Forms, Core Components
exl-id: 495948e8-30a7-4e7c-952f-c71de15520f0
role: User, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 11%

---


# Azione di invio modulo adattivo {#configuring-the-submit-action}

<span class="preview"> Adobe consiglia di utilizzare i Componenti core per [aggiungere Forms adattivo a una pagina AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md) o per [creare Forms adattivo autonomo](/help/forms/creating-adaptive-form-core-components.md). </span>


| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-submit-actions.html?lang=it) |
| AEM as a Cloud Service (Componenti di base) | [Fai clic qui](/help/forms/configuring-submit-actions.md) |
| AEM as a Cloud Service (Componenti core) | Questo articolo |

Un’azione di invio consente di scegliere la destinazione dei dati acquisiti tramite un modulo adattivo. Viene attivato quando un utente fa clic sul pulsante **[!UICONTROL Invia]** in un modulo adattivo. Forms as a Cloud Service, per Forms adattivo basato su Componenti core, offre una serie di azioni di invio predefinite. Queste azioni di invio pronte all’uso ti consentono di:

* Invia facilmente i dati del modulo tramite e-mail.
* Avvia flussi di lavoro Microsoft® Power Automate o AEM durante la trasmissione dei dati.
* Trasmette direttamente i dati del modulo a Microsoft® SharePoint Server, Microsoft® Azure Blob Storage o Microsoft® OneDrive.
* Invia facilmente i dati a un’origine dati configurata utilizzando il modello dati del modulo (FDM).
* Invia in modo semplice i dati a un endpoint REST.

È possibile [estendere le azioni di invio predefinite](custom-submit-action-form.md). È inoltre possibile personalizzare le azioni di invio in base ai requisiti specifici dell&#39;organizzazione.

Per definire un&#39;azione di invio per un modulo adattivo, utilizzare la finestra di dialogo per configurazione di un componente **Contenitore modulo adattivo**. La finestra di dialogo per configurazione di un componente **Contenitore modulo adattivo** include:

* Scheda Base
* Scheda Modello dati modulo
* Scheda Invio

Puoi definire le proprietà del Contenitore modulo utilizzando la finestra di dialogo per configurazione. Per ulteriori informazioni sulla finestra di dialogo per configurazione di un componente Contenitore modulo, [fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/form-container.html?lang=it).

## Selezionare e configurare un’azione di invio per un modulo adattivo {#select-and-configure-submit-action}

Per selezionare e configurare un&#39;azione di invio per il modulo:

1. Apri il browser Contenuto e seleziona il componente **[!UICONTROL Contenitore guida]** del modulo adattivo.
1. Fare clic sull&#39;icona delle proprietà del Contenitore Guida TV ![Proprietà Guida](/help/forms/assets/configure-icon.svg). Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).

1. Fare clic sulla scheda **[!UICONTROL Invio]**.

   ![Fai clic sull&#39;icona chiave inglese per aprire la finestra di dialogo Contenitore modulo adattivo e configurare un&#39;azione di invio](/help/forms/assets/adaptive-forms-submit-message.png)

1. Seleziona e configura un&#39;azione **[!UICONTROL Invia]** in base alle tue esigenze.

Puoi anche configurare diverse azioni per l’invio di un modulo adattivo.
* **URL/percorso di reindirizzamento** - Questa opzione consente all&#39;utente di configurare una pagina per ogni modulo, alla quale gli utenti del modulo vengono reindirizzati dopo l&#39;invio di un modulo adattivo.
* **Mostra Messaggio**: questa opzione consente agli utenti di aggiungere un messaggio da visualizzare quando il modulo adattivo viene inviato correttamente. Il testo predefinito viene incluso nella finestra di dialogo e può essere modificato dall&#39;utente.

Per informazioni dettagliate sulle seguenti azioni di invio, vedere:

* [Invia e-mail](/help/forms/configure-submit-action-send-email.md)
* [Richiama un flusso Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
* [Invia a SharePoint](/help/forms/configure-submit-action-sharepoint.md)
* [Richiama Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
* [Invia utilizzando il modello dati modulo (FDM)](/help/forms/using-form-data-model.md)
* [Invia ad Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md)
* [Invia all’endpoint REST](/help/forms/configure-submit-action-restpoint.md)
* [Invia a OneDrive](/help/forms/configure-submit-action-onedrive.md)
* [Richiama un flusso di lavoro AEM](/help/forms/configure-submit-action-workflow.md)
* [Invia a Marketo enagage](/help/forms/submit-adaptive-form-to-marketo-engage.md)

È inoltre possibile inviare un modulo adattivo ad altre configurazioni di archiviazione:

* [Collegare un modulo adattivo all’applicazione Salesforce](/help/forms/aem-forms-salesforce-integration.md)
* [Collegare un modulo adattivo a Microsoft](/help/forms/ms-dynamics-odata-configuration.md)
* [Collegare un modulo adattivo a Marketo Engage](/help/forms/integrate-form-to-marketo-engage.md)

È possibile [personalizzare le azioni di invio predefinite](custom-submit-action-form.md). Inoltre, puoi personalizzare le azioni di invio per allinearle a specifici requisiti organizzativi.


<!--
## Send Email {#send-email}

To send an email to one or more recipients upon successful submission of the form, you can use the **[!UICONTROL Send Email]** Submit Action. 

Refer to [configure the send email submit action for an Adaptive Form](/help/forms/configure-submit-action-send-email.md) to learn how to set up an Adaptive Form to send an email upon successful submission.
[!NOTE]
>
>Send PDF via Email Submit Action is applicable only to Adaptive Forms that use XFA template as form model. 

>[!NOTE]
>
>Ensure that the [AEM_Installation_Directory]\crx-quickstart\temp\datamanager\ASM folder
>exists. The directory is required to temporarily store attachments. If the directory does not exist, create it.


>[!CAUTION]
>
>If you  [prefill](prepopulate-adaptive-form-fields.md) a form template,  a Form Data Model (FDM) or schema based Adaptive Form with XML or JSON data complaint to a schema (XML schema, JSON schema , form template, or form data model (FDM)) that is data does not contain &lt;afData&gt;, &lt;afBoundData&gt;, and &lt;/afUnboundData&gt; tags, then the data of unbounded fields (Unbounded fields are Adaptive Form fields without [bindref](prepopulate-adaptive-form-fields.md) property) of the Adaptive Form is lost. 

>[!CAUTION]
>
>If you [prefill](prepopulate-adaptive-form-fields.md) a form template, a Form Data Model (FDM) or schema based Adaptive Form with XML or JSON data complaint to a schema (XML schema, JSON schema, or form data model(FDM)) that does not contain &lt;afData&gt;, &lt;afBoundData&gt;, and &lt;/afUnboundData&gt; tags, then the data of unbounded fields (Unbounded fields are Adaptive Form fields without [bindref](prepopulate-adaptive-form-fields.md) property) of the Adaptive Form is lost.

## Submit to Microsoft&reg; SharePoint {#submit-to-sharedrive}

The **[!UICONTROL Submit to SharePoint]** Submit Action connects an Adaptive Form with a Microsoft&reg; SharePoint Storage. You can submit the form data files, attachments, or Document of Record to the connected Microsoft&reg; Sharepoint Storage. 

Integration of AEM Adaptive Form with Microsoft&reg; SharePoint enables the submission, retrieval, or storage of data, files, and other relevant information within the SharePoint storage. To learn how to configure submit to SharePoint submit action for an Adaptive Form, [click here](/help/forms/configure-submit-action-sharepoint.md). 

## Submit using Form Data Model (FDM) {#submit-using-form-data-model}

The **[!UICONTROL Submit using Form Data Model (FDM)]** Submit Action writes submitted Adaptive Form data for the specified data model object in a Form Data Model (FDM) to its data source. When configuring the Submit Action, you can choose a data model object whose submitted data you want to write back to its data source.

When a user submits a form based on a form data model (FDM), you can [configure the form to write the submitted data to the data sources associated with the data model object](/help/forms/using-form-data-model.md#write-submitted-adaptive-form-data-into-data-sources-write-af).

## Submit to REST endpoint {#submit-to-rest-endpoint}

The **[!UICONTROL Submit to REST Endpoint]** submit action sends the submitted data to a REST URL. This URL can be either an internal server (the server where the form is displayed) or an external server. The data of an Adaptive Form is submitted to a REST URL using the **[!UICONTROL Submit to REST endpoint]** Submit Action.

For a comprehensive guide on the detailed steps to post or submit data to a REST URL, refer to [configure submit to REST Endpoint submit action for Adaptive Forms](/help/forms/configure-submit-action-restpoint.md).

## Invoke an AEM Workflow {#invoke-an-aem-workflow}

The **[!UICONTROL Invoke an AEM Workflow]** Submit Action integrates an Adaptive Form with an [AEM Workflow](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=it#extending-aem). When a form is submitted, the selected workflow starts automatically. 

 [Integrate AEM Adaptive Form with AEM Workflow: Streamlining Business Processes](/help/forms/configure-submit-action-workflow.md) provides step-by-step instructions to seamlessly integrate AEM Workflow with Adaptive Forms, optimizing business processes and enhancing workflow automation.

## Submit to OneDrive {#submit-to-onedrive}

The **[!UICONTROL Submit to OneDrive]** Submit Action connects an Adaptive Form with a Microsoft&reg; OneDrive. You can submit the form data, files, attachments, or Document of Record to the connected Microsoft&reg; OneDrive Storage. 

AEM Forms Cloud Service with Microsoft&reg; OneDrive helps in optimize data submission. Explore the steps of [integrating OneDrive with AEM Forms](/help/forms/configure-submit-action-onedrive.md) for streamlined and secure storage.

## Submit to Azure Blob Storage {#submit-to-azure-blob-storage}

The **[!UICONTROL Submit to Azure Blob Storage]** Submit Action connects an Adaptive Form with a Microsoft&reg; Azure portal and allows you to submit various elements such as form data, files, attachments, or Document of Record to the associated Azure Storage containers.

AEM as a Cloud Service allows submitting data to Azure Storage from AEM Adaptive Forms. Learn how to [create and use Azure Blob Storage configuration in AEM Forms](/help/forms/configure-submit-action-azure-blob-storage.md) for efficient data storage. 

To set values of a configuration, [Generate OSGi Configurations using the AEM SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=it#generating-osgi-configurations-using-the-aem-sdk-quickstart), and [deploy the configuration](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=it#deployment-process) to your Cloud Service instance.

## Submit to Power Automate {#microsoft-power-automate}

You can configure an Adaptive Form to run a Microsoft&reg; Power Automate Cloud Flow on submission. The configured Adaptive Form sends captured data, attachments, and Document Of Record to Power Automate Cloud Flow for processing. It helps you build custom data capture experience while harnessing the power of Microsoft&reg; Power Automate to build business logics around captured data and automate customer workflows. 
Adaptive Forms editor provides the **Invoke a Microsoft&reg; Power Automate flow** submit action to send adaptive forms data, attachments, and Document Of Record to Power Automate Cloud Flow. To use the Submit action to send captured data to Microsoft&reg; Power Automate, [Connect your Forms as a Cloud Service instance with Microsoft&reg; Power Automate](forms-microsoft-power-automate-integration.md)  

After a successful configuration, use the [Invoke a Microsoft&reg; Power Automate flow](forms-microsoft-power-automate-integration.md#use-the-invoke-a-microsoft&reg;-power-automate-flow-submit-action-to-send-data-to-a-power-automate-flow-use-the-invoke-microsoft-power-automate-flow-submit-action) submit action to send data to a Power Automate Flow.  

## Submit to Workfront Fusion {#workfront-fusion}

You can configure an Adaptive Form to submit data to Workfront Fusion on submission. Workfront Fusion allows automation of processes so that user can concentrate on new tasks rather than repeating the same tasks again and again. It automates both simple and complex tasks, saving time and ensuring consistent process execution.

The Adaptive Forms editor provides the **Invoke a WorkFront Fusion Scenario** submit action to send Adaptive Forms data or attachments to a Workfront Fusion scenario. To use the submit action for sending captured data to a Workfront Fusion scenario, refer to [Submit an Adaptive Form to Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md).

## Send PDF via Email {#send-pdf-via-email}

The **Send PDF via Email** Submit Action sends an email with a PDF containing form data, to one or more recipients on successful submission of the form.

>[!NOTE]
>
>This Submit Action is available for XFA-based Adaptive Forms and XSD-based adaption forms that have the Document of Record template. 
## Invoke a forms workflow {#invoke-a-forms-workflow}

The **Submit to Forms workflow** submit option sends a data xml and file attachments (if any) to an existing Adobe LiveCycle or [!DNL AEM Forms] on JEE process.

For information about how to configure the Submit to forms workflow Submit Action, see [Submitting and processing your form data using forms workflows](submit-form-data-livecycle-process.md). 
## Forms Portal Submit Action {#forms-portal-submit-action}

The **Forms Portal Submit Action** option makes form data available through an [!DNL AEM Forms] portal.

For more information about the Forms Portal and Submit Action, see [Drafts and submissions component](draft-submission-component.md). 

## Use synchronous or asynchronous submission {#use-synchronous-or-asynchronous-submission}

A Submit Action can use synchronous or asynchronous submission.

**Synchronous submission**: Traditionally, web forms are configured to submit synchronously. In a synchronous submission, when users submit a form, they are redirected to an acknowledgment page, a thank you page, or if there is submission failure, an error page. You can select the **[!UICONTROL Use asynchronous submission]** option to redirect the users to a webpage or show a message on submission.  

![Configure Submit Action](assets/thank-you-setting.png)

**Asynchronous submission**: Modern web experiences like single page applications are gaining popularity where the web page remains static while client-server interaction happens in the background. You can now provide this experience with Adaptive Forms by [configuring asynchronous submission](asynchronous-submissions-adaptive-forms.md).

## Server-Side Revalidation in Adaptive Form {#server-side-revalidation-in-adaptive-form}

Typically, in any online data capture system, developers place someJavaScript validations on client side to enforce a few business rules. But in modern browsers, end users have way to bypass those validations and manually do submissions using various techniques, Such as Web Browser DevTools Console. Such techniques are also valid for Adaptive Forms. A forms developer can create various validation logics, but technically, end users can bypass those validation logics and submit invalid data to the server. Invalid data would break the business rules that a form author has enforced.

The server-side revalidation feature provides the ability to run the validations that an Adaptive Forms author has provided while designing an Adaptive Form on the server. It prevents any possible compromise of data submissions and business rules violations represented in terms of form validations.

### What to validate on Server? {#what-to-validate-on-server-br}

All out of the box (OOTB) field validations of an Adaptive Form that are rerun at the server are:

* Required
* Validation Picture Clause
* Validation Expression

### Enabling Server-side Validation {#enabling-server-side-validation-br}

Use the **[!UICONTROL Revalidate on server]** under Adaptive Form Container in the sidebar to enable or disable server-side validation for the current form.

![Enabling Server-Side Validation](assets/revalidate-on-server.png)

Enabling Server-Side Validation

If end-user bypass those validations and submit the forms, the server again performs the validation. If the validation fails at server end, then the submit transaction is stopped. The user is presented with the original form again. The captured data and submitted data are presented to the user as an error.

>[!NOTE]
>
>Server-side validation validates the form model. You are recommended to create a separate client library for validations and not mix it with other things like HTML styling and DOM manipulation in the same client library.
-->

## Gestione degli errori nell’azione di invio {#error-handling-on-submit-action}

Come parte delle linee guida sulla sicurezza e l’irrigidimento dell’AEM, configura pagine di errore personalizzate come 400.jsp, 404.jsp e 500.jsp. Questi gestori vengono chiamati quando all’invio di un modulo vengono visualizzati errori 400, 404 o 500. I gestori vengono chiamati anche quando questi codici di errore vengono attivati sul nodo Publish. Puoi anche creare pagine JSP per altri codici di errore HTTP.

Quando si precompila un modello di dati modulo (FDM) o un modulo adattivo basato su schema con dati XML o JSON a uno schema che non contiene tag `<afData>`, `<afBoundData>` e `</afUnboundData>`, i dati dei campi non limitati del modulo adattivo andranno persi. Lo schema può essere uno schema XML, uno schema JSON o un modello dati modulo (FDM). I campi non limitati sono campi modulo adattivo senza la proprietà `bindref`.

<!-- For more information, see [Customizing Pages shown by the Error Handler](/help/sites-developing/customizing-errorhandler-pages.md). -->


<!--
## See next

* [Create style or themes for your forms](using-themes-in-core-components.md)
* [Create an Adaptive Form (core components)](/help/forms/creating-adaptive-form-core-components.md)
* [Create a custom Submit Action for Adaptive Forms](/help/forms/custom-submit-action-form.md)

-->

## Consulta anche {#see-also}

{{see-also}}

