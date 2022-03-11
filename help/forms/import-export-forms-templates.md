---
title: Importare, esportare e organizzare Forms adattivo, PDF forms e altre risorse
seo-title: Learn to import, export, and organize Adaptive Forms, PDF forms, and other assets on an[!DNL AEM Forms] instance
description: 'Stai cercando di migrare da e verso le istanze di AEM risorse e Forms adattivi? Scopri come importare ed esportare Forms adattivo, PDF forms, temi e altre risorse di supporto da un’ [!DNL AEM Forms] istanza. '
seo-description: Looking to migrate Adaptive Forms and assets to and from an AEM instances? Learn here how to import and export Adaptive Forms, PDF forms, themes, and other supporting assets from an [!DNL AEM Forms] instance.
topic-tags: forms-manager
exl-id: f5105fb7-b8c0-4656-8095-b21d392746c0
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1211'
ht-degree: 2%

---

# Importare, esportare e organizzare Forms adattivo, PDF forms e altre risorse{#importing-and-exporting-assets-to-aem-forms}

È possibile spostare Forms adattivo e le risorse correlate, come i temi dei moduli adattivi, i modelli di dati dei moduli adattivi, i frammenti di documento e i PDF forms tra [!DNL AEM Forms] istanze. Puoi importare ed esportare le risorse in un pacchetto CRX o in formati di file binari.

