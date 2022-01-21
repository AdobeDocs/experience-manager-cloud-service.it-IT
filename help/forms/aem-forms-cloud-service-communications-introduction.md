---
title: Introduzione alle comunicazioni as a Cloud Service di Forms
description: Unisci automaticamente i dati con i modelli XDP e PDF o genera l’output nei formati PCL, ZPL e PostScript
exl-id: b6f05b2f-5665-4992-8689-d566351d54f1
source-git-commit: d136062ed0851b89f954e5485c2cfac64afeda2d
workflow-type: tm+mt
source-wordcount: '1869'
ht-degree: 1%

---

# Usa comunicazioni as a Cloud Service di AEM Forms {#frequently-asked-questions}

**La funzione di comunicazione as a Cloud Service di AEM Forms è in versione beta.**

La funzionalità di comunicazione ti consente di creare documenti orientati al marchio, personalizzati e standardizzati, come corrispondenze aziendali, dichiarazioni, lettere di elaborazione delle richieste, note sui benefit, fatture mensili o kit di benvenuto.


È possibile generare un documento su richiesta o creare un processo batch per generare più documenti a intervalli definiti. Le API di comunicazione forniscono:

* funzionalità semplificate di generazione della documentazione on-demand e batch

* API HTTP per una più semplice integrazione con i sistemi esistenti. Sono incluse API separate per le operazioni on-demand (bassa latenza) e batch (operazioni con throughput elevato). La generazione dei documenti è un compito efficiente.

* un accesso sicuro ai dati. Le API di comunicazione si connettono e accedono ai dati solo dagli archivi di dati designati dal cliente, non effettuano copie locali dei dati, il che rende le comunicazioni altamente sicure.

![Esempio di dichiarazione della carta di credito](assets/statement.png)
È possibile creare un rendiconto della carta di credito utilizzando le API di comunicazione. Questa istruzione di esempio utilizza lo stesso modello ma dati separati per ogni cliente a seconda dell&#39;uso della carta di credito.

## Come funziona?

