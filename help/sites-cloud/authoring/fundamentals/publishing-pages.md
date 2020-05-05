---
title: Pubblicazione delle pagine
description: Come pubblicare e annullare la pubblicazione di pagine con AEM
translation-type: ht
source-git-commit: f04dd39a5a22f44f976f2e473689780099f10f9a

---


# Pubblicazione delle pagine {#publishing-pages}

Dopo aver creato e rivisto i contenuti nell’ambiente di authoring, [devi renderli disponibili nel sito Web pubblico](/help/sites-cloud/authoring/getting-started/concepts.md) (l’ambiente di pubblicazione).

Questa operazione è denominata pubblicazione della pagina. Quando si rimuove una pagina dall’ambiente di pubblicazione, si parla di annullamento della pubblicazione. Quando si pubblica e si annulla la pubblicazione di una pagina, quest’ultima rimane disponibile nell’ambiente di authoring per ulteriori modifiche, finché non decidi di eliminarla.

Puoi anche pubblicare o annullare la pubblicazione di una pagina immediatamente o in una data/ora futura predefinita.

## Terminologia {#terminology}

Quando lavori con AEM, potresti notare diversi termini relativi alla pubblicazione.

* **Pubblicare/Annullare la pubblicazione**
   * Termini principali per le azioni che consentono di rendere o meno i contenuti disponibili al pubblico nell’ambiente di pubblicazione.
   * Questi termini sono utilizzati nella documentazione di AEM.
* **Attivare/Disattivare**
   * Sinonimi di pubblicare/annullare la pubblicazione.
   * Questi termini sono stati utilizzati nelle versioni precedenti di AEM.
* **Replicare/Replica**
   * Questi sono i termini tecnici che descrivono lo spostamento di dati da un ambiente all’altro al momento di pubblicare una pagina, ad esempio: contenuto di una pagina, file, codice e commenti degli utenti.
   * Questi termini vengono utilizzati principalmente dagli sviluppatori.

## Pubblicazione delle pagine {#publishing-pages-1}

A seconda della tua posizione, puoi pubblicare:

* [Dall’editor di pagine](#publishing-from-the-editor)
* [Dalla console Sites](#publishing-from-the-console)

>[!NOTE]
>
>Se non disponi delle autorizzazioni necessarie per pubblicare una specifica pagina:
>
>* Viene avviato un flusso di lavoro per comunicare al soggetto adeguato la tua richiesta di pubblicazione.
>* Questo flusso di lavoro potrebbe essere stato personalizzato dal team di sviluppo.
>* Verrà visualizzato brevemente un messaggio che informa che il flusso di lavoro è stato attivato.


<!--
>* This [workflow may have been customized](/help/sites-developing/workflows-models.md#main-pars-procedure-6fe6) by your development team.
>* A message will be displayed briefly to notify you that the workflow was triggered.
-->

### Pubblicazione dall’editor {#publishing-from-the-editor}

Se stai modificando una pagina, puoi pubblicarla direttamente dall’editor.

1. Seleziona l’icona **Informazioni pagina** per aprire il menu, quindi l’opzione **Pubblica pagina**.

   ![Pubblicazione di una pagina tramite le opzioni di pagina](/help/sites-cloud/authoring/assets/publishing-page-options.png)

1. A seconda che la pagina includa o meno riferimenti che devono essere pubblicati:

   * La pagina verrà pubblicata direttamente, se non sono presenti riferimenti da pubblicare.
   * Se la pagina include riferimenti da pubblicare, questi saranno elencati nella procedura guidata di **Pubblicazione**, dove è possibile:
      * Specifica le risorse, i tag ecc. da pubblicare insieme alla pagina, quindi seleziona **Pubblica** per completare il processo.
      * Seleziona **Annulla** per annullare l’azione.
   ![Pubblicazione di riferimenti alla pagina](/help/sites-cloud/authoring/assets/publishing-references.png)

1. Se selezioni l’opzione **Pubblica**, la pagina verrà replicata nell’ambiente di pubblicazione. Nell’editor di pagine verrà visualizzato un banner informativo che conferma l’azione di pubblicazione.

   ![Banner informazioni stato di pubblicazione](/help/sites-cloud/authoring/assets/publishing-info.png)

   Quando visualizzi la stessa pagina nella console, lo stato aggiornato della pubblicazione è visibile.

   ![Stato di pubblicazione della pagina nella vista a colonne della console Sites](/help/sites-cloud/authoring/assets/publishing-status-console-column.png)

>[!NOTE]
>
>La pubblicazione dall’editor è “superficiale”, ovvero vengono pubblicate solo le pagine selezionate e non le relative pagine figlie.

### Pubblicazione dalla console {#publishing-from-the-console}

Nella console Sites vi sono due opzioni di modifica:

* [Pubblicazione rapida](#quick-publish)
* [Gestisci pubblicazione](#manage-publication)

#### Pubblicazione rapida  {#quick-publish}

**Pubblicazione rapida** si usa in casi semplici; le pagine selezionate vengono pubblicate immediatamente senza ulteriore interazione. Anche eventuali riferimenti non pubblicati verranno pubblicati automaticamente.

Per pubblicare una pagina con Pubblicazione rapida:

1. Seleziona le pagine desiderate nella console Sites e fai clic sul pulsante **Pubblicazione rapida**.

   ![Selezione delle pagine per la pubblicazione](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. Nella finestra di dialogo Pubblicazione rapida, conferma la pubblicazione facendo clic su **Pubblica** o annulla la pubblicazione facendo clic su **Annulla**. Tieni presente che verranno pubblicati automaticamente anche eventuali riferimenti non pubblicati.

   ![Conferma Pubblicazione rapida](/help/sites-cloud/authoring/assets/publishing-quick-publish.png)

1. Quando la pagina viene pubblicata, viene visualizzato un avviso di conferma della pubblicazione.

>[!NOTE]
>
>La pubblicazione rapida è “superficiale”, ovvero vengono pubblicate solo le pagine selezionate e non le relative pagine figlie.

#### Gestisci pubblicazione  {#manage-publication}

**Gestisci pubblicazione** offre più opzioni rispetto alla pubblicazione rapida e consente di includere pagine figlie, personalizzare i riferimenti e avviare tutti i flussi di lavoro applicabili; consente inoltre di pubblicare la pagina in un secondo momento.

Per pubblicare una pagina o annullarne la pubblicazione tramite Gestisci pubblicazione:

1. Seleziona le pagine desiderate nella console Sites e fai clic sul pulsante **Gestisci pubblicazione**.

   ![Selezione delle pagine per la pubblicazione](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. Viene avviata la procedura guidata **Gestisci pubblicazione**. Il primo passaggio, **Opzioni**, consente di:

   * Scegliere di pubblicare le pagine selezionate o annullarne la pubblicazione.
   * Scegliere di eseguire l’azione immediatamente o in un secondo momento.
   Con Pubblica più tardi viene avviato un flusso di lavoro per attivare le pagine selezionate alla data e all’ora specificate. In modo analogo, se si sceglie di annullare la pubblicazione in un secondo momento, verrà attivato un flusso di lavoro per disattivare le pagine selezionate alla data e all’ora specificate.

   Per annullare un’attività di pubblicazione, anche programmata per un momento successivo, accedi alla console Flusso di lavoro e interrompi il flusso di lavoro corrispondente. <!--If you want to cancel a publish/unpublish later, go to the [Workflow Console](/help/sites-administering/workflows.md) to terminate the corresponding workflow.-->

   ![Opzioni di Gestisci pubblicazione](/help/sites-cloud/authoring/assets/publishing-manage-publication-options.png)

   Fai clic su **Avanti** per continuare.

1. Nel passaggio successivo della procedura guidata Gestisci pubblicazione, **Ambito**, puoi definire l’ambito della pubblicazione o dell’annullamento della pubblicazione, ad esempio decidendo se includere pagine figlie e/o riferimenti.

   ![Ambito di Gestisci pubblicazione](/help/sites-cloud/authoring/assets/publishing-manage-publication-scope.png)

   Puoi usare il pulsante **Aggiungi contenuto** per aggiungere ulteriori pagine all’elenco delle pagine da pubblicare, nel caso in cui ti sia dimenticato di selezionarne una prima di avviare la procedura guidata Gestisci pubblicazione.

   Facendo clic sul pulsante Aggiungi contenuto si avvia il [browser percorsi](/help/sites-cloud/authoring/fundamentals/environment-tools.md#path-browser), che consente di selezionare contenuti.

   Seleziona le pagine desiderate e fai clic su **Seleziona** per aggiungere contenuti alla procedura guidata o su **Annulla** per annullare la selezione e tornare alla procedura guidata.

   Nella procedura guidata puoi selezionare un elemento nell’elenco per configurare ulteriori opzioni, come:

   * Includere gli elementi figlio.
   * Rimuoverlo dalla selezione.
   * Gestire i relativi riferimenti pubblicati.
   ![Selezione pagine di Gestisci pubblicazione](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   Facendo clic su **Includi elementi figlio** viene visualizzata una finestra di dialogo che consente di includere:

   * Solo gli elementi figli di primo livello.
   * Solo pagine modificate.
   * Solo pagine già pubblicate.
   Fai clic su **Aggiungi** per aggiungere le pagine figlio nell’elenco delle pagine da pubblicare o di cui annullare la pubblicazione, in base alle opzioni selezionate. Fai clic su **Annulla** per annullare la selezione e tornare alla procedura guidata.

   ![Inclusione di elementi figlio in Gestisci pubblicazione](/help/sites-cloud/authoring/assets/publishing-include-children.png)

   Tornando alla procedura guidata vengono visualizzate le pagine aggiunte in base alle opzioni selezionate nella finestra di dialogo Includi elementi figlio.

   Puoi visualizzare e modificare i riferimenti da pubblicare o di cui annullare la pubblicazione per una pagina selezionandola e facendo clic sul pulsante **Riferimenti pubblicati**.

   ![Opzioni di Gestisci pubblicazione](/help/sites-cloud/authoring/assets/publishing-manage-publication-references.png)

   La finestra di dialogo **Riferimenti pubblicati** visualizza i riferimenti per il contenuto selezionato. Per impostazione predefinita sono tutti selezionati e verranno pubblicati o ne verrà annullata la pubblicazione, ma puoi deselezionarli in modo da non includerli nell’azione.

   Fai clic su **Fine** per salvare le modifiche o su **Annulla** per annullare la selezione e tornare alla procedura guidata.

   Nella procedura guidata, la colonna **Riferimenti** verrà aggiornata per riflettere la selezione dei riferimenti da pubblicare o di cui annullare la pubblicazione.

   ![Selezione pagine di Gestisci pubblicazione](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

1. Fai clic su **Pubblica** per completare l’azione.

   Nella console Sites, un messaggio di notifica confermerà la pubblicazione.

1. Se le pagine pubblicate sono associate a flussi di lavoro, potrebbero essere visualizzati in un passaggio finale **Flussi di lavoro** della procedura guidata di pubblicazione.

   >[!NOTE]
   >
   >Il passaggio **Flussi di lavoro** verrà visualizzato in base ai diritti di cui dispone l’utente. Vedi la nota precedente su questa pagina per quanto riguarda i privilegi di pubblicazione, nonché gli argomenti Gestione dell’accesso ai flussi di lavoro e [Applicazione dei flussi di lavoro alle pagine](/help/sites-cloud/authoring/workflows/applying.md) per ulteriori dettagli.
   <!--
   >The **Workflows** step will be shown based on what rights your user may or may not have. See the previous note on this page regarding publishing privileges as well as [Managing Access to Workflows](/help/sites-administering/workflows-managing.md) and [Applying Workflows to Pages](/help/sites-cloud/authoring/workflows/applying.md) for details.
   -->

   Le risorse vengono raggruppate in base ai flussi di lavoro attivati e per ognuna sono disponibili opzioni per:

   * Definire il titolo del flusso di lavoro.
   * Mantenere il pacchetto del flusso di lavoro, a condizione che il flusso di lavoro sia dotato di supporto per più risorse.
   <!--Keep the workflow package, provided that the workflow has [multi-resource support](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support).
    -->

   * Definire un titolo del pacchetto del flusso di lavoro se è stata selezionata l’opzione per mantenere il pacchetto del flusso di lavoro.
   Fai clic su **Pubblica** o **Pubblica più tardi** per completare la pubblicazione.

## Annullamento della pubblicazione delle pagine {#unpublishing-pages}

L’annullamento della pubblicazione di una pagina ne effettua la rimozione dall’ambiente di pubblicazione e la pagina non sarà più disponibile per i lettori.

Con una procedura [simile alla pubblicazione](#publishing-pages), è possibile annullare la pubblicazione di una o più pagine:

* [Dall’editor di pagine](#unpublishing-from-the-editor)
* [Dalla console Sites](#unpublishing-from-the-console)

### Annullamento della pubblicazione dall’editor  {#unpublishing-from-the-editor}

Durante la modifica di una pagina, se desideri annullarne la pubblicazione seleziona **Annulla pubblicazione pagina** nel menu **Informazioni pagina**. La procedura è simile a quella di [pubblicazione della pagina](#publishing-from-the-editor).

### Annullamento della pubblicazione dalla console  {#unpublishing-from-the-console}

Puoi utilizzare [l’opzione Gestisci pubblicazione per eseguire la pubblicazione](#manage-publication), ma anche per annullarla.

1. Seleziona le pagine desiderate nella console Sites e fai clic sul pulsante **Gestisci pubblicazione**.
1. Viene avviata la procedura guidata **Gestisci pubblicazione**. Nel primo passaggio, **Opzioni**, seleziona **Annulla pubblicazione** anziché l’opzione predefinita **Pubblica**.

   ![Annullamento della pubblicazione](/help/sites-cloud/authoring/assets/publishing-unpublish.png)

   Con Pubblica più tardi viene avviato un flusso di lavoro per pubblicare tale versione della pagina alla data e all’ora specificate. In modo analogo, se si sceglie di annullare la pubblicazione in un secondo momento, verrà attivato un flusso di lavoro per annullare la pubblicazione delle pagine selezionate alla data e all’ora specificate.

   Per annullare un’attività di pubblicazione, anche programmata per un momento successivo, accedi alla console Flusso di lavoro e interrompi il flusso di lavoro corrispondente. <!--If you want to cancel a publish/unpublish later, go to the [Workflow Console](/help/sites-administering/workflows.md) to terminate the corresponding workflow.-->

1. Per completare l’annullamento della pubblicazione, continua a seguire la procedura guidata come faresti per [pubblicare la pagina](#manage-publication).

## Pubblicazione e annullamento della pubblicazione di una struttura {#publishing-and-unpublishing-a-tree}

Se hai inserito o aggiornato un numero considerevole di pagine di contenuto, tutte residenti sotto la stessa pagina principale, può essere più semplice pubblicare l’intera struttura con una singola azione.

Puoi utilizzare l’opzione [Gestisci pubblicazione](#manage-publication) sulla console Sites per eseguire questa operazione.

1. Nella console Sites, seleziona la pagina principale della struttura che desideri pubblicare o di cui desideri annullare la pubblicazione e seleziona **Gestisci pubblicazione**.
1. Viene avviata la procedura guidata **Gestisci pubblicazione**. Scegli se e quando eseguire o annullare la pubblicazione, quindi seleziona **Avanti** per continuare.
1. Nel passaggio **Ambito**, seleziona la pagina principale e seleziona **Includi elementi figlio**.

   ![Selezione pagine di Gestisci pubblicazione](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

1. Nella finestra di dialogo **Includi elementi figlio**, deseleziona le opzioni:

   * Solo gli elementi figli di primo livello
   * Solo pagine già pubblicate
   Queste opzioni sono selezionate per impostazione predefinita, pertanto dovrai ricordarti di deselezionarle. Fai clic su **Aggiungi** per confermare e aggiungere il contenuto alla pubblicazione o all’annullamento della pubblicazione.

   ![Inclusione di elementi figlio durante l’annullamento della pubblicazione](/help/sites-cloud/authoring/assets/publishing-tree-children.png)

1. La procedura guidata **Gestisci pubblicazione** elenca il contenuto della struttura a scopi di revisione. Puoi personalizzare ulteriormente la selezione aggiungendo ulteriori pagine o rimuovendo quelle selezionate.

   ![Opzioni di Gestisci pubblicazione](/help/sites-cloud/authoring/assets/publishing-tree-select.png)

   Non dimenticare che è anche possibile esaminare i riferimenti da pubblicare tramite l’opzione **Riferimenti pubblicati**.

1. [Continua a seguire normalmente la procedura guidata Gestisci pubblicazione](#manage-publication) per completare la pubblicazione o annullare la pubblicazione della struttura.

## Determinazione dello stato di pubblicazione {#determining-publication-status}

Puoi determinare lo stato di pubblicazione di una pagina:

* Nelle [informazioni generali sulla risorsa nella console Sites](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)

   ![Stato della pubblicazione nella vista a schede](/help/sites-cloud/authoring/assets/publishing-status-console-card.png)

   Lo stato di pubblicazione è indicato nelle viste [a schede](/help/sites-cloud/authoring/getting-started/basic-handling.md#card-view), [a colonne](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view) e [a elenco](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view) nella console Sites.

* Nella [timeline](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)

   ![Stato della pubblicazione nella visualizzazione timeline](/help/sites-cloud/authoring/assets/publishing-status-timeline.png)

* Nel menu [Informazioni pagina](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) durante la modifica di una pagina

   ![Stato della pubblicazione nel menu Informazioni pagina](/help/sites-cloud/authoring/assets/publishing-status-page-information.png)
