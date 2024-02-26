---
title: Processi asincroni
description: Adobe Experience Manager ottimizza le prestazioni completando in modo asincrono alcune attività a uso intensivo di risorse come operazioni in background.
exl-id: 9c5c4604-1290-4dea-a14d-08f3ab3ef829
source-git-commit: 1a4c5e618adaef99d82a00e1118d1a0f8536fc14
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 64%

---

# Operazioni asincrone {#asynchronous-operations}

Per ridurre l’impatto negativo sulle prestazioni, Adobe Experience Manager elabora in modo asincrono alcune operazioni che richiedono tempo e risorse, come operazioni in background. L’elaborazione asincrona comporta l’accodamento di più processi e la loro esecuzione in modo seriale, in base alla disponibilità delle risorse di sistema.

Alcune di queste operazioni sono:

* Eliminazione di numerose risorse
* Spostamento di più di una risorsa o risorse con più riferimenti
* Esportazione/importazione in blocco dei metadati di una risorsa
* Recupero di risorse che superano il limite di soglia impostato da una implementazione remota di Experience Manager
* Rollout di Live Copy

È possibile visualizzare lo stato dei processi asincroni da **[!UICONTROL Operazioni in background]** dashboard in **Navigazione globale** > **Strumenti** > **Generale** > **Processi**.

