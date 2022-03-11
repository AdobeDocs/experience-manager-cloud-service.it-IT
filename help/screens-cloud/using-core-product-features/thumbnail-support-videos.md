---
title: Supporto delle miniature per i video in Screens as a Cloud Service
description: Questa pagina descrive come aggiungere il supporto per le miniature per i video in Screens as a Cloud Service.
index: true
exl-id: 7b15d7cc-f089-4008-9039-5f48343a0f20
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 1%

---

# Supporto delle miniature per video {#thumbnail-support-videos}

## Introduzione {#introduction}

Un autore di contenuti può definire una miniatura per i video in modo che l’immagine possa essere utilizzata come segnaposto e possa testare correttamente la riproduzione e il targeting del contenuto, mentre il video effettivo viene finalizzato dal team appropriato. L&#39;immagine può anche essere utilizzata, nel caso in cui la riproduzione del video non riesca.

L’aggiunta del supporto per un’immagine in miniatura sul componente video consente al cliente di aggiungere correttamente un componente valido nel canale, con contenuto effettivo, ed eseguire eventuali configurazioni di targeting prima che il video venga effettivamente distribuito.

>[!NOTE]
>L’immagine miniatura, se impostata sul componente video, viene riprodotta in caso di errore di riproduzione video sul lettore. Questo consente di inviare il messaggio desiderato al pubblico (riproducendo il contenuto) anziché ignorarlo completamente.

Il supporto per le miniature consente di:

* Prepara un’esperienza di canale quando i video non sono ancora pronti o quando non desideri necessariamente testare un download di risorse di grandi dimensioni sui lettori.

* Imposta un meccanismo di fallback, in caso di problemi di riproduzione sul dispositivo.

## Utilizzo delle miniature nei video {#using-thumbnails}

>[!IMPORTANT]
>**Prerequisiti**
>Prima di imparare a utilizzare le miniature per i video, assicurati di imparare a creare rappresentazioni video per i canali nel progetto as a Cloud Service di Screens. Vedi [qui](/help/screens-cloud/configuring/creating-screens-video-renditions-cloud-service.md) per ulteriori dettagli.

Per usare le miniature nei video, effettua le seguenti operazioni:

1. Passa a un canale Screens esistente o creane uno nuovo.

   >[!NOTE]
   >Per scoprire come creare un canale e aggiungere contenuti a un canale, vedi [Creazione e gestione di un canale in Screens as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/creating-channels-screens-cloud.html?lang=en).

1. Seleziona il canale e fai clic su **Modifica** dalla barra delle azioni per aprire l’editor.

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-1.png)

1. Aggiungi o modifica un componente video esistente, come illustrato nella figura riportata di seguito.

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-2.png)

1. Seleziona il video e fai clic sul *chiave* per aprire le proprietà video.

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-3.png)

1. La **Video** viene visualizzata la finestra di dialogo in cui viene visualizzata la **Miniatura** zona di rilascio.

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-4.png)

1. Trascina e rilascia un’immagine dal selettore delle risorse al **Miniatura** zona di rilascio e fai clic su **Fine**.

   ![](/help/screens-cloud/using-core-product-features/assets/thumbnail-5.png)

1. Fai clic su **Anteprima**.

1. Se un video è impostato sul componente, il video verrà riprodotto. In caso contrario, e la miniatura è impostata, la miniatura viene riprodotta. In caso contrario, il componente viene considerato non configurato e verrà ignorato.

## Casi d&#39;uso supportati quando si utilizza la miniatura nei video {#understand-use-case}

La miniatura nei video supporta i seguenti casi d’uso:

* Un componente video non configurato verrà ignorato.

* Un componente video con solo le miniature impostate riproduce la miniatura.

* Un componente video con sia il video (se il video ha una rappresentazione corretta) che il set di miniature riprodurranno il video.

* Un componente video con il set di video riproduce la miniatura, in caso di errore di riproduzione, oppure passa all’elemento successivo nel caso in cui la miniatura non sia configurata.
