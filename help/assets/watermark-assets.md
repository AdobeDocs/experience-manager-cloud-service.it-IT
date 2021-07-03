---
title: Filtrare le risorse
description: Aggiungi una filigrana alle risorse digitali.
contentOwner: AG
feature: Gestione risorse,Pubblicazione
role: User,Admin
exl-id: 210f8925-bd15-4b4a-8714-5a1486eeb49e
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# Filtrare le risorse {#watermark-assets}

[!DNL Adobe Experience Manager Assets] consente di aggiungere una filigrana digitale alle immagini. [!DNL Assets] supporta l’applicazione di un’immagine come filigrana ad altri file di immagine. Le filigrane possono aiutare gli utenti a verificare l’autenticità e la proprietà del copyright delle risorse. Inoltre, una filigrana può essere utilizzata per indicare lo stato di un documento come confidenziale, bozza, validità e così via.

Per configurare [!DNL Experience Manager] in modo che le risorse vengano filigrate, effettua le seguenti operazioni:

1. Un file PNG viene applicato come filigrana. Carica questo file nel tuo archivio DAM.

1. Accedi all’ archivio Git [!DNL Cloud Manager] associato al tuo ambiente. Commit di un file denominato `com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.cfg.json` nell’archivio con il seguente contenuto. Per istruzioni, consulta [come eseguire la configurazione OSGi in [!DNL Experience Manager] come a [!DNL Cloud Service]](/help/implementing/deploying/configuring-osgi.md).

   ```json
   {
   "watermark": "/content/dam/<path-to-watermark-image.png>",
    "width": 100
   }
   ```

1. [Crea un ](/help/assets/asset-microservices-configure-and-use.md#create-custom-profile) profilo di elaborazione per sfruttare i microservizi delle risorse per applicare la filigrana.

   ![Profilo di elaborazione delle risorse per creare una filigrana](assets/watermark-processing-profile.png)

1. [Applica i profili di elaborazione a una ](/help/assets/asset-microservices-configure-and-use.md#use-profiles) cartella per creare risorse con filigrana.

## Suggerimenti e limitazioni {#tips-limitations-bestpractices}

* Puoi utilizzare una singola configurazione per applicare una filigrana a tutte le risorse. Per la filigrana viene utilizzata una sola immagine e la sua larghezza è fissa.
* È possibile posizionare la filigrana al centro senza piastrelle.
* Le filigrane basate su testo non sono supportate.

>[!MORELIKETHIS]
>
>* [Panoramica dei microservizi per le risorse](/help/assets/asset-microservices-overview.md).
>* [Utilizza i microservizi per le risorse con i profili](/help/assets/asset-microservices-configure-and-use.md) di elaborazione.

