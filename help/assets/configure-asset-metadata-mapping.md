---
title: Configurare la mappatura dei metadati delle risorse tra Workfront e Experience Manager Assets
description: Mappa i campi di metadati delle risorse tra le applicazioni Adobe Workfront e Experience Manager as a Cloud Service. Come risultato della mappatura dei campi di metadati, quando invii una risorsa da Workfront a Experience Manager Assets, puoi visualizzare i metadati della risorsa mappata in Experience Manager Assets.
exl-id: 71400769-b2bc-4f5d-8b6b-a73598e837b4
source-git-commit: e2505c0fec1da8395930f131bfc55e1e2ce05881
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 4%

---

# Configurare la mappatura dei metadati delle risorse tra Adobe Workfront e Experience Manager Assets {#asset-metadata-mapping-workfront-aem-assets}

Puoi mappare i campi di metadati delle risorse tra Adobe Workfront e le applicazioni Experience Manager as a Cloud Service. Come risultato della mappatura dei campi di metadati, quando invii una risorsa da Workfront a Experience Manager Assets, puoi visualizzare i metadati della risorsa mappata in Experience Manager Assets.

Workfront Ad esempio, se quando invii l’immagine a Experience Manager Assets devi mantenere i campi di metadati per un’immagine come nome, descrizione e il progetto a cui appartiene, configura e mappa questi campi sulle proprietà di Experience Manager Assets.

**Caso d’uso**

Un&#39;immagine `add-users-workfront.png` esiste in `Metadata Syncs` progetto nell’applicazione Adobe Workfront. È necessario inviare l’immagine a Experience Manager Assets as a Cloud Service con i seguenti metadati:

* Nome progetto

* Nome documento

* Descrizione documento

## Prerequisiti {#prerequisites}

* Un amministratore accede alle applicazioni as a Cloud Service di Workfront e Experience Manager Assets.

* Un’integrazione tra [Applicazioni as a Cloud Service Workfront e Experience Manager Assets](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FDocuments%2FAdobe_Workfront_for_Experience_Manager_Assets_Essentials%2Fsetup-asset-essentials.htm&amp;_LANG=enus).

## Configurare la mappatura dei metadati in Workfront {#set-up-metadata-mapping}

Per impostare la mappatura dei metadati per i campi Nome progetto, Nome documento e Descrizione documento in Workfront:

1. Fai clic sull’icona Menu principale ![Mostra menu](assets/show-menu.svg) disponibile nell’angolo superiore destro dell’applicazione Adobe Workfront, quindi fai clic su **[!UICONTROL Configurazione]**.

1. Seleziona **[!UICONTROL Documenti]** nel pannello a sinistra, seleziona quindi **[!UICONTROL Experience Manager Assets]**.

1. Seleziona l’integrazione di Experience Manager Assets e fai clic su **[!UICONTROL Modifica]**.

1. Clic **[!UICONTROL Metadati]**. In **[!UICONTROL Risorse]** , mappare [!UICONTROL Progetto] > [!UICONTROL Nome] Campo Workfront al `wm:projectName` Campo Experience Manager Assets. Se non trovi la corrispondenza esatta, l’Adobe consiglia di cercare la corrispondenza migliore per mappare i campi Workfront e Experience Manager Assets. Puoi evitare di mappare campi di tipi di dati diversi. Ad esempio, mappare un campo Workfront data a un campo Assets descrizione.
1. Mappa il [!UICONTROL Documento] > [!UICONTROL Nome] Campo Workfront al `wm:documentName` Campo Experience Manager Assets.

   ![Mappatura in Workfront](assets/workfront-metadata-mapping.png)

