---
title: Architettura AEM Forms as a Cloud Service per Forms adattivo e API di comunicazione
description: Scopri l'architettura di  [!DNL AEM Forms] as a Cloud Service per scoprire gli aspetti relativi a scalabilità, resilienza e prestazioni della piattaforma.
role: Admin, Developer, User
feature: Adaptive Forms
exl-id: 9d677bee-50ca-460e-b503-6b7799900735
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 2%

---

# Architettura di Forms as a Cloud Service [!DNL AEM] {#architecture}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/aem-forms-architecture-deployment.html?lang=it) |
| AEM as a Cloud Service | Questo articolo |

[!DNL Adobe Experience Manager Forms] as a Cloud Service è una soluzione nativa per il cloud che consente alle aziende di creare, gestire, pubblicare e aggiornare moduli digitali e comunicazioni complesse, integrando al contempo i dati inviati con processi di back-end, regole aziendali e salvando i dati in un archivio dati esterno. Estende [!DNL Adobe Experience Manager as a Cloud Service]. Per ulteriori informazioni su scalabilità, distribuzione, ambienti e altre infrastrutture, vedere [Introduzione all&#39;architettura di [!DNL Adobe Experience Manager as a Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html?lang=it).

AEM Forms as a Cloud Service supporta due casi d’uso principali: iscrizione digitale e comunicazioni con i clienti. Le illustrazioni seguenti illustrano l’architettura di entrambi i casi d’uso.

## Iscrizione digitale Forms

![Registrazione digitale Forms](assets/forms-cloud-service-architecture-forms-digital-enrollment.svg)

## Comunicazioni Forms

![Comunicazione Forms](assets/forms-cloud-service-architecture-forms-communications.svg)

## Applicabilità e casi d’uso

### Assicurazione

## AEM Forms è in grado di gestire le operazioni assicurative su larga scala?

Sì. Se implementato utilizzando le architetture consigliate su Adobe Managed Services o cloud privato, AEM Forms supporta l’invio di moduli a volumi elevati e carichi di lavoro su scala aziendale.

## AEM Forms è sicuro per i dati assicurativi?

Sì. AEM Forms supporta la trasmissione sicura dei dati, l’accesso controllato e i meccanismi di autenticazione aziendale, rendendola adatta alla gestione di dati assicurativi sensibili.

## Componenti

Forms as a Cloud Service comprende più componenti:

### CDN (Content Delivery Network)

Ogni programma as a Cloud Service di AEM Forms ha accesso a [servizio CDN integrato](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn). È incluso nella licenza di Forms as a Cloud Services.

### Autore

Un’istanza Autore è un’istanza di AEM Forms as a Cloud Service in esecuzione nella modalità di esecuzione Autore standard. È destinato agli utenti interni, ai progettisti di moduli e agli sviluppatori. Un ambiente di authoring abilita le seguenti funzionalità:

* Authoring e gestione dei moduli.
* Connessione al servizio di conversione automatica dei moduli per convertire un modulo PDF o XDP in un modulo adattivo.
* Creazione ed esecuzione di flussi di lavoro incentrati su Forms.
* Gestione delle risorse dei moduli adattivi.
* Gestione delle risorse di comunicazione.
* API RESTful sincrone (API in tempo reale) e API Batch per creare, assemblare e distribuire comunicazioni personalizzate e orientate al brand.
* API sincrone per combinare, ridisporre e convalidare documenti PDF.

### Pubblicazione

Un’istanza Publish è un’as a Cloud Service di AEM Forms in esecuzione nella modalità di esecuzione Pubblicazione standard. Le istanze di pubblicazione sono destinate agli utenti finali di applicazioni basate su moduli, ad esempio gli utenti che accedono a un sito Web pubblico e inviano moduli. Abilita le seguenti funzionalità:

* Rendering e invio di moduli per gli utenti finali.
* Trasporto dei dati grezzi del modulo per ulteriore elaborazione e archiviazione nel sistema di registrazione finale.
* Connessione a Customer Managed Storage per l&#39;archiviazione dei dati.
* Connessione ad Adobe Sign per la firma elettronica di un record di invio di un modulo adattivo.
* Sincronizza le API per creare, assemblare e distribuire comunicazioni personalizzate e orientate al brand.
* Sincronizza le API per combinare, ridisporre e convalidare i documenti PDF.

La replica inversa non è disponibile in AEM as a Cloud Service per inviare contenuti/dati dal servizio di pubblicazione al servizio di authoring. Tuttavia, puoi configurare un Forms adattivo in esecuzione alla pubblicazione per inviare dati a un flusso di lavoro su un autore (i flussi di lavoro possono essere eseguiti solo sull’autore). Questa funzione è utile nei casi di utilizzo dell’approvazione.

#### Dispatcher

[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=it) è lo strumento di caching e/o bilanciamento del carico di Adobe Experience Manager che può essere utilizzato con un server Web di classe enterprise.

### Servizi Adobe

**Servizio automatizzato di conversione moduli**

[Il servizio di conversione automatica dei moduli](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/introduction.html?lang=it) converte automaticamente i moduli PDF e XFA in moduli adattivi basati su HTML5, reattivi e facili da usare sui dispositivi.

**Adobe Sign**

Adobe Sign è un servizio di firma elettronica basato su cloud che consente all’utente di inviare, firmare, tracciare e gestire i processi di firma tramite un browser o un dispositivo mobile. È possibile integrare Adobe Sign con un modulo adattivo per automatizzare i flussi di lavoro di firma, semplificare i processi a firma singola e multipla e firmare elettronicamente i moduli adattivi.

<!-- **PDF Service API**
Adobe’s PDF Services API lets create, combine, export, and extract data from PDFs through powerful and flexible cloud-based APIs. -->

### Archiviazione gestita dal cliente

Forms as a Cloud Service fornisce opzioni per archiviare il contenuto in un sistema di archiviazione esterno, ad esempio Archivio BLOB, Database o un servizio di archiviazione. Puoi anche memorizzare i dati dei flussi di lavoro in elaborazione (dati sulle variabili di flusso di lavoro di AEM) che contengono elementi di dati personali sensibili (SPD) in un archivio gestito dal cliente per un’elaborazione sicura. Adobe consiglia di memorizzare dati sensibili solo su archivi gestiti dal cliente.

È possibile utilizzare **Connettore di archiviazione unificata** per connettersi all&#39;archiviazione BLOB e **Modello dati modulo (FDM)** per connettersi ai database o ai servizi back-end (RESTful, SOAP, Archiviazione BLOB di Azure e altro).

### Servizi per documenti

I servizi di documentazione sono i seguenti:

* **Servizio di output (comunicazioni - API per la generazione di documenti)** consente di creare documenti approvati, personalizzati e standardizzati dal marchio, quali corrispondenza aziendale, rendiconti, lettere di elaborazione delle richieste di rimborso, avvisi sui benefit, fatture mensili o kit di benvenuto.

* **Il servizio Assembler (Communications - Document Manipulation APIs)** consente di combinare, ridisporre e convalidare i documenti di PDF.

* Il servizio **Document of Record (DoR)** consente di generare documenti di record (DoR). Il servizio viene eseguito nei propri pod separati dalle istanze Author e Publish di Forms as a Cloud Service. Aiuta a fornire prestazioni migliori e scalare i pod in modo indipendente a seconda del carico.

### Cloud Manager

Cloud Manager è un componente essenziale di [AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=it). È il punto di ingresso singolo per le operazioni e gli sviluppatori dei nostri clienti. È il luogo da cui è possibile gestire i programmi e gli ambienti di AEM. Cloud Manager si è evoluto come portale self-service in cui è possibile creare e configurare i componenti principali di AEM as a Cloud Service:

* Creazione e gestione di programmi
* Creazione e gestione degli ambienti AEM all’interno dei programmi
* Creazione e gestione delle pipeline per la distribuzione del codice cliente e della configurazione in un particolare ambiente
* Ricezione di notifiche su importanti eventi del ciclo di vita per questi componenti (ad esempio, aggiornamenti dei prodotti)
Per ulteriori informazioni su Cloud Manager, vedere [Comprendere Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/cloud-manager/understand-cloud-manager-for-aem.html?lang=it) e [Introduzione a Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=it).

### Developer Console

Un Developer Console fornisce vari dettagli di ogni ambiente Forms as a Cloud Service in esecuzione. Questi dettagli sono utili per il debug dell’ambiente. Per informazioni dettagliate, vedere [Debug di AEM as a Cloud Service con Developer Console](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=it).

<!--

+++CDN (Content Delivery Network):

Every AEM Forms as a Cloud Service program has access to Fastly CDN service. It is included in the licence of Forms as a Cloud Services.

+++

+++Adaptive Forms
Adaptive Forms enable customers to author web-friendly reflowable web forms and fragments that are used by the customers for their data capture needs. This feature enables customers to manage their complex data capture needs easily, by using multiple integrations with Adobe Sign, Document Services, Form Data Model (FDM), Automated Forms Conversion service, and more.

+++

+++Automated Forms Conversion Service (AFCS)
Automated Forms Conversion service helps accelerate digitization and modernization of data capture experience through automated conversion of PDF forms to adaptive forms. The service, powered by Adobe AI, automatically converts your PDF forms to device-friendly, responsive, and HTML5-based adaptive forms. While using the existing investments in PDF Forms and XFA, the service also applies appropriate validations, styling, and layout to adaptive form fields during conversion.

+++

+++Form Data Model (FDM)
The Form Data Model (FDM) feature is the standard way of creating data integrations with external/internal data sources and using them across the different Forms as a Cloud Service features. FDM provides a rich editor for customers to integrate, define, and manage relationships between the different entities and data sources and perform operations on them. Form data is stored in a data store hosted on the customer premises. Organizations can also use blob store hosted by the cloud provider and Adobe Experince Platform to store data.

+++

+++Forms Workflows
Forms-centric workflows is an extension to the default AEM Workflow and provides our customers with additional workflow capabilities like Form Data review, task assignment, and document services invocation.

+++

+++Communications
Forms as a Cloud Service offering consists of multiple services tailored specifically for document processing.

+++

+++Document of Record
A Document of Record is a PDF version of a form. It provides an ability to keep a record of the information  that you provide and submit in an Adaptive Form in PDF fromat. The service provides a default DoR template and tools to develop a custom template.

+++

## Terminologies

<!-- ## Cloud Manager{#cloud-manager}

Cloud Manager is an essential component to [AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=it). Each new tenant of the [!DNL AEM Forms] as a Cloud Service is first provisioned for Cloud Manager access. Cloud Manager is the single-entry point for the operations and developer persona of our customers. It is the place from where the AEM programs and environments can be managed. Cloud Manager has evolved as a self-service portal where the main components of the AEM as a Cloud Service can be created and configured:

* Creating and managing programs
* Creating and managing the AEM environments within the programs
* Creating and managing the pipelines for deploying the customer code and configuration to a particular environment
* Getting notified of important lifecycle events for these components (for example, product updates)
For more information about Cloud Manager, see [Understand Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/cloud-manager/understand-cloud-manager-for-aem.html?lang=it) and [Introduction to Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=it).

## Users and Authentication {#users-and-authentication}

AEM as a Cloud Service includes Admin Console support for AEM instances and Adobe Identity Management System (IMS) based authentication. The Admin Console allows administrators to centrally manage all Experience Cloud users. Users and Groups can be assigned to product profiles associated with AEM as a Cloud Service instances, allowing them to log in to that instance. For more information about users, authentication, and, and accessing an instance of AEM as a Cloud Service, see [IMS Support for [!DNL Adobe Experience Manager] as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=it#introduction).

Various personas are involved in a typical [!DNL AEM Forms] project. After you log in to your [!DNL AEM Forms] as a Cloud Service instance, you can [add users in admin console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=it) for personas applicable to your organization or project and [assign users to built-in groups](forms-groups-privileges-tasks.md) to provide them required privileges.

To learn various in-built [!DNL AEM Forms] specific user groups and privileges available on [!DNL AEM Forms] as a Cloud Services instance, see [Configure, user, roles and groups](forms-groups-privileges-tasks.md). 

## Developer Experience {#developer-experience}

The new architecture supporting AEM as a Cloud Service brings some key changes to the overall developer experience. One of the major goals for the changes to developer experience is to allow migration to AEM as a Cloud Service as quickly as possible, with little modifications to existing custom code.

## Cloud development {#cloud-development}

Here are the guidelines to run your existing code smoothly on AEM as a Cloud Service environment:

* Store your code and configurations to the Git repository of the associated Cloud Manager program. It makes managing and integrating code with CI/CD a breeze.  
* Make application code and configuration compatible with the baseline [!DNL AEM Forms] images. Using the latest APIs helps to build faster and secure applications.
* Use the Cloud Manager pipeline associated with the Cloud Manager environment to build and deploy applications. It helps you bring the latest features and bug fixed for [!DNL AEM Forms] as a Cloud Service to your environment.
* Try that your custom applications pass all the code quality, security, and performance gates enforced in the pipeline. It helps build secure and better performing applications which leads to better customer experience. You can always use Cloud Manager UI to skip some checks.
This process is commonly referred to as cloud-first development. [!DNL AEM Forms] as a Cloud Service also provides an SDK to support rapid development before the pending code and configuration changes are attempted in the cloud.
Some interfaces that were previously part of the AEM QuickStart are no longer available to the users of the AEM as a Cloud Service environment. For instance, the Web Console where OSGI bundles and their associated configuration are managed. The CRXDE Lite content repository browser becomes only accessible on non-production environment types. A subset of the Web Console functionalities that developers require, especially when it comes to diagnostics and status purposes, is made available via a new developer console.
Also, one of the most common requirements for developers is quick access to the log files of the various environments. With [!DNL AEM Cloud Service], the log files of the different nodes in the Author, Publish are made available via the Cloud Manager, either in the form of files that can be downloaded or via APIs for tailing the logs. Due to the clear separation of code and content, developers can use a particular process for updating content as part of a deployment. The typical use cases for mutable content are:
* Standard “default” content that is part of the customer project (for example, folders, templates, workflows...)
* Search index definitions
* ACLs and permissions
* Service users and user groups
Set up your development environment, [Configure your CI/CD Pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html?lang=it), and learn to [deploy your code](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=it) on the environment. -->

### Authoring di moduli adattivi {#local-development}

Quando si imposta e si configura un ambiente as a Cloud Service [!DNL AEM Forms], vengono impostati gli ambienti di sviluppo, staging e produzione. Inoltre, imposta e configura un ambiente di sviluppo locale per le iterazioni e lo sviluppo rapidi. È possibile scaricare e configurare l&#39;archivio delle funzionalità aggiuntive di AEM SDK e [!DNL AEM Forms] per configurare un ambiente di sviluppo as a Cloud Service [!DNL Forms] locale.  Per istruzioni dettagliate, vedere [Configurare un ambiente di sviluppo locale](setup-local-development-environment.md).

## Debugging {#debugging}

AEM as a Cloud Service viene eseguito su un’infrastruttura cloud scalabile e self-service. Richiede che gli sviluppatori di AEM comprendano ed eseguano il debug di vari aspetti di AEM as a Cloud Service, dalla generazione e distribuzione fino a ottenere i dettagli sull’esecuzione delle applicazioni AEM. Per informazioni dettagliate, vedere [Debug di AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=it).


>[!MORELIKETHIS]
>
>* [Introduzione ad AEM Forms as a Cloud Service Communications](/help/forms/aem-forms-cloud-service-communications-introduction.md)
>* [Elaborazione batch di comunicazioni AEM Forms as a Cloud Service](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
>* [Elaborazione comunicazione - API sincrone](/help/forms/aem-forms-cloud-service-communications.md)
