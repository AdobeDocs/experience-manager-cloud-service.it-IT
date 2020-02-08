---
title: Casella in entrata
description: Gestione delle attività con la casella in entrata
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Casella in entrata {#your-inbox}

Puoi ricevere notifiche da varie aree di AEM, compresi flussi di lavoro e progetti. Ad esempio, potresti ricevere notifiche su:

* Attività:
   * These can also be created at various points within the AEM UI, for example, under **Projects**.
   * These can be the product of a workflow **Create Task** or **Create Project Task** step.
* Flussi di lavoro:
   * Elementi di lavoro che rappresentano azioni da eseguire sul contenuto della pagina
      * These are the product of workflow **Participant** steps.
   * Errori negli elementi, per consentire agli amministratori di ripetere il passaggio non riuscito

Queste notifiche arrivano nella casella in entrata, dove puoi visualizzarle e intraprendere le azioni necessarie.

>[!NOTE]
>
>Per ulteriori informazioni sui tipi di elementi vedi anche:
>
>* [Progetti](/help/sites-cloud/authoring/projects/overview.md)
>* [Progetti: lavorare con le attività](/help/sites-cloud/authoring/projects/tasks.md) 
>* [Flussi di lavoro](/help/sites-cloud/authoring/workflows/overview.md)


## Casella in entrata nell’intestazione {#inbox-in-the-header}

Per le varie console, il numero corrente di elementi nella casella in entrata è riportato nell’intestazione. Mediante questo indicatore è possibile accedere rapidamente alle pagine che richiedono interventi o alla casella in entrata:

![Panoramica della casella in entrata nell’intestazione](/help/sites-cloud/authoring/assets/inbox-header.png)

>[!NOTE]
>
>Alcune azioni sono anche visualizzate nella [vista a schede della relativa risorsa](/help/sites-cloud/authoring/getting-started/basic-handling.md#card-view).

## Apertura della casella in entrata {#opening-the-inbox}

Per aprire la casella in entrata delle notifiche AEM:

1. Toccate o fate clic sull’indicatore nella barra degli strumenti.

1. Seleziona **Visualizza tutto**. Viene aperta la **Casella in entrata AEM.** La casella in entrata mostra gli elementi dei flussi di lavoro, delle attività e dei progetti.
1. La vista predefinita è [Vista a elenco](#inbox-list-view), ma puoi anche passare alla [Vista calendario](#inbox-calendar-view) dal selettore delle viste (barra degli strumenti in alto a destra).

   For both views you can also define [View Settings](#inbox-view-settings). The options available are dependent on the current view.

   ![Impostazioni della vista Inbox](/help/sites-cloud/authoring/assets/inbox-view-settings.png)

>[!NOTE]
>
>The Inbox operates as a console, so use [Global Navigation](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation) or [Search](/help/sites-cloud/authoring/getting-started/search.md) to navigate to another location when you are finished.

### Casella in entrata - Vista a elenco {#inbox-list-view}

Questa visualizzazione elenca tutti gli elementi, insieme alle informazioni pertinenti:

![Vista elenco Posta in arrivo](/help/sites-cloud/authoring/assets/inbox-list-view.png)

### Casella in entrata - Vista calendario {#inbox-calendar-view}

Questa visualizzazione presenta gli elementi in base alla loro posizione nel calendario:

![Vista calendario Posta in arrivo](/help/sites-cloud/authoring/assets/inbox-calendar-view.png)

Tieni presente quanto segue:

* Select a specific view: **Timeline**, **Column**, **List**
* Specify the tasks to display according to **Schedule**: **All**, **Planned**, **In Progress**, **Due Soon**, **Past Due**
* Approfondisci per informazioni più dettagliate su un elemento
* Selezionare un intervallo di date per attivare la visualizzazione:

![Intervallo date visualizzazione calendario in entrata](/help/sites-cloud/authoring/assets/inbox-calendar-range.png)

### Casella in entrata - Visualizza impostazioni {#inbox-view-settings}

Puoi definire le impostazioni per entrambe le viste (Elenco e Calendario):

* **Vista calendario**

   Per la **Vista calendario** puoi configurare:

   * **Raggruppa per**
   * **Programma** o **Nessuno**
   * **Dimensioni scheda**
   ![Impostazioni visualizzazione calendario in entrata](/help/sites-cloud/authoring/assets/inbox-calendar-settings.png)

* **Vista a elenco**

   Per la **Vista a elenco** puoi configurare il metodo di ordinamento:

   * **Ordina per**
   * **Ordinamento**
   ![Impostazioni visualizzazione elenco Posta in arrivo](/help/sites-cloud/authoring/assets/inbox-list-settings.png)

   Puoi anche delegare il calendario ad altri utenti, nonché richiedere la delega ad altri utenti e gestire le delegazioni.

   ![Impostazioni di delega della vista elenco Posta in arrivo](/help/sites-cloud/authoring/assets/inbox-delegation.png)

## Intraprendere un’azione su un elemento {#taking-action-on-an-item}

1. Per intervenire su un elemento, seleziona la miniatura dell&#39;elemento appropriato. Le icone per le azioni applicabili per l’elemento in questione sono disponibili nella barra degli strumenti:

   ![Seleziona elemento inbox](/help/sites-cloud/authoring/assets/inbox-select-item.png)

   Le azioni dipendono dall’elemento selezionato e includono:

   * **Completa** azione
   * **Delega** di un elemento
   * **Aprite** un elemento, a seconda del tipo di elemento, questa azione può:

      * Mostra proprietà elemento
      * Aprire una dashboard o una procedura guidata appropriata per ulteriori azioni
      * Apri documentazione correlata
   * **Indietro** per tornare a un passaggio precedente
   * Visualizzare il payload di un flusso di lavoro
   * Creare un progetto dall&#39;elemento
   >[!NOTE]
   >
   >Per ulteriori informazioni, consulta:
   >
   >* Elementi di flussi di lavoro - [Partecipazione ai flussi di lavoro](/help/sites-cloud/authoring/workflows/participating.md)


1. A seconda dell’elemento selezionato, verrà avviata un’azione, ad esempio:

   * Viene aperta la finestra di dialogo relativa all’azione
   * Verrà avviata un&#39;azione guidata
   * Viene aperta una pagina della documentazione
   For example, **Delegate** will open a dialog:

   ![Delega attività inbox](/help/sites-cloud/authoring/assets/inbox-assign-task.png)

   A seconda della finestra di dialogo, procedura guidata o pagina di documentazione aperta, è possibile:

   * Confermate l’azione appropriata, ad esempio riassegnate.
   * Annullare l’azione
   * Selezionate la freccia indietro per tornare alla inbox, ad esempio se è stata aperta un&#39;azione guidata o una pagina della documentazione, potete tornare alla inbox.


## Creazione di un’attività {#creating-a-task}

Dalla casella in entrata è possibile creare le attività:

1. Seleziona **Crea**, quindi **Attività**.
1. Complete the necessary fields in the **Basic** and **Advanced** tabs (only the **Title** is mandatory, all others are optional):

   * **Base**:

      * **Titolo**
      * **Progetto**
      * **Assegnatario**
      * **Contenuto**, simile a Payload, è un riferimento dall&#39;attività a una posizione nella directory archivio
      * **Descrizione**
      * **Priorità attività**
      * **Data iniziale**
      * **Data di scadenza**
   ![Casella in entrata aggiungi attività](/help/sites-cloud/authoring/assets/inbox-create-task.png)

   * **Avanzate**

      * **Nome**: verrà utilizzato per creare l’URL e, se vuoto, verrà basato sul **Titolo**.
   ![Casella in entrata aggiungere le opzioni avanzate dell&#39;attività](/help/sites-cloud/authoring/assets/inbox-add-task-advanced.png)

1. Seleziona **Invia**.

## Creazione di un progetto {#creating-a-project}

Per determinate attività, puoi creare un [Progetto](/help/sites-cloud/authoring/projects/overview.md) basato su tale attività:

1. Seleziona l’attività appropriata toccando o facendo clic sulla miniatura.

   >[!NOTE]
   >
   >Only tasks created using the **Create** option of the **Inbox** can be used to create a project.
   >
   >Gli elementi di lavoro (da un flusso di lavoro) non possono essere utilizzati per creare un progetto.

1. Seleziona **Crea progetto** nella barra degli strumenti per aprire la procedura guidata.
1. Seleziona il modello appropriato, quindi **Avanti**.
1. Specifica le proprietà richieste:

   * **Base**

      * **Titolo**
      * **Descrizione**
      * **Data iniziale**
      * **Data di scadenza**
      * **Utente** e ruolo
   * **Avanzate**

      * **Nome**
   >[!NOTE]
   >
   >Per maggiori informazioni, consulta [Creazione di un progetto](/help/sites-cloud/authoring/projects/managing.md#creating-a-project).

1. Seleziona **Crea** per confermare l’azione.

## Filtrare gli elementi nella casella in entrata di AEM {#filtering-items-in-the-aem-inbox}

Potete filtrare gli elementi elencati:

1. Apri la **Casella in entrata AEM**.

1. Apri il selettore del filtro:

   ![Ricerca in entrata](/help/sites-cloud/authoring/assets/inbox-search.png)

1. Potete filtrare gli elementi elencati in base a una serie di criteri, molti dei quali possono essere regolati.Ad esempio:

   ![Filtro ricerca Inbox](/help/sites-cloud/authoring/assets/inbox-search-filter.png)

   >[!NOTE]
   >
   >Con [Visualizza impostazioni](#inbox-view-settings) è anche possibile configurare l’ordinamento quando si usa la [Vista a elenco](#inbox-list-view).
