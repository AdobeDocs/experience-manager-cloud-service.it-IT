---
title: API di comunicazione AEM Forms as a Cloud Service
description: Generare, manipolare e proteggere i documenti con le API di comunicazione di AEM Forms nel cloud
Keywords: document generation, PDF manipulation, document security, batch processing, document conversion, PDF/A compliance
feature: Adaptive Forms, APIs & Integrations, Document Services
role: Admin, Developer, User
exl-id: b6f05b2f-5665-4992-8689-d566351d54f1
source-git-commit: a9eed5b6219163e721d81c9d77a31604666a2ac5
workflow-type: tm+mt
source-wordcount: '1432'
ht-degree: 3%

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

## Funzionalità principali

Le API di comunicazione forniscono un set completo di funzionalità di elaborazione dei documenti organizzate nelle seguenti aree funzionali:


| Generazione di documenti | Manipolazione documento | Estrazione documento | Conversione documento | Document Assurance |
|---------------------|----------------------|---------------------|---------------------|-------------------|
| Genera documenti personalizzati unendo modelli con dati in vari formati, tra cui PDF e formati di stampa. | Combinare, ridisporre e convalidare i documenti di PDF a livello di programmazione per creare nuovi pacchetti di documenti. | Estrai proprietà, metadati e contenuto dai documenti di PDF per ulteriore elaborazione. | Conversione di documenti tra formati diversi, inclusa la convalida della conformità PDF/A per le esigenze di archiviazione. | Applicazione di firme digitali, certificazione e crittografia per proteggere i documenti. |

## Generazione di documenti

Le API per la generazione di documenti di comunicazione combinano modelli (XFA o PDF) con dati dei clienti (XML) per creare documenti personalizzati in PDF e vari formati di stampa (PS, PCL, DPL, IPL, ZPL).

### Funzionamento della generazione di documenti

Il flusso di lavoro tipico prevede:

1. Creazione di un modello con [Designer](use-forms-designer.md)
2. Preparazione dei dati XML per compilare il modello
3. Utilizzo delle API di comunicazione per unire il modello ai dati
4. Generazione di documenti di output nel formato desiderato

![Flusso di lavoro per la generazione dei documenti di comunicazione](assets/communicaions-workflow.png)

### Creazione di documenti PDF

Le API per la generazione di documenti consentono di creare documenti PDF non interattivi unendo dati XML con modelli di modulo:

![Crea documenti PDF](assets/outPutPDF_popup.png)

Puoi distribuire i PDF generati agli utenti tramite download, memorizzarli in un archivio o, facoltativamente, caricarli nell’archiviazione BLOB di Azure.

<span class="preview">Il caricamento dei PDF generati nell&#39;archiviazione BLOB di Azure è disponibile tramite il [programma di adozione anticipata](/help/forms/early-access-ea-features.md). Contatta aem-forms-ea@adobe.com dal tuo indirizzo e-mail ufficiale per partecipare.</span>

### Creazione di documenti in formato di stampa

Generare documenti in formati di stampa, tra cui:
* PostScript (PS)
* PCL (Printer Command Language)
* Lingua di stampa Zebra (ZPL)

Questi formati sono ideali per le operazioni di stampa di grandi volumi e per le esigenze di stampa particolari.

### Elaborazione in batch per più documenti

Elaborare grandi volumi di documenti in modo efficiente utilizzando le API batch:

![Flusso di lavoro elaborazione batch](assets/ou_OutputBatchMany_popup.png)

L’elaborazione in batch consente di:

* Generare documenti separati per ogni record in un&#39;origine dati XML
* Elabora i documenti in modo asincrono per migliorare le prestazioni
* Configurare vari parametri di conversione per il processo batch

## Manipolazione documento

Le API per la manipolazione dei documenti consentono di combinare, ridisporre e trasformare i documenti di PDF a livello di programmazione.

### Assembly documenti

Combinazione di più documenti PDF o XDP in un unico documento coeso:

![Assemblaggio di un semplice documento PDF da più documenti PDF](assets/as_document_assembly.png)

Le funzionalità di assemblaggio dei documenti includono:
* Creazione di semplici documenti PDF da più origini
* Creazione di portafogli PDF
* Assemblaggio di documenti crittografati
* Aggiunta della numerazione Bates per i documenti legali
* Appiattimento e assemblaggio di moduli interattivi

### Disassemblaggio documento

Suddividere i documenti PDF di grandi dimensioni in componenti più piccoli e gestibili:

![Divisione di un documento di origine basato su segnalibri in più documenti](assets/as_intro_pdfsfrombookmarks.png)

Il disassemblaggio del documento consente di:
* Estrai pagine specifiche dai documenti di origine
* Dividere i documenti in base ai segnalibri
* Creare set di documenti logici da compilazioni di grandi dimensioni

