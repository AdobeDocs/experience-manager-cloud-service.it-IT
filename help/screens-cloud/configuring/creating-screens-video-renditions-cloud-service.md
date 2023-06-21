---
title: Creazione di rappresentazioni video in Screens as a Cloud Service
description: Questa pagina descrive come creare rappresentazioni video in Screens as a Cloud Service.
exl-id: a9c46036-cd29-47fa-81d9-c865cf22c98a
source-git-commit: cf1e2717342ca4e00780428d6ccf264bd8eca371
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---

# Creazione di rappresentazioni video in Screens as a Cloud Service {#creating-screens-video-renditions}

## Introduzione {#introduction}

Questa sezione descrive come creare rappresentazioni video utilizzate nei lettori Screens.

>[!IMPORTANT]
>Se intendi utilizzare i video nei canali Screens, è necessario configurare i passaggi evidenziati in questa sezione.

## Passaggi per creare rappresentazioni video in Screens as a Cloud Service {#steps-creating-screens-video-renditions}

Per creare rappresentazioni video in Screens as a Cloud Service dal provider di contenuti Screens, segui i passaggi seguenti:

1. Passa al tuo canale nel provider di contenuti Screens.

   >[!NOTE]
   >Fai riferimento a [Utilizzo del provider di contenuti Screens](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=en#screens-content-provider) per ulteriori dettagli.

1. Fai clic sulla sezione Strumenti nella barra di navigazione a sinistra, quindi fai clic su **Risorse** e quindi fare clic su **Profili elaborazione**.

   ![Fai clic sui profili di elaborazione](/help/screens-cloud/assets/configure/screens-cp-3.png)

1. Fai clic su **Crea** per creare un nuovo profilo di elaborazione.

   ![Fai clic su Crea](/help/screens-cloud/assets/configure/screens-video-2.png)

1. Inserisci il **Nome**, ad esempio **ScreensProcessingProfile**.

   ![](/help/screens-cloud/assets/configure/screens-video-3.png)

1. Accedi a **Video** per aggiungere una codifica video e fare clic su **Aggiungi nuovo**.

   ![](/help/screens-cloud/assets/configure/screens-video-4a.png)

1. Inserisci il **Nome codifica** ad esempio, **schermo intero** e **Bitrate** as **2500**.

   ![](/help/screens-cloud/assets/configure/screens-video-4.png)

   >[!IMPORTANT]
   >Assicurati di utilizzare il nome della codifica che inizia con &quot;screens-&quot;, solo queste rappresentazioni video sono considerate per riprodurre l’esperienza video in Screens as a Cloud Service. Immetti il bitrate che funziona con i video (2500 kbps per i video a 720 px e 5000 kbps per i video a 1080 px).

   >[!NOTE]
   >Per lavorare con i video è possibile aggiungere più rappresentazioni video con larghezza/altezza/bitrate variabile. Tutti gli schermi e i rendering vengono scaricati dai dispositivi Screens, anche se il dispositivo riproduce solo il rendering video.

1. Fai clic su **Salva**.

1. Seleziona il profilo di elaborazione e fai clic su **Applica profilo a cartelle**.

   ![Applica profilo a cartella](/help/screens-cloud/assets/configure/screens-video-5.png)

1. Seleziona le cartelle in cui vengono conservati i video Screens e fai clic su **Applica**.

   ![Fai clic su Applica.](/help/screens-cloud/assets/configure/screens-video-6.png)

   >[!NOTE]
   >* Puoi creare più profili di elaborazione e applicarli alle cartelle corrispondenti, in modo che i video in tali cartelle ottengano le rappresentazioni video specifiche.
   >* Quando carichi dei video nella cartella in cui viene applicato il profilo di elaborazione, vengono elaborati i video e creati i rendering configurati, ulteriormente utilizzati dai dispositivi Screens per riprodurre i video.