Quando si esporta un modulo adattivo, i criteri dei contenuti e i modelli non vengono esportati. Utilizzo [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#how-rolling-deployments-work) per esportare tali beni.

## Scaricare Forms adattivo, PDF forms o risorse correlate {#download-forms-amp-documents-assets}

Per scaricare moduli o risorse correlate:

1. Accedi al tuo [!DNL AEM Forms] istanza.
1. Tocca **[!UICONTROL Adobe Experience Manager]** ![adobeexperiencemanager](assets/adobeexperiencemanager.png) icona > **[!UICONTROL Navigazione]** ![bussola](assets/Smock_Compass_18_N.svg) icona > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Seleziona le risorse e tocca il **[!UICONTROL Scarica]** icona.
1. In Scarica risorse , scegli una delle seguenti opzioni e tocca **[!UICONTROL Scarica]**.

   * **Scarica come pacchetto CRX:** Utilizza l’opzione per scaricare e spostare tutte le risorse selezionate e le dipendenze correlate da un [!DNL AEM Forms] istanza a un&#39;altra. Scarica tutte le risorse e le cartelle come pacchetto CRX, inclusi i moduli creati in AEM (Forms adattivo e frammenti di modulo adattivo), i set di moduli, il modello di dati del modulo, i modelli di moduli, i documenti PDF e le risorse di riferimento (XSD e immagini).
Il vantaggio di scaricare le risorse come pacchetto è che scarica anche i riferimenti dalle risorse selezionate. Ad esempio, se si dispone di un Modulo adattivo che utilizza un modello di modulo, XSD e un’immagine. Quando si seleziona questo modulo adattivo e lo si scarica come pacchetto, il pacchetto scaricato contiene anche il modello di modulo, XSD e l’immagine. Vengono scaricate anche tutte le proprietà di metadati (comprese le proprietà personalizzate) associate alla risorsa.

   * **Scarica le risorse come file binari:** Utilizzare l’opzione per scaricare solo i modelli di modulo (XDP), i PDF forms (PDF), il documento (PDF) e le risorse (immagini, schemi, fogli di stile). Puoi modificare queste risorse con applicazioni esterne. Scarica come file zip le risorse che hanno binari, come immagini, PDF e altri formati supportati.
Non è possibile scaricare Forms adattivo, frammenti di modulo adattivi, temi e set di moduli con **[!UICONTROL Scaricare le risorse come file binari]** opzione . Per scaricare queste risorse, utilizza **[!UICONTROL Scarica come pacchetto CRX]** opzione .

   Le risorse selezionate vengono scaricate come archivio (file .zip).

   >[!NOTE]
   >
   >Sia il pacchetto AEM che i file binari vengono scaricati come archivio (file .zip). I modelli per le risorse non vengono scaricati insieme alle risorse. È necessario esportare i modelli di risorse separatamente.

## Caricare Forms adattivo, PDF forms o risorse correlate {#upload-forms-amp-documents-assets}

Puoi caricare i tipi di risorse supportati singolarmente o come archivio ZIP. Per un file ZIP, vengono visualizzati i percorsi relativi di tutte le risorse supportate. Le risorse non supportate all&#39;interno dello ZIP vengono ignorate e non elencate. Tuttavia, se l’archivio ZIP contiene solo le risorse non supportate, viene visualizzato un messaggio di errore invece della finestra di dialogo a comparsa.
Per caricare un modulo o una risorsa correlata:

1. Accedi al tuo [!DNL AEM Forms] istanza.
1. Tocca **[!UICONTROL Adobe Experience Manager]** ![adobeexperiencemanager](assets/adobeexperiencemanager.png) icona > **[!UICONTROL Navigazione]** ![bussola](assets/Smock_Compass_18_N.svg) icona > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Tocca **[!UICONTROL Crea]** > **[!UICONTROL Caricamento file]**. Viene visualizzata una finestra di dialogo.
1. Nella finestra di dialogo, sfoglia e seleziona il pacchetto o l’archivio da importare. È inoltre possibile selezionare altri tipi di file supportati. Tocca **[!UICONTROL Apri]**. La cartella o il nome del file selezionato non deve includere caratteri speciali.

   Nella finestra di dialogo, verifica i dettagli delle risorse caricate e tocca **[!UICONTROL Carica]**.

   Se carichi una risorsa di moduli esistente, la risorsa viene aggiornata.

   >[!NOTE]
   >
   > * Quando un nome è in conflitto con tipi di risorse diversi, il caricamento di un pacchetto non sostituisce la gerarchia di cartelle esistente. Ad esempio, se disponi di un modulo adattivo denominato &quot;Training&quot; in posizione /content/dam/formsanddocuments su un server. Scarica il modulo adattivo e caricalo su un altro server. Il secondo server ha anche una cartella denominata &#39;Training&#39; nella stessa posizione /content/dam/formsanddocuments. Il caricamento non riesce.
   > * Solo un membro del `form-power-user` gruppo può caricare file XDP.



## Scaricare un tema {#downloading-a-theme}

Puoi esportare i temi in [!DNL AEM Forms] che puoi utilizzare in altri progetti o istanze. AEM consente di scaricare i temi come file zip, che puoi caricare sull’istanza.

Per scaricare un tema:

1. Accedi al tuo [!DNL AEM Forms] istanza.
1. Tocca **[!UICONTROL Adobe Experience Manager]** ![adobeexperiencemanager](assets/adobeexperiencemanager.png) icona > **[!UICONTROL Navigazione]** ![bussola](assets/Smock_Compass_18_N.svg) icona > **[!UICONTROL Forms]** > **[!UICONTROL Temi]**.
1. Seleziona il tema e tocca **[!UICONTROL Scarica]**. Il tema viene scaricato come archivio (file .zip).

## Caricare un tema {#uploading-a-theme}

È possibile caricare e utilizzare i temi creati da altri nei moduli. Per caricare un tema:

1. Ad Experience Manager, passa a **[!UICONTROL Forms]** > **[!UICONTROL Temi]**.
1. Nella pagina Temi fare clic su **[!UICONTROL Crea]** > **[!UICONTROL Caricamento file]**.
1. Nel prompt Caricamento file, sfoglia e seleziona un pacchetto tema sul computer e fai clic su **[!UICONTROL Carica]**. Il tema caricato è disponibile nella pagina dei temi.

<!-- ## Import and export assets in Correspondence Management {#import-and-export-assets-in-correspondence-management}

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

<!-- ### Import Document Fragments, Letters and/or Data Dictionaries into Correspondence Management {#import-document-fragments-letters-and-or-data-dictionaries-into-correspondence-management}

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
   >For you to be able to upload XDPs (as part of the cmp file or otherwise), you need to be a part of forms-power-users group. For access rights, contact the administrator. -->

## Esportare un’applicazione di flusso di lavoro {#export-a-workflow-application}

Puoi utilizzare il gestore dei pacchetti per esportare le applicazioni del flusso di lavoro. La procedura è la seguente:

1. Apri [!DNL AEM Forms] gestore dei pacchetti. L&#39;URL del gestore dei pacchetti è `https://[server]:[port]/crx/packmgr`.
1. Fai clic su **[!UICONTROL Crea pacchetto]**. La **[!UICONTROL Nuovo pacchetto]** viene visualizzata la finestra di dialogo.
1. Specifica il nome, la versione e il gruppo del pacchetto. Fai clic su **[!UICONTROL OK]**.
1. Fai clic su **[!UICONTROL Modifica]** e aprire **[!UICONTROL Filtri]** scheda . Fai clic su **[!UICONTROL Aggiungi filtro]**. Specifica il percorso dell’applicazione del flusso di lavoro. Ad esempio, /etc/fd/dashboard/startpoints/homemortgage. Fai clic su **[!UICONTROL Aggiungi regola]**.

1. Apri la scheda **[!UICONTROL Avanzate.]** Seleziona **[!UICONTROL Unisci]** o **[!UICONTROL Sovrascrittura]** nel campo Gestione ACL. Fai clic su **[!UICONTROL Salva]**.
1. Fai clic su **[!UICONTROL Crea]** per creare il pacchetto.

   Una volta generato il pacchetto, puoi scaricarlo e importarlo nell’altro server. L&#39;applicazione del flusso di lavoro viene visualizzata sul server in cui viene caricato il pacchetto.

   >[!NOTE]
   >
   >Affinché l’applicazione del flusso di lavoro funzioni correttamente, esporta anche il corrispondente modello di modulo adattivo e di flusso di lavoro con l’applicazione di lavoro.

## Utilizzare le cartelle per organizzare Forms adattivo, PDF forms e risorse correlate  {#folders-and-organizing-assets}

È possibile utilizzare le cartelle per disporre e organizzare le risorse. L’organizzazione di documenti e risorse in una cartella consente di raggruppare i file per facilitarne la gestione. È possibile selezionare una cartella e scegliere di scaricarla o eliminarla. Per creare una cartella, completa i passaggi seguenti:

### Crea una cartella . {#create-a-folder}

1. Accedi al tuo [!DNL AEM Forms] istanza.
1. Tocca Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) icona > navigazione ![bussola](assets/Smock_Compass_18_N.svg) icon> **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**.
1. Tocca **[!UICONTROL Crea]** > **[!UICONTROL Cartella]**.
1. Immetti i seguenti dettagli:

   * **[!UICONTROL Titolo]**: Nome visualizzato della cartella
   * **[!UICONTROL Nome]**: *(Obbligatorio)* Nome del nodo in cui si desidera memorizzare la cartella nel repository

   >[!NOTE]
   >
   >Per impostazione predefinita, il valore del campo nome viene compilato automaticamente a partire dal titolo. Il nome può contenere solo caratteri alfanumerici oppure i trattini (-) e i caratteri speciali carattere di sottolineatura (_). Tutti gli altri caratteri speciali immessi nel titolo vengono automaticamente sostituiti con un trattino e viene richiesto di confermare il nuovo nome. Puoi scegliere di continuare con il nome suggerito o modificarlo ulteriormente.

