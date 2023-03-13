---
title: Replica
description: Distribuzione e risoluzione dei problemi di replica.
exl-id: c84b4d29-d656-480a-a03a-fbeea16db4cd
source-git-commit: 1a42cfaa1010686279bc11ca92f50afc75d89e9d
workflow-type: tm+mt
source-wordcount: '1374'
ht-degree: 91%

---

# Replica {#replication}

Adobe Experience Manager as a Cloud Service utilizza la funzionalità di [Distribuzione dei contenuti Sling](https://sling.apache.org/documentation/bundles/content-distribution.html) per spostare il contenuto da replicare in un servizio pipeline eseguito su un Adobe I/O che si trova al di fuori del runtime AEM.

>[!NOTE]
>
>Leggi [Distribuzione](/help/overview/architecture.md#content-distribution) per ulteriori informazioni.

## Metodi di pubblicazione dei contenuti {#methods-of-publishing-content}

>[!NOTE]
>
>Se ti interessa pubblicare contenuti in blocco, utilizza [Flusso di lavoro per pubblicazione struttura contenuto](#publish-content-tree-workflow).
>Questo passaggio di flusso di lavoro è stato creato appositamente per il Cloud Service e può gestire in modo efficiente payload di grandi dimensioni.
>Si sconsiglia di creare un codice personalizzato per la pubblicazione in blocco.
>Se hai bisogno di personalizzare per qualsiasi motivo, puoi attivare questo passaggio di flusso di lavoro o flusso di lavoro utilizzando le API di flusso di lavoro esistenti.
>Anche se è sempre buona prassi pubblicare solo i contenuti da pubblicare ed essere prudenti nel non cercare di pubblicare un numero elevato di contenuti se non necessario, non ci sono limiti alla quantità di contenuti che puoi inviare tramite il flusso di lavoro Pubblica struttura dei contenuti.

### Annullamento/pubblicazione rapida - Annullamento/pubblicazione pianificata {#publish-unpublish}

Questo consente di pubblicare immediatamente le pagine selezionate, senza le opzioni aggiuntive disponibili con l’approccio Gestisci pubblicazione.

Per ulteriori informazioni, consulta [Gestisci pubblicazione](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#manage-publication).

### Tempi di attivazione e disattivazione - Configurazione dell’attivatore {#on-and-off-times-trigger-configuration}

Sono disponibili possibilità aggiuntive di **Ora di attivazione** e **Ora di disattivazione** dalla [scheda Base delle Proprietà pagina](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic).

Per realizzare la replica automatica in questo caso è necessario abilitare **Replica automatica** in [Configurazione OSGi](/help/implementing/deploying/configuring-osgi.md) **Configurazione attivazione/disattivazione**:

![Configurazione attivazione/disattivazione OSGi](/help/operations/assets/replication-on-off-trigger.png)

### Gestisci pubblicazione  {#manage-publication}

Gestisci pubblicazione offre più opzioni rispetto alla Pubblicazione rapida e consente di includere pagine secondarie, personalizzare i riferimenti e avviare tutti i flussi di lavoro applicabili. Consente inoltre di pubblicare la pagina in un secondo momento.

L’inclusione degli elementi secondari di una cartella per l’opzione “Pubblica più tardi” richiamerà il flusso di lavoro Pubblica struttura del contenuto descritto in questo articolo.

Puoi trovare informazioni più dettagliate su Gestisci pubblicazione nella sezione [Documentazione di base sulla pubblicazione](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#manage-publication).

### Flusso di lavoro della struttura dei contenuti di pubblicazione {#publish-content-tree-workflow}

È possibile attivare una replica della struttura scegliendo **Strumenti - Flusso di lavoro - Modelli** e copiando il modello di flusso di lavoro preconfigurato **Pubblica struttura contenuto**, come mostrato di seguito:

![](/help/operations/assets/publishcontenttreeworkflow.png)

Non modificare o richiamare il modello originale. Assicurati invece di fare prima la copia del modello e quindi modificare o richiamare tale copia.

Come tutti i flussi di lavoro, può anche essere richiamato tramite API. Per ulteriori informazioni, consulta [Interazione con i flussi di lavoro a livello di programmazione](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-program-interaction.html?lang=it#extending-aem).

In alternativa, è possibile ottenere questo risultato creando un modello di flusso di lavoro che utilizza la fase `Publish Content Tree` del processo:

1. Dalla home page di AEM as a Cloud Service, vai a **Strumenti - Flusso di lavoro - Modelli**
1. Nella pagina Modelli di flusso di lavoro, premi **Crea** nell’angolo superiore destro dello schermo
1. Aggiungi un titolo e un nome al modello. Per ulteriori informazioni, consulta [Creazione di modelli di flussi di lavoro](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html?lang=it)
1. Seleziona dall’elenco il modello appena creato e premi **Modifica**
1. Nella finestra successiva, trascina e rilascia il Passaggio del processo nel flusso del modello corrente:

   ![Passaggio processo](/help/operations/assets/processstep.png)

1. Fai clic sul Passaggio del processo nel flusso e seleziona **Configura** premendo l’icona a forma di chiave inglese
1. Fai clic sulla scheda **Processo** e seleziona `Publish Content Tree` dall’elenco a discesa

   ![Attivazione struttura](/help/operations/assets/newstep.png)

1. Imposta eventuali parametri aggiuntivi nel campo **Argomenti**. Più argomenti separati da virgole possono essere raggruppati. Esempio:

   `enableVersion=true,agentId=publish,includeChildren=true`


   >[!NOTE]
   >
   >Per l’elenco dei parametri, consulta la sezione **Parametri** di seguito.

1. Premi **Fine** per salvare il modello di flusso di lavoro.

**Parametri**

* `includeChildren` (valore booleano, predefinito: `false`). false significa che viene pubblicato solo il percorso. true significa che vengono pubblicati anche gli elementi secondari.
* `replicateAsParticipant` (valore booleano, predefinito: `false`). Se configurata come `true`, la replica utilizza `userid` dell’entità principale che ha eseguito il Passaggio partecipante.
* `enableVersion` (valore booleano, predefinito: `true`). Questo parametro determina se viene creata una nuova versione al momento della replica.
* `agentId` (valore stringa, “default” indica che vengono utilizzati solo gli agenti per la pubblicazione). Si consiglia di impostare un valore esplicito per agentId; ad esempio: publish. Se si imposta l’agente su `preview`, verrà eseguita la pubblicazione nel servizio di anteprima.
* `filters` (valore stringa, “default” significa che tutti i percorsi sono attivati). I valori disponibili sono:
   * `onlyActivated` : attiva solo le pagine che sono state (già) attivate. Si tratta di una forma di riattivazione.
   * `onlyModified`: verranno attivati solo i percorsi già attivati e la cui data di modifica è successiva alla data di attivazione.
   * Quanto sopra può essere impostato con OR inserendo il simbolo “|”. Esempio: `onlyActivated|onlyModified`.

**Registrazione**

Quando viene avviato il passaggio del flusso di lavoro di attivazione della struttura, i relativi parametri di configurazione vengono registrati nel loglevel INFO. Un’istruzione INFO viene registrata anche qando i percorsi vengono attivati.

Quindi, dopo che il passaggio del flusso di lavoro ha replicato tutti i percorsi, viene registrata un’istruzione INFO finale.

Inoltre puoi aumentare il loglevel dei logger nella sezione `com.day.cq.wcm.workflow.process.impl` per DEBUG/TRACE, in modo da ottenere ulteriori informazioni nel registro.

In caso di errori, il passaggio del flusso di lavoro termina con `WorkflowException`, in cui viene racchiusa l’eccezione sottostante.

Di seguito sono riportati alcuni esempi di registri generati durante uno di flusso di lavoro per la struttura dei contenuti da pubblicare:

```
21.04.2021 19:14:55.566 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.treeactivation.TreeActivationWorkflowProcess TreeActivation options: replicateAsParticipant=false(userid=workflow-process-service), agentId=publish, chunkSize=100, filter=, enableVersion=false
```

```
21.04.2021 19:14:58.541 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.ChunkedReplicator closing chunkedReplication-VolatileWorkItem_node1_var_workflow_instances_server60_2021-04-20_brian-tree-replication-test-2_1, 17 paths replicated in 2971 ms
```

**Supporto per la ripresa in seguito a interruzioni**

Il flusso di lavoro elabora il contenuto in blocchi, ciascuno dei quali rappresenta un sottoinsieme del contenuto completo da pubblicare. Se per qualsiasi motivo il flusso di lavoro viene interrotto dal sistema, verrà riavviato ed elaborato partendo dal blocco non ancora elaborato. Un’istruzione di registro indicherà che il contenuto è stato ripreso da un percorso specifico.

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

Quando si replicano le risorse come nell’esempio precedente, verranno utilizzati solo gli agenti che sono attivi per impostazione predefinita. In AEM as a Cloud Service, questo sarà solo l’agente denominato “publish”, che collega il livello di authoring a quello di pubblicazione.

Per supportare la funzionalità di anteprima, è stato aggiunto un nuovo agente denominato “preview”, che non è attivo per impostazione predefinita. Questo agente viene utilizzato per collegare il livello di authoring a quello di anteprima. Se desideri eseguire la replica solo tramite l’agente preview, devi selezionare esplicitamente l’agente preview tramite `AgentFilter`.

Ecco un esempio di come eseguire questa operazione:

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

Lo stato `ReplicationStatus` complessivo di una risorsa viene modificato solo se l’azione di replica include almeno un agente attivo per impostazione predefinita. Nell’esempio precedente questo non avviene, in quanto la replica utilizza solo l’agente “preview”. Pertanto, devi utilizzare il nuovo metodo `getStatusForAgent()`, che consente di eseguire una query sullo stato di un agente specifico. Questo metodo funziona anche per l’agente “publish”. Se è stata eseguita un’azione di replica utilizzando l’agente fornito, viene restituito un valore non-null.

### Metodi di invalidazione dei contenuti {#invalidating-content}

Puoi annullare direttamente la validità del contenuto utilizzando l’Invalidazione dei contenuti Sling (SCD) dall’authoring (metodo preferito) oppure utilizzando l’API di replica per richiamare l’agente di svuotamento del Dispatcher per la pubblicazione. Per ulteriori dettagli, fai riferimento alla pagina [Memorizzazione in cache](/help/implementing/dispatcher/caching.md).

**Limiti di capacità dell’API di replica**

Si consiglia di replicare meno di 100 percorsi alla volta; il limite massimo consentito è 500. Al di sopra del limite massimo, si verifica un’eccezione `ReplicationException`.
Se la logica dell’applicazione non richiede la replica atomica, questo limite può essere superato impostando `ReplicationOptions.setUseAtomicCalls` su false: questo consente di accettare qualsiasi numero di percorsi, ma vengono creati internamente dei bucket al fine di rimanere al di sotto di questo limite.

La dimensione del contenuto trasmesso per chiamata di replica non deve superare i `10 MB`. Ciò include i nodi e le proprietà, ma non eventuali dati binari (i pacchetti di flusso di lavoro e i pacchetti di contenuto sono considerati dati binari).


## Risoluzione dei problemi {#troubleshooting}

Per risolvere i problemi di replica, accedi alle code di replica nell’interfaccia web del servizio AEM Author:

1. Dal menu Avvia di AEM, vai a **Strumenti > Implementazione > Distribuzione**
2. Seleziona la scheda **Pubblica**.
   ![Stato](assets/publish-status.png "Stato")
3. Controlla lo stato della coda, che dovrebbe essere verde.
4. È possibile verificare la connessione al servizio di replica
5. Seleziona la scheda **Registri** che mostra la cronologia delle pubblicazioni di contenuti

![Registri](assets/publish-logs.png "Registri")

Se non è stato possibile pubblicare il contenuto, l’intera pubblicazione viene ripristinata dal servizio di pubblicazione di AEM.
In tal caso, la coda principale modificabile mostrerà uno stato rosso e dovrebbe essere rivista per identificare gli elementi che hanno causato l’annullamento della pubblicazione. Facendo clic su tale coda, verranno visualizzati i relativi elementi in sospeso, da cui è possibile cancellare un singolo elemento o tutti gli elementi, se necessario.
