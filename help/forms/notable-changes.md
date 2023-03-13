---
title: Cosa è cambiato tra AEM 6.5 Forms e AEM Cloud Services
description: Sei un utente di Experience Manager Forms e stai cercando di effettuare l’aggiornamento ad Adobe Experience Manager Forms as a Cloud Service? Scopri le modifiche più importanti prima di eseguire l’aggiornamento o la migrazione al Cloud Service.
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
contentOwner: khsingh
source-git-commit: fa8629fefe3ad29f70213b15bb31623a2f7d5420
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 0%

---

# Modifiche di rilievo per gli utenti esistenti di Adobe Experience Manager 6.5 Forms  {#notable-changes-for-existing-AEM-Forms-users}

Adobe Experience Manager Forms as a Cloud Service apporta alcune modifiche di rilievo alle funzioni esistenti rispetto ad Adobe Experience Manager Forms On-Premise e [!DNL Adobe-Managed Service] ambienti. Le differenze principali sono elencate di seguito:

| Funzionalità | [!DNL AEM Forms] as a Cloud Service | AEM 6.5 Forms |
|---|---|---|
| Architettura nativa per il cloud | ✅ | ⛌ |
| Ridimensionamento automatico in base al carico | ✅ | ⛌ |
| Nessuna interruzione delle attività per gli aggiornamenti | ✅ | ⛌ |
| Frequenza rollout delle funzioni | Agile* | Trimestrale |
| CDN (content delivery network) inclusa | ✅ | ⛌ |
| Topologie ottimizzate per la massima resilienza ed efficienza | ✅ | ⛌ |
| Ambiente di sviluppo nativo per il cloud | ✅ | ⛌ |
| Self-service tramite Cloud Manager | ✅ | ⛌ |
| Aggiornamenti automatizzati con integrazione continua e distribuzione continua (CI/CD) | ✅ | ⛌ |
| Integrazione con [!DNL Micosoft Power Automate] | ✅ | ⛌ |
| Integrazione con [!DNL DocuSign] | ✅ | ⛌ |
| Connettività semplificata con Microsoft Dynamics e Salesforce | ✅ | ⛌ |
| Connettività semplificata con gli archivi dati di Microsoft Azure | ✅ | ⛌ |
| Editor regole avanzate | ✅ | ⛌ |
| Creazione guidata modulo | ✅ | ⛌ |
| Supporto XCI personalizzato per documento record | ✅ | ⛌ |
| Forms adattivo <sup>1</sup> | ✅ | ✅ |
| API di comunicazione (Document Services) <sup>2.3</sup> | ✅ | ✅ |
| Servizio automated forms conversion <sup>4</sup> | ✅ | ✅ |
| Forms Portal <sup>5</sup> | ✅ | ✅ |
| Modello dati Forms <sup>6</sup> | ✅ | ✅ |
| HTML5 FORMS <sup>7</sup> | ⛌ | ✅ |
| Document Security | ⛌ | ✅ |

Prima di procedere con il servizio, tenere conto dei seguenti casi eccezionali:

+++ 1. Forms adattivo

