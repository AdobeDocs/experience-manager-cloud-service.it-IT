---
title: Come si collega il modulo adattivo AEM all’elenco di Microsoft® SharePoint?
description: Collegare un modulo adattivo all’elenco di Microsoft® SharePoint. Scopri come configurare l’elenco Microsoft® SharePoint e creare un modello di dati del modulo utilizzando la configurazione. Scoprirai inoltre come integrare FDM con il modulo adattivo.
role: User, Developer
keywords: Collega Modulo adattivo AEM a Elenco Microsoft SharePoint, connetti Modulo adattivo a Elenco Microsoft SharePoint, integra Modulo adattivo AEM a Elenco Microsoft SharePoint, integra Modulo adattivo a Elenco Microsoft SharePoint, invia dati da un Modulo adattivo a Elenco SharePoint, invia flusso di lavoro di a Elenco AEM SharePoint.
hide: true
hidefromToC: true
source-git-commit: 397e7d4f23202b8ae7419b0ad5436a6a10e2efb8
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 3%

---


# Collegare un modulo adattivo all’elenco di Microsoft® SharePoint

<span class="preview"> Si tratta di una funzione pre-release accessibile tramite [canale preliminare](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features). </span>

**Microsoft® SharePoint**: Microsoft® SharePoint consente la collaborazione fornendo siti di team dinamici ed efficienti per tutti i team, i reparti e le divisioni. Viene utilizzato per memorizzare, organizzare, condividere e accedere alle informazioni da qualsiasi dispositivo utilizzando qualsiasi browser web, ad esempio Microsoft® Edge, Internet Explorer, Chrome o Firefox. I due componenti principali di **Microsoft® SharePoint** sono:

* **Libreria documenti Microsoft® SharePoint**: Raccolta documenti di Microsoft® SharePoint visualizza un elenco di file e cartelle con le relative informazioni chiave, ad esempio la data dell&#39;ultima modifica e il proprietario di un file. Questa funzione semplifica l&#39;organizzazione e la navigazione dei file.
Per istruzioni su come integrare un **Libreria documenti Microsoft® SharePoint** con un modulo adattivo, consulta [Azione di invio modulo adattivo](/help/forms/configuring-submit-actions.md#submit-to-sharepoint) articolo.

* **Elenco SharePoint Microsoft®**: Microsoft® SharePoint List è una raccolta di dati. Puoi aggiungere colonne per diversi tipi di dati e creare viste per visualizzare i dati in modo efficace. È possibile raggruppare, filtrare, ordinare e formattare facilmente gli elenchi.

>[!VIDEO](https://video.tv.adobe.com/v/3424820/connect-aem-adaptive-form-to-sharepointlist/?quality=12&learn=on)

## Prerequisiti per collegare un modulo adattivo a Microsoft® SharePoint List {#prerequisites}

Prima di collegare un modulo adattivo a Microsoft® SharePoint List, effettua le seguenti operazioni:

1. [Configura elenco SharePoint Microsoft®](/help/forms/configure-data-sources.md#configure-microsoft-sharepoint-list)
1. [Creare un modello dati modulo utilizzando la configurazione Elenco Microsoft® SharePoint](/help/forms/create-form-data-models.md)
1. [Configurare il modello dati modulo per recuperare e inviare dati](/help/forms/work-with-form-data-model.md#configure-services)
1. [Creare un modulo adattivo](/help/forms/creating-adaptive-form-core-components.md)

Ora è possibile:

* [Connettere Microsoft® SharePoint List a un modulo adattivo](#connect-an-adaptive-form-to-microsoft-sharepoint-list-connect-af-sharepoint-list)
* [Collegare Microsoft® SharePoint List a un flusso di lavoro AEM](#connect-sharepoint-list-workflow)

## Collegare un modulo adattivo all’elenco di Microsoft® SharePoint {#connect-af-sharepoint-list}

Integrare Microsoft® SharePoint List nel modulo adattivo [configurare un modulo adattivo per l’utilizzo di un modello dati modulo](/help/forms/creating-adaptive-form-core-components.md#configure-a-schema-or-form-data-model-for-an-adaptive-formconfigure-schema-or-data-model-for-form)

Dopo aver configurato un modulo adattivo per l’utilizzo di un modello dati modulo, puoi:

* [Configurare l’azione di invio utilizzando un modello dati modulo](/help/forms/configuring-submit-actions.md#submit-using-form-data-model)
* [Configurare l’editor di regole per richiamare un modello dati modulo](/help/forms/rule-editor.md#invoke-form-data-model-service-invoke)

## Collegare Microsoft® SharePoint List a un flusso di lavoro AEM {#connect-sharepoint-list-workflow}

Per integrare Microsoft® SharePoint List in un flusso di lavoro AEM:

1. [Creare un flusso di lavoro per richiamare un modello dati modulo](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=it)

   <!--
    To create a new workflow with the editor, perform the following steps:
    1.  Go to your **AEM Forms Author** instance > **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
    1.  Click **[!UICONTROL Create]** > **[!UICONTROL Create Model]**. The Add Workflow Model dialog appears. 
    1. Specify **[!UICONTROL Title]** and **[!UICONTROL Name (optional)]**.
    1. Click **[!UICONTROL Done]**. The new model is listed in the Workflow Models console.
    1. Select your new workflow, then use **[!UICONTROL Edit]** to open it for configuration.
    1. Add **[!UICONTROL Invoke Form Data Model Service]** step to your workflow.
    1. Confirm the changes with Sync (editor toolbar) to generate the runtime model.
    -->

1. [Configurare l’azione di invio per richiamare un flusso di lavoro AEM](/help/forms/configuring-submit-actions.md#invoke-an-aem-workflow)


Scopri come [utilizzare il flusso di lavoro AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/workflow/use-workflow.html) collaborare, gestire ed elaborare contenuti in un modulo adattivo.

## Best practice {#best-practices}

<!-- * For storing data in a tabular format or implementing data permissions, it is advisable to use Microsoft® SharePoint List rather than Microsoft® SharePoint Document Library. -->
* In Microsoft® SharePoint List non sono supportati i seguenti tipi di colonna:
   * colonna immagine
   * colonna metadati
   * colonna persona
   * colonna di dati esterni

## Consulta anche {#see-also}

* [Creare un modulo adattivo basato su componenti core](/help/forms/creating-adaptive-form-core-components.md)
* [Configurare origini dati](/help/forms/configuring-submit-actions.md)
* [Crea modello dati modulo](/help/forms/create-form-data-models.md)
* [Utilizzare flussi di lavoro AEM incentrati su Forms - Riferimento alla fase per automatizzare i processi aziendali](/help/forms/aem-forms-workflow-step-reference.md)
* [Creare un’azione di invio personalizzata per Adaptive Forms](/help/forms/custom-submit-action-form.md)
* [Creare o aggiungere un modulo adattivo a una pagina di AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Incorporare un modulo adattivo in una pagina AEM Sites](/help/forms/embed-adaptive-form-aem-sites.md)
* [Creare, utilizzare e personalizzare i temi in un modulo adattivo](/help/forms/using-themes-in-core-components.md)







