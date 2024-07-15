---
title: Come si salva un modulo adattivo basato su componente core come bozza?
description: Scopri come salvare un modulo adattivo basato su componenti core come bozza, creare un portale Forms e utilizzare i componenti core predefiniti in una pagina AEM Sites.
feature: Adaptive Forms, Core Components
exl-id: c0653bef-afeb-40c1-b131-7d87ca5542bc
role: User, Developer, Admin
source-git-commit: 52b87073cad84705b5dc0c6530aff44d1e686609
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 1%

---


# Salva modulo adattivo basato su componente core come bozza {#save-af-form}

Salvare un modulo adattivo come bozza è una funzione essenziale che migliora l’efficienza e la precisione dell’utente. Questa funzionalità consente agli utenti di salvare l’avanzamento e tornare per completare le attività in un secondo momento senza perdere le informazioni immesse. L&#39;opzione `save-as-draft` garantisce flessibilità nella gestione dei tempi, riduce il rischio di perdita di dati e mantiene la precisione delle richieste. È possibile salvare i moduli come bozze per completarli in un secondo momento.

## Considerazioni

* [Abilita i componenti core Adaptive Forms per il tuo ambiente.](/help/forms/enable-adaptive-forms-core-components.md)

* Verificare che il componente core [sia impostato sulla versione 3.0.24 o successiva](https://github.com/adobe/aem-core-forms-components) per utilizzare questa funzionalità.
* Assicurati di disporre di un account di archiviazione [Azure e di una chiave di accesso](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal) per autorizzare l&#39;accesso all&#39;account di archiviazione Azure.

## Salvare un modulo adattivo come bozza

L&#39;integrazione dei dati di [!DNL Experience Manager Forms] (data-integration.md) fornisce la configurazione dell&#39;archiviazione [!DNL Azure] per integrare i moduli con i servizi di archiviazione [!DNL Azure]. Il modello dati modulo può essere utilizzato per creare Forms adattivo che interagisce con il server [!DNL Azure] per abilitare i flussi di lavoro aziendali.

Per salvare il modulo come bozza, verificare di disporre di un account di archiviazione Azure e di una chiave di accesso per autorizzare l&#39;accesso all&#39;account di archiviazione [!DNL Azure]. Per salvare un modulo come bozza, effettuare le seguenti operazioni:

1. [Crea configurazione archiviazione Azure](#create-azure-storage-configuration)
1. [Configurare il connettore di archiviazione unificata per Forms Portal](#configure-usc-forms-portal)
1. [Creare una regola per salvare un modulo adattivo come bozza](#rule-to-save-adaptive-form-as-draft)


### 1. Creare la configurazione di archiviazione Azure {#create-azure-storage-configuration}

Una volta che si dispone di un account di archiviazione Azure e di una chiave di accesso per autorizzare l&#39;accesso all&#39;account di archiviazione [!DNL Azure], eseguire la procedura seguente per creare la configurazione di archiviazione Azure:

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Archiviazione Azure]**.

   ![Selezione scheda di archiviazione Azure](/help/forms/assets/save-form-as-draft-azure-card.png)

1. Selezionare una cartella di configurazione per creare la configurazione e selezionare **[!UICONTROL Crea]**.

   ![Seleziona cartella di configurazione archiviazione di Azure](/help/forms/assets/save-form-as-draft-select-config-folder.png)

1. Specifica un titolo per la configurazione nel campo **[!UICONTROL Titolo]**.
1. Specificare il nome dell&#39;account di archiviazione [!DNL Azure] nei campi **[!UICONTROL Account di archiviazione Azure]** e **[!UICONTROL Chiave di accesso Azure]**.

   ![Configurazione archiviazione Azure](/help/forms/assets/save-form-as-draft-azure-storage.png)

1. Fai clic su **Salva**.

>[!NOTE]
>
> È possibile recuperare l&#39;**[!UICONTROL account di archiviazione Azure]** e la **[!UICONTROL chiave di accesso Azure]** dal [portale Microsoft Azure](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal).


### 2. Configurare il connettore di archiviazione unificata per Forms Portal {#configure-usc-forms-portal}

Dopo aver creato la configurazione di archiviazione di Azure, configurare il connettore di archiviazione unificata per Forms Portal, attenendosi alla procedura seguente:

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Forms]** > **[!UICONTROL Connettore di archiviazione unificata]**.

   ![Archiviazione connettore unificato](/help/forms/assets/save-form-as-draft-unified-connector.png)

1. Nella sezione **[!UICONTROL Forms Portal]**, selezionare **[!UICONTROL Azure]** dall&#39;elenco a discesa **[!UICONTROL Archiviazione]**.
1. Specificare il [percorso di configurazione per la configurazione di archiviazione Azure](#create-azure-storage-configuration) nel campo **[!UICONTROL Percorso configurazione di archiviazione]**.

   ![Impostazione archiviazione connettore unificato](/help/forms/assets/save-form-as-draft-unified-connector-storage.png)

1. Seleziona **[!UICONTROL Salva]**, quindi seleziona **[!UICONTROL Publish]** per pubblicare la configurazione.

### 3. Creare regole per salvare un modulo adattivo come bozza {#rule-to-save-adaptive-form-as-draft}

Per salvare un modulo come bozza, creare una regola **Salva modulo** in un componente modulo, ad esempio un pulsante. Quando si fa clic sul pulsante, la regola viene attivata e il modulo viene salvato come bozza. Per creare la regola **Salva modulo** in un componente pulsante, effettua le seguenti operazioni:

1. Nell’istanza Autore, apri un modulo adattivo in modalità di modifica.
1. Dal riquadro di sinistra, selezionare l&#39;icona ![Componenti](assets/components_icon.png) e trascinare il componente **[!UICONTROL Pulsante]** nel modulo.
1. Selezionare il componente **[!UICONTROL Button]**, quindi l&#39;icona ![Configura](assets/configure_icon.png).
1. Seleziona l&#39;icona **[!UICONTROL Modifica regole]** per aprire l&#39;editor di regole.
1. Seleziona **[!UICONTROL Crea]** per configurare e creare la regola.
1. Nella sezione **[!UICONTROL When]**, seleziona **is clicked** e nella sezione **[!UICONTROL Then]** seleziona l&#39;opzione **Save Form**.
1. Seleziona **[!UICONTROL Fine]** per salvare la regola.

![Crea regola per il pulsante](/help/forms/assets/save-form-as-drfat-create-rule.png)

Quando visualizzi l&#39;anteprima di un modulo adattivo, lo compili e fai clic sul pulsante **Salva modulo**, il modulo viene salvato come bozza per un utilizzo successivo.

## Componente Bozze e invii per elencare le bozze sulla pagina AEM Sites

AEM Forms fornisce il componente portale **Bozze e invii** pronto all&#39;uso per visualizzare i moduli salvati sulle pagine di AEM Sites. Il componente **Bozze e invii** mostra i moduli salvati come bozze per il completamento successivo e i moduli inviati. Questo componente offre un’esperienza personalizzata per qualsiasi utente connesso elencando le bozze e gli invii relativi al Forms adattivo creato dall’utente.

È possibile utilizzare i componenti predefiniti di Forms Portal per elencare le bozze dei moduli nella pagina di AEM Sites. Per utilizzare il componente portale **Bozze e invii**, effettua le seguenti operazioni:

1. [Abilita componente Forms Portal per bozze e invii](#enable-component)
2. [Pagina Aggiungi componenti Bozze e invii in AEM Sites](#Add-drafts-submissions-component)
3. [Configura componente Bozze e invii](#configure-drafts-submissions-component)

### 1. Abilitare il componente Forms Portal Bozze e invii{#enable-component}

Per abilitare il componente **[!UICONTROL Bozze e invii]** nel criterio del modello, effettuare le seguenti operazioni:

1. Apri la pagina AEM Sites in modalità **Modifica**.
1. Vai a **[!UICONTROL Informazioni pagina]** > **[!UICONTROL Modifica modello]**
   ![Modifica criterio modello](/help/forms/assets/save-form-as-draft-edit-template.png)

1. Fai clic sul **[!UICONTROL Criterio]** e seleziona la casella di controllo **[!UICONTROL Bozze e invii]** in **[Nome progetto archetipo AEM] - Forms and Communications Portal**.

   ![Selezione criteri](/help/forms/assets/save-form-as-draft-enable-policy.png)

1. Fai clic su **[!UICONTROL Fine]**.

Una volta abilitato il componente portale, puoi utilizzarlo nell’istanza di authoring della pagina AEM Sites.

### 2. Pagina Aggiungere il componente Bozze e invii di AEM Sites{#Add-drafts-submissions-component}

Puoi creare e personalizzare Forms Portal sui siti web creati con AEM aggiungendo e configurando i componenti del portale. Prima di utilizzare il componente [Bozze e invii nella pagina AEM Sites, assicurati che sia abilitato](#enable-component).

Per aggiungere un componente, trascina e rilascia il componente dal riquadro del componente **Bozze e invii** al contenitore di layout nella pagina, oppure seleziona l&#39;icona Aggiungi sul contenitore di layout e aggiungi il componente dalla finestra di dialogo **[!UICONTROL Inserisci nuovo componente]**.

![Aggiungi bozza e componente invio](/help/forms/assets/save-form-as-draft-add-dns.png)

### 3. Configurare il componente Bozze e invii {#configure-drafts-submissions-component}

Il componente **Bozze e invii** visualizza i moduli salvati come bozza per il completamento successivo e i moduli inviati. Per configurare **Bozze e invii**, effettuare le seguenti operazioni:
1. Seleziona il componente **Bozze e invii**.
1. Fare clic sull&#39;icona ![Configura](assets/configure_icon.png) per visualizzare la finestra di dialogo.
1. Nella finestra di dialogo **[!UICONTROL Bozze e invii]**, specifica quanto segue:
   * **Titolo** Per identificare un componente in una pagina Sites e per impostazione predefinita, il titolo viene visualizzato sopra il componente.
   * **Tipo**: per indicare il modulo come bozza o inviato.
   * **Layout**: per visualizzare le bozze degli elenchi o i moduli inviati in formato scheda o elenco.

   ![Proprietà dei componenti Bozza e Invio](/help/forms/assets/save-form-as-draft-dns-properties.png)

1. Fai clic su **Fine**.

Quando **[!UICONTROL Seleziona tipo]** è selezionato come **Bozza di Forms**, vengono visualizzati i moduli salvati come bozze:
![Icona Bozze](assets/drafts-component.png)

Quando **[!UICONTROL Seleziona tipo]** è selezionato come **Forms inviato**, vengono visualizzati i moduli inviati:

![Icona Invii](assets/submission-listing.png)

È possibile aprire il modulo facendo clic sul relativo modulo.

<!--

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

## Consulta anche {#see-also}

{{see-also}}



<!--

>[!MORELIKETHIS]
>
>* [Configure data sources for AEM Forms](/help/forms/configure-data-sources.md)
>* [Configure Azure storage for AEM Forms](/help/forms/configure-azure-storage.md)
>* [Integrate Microsoft Dynamics 365 and Salesforce with Adaptive Forms](/help/forms/configure-msdynamics-salesforce.md)

-->
