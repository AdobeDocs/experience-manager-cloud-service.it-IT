---
title: Casella in entrata
description: Scopri come utilizzare le notifiche che arrivano nella casella in entrata per gestire le attività.
exl-id: 37d0cf43-192f-4a50-b174-42d7dced3b63
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 88%

---

# Casella in entrata {#your-inbox}

Puoi ricevere notifiche da diverse aree di AEM, inclusi flussi di lavoro e progetti. Ad esempio, puoi ricevere notifiche relative a:

* Attività:
   * Possono essere create anche in diversi punti nell’interfaccia di AEM, ad esempio in **Progetti**.
   * Possono essere il prodotto del passaggio **Crea attività** o **Crea attività per progetto** di un flusso di lavoro.
* Flussi di lavoro:
   * Elementi di lavoro che rappresentano le azioni da eseguire sul contenuto di una pagina
      * Sono il prodotto dei passaggi **Partecipante** di un flusso di lavoro.
   * Elementi con errori, per consentire agli amministratori di ripetere il passaggio non riuscito

Queste notifiche vengono ricevute nella tua casella in entrata, dove puoi visualizzarle e agire di conseguenza.

>[!NOTE]
>
>Per ulteriori informazioni sui tipi di elemento, consulta quanto segue:
>
>* [Progetti](/help/sites-cloud/authoring/projects/overview.md)
>* [Progetti: lavorare con le attività](/help/sites-cloud/authoring/projects/tasks.md)
>* [Flussi di lavoro](/help/sites-cloud/authoring/workflows/overview.md)

## Casella in entrata nell’intestazione {#inbox-in-the-header}

Da una qualsiasi console, il numero corrente di elementi nella casella in entrata viene visualizzato nell’intestazione. L’indicatore può anche essere aperto per fornire un accesso rapido alle pagine che richiedono azioni o accesso alla casella in entrata:

![Panoramica della casella in entrata nell’intestazione](/help/sites-cloud/authoring/assets/inbox-header.png)

