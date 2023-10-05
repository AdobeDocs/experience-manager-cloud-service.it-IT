---
title: Gestione delle pipeline
description: Scopri come gestire, modificare, eseguire ed eliminare le pipeline esistenti.
index: true
exl-id: 4aff5a84-134a-43fa-8de8-8d564f4edd16
source-git-commit: b8d692e354851a31b4f66b24135c863b5ca723b4
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 80%

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
