---
title: Aggiungere un sito Edge Delivery a Cloud Manager
description: Scopri come aggiungere un sito Edge Delivery al programma di produzione o al programma sandbox e i vantaggi che offre.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 68f05c49ebc3d46aa44b3998e6142ab8547e5455
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 2%

---


# Aggiungere un sito Edge Delivery a Cloud Manager {#eds-add-site}

Scopri come aggiungere un sito Edge Delivery al programma di produzione o al programma sandbox e i vantaggi che offre.

## Introduzione {#introduction}

Come parte del progetto di Edge Delivery Services con AEM as a Cloud Service, ti invitiamo ad aggiungere il tuo sito Edge Delivery a Cloud Manager. L’aggiunta del sito web Edge Delivery a Cloud Manager offre i seguenti vantaggi.

* [Accesso alla rete CDN gestita da Adobe](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md)
* [Accesso ai rapporti di SLA](/help/implementing/cloud-manager/sla-reporting.md)
* [Accesso ai report sull&#39;utilizzo delle licenze](/help/implementing/cloud-manager/license-dashboard.md)

Tieni presente che l&#39;aggiunta del tuo sito Edge Delivery a Cloud Manager è necessaria per [registrare un ticket di supporto per il progetto Edge Delivery.](/help/edge/overview.md##support-ticket)

## Aggiunta di un sito e di Edge Delivery a Cloud Manager {#adding}

1. Accedere a Cloud Manager all&#39;indirizzo [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) e selezionare il programma appropriato.
1. Effettua una delle operazioni seguenti:
   * Dalla pagina **Panoramica del programma**, fai clic sulla scheda **Edge Delivery**. Quindi, nell&#39;angolo inferiore destro della pagina, fare clic su **Aggiungi sito Edge Delivery**.

     ![Aggiungi sito Edge Delivery dalla scheda Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

   * Nell’angolo in alto a sinistra della pagina, fai clic sull’icona dell’hamburger per visualizzare il menu di navigazione a sinistra. Nell&#39;intestazione **Services** fare clic su **Siti Edge Delivery**. Fai clic su **Aggiungi sito** nell&#39;angolo superiore destro della pagina.

     ![Aggiungi sito Edge Delivery dal pulsante Siti Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

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

Dopo aver aggiunto i Edge Delivery Services a un programma di produzione, viene applicata la licenza del Edge Delivery Services.

Ogni sito Edge Delivery ha un **elenco attività di Edge Delivery** per guidarti nella creazione del tuo sito Edge Delivery.

![app Edge Delivery](/help/implementing/cloud-manager/assets/edge-delivery-to-do-ist.png)

Per informazioni dettagliate su questi passaggi, vedere il documento [Introduzione ai Edge Delivery Services in Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md#ed-todo-list).
