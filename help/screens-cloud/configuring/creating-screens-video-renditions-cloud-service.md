---
title: Creazione di rappresentazioni video Screens in Screens come Cloud Service
description: Questa pagina descrive come creare rappresentazioni video Screens in Screens come Cloud Service.
source-git-commit: ec939ac6a91523a9ba64a555943eba8e6da071eb
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# Creazione di rappresentazioni video Screens in Screens come Cloud Service {#creating-screens-video-renditions}

## Introduzione {#introduction}

Questa guida descrive come creare rappresentazioni video utilizzate nei lettori Screens.

>[!IMPORTANT]
>I passaggi evidenziati in questa sezione devono essere configurati se intendi utilizzare i video nei canali Screens.

## Passaggi per creare rappresentazioni video Screens in Screens come Cloud Service {#steps-creating-screens-video-renditions}

1. Passa al canale nel provider di contenuti Screens.

   >[!NOTE]
   >Per ulteriori informazioni, consulta [Utilizzo di Screens Content Provider](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=en#screens-content-provider) .

1. Fai clic sulla sezione Strumenti nella barra di navigazione a sinistra e fai clic su **Risorse**, quindi fai clic su **Profili di elaborazione**.

   ![](/help/screens-cloud/assets/configure/screens-cp-3.png)

1. Fai clic su **Crea** per creare un nuovo profilo di elaborazione.

   ![](/help/screens-cloud/assets/configure/screens-video-2.png)

1. Inserisci il **Nome**, ad esempio **ScreensProcessingProfile**.

   ![](/help/screens-cloud/assets/configure/screens-video-3.png)

1. Passa alla scheda **Video** per aggiungere una codifica video e fai clic su **Aggiungi nuovo**.


   >[!IMPORTANT]
   >Assicurati di utilizzare il nome di codifica che inizia con &quot;screens-&quot;, solo queste rappresentazioni video saranno considerate per riprodurre l’esperienza video in Screens As a Cloud Service. Immettere il bit rate adatto ai video (2500 kbps per video 720 px e 5000 kbps per video 1080 px)

   >[!NOTE]
   >È possibile aggiungere più rappresentazioni video con larghezza/altezza/bitrate variabili in base alle esigenze, ma ricorda che tutte le schermate- rappresentazioni saranno scaricate dai dispositivi Screens, anche se il dispositivo riproduce solo rappresentazioni video.

1. Fai clic su Salva

1. Seleziona il profilo di elaborazione e fai clic su &quot;Applica profilo a cartelle&quot;

1. Seleziona le cartelle in cui vengono conservati i video Screens e fai clic su Applica

1. Puoi creare più profili di elaborazione e applicarli alle cartelle corrispondenti, in modo che i video presenti in tali cartelle ottengano le rappresentazioni video specifiche

1. Quando carichi dei video nella cartella in cui viene applicato il profilo di elaborazione, i video verranno elaborati e configurati e verranno creati rendering, che verranno utilizzati dai dispositivi Screens per riprodurre i video.

