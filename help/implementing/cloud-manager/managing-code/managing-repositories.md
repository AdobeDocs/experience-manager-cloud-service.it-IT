---
title: Gestione degli archivi in Cloud Manager
description: Scopri come creare, visualizzare ed eliminare gli archivi Git in Cloud Manager.
exl-id: 6e1cf636-78f5-4270-9a21-38b4d5e5a0b0
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 92%

---


# Gestione degli archivi in Cloud Manager {#managing-repos}

Scopri come creare, visualizzare ed eliminare gli archivi Git in Cloud Manager.

## Panoramica {#overview}

Gli archivi vengono utilizzati per archiviare e gestire il codice del progetto utilizzando Git. Per ogni programma che crei in Cloud Manager viene creato un archivio gestito da Adobe.

Puoi creare archivi aggiuntivi gestiti da Adobe e puoi anche aggiungere archivi privati. Tutti gli archivi associati al programma possono essere visualizzati nella finestra **Archivi**.

Gli archivi creati in Cloud Manager sono disponibili per la selezione anche quando aggiungi o modifichi le pipeline. Per ulteriori informazioni, consulta [Pipeline CI-CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).

Esiste un singolo archivio principale o ramo per ogni pipeline. Grazie al [supporto dei sottomoduli Git](git-submodules.md), al momento della creazione è possibile aggiungere molti rami secondari.

## Finestra Archivi {#repositories-window}

1. Accedi a Cloud Manager all’indirizzo [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) e seleziona l’organizzazione e il programma appropriati.

1. Dalla pagina **Panoramica del programma**, seleziona la scheda **Archivi** per passare alla pagina **Archivi**.

1. Nella finestra **Archivi** vengono visualizzati tutti gli archivi associati al programma.

   ![Finestra Archivi](assets/repositories.png)

La finestra **Archivi** fornisce dettagli sugli archivi:

* Tipo di archivio
   * **Adobe** indica archivi gestiti da Adobe
   * **GitHub** indica archivi GitHub privati che gestisci tu direttamente
* Data di creazione
* Pipeline associate all’archivio

In questa finestra puoi selezionare un archivio e fare clic sul pulsante con i puntini di sospensione per intervenire sull’archivio selezionato.

* **[Controlla rami/Crea progetto](#check-branches)** (disponibile solo per gli archivi Adobe)
* **[Copia URL archivio](#copy-url)**
* **[Visualizza e aggiorna](#view-update)**
* **[Elimina](#delete)**

![Azioni per un archivio](assets/repository-actions.png)

## Aggiunta di archivi {#adding-repositories}

Tocca o fai clic sul pulsante **Aggiungi archivio** nella finestra **Archivi** per avviare la procedura guidata **Aggiungi archivio**.

![Procedura guidata Aggiungi archivio](assets/add-repository-wizard.png)

Cloud Manager supporta sia gli archivi gestiti da Adobe (**Archivio Adobe**) sia quelli che puoi gestire direttamente (**Archivio privato**). I campi obbligatori dipendono dal tipo di archivio che scegli di aggiungere. Per ulteriori dettagli, consulta i seguenti documenti.

* [Aggiunta di archivi Adobe in Cloud Manager](adobe-repositories.md)
* [Aggiunta di archivi privati in Cloud Manager](private-repositories.md)

>[!NOTE]
>
>* Per poter aggiungere un archivio, l’utente deve avere il ruolo **Manager implementazione** o **Proprietario business**.
>* Per ogni azienda o organizzazione IMS, vi è un limite di 300 archivi per tutti i programmi.

## Accedi a dati archivio {#repo-info}

Quando visualizzi i tuoi archivi nella finestra **Archivi**, puoi visualizzare i dettagli su come accedere agli archivi gestiti da Adobe a livello di programmazione facendo clic sul pulsante **Accedi a dati archivio** nella barra degli strumenti.

![Informazioni sull’archivio](assets/repo-info.png)

La finestra **Informazioni archivio** si apre con i dettagli. Per ulteriori informazioni sull&#39;accesso alle informazioni del repository, vedere il documento [Accesso alle informazioni del repository](accessing-repos.md).

## Controlla rami/Crea progetto {#check-branches}

L’azione **Controlla rami/Crea progetto** esegue due funzioni a seconda dello stato dell’archivio.

* Se l’archivio è stato appena creato, l’azione crea un progetto di esempio basato sull’[Archetipo progetto AEM](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/developing/archetype/overview).
* Se nell’archivio è già stato creato il progetto di esempio, viene verificato lo stato dell’archivio e dei relativi rami e vengono generati rapporti se il progetto di esempio esiste già.

![Azione Controlla rami](assets/check-branches.png)

## Copia URL archivio {#copy-url}

L’azione **Copia URL archivio** copia negli Appunti l’URL dell’archivio selezionato nella finestra **Archivi**, per utilizzarlo altrove.

## Visualizza e aggiorna {#view-update}

L’azione **Visualizza e aggiorna** apre la finestra di dialogo **Aggiorna archivio**. Questo permette di visualizzare **Nome** e **Anteprima URL archivio** nonché di aggiornare la **Descrizione** dell’archivio.

![Visualizzare e aggiornare le informazioni del dell’archivio](assets/view-update.png)

## Elimina {#delete}

L’azione **Elimina** rimuove l’archivio dal progetto. Un archivio non può essere eliminato se è associato a una pipeline.

![Elimina](assets/delete.png)

L’eliminazione di un archivio:

* Rende il nome dell’archivio eliminato inutilizzabile per i nuovi archivi che possono essere creati in futuro.
   * In tali casi viene visualizzato il messaggio di errore `Repository name should be unique within organization.`.
* Rende l’archivio eliminato non disponibile in Cloud Manager e non disponibile per il collegamento a una pipeline.
