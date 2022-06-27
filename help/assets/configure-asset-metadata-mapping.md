---
title: Configurare la mappatura dei metadati delle risorse tra Workfront e Experience Manager Assets
description: Mappa i campi dei metadati della risorsa tra Adobe Workfront e le applicazioni Experience Manager as a Cloud Service. Come risultato della mappatura dei campi di metadati, quando invii una risorsa da Workfront a Experience Manager Assets, puoi visualizzare i metadati della risorsa mappata in Experience Manager Assets.
source-git-commit: 212ecb5330de739b2e479d36462953ce33697c1c
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 0%

---

# Configurare la mappatura dei metadati delle risorse tra Adobe Workfront e Experience Manager Assets {#asset-metadata-mapping-workfront-aem-assets}

Puoi mappare i campi dei metadati delle risorse tra Adobe Workfront e le applicazioni Experience Manager as a Cloud Service. Come risultato della mappatura dei campi di metadati, quando invii una risorsa da Workfront a Experience Manager Assets, puoi visualizzare i metadati della risorsa mappata in Experience Manager Assets.

Ad esempio, se devi conservare i campi di metadati di un’immagine, come nome, descrizione e progetto a cui appartiene in Workfront quando invii l’immagine a Experience Manager Assets, configura e mappa tali campi nelle proprietà Experience Manager Assets.

**Caso d’uso**

Un&#39;immagine `add-users-workfront.png` esiste in `Metadata Syncs` nell’applicazione Adobe Workfront. Devi inviare l’immagine ad Experience Manager Assets as a Cloud Service con i seguenti metadati:

* Nome progetto

* Nome documento

* Descrizione documento

## Prerequisiti {#prerequisites}

* Accesso amministratore alle applicazioni as a Cloud Service Workfront e Experience Manager Assets.

* Integrazione tra [Applicazioni as a Cloud Service Workfront e Experience Manager Assets](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FDocuments%2FAdobe_Workfront_for_Experience_Manager_Assets_Essentials%2Fsetup-asset-essentials.htm&amp;_LANG=enus).

## Impostare la mappatura dei metadati in Workfront {#set-up-metadata-mapping}

Per impostare la mappatura dei metadati per i campi Nome progetto, Nome documento e Descrizione documento in Workfront:

1. Fai clic sull’icona Menu principale ![Mostra menu](assets/show-menu.svg) disponibile nell’angolo superiore destro dell’applicazione Adobe Workfront, quindi fai clic su **[!UICONTROL Configurazione]**.

1. Seleziona **[!UICONTROL Documenti]** nel pannello a sinistra, seleziona **[!UICONTROL Experience Manager Assets]**.

1. Seleziona l’integrazione Experience Manager Assets e fai clic su **[!UICONTROL Modifica]**.

1. Fai clic su **[!UICONTROL Metadati]**. In **[!UICONTROL Risorse]** mappa [!UICONTROL Progetto] > [!UICONTROL Nome] Campo Workfront per `wm:projectName` Campo Experience Manager Assets. Se non trovi la corrispondenza esatta, Adobe consiglia di cercare la corrispondenza migliore per mappare il campo Workfront e Experience Manager Assets . Puoi evitare la mappatura di campi di diversi tipi di dati. Ad esempio, mappare un campo Workfront data in un campo Risorse descrizione.
1. Mappa la [!UICONTROL Documento] > [!UICONTROL Nome] Campo Workfront per `wm:documentName` Campo Experience Manager Assets.

   ![Mappatura in Workfront](assets/workfront-metadata-mapping.png)

