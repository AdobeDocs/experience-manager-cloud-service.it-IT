---
title: Creazione di PDF in blocco semplice - Padroneggiare l’arte con l’elaborazione in batch - Guida autonoma alla generazione di milioni di documenti PDF!
description: Come si creano comunicazioni personalizzate e orientate al brand?
feature: Adaptive Forms, APIs & Integrations
role: Admin, Developer, User
exl-id: 542c8480-c1a7-492e-9265-11cb0288ce98
source-git-commit: 5e3175cc4d96c89df4154ae42c5042cf9c2ca739
workflow-type: tm+mt
source-wordcount: '1710'
ht-degree: 2%

---

# Elaborazione batch di comunicazioni AEM Forms as a Cloud Service

Le comunicazioni consentono di creare, assemblare e distribuire comunicazioni personalizzate e orientate al brand, ad esempio corrispondenza aziendale, documenti, rendiconti, lettere di elaborazione delle richieste di rimborso, avvisi sui benefit, fatture mensili e kit di benvenuto. Puoi utilizzare le API di comunicazione per combinare un modello (XFA o PDF) con i dati del cliente per generare documenti in formati PDF, PS, PCL, DPL, IPL e ZPL.

Le comunicazioni forniscono API per la generazione di documenti su richiesta e pianificata. È possibile utilizzare API sincrone per API batch e on-demand (API asincrone) per la generazione pianificata dei documenti:

* Le API sincrone sono adatte per casi di utilizzo su richiesta, a bassa latenza e per la generazione di documenti a record singolo. Queste API sono più adatte ai casi d’uso basati su azioni dell’utente. Ad esempio, la generazione di un documento dopo che un utente ha compilato un modulo.

* Le API in batch (API asincrone) sono adatte per casi di utilizzo pianificati di generazione di documenti con throughput elevato. Queste API generano documenti in batch. Ad esempio, bollette telefoniche, rendiconti per carta di credito e rendiconti dei benefit generati ogni mese.

<!-- The following skills are required to create templates and use HTTP APIs: 

* Understanding of Adobe Forms Designer or Acrobat Forms to create templates

* Understanding of HTTP APIs and experience of using HTTP APIs

* Basic understanding of Adobe Experience Manager -->


## Operazioni batch {#batch-operations}

Un&#39;operazione batch è un processo di generazione di più documenti di tipo simile per un set di record a intervalli pianificati. Un&#39;operazione batch è composta da due parti: Configurazione (definizione) ed esecuzione.

* **Configurazione (definizione)**: una configurazione batch memorizza informazioni su varie risorse e proprietà da impostare per i documenti generati. Ad esempio, fornisce dettagli sul modello XDP o PDF e sulla posizione dei dati dei clienti da utilizzare, oltre a specificare varie proprietà per i documenti di output.

* **Esecuzione**: per avviare un&#39;operazione batch, passare il nome della configurazione batch all&#39;API di esecuzione batch.

### Componenti di un&#39;operazione batch {#components-of-a-batch-operations}

**Configurazione cloud**: la configurazione di Experience Manager Cloud consente di connettere un&#39;istanza di Experience Manager all&#39;archiviazione di Microsoft Azure di proprietà del cliente. Consente di specificare le credenziali per l&#39;account Microsoft Azure di proprietà del cliente per la connessione.

**Configurazione archivio dati batch (USC)**: la configurazione dei dati batch consente di configurare un&#39;istanza specifica dell&#39;archivio BLOB per le API batch. Consente di specificare i percorsi di input e output nell’archiviazione BLOB di Microsoft Azure di proprietà del cliente.

**API batch**: consente di creare configurazioni batch ed eseguire esecuzioni batch basate su queste configurazioni per unire un modello PDF o XDP con i dati e generare output nei formati PDF, PS, PCL, DPL, IPL e ZPL. Le comunicazioni forniscono API batch per la gestione della configurazione e l’esecuzione in batch.

