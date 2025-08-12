---
title: Replica
description: Scopri la distribuzione e la risoluzione dei problemi di replica in AEM as a Cloud Service.
exl-id: c84b4d29-d656-480a-a03a-fbeea16db4cd
feature: Operations
role: Admin
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '1711'
ht-degree: 31%

---

# Replica {#replication}

Adobe Experience Manager as a Cloud Service utilizza la funzionalità [Distribuzione contenuto Sling](https://sling.apache.org/documentation/bundles/content-distribution.html) per spostare il contenuto da replicare in un servizio pipeline eseguito su Adobe Developer che si trova al di fuori del runtime AEM.

>[!NOTE]
>
>Leggi [Distribuzione](/help/overview/architecture.md#content-distribution) per ulteriori informazioni.

## Metodi di pubblicazione dei contenuti {#methods-of-publishing-content}

>[!NOTE]
>
>Se ti interessa pubblicare contenuti in blocco, crea un flusso di lavoro utilizzando il [Passaggio del flusso di lavoro di attivazione struttura](#tree-activation), che può gestire in modo efficiente payload di grandi dimensioni.
>&#x200B;>Si sconsiglia di creare un codice personalizzato per la pubblicazione in blocco.
>&#x200B;>Se devi personalizzare per qualsiasi motivo, puoi attivare un flusso di lavoro con questo passaggio utilizzando API di flusso di lavoro esistenti.
>&#x200B;>È sempre buona prassi pubblicare solo i contenuti che devono essere pubblicati. E fai attenzione a non pubblicare un gran numero di contenuti, se non è necessario. Tuttavia, non vi sono limiti alla quantità di contenuto che è possibile inviare tramite flussi di lavoro con il passaggio Flusso di lavoro di attivazione struttura.

### Annullamento/pubblicazione rapida - Annullamento/pubblicazione pianificata {#publish-unpublish}

Questa funzione ti consente di pubblicare immediatamente le pagine selezionate, senza le opzioni aggiuntive possibili con l’approccio Gestisci pubblicazione.

Per ulteriori informazioni, consulta [Gestisci pubblicazione](/help/sites-cloud/authoring/sites-console/publishing-pages.md#manage-publication).

### Tempi di attivazione e disattivazione - Configurazione dell’attivatore {#on-and-off-times-trigger-configuration}

Sono disponibili possibilità aggiuntive di **Ora di attivazione** e **Ora di disattivazione** dalla [scheda Base delle Proprietà pagina](/help/sites-cloud/authoring/sites-console/page-properties.md#basic).

Per realizzare la replica automatica per questa funzionalità, abilitare **Replica automatica** nella [configurazione OSGi](/help/implementing/deploying/configuring-osgi.md) **Configurazione attivazione/disattivazione**:

![Configurazione attivazione/disattivazione OSGi](/help/operations/assets/replication-on-off-trigger.png)

### Gestisci pubblicazione  {#manage-publication}

Gestisci pubblicazione offre più opzioni rispetto alla Pubblicazione rapida e consente di includere pagine figlie, personalizzare i riferimenti, avviare tutti i flussi di lavoro applicabili e pubblicare successivamente.

L’inclusione degli elementi secondari di una cartella per l’opzione &quot;Pubblica più tardi&quot; richiama il flusso di lavoro Pubblica struttura del contenuto descritto in questo articolo.

Puoi trovare informazioni più dettagliate su Gestisci pubblicazione nella sezione [Documentazione di base sulla pubblicazione](/help/sites-cloud/authoring/sites-console/publishing-pages.md#manage-publication).

### Passaggio del flusso di lavoro di attivazione struttura {#tree-activation}

Il passaggio del flusso di lavoro Attivazione albero ha lo scopo di replicare in modo performante una gerarchia profonda di nodi di contenuto. Si interrompe automaticamente quando la coda diventa troppo grande per consentire ad altre repliche di procedere in parallelo con latenza minima.

Creare un modello di flusso di lavoro che utilizza il passaggio del processo `TreeActivation`:

1. Dalla home page di AEM as a Cloud Service, vai a **Strumenti - Flusso di lavoro - Modelli**.
1. Nella pagina Modelli di flusso di lavoro, premi **Crea** nell&#39;angolo superiore destro dello schermo.
1. Aggiungi un titolo e un nome al modello. Per ulteriori informazioni, vedere [Creazione di modelli di flussi di lavoro](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=it).
1. Selezionare il modello creato dall&#39;elenco e premere **Modifica**
1. Nella finestra seguente, eliminare il passo visualizzato per impostazione predefinita
1. Trascinate il passo del processo nel flusso del modello corrente:

   ![Passaggio processo](/help/operations/assets/processstep.png)

1. Selezionare il passaggio Processo nel flusso e selezionare **Configura** premendo l&#39;icona chiave inglese.
1. Seleziona la scheda **Processo** e seleziona `Publish Content Tree` dall&#39;elenco a discesa, quindi seleziona la casella di controllo **Avanzamento gestore**

   ![Attivazione struttura](/help/operations/assets/new-treeactivationstep.png)

1. Imposta eventuali parametri aggiuntivi nel campo **Argomenti**. Più argomenti separati da virgole possono essere uniti tra loro. Esempio:

   `enableVersion=false,agentId=publish,chunkSize=50,maxTreeSize=500000,dryRun=false,filters=onlyModified,maxQueueSize=10`

   >[!NOTE]
   >
   >Per l’elenco dei parametri, consulta la sezione **Parametri** di seguito.

1. Premi **Fine** per salvare il modello di flusso di lavoro.

**Parametri**

| Nome | predefinito | descrizione |
| -------------- | ------- | --------------------------------------------------------------- |
| percorso |         | percorso principale da cui iniziare |
| agentId | pubblicazione | Nome dell’agente di replica da utilizzare |
| chunkSize | 50 | Numero di percorsi da raggruppare in una singola replica |
| maxTreeSize | 500000 | Numero massimo di nodi per una struttura da considerare di piccole dimensioni |
| maxQueueSize | 10 | Numero massimo di elementi nella coda di replica |
| enableVersion | false | Abilita controllo delle versioni |
| dryRun | false | Se è impostato su true, la replica non viene chiamata |
| userId |         | solo per il lavoro. Nel flusso di lavoro viene utilizzato l’utente che chiama il flusso di lavoro |
| filtri |         | Elenco dei nomi dei filtri dei nodi. Vedi il filtro supportato di seguito |

**Filtri di supporto**

| Nome | Descrizione |
| ------------- | ------------------------------------------- |
| onlyModified | Nodi: sia nuovi che preesistenti che sono stati modificati dall’ultima pubblicazione |
| onlyActivated | Nodi: pubblicati prima dell’ultima pubblicazione |


**Supporto per la ripresa in seguito a interruzioni**

Il flusso di lavoro elabora il contenuto in blocchi, ciascuno dei quali rappresenta un sottoinsieme del contenuto completo da pubblicare.  Se il flusso di lavoro viene interrotto dal sistema, continuerà da dove è stato interrotto.

**Monitoraggio dell&#39;avanzamento del flusso di lavoro**

1. Dalla home page di AEM as a Cloud Service, vai a **Strumenti - Generale - Processi**.
1. Osserva la riga corrispondente al flusso di lavoro. La colonna *progress* fornisce un&#39;indicazione dell&#39;avanzamento della replica. Ad esempio, può visualizzare 41/564 e, dopo l’aggiornamento, può essere aggiornato a 52/564.

   ![Stato attivazione albero](/help/operations/assets/treeactivation-progress.png)


1. Selezionando e aprendo la riga verranno forniti ulteriori dettagli sullo stato dell’esecuzione del flusso di lavoro.

   ![Dettagli stato attivazione albero](/help/operations/assets/treeactivation-progress-details.png)



### Flusso di lavoro della struttura dei contenuti di pubblicazione {#publish-content-tree-workflow}

>[!NOTE]
>
>Questa funzione è stata sostituita dal passaggio Attivazione albero più performante, che può essere incluso in un flusso di lavoro personalizzato.

+++ Fai clic qui per ulteriori informazioni su questa funzione obsoleta.

È possibile attivare una replica della struttura scegliendo **Strumenti - Flusso di lavoro - Modelli** e copiando il modello di flusso di lavoro preconfigurato **Pubblica struttura contenuto**, come mostrato di seguito:

![Scheda Flusso Di Lavoro Pubblica Struttura Contenuto](/help/operations/assets/publishcontenttreeworkflow.png)

Non richiamare il modello originale. Assicurati invece di copiare prima il modello e richiamare tale copia.

Come tutti i flussi di lavoro, può anche essere richiamato tramite API. Per ulteriori informazioni, vedere [Interazione con i flussi di lavoro a livello di programmazione](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-program-interaction.html?lang=it#extending-aem).

In alternativa, è possibile creare un modello di flusso di lavoro che utilizza il passaggio del processo `Publish Content Tree`.

1. Dalla home page di AEM as a Cloud Service, vai a **Strumenti - Flusso di lavoro - Modelli**.
1. Nella pagina Modelli di flusso di lavoro, premi **Crea** nell&#39;angolo superiore destro dello schermo.
1. Aggiungi un titolo e un nome al modello. Per ulteriori informazioni, vedere [Creazione di modelli di flussi di lavoro](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=it).
1. Selezionare il modello creato dall&#39;elenco e premere **Modifica**
1. Nella finestra successiva, trascina e rilascia il Passaggio del processo nel flusso del modello corrente:

   ![Passaggio processo](/help/operations/assets/processstep.png)

1. Selezionare il passaggio Processo nel flusso e selezionare **Configura** premendo l&#39;icona chiave inglese.
1. Seleziona la scheda **Processo** e seleziona `Publish Content Tree` dall&#39;elenco a discesa, quindi seleziona la casella di controllo **Avanzamento gestore**

   ![Attivazione struttura](/help/operations/assets/newstep.png)

1. Imposta eventuali parametri aggiuntivi nel campo **Argomenti**. Più argomenti separati da virgole possono essere uniti tra loro. Esempio:

   `enableVersion=true,agentId=publish,includeChildren=true`


   >[!NOTE]
   >
   >Per l’elenco dei parametri, consulta la sezione **Parametri** di seguito.

1. Premi **Fine** per salvare il modello di flusso di lavoro.

**Parametri**

* `includeChildren` (valore booleano, predefinito: `false`). Il valore `false` indica che viene pubblicato solo il percorso; `true` indica che vengono pubblicati anche gli elementi secondari.
* `replicateAsParticipant` (valore booleano, predefinito: `false`). Se configurata come `true`, la replica utilizza `userid` dell’entità principale che ha eseguito il Passaggio partecipante.
* `enableVersion` (valore booleano, predefinito: `false`). Questo parametro determina se viene creata una nuova versione al momento della replica.
* `agentId` (valore stringa, “default” indica che vengono utilizzati solo gli agenti per la pubblicazione). Si consiglia di impostare un valore esplicito per agentId; ad esempio: publish. L&#39;impostazione dell&#39;agente su `preview` consente di eseguire le pubblicazioni nel servizio di anteprima.
* `filters` (valore stringa, il valore predefinito indica che tutti i percorsi sono attivati). I valori disponibili sono:
   * `onlyActivated` - attiva solo le pagine che sono (già) state attivate. Agisce come una forma di riattivazione.
   * `onlyModified`: verranno attivati solo i percorsi già attivati e la cui data di modifica è successiva alla data di attivazione.
   * Quanto sopra può essere impostato con OR inserendo il simbolo “|”. Esempio: `onlyActivated|onlyModified`.

**Registrazione**

All&#39;avvio del passaggio del flusso di lavoro di attivazione della struttura, i parametri di configurazione vengono registrati nel loglevel INFO. Un’istruzione INFO viene registrata anche qando i percorsi vengono attivati.

Dopo che il passaggio del flusso di lavoro ha replicato tutti i percorsi, viene registrata un’istruzione INFO finale.

Inoltre, è possibile aumentare il loglevel dei logger al di sotto di `com.day.cq.wcm.workflow.process.impl` a DEBUG/TRACE per ottenere ulteriori informazioni di registro.

In caso di errori, il passaggio del flusso di lavoro termina con `WorkflowException`, in cui viene racchiusa l&#39;eccezione sottostante.

Di seguito sono riportati alcuni esempi di registri generati durante un flusso di lavoro della struttura dei contenuti di pubblicazione di esempio:

```
21.04.2021 19:14:55.566 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.treeactivation.TreeActivationWorkflowProcess TreeActivation options: replicateAsParticipant=false(userid=workflow-process-service), agentId=publish, chunkSize=100, filter=, enableVersion=false
```

```
21.04.2021 19:14:58.541 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.ChunkedReplicator closing chunkedReplication-VolatileWorkItem_node1_var_workflow_instances_server60_2021-04-20_brian-tree-replication-test-2_1, 17 paths replicated in 2971 ms
```

+++

### API di replica {#replication-api}

Puoi pubblicare il contenuto utilizzando l’API di replica disponibile in AEM as a Cloud Service.

Per ulteriori informazioni, consulta la [documentazione dell’API](https://javadoc.io/doc/com.adobe.aem/aem-sdk-api/latest/com/day/cq/replication/package-summary.html).

**Utilizzo di base dell’API**

```
@Reference
Replicator replicator;
@Reference
ReplicationStatusProvider replicationStatusProvider;

....
Session session = ...
// Activate a single page to all agents, which are active by default
replicator.replicate(session,ReplicationActionType.ACTIVATE,"/content/we-retail/en");
// Activate multiple pages (but try to limit it to approx 100 at max)
replicator.replicate(session,ReplicationActionType.ACTIVATE, new String[]{"/content/we-retail/en","/content/we-retail/de"});

// ways to get the replication status
Resource enResource = resourceResolver.getResource("/content/we-retail/en");
Resource deResource = resourceResolver.getResource("/content/we-retail/de");
ReplicationStatus enStatus = enResource.adaptTo(ReplicationStatus.class);
// if you need to get the status for more more than 1 resource at once, this approach is more performant
Map<String,ReplicationStatus> allStatus = replicationStatusProvider.getBatchReplicationStatus(enResource,deResource);
```

**Replica con agenti specifici**

Durante la replica delle risorse, come nell’esempio precedente, vengono utilizzati solo gli agenti attivi per impostazione predefinita. In AEM as a Cloud Service, significa solo l’agente denominato &quot;publish&quot;, che collega il livello di authoring a quello di pubblicazione.

Per supportare la funzionalità di anteprima, è stato aggiunto un nuovo agente denominato “preview”, che non è attivo per impostazione predefinita. Questo agente viene utilizzato per collegare il livello di authoring a quello di anteprima. Se si desidera eseguire la replica solo tramite l&#39;agente preview, è necessario selezionare esplicitamente l&#39;agente preview tramite `AgentFilter`.

Vedi l’esempio seguente:

```
private static final String PREVIEW_AGENT = "preview";

ReplicationStatus beforeStatus = enResource.adaptTo(ReplicationStatus.class); // beforeStatus.isActivated == false

ReplicationOptions options = new ReplicationOptions();
options.setFilter(new AgentFilter() {
  @Override
  public boolean isIncluded (Agent agent) {
    return agent.getId().equals(PREVIEW_AGENT);
  }
});
// will replicate only to preview
replicator.replicate(session,ReplicationActionType.ACTIVATE,"/content/we-retail/en", options);

ReplicationStatus afterStatus = enResource.adaptTo(ReplicationStatus.class); // afterStatus.isActivated == false
ReplicationStatus previewStatus = afterStatus.getStatusForAgent(PREVIEW_AGENT); // previewStatus.isActivated == true
```

Nel caso in cui non si fornisca un filtro di questo tipo e si utilizzi solo l’agente “publish”, l’agente “preview” non viene utilizzato e l’azione di replica non influisce sul livello di anteprima.

Lo stato `ReplicationStatus` complessivo di una risorsa viene modificato solo se l’azione di replica include almeno un agente attivo per impostazione predefinita. Nell’esempio precedente, questo flusso non si è verificato. La replica utilizzava solo l’agente &quot;preview&quot;. Pertanto, è necessario utilizzare il nuovo metodo `getStatusForAgent()`, che consente di eseguire una query sullo stato di un agente specifico. Questo metodo funziona anche per l’agente “publish”. Se è stata eseguita un’azione di replica utilizzando l’agente fornito, viene restituito un valore non-null.

### Metodi di invalidazione dei contenuti {#invalidating-content}

Puoi annullare direttamente la validità del contenuto utilizzando l’Invalidazione dei contenuti Sling (SCD) dall’authoring (metodo preferito) o utilizzando l’API di replica per richiamare l’agente di svuotamento del Dispatcher di pubblicazione. Per ulteriori dettagli, vedere la pagina [Memorizzazione in cache](/help/implementing/dispatcher/caching.md).

**Limiti di capacità dell’API di replica**

Replica meno di 100 percorsi alla volta; il limite massimo consentito è 500. Al di sopra del limite, viene generato un `ReplicationException`.
Se la logica dell&#39;applicazione non richiede la replica atomica, questo limite può essere superato impostando `ReplicationOptions.setUseAtomicCalls` su false, che accetta qualsiasi numero di percorsi, ma crea internamente dei bucket al fine di rimanere al di sotto di questo limite.

La dimensione del contenuto trasmesso per chiamata di replica non deve superare i `10 MB`. Questa regola include i nodi e le proprietà, ma non eventuali dati binari (i pacchetti di flusso di lavoro e i pacchetti di contenuto sono considerati dati binari).


## Risoluzione dei problemi {#troubleshooting}

Per risolvere i problemi di replica, accedi alle code di replica nell’interfaccia web del servizio AEM Author:

1. Dalla [Navigazione globale](/help/sites-cloud/authoring/basic-handling.md#global-navigation) di AEM, passa a **Strumenti** > **Distribuzione** > **Distribuzione**
1. Seleziona la scheda **Pubblica**.

   ![Stato](assets/publish-status.png "Stato")

1. Controlla lo stato della coda, che dovrebbe essere verde.
1. È possibile verificare la connessione al servizio di replica
1. Seleziona la scheda **Registri** che mostra la cronologia delle pubblicazioni di contenuti

![Registri](assets/publish-logs.png "Registri")

Se non è stato possibile pubblicare il contenuto, l’intera pubblicazione viene ripristinata da AEM Publish Service.

In tal caso, la coda principale modificabile presenta uno stato rosso e deve essere rivista per identificare gli elementi che hanno causato l’annullamento della pubblicazione. Facendo clic su tale coda, vengono visualizzati i relativi elementi in sospeso, da cui è possibile cancellare un singolo elemento o tutti gli elementi, se necessario.
