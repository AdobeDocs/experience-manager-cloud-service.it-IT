---
title: Come importare, esportare e organizzare Adaptive Forms o PDF forms in un’istanza di AEM Forms?
description: Scopri come migrare Forms adattivo, PDF forms, temi e altre risorse di supporto da e verso le istanze di AEM.
topic-tags: forms-manager
role: Admin, User
feature: Adaptive Forms
exl-id: f5105fb7-b8c0-4656-8095-b21d392746c0
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 3%

---

# Importare o esportare risorse Adaptive Forms e AEM Forms {#importing-and-exporting-assets-to-aem-forms}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/manage-administer-aem-forms/import-export-forms-templates) |
| AEM as a Cloud Service | Questo articolo |

È possibile spostare tra [!DNL AEM Forms] istanze Forms adattivo e risorse correlate, ad esempio temi di moduli adattivi, modello dati modulo (FDM), modelli di moduli adattivi, frammenti e PDF forms.

## Scaricare Forms adattivo, PDF forms o risorse correlate {#download-forms-amp-documents-assets}

Per scaricare i moduli o le risorse correlate:

1. Accedi all&#39;istanza [!DNL Experience Manager Forms].
1. Selezionare **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.

   ![Seleziona Forms](/help/forms/assets/select-forms.png)

1. Seleziona le risorse e fai clic sull&#39;icona **[!UICONTROL Scarica]** nella barra superiore.

   ![Scarica Forms](/help/forms/assets/download-form.png)

   Quando si scarica il modulo, viene visualizzata la finestra di dialogo **[!UICONTROL Scarica risorse]**.

   ![Scarica risorse moduli](/help/forms/assets/download-form-assets.png)

1. Fai clic su **[!UICONTROL Scarica]**.

Le risorse selezionate vengono scaricate come archivio (file .zip).

## Caricare Forms adattivo, PDF forms o risorse correlate {#upload-forms-amp-documents-assets}

Puoi caricare i tipi di risorse supportati singolarmente o come archivio ZIP. Per un file ZIP, vengono visualizzati i percorsi relativi di tutte le risorse supportate. Le risorse non supportate nel file ZIP vengono ignorate e non elencate. Tuttavia, se l’archivio ZIP contiene solo le risorse non supportate, viene visualizzato un messaggio di errore al posto della finestra di dialogo a comparsa.
Per caricare un modulo o una risorsa correlata:

1. Accedi all&#39;istanza [!DNL Experience Manager Forms].
1. Selezionare **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.

   ![Seleziona Forms](/help/forms/assets/select-forms.png)

1. Selezionare **[!UICONTROL Crea]** > **[!UICONTROL Caricamento file]**. Viene visualizzata una finestra di dialogo.

   ![Carica Forms](/help/forms/assets/form-upload.png)

1. Nella finestra di dialogo, sfoglia e seleziona il pacchetto o l’archivio da importare. Puoi anche selezionare altri tipi di file supportati. Seleziona **[!UICONTROL Apri]**. La cartella o il nome del file selezionato non deve contenere caratteri speciali.

   Nella finestra di dialogo, verifica i dettagli delle risorse caricate e seleziona **[!UICONTROL Carica]**.

   Se carichi una risorsa Forms esistente, la risorsa viene aggiornata.

   >[!NOTE]
   >
   > Quando un nome è in conflitto con tipi di risorse diversi, il caricamento di un pacchetto non sostituisce la gerarchia di cartelle esistente. Ad esempio, se disponi di un modulo adattivo denominato &quot;Training&quot; nella posizione `/content/dam/formsanddocuments` su un server. Puoi scaricare il modulo adattivo e caricarlo su un altro server. Nel secondo server è presente anche una cartella denominata &quot;Training&quot; nella stessa posizione `/content/dam/formsanddocuments`. Caricamento non riuscito.

## Scaricare un tema

È possibile esportare i temi in [!DNL AEM Forms] che è possibile utilizzare in altri progetti o istanze. AEM ti consente di scaricare i temi come file zip, che puoi caricare sull’istanza.
Per scaricare un tema:

1. Accedi all’istanza di authoring [!DNL Experience Manager Forms].
1. Seleziona **[!UICONTROL Forms]** > **[!UICONTROL Temi]**.

   ![Seleziona tema](/help/forms/assets/select-theme.png)

