---
title: Pubblicazione delle pagine
description: Come pubblicare e annullare la pubblicazione di pagine con AEM
translation-type: tm+mt
source-git-commit: e88a814a901d7fa0da2675fa6017c66d61a73445

---


# Pubblicazione delle pagine {#publishing-pages}

Dopo aver creato e rivisto i contenuti nell’ambiente di authoring, [devi renderli disponibili nel sito Web pubblico](/help/sites-cloud/authoring/getting-started/concepts.md) (l’ambiente di pubblicazione).

Questa operazione è denominata pubblicazione della pagina. Quando si rimuove una pagina dall’ambiente di pubblicazione, si parla di annullamento della pubblicazione. Quando si pubblica e si annulla la pubblicazione di una pagina, quest’ultima rimane disponibile nell’ambiente di authoring per ulteriori modifiche, finché non decidi di eliminarla.

Potete pubblicare/annullare la pubblicazione di una pagina immediatamente o in una data/ora futura predefinita.

## Terminologia {#terminology}

Quando lavorate con AEM, potrebbero verificarsi termini diversi relativi alla pubblicazione.

* **Pubblicare / Annullare la pubblicazione**
   * Termini principali per le azioni che rendono o meno i contenuti disponibili al pubblico nell’ambiente di pubblicazione.
   * Termini utilizzati nella documentazione di AEM.
* **Attiva/Disattiva**
   * Sinonimi di pubblicare/annullare la pubblicazione.
   * Questi termini sono stati utilizzati nelle versioni precedenti di AEM.
* **Replicare / Replica**
   * Questi sono i termini tecnici che descrivono lo spostamento di dati (ad esempio contenuto di una pagina, file, codice, commenti degli utenti) da un ambiente all’altro quando si pubblica una pagina.
   * Questi termini vengono utilizzati principalmente dagli sviluppatori.

## Pubblicazione delle pagine {#publishing-pages-1}

A seconda della tua posizione, puoi pubblicare:

* [Dall’Editor pagina](#publishing-from-the-editor)
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

1. Select the **Page Information** icon to open the menu and then the **Publish Page** option.

   ![Pubblicazione di una pagina tramite le opzioni di pagina](/help/sites-cloud/authoring/assets/publishing-page-options.png)

1. A seconda che la pagina includa o meno riferimenti che devono essere pubblicati:

   * La pagina verrà pubblicata direttamente, se non sono presenti riferimenti da pubblicare.
   * Se la pagina include riferimenti da pubblicare, questi saranno elencati nella procedura guidata di **Pubblicazione**, dove è possibile:
      * Specify which of the assets/tags/etc. you want to publish together with the page, then use **Publish** to complete the process.
      * utilizzare **Annulla** per annullare l’azione.
   ![Pubblicazione di riferimenti con la pagina](/help/sites-cloud/authoring/assets/publishing-references.png)

1. Selecting **Publish** will replicate the page to the publish environment. Nell’editor pagina verrà visualizzato un banner informativo che conferma l’azione di pubblicazione.

   ![Banner informazioni stato di pubblicazione](/help/sites-cloud/authoring/assets/publishing-info.png)

   Quando visualizzi la stessa pagina nella console, lo stato aggiornato della pubblicazione è visibile.

   ![Stato di pubblicazione delle pagine nella vista a colonne nella console Siti](/help/sites-cloud/authoring/assets/publishing-status-console-column.png)

>[!NOTE]
>
>La pubblicazione dall’editor è superficiale, ovvero vengono pubblicate solo le pagine selezionate e non le pagine figlie.

### Pubblicazione dalla console {#publishing-from-the-console}

Nella console Sites vi sono due opzioni di modifica:

* [Pubblicazione rapida](#quick-publish)
* [Gestisci pubblicazione](#manage-publication)

#### Pubblicazione rapida {#quick-publish}

**Pubblicazione** rapida si riferisce a casi semplici e pubblica immediatamente le pagine selezionate senza ulteriore interazione. Anche eventuali riferimenti non pubblicati verranno pubblicati automaticamente.

Per pubblicare una pagina con Pubblicazione rapida:

1. Select the page or pages in the sites console and click on the **Quick Publish** button.

   ![Selezione delle pagine per la pubblicazione](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. In the Quick Publish dialog, confirm the publication by clicking on **Publish** or cancel by clicking on **Cancel**. Tieni presente che verranno pubblicati automaticamente anche eventuali riferimenti non pubblicati.

   ![Conferma rapida pubblicazione](/help/sites-cloud/authoring/assets/publishing-quick-publish.png)

1. Quando la pagina viene pubblicata, viene visualizzato un avviso di conferma della pubblicazione.

>[!NOTE]
>
>La pubblicazione rapida è “superficiale”, ovvero vengono pubblicate solo le pagine selezionate e non le relative pagine figlie.

#### Gestisci pubblicazione {#manage-publication}

**Gestisci pubblicazione** offre più opzioni rispetto alla pubblicazione rapida, consentendo l’inclusione di pagine figlie, la personalizzazione dei riferimenti e l’avvio di eventuali flussi di lavoro applicabili, nonché l’opzione di pubblicazione in un secondo momento.

Per pubblicare una pagina o annullarne la pubblicazione tramite Gestisci pubblicazione:

1. Select the page or pages in the sites console and click on the **Manage Publication** button.

   ![Selezione delle pagine per la pubblicazione](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. The **Manage Publication** wizard starts. The first step, **Options**, allows you to:

   * Scegliere di pubblicare le pagine selezionate o annullarne la pubblicazione.
   * Scegliere di eseguire l’azione immediatamente o in un secondo momento.
   Con Pubblica più tardi viene avviato un flusso di lavoro per attivare le pagine selezionate alla data e all’ora specificate. In modo analogo, se si sceglie di annullare la pubblicazione in un secondo momento, verrà attivato un flusso di lavoro per disattivare le pagine selezionate alla data e all’ora specificate.

   Per annullare un’attività di pubblicazione, anche programmata per un momento successivo, accedete alla console Flusso di lavoro e interrompete il flusso di lavoro corrispondente. <!--If you want to cancel a publish/unpublish later, go to the [Workflow Console](/help/sites-administering/workflows.md) to terminate the corresponding workflow.-->

   ![Gestisci opzioni pubblicazione](/help/sites-cloud/authoring/assets/publishing-manage-publication-options.png)

   Fai clic su **Avanti** per continuare.

1. In the next step of the Manage Publication wizard, **Scope**, you can define the scope of the publication/un-publication such as including to include child pages and/or including references.

   ![Gestisci ambito pubblicazione](/help/sites-cloud/authoring/assets/publishing-manage-publication-scope.png)

   You can use the **Add Content** button to add additional pages to the list of pages to be published in case you neglected to select one before starting the Manage Publication wizard.

   Facendo clic sul pulsante Aggiungi contenuto si avvia il [browser percorsi](/help/sites-cloud/authoring/fundamentals/environment-tools.md#path-browser), che consente di selezionare contenuti.

   Select the required pages and then click **Select** to add the content to the wizard or **Cancel **to cancel the selection and return to the wizard.

   Nella procedura guidata puoi selezionare un elemento nell’elenco per configurare ulteriori opzioni, come:

   * Includere gli elementi figlio.
   * Rimuoverlo dalla selezione.
   * Gestire i relativi riferimenti pubblicati.
   ![Gestisci pubblicazione selezione pagine](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   Clicking **Include Children** opens a dialogue allowing you to:

   * Solo gli elementi figli di primo livello.
   * Solo pagine modificate.
   * Solo pagine già pubblicate.
   Click **Add** to add the children pages to the list of pages to be published or unpublished based on the selection options. Click **Cancel** to cancel the selection and return to the wizard.

   ![Gestisci pubblicazione inclusi gli elementi figlio](/help/sites-cloud/authoring/assets/publishing-include-children.png)

   Tornando alla procedura guidata vengono visualizzate le pagine aggiunte in base alle opzioni selezionate nella finestra di dialogo Includi elementi figlio.

   You can view and modify the references to be published or unpublished for a page by selecting it and then clicking the **Published References** button.

   ![Gestisci opzioni pubblicazione](/help/sites-cloud/authoring/assets/publishing-manage-publication-references.png)

   The **Published References** dialog displays the references for the selected content. Per impostazione predefinita, sono tutti selezionati e verranno pubblicati o ne verrà annullata la pubblicazione, ma potete deselezionare questa opzione per non includerli nell’azione.

   Click **Done** to save your changes or **Cancel** to cancel the selection and return to the wizard.

   Nella procedura guidata, la colonna **Riferimenti** verrà aggiornata per riflettere la selezione dei riferimenti da pubblicare o di cui annullare la pubblicazione.

   ![Gestisci pubblicazione selezione pagine](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

1. Click **Publish** to complete.

   Nella console Sites, un messaggio di notifica confermerà la pubblicazione.

1. If the published pages are associated with workflows, they may be shown in a final **Workflows** step of the publication wizard.

   >[!NOTE]
   >
   >The **Workflows** step will be shown based on what rights your user may or may not have. See the previous note on this page regarding publishing privileges as well as Managing Access to Workflows and [Applying Workflows to Pages](/help/sites-cloud/authoring/workflows/applying.md) for details.
   <!--
   >The **Workflows** step will be shown based on what rights your user may or may not have. See the previous note on this page regarding publishing privileges as well as [Managing Access to Workflows](/help/sites-administering/workflows-managing.md) and [Applying Workflows to Pages](/help/sites-cloud/authoring/workflows/applying.md) for details.
   -->

   Le risorse vengono raggruppate in base ai flussi di lavoro attivati e per ognuna sono disponibili opzioni per:

   * Definire il titolo del flusso di lavoro.
   * Keep the workflow package, provided that the workflow has multi-resource support. <!--Keep the workflow package, provided that the workflow has [multi-resource support](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support).-->
   * Definire un titolo del pacchetto del flusso di lavoro se è stata selezionata l’opzione per mantenere il pacchetto del flusso di lavoro.
   Click **Publish** or **Publish Later** to complete the publication.

## Annullamento della pubblicazione delle pagine {#unpublishing-pages}

L’annullamento della pubblicazione di una pagina ne effettua la rimozione dall’ambiente di pubblicazione e la pagina non sarà più disponibile per i lettori.

In a [manner similar to publishing](#publishing-pages), one or more pages can be unpublished:

* [Dall’Editor pagina](#unpublishing-from-the-editor)
* [Dalla console Sites](#unpublishing-from-the-console)

### Annullamento della pubblicazione dall’editor {#unpublishing-from-the-editor}

Durante la modifica di una pagina, se desideri annullarne la pubblicazione seleziona **Annulla pubblicazione pagina** nel menu **Informazioni pagina**. La procedura è simile a quella di [pubblicazione della pagina](#publishing-from-the-editor).

### Annullamento della pubblicazione dalla console {#unpublishing-from-the-console}

Puoi utilizzare [l’opzione Gestisci pubblicazione per eseguire la pubblicazione](#manage-publication), ma anche per annullarla.

1. Select the page or pages in the sites console and click on the **Manage Publication** button.
1. The **Manage Publication** wizard starts. In the first step, **Options**, select to **Unpublish** instead of the default option of **Publish**.

   ![Annullamento della pubblicazione](/help/sites-cloud/authoring/assets/publishing-unpublish.png)

   Con Pubblica più tardi viene avviato un flusso di lavoro per pubblicare tale versione della pagina alla data e all’ora specificate. In modo analogo, se si sceglie di annullare la pubblicazione in un secondo momento, verrà attivato un flusso di lavoro per annullare la pubblicazione delle pagine selezionate alla data e all’ora specificate.

   Per annullare un’attività di pubblicazione, anche programmata per un momento successivo, accedete alla console Flusso di lavoro e interrompete il flusso di lavoro corrispondente. <!--If you want to cancel a publish/unpublish later, go to the [Workflow Console](/help/sites-administering/workflows.md) to terminate the corresponding workflow.-->

1. To complete the un-publication, continue through the wizard as you would to [publish the page](#manage-publication).

## Pubblicazione e annullamento della pubblicazione di una struttura {#publishing-and-unpublishing-a-tree}

Se hai inserito o aggiornato un numero considerevole di pagine di contenuto, tutte residenti sotto la stessa pagina principale, può essere più semplice pubblicare l’intera struttura con una singola azione.

Puoi utilizzare l’opzione [Gestisci pubblicazione](#manage-publication) sulla console Sites per eseguire questa operazione.

1. Nella console Sites, seleziona la pagina principale della struttura che desideri pubblicare o di cui desideri annullare la pubblicazione e seleziona **Gestisci pubblicazione**.
1. The **Manage Publication** wizard starts. Scegli se e quando eseguire o annullare la pubblicazione, quindi seleziona **Avanti** per continuare.
1. Nel passaggio **Ambito**, seleziona la pagina principale e seleziona **Includi elementi figlio**.

   ![Gestisci pubblicazione selezione pagine](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

1. In the **Include Children** dialogue, un-check the options:

   * Solo gli elementi figli di primo livello
   * Solo pagine già pubblicate
   Queste opzioni sono selezionate per impostazione predefinita, pertanto dovrai ricordarti di deselezionarle. Click **Add** to confirm and add the content to the publication/un-publication.

   ![Inclusione di elementi figlio durante l&#39;annullamento della pubblicazione](/help/sites-cloud/authoring/assets/publishing-tree-children.png)

1. La procedura guidata **Gestisci pubblicazione** elenca il contenuto della struttura a scopi di revisione. Puoi personalizzare ulteriormente la selezione aggiungendo ulteriori pagine o rimuovendo quelle selezionate.

   ![Gestisci opzioni pubblicazione](/help/sites-cloud/authoring/assets/publishing-tree-select.png)

   Remember that you can also review the references to be published via the **Published References** option.

1. [Continua a seguire normalmente](#manage-publication) la procedura guidata Gestisci pubblicazione per completare la pubblicazione o annullare la pubblicazione della struttura.

## Determinazione dello stato di pubblicazione {#determining-publication-status}

È possibile determinare lo stato di pubblicazione di una pagina:

* Nelle [informazioni generali sulla risorsa nella console Sites](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) 

   ![Stato della pubblicazione nella vista a schede](/help/sites-cloud/authoring/assets/publishing-status-console-card.png)

   Lo stato di pubblicazione è indicato nelle viste [a schede](/help/sites-cloud/authoring/getting-started/basic-handling.md#card-view), [a colonne](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view) e [a elenco](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view) nella console Sites.

* In the [timeline](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline)

   ![Stato della pubblicazione nella visualizzazione timeline](/help/sites-cloud/authoring/assets/publishing-status-timeline.png)

* In the [Page Information menu](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) when editing a page

   ![Stato della pubblicazione nel menu Informazioni pagina](/help/sites-cloud/authoring/assets/publishing-status-page-information.png)