1. Mappa la [!UICONTROL Documento] > [!UICONTROL Descrizione] Campo Workfront per `dc:description` Campo Experience Manager Assets.

   >[!VIDEO](https://video.tv.adobe.com/v/344255)

## Inviare l&#39;immagine da Workfront a Experience Manager Assets {#send-image-workfront-assets}

Per inviare l&#39;immagine da Workfront a Experience Manager Assets:

1. Fai clic sull’icona Menu principale ![Mostra menu](assets/show-menu.svg) disponibile nell’angolo superiore destro dell’applicazione Adobe Workfront, quindi fai clic su **[!UICONTROL Progetti]**.

1. Fai clic su **[!UICONTROL Nuovo progetto]** per creare un nuovo progetto.

1. Fai clic su **[!UICONTROL Documenti]** nel riquadro a sinistra, trascina e seleziona l’immagine da inviare a Experience Manager Assets.

1. Fai clic su **[!UICONTROL Invia a]**, quindi scegli il nome dell’integrazione Experience Manager Assets Essentials.

   ![Invia a AEM](assets/send-to-aem.png)

1. Scegli la cartella di destinazione della risorsa, quindi fai clic su **[!UICONTROL Seleziona cartella]**.

1. Fai clic su **[!UICONTROL Salva]**.

## Configurare la mappatura dei metadati delle risorse in Experience Manager as a Cloud Service {#metadata-mapping-aem}

Dopo [configurazione della mappatura dei metadati delle risorse in Adobe Workfront](#set-up-metadata-mapping), è necessario utilizzare la stessa mappatura nell’applicazione Experience Manager Assets as a Cloud Service per visualizzare i risultati dei metadati appropriati per l’immagine.

La mappatura dei metadati viene eseguita utilizzando gli schemi di metadati in Experience Manager Assets. È possibile modificare un modulo schema metadati appena aggiunto o esistente. Il modulo schema metadati include schede ed elementi modulo all’interno di schede. Puoi mappare/configurare questi elementi del modulo su un campo all’interno di un nodo di metadati nell’archivio CRX. È possibile aggiungere schede o elementi modulo al modulo schema metadati. Per ulteriori informazioni, consulta [Schemi metadati](metadata-schemas.md).

Per configurare la mappatura dei metadati utilizzando un nuovo modulo metadati in Experience Manager Assets as a Cloud Service:

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Schemi metadati]**.

1. Fai clic su **[!UICONTROL Crea]** dalla barra degli strumenti. Nella finestra di dialogo, fornisci il titolo del modulo schema e fai clic su **[!UICONTROL Crea]** per completare il processo di creazione del modulo.

1. Seleziona il modulo schema e fai clic su **[!UICONTROL Modifica]**.

1. (Facoltativo) Nell’Editor moduli schema metadati, fai clic su `+` per creare una nuova scheda per i campi Workfront.

1. Fai clic sul pulsante **[!UICONTROL Crea modulo]** e trascina **[!UICONTROL Testo a riga singola]** al modulo. Fai clic sul componente nel modulo. In **[!UICONTROL Crea modulo]** scheda:

   1. Specifica `Project Name` in **[!UICONTROL Etichetta campo]** campo .

   1. Specifica `./jcr:content/metadata/wm:projectName` in **[!UICONTROL Mappa su proprietà]** campo . Come linea guida, utilizza il seguente modello per definire le mappature dei campi in Experience Manager Assets:
      `./jcr:content/metadata/<mapping defined for the field in workfront>`.

      Durante la configurazione delle mappature in Workfront, hai mappato `wm:projectName` Campo Experience Manager Assets in Progetto > Nome campo Workfront .

      `wm` fa riferimento al nome dello spazio dei nomi e `projectName` fa riferimento al titolo della proprietà. Utilizza la `namespace:propertyTitle` per definire le mappature dei campi metadati.

      ![Invia a AEM](assets/metadata-schema-mapping.png)

1. Fai clic sul pulsante **[!UICONTROL Crea modulo]** e trascina **[!UICONTROL Testo a riga singola]** al modulo. Fai clic sul componente nel modulo. In **[!UICONTROL Crea modulo]** scheda:

   1. Specifica `Document Name` in **[!UICONTROL Etichetta campo]** campo .

   1. Specifica `./jcr:content/metadata/wm:documentName` in **[!UICONTROL Mappa su proprietà]** campo .
Durante la configurazione delle mappature in Workfront, hai mappato `wm:documentName` Campo Experience Manager Assets in Documento > Nome campo Workfront.

1. Fai clic sul pulsante **[!UICONTROL Crea modulo]** e trascina **[!UICONTROL Testo a più righe]** al modulo. Fai clic sul componente nel modulo. In **[!UICONTROL Crea modulo]** scheda:

   1. Specifica `Document Description` in **[!UICONTROL Etichetta campo]** campo .

   1. Specifica `./jcr:content/metadata/dc:description` in **[!UICONTROL Mappa su proprietà]** campo .
Durante la configurazione delle mappature in Workfront, hai mappato `dc:description` Campo Experience Manager Assets in Documento > Descrizione Campo Workfront.

1. Fai clic su **[!UICONTROL Salva]** per salvare le modifiche.

   >[!VIDEO](https://video.tv.adobe.com/v/344314)

## Applicare le impostazioni metadati alla cartella immagine {#apply-metadata-settings-image-folder}

Dopo aver configurato le impostazioni dei metadati nell&#39;applicazione as a Cloud Service di Experience Manager, applica tali impostazioni al [cartella contenente l&#39;immagine inviata dall&#39;applicazione Workfront](#send-image-workfront-assets).

Per applicare le impostazioni metadati alla cartella immagine:

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Schemi metadati]**.

1. Seleziona lo schema metadati dall’elenco disponibile e fai clic su **[!UICONTROL Applica a cartelle]**.

1. Selezionare la cartella di destinazione in cui [l’immagine viene inviata dall’applicazione Adobe Workfront](#send-image-workfront-assets) e fai clic su **[!UICONTROL Applica]**.

Puoi passare all’immagine in Experience Manager Assets e visualizzare i metadati associati all’immagine. Seleziona l’immagine e fai clic su **[!UICONTROL Proprietà]** per visualizzare i metadati dell&#39;immagine.



