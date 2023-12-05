---
title: Come importare, esportare e organizzare Forms o PDF forms adattivi in un’istanza di AEM Forms?
description: Scopri come migrare Forms adattivo, PDF forms, temi e altre risorse di supporto da e verso istanze AEM.
topic-tags: forms-manager
exl-id: f5105fb7-b8c0-4656-8095-b21d392746c0
source-git-commit: abe5f8a4b19473c3dddfb79674fb5f5ab7e52fbf
workflow-type: tm+mt
source-wordcount: '1193'
ht-degree: 0%

---

# Importare o esportare risorse Adaptive Forms e AEM Forms {#importing-and-exporting-assets-to-aem-forms}

È possibile spostare Forms adattivo e le risorse correlate, ad esempio i temi dei moduli adattivi, i modelli di dati dei moduli, i modelli di moduli adattivi, i frammenti di documento e i PDF forms tra [!DNL AEM Forms] istanze. Potete importare ed esportare le risorse in formato pacchetto CRX o file binario.

Quando si esporta un modulo adattivo, i criteri e i modelli di contenuto non vengono esportati. Utilizzare [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#how-rolling-deployments-work) per esportare tali risorse.

## Scaricare Forms adattivo, PDF forms o risorse correlate {#download-forms-amp-documents-assets}

Per scaricare i moduli o le risorse correlate:

1. Accedi al tuo [!DNL AEM Forms] dell&#39;istanza.
1. Seleziona **[!UICONTROL Adobe Experience Manager]** ![adobeexperiencemanager](assets/adobeexperiencemanager.png) icona > **[!UICONTROL Navigazione]** ![bussola](assets/Smock_Compass_18_N.svg) icona > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Seleziona le risorse e fai clic su **[!UICONTROL Scarica]** icona.
1. In Scarica risorse, scegli una delle seguenti opzioni e seleziona **[!UICONTROL Scarica]**.

   * **Scarica come pacchetto CRX:** Utilizza l’opzione per scaricare e spostare tutte le risorse selezionate e le relative dipendenze da un [!DNL AEM Forms] a un&#39;altra. Scarica tutte le risorse e le cartelle come pacchetto CRX, inclusi i moduli creati in AEM (Forms adattivo e frammenti di moduli adattivi), i set di moduli, il modello di dati del modulo, i modelli di modulo, i documenti PDF e le risorse di riferimento (XSD e immagini).
Il vantaggio di scaricare le risorse come pacchetto è che viene scaricato anche il riferimento dalle risorse selezionate. Ad esempio, se disponi di un modulo adattivo che utilizza un modello di modulo, XSD e un’immagine. Quando selezioni questo modulo adattivo e lo scarichi come pacchetto, il pacchetto scaricato contiene anche il modello del modulo, XSD e l’immagine. Vengono scaricate anche tutte le proprietà di metadati (comprese le proprietà personalizzate) associate alla risorsa.

   * **Scaricare le risorse come file binari:** Utilizza l’opzione per scaricare solo modelli di modulo (XDP), PDF forms (PDF), documento (PDF) e risorse (immagini, schemi, fogli di stile). Puoi modificare queste risorse con applicazioni esterne. Scarica come file .zip le risorse con file binari, come immagini, PDF e altri formati supportati.
Non è possibile scaricare Forms adattivo, frammenti di moduli adattivi, temi e set di moduli con **[!UICONTROL Scaricare le risorse come file binari]** opzione. Per scaricare queste risorse, utilizza **[!UICONTROL Scarica come pacchetto CRX]** opzione.

   Le risorse selezionate vengono scaricate come archivio (file .zip).

   >[!NOTE]
   >
   >Sia il pacchetto AEM che i file binari vengono scaricati come archivio (file .zip). I modelli per le risorse non vengono scaricati insieme alle risorse. È necessario esportare i modelli di risorse separatamente.

## Caricare Forms adattivo, PDF forms o risorse correlate {#upload-forms-amp-documents-assets}

Puoi caricare i tipi di risorse supportati singolarmente o come archivio ZIP. Per un file ZIP, vengono visualizzati i percorsi relativi di tutte le risorse supportate. Le risorse non supportate nel file ZIP vengono ignorate e non elencate. Tuttavia, se l’archivio ZIP contiene solo le risorse non supportate, viene visualizzato un messaggio di errore al posto della finestra di dialogo a comparsa.
Per caricare un modulo o una risorsa correlata:

1. Accedi al tuo [!DNL AEM Forms] dell&#39;istanza.
1. Seleziona **[!UICONTROL Adobe Experience Manager]** ![adobeexperiencemanager](assets/adobeexperiencemanager.png) icona > **[!UICONTROL Navigazione]** ![bussola](assets/Smock_Compass_18_N.svg) icona > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Seleziona **[!UICONTROL Crea]** > **[!UICONTROL Caricamento file]**. Viene visualizzata una finestra di dialogo.
1. Nella finestra di dialogo, sfoglia e seleziona il pacchetto o l’archivio da importare. Puoi anche selezionare altri tipi di file supportati. Seleziona **[!UICONTROL Apri]**. La cartella o il nome del file selezionato non deve contenere caratteri speciali.

   Nella finestra di dialogo, verifica i dettagli delle risorse caricate e seleziona **[!UICONTROL Carica]**.

   Se carichi una risorsa Forms esistente, la risorsa viene aggiornata.

   >[!NOTE]
   >
   > * Quando un nome è in conflitto con tipi di risorse diversi, il caricamento di un pacchetto non sostituisce la gerarchia di cartelle esistente. Ad esempio, se disponi di un modulo adattivo denominato &quot;Training&quot; nella posizione /content/dam/formsanddocuments su un server. Scarica il modulo adattivo e carica il modulo su un altro server. Il secondo server dispone inoltre di una cartella denominata Training nella stessa posizione /content/dam/formsanddocuments. Caricamento non riuscito.
   > * Solo un membro del `form-power-user` Il gruppo può caricare file XDP.


## Scaricare un tema {#downloading-a-theme}

Puoi esportare i temi in [!DNL AEM Forms] che puoi utilizzare in altri progetti o istanze. AEM consente di scaricare i temi come file zip, che puoi caricare sull’istanza.

Per scaricare un tema:

1. Accedi al tuo [!DNL AEM Forms] dell&#39;istanza.
1. Seleziona **[!UICONTROL Adobe Experience Manager]** ![adobeexperiencemanager](assets/adobeexperiencemanager.png) icona > **[!UICONTROL Navigazione]** ![bussola](assets/Smock_Compass_18_N.svg) icona > **[!UICONTROL Forms]** > **[!UICONTROL Temi]**.
1. Seleziona il tema e seleziona **[!UICONTROL Scarica]**. Il tema viene scaricato come archivio (file .zip).

## Carica un tema {#uploading-a-theme}

È possibile caricare e utilizzare i temi creati da altri utenti nei moduli. Per caricare un tema:

1. Ad Experience Manager, passa a **[!UICONTROL Forms]** > **[!UICONTROL Temi]**.
1. Nella pagina Temi fare clic su **[!UICONTROL Crea]** > **[!UICONTROL Caricamento file]**.
1. Nella richiesta di caricamento file, individua e seleziona un pacchetto di temi sul computer e fai clic su **[!UICONTROL Carica]**. Il tema caricato è disponibile nella pagina dei temi.

<!-- ## Import and export assets in Correspondence Management {#import-and-export-assets-in-correspondence-management}

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

## Esportare un’applicazione del flusso di lavoro {#export-a-workflow-application}

È possibile utilizzare Gestione pacchetti per esportare applicazioni flusso di lavoro. La procedura è descritta di seguito:

1. Apri [!DNL AEM Forms] gestione pacchetti. L’URL del gestore pacchetti è `https://[server]:[port]/crx/packmgr`.
1. Clic **[!UICONTROL Crea pacchetto]**. Il **[!UICONTROL Nuovo pacchetto]** viene visualizzata.
1. Specificare il nome, la versione e il gruppo del pacchetto. Fai clic su **[!UICONTROL OK]**.
1. Clic **[!UICONTROL Modifica]** e apri **[!UICONTROL Filtri]** scheda. Clic **[!UICONTROL Aggiungi filtro]**. Specifica il percorso dell’applicazione del flusso di lavoro. Ad esempio, /etc/fd/dashboard/startpoints/homemortgage. Clic **[!UICONTROL Aggiungi regola]**.

1. Apri **[!UICONTROL Avanzate]** scheda. Seleziona **[!UICONTROL Unisci]** o **[!UICONTROL Sovrascrivere]** nel campo Gestione ACL. Fai clic su **[!UICONTROL Salva]**.
1. Clic **[!UICONTROL Genera]** per creare il pacchetto.

   Una volta creato il pacchetto, è possibile scaricarlo e importarlo nell&#39;altro server. L’applicazione del flusso di lavoro viene visualizzata sul server in cui viene caricato il pacchetto.

   >[!NOTE]
   >
   >Affinché l’applicazione del flusso di lavoro funzioni correttamente, esporta anche il modulo adattivo e il modello di flusso di lavoro corrispondenti con l’applicazione di lavoro.

## Utilizzare le cartelle per organizzare Forms adattivo, PDF forms e risorse correlate  {#folders-and-organizing-assets}

Puoi utilizzare le cartelle per organizzare e disporre le risorse. L’organizzazione di documenti e risorse in una cartella consente di raggruppare i file per semplificarne la gestione. Puoi selezionare una cartella e scegliere se scaricarla o eliminarla. La procedura seguente illustra come creare una cartella:

### Creare una cartella {#create-a-folder}

1. Accedi al tuo [!DNL AEM Forms] dell&#39;istanza.
1. Seleziona Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) icona > navigazione ![bussola](assets/Smock_Compass_18_N.svg) icon> **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Seleziona **[!UICONTROL Crea]** > **[!UICONTROL Cartella]**.
1. Immetti i seguenti dettagli:

   * **[!UICONTROL Titolo]**: nome visualizzato per la cartella
   * **[!UICONTROL Nome]**: *(Obbligatorio)* Nome del nodo in cui si desidera archiviare la cartella nell&#39;archivio

   >[!NOTE]
   >
   >Per impostazione predefinita, il valore del campo del nome viene compilato automaticamente dal titolo. Il nome può contenere solo caratteri alfanumerici o trattini (-) e trattini bassi (_) caratteri speciali. Tutti gli altri caratteri speciali immessi nel titolo vengono automaticamente sostituiti da un trattino e viene richiesto di confermare il nuovo nome. Puoi scegliere di continuare con il nome suggerito o modificarlo ulteriormente.

