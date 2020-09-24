---
title: Filigrana le risorse
description: Aggiungi una filigrana alle risorse digitali.
contentOwner: AG
translation-type: tm+mt
source-git-commit: f1fcddf196a1a2bfa2629dbd6a8fe0ac057a3d07
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Filigrana le risorse {#watermark-assets}

[!DNL Adobe Experience Manager Assets] consente di aggiungere una filigrana digitale alle immagini. [!DNL Assets] supporta l’applicazione di un’immagine come filigrana ad altri file di immagine. Le filigrane possono aiutare gli utenti a verificare l’autenticità e la proprietà dei diritti d’autore delle risorse. È inoltre possibile utilizzare una filigrana per indicare lo stato di un documento come confidenziale, bozza, validità e così via.

Per configurare  Experience Manager in filigrane, effettuate le seguenti operazioni:

1. Un file PNG viene applicato come filigrana. Caricate questo file nell&#39;archivio DAM.

1. Accedi al repository Git di Cloud Manager associato al tuo ambiente. Commit di un file denominato `com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.json` nel repository Git di Cloud Manager con i seguenti contenuti. Per ulteriori dettagli, consultate [come eseguire la configurazione OSGi in  Experience Manager come Cloud Service](/help/implementing/deploying/configuring-osgi.md).

   ```json
   {
   "watermark": "/content/dam/<path-to-watermark-image.png>",
    "width": 100
   }
   ```

1. [Create un profilo](/help/assets/asset-microservices-configure-and-use.md#create-custom-profile) di elaborazione per utilizzare i microservizi delle risorse per applicare la filigrana.

   ![Profilo di elaborazione delle risorse per creare una filigrana](assets/watermark-processing-profile.png)

1. [Applicate i profili di elaborazione a una cartella](/help/assets/asset-microservices-configure-and-use.md#use-profiles) per creare risorse con filigrana.

## Suggerimenti e limitazioni {#tips-limitations-bestpractices}

* Potete usare una singola configurazione per applicare una filigrana a tutte le risorse. Per le filigrane viene utilizzata una sola immagine e la relativa larghezza è fissa.
* È possibile posizionare la filigrana al centro senza ripeterne l&#39;inclinazione.
* Le filigrane basate su testo non sono supportate.

>[!MORELIKETHIS]
>
>* [Panoramica](/help/assets/asset-microservices-overview.md)dei microservizi di risorse.
>* [Utilizzare i microservizi di risorse con i profili](/help/assets/asset-microservices-configure-and-use.md)di elaborazione.

