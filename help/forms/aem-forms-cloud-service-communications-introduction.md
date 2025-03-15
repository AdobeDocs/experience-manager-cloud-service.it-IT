---
title: API di comunicazione AEM Forms as a Cloud Service
description: Generare, manipolare e proteggere i documenti con le API di comunicazione di AEM Forms nel cloud
Keywords: document generation, PDF manipulation, document security, batch processing, document conversion, PDF/A compliance
feature: Adaptive Forms, APIs & Integrations, Document Services
role: Admin, Developer, User
exl-id: b6f05b2f-5665-4992-8689-d566351d54f1
source-git-commit: a5bbcd19b41b3aeff94f900da13e98de65651f8c
workflow-type: tm+mt
source-wordcount: '2497'
ht-degree: 34%

---


# API di comunicazione AEM Forms as a Cloud Service {#communications-apis-overview}

> **Disponibilità versione**
>
> * **AEM 6.5**: [Panoramica di AEM Document Services](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/overview-aem-document-services.html)
> * **AEM as a Cloud Service**: questo articolo

## Introduzione

Le API di comunicazione in AEM Forms as a Cloud Service consentono di creare documenti approvati, personalizzati e standardizzati per le esigenze aziendali. Queste potenti API consentono di generare, manipolare e proteggere i documenti a livello di programmazione, sia su richiesta che in processi batch di grandi volumi.

### Vantaggi principali

* **Generazione documenti semplificata** - Creazione di documenti personalizzati mediante l&#39;unione di modelli e dati dei clienti
* **Potente manipolazione dei documenti** - Combinare, ridisporre e convalidare i documenti di PDF a livello di programmazione
* **Opzioni di distribuzione flessibili** - Utilizzare API on-demand per esigenze di bassa latenza o API batch per operazioni ad alta velocità
* **Protezione avanzata** - Applicazione di firme digitali, certificazione e crittografia per proteggere i documenti sensibili
* **Architettura nativa per il cloud**: utilizzo di un&#39;infrastruttura cloud scalabile e sicura senza costi di manutenzione

## Panoramica delle funzionalità API

Le API di comunicazione forniscono un set completo di funzionalità di elaborazione dei documenti organizzate nelle seguenti aree funzionali:

| Generazione di documenti | Manipolazione documento | Estrazione documento | Conversione documento | Document Assurance |
|---------------------|----------------------|---------------------|---------------------|-------------------|
| Genera documenti personalizzati unendo modelli con dati in vari formati, tra cui PDF e formati di stampa. | Combinare, ridisporre e convalidare i documenti di PDF a livello di programmazione per creare nuovi pacchetti di documenti. | Estrai proprietà, metadati e contenuto dai documenti di PDF per ulteriore elaborazione. | Conversione di documenti tra formati diversi, inclusa la convalida della conformità PDF/A per le esigenze di archiviazione. | Applicazione di firme digitali, certificazione e crittografia per proteggere i documenti. |

La [documentazione di riferimento API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/) fornisce informazioni dettagliate su tutti i parametri, i metodi di autenticazione e i vari servizi forniti dalle API. La documentazione di riferimento API è disponibile anche in formato .yaml. Puoi scaricare il file .yaml e caricarlo su Postman per verificare la funzionalità delle API.

## Generazione di documenti