1. Mappa il [!UICONTROL Documento] > [!UICONTROL Descrizione] Campo Workfront al `dc:description` Campo Experience Manager Assets.

   >[!VIDEO](https://video.tv.adobe.com/v/344255)

## Inviare l’immagine da Workfront a Experience Manager Assets {#send-image-workfront-assets}

Per inviare l&#39;immagine da Workfront a Experience Manager Assets:

1. Fai clic sull’icona Menu principale ![Mostra menu](assets/show-menu.svg) disponibile nell’angolo superiore destro dell’applicazione Adobe Workfront, quindi fai clic su **[!UICONTROL Progetti]**.

1. Clic **[!UICONTROL Nuovo progetto]** per creare un progetto.

1. Clic **[!UICONTROL Documenti]** opzione disponibile nel riquadro a sinistra, trascina e seleziona l’immagine da inviare a Experience Manager Assets.

1. Clic **[!UICONTROL Invia a]**, quindi scegli il nome dell’integrazione Experience Manager Assets Essentials.

   ![Invia ad AEM](assets/send-to-aem.png)

1. Scegli la cartella di destinazione della risorsa, quindi fai clic su **[!UICONTROL Seleziona cartella]**.

1. Fai clic su **[!UICONTROL Salva]**.

## Configurare la mappatura dei metadati delle risorse in Experience Manager as a Cloud Service {#metadata-mapping-aem}

Dopo [configurazione della mappatura dei metadati delle risorse in Adobe Workfront](#set-up-metadata-mapping), è necessario utilizzare la stessa mappatura nell’applicazione Experience Manager Assets as a Cloud Service per visualizzare i risultati dei metadati appropriati per l’immagine.

La mappatura dei metadati viene eseguita utilizzando gli schemi di metadati in Experience Manager Assets. Puoi modificare un modulo schema metadati appena aggiunto o esistente. Il modulo schema metadati include schede ed elementi modulo all’interno di schede. Puoi mappare/configurare questi elementi modulo su un campo all’interno di un nodo di metadati nell’archivio CRX. È possibile aggiungere schede o elementi del modulo al modulo schema metadati. Per ulteriori informazioni, consulta [Schemi metadati](metadata-schemas.md).

Per configurare la mappatura dei metadati utilizzando un nuovo modulo metadati in Experience Manager Assets as a Cloud Service:

1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Schemi metadati]**.

1. Clic **[!UICONTROL Crea]** dalla barra degli strumenti. Nella finestra di dialogo, specifica il titolo del modulo schema e fai clic su **[!UICONTROL Crea]** per completare il processo di creazione del modulo.

1. Seleziona il modulo schema e fai clic su **[!UICONTROL Modifica]**.

1. (Facoltativo) Nell’Editor modulo schema metadati, fai clic su `+` per creare una scheda per i campi Workfront.

1. Fai clic su **[!UICONTROL Genera modulo]** e trascinare il **[!UICONTROL Testo su riga singola]** al modulo. Fai clic sul componente nel modulo. In **[!UICONTROL Genera modulo]** scheda:

   1. Specifica `Project Name` nel **[!UICONTROL Etichetta campo]** campo.

   1. Specifica `./jcr:content/metadata/wm:projectName` nel **[!UICONTROL Mappa su proprietà]** campo. Come linea guida, utilizza il seguente modello per definire le mappature dei campi in Experience Manager Assets:
      `./jcr:content/metadata/<mapping defined for the field in workfront>`.

      Durante la configurazione delle mappature in Workfront, hai mappato `wm:projectName` Campo Experience Manager Assets a Progetto > Nome campo Workfront.

      `wm` fa riferimento al nome dello spazio dei nomi e `projectName` fa riferimento al titolo della proprietà. Utilizza il `namespace:propertyTitle` per definire le mappature dei campi di metadati.

      ![Invia ad AEM](assets/metadata-schema-mapping.png)

1. Fai clic su **[!UICONTROL Genera modulo]** e trascinare il **[!UICONTROL Testo su riga singola]** al modulo. Fai clic sul componente nel modulo. In **[!UICONTROL Genera modulo]** scheda:

   1. Specifica `Document Name` nel **[!UICONTROL Etichetta campo]** campo.

   1. Specifica `./jcr:content/metadata/wm:documentName` nel **[!UICONTROL Mappa su proprietà]** campo.
Durante la configurazione delle mappature in Workfront, hai mappato `wm:documentName` Campo Experience Manager Assets in Documento > Nome campo Workfront.

1. Fai clic su **[!UICONTROL Genera modulo]** e trascinare il **[!UICONTROL Testo su più righe]** al modulo. Fai clic sul componente nel modulo. In **[!UICONTROL Genera modulo]** scheda:

   1. Specifica `Document Description` nel **[!UICONTROL Etichetta campo]** campo.

   1. Specifica `./jcr:content/metadata/dc:description` nel **[!UICONTROL Mappa su proprietà]** campo.
Durante la configurazione delle mappature in Workfront, hai mappato `dc:description` Campo Experience Manager Assets in Documento > Campo Workfront descrizione.

1. Clic **[!UICONTROL Salva]** per salvare le modifiche.

   >[!VIDEO](https://video.tv.adobe.com/v/344314)

## Applica impostazioni metadati a cartella immagini {#apply-metadata-settings-image-folder}

Dopo aver configurato le impostazioni dei metadati nell’applicazione Experience Manager as a Cloud Service, applica tali impostazioni alla [cartella contenente l&#39;immagine inviata dall&#39;applicazione Workfront](#send-image-workfront-assets).

Per applicare le impostazioni dei metadati alla cartella di immagini:

1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Schemi metadati]**.

1. Seleziona lo schema metadati dall’elenco disponibile e fai clic su **[!UICONTROL Applica a cartelle]**.

1. Seleziona la cartella di destinazione [l’immagine viene inviata dall’applicazione Adobe Workfront](#send-image-workfront-assets) e fai clic su **[!UICONTROL Applica]**.

Puoi passare all’immagine in Experience Manager Assets e visualizzare i metadati associati all’immagine. Seleziona l’immagine e fai clic su **[!UICONTROL Proprietà]** per visualizzare i metadati dell&#39;immagine.

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)
