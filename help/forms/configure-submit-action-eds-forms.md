---
title: Come configurare un’azione di invio per un modulo adattivo?
description: Un modulo adattivo fornisce più azioni di invio. Un’azione di invio definisce il modo in cui un modulo adattivo viene elaborato dopo l’invio. Puoi utilizzare le azioni di invio incorporate o crearne di personalizzate.
keywords: come selezionare l’azione di invio per un modulo adattivo, collegare un modulo adattivo a un elenco di sharepoint, collegare un modulo adattivo a una libreria di documenti di sharepoint, collegare un modulo adattivo a un modello dati modulo (FDM)
feature: Adaptive Forms, Edge Delivery Services
role: User, Developer
badgeSaas: label="AEM Forms" type="Positive" tooltip="Si applica ad AEM Forms)."
exl-id: 3f8950c3-9022-4e9f-b3ed-723245201e45
source-git-commit: fa8035f826a4d08c18bc0d2b7664015c6fc82698
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 66%

---

# Azioni di invio per Edge Delivery Services Forms

| Versione | Collegamento all’articolo |
|---------|-----------------------------|
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-submit-actions.html?lang=it) |
| AEM as a Cloud Service (componenti di base) | [Fai clic qui](/help/forms/configuring-submit-actions.md) |
| AEM as a Cloud Service (componenti core) | [Fai clic qui](/help/forms/configure-submit-actions-core-components.md) |
| AEM as a Cloud Service (Edge Delivery Services) | Questo articolo |

Le azioni di invio definiscono ciò che accade quando un utente invia un modulo, ad esempio l’archiviazione di dati, l’attivazione di flussi di lavoro o l’integrazione con sistemi di terze parti. Il tipo di azioni di invio che è possibile configurare dipende dal metodo di creazione utilizzato per creare Edge Delivery Services Forms.

È possibile creare Edge Delivery Services Forms utilizzando [Universal Editor](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) o l&#39;authoring di [Document Based Forms](/help/edge/docs/forms/overview.md) e configurare di conseguenza i moduli con azioni di invio diverse.

## Azioni di invio per moduli creati nell’editor universale

Le seguenti azioni di invio sono supportate da [moduli adattivi creati nell’editor universale](/help/edge/docs/forms/universal-editor/create-forms.md):

* [Inviare e-mail](/help/forms/configure-submit-action-send-email.md)
* [Richiamare un flusso Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
* [Inviare a SharePoint](/help/forms/configure-submit-action-sharepoint.md)
* [Richiamare uno scenario Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
* [Inviare mediante un modello dati modulo (FDM)](/help/forms/integrate-adaptive-form-with-fdm.md)
* [Inviare all’archiviazione Blob di Azure](/help/forms/configure-submit-action-azure-blob-storage.md)
* [Inviare all’endpoint REST](/help/forms/configure-submit-action-restpoint.md)
* [Inviare a OneDrive](/help/forms/configure-submit-action-onedrive.md)
* [Richiama un flusso di lavoro AEM](/help/forms/configure-submit-action-workflow.md)
* [Inviare a Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)
* [Inviare ad Adobe Experience Platform (AEP)](/help/forms/aem-forms-aep-connector.md)
* [Inviare al foglio di calcolo](/help/forms/forms-submission-service.md)

<!--
You can also submit an Adaptive Form in the Universal Editor to other storage or CRM integrations:

* [Connect Adaptive Form to Salesforce](/help/forms/aem-forms-salesforce-integration.md)
* [Connect an Adaptive Form to Microsoft&reg; Dynamics OData](/help/forms/ms-dynamics-odata-configuration.md)
-->

Puoi configurare l’azione di invio per i moduli creati nell’editor universale utilizzando la scheda **Invio** dell’estensione **Modifica le proprietà del modulo**.

<!--
**How to Configure Submit Action for Forms authored in Universal Editor?**
You can configure the submit action for forms created in the Universal Editor using the **Submission** tab of the **Edit Form Properties** extension.

![Form properties icon](/help/forms/assets/ue-form-properties-icon.png)

![Universal Editor Form Properties](/help/forms/assets/ue-form-properties.png)
-->

>[!NOTE]
>
> * Se non visualizzi l’icona **Modifica le proprietà del modulo** nell’interfaccia dell’editor universale, abilita l’estensione **Modifica le proprietà del modulo** in Extension Manager.
> * Per scoprire come abilitare e disabilitare le estensioni nell’editor universale, fai riferimento all’articolo [Caratteristiche principali delle funzioni di Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions).

## Azioni di invio per Forms basato su documenti

I Forms basati su documenti supportano l&#39;invio solo ai fogli di calcolo. Per informazioni su come impostare il foglio di calcolo per la ricezione dei dati inviati, vedere le istruzioni contenute nell&#39;articolo [Configurare i fogli di Google o i file di Microsoft Excel per iniziare ad accettare i dati](/help/edge/docs/forms/submit-forms.md).

## Consulta anche {#see-also}

{{af-submit-action}}
