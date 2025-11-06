---
title: Gestire le pipeline
description: Scopri come gestire, modificare, eseguire ed eliminare le pipeline esistenti.
index: true
exl-id: 4aff5a84-134a-43fa-8de8-8d564f4edd16
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1493'
ht-degree: 28%

---


# Gestire le pipeline {#managing-pipelines}

Scopri come gestire, modificare, eseguire ed eliminare le pipeline esistenti.

## Scheda Pipeline {#pipeline-card}

La scheda **Pipeline** della pagina **Panoramica del programma** in Cloud Manager offre una panoramica di tutte le pipeline e del relativo stato corrente.

![Scheda Pipeline in Cloud Manager](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

Facendo clic sull&#39;icona ![Puntini di sospensione - Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) accanto a ciascuna pipeline, è possibile eseguire le azioni seguenti:

* [Eseguire una pipeline](#running-pipelines)
* [Annullare una pipeline](#cancel)
* [Modificare una pipeline](#editing-pipelines)
* [Eliminare una pipeline](#deleting-pipelines)
* [Visualizzare i dettagli dell’ultima esecuzione di una pipeline](#view-details)

Nella parte inferiore dell’elenco delle pipeline sono disponibili le seguenti opzioni generali:

* **Aggiungi** - A [aggiungi una nuova pipeline di produzione](configuring-production-pipelines.md) o [aggiungi una nuova pipeline non di produzione](configuring-non-production-pipelines.md)
* **Mostra tutto**: reindirizza l’utente alla schermata Pipeline per visualizzare tutte le pipeline in una tabella più dettagliata.
* **Accedi a dati archivio**: consente di visualizzare le informazioni necessarie per accedere all’archivio Git di Cloud Manager.
* **Ulteriori informazioni**: consente di accedere alle risorse della documentazione sulla pipeline CI/CD.

## Pagina Pipeline {#pipelines}

La pagina **Pipeline** mostra un elenco completo di tutte le pipeline per il programma selezionato. Queste informazioni sono utili perché presentano informazioni più complete di quelle disponibili nella [scheda della pipeline](#pipeline-card).

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.

1. Dalla pagina **Panoramica programma**, fai clic sulla scheda ![Pipeline - Icona flusso di lavoro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **Pipeline**.

1. Nella pagina **Pipeline** è possibile visualizzare un elenco di tutte le pipeline per il programma e avviare e interrompere l&#39;esecuzione della pipeline come si farebbe nella **Scheda pipeline**.

Se una pipeline è in esecuzione, fare clic su ![Informazioni - icona supporto](https://spectrum.adobe.com/static/icons/ui_18/InfoMedium.svg) nella colonna **Stato** per visualizzare un popup con i dettagli sull&#39;esecuzione. Nel popup, fai clic su **Visualizza dettagli** per visualizzare i [dettagli dell&#39;esecuzione della pipeline](#view-details).

![Dettagli di esecuzione della pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-status.png)


Puoi anche fare clic sull&#39;icona ![Puntini di sospensione - Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) accanto alla pipeline per eseguire altre azioni appropriate allo stato della pipeline, ad esempio [modificarla](#editing-pipelines) o [annullare l&#39;esecuzione](#cancel).

![Azioni pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-actions.png)

### Contrassegnare i preferiti della pipeline{#pipeline-favorites}

Puoi contrassegnare specifiche pipeline come preferite in modo che vengano visualizzate nella parte superiore dell&#39;elenco nella pagina **Pipeline**. Questa funzionalità semplifica la ricerca e l’esecuzione delle pipeline a cui si accede di frequente.

**Per contrassegnare i preferiti della pipeline:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.
1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.
1. Dalla pagina **Panoramica programma**, fai clic sulla scheda ![Pipeline - Icona flusso di lavoro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **Pipeline**.
1. Nella pagina Pipeline, a sinistra del nome e del tipo di una pipeline, fai clic su ![Icona a forma di stella per la pipeline non preferita](https://spectrum.adobe.com/static/icons/workflow_18/Smock_StarOutline_18_N.svg) per aggiungerla all&#39;elenco dei preferiti.
In alternativa, fai clic sull&#39;icona ![Stella per una pipeline preferita](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Star_18_N.svg) per rimuovere la pipeline dall&#39;elenco dei preferiti.


## Pagina Attività {#activity}

Nella pagina **Attività** è visualizzato un elenco completo di tutte le esecuzioni delle pipeline per il programma selezionato e altri importanti eventi del programma.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Nella pagina **Panoramica programma**, nel menu laterale, fare clic su ![icona campana](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bell_18_N.svg) **Attività**.

1. Nella pagina **Attività** è disponibile un elenco di tutte le esecuzioni della pipeline del programma, incluse le esecuzioni correnti e cronologiche.

Se una pipeline è in esecuzione, è possibile fare clic sull&#39;icona ![Info - medium](https://spectrum.adobe.com/static/icons/ui_18/InfoMedium.svg) nella colonna **Status** per visualizzare un popup contenente informazioni sull&#39;esecuzione.

![Dettagli di esecuzione della pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-activity.png)

Fare clic sulla riga che rappresenta l&#39;esecuzione della pipeline per visualizzare i [dettagli dell&#39;esecuzione della pipeline](#view-details).

Puoi anche fare clic sull&#39;icona ![Puntini di sospensione - Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) per eseguire ulteriori azioni sull&#39;esecuzione della pipeline, ad esempio per visualizzarne i dettagli o scaricare il registro, che ti porta alla [pagina dei dettagli della pipeline](#view-details).

![Azioni di esecuzione della pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-execution-actions.png)

## Eseguire una pipeline {#running-pipelines}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Passa alla scheda **Pipeline** dalla pagina **Panoramica del programma**.

1. Fai clic sull&#39;icona ![Puntini di sospensione - Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) accanto alla pipeline eseguita.

1. Dal menu a discesa, fare clic sull&#39;icona ![Esegui - Riproduci](https://spectrum.adobe.com/static/icons/workflow_18/Smock_PlayCircle_18_N.svg) **Esegui**.

   L&#39;esecuzione della pipeline viene avviata e l&#39;avanzamento della colonna **Stato** viene visualizzato.

Per visualizzare i dettagli dell&#39;esecuzione, fai nuovamente clic su ![Puntini di sospensione - Icona Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) e quindi su **[Visualizza dettagli](#view-details)**.

A seconda del tipo di pipeline, è possibile annullare l&#39;esecuzione facendo nuovamente clic su ![Puntini di sospensione - Icona Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) e su **Annulla**.

## Eseguire più pipeline {#run-multiple-pipelines}

Con Cloud Manager è possibile eseguire più pipeline contemporaneamente, migliorando l’efficienza della distribuzione per i clienti AEM as a Cloud Service. La funzionalità **Esegui selezionati** consente di selezionare più pipeline e attivarle per l&#39;esecuzione simultanea. Semplifica l’esecuzione manuale delle pipeline singolarmente e ottimizza i flussi di lavoro di build e distribuzione.

**Per eseguire più pipeline:**

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.
1. Dal menu a sinistra, fare clic sull&#39;icona ![Flusso di lavoro &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **Pipeline**.
1. Nella tabella della pagina **Pipeline**, seleziona le caselle di controllo accanto alle pipeline da eseguire.
Se necessario, fai clic sull&#39;icona ![Filtro, su funnel](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Filter_18_N.svg) **Filtri** per ordinare le pipeline in base al nome, all&#39;ambiente, al tipo di codice distribuito o a una combinazione di tutte e tre.
1. Nell&#39;angolo superiore destro della pagina fare clic su **Esegui selezionato (x)**.
1. Nella finestra di dialogo **Esegui pipeline selezionate (x)**, fai clic su **Esegui (x)**.

   Il pulsante **Esegui** riflette il numero di pipeline che possono continuare. Ad esempio, potresti aver selezionato quattro pipeline, ma una è già in esecuzione. In alternativa, un ambiente collegato a una pipeline selezionata non esiste più. In tali casi, il sistema si adegua di conseguenza. Il pulsante si aggiorna a &quot;Esegui (3)&quot; per indicare che tre pipeline possono procedere.

1. Le pipeline iniziano a essere in esecuzione e il loro stato viene aggiornato nell&#39;elenco **Pipeline**.

## Modificare una pipeline {#editing-pipelines}

Se non è in esecuzione, puoi modificare una pipeline.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Passa alla scheda **Pipeline** dalla pagina **Panoramica del programma**.

1. Fai clic sull&#39;icona ![Puntini di sospensione - Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) accanto alla pipeline da modificare.

1. Dal menu a discesa, fare clic su **Modifica**.

1. Nella finestra di dialogo **Modifica pipeline di produzione** o **Modifica pipeline non di produzione**, modifica gli stessi dettagli immessi durante la creazione della pipeline.

   Per informazioni dettagliate sui campi e le opzioni di configurazione disponibili per le pipeline, consulta le pagine seguenti.
   * [Configurare una pipeline di produzione](configuring-production-pipelines.md)
   * [Configurare una pipeline non di produzione](configuring-non-production-pipelines.md)

1. Al termine, fare clic su **Aggiorna**.

>[!NOTE]
>
>Le pipeline a livello web e di configurazione non sono supportate con gli archivi privati. Per informazioni dettagliate e l&#39;elenco completo delle limitazioni, vedere [Aggiungere un archivio GitHub privato in Cloud Manager](/help/implementing/cloud-manager/managing-code/private-repositories.md).

## Eliminare una pipeline {#deleting-pipelines}

È possibile eliminare una pipeline se non è in esecuzione.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Passa alla scheda **Pipeline** dalla pagina **Panoramica del programma**.

1. Fai clic sull&#39;icona ![Puntini di sospensione - Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) accanto alla pipeline eseguita.

1. Dal menu a discesa, fare clic su **Elimina**.


## Visualizzare i dettagli dell’ultima esecuzione di una pipeline {#view-details}

Puoi controllare i dettagli di una pipeline per visualizzarne lo stato e i registri dall’esecuzione più recente. Tuttavia, puoi accedere ai dettagli solo se la pipeline è attualmente in esecuzione o è stata eseguita almeno una volta.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Passa alla scheda **Pipeline** dalla pagina **Panoramica del programma**.

1. Dal menu a discesa, fai clic sull&#39;icona ![Puntini di sospensione - Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) accanto alla pipeline eseguita.

1. Dal menu a discesa, fare clic su **Visualizza ultima esecuzione**.

   L’opzione reindirizza alla pagina dei dettagli della pipeline in esecuzione.

   ![Dettagli della pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-running-details.png)

   Da qui è possibile visualizzare lo stato dei vari passaggi della pipeline e recuperare i registri della build per finalità diagnostiche. Per ulteriori informazioni sulla distribuzione del codice e sull&#39;esecuzione dei test, vedere [Distribuire il codice](/help/implementing/cloud-manager/deploy-code.md).

   Tutti i passaggi dell’esecuzione di una pipeline vengono visualizzati con quelli non ancora avviati non selezionabili. I passaggi completati mostrano la loro durata.

   Al termine di un passaggio della pipeline viene visualizzato un riepilogo.

   ![Riepilogo del passaggio](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-step.png)

1. Fai clic su **Visualizza dettagli** per espandere la sezione **Durata**, in cui puoi visualizzare la durata media della pipeline in base alle tendenze storiche del programma.

   ![Durata](/help/implementing/cloud-manager/assets/configure-pipeline/duration.png)

1. Se la pipeline include un passaggio **Analisi del codice** che segnala i problemi, fai clic su **Scarica dettagli** per accedere a un elenco di [test di qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md) non superati.

   ![Problemi di qualità del codice](assets/managing-pipelines-code-quality-issues.png)

   Il file CSV include una colonna **Posizione file di progetto** che mostra il percorso del codice problematico relativo al progetto. La colonna **Posizione file** riflette invece il percorso generato da Maven.

   ![Dettagli di problemi rilevati dalla scansione del codice del progetto](assets/managing-pipelines-code-quality-details.png)

## Annullare una pipeline {#cancel}

Puoi annullare in modo sicuro l’esecuzione della pipeline se si trova nella fase di convalida o di creazione dell’immagine.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina della panoramica del programma, fai clic sull&#39;icona ![Puntini di sospensione - Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) della pipeline che desideri annullare sulla scheda **Pipeline**.

   ![Annullamento di una pipeline](/help/implementing/cloud-manager/assets/cancel-pipeline.png)

1. Fare clic su **Annulla**.

In alternativa, puoi annullare una pipeline dalla pagina dei dettagli della pipeline.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Passa alla scheda ![Pipeline - Icona flusso di lavoro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **Pipeline** dalla pagina **Panoramica del programma** e seleziona la pipeline da annullare.

   L’opzione reindirizza alla pagina dei dettagli della pipeline in esecuzione.

   ![Annulla dettagli pipeline](/help/implementing/cloud-manager/assets/cancel-pipeline-details.png)

1. Fare clic su **Annulla**.

