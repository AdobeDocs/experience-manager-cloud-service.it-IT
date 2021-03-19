---
title: Amministrazione delle istanze dei flussi di lavoro
description: Scopri come amministrare le istanze dei flussi di lavoro
feature: Amministrazione
role: Administrator
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 1%

---


# Amministrazione delle istanze dei flussi di lavoro {#administering-workflow-instances}

La console del flusso di lavoro fornisce diversi strumenti per l’amministrazione delle istanze del flusso di lavoro, in modo che vengano eseguite come previsto.

Sono disponibili diverse console per l’amministrazione dei flussi di lavoro. Utilizza la [navigazione globale](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation) per aprire il riquadro **Strumenti**, quindi seleziona **Flusso di lavoro**:

* **Modelli**: Gestire le definizioni dei flussi di lavoro
* **Istanze**: Visualizzare e gestire le istanze del flusso di lavoro in esecuzione
* **Lanci**: Gestire il modo in cui avviare i flussi di lavoro
* **Archivia**: Visualizzare la cronologia dei flussi di lavoro completati correttamente
* **Errori**: Visualizzare la cronologia dei flussi di lavoro completati con errori
* **Assegnazione** automatica: Configurare l’assegnazione automatica dei flussi di lavoro ai modelli

## Monitoraggio dello stato delle istanze del flusso di lavoro {#monitoring-the-status-of-workflow-instances}

1. Utilizzando Navigazione selezionare **Strumenti**, quindi **Flusso di lavoro**.
1. Seleziona **Istanze** per visualizzare l&#39;elenco delle istanze del flusso di lavoro attualmente in corso.

   ![wf-97](/help/sites-cloud/administering/assets/wf-97.png)


## Cerca istanze del flusso di lavoro {#search-workflow-instances}

1. Utilizzando Navigazione selezionare **Strumenti**, quindi **Flusso di lavoro**.
1. Seleziona **Istanze** per visualizzare l&#39;elenco delle istanze del flusso di lavoro attualmente in corso. Nella barra superiore, nell’angolo sinistro, seleziona **Filtri**. In alternativa, è possibile utilizzare i tasti alt+1. Viene visualizzata la seguente finestra di dialogo:

   ![wf-99-1](/help/sites-cloud/administering/assets/wf-99-1.png)

1. Nella finestra di dialogo Filtro , seleziona i criteri di ricerca del flusso di lavoro. Puoi eseguire ricerche in base ai seguenti input:

   * Percorso payload: Selezionare un percorso specifico
   * Modello di flusso di lavoro: Selezionare un modello di flusso di lavoro
   * Assegnatario: Selezionare un assegnatario del flusso di lavoro
   * Tipo: Attività, elemento del flusso di lavoro o errore del flusso di lavoro
   * Stato attività: Attivo, Completo o Terminato
   * Dove Sono: Proprietario e assegnatario, solo proprietario, solo assegnatario
   * Data di inizio: Data di inizio prima o dopo una data specificata
   * Data di fine: Data di fine prima o dopo una data specificata
   * Data di scadenza: Data di scadenza prima o dopo una data specificata
   * Data aggiornamento: Data aggiornata prima o dopo una data specificata

## Sospensione, ripresa e terminazione di un&#39;istanza di flusso di lavoro {#suspending-resuming-and-terminating-a-workflow-instance}

1. Utilizzando Navigazione selezionare **Strumenti**, quindi **Flusso di lavoro**.
1. Seleziona **Istanze** per visualizzare l&#39;elenco delle istanze del flusso di lavoro attualmente in corso.

   ![wf-96-1](/help/sites-cloud/administering/assets/wf-96-1.png)

1. Seleziona un elemento specifico, quindi utilizza **Termina**, **Sospendi** o **Riprendi**, a seconda dei casi; conferma e/o ulteriori dettagli sono richiesti:

   ![wf-97-1](/help/sites-cloud/administering/assets/wf-97-1.png)

## Visualizzazione dei flussi di lavoro archiviati {#viewing-archived-workflows}

1. Utilizzando Navigazione selezionare **Strumenti**, quindi **Flusso di lavoro**.

1. Seleziona **Archivia** per visualizzare l&#39;elenco delle istanze del flusso di lavoro completate correttamente.

   ![wf-98](/help/sites-cloud/administering/assets/wf-98.png)

   >[!NOTE]
   >Lo stato di interruzione viene considerato come una terminazione corretta in quanto si verifica in seguito a un&#39;azione dell&#39;utente; ad esempio:
   >
   >* utilizzo dell&#39;azione **Termina**
   >* quando una pagina, soggetta a un flusso di lavoro, viene (forzata) eliminata, il flusso di lavoro viene terminato


1. Seleziona un elemento specifico, quindi **Apri cronologia** per visualizzare ulteriori dettagli:

   ![wf-99](/help/sites-cloud/administering/assets/wf-99.png)

## Correzione degli errori di istanza del flusso di lavoro {#fixing-workflow-instance-failures}

Quando un flusso di lavoro non riesce, AEM fornisce la console **Errori** per indagare e intraprendere azioni appropriate una volta gestita la causa originale:

* **Errore**
DettagliApre una finestra per visualizzare 
**Messaggio** di errore,  **** Stepand  **Failure Stack**.

