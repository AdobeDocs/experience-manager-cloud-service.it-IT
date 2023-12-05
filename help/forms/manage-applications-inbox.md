---
title: Come posso gestire moduli, applicazioni e attività nella casella in entrata AEM?
description: Casella in entrata AEM consente di avviare flussi di lavoro incentrati su Forms tramite l'invio di applicazioni e la gestione di attività.
uuid: c6c0d8ea-743f-4852-99d1-69fd50a0994e
contentOwner: vishgupt
topic-tags: document_services, publish
discoiquuid: dd11fd83-3df1-4727-8340-8c5426812823
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 2%

---


# Gestione delle applicazioni e delle attività di Forms nella casella in entrata AEM{#manage-forms-applications-and-tasks-in-aem-inbox}

Uno dei modi per avviare o attivare un flusso di lavoro incentrato su Forms è tramite le applicazioni nella casella in entrata AEM. Per rendere disponibile un Forms Workflow come applicazione in Posta in arrivo, è necessario creare un&#39;applicazione del flusso di lavoro. Per ulteriori informazioni sull’applicazione del flusso di lavoro e su altri modi per avviare i flussi di lavoro di Forms, consulta [Avviare un flusso di lavoro incentrato su Forms su OSGi](aem-forms-workflow.md#launch).

Inoltre, la Casella in entrata AEM consolida le notifiche e le attività da vari componenti AEM, inclusi i flussi di lavoro Forms. Quando viene attivato un Forms Workflow contenente un passaggio Assegna attività, l&#39;applicazione associata viene elencata come attività nella casella in entrata dell&#39;assegnatario. Se l&#39;assegnatario è un gruppo, l&#39;attività viene visualizzata nella Posta in arrivo di tutti i membri del gruppo fino a quando un singolo utente non richiede o delega l&#39;attività.

L&#39;interfaccia utente Casella in entrata fornisce viste elenco e calendario per visualizzare le attività. È inoltre possibile configurare le impostazioni di visualizzazione. Puoi filtrare le attività in base a vari parametri. Per ulteriori informazioni sulla visualizzazione e sui filtri, consulta [Casella in entrata](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/inbox.html#inbox-in-the-header).

In sintesi, Casella in entrata consente di creare un&#39;applicazione e gestire le attività assegnate.

>[!NOTE]
>
>Devi essere membro di [!DNL workflow-users] per poter utilizzare la casella in entrata AEM.

## Crea applicazione {#create-application}

1. Vai alla casella in entrata AEM all’indirizzo https://&#39;[server]:[porta]&#39;/aem/inbox.
1. Nell’interfaccia utente della casella in entrata, seleziona **[!UICONTROL Crea > Applicazione]**. Viene visualizzata la pagina Seleziona applicazione.
1. Seleziona un’applicazione e fai clic su **[!UICONTROL Crea]**. Viene aperto il modulo adattivo associato all’applicazione. Compila le informazioni nel modulo adattivo e seleziona **[!UICONTROL Invia]**. Avvia il flusso di lavoro associato e crea un&#39;attività nella Posta in arrivo dell&#39;assegnatario.

## Gestione attività {#manage-tasks}

Quando si attiva un flusso di lavoro di Forms e si è assegnatari o parte del gruppo assegnatari, nella casella in entrata viene visualizzata un&#39;attività. È possibile visualizzare i dettagli dell&#39;attività ed eseguire le azioni disponibili sull&#39;attività dalla casella in entrata.

### Richiedi o delega attività {#claim-or-delegate-tasks}

Le attività assegnate a un gruppo vengono visualizzate nella cartella Posta in arrivo di tutti i membri del gruppo. Qualsiasi membro del gruppo può rivendicare tale attività o delegarla a un altro membro del gruppo. Per eseguire questa operazione:

1. Selezionare per selezionare la miniatura dell&#39;attività. Le opzioni per aprire o delegare l&#39;attività vengono visualizzate nella parte superiore.

   ![select-task](assets/select-task.png)

