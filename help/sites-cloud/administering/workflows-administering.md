---
title: Amministrazione delle istanze dei flussi di lavoro
description: Scopri come amministrare le istanze dei flussi di lavoro
translation-type: tm+mt
source-git-commit: c19079b1be36c4e87962491f263ddf97ab98f831
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 0%

---


# Amministrazione delle istanze dei flussi di lavoro {#administering-workflow-instances}

La console del flusso di lavoro offre diversi strumenti per l’amministrazione delle istanze del flusso di lavoro, in modo da garantirne l’esecuzione come previsto.

Sono disponibili diverse console per la gestione dei flussi di lavoro. Utilizza la navigazione [](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation) globale per aprire il riquadro **Strumenti** , quindi seleziona **Flusso di lavoro**:

* **Modelli**: Gestione delle definizioni dei flussi di lavoro
* **Istanze**: Visualizzare e gestire le istanze del flusso di lavoro in esecuzione
* **Avviatori**: Gestione delle modalità di avvio dei flussi di lavoro
* **Archivia**: Visualizzare la cronologia dei flussi di lavoro completati con successo
* **Errori**: Visualizza cronologia dei flussi di lavoro completati con errori
* **Assegnazione** automatica: Configurare l&#39;assegnazione automatica dei flussi di lavoro ai modelli

## Monitoraggio dello stato delle istanze del flusso di lavoro {#monitoring-the-status-of-workflow-instances}

1. Utilizzando Navigazione selezionare **Strumenti**, quindi **Flusso di lavoro**.
1. Selezionate **Istanze** per visualizzare l&#39;elenco delle istanze del flusso di lavoro attualmente in corso.

   ![wf-97](/help/sites-cloud/administering/assets/wf-97.png)


## Cerca istanze flusso di lavoro {#search-workflow-instances}

1. Utilizzando Navigazione selezionare **Strumenti**, quindi **Flusso di lavoro**.
1. Selezionate **Istanze** per visualizzare l&#39;elenco delle istanze del flusso di lavoro attualmente in corso. Nella barra superiore, nell’angolo sinistro, selezionare **Filtri**. In alternativa, è possibile utilizzare i tasti Alt+1. Viene visualizzata la finestra di dialogo seguente:

   ![wf-99-1](/help/sites-cloud/administering/assets/wf-99-1.png)

1. Nella finestra di dialogo Filtro, selezionate i criteri di ricerca del flusso di lavoro. Potete effettuare ricerche in base ai seguenti input:

   * Percorso payload: Selezionare un percorso specifico
   * Modello flusso di lavoro: Selezionare un modello di workflow
   * Assegnatario: Selezionare un assegnatario del flusso di lavoro
   * Tipo: Attività, elemento del flusso di lavoro o errore del flusso di lavoro
   * Stato attività: Attivo, Completo o Terminato
   * Dove Sono: Proprietario e assegnatario, solo Proprietario, solo Assegnatario
   * Data inizio: Data di inizio prima o dopo una data specificata
   * Data di fine: Data di fine prima o dopo una data specificata
   * Data scadenza: Data di scadenza prima o dopo una data specificata
   * Data aggiornamento: Data di aggiornamento prima o dopo una data specificata

## Sospensione, ripresa e chiusura di un’istanza del flusso di lavoro {#suspending-resuming-and-terminating-a-workflow-instance}

1. Utilizzando Navigazione selezionare **Strumenti**, quindi **Flusso di lavoro**.
1. Selezionate **Istanze** per visualizzare l&#39;elenco delle istanze del flusso di lavoro attualmente in corso.

   ![wf-96-1](/help/sites-cloud/administering/assets/wf-96-1.png)

1. Selezionate un elemento specifico, quindi utilizzate **Termina**, **Sospendi** o **Riprendi**, a seconda dei casi; sono necessari conferma e/o ulteriori dettagli:

   ![wf-97-1](/help/sites-cloud/administering/assets/wf-97-1.png)

## Visualizzazione dei flussi di lavoro archiviati {#viewing-archived-workflows}

1. Utilizzando Navigazione selezionare **Strumenti**, quindi **Flusso di lavoro**.

1. Selezionare **Archivia** per visualizzare l&#39;elenco delle istanze del flusso di lavoro completate correttamente.

   ![wf-98](/help/sites-cloud/administering/assets/wf-98.png)

   >[!NOTE]
   >Lo stato di interruzione è considerato come una cessazione riuscita, in quanto si verifica a seguito di un&#39;azione dell&#39;utente; ad esempio:
   >
   >* utilizzo dell&#39;azione **Terminate**
   >* quando una pagina, soggetta a un flusso di lavoro, viene (forzata) eliminata, il flusso di lavoro viene terminato


1. Selezionate un elemento specifico, quindi **Apri cronologia** per visualizzare ulteriori dettagli:

   ![wf-99](/help/sites-cloud/administering/assets/wf-99.png)