>[!NOTE]
>
> AEM Forms include molti font incorporati che si integrano perfettamente con i file PDF. Per un elenco completo dei font supportati, [fai clic qui](/help/forms/supported-out-of-the-box-fonts.md).

## Estrazione documento

<span class="preview">L&#39;estrazione del documento è disponibile tramite il [programma di adozione anticipata](/help/forms/early-access-ea-features.md). Contatta aem-forms-ea@adobe.com dal tuo indirizzo e-mail ufficiale per partecipare.</span>

Le API di estrazione documenti consentono di recuperare informazioni dai documenti di PDF, tra cui:

* Proprietà del documento (è un modulo compilabile, contiene allegati, ecc.)
* Diritti di utilizzo e autorizzazioni
* Informazioni sui metadati tramite Adobe Extensible Metadata Platform (XMP)

Questa funzionalità è particolarmente utile per i sistemi di gestione dei documenti, le soluzioni di archiviazione e l&#39;automazione dei flussi di lavoro.

## Conversione documento

### Conversione e convalida PDF/A

Conversione di documenti PDF standard in formato PDF/A per l&#39;archiviazione a lungo termine:

* Supporto per gli standard di conformità PDF/A-1a, 1b, 2a, 2b, 3a e 3b
* Convalida della conformità PDF/A
* Mantenimento dell&#39;integrità del documento con font incorporati e contenuto non compresso

### Conversione da PDF a XDP

<span class="preview">La conversione da PDF a XDP è disponibile tramite il [Programma di adozione anticipata](/help/forms/early-access-ea-features.md). Contatta aem-forms-ea@adobe.com dal tuo indirizzo e-mail ufficiale per partecipare.</span>

Converti i documenti PDF contenenti flussi XFA in formato XDP per la modifica e il riutilizzo dei modelli.

## Document Assurance {#doc-assurance}

Document Assurance include API di firma e crittografia per proteggere i documenti durante tutto il loro ciclo di vita.

### API di firma

Proteggere i documenti PDF con firme digitali e certificazione:

* Aggiungere campi di firma visibili o invisibili
* Applica firma digitale ai campi firma
* Certificare i documenti per l&#39;integrità
* Rimuovere le firme dai documenti
* Elimina campi firma dai documenti

<span class="preview">La rimozione della firma e l&#39;eliminazione del campo della firma sono disponibili tramite il [programma di adozione anticipata](/help/forms/early-access-ea-features.md). Contatta aem-forms-ea@adobe.com dal tuo indirizzo e-mail ufficiale per partecipare.</span>

### API di crittografia

Protezione del contenuto dei documenti con crittografia:

* Crittografa documenti PDF con password
* Rimuovi crittografia basata su password
* Determinare i tipi di protezione applicati ai documenti
* Recuperare le informazioni di protezione dai documenti protetti

### Utilità documenti {#doc-utility}

Le utilità per documenti forniscono funzionalità aggiuntive per l’utilizzo dei documenti di PDF:

#### API per i diritti di utilizzo (estensione Reader)

<span class="preview">I diritti di utilizzo (estensione Reader) sono disponibili tramite il [programma di adozione anticipata](/help/forms/early-access-ea-features.md). Contatta aem-forms-ea@adobe.com dal tuo indirizzo e-mail ufficiale per partecipare.</span>

Estendi la funzionalità di Adobe Reader aggiungendo diritti di utilizzo ai documenti di PDF, abilitando funzioni come:

* Compilazione e salvataggio di moduli
* Aggiunta di commenti e annotazioni
* Firma digitale
* File allegati
* Importazione/esportazione dati modulo
* Accesso ai servizi web e alle banche dati

I diritti di utilizzo disponibili includono:

* **Interazione Modulo**: Compilazione Modulo, Importazione/Esportazione Dati Modulo, Campi Modulo Dinamici/Pagine
* **Annotazioni**: commenti (online e offline), firme digitali
* **Gestione Documenti**: File Incorporati, Invia Standalone, Decodifica Dei Codici A Barre
* **Servizi in linea**: Forms in linea, accesso ai servizi Web

## Tipi di API di comunicazione {#types}

Le comunicazioni forniscono due tipi di API per soddisfare i diversi casi d’uso:

### API sincrone

**Ideale per**: generazione di documenti singoli a richiesta, a bassa latenza
**Casi d&#39;uso**: generazione di documenti attivata dall&#39;utente, applicazioni interattive
**Documentazione**: [Riferimento API sincrono](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)

### API batch (asincrone)

**Ideale per**: generazione pianificata, ad alta velocità e multipla di documenti
**Casi d&#39;uso**: rendiconti mensili, fatture, avvisi, rapporti pianificati
**Documentazione**: [Riferimento API batch](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)

## Guida introduttiva alle API di comunicazione

### Processo di onboarding

Le comunicazioni sono disponibili come modulo autonomo o componente aggiuntivo per gli utenti di Forms as a Cloud Service:

1. Per richiedere l’accesso, contatta l’ufficio vendite Adobe o il tuo rappresentante Adobe
2. Adobe consentirà l’accesso per la tua organizzazione e concederà i privilegi di amministratore
3. L’amministratore può quindi concedere l’accesso agli sviluppatori della tua organizzazione

### Abilitazione delle comunicazioni nell&#39;ambiente

Per abilitare le comunicazioni per l’ambiente Forms as a Cloud Service, effettua le seguenti operazioni:

1. Accedi a Cloud Manager e apri la tua istanza di AEM Forms as a Cloud Service
2. Apri l’opzione Modifica programma e vai alla scheda Soluzioni e componenti aggiuntivi
3. Seleziona l&#39;opzione **[!UICONTROL Forms - Comunicazioni]**

   ![Comunicazioni](assets/communications.png)

   Se hai già abilitato **[!UICONTROL Forms - Digital Enrollment]**, seleziona l&#39;opzione **[!UICONTROL Forms - Communications Add-On]**.

   ![Aggiuntivo](assets/add-on.png)

4. Fai clic su **[!UICONTROL Aggiorna]**
5. Eseguire la pipeline di build: le API di comunicazione verranno abilitate dopo il completamento corretto

>[!NOTE]
>
> Per abilitare le API di manipolazione dei documenti, aggiungi la seguente regola alla [configurazione Dispatcher](setup-local-development-environment.md#forms-specific-rules-to-dispatcher):
>
> `# Allow Forms Doc Generation requests`
> `/0062 { /type "allow" /method "POST" /url "/adobe/forms/assembler/*" }`

## Documentazione di riferimento API {#api-reference}

Le API di comunicazione sono organizzate in diverse categorie funzionali, ciascuna con documentazione di riferimento dettagliata. Questi riferimenti API forniscono informazioni complete su endpoint, parametri, formati di richiesta/risposta e requisiti di autenticazione.

### API per la generazione di documenti

| API | Descrizione | Collegamento di riferimento |
|-----|-------------|----------------|
| Generazione documento - Sincrona | Generazione di documenti on-demand con latenza ridotta per scenari interattivi | [Riferimento API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/) |
| Generazione documento - Batch | Elaborazione di grandi volumi di documenti in modo asincrono per le operazioni pianificate | [Riferimento API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/) |

### API per la manipolazione dei documenti

| API | Descrizione | Collegamento di riferimento |
|-----|-------------|----------------|
| Manipolazione documento - Sincrona | Combinare, dividere e trasformare documenti PDF utilizzando le istruzioni DDX | [Riferimento API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/) |

### Documentare le API di Assurance

| API | Descrizione | Collegamento di riferimento |
|-----|-------------|----------------|
| DocAssurance - Sincrono | Applicazione di firme digitali, certificazioni, crittografia ed estensioni di lettura | [Riferimento API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/docassurance/) |

### Parametri API comuni

Ogni categoria API dispone di parametri specifici, ma alcuni parametri comuni includono:

#### Parametri di generazione del documento

| Parametro | Tipo | Obbligatorio | Descrizione |
|-----------|------|----------|-------------|
| `template` | Stringa | Sì | Percorso del file modello XDP o PDF |
| `data` | Stringa | No | Dati XML da unire con il modello |
| `outputOptions` | Oggetto | No | Opzioni di configurazione per il documento di output |

#### Parametri di manipolazione dei documenti

| Parametro | Tipo | Obbligatorio | Descrizione |
|-----------|------|----------|-------------|
| `ddx` | Stringa | Sì | Istruzioni DDX per l&#39;assemblaggio o lo smontaggio del documento |
| `inputDocuments` | Oggetto | Sì | Mappa dei documenti di input da elaborare |
| `outputOptions` | Oggetto | No | Opzioni di configurazione per il documento di output |

#### Documenta parametri Assurance

| Parametro | Tipo | Obbligatorio | Descrizione |
|-----------|------|----------|-------------|
| `inputPDF` | Stringa | Sì | Documento PDF di input da proteggere o firmare |
| `certificateAlias` | Stringa | Condizionale | Alias del certificato per le operazioni di firma |
| `credentialPassword` | Stringa | Condizionale | Password per le credenziali utilizzate per la firma |

Per informazioni complete sui parametri, i requisiti di autenticazione e esempi di richieste/risposte, consulta la documentazione di riferimento API specifica collegata alle tabelle precedenti.

## Risorse aggiuntive {#see-also}

* [Elaborazione della comunicazione - API sincrone](/help/forms/aem-forms-cloud-service-communications.md)
* [Elaborazione della comunicazione - API batch](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
* [Architettura di AEM Forms as a Cloud Service](/help/forms/aem-forms-cloud-service-architecture.md)
* [Documentazione di riferimento API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)
* [Caratteristiche preliminari del programma](/help/forms/early-access-ea-features.md)