* **Forms adattivo basato su XSD:** Il servizio non supporta HTML5 Forms (Mobile Forms). Se esegui il rendering dei moduli basati su XDP come HTML5 Forms, puoi continuare a utilizzare la funzione su AEM 6.5 Forms. È possibile utilizzare il modello XDP per progettare un modello per Document for Record. Il servizio non supporta Forms adattivo basato su XFA
* **Importazione di modelli di modulo adattivo:** Utilizza la pipeline di build e l’archivio Git corrispondente del programma per importare i modelli di moduli adattivi esistenti.
* **Editor regole:** AEM Forms as a Cloud Service offre una [Editor regole](rule-editor.md#visual-rule-editor). L’editor di codice non è disponibile su Forms as a Cloud Service. L’utility di migrazione consente di migrare i moduli con regole personalizzate (create nell’editor di codice). L’utility converte tali regole in funzioni personalizzate supportate su Forms as a Cloud Service. È possibile utilizzare le funzioni riutilizzabili con l’editor di regole per continuare a ottenere risultati ottenuti con gli script di regole. `onSubmitError` o `onSubmitSuccess` Le funzioni di sono ora disponibili come azioni nell’Editor di regole.
* **Bozze e proposte:** Il servizio non mantiene i metadati per le bozze e i Forms adattivi inviati.
* **Servizio preriempimento:** Per impostazione predefinita, il servizio di precompilazione unisce i dati con un modulo adattivo sul client, invece di unire i dati sul server in Forms con AEM 6.5. Questa funzione consente di migliorare il tempo necessario per la precompilazione di un modulo adattivo. Puoi sempre configurare per eseguire l’azione di unione sul server Adobe Experience Manager Forms.
* **Inviare azioni:** Il **Invia e-mail come PDF** azione non disponibile. Il **E-mail** azione di invio fornisce opzioni per l’invio di allegati e allega un documento Record (DoR) all’e-mail.
* **Componenti**: il servizio non supporta l’esperienza di firma interna ai moduli e non include i componenti Riepilogo e Verifica per Adaptive Forms.



+++


+++ 2. Document Services: API per la manipolazione dei documenti (servizio assemblatore)


Il servizio non supporta operazioni dipendenti da altri servizi o applicazioni:

* La conversione di documenti in formato non PDF in formato PDF non è supportata. Microsoft Word to PDF, Microsoft Excel to PDF e HTML to PDF, ad esempio, non sono supportati. Se i documenti sono in un formato non PDF. Converti tali documenti in formato PDF prima di utilizzarli con le API Communications Document Manipulation. Se ad esempio i documenti sono in formato Microsoft Office, HTML, PostScript (PS) o XDP, convertire i documenti in formato PDF prima di utilizzarli con i documenti PDF.
* Adobe Le conversioni basate su Distiller non sono supportate. Ad esempio, PostScript(PS) a PDF
* Le conversioni basate sui servizi di Forms non sono supportate. Ad esempio, da XDP a PDF forms.
* Il servizio non supporta la conversione di un file Signed PDF o Transparent PDF in un altro formato PDF.
* L’applicazione dei diritti di utilizzo tramite il servizio Estensioni di Reader non è disponibile.
* Il servizio non consente di convertire documenti PDF firmati o trasparenti in formato PDF/A.

+++


+++ 3. Document Services: API per la generazione di documenti (servizio di output)

In una singola chiamata API o in un batch, è possibile utilizzare un solo modello con più file XML DATI. L’utilizzo di più modelli con più file di dati in una singola chiamata API non è supportato.

+++

+++ 4. Servizio di Automated forms conversion

Il servizio non fornisce un metamodello per il servizio di Automated forms conversion. È possibile [scarica dalla documentazione di Automated forms conversion Service](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).

+++

+++ 5. Forms Portal

Il supporto per l’utilizzo anonimo di Forms Portal non è disponibile come funzionalità integrata (OOTB). È possibile personalizzare Forms Portal per abilitare la visualizzazione dei moduli per gli utenti non connessi.

+++

+++ 6. Modello dati modulo

* Il modello dati di Forms supporta solo endpoint HTTP e HTTP per l’invio dei dati. Il servizio non supporta SSL reciproco per il connettore REST e l&#39;autenticazione basata su certificato x509 per le origini dati SOAP.

* Forms as a Cloud Service consente di utilizzare Microsoft Azure Blob, Microsoft Sharepoint, Microsoft OneDrive e i servizi che supportano operazioni CRUD (Create, Read, Update, Delete) generali come archivi di dati. Sono supportate sia la specifica API Open 2.0 che la specifica API Open. Il servizio supporta anche il connettore JDBC.

+++


+++ 7. HTML5 Forms

* Il servizio non supporta HTML5 Forms (Mobile Forms). Se esegui il rendering dei moduli basati su XDP come HTML5 Forms, puoi continuare a utilizzare la funzione su AEM 6.5 Forms.

* Se si dispone di un caso d&#39;uso per acquisire dati offline e sincronizzarli al successivo ritorno online, è possibile continuare a utilizzare [AEM Forms Workspace](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-aem-forms-workspace/introduction-html-workspace.html) su AEM 6.5 Forms.

+++





+++ 8. Ambiente sviluppatore

* Un ambiente nativo per il cloud non dispone di una console web (gestione della configurazione). È possibile utilizzare [[!DNL AEM Forms] SDK as a Cloud Service per generare configurazioni](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) e la pipeline CI/CD per [distribuire la configurazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) all’istanza di Cloud Service.
* Per impostazione predefinita, le e-mail supportano solo i protocolli HTTP e HTTP. [Contatta il team di supporto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) per abilitare le porte per l’invio di e-mail e il protocollo SMTP per il tuo ambiente.
* Il servizio non supporta la conversione di un file Signed PDF o Transparent PDF in un altro formato PDF. Prima di utilizzare i bundle per i clienti con Forms as a Cloud Service, ricompila il codice personalizzato con l’ultima versione della convenzione URL adobe-aemfd-docmanager* di localized Forms ora supporta la specifica di una lingua nell’URL. La nuova convenzione URL consente di memorizzare nella cache i moduli localizzati su una rete CDN o Dispatcher. In ambiente di Cloud Service, utilizza il formato URL `http://host:port/content/forms/af/<afName>.<locale>.html` per richiedere una versione localizzata di un modulo adattivo anziché `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. L’Adobe consiglia di utilizzare il caching di Dispatcher o CDN. Consente di migliorare la velocità di rendering dei moduli precompilati
* Adobe Experience Manager Forms as a Cloud Service introduce molte nuove funzioni e possibilità nei tuoi progetti AEM. Tuttavia, sono necessarie alcune modifiche ai progetti Adobe Experience Manager Maven per renderli compatibili con AEM Cloud Service. Ad alto livello, l&#39;AEM richiede una separazione del contenuto e del codice in subpacchetti distinti per rispettare la ripartizione tra contenuto mutabile e immutabile. Utilizza il [Repository Modernizer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) strumento per ristrutturare i pacchetti di progetto esistenti separando il contenuto e il codice in pacchetti discreti per renderli compatibili con la struttura di progetto definita per Adobe Experience Manager as a Cloud Service.


+++

<!-- 

### HTML5 Forms (Mobile Forms)

The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms.

### Adaptive Forms 

* **XSD-Based Adaptive Forms:** The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms. You can use XDP-template to design a template for Document for Record. The service does not support XFA based Adaptive Forms  
* **Importing Adaptive Form templates:** Use build pipeline and corresponding Git repository of your program to import existing Adaptive Form templates. 
*  **Rule editor:** AEM Forms as a Cloud Service provides a hardened [Rule editor](rule-editor.md#visual-rule-editor). The code editor is not available on Forms as a Cloud Service. The migration utility helps you migrate your forms that have custom rules (created in code editor). The utility converts such rules into custom functions supported on Forms as a Cloud Service. You can use the reusable functions with Rule editor to continue obtaining results obtained with rule scripts  The `onSubmitError` or `onSubmitSuccess` functions are now available as actions the Rule Editor.  
* **Drafts and submissions:** The service does not retain metadata for drafts and submitted Adaptive Forms.  
* **Prefill Service:** By default, the prefill service merges data with an Adaptive Form at client as opposed to merging data on Server in AEM 6.5 Forms. The feature helps improve the time required to prefill an Adaptive Form. You can always configure to run the merge action on the Adobe Experience Manager Forms Server. 
* **Submit actions:** The **Email as PDF** action is not available. The **Email** submit action provide options to send attachments and attach Document of Record (DoR) with email. 
* **Components**:  The service does not support in-form signing experience and does not include the Summary and Verify components for Adaptive Forms.  
* **Forms portal**: Support for anonymous use of Forms portal is not available out of the box (OOTB). You can customize the forms portal to enable displaying forms for non-logged in users.

### Form Data Model

* Forms data model supports only HTTP and HTTPs endpoints to submit data. The service does not support Mutual SSL for REST connector and x509 certificate-based authentication for SOAP data sources. * Forms as a Cloud Service allows to use Microsoft Azure Blob, Microsoft Sharepoint, Microsoft OneDrive, and services supporting general CRUD (Create, Read, Update, and Delete) operations as data stores, both Open API specification 2.0 and Open API specification are supported. The service also provides support for JDBC connector.


### Automated Forms Conversion Service     

The service does not provide meta-model for Automated Forms Conversion Service. You can [download it from Automated Forms Conversion Service documentation](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).


### Configurations

* Email support only HTTP and HTTPs protocols, by default. [Contact the support team](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) to enable ports for sending emails and to enable SMTP protocol for your environment.  
* If you use custom bundles, recompile your code with latest version of adobe-aemfd-docmanager before using these bundles with Forms as a Cloud Service. 


### Document Services: Document Manipulation APIs (Assembler Service)

The service does not support operations dependent on other services or applications:  

* Conversion of documents in a non-PDF format to a PDF format is not supported. For example, Microsoft Word to PDF, Microsoft Excel to PDF, and HTML to PDF are not supported. If your documents are in a non-PDF format. Convert such documents to PDF format before using those with Communications Document Manipulation APIs. For example, if your documents are in Microsoft Office, HTML, PostScript (PS), XDP format, convert these documents to PDF format before using those with PDF documents. 
* Adobe Distiller-based conversions are not supported. For example, PostScript(PS) to PDF
* Forms Service-based conversions are not supported. For example, XDP to PDF Forms.
* The service does not support converting a Signed PDF or Transparent PDF to another PDF format.
* Applying usage rights using Reader Extensions Service is not available. 
* The service does not provide the ability to convert signed or transparent PDF Documents to PDF/A format. 

### Document Services: Document Generation APIs (Output Service)

* In a single API call or batch, you can use one template with multiple DATA XML files. Using mutiple templates with multiple data files in a single API call is not supported. 

### Other differences

* A cloud-native environment does not have web console (configuration manager). You can use [[!DNL AEM Forms] as a Cloud Service SDK to generate configurations](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) and CI/CD pipeline to [deploy the configuration](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) to your Cloud Service instance.
* Email support only HTTP and HTTPs protocols, by default. [Contact the support team](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) to enable ports for sending emails and to enable SMTP protocol for your environment.
* The service does not support converting a Signed PDF or Transparent PDF to another PDF format.* Before using your customer bundles with Forms as a Cloud Service, recompile your custom code with the latest version of adobe-aemfd-docmanager* URL convention of localized Adaptive Forms now supports specifying a locale in the URL. New URL convention enables caching localized forms on a Dispatcher or CDN. On Cloud Service environment, use the URL format `http://host:port/content/forms/af/<afName>.<locale>.html` to request a localized version of an Adaptive Form instead of `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. Adobe recommends using Dispatcher or CDN caching. It helps improve rendering speed of prefilled forms 
* Adobe Experience Manager Forms as a Cloud Service brings many new features and possibilities into your AEM Projects. However, there are some changes required to Adobe Experience Manager Maven projects to be compatible with AEM Cloud Service. At a high-level, AEM requires a separation of content and code into discrete subpackages to respect the split between mutable and immutable content. Use the [Repository Modernizer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) tool to restructure existing project packages by separating content and code into discrete packages to be compatible with the project structure defined for Adobe Experience Manager as a Cloud Service.
-->