## Correzione degli errori di istanza del flusso di lavoro {#fixing-workflow-instance-failures}

In caso di errore di un flusso di lavoro, AEM fornisce la console **Errori** per consentire di esaminare e intraprendere le azioni appropriate una volta gestita la causa originale:

* **Dettagli** errore Apre una finestra per visualizzare 
**Messaggio** di errore, **passo** e **stack** di errore.

* **Cronologia** di apertura Mostra i dettagli della cronologia del flusso di lavoro.

* **Riprova** esegue di nuovo l&#39;istanza del componente Passaggio script. Dopo aver risolto la causa dell’errore originale, usate il comando Ritenta passo. Ad esempio, ripetere il passaggio dopo aver corretto un bug nello script eseguito dal passaggio di elaborazione.
* **Terminare** Terminare il flusso di lavoro se l&#39;errore ha causato una situazione inconciliabile per il flusso di lavoro. Ad esempio, il flusso di lavoro può dipendere da condizioni ambientali, come le informazioni presenti nell&#39;archivio che non sono più valide per l&#39;istanza del flusso di lavoro.
* **Termina e Riprova** Simili a **Termina** , con la differenza che una nuova istanza del flusso di lavoro viene avviata utilizzando il payload, il titolo e la descrizione originali.

Per indagare sugli errori, quindi riprendere o terminare il flusso di lavoro in seguito, attenetevi alla seguente procedura:

1. Utilizzando Navigazione selezionare **Strumenti**, quindi **Flusso di lavoro**.

1. Selezionate **Errori** per visualizzare l&#39;elenco delle istanze del flusso di lavoro che non sono state completate correttamente.
1. Selezionate un elemento specifico, quindi l’azione appropriata:

   ![wf-47](/help/sites-cloud/administering/assets/wf-47.png)

## Rimozione regolare delle istanze del flusso di lavoro {#regular-purging-of-workflow-instances}

Riducendo il numero di istanze del flusso di lavoro si ottengono maggiori prestazioni nel motore del flusso di lavoro, è possibile eliminare regolarmente dal repository le istanze del flusso di lavoro completate o in esecuzione.

Configurare **configurazione** Adobe di rimozione del flusso di lavoro Granite per eliminare le istanze del flusso di lavoro in base alla loro età e stato. Potete anche eliminare le istanze del flusso di lavoro di tutti i modelli o di un modello specifico.

Potete anche creare più configurazioni del servizio per eliminare le istanze del flusso di lavoro che soddisfano criteri diversi. Ad esempio, create una configurazione che svuota le istanze di un particolare modello di flusso di lavoro quando sono in esecuzione per un periodo molto più lungo del tempo previsto. Create un&#39;altra configurazione che eliminerà tutti i flussi di lavoro completati dopo un certo numero di giorni per ridurre al minimo le dimensioni del repository.

Per configurare il servizio, potete configurare i file di configurazione OSGi; vedete File di configurazione [OSGi](/help/implementing/deploying/configuring-osgi.md). Nella tabella seguente sono descritte le proprietà necessarie per entrambi i metodi.

>[!NOTE]
>Per aggiungere la configurazione al repository, il servizio PID è:
>`com.adobe.granite.workflow.purge.Scheduler`
>Poiché il servizio è un servizio factory, il nome del `sling:OsgiConfig` nodo richiede un suffisso di identificatore, ad esempio:
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
   <td>Un nome descrittivo per la rimozione pianificata.</td>
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
   <td>Modelli Da Rimuovere</td>
   <td>scheduledpurge.modelIds</td>
   <td><p>ID dei modelli di workflow da eliminare. L'ID è il percorso del nodo del modello, ad esempio:<br /> /conf/global/settings/workflow/models/dam/update_asset/jcr:content/model<br /> Non specificare alcun valore per eliminare le istanze di tutti i modelli di workflow.</p> <p>Per specificare più modelli, fate clic sul pulsante + nella console Web. </p> </td>
  </tr>
  <tr>
   <td>Età flusso di lavoro</td>
   <td>scheduledpurge.daysold</td>
   <td>Età delle istanze del flusso di lavoro da eliminare, espressa in giorni.</td>
  </tr>
 </tbody>
</table>

## Impostazione della dimensione massima della casella in entrata {#setting-the-maximum-size-of-the-inbox}

Per impostare la dimensione massima della inbox, configurare il servizio **** Adobe Granite Workflow Service [. Consultate](/help/implementing/deploying/configuring-osgi.md)aggiungere una configurazione OSGi alla directory archivio. La tabella seguente descrive la proprietà configurata.

>[!NOTE]
>Per aggiungere la configurazione al repository, il servizio PID è:
>`com.adobe.granite.workflow.core.WorkflowSessionFactory`.

| Nome proprietà (console Web) | Nome proprietà OSGi |
|---|---|
| Dimensione massima query Posta in arrivo | granite.workflow.inboxQuerySize |