![data-merge-table](assets/communications-batch-structure.png)

**Archiviazione**: le API di comunicazione utilizzano l&#39;archiviazione cloud di Microsoft Azure di proprietà del cliente per recuperare i record dei clienti e archiviare i documenti generati. È possibile configurare l’archiviazione di Microsoft Azure nella configurazione di Experience Manager Cloud Service.

**App**: applicazione personalizzata per l&#39;utilizzo delle API Batch per generare e utilizzare documenti.

## Generare più documenti utilizzando operazioni batch {#generate-multiple-documents-using-batch-operations}

È possibile utilizzare le operazioni batch per generare più documenti a intervalli pianificati.

>[!VIDEO](https://video.tv.adobe.com/v/338349)

È possibile guardare il video o eseguire le istruzioni riportate di seguito per imparare a generare documenti utilizzando operazioni batch. La documentazione di riferimento API utilizzata nei video è disponibile in formato .yaml. Puoi scaricare il file [API batch](assets/batch-api.yaml) e caricarlo in Postman per verificare la funzionalità delle API e seguire il video.

### Prerequisiti {#pre-requisites}

Per utilizzare l’API Batch, è necessario quanto segue:

* [Account di archiviazione Microsoft Azure](https://docs.microsoft.com/en-us/azure/storage/common/storage-account-create)
* Modelli PDF o XDP
* [Dati da unire con i modelli](#form-data)
* Utenti con privilegi di amministratore Experience Manager

### Configurare l’ambiente {#setup-your-environment}

Prima di utilizzare un&#39;operazione batch:

* Carica dati cliente (file XML) nell’archiviazione BLOB di Microsoft Azure
* Creare una configurazione cloud
* Crea configurazione archivio dati batch
* Caricare modelli e altre risorse nell’istanza di Experience Manager Forms Cloud Service

### Carica dati cliente (file XML) nell’archiviazione di Azure

Nell&#39;archiviazione di Microsoft Azure creare [contenitori](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs) e [caricare i dati del cliente (XML)](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container) nelle [cartelle](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-portal) all&#39;interno dei contenitori.

>[!NOTE]
>
>È possibile configurare l&#39;archiviazione di Microsoft Azure per pulire automaticamente la cartella di input o spostare il contenuto della cartella di output in una posizione diversa a intervalli pianificati. Tuttavia, assicurati che le cartelle non vengano pulite quando è ancora in esecuzione un’operazione batch che fa riferimento alle cartelle.

### Creare una configurazione cloud {#create-a-cloud-configuration}

La configurazione Cloud connette l’istanza di Experience Manager all’archiviazione di Microsoft Azure. Per creare una configurazione Cloud:

1. Vai a Strumenti > Cloud Services > Archiviazione Azure
1. Apri una cartella per ospitare la configurazione e fai clic su Crea. Puoi utilizzare la cartella Globale o crearne una.
1. Specifica il nome della configurazione e le credenziali per la connessione al servizio. È possibile [recuperare queste credenziali dal portale di archiviazione di Microsoft Azure](https://docs.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal#view-account-access-keys).
1. Fai clic su Crea.

L&#39;istanza di Experience Manager è ora pronta per connettersi all&#39;archiviazione di Microsoft Azure e utilizzarla per archiviare e leggere il contenuto, quando necessario.

### Crea configurazione archivio dati batch {#create-batch-data-store-configuration}

La configurazione dei dati in batch consente di configurare contenitori e cartelle per l’input e l’output. I record dei clienti vengono conservati nella cartella di Source e i documenti generati vengono inseriti nella cartella di destinazione.

Per creare la configurazione:

1. Vai a Strumenti > Forms > Connettore di archiviazione unificata.
1. Apri una cartella per ospitare la configurazione e fai clic su Crea. Puoi utilizzare la cartella Globale o crearne una.
1. Specifica Titolo e Nome della configurazione. In Archiviazione selezionare Archiviazione Microsoft Azure.
1. In Percorso configurazione archiviazione, sfoglia e seleziona la configurazione cloud che contiene le credenziali dell’account di archiviazione Azure di proprietà del cliente.
1. Nella cartella Source, specifica il nome del contenitore di archiviazione Azure e della cartella contenente i record.
1. Nella cartella di destinazione, specifica il percorso del contenitore e della cartella di archiviazione Azure in cui archiviare i documenti generati.
1. Fai clic su Crea.

L&#39;istanza di Experience Manager è ora connessa all&#39;archiviazione di Microsoft Azure e configurata per recuperare e inviare dati a posizioni specifiche nell&#39;archiviazione di Microsoft Azure.

### Carica modelli e altre risorse nella tua istanza di Experience Manager {#upload-templates-and-other-assets-to-your-AEM-instance}

In genere, un’organizzazione dispone di più modelli. Ad esempio, un modello per gli estratti conto della carta di credito, gli estratti conto benefit e le richieste di rimborso. Carica tutti i modelli XDP e PDF nella tua istanza Experience Manager. Per caricare un modello:

1. Apri l’istanza di Experience Manager.
1. Passa a Forms > Forms e documenti
1. Fai clic su Crea > Cartella e crea una cartella. Apri la cartella.
1. Fai clic su Crea > Carica file e carica i modelli.

## Utilizzare l’API batch per generare documenti {#use-batch-API-to-generate-documents}

Per utilizzare un’API batch, crea una configurazione batch ed esegui un’esecuzione basata su tale configurazione. La documentazione API fornisce informazioni sulle API per creare ed eseguire un batch, i parametri corrispondenti e i possibili errori. È possibile scaricare il file di definizione [API](assets/batch-api.yaml) e caricarlo in [Postman](https://go.postman.co/home) o software simile per testare le API per creare ed eseguire un&#39;operazione batch.

### Creare un batch {#create-a-batch}

Per creare un batch, utilizzare l&#39;API `POST /config`. Includi le seguenti proprietà obbligatorie nel corpo della richiesta HTTP:

* **configName**: specificare un nome univoco per il batch. Ad esempio `wknd-job`
* **dataSourceConfigUri**: specificare il percorso della configurazione dell&#39;archivio dati batch. Può essere un percorso relativo o assoluto della configurazione. Esempio: `/conf/global/settings/forms/usc/batch/wknd-batch`
* **outputTypes**: Specificare i formati di output: PDF e PRINT. Se si utilizza il tipo di output PRINT, nella proprietà `printedOutputOptionsList` specificare almeno una opzione di stampa. Le opzioni di stampa sono identificate dal relativo tipo di rendering, pertanto al momento non sono consentite più opzioni di stampa con lo stesso tipo di rendering. I formati supportati sono PS, PCL, DPL, IPL e ZPL.

* **modello**: specificare il percorso assoluto o relativo del modello. Ad esempio `crx:///content/dam/formsanddocuments/wknd/statements.xdp`

Se specifichi un percorso relativo, specifica anche una directory principale del contenuto. Consulta la documentazione API per informazioni dettagliate sulla directory principale dei contenuti.

<!-- For example, you include the following JSON in the body of HTTP APIs to create a batch named wknd-job: -->

È possibile utilizzare `GET /config /[configName]` per visualizzare i dettagli della configurazione batch.

### Eseguire un batch {#run-a-batch}

Per eseguire un batch, utilizzare `POST /config /[configName]/execution`. Ad esempio, per eseguire un batch denominato wknd-demo, utilizza /config/wknd-demo/execution. All’accettazione della richiesta, il server restituisce il codice di risposta HTTP 202. L’API non restituisce alcun payload, ad eccezione di un codice univoco (identificatore di esecuzione) nell’intestazione della risposta HTTP per il processo batch in esecuzione sul server. È possibile utilizzare l&#39;identificatore di esecuzione per recuperare lo stato del batch.

>[!NOTE]
>
>Mentre il batch è in esecuzione, non apportare modifiche alle cartelle di origine e di destinazione corrispondenti, alla configurazione dell&#39;origine dati e alla configurazione di Microsoft Azure Cloud.

### Controllare lo stato di un batch {#status-of-a-batch}

Per recuperare lo stato di un batch, utilizzare `GET /config /[configName]/execution/[execution-identifier]`. L’identificatore di esecuzione è incluso nell’intestazione della risposta HTTP per la richiesta di esecuzione batch.

La risposta della richiesta di stato contiene la sezione relativa allo stato. Fornisce dettagli sullo stato del processo batch, sul numero di record già nella pipeline (già letti ed elaborati) e sullo stato di ciascun outputType/renderType(numero di elementi in corso, riusciti e non riusciti). Lo stato include anche l&#39;ora di inizio e di fine del processo batch insieme alle informazioni sugli eventuali errori. L&#39;ora di fine è -1 fino al completamento dell&#39;esecuzione batch.

>[!NOTE]
>
>* Quando si richiedono più formati PRINT, lo stato contiene più voci. Ad esempio PRINT/ZPL, PRINT/IPL.
>* Un processo batch non legge tutti i record contemporaneamente, ma continua a leggere e ad incrementare il numero di record. Lo stato restituisce quindi -1 finché tutti i record non sono stati letti.

### Visualizza documenti generati {#view-generated-documents}

Al termine del processo, i documenti generati vengono archiviati nella cartella `success` nel percorso di destinazione specificato nella configurazione dell&#39;archivio dati batch. In caso di errori, il servizio crea una cartella `failure`. Fornisce informazioni sul tipo e sul motivo degli errori.

Comprendiamo con l&#39;aiuto di un esempio: si supponga che esista un file di dati di input `record1.xml` e due tipi di output: `PDF` e `PCL`. Il percorso di destinazione contiene quindi due sottocartelle `pdf` e `pcl`, una per ciascuno dei tipi di output. Supponiamo che la generazione di PDF sia riuscita, quindi la sottocartella `pdf` contiene la sottocartella `success` che a sua volta contiene il documento PDF generato `record1.pdf`. Supponiamo che la generazione PCL non sia riuscita, quindi la sottocartella `pcl` contiene una sottocartella `failure` che a sua volta contiene un file di errore `record1.error.txt` contenente i dettagli dell&#39;errore. Inoltre, il percorso di destinazione contiene una cartella temporanea denominata `__tmp__` che contiene alcuni file necessari durante l&#39;esecuzione batch. È possibile eliminare questa cartella se non sono presenti esecuzioni batch attive che fanno riferimento alla cartella di destinazione.

>[!NOTE]
>
>L’elaborazione di un batch può richiedere un po’ di tempo a seconda del numero di record di input e della complessità del modello, attendi alcuni minuti prima di controllare le cartelle di destinazione per i file di output.

## Documentazione di riferimento API

La documentazione di riferimento API fornisce informazioni dettagliate su tutti i parametri, i metodi di autenticazione e i vari servizi forniti dalle API. La documentazione di riferimento API è disponibile in formato .yaml. Puoi scaricare il file [API batch](assets/batch-api.yaml) e caricarlo in Postman per verificare la funzionalità delle API.

>[!MORELIKETHIS]
>
>* [Introduzione ad AEM Forms as a Cloud Service Communications](/help/forms/aem-forms-cloud-service-communications-introduction.md)
>* [Architettura AEM Forms as a Cloud Service per API Forms adattivi e di comunicazione](/help/forms/aem-forms-cloud-service-architecture.md)
>* [Elaborazione comunicazione - API sincrone](/help/forms/aem-forms-cloud-service-communications.md)
>* [Elaborazione comunicazione - API batch](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
>* [Elaborazione comunicazione - API on-demand](/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md)
