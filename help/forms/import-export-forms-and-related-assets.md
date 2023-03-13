---
title: Importare ed esportare le risorse
seo-title: Import and export assets to [!DNL AEM Forms]
description: Puoi importare ed esportare Forms adattivo e le risorse correlate in istanze AEM. Ciò consente di migrare i moduli o spostarli tra i sistemi.
seo-description: You can import and export Adaptive Forms and templates from and in to AEM instances. This helps in migrating forms or moving them across systems.
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1325'
ht-degree: 1%

---


# Importare ed esportare le risorse {#importing-and-exporting-assets-to-aem-forms}

È possibile spostare moduli, temi, modelli, frammenti di documenti, temi e altre risorse tra diversi [!DNL AEM Forms] istanze. Tale spostamento è necessario per la migrazione di sistemi o lo spostamento di moduli da un server di sviluppo o di gestione temporanea a un server di produzione.

Per le risorse di cui caricare e importare tramite [!DNL AEM Forms] L’interfaccia utente di è supportata e l’utilizzo dell’interfaccia utente di Forms è consigliato per l’esportazione o l’importazione. Non è consigliabile utilizzare Gestione pacchetti AEM per esportare o importare tali risorse.

## Scaricare o caricare risorse Forms &amp; Documents {#download-or-upload-forms-amp-documents-assets}

[!DNL AEM Forms] L’interfaccia utente ti consente di esportare le risorse da un’istanza AEM scaricandole come un pacchetto CRX dell’AEM o come file binari. Puoi quindi importare il pacchetto AEM CRX scaricato o il file binario in un’altra istanza AEM.

Esportazione e importazione tramite [!DNL AEM Forms] L’interfaccia utente di è supportata per tutte le risorse, ad eccezione dei modelli di moduli adattivi e dei criteri per il contenuto dei moduli adattivi. Pertanto, all’esportazione di un modulo adattivo da [!DNL AEM Forms] L’interfaccia utente, il modello di modulo adattivo e i criteri del contenuto correlati non vengono esportati automaticamente come altre risorse correlate.

Per questi tipi di risorse, devi utilizzare Gestione pacchetti AEM per creare un pacchetto CRX sul server AEM di origine e installare il pacchetto sul server di destinazione. Per informazioni sulla creazione e l&#39;installazione dei pacchetti, vedere [Distribuzione a AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=it).

### Scaricare risorse Forms e Documents {#download-forms-amp-documents-assets}

Per scaricare le risorse Forms e Documents:

1. Accedi a [!DNL AEM Forms] dell&#39;istanza.
1. Experience Manager tocco ![adobeexperiencemanager](assets/adobeexperiencemanager.png) icona > navigazione ![bussola](assets/Smock_Compass_18_N.svg) icon> **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Seleziona le risorse dei moduli e tocca **[!UICONTROL Scarica]** icona.
1. In Scarica risorse, scegli una delle seguenti opzioni e tocca **[!UICONTROL Scarica]**.

   * **Scarica come pacchetto CRX:** Utilizza l&#39;opzione per scaricare e spostare tutte le risorse selezionate e le relative dipendenze da un [!DNL AEM Forms] a un&#39;altra. Scarica tutte le risorse e le cartelle come pacchetto crx. Qualsiasi risorsa modulo, compresi i moduli creati in AEM (Forms adattivo e frammenti di moduli adattivi), i documenti PDF e le risorse (XSD, XFS, immagini) possono essere scaricati come pacchetto da [!DNL AEM Forms] UI.
Il vantaggio di scaricare le risorse come pacchetto è che scarica anche le risorse utilizzate dalla risorsa selezionata per il download. Ad esempio, se disponi di un modulo adattivo che utilizza un modello di modulo, XSD e un’immagine. Quando selezioni questo modulo adattivo e lo scarichi come pacchetto, il pacchetto scaricato contiene anche il modello del modulo, XSD e l’immagine. Vengono scaricate anche tutte le proprietà di metadati (comprese le proprietà personalizzate) associate alla risorsa.

   * **Scaricate le risorse come file binari:** Utilizza l’opzione per scaricare solo modelli di modulo (XDP), PDF forms (PDF), documento (PDF) e risorse (immagini, schemi, fogli di stile). Puoi modificare queste risorse con applicazioni esterne. Scarica come file .zip le risorse dei moduli che hanno file binari, come XSD, XDP, immagini, PDF e XDP.
