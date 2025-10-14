---
title: Supporto delle miniature per video in Screens as a Cloud Service
description: Questa pagina descrive come aggiungere il supporto miniature per video in Screens as a Cloud Service.
index: true
exl-id: 7b15d7cc-f089-4008-9039-5f48343a0f20
feature: Developing Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 1%

---

# Supporto delle miniature per video {#thumbnail-support-videos}

## Introduzione {#introduction}

Un autore di contenuti può definire una miniatura per video in modo che l’immagine venga utilizzata come segnaposto e possa testare correttamente la riproduzione e il targeting del contenuto, mentre il video effettivo viene finalizzato dal team appropriato. L’immagine può essere utilizzata anche nel caso in cui la riproduzione del video non riesca.

L’aggiunta di supporto per un’immagine miniatura sul componente video consente al cliente di aggiungere correttamente un componente valido nel canale, con il contenuto effettivo ed eseguire eventuali configurazioni di targeting prima che il video venga consegnato.

>[!NOTE]
>L’immagine miniatura, se impostata sul componente video, viene riprodotta in caso di errore di riproduzione video sul lettore. Questo flusso di lavoro ti consente di inviare il messaggio desiderato al pubblico (riproducendo il contenuto) invece di saltarlo completamente.

Il Supporto miniature consente di effettuare le seguenti operazioni:

* Prepara un’esperienza di canale quando i video non sono ancora pronti o quando non desideri necessariamente testare il download di una risorsa di grandi dimensioni sui lettori

* Imposta un meccanismo di fallback, nel caso in cui si verifichino problemi di riproduzione sul dispositivo.

## Utilizzo delle miniature nei video {#using-thumbnails}

>[!IMPORTANT]
>**Prerequisiti**
>Prima di scoprire come utilizzare le miniature per i video, assicurati di imparare a creare rappresentazioni video per i canali in Screens as a Cloud Service Project. Consulta [Creazione di rappresentazioni video in Screens as a Cloud Service](/help/screens-cloud/configuring/creating-screens-video-renditions-cloud-service.md).

Per usare la miniatura nei video, segui la procedura indicata di seguito:

1. Passa a un canale Screens esistente o creane uno.

   >[!NOTE]
   >Per informazioni su come creare un canale e aggiungere contenuto a un canale, vedere [Creazione e gestione di un canale in Screens as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/create-content/creating-channels-screens-cloud.html?lang=it).

1. Seleziona il canale. Sulla barra delle azioni fare clic su **Modifica** per aprire l&#39;editor.


   ![Pulsante Modifica sulla barra delle azioni](/help/screens-cloud/using-core-product-features/assets/thumbnail-1.png).

1. Aggiungi o modifica un componente video esistente, come illustrato nella figura riportata di seguito.

   ![Immagine evidenziata di una risorsa video](/help/screens-cloud/using-core-product-features/assets/thumbnail-2.png).

1. Aggiungi o modifica un componente video esistente, come illustrato nella figura riportata di seguito.

1. Seleziona il video e fai clic sull&#39;icona Configura (*chiave inglese*) per aprire le proprietà del video.

   ![Immagine della risorsa video selezionata con freccia rivolta verso l&#39;icona Configura, rappresentata come una chiave inglese. sulla barra degli strumenti &#x200B;](/help/screens-cloud/using-core-product-features/assets/thumbnail-3.png).

1. Viene visualizzata la finestra di dialogo **Video** in cui è possibile visualizzare la zona di rilascio **Miniatura**.

   ![Finestra di dialogo Video con l&#39;immagine della risorsa video e la casella di riepilogo Miniatura](/help/screens-cloud/using-core-product-features/assets/thumbnail-4.png).

1. Trascina e rilascia un&#39;immagine dal selettore risorse alla zona di rilascio **Miniatura** e fai clic su **Fine**.

   ![Selezione immagini risorse visualizzata dietro la finestra di dialogo Video con la risorsa immagine visualizzata nella casella di riepilogo Miniature](/help/screens-cloud/using-core-product-features/assets/thumbnail-5.png).

1. Fare clic su **Anteprima**.

1. Se un video è impostato sul componente, viene riprodotto. In caso contrario, e la miniatura è impostata, la miniatura viene riprodotta. In caso contrario, il componente viene considerato non configurato e viene saltato.

## Casi d’uso supportati durante l’utilizzo della miniatura nei video {#understand-use-case}

La miniatura nei video supporta i seguenti casi d’uso:

* Viene saltato un componente video senza alcuna configurazione.

* Un componente video con solo la miniatura impostata riproduce la miniatura.

* Un componente video con il video (se il video ha una rappresentazione corretta) e il set di miniature riproduce il video.

* Un componente video con il set di video riproduce la miniatura, se si verifica un errore di riproduzione, o passa all’elemento successivo nel caso in cui la miniatura non sia configurata.
