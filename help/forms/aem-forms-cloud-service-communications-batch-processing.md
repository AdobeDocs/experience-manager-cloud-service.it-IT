---
title: Experience Manager [!DNL Forms] Elaborazione batch di comunicazioni as a Cloud Service
description: Come creare comunicazioni personalizzate e orientate al brand?
exl-id: 542c8480-c1a7-492e-9265-11cb0288ce98
source-git-commit: f435751c9c4da8aa90ad0c6705476466bde33afc
workflow-type: tm+mt
source-wordcount: '2250'
ht-degree: 0%

---

# Forms as a Cloud Service Communications - elaborazione batch

Le comunicazioni consentono di creare, assemblare e distribuire comunicazioni personalizzate e orientate al marchio, ad esempio corrispondenze aziendali, documenti, dichiarazioni, lettere di elaborazione delle richieste, note sui benefit, lettere di elaborazione delle richieste, fatture mensili e kit di benvenuto. È possibile utilizzare le API di comunicazione per combinare un modello (XFA o PDF) con i dati dei clienti per generare documenti nei formati PDF, PS, PCL, DPL, IPL e ZPL.

Le comunicazioni forniscono API per la generazione di documenti on-demand e pianificati. Puoi utilizzare le API sincrone per le API on-demand e batch (API asincrone) per la generazione pianificata dei documenti:

* Le API sincrone sono adatte a casi d’uso on-demand, a bassa latenza e per la generazione di documenti a record singolo. Queste API sono più adatte ai casi d’uso basati su azioni dell’utente. Ad esempio, la generazione di un documento dopo la compilazione da parte dell’utente di un modulo.

* Le API Batch (API asincrone) sono adatte a casi d’uso pianificati di alta velocità per la generazione di documenti multipli. Queste API generano documenti in batch. Ad esempio, bollette telefoniche, dichiarazioni con carta di credito e dichiarazioni con benefit generate ogni mese.

<!-- The following skills are required to create templates and use HTTP APIs: 

* Understanding of Adobe Forms Designer or Acrobat Forms to create templates

* Understanding of HTTP APIs and experience of using HTTP APIs

* Basic understanding of Adobe Experience Manager -->


## Operazioni in batch {#batch-operations}

Un&#39;operazione batch è un processo di generazione di più documenti di tipo simile per un set di record a intervalli pianificati. Un&#39;operazione batch ha due parti: Configurazione (definizione) ed esecuzione.

* **Configurazione (definizione)**: Una configurazione batch memorizza informazioni su varie risorse e proprietà da impostare per i documenti generati. Ad esempio, fornisce dettagli sul modello XDP o PDF e sulla posizione dei dati dei clienti da utilizzare, oltre a specificare varie proprietà per i documenti di output.

* **Esecuzione**: Per avviare un&#39;operazione batch, passa il nome della configurazione batch all&#39;API di esecuzione batch.

### Componenti di un’operazione batch {#components-of-a-batch-operations}

**Configurazione cloud**: La configurazione di Experience Manager Cloud consente di collegare un’istanza di Experience Manager all’archiviazione Microsoft Azure di proprietà del cliente. Ti consente di specificare le credenziali per l’account Microsoft Azure di proprietà del cliente per connettersi ad esso.

**Configurazione dell’archivio dati in batch (USC)**: La configurazione dei dati in batch consente di configurare un’istanza specifica di archiviazione BLOB per le API Batch. Consente di specificare le posizioni di input e output nell’archivio BLOB di Microsoft Azure di proprietà del cliente.

**API batch**: Consente di creare configurazioni batch ed eseguire le esecuzioni batch in base a queste configurazioni per unire un modello PDF o XDP con i dati e generare output nei formati PDF, PS, PCL, DPL, IPL e ZPL. Le comunicazioni forniscono API batch per la gestione della configurazione e l’esecuzione batch.

![data-merge-table](assets/communications-batch-structure.png)

**Storage**: Le API di comunicazione utilizzano l’archiviazione di Microsoft Azure Cloud di proprietà del cliente per recuperare i record dei clienti e archiviare i documenti generati. È possibile configurare l’archiviazione Microsoft Azure in Configurazione Experience Manager Cloud Service.

