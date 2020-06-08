---
title: Partecipare ai Flussi di lavoro
description: I flussi di lavoro generalmente includono passaggi che richiedono di eseguire un’attività in una pagina o una risorsa.
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '1545'
ht-degree: 72%

---


# Partecipare ai Flussi di lavoro {#participating-in-workflows}

I flussi di lavoro generalmente includono passaggi che richiedono di eseguire un’attività in una pagina o una risorsa. Il flusso di lavoro seleziona un utente o un gruppo che esegua l’attività e assegna loro un elemento di lavoro. L&#39;utente riceve la notifica e intraprende l&#39;azione appropriata:

* [Visualizzazione delle notifiche](#notifications-of-available-workflow-actions)
* [Completa un Passaggio Partecipante](#completing-a-participant-step)
* [Delega un Passaggio Partecipante](#delegating-a-participant-step)
* [Esegui un passo indietro su un Passaggio Partecipante](#performing-step-back-on-a-participant-step)
* [Apri un elemento del flusso di lavoro per visualizzare i dettagli (e Intraprendere Azioni)](#opening-a-workflow-item-to-view-details-and-take-actions)
* [Visualizza il Payload flusso di lavoro (Risorse Multiple)](#viewing-the-workflow-payload-multiple-resources)

## Notifiche delle Azioni disponibili per il Flusso di lavoro {#notifications-of-available-workflow-actions}

Quando ti viene assegnato un elemento di lavoro (ad esempio, **Approva contenuto**) vengono visualizzati diversi avvisi e/o notifiche:

* L&#39;indicatore di [notifica](/help/sites-cloud/authoring/getting-started/inbox.md) (barra degli strumenti) indica un numero incrementato di uno:

   ![Barra degli strumenti Notifica](/help/sites-cloud/authoring/assets/workflows-notifications.png)

* L&#39;oggetto viene inserito nelle notifiche della [Casella in entrata](/help/sites-cloud/authoring/getting-started/inbox.md):

   ![Notifiche nella inbox](/help/sites-cloud/authoring/assets/workflows-inbox.png)

* Quando utilizzi l&#39;Editor pagina, la barra di stato mostra:
   * Il nome dei flussi di lavoro applicati alla pagina, come ad esempio Richiedi attivazione.
   * Qualsiasi azione disponibile per l&#39;utente nella fase corrente del flusso di lavoro, per esempio: Completa, Delega, Visualizza dettagli.
   * Il numero di flussi di lavoro a cui è soggetta la pagina. Operazioni disponibili:
      * utilizzare la freccia sinistra/destra per navigare tra le informazioni di stato dei vari flussi di lavoro.
      * fare clic/toccare il numero totale per aprire un elenco a discesa di tutti i flussi di lavoro applicabili e quindi selezionare il flusso di lavoro che si desidera visualizzare nella barra di stato.
   ![Pagina con più flussi di lavoro](/help/sites-cloud/authoring/assets/workflows-multiple.png)

   >[!NOTE]
   >
   >The status bar is only visible to users with workflow privileges; for example, members of the `workflow-users` group.
   >
   >
   >Le azioni vengono visualizzate quando l&#39;utente è direttamente coinvolto nella fase corrente del flusso di lavoro.

* Quando la **Timeline** è aperta per la risorsa, verrà mostrato il passo del flusso di lavoro. Quando si fa clic o si tocca il banner di avviso, vengono anche visualizzate le azioni disponibili:

   ![Flusso di lavoro nella timeline](/help/sites-cloud/authoring/assets/workflows-timeline.png)

### Completamento di un passaggio partecipante {#completing-a-participant-step}

Quando si completa un elemento di lavoro, il flusso di lavoro procede al passaggio successivo.

Per questa azione è possibile indicare:

* **Passaggio successivo**: il passaggio successivo da compiere (è possibile selezionarlo da un elenco)
* **Commento**: se necessario

È possibile completare un passaggio partecipante a partire da:

* [Casella in entrata](#completing-a-participant-step-inbox)
* [Editor pagina](#completing-a-participant-step-page-editor)
* [Timeline](#completing-a-participant-step-timeline)
* When [opening a workflow item to view details](#opening-a-workflow-item-to-view-details-and-take-actions).

#### Completare un Passaggio partecipante: Casella in entrata {#completing-a-participant-step-inbox}

Utilizza la seguente procedura per completare l’elemento di lavoro:

1. Apri la **[Casella in entrata AEM](/help/sites-cloud/authoring/getting-started/inbox.md)**.
1. Seleziona l’elemento del flusso di lavoro su cui desideri intervenire (tocca o fai clic sull’anteprima).
1. Select **Complete** from the toolbar.
1. Si apre la finestra di dialogo **Completa elemento di lavoro**. Select the **Next Step** from the drop down selector and add a **Comment** if required.
1. Use **OK** to complete the step (or the **Cancel** to abort the action).

#### Completare un Passaggio partecipante: Editor pagina {#completing-a-participant-step-page-editor}

Utilizza la seguente procedura per completare l’elemento di lavoro:

1. Apri la [pagina da modificare](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing).
1. Select **Complete** from the status bar at the top.
1. Si apre la finestra di dialogo **Completa elemento di lavoro**. Select the **Next Step** from the drop down selector and add a **Comment** if required.
1. Use **OK** to complete the step (or the **Cancel** to abort the action).

#### Completare un Passaggio partecipante: Timeline {#completing-a-participant-step-timeline}

È possibile utilizzare la timelineper completare un passaggio e avanzare:

1. Select the required page and open **Timeline** (or open **Timeline** and select the page):

   ![Completamento di un passaggio](/help/sites-cloud/authoring/assets/workflows-timeline-completing.png)

1. Tocca o fai clic sul banner di avviso per visualizzare le azioni disponibili. Seleziona **Avanti**:

   ![Avanzamento del passaggio](/help/sites-cloud/authoring/assets/workflows-timeline-advance.png)

1. A seconda del flusso di lavoro, è possibile selezionare la fase successiva:

   ![Selezione del passaggio successivo](/help/sites-cloud/authoring/assets/workflows-next-step.png)

1. Seleziona **Avanti** per confermare l&#39;azione.

### Delega di un passaggio partecipante {#delegating-a-participant-step}

Se ti è stato assegnato un passaggio, ma per qualche motivo non ti è possibile procedere, puoi delegarlo a un altro utente o gruppo.

Gli utenti disponibili per la delega dipendono dal tipo di assegnatario:

* Se l’elemento di lavoro è stato assegnato a un gruppo, sono disponibili i membri del gruppo.
* Se l’elemento di lavoro è stato assegnato a un gruppo e poi è stato delegato a un utente, sono disponibili i membri del gruppo e il gruppo.
* Se l&#39;elemento di lavoro è stato assegnato a un singolo utente, l’elemento di lavoro non può essere delegato.

Per questa azione è possibile indicare:

* **Utente**: l&#39;utente a cui si vuole delegare. È possibile scegliere da un elenco
* **Commento**: se necessario

È possibile delegare un passaggio partecipante a partire da:

* [Casella in entrata](#delegating-a-participant-step-inbox)
* [Editor pagina](#delegating-a-participant-step-page-editor)
* [Timeline](#delegating-a-participant-step-timeline)
* When [opening a workflow item to view details](#opening-a-workflow-item-to-view-details-and-take-actions).

#### Delegare un Passaggio partecipante: Casella in entrata {#delegating-a-participant-step-inbox}

Segui la procedura seguente per delegare un elemento di lavoro:

1. Apri la **[Casella in entrata AEM](/help/sites-cloud/authoring/getting-started/inbox.md)**.
1. Seleziona l’elemento del flusso di lavoro su cui desideri intervenire (tocca o fai clic sull’anteprima).
1. Select **Delegate** from the toolbar.
1. Viene aperta una finestra di dialogo. Specify the **User** from the drop down selector (this can also be a group) and add a **Comment** if required.
1. Use **OK** to complete the step (or the **Cancel** to abort the action).

#### Delegare un Passaggio partecipante: Editor pagina {#delegating-a-participant-step-page-editor}

Segui la procedura seguente per delegare un elemento di lavoro:

1. Apri la [pagina da modificare](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing).
1. Select **Delegate** from the status bar at the top.
1. Viene aperta una finestra di dialogo. Specify the **User** from the drop down selector (this can also be a group) and add a **Comment** if required.
1. Use **OK** to complete the step (or the **Cancel** to abort the action).

#### Delegare un Passaggio partecipante: Timeline {#delegating-a-participant-step-timeline}

È anche possibile utilizzare la timeline per delegare e/o assegnare un passaggio:

1. Select the required page and open **Timeline** (or open **Timeline** and select the page).
1. Tocca o fai clic sul banner di avviso per visualizzare le azioni disponibili. Seleziona **Cambia assegnatario**:

   ![Passaggio delegato](/help/sites-cloud/authoring/assets/workflows-delegate.png)

1. Specifica un nuovo assegnatario:

   ![Modifica assegnatario](/help/sites-cloud/authoring/assets/workflows-assignee.png)

1. Select **Assign** to confirm the action.

### Tornare indietro di un passaggio {#performing-step-back-on-a-participant-step}

Se devi ripetere un passaggio o una serie di passaggi, puoi tornare indietro. Puoi quindi selezionare un passaggio precedente nel flusso di lavoro, per rielaborarlo. Il flusso di lavoro torna al passaggio specificato e procede da tale punto.

Per questa azione è possibile indicare:

* **Passaggio precedente:** il passaggio da cui si vuole ripartire. È possibile selezionarlo da un elenco.
* **Commento**: se necessario

È possibile eseguire un passo indietro su un passaggio partecipante a partire da:

* [Casella in entrata](#performing-step-back-on-a-participant-step-inbox)
* [Editor pagina](#performing-step-back-on-a-participant-step-page-editor)
* [Timeline](#performing-step-back-on-a-participant-step-timeline)
* When [opening a workflow item to view details](#opening-a-workflow-item-to-view-details-and-take-actions).

#### Eseguire un passo indietro su un Passaggio partecipante: Casella in entrata {#performing-step-back-on-a-participant-step-inbox}

Utilizza la seguente procedura per fare un passo indietro:

1. Apri la **[Casella in entrata AEM](/help/sites-cloud/authoring/getting-started/inbox.md)**.
1. Seleziona l’elemento del flusso di lavoro su cui desideri intervenire (tocca o fai clic sull’anteprima).
1. Select **Step Back** to open the dialog.
1. Specify the **Previous Step** and add a **Comment** if required.
1. Use **OK** to complete the step (or the **Cancel** to abort the action).

#### Eseguire un passo indietro su un Passaggio partecipante: Editor pagina {#performing-step-back-on-a-participant-step-page-editor}

Utilizza la seguente procedura per fare un passo indietro:

1. Apri la [pagina da modificare](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing).
1. Select **Step Back** from the status bar at the top.
1. Specify the **Previous Step** and add a **Comment** if required.
1. Use **OK** to complete the step (or the **Cancel** to abort the action).

#### Eseguire un passo indietro su un Passaggio partecipante: Timeline {#performing-step-back-on-a-participant-step-timeline}

È anche possibile utilizzare la timeline per tornare a un passaggio precedente:

1. Select the required page and open **Timeline** (or open **Timeline** and select the page).
1. Tocca o fai clic sul banner di avviso per visualizzare le azioni disponibili. Seleziona **Ripristina versione precedente**:

   ![Ripristino di un passaggio](/help/sites-cloud/authoring/assets/workflows-roll-back.png)

1. Specifica il passaggio precedente a cui il flusso di lavoro deve tornare:

   ![Specificare il passaggio](/help/sites-cloud/authoring/assets/workflows-roll-back-step.png)

1. Select **Roll back** to confirm the action.

### Aprire un elemento del flusso di lavoro per visualizzare i dettagli (e Intraprendere Azioni) {#opening-a-workflow-item-to-view-details-and-take-actions}

Visualizzare i dettagli dell&#39;elemento del flusso di lavoro e intraprendere le azioni appropriate.

I dettagli del flusso di lavoro vengono visualizzati in schede e le relative azioni appropriate sono disponibili nella barra degli strumenti:

* Scheda **ELEMENTO DI LAVORO:**

   Scheda ![ELEMENTO DI LAVORO](/help/sites-cloud/authoring/assets/workflows-work-item.png)

* **scheda INFORMAZIONI** FLUSSO DI LAVORO:

   ![scheda WORKFLOW](/help/sites-cloud/authoring/assets/workflows-workflow-info.png)

   Se per il modello sono stati configurati gli Stadi del Flusso di lavoro, è possibile visualizzare lo stato di avanzamento in base a questi: <!--If [Workflow Stages](/help/sites-developing/workflows.md#workflow-stages) have been configured for the model, you can view the progress according to these:-->

   ![Fasi del flusso di lavoro](/help/sites-cloud/authoring/assets/workflows-workflow-stages.png)

* **Scheda COMMENTI** :

   ![Scheda COMMENTI](/help/sites-cloud/authoring/assets/workflows-comments.png)

È possibile aprire i dettagli dell&#39;elemento di lavoro in uno a partire da:

* [Casella in entrata](#performing-step-back-on-a-participant-step-inbox)
* [Editor pagina](#performing-step-back-on-a-participant-step-page-editor)

#### Aprire dei dettagli del flusso di lavoro: Casella in entrata {#opening-workflow-details-inbox}

Per aprire un elemento del flusso di lavoro e visualizzare i dettagli:

1. Apri la **[Casella in entrata AEM](/help/sites-cloud/authoring/getting-started/inbox.md)**.
1. Seleziona l’elemento del flusso di lavoro su cui desideri intervenire (tocca o fai clic sull’anteprima).
1. Select **Open** to open the information tabs.
1. Se necessario, seleziona l’azione appropriata, inserisci tutte le informazioni richieste e conferma con **OK** (o **Annulla**).
1. Use **Save** or **Cancel** to exit.

#### Apertura dei dettagli del flusso di lavoro: Editor pagina {#opening-workflow-details-page-editor}

Per aprire un elemento del flusso di lavoro e visualizzare i dettagli:

1. Apri la [pagina da modificare](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#opening-a-page-for-editing).
1. Select **View Details** from the status bar to open the information tabs.
1. Se necessario, seleziona l’azione appropriata, inserisci tutte le informazioni richieste e conferma con **OK** (o **Annulla**).
1. Use **Save** or **Cancel** to exit.

### Visualizzare il Payload flusso di lavoro (Risorse Multiple) {#viewing-the-workflow-payload-multiple-resources}

È possibile visualizzare i dettagli del carico utile associato al singolo flusso di lavoro. All&#39;inizio vengono visualizzate le risorse nel pacchetto. È possibile, poi, scorrere per visualizzare le singole pagine.

Per visualizzare il carico utile e le risorse del singolo flusso di lavoro:

1. Apri la **[Casella in entrata AEM](/help/sites-cloud/authoring/getting-started/inbox.md)**.
1. Seleziona l’elemento del flusso di lavoro su cui desideri intervenire (tocca o fai clic sull’anteprima).
1. Select **View Payload** from the toolbar to open the dialog.
   * Poiché un pacchetto di flusso di lavoro è semplicemente un insieme di puntatori ai percorsi all&#39;interno della libreria, è possibile aggiungere, rimuovere e modificare le voci qui indicate per regolare i riferimenti del pacchetto del flusso di lavoro. Usa il componente **Definizione risorsa** per aggiungere nuove voci.
1. I link possono essere usati per aprire le singole pagine.