Le comunicazioni utilizzano [Modelli PDF e XFA](#supported-document-types) con [Dati XML](#form-data) per generare un singolo documento su richiesta o più documenti utilizzando un processo batch a un intervallo definito.

Un’API di comunicazione consente di combinare un modello (XFA o PDF) con i dati del cliente ([Dati XML](#form-data)) per generare documenti nei formati PDF e Print come i formati PS, PCL, DPL, IPL e ZPL.

In genere, si crea un modello utilizzando [Designer](use-forms-designer.md) e utilizza le API di comunicazione per unire i dati con il modello. L&#39;applicazione può inviare il documento di output a una stampante di rete, a una stampante locale o a un sistema di storage per l&#39;archiviazione. I flussi di lavoro predefiniti e personalizzati si presentano come segue:

![Workflow delle comunicazioni](assets/communicaions-workflow.png)

A seconda del caso d’uso, è anche possibile rendere disponibili questi documenti per il download tramite il sito web o un server di storage.

## API di comunicazione

Le comunicazioni forniscono API HTTP per la generazione di documenti on-demand e batch:

* **[API sincrone](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/api/sync/)** sono adatti a scenari di generazione di documenti a richiesta, a bassa latenza e a record singolo. Queste API sono più adatte ai casi d’uso basati su azioni dell’utente. Ad esempio, la generazione di un documento al termine della compilazione del modulo da parte dell’utente.

* **[API batch (API asincrone)](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/api/batch/)** sono adatti a scenari di generazione pianificati, di alta velocità e di documenti multipli. Queste API generano documenti in batch. Ad esempio, bollette telefoniche, dichiarazioni con carta di credito e dichiarazioni con benefit generate ogni mese.

## Onboarding

Le comunicazioni sono disponibili come modulo indipendente e aggiuntivo per l’utente as a Cloud Service di Forms. Per richiedere l’accesso, contatta il team di vendita Adobe o il tuo rappresentante Adobe.

Adobe abilita l’accesso per la tua organizzazione e fornisce i privilegi richiesti alla persona designata come amministratore dell’organizzazione. L’amministratore può concedere l’accesso agli sviluppatori AEM Forms (utenti) della tua organizzazione per utilizzare le API.

<!--

Communication help you combine a template and XML data to generate print documents in various formats. The service allows you to generate documents in synchronous and batch modes. The APIs enables you to create applications that let you:

  * Generate documents by populating template files (PDF and XDP) with XML data.
  * Generate output forms in various formats, including non-interactive PDF print streams.

Consider a scenario where you have one or more templates and multiple records of XML data for each template. You can use Communications APIs to generate a print document for each record.  You can also combine the records into a single document.  The result is a non-interactive PDF document. A non-interactive PDF document does not let users enter data into its fields.

 There are two main Communications APIs. The _generatePDFOutput_ generates PDFs, while the _generatePrintedOutput_ generates PostScript, ZPL, and PCL formats. These APIs are available as REST endpoints on your environment, both on author and publish instances. Since the publish instances are configured to scale faster than the author instances, it is recommended use these APIs via publish instances.

The first parameter of both the operations accept the path and name of the template file (for example ExpenseClaim.xdp). You can specify a fully qualified path, reference path of your AEM Repository, or path of a binary file. The second parameter accepts an XML document that is merged with the template while generating the output document.  

The [API reference documentation](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:b1223732-ae0f-4921-bdc0-c31e48b56044) provides detailed information about all the parameters, authentication methods, and various services provided by APIs. The API reference documentation is also available in the .yaml format. You can download the .yaml for [Batch APIs](assets/batch-api.yaml) or [non-Batch API.yaml](assets/non-batch-api.yaml) file and upload it to postman to check functionality of APIs.

>[!VIDEO](https://video.tv.adobe.com/v/335771)

Uploading Communication APIs .yaml file to postman to check functionality of APIs.

## Using the Communications APIs {#workflows}

Typically, you create a template using [Designer](use-forms-designer.md) and use communications APIs ( generatePDFOutput and generatePrintedOutput) to:

* Convert these templates to various formats, including PDF, PostScript, ZPL, and PCL.
* Merge XML form data with a form design to generate a document.
* Generate a document without merging XML form data into the document. However, the primary workflow is merging data into the document.

Then, the output document is stored to a file. You can design custom workflows to send the file to a network printer, a local printer, or to a storage system for archival. A typical out of the box and custom workflows look like the following:

![Communications Workflow](assets/communicaions-workflow.png)

### Create PDF documents {#create-pdf-documents}

You can use the _generatePDFOutput_ API to create PDF document that is based on a form design and XML form data. The output is a non-interactive PDF document. That is, users cannot enter or modify form data. A basic workflow is to merge XML form data with a form design to create a PDF document. The following illustration shows the merging of a form design and XML form data to produce a PDF document.

![Create PDF Documents](assets/outPutPDF_popup.png)

### Create PostScript (PS), Printer Command Language (PCL), Zebra Printing Language (ZPL) document {#create-PS-PCL-ZPL-documents}

You can use Communications APIs to create PostScript (PS), Printer Command Language (PCL), and Zebra Printing Language (ZPL) document that are based on a XDP form design or PDF document. The _generatePrintedOutput_ API merges a form design with form data to generate a document. You can save the document to a file and develop a custom process to send it to a printer.

 ### Processing batch data to create multiple documents

Communications APIs can create separate documents for each record within an XML batch data source. The APIs can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you instruct the APIs to create a separate document for each record (for example, PDF documents). As a result, the APIs generate ten PDF documents.

The following illustration also shows Communications APIs processing an XML data file that contains multiple records. However, assume that you instruct the APIs to create a single PDF document that contains all data records. In this situation, the APIs generate one document that contains all of the records.

The following illustration shows Communications APIs processing an XML data file that contains multiple records. Assume that you instruct the Communications APIs to create a separate PDF document for each data record. In this situation, the APIs generates a separate PDF document for each data record.



### Processing batch data to create multiple documents {#processing-batch-data-to-create-multiple-documents}

You create separate documents for each record within an XML batch data source. You can can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you have a requirement to create a separate document for each record (for example, PDF documents). You can use the Communication APIs to generate ten PDF documents.

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. However, assume that you instruct the Communication APIs to create a single PDF document that contains all data records. In this situation, the Communication APIs generate one document that contains all of the records.

![Create PDF Documents](assets/ou_OutputBatchSingle_popup.png)

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. Assume that you instruct the Communication APIs to create a separate PDF document for each data record. In this situation, the Communication APIs generates a separate PDF document for each data record.

![Create PDF Documents](assets/ou_OutputBatchMany_popup.png)

For detailed information on using Batch APIs, see Communication APIs: Processing batch data to create multiple documents.

### Flatten interactive PDF documents {#flatten-interactive-pdf-documents}

You can use the Communications APIs to transform an interactive PDF document (for example, a form) to a non-interactive PDF document. An interactive PDF document lets users enter or modify data located in the PDF document fields. The process of transforming an interactive PDF document to a non-interactive PDF document is called flattening. When a PDF document is flattened, a user cannot modify the data located in the document’s fields. One reason to flatten a PDF document is to ensure that data cannot be modified.

You can flatten the following types of PDF documents:

* Interactive PDF documents created in Designer (that contain XFA streams).

* Acrobat PDF forms

If you attempt to flatten a non-interactive PDF document, an exception occurs.

### Retain Form State {#retain-form-state}

An interactive PDF document contains various elements that constitute a form. These elements may include fields (to accept or display data), buttons (to trigger events), and scripts (commands to perform a specific action). Clicking a button may trigger an event that changes the state of a field. For example, choosing a gender option may change the color of a field or the appearance of the form. This is an example of a manual event causing the form state to change.

When such an interactive PDF document is flattened using the Communications APIs, the state of the form is not retained. To ensure that the state of the form is retained even after the form is flattened, set the Boolean value _retainFormState_ to True to save and retain the state of the form.  -->

## Considerazioni {#considerations-for-communications-apis}

Prima di iniziare a generare documenti utilizzando le API di comunicazione, considera le seguenti considerazioni:

### Dati modulo {#form-data}

Le API di comunicazione accettano una struttura del modulo tipicamente creata in [Designer](use-forms-designer.md) e i dati del modulo XML come input. Per compilare un documento con i dati, nei dati del modulo XML deve esistere un elemento XML per ogni campo del modulo che si desidera compilare. Il nome dell&#39;elemento XML deve corrispondere al nome del campo. Se un elemento XML non corrisponde a un campo modulo o se il nome dell’elemento XML non corrisponde al nome del campo, l’elemento XML viene ignorato. Non è necessario stabilire una corrispondenza con l’ordine di visualizzazione degli elementi XML. Il fattore importante è che gli elementi XML sono specificati con i valori corrispondenti.

Prendi in considerazione il seguente modulo di richiesta di prestito:

![Modulo di domanda di prestito](assets/loanFormData.png)

Per unire i dati alla struttura del modulo, creare un’origine dati XML corrispondente alla gerarchia del modulo, alla denominazione del campo e ai tipi di dati. L&#39;XML seguente rappresenta un&#39;origine dati XML corrispondente al modulo di applicazione per l&#39;ipoteca di esempio.

```XML
* <xfa:datasets xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/">
* <xfa:data>
* <data>
    * <Layer>
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
    * <Mortgage>
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

Per un accesso completo alle funzionalità di rendering delle API di comunicazione, si consiglia di utilizzare un file XDP come input. A volte è possibile utilizzare un file PDF. Tuttavia, l’utilizzo di un file PDF come input presenta le seguenti limitazioni:

Un documento PDF che non contiene un flusso XFA non può essere rappresentato come PostScript, PCL o ZPL. Le API di comunicazione possono eseguire il rendering dei documenti PDF con flussi XFA (ovvero, dei moduli creati in [Designer](use-forms-designer.md)) nei formati laser ed etichette. Se il documento PDF è firmato, certificato o contiene diritti di utilizzo (applicati utilizzando il servizio AEM Forms Reader Extensions), non può essere sottoposto a rendering in questi formati di stampa.

<!-- Run-time options such as PDF version and tagged PDF are not supported for Acrobat forms. They are valid for PDF forms that contain XFA streams; however, these forms cannot be signed or certified. 

### Email support {#email-support}

For email functionality, you can create a process in Experience Manager Workflows that uses the Email Step. A workflow represents a business process that you are automating. -->

### Aree stampabili {#printable-areas}

Il margine non stampabile predefinito da 0,25&quot; non è esatto per le stampanti di etichette e varia dalla stampante alla stampante e dalle dimensioni dell&#39;etichetta alle dimensioni dell&#39;etichetta, tuttavia, si consiglia di mantenere il margine di 0,25&quot; o ridurlo. Tuttavia, si consiglia di non aumentare il margine non stampabile. In caso contrario, le informazioni contenute nell&#39;area stampabile non vengono stampate correttamente.

Assicurarsi sempre di utilizzare il file XDC corretto per la stampante. Ad esempio, evitare di scegliere un file XDC per una stampante a 300 dpi e inviare il documento a una stampante a 200 dpi.

### Script solo per i moduli XFA (XDP/PDF) {#scripts}

Una struttura del modulo utilizzata con le API di comunicazione può contenere script eseguiti sul server. Assicurarsi che una struttura del modulo non contenga script eseguiti sul client. Per informazioni sulla creazione degli script di struttura del modulo, vedere [Guida di Designer](use-forms-designer.md).

<!-- #### Working with Fonts
 Document Considerations for Working with Fonts>> -->

### Mappatura dei font {#font-mapping}

Per progettare un modulo che utilizza font residenti nella stampante, scegliere un nome di font corrispondente ai font disponibili nella stampante in Designer. Un elenco di font supportati per PCL o PostScript si trova nei corrispondenti profili dispositivo (file XDC). In alternativa, è possibile creare la mappatura dei font per associare i font non residenti nella stampante ai font residenti nella stampante con un nome di font diverso. Ad esempio, in uno scenario PostScript, i riferimenti al carattere Arial® possono essere mappati al carattere Helvetica® residente nella stampante.

Se un font è installato in un computer client, è disponibile nell’elenco a discesa in Designer. Se il font non è installato, è necessario specificare manualmente il nome del font. L’opzione &quot;Sostituisci definitivamente font non disponibili&quot; in Designer può essere disattivata. In caso contrario, quando il file XDP viene salvato in Designer, il nome del font sostitutivo viene scritto nel file XDP. Ciò significa che il font residente nella stampante non viene utilizzato.

Esistono due tipi di font OpenType®. Un tipo è un font TrueType OpenType® supportato da PCL. L&#39;altro è CFF OpenType®. L&#39;output PDF e PostScript supporta i font incorporati Type-1, TrueType e OpenType®. L&#39;output PCL supporta i font TrueType incorporati.

I font Type-1 e OpenType® non sono incorporati nell&#39;output PCL. Il contenuto formattato con font Type-1 e OpenType® viene rasterizzato e generato come immagine bitmap di grandi dimensioni e più lento da generare.

I font scaricati o incorporati vengono sostituiti automaticamente durante la generazione dell’output PostScript, PCL o PDF. Ciò significa che solo il sottoinsieme dei glifi di font necessari per il corretto rendering del documento generato è incluso nell’output generato.

### Utilizzo dei file di profilo del dispositivo (file XDC) {#working-with-xdc-files}

Un profilo dispositivo (file XDC) è un file di descrizione della stampante in formato XML. Questo file consente alle API di comunicazione di inviare i documenti come formati laser o di stampa delle etichette. Le API di comunicazione utilizzano i file XDC, tra cui:

* hppcl5c.xdc

* hppcl5e.xdc

* ps_plain_level3.xdc

* ps_plain.xdc

* zpl300.xdc

* zpl600.xdc

* zpl300.xdc

* ipl300.xdc

* ipl400.xdc

* tpcl600.xdc

* dpl300.xdc

* dpl406.xdc

* dpl600.xdc

È possibile utilizzare i file XDC forniti per generare documenti di stampa o modificarli in base alle proprie esigenze.
<!-- It is not necessary to modify these files to create documents. However, you can modify them to meet your business requirements. -->

Questi file sono file XDC di riferimento che supportano le caratteristiche di stampanti specifiche, ad esempio font residenti, vassoi di carta e graffette. Lo scopo di questo riferimento è quello di aiutarti a capire come impostare le tue stampanti utilizzando i profili dei dispositivi. Il riferimento è anche un punto di partenza per stampanti simili della stessa linea di prodotti.

### Utilizzo del file di configurazione XCI {#working-with-xci-files}

Le API di comunicazione utilizzano un file di configurazione XCI per eseguire attività quali controllare se l’output è un singolo pannello o impaginato. Anche se questo file contiene impostazioni che possono essere impostate, non è tipico modificare questo valore. <!-- The default.xci file is located in the svcdata\XMLFormService folder. -->

Puoi trasmettere un file XCI modificato mentre utilizzi un’API di comunicazione. In questo modo, crea una copia del file predefinito, modifica solo i valori che richiedono modifiche per soddisfare i requisiti aziendali e utilizza il file XCI modificato.

Le API di comunicazione iniziano con il file XCI predefinito (o il file modificato). Quindi applica i valori specificati utilizzando le API di comunicazione. Questi valori sostituiscono le impostazioni XCI.

La tabella seguente specifica le opzioni XCI.

| Opzione XCI | Descrizione |
| ------------------------------------| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| config/current/pdf/creator | Identifica il creatore del documento utilizzando la voce Creatore nel dizionario Informazioni documento. Per informazioni su questo dizionario, consultare la guida di riferimento di PDF. |
| config/present/pdf/produttore | Identifica il produttore del documento utilizzando la voce Produttore nel dizionario Informazioni documento. Per informazioni su questo dizionario, consultare la guida di riferimento di PDF. |
| configurazione/attuale/layout | Controlla se l&#39;output è un singolo pannello o impaginato. |
| config/current/pdf/compressione/level | Specifica il grado di compressione da utilizzare per la generazione di un documento PDF. |
| config/current/pdf/scriptModel | Controlla se le informazioni specifiche di XFA sono incluse nel documento PDF di output. |
| config/current/common/data/adjustData | Controlla se l&#39;applicazione XFA regola i dati dopo l&#39;unione. |
| config/current/pdf/renderPolicy | Controlla se la generazione del contenuto della pagina viene eseguita sul server o differita al client. |
| config/present/common/locale | Specifica le impostazioni internazionali predefinite utilizzate nel documento di output. |
| configurazione/presente/destinazione | Se contenuto da un elemento presente, specifica il formato di output. Se contenuto in un elemento openAction, specifica l&#39;azione da eseguire all&#39;apertura del documento in un client interattivo. |
| configurazione/attuale/uscita/tipo | Specifica il tipo di compressione da applicare a un file o il tipo di output da produrre. |
| config/current/common/temp/uri | Specifica l’URI del modulo. |
| config/present/common/template/base | Fornisce una posizione di base per gli URI nella struttura del modulo. Quando questo elemento è assente o vuoto, la posizione della struttura del modulo viene utilizzata come base. |
| config/present/common/log/to | Controlla la posizione in cui vengono scritti i dati di registro o di output. |
| config/current/output/to | Controlla la posizione in cui vengono scritti i dati di registro o di output. |
| config/present/script/currentPage | Specifica la pagina iniziale all&#39;apertura del documento. |
| config/present/script/exclude | Indica alle API server/comunicazioni di AEM Forms gli eventi da ignorare. |
| config/current/pdf/linearized | Controlla se il documento PDF di output è linearizzato. |
| config/present/script/runScripts | Controlla quale insieme di script viene eseguito da AEM Forms. |
| config/present/pdf/tagged | Controlla l’inclusione dei tag nel documento PDF di output. I tag, nel contesto di PDF, sono informazioni aggiuntive incluse in un documento per esporre la struttura logica del documento. I tag facilitano gli strumenti di accessibilità e la riformattazione. Ad esempio, un numero di pagina può essere contrassegnato come artefatto in modo che l’assistente vocale non lo pronunci al centro del testo. Anche se i tag rendono un documento più utile, aumentano anche le dimensioni del documento e il tempo di elaborazione necessario per crearlo. |
| config/present/pdf/version | Specifica la versione del documento PDF da generare. |