>[!NOTE]
>
>Per impostazione predefinita, i processi asincroni vengono eseguiti in parallelo. Se *`n`* è il numero di core della CPU, per impostazione predefinita è possibile eseguire in parallelo *`n/2`* processi. Per personalizzare le impostazioni della coda dei processi, modifica la **[!UICONTROL configurazione della coda predefinita dell’operazione asincrona]** e la **configurazione per spostamento e rollout pagina dell’operazione asincrona** dalla console Web.
>
>Per ulteriori informazioni, consulta [Configurazione della coda](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#queue-configurations).

## Monitorare lo stato delle operazioni asincrone {#monitor-the-status-of-asynchronous-operations}

Ogni volta che AEM elabora un’operazione in modo asincrono, ricevi una notifica nella tua [casella in entrata](/help/sites-cloud/authoring/inbox.md) e tramite e-mail (se abilitata).

Per visualizzare in dettaglio lo stato delle operazioni asincrone, passare alla **[!UICONTROL Operazioni in background]** pagina.

1. Nell’interfaccia Experience Manager seleziona **Navigazione globale** > **Strumenti** > **Generale** > **Processi**.

1. In **[!UICONTROL Operazioni in background]** , rivedere i dettagli delle operazioni.

   ![Stato e dettagli delle operazioni asincrone](assets/async-operation-status.png)

   Per determinare l’avanzamento di una particolare operazione, controlla il valore nella colonna **[!UICONTROL Stato]**. A seconda dell’avanzamento, viene visualizzato uno dei seguenti stati:

   * **[!UICONTROL Attivo]**: elaborazione dell’operazione in corso

   * **[!UICONTROL Completato]**: operazione completata

   * **[!UICONTROL Non riuscito]** o **[!UICONTROL Errore]**: impossibile elaborare l’operazione

   * **[!UICONTROL Pianificato]**: l’elaborazione dell’operazione è pianificata per un momento successivo

1. Per interrompere un’operazione attiva, selezionala nell’elenco e scegli **[!UICONTROL Interrompi]** nella barra degli strumenti.

   ![stop_icon](assets/async-stop-icon.png)

1. Per visualizzare ulteriori dettagli, ad esempio descrizione e registri, seleziona l’operazione e fai clic su **[!UICONTROL Apri]** dalla barra degli strumenti.

   ![open_icon](assets/async-open-icon.png)

   Viene visualizzata la pagina dei dettagli del processo.

   ![job_details](assets/async-job-details.png)

1. Per eliminare un’operazione dall’elenco, seleziona **[!UICONTROL Elimina]** dalla barra degli strumenti. Per scaricare i dettagli in un file CSV, fai clic su **[!UICONTROL Scarica]**.

   >[!NOTE]
   >
   >Non è possibile eliminare un processo se il suo stato è **Attivo** o **In coda**.

## Configurazione delle opzioni di elaborazione del processo asincrono {#configure}

È possibile configurare diverse opzioni per i processi asincroni. Gli esempi seguenti mostrano come eseguire questa operazione utilizzando la gestione della configurazione su un sistema di sviluppo locale.

>[!NOTE]
>
>[Configurazioni OSGi](/help/implementing/deploying/configuring-osgi.md#creating-osgi-configurations) sono considerati contenuti mutabili e tali configurazioni devono essere distribuite come pacchetto di contenuti per un ambiente di produzione.

### Rimuovi processi completati {#purging-completed-jobs}

AEM esegue un processo di eliminazione ogni giorno alle 01:00 per eliminare i processi asincroni completati da più di un giorno.

Puoi modificare la pianificazione per il processo di eliminazione e il periodo per il quale i dettagli dei processi completati vengono conservati prima di essere eliminati. Puoi anche configurare il numero massimo di processi completati per i quali i dettagli devono essere conservati.

1. Accedi alla console web AEM di Quickstart Jar per l’SDK dell’AEM all’indirizzo `https://<host>:<port>/system/console` come utente amministratore.
1. Accedi a **OSGi** > **Configurazione**
1. Apri il lavoro **[!UICONTROL Adobe Granite Async Jobs Purge Scheduled Job]** (Processo pianificato di rimozione dei processi asincroni di Adobe Granite).
1. Specifica:
   * Il numero limite di giorni oltre i quali i processi completati vengono eliminati.
   * Il numero massimo di processi per i quali i dettagli vengono conservati nella cronologia.
   * L’espressione cron per indicare quando deve essere eseguita la rimozione.

   ![Configurazione della rimozione pianificata dei processi asincroni](assets/async-purge-job.png)

1. Salva le modifiche.

### Configurare le operazioni di eliminazione delle risorse asincrone {#configuring-synchronous-delete-operations}

Quando il numero di risorse o cartelle da eliminare supera la soglia, l’operazione di eliminazione viene eseguita in modo asincrono.

1. Accedi alla console web AEM di Quickstart Jar per l’SDK dell’AEM all’indirizzo `https://<host>:<port>/system/console` come utente amministratore.
1. Accedi a **OSGi** > **Configurazione**
1. Dalla console Web, apri la **[!UICONTROL configurazione della coda predefinita del processo asincrono]**.
1. Nella casella **[!UICONTROL Threshold number of assets]** (Soglia risorse), specifica il limite di risorse o cartelle per l’elaborazione asincrona delle operazioni di eliminazione.

   ![Soglia per l’eliminazione delle risorse](assets/async-delete-threshold.png)

1. Seleziona l’opzione **Enable email notification** (Abilita notifica e-mail) per ricevere notifiche e-mail sullo stato del processo. ad esempio, success, failed.
1. Salva le modifiche.

### Configurare le operazioni di spostamento delle risorse asincrone {#configuring-asynchronous-move-operations}

Quando il numero di risorse, cartelle o riferimenti da spostare supera la soglia, l’operazione di spostamento viene eseguita in modo asincrono.

1. Accedi alla console web AEM di Quickstart Jar per l’SDK dell’AEM all’indirizzo `https://<host>:<port>/system/console` come utente amministratore.
1. Accedi a **OSGi** > **Configurazione**
1. Dalla console Web, apri la **[!UICONTROL configurazione dell’elaborazione asincrona del processo di spostamento.]**
1. Nella casella **[!UICONTROL Threshold number of assets/references]** (Soglia risorse/riferimenti), specifica il numero limite di risorse, cartelle o riferimenti per l’elaborazione asincrona delle operazioni di spostamento.

   ![Soglia per lo spostamento delle risorse](assets/async-move-threshold.png)

1. Seleziona l’opzione **Enable email notification** (Abilita notifica e-mail) per ricevere notifiche e-mail sullo stato del processo. Ad esempio, success, failed.
1. Salva le modifiche.

### Configurare le operazioni MSM asincrone {#configuring-asynchronous-msm-operations}

1. Accedi alla console web AEM di Quickstart Jar per l’SDK dell’AEM all’indirizzo `https://<host>:<port>/system/console` come utente amministratore.
1. Accedi a **OSGi** > **Configurazione**
1. Dalla console Web, apri la **[!UICONTROL configurazione dell’elaborazione asincrona del processo di spostamento.]**
1. Seleziona l’opzione **Enable email notification** (Abilita notifica e-mail) per ricevere notifiche e-mail sullo stato del processo. Ad esempio, success, failed.

   ![Configurazione MSM](assets/async-msm.png)

1. Salva le modifiche.

>[!MORELIKETHIS]
>
>* [Gestione delle pagine](/help/sites-cloud/authoring/sites-console/managing-pages.md)
>* [Importare ed esportare in blocco i metadati delle risorse](/help/assets/metadata-import-export.md).
>* [Utilizzare le risorse collegate per condividere le risorse DAM da implementazioni remote](/help/assets/use-assets-across-connected-assets-instances.md).
