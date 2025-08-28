---
title: Come configurare un’azione di invio per un modulo adattivo?
description: Un modulo adattivo fornisce più azioni di invio. Un’azione di invio definisce il modo in cui un modulo adattivo viene elaborato dopo l’invio. Puoi utilizzare le azioni di invio incorporate o crearne di personalizzate.
keywords: come selezionare l’azione di invio per un modulo adattivo, collegare un modulo adattivo a un elenco di sharepoint, collegare un modulo adattivo a una libreria di documenti di sharepoint, collegare un modulo adattivo a un modello dati modulo (FDM)
feature: Adaptive Forms, Edge Delivery Services
role: User, Developer
exl-id: beee9be7-8215-496b-9fb9-61fba000a055
source-git-commit: bf35f847f6f00d21915dfedb10cf38ea74344988
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 100%

---

# Azione di invio per modulo adattivo

| Versione | Collegamento all’articolo |
|---------|-----------------------------|
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-submit-actions.html?lang=it) |
| AEM as a Cloud Service (componenti di base) | [Fai clic qui](/help/forms/configuring-submit-actions.md) |
| AEM as a Cloud Service (componenti core) | [Fai clic qui](/help/forms/configure-submit-actions-core-components.md) |
| AEM as a Cloud Service (Edge Delivery Services) | Questo articolo |


L’invio di un modulo è il passaggio finale critico nel percorso dell’utente, dove i dati raccolti vengono elaborati e vengono intraprese azioni. Questo documento fornisce una guida completa alla configurazione e alla gestione delle azioni di invio per moduli adattivi nell’editor universale.

## Che cosa imparerai

Alla fine di questo documento comprenderai come:

- Configurare diversi tipi di azioni di invio per i moduli
- Configurare gli invii di endpoint REST per l’integrazione con i sistemi esterni
- Configurare gli invii di e-mail per le risposte ai moduli
- Implementare azioni di invio personalizzate per esigenze aziendali specifiche
- Gestire gli scenari di errore e convalida del modulo durante l’invio

## Pubblico target

Questa guida è progettata per:

- **Sviluppatori di moduli** che implementano la logica di invio
- **Integratori di sistema** che collegano i moduli ai sistemi di back-end
- **Analisti ziendali** che definiscono i flussi di lavoro del modulo
- **Architetti tecnici** che progettano i processi di invio del modulo

## Azioni di invio per moduli creati nell’editor universale

Le seguenti azioni di invio sono supportate da [moduli adattivi creati nell’editor universale](/help/edge/docs/forms/universal-editor/create-forms.md):

- [Inviare e-mail](/help/forms/configure-submit-action-send-email.md)
- [Richiamare un flusso Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
- [Inviare a SharePoint](/help/forms/configure-submit-action-sharepoint.md)
- [Richiamare uno scenario Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
- [Inviare mediante il modello di dati modulo (FDM)](/help/forms/integrate-adaptive-form-with-fdm.md)
- [Inviare all’archiviazione Blob di Azure](/help/forms/configure-submit-action-azure-blob-storage.md)
- [Inviare all’endpoint REST](/help/forms/configure-submit-action-restpoint.md)
- [Inviare a OneDrive](/help/forms/configure-submit-action-onedrive.md)
- [Richiama un flusso di lavoro AEM](/help/forms/configure-submit-action-workflow.md)
- [Inviare a Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)
- [Inviare ad Adobe Experience Platform (AEP)](/help/forms/aem-forms-aep-connector.md)
- [Inviare al foglio di calcolo](/help/forms/forms-submission-service.md)

<!--You can also submit an Adaptive Form in the Universal Editor to other storage or CRM integrations:

* [Connect Adaptive Form to Salesforce](/help/forms/aem-forms-salesforce-integration.md)
* [Connect an Adaptive Form to Microsoft&reg; Dynamics OData](/help/forms/ms-dynamics-odata-configuration.md)-->

Puoi configurare l’azione di invio per i moduli creati nell’editor universale utilizzando la scheda **Invio** dell’estensione **Modifica le proprietà del modulo**.

**Come configurare l’azione di invio per i moduli creati nell’editor universale?**
Puoi configurare l’azione di invio per i moduli creati nell’editor universale utilizzando la scheda **Invio** dell’estensione **Modifica le proprietà del modulo**.

![Icona delle proprietà del modulo](/help/forms/assets/ue-form-properties-icon.png)

![Proprietà del modulo dell’editor universale](/help/forms/assets/ue-form-properties.png)

>[!NOTE]
>
> - Se non visualizzi l’icona **Modifica le proprietà del modulo** nell’interfaccia dell’editor universale, abilita l’estensione **Modifica le proprietà del modulo** in Extension Manager.
> - Per scoprire come abilitare e disabilitare le estensioni nell’editor universale, fai riferimento all’articolo [Caratteristiche principali delle funzioni di Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions).