1. Effettua una delle operazioni seguenti:

   * Per delegare l’attività, seleziona **[!UICONTROL Delega]**. Viene visualizzata la finestra di dialogo Delega elemento. Seleziona un utente, facoltativamente aggiungi un commento e seleziona **[!UICONTROL OK]**.

   ![delegare](assets/delegate.png)

   * Per richiedere l&#39;attività, selezionare **[!UICONTROL Apri]**. Viene visualizzata la finestra di dialogo Assegna a sé. Seleziona **[!UICONTROL Procedi]** per richiedere l&#39;attività. L&#39;attività richiesta viene visualizzata come assegnatario nella cartella Posta in arrivo.

   ![reclamo](assets/claim.png)

### Visualizzare i dettagli ed eseguire azioni sulle attività {#view-details-and-perform-actions-on-tasks}

Quando si apre un&#39;attività, è possibile visualizzarne i dettagli ed eseguire le azioni disponibili. Le azioni disponibili per un&#39;attività sono definite nel passaggio Assegna attività del Forms Workflow associato.

1. Selezionare per selezionare la miniatura dell&#39;attività. Le opzioni per aprire o delegare l&#39;attività selezionata vengono visualizzate nella parte superiore.
1. Seleziona **Apri** per visualizzare i dettagli dell&#39;attività e le azioni disponibili. Viene visualizzata la vista dettagliata dell&#39;operazione. In questa visualizzazione è possibile visualizzare i dettagli di un&#39;attività e intervenire su di essa.

   >[!NOTE]
   >
   >Se un&#39;attività è assegnata a un gruppo, è necessario dichiararla per essere in grado di aprirla in visualizzazione dettagliata.

![task-details](assets/task-details.png)

La vista dettagliata delle attività comprende le sezioni riportate di seguito.

* Dettagli attività
* Modulo
* Dettagli flusso di lavoro
* Barra delle azioni

#### Dettagli attività {#task-details}

Nella sezione Dettagli attività vengono visualizzate informazioni sull&#39;attività. Le informazioni visualizzate dipendono dalle impostazioni di configurazione del [Assegna passaggio attività](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem) nel flusso di lavoro. Nell&#39;esempio precedente vengono visualizzati la descrizione, lo stato, la data di inizio e il flusso di lavoro utilizzati per l&#39;attività. Consente inoltre di allegare un file all&#39;operazione.

#### Modulo {#form}

La scheda Modulo nell’area del contenuto principale visualizza il modulo inviato e gli eventuali allegati a livello di campo.

#### Dettagli flusso di lavoro {#workflow-details}

La scheda Dettagli flusso di lavoro nella parte superiore mostra l’avanzamento dell’attività attraverso le varie fasi del flusso di lavoro. Vengono visualizzate le fasi completata, corrente e in sospeso per l&#39;attività. Le fasi di un flusso di lavoro sono definite nel [Assegna passaggio attività](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem) del workflow associato.

Inoltre, nella scheda viene visualizzata la cronologia delle attività per ogni fase completata del flusso di lavoro. Puoi selezionare **[!UICONTROL Visualizza dettagli]** per una fase completata per conoscere i dettagli su tale fase. Vengono visualizzati i commenti, gli allegati del modulo e dell&#39;attività, lo stato, le date di inizio e di fine e così via relativi all&#39;attività.

![workflow-details](assets/workflow-details.png)

#### Barra delle azioni {#actions-toolbar}

La barra degli strumenti Azioni mostra tutte le opzioni disponibili per l&#39;attività. Mentre Salva, Reimposta e Delega sono azioni predefinite, altre azioni disponibili sono configurate in [Assegna passaggio attività](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem). Nell’esempio precedente, Approve (Approva) e Reject (Rifiuta) sono configurati nel flusso di lavoro.

