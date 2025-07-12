---
title: Ripristina il codice Source precedente distribuito
description: Scopri come ripristinare l’ultima build riuscita di un ambiente &ndash; non è richiesta alcuna esecuzione della pipeline.
feature: Operations
role: Admin
badge: label="Alfa" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket"
source-git-commit: ae90f527d398af40cf9e6963d2e27de3368f2e8f
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 3%

---

# Ripristina il codice sorgente precedente distribuito in AEM as a Cloud Service {#restore-previous-code-deployed}

>[!NOTE]
>
>&#x200B;>La funzione descritta in questo articolo è disponibile solo attraverso il primo programma alfa per utenti. Per iscriverti all&#39;Alfa, vedi [Rollback con un solo clic per le distribuzioni della pipeline](/help/implementing/cloud-manager/release-notes/current.md##one-click-rollback).

Utilizza **Ripristina il codice precedente distribuito** per ripristinare immediatamente l&#39;ultima compilazione riuscita di un ambiente, senza richiedere alcuna esecuzione della pipeline.

È sufficiente aprire il menu dell&#39;icona ![Altro o l&#39;icona del menu con i puntini di sospensione](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) dell&#39;ambiente selezionato e scegliere **Ripristina** > **Codice precedente distribuito** per eseguire il rollback dell&#39;ultimo codice sorgente distribuito in pochi secondi.

>[!TIP]
>
>È possibile visualizzare la versione del codice sorgente attivo utilizzata nella visualizzazione dei dettagli dell&#39;ambiente nella scheda **Generale**. Vedi [Visualizza i dettagli di un ambiente](/help/implementing/cloud-manager/manage-environments.md#viewing-environment).
>
>![Versione del codice Source in uso](/help/operations/assets/environments-view-details-sourcecodeversion.png)

La funzionalità **Ripristina codice precedente distribuito** diventa disponibile solo quando **ogni** condizione seguente è true:

* Si dispone dell&#39;autorizzazione **Creazione ripristino ambiente**. Per informazioni dettagliate sulla gestione delle autorizzazioni, vedere [Autorizzazioni personalizzate](/help/implementing/cloud-manager/custom-permissions.md).
* L’organizzazione è iscritta al programma Early Adopter e il flag di funzione è attivato.
* Il programma viene eseguito su **AEM as a Cloud Service**.
* L&#39;ambiente scelto è un ambiente **DEV** (limite temporaneo di Alpha).
* L&#39;ultima pipeline per l&#39;ambiente ha completato **correttamente** ed è stata eseguita **meno di 10 giorni** fa.
* Lo stato dell&#39;ambiente è **In esecuzione** e nessuna pipeline è in corso.
* La versione del codice sorgente di destinazione da ripristinare è stata distribuita **entro 30 giorni**.

Se un controllo non riesce, Cloud Manager apre la seguente finestra di dialogo in cui sono elencate una o più condizioni non soddisfatte e disabilita **Conferma**, impedendo il ripristino.

![Finestra di dialogo Ripristina errore precedente distribuito del codice](/help/operations/assets/restore-previous-code-deployment-not-allowed.png).

Se si desidera semplicemente ripristinare le condizioni originali dei dati persi, danneggiati o accidentalmente eliminati, è possibile utilizzare [Ripristina contenuto in AEM as a Cloud Service](/help/operations/restore.md). Questo processo di ripristino influisce solo sul contenuto, lasciando invariati il codice sorgente e la versione di AEM.

**Per ripristinare il codice precedente distribuito:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Fare clic sul programma per il quale si desidera avviare il ripristino.

1. Elencare tutti gli ambienti per il programma eseguendo una delle operazioni seguenti:

   * Dal menu a sinistra, in **Servizi**, fai clic sull&#39;icona ![Dati](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Ambienti**.

     ![Scheda Ambienti](assets/environments-1.png)

   * Dal menu a sinistra, nella sezione **Programma**, fai clic su **Panoramica**, quindi dalla scheda **Ambienti** fai clic sull&#39;icona ![Flusso di lavoro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **Mostra tutto**.

     ![Opzione Mostra tutto](assets/environments-2.png)

     >[!NOTE]
     >
     >Nella scheda **Ambienti** sono elencati solo tre ambienti. Fai clic su **Mostra tutto** nella scheda per visualizzare *tutti* gli ambienti del programma.

1. Nella tabella Ambienti, a destra di un ambiente di cui desideri ripristinare il codice sorgente, fai clic sull&#39;icona ![Altro o sull&#39;icona del menu con i puntini di sospensione](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg), quindi fai clic su **Ripristina** > **Codice precedente distribuito**.

   ![Ripristina il codice precedente distribuito dal menu con i puntini di sospensione](/help/operations/assets/restore-previous-code-deployed-menu.png)

1. Nella finestra di dialogo **Ripristina codice precedente distribuito**, controlla la versione attualmente distribuita e la versione da ripristinare, quindi fai clic su **Conferma**.

   ![Finestra di dialogo Ripristina codice precedente distribuito](/help/operations/assets/restore-previous-code-deployed-dialogbox.png)

1. Cloud Manager riporta l&#39;ambiente alla build precedente, mantiene intatti il contenuto e la configurazione e contrassegna l&#39;ambiente **Ripristino** nella pagina Ambienti fino al completamento della distribuzione.

   ![Ripristino dell&#39;attivazione](/help/operations/assets/restore-previous-code-deployed-restoring.png)
