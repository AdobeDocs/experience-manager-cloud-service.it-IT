---
title: Come si configura un’azione di invio per un modulo adattivo?
description: Un modulo adattivo fornisce più azioni di invio. Un’azione di invio definisce il modo in cui un modulo adattivo viene elaborato dopo l’invio. Puoi utilizzare le azioni di invio integrate o crearne di personalizzate.
keywords: come selezionare l’azione di invio per un modulo adattivo, collegare un modulo adattivo a un elenco di sharepoint, collegare un modulo adattivo a una raccolta documenti di sharepoint, collegare un modulo adattivo a un modello di dati modulo (FDM)
feature: Adaptive Forms, Edge Delivery Services
role: User, Developer
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 39%

---

# Azione di invio per modulo adattivo

| Versione | Collegamento articolo |
|---------|-----------------------------|
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/configuring-submit-actions.html) |
| AEM as a Cloud Service (Componenti di base) | [Fai clic qui](/help/forms/configuring-submit-actions.md) |
| AEM as a Cloud Service (Componenti core) | [Fai clic qui](/help/forms/configure-submit-actions-core-components.md) |
| AEM as a Cloud Service (Edge Delivery Services) | Questo articolo |


L’invio di un modulo è il passaggio finale critico nel percorso dell’utente, dove i dati raccolti vengono elaborati e vengono intraprese azioni. Questo documento fornisce una guida completa alla configurazione e alla gestione delle azioni di invio per moduli adattivi nell’editor universale.

### Che cosa imparerai

Alla fine di questo documento comprenderai come:

- Configurare diversi tipi di azioni di invio per i moduli
- Configurare gli invii di endpoint REST per l’integrazione con i sistemi esterni
- Configurare gli invii di e-mail per le risposte ai moduli
- Implementare azioni di invio personalizzate per esigenze aziendali specifiche
- Gestire gli scenari di errore e convalida del modulo durante l’invio

### Pubblico target

Questa guida è progettata per:

- **Sviluppatori di moduli** che implementano la logica di invio
- **Integratori di sistema** che collegano i moduli ai sistemi di back-end
- **Analisti ziendali** che definiscono i flussi di lavoro del modulo
- **Architetti tecnici** che progettano i processi di invio del modulo

## Azioni di invio per Forms create in Universal Editor

Le seguenti azioni di invio sono supportate da [Forms adattivo creato nell&#39;editor universale](/help/edge/docs/forms/universal-editor/create-forms.md):

- [Invia e-mail](/help/forms/configure-submit-action-send-email.md)
- [Richiama un flusso Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
- [Invia a SharePoint](/help/forms/configure-submit-action-sharepoint.md)
- [Richiama Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
- [Inviare mediante il modello di dati modulo (FDM)](/help/forms/integrate-adaptive-form-with-fdm.md)
- [Inviare ad Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md)
- [Invia all’endpoint REST](/help/forms/configure-submit-action-restpoint.md)
- [Invia a OneDrive](/help/forms/configure-submit-action-onedrive.md)
- [Richiama un flusso di lavoro AEM](/help/forms/configure-submit-action-workflow.md)
- [Invia a Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)
- [Invia a Adobe Experience Platform (AEP)](/help/forms/aem-forms-aep-connector.md)
- [Invia a foglio di calcolo](/help/forms/forms-submission-service.md)

<!--You can also submit an Adaptive Form in the Universal Editor to other storage or CRM integrations:

* [Connect Adaptive Form to Salesforce](/help/forms/aem-forms-salesforce-integration.md)
* [Connect an Adaptive Form to Microsoft&reg; Dynamics OData](/help/forms/ms-dynamics-odata-configuration.md)-->

È possibile configurare l&#39;azione di invio per i moduli creati nell&#39;Editor universale utilizzando la scheda **Invio** dell&#39;estensione **Modifica proprietà modulo**.

**Come configurare l&#39;azione di invio per Forms creato in Universal Editor?**
Puoi configurare l&#39;azione di invio per i moduli creati nell&#39;Editor universale utilizzando la scheda **Invio** dell&#39;estensione **Modifica proprietà modulo**.

![Icona proprietà modulo](/help/forms/assets/ue-form-properties-icon.png)

![Proprietà modulo editor universale](/help/forms/assets/ue-form-properties.png)

>[!NOTE]
>
> - Se l&#39;icona **Modifica proprietà modulo** non è visibile nell&#39;interfaccia di Universal Editor, abilitare l&#39;estensione **Modifica proprietà modulo** in Extension Manager.
> - Per informazioni su come abilitare o disabilitare le estensioni nell&#39;editor universale, consulta l&#39;articolo [Caratteristiche principali di Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions).



