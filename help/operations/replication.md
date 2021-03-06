---
title: Replica
description: Distribuzione e risoluzione dei problemi di replica.
exl-id: c84b4d29-d656-480a-a03a-fbeea16db4cd
source-git-commit: b79752c43cd9907236b511aa1be60b5b2256a7b8
workflow-type: tm+mt
source-wordcount: '1259'
ht-degree: 4%

---

# Replica {#replication}

Adobe Experience Manager as a Cloud Service utilizza [Distribuzione dei contenuti Sling](https://sling.apache.org/documentation/bundles/content-distribution.html) capacità di spostare il contenuto per la replica in un servizio pipeline eseguito su un Adobe I/O che si trova al di fuori del runtime AEM.

>[!NOTE]
>
>Leggi [Distribuzione](/help/overview/architecture.md#content-distribution) per ulteriori informazioni.

## Metodi di pubblicazione dei contenuti {#methods-of-publishing-content}

### Annullamento/pubblicazione rapida - Annullamento/pubblicazione pianificata {#publish-unpublish}

Questo consente di pubblicare immediatamente le pagine selezionate, senza le opzioni aggiuntive possibili con l’approccio Gestisci pubblicazione .

Per ulteriori informazioni, consulta [Gestisci pubblicazione](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#manage-publication).

### Tempi di attivazione e disattivazione - Configurazione dell&#39;attivatore {#on-and-off-times-trigger-configuration}

Le possibilità aggiuntive di **Ora di attivazione** e **Ora di disattivazione** sono disponibili dal [Scheda Base delle Proprietà pagina](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic).

Per realizzare la replica automatica è necessario abilitare **Replica automatica** in [Configurazione OSGi](/help/implementing/deploying/configuring-osgi.md) **Configurazione attivazione/disattivazione**:

![Configurazione trigger OSGi On Off](/help/operations/assets/replication-on-off-trigger.png)

### Gestisci pubblicazione  {#manage-publication}

Gestisci pubblicazione offre più opzioni rispetto alla Pubblicazione rapida e consente di includere pagine figlie, personalizzare i riferimenti e avviare tutti i flussi di lavoro applicabili. Consente inoltre di pubblicare la pagina in un secondo momento.

L’inclusione degli elementi figlio di una cartella per l’opzione &quot;Pubblica più tardi&quot; richiamerà il flusso di lavoro Pubblica albero del contenuto descritto in questo articolo.

Puoi trovare informazioni più dettagliate su Gestisci pubblicazione nella sezione [Documentazione di base sulla pubblicazione](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#manage-publication).

### Flusso di lavoro della struttura dei contenuti di pubblicazione {#publish-content-tree-workflow}

È possibile attivare una replica ad albero scegliendo **Strumenti - Flusso di lavoro - Modelli** e copiando **Pubblica struttura contenuto** modello di flusso di lavoro preconfigurato, come mostrato di seguito:

![](/help/operations/assets/publishcontenttreeworkflow.png)

Non modificare o richiamare il modello originale. Assicurati invece di copiare prima il modello e quindi modificare o richiamare tale copia.

Come tutti i flussi di lavoro, può anche essere richiamato tramite API. Per ulteriori informazioni, consulta [Interazione con i flussi di lavoro a livello di programmazione](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-program-interaction.html?lang=en#extending-aem).

In alternativa, è possibile ottenere questo risultato creando un modello di flusso di lavoro che utilizza il `Publish Content Tree` fase del processo:

1. Dalla home page di AEM as a Cloud Service, vai a **Strumenti - Flusso di lavoro - Modelli**
1. Nella pagina Modelli di flusso di lavoro , premi **Crea** nell&#39;angolo superiore destro dello schermo
1. Aggiungete un titolo e un nome al modello. Per ulteriori informazioni, consulta [Creazione di modelli di flussi di lavoro](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html)
1. Selezionare il modello appena creato dall&#39;elenco e premere **Modifica**
1. Nella finestra seguente, trascina e rilascia il Passaggio processo nel flusso del modello corrente:

   ![Passaggio processo](/help/operations/assets/processstep.png)

1. Fai clic sul passaggio Processo nel flusso e seleziona **Configura** premendo l&#39;icona a forma di chiave inglese
1. Fai clic sul pulsante **Processo** e seleziona `Publish Content Tree` dall’elenco a discesa

   ![Attivazione ad albero](/help/operations/assets/newstep.png)

1. Imposta eventuali parametri aggiuntivi nella **Argomenti** campo . Gli argomenti separati da virgole multipli possono essere raggruppati. Esempio:

   `enableVersion=true,agentId=publish,includeChildren=true`


   >[!NOTE]
   >
   >Per l’elenco dei parametri, consulta la sezione **Parametri** di seguito.

1. Press **Fine** per salvare il modello Workflow.

**Parametri**

* `includeChildren` (valore booleano, predefinito: `false`). false significa che viene pubblicato solo il percorso . true significa che anche i bambini vengono pubblicati.
* `replicateAsParticipant` (valore booleano, predefinito: `false`). Se configurato come `true`, la replica utilizza `userid` dell&#39;entità che ha eseguito la fase del partecipante.
* `enableVersion` (valore booleano, predefinito: `true`). Questo parametro determina se una nuova versione viene creata al momento della replica.
* `agentId` (valore stringa, per impostazione predefinita vengono utilizzati solo gli agenti per la pubblicazione). Si consiglia di essere esplicito sull&#39;agentId; ad esempio, impostandolo come valore: pubblicare. Impostazione dell&#39;agente su `preview` verrà pubblicato nel servizio di anteprima
* `filters` (valore stringa, impostazione predefinita significa che tutti i percorsi sono attivati). I valori disponibili sono:
   * `onlyActivated` - verranno attivati solo i percorsi non contrassegnati come attivati.
   * `onlyModified` - attiva solo i percorsi già attivati e la cui data di modifica è successiva alla data di attivazione.
   * Il sopra può essere OPPURE con una tubazione &quot;|&quot;. Esempio, `onlyActivated|onlyModified`.

**Registrazione**

Quando il passaggio del flusso di lavoro di attivazione della struttura viene avviato, i relativi parametri di configurazione verranno registrati nel livello di registro INFO. Quando i percorsi vengono attivati, viene registrata anche un&#39;istruzione INFO.

Un&#39;istruzione INFO finale verrà quindi registrata dopo che il passaggio del flusso di lavoro ha replicato tutti i percorsi.

Inoltre puoi aumentare il livello di loglevel dei logger qui sotto `com.day.cq.wcm.workflow.process.impl` a DEBUG/TRACE per ottenere ulteriori informazioni sul registro.

In caso di errori, il passaggio del flusso di lavoro termina con un `WorkflowException`, che racchiude l&#39;eccezione sottostante.

Di seguito sono riportati alcuni esempi di registri generati durante un flusso di lavoro della struttura dei contenuti di pubblicazione di esempio:

```
21.04.2021 19:14:55.566 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.treeactivation.TreeActivationWorkflowProcess TreeActivation options: replicateAsParticipant=false(userid=workflow-process-service), agentId=publish, chunkSize=100, filter=, enableVersion=false
```

```
21.04.2021 19:14:58.541 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.ChunkedReplicator closing chunkedReplication-VolatileWorkItem_node1_var_workflow_instances_server60_2021-04-20_brian-tree-replication-test-2_1, 17 paths replicated in 2971 ms
```

**Riprendi supporto**

Il flusso di lavoro elabora il contenuto in blocchi, ciascuno dei quali rappresenta un sottoinsieme del contenuto completo da pubblicare. Se per qualsiasi motivo il flusso di lavoro viene interrotto dal sistema, verrà riavviato ed elaborato il blocco non ancora elaborato. Un’istruzione di registro indicherà che il contenuto è stato ripreso da un percorso specifico.

### API di replica {#replication-api}

Puoi pubblicare il contenuto utilizzando l’API di replica descritta in AEM as a Cloud Service.

Per ulteriori informazioni, consulta la sezione [Documentazione API](https://javadoc.io/doc/com.adobe.aem/aem-sdk-api/latest/com/day/cq/replication/package-summary.html).

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

Quando si replicano le risorse come nell’esempio precedente, verranno utilizzati solo gli agenti che sono attivi per impostazione predefinita. In AEM as a Cloud Service, questo sarà solo l’agente denominato &quot;publish&quot;, che collega l’autore al livello di pubblicazione.

Per supportare la funzionalità di anteprima, è stato aggiunto un nuovo agente denominato &quot;anteprima&quot;, che non è attivo per impostazione predefinita. Questo agente viene utilizzato per collegare l’autore al livello di anteprima. Se desideri replicare solo tramite l’agente di anteprima, devi selezionare esplicitamente questo agente di anteprima tramite un `AgentFilter`.

Vedi l&#39;esempio seguente su come eseguire questa operazione:

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

Nel caso in cui non si fornisca un filtro di questo tipo e si utilizzi solo l’agente &quot;publish&quot;, l’agente &quot;preview&quot; non viene utilizzato e l’azione di replica non influisce sul livello di anteprima.

Il `ReplicationStatus` di una risorsa viene modificata solo se l&#39;azione di replica include almeno un agente attivo per impostazione predefinita. Nell’esempio precedente questo non avviene, in quanto la replica utilizza solo l’agente &quot;preview&quot;. Pertanto, devi utilizzare il nuovo `getStatusForAgent()` , che consente di eseguire una query sullo stato di un agente specifico. Questo metodo funziona anche per l’agente &quot;publish&quot;. Restituisce un valore non-null se è stata eseguita un&#39;azione di replica utilizzando l&#39;agente fornito.

### Metodi di invalidazione dei contenuti {#invalidating-content}

Puoi annullare direttamente la validità del contenuto utilizzando Sling Content Invalidation (SCD) dell’autore (metodo preferito) o utilizzando l’API di replica per richiamare l’agente di replica dello scaricamento del dispatcher per la pubblicazione. Fai riferimento a [Memorizzazione in cache](/help/implementing/dispatcher/caching.md) per ulteriori dettagli.

**Limiti di capacità dell’API di replica**

Si consiglia di replicare meno di 100 percorsi alla volta, con 500 come limite rigido. Al di sopra del limite rigido, un `ReplicationException` verranno lanciati.
Se la logica dell&#39;applicazione non richiede la replica atomica, questo limite può essere superato impostando il `ReplicationOptions.setUseAtomicCalls` su false, che accetta qualsiasi numero di percorsi, ma crea internamente bucket per rimanere al di sotto di questo limite.

La dimensione del contenuto trasmesso per chiamata di replica non deve superare `10 MB`. Ciò include i nodi e le proprietà, ma non eventuali binari (i pacchetti di flusso di lavoro e i pacchetti di contenuto sono considerati binari).


## Risoluzione dei problemi {#troubleshooting}

Per risolvere i problemi di replica, accedi alle code di replica nell’interfaccia utente Web di AEM Author Service:

1. Dal menu di avvio AEM, passa a **Strumenti > Implementazione > Distribuzione**
2. Seleziona la scheda **pubblicare**
   ![Stato](assets/publish-status.png "Stato")
3. Controlla lo stato della coda che dovrebbe essere verde
4. È possibile verificare la connessione al servizio di replica
5. Seleziona la **Registri** scheda che mostra la cronologia delle pubblicazioni di contenuti

![Registri](assets/publish-logs.png "Registri")

Se non è stato possibile pubblicare il contenuto, l’intera pubblicazione viene ripristinata da AEM Publish Service.
In tal caso, la coda principale modificabile mostrerà uno stato rosso e dovrebbe essere rivista per identificare gli elementi che hanno causato l’annullamento della pubblicazione. Facendo clic su tale coda, verranno visualizzati i relativi elementi in sospeso, da cui è possibile cancellare un singolo elemento o tutti gli elementi, se necessario.
