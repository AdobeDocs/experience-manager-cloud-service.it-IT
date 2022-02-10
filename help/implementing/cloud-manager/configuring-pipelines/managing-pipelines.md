---
title: Gestione delle pipeline
description: Scopri come gestire le pipeline esistenti, tra cui modificarle, eseguirle ed eliminarle.
index: true
source-git-commit: 22a08a0cb80052485309ce3d33537e9fe303c6f5
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---


# Gestione delle pipeline {#managing-pipelines}

Scopri come gestire le pipeline esistenti, tra cui modificarle, eseguirle ed eliminarle.

## Scheda pipeline {#pipeline-card}

La **Tubi** scheda **Panoramica del programma** in Cloud Manager offre una panoramica di tutte le pipeline e del loro stato corrente.

![Scheda pipeline in Cloud Manager](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

Facendo clic sul pulsante con i puntini di sospensione accanto a ciascuna pipeline puoi effettuare le seguenti operazioni.

* [Eseguire la pipeline](#running-pipelines)
* [Modificare la pipeline](#editing-pipelines)
* [Eliminare la pipeline](#deleting-pipelines)
* [Visualizza dettagli](#view-details)

Nella parte inferiore dell’elenco delle pipeline sono disponibili opzioni generali.

* **Aggiungi** - A [aggiungi una nuova pipeline di produzione](configuring-production-pipelines.md) o [aggiungi nuova pipeline non di produzione](configuring-non-production-pipelines.md)
* **Mostra tutto** - Consente all’utente di passare alla schermata Pipelines (Pipelines) per visualizzare tutte le pipeline in una tabella più dettagliata.
* **Accesso alle informazioni sul repository** - Visualizza le informazioni necessarie per accedere all’archivio Git di Cloud Manager.
* **Ulteriori informazioni** - Passa alle risorse della documentazione della pipeline CI/CD.

## Pipellini in esecuzione {#running-pipelines}

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione e il programma appropriati.

1. Passa a **Tubi** scheda da **Panoramica del programma** e fai clic sul pulsante dei puntini di sospensione accanto alla pipeline eseguita, seleziona **Esegui** dal menu.

1. L’esecuzione della pipeline inizia ed è indicata dalla **Stato** colonna.

Per visualizzare i dettagli dell&#39;esecuzione, fai nuovamente clic sul pulsante con i puntini di sospensione e seleziona **[Visualizza i dettagli.](#view-details)**

A seconda del tipo di pipeline, può essere possibile annullare l’esecuzione facendo nuovamente clic sul pulsante con i puntini di sospensione e selezionando **Annulla**.

## Modifica delle pipeline {#editing-pipelines}

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione e il programma appropriati.

1. Passa a **Tubi** scheda da **Panoramica del programma** fate clic sul pulsante dei puntini di sospensione accanto alla pipeline da modificare, quindi selezionate **Modifica** dal menu.

1. La **Modifica pipeline di produzione** o **Modifica pipeline non di produzione** viene visualizzata una finestra di dialogo che consente di modificare gli stessi dettagli immessi durante la creazione della pipeline.

   * Vedi le pagine seguenti per i dettagli su tutti i campi e le opzioni di configurazione disponibili per le pipeline.
      * [Configurazione delle pipeline di produzione](configuring-production-pipelines.md)
      * [Configurazione di pipeline non di produzione](configuring-non-production-pipelines.md)

1. Fai clic su **Aggiorna** una volta completata la modifica della pipeline.

>[!NOTE]
>
>Non è possibile modificare una pipeline in esecuzione.

## Eliminazione delle pipeline {#deleting-pipelines}

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione e il programma appropriati.

1. Passa a **Tubi** scheda da **Panoramica del programma** e fai clic sul pulsante dei puntini di sospensione accanto alla pipeline eseguita, seleziona **Elimina** dal menu.

>[!NOTE]
>
>Non è possibile eliminare una pipeline in esecuzione.

## Visualizza dettagli {#view-details}

1. Accedi a Cloud Manager all&#39;indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e selezionare l&#39;organizzazione e il programma appropriati.

1. Passa a **Tubi** scheda da **Panoramica del programma** e fai clic sul pulsante dei puntini di sospensione accanto alla pipeline eseguita, seleziona **Visualizza dettagli** dal menu.

1. Viene visualizzata la pagina dei dettagli della pipeline in esecuzione.

![Dettagli della pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-running-details.png)

Da qui puoi vedere lo stato dei vari passaggi della pipeline e recuperare i registri di creazione a scopo diagnostico. Vedere il documento [Implementazione del codice](/help/implementing/cloud-manager/deploy-code.md) per ulteriori informazioni.

>[!NOTE]
>
>È possibile visualizzare solo i dettagli di una pipeline in esecuzione o eseguita almeno una volta.