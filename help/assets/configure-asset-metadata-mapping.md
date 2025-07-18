---
title: Configurare la mappatura dei metadati delle risorse tra Workfront e Experience Manager Assets
description: Mappa i campi di metadati delle risorse tra le applicazioni Adobe Workfront e Experience Manager as a Cloud Service. Come risultato della mappatura dei campi di metadati, quando invii una risorsa da Workfront a Experience Manager Assets, puoi visualizzare i metadati della risorsa mappata in Experience Manager Assets.
exl-id: 71400769-b2bc-4f5d-8b6b-a73598e837b4
feature: Metadata, Workfront Integrations and Apps
role: User, Admin
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 4%

---

# Configurare la mappatura dei metadati delle risorse tra Adobe Workfront e Experience Manager Assets {#asset-metadata-mapping-workfront-aem-assets}

Puoi mappare i campi di metadati delle risorse tra le applicazioni Adobe Workfront e Experience Manager as a Cloud Service. Come risultato della mappatura dei campi di metadati, quando invii una risorsa da Workfront a Experience Manager Assets, puoi visualizzare i metadati della risorsa mappata in Experience Manager Assets.

Workfront Ad esempio, se quando invii l’immagine a Experience Manager Assets devi mantenere i campi di metadati per un’immagine come nome, descrizione e il progetto a cui appartiene, configura e mappa questi campi sulle proprietà di Experience Manager Assets.

**Caso d’uso**

Un&#39;immagine `add-users-workfront.png` esiste nel progetto `Metadata Syncs` nell&#39;applicazione Adobe Workfront. È necessario inviare l’immagine a Experience Manager Assets as a Cloud Service con i seguenti metadati:

* Nome progetto

* Nome documento

* Descrizione documento

## Prerequisiti {#prerequisites}

* Un amministratore accede alle applicazioni Workfront e Experience Manager Assets as a Cloud Service.

* Integrazione tra [applicazioni Workfront e Experience Manager Assets as a Cloud Service](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&topicId=Content%2FDocuments%2FAdobe_Workfront_for_Experience_Manager_Assets_Essentials%2Fsetup-asset-essentials.htm&_LANG=enus).

## Configurare la mappatura dei metadati in Workfront {#set-up-metadata-mapping}

Per impostare la mappatura dei metadati per i campi Nome progetto, Nome documento e Descrizione documento in Workfront:

1. Fai clic sull&#39;icona Menu principale ![Mostra menu](assets/show-menu.svg) disponibile nell&#39;angolo superiore destro dell&#39;applicazione Adobe Workfront, quindi fai clic su **[!UICONTROL Configurazione]**.

1. Seleziona **[!UICONTROL Documenti]** nel pannello a sinistra, quindi seleziona **[!UICONTROL Experience Manager Assets]**.

1. Seleziona l&#39;integrazione Experience Manager Assets e fai clic su **[!UICONTROL Modifica]**.

1. Fare clic su **[!UICONTROL Metadati]**. Nella scheda **[!UICONTROL Assets]**, mappa il campo Workfront [!UICONTROL Progetto] > [!UICONTROL Nome] con il campo Experience Manager Assets `wm:projectName`. Se non trovi la corrispondenza esatta, Adobe consiglia di cercare la corrispondenza migliore per mappare i campi Workfront e Experience Manager Assets. Puoi evitare di mappare campi di tipi di dati diversi. Ad esempio, la mappatura di un campo Workfront della data su un campo Assets della descrizione.
1. Mappa il campo Workfront [!UICONTROL Document] > [!UICONTROL Name] al campo Experience Manager Assets `wm:documentName`.

   ![Mappatura in Workfront](assets/workfront-metadata-mapping.png)

