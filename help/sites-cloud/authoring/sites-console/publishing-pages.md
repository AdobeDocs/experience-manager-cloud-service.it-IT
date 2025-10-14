---
title: Pubblicazione di pagine dalla console Sites
description: Scopri come pubblicare e annullare la pubblicazione delle pagine utilizzando la console Sites.
exl-id: 89f2363c-7922-4ca5-92cb-cbee6a393ee3
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 5ad91a32d705ef61e8b9799bf7fb1e136bb8bfa0
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 73%

---


# Pubblicazione di pagine dalla console Sites {#publishing-pages}

Dopo aver creato e rivisto i contenuti nell’ambiente di authoring, l’obiettivo è [renderli disponibili nel sito web pubblico](/help/sites-cloud/authoring/author-publish.md) (l’ambiente di pubblicazione).

Questa operazione è denominata pubblicazione della pagina. Quando si rimuove una pagina dall’ambiente di pubblicazione, si parla di annullamento della pubblicazione. Durante la pubblicazione e l’annullamento della pubblicazione, la pagina rimane disponibile nell’ambiente di authoring per ulteriori modifiche fino a quando non viene eliminata.

È possibile utilizzare la console [**Sites**](/help/sites-cloud/authoring/sites-console/introduction.md) per pubblicare/annullare la pubblicazione di una pagina immediatamente o in una data/ora futura predefinita.

>[!TIP]
>
>Puoi pubblicare da posizioni diverse dalla console Sites.
>
>* [Dall&#39;Editor pagina](/help/sites-cloud/authoring/page-editor/publishing.md)
>* [Dall&#39;editor universale](/help/sites-cloud/authoring/universal-editor/publishing.md)
>* [Dalla console o dall&#39;editor frammenti di esperienza](/help/sites-cloud/authoring/fragments/experience-fragments.md)
>
>La pubblicazione da queste posizioni offre diverse opzioni, ma segue procedure simili e idee generali descritte qui.

## Terminologia {#terminology}

È possibile riscontrare termini diversi relativi alla pubblicazione mentre si lavora con Adobe Experience Manager (AEM) as a Cloud Service.

* **Pubblicare/Annullare la pubblicazione**
   * Termini principali per le azioni che consentono di rendere o meno i contenuti disponibili al pubblico negli ambienti di pubblicazione e/o anteprima.
   * Questi termini sono utilizzati nella documentazione di AEM.
* **Attivare/Disattivare**
   * Sinonimi di pubblicare/annullare la pubblicazione.
   * Questi termini sono stati utilizzati nelle versioni precedenti di AEM.
* **Replicare/Replica**
   * Questi sono i termini tecnici che descrivono lo spostamento di dati (ad esempio contenuto di una pagina, file, codice e commenti degli utenti) da un servizio all’altro al momento della pubblicazione di una pagina (ad esempio, dall’authoring all’anteprima).
   * Questi termini vengono utilizzati principalmente dagli sviluppatori.

>[!NOTE]
>
>Se non disponi dei privilegi necessari per la pubblicazione di una pagina specifica:
>
>* Viene avviato un flusso di lavoro per comunicare al soggetto adeguato la tua richiesta di pubblicazione.
>* Questo flusso di lavoro potrebbe essere stato personalizzato dal team di sviluppo.
>* Viene visualizzato brevemente un messaggio che informa che il flusso di lavoro è stato attivato.

>[!NOTE]
>
>Se vuoi mantenere l&#39;ordine delle pagine devi utilizzare [Gestisci pubblicazione](#manage-publication) per pubblicare la pagina padre insieme alle pagine figlie in un&#39;unica azione.
>
>L’ordine delle pagine non è garantito:
>
>* Se vengono selezionate per la pubblicazione solo le pagine figlie (in quanto le informazioni sull’ordine si trovano nella pagina padre)
>* Se le pagine padre e figlio vengono pubblicate in azioni separate

## Pubblicazione di pagine dalla console Sites {#publishing-from-the-sites-console}

Nella console **Sites** sono disponibili due opzioni per la pubblicazione:

* [Pubblicazione rapida &#x200B;](#quick-publish)
* [Gestisci pubblicazione &#x200B;](#manage-publication)

### Pubblicazione rapida  {#quick-publish}

**Pubblicazione rapida** si usa in casi semplici; le pagine selezionate vengono pubblicate immediatamente senza ulteriore interazione. Per questo motivo, anche eventuali riferimenti non pubblicati verranno pubblicati automaticamente.

Per pubblicare una pagina con Pubblicazione rapida:

1. Selezionare le pagine desiderate nella console Sites e fare clic sul pulsante **Pubblicazione rapida**.

   ![Selezione delle pagine per la pubblicazione](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. Nella finestra di dialogo Pubblicazione rapida, conferma la pubblicazione facendo clic su **Pubblica** o annulla la pubblicazione facendo clic su **Annulla**. Tieni presente che verranno pubblicati automaticamente anche eventuali riferimenti non pubblicati.

   ![Conferma Pubblicazione rapida](/help/sites-cloud/authoring/assets/publishing-quick-publish.png)

1. Quando la pagina viene pubblicata, viene visualizzato un avviso che ne conferma la pubblicazione.

>[!NOTE]
>
>La pubblicazione rapida è una pubblicazione “superficiale”, ovvero vengono pubblicate solo le pagine selezionate e non le relative pagine secondarie.

### Gestisci pubblicazione  {#manage-publication}

**Gestisci pubblicazione** offre più opzioni rispetto a **Pubblicazione rapida**, consentendo l&#39;inclusione di pagine figlie, la personalizzazione dei riferimenti, la pubblicazione in un servizio di anteprima (se disponibile) e l&#39;avvio di tutti i flussi di lavoro applicabili e offrendo la possibilità di pubblicare in un secondo momento.

Per pubblicare una pagina o annullarne la pubblicazione tramite Gestisci pubblicazione:

1. Selezionare le pagine desiderate nella console Sites e fare clic sul pulsante **Gestisci pubblicazione**.

   ![Selezione delle pagine per la pubblicazione](/help/sites-cloud/authoring/assets/publishing-select-pages.png)

1. Viene avviata la procedura guidata **Gestisci pubblicazione**. Il primo passaggio, **Opzioni**, consente di:

   * **Azione**

     Scegliere di pubblicare le pagine selezionate o annullarne la pubblicazione.

   * **Destinazione**

     Scegli se desideri pubblicare nel servizio di pubblicazione (impostazione predefinita) o nel servizio di anteprima. Disponibile solo se è configurato il servizio di anteprima [.](/help/sites-cloud/authoring/sites-console/previewing-content.md)

   * **Pianificazione**

     Scegli se eseguire l’azione ora o in un secondo momento.

     Con Pubblica più tardi viene avviato un flusso di lavoro per attivare le pagine selezionate alla data e all’ora specificate. Al contrario, l’annullamento della pubblicazione in un secondo momento avvia un flusso di lavoro per annullare la pubblicazione della pagina o delle pagine selezionate in un momento specifico.

     >[!TIP]
     >
     >Per annullare un’attività di pubblicazione, anche programmata per un momento successivo, accedete alla [console Flusso di lavoro](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance) e interrompete il flusso di lavoro corrispondente.

     >[!TIP]
     >
     >La pianificazione del contenuto per la pubblicazione replica il contenuto e rispetta i flussi di lavoro di pubblicazione. Se desideri nascondere temporaneamente il contenuto già pubblicato senza annullare la pubblicazione, considera [**Ora di attivazione** e **Ora di disattivazione** disponibili nelle proprietà della pagina.](/help/sites-cloud/authoring/sites-console/page-properties.md#basic)

   ![Opzioni di Gestisci pubblicazione](/help/sites-cloud/authoring/assets/publishing-manage-publication-options.png)

1. Fai clic su **Avanti** per continuare.

1. Nel passaggio successivo della procedura guidata Gestisci pubblicazione, **Ambito**, puoi definire l’ambito della pubblicazione o dell’annullamento della pubblicazione, ad esempio decidendo se includere pagine secondarie e/o riferimenti.

   ![Ambito di Gestisci pubblicazione](/help/sites-cloud/authoring/assets/publishing-manage-publication-scope.png)

   **Aggiungi contenuto**

   Puoi usare il pulsante **Aggiungi contenuto** per aggiungere ulteriori pagine all’elenco delle pagine da pubblicare, nel caso in cui ti sia dimenticato di selezionarne una prima di avviare la procedura guidata Gestisci pubblicazione.

   Selezionando il pulsante **Aggiungi contenuto** si avvia il [browser percorsi](/help/sites-cloud/authoring/path-selection.md), che consente di selezionare contenuti.

   Seleziona le pagine desiderate e fai clic su **Seleziona** per aggiungere contenuti alla procedura guidata o su **Annulla** per annullare la selezione e tornare alla procedura guidata.

   **Rimuovi selezione**

   Nella procedura guidata, puoi selezionare un elemento nell’elenco per rimuoverlo dalla selezione.

   ![Selezione pagine di Gestisci pubblicazione](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   **Riferimenti pubblicati**

   Puoi visualizzare e modificare i riferimenti da pubblicare o di cui annullare la pubblicazione per una pagina selezionandola e facendo clic sul pulsante **Riferimenti pubblicati**.

   ![Opzioni di Gestisci pubblicazione](/help/sites-cloud/authoring/assets/publishing-manage-publication-references.png)

   La finestra di dialogo **Riferimenti pubblicati** visualizza i riferimenti per il contenuto selezionato. Per impostazione predefinita si presentano tutti selezionati e verranno pubblicati o ne verrà annullata la pubblicazione, ma puoi deselezionarli in modo da non includerli nell’azione.

   Fai clic su **Fine** per salvare le modifiche o su **Annulla** per annullare la selezione e tornare alla procedura guidata.

   Nella procedura guidata, la colonna **Riferimenti** verrà aggiornata per riflettere la selezione dei riferimenti da pubblicare o di cui annullare la pubblicazione.

   ![Selezione pagine di Gestisci pubblicazione](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

   **Includi elementi secondari**

   >[!NOTE]
   >
   >Consulta [Pubblicazione e annullamento della pubblicazione di una struttura](#publishing-and-unpublishing-a-tree)

   Facendo clic su **Includi elementi secondari** viene visualizzata una finestra di dialogo che consente di:

   * **Includi elementi secondari**
   * **Solo gli elementi secondari di primo livello**
   * **Solo pagine modificate**
   * **Solo pagine già pubblicate**

   Attiva le opzioni richieste e conferma con **OK** per aggiungere le pagine secondarie all’elenco delle pagine da pubblicare o di cui annullare la pubblicazione, in base alle opzioni selezionate. Fai clic su **Annulla** per annullare la selezione e tornare alla procedura guidata.

   ![Inclusione di elementi secondari in Gestisci pubblicazione](/help/sites-cloud/authoring/assets/publishing-include-children.png)

1. Fai clic su **Pubblica** per completare l’azione.

   Nella console Sites, un messaggio di notifica confermerà la pubblicazione.

1. Se le pagine pubblicate sono associate a flussi di lavoro, potrebbero essere visualizzati in un passaggio finale **Flussi di lavoro** della procedura guidata di pubblicazione.

   ![Selezione pagine di Gestisci pubblicazione](/help/sites-cloud/authoring/assets/publishing-manage-publication-workflow.png)

   >[!NOTE]
   >
   >Il passaggio **Flussi di lavoro** verrà visualizzato in base ai diritti di cui dispone o meno l’utente. Per ulteriori dettagli, consulta la nota precedente su questa pagina inerente i privilegi di pubblicazione, nonché gli argomenti Gestione dell’accesso ai flussi di lavoro e [Applicazione dei flussi di lavoro alle pagine](/help/sites-cloud/authoring/workflows/applying.md).

   Le risorse sono raggruppate in base ai flussi di lavoro attivati e a ciascuna opzione specificata per:

   * Definire il titolo del flusso di lavoro.
   * Mantenere il pacchetto del flusso di lavoro, a condizione che il flusso di lavoro sia dotato di supporto per più risorse.
   * Definire un titolo del pacchetto del flusso di lavoro se è stata selezionata l’opzione per mantenere il pacchetto del flusso di lavoro.

1. Fai clic su **Pubblica** o **Pubblica più tardi** per completare la pubblicazione.

## Annullamento della pubblicazione delle pagine {#unpublishing-pages}

L&#39;annullamento della pubblicazione di una pagina ne effettua la rimozione dall&#39;ambiente di pubblicazione o [anteprima](/help/sites-cloud/authoring/sites-console/previewing-content.md) e la pagina non sarà più disponibile per i lettori.

Puoi utilizzare [l’opzione Gestisci pubblicazione per eseguire la pubblicazione](#manage-publication), ma anche per annullarla.

1. Selezionare le pagine desiderate nella console Sites e fare clic sul pulsante **Gestisci pubblicazione**.
1. Viene avviata la procedura guidata **Gestisci pubblicazione**. Nel primo passaggio, **Opzioni**, seleziona **Annulla pubblicazione** anziché l’opzione predefinita **Pubblica**.

   ![Annullamento della pubblicazione - Opzioni](/help/sites-cloud/authoring/assets/publishing-unpublish.png)

   Con Pubblica più tardi viene avviato un flusso di lavoro per pubblicare tale versione della pagina alla data e all’ora specificate. In modo analogo, se si sceglie di annullare la pubblicazione in un secondo momento, verrà attivato un flusso di lavoro per annullare la pubblicazione delle pagine selezionate alla data e all’ora specificate.

   >[!NOTE]
   >
   >Per annullare un’attività di pubblicazione, anche programmata per un momento successivo, accedete alla [console Flusso di lavoro](/help/sites-cloud/administering/workflows-administering.md#suspending-resuming-and-terminating-a-workflow-instance) e interrompete il flusso di lavoro corrispondente.

   >[!NOTE]
   >Se hai un ambiente [Anteprima](/help/sites-cloud/authoring/sites-console/previewing-content.md) puoi selezionare la **Destinazione** durante Gestisci pubblicazione.

1. Per completare l’annullamento della pubblicazione, continua a seguire la procedura guidata come faresti per [pubblicare la pagina](#manage-publication).

   ![Annullamento della pubblicazione - Ambito](/help/sites-cloud/authoring/assets/publishing-unpublish-scope.png)

## Pubblicazione e annullamento della pubblicazione di una struttura {#publishing-and-unpublishing-a-tree}

Dopo aver inserito o aggiornato un numero considerevole di pagine di contenuto, tutte memorizzate nella stessa pagina principale, può risultare più semplice pubblicare l’intera struttura in un’unica azione.

È possibile utilizzare [Gestisci pubblicazione](#manage-publication) nella console Sites.

1. Nella console Sites, seleziona la pagina principale della struttura che desideri pubblicare o annullare la pubblicazione e seleziona **Gestisci pubblicazione**.
1. Viene avviata la procedura guidata **Gestisci pubblicazione**. Scegli se e quando pubblicare o annullare la pubblicazione e seleziona **Avanti** per continuare.
1. Nel passaggio **Ambito**, seleziona la pagina principale e fai clic su **Includi elementi secondari**.

   ![Selezione pagine di Gestisci pubblicazione](/help/sites-cloud/authoring/assets/publishing-manage-publication-select.png)

1. Nella finestra di dialogo **Includi elementi secondari**:

   * seleziona **Includi elementi secondari**
   * deseleziona **Includi solo gli elementi secondari di primo livello**
   * deseleziona **Includi solo pagine già pubblicate**
   * configura **Includi solo pagine modificate** come richiesto

   Queste opzioni sono selezionate per impostazione predefinita, pertanto dovrai ricordarti di configurarle. Conferma la selezione con **OK** per aggiungere il contenuto alla pubblicazione o all’annullamento della pubblicazione.

   ![Inclusione di elementi secondari per la pubblicazione della struttura](/help/sites-cloud/authoring/assets/publishing-include-children-tree.png)

1. Nella procedura guidata **Gestisci pubblicazione** è possibile personalizzare ulteriormente la selezione aggiungendo ulteriori pagine o rimuovendo quelle selezionate.

   Non dimenticare che è anche possibile esaminare i riferimenti da pubblicare tramite l’opzione **Riferimenti pubblicati**.

1. [Continua a seguire normalmente la procedura guidata Gestisci pubblicazione](#manage-publication) per completare la pubblicazione o annullare la pubblicazione della struttura.

## Determinazione dello stato di pubblicazione {#determining-publication-status}

Puoi determinare lo stato di pubblicazione di una pagina:

* Nelle [informazioni generali sulla risorsa nella console Sites](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources)

  ![Stato della pubblicazione nella vista a schede](/help/sites-cloud/authoring/assets/publishing-status-console-card.png)

  Lo stato di pubblicazione è indicato nelle viste [a schede](/help/sites-cloud/authoring/basic-handling.md#card-view), [a colonne](/help/sites-cloud/authoring/basic-handling.md#column-view) e [a elenco](/help/sites-cloud/authoring/basic-handling.md#list-view) nella console Sites.

* Nella [timeline](/help/sites-cloud/authoring/basic-handling.md#timeline)

  ![Stato della pubblicazione nella visualizzazione timeline](/help/sites-cloud/authoring/assets/publishing-status-timeline.png)

* Nel menu [Informazioni pagina](/help/sites-cloud/authoring/page-editor/introduction.md#page-information) durante la modifica di una pagina

  ![Stato della pubblicazione nel menu Informazioni pagina](/help/sites-cloud/authoring/assets/publishing-status-page-information.png)