Non è possibile scaricare Forms adattivo, frammenti di modulo adattivo e temi con **[!UICONTROL Scarica risorse come file binari]** opzione. Per scaricare queste risorse, utilizza **[!UICONTROL Scarica come pacchetto CRX]** opzione.

   Le risorse selezionate vengono scaricate come archivio (file .zip).

   >[!NOTE]
   >
   >Sia il pacchetto AEM che i file binari vengono scaricati come archivio (file .zip). I modelli per le risorse non vengono scaricati insieme alle risorse. È necessario esportare i modelli di risorse separatamente.

### Caricare le risorse {#upload-forms-amp-documents-assets}

Per caricare le risorse Forms e Documents:

1. Accedi a [!DNL AEM Forms] dell&#39;istanza.
1. Experience Manager tocco ![adobeexperiencemanager](assets/adobeexperiencemanager.png) icona > navigazione ![bussola](assets/Smock_Compass_18_N.svg) icon> **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Tocca **Crea** >**Caricamento file**. Viene visualizzata la finestra di dialogo Carica moduli o pacchetto.
1. Nella finestra di dialogo, sfoglia e seleziona il pacchetto o l’archivio da importare. È inoltre possibile selezionare documenti PDF, XSD, immagini, fogli di stile e moduli XDP. Tocca **[!UICONTROL Apri]**. La cartella o il nome del file selezionato non deve contenere caratteri speciali.

   Nella finestra di dialogo, verifica i dettagli delle risorse caricate e tocca **[!UICONTROL Carica]**.

   Se carichi una risorsa Forms esistente, la risorsa viene aggiornata.

   >[!NOTE]
   >
   >Il caricamento di un pacchetto non sostituisce la gerarchia di cartelle esistente. Ad esempio, se disponi di un modulo adattivo denominato &quot;Training&quot; nella posizione /content/dam/formsanddocuments su un server. Scarica il modulo adattivo e carica il modulo su un altro server. Il secondo server dispone inoltre di una cartella denominata Training nella stessa posizione /content/dam/formsanddocuments. Caricamento non riuscito.

## Download o caricamento di un tema {#downloading-or-uploading-a-theme}

Con [!DNL AEM Forms], puoi creare, scaricare o caricare temi. Un tema viene creato come altre risorse, ad esempio moduli, documenti e lettere. Puoi creare un tema, scaricarlo e caricarlo in un’istanza separata per riutilizzarlo. Per ulteriori informazioni sui temi, vedi [Temi](themes.md) in [!DNL AEM Forms].

### Download di un tema {#downloading-a-theme}

Puoi esportare i temi in [!DNL AEM Forms] che puoi utilizzare in altri progetti o istanze. AEM consente di scaricare il tema come file zip, che puoi caricare sull’istanza.

Per scaricare un tema:

1. Accedi a [!DNL AEM Forms] dell&#39;istanza.
1. Experience Manager tocco ![adobeexperiencemanager](assets/adobeexperiencemanager.png) icona > navigazione ![bussola](assets/Smock_Compass_18_N.svg) icon> **[!UICONTROL Forms]** > **[!UICONTROL Temi]**.
1. Seleziona il tema e tocca **[!UICONTROL Scarica]**. Il tema viene scaricato come archivio (file .zip).

### Caricamento di un tema {#uploading-a-theme}

Puoi utilizzare i temi creati con predefiniti di stile sul progetto. Puoi importare pacchetti tema creati da altri caricandoli sul progetto.

Per caricare un tema:

1. Ad Experience Manager, passa a **[!UICONTROL Forms]** > **[!UICONTROL Temi Forms]**.
1. Nella pagina Temi fare clic su **[!UICONTROL Creazione Forms]** > **[!UICONTROL Caricamento file Forms]**.
1. Nella richiesta di caricamento file, individua e seleziona un pacchetto di temi sul computer e fai clic su **[!UICONTROL Caricamento Forms]**. Il tema viene caricato.

<!--

## Import and export assets in Correspondence Management {#import-and-export-assets-in-correspondence-management}

To share assets, such as data dictionaries, letters, and document fragments, between two different implementations of Correspondence Management, you can create and share .cmp files. A .cmp file can include one or more data dictionaries, letters, document fragments, and forms.

### Export Document Fragments, Letters, and/or Data Dictionaries {#export-document-fragments-letters-and-or-data-dictionaries}

1. In the letters, document fragments, or data dictionary pages, tap and select the assets you want to export to a single package, and then tap Queue For Download. The assets are lined-up for export.
1. As required, repeat the above step to add letters, document fragments, and data dictionaries.
1. Tap **Download**.
1. Correspondence Management displays Download Asset(s) dialog with a list of assets in the export list.

   ![export](assets/export.png)

