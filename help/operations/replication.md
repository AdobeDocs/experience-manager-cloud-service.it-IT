---
title: Replica
description: Distribuzione e risoluzione dei problemi di replica.
exl-id: c84b4d29-d656-480a-a03a-fbeea16db4cd
translation-type: tm+mt
source-git-commit: eb92c66f2b9e8e6ec859114da2de049747ec251e
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 2%

---

# Replica {#replication}

Adobe Experience Manager as a Cloud Service utilizza la funzionalità [Sling Content Distribution](https://sling.apache.org/documentation/bundles/content-distribution.html) per spostare il contenuto in una replica in un servizio pipeline eseguito su un Adobe I/O che si trova al di fuori del runtime AEM.

>[!NOTE]
>
>Leggi [Distribuzione](/help/core-concepts/architecture.md#content-distribution) per ulteriori informazioni.

## Metodi di pubblicazione dei contenuti {#methods-of-publishing-content}

### Annullamento/Pubblicazione rapida - Pubblicazione programmata {#publish-unpublish}

Queste funzionalità standard AEM per gli autori non cambiano con il Cloud Service AEM.

### Tempi di attivazione e disattivazione - Configurazione del trigger {#on-and-off-times-trigger-configuration}

Le possibilità aggiuntive di **On Time** e **Off Time** sono disponibili nella scheda [Basic delle Proprietà pagina](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic).

Per realizzare la replica automatica è necessario abilitare **Auto Replicate** nella [configurazione OSGi](/help/implementing/deploying/configuring-osgi.md) **On Off Trigger Configuration**:

![Configurazione trigger OSGi On Off](/help/operations/assets/replication-on-off-trigger.png)

### Attivazione albero {#tree-activation}

Per eseguire un&#39;attivazione ad albero:

1. Dal menu di avvio AEM passa a **Strumenti > Implementazione > Distribuzione**
2. Seleziona la scheda **forwardPublisher**
3. Una volta nell&#39;interfaccia della console Web di Publisher anticipata, **selezionare Distribuisci**

   ![](assets/distribute.png "DistribuisciDistribuisci")
4. Seleziona il percorso nel browser percorsi, scegli di aggiungere un nodo, un albero o elimina come richiesto e seleziona **Invia**

### Flusso di lavoro della struttura dei contenuti di pubblicazione {#publish-content-tree-workflow}

Puoi attivare una replica ad albero scegliendo **Strumenti - Flusso di lavoro - Modelli** e copiando il modello di flusso di lavoro preconfigurato **Pubblica albero dei contenuti** , come mostrato di seguito:

![](/help/operations/assets/publishcontenttreeworkflow.png)

Non modificare o richiamare il modello originale. Assicurati invece di copiare prima il modello e quindi modificare o richiamare tale copia.

Come tutti i flussi di lavoro, può anche essere richiamato tramite API. Per ulteriori informazioni, vedere [Interazione con i flussi di lavoro a livello di programmazione](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-program-interaction.html?lang=en#extending-aem).

In alternativa, è possibile ottenere questo risultato anche creando un modello di flusso di lavoro che utilizza il passaggio del processo `Publish Content Tree`:

1. Dalla home page di AEM come Cloud Service, vai a **Strumenti - Flusso di lavoro - Modelli**
1. Nella pagina Modelli di flusso di lavoro, premi **Crea** nell&#39;angolo superiore destro dello schermo
1. Aggiungete un titolo e un nome al modello. Per ulteriori informazioni, consulta [Creazione di modelli di flusso di lavoro](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html)
1. Seleziona il modello appena creato dall&#39;elenco e premi **Modifica**
1. Nella finestra seguente, trascina e rilascia il Passaggio processo nel flusso del modello corrente:

   ![Passaggio processo](/help/operations/assets/processstep.png)

1. Fai clic sul passaggio Processo nel flusso e seleziona **Configura** premendo l&#39;icona a forma di chiave inglese
1. Fai clic sulla scheda **Processo** e seleziona `Publish Content Tree` dall’elenco a discesa

   ![Attivazione ad albero](/help/operations/assets/newstep.png)

1. Imposta eventuali parametri aggiuntivi nel campo **Argomenti** . Gli argomenti separati da virgole multipli possono essere raggruppati. Esempio:

   `enableVersion=true,agentId=publish`


   >[!NOTE]
   >
   >Per l&#39;elenco dei parametri, consulta la sezione **Parametri** di seguito.

1. Premere **Fine** per salvare il modello Flusso di lavoro.

**Parametri**

* `replicateAsParticipant` (valore booleano, predefinito:  `false`). Se configurata come `true`, la replica utilizza `userid` dell&#39;entità principale che ha eseguito il passaggio del partecipante.
* `enableVersion` (valore booleano, predefinito:  `true`). Questo parametro determina se una nuova versione viene creata al momento della replica.
* `agentId` (valore stringa, per impostazione predefinita vengono utilizzati tutti gli agenti abilitati).
* `filters` (valore stringa, impostazione predefinita significa che tutti i percorsi sono attivati). I valori disponibili sono:
   * `onlyActivated` - verranno attivati solo i percorsi non contrassegnati come attivati.
   * `onlyModified` - attiva solo i percorsi già attivati e la cui data di modifica è successiva alla data di attivazione.
   * Il sopra può essere OPPURE con una tubazione &quot;|&quot;. Esempio, `onlyActivated|onlyModified`.

**Registrazione**

Quando il passaggio del flusso di lavoro di attivazione della struttura viene avviato, i relativi parametri di configurazione verranno registrati nel livello di registro INFO. Quando i percorsi vengono attivati, viene registrata anche un&#39;istruzione INFO.

Un&#39;istruzione INFO finale verrà quindi registrata dopo che il passaggio del flusso di lavoro ha replicato tutti i percorsi.

Inoltre puoi aumentare il livello di registro dei logger sotto `com.day.cq.wcm.workflow.process.impl` a DEBUG/TRACE per ottenere ulteriori informazioni sui log.

In caso di errori, il passaggio del flusso di lavoro termina con un `WorkflowException`, che racchiude l&#39;eccezione sottostante.

Di seguito sono riportati alcuni esempi di registri generati durante un flusso di lavoro della struttura dei contenuti di pubblicazione di esempio:

```
21.04.2021 19:14:55.566 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.treeactivation.TreeActivationWorkflowProcess TreeActivation options: replicateAsParticipant=false(userid=workflow-process-service), agentId=publish, chunkSize=100, filter=, enableVersion=false
```

```
21.04.2021 19:14:58.541 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.ChunkedReplicator closing chunkedReplication-VolatileWorkItem_node1_var_workflow_instances_server60_2021-04-20_brian-tree-replication-test-2_1, 17 paths replicated in 2971 ms
```

**Riprendi supporto**

Il flusso di lavoro elabora il contenuto in blocchi, ognuno dei quali rappresenta un sottoinsieme del contenuto completo da pubblicare. Se per qualsiasi motivo il flusso di lavoro viene interrotto dal sistema, verrà riavviato ed elaborato il blocco non ancora elaborato. Un’istruzione di registro indicherà che il contenuto è stato ripreso da un percorso specifico.

## Risoluzione dei problemi {#troubleshooting}

Per risolvere i problemi di replica, accedi alle code di replica nell’interfaccia utente Web di AEM Author Service:

1. Dal menu di avvio AEM passa a **Strumenti > Implementazione > Distribuzione**
2. Seleziona la scheda **forwardPublisher**
   ![](assets/status.png "StatusStatus")
3. Controlla lo stato della coda che dovrebbe essere verde
4. È possibile verificare la connessione al servizio di replica
5. Seleziona la scheda **Logs** che mostra la cronologia delle pubblicazioni di contenuti

![](assets/logs.png "Registri")

Se non è stato possibile pubblicare il contenuto, l’intera pubblicazione viene ripristinata da AEM Publish Service.
In tal caso, le code devono essere riviste per identificare quali elementi hanno causato l&#39;annullamento della pubblicazione. Facendo clic su una coda che mostra uno stato rosso, viene visualizzata la coda con gli elementi in sospeso, da cui è possibile cancellare singoli o tutti gli elementi, se necessario.
