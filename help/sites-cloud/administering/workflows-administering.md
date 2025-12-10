---
title: Amministrazione delle istanze dei flussi di lavoro
description: Scopri come amministrare le istanze dei flussi di lavoro utilizzando la console dei flussi di lavoro
feature: Administering
role: Admin
exl-id: d2adb5e8-3f0e-4a3b-b7d0-dbbc5450e45f
solution: Experience Manager Sites
source-git-commit: 372d8969b1939e9a24d7910a1678a17c0dc9f9fd
workflow-type: tm+mt
source-wordcount: '1282'
ht-degree: 90%

---

# Amministrazione delle istanze dei flussi di lavoro {#administering-workflow-instances}

La console Flusso di lavoro fornisce diversi strumenti per l’amministrazione delle istanze del flusso di lavoro, in modo che vengano eseguite come previsto.

Sono disponibili diverse console per l’amministrazione dei flussi di lavoro. Utilizza la [navigazione globale](/help/sites-cloud/authoring/basic-handling.md#global-navigation) per aprire il riquadro **Strumenti**, quindi selezionare **Flusso di lavoro**:

* **Modelli**: gestire le definizioni dei flussi di lavoro
* **Istanze**: visualizzazione e gestione delle istanze di flussi di lavoro in esecuzione
* **Moduli di avvio**: gestire le modalità di avvio dei flussi di lavoro
* **Archiviazione**: visualizzazione della cronologia dei flussi di lavoro completati con successo
* **Errori**: visualizzazione della cronologia dei flussi di lavoro completati con errori
* **Assegnazione automatica**: configura l’assegnazione automatica dei flussi di lavoro ai modelli

## Monitoraggio dello stato delle istanze del flusso di lavoro {#monitoring-the-status-of-workflow-instances}

1. Tramite navigazione, seleziona **Strumenti**, quindi **Flusso di lavoro**.
1. Seleziona **Istanze** per visualizzare l’elenco delle istanze in esecuzione del flusso di lavoro attualmente in corso.
1. Nella barra superiore, nell’angolo a destra, le istanze del flusso di lavoro mostrano i **Flussi di lavoro in esecuzione**, lo **Stato** e i **Dettagli**.
1. L’istanza **Flussi di lavoro in esecuzione** mostra il numero di flussi di lavoro in esecuzione e il relativo stato. Ad esempio, nelle immagini specificate, viene mostrato il numero di **Flussi di lavoro in esecuzione** e lo **Stato** dell’istanza di AEM:

   * **Stato: integro**
     ![status-healthy](/help/sites-cloud/administering/assets/status-healthy.png)

   * **Stato: non integro**
     ![status-unhealthy](/help/sites-cloud/administering/assets/status-unhealthy.png)

1. Per i **Dettagli dello stato** delle istanze del flusso di lavoro, fai clic su **Dettagli**, per visualizzare il **numero di istanze di flussi di lavoro in esecuzione**, le **istanze di flusso di lavoro completate**, le **istanze di flusso di lavoro interrotte**, le **istanze di flusso di lavoro non riuscite** e così via. Ad esempio, di seguito sono riportate le immagini che mostrano i **Dettagli dello stato** con:

   * **Dettagli dello stato: integro**
     ![status-details-healthy](/help/sites-cloud/administering/assets/status-details-healthy.png)

   * **Dettagli dello stato: non integro**
     ![status-details-unhealthy](/help/sites-cloud/administering/assets/status-details-unhealthy.png)

   >[!NOTE]
   >
   > Per mantenere integra l’istanza del flusso di lavoro, segui le best practice in [Eliminazione regolare delle istanze del flusso di lavoro](#regular-purging-of-workflow-instances) o [Migliori best practice per i flussi di lavoro](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-best-practices.html).

## Cerca istanze del flusso di lavoro {#search-workflow-instances}

1. Tramite navigazione, seleziona **Strumenti**, quindi **Flusso di lavoro**.
1. Seleziona **Istanze** per visualizzare l’elenco delle istanze del flusso di lavoro attualmente in corso. Nella barra superiore, nell’angolo sinistro, seleziona **Filtri**. In alternativa, è possibile utilizzare i tasti Alt+1. Viene visualizzata la seguente finestra di dialogo:

   ![wf-99-1](/help/sites-cloud/administering/assets/wf-99-1.png)

1. Nella finestra di dialogo Filtro, seleziona i criteri di ricerca del flusso di lavoro. Puoi eseguire ricerche in base ai seguenti input:

   * Percorso payload: selezionare un percorso specifico
   * Modello di flusso di lavoro: selezionare un modello di flusso di lavoro
   * Assegnatario: selezionare un assegnatario del flusso di lavoro
   * Tipo: Attività, Elemento del flusso di lavoro o Errore del flusso di lavoro
   * Stato attività: attivo, completato o terminato
   * Dove sono: Proprietario AND Assegnatario, Solo proprietario, Solo assegnatario
   * Data di inizio: data di inizio prima o dopo una data specificata
   * Data di fine: data di fine prima o dopo una data specificata
   * Data di scadenza: data di scadenza prima o dopo una data specificata
   * Data aggiornamento: data aggiornata prima o dopo una data specificata

## Sospensione, Ripresa e Chiusura di un’istanza di flusso di lavoro {#suspending-resuming-and-terminating-a-workflow-instance}

1. Tramite navigazione, seleziona **Strumenti**, quindi **Flusso di lavoro**.
1. Seleziona **Istanze** per visualizzare l’elenco delle istanze del flusso di lavoro attualmente in corso.

   ![wf-96-1](/help/sites-cloud/administering/assets/wf-96-1.png)

1. Seleziona un elemento specifico, quindi utilizza **Termina**, **Sospendi** oppure **Riprendi**, a seconda del caso; verrà richiesto di confermare e/o fornire ulteriori dettagli:

   ![wf-97-1](/help/sites-cloud/administering/assets/wf-97-1.png)

   >[!NOTE]
   >
   >
   >Per terminare o interrompere un flusso di lavoro, è necessario che si trovi in uno stato di attesa dell’intervento dell’utente, come Passaggio partecipante. Il tentativo di interrompere un flusso di lavoro che ha processi in esecuzione (thread attivi in esecuzione) potrebbe non produrre i risultati previsti.


## Visualizzazione dei flussi di lavoro archiviati {#viewing-archived-workflows}

1. Tramite navigazione, seleziona **Strumenti**, quindi **Flusso di lavoro**.

1. Seleziona **Archivio** per visualizzare l’elenco delle istanze del flusso di lavoro completate correttamente.

   ![archived-instances](/help/sites-cloud/administering/assets/archived-instances.png)

   >[!NOTE]
   >
   >
   >Lo stato di interruzione viene considerato come una terminazione corretta in quanto si verifica in seguito a un’azione dell’utente; ad esempio:
   >
   >* utilizzo dell’azione **Termina**
   >* quando una pagina, soggetta a un flusso di lavoro, viene eliminata (forzatamente), il flusso di lavoro viene terminato.

1. Seleziona un elemento specifico, quindi **Cronologia elementi aperti** per ulteriori dettagli:

   ![wf-99](/help/sites-cloud/administering/assets/wf-99.png)

## Correzione degli errori di un&#39;istanza del flusso di lavoro {#fixing-workflow-instance-failures}

Quando un flusso di lavoro non riesce, AEM mette a disposizione la console **Errori** per indagare e intraprendere azioni appropriate una volta gestita la causa originale:

* **Dettagli errore**
Apre una finestra per visualizzare **Messaggio di errore**, **Passaggio e &#x200B;** Stack errori**.

* **Cronologia elementi aperti**
Mostra i dettagli della cronologia del flusso di lavoro.

* **Ritenta passaggio** Esegue nuovamente lo script del passaggio dell’istanza del componente. Utilizza il comando Ritenta passaggio dopo aver risolto la causa dell’errore originale. Ad esempio, prova a ripetere il passaggio dopo aver corretto un bug nello script eseguito dal passaggio del processo.
* **Termina** Termina il flusso di lavoro se l’errore ha causato una situazione inconciliabile per il flusso di lavoro. Ad esempio, il flusso di lavoro può basarsi su condizioni ambientali quali le informazioni nell’archivio che non sono più valide per l’istanza del flusso di lavoro.
* **Termina e riprova** è simile a **Termina** tranne per il fatto che una nuova istanza di flusso di lavoro viene avviata utilizzando il payload, il titolo e la descrizione originali.

Per approfondire gli errori, quindi riprendere o terminare il flusso di lavoro in seguito, utilizza i seguenti passaggi:

1. Tramite navigazione, seleziona **Strumenti**, quindi **Flusso di lavoro**.

1. Seleziona **Errori** per visualizzare l’elenco delle istanze del flusso di lavoro che non sono state completate correttamente.
1. Seleziona un elemento specifico, quindi l’azione appropriata:

![workflow-failure](/help/sites-cloud/administering/assets/workflow-failure.png)

## Rimozione regolare delle istanze del flusso di lavoro {#regular-purging-of-workflow-instances}

Minimizzare il numero di istanze del flusso di lavoro aumenta le prestazioni del motore del flusso di lavoro, in modo da poter eliminare regolarmente dall’archivio le istanze del flusso di lavoro completate o in esecuzione.

Configura **Configurazione di eliminazione del flusso di lavoro di Adobe Granite** per eliminare le istanze del flusso di lavoro in base all’età e allo stato. È inoltre possibile eliminare le istanze del flusso di lavoro di tutti i modelli o di un modello specifico.

Puoi anche creare più configurazioni del servizio per eliminare le istanze del flusso di lavoro che soddisfano criteri diversi. Ad esempio, crea una configurazione che elimina le istanze di un particolare modello di flusso di lavoro quando restano in esecuzione per molto più tempo del tempo previsto. Crea un’altra configurazione che elimina tutti i flussi di lavoro completati dopo alcuni giorni per ridurre al minino le dimensioni dell’archivio.

Per configurare il servizio, puoi settare i file di configurazione OSGi; vedi [File di configurazione OSGi](/help/implementing/deploying/configuring-osgi.md). Nella tabella seguente sono descritte le proprietà necessarie per entrambi i metodi.

>[!NOTE]
>Per aggiungere la configurazione all’archivio, il PID del servizio è:
>`com.adobe.granite.workflow.purge.Scheduler`
>Poiché si tratta di un servizio di fabbrica, il nome del nodo `sling:OsgiConfig` richiede un suffisso di identificatore, ad esempio:
>`com.adobe.granite.workflow.purge.Scheduler-myidentifier`

| Nome proprietà (console Web) | Nome proprietà OSGi | Descrizione |
|--- |--- |--- |
| Nome processo  | `scheduledpurge.name` | Nome descrittivo per l’eliminazione pianificata. |
| Stato flusso di lavoro | `scheduledpurge.workflowStatus` | Stato delle istanze del flusso di lavoro da eliminare. Valori validi:<br><br>- COMPLETATO: le istanze del flusso di lavoro completate vengono eliminate.<br>- IN ESECUZIONE: le istanze del flusso di lavoro in esecuzione vengono eliminate. |
| Modelli da eliminare | `scheduledpurge.modelIds` | ID dei modelli di flusso di lavoro da eliminare.<br>L&#39;ID è il percorso del nodo del modello, ad esempio:<br> `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model` <br><br> Non specificare alcun valore per eliminare le istanze di tutti i modelli di flusso di lavoro.<br>Per specificare più modelli, fare clic sul pulsante `+` nella console Web. |
| Età del flusso di lavoro | `scheduledpurge.daysold` | Età in giorni delle istanze del flusso di lavoro da eliminare. |
| Pacchetto payload flusso di lavoro | `scheduledpurge.purgePackagePayload` | Indica se il pacchetto di payload deve essere eliminato; `true` o `false`. |


## Impostazione della dimensione massima della casella in entrata {#setting-the-maximum-size-of-the-inbox}

Puoi impostare la dimensione massima della casella in entrata tramite il **Servizio flusso di lavoro di Adobe Granite**; vedi [aggiungi una configurazione OSGi all’archivio](/help/implementing/deploying/configuring-osgi.md). La tabella seguente descrive le proprietà che puoi configurare.

>[!NOTE]
>Per aggiungere la configurazione all’archivio, il PID del servizio è:
>`com.adobe.granite.workflow.core.WorkflowSessionFactory`.

| Nome proprietà (console Web) | Nome proprietà OSGi |
|---|---|
| Dimensione massima query casella in entrata | granite.workflow.inboxQuerySize |

## Utilizzo delle variabili del flusso di lavoro per i datastore di proprietà del cliente {#using-workflow-variables-customer-datastore}

I dati elaborati dai flussi di lavoro vengono memorizzati nell’archiviazione fornita da Adobe (JCR). Per loro natura tali dati possono essere sensibili. È possibile salvare tutti i metadati/dati definiti dall’utente nello spazio di archiviazione personale anziché nell’archiviazione fornita da Adobe. Le presenti sezioni descrivono come configurare queste variabili per l’archiviazione esterna.

### Impostare il modello per l’utilizzo dell’archiviazione esterna dei metadati {#set-model-for-external-storage}

Viene fornito un flag a livello di modello di flusso di lavoro per indicare che tale modello (e le sue istanze di runtime) dispone di archiviazione esterna dei metadati. Le variabili del flusso di lavoro non saranno rese persistenti in JCR per quelle istanze dei modelli contrassegnati per l’archiviazione esterna.

La proprietà *userMetadataPersistenceEnabled* è archiviata nel nodo *jcr:content* del modello di flusso di lavoro. Questo flag è persistente nei metadati del flusso di lavoro come *cq:userMetaDataCustomPersistenceEnabled*.

L’illustrazione seguente mostra come configurare il flag in un flusso di lavoro.

![workflow-externalize-config](/help/sites-cloud/administering/assets/workflow-externalize-config.png)

### API per metadati nell’archiviazione esterna {#apis-for-metadata-external-storage}

Per archiviare le variabili esternamente, devi implementare le API esposte dal flusso di lavoro.

UserMetaDataPersistenceContext

Gli esempi seguenti mostrano come utilizzare l’API.

```
@ProviderType
public interface UserMetaDataPersistenceContext {
 
    /**
     * Gets the workflow for persistence
     * @return workflow
     */
    Workflow getWorkflow();
 
    /**
     * Gets the workflow id for persistence
     * @return workflowId
     */
    String getWorkflowId();
 
    /**
     * Gets the user metadata persistence id
     * @return userDataId
     */
    String getUserDataId();
}
```

UserMetaDataPersistenceProvider

```
/**
 * This provider can be implemented to store the user defined workflow-data metadata in a custom storage location
 */
@ConsumerType
public interface UserMetaDataPersistenceProvider {
 
   /**
    * Retrieves the metadata using a unique identifier
    * @param userMetaDataPersistenceContext
    * @param metaDataMap of user defined workflow data metaData
    * @throws WorkflowException
    */
   void get(UserMetaDataPersistenceContext userMetaDataPersistenceContext, MetaDataMap metaDataMap) throws WorkflowException;
 
   /**
    * Stores the given metadata to the custom storage location
    * @param userMetaDataPersistenceContext
    * @param metaDataMap metadata map
    * @return the unique identifier that can be used to retrieve metadata. If null is returned, then workflowId is used.
    * @throws WorkflowException
    */
   String put(UserMetaDataPersistenceContext userMetaDataPersistenceContext, MetaDataMap metaDataMap) throws WorkflowException;
 
} 
```