1. Nell’elenco delle risorse, nella posizione corrente viene visualizzata una nuova cartella con il titolo definito.

   Se esiste una cartella con il nome specificato, l’invio non riesce e viene visualizzato un errore. Puoi visualizzare il messaggio di errore passando il cursore sopra l’errore ![aem6forms_error_alert](assets/Smock_Alert_18_N.svg) accanto al campo del nome.

   Puoi selezionare la cartella creata per entrarvi e creare risorse o cartelle al suo interno. Inoltre, puoi selezionare una cartella e scegliere di metterla in coda per il download, eliminarla o modificarne il nome.


<!-- ### Create copies of one or more assets or letters {#create-copies-of-one-or-more-assets-or-letters}

You can use an existing assets to quickly create an asset with similar properties, content, and inherited assets.

Complete the following steps to create copies of assets and letters:

1. On the relevant assets page, select one or more assets. The UI displays the Copy icon.
1. Select **[!UICONTROL Copy]**. The UI displays the **[!UICONTROL Paste]** icon. You can also choose to go/navigate inside a folder before you paste. Different folders can contain assets with same names. For more information on folders, see [Folders and organizing assets](#folders-and-organizing-assets).
1. Select **[!UICONTROL Paste]**. The **[!UICONTROL Paste]** dialog appears. The system auto generates names and titles to the new copies of assets/letters, but you can edit the titles and names of the assets/letters.

   If you are copying and pasting the assets/letters at the same place, a suffix "-CopyXX" gets added to the existing name of the asset/letter. If no title existed for the copied asset/letter, the auto generated title field remains blank.

1. If necessary, edit the Title and Name with which you want to save the copy of the asset/letter.
1. Select **[!UICONTROL Paste]**. New copies of the copied assets are created.

## Search {#search-forms}

You ca use the top bar **[A]** to search your content. When you search for assets, a side panel is displayed. You can also select ![assets-browser-content-only](assets/assets-browser-content-only.png) &gt; Filter **[B]** to invoke the side panel. Using the various filters in the side panel, you can narrow down your search. The side panel also lets you save your searches.

![search_topbar](assets/search_topbar.png)

**A.** Search **B.** Filter

![Side panel - Filters](assets/search_sidepanel.png)

Side panel - Filters

On the side panel, you can use the following to narrow down your search results:

* Search Directory
* Tags
* Search Criteria; for example, Modified Dates, Publish Status, LiveCopy Status.

The side panel also lets you save your search settings with names of your choice.

For more information and instructions on using search, filters, saved search, and side panel, see [Search](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html). -->

>[!MORELIKETHIS]
>
>* [Utilizzare i temi nei componenti core dei moduli adattivi](/help/forms/using-themes-in-core-components.md)