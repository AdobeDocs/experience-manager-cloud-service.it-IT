---
title: Come si salva un modulo adattivo basato su componente core come bozza?
description: Scopri come salvare un modulo adattivo basato su componenti core come bozza, creare un portale Forms e utilizzare i componenti core predefiniti in una pagina AEM Sites.
feature: Adaptive Forms, Core Components
exl-id: c0653bef-afeb-40c1-b131-7d87ca5542bc
role: User, Developer, Admin
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 2%

---

<span class="preview"> Questo articolo contiene contenuti per la funzione pre-release. La funzione di pre-release è accessibile solo tramite [canale preliminare](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=it#new-features).

# Salva modulo adattivo basato su componente core come bozza {#save-af-form}

Salvare un modulo adattivo come bozza è una funzione essenziale che migliora l’efficienza e la precisione dell’utente. Questa funzionalità consente agli utenti di salvare l’avanzamento e tornare per completare le attività in un secondo momento senza perdere le informazioni immesse. Fornire un  `save-as-draft` garantisce flessibilità nella gestione dei tempi, riduce il rischio di perdita di dati e mantiene la precisione delle richieste. È possibile salvare i moduli come bozze per completarli in un secondo momento.

## Considerazioni

* [Abilita i componenti core Adaptive Forms per il tuo ambiente.](/help/forms/enable-adaptive-forms-core-components.md)

* Assicurati che [Componente core impostato su versione 3.0.24 o successiva](https://github.com/adobe/aem-core-forms-components) per utilizzare questa funzione.
* Assicurati di disporre di [Account di archiviazione Azure e chiave di accesso](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal) per autorizzare l’accesso all’account di archiviazione Azure.

## Salvare un modulo adattivo come bozza

[!DNL Experience Manager Forms] Data Integration (data-integration.md) fornisce [!DNL Azure] configurazione di archiviazione per integrare forms con [!DNL Azure] servizi di storage. Il Modello dati modulo (FDM) può essere utilizzato per creare Forms adattivi che interagiscono con [!DNL Azure] per abilitare i flussi di lavoro aziendali.

Per salvare il modulo come bozza, assicurati di disporre di un account di archiviazione Azure e di una chiave di accesso per autorizzare l’accesso a [!DNL Azure] account di archiviazione. Per salvare un modulo come bozza, effettuare le seguenti operazioni:

1. [Crea configurazione archiviazione Azure](#create-azure-storage-configuration)
1. [Configurare il connettore di archiviazione unificata per Forms Portal](#configure-usc-forms-portal)
1. [Creare una regola per salvare un modulo adattivo come bozza](#rule-to-save-adaptive-form-as-draft)


### 1. Creare la configurazione di archiviazione Azure {#create-azure-storage-configuration}

Una volta, si dispone di un account di archiviazione Azure e di una chiave di accesso per autorizzare l’accesso a [!DNL Azure] account di archiviazione, eseguire la procedura seguente per creare la configurazione di archiviazione Azure:

1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Archiviazione Azure]**.

   ![Selezione scheda di archiviazione Azure](/help/forms/assets/save-form-as-draft-azure-card.png)

1. Seleziona una cartella di configurazione per creare la configurazione e seleziona **[!UICONTROL Crea]**.

   ![Seleziona cartella di configurazione archiviazione di Azure](/help/forms/assets/save-form-as-draft-select-config-folder.png)

1. Specifica un titolo per la configurazione nella **[!UICONTROL Titolo]** campo.
1. Specifica il nome del [!DNL Azure] account di archiviazione in **[!UICONTROL Account di archiviazione Azure]** e **[!UICONTROL Chiave di accesso Azure]** campi.

   ![Configurazione archiviazione Azure](/help/forms/assets/save-form-as-draft-azure-storage.png)

1. Fai clic su **Salva**.

>[!NOTE]
>
> È possibile recuperare **[!UICONTROL Account di archiviazione Azure]** e **[!UICONTROL Chiave di accesso Azure]** dal [Portale Microsoft Azure](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal).


### 2. Configurare il connettore di archiviazione unificata per Forms Portal {#configure-usc-forms-portal}

Dopo aver creato la configurazione di archiviazione di Azure, configurare il connettore di archiviazione unificata per Forms Portal, attenendosi alla procedura seguente:

1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Forms]** > **[!UICONTROL Connettore di archiviazione unificata]**.

   ![Archiviazione connettore unificato](/help/forms/assets/save-form-as-draft-unified-connector.png)

1. In **[!UICONTROL Forms Portal]** sezione, seleziona **[!UICONTROL Azure]** dal **[!UICONTROL Storage]** elenco a discesa.
1. Specifica la [percorso di configurazione per la configurazione dell’archiviazione Azure](#create-azure-storage-configuration) nel **[!UICONTROL Percorso configurazione archiviazione]** campo.

   ![Impostazione di memorizzazione del connettore unificato](/help/forms/assets/save-form-as-draft-unified-connector-storage.png)

1. Seleziona **[!UICONTROL Salva]** e quindi seleziona **[!UICONTROL Publish]** per pubblicare la configurazione.

### 3. Creare regole per salvare un modulo adattivo come bozza {#rule-to-save-adaptive-form-as-draft}

Per salvare un modulo come bozza, creare un **Salva modulo** su un componente modulo, ad esempio un pulsante. Quando si fa clic sul pulsante, la regola viene attivata e il modulo viene salvato come bozza. Per creare, effettua le seguenti operazioni **Salva modulo** regola su un componente pulsante:

1. Nell’istanza Autore, apri un modulo adattivo in modalità di modifica.
1. Dal riquadro a sinistra, seleziona ![Icona Componenti](assets/components_icon.png) e trascina **[!UICONTROL Pulsante]** al modulo.
1. Seleziona la **[!UICONTROL Pulsante]** e quindi selezionare il ![Icona Configura](assets/configure_icon.png).
1. Seleziona la **[!UICONTROL Modifica regole]** per aprire l&#39;editor di regole.
1. Seleziona **[!UICONTROL Crea]** per configurare e creare la regola.
1. In **[!UICONTROL Quando]** sezione, seleziona **ha fatto clic su** e nella **[!UICONTROL Then]** , seleziona la sezione **Salva modulo** opzione.
1. Seleziona **[!UICONTROL Fine]** per salvare la regola.

![Crea regola per pulsante](/help/forms/assets/save-form-as-drfat-create-rule.png)

Quando visualizzi l’anteprima di un modulo adattivo, compilalo e fai clic su **Salva modulo** , il modulo viene salvato come bozza per un utilizzo successivo.

## Componente Bozze e invii per elencare le bozze sulla pagina AEM Sites

AEM Forms fornisce **Bozze e invii** componente portale pronto all’uso per visualizzare i moduli salvati sulle pagine AEM Sites. Il **Bozze e invii** Il componente mostra i moduli salvati come bozze da completare in un secondo momento, nonché i moduli inviati. Questo componente offre un’esperienza personalizzata per qualsiasi utente connesso elencando le bozze e gli invii relativi al Forms adattivo creato dall’utente.

È possibile utilizzare i componenti predefiniti di Forms Portal per elencare le bozze dei moduli nella pagina di AEM Sites. Per utilizzare il **Bozze e invii** componente portale:

1. [Abilita componente Forms Portal per bozze e invii](#enable-component)
2. [Pagina Aggiungi componenti Bozze e invii in AEM Sites](#Add-drafts-submissions-component)
3. [Configura componente Bozze e invii](#configure-drafts-submissions-component)

### 1. Abilitare il componente Forms Portal Bozze e invii{#enable-component}

Per attivare **[!UICONTROL Bozze e invii]** nel criterio del modello, effettuare le seguenti operazioni:

1. Apri la pagina AEM Sites in un **Modifica** modalità.
1. Vai a **[!UICONTROL Informazioni pagina]** > **[!UICONTROL Modifica modello]**
   ![Modifica criterio modello](/help/forms/assets/save-form-as-draft-edit-template.png)

1. Fai clic su **[!UICONTROL Policy]** e seleziona la **[!UICONTROL Bozze e invii]**  casella di controllo sotto **[Nome progetto archetipo AEM] - Forms e portale delle comunicazioni**.

   ![Selezione criteri](/help/forms/assets/save-form-as-draft-enable-policy.png)

1. Fai clic su **[!UICONTROL Fine]**.

Una volta abilitato il componente portale, puoi utilizzarlo nell’istanza di authoring della pagina AEM Sites.

### 2. Pagina Aggiungere il componente Bozze e invii di AEM Sites{#Add-drafts-submissions-component}

Puoi creare e personalizzare Forms Portal sui siti web creati con AEM aggiungendo e configurando i componenti del portale. Assicurati che [Il componente Bozze e invii è abilitato](#enable-component) prima di utilizzarli nella pagina AEM Sites.

Per aggiungere un componente, trascina e rilascia il componente dalla sezione **Bozze e invii** al contenitore di layout sulla pagina, oppure seleziona l’icona aggiungi sul contenitore di layout e aggiungi il componente dalla sezione **[!UICONTROL Inserisci nuovo componente]** .

![Aggiungi componente bozza e invio](/help/forms/assets/save-form-as-draft-add-dns.png)

### 3. Configurare il componente Bozze e invii {#configure-drafts-submissions-component}

Il **Bozze e invii** Nel componente vengono visualizzati i moduli salvati come bozza per il completamento successivo e i moduli inviati. Per configurare **Bozze e invii**, effettua le seguenti operazioni:
1. Seleziona la **Bozze e invii** componente.
1. Fai clic su ![Icona Configura](assets/configure_icon.png) e viene visualizzata la finestra di dialogo.
1. In **[!UICONTROL Bozze e invii]** , specificare quanto segue:
   * **Titolo** Per identificare un componente in una pagina Sites e per impostazione predefinita, il titolo viene visualizzato sopra il componente.
   * **Tipo**: per indicare l’elenco dei moduli come moduli bozza o inviati.
   * **Layout**: per visualizzare le bozze degli elenchi o i moduli inviati in formato scheda o elenco.

   ![Proprietà dei componenti Bozza e Invio](/help/forms/assets/save-form-as-draft-dns-properties.png)

1. Fai clic su **Fine**.

Quando **[!UICONTROL Seleziona tipo]** è selezionato come **Bozza di Forms**, vengono visualizzati i moduli salvati come bozze:
![Icona Bozze](assets/drafts-component.png)

Quando **[!UICONTROL Seleziona tipo]** è selezionato come **Forms inviato**, i moduli inviati vengono visualizzati:

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