Quando si agisce sull’attività, questa procede ulteriormente nel flusso di lavoro.

### Visualizza attività completate {#view-completed-tasks}

Nella casella in entrata AEM vengono visualizzate solo le attività attive. Le attività completate non vengono visualizzate nell&#39;elenco. È tuttavia possibile utilizzare i filtri Posta in arrivo per filtrare le attività in base a diversi parametri, quali tipo di attività, stato, date di inizio e di fine. Per visualizzare le attività completate:

1. Nella casella in entrata AEM selezionare ![interruttore-side-panel1](assets/toggle-side-panel1.png) per aprire il selettore dei filtri.
1. Seleziona **[!UICONTROL Stato attività]** Pannello a soffietto e selezione **[!UICONTROL Completa]**. Vengono visualizzate tutte le attività completate.

   ![filter](assets/filter.png)

1. Seleziona per selezionare un’attività e fai clic su **[!UICONTROL Apri]**.

Viene visualizzata l’attività per visualizzare il documento o il modulo adattivo associato all’attività. Per il modulo adattivo, l’attività visualizza il modulo adattivo di sola lettura o il relativo documento di record PDF come configurato nella scheda Modulo/Documento del [Passaggio del flusso di lavoro Assegna attività](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-step-ref.html#extending-aem).

Nella sezione dei dettagli dell&#39;attività vengono visualizzate informazioni quali l&#39;azione intrapresa, lo stato dell&#39;attività, la data di inizio e la data di fine.

![attività completata](assets/completed-task.png)

Il **[!UICONTROL Dettagli flusso di lavoro]** mostra ogni passaggio del flusso di lavoro. Seleziona **[!UICONTROL Visualizza dettagli]** per informazioni dettagliate.

![completed-task-workflow](assets/completed-task-workflow.png)

## Risoluzione dei problemi {#troubleshooting-workflows}

### Impossibile visualizzare gli elementi relativi al flusso di lavoro AEM nella casella in entrata AEM {#unable-to-see-aem-worklow-items}

Il proprietario di un modello di flusso di lavoro non è in grado di visualizzare gli elementi relativi al flusso di lavoro AEM nella casella in entrata AEM. Per risolvere il problema, aggiungi gli indici elencati di seguito al tuo archivio AEM e ricostruisci l’indice.

1. Per aggiungere indici, utilizzate uno dei seguenti metodi:

   * Crea i seguenti nodi in CRX DE in `/oak:index/workflowDataLucene/indexRules/granite:InboxItem/properties` con le rispettive proprietà specificate nella tabella seguente:

     | Nodo | Proprietà | Tipo |
     |---|---|---|
     | sharedWith | sharedWith | STRINGA |
     | protetto | protetto | BOOLEANO |
     | ha restituito | ha restituito | BOOLEANO |
     | allowInboxSharing | allowInboxSharing | BOOLEANO |
     | allowExplicitSharing | allowExplicitSharing | BOOLEANO |


   * Implementare gli indici tramite un pacchetto AEM. È possibile utilizzare un’ [Archetipo AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) per creare un pacchetto AEM distribuibile. Utilizza il seguente codice di esempio per aggiungere indici a un progetto dell’archetipo AEM:

   ```Java
      .property("sharedWith", "sharedWith").type(TYPENAME_STRING).propertyIndex()
      .property("locked", "locked").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("returned", "returned").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("allowInboxSharing", "allowInboxSharing").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("allowExplicitSharing", "allowExplicitSharing").type(TYPENAME_BOOLEAN).propertyIndex()
   ```

1. [Creare un indice delle proprietà e impostarlo su true](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/queries-and-indexing.html?lang=en#the-property-index).

1. Dopo la configurazione degli indici in CRX DE o la distribuzione tramite un pacchetto, [reindicizzare l’archivio](https://helpx.adobe.com/in/experience-manager/kb/HowToCheckLuceneIndex.html#Completelyrebuildtheindex).