* **Apri**
cronologiaMostra i dettagli della cronologia del flusso di lavoro.

* **Riprova** StepEsegue di nuovo l&#39;istanza del componente Passaggio script. Utilizzare il comando Riprova passaggio dopo aver risolto la causa dell&#39;errore originale. Ad esempio, prova a ripetere il passaggio dopo aver corretto un bug nello script eseguito dal passaggio del processo.
* **** TerminareTerminare il flusso di lavoro se l’errore ha causato una situazione inconciliabile per il flusso di lavoro. Ad esempio, il flusso di lavoro può basarsi su condizioni ambientali quali le informazioni nell’archivio che non sono più valide per l’istanza del flusso di lavoro.
* **Termina e** RiprovaSimile a  **** Terminateeccetto per il fatto che una nuova istanza di flusso di lavoro viene avviata utilizzando il payload, il titolo e la descrizione originali.

Per indagare gli errori, quindi riprendere o terminare il flusso di lavoro in seguito, utilizza i seguenti passaggi:

1. Utilizzando Navigazione selezionare **Strumenti**, quindi **Flusso di lavoro**.

1. Selezionare **Errori** per visualizzare l&#39;elenco delle istanze del flusso di lavoro che non sono state completate correttamente.
1. Seleziona un elemento specifico, quindi l’azione appropriata:

   ![wf-47](/help/sites-cloud/administering/assets/wf-47.png)

## Rimozione regolare delle istanze del flusso di lavoro {#regular-purging-of-workflow-instances}

Minimizzare il numero di istanze del flusso di lavoro aumenta le prestazioni del motore del flusso di lavoro, in modo da poter eliminare regolarmente dall’archivio le istanze del flusso di lavoro completate o in esecuzione.

Configura **Adobe Granite Workflow Purge Configuration** per eliminare le istanze del flusso di lavoro in base alla loro età e al loro stato. È inoltre possibile eliminare le istanze del flusso di lavoro di tutti i modelli o di un modello specifico.

Puoi anche creare più configurazioni del servizio per eliminare le istanze del flusso di lavoro che soddisfano criteri diversi. Ad esempio, crea una configurazione che elimina le istanze di un particolare modello di flusso di lavoro quando sono in esecuzione per molto più tempo del tempo previsto. Crea un’altra configurazione che elimina tutti i flussi di lavoro completati dopo un certo numero di giorni per ridurre al minimo le dimensioni dell’archivio.

Per configurare il servizio, puoi configurare i file di configurazione OSGi vedi [File di configurazione OSGi](/help/implementing/deploying/configuring-osgi.md). Nella tabella seguente sono descritte le proprietà necessarie per entrambi i metodi.

>[!NOTE]
>Per aggiungere la configurazione all’archivio, il PID del servizio è:
>`com.adobe.granite.workflow.purge.Scheduler`
>Poiché il servizio è un servizio di fabbrica, il nome del nodo `sling:OsgiConfig` richiede un suffisso di identificazione, ad esempio:
>`com.adobe.granite.workflow.purge.Scheduler-myidentifier`

<table>
 <tbody>
  <tr>
   <th>Nome proprietà (console Web)</th>
   <th>Nome proprietà OSGi</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>Nome processo</td>
   <td>scheduledpurge.name</td>
   <td>Un nome descrittivo per l'eliminazione pianificata.</td>
  </tr>
  <tr>
   <td>Stato flusso di lavoro</td>
   <td>scheduledpurge.workflowStatus</td>
   <td><p>Lo stato delle istanze del flusso di lavoro da eliminare. I seguenti valori sono validi:</p>
    <ul>
     <li>COMPLETATO: Le istanze del flusso di lavoro completate vengono eliminate.</li>
     <li>IN ESECUZIONE: Le istanze del flusso di lavoro in esecuzione vengono eliminate.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Modelli da eliminare</td>
   <td>scheduledpurge.modelIds</td>
   <td><p>ID dei modelli di flusso di lavoro da eliminare. L'ID è il percorso del nodo del modello, ad esempio:<br /> /conf/global/settings/workflow/models/dam/update_asset/jcr:content/model<br /> Non specificare alcun valore per eliminare le istanze di tutti i modelli di flusso di lavoro.</p> <p>Per specificare più modelli, fare clic sul pulsante + nella console Web. </p> </td>
  </tr>
  <tr>
   <td>Età del flusso di lavoro</td>
   <td>scheduledpurge.daysold</td>
   <td>L’età in giorni delle istanze del flusso di lavoro da eliminare.</td>
  </tr>
 </tbody>
</table>

## Impostazione della dimensione massima della casella in entrata {#setting-the-maximum-size-of-the-inbox}

Puoi impostare la dimensione massima della casella in entrata configurando il **Adobe Granite Workflow Service**, vedi [aggiungere una configurazione OSGi all&#39;archivio](/help/implementing/deploying/configuring-osgi.md). Nella tabella seguente viene descritta la proprietà configurata.

>[!NOTE]
>Per aggiungere la configurazione all’archivio, il PID del servizio è:
>`com.adobe.granite.workflow.core.WorkflowSessionFactory`.

| Nome proprietà (console Web) | Nome proprietà OSGi |
|---|---|
| Dimensione massima query casella in entrata | granite.workflow.inboxQuerySize |

