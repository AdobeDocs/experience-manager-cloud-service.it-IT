---
title: Guida alla migrazione alle risorse
description: Illustra come inserire risorse in AEM, applicare metadati, generare rappresentazioni e attivarle per pubblicare istanze.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# Guida alla migrazione alle risorse {#assets-migration-guide}

Durante la migrazione delle risorse in AEM, è necessario tenere in considerazione diversi passaggi. L’estrazione di risorse e metadati dalla propria cartella principale corrente esula dall’ambito del presente documento in quanto varia notevolmente tra le diverse implementazioni, ma in questo documento viene descritto come trasferire tali risorse in AEM, applicarne i metadati, generare rappresentazioni e attivarle per pubblicare le istanze.

## Prerequisiti {#prerequisites}

Prima di eseguire effettivamente una qualsiasi delle fasi di questa metodologia, consulta e implementa le linee guida per l&#39;ottimizzazione delle prestazioni. Molti dei passaggi, come la configurazione del numero massimo di processi simultanei, migliorano notevolmente la stabilità e le prestazioni del server in condizioni di carico. Altri passaggi, come la configurazione di un archivio dati file, sono molto più difficili da eseguire dopo che il sistema è stato caricato con le risorse.

>[!NOTE]
>
>I seguenti strumenti di migrazione delle risorse non fanno parte di AEM e non sono supportati dal supporto Adobe:
>
>* Tag Maker di ACS AEM Tools
>* Importazione risorse CSV degli strumenti AEM
>* ACS Commons Bulk Workflow Manager
>* ACS Commons Fast Action Manager
>* Flusso di lavoro sintetico
>
>
Questo software è open source ed è coperto dalla [Licenza Apache v2](https://adobe-consulting-services.github.io/pages/license.html). Per porre una domanda o segnalare un problema, visita rispettivamente [GitHub Issues for ACS AEM Tools](https://github.com/Adobe-Consulting-Services/acs-aem-commons/issues) e [ACS AEM Commons](https://github.com/Adobe-Consulting-Services/acs-aem-tools/issues).

## Migrazione ad AEM {#migrating-to-aem}

La migrazione delle risorse ad AEM richiede diversi passaggi e deve essere vista come un processo graduale. Le fasi della migrazione sono le seguenti:

1. Disattiva flussi di lavoro.
1. Caricare i tag.
1. Consente di inserire le risorse.
1. Elaborazione di rappresentazioni.
1. Attivare le risorse.
1. Abilita flussi di lavoro.

![chlimage_1-223](assets/chlimage_1-223.png)

### Disattivazione dei flussi di lavoro {#disabling-workflows}

Prima di avviare la migrazione, disattivate i avviatori per il flusso di lavoro DAM Update Asset. È meglio assimilare tutte le risorse nel sistema ed eseguire i flussi di lavoro in batch. Se siete già in diretta mentre la migrazione è in corso, potete pianificare l&#39;esecuzione di queste attività in orari non previsti.

### Loading Tags {#loading-tags}

È possibile che sia già presente una tassonomia di tag applicata alle immagini. Sebbene strumenti come Importazione risorse CSV e il supporto di AEM per i profili di metadati possano automatizzare il processo di applicazione dei tag alle risorse, i tag devono essere caricati nel sistema. La funzione [ACS AEM Tools Tag Maker](https://adobe-consulting-services.github.io/acs-aem-tools/features/tag-maker/index.html) consente di compilare i tag utilizzando un foglio di calcolo di Microsoft Excel caricato nel sistema.

### Inserimento di risorse {#ingesting-assets}

Le prestazioni e la stabilità sono fattori importanti per l’assimilazione delle risorse nel sistema. Poiché si sta caricando una grande quantità di dati nel sistema, si desidera assicurarsi che il sistema funziona così come può ridurre al minimo il tempo necessario ed evitare di sovraccaricare il sistema, che può causare un arresto anomalo del sistema, soprattutto nei sistemi già in produzione.

Esistono due approcci per caricare le risorse nel sistema: un approccio basato su push mediante HTTP o un approccio basato su pull mediante le API JCR.

#### Invio tramite HTTP {#pushing-through-http}

Il team dei servizi gestiti di Adobe utilizza uno strumento denominato Glutton per caricare i dati negli ambienti dei clienti. Glutton è una piccola applicazione Java che carica tutte le risorse da una directory a un&#39;altra in un&#39;istanza di AEM. Al posto di Glutton, potete anche utilizzare strumenti come gli script Perl per inserire le risorse nella directory archivio.

Esistono due aspetti negativi principali dell&#39;utilizzo dell&#39;approccio di spingere attraverso https:

1. Le risorse devono essere trasmesse al server tramite HTTP. Ciò richiede un notevole sovraccarico e richiede molto tempo, il che aumenta il tempo necessario per eseguire la migrazione.
1. Se disponete di tag e metadati personalizzati da applicare alle risorse, questo approccio richiede un secondo processo personalizzato da eseguire per applicare questi metadati alle risorse una volta importati.

L’altro approccio per l’assimilazione delle risorse consiste nel estrarre le risorse dal file system locale. Tuttavia, se non riuscite a ottenere un&#39;unità esterna o una condivisione di rete montata sul server per eseguire un approccio basato su pull, è consigliabile pubblicare le risorse su HTTP.

#### Estrazione dal file system locale {#pulling-from-the-local-filesystem}

Importazione risorse CSV degli strumenti [ACS AEM](https://adobe-consulting-services.github.io/acs-aem-tools/features/csv-asset-importer/index.html) estrae le risorse dal file system e dai metadati delle risorse da un file CSV per l’importazione delle risorse. L’API AEM Asset Manager viene utilizzata per importare le risorse nel sistema e applicare le proprietà dei metadati configurate. Idealmente, le risorse sono montate sul server tramite un montaggio di file di rete o tramite un&#39;unità esterna.

Poiché le risorse non devono essere trasmesse in rete, le prestazioni complessive migliorano notevolmente e questo metodo è generalmente considerato il modo più efficiente per caricare le risorse nell’archivio. Inoltre, poiché lo strumento supporta l’assimilazione dei metadati, potete importare tutte le risorse e i metadati in un singolo passaggio, anziché creare un secondo passaggio per applicare i metadati tramite uno strumento separato.

### Processing Renditions {#processing-renditions}

Dopo aver caricato le risorse nel sistema, è necessario elaborarle tramite il flusso di lavoro DAM Update Asset per estrarre i metadati e generare le rappresentazioni. Prima di eseguire questo passaggio, dovete duplicare e modificare il flusso di lavoro DAM Update Asset (Aggiorna risorsa) in base alle vostre esigenze. Il flusso di lavoro predefinito contiene molti passaggi che potrebbero non essere necessari, ad esempio generazione PTIFF di Scene7 o integrazione con il server InDesign.

Dopo aver configurato il flusso di lavoro in base alle esigenze, potete eseguire il flusso di lavoro in due modi:

1. L&#39;approccio più semplice è [ACS Commons&#39;s Bulk Workflow Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/bulk-workflow-manager.html). Questo strumento consente di eseguire una query ed elaborare i risultati della query attraverso un flusso di lavoro. Sono inoltre disponibili opzioni per impostare le dimensioni batch.
1. Puoi utilizzare [ACS Commons Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) insieme a [Synthetic Workflows](https://adobe-consulting-services.github.io/acs-aem-commons/features/synthetic-workflow.html) (Flussi di lavoro sintetici). Questo approccio è molto più complesso, ma consente di rimuovere il sovraccarico del motore del flusso di lavoro AEM, ottimizzando l’utilizzo delle risorse del server. Inoltre, Fast Action Manager migliora ulteriormente le prestazioni monitorando dinamicamente le risorse del server e riducendo il carico posizionato sul sistema. Gli script di esempio sono stati forniti nella pagina delle funzioni di ACS Commons.

### Attivazione delle risorse {#activating-assets}

Per le distribuzioni con un livello di pubblicazione, è necessario attivare le risorse nella farm di pubblicazione. Adobe consiglia di eseguire più di un’istanza di pubblicazione, ma è più efficace replicare tutte le risorse in un’unica istanza di pubblicazione e quindi duplicarla. Quando si attivano numerose risorse, dopo l’attivazione di una struttura ad albero potrebbe essere necessario intervenire. Ecco perché: Quando si disattivano le attivazioni, gli elementi vengono aggiunti alla coda di processi Sling/eventi. Dopo che la dimensione di questa coda inizia a superare circa 40.000 elementi, l&#39;elaborazione rallenta notevolmente. Dopo che la dimensione di questa coda supera i 100.000 elementi, la stabilità del sistema inizia a soffrire.

Per risolvere questo problema, potete utilizzare [Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) per gestire la replica delle risorse. Ciò funziona senza l&#39;utilizzo delle code Sling, riducendo il sovraccarico e riducendo al contempo il carico di lavoro per evitare che il server venga sovraccaricato. Un esempio di utilizzo di FAM per gestire la replica è riportato nella pagina della documentazione della funzione.

Le altre opzioni per spostare le risorse nella farm di pubblicazione includono l’utilizzo di [vlt-rcp](https://jackrabbit.apache.org/filevault/rcp.html) o [oak-run](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run), forniti come strumenti nell’ambito di Jackrabbit. Un’altra opzione consiste nello sfruttare uno strumento open-source per l’infrastruttura AEM, detto [Grabbit](https://github.com/TWCable/grabbit), che promette prestazioni più veloci rispetto a vlt.

Per ciascuno di questi approcci, l’avviso è che le risorse nell’istanza di creazione non vengono visualizzate come attivate. Per gestire il contrassegno di queste risorse con lo stato di attivazione corretto, è inoltre necessario eseguire uno script per contrassegnare le risorse come attivate.

>[!NOTE]
>
>Adobe non mantiene o supporta Grabbit.

### Clonazione pubblicazione {#cloning-publish}

Dopo che le risorse sono state attivate, potete duplicare l’istanza di pubblicazione per creare tutte le copie necessarie per la distribuzione. La duplicazione di un server è abbastanza semplice, ma ci sono alcuni passi importanti da ricordare. Per duplicare la pubblicazione:

1. Eseguire il backup dell&#39;istanza di origine e dell&#39;archivio dati.
1. Ripristinare il backup dell&#39;istanza e del datastore nel percorso di destinazione. I seguenti passaggi fanno riferimento a questa nuova istanza.
1. Esegui una ricerca filesystem in **crx-quickstart/launchpad/felix** per **sling.id**. Elimina questo file.
1. Sotto il percorso principale dell&#39;archivio dati, individuare ed eliminare eventuali file **repository-XXX** .
1. Modificate **crx-quickstart/install/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config** e **crx-quickstart/launchpad/config/org/apache/jackrabbit/oak/plugins/blob/datastore/FileDataStore.config** per puntare alla posizione del datastore sul nuovo ambiente.
1. Avviate l&#39;ambiente.
1. Aggiornate la configurazione di eventuali agenti di replica negli autori per indicare le istanze di pubblicazione corrette o gli agenti di eliminazione del dispatcher nella nuova istanza, in modo da puntare ai dispatcher corretti per il nuovo ambiente.

### Abilitazione dei flussi di lavoro {#enabling-workflows}

Una volta completata la migrazione, gli avviatori per i flussi di lavoro DAM Update Asset dovrebbero essere riabilitati per supportare la generazione di rappresentazioni e l&#39;estrazione di metadati per un utilizzo quotidiano del sistema.

## Migrazione tra istanze AEM {#migrating-between-aem-instances}

Anche se non è altrettanto comune, a volte è necessario migrare grandi quantità di dati da un’istanza di AEM a un’altra; ad esempio, quando eseguite un aggiornamento AEM, aggiornate l’hardware o eseguite la migrazione a un nuovo centro dati, ad esempio con una migrazione AMS.

In questo caso, le risorse sono già popolate con metadati e le rappresentazioni sono già generate. Potete semplicemente concentrarvi sullo spostamento delle risorse da un’istanza all’altra. Durante la migrazione tra le istanze di AEM, effettuate le seguenti operazioni:

1. Disattiva flussi di lavoro.

   Poiché state eseguendo la migrazione delle rappresentazioni insieme alle risorse, desiderate disattivare gli avviatori dei flussi di lavoro per DAM Update Asset.

1. Migrare i tag.

   Poiché i tag sono già stati caricati nell’istanza AEM di origine, potete crearli in un pacchetto di contenuto e installare il pacchetto sull’istanza di destinazione.

1. Migrare le risorse.

   Per spostare le risorse da un’istanza di AEM a un’altra sono consigliati due strumenti:

   * **Vault Remote Copy**, o vlt rcp, consente di utilizzare vlt in una rete. È possibile specificare una directory di origine e di destinazione e vlt scarica tutti i dati del repository da un&#39;istanza e li carica nell&#39;altra. Vlt rcp è documentato all&#39;indirizzo [https://jackrabbit.apache.org/filevault/rcp.html](https://jackrabbit.apache.org/filevault/rcp.html)
   * **Grabbit** è uno strumento di sincronizzazione dei contenuti open-source sviluppato da Time Warner Cable per la loro implementazione AEM. Poiché utilizza flussi di dati continui, rispetto a vLt rcp, ha una latenza inferiore e dichiara un miglioramento della velocità da due a dieci volte più veloce di vlt rcp. Grabbit supporta anche la sincronizzazione solo del contenuto delta, che consente di sincronizzare le modifiche dopo il completamento di un passaggio di migrazione iniziale.

1. Attivare le risorse.

   Seguite le istruzioni per [attivare le risorse](#activating-assets) documentate per la migrazione iniziale ad AEM.

1. Clona pubblicazione.

   Come per la nuova migrazione, il caricamento di un’istanza di pubblicazione singola e la duplicazione è più efficiente rispetto all’attivazione del contenuto su entrambi i nodi. Consultate [Clonazione della pubblicazione.](#cloning-publish)

1. Attivazione dei flussi di lavoro.

   Dopo aver completato la migrazione, riattivate i lanciatori per i flussi di lavoro DAM Update Asset per supportare la generazione di rappresentazioni e l&#39;estrazione di metadati per un utilizzo quotidiano del sistema.

