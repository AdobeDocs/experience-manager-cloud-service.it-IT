---
title: Cosa sono le API di comunicazione di Forms as a Cloud Service?
description: Utilizza le API di comunicazione per firmare, certificare o proteggere i documenti, automatizzare i processi di generazione di PDF e convertire i documenti PDF in un altro formato.
Keywords: How to generate document?, Generate PDF document, Manipulation PDF documents, Assembling PDF documents, Validating PDF document, APIs used in encrypting or decrypting PDFs.
feature: Adaptive Forms, APIs & Integrations
role: Admin, Developer, User
exl-id: b6f05b2f-5665-4992-8689-d566351d54f1
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '2290'
ht-degree: 42%

---

# API di comunicazione di AEM Forms as a Cloud Service {#frequently-asked-questions}

![Immagine protagonista](assets/cloud-communication-apis-hero-image.jpeg)


| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/overview-aem-document-services.html) |
| AEM as a Cloud Service | Questo articolo |

La funzionalità di comunicazione consente di creare documenti approvati, personalizzati e standardizzati per il marchio, ad esempio corrispondenze aziendali, dichiarazioni, lettere di elaborazione delle richieste di rimborso, note sui benefit, fatture mensili o kit di benvenuto.

La funzionalità fornisce API per generare e manipolare i documenti. È possibile generare o manipolare un documento su richiesta oppure creare un processo batch per generare più documenti a intervalli definiti. Le API di comunicazione forniscono:

* funzionalità ottimizzate di generazione della documentazione on-demand e batch.

* capacità di combinare, ridisporre e convalidare documenti PDF su richiesta.

* API HTTP per una più semplice integrazione con sistemi esterni. Sono incluse API separate per le operazioni on-demand (bassa latenza) e batch (operazioni con produttività elevata).

* un accesso sicuro ai dati. Le API di comunicazione si connettono e accedono ai dati solo dagli archivi di dati designati dal cliente e dalla cliente, il che rende le comunicazioni estremamente sicure.

<!-- 
![A sample credit card statement](assets/statement.png)
A credit card statement can be created using Communications APIs. This sample statement uses same template but separate data for each customer depending on their usage of credit card.

-->

## Generazione di documenti

