---
title: Gestione degli archivi in Cloud Manager
description: Scopri come creare, visualizzare ed eliminare gli archivi Git in Cloud Manager.
exl-id: 6e1cf636-78f5-4270-9a21-38b4d5e5a0b0
source-git-commit: e467c8058531441524fedd37e14b82b7fb255c69
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 29%

---


# Gestione degli archivi in Cloud Manager {#managing-repos}

Scopri come creare, visualizzare ed eliminare gli archivi Git in Cloud Manager.

## Panoramica {#overview}

Gli archivi vengono utilizzati per archiviare e gestire il codice del progetto utilizzando Git. Ogni programma creato in Cloud Manager dispone di un archivio gestito da Adobe.

Puoi scegliere di creare archivi aggiuntivi per la gestione degli Adobi e aggiungere anche archivi privati. Tutti gli archivi associati al programma possono essere visualizzati nella sezione **Archivi** finestra.

Gli archivi creati in Cloud Manager sono disponibili per la selezione anche quando aggiungi o modifichi le pipeline. Per ulteriori informazioni, consulta [Pipeline CI-CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).

Esiste un singolo archivio principale o ramo per ogni pipeline. Con [supporto per i moduli Git secondari,](git-submodules.md) molti rami secondari possono essere inclusi al momento della generazione.

## Finestra Archivi {#repositories-window}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla sezione **Panoramica del programma** , seleziona la **Archivi** per passare alla scheda **Archivi** pagina.

1. Il **Archivi** visualizza tutti gli archivi associati al programma.

   ![Finestra Archivi](assets/repositories.png)

Il **Archivi** fornisce dettagli sugli archivi:

* Tipo di archivio
   * **Adobe** indica archivi gestiti da Adobe
   * **GitHub** indica gli archivi GitHub privati che gestisci
* Quando è stato creato
* Pipeline associate all’archivio

Puoi selezionare l’archivio nella finestra e fare clic sul pulsante con i puntini di sospensione per intervenire sull’archivio selezionato.

* **[Controlla rami/Crea progetto](#check-branches)** (disponibile solo per archivi di Adobi)
* **[Copia URL archivio](#copy-url)**
* **[Visualizza e aggiorna](#view-update)**
* **[Eliminare](#delete)**

![Azioni dell’archivio](assets/repository-actions.png)

## Aggiunta di archivi {#adding-repositories}

Tocca o fai clic su **Aggiungi archivio** pulsante in **Archivi** finestra per avviare **Aggiungi archivio** procedura guidata.

![Aggiunta guidata archivio](assets/add-repository-wizard.png)

Cloud Manager supporta entrambi gli archivi gestiti da Adobe (**Archivio Adobe**) e i tuoi archivi gestiti autonomamente (**Archivio privato**). I campi obbligatori variano a seconda del tipo di archivio che si sceglie di aggiungere. Per ulteriori informazioni, consulta i seguenti documenti.

* [Aggiunta di archivi di Adobi in Cloud Manager](adobe-repositories.md)
* [Aggiunta di archivi privati in Cloud Manager](private-repositories.md)

>[!NOTE]
>
>* Per poter aggiungere un archivio, l’utente deve avere il ruolo **Responsabile dell’implementazione** o **Proprietario business**.
>* Per ogni azienda o organizzazione IMS, vi è un limite di 300 archivi per tutti i programmi.

## Accedi a dati archivio {#repo-info}

Quando visualizzi gli archivi in **Archivi** , puoi visualizzare i dettagli su come accedere agli archivi gestiti da Adobe a livello di programmazione toccando o facendo clic sul pulsante **Accedi a dati archivio** nella barra degli strumenti.

![Informazioni sull’archivio](assets/repo-info.png)

Il **Informazioni archivio** Viene visualizzata la finestra con i dettagli. Per ulteriori informazioni sull’accesso alle informazioni dell’archivio, consulta il documento [Accesso alle informazioni dell’archivio.](accessing-repos.md)

## Controlla rami/Crea progetto {#check-branches}

Il **Controlla rami/Crea progetto** action esegue due funzioni a seconda dello stato dell’archivio.

* Se l’archivio è stato appena creato, l’azione crea un progetto di esempio basato su [l’archetipo del progetto AEM.](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/developing/archetype/overview)
* Se nell’archivio è già stato creato il progetto di esempio, viene verificato lo stato dell’archivio e dei relativi rami e vengono generati rapporti se il progetto di esempio esiste già.

![Azione Controlla rami](assets/check-branches.png)

## Copia URL archivio {#copy-url}

Il **Copia URL archivio** copia l’URL dell’archivio selezionato nella **Archivi** negli Appunti da utilizzare altrove.

## Visualizza e aggiorna {#view-update}

Il **Visualizza e aggiorna** azione apre il **Aggiorna archivio** . È possibile visualizzare **Nome** e **Anteprima URL archivio** nonché aggiornare **Descrizione** dell’archivio.

![Visualizzare e aggiornare le informazioni del repository](assets/view-update.png)

## Eliminare {#delete}

Il **Elimina** rimuove l’archivio dal progetto. Un archivio non può essere eliminato se è associato a una pipeline.

![Eliminare](assets/delete.png)

L’eliminazione di un archivio:

* Rende il nome dell’archivio eliminato inutilizzabile per i nuovi archivi che possono essere creati in futuro.
   * In tali casi viene visualizzato il messaggio di errore `Repository name should be unique within organization.`.
* Rende l’archivio eliminato non disponibile in Cloud Manager e non disponibile per il collegamento a una pipeline.