Le API di comunicazione per la generazione di documenti consentono di combinare un modello (XFA o PDF) con i dati dei clienti e delle clienti (XML) per generare documenti in formati PDF e Print come i formati PS, PCL, DPL, IPL e ZPL. Queste API utilizzano modelli PDF e XFA con [dati XML](communications-known-issues-limitations.md#form-data) per generare un singolo documento su richiesta o più documenti utilizzando un processo batch.

In genere, si crea un modello con [Designer](use-forms-designer.md) e si utilizzano le API di comunicazione per unire i dati al modello. L’applicazione può inviare il documento di output a una stampante di rete, a una stampante locale o a un sistema di archiviazione. I flussi di lavoro predefiniti e personalizzati si presentano così:

![Flusso di lavoro per la generazione dei documenti di comunicazione](assets/communicaions-workflow.png)

A seconda del tipo di uso, è possibile rendere disponibili questi documenti anche per il download tramite il sito web o un server di archiviazione.

### Funzionalità chiave per la generazione di documenti

#### Creazione di documenti PDF {#create-pdf-documents}

Le API per la generazione dei documenti possono essere utilizzate per creare un documento PDF basato sulla struttura di un modulo e sui dati del modulo XML. L’output è un documento PDF non interattivo. In altre parole, gli utenti non possono inserire o modificare i dati del modulo. Un flusso di lavoro fondamentale consiste nell’unire i dati del modulo XML a una struttura del modulo per creare un documento PDF. Nell’immagine seguente viene illustrata l’unione della struttura di un modulo e dei dati del modulo XML per produrre un documento PDF.

![Creazione di documenti PDF](assets/outPutPDF_popup.png)
Figura: flusso di lavoro tipico per la creazione di un documento PDF

L’API di generazione del documento restituisce il documento PDF generato. Facoltativamente, puoi anche caricare i PDF generati nell’archiviazione BLOB di Azure.

<span class="preview"> Il caricamento dei PDF generati utilizzando l&#39;API di generazione documenti nella funzionalità di archiviazione BLOB di Azure si trova in [Programma di adozione anticipata](/help/forms/early-access-ea-features.md). Per partecipare al programma per i primi utilizzatori, richiedi l’accesso alla funzionalità inviando una e-mail dal tuo account ufficiale all’indirizzo aem-forms-ea@adobe.com. </span>

#### Creazione di documenti PostScript (PS), PCL (Printer Command Language) e Zebra Printing Language (ZPL) {#create-PS-PCL-ZPL-documents}

È possibile utilizzare le API di generazione dei documenti per creare documenti PostScript (PS), Printer Command Language (PCL) e Zebra Printing Language (ZPL) basati su una progettazione di moduli XDP o su un documento PDF. Queste API consentono di unire la struttura di un modulo ai dati del modulo per generare un documento. È possibile salvare il documento in un file e sviluppare un processo personalizzato per inviarlo a una stampante.

#### Elaborazione di dati batch per creare più documenti {#processing-batch-data-to-create-multiple-documents}

Le API per la generazione di documenti possono essere utilizzate per creare documenti separati per ogni record all’interno di una fonte di dati batch XML. Puoi generare documenti in blocco e in modalità asincrona. Puoi configurare vari parametri per la conversione e quindi avviare l’elaborazione in batch.

![Creazione documenti PDF](assets/ou_OutputBatchMany_popup.png)

## Manipolazione documento

Le API per la manipolazione dei documenti di comunicazione (Document Transformation) consentono di combinare e ridisporre i documenti di PDF. In genere, si crea un DDX e lo si invia alle API di manipolazione dei documenti per assemblare o ridisporre un documento. Il [Documento DDX](https://helpx.adobe.com/content/dam/help/en/experience-manager/forms-cloud-service/ddxRef.pdf) fornisce istruzioni su come utilizzare i documenti di origine per produrre un set di documenti richiesti. La documentazione di riferimento DDX fornisce informazioni dettagliate su tutte le operazioni supportate.

### Funzionalità principali di manipolazione dei documenti

#### assemblare documenti PDF

È possibile utilizzare le API di manipolazione dei documenti per assemblare due o più documenti PDF o XDP in un singolo documento PDF o Portfolio PDF. Di seguito sono riportati alcuni dei modi in cui è possibile assemblare i documenti di PDF:

* Assemblare un semplice documento PDF
* Creare un portfolio PDF
* Assemblare documenti crittografati
* Assemblare documenti utilizzando la numerazione Bates
* Uniformare e assemblare documenti

![Assemblaggio di un semplice documento PDF da più documenti PDF](assets/as_document_assembly.png)
Figura: assemblaggio di un semplice documento PDF da più documenti PDF

#### Separare i documenti PDF

È possibile utilizzare le API di manipolazione del documento per smontare un documento PDF. Le API possono estrarre pagine dal documento di origine o dividere un documento di origine basato sui segnalibri. In genere, questa attività è utile se il documento PDF è stato creato in origine da molti documenti singoli, ad esempio da una raccolta di istruzioni.

* Estrarre pagine da un documento di origine
* Dividere un documento di origine basato sui segnalibri

![Dividere un documento di origine basato sui segnalibri in più documenti](assets/as_intro_pdfsfrombookmarks.png)
Figura: dividere un documento di origine basato sui segnalibri in più documenti

>[!NOTE]
>
> AEM Forms offre una varietà di font incorporati che si integrano facilmente con i file PDF. Per visualizzare l&#39;elenco dei caratteri supportati, [fare clic qui](/help/forms/supported-out-of-the-box-fonts.md).

## Estrazione documento

<span class="preview"> La funzionalità di estrazione dei documenti si trova nel programma Early Adopter. Per partecipare al programma per i primi utilizzatori, richiedi l’accesso alla funzionalità inviando una e-mail dal tuo account ufficiale all’indirizzo aem-forms-ea@adobe.com. </span>

Il servizio Document Extraction consente di ottenere le proprietà di un documento PDF, ad esempio i diritti di utilizzo, le proprietà e i metadati di PDF. Le funzionalità di estrazione dei documenti sono:

* Ottiene le proprietà di un documento PDF, ad esempio se il PDF contiene allegati, commenti, la versione Acrobat e molto altro.
* Estrarre i diritti di utilizzo abilitati in un documento PDF, gli utenti recuperano i diritti di utilizzo abilitati o disabilitati in un documento PDF per l&#39;estensibilità Adobe Acrobat Reader.
* Ottenere le informazioni sui metadati presenti in un documento di PDF; i metadati sono informazioni sul documento (distinte dal contenuto del documento, ad esempio testo e grafica). Adobe Extensible Metadata Platform (XMP) è uno standard per la gestione dei metadati dei documenti. Il servizio XMP Utilities può recuperare i metadati XMP dai documenti PDF ed esportare i metadati XMP nei documenti PDF.

La [documentazione di riferimento API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/) fornisce informazioni dettagliate su tutti i parametri, i metodi di autenticazione e i servizi forniti dalle API. La documentazione di riferimento API è disponibile anche in formato .yaml. Puoi scaricare il file .yaml e caricarlo su Postman per verificare la funzionalità delle API.

## Conversione documento

### Convertire e convalidare documenti conformi a PDF/A

Le API di conversione dei documenti di comunicazione aiutano a convertire un documento PDF in PDF/A. È possibile utilizzare le API per convertire un documento di PDF in un documento conforme a PDF/A e anche per determinare se un documento di PDF è conforme a PDF/A. PDF/A è un formato di archiviazione destinato alla conservazione a lungo termine del contenuto del documento. I font vengono incorporati nel documento e il file non è compresso. Di conseguenza, un documento PDF/A è generalmente più grande di un documento PDF standard. Inoltre, un documento PDF/A non contiene contenuti audio e video. Gli standard di conformità PDF/A supportati includono PDF/A-1a, 1b, 2a, 2b, 3a e 3b.

### Conversione da PDF a XDP {#convert-pdf-to-xdp}

<span class="preview"> La funzionalità di conversione da PDF a XDP si trova nel programma Early Adopter. Per partecipare al programma per i primi utilizzatori, richiedi l’accesso alla funzionalità inviando una e-mail dal tuo account ufficiale all’indirizzo aem-forms-ea@adobe.com. </span>

Converte un documento PDF in un file XDP. Per convertire correttamente un documento PDF in un file XDP, il documento PDF deve contenere un flusso XFA nel dizionario.

## Document Assurance {#doc-assurance}

Il servizio DocAssurance include le API Signature e Encryption:

### API di firma

Le API di firma consentono all’organizzazione di proteggere la sicurezza e la privacy dei documenti Adobe PDF che distribuisce e riceve. <!--This service uses digital signatures and certification to ensure that only intended recipients can alter documents. --> Le funzionalità di protezione vengono applicate al documento stesso, che rimane protetto e controllato per l&#39;intero ciclo di vita. Il documento rimane protetto oltre il firewall, quando viene scaricato offline e quando viene inviato nuovamente alla tua organizzazione. Puoi eseguire le seguenti attività utilizzando le API di firma:

* Aggiungere un campo di firma visibile a un documento di PDF.
* Aggiungere un campo firma invisibile a un documento di PDF.
* Firma il campo della firma specificato in un documento PDF.
* Certifica un documento PDF
* Rimuovi la firma dal campo della firma specificato in un documento PDF
* Elimina il campo della firma specificato da un documento PDF

<span class="preview"> Rimuovere la firma dal campo della firma specificato ed eliminare il campo della firma specificato da un documento di PDF disponibile nel programma per l&#39;adozione anticipata. Per partecipare al programma per i primi utilizzatori, richiedi l’accesso alla funzionalità inviando una e-mail dal tuo account ufficiale all’indirizzo aem-forms-ea@adobe.com. </span>

### API di crittografia

Le API di crittografia consentono di crittografare e decrittografare i documenti. Quando un documento viene crittografato, il suo contenuto diventa illeggibile. Un utente autorizzato può decrittografare il documento per ottenere l’accesso al contenuto. Se un documento PDF è crittografato con una password, l’utente deve specificare la password di apertura prima che il documento possa essere visualizzato in Adobe Reader o Adobe Acrobat. <!-- Likewise, if a PDF document is encrypted with a certificate, the user must decrypt the PDF document with the public key that corresponds to the certificate (private key) that was used to encrypt the PDF document.-->

Puoi eseguire queste attività utilizzando le API di crittografia:

* Crittografare un documento PDF con una password.
* Rimuovere la crittografia basata su password da un documento PDF.
* Recuperare il tipo di protezione applicato a un documento PDF.
* Restituisce il tipo di protezione applicato a un documento PDF.

Sia le API di firma che quelle di crittografia sono [API sincrone](#types-of-communications-apis-types).

### Utilità documenti {#doc-utility}

Le utilità per documenti con API sincrone consentono di convertire i documenti tra i formati di file PDF e XDP. Applicare i diritti di utilizzo a un documento ed estrarre i diritti di utilizzo attivati da un documento. Eseguire una query su un documento di PDF. <!-- determines whether a PDF document contains comments or attachments and more, and use document transformation services for XMP utilities--> I dettagli delle API per i diritti di utilizzo sono riportati di seguito:

#### API per i diritti di utilizzo (estensione Reader)

<span class="preview"> La funzionalità Diritti di utilizzo (estensione Reader) è inclusa nel programma Early Adopter. Per partecipare al programma per i primi utilizzatori, richiedi l’accesso alla funzionalità inviando una e-mail dal tuo account ufficiale all’indirizzo aem-forms-ea@adobe.com. </span>

La funzionalità Diritti di utilizzo consente all&#39;organizzazione di condividere facilmente documenti PDF interattivi estendendo la funzionalità di Adobe Reader con diritti di utilizzo aggiuntivi. Il servizio funziona con Adobe Reader 7.0 o versione successiva e aggiunge diritti di utilizzo a un documento PDF. Questa azione attiva le funzioni che in genere non sono disponibili quando un documento di PDF viene aperto mediante Adobe Reader, ad esempio l&#39;aggiunta di commenti a un documento, la compilazione di moduli e il salvataggio del documento.

Quando ai documenti di PDF vengono aggiunti i diritti di utilizzo appropriati, i destinatari possono eseguire le seguenti attività da Adobe Reader:

* Completare i documenti e i moduli di PDF online o offline, consentendo ai destinatari di salvare le copie in locale per i propri record e di mantenere intatte le informazioni aggiunte.
* Salvare i documenti PDF su un disco rigido locale per conservare il documento originale ed eventuali commenti, dati o allegati aggiuntivi.
* Allegare file e clip multimediali a documenti PDF.
* Firma, certifica e autentica i documenti PDF applicando firme digitali utilizzando tecnologie PKI (Public Key Infrastructure) standard.
* Inviare elettronicamente i documenti PDF completati o con annotazioni.
* Utilizzare i documenti e i moduli di PDF come front-end di sviluppo intuitivo per i database interni e i servizi Web.
* Condividere documenti PDF con altri utenti in modo che i revisori possano aggiungere commenti utilizzando strumenti di markup intuitivi. Questi strumenti includono note adesive elettroniche, timbri, evidenziazioni e barrati di testo. Le stesse funzioni sono disponibili in Acrobat.
* Supporto della decodifica Forms in codice a barre.

Queste speciali funzionalità relative ai diritti di utilizzo vengono attivate automaticamente quando si apre un documento PDF con abilitazione per i diritti in Adobe Reader. Al termine dell’utilizzo di un documento con abilitazione per i diritti, tali funzioni vengono nuovamente disabilitate in Adobe Reader. Rimangono disattivati finché l’utente non riceve un altro documento PDF con abilitazione per i diritti.

#### Attivare o disattivare i diritti di utilizzo

Le varie funzionalità relative ai diritti di utilizzo per l’estensione dei servizi PDF Reader sono:

* **Decodifica dei codici a barre**: per decodificare i codici a barre all&#39;interno del documento PDF.

* **Commenti**: per aggiungere commenti non in linea al documento PDF.

* **Commenti in linea**: per aggiungere commenti in linea al documento di PDF.

* **Firma digitale**: per aggiungere firme digitali a un documento di PDF.

* **Campi modulo dinamici**: per aggiungere campi modulo a un documento di PDF.

* **Pagine modulo dinamico**: per aggiungere pagine modulo a un documento di PDF.

* **File incorporati**: per incorporare file in un documento PDF.

* **Importazione dati modulo**: per importare i dati del modulo in un documento di PDF.

* **Esportazione dati modulo**: per importare i dati del modulo in un documento di PDF.

* **Compilazione modulo**: per compilare i campi modulo all&#39;interno di un documento PDF.

* **Forms in linea**: per accedere a un servizio Web o a un database da un documento di PDF.

* **Invio autonomo**: per inviare i dati del modulo offline da un documento di PDF.

#### Altre funzionalità

* **Messaggio**: messaggio visualizzato in Adobe Acrobat Reader all&#39;apertura di un documento PDF a cui sono applicati uno o più diritti di utilizzo.
* **Sblocca password**: password necessaria per aprire un documento PDF crittografato. In genere si tratta della password di apertura del documento, ma se il documento PDF è protetto anche da una password di autorizzazione, è possibile utilizzarlo per aprirlo.

## Tipi di API di comunicazione {#types}

Le comunicazioni forniscono API HTTP per la generazione di documenti on-demand e batch:

* Le **[API sincrone](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)** sono adatte a scenari di generazione di documenti a richiesta, a bassa latenza e a record singolo. Queste API sono più adatte ai casi d’uso basati su azioni dell’utente. Ad esempio, la generazione di un documento al termine della compilazione del modulo da parte dell’utente.

* Le **[API batch (API asincrone)](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)** sono adatte a scenari di generazione pianificati, di produttività elevata e di documenti multipli. Queste API generano documenti in batch. Ad esempio, bollette telefoniche, estratti conto della carta di credito e rendiconti benefit vengono generati ogni mese.

## Onboarding

La funzionalità di comunicazione è disponibile come modulo indipendente e aggiuntivo per gli utenti e le utenti di Forms as a Cloud Service. Per richiedere l’accesso, puoi contattare il team di vendita Adobe o il tuo rappresentante Adobe. Adobe abilita l’accesso per la tua organizzazione e fornisce i privilegi richiesti alla persona designata come amministratore dell’organizzazione. L’amministratore può concedere l’accesso alle API agli sviluppatori Forms as a Cloud Service (utenti) dell’organizzazione.

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
> Per abilitare e configurare le API di manipolazione dei documenti, aggiungere la regola seguente alla [configurazione Dispatcher](setup-local-development-environment.md#forms-specific-rules-to-dispatcher):
>
> `# Allow Forms Doc Generation requests`
> `/0062 { /type "allow" /method "POST" /url "/adobe/forms/assembler/*" }`

## Risorse aggiuntive {#see-also}

* [Elaborazione della comunicazione - API sincrone](/help/forms/aem-forms-cloud-service-communications.md)
* [Elaborazione della comunicazione - API batch](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
* [Architettura di AEM Forms as a Cloud Service](/help/forms/aem-forms-cloud-service-architecture.md)
* [Documentazione di riferimento API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)
* [Caratteristiche preliminari del programma](/help/forms/early-access-ea-features.md)