Le API di comunicazione per la generazione di documenti consentono di combinare un modello (XFA o PDF) con i dati dei clienti e delle clienti (XML) per generare documenti in formati PDF e Print come i formati PS, PCL, DPL, IPL e ZPL. Queste API utilizzano modelli PDF e XFA con [dati XML](communications-known-issues-limitations.md#form-data) per generare un singolo documento su richiesta o più documenti utilizzando un processo batch.

In genere, si crea un modello con [Designer](use-forms-designer.md) e si utilizzano le API di comunicazione per unire i dati al modello. L’applicazione può inviare il documento di output a una stampante di rete, a una stampante locale o a un sistema di archiviazione. I flussi di lavoro predefiniti e personalizzati si presentano così:

![Flusso di lavoro per la generazione dei documenti di comunicazione](assets/communicaions-workflow.png)

A seconda del tipo di uso, è possibile rendere disponibili questi documenti anche per il download tramite il sito web o un server di archiviazione.

Alcuni esempi di API per la generazione di documenti:

### Creazione di documenti PDF {#create-pdf-documents}

Le API per la generazione dei documenti possono essere utilizzate per creare un documento PDF basato sulla struttura di un modulo e sui dati del modulo XML. L’output è un documento PDF non interattivo. In altre parole, gli utenti non possono inserire o modificare i dati del modulo. Un flusso di lavoro fondamentale consiste nell’unire i dati del modulo XML a una struttura del modulo per creare un documento PDF. Nell’immagine seguente viene illustrata l’unione della struttura di un modulo e dei dati del modulo XML per produrre un documento PDF.

![Creazione di documenti PDF](assets/outPutPDF_popup.png)
Figura: flusso di lavoro tipico per la creazione di un documento PDF

### Creazione di documenti PostScript (PS), PCL (Printer Command Language) e Zebra Printing Language (ZPL) {#create-PS-PCL-ZPL-documents}

È possibile utilizzare le API di generazione dei documenti per creare documenti PostScript (PS), Printer Command Language (PCL) e Zebra Printing Language (ZPL) basati su un progetto di modulo XDP o su un documento PDF. Queste API consentono di unire la struttura di un modulo ai dati del modulo per generare un documento. È possibile salvare il documento in un file e sviluppare un processo personalizzato per inviarlo a una stampante.

<!-- ### Processing batch data to create multiple documents

Communications APIs can create separate documents for each record within an XML batch data source. The APIs can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you instruct the APIs to create a separate document for each record (for example, PDF documents). As a result, the APIs generate ten PDF documents.

The following illustration also shows Communications APIs processing an XML data file that contains multiple records. However, assume that you instruct the APIs to create a single PDF document that contains all data records. In this situation, the APIs generate one document that contains all the records.

The following illustration shows Communications APIs processing an XML data file that con tains multiple records. Assume that you instruct the Communications APIs to create a separate PDF document for each data record. In this situation, the APIs generates a separate PDF document for each data record.

 -->

### Elaborazione di dati batch per creare più documenti {#processing-batch-data-to-create-multiple-documents}

Le API per la generazione di documenti possono essere utilizzate per creare documenti separati per ogni record all’interno di una fonte di dati batch XML. Puoi generare documenti in blocco e in modalità asincrona. Puoi configurare vari parametri per la conversione e quindi avviare l’elaborazione in batch.

![Creazione documenti PDF](assets/ou_OutputBatchMany_popup.png)

<!-- You can can also create a single document that contains all records (this functionality is the default).  Assume that an XML data source contains ten records and you have a requirement to create a separate document for each record (for example, PDF documents). You can use the Communication APIs to generate ten PDF documents. -->

<!-- The following illustration shows the Communication APIs processing an XML data file that contains multiple records. However, assume that you instruct the Communication APIs to create a single PDF document that contains all data records. In this situation, the Communication APIs generate one document that contains all the records.

![Create PDF Documents](assets/ou_OutputBatchSingle_popup.png)

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. Assume that you instruct the Communication APIs to create a separate PDF document for each data record. In this situation, the Communication APIs generates a separate PDF document for each data record.

![Create PDF Documents](assets/ou_OutputBatchMany_popup.png)

For detailed information on using Batch APIs, see Communication APIs: Processing batch data to create multiple documents. 

### Flatten interactive PDF documents {#flatten-interactive-pdf-documents}

You can use document generation APIs to transform an interactive PDF document (for example, a form) to a non-interactive PDF document. An interactive PDF document lets users enter or modify data located in the PDF document fields. The process of transforming an interactive PDF document to a non-interactive PDF document is called flattening. When a PDF document is flattened, a user cannot modify the data located in the document's fields. One reason to flatten a PDF document is to ensure that data cannot be modified.

You can flatten the following types of PDF documents:

* Interactive PDF documents created in Designer (that contain XFA streams).

* Acrobat PDF forms

If you attempt to flatten a non-interactive PDF document, an exception occurs.

### Retain Form State {#retain-form-state}

An interactive PDF document contains various elements that constitute a form. These elements may include fields (to accept or display data), buttons (to trigger events), and scripts (commands to perform a specific action). Clicking a button may trigger an event that changes the state of a field. For example, choosing a gender option may change the color of a field or the appearance of the form. This is an example of a manual event causing the form state to change.

When such an interactive PDF document is flattened using the Communications APIs, the state of the form is not retained. To ensure that the state of the form is retained even after the form is flattened, set the Boolean value _retainFormState_ to True to save and retain the state of the form. -->

## Manipolazione documento

Le API per la manipolazione dei documenti di comunicazione (Document Transformation) consentono di combinare e ridisporre i documenti di PDF. In genere, si crea un DDX e lo si invia alle API di manipolazione dei documenti per assemblare o ridisporre un documento. Il [Documento DDX](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf) fornisce istruzioni su come utilizzare i documenti di origine per produrre un set di documenti richiesti. La documentazione di riferimento DDX fornisce informazioni dettagliate su tutte le operazioni supportate. Alcuni esempi di manipolazione dei documenti sono:

### assemblare documenti PDF

È possibile utilizzare le API di manipolazione dei documenti per assemblare due o più documenti PDF o XDP in un singolo documento PDF o Portfolio PDF. Di seguito sono riportati alcuni dei modi in cui è possibile assemblare i documenti PDF:

* Assemblare un semplice documento PDF
* Creare un portfolio PDF
* Assemblare documenti crittografati
* Assemblare documenti utilizzando la numerazione Bates
* Uniformare e assemblare documenti

![Assemblaggio di un semplice documento PDF da più documenti PDF](assets/as_document_assembly.png)
Figura: assemblaggio di un semplice documento PDF da più documenti PDF

### Separare i documenti PDF

È possibile utilizzare le API di manipolazione del documento per smontare un documento PDF. Le API possono estrarre pagine dal documento di origine o dividere un documento di origine basato sui segnalibri. In genere, questa attività è utile se il documento PDF è stato creato in origine da molti documenti singoli, ad esempio da una raccolta di istruzioni.

* Estrarre pagine da un documento di origine
* Dividere un documento di origine basato sui segnalibri

![Dividere un documento di origine basato sui segnalibri in più documenti](assets/as_intro_pdfsfrombookmarks.png)
Figura: dividere un documento di origine basato sui segnalibri in più documenti

>[!NOTE]
>
> AEM Forms offre una varietà di font incorporati che si integrano facilmente con i file PDF. Per visualizzare l&#39;elenco dei tipi di carattere supportati: [fai clic qui](/help/forms/supported-out-of-the-box-fonts.md).

<!-- 

## Document utilities

Document utilities synchronous APIs helps you convert documents between PDF and XDP file formats, and query information about a PDF document. For example, you can determine whether a PDF document contains comments or attachments.

### Retrieve PDF document properties

You can [query a PDF document](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/pdf-utility-sync/#tag/Document-Extraction/) for the following information:

* Is a PDF Document: Check whether the source document is a PDF document.
* Is a fillable form: Check whether the source PDF document is a fillable form.
* Form Type: Retrieve the form type of the document.
* Check for Attachments: Check whether the source PDF document has any attachments.
* Check for Comments: Check whether the source PDF document has any review comments.
* Is a PDF Package: Check whether the document is a PDF package.
* Get the PDF Version: Retrieve the [version of the PDF document](https://en.wikipedia.org/wiki/History_of_PDF).
* Recommended Acrobat Version: Retrieve the required version of Acrobat (Reader) to open the PDF document.
* Is an XFA Document: Check whether the source PDF document is an XFA-based PDF document.
* Is Shell PDF: Check whether the source PDF document is shell PDF. A shell PDF contains only an XFA stream, font and image resources, and one page that is either blank or contains a warning that the document must be opened using Acrobat or Adobe Reader. The shell PDF is used with PDF transformation to optimize delivery of PDFForm transformations only.
* Get the XFA Version: Retrieve the [XFA Version for an XFA-based PDF document](https://en.wikipedia.org/wiki/XFA#XFA_versions).

### Convert PDF Documents into XDP Documents

The [PDF to XDP API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/pdf-utility-sync/#tag/Document-Conversion) converts a PDF document to an XDP file. For a PDF document to be successfully converted to an XDP file, the PDF document must contain an XFA stream in the dictionary. -->

## Estrazione documento

<span class="preview"> La funzionalità di estrazione dei documenti si trova nel programma Early Adopter. Per partecipare al programma per i primi utilizzatori, richiedi l’accesso alla funzionalità inviando una e-mail dal tuo account ufficiale all’indirizzo aem-forms-ea@adobe.com. </span>

Il servizio di estrazione documenti consente di ottenere le proprietà di un documento PDF, ad esempio i diritti di utilizzo, le proprietà e i metadati del PDF. Le funzionalità di estrazione dei documenti sono:

* Ottiene le proprietà di un documento PDF, ad esempio se il PDF dispone di allegati, commenti, versione Acrobat e molto altro.
* Estrai i diritti di utilizzo abilitati in un documento PDF, gli utenti recuperano i diritti di utilizzo abilitati o disabilitati in un documento PDF per l’estensibilità di Adobe Acrobat Reader.
* Ottenere le informazioni sui metadati presenti in un documento PDF; i metadati sono informazioni sul documento, distinte dal contenuto del documento, ad esempio testo e grafica. L&#39;Adobe Piattaforma di metadati estensibili (XMP) è uno standard per la gestione dei metadati dei documenti. Il servizio XMP Utilities può recuperare i metadati XMP dai documenti PDF ed esportare i metadati XMP nei documenti PDF.

Il [Documentazione di riferimento API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/) fornisce informazioni dettagliate su tutti i parametri, i metodi di autenticazione e i servizi forniti dalle API. La documentazione di riferimento API è disponibile anche in formato .yaml. Puoi scaricare il file .yaml e caricarlo su Postman per verificare la funzionalità delle API.

<!--

<span class="preview"> The XMP Utilities Service capability is under Early Adopter Program. You can write to aem-forms-ea@adobe.com from your official email id to join the early adopter program and request access to the capability. </span>

### XMP Utilities {#XMP-utilities}

<span class="preview"> The XMP Utilities Service capability is under Early Adopter Program. You can write to aem-forms-ea@adobe.com from your official email id to join the early adopter program and request access to the capability. </span>

PDF documents contain metadata, which is information about the document (as distinguished from the contents of the document, such as text and graphics). The Adobe Extensible Metadata Platform (XMP) is a standard for handling document metadata. The XMP Utilities service can retrieve and save XMP metadata from PDF documents and import XMP metadata into PDF documents.

-->

## Conversione documento

### Convertire e convalidare documenti conformi a PDF/A

Le API per la conversione di documenti di comunicazione consentono di convertire un documento PDF in PDF/A. È possibile utilizzare le API per convertire un documento PDF in un documento conforme a PDF/A e anche per determinare se un documento PDF è conforme a PDF/A. PDF/A è un formato di archiviazione destinato alla conservazione a lungo termine del contenuto del documento. I font vengono incorporati nel documento e il file non è compresso. Di conseguenza, un documento PDF/A è generalmente più grande di un documento PDF standard. Inoltre, un documento PDF/A non include contenuti audio e video.

### Converti PDF in XDP {#convert-pdf-to-xdp}

<span class="preview"> La funzionalità Convert PDF to XDP è disponibile nel programma Early Adopter. Per partecipare al programma per i primi utilizzatori, richiedi l’accesso alla funzionalità inviando una e-mail dal tuo account ufficiale all’indirizzo aem-forms-ea@adobe.com. </span>

Converte un documento PDF in un file XDP. Affinché un documento PDF possa essere convertito correttamente in un file XDP, il documento PDF deve contenere un flusso XFA nel dizionario.

## Document Assurance {#doc-assurance}

Il servizio DocAssurance include le API Signature e Encryption:

### API di firma

Le API di firma consentono all’organizzazione di proteggere la sicurezza e la privacy dei documenti Adobe PDF che distribuisce e riceve. <!--This service uses digital signatures and certification to ensure that only intended recipients can alter documents. --> Le funzioni di sicurezza vengono applicate al documento stesso, che rimane protetto e controllato per l&#39;intero ciclo di vita. Il documento rimane protetto oltre il firewall, quando viene scaricato offline e quando viene inviato nuovamente alla tua organizzazione. Puoi eseguire le seguenti attività utilizzando le API di firma:

* Aggiungere un campo di firma visibile a un documento PDF.
* Aggiungere un campo firma invisibile a un documento PDF.
* Firma il campo della firma specificato in un documento PDF.
* Certifica un documento PDF

### API di crittografia

Le API di crittografia consentono di crittografare e decrittografare i documenti. Quando un documento viene crittografato, il suo contenuto diventa illeggibile. Un utente autorizzato può decrittografare il documento per ottenere l’accesso al contenuto. Se un documento PDF è crittografato con una password, l’utente deve specificare la password di apertura prima che il documento possa essere visualizzato in Adobe Reader o Adobe Acrobat. <!-- Likewise, if a PDF document is encrypted with a certificate, the user must decrypt the PDF document with the public key that corresponds to the certificate (private key) that was used to encrypt the PDF document.-->

Puoi eseguire queste attività utilizzando le API di crittografia:

* Crittografa un documento PDF con una password.
* Rimuovere la crittografia basata su password da un documento PDF.
* Recuperare il tipo di protezione applicato a un documento PDF.
* Restituisce il tipo di protezione applicato a un documento PDF.

Le API di firma e di crittografia sono [API sincrone](#types-of-communications-apis-types).


### Utilità documenti {#doc-utility}

Le utilità per documenti con API sincrone consentono di convertire i documenti tra i formati di file PDF e XDP. Applicare i diritti di utilizzo a un documento ed estrarre i diritti di utilizzo attivati da un documento. Eseguire una query sulle informazioni relative a un documento PDF. <!-- determines whether a PDF document contains comments or attachments and more, and use document transformation services for XMP utilities--> I dettagli delle API per i diritti di utilizzo sono riportati di seguito:


#### API per i diritti di utilizzo (estensione Reader)

<span class="preview"> La funzionalità Diritti di utilizzo (estensione Reader) si trova nel programma Early Adopter. Per partecipare al programma per i primi utilizzatori, richiedi l’accesso alla funzionalità inviando una e-mail dal tuo account ufficiale all’indirizzo aem-forms-ea@adobe.com. </span>

La funzionalità Diritti di utilizzo consente all’organizzazione di condividere facilmente i documenti interattivi di PDF estendendo la funzionalità di Adobe Reader con diritti di utilizzo aggiuntivi. Il servizio funziona con Adobe Reader 7.0 o versione successiva e aggiunge diritti di utilizzo a un documento PDF. Questa azione attiva caratteristiche che in genere non sono disponibili quando un documento PDF viene aperto mediante Adobe Reader, ad esempio l’aggiunta di commenti a un documento, la compilazione di moduli e il salvataggio del documento.

Quando ai documenti PDF vengono aggiunti i diritti di utilizzo appropriati, i destinatari possono eseguire le seguenti attività da Adobe Reader:

* Compilazione di documenti e moduli PDF in linea o non in linea, consentendo ai destinatari di salvare localmente le copie dei propri record e di mantenere intatte le informazioni aggiunte.
* Salvare i documenti PDF su un disco rigido locale per conservare il documento originale ed eventuali commenti, dati o allegati aggiuntivi.
* Allegare file e clip multimediali a documenti PDF.
* Firma, certifica e autentica i documenti di PDF applicando firme digitali utilizzando tecnologie PKI (Public Key Infrastructure) standard.
* Inviare elettronicamente i documenti PDF completati o con annotazioni.
* Utilizzare i documenti e i moduli di PDF come sviluppo front-end intuitivo per i database interni e i servizi Web.
* Condividere documenti PDF con altri utenti in modo che i revisori possano aggiungere commenti utilizzando strumenti di markup intuitivi. Questi strumenti includono note adesive elettroniche, timbri, evidenziazioni e barrati di testo. Le stesse funzioni sono disponibili in Acrobat.
* Supporto della decodifica Forms in codice a barre.

Queste funzionalità speciali relative ai diritti di utilizzo vengono attivate automaticamente quando si apre un documento PDF con abilitazione per i diritti in Adobe Reader. Al termine dell’utilizzo di un documento abilitato ai diritti, tali funzioni vengono nuovamente disabilitate in Adobe Reader. Rimangono disattivati finché l’utente non riceve un altro documento di PDF abilitato per i diritti.

#### Attivare o disattivare i diritti di utilizzo

Le varie funzionalità relative ai diritti di utilizzo per l’estensione dei servizi di Reader PDF sono:

* **Decodifica dei codici a barre**: per decodificare i codici a barre all’interno del documento PDF.

* **Commenti**: per aggiungere un commento offline al documento PDF.

* **Commenti online**: per aggiungere un commento online al documento PDF.

* **Firma digitale**: per aggiungere firme digitali a un documento PDF.

* **Campi modulo dinamici**: per aggiungere campi modulo a un documento PDF.

* **Pagine modulo dinamico**: per aggiungere pagine modulo a un documento PDF.

* **File incorporati**: per incorporare file in un documento PDF.

* **Importazione dati modulo**: per importare i dati del modulo in un documento PDF.

* **Esportazione dati modulo**: per importare i dati del modulo in un documento PDF.

* **Compilazione modulo**: per compilare i campi modulo all’interno di un documento PDF.

* **Forms online**: per accedere a un servizio Web o a un database da un documento di PDF.

* **Invia in modo autonomo**: per inviare i dati del modulo offline da un documento PDF.


#### Altre funzionalità

* **Messaggio**: messaggio visualizzato in Adobe Acrobat Reader all’apertura di un documento PDF a cui sono applicati uno o più diritti di utilizzo.
* **Sblocca password**: password necessaria per aprire un documento PDF crittografato. In genere si tratta della password di apertura del documento, ma se il documento PDF è protetto anche da una password di autorizzazione, è possibile utilizzarlo per aprirlo.

Il [Documentazione di riferimento API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/) fornisce informazioni dettagliate su tutti i parametri, i metodi di autenticazione e i vari servizi forniti dalle API. La documentazione di riferimento API è disponibile anche in formato .yaml. Puoi scaricare il file .yaml e caricarlo su Postman per verificare la funzionalità delle API.

## Tipi di API di comunicazione {#types}

Le comunicazioni forniscono API HTTP per la generazione di documenti on-demand e batch:

* Le **[API sincrone](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)** sono adatte a scenari di generazione di documenti a richiesta, a bassa latenza e a record singolo. Queste API sono più adatte ai casi d’uso basati su azioni dell’utente. Ad esempio, la generazione di un documento al termine della compilazione del modulo da parte dell’utente.

* Le **[API batch (API asincrone)](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)** sono adatte a scenari di generazione pianificati, di produttività elevata e di documenti multipli. Queste API generano documenti in batch. Ad esempio, bollette telefoniche, estratti conto della carta di credito e rendiconti benefit vengono generati ogni mese.

## Onboarding

La funzionalità di comunicazione è disponibile come modulo indipendente e aggiuntivo per gli utenti e le utenti di Forms as a Cloud Service. Per richiedere l’accesso, puoi contattare il team di vendita Adobe o il tuo rappresentante Adobe. Adobe abilita l’accesso per la tua organizzazione e fornisce i privilegi richiesti alla persona designata come amministratore dell’organizzazione. L’amministratore può concedere l’accesso agli sviluppatori Forms as a Cloud Service (utenti) dell’organizzazione per l’utilizzo delle API.

Dopo l’onboarding, per abilitare le funzionalità di comunicazione per l’ambiente Forms as a Cloud Service:

1. Accedi a Cloud Manager e apri la tua istanza AEM Forms as a Cloud Service.

1. Apri l’opzione Modifica programma, vai alla scheda Soluzioni e componenti aggiuntivi e seleziona l’opzione **[!UICONTROL Forms - Comunicazioni]**.

   ![Comunicazioni](assets/communications.png)

   Se hai già abilitato l’opzione **[!UICONTROL Forms - Registrazione digitale]**, allora seleziona l’opzione **[!UICONTROL Forms - Componente aggiuntivo per le comunicazioni]**.

   ![Aggiuntivo](assets/add-on.png)

1. Fai clic su **[!UICONTROL Aggiorna]**.

1. Esegui la pipeline di compilazione. Una volta che la pipeline di compilazione ha esito positivo, le API di comunicazione sono abilitate per l’ambiente.

>[!NOTE]
>
> Per abilitare e configurare le API di manipolazione dei documenti, aggiungi la seguente regola alla [Configurazione Dispatcher](setup-local-development-environment.md#forms-specific-rules-to-dispatcher):
>
> `# Allow Forms Doc Generation requests`
> `/0062 { /type "allow" /method "POST" /url "/adobe/forms/assembler/*" }`

<!--

Communication help you combine a template and XML data to generate print documents in various formats. The service lets you generate documents in synchronous and batch modes. The APIs enables you to create applications that let you:

  * Generate documents by populating template files (PDF and XDP) with XML data.
  * Generate output forms in various formats, including non-interactive PDF print streams.

Consider a scenario where you have one or more templates and multiple records of XML data for each template. You can use Communications APIs to generate a print document for each record.  You can also combine the records into a single document.  The result is a non-interactive PDF document. A non-interactive PDF document does not let users enter data into its fields.

 There are two main Communications APIs. The _generatePDFOutput_ generates PDFs, while the _generatePrintedOutput_ generates PostScript, ZPL, and PCL formats. These APIs are available as REST endpoints on your environment, both on author and publish instances. Since the publish instances are configured to scale faster than the author instances, it is recommended use these APIs via publish instances.

The first parameter of both the operations accept the path and name of the template file (for example, ExpenseClaim.xdp). You can specify a fully qualified path, reference path of your AEM Repository, or path of a binary file. The second parameter accepts an XML document that is merged with the template while generating the output document.  

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

You can use Communications APIs to create PostScript (PS), Printer Command Language (PCL), and Zebra Printing Language (ZPL) document that are based on an XDP form design or PDF document. The _generatePrintedOutput_ API merges a form design with form data to generate a document. You can save the document to a file and develop a custom process to send it to a printer.

 ### Processing batch data to create multiple documents

Communications APIs can create separate documents for each record within an XML batch data source. The APIs can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you instruct the APIs to create a separate document for each record (for example, PDF documents). As a result, the APIs generate ten PDF documents.

The following illustration also shows Communications APIs processing an XML data file that contains multiple records. However, assume that you instruct the APIs to create a single PDF document that contains all data records. In this situation, the APIs generate one document that contains all the records.

The following illustration shows Communications APIs processing an XML data file that contains multiple records. Assume that you instruct the Communications APIs to create a separate PDF document for each data record. In this situation, the APIs generates a separate PDF document for each data record.

### Processing batch data to create multiple documents {#processing-batch-data-to-create-multiple-documents}

You create separate documents for each record within an XML batch data source. You can can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you have a requirement to create a separate document for each record (for example, PDF documents). You can use the Communication APIs to generate ten PDF documents.

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. However, assume that you instruct the Communication APIs to create a single PDF document that contains all data records. In this situation, the Communication APIs generate one document that contains all the records.

![Create PDF Documents](assets/ou_OutputBatchSingle_popup.png)

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. Assume that you instruct the Communication APIs to create a separate PDF document for each data record. In this situation, the Communication APIs generates a separate PDF document for each data record.

![Create PDF Documents](assets/ou_OutputBatchMany_popup.png)

For detailed information on using Batch APIs, see Communication APIs: Processing batch data to create multiple documents.

### Flatten interactive PDF documents {#flatten-interactive-pdf-documents}

You can use the Communications APIs to transform an interactive PDF document (for example, a form) to a non-interactive PDF document. An interactive PDF document lets users enter or modify data located in the PDF document fields. The process of transforming an interactive PDF document to a non-interactive PDF document is called flattening. When a PDF document is flattened, a user cannot modify the data located in the document's fields. One reason to flatten a PDF document is to ensure that data cannot be modified.

You can flatten the following types of PDF documents:

* Interactive PDF documents created in Designer (that contain XFA streams).

* Acrobat PDF forms

If you attempt to flatten a non-interactive PDF document, an exception occurs.

### Retain Form State {#retain-form-state}

An interactive PDF document contains various elements that constitute a form. These elements may include fields (to accept or display data), buttons (to trigger events), and scripts (commands to perform a specific action). Clicking a button may trigger an event that changes the state of a field. For example, choosing a gender option may change the color of a field or the appearance of the form. This is an example of a manual event causing the form state to change.

When such an interactive PDF document is flattened using the Communications APIs, the state of the form is not retained. To ensure that the state of the form is retained even after the form is flattened, set the Boolean value _retainFormState_ to True to save and retain the state of the form.  -->

## Consulta anche {#see-also}

* [Elaborazione della comunicazione - API sincrone](/help/forms/aem-forms-cloud-service-communications.md)
* [Elaborazione della comunicazione - API batch](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
* [Architettura AEM Forms as a Cloud Service per Forms adattivo e API di comunicazione](/help/forms/aem-forms-cloud-service-architecture.md)
