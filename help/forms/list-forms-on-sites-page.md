---
title: Come si elencano i moduli su una pagina di Adobe Experience Manager Sites utilizzando il componente Forms Portal?
description: Scopri come elencare i moduli su una pagina AEM Sites.
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: 37e3ddd9-b20d-4156-b52e-64e36c455184
source-git-commit: 16b1e7ffa4e3812e9207bb283c63029939f7d14e
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 1%

---

# Elencare i moduli nella pagina Sites

Immaginate un utente che visita il sito web della banca alla ricerca di un modulo per l&#39;apertura di un conto. La banca utilizza il componente Forms Portal per aiutare gli utenti a trovare rapidamente il modulo inserendo parole chiave specifiche o filtrando per categorie quali &quot;Nuovi account&quot; o &quot;Personal Banking&quot; e consente agli utenti di individuare facilmente il modulo desiderato senza dover scorrere lunghi elenchi.

Il componente **Ricerca ed elenco** del portale Forms consente di visualizzare ed elencare i moduli in una pagina Sites. Gli utenti possono configurare e presentare un elenco completo di moduli basato su criteri specifici per soddisfare i requisiti organizzativi. Gli utenti anonimi possono visitare la pagina Sites per visualizzare e sfogliare i moduli disponibili. I moduli elencati possono essere ordinati in ordine crescente o decrescente utilizzando l&#39;opzione a discesa **Ordina per** nell&#39;angolo superiore destro dello schermo.

![Icona Ricerca ed elenco](assets/search-and-lister-component.png)

## Prerequisito

Prima di esplorare le varie funzionalità di un componente Forms Portal, accertati che i Componenti core siano abilitati per il tuo ambiente. Installa la versione più recente per abilitare i componenti core Adaptive Forms per il tuo ambiente AEM Cloud Service.

<!--
## Enable Forms Portal components for your existing environment

To enable out-of-the-box Forms Portal components on existing AEM Forms as a Cloud Service, perform the following steps:

1. **Clone Cloud Manager Git repository on your local development instance:**  Your Cloud Manager Git repository contains a default AEM project. It is based on [AEM Archetype](https://github.com/adobe/aem-project-archetype/). Clone your Cloud Manager Git Repository using Self-Service Git Account Management from Cloud Manager UI to bring the project on your local development environment. For details on accessing the repository, see [Accessing Repositories](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/accessing-repos.html).  

1. **Create [!DNL Experience Manager Forms] as a [Cloud Service] project:** Create [!DNL Experience Manager Forms] as a [Cloud Service] project based on [AEM Archetype 50](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-50) or later. The archetype help developers easily start developing for [!DNL AEM Forms] as a Cloud Service. It also includes some sample themes and templates to help you started quickly.

    To create [!DNL Experience Manager Forms] as a Cloud Service project, open the command prompt and run the below command. To include [!DNL Forms] specific configurations, themes, and templates, set `includeForms=y`.  

    ```shell
    mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=30 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
    ```

    Also, change `appTitle`, `appId`, and `groupId`, in the above command to reflect your environment.

    After the project is ready, update the `<core.forms.components.version>x.y.z</core.forms.components.version>` property in the top-level `pom.xml` of the Archetype project to reflect the latest version of [core-forms-components](https://github.com/adobe/aem-core-forms-components) in your `AEM Archetype` project. 
 
1. **Deploy the project to your local development environment:** You can use the following command to deploy to your local development environment

    `mvn -PautoInstallPackage clean install`

    For the complete list of commands, see [Building and Installing](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#building-and-installing)

1. [Deploy the archetype to your [!DNL AEM Forms] as a Cloud Service environment](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html#embeddeds). -->

Dopo aver distribuito i Componenti core più recenti nell’ambiente, i componenti del portale Forms diventano accessibili nell’ambiente di authoring.

## Elencare moduli nella pagina Sites

Per aggiungere il componente del portale **Ricerca e elenco** alla pagina Sites, effettuare le seguenti operazioni:

1. Apri la pagina AEM Sites in modalità **Modifica**.
1. Vai a **[!UICONTROL Informazioni pagina]** > **[!UICONTROL Modifica modello]**
   ![Modifica criterio modello](/help/forms/assets/save-form-as-draft-edit-template.png)

1. Fai clic sul **[!UICONTROL Criterio]** e seleziona la casella di controllo **[!UICONTROL Ricerca ed elenco]** in **[Nome progetto Archetipo AEM] - Forms and Communications Portal**.

   ![Selezione criteri](/help/forms/assets/search-lister-enable-policy.png)

1. Fai clic su **[!UICONTROL Fine]**.
1. Ora riapri la pagina AEM Sites in modalità di authoring.
1. Nell’editor pagina, individua la sezione che consente di aggiungere il componente Forms Portal.

1. Fai clic sull&#39;icona **Aggiungi**. L’icona è un segno più (+) che indica l’opzione per aggiungere nuovi componenti.

   Facendo clic sull&#39;icona **Aggiungi** viene visualizzata una finestra di dialogo **Inserisci nuovo componente** in cui sono visualizzati vari componenti da inserire.

   >[!NOTE]
   >
   > In alternativa, puoi anche trascinare e rilasciare il componente.

1. Sfoglia i componenti disponibili nella finestra di dialogo e seleziona il componente desiderato dall’elenco. Selezionare ad esempio il componente **Ricerca ed elenco** dall&#39;elenco per aggiungere il componente **Ricerca ed elenco** di Forms Portal.

   ![Componente Ricerca ed elenco](/help/forms/assets/add-search-lister.png)

Ora configura le proprietà del componente **Ricerca ed elenco**.

## Comprendere le proprietà del componente Ricerca ed Elenco

Puoi personalizzare facilmente le proprietà dei componenti **Cerca ed Elenca** tramite la finestra di dialogo per configurazione per un&#39;esperienza utente ottimale. Per configurare, selezionare il componente, quindi selezionare l&#39;icona ![Configura](assets/configure_icon.png). Viene visualizzata la finestra di dialogo **[!UICONTROL Ricerca ed elenco]**.

### Scheda Visualizzazione

![Scheda Visualizzazione](/help/forms/assets/search-and-lister-display-tab.png)

1. In **[!UICONTROL Titolo]**, specificare il titolo del componente Ricerca ed elenco. Un titolo indicativo consente agli utenti di eseguire una ricerca rapida nell’elenco dei moduli.
1. Dall&#39;elenco **[!UICONTROL Layout]**, selezionare il layout per rappresentare i moduli nel formato scheda o elenco.
1. Seleziona **[!UICONTROL Nascondi ricerca]** e **[!UICONTROL Nascondi ordinamento]** per nascondere la ricerca e ordinare per funzionalità.
1. In **[!UICONTROL Descrizione]**, fornire la descrizione che viene visualizzata quando si passa il puntatore sul componente.

### Scheda Risorsa

![Scheda Risorsa](/help/forms/assets/search-and-lister-asset-tab.png)

1. Nella scheda **[!UICONTROL Cartella risorse]**, specifica il percorso da cui i moduli vengono estratti ed elencati nella pagina.
1. Utilizzando **[!UICONTROL Aggiungi un altro percorso]**, puoi configurare più percorsi cartella.

### Scheda Risultati

![Scheda Visualizzazione](/help/forms/assets/search-and-lister-result-tab.png)

Nella scheda **[!UICONTROL Risultati]**, configura il numero massimo di moduli da visualizzare per pagina. Il valore predefinito è otto moduli per pagina.

## Visualizzare i moduli nella pagina Sites utilizzando il componente Ricerca ed elenco

Per visualizzare l&#39;elenco dei moduli, utilizzare il componente **Ricerca e elenco** di Forms Portal. Visualizza l&#39;anteprima della pagina AEM Sites per visualizzare l&#39;elenco dei moduli della cartella **Assets** visualizzata sullo schermo. Puoi anche cercare un modulo specifico utilizzando la barra di ricerca.

![Icona Ricerca ed elenco](assets/search-and-lister-component.png)

<!--
## Configure Azure Storage for Adaptive Forms {#configure-azure-storage-adaptive-forms}

[[!DNL Experience Manager Forms] Data Integration](data-integration.md) provides [!DNL Azure] storage configuration to integrate forms with [!DNL Azure] storage services. The Form Data Model (FDM) can be used to create Adaptive Forms that interact with [!DNL Azure] server to enable business workflows.

### Create Azure Storage Configuration {#create-azure-storage-configuration}

Before executing these steps, ensure that you have an Azure storage account and an access key to authorize access to the [!DNL Azure] storage account.

1. Navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Cloud Services]** &gt; **[!UICONTROL Azure Storage]**.
1. Select a folder to create the configuration and select **[!UICONTROL Create]**.
1. Specify a title for the configuration in the **[!UICONTROL Title]** field.
1. Specify the name of the [!DNL Azure] storage account in the **[!UICONTROL Azure Storage Account]** field.

### Configure Unified Storage Connector for Forms Portal {#configure-usc-forms-portal}

Perform the following steps to configure Unified Storage Connector for AEM Workflows:

1. Navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Forms]** &gt; **[!UICONTROL Unified Storage Connector]**.
1. In the **[!UICONTROL Forms Portal]** section, select **[!UICONTROL Azure]** from the **[!UICONTROL Storage]** drop-down list.
1. Specify the [configuration path for the Azure storage configuration](#create-azure-storage-configuration) in the **[!UICONTROL Storage Configuration Path]** field.
1. Select **[!UICONTROL Publish]** and then select **[!UICONTROL Save]** to save the configuration.

## Enable Forms Portal Components {#enable-forms-portal-components}

To use any core component (including the out-of-the-box portal components) in an Adobe Experience Manager (AEM) site, you must create a proxy component and enable it for your site. For creating a proxy component and enabling portal components, see [Using Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html?lang=en#create-proxy-components). 

Once a portal component is enabled, you can use it in the author instance of your sites page.

## Add and Configure Forms Portal Components {#configure-forms-portal-components}

You can create and customize Forms Portal on websites authored using AEM by adding and configuring the portal components. Ensure that the [components are enabled](#enable-forms-portal-components) before using them in the Forms Portal.

To add a component, either drag and drop the component from the Components pane to the layout container on the page, or select the add icon on the layout container and add the component from the [!UICONTROL Insert New Component] dialog.

### Configure Drafts & Submissions Component {#configure-drafts-submissions-component}

The Drafts & Submissions component displays forms that are saved as draft for completing later and submitted forms. To configure, select the component and then select the ![Configure icon](assets/configure_icon.png). In the [!UICONTROL Drafts and Submissions] dialog, specify the title to indicate the form listing as draft or submitted forms. Also select whether the component should list draft forms or submitted forms in card or list format.

![Drafts icon](assets/drafts-component.png)

![Submissions icon](assets/submission-listing.png)

### Configure Search & Lister Component {#configure-search-lister-component}

The Search & Lister component is used to list adaptive forms on a page and to implement search on the listed forms. 

![Search and Lister icon](assets/search-and-lister-component.png)

To configure, select the component and then select the ![Configure icon](assets/configure_icon.png). The [!UICONTROL Search and Lister] dialog opens.

1. In the [!UICONTROL Display] tab, configure the following:
    * In **[!UICONTROL Title]**, specify the title for the Search & Lister component. An indicative title enables the users perform quick search across the list of forms.
    * From the **[!UICONTROL Layout]** list, select the layout to represent the forms in card or list format.
    * Select **[!UICONTROL Hide Search]** and **[!UICONTROL Hide Sorting]** to hide the search and sort by features.
    * In **[!UICONTROL Tooltip]**, provide the tooltip that appears when you hover over the component. 
1. In the [!UICONTROL Asset Folder] tab, specify the location from where the forms are pulled and listed on the page. You can configure multiple folder locations.
1. In the [!UICONTROL Results] tab, configure the maximum number of forms to display per page. The default is eight forms per page.

### Configure Link Component {#configure-link-component}

The link component enables you to provide links to an adaptive form on the page. To configure, select the component and then select the ![Configure icon](assets/configure_icon.png). The [!UICONTROL Edit Link Component] dialog opens.

1. In the [!UICONTROL Display] tab, provide the link caption and tooltip to ease identification of the forms represented by the link.
1. In the [!UICONTROL Asset Info] tab, specify the repository path where the asset is stored. 
1. In the [!UICONTROL Query Params] tab, specify the additional parameters in the key-value pair format. When the link is clicked, these additional parameters and passed along with the form.

## Configure Asynchronous Form Submission Using Adobe Sign {#configure-asynchronous-form-submission-using-adobe-sign}

You can configure to submit an adaptive form only when all the recipients have completed the signing ceremony. Follow the steps below to configure the setting using Adobe Sign.

1. In the author instance, open an Adaptive Form in the edit mode.
1. From the left pane, select the Properties icon and expand the **[!UICONTROL ELECTRONIC SIGNTATURE]** option.
1. Select **[!UICONTROL Enable Adobe Sign]**. Various configuration options display. 
1. In the [!UICONTROL Submit the form] section, select the **[!UICONTROL after every recipient completes signing ceremony]** option to configure the Submit Form action, where the form is first sent to all the recipients for signing. Once all the recipients have signed the form, only then the form is submitted. 

## Save Adaptive Forms As Drafts {#save-adaptive-forms-as-drafts}

You can save forms as Drafts for completing them later. There are two ways in which a form is saved as a draft:

* Create a "Save Form" rule on a form component, for example, a button. On clicking the button, the rule triggers and the form are saved a draft.
* Enable Auto-Save feature, which saves the form as per the specified event or after a configured interval of time.

### Create Rules to Save an Adaptive Form as Draft {#rule-to-save-adaptive-form-as-draft}

To create a "Save Form" rule on a form component, for example, a button, follow the steps below:

1. In the author instance, open an Adaptive Form in edit mode.
1. From the left pane, select ![Components icon](assets/components_icon.png) and drag the [!UICONTROL Button] component to the form.
1. Select the [!UICONTROL Button] component and then select the ![Configure icon](assets/configure_icon.png). 
1. Select the [!UICONTROL Edit Rules] icon to open the Rule Editor. 
1. Select **[!UICONTROL Create]** to configure and create the rule.
1. In the [!UICONTROL When] section, select "is clicked" and in the [!UICONTROL Then] section, select the "Save Form" options.
1. Select **[!UICONTROL Done]** to save the rule.

### Enable Auto-save {#enable-auto-save}

You can configure the auto-save feature for an adaptive form as follows:

1. In the author instance, open an Adaptive Form in edit mode.
1. From the left pane, select the ![Properties icon](assets/configure_icon.png) and expand the [!UICONTROL AUTO-SAVE] option.
1. Select the **[!UICONTROL Enable]** check box to enable auto-save of the form. You can configure the following:
* By default, the [!UICONTROL Adaptive Form Event] is set to "true", which implies that the form is auto-saved after every event.
* In [!UICONTROL Trigger], configure to trigger auto-save based on the occurrence of an event or after a specific interval of time.
-->


## Passaggi successivi

Nel prossimo articolo, verrà illustrato [come salvare i moduli come bozze e elencarli in una pagina di Sites utilizzando il componente Forms Portal Bozze e invii](/help/forms/save-core-component-based-form-as-draft.md).

## Articoli correlati

{{forms-portal-see-also}}

## Consulta anche {#see-also}

{{see-also}}
