---
title: Come si configura un’azione di invio per un modulo adattivo?
description: Un modulo adattivo fornisce più azioni di invio. Un’azione di invio definisce il modo in cui un modulo adattivo viene elaborato dopo l’invio. Puoi utilizzare le azioni di invio integrate o crearne di personalizzate.
keywords: come selezionare l’azione di invio per un modulo adattivo, collegare un modulo adattivo a un elenco di sharepoint, collegare un modulo adattivo a una raccolta documenti di sharepoint, collegare un modulo adattivo a un modello di dati modulo (FDM)
feature: Adaptive Forms, Edge Delivery Services
role: User, Developer
source-git-commit: c0df3c6eaf4e3530cca04157e1a5810ebf5b4055
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 11%

---


# Azioni di invio per Edge Delivery Services Forms

| Versione | Collegamento articolo |
|---------|-----------------------------|
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-submit-actions.html) |
| AEM as a Cloud Service (Componenti di base) | [Fai clic qui](/help/forms/configuring-submit-actions.md) |
| AEM as a Cloud Service (Componenti core) | [Fai clic qui](/help/forms/configure-submit-actions-core-components.md) |
| AEM as a Cloud Service (Edge Delivery Services) | Questo articolo |

Le azioni di invio definiscono ciò che accade quando un utente invia un modulo, ad esempio l’archiviazione di dati, l’attivazione di flussi di lavoro o l’integrazione con sistemi di terze parti. Il tipo di azioni di invio che è possibile configurare dipende dal metodo di creazione utilizzato per creare Edge Delivery Services Forms.

È possibile creare Edge Delivery Services Forms utilizzando [Universal Editor](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) o l&#39;authoring di [Document Based Forms](/help/edge/docs/forms/overview.md) e configurare di conseguenza i moduli con azioni di invio diverse.

## Azioni di invio per Forms create in Universal Editor

Le seguenti azioni di invio sono supportate da [Forms adattivo creato nell&#39;editor universale](/help/edge/docs/forms/universal-editor/create-forms.md):

* [Invia e-mail](/help/forms/configure-submit-action-send-email.md)
* [Richiama un flusso Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
* [Invia a SharePoint](/help/forms/configure-submit-action-sharepoint.md)
* [Richiama Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
* [Inviare mediante il modello di dati modulo (FDM)](/help/forms/using-form-data-model.md)
* [Inviare ad Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md)
* [Invia all’endpoint REST](/help/forms/configure-submit-action-restpoint.md)
* [Invia a OneDrive](/help/forms/configure-submit-action-onedrive.md)
* [Richiama un flusso di lavoro AEM](/help/forms/configure-submit-action-workflow.md)
* [Invia a Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)
* [Invia a Adobe Experience Platform (AEP)](/help/forms/aem-forms-aep-connector.md)
* [Invia a foglio di calcolo](/help/forms/forms-submission-service.md)

<!--You can also submit an Adaptive Form in the Universal Editor to other storage or CRM integrations:

* [Connect Adaptive Form to Salesforce](/help/forms/aem-forms-salesforce-integration.md)
* [Connect an Adaptive Form to Microsoft&reg; Dynamics OData](/help/forms/ms-dynamics-odata-configuration.md)-->

È possibile configurare l&#39;azione di invio per i moduli creati nell&#39;Editor universale utilizzando la scheda **Invio** dell&#39;estensione **Modifica proprietà modulo**.

<!--**How to Configure Submit Action for Forms authored in Universal Editor?**
You can configure the submit action for forms created in the Universal Editor using the **Submission** tab of the **Edit Form Properties** extension.

![Form properties icon](/help/forms/assets/ue-form-properties-icon.png)

![Universal Editor Form Properties](/help/forms/assets/ue-form-properties.png)-->

>[!NOTE]
>
> * Se l&#39;icona **Modifica proprietà modulo** non è visibile nell&#39;interfaccia di Universal Editor, abilitare l&#39;estensione **Modifica proprietà modulo** in Extension Manager.
> * Per informazioni su come abilitare o disabilitare le estensioni nell&#39;editor universale, consulta l&#39;articolo [Caratteristiche principali di Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions).

## Azioni di invio per Forms basato su documenti

I Forms basati su documenti supportano l&#39;invio solo ai fogli di calcolo. Per informazioni su come impostare il foglio di calcolo per la ricezione dei dati inviati, vedere le istruzioni contenute nell&#39;articolo [Configurare i fogli di Google o i file di Microsoft Excel per iniziare ad accettare i dati](/help/edge/docs/forms/submit-forms.md).

## Consulta anche {#see-also}

{{af-submit-action}}

