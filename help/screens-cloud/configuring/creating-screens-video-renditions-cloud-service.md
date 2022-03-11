---
title: Creazione di rappresentazioni video in Screens as a Cloud Service
description: Questa pagina descrive come creare rappresentazioni video in Screens as a Cloud Service.
exl-id: a9c46036-cd29-47fa-81d9-c865cf22c98a
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# Creazione di rappresentazioni video in Screens as a Cloud Service {#creating-screens-video-renditions}

## Introduzione {#introduction}

Questa sezione descrive come creare rappresentazioni video utilizzate nei lettori Screens.

>[!IMPORTANT]
>I passaggi evidenziati in questa sezione devono essere configurati, se intendi utilizzare i video nei canali Screens.

## Passaggi per creare rappresentazioni video in Screens as a Cloud Service {#steps-creating-screens-video-renditions}

Per creare rappresentazioni video in Screens as a Cloud Service da Screens Content Provider, effettua le seguenti operazioni:

1. Passa al canale nel provider di contenuti Screens.

   >[!NOTE]
   >Fai riferimento a [Utilizzo del provider di contenuti Screens](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=en#screens-content-provider) per ulteriori dettagli.

1. Fai clic sulla sezione Strumenti dalla barra di navigazione a sinistra e fai clic su **Risorse** e quindi fai clic su **Profili di elaborazione**.

   ![](/help/screens-cloud/assets/configure/screens-cp-3.png)

1. Fai clic su **Crea** per creare un nuovo profilo di elaborazione.

   ![](/help/screens-cloud/assets/configure/screens-video-2.png)

1. Inserisci il **Nome**, quali **ScreensProcessingProfile**.

   ![](/help/screens-cloud/assets/configure/screens-video-3.png)

1. Passa a **Video** per aggiungere una codifica video e fai clic su **Aggiungi nuovo**.

   ![](/help/screens-cloud/assets/configure/screens-video-4a.png)

1. Inserisci il **Nome codifica** , ad esempio **screens-fullhd** e **Bitrate** come **2500**.

   ![](/help/screens-cloud/assets/configure/screens-video-4.png)

   >[!IMPORTANT]
   >Assicurati di utilizzare il nome di codifica che inizia con &quot;screens-&quot;, solo queste rappresentazioni video saranno considerate per riprodurre l’esperienza video in Screens as a Cloud Service. Inserisci il bitrate che funziona i tuoi video (2500 kbps per video 720px e 5000 kbps per 1080px).

   >[!NOTE]
   >Per lavorare i video, è possibile aggiungere più rappresentazioni video con larghezza/altezza/bitrate variabili. Ricorda che tutte le schermate- rappresentazioni saranno scaricate dai dispositivi Screens, anche se il dispositivo riproduce solo rendering video.

1. Fai clic su **Salva**.

1. Seleziona il profilo di elaborazione e fai clic su **Applica profilo a cartelle**.

   ![](/help/screens-cloud/assets/configure/screens-video-5.png)

1. Seleziona le cartelle in cui vengono conservati i video Screens e fai clic su **Applica**.

   ![](/help/screens-cloud/assets/configure/screens-video-6.png)

   >[!NOTE]
   >* Puoi creare più profili di elaborazione e applicarli alle cartelle corrispondenti, in modo che i video presenti in tali cartelle ricevano le rappresentazioni video specifiche.
   >* Quando carichi dei video nella cartella in cui viene applicato il profilo di elaborazione, i video vengono elaborati e configurati e vengono create rappresentazioni, che vengono ulteriormente utilizzate dai dispositivi Screens per riprodurre i video.