1. To view the dependencies that are exported, Tap Resolve. Or skip to the next step. Even if you do not tap resolve, the dependencies are still exported.
1. To download the .cmp file, tap **OK**.
1. Correspondence Management downloads a .cmp file to your computer.

   The .cmp file includes the exported assets. You can share the .cmp file with others. Other users can import the .cmp file in a different server to get all the assets in the new server.

### Export all the Correspondence Management assets as a package {#export-all-the-correspondence-management-assets-as-a-package}

Use this option to download all the Correspondence Management assets and related dependencies as a package from an [!DNL AEM Forms] instance.

For example, if Correspondence Management has a letter that uses an image and text, the downloaded package also contains the image and the text related to the letter. All the metadata properties (including custom properties) associated with the asset are also downloaded. Once you have downloaded the package (.cmp), you can [import the package to a different [!DNL AEM Forms] instance](import-export-forms-templates.md#p-upload-forms-documents-assets-p).

To download all the Correspondence Management assets and related dependencies as a package, complete the following steps:

1. Log in to [!DNL AEM Forms] server as a forms user.
1. Tap **Adobe Experience Manager** in the Global Navigation bar.
1. Tap tools ( ![tools](assets/tools.png)) and then tap **Forms**.
1. Tap **Export Correspondence Management Assets**.

   ![publish-cmp-assets-1](assets/publish-cmp-assets-1.png)

   ( ``The Export All Correspondence Management Assets page appears and displays the information about the last time the Export process was attempted and a link to download the last successfully exported package.

   ![export-last-run-details](assets/export-last-run-details.png)

1. Tap **Export** and, in the confirm message, tap **OK**.

   After a batch process is complete, the last run details and the link to download the package are updated. This includes information such as the Administrator login and if the batch run successfully or failed. The assets are exported to a package and the Download Exported Package link appears.

   >[!NOTE]
   >
   >The Export All Assets process cannot be canceled once initiated. Also, while the export all operation is in process, do not create, delete, modify, or publish any assets or initiate Publish All Assets process.a

1. Tap the **Download Exported Package** link to download the package file.

   To add the assets in the package to another instance of Correspondence Management, [import the package to an [!DNL AEM Forms] instance](import-export-forms-templates.md#p-upload-forms-documents-assets-p).

### Import Document Fragments, Letters and/or Data Dictionaries into Correspondence Management {#import-document-fragments-letters-and-or-data-dictionaries-into-correspondence-management}

You can import assets that are exported into a .cmp file. A .cmp file can have one or more letters, data dictionaries, document fragments, and dependent assets.

>[!NOTE]
>
>While importing old Correspondence Management assets for migration, log in using an Admin account. For more information on Migrating old Correspondence Management assets, see [Migrate Correspondence Management assets to AEM 6.1 forms](migration-utility.md).

1. On the data dictionary, letters, or document fragments page, tap **Create &gt; File Upload** and select the .cmp file.
1. Correspondence Management displays the Import Assets dialog with the list of assets that are imported. Tap **Import**.

   After importing the assets, the following properties of the assets are updated while the other properties remain the same:

    * Author: Displays the ID of the user that imported the asset to the server
    * Modified: The time when the asset was imported to the server

   >[!NOTE]
   >
   >For you to be able to upload XDPs (as part of the cmp file or otherwise), you need to be a part of forms-power-users group. For access rights, contact the administrator.
-->

## Esportare un’applicazione del flusso di lavoro {#export-a-workflow-application}

Puoi utilizzare Gestione pacchetti AEM per esportare le applicazioni del flusso di lavoro. La procedura è descritta di seguito:

1. Apri [!DNL AEM Forms] gestione pacchetti.
1. Clic **[!UICONTROL Crea pacchetto]**. Il **[!UICONTROL Nuovo pacchetto]** viene visualizzata.
1. Specificare nome, versione e gruppo per il pacchetto. Fai clic su **[!UICONTROL OK]**.
1. Clic **[!UICONTROL Modifica]** e apri **[!UICONTROL Filtri]** scheda. Clic **[!UICONTROL Aggiungi filtro]**. Specifica il percorso dell’applicazione del flusso di lavoro. Ad esempio, /etc/fd/dashboard/startpoints/homemortgage. Clic **[!UICONTROL Aggiungi regola]**.

1. Apri la scheda **[!UICONTROL Avanzate.]** Seleziona **[!UICONTROL Unisci]** o **[!UICONTROL Sovrascrivere]** nel campo Gestione ACL. Fai clic su **[!UICONTROL Salva]**.
1. Clic **[!UICONTROL Genera]** per creare il pacchetto.

   Una volta creato il pacchetto, è possibile scaricarlo e importarlo nell&#39;altro server. L’applicazione del flusso di lavoro viene visualizzata sul server in cui viene caricato il pacchetto.

   >[!NOTE]
   >
   >Affinché l’applicazione del flusso di lavoro funzioni correttamente, esporta anche il modulo adattivo e il modello di flusso di lavoro corrispondenti con l’applicazione di lavoro.

## Cartelle e organizzazione delle risorse {#folders-and-organizing-assets}

[!DNL AEM Forms] l’interfaccia utente utilizza le cartelle per disporre le risorse. Queste cartelle vengono utilizzate per organizzare le risorse create in [!DNL AEM Forms] dell&#39;utente. È possibile rinominare, creare sottocartelle e archiviare risorse e documenti in queste cartelle. L’organizzazione di documenti e risorse in una cartella consente di raggruppare i file per facilitarne la gestione. Puoi selezionare una cartella e scegliere se scaricarla o eliminarla.

La procedura seguente illustra come creare una cartella:

### Crea una cartella . {#create-a-folder}

1. Accedi a [!DNL AEM Forms] interfaccia utente in `https://<server>:<port>/aem/forms.html`.
1. Passare alla posizione in cui si desidera creare una cartella.
1. Tocca **[!UICONTROL Crea]** > **[!UICONTROL Cartella]**.
1. Immetti i seguenti dettagli:

   * **Titolo:** Nome visualizzato per la cartella
   * **Nome:** *(Obbligatorio)* Nome del nodo in cui si desidera archiviare la cartella nell&#39;archivio

   >[!NOTE]
   >
   >Per impostazione predefinita, il valore del campo nome viene compilato automaticamente dal titolo. Il nome può contenere solo caratteri alfanumerici o trattini (-) e trattini bassi (_) caratteri speciali. Tutti gli altri caratteri speciali immessi nel titolo vengono automaticamente sostituiti da un trattino e viene richiesto di confermare il nuovo nome. Puoi scegliere di continuare con il nome suggerito o modificarlo ulteriormente.

1. Nell’elenco delle risorse, nella posizione corrente viene visualizzata una nuova cartella con il titolo definito.

   Se esiste una cartella con il nome specificato, l’invio non riesce e viene visualizzato un errore. Puoi visualizzare il messaggio di errore passando il cursore sopra l’errore ![aem6forms_error_alert](assets/Smock_Alert_18_N.svg) accanto al campo del nome.

   Tocca la cartella appena creata per entrarvi e creare risorse o cartelle al suo interno. Inoltre, puoi selezionare una cartella e scegliere di metterla in coda per il download, eliminarla o modificarne il nome.

<!-- ### Create copies of one or more assets or letters {#create-copies-of-one-or-more-assets-or-letters}

You can use an existing assets and letters to quickly create a assets and letters with similar properties, content, and inherited assets. You can copy and paste data dictionaries, document fragments, and letters.

Complete the following steps to create copies of assets and letters:

1. In the relevant Assets or Letters page, select one or more assets/letters. The UI displays the Copy icon.
1. Tap Copy. The UI displays the Paste icon. You can also choose to go/navigate inside a folder before you paste. Different folders can contain assets with same names. For more information on folders, see [Folders and organizing assets](#folders-and-organizing-assets).
1. Tap Paste. The Paste dialog appears. The system auto generates names and titles to the new copies of assets/letters, but you can edit the titles and names of the assets/letters.

   If you are copying and pasting the assets/letters at the same place, a suffix "-CopyXX" gets added to the existing name of the asset/letter. If no title existed for the copied asset/letter, the auto generated title field remains blank.

1. If required, edit the Title and Name with which you want to save the copy of the asset/letter.
1. Tap Paste. New copies of the copied assets are created.

## Search {#search-forms}

[!DNL AEM Forms] UI allows you to search your content. Using the top bar, you can tap Search **[A]** to search your content for resources such as assets and documents.

When you search for assets, [!DNL AEM Forms] displays the side panel. You can also tap ![assets-browser-content-only](assets/assets-browser-content-only.png) &gt; Filter **[B]** to invoke the side panel. Using the various filters in the side panel, you can narrow down your search. The side panel also allows you to save your searches.

![search_topbar](assets/search_topbar.png)

**A.** Search **B.** Filter

![Side panel - Filters](assets/search_sidepanel.png)

Side panel - Filters

On the side panel, you can use the following to narrow down your search results:

* Search Directory
* Tags
* Search Criteria; for example, Modified Dates, Publish Status, LiveCopy Status.

The side panel also allows you to save your search settings with names of your choice.

For more information and instructions on using search, filters, saved search, and side panel, see [Search](/help/sites-authoring/search.md).

-->
