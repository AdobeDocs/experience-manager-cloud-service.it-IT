---
title: Applicazione dei flussi di lavoro alle pagine
description: Durante l’authoring, è possibile ricorrere ai flussi di lavoro per intraprendere azioni sulle pagine; è inoltre possibile applicare più di un flusso di lavoro..
exl-id: 86e71f0e-e53e-40bc-901d-2a1ab347bd0a
source-git-commit: a01583483fa89f89b60277c2ce4e1c440590e96c
workflow-type: ht
source-wordcount: '660'
ht-degree: 100%

---

# Applicazione dei flussi di lavoro alle pagine {#applying-workflows-to-pages}

Durante l’authoring, è possibile ricorrere ai flussi di lavoro per intraprendere azioni sulle pagine; è inoltre possibile applicare più di un flusso di lavoro.

Quando applichi il flusso di lavoro, specifichi le informazioni seguenti:

* Flusso di lavoro da applicare.
   * Puoi utilizzare qualsiasi flusso di lavoro a cui hai accesso, secondo quanto assegnato dall’amministratore AEM.
* Facoltativamente, un titolo che consente di identificare l’istanza del flusso di lavoro nella casella in entrata di un utente.
* Il payload del flusso di lavoro; può essere costituito da una o più pagine.

I flussi di lavoro possono essere avviati da:

* [La console Sites](#starting-a-workflow-from-the-sites-console);
* [durante la modifica di una pagina, da Informazioni pagina](#starting-a-workflow-from-the-page-editor).

>[!NOTE]
>
>Consulta anche:
>
>* Come applicare i flussi di lavoro alle risorse DAM.
>* [Utilizzo dei flussi di lavoro per i progetti](/help/sites-cloud/authoring/projects/workflows.md).

<!-- 
>* [How to apply workflows to DAM assets](/help/assets/assets-workflow.md).
>* [Working with Project Workflows](/help/sites-cloud/authoring/projects/workflows.md).
-->

>[!NOTE]
>
>Gli amministratori AEM possono avviare i flussi di lavoro attraverso molti altri metodi.

<!-- 
>AEM administrators can [start workflows using several other methods](/help/sites-administering/workflows-starting.md).
-->

## Avvio di un flusso di lavoro dalla console Sites {#starting-a-workflow-from-the-sites-console}

Puoi avviare un flusso di lavoro da:

* [con l’opzione Crea della barra degli strumenti di Sites](#starting-a-workflow-from-the-sites-toolbar);
* [dalla barra Timeline della console Sites](#starting-a-workflow-from-the-timeline).

In entrambi i casi sarà necessario:

* [Specificare i dettagli del flusso di lavoro nella procedura guidata Crea flusso di lavoro](#specifying-workflow-details-in-the-create-workflow-wizard).

### Avvio di un flusso di lavoro dalla barra degli strumenti di Sites {#starting-a-workflow-from-the-sites-toolbar}

Puoi avviare un flusso di lavoro dalla barra degli strumenti della console **Sites**:

1. Vai alla pagina richiesta e selezionala.

1. Dall’opzione **Crea** nella barra degli strumenti è ora possibile selezionare **Flusso di lavoro**.

   ![Creare un flusso di lavoro dalla barra degli strumenti](/help/sites-cloud/authoring/assets/workflows-create-from-toolbar.png)

1. La procedura guidata **Crea flusso di lavoro** ti aiuterà a [specificare i dettagli del flusso di lavoro](#specifying-workflow-details-in-the-create-workflow-wizard).

### Avvio di un flusso di lavoro dalla timeline {#starting-a-workflow-from-the-timeline}

Dalla sezione **Timeline** puoi avviare un flusso di lavoro da applicare alla risorsa selezionata.

1. [Seleziona la risorsa](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) e apri [Timeline](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) (o apri Timeline, quindi seleziona la risorsa).
1. Puoi utilizzare la freccia dal campo commento per visualizzare **Avvia flusso di lavoro**:

   ![Creare un flusso di lavoro dalla timeline](/help/sites-cloud/authoring/assets/workflows-create-from-timeline.png)

1. La procedura guidata **Crea flusso di lavoro** ti aiuterà a [specificare i dettagli del flusso di lavoro](#specifying-workflow-details-in-the-create-workflow-wizard).

### Specifica dei dettagli del flusso di lavoro nella procedura guidata Crea flusso di lavoro {#specifying-workflow-details-in-the-create-workflow-wizard}

La procedura guidata **Crea flusso di lavoro** sarà d’aiuto per selezionare il flusso di lavoro e specificare i dettagli richiesti.

Dopo l’apertura della procedura guidata **Crea flusso di lavoro** da:

* [con l’opzione Crea della barra degli strumenti di Sites](#starting-a-workflow-from-the-sites-toolbar);
* [dalla barra Timeline della console Sites](#starting-a-workflow-from-the-timeline).

Puoi specificare i dettagli:

1. Nel passaggio **Proprietà** vengono definite le opzioni di base del flusso di lavoro:

   * **Modello flusso di lavoro**
   * **Titolo flusso di lavoro**

      * Puoi specificare un titolo per questa istanza per facilitarne l’identificazione in una fase successiva.

   A seconda del modello di flusso di lavoro, sono disponibili anche le seguenti opzioni. Queste consentono di mantenere il pacchetto creato come payload al termine del flusso di lavoro.

   * **Mantieni pacchetto flusso di lavoro**
   * **Titolo pacchetto**

      * Puoi specificare un titolo per il pacchetto per facilitare l’identificazione.

   >[!NOTE]
   >
   >L’opzione **Mantieni pacchetto flusso di lavoro** è disponibile quando il flusso di lavoro è stato configurato per Supporto risorse multiple e sono state selezionate più risorse.

   <!--
   >The **Keep workflow package** option is available when the workflow has been configured for [Multi Resource Support](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) and multiple resources have been selected.
   -->

   Una volta completato, premere su **Successivo** per continuare.

   ![Specifica delle proprietà del flusso di lavoro](/help/sites-cloud/authoring/assets/workflows-properties.png)

1. Al passaggio **Ambito** puoi selezionare:

   * **Aggiungi contenuto**, per aprire il [browser percorsi](/help/sites-cloud/authoring/fundamentals/environment-tools.md#path-browser) e selezionare altre risorse; una volta nel browser, tocca o fai clic su **Seleziona** per aggiungere contenuti all’istanza di flusso di lavoro.

   * Una risorsa esistente per visualizzare le seguenti azioni:

      * **Includi elementi secondari** per specificare gli elementi secondari di tale risorsa che vengono inclusi nel flusso di lavoro.
Una finestra di dialogo si apre per permettere di perfezionare la selezione includendo:

         * Solo gli elementi secondari di primo livello.
         * Solo pagine modificate.
         * Solo pagine già pubblicate.

        Eventuali elementi secondari specificati vengono aggiunti all’elenco delle risorse a cui verrà applicato il flusso di lavoro.

      * **Rimuovi selezione** per rimuovere tale risorsa dal flusso di lavoro.

   ![Definire l’ambito del flusso di lavoro](/help/sites-cloud/authoring/assets/workflows-scope.png)

   >[!NOTE]
   >
   >Se aggiungi ulteriori risorse, puoi selezionare **Indietro** per regolare l’impostazione di **Mantieni pacchetto flusso di lavoro** nel passaggio **Proprietà**.

1. Usa **Crea** per chiudere la procedura guidata e creare l’istanza di flusso di lavoro. Nella console Sites viene visualizzata una notifica.

## Avvio di un flusso di lavoro dall’editor pagina {#starting-a-workflow-from-the-page-editor}

Quando modifichi una pagina puoi selezionare **Informazioni pagina** dalla barra degli strumenti. Il menu a discesa include l’opzione **Inizia nel flusso di lavoro**. Questa apre una finestra di dialogo nella quale puoi specificare il flusso di lavoro obbligatorio, insieme a un titolo richiesto:

![Avviare un flusso di lavoro dall’editor pagina](/help/sites-cloud/authoring/assets/workflows-create-page-editor.png)
