---
title: Aggiungere un sito Edge Delivery a Cloud Manager
description: Scopri come aggiungere un sito Edge Delivery al programma di produzione o al programma sandbox.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 40a76e39750d6dbeb03c43c8b68cddaf515a2614
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 5%

---


# Aggiungere un sito Edge Delivery a Cloud Manager {#adding}

Dopo aver aggiunto un sito Edge Delivery al programma di produzione, viene applicata la licenza di Edge Delivery Services.

Per [registrare un ticket di supporto per il progetto Edge Delivery](/help/edge/overview.md##support-ticket) è necessario aggiungere un sito Edge Delivery a Cloud Manager.

Vedere anche [Introduzione ai Edge Delivery Services in Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md).

**Per aggiungere un sito Edge Delivery a Cloud Manager:**

1. Accedere a Cloud Manager all&#39;indirizzo [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) e selezionare il programma appropriato.
1. Effettua una delle operazioni seguenti:

   * Dalla pagina **Panoramica del programma**, fai clic sulla scheda **Edge Delivery**. Quindi, nell&#39;angolo inferiore destro della pagina, fare clic su **Aggiungi sito Edge Delivery**.

     ![Aggiungi sito Edge Delivery dalla scheda Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

   * Nell&#39;angolo superiore sinistro della pagina fare clic su ![Mostra icona menu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) per visualizzare il menu sul lato sinistro.
Nell&#39;intestazione **Services** fare clic sull&#39;icona ![Pagina Web](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Siti Edge Delivery**.
Fai clic su **Aggiungi sito** nell&#39;angolo superiore destro della pagina.

     ![Aggiungi sito Edge Delivery dal pulsante Edge Delivery Sites](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

1. Nella finestra di dialogo **Aggiungi sito Edge Delivery**, fornisci le seguenti informazioni nei campi obbligatori:

   | Campo di testo | Descrizione |
   | - | --- |
   | Nome sito | Immetti il nome del sito Edge Delivery che stai aggiungendo.<br>Il nome funge da identificatore univoco per il sito in Cloud Manager. |
   | URL archivio | Immetti l’archivio Git in cui è memorizzato il codice del sito web.<br>Questo campo consente a Cloud Manager di estrarre il codice da tale archivio durante il processo di distribuzione. |
   | Descrizione sito (facoltativa) | Immetti una breve descrizione del sito Edge Delivery che stai aggiungendo.<br>Una descrizione consente di identificare e differenziare il sito, semplificandone la gestione e il riconoscimento tra gli altri siti aggiunti. |

1. Nell&#39;angolo inferiore destro della finestra di dialogo fare clic su **Aggiungi**.

1. Nella finestra di dialogo **Verifica proprietà del repository**, verificare la proprietà del repository eseguendo la procedura seguente:

   | Numero passaggio | Descrizione |
   | - | - |
   | **1** | Aggiungere un file con percorso e nome `well-known/adobe/cloudmanager-challenge.txt` al ramo `main` dell&#39;archivio Git elencato nel campo **URL archivio**. *non* aggiungere un punto all&#39;inizio del percorso.<br>Se necessario, fare clic su ![Copia](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) per copiare il percorso negli Appunti. |
   | **2** | Aggiungi il codice visualizzato nel campo di testo del passaggio 2 al file appena creato nel passaggio 1.<br>Se necessario, fai clic su ![Copia](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) per copiare il codice negli Appunti. |
   | **3** | Crea una richiesta di pull nell&#39;archivio Git per le modifiche appena create, quindi uniscila in `main` per eseguire il commit del codice. |

1. Fare clic su **Verifica**.

Una volta verificato l’archivio, il suo stato nella tabella Edge Delivery Sites viene aggiornato. Un cerchio verde con un segno di spunta bianco all&#39;interno indica lo stato.

Nella stessa tabella fare clic su ![Informazioni sul sito Edge Delivery](https://spectrum.adobe.com/static/icons/workflow_18/Smock_InfoOutline_18_N.svg) per visualizzare i dettagli del sito. Queste informazioni includono l’URL dell’archivio verificato, insieme agli URL del sito web di anteprima e produzione.


