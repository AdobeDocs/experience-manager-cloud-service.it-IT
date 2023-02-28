---
title: Modifiche apportate tra AEM 6.5 Forms e AEM Cloud Services
description: Sei un utente di Experience Manager Forms e vuoi effettuare l’aggiornamento ad Adobe Experience Manager Forms as a Cloud Service? Scopri le modifiche più importanti prima di eseguire l’aggiornamento o la migrazione al Cloud Service.
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
contentOwner: khsingh
source-git-commit: f44a789984c38f6d34eb5c7d6999d5148b15aec8
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 0%

---

# Modifiche di rilievo per gli utenti Forms esistenti di Adobe Experience Manager 6.5  {#notable-changes-for-existing-AEM-Forms-users}

Adobe Experience Manager Forms as a Cloud Service apporta alcune modifiche di rilievo alle funzioni esistenti rispetto ad Adobe Experience Manager Forms On-Premise e [!DNL Adobe-Managed Service] ambienti. Le differenze chiave sono elencate di seguito:

| Funzionalità/Funzionalità | [!DNL AEM Forms] as a Cloud Service | AEM 6.5 Forms |
|---|---|---|
| Architettura nativa per il cloud | ✅ | ⛌ |
| Ridimensionamento automatico in base al carico | ✅ | ⛌ |
| Nessun tempo di inattività per gli aggiornamenti | ✅ | ⛌ |
| Frequenza di rollout delle funzioni | Agile* | Trimestrale |
| CDN (content delivery network) incluso | ✅ | ⛌ |
| Topologie ottimizzate per la massima resilienza ed efficienza | ✅ | ⛌ |
| Ambiente di sviluppo nativo per cloud | ✅ | ⛌ |
| Self-Service tramite Cloud Manager | ✅ | ⛌ |
| Aggiornamenti automatizzati con integrazione continua e distribuzione continua (CI/CD) | ✅ | ⛌ |
| Integrazione con [!DNL Micosoft Power Automate] | ✅ | ⛌ |
| Integrazione con [!DNL DocuSign] | ✅ | ⛌ |
| Facile connettività con Microsoft Dynamics e Salesforce | ✅ | ⛌ |
| Facile connettività con gli archivi dati di Microsoft Azure | ✅ | ⛌ |
| Editor di regole avanzate | ✅ | ⛌ |
| Creazione guidata modulo | ✅ | ⛌ |
| Supporto XCI personalizzato per documenti di record | ✅ | ⛌ |
| Forms adattivo <sup>1</sup> | ✅ | ✅ |
| API di comunicazione (Document Services) <sup>2,3</sup> | ✅ | ✅ |
| Servizio automated forms conversion <sup>4</sup> | ✅ | ✅ |
| Portale Forms <sup>5</sup> | ✅ | ✅ |
| Modello dati Forms <sup>6</sup> | ✅ | ✅ |
| HTML5 Forms <sup>7</sup> | ⛌ | ✅ |
| Document Security | ⛌ | ✅ |

Prima di procedere con il servizio, tenere conto dei seguenti casi eccezionali:

+++ 1. Forms adattivo