>[!NOTE]
>
>Alcune azioni sono anche visualizzate nella [vista a schede della relativa risorsa](/help/sites-cloud/authoring/basic-handling.md#card-view).

## Apertura della casella in entrata  {#opening-the-inbox}

Per aprire la casella in entrata delle notifiche AEM:

1. Seleziona l’indicatore nella barra degli strumenti.

1. Seleziona **Visualizza tutto**. Il **Casella in entrata AEM** viene aperto. La casella in entrata mostra gli elementi dei flussi di lavoro, delle attività e dei progetti.
1. La vista predefinita è [Vista elenco](#inbox-list-view), ma puoi anche passare alla [Vista calendario](#inbox-calendar-view). Questa operazione viene effettuata con il selettore vista (barra degli strumenti, in alto a destra).

   Per entrambe le viste puoi inoltre definire le [Impostazioni vista](#inbox-view-settings). Le opzioni disponibili dipendono dalla vista corrente.

   ![Casella in entrata - Impostazioni vista](/help/sites-cloud/authoring/assets/inbox-view-settings.png)

>[!NOTE]
>
>La casella in entrata funziona come una console; puoi quindi utilizzare le funzioni di [Navigazione globale](/help/sites-cloud/authoring/basic-handling.md#global-navigation) o [Ricerca](/help/sites-cloud/authoring/search.md) per passare a un’altra posizione al termine dell’operazione.

### Casella in entrata - Vista a elenco {#inbox-list-view}

Questa vista mostra tutti gli elementi con le relative informazioni:

![Casella in entrata - Vista a elenco](/help/sites-cloud/authoring/assets/inbox-list-view.png)

### Casella in entrata - Vista calendario {#inbox-calendar-view}

Questa vista mostra gli elementi in base alla loro posizione nel calendario:

![Casella in entrata - Vista calendario](/help/sites-cloud/authoring/assets/inbox-calendar-view.png)

Operazioni disponibili:

* Selezionare una vista specifica: **Timeline**,**Colonna**, **Elenco**
* Specificare le attività da visualizzare in base a **Pianificazione**: **Tutti**, **Pianificato**, **In corso**, **In scadenza**, **Scaduto**
* Eseguire un drill-down per ottenere informazioni più dettagliate su un elemento
* Selezionare un intervallo di date per restringere la visualizzazione:

![Casella in entrata - Intervallo di date per la vista calendario](/help/sites-cloud/authoring/assets/inbox-calendar-range.png)

### Casella in entrata - Impostazioni vista {#inbox-view-settings}

Per entrambe le viste (Elenco e Calendario) puoi definire le impostazioni:

* **Vista calendario**

  Per **Vista calendario** puoi configurare:

   * **Raggruppa per**
   * **Pianificazione** o **Nessuna**
   * **Dimensioni scheda**

  ![Casella in entrata - Impostazioni della vista calendario](/help/sites-cloud/authoring/assets/inbox-calendar-settings.png)

* **Vista a elenco**

  Per **Vista a elenco** puoi configurare il metodo di ordinamento:

   * **Ordina per**
   * **Ordinamento**

  ![Casella in entrata - Impostazioni della vista a elenco](/help/sites-cloud/authoring/assets/inbox-list-settings.png)

  Puoi anche delegare il calendario ad altri utenti, richiedere la delega ad altri utenti e gestire le tue deleghe.

  ![Casella in entrata - Impostazioni di delega della vista a elenco](/help/sites-cloud/authoring/assets/inbox-delegation.png)

## Intervenire su un elemento {#taking-action-on-an-item}

>[!NOTE]
>
>Sebbene sia possibile selezionare più elementi, le azioni possono essere eseguite solo su un elemento alla volta.

1. Per intervenire su un elemento, seleziona la miniatura dell’elemento appropriato. Le icone per le azioni applicabili a tale elemento sono visualizzate nella barra degli strumenti:

   ![Selezione dell’elemento della casella in entrata](/help/sites-cloud/authoring/assets/inbox-select-item.png)

   Le azioni dipendono dall’elemento selezionato e includono:

   * **Completa** l’azione
   * **Delega** un elemento
   * **Apri** un elemento; a seconda del tipo di elemento, questa azione può:

      * Mostrare le proprietà dell’elemento
      * Aprire un dashboard o una procedura guidata per eseguire ulteriori azioni
      * Aprire la documentazione correlata

   * **Indietro** per tornare a un passaggio precedente
   * Visualizzazione del payload di un flusso di lavoro
   * Creazione di un progetto dall’elemento

   >[!NOTE]
   >
   >Per ulteriori informazioni, consulta:
   >
   >* Elementi del flusso di lavoro - [Partecipazione ai flussi di lavoro](/help/sites-cloud/authoring/workflows/participating.md)

2. A seconda dell’elemento selezionato, viene avviata un’azione, ad esempio:

   * Viene aperta una finestra di dialogo appropriata per l’azione
   * Viene avviata una procedura guidata per un’azione
   * Viene aperta una pagina della documentazione

   Ad esempio: **Delega** apre una finestra di dialogo:

   ![Delega di un’attività della casella in entrata](/help/sites-cloud/authoring/assets/inbox-assign-task.png)

   A seconda della finestra di dialogo, procedura guidata o pagina di documentazione aperta, è possibile:

   * Conferma l’azione appropriata, ad esempio Riassegna.
   * Annullare l’azione.
   * Seleziona la freccia indietro per tornare alla casella in entrata. Ad esempio, se è stata aperta una Action Wizard o una pagina della documentazione, puoi tornare alla casella in entrata.

## Creazione di un’attività {#creating-a-task}

Dalla casella in entrata è possibile creare le attività:

1. Seleziona **Crea**, quindi **Attività**.
1. Compila i campi necessari nelle schede **Base** e **Avanzate**. È obbligatorio solo il campo **Titolo**; tutti gli altri campi sono facoltativi.

   * **Base**:

      * **Titolo**
      * **Progetto**
      * **Assegnatario**
      * **Contenuto**: simile al payload, è un riferimento dall’attività a una posizione nell’archivio.
      * **Descrizione**
      * **Priorità attività**
      * **Data inizio**
      * **Data di scadenza**

   ![Casella in entrata - Aggiunta di un’attività](/help/sites-cloud/authoring/assets/inbox-create-task.png)

   * **Avanzate**

      * **Nome**: utilizzato per formare l’URL; se vuoto, si basa sul valore **Titolo**.

   ![Casella in entrata - Opzioni avanzate per l’aggiunta di un’attività](/help/sites-cloud/authoring/assets/inbox-add-task-advanced.png)

1. Seleziona **Invia**.

## Creazione di un progetto  {#creating-a-project}

Per alcune attività puoi creare un [Progetto](/help/sites-cloud/authoring/projects/overview.md) in base all’attività in questione:

1. Seleziona l’attività appropriata, toccando o facendo clic sulla miniatura.

   >[!NOTE]
   >
   >Per creare un progetto, è possibile utilizzare solo le attività create con l’opzione **Crea** della **Casella in entrata**.
   >
   >Gli elementi di lavoro (di un flusso di lavoro) non possono essere utilizzati per creare un progetto.

1. Dalla barra degli strumenti, seleziona **Crea progetto** per aprire la procedura guidata.
1. Seleziona il modello appropriato, quindi **Avanti**.
1. Specifica le proprietà richieste:

   * **Base**

      * **Titolo**
      * **Descrizione**
      * **Data inizio**
      * **Data di scadenza**
      * **Utente** e ruolo

   * **Avanzate**

      * **Nome**

   >[!NOTE]
   >
   >Consulta [Creazione di un progetto](/help/sites-cloud/authoring/projects/managing.md#creating-a-project) per ricevere informazioni complete.

1. Seleziona **Crea** per confermare l’azione.

## Filtrare gli elementi nella Casella in entrata AEM {#filtering-items-in-the-aem-inbox}

Puoi filtrare gli elementi elencati:

1. Apri la **Casella in entrata AEM**.

1. Apri il selettore del filtro:

   ![Casella in entrata - Ricerca](/help/sites-cloud/authoring/assets/inbox-search.png)

1. Puoi filtrare gli elementi elencati in base a diversi criteri, molti dei quali possono essere regolati, ad esempio:

   ![Casella in entrata - Filtro di ricerca](/help/sites-cloud/authoring/assets/inbox-search-filter.png)

   >[!NOTE]
   >
   >Con [Impostazioni vista](#inbox-view-settings) è anche possibile configurare l’ordinamento quando si utilizza la [Vista a elenco](#inbox-list-view).