**App**: L’applicazione personalizzata per utilizzare le API Batch per generare e utilizzare documenti.

## Genera più documenti utilizzando le operazioni batch {#generate-multiple-documents-using-batch-operations}

È possibile utilizzare le operazioni batch per generare più documenti a intervalli pianificati.

>[!VIDEO](https://video.tv.adobe.com/v/338349)

Puoi guardare il video o eseguire le istruzioni riportate di seguito per scoprire come generare documenti utilizzando operazioni batch. La documentazione di riferimento API utilizzata nei video è disponibile in formato .yaml. È possibile scaricare [API batch](assets/batch-api.yaml) filma e caricalo su Postman per verificare la funzionalità delle API e segui il video.

### Prerequisiti {#pre-requisites}

Per utilizzare l’API Batch, è necessario quanto segue:

* [Account di archiviazione di Microsoft Azure](https://docs.microsoft.com/en-us/azure/storage/common/storage-account-create)
* Modelli PDF o XDP
* [Dati da unire con i modelli](#form-data)
* Utenti con privilegi di amministratore di Experience Manager

### Configurare l’ambiente {#setup-your-environment}

Prima di utilizzare un&#39;operazione batch:

* Caricare i dati dei clienti (file XML) nell’archiviazione BLOB di Microsoft Azure
* Creare una configurazione Cloud
* Creare la configurazione dell’archivio dati in batch
* Caricare modelli e altre risorse nell’istanza di Cloud Service Experience Manager Forms

### Caricare i dati dei clienti (file XML) nell’archivio di Azure {#upload-customer-data-to-Azure-Storage}

Nell’archivio di Microsoft Azure, crea [contenitori](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs) e [caricare dati cliente (XML)](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container) al [cartelle](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-portal) all&#39;interno dei contenitori.
>[!NOTE]
>
>È possibile configurare l’archiviazione Microsoft Azure per pulire automaticamente la cartella di input o spostare il contenuto della cartella di output in una posizione diversa a intervalli pianificati. Tuttavia, assicurati che le cartelle non vengano pulite quando un&#39;operazione batch che fa riferimento alle cartelle è ancora in esecuzione.

### Creare una configurazione Cloud {#create-a-cloud-configuration}

La configurazione Cloud collega l’istanza di Experience Manager all’archiviazione Microsoft Azure. Per creare una configurazione Cloud:

1. Vai a Strumenti > Cloud Services > Archiviazione di Azure
1. Apri una cartella per ospitare la configurazione e fai clic su Crea. Utilizza la cartella Globale o crea una cartella.
1. Specifica il nome della configurazione e le credenziali per la connessione al servizio. È possibile [recupera le credenziali dal portale di archiviazione di Microsoft Azure](https://docs.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal#view-account-access-keys).
1. Fai clic su Crea.

L’istanza di Experience Manager è ora pronta per la connessione all’archiviazione Microsoft Azure e per utilizzarla per archiviare e leggere il contenuto, se necessario.

### Creare la configurazione dell’archivio dati in batch {#create-batch-data-store-configuration}

La configurazione dei dati in batch consente di configurare contenitori e cartelle per l’input e l’output. I record del cliente vengono conservati nella cartella Sorgente e i documenti generati vengono inseriti nella cartella Destinazione.

Per creare la configurazione:

1. Selezionare Strumenti > Forms > Connettore di archiviazione unificata.
1. Apri una cartella per ospitare la configurazione e fai clic su Crea. Utilizza la cartella Globale o crea una cartella.
1. Specifica il Titolo e il Nome della configurazione. In Archiviazione selezionare Archiviazione di Microsoft Azure.
1. In Percorso di configurazione dell&#39;archiviazione, sfoglia e seleziona la configurazione cloud che contiene le credenziali dell&#39;account di archiviazione Azure di proprietà del cliente.
1. Nella cartella di origine, specifica il nome del contenitore Archiviazione di Azure e la cartella contenente i record.
1. Nella cartella di destinazione, specifica il percorso del contenitore e della cartella Archiviazione di Azure per memorizzare i documenti generati.
1. Fai clic su Crea.

L’istanza di Experience Manager è ora connessa all’archiviazione Microsoft Azure e configurata per recuperare e inviare dati a posizioni specifiche nell’archiviazione Microsoft Azure.

### Carica modelli e altre risorse nell’istanza di Experience Manager {#upload-templates-and-other-assets-to-your-AEM-instance}

In genere, un&#39;organizzazione dispone di più modelli. Ad esempio, un modello per i rendiconti della carta di credito, i rendiconti benefici e le applicazioni di credito. Carica tutti i modelli XDP e PDF nella tua istanza Experience Manager. Per caricare un modello:

1. Apri l’istanza di Experience Manager .
1. Vai a Forms > Forms e documenti
1. Fai clic su Crea > Cartella e crea una cartella. Apri la cartella.
1. Fai clic su Crea > Carica file e carica i modelli.

## Utilizza l’API batch per generare documenti {#use-batch-API-to-generate-documents}

Per utilizzare un’API batch, crea una configurazione batch ed esegui un’esecuzione in base a tale configurazione. La documentazione API fornisce informazioni sulle API per creare ed eseguire un batch, i parametri corrispondenti e i possibili errori. È possibile scaricare [File di definizione API](assets/batch-api.yaml) e caricalo in [Postman](https://go.postman.co/home) o software simile per testare le API per creare ed eseguire un&#39;operazione batch.

### Creare un batch {#create-a-batch}

Per creare un batch, utilizza il `POST /config` API. Includi le seguenti proprietà obbligatorie nel corpo della richiesta HTTP:

* **configName**: Specificare il nome univoco del batch. Esempio, `wknd-job`
* **dataSourceConfigUri**: Specificare il percorso della configurazione dell&#39;archivio dati batch. Può essere un percorso relativo o assoluto della configurazione. Esempio: `/conf/global/settings/forms/usc/batch/wknd-batch`
* **outputTypes**: Specifica i formati di output: PDF e STAMPA. Se si utilizza il tipo di output PRINT, in `printedOutputOptionsList` specificare almeno una opzione di stampa. Le opzioni di stampa sono identificate dal relativo tipo di rendering, pertanto al momento non sono consentite più opzioni di stampa con lo stesso tipo di rendering. I formati supportati sono PS, PCL, DPL, IPL e ZPL.

* **template**: Specifica il percorso assoluto o relativo del modello. Esempio, `crx:///content/dam/formsanddocuments/wknd/statements.xdp`

Se specifichi un percorso relativo, fornisci anche una directory principale del contenuto. Per informazioni sulla directory principale dei contenuti, consulta la documentazione API .

<!-- For example, you include the following JSON in the body of HTTP APIs to create a batch named wknd-job: -->

È possibile utilizzare `GET /config /[configName]` per visualizzare i dettagli della configurazione batch.

### Eseguire un batch {#run-a-batch}

Per eseguire (eseguire) un batch, utilizza `POST /config /[configName]/execution`. Ad esempio, per eseguire un batch denominato wknd-demo, utilizzare /config/wknd-demo/execute. Il server restituisce il codice di risposta HTTP 202 quando accetta la richiesta. L’API non restituisce alcun payload, tranne un codice univoco (identificativo dell’esecuzione) nell’intestazione della risposta HTTP per il processo batch in esecuzione sul server. Puoi utilizzare l’identificatore di esecuzione per recuperare lo stato del batch.

>[!NOTE]
>
>Durante l’esecuzione del batch, non apportare modifiche alle cartelle di origine e di destinazione corrispondenti, alla configurazione dell’origine dati e alla configurazione di Microsoft Azure Cloud.

### Verifica lo stato di un batch {#status-of-a-batch}

Per recuperare lo stato di un batch, utilizza il `GET /config /[configName]/execution/[execution-identifier]`. L’identificatore di esecuzione è incluso nell’intestazione della risposta HTTP per la richiesta di esecuzione batch.

La risposta della richiesta di stato contiene la sezione di stato . Fornisce dettagli sullo stato del processo batch, sul numero di record già presenti nella pipeline (già letti e in fase di elaborazione) e sullo stato di ogni outputType/renderType(numero di elementi in corso, completati e non riusciti). Lo stato include anche l&#39;ora di inizio e di fine del processo batch insieme alle informazioni sugli eventuali errori. L&#39;ora di fine è -1 fino al completamento dell&#39;esecuzione batch.

>[!NOTE]
>
>* Quando si richiedono più formati PRINT, lo stato contiene più voci. Ad esempio, PRINT/ZPL, PRINT/IPL.
>* Un processo batch non legge tutti i record contemporaneamente, ma continua a leggere e ad incrementare il numero di record. Quindi, lo stato restituisce -1 finché tutti i record non sono stati letti.


### Visualizza documenti generati {#view-generated-documents}

Al termine del processo, i documenti generati vengono memorizzati nella `success` nella posizione di destinazione specificata nella configurazione dell&#39;archivio dati batch. In caso di errori, il servizio crea un `failure` cartella. Fornisce informazioni sul tipo e il motivo degli errori.

Comprendiamo con l&#39;aiuto di un esempio: Supponiamo che sia presente un file di dati di input `record1.xml` e due tipi di output: `PDF` e `PCL`. Quindi la posizione di destinazione contiene due sottocartelle `pdf` e `pcl`, uno per ciascuno dei tipi di output. Supponiamo che la generazione di PDF sia riuscita, quindi il `pdf` la sottocartella contiene `success` sottocartella che a sua volta contiene il documento PDF generato `record1.pdf`. Supponiamo che la generazione di PCL non sia riuscita, quindi `pcl` la sottocartella contiene un `failure` sottocartella che a sua volta contiene un file di errore `record1.error.txt` che contiene i dettagli dell&#39;errore. Inoltre, il percorso di destinazione contiene una cartella temporanea denominata `__tmp__` che contiene alcuni file richiesti durante l&#39;esecuzione batch. Questa cartella può essere eliminata quando non sono presenti esecuzioni batch attive che fanno riferimento alla cartella di destinazione.

>[!NOTE]
>
>L&#39;elaborazione di un batch può richiedere un po&#39; di tempo a seconda del numero di record di input e della complessità del modello, attendere alcuni minuti prima di controllare le cartelle di destinazione per i file di output.

## Considerazioni  {#considerations-for-communications-apis}

### Dati modulo {#form-data}

Le API di comunicazione accettano come input sia una struttura del modulo generalmente creata in Designer che i dati del modulo XML. Per compilare un documento con i dati, nei dati del modulo XML deve esistere un elemento XML per ogni campo del modulo che si desidera compilare. Il nome dell&#39;elemento XML deve corrispondere al nome del campo. Un elemento XML viene ignorato se non corrisponde a un campo modulo o se il nome dell’elemento XML non corrisponde al nome del campo. Non è necessario stabilire una corrispondenza con l’ordine di visualizzazione degli elementi XML. Il fattore importante è che gli elementi XML sono specificati con i valori corrispondenti.

Prendi in considerazione il seguente modulo di richiesta di prestito:

![Modulo di domanda di prestito](assets/loanFormData.png)

Per unire i dati alla struttura del modulo, creare un’origine dati XML corrispondente al modulo. L&#39;XML seguente rappresenta un&#39;origine dati XML corrispondente al modulo di applicazione per l&#39;ipoteca di esempio.

```XML
<?xml version="1.0" encoding="UTF-8" ?>
- <xfa:datasets xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/">
- <xfa:data>
- <data>
    - <Layer>
        <closeDate>1/26/2007</closeDate>
        <lastName>Johnson</lastName>
        <firstName>Jerry</firstName>
        <mailingAddress>JJohnson@NoMailServer.com</mailingAddress>
        <city>New York</city>
        <zipCode>00501</zipCode>
        <state>NY</state>
        <dateBirth>26/08/1973</dateBirth>
        <middleInitials>D</middleInitials>
        <socialSecurityNumber>(555) 555-5555</socialSecurityNumber>
        <phoneNumber>5555550000</phoneNumber>
    </Layer>
    - <Mortgage>
        <mortgageAmount>295000.00</mortgageAmount>
        <monthlyMortgagePayment>1724.54</monthlyMortgagePayment>
        <purchasePrice>300000</purchasePrice>
        <downPayment>5000</downPayment>
        <term>25</term>
        <interestRate>5.00</interestRate>
    </Mortgage>
</data>
</xfa:data>
</xfa:datasets>
```

### Tipi di documenti supportati {#supported-document-types}

Per un accesso completo alle funzionalità di rendering delle API di comunicazione, si consiglia di utilizzare un file XDP come input. A volte è possibile utilizzare un file PDF. Tuttavia, l’utilizzo di un file PDF come input presenta alcune limitazioni:

Un documento PDF che non contiene un flusso XFA non può essere rappresentato come PostScript, PCL o ZPL. Le API di comunicazione possono eseguire il rendering dei documenti PDF con flussi XFA (ovvero moduli creati in Designer) in formati laser ed etichette. Se il documento PDF è firmato, certificato o contiene diritti di utilizzo (applicati utilizzando il servizio AEM Forms Reader Extensions), non può essere sottoposto a rendering in questi formati di stampa.

## Documentazione di riferimento API

La documentazione di riferimento API fornisce informazioni dettagliate su tutti i parametri, i metodi di autenticazione e i vari servizi forniti dalle API. La documentazione di riferimento API è disponibile in formato .yaml. È possibile scaricare [API batch](assets/batch-api.yaml) e caricalo su Postman per verificare la funzionalità delle API.

## Problemi noti {#known-issues}

* Quando si specifica PRINT, è possibile specificare un particolare tipo di rendering solo una volta nell&#39;elenco delle opzioni di stampa. Ad esempio, non è possibile avere due opzioni di stampa ciascuna che specificano un tipo di rendering PCL.

* Non modificare la configurazione USC/Azure Cloud dell’origine dati utilizzata in una configurazione batch mentre il batch è in esecuzione. Anche dopo l&#39;esecuzione, se è necessario un aggiornamento, crea una copia della configurazione invece di aggiornare quella utilizzata in una configurazione batch esistente.

## Best practice   {#best-practices}

* Adobe consiglia di ospitare l’archivio dei contenitori BLOB di file di dati nell’area cloud utilizzata da Experience Manager Cloud Service.

## Domande frequenti {#faq}

**È possibile utilizzare una cartella controllata o altri meccanismi di archiviazione per memorizzare l&#39;input e l&#39;output?**

Al momento, è possibile utilizzare l’archiviazione Microsoft Azure per salvare i dati di input e i documenti generati. L’archiviazione di Microsoft Azure offre diverse opzioni per [automatizzare le operazioni di spostamento dei dati](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10).

**Un account di archiviazione Microsoft Azure è incluso con la licenza di Cloud Service Experience Manager Forms?**

L’account di archiviazione Microsoft Azure è indipendente dalla licenza del Cloud Service Experience Manager Forms.

**Le API di comunicazione memorizzano i dati sui server di Cloud Service Experience Manager Forms?**

I dati di input e output vengono salvati solo nell’archiviazione Microsoft Azure.

**Le API di comunicazione sono disponibili solo per il Cloud Service Experience Manager Forms? Posso ottenere funzionalità simili in ambiente on-premise?**

È possibile utilizzare il servizio AEM Forms Output per combinare un modello (XFA o PDF) con i dati dei clienti per generare documenti nei formati PDF, PS, PCL e ZPL.

Rispetto all&#39;ambiente on-premise, il Cloud Service offre ulteriori vantaggi in termini di scalabilità automatica ed efficienza in termini di costi.

<!--**Where is data processed?**

**Who has access to data?**

**Is data encrypted?**

**Where is data hosted?** -->

**È possibile eseguire più operazioni batch contemporaneamente?**
Sì, è possibile eseguire più operazioni batch contemporaneamente. Utilizzare sempre cartelle di origine e di destinazione diverse per ogni operazione per evitare conflitti.