1. Nella posizione corrente nell’elenco delle risorse viene visualizzata una nuova cartella con il titolo definito.

   Se esiste una cartella con il nome specificato, l’invio non riesce e viene visualizzato un errore. Puoi visualizzare il messaggio di errore passando il cursore sopra l’errore ![aem6forms_error_alert](assets/Smock_Alert_18_N.svg) accanto al campo nome.

   Tocca la cartella appena creata per entrare nella cartella e creare risorse o cartelle all’interno della cartella. Inoltre, puoi selezionare una cartella e scegliere di accodarla per il download, eliminarla o modificarne il nome.


<!-- ### Create copies of one or more assets or letters {#create-copies-of-one-or-more-assets-or-letters}

You can use an existing assets to quickly create an asset with similar properties, content, and inherited assets.

Complete the following steps to create copies of assets and letters:

1. On the relevant assets page, select one or more assets. The UI displays the Copy icon.
1. Tap **[!UICONTROL Copy]**. The UI displays the **[!UICONTROL Paste]** icon. You can also choose to go/navigate inside a folder before you paste. Different folders can contain assets with same names. For more information on folders, see [Folders and organizing assets](#folders-and-organizing-assets).
1. Tap **[!UICONTROL Paste]**. The **[!UICONTROL Paste]** dialog appears. The system auto generates names and titles to the new copies of assets/letters, but you can edit the titles and names of the assets/letters.

   If you are copying and pasting the assets/letters at the same place, a suffix "-CopyXX" gets added to the existing name of the asset/letter. If no title existed for the copied asset/letter, the auto generated title field remains blank.

1. If required, edit the Title and Name with which you want to save the copy of the asset/letter.
1. Tap **[!UICONTROL Paste]**. New copies of the copied assets are created.

## Search {#search-forms}

You ca use the top bar **[A]** to search your content. When you search for assets, a side panel is displayed. You can also tap ![assets-browser-content-only](assets/assets-browser-content-only.png) &gt; Filter **[B]** to invoke the side panel. Using the various filters in the side panel, you can narrow down your search. The side panel also allows you to save your searches.

![search_topbar](assets/search_topbar.png)

**A.** Search **B.** Filter

![Side panel - Filters](assets/search_sidepanel.png)

Side panel - Filters

On the side panel, you can use the following to narrow down your search results:

* Search Directory
* Tags
* Search Criteria; for example, Modified Dates, Publish Status, LiveCopy Status.

The side panel also allows you to save your search settings with names of your choice.

For more information and instructions on using search, filters, saved search, and side panel, see [Search](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html). -->
