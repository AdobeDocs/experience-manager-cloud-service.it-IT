---
title: Filigrana delle risorse
description: Aggiungi una filigrana alle risorse digitali.
contentOwner: AG
translation-type: tm+mt
source-git-commit: af27295b618fb3909d43ed94a74148f7c4f59c10
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Filigrana delle risorse {#watermark-assets}

[!DNL Adobe Experience Manager Assets] consente di aggiungere una filigrana digitale alle immagini. [!DNL Assets] supporta l’applicazione di un’immagine come filigrana ad altri file di immagine. Le filigrane possono aiutare gli utenti a verificare l’autenticità e la proprietà dei diritti d’autore delle risorse. È inoltre possibile utilizzare una filigrana per indicare lo stato di un documento come confidenziale, bozza, validità e così via.

Per configurare [!DNL Experience Manager] per le risorse delle filigrane, effettuate le seguenti operazioni:

1. Un file PNG viene applicato come filigrana. Caricate questo file nell&#39;archivio DAM.

1. Accedere al repository Git [!DNL Cloud Manager] associato al proprio ambiente. Confermate un file denominato `com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.cfg.json` nella directory archivio con i seguenti contenuti. Per istruzioni, vedere [come eseguire la configurazione OSGi in [!DNL Experience Manager] come Cloud Service](/help/implementing/deploying/configuring-osgi.md).

   ```json
   {
   "watermark": "/content/dam/<path-to-watermark-image.png>",
    "width": 100
   }
   ```

1. [Create un ](/help/assets/asset-microservices-configure-and-use.md#create-custom-profile) profilo di elaborazione per utilizzare i microservizi delle risorse per applicare la filigrana.

   ![Profilo di elaborazione delle risorse per creare una filigrana](assets/watermark-processing-profile.png)

1. [Applicate i profili di elaborazione a una ](/help/assets/asset-microservices-configure-and-use.md#use-profiles) cartella per creare risorse con filigrana.

## Suggerimenti e limitazioni {#tips-limitations-bestpractices}

* Potete usare una singola configurazione per applicare una filigrana a tutte le risorse. Per le filigrane viene utilizzata una sola immagine e la relativa larghezza è fissa.
* È possibile posizionare la filigrana al centro senza ripeterne l&#39;inclinazione.
* Le filigrane basate su testo non sono supportate.

>[!MORELIKETHIS]
>
>* [Panoramica](/help/assets/asset-microservices-overview.md) dei microservizi di risorse.
>* [Utilizzare i microservizi di risorse con i profili](/help/assets/asset-microservices-configure-and-use.md) di elaborazione.

