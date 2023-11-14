---
title: Gestione delle pipeline
description: Scopri come gestire, modificare, eseguire ed eliminare le pipeline esistenti.
index: true
exl-id: 4aff5a84-134a-43fa-8de8-8d564f4edd16
source-git-commit: 01a89f779689733fb82a556291e091026def63e0
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 59%

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
* [Visualizza dettagli](#view-details)

Nella parte inferiore dell’elenco delle pipeline sono disponibili le opzioni generali.

* **Aggiungi**: per [aggiungere una nuova pipeline di produzione](configuring-production-pipelines.md) o [una nuova pipeline non di produzione](configuring-non-production-pipelines.md).
* **Mostra tutto**: reindirizza l’utente alla schermata Pipeline per visualizzare tutte le pipeline in una tabella più dettagliata.
* **Accedi a dati archivio**: consente di visualizzare le informazioni necessarie per accedere all’archivio Git di Cloud Manager.
* **Ulteriori informazioni**: consente di accedere alle risorse della documentazione sulla pipeline CI/CD.

## Finestra Pipeline {#pipelines}

Il **Pipeline** viene visualizzato un elenco completo di tutte le pipeline per il programma selezionato. Questa funzione è utile in quanto presenta informazioni più complete rispetto a quelle disponibili nella [Scheda pipeline.](#pipeline-card)

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla sezione **Panoramica del programma** pagina, tocca o fai clic su **Pipeline** per passare alla scheda **Pipeline** finestra.

1. Qui puoi visualizzare un elenco di tutte le pipeline del programma, nonché avviare e interrompere l’esecuzione della pipeline come faresti nella **Scheda Pipeline**.

Se una pipeline è in esecuzione, passa il cursore sopra la relativa **Stato** rivelerà i dettagli sull’esecuzione.

![Dettagli di esecuzione della pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-status.png)

Toccare o fare clic **Visualizza dettagli** ti porterà al [i dettagli dell’esecuzione della pipeline.](#view-details)

## Finestra Attività {#activity}

Il **Attività** mostra un elenco completo di tutte le esecuzioni di pipeline per il programma selezionato.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla sezione **Panoramica del programma** pagina, tocca o fai clic su **Attività** per passare alla scheda **Attività** finestra.

1. Qui puoi vedere un elenco di tutte le esecuzioni della pipeline del programma, comprese le esecuzioni correnti e storiche.

Se una pipeline è in esecuzione, passa il cursore sopra la relativa **Stato** rivelerà i dettagli sull’esecuzione.

![Dettagli di esecuzione della pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-activity.png)

Toccare o fare clic **Visualizza dettagli** ti porterà al [i dettagli dell’esecuzione della pipeline.](#view-details)

## Esecuzione delle pipeline {#running-pipelines}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina **Panoramica del programma**, accedi alla scheda **Pipeline** e fai clic sul pulsante con i puntini di sospensione a fianco della pipeline eseguita, quindi seleziona **Esegui** dal menu.

1. L’esecuzione della pipeline viene avviata ed è indicata dalla colonna **Stato**.

Per visualizzare i dettagli dell’esecuzione, fai nuovamente clic sul pulsante con i puntini di sospensione e seleziona **[Visualizza dettagli.](#view-details)**

A seconda del tipo di pipeline, puoi annullare l’esecuzione facendo nuovamente clic sul pulsante con i puntini di sospensione e selezionando **Annulla**.

## Modifica delle pipeline {#editing-pipelines}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina **Panoramica del programma**, accedi alla scheda **Pipeline** e fai clic sul pulsante con i puntini di sospensione a fianco della pipeline che desideri modificare, quindi seleziona **Modifica** dal menu.

1. Viene visualizzata la finestra di dialogo **Modifica pipeline di produzione** o **Modifica pipeline non di produzione**, che consente di modificare i dettagli inseriti durante la creazione della pipeline.

   * Per ulteriori informazioni su tutti i campi e le opzioni di configurazione disponibili per le pipeline, consulta le pagine successive.
      * [Configurazione delle pipeline di produzione](configuring-production-pipelines.md)
      * [Configurazione delle pipeline non di produzione](configuring-non-production-pipelines.md)

1. Dopo aver ultimato la modifica della pipeline, fai clic su **Aggiorna**.

>[!NOTE]
>
>Non è possibile modificare una pipeline in esecuzione.

## Eliminazione delle pipeline {#deleting-pipelines}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina **Panoramica del programma**, accedi alla scheda **Pipeline** e fai clic sul pulsante con i puntini di sospensione a fianco della pipeline eseguita, quindi seleziona **Elimina** dal menu.

>[!NOTE]
>
>Non è possibile eliminare una pipeline in esecuzione.

## Visualizzare i dettagli della pipeline {#view-details}

Puoi visualizzare i dettagli di una pipeline per visualizzarne lo stato e i registri dell’ultima esecuzione.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina **Panoramica del programma**, accedi alla scheda **Pipeline** e fai clic sul pulsante con i puntini di sospensione a fianco della pipeline eseguita, quindi seleziona **Visualizza dettagli** dal menu.

1. L’opzione reindirizza alla pagina dei dettagli della pipeline in esecuzione.

![Dettagli della pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-running-details.png)

Da qui è possibile visualizzare lo stato dei vari passaggi della pipeline e recuperare i registri della build per finalità diagnostiche. Consulta il documento [Implementazione del codice](/help/implementing/cloud-manager/deploy-code.md) per ulteriori informazioni sulla distribuzione del codice e sull’esecuzione dei test.

Tutti i passaggi di un’esecuzione della pipeline vengono visualizzati con quelli non ancora avviati in grigio. I passaggi completati mostrano la loro durata.

Una volta completato un passaggio della pipeline, viene presentato un riepilogo.

![Riepilogo del passaggio](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-step.png)

Tocca o fai clic su **Visualizza dettagli** collegamento per visualizzare **Durata** sezione. Ciò include la durata media della pipeline in base alla tendenza storica per quel programma.

![Durata](/help/implementing/cloud-manager/assets/configure-pipeline/duration.png)

>[!NOTE]
>
>È possibile visualizzare i dettagli solo di una pipeline in esecuzione o eseguita almeno una volta.

## Annulla pipeline {#cancel}

Se una pipeline si trova in fase di convalida o di creazione dell’immagine, puoi annullare l’esecuzione della pipeline in modo sicuro.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina della panoramica del programma, fai clic sul pulsante con i puntini di sospensione della pipeline che desideri annullare nella **Pipeline** Card.

   ![Annullamento di una pipeline](/help/implementing/cloud-manager/assets/cancel-pipeline.png)

1. Tocca o fai clic su **Annulla**.

In alternativa, puoi annullare una pipeline dalla pagina dei dettagli della pipeline.

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Accedi a **Pipeline** scheda da **Panoramica del programma** tocca o fai clic sulla pipeline da annullare.

1. L’opzione reindirizza alla pagina dei dettagli della pipeline in esecuzione.

   ![Annulla dettagli pipeline](/help/implementing/cloud-manager/assets/cancel-pipeline-details.png)

1. Tocca o fai clic su **Annulla**.
