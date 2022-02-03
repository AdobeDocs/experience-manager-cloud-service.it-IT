---
title: Filtrare le risorse
description: Aggiungi una filigrana alle risorse digitali.
contentOwner: AG
feature: Asset Management,Publishing
role: User,Admin
exl-id: 210f8925-bd15-4b4a-8714-5a1486eeb49e
source-git-commit: 8f7dc67a8335822b51e4c7796ab55244199fb214
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 1%

---

# Filtrare le risorse {#watermark-assets}

[!DNL Adobe Experience Manager Assets] consente di aggiungere una filigrana digitale alle immagini. [!DNL Assets] supporta l’applicazione di un’immagine come filigrana ad altri file di immagine. Le filigrane possono aiutare gli utenti a verificare l’autenticità e la proprietà del copyright delle risorse. Inoltre, una filigrana può essere utilizzata per indicare lo stato di un documento come confidenziale, bozza, validità e così via.

>[!NOTE]
>
>Questa funzione è disponibile nel canale prerelease. Vedi [Documentazione sul canale prerelease](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=en#enable-prerelease) per informazioni su come abilitare la funzione per l’ambiente.

Per configurare [!DNL Experience Manager] per applicare una filigrana alle risorse:

1. Un file PNG viene applicato come filigrana. Carica questo file nel tuo archivio DAM.

1. Passa a **[!UICONTROL Strumenti > Risorse > Configurazioni risorse]**.

1. Fai clic su **[!UICONTROL Profilo di filigrana del sistema]**.

1. Sulla [!UICONTROL Pagina del profilo di filigrana del sistema], specifica il percorso immagine caricato nell’archivio DAM al passaggio 1.

1. Specifica la scala della filigrana, da 0,0 a 1,0, relativa alla larghezza del rendering, nella **[!UICONTROL Scala]** campo .

1. Fai clic su **[!UICONTROL Salva]**.

   ![Rilevamento duplicazione risorse](assets/system-watermarking-profile.png)

   >[!NOTE]
   >
   >Se hai configurato il profilo di filigrana di sistema utilizzando `com.adobe.cq.assetcompute.impl.profile.WatermarkingProfileServiceImpl.cfg.json` file di configurazione (configurazione OSGi), è possibile continuare a utilizzarlo, tuttavia, Adobe consiglia di utilizzare il nuovo metodo.


1. [Creare un profilo di elaborazione](/help/assets/asset-microservices-configure-and-use.md#create-custom-profile) per sfruttare i microservizi delle risorse per applicare la filigrana.

   ![Profilo di elaborazione delle risorse per creare una filigrana](assets/watermark-processing-profile.png)

   Assicurati di abilitare il **[!UICONTROL Filigrana]** durante la creazione del profilo di elaborazione.

1. [Applicare i profili di elaborazione a una cartella](/help/assets/asset-microservices-configure-and-use.md#use-profiles) per creare risorse con filigrana.

## Suggerimenti e limitazioni {#tips-limitations-bestpractices}

* Puoi utilizzare una singola configurazione per applicare una filigrana a tutte le risorse. Per la filigrana viene utilizzata una sola immagine e la sua larghezza è fissa.
* È possibile posizionare la filigrana al centro senza piastrelle.
* Le filigrane basate su testo non sono supportate.

>[!MORELIKETHIS]
>
>* [Panoramica dei microservizi per le risorse](/help/assets/asset-microservices-overview.md).
>* [Utilizzare i microservizi per le risorse con i profili di elaborazione](/help/assets/asset-microservices-configure-and-use.md).

