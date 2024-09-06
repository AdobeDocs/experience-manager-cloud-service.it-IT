---
title: Gestione delle pipeline
description: Scopri come gestire, modificare, eseguire ed eliminare le pipeline esistenti.
index: true
exl-id: 4aff5a84-134a-43fa-8de8-8d564f4edd16
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '1110'
ht-degree: 70%

---


# Gestione delle pipeline {#managing-pipelines}

Scopri come gestire, modificare, eseguire ed eliminare le pipeline esistenti.

## Scheda Pipeline {#pipeline-card}

La scheda **Pipeline** della pagina **Panoramica del programma** in Cloud Manager offre una panoramica di tutte le pipeline e del relativo stato corrente.

![Scheda Pipeline in Cloud Manager](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

Facendo clic sul pulsante con i puntini di sospensione accanto a ogni pipeline è possibile effettuare le seguenti operazioni.

* [Eseguire la pipeline](#running-pipelines)
* [Modificare la pipeline](#editing-pipelines)
* [Eliminare la pipeline](#deleting-pipelines)
* [Visualizzare dettagli](#view-details)

Nella parte inferiore dell’elenco delle pipeline sono disponibili le opzioni generali.

* **Aggiungi**: per [aggiungere una nuova pipeline di produzione](configuring-production-pipelines.md) o [una nuova pipeline non di produzione](configuring-non-production-pipelines.md).
* **Mostra tutto**: reindirizza l’utente alla schermata Pipeline per visualizzare tutte le pipeline in una tabella più dettagliata.
* **Accedi a dati archivio**: consente di visualizzare le informazioni necessarie per accedere all’archivio Git di Cloud Manager.
* **Ulteriori informazioni**: consente di accedere alle risorse della documentazione sulla pipeline CI/CD.

## Finestra Pipeline {#pipelines}

La finestra **Pipeline** mostra un elenco completo di tutte le pipeline per il programma selezionato. Questa funzione è utile in quanto presenta informazioni più complete rispetto a quelle disponibili nella [Scheda pipeline](#pipeline-card).

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione appropriata.

1. Nella console **[I miei programmi](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleziona il programma.

1. Dalla pagina **Panoramica del programma**, seleziona la scheda **Pipeline** per passare alla finestra **Pipeline**.

1. Qui puoi visualizzare un elenco di tutte le pipeline del programma, nonché avviare e interrompere l’esecuzione della pipeline come faresti nella **Scheda Pipeline**.

Se una pipeline è in esecuzione, facendo clic sull&#39;icona delle informazioni nella colonna **Stato** vengono visualizzati i dettagli relativi all&#39;esecuzione.

![Dettagli di esecuzione della pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-status.png)

Facendo clic su **Visualizza dettagli**, vieni reindirizzato ai [dettagli dell’esecuzione della pipeline](#view-details).

Puoi anche fare clic sul pulsante con i puntini di sospensione della pipeline per eseguire altre azioni appropriate allo stato della pipeline, ad esempio [modificarla](#editing-pipelines) o [annullare l&#39;esecuzione](#cancel).

![Azioni pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-actions.png)

## Finestra Attività {#activity}

La finestra **Attività** mostra un elenco completo di tutte le esecuzioni delle pipeline per il programma selezionato e di altri importanti eventi del programma.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina **Panoramica programma**, seleziona la scheda **Attività** per passare alla finestra **Attività**.

1. Qui puoi visualizzare un elenco di tutte le esecuzioni della pipeline del programma, comprese le esecuzioni correnti e quelle precedenti.

Se una pipeline è in esecuzione, facendo clic sull&#39;icona delle informazioni nella colonna **Stato** verranno visualizzati i dettagli sull&#39;esecuzione.

![Dettagli di esecuzione della pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-activity.png)

Toccando o facendo clic sulla riga che rappresenta l&#39;esecuzione della pipeline, viene visualizzato il [dettaglio dell&#39;esecuzione della pipeline](#view-details).

Puoi anche fare clic sul pulsante con i puntini di sospensione per intraprendere ulteriori azioni sull&#39;esecuzione della pipeline, ad esempio visualizzarne i dettagli o scaricare il registro, per passare alla [pagina dei dettagli della pipeline](#view-details).

![Azioni di esecuzione della pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-execution-actions.png)

## Esecuzione delle pipeline {#running-pipelines}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Passa alla scheda **Pipeline** dalla pagina **Panoramica del programma** e fai clic sul pulsante con i puntini di sospensione accanto alla pipeline eseguita, quindi seleziona **Esegui** dal menu.

1. L’esecuzione della pipeline viene avviata ed è indicata dalla colonna **Stato**.

Per visualizzare i dettagli dell’esecuzione, fai nuovamente clic sul pulsante con i puntini di sospensione e seleziona **[Visualizza dettagli](#view-details)**.

A seconda del tipo di pipeline, può essere possibile annullare l’esecuzione facendo nuovamente clic sul pulsante con i puntini di sospensione e selezionando **Annulla**.

## Modifica delle pipeline {#editing-pipelines}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Passa alla scheda **Pipeline** dalla pagina **Panoramica del programma**, fai clic sul pulsante dei puntini di sospensione accanto alla pipeline da modificare e seleziona **Modifica** dal menu.

1. Viene visualizzata la finestra di dialogo **Modifica pipeline di produzione** o **Modifica pipeline non di produzione**, che consente di modificare i dettagli inseriti durante la creazione della pipeline.

   * Per informazioni dettagliate sui campi e le opzioni di configurazione disponibili per le pipeline, consulta le pagine seguenti.
      * [Configurazione delle pipeline di produzione](configuring-production-pipelines.md)
      * [Configurazione delle pipeline non di produzione](configuring-non-production-pipelines.md)

1. Una volta completata la modifica della pipeline, fai clic su **Aggiorna**.

>[!NOTE]
>
>Non è possibile modificare una pipeline in esecuzione.

>[!NOTE]
>
>Le pipeline a livello web e di configurazione non sono supportate con gli archivi privati. Per dettagli e un elenco completo delle limitazioni, consulta [Aggiunta di archivi privati in Cloud Manager](/help/implementing/cloud-manager/managing-code/private-repositories.md).

## Eliminazione delle pipeline {#deleting-pipelines}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Passa alla scheda **Pipeline** dalla pagina **Panoramica del programma** e fai clic sul pulsante con i puntini di sospensione accanto alla pipeline eseguita, quindi seleziona **Elimina** dal menu.

>[!NOTE]
>
>Non è possibile eliminare una pipeline in esecuzione.

## Visualizzare i dettagli della pipeline {#view-details}

Puoi visualizzare i dettagli di una pipeline per visualizzarne lo stato e i registri dell’ultima esecuzione.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Passa alla scheda **Pipeline** dalla pagina **Panoramica programma**, fai clic sul pulsante con i puntini di sospensione accanto alla pipeline eseguita, quindi seleziona **Visualizza dettagli** dal menu.

1. L’opzione reindirizza alla pagina dei dettagli della pipeline in esecuzione.

![Dettagli della pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-running-details.png)

Da qui è possibile visualizzare lo stato dei vari passaggi della pipeline e recuperare i registri della build per finalità diagnostiche. Per ulteriori informazioni sulla distribuzione del codice e sull&#39;esecuzione dei test, vedere il documento [Distribuzione del codice](/help/implementing/cloud-manager/deploy-code.md).

Tutti i passaggi dell’esecuzione di una pipeline vengono visualizzati con quelli non ancora avviati non selezionabili. I passaggi completati mostrano la loro durata.

Una volta completato un passaggio della pipeline, viene presentato un riepilogo.

![Riepilogo del passaggio](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-step.png)

Seleziona il collegamento **Visualizza dettagli** per visualizzare la sezione **Durata**. Ciò include la durata media della pipeline in base alla tendenza storica per quel programma.

![Durata](/help/implementing/cloud-manager/assets/configure-pipeline/duration.png)

Se la pipeline conteneva un passaggio **Scansione del codice** durante il quale sono stati rilevati dei problemi, tocca o fai clic sul pulsante **Scarica dettagli** per visualizzare un elenco dei [test di qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md) che non sono stati superati.

![Problemi di qualità del codice](assets/managing-pipelines-code-quality-issues.png)

Nel file CSV, una colonna **Project File Location** (Percorso file di progetto) indica dove si trova il codice in cui è stato riscontrato un problema. Questa colonna contiene un percorso relativo al progetto, mentre la colonna **File Location** (Percorso file) è generata da Maven.

![Dettagli di problemi rilevati dalla scansione del codice del progetto](assets/managing-pipelines-code-quality-details.png)

>[!NOTE]
>
>È possibile visualizzare i dettagli solo per una pipeline in esecuzione o che è stata eseguita almeno una volta.

## Annulla pipeline {#cancel}

Se una pipeline si trova in fase di convalida o di creazione dell’immagine, puoi annullare l’esecuzione della pipeline in modo sicuro.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina della panoramica del programma, fai clic sul pulsante con i puntini di sospensione della pipeline che desideri annullare sulla scheda **Pipeline**.

   ![Annullamento di una pipeline](/help/implementing/cloud-manager/assets/cancel-pipeline.png)

1. Seleziona **Annulla**.

In alternativa, puoi annullare una pipeline dalla pagina dei dettagli della pipeline.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina **Panoramica del programma**, accedi alla scheda **Pipeline** e seleziona la pipeline da annullare.

1. L’opzione reindirizza alla pagina dei dettagli della pipeline in esecuzione.

   ![Annulla dettagli pipeline](/help/implementing/cloud-manager/assets/cancel-pipeline-details.png)

1. Seleziona **Annulla**.