1. Mappa il campo Workfront [!UICONTROL Documento] > [!UICONTROL Descrizione] al campo Experience Manager Assets `dc:description`.

   >[!VIDEO](https://video.tv.adobe.com/v/344255)

## Inviare l’immagine da Workfront a Experience Manager Assets {#send-image-workfront-assets}

Per inviare l&#39;immagine da Workfront a Experience Manager Assets:

1. Fai clic sull&#39;icona Menu principale ![Mostra menu](assets/show-menu.svg) disponibile nell&#39;angolo superiore destro dell&#39;applicazione Adobe Workfront, quindi fai clic su **[!UICONTROL Progetti]**.

1. Fai clic su **[!UICONTROL Nuovo progetto]** per creare un progetto.

1. Fai clic sull&#39;opzione **[!UICONTROL Documenti]** disponibile nel riquadro a sinistra, trascina e seleziona l&#39;immagine da inviare a Experience Manager Assets.

1. Fai clic su **[!UICONTROL Invia a]**, quindi scegli il nome dell&#39;integrazione Experience Manager Assets Essentials.

   ![Invia ad AEM](assets/send-to-aem.png)

1. Scegliere la cartella di destinazione della risorsa, quindi fare clic su **[!UICONTROL Seleziona cartella]**.

1. Fai clic su **[!UICONTROL Salva]**.

## Configurare la mappatura dei metadati delle risorse in Experience Manager as a Cloud Service {#metadata-mapping-aem}

Dopo la [configurazione della mappatura dei metadati delle risorse in Adobe Workfront](#set-up-metadata-mapping), è necessario utilizzare la stessa mappatura nell&#39;applicazione Experience Manager Assets as a Cloud Service per visualizzare i risultati dei metadati appropriati per l&#39;immagine.

La mappatura dei metadati viene eseguita utilizzando gli schemi di metadati in Experience Manager Assets. Puoi modificare un modulo schema metadati appena aggiunto o esistente. Il modulo schema metadati include schede ed elementi modulo all’interno di schede. Puoi mappare/configurare questi elementi modulo su un campo all’interno di un nodo di metadati nell’archivio CRX. È possibile aggiungere schede o elementi del modulo al modulo schema metadati. Per ulteriori informazioni, vedere [Schemi metadati](metadata-schemas.md).

Per configurare la mappatura dei metadati utilizzando un nuovo modulo metadati in Experience Manager Assets as a Cloud Service:

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Schemi metadati]**.

1. Fai clic su **[!UICONTROL Crea]** nella barra degli strumenti. Nella finestra di dialogo, specifica il titolo del modulo schema e fai clic su **[!UICONTROL Crea]** per completare il processo di creazione del modulo.

1. Seleziona il modulo schema e fai clic su **[!UICONTROL Modifica]**.

1. (Facoltativo) Nell&#39;Editor modulo schema metadati fare clic su `+` per creare una scheda per i campi Workfront.

1. Fai clic sulla scheda **[!UICONTROL Genera modulo]** e trascina nel modulo il componente **[!UICONTROL Testo a riga singola]**. Fai clic sul componente nel modulo. Nella scheda **[!UICONTROL Genera modulo]**:

   1. Specificare `Project Name` nel campo **[!UICONTROL Etichetta campo]**.

   1. Specificare `./jcr:content/metadata/wm:projectName` nel campo **[!UICONTROL Mappa su proprietà]**. Come linea guida, utilizza il seguente modello per definire le mappature dei campi in Experience Manager Assets:

      `./jcr:content/metadata/<mapping defined for the field in workfront>`.

      Durante la configurazione delle mappature in Workfront, hai mappato il campo Experience Manager Assets `wm:projectName` al campo Progetto > Nome Workfront.

      `wm` fa riferimento al nome dello spazio dei nomi e `projectName` al titolo della proprietà. Utilizza il formato `namespace:propertyTitle` per definire le mappature dei campi di metadati.

      ![Invia ad AEM](assets/metadata-schema-mapping.png)

1. Fai clic sulla scheda **[!UICONTROL Genera modulo]** e trascina nel modulo il componente **[!UICONTROL Testo a riga singola]**. Fai clic sul componente nel modulo. Nella scheda **[!UICONTROL Genera modulo]**:

   1. Specificare `Document Name` nel campo **[!UICONTROL Etichetta campo]**.

   1. Specificare `./jcr:content/metadata/wm:documentName` nel campo **[!UICONTROL Mappa su proprietà]**.
Durante la configurazione delle mappature in Workfront, hai mappato il campo Experience Manager Assets `wm:documentName` al campo Documento > Nome Workfront.

1. Fai clic sulla scheda **[!UICONTROL Genera modulo]** e trascina nel modulo il componente **[!UICONTROL Testo su più righe]**. Fai clic sul componente nel modulo. Nella scheda **[!UICONTROL Genera modulo]**:

   1. Specificare `Document Description` nel campo **[!UICONTROL Etichetta campo]**.

   1. Specificare `./jcr:content/metadata/dc:description` nel campo **[!UICONTROL Mappa su proprietà]**.
Durante la configurazione delle mappature in Workfront, hai mappato il campo Experience Manager Assets `dc:description` al campo Workfront Documento > Descrizione.

1. Fai clic su **[!UICONTROL Salva]** per salvare le modifiche.

   >[!VIDEO](https://video.tv.adobe.com/v/344314)

## Applica impostazioni metadati a cartella immagini {#apply-metadata-settings-image-folder}

Dopo aver configurato le impostazioni dei metadati nell&#39;applicazione Experience Manager as a Cloud Service, applicare tali impostazioni alla cartella [contenente l&#39;immagine inviata dall&#39;applicazione Workfront](#send-image-workfront-assets).

Per applicare le impostazioni dei metadati alla cartella di immagini:

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Schemi metadati]**.

1. Selezionare lo schema metadati dall&#39;elenco disponibile e fare clic su **[!UICONTROL Applica alle cartelle]**.

1. Seleziona la cartella di destinazione a cui [l&#39;immagine viene inviata dall&#39;applicazione Adobe Workfront](#send-image-workfront-assets) e fai clic su **[!UICONTROL Applica]**.

Puoi passare all’immagine in Experience Manager Assets e visualizzare i metadati associati all’immagine. Seleziona l&#39;immagine e fai clic su **[!UICONTROL Proprietà]** per visualizzarne i metadati.

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
* [Pubblicare risorse in AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
