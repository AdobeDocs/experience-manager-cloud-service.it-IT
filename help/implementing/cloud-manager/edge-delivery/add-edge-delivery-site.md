---
title: Aggiungere un sito Edge Delivery a Cloud Manager
description: Scopri come aggiungere un sito Edge Delivery al programma di produzione o al programma sandbox.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: c952e69aa637b30abec4deba0e643b4287d84330
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 2%

---


# Aggiungere un sito Edge Delivery a Cloud Manager {#adding}

Puoi aggiungere un sito Edge Delivery al programma di produzione o al programma sandbox.

Per [registrare un ticket di supporto per il progetto Edge Delivery](/help/edge/overview.md##support-ticket) è necessario aggiungere un sito Edge Delivery a Cloud Manager.

Vedere anche [Introduzione ai Edge Delivery Services in Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md).

**Per aggiungere un sito Edge Delivery a Cloud Manager:**

1. Accedere a Cloud Manager all&#39;indirizzo [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) e selezionare il programma appropriato.
1. Effettua una delle operazioni seguenti:

   * Dalla pagina **Panoramica del programma**, fai clic sulla scheda **Edge Delivery**. Quindi, nell&#39;angolo inferiore destro della pagina, fare clic su **Aggiungi sito Edge Delivery**.

     ![Aggiungi sito Edge Delivery dalla scheda Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

   * Nell’angolo in alto a sinistra della pagina, fai clic sull’icona dell’hamburger per visualizzare il menu di navigazione a sinistra. Nell&#39;intestazione **Services** fare clic su **Siti Edge Delivery**. Fai clic su **Aggiungi sito** nell&#39;angolo superiore destro della pagina.

     ![Aggiungi sito Edge Delivery dal pulsante Edge Delivery Sites](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

1. Nella finestra di dialogo **Aggiungi sito Edge Delivery**, fornisci le seguenti informazioni nei campi obbligatori:

   | Campo di testo | Dati da fornire |
   | --- | --- |
   | Nome sito | Immetti il nome del sito Edge Delivery che stai aggiungendo. Il nome funge da identificatore univoco del sito all’interno di Cloud Manager. |
   | URL archivio | Questo campo si riferisce all’archivio Git in cui è memorizzato il codice del sito web. Questo campo consente a Cloud Manager di estrarre il codice da tale archivio durante il processo di distribuzione. |
   | Descrizione sito (facoltativa) | Immetti una breve descrizione del sito Edge Delivery che stai aggiungendo. Questa descrizione consente di identificare e differenziare il sito, semplificandone la gestione e il riconoscimento tra gli altri siti aggiunti. |

1. Nell&#39;angolo inferiore destro della finestra di dialogo fare clic su **Aggiungi**.

1. Viene visualizzata la finestra di dialogo **Verifica proprietà repository**. Una volta aperto, effettuare le seguenti operazioni:

   1. Aggiungere un file con percorso e nome `well-known/adobe/cloudmanager-challenge.txt` al ramo `main` dell&#39;archivio Git elencato nel campo **URL archivio**.
      * Se necessario, fai clic sull&#39;icona **Copia** per copiare il percorso negli Appunti.
      * *non* aggiungere un punto all&#39;inizio del percorso.
   1. Aggiungere il codice del campo **Step &amp;num; 1** al file creato nel passaggio precedente.
      * Se necessario, fai clic sull&#39;icona **Copia** per copiare il codice negli Appunti.
   1. Nell&#39;archivio Git creare una richiesta di pull per le modifiche appena create, quindi unirla a `main`.

1. Fare clic su **Verifica**.

Dopo la verifica dell’archivio, il suo stato nella tabella Edge Deliver Sites cambia in un cerchio verde con un segno di spunta bianco all’interno.