* **Forms adattivo basato su XSD:** Il servizio non supporta HTML5 Forms (Mobile Forms). Se esegui il rendering dei moduli basati su XDP come HTML5 Forms, puoi continuare a utilizzare la funzione su Forms 6.5. È possibile utilizzare XDP-template per progettare un template per Document for Record. Il servizio non supporta Forms adattivo basato su XFA
* **Importazione di modelli di moduli adattivi:** Utilizza la pipeline di compilazione e l’archivio Git corrispondente del programma per importare i modelli di moduli adattivi esistenti.
* **Editor di regole:** AEM Forms as a Cloud Service fornisce un [Editor di regole](rule-editor.md#visual-rule-editor). L&#39;editor di codice non è disponibile su Forms as a Cloud Service. L’utility di migrazione consente di migrare i moduli con regole personalizzate (create nell’editor di codice). L&#39;utility converte tali regole in funzioni personalizzate supportate su Forms as a Cloud Service. È possibile utilizzare le funzioni riutilizzabili con l&#39;editor di regole per continuare a ottenere i risultati ottenuti con gli script di regole Il `onSubmitError` o `onSubmitSuccess` Le funzioni sono ora disponibili come azioni nell’editor di regole.
* **Progetti e osservazioni:** Il servizio non conserva i metadati per le bozze e invia Adaptive Forms.
* **Servizio di precompilazione:** Per impostazione predefinita, il servizio di precompilazione unisce i dati con un modulo adattivo sul client anziché con l’unione dei dati sul server in Forms 6.5 AEM. Questa funzione consente di migliorare il tempo necessario per precompilare un modulo adattivo. È sempre possibile configurare l&#39;esecuzione dell&#39;azione di unione sul server Adobe Experience Manager Forms.
* **Azioni di invio:** La **Invia e-mail come PDF** azione non disponibile. La **E-mail** l’azione di invio fornisce opzioni per l’invio di allegati e allega documento di record (DoR) con e-mail.
* **Componenti**: Il servizio non supporta l’esperienza di firma in-form e non include i componenti Riepilogo e Verifica per Adaptive Forms.



+++


+++ 2. Servizi documentali: API di manipolazione documenti (servizio Assembler)


Il servizio non supporta operazioni dipendenti da altri servizi o applicazioni:

* La conversione di documenti in formato non PDF in formato PDF non è supportata. Ad esempio, Microsoft Word in PDF, Microsoft Excel in PDF e HTML in PDF non sono supportati. Se i documenti sono in un formato diverso da PDF. Converti tali documenti in formato PDF prima di utilizzare quelli con le API di manipolazione documenti di comunicazione. Ad esempio, se i documenti sono in formato Microsoft Office, HTML, PostScript (PS) e XDP, convertire questi documenti in formato PDF prima di utilizzarli con i documenti PDF.
* Adobe Le conversioni basate su Distiller non sono supportate. Ad esempio, da PostScript(PS) a PDF
* Le conversioni basate su servizi Forms non sono supportate. Ad esempio, da XDP a PDF forms.
* Il servizio non supporta la conversione di un PDF o di un PDF trasparente con firma in un altro formato di PDF.
* L’applicazione dei diritti di utilizzo tramite il servizio Estensioni di Reader non è disponibile.
* Il servizio non consente di convertire documenti PDF firmati o trasparenti in formato PDF/A.

+++


+++ 3. Servizi documentali: API per la generazione di documenti (servizio di output)

In una singola chiamata API o batch, puoi utilizzare un solo modello con più file XML DATI. L’utilizzo di più modelli con più file di dati in una singola chiamata API non è supportato.

+++

+++ 4. Servizio Automated forms conversion

Il servizio non fornisce un metamodello per il servizio di Automated forms conversion. È possibile [scaricarlo dalla documentazione di Automated forms conversion Service](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).

+++

+++ 5. Portale Forms

Il supporto per l’uso anonimo di Forms Portal non è disponibile come standard (OOTB). Puoi personalizzare il portale Forms per abilitare la visualizzazione dei moduli per gli utenti non connessi.

+++

+++ 6. Modello dati modulo

* Il modello dati Forms supporta solo endpoint HTTP e HTTP per l’invio dei dati. Il servizio non supporta SSL reciproco per il connettore REST e l’autenticazione basata su certificato x509 per le origini dati SOAP.

* Forms as a Cloud Service consente di utilizzare Microsoft Azure Blob, Microsoft Sharepoint, Microsoft OneDrive e i servizi che supportano le operazioni generali CRUD (creazione, lettura, aggiornamento ed eliminazione) come archivi di dati, sono supportate sia la specifica API Open 2.0 che la specifica API Open. Il servizio supporta anche il connettore JDBC.

+++


+++ 7. HTML5 Forms (Mobile Forms)

* Il servizio non supporta HTML5 Forms (Mobile Forms). Se esegui il rendering dei moduli basati su XDP come HTML5 Forms, puoi continuare a utilizzare la funzione su Forms 6.5.

* Se hai un caso d’uso per acquisire i dati offline e sincronizzarli la prossima volta che ritorni online, puoi continuare a utilizzare la funzione [AEM Forms Workspace](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-aem-forms-workspace/introduction-html-workspace.html) funzionalità su Forms 6.5 AEM.

+++





+++ 8. Ambiente per sviluppatori

* Un ambiente nativo per il cloud non dispone di console Web (gestione della configurazione). È possibile utilizzare [[!DNL AEM Forms] SDK as a Cloud Service per generare configurazioni](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) e la pipeline CI/CD a [distribuire la configurazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) all&#39;istanza di Cloud Service.
* Per impostazione predefinita, le e-mail supportano solo i protocolli HTTP e HTTP. [Contatta il team di supporto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) per abilitare le porte per l’invio di e-mail e per abilitare il protocollo SMTP per l’ambiente.
* Il servizio non supporta la conversione di un PDF o di un PDF trasparente con firma in un altro formato di PDF. Prima di utilizzare i bundle dei clienti con Forms as a Cloud Service, ricompila il codice personalizzato con l&#39;ultima versione della convenzione URL adobe-aemfd-docmanager* di adattivo localizzato Forms ora supporta la specifica di impostazioni internazionali nell&#39;URL. La nuova convenzione URL consente di memorizzare nella cache i moduli localizzati su un’istanza di Dispatcher o CDN. Nell’ambiente di Cloud Service, utilizza il formato URL `http://host:port/content/forms/af/<afName>.<locale>.html` per richiedere una versione localizzata di un modulo adattivo anziché `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. Adobe consiglia di utilizzare Dispatcher o la memorizzazione in cache CDN. Consente di migliorare la velocità di rendering dei moduli precompilati
* Adobe Experience Manager Forms as a Cloud Service introduce molte nuove funzioni e possibilità nei progetti AEM. Tuttavia, sono necessarie alcune modifiche per rendere i progetti Adobe Experience Manager Maven compatibili con AEM Cloud Service. Ad alto livello, AEM richiede una separazione di contenuto e codice in pacchetti secondari distinti per rispettare la suddivisione tra contenuto mutabile e immutabile. Utilizza la [Modernizzatore dell&#39;archivio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) strumento per ristrutturare i pacchetti di progetto esistenti separando il contenuto e il codice in pacchetti discreti in modo che siano compatibili con la struttura di progetto definita per Adobe Experience Manager as a Cloud Service.


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