1. Nella pagina Temi, seleziona il tema e fai clic sull&#39;icona **[!UICONTROL Scarica]** nella barra superiore.

   ![Scarica tema](/help/forms/assets/download-theme.png)

   Quando si scarica il tema, viene visualizzata la finestra di dialogo **[!UICONTROL Scarica risorse]**.

   ![Scarica risorse tema](/help/forms/assets/download-theme-asset.png)

1. Fai clic su **[!UICONTROL Scarica]**.

Le risorse selezionate vengono scaricate come archivio (file .zip).

## Carica un tema {#uploading-a-theme}

È possibile caricare e utilizzare i temi creati da altri utenti nei moduli.
Per caricare un tema:

1. Accedi all&#39;istanza [!DNL Experience Manager Forms].
1. In Experience Manager, passa a **[!UICONTROL Forms]** > **[!UICONTROL Temi]**.

   ![Seleziona tema](/help/forms/assets/select-theme.png)

1. Nella pagina Temi fare clic su **[!UICONTROL Crea]** > **[!UICONTROL Caricamento file]**.

   ![Carica tema](/help/forms/assets/theme-upload.png)

1. Sfoglia e seleziona un pacchetto tema nel computer e fai clic su **[!UICONTROL Carica]**. Il tema caricato diventa disponibile nella pagina Temi.

## Utilizzare le cartelle per organizzare Forms adattivo, PDF forms e le risorse correlate  {#folders-and-organizing-assets}

Puoi utilizzare le cartelle per organizzare e disporre le risorse. L’organizzazione di documenti e risorse in una cartella consente di raggruppare i file per semplificarne la gestione. Puoi selezionare una cartella e scegliere se scaricarla o eliminarla.

### Crea una cartella {#create-a-folder}

Per creare una cartella:

1. Accedi all&#39;istanza [!DNL Experience Manager Forms].
1. Selezionare **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.

   ![Seleziona modulo](/help/forms/assets/select-forms.png)

1. Selezionare **[!UICONTROL Crea]** > **[!UICONTROL Cartella]**.

   ![Crea cartella](/help/forms/assets/create-folder.png)

   Viene visualizzata la finestra di dialogo **[!UICONTROL Aggiungi cartella]**.
1. Immetti il **[!UICONTROL Titolo]**. Il **[!UICONTROL Nome]** viene popolato automaticamente durante la digitazione del **[!UICONTROL Titolo]**.

   ![Aggiungi cartella](/help/forms/assets/add-folder.png)

1. Fai clic su **[!UICONTROL Crea]**.

   >[!NOTE]
   >
   >Per impostazione predefinita, il valore del campo del nome viene compilato automaticamente dal titolo. Il nome può contenere solo caratteri alfanumerici o trattini (-) e trattini bassi (_) caratteri speciali. Tutti gli altri caratteri speciali immessi nel titolo vengono automaticamente sostituiti da un trattino e viene richiesto di confermare il nuovo nome. Puoi scegliere di continuare con il nome suggerito o modificarlo ulteriormente.

Nell’elenco delle risorse, nella posizione corrente viene visualizzata una nuova cartella con il titolo definito.

Se esiste una cartella con il nome specificato, l’invio non riesce e viene visualizzato un errore. Puoi visualizzare il messaggio di errore passando il cursore sull&#39;icona di errore ![aem6forms_error_alert](assets/Smock_Alert_18_N.svg) visualizzata accanto al campo del nome.

Puoi selezionare la cartella creata per entrarvi e creare risorse o cartelle al suo interno. Inoltre, puoi selezionare una cartella e scegliere di metterla in coda per il download, eliminarla o modificarne il nome.

### Creare copie di una o più risorse {#create-copies-of-one-or-more-assets-or-letters}

Puoi utilizzare una risorsa esistente per creare rapidamente una risorsa con proprietà, contenuto e risorse ereditate simili.

Per creare copie delle risorse:

1. Accedi all&#39;istanza [!DNL Experience Manager Forms].
1. Nella pagina relativa alle risorse, seleziona una o più risorse. Nell&#39;interfaccia utente viene visualizzata l&#39;icona **[!UICONTROL Copia]**.
1. Seleziona **[!UICONTROL Copia]**. Nell&#39;interfaccia utente viene visualizzata l&#39;icona ![Incolla](/help/forms/assets/Smock_Paste_18_N.svg).

   ![Copia risorsa](/help/forms/assets/copy-asset.png)

   Puoi anche scegliere di spostarti/spostarti all’interno di una cartella prima di incollarla. Cartelle diverse possono contenere risorse con gli stessi nomi. Per ulteriori informazioni sulle cartelle, consulta [Cartelle e organizzazione delle risorse](#folders-and-organizing-assets).
1. Seleziona **[!UICONTROL Incolla]**.

   ![Incolla risorsa](/help/forms/assets/paste-asset.png)

1. Viene visualizzata la finestra di dialogo **[!UICONTROL Incolla]**. Il sistema genera automaticamente nomi e titoli nelle nuove copie delle risorse, ma puoi modificare i titoli e i nomi delle risorse.

   Se le risorse vengono copiate e incollate nello stesso punto, viene aggiunto il suffisso &quot;-CopyXX&quot; al nome esistente di `asset`. Se per la risorsa copiata non esisteva alcun titolo, il campo del titolo generato automaticamente rimane vuoto.

   ![Incolla risorsa nella nuova posizione](/help/forms/assets/paste-click-asset.png)

   Se necessario, modifica il **[!UICONTROL Titolo]** con cui vuoi salvare la copia della risorsa. Il **[!UICONTROL Nome]** viene popolato automaticamente durante la digitazione del **[!UICONTROL Titolo]**.
1. Seleziona **[!UICONTROL Incolla]**. Vengono create nuove copie delle risorse copiate.

## Ricerca {#search-forms}

Quando si dispone di un numero elevato di risorse, la ricerca della risorsa corretta richiede tempo. Puoi eseguire una ricerca testuale per una risorsa specifica nella pagina della risorsa.

Per cercare la risorsa:

1. Accedi all&#39;istanza [!DNL Experience Manager Forms].
1. Fare clic sull&#39;icona di ricerca ![icona di ricerca](assets/folder-search-icon.svg).

   ![Modulo di ricerca](/help/forms/assets/search-form.png)

1. Immetti il nome della risorsa da cercare nella barra di ricerca.

1. Viene visualizzato un elenco delle risorse correlate. Seleziona la risorsa desiderata dall’elenco delle risorse visualizzato.

   ![Cercare risorse](/help/forms/assets/search-bar.png)

Per ulteriori informazioni e istruzioni sull&#39;utilizzo della ricerca, vedere [Ricerca](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=it).

<!--
## Export or create a package {#export-a-workflow-application}

You can use packages to install new content, install new functionality, transfer content between instances, and back up content.
To export or create a package:

1. Log in to your [!DNL Experience Manager Forms] instance.
1. Navigate to **[!UICONTROL Tools]** ![hammer](assets/hammer.png) &gt; **[!UICONTROL Deployment]** &gt; **[!UICONTROL Packages]**.

   ![Package Manager](/help/forms/assets/package-manager.png)

1. Click **[!UICONTROL Create Package]**.

   ![Create package](/help/forms/assets/create-package.png)   
   
   When **[!UICONTROL Create Package]** is clicked, the **[!UICONTROL New Package]** dialog box appears.
1. Specify the package name, version, and group for the package. 
   
   ![New package](/help/forms/assets/new-package.png)  

   * **Package Name** - Select a descriptive name to help you identify the contents of the package.

   * **Version** - It is a textual field to indicate a version. This is appended to the package name to form the name of the zip file.

   * **Group** - This is the target group (or folder) name. Groups help you organize your packages. A folder is created for the group if it does not already exist. If you leave the group name blank, it creates the package in the main package list.

1. Click **[!UICONTROL OK]**.

   Once the package is created, it appears at the top of the list of packages.

1. Click **[!UICONTROL Edit]**.
   
   ![Edit Package](/help/forms/assets/edit-package.png)
    
1. Open the **[!UICONTROL Filters]** tab.
   
   ![Open filter tab](/help/forms/assets/add-filter-package.png)
   
1.  Click **[!UICONTROL Add Filter]**. 
   
      ![Add filter](/help/forms/assets/add-filter.png)

      You can specify the path of the package. You can also add rules and other validations for the package.

      ![Add path](/help/forms/assets/add-path.png)

1. Click **[!UICONTROL Save]** after you are finished editing the settings.
1. Click **[!UICONTROL Build]** to create the package.
    
     ![Build path](/help/forms/assets/build-package.png)

   After the package is built, you can download the package and import it to the other server. The workflow application appears on the server where the package is uploaded.

   >[!NOTE]
   >
   >For the workflow application to work properly, also export the corresponding Adaptive Form and workflow model with the work application.

   Once a package is uploaded to AEM, you can modify its settings. You can also download or delete the package.

## Import and export assets in Correspondence Management {#import-and-export-assets-in-correspondence-management}

To share assets, such as data dictionaries, letters, and document fragments, between two different implementations of Correspondence Management, you can create and share .cmp files. A .cmp file can include one or more data dictionaries, letters, document fragments, and forms.

### Export Document Fragments, Letters, and/or Data Dictionaries {#export-document-fragments-letters-and-or-data-dictionaries}

1. In the letters, document fragments, or data dictionary pages, select and select the assets you want to export to a single package, and then select Queue For Download. The assets are lined-up for export.
1. As required, repeat the above step to add letters, document fragments, and data dictionaries.
1. Select **Download**.
1. Correspondence Management displays Download Asset(s) dialog with a list of assets in the export list.

   ![export](assets/export.png)

1. To view the dependencies that are exported, Select Resolve. Or skip to the next step. Even if you do not select resolve, the dependencies are still exported.
1. To download the .cmp file, select **OK**.
1. Correspondence Management downloads a .cmp file to your computer.

   The .cmp file includes the exported assets. You can share the .cmp file with others. Other users can import the .cmp file in a different server to get all the assets in the new server.

### Export all the Correspondence Management assets as a package {#export-all-the-correspondence-management-assets-as-a-package}

Use this option to download all the Correspondence Management assets and related dependencies as a package from an [!DNL AEM Forms] instance.

For example, if Correspondence Management has a letter that uses an image and text, the downloaded package also contains the image and the text related to the letter. All the metadata properties (including custom properties) associated with the asset are also downloaded. Once you have downloaded the package (.cmp), you can [import the package to a different [!DNL AEM Forms] instance](import-export-forms-templates.md#p-upload-forms-documents-assets-p).

To download all the Correspondence Management assets and related dependencies as a package, complete the following steps:

1. Log in to [!DNL AEM Forms] server as a forms user.
1. Select **Adobe Experience Manager** in the Global Navigation bar.
1. Select tools ( ![tools](assets/tools.png)) and then select **Forms**.
1. Select **Export Correspondence Management Assets**.

   ![publish-cmp-assets-1](assets/publish-cmp-assets-1.png)

   ( ``The Export All Correspondence Management Assets page appears and displays the information about the last time the Export process was attempted and a link to download the last successfully exported package.

   ![export-last-run-details](assets/export-last-run-details.png)

1. Select **Export** and, in the confirm message, select **OK**.

   After a batch process is complete, the last run details and the link to download the package are updated. This includes information such as the Administrator login and if the batch run successfully or failed. The assets are exported to a package and the Download Exported Package link appears.

   >[!NOTE]
   >
   >The Export All Assets process cannot be canceled once initiated. Also, while the export all operation is in process, do not create, delete, modify, or publish any assets or initiate Publish All Assets process.a

1. Select the **Download Exported Package** link to download the package file.

   To add the assets in the package to another instance of Correspondence Management, [import the package to an [!DNL AEM Forms] instance](import-export-forms-templates.md#p-upload-forms-documents-assets-p).

<!-- ### Import Document Fragments, Letters and/or Data Dictionaries into Correspondence Management {#import-document-fragments-letters-and-or-data-dictionaries-into-correspondence-management}

You can import assets that are exported into a .cmp file. A .cmp file can have one or more letters, data dictionaries, document fragments, and dependent assets.

>[!NOTE]
>
>While importing old Correspondence Management assets for migration, log in using an Admin account. For more information on Migrating old Correspondence Management assets, see [Migrate Correspondence Management assets to AEM 6.1 forms](migration-utility.md).

1. On the data dictionary, letters, or document fragments page, select **Create &gt; File Upload** and select the .cmp file.
1. Correspondence Management displays the Import Assets dialog with the list of assets that are imported. Select **Import**.

   After importing the assets, the following properties of the assets are updated while the other properties remain the same:

    * Author: Displays the ID of the user that imported the asset to the server
    * Modified: The time when the asset was imported to the server

   >[!NOTE]
   >
   >For you to be able to upload XDPs (as part of the cmp file or otherwise), you need to be a part of forms-power-users group. For access rights, contact the administrator. -->

## Consulta anche {#see-also}

{{see-also}}
