---
title: Experience Manager [!DNL AEM Forms] Architettura as a Cloud Service
description: Comprendere l'architettura [!DNL AEM Forms] as a Cloud Service per scoprire gli aspetti relativi a scalabilità, resilienza e prestazioni della piattaforma.
exl-id: 9d677bee-50ca-460e-b503-6b7799900735
source-git-commit: cd9ef0db59f07173c8c5bd4b38ff946b774ce53c
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 2%

---

# [!DNL AEM] Architettura as a Cloud Service di Forms {#architecture}

[!DNL Adobe Experience Manager Forms] as a Cloud Service è una soluzione nativa per il cloud che consente alle aziende di creare, gestire, pubblicare e aggiornare complessi moduli digitali e comunicazioni, integrando i dati inviati con processi back-end, regole aziendali e salvando i dati in un archivio dati esterno. Si estende [!DNL Adobe Experience Manager as a Cloud Service]. Per ulteriori informazioni su scalabilità, distribuzione, ambienti e altre infrastrutture, consulta [Introduzione all&#39;architettura di [!DNL Adobe Experience Manager as a Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html).

AEM Forms as a Cloud Service supporta due casi d’uso principali: Iscrizione digitale e comunicazioni con i clienti. Le illustrazioni seguenti descrivono l’architettura per entrambi i casi d’uso.

## Registrazione digitale Forms

![Iscrizione Forms-Digital](assets/forms-cloud-service-architecture-forms-digital-enrollment.svg)

## Comunicazioni Forms

![Comunicazione Forms](assets/forms-cloud-service-architecture-forms-communications.svg)

## Componenti

Forms as a Cloud Service comprende più componenti:

### CDN (Content Delivery Network)

Ogni programma AEM Forms as a Cloud Service ha accesso a [servizio CDN integrato](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html). È incluso nella licenza di Forms as a Cloud Services.

### Autore

Un autore è un’istanza as a Cloud Service di AEM Forms in esecuzione nella modalità di esecuzione standard di Author. È destinato a utenti interni, designer e sviluppatori di moduli. Un ambiente di authoring abilita le seguenti funzionalità:

* Creazione e gestione dei moduli.
* Connessione al servizio Automated forms conversion per convertire un modulo PDF o XDP in un modulo adattivo.
* Creazione ed esecuzione di flussi di lavoro incentrati su Forms.
* Gestione delle risorse dei moduli adattivi.
* Gestione delle risorse di Communications.
* API RESTful sincrone (API Real-time) e API Batch per creare, assemblare e fornire comunicazioni personalizzate e orientate al marchio.
* API sincrone per combinare, ridisporre e convalidare i documenti PDF.

### Pubblicazione

Un’istanza Publish è un’istanza AEM Forms as a Cloud Service in esecuzione nella modalità di esecuzione standard Publish. Le istanze di pubblicazione sono destinate agli utenti finali di applicazioni basate su moduli, ad esempio gli utenti che accedono a un sito web pubblico e inviano moduli. Abilita le seguenti funzionalità:

* Rendering e invio di moduli per gli utenti finali.
* Trasporto dei dati dei moduli non trasmessi per ulteriore elaborazione e archiviazione nel sistema di registrazione finale.
* Connessione allo storage gestito dal cliente per l&#39;archiviazione dei dati.
* Connessione con Adobe Sign per la firma elettronica di un record di invio del modulo adattivo.
* Sincronizza API per creare, assemblare e distribuire comunicazioni personalizzate e orientate al brand.
* Sincronizza API per combinare, ridisporre e convalidare i documenti PDF.

La replica inversa non è disponibile su AEM as a Cloud Service per inviare contenuti/dati dal servizio di pubblicazione al servizio di authoring. Tuttavia, puoi configurare un Forms adattivo in esecuzione su Pubblica per inviare dati a un flusso di lavoro su un autore (i flussi di lavoro possono essere eseguiti solo sull’autore). Questo è utile nei casi di utilizzo dell’approvazione.

#### Dispatcher

[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html) è lo strumento di caching e/o bilanciamento del carico di Adobe Experience Manager che può essere utilizzato con un server web di classe enterprise.

### Servizi Adobe

**Servizio automated forms conversion**

[servizio automated forms conversion](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/introduction.html?lang=it) converte automaticamente i moduli PDF e XFA in moduli adattivi facili da usare su dispositivi, reattivi e basati su HTML5.

**Adobe Sign**

Adobe Sign è un servizio di firma elettronica basato su cloud che consente all’utente di inviare, firmare, tenere traccia e gestire i processi di firma utilizzando un browser o un dispositivo mobile. È possibile integrare Adobe Sign con un modulo adattivo per automatizzare i flussi di lavoro di firma, semplificare i processi di firma singola e multipla e per firmare elettronicamente i moduli adattivi.

<!-- **PDF Service API**
Adobe’s PDF Services API lets create, combine, export, and extract data from PDFs through powerful and flexible cloud-based APIs. -->

### Archiviazione gestita da clienti

Forms as a Cloud Service fornisce opzioni per archiviare il contenuto in un sistema di storage esterno, ad esempio Blob Store, Database o un servizio di archiviazione. È inoltre possibile archiviare i dati dei flussi di lavoro nel processo (AEM dati variabili del flusso di lavoro) contenenti elementi di dati personali sensibili (SPD) in un archivio gestito dal cliente per un’elaborazione sicura. Adobe consiglia di memorizzare dati sensibili solo negli archivi gestiti dai clienti.

È possibile utilizzare **Connettore di archiviazione unificata** per la connessione a Blob Storage e **Modello dati modulo** per connettersi a database o servizi di backend (RESTful, SOAP, Azure Blob Storage e altro).

### Document Services

I servizi documentali costituiscono:

* **Servizio di output (comunicazioni - API per la generazione di documenti)** consente di creare documenti approvati dal marchio, personalizzati e standardizzati, ad esempio corrispondenze aziendali, dichiarazioni, lettere di elaborazione delle richieste, note sui benefit, fatture mensili o kit di benvenuto.

* **Servizio Assembler (comunicazioni - API di manipolazione documenti)** consente di combinare, ridisporre e convalidare i documenti PDF.

* **Servizio del documento di registrazione (DoR)** consente di generare documenti di record (DoR). Il servizio viene eseguito nei propri pod separati dalle istanze Author e Publish di Forms as a Cloud Service. Aiuta a fornire prestazioni migliori e scalare i baccelli in modo indipendente a seconda del carico.

### Cloud Manager

Cloud Manager è un componente essenziale per [AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html). È il punto di ingresso unico per le operazioni e l’utente tipo sviluppatore dei nostri clienti. È il luogo da cui è possibile gestire i programmi e gli ambienti AEM. Cloud Manager si è evoluto come portale self-service in cui è possibile creare e configurare i componenti principali dell’AEM as a Cloud Service:

* Creazione e gestione di programmi
* Creazione e gestione degli ambienti AEM all’interno dei programmi
* Creazione e gestione delle pipeline per la distribuzione del codice cliente e della configurazione in un ambiente specifico
* Ricevere notifiche su importanti eventi del ciclo di vita per questi componenti (ad esempio, aggiornamenti dei prodotti) Per ulteriori informazioni su Cloud Manager, consulta [Comprendere Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/cloud-manager/understand-cloud-manager-for-aem.html) e [Introduzione a Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=it).

### Console per sviluppatori

Una Console per sviluppatori fornisce vari dettagli su ogni ambiente in cui è in esecuzione Forms as a Cloud Service. Questi dettagli sono utili per eseguire il debug dell’ambiente. Per maggiori dettagli, vedi [Debug AEM as a Cloud Service con Developer Console](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html).

<!--

+++CDN (Content Delivery Network):

Every AEM Forms as a Cloud Service program has access to Fastly CDN service. It is included in the licence of Forms as a Cloud Services.

+++

+++Adaptive Forms
Adaptive Forms enable customers to author web-friendly reflowable web forms and fragments that are used by the customers for their data capture needs. This feature enables customers to manage their complex data capture needs easily, by leveraging multiple integrations with Adobe Sign, Document Services, Form Data Model, Automated Forms Conversion service, and more.

+++

+++Automated Forms Conversion Service (AFCS)
Automated Forms Conversion service helps accelerate digitization and modernization of data capture experience through automated conversion of PDF forms to adaptive forms. The service, powered by Adobe Sensei, automatically converts your PDF forms to device-friendly, responsive, and HTML5-based adaptive forms. While leveraging the existing investments in PDF Forms and XFA, the service also applies appropriate validations, styling, and layout to adaptive form fields during conversion.

+++

+++Form Data Model
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

Cloud Manager is an essential component to [AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en). Each new tenant of the [!DNL AEM Forms] as a Cloud Service is first provisioned for Cloud Manager access. Cloud Manager is the single-entry point for the operations and developer persona of our customers. It is the place from where the AEM programs and environments can be managed. Cloud Manager has evolved as a self-service portal where the main components of the AEM as a Cloud Service can be created and configured:

* Creating and managing programs
* Creating and managing the AEM environments within the programs
* Creating and managing the pipelines for deploying the customer code and configuration to a particular environment
* Getting notified of important lifecycle events for these components (e.g. product updates)
For more information about Cloud Manager, see [Understand Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/cloud-manager/understand-cloud-manager-for-aem.html) and [Introduction to Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html).

## Users and Authentication {#users-and-authentication}

AEM as a Cloud Service includes Admin Console support for AEM instances and Adobe Identity Management System (IMS) based authentication. The Admin Console allows administrators to centrally manage all Experience Cloud users. Users and Groups can be assigned to product profiles associated with AEM as a Cloud Service instances, allowing them to log in to that instance. For more information about users, authentication, and, and accessing an instance of AEM as a Cloud Service, see [IMS Support for [!DNL Adobe Experience Manager] as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#introduction).

Various personas are involved in a typical [!DNL AEM Forms] project. After you log in to your [!DNL AEM Forms] as a Cloud Service instance, you can [add users in admin console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html) for personas applicable to your organization or project and [assign users to built-in groups](forms-groups-privileges-tasks.md) to provide them required privileges.

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
Also, one of the most common requirements for developers is quick access to the log files of the various environments. With [!DNL AEM Cloud Service], the log files of the different nodes in the Author, Publish are made available via the Cloud Manager, either in the form of files that can be downloaded or via APIs for tailing the logs. Due to the clear separation of code and content, developers can leverage a particular process for updating content as part of a deployment. The typical use cases for mutable content are:
* Standard “default” content that is part of the customer project (e.g. folders, templates, workflows...)
* Search index definitions
* ACLs and permissions
* Service users and user groups
Set up your development environment, [Configure your CI/CD Pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html), and learn to [deploy your code](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html) on the environment. -->

### Authoring di moduli adattivi {#local-development}

Quando configuri e configuri un [!DNL AEM Forms] Ambiente as a Cloud Service, puoi configurare ambienti di sviluppo, staging e produzione. Inoltre, crea e configura un ambiente di sviluppo locale per iterazioni e sviluppo rapidi. Puoi scaricare e configurare AEM SDK e [!DNL AEM Forms] archivio di funzionalità aggiuntive per configurare un [!DNL Forms] Ambiente di sviluppo as a Cloud Service.  Per istruzioni dettagliate, vedi [Configurare un ambiente di sviluppo locale](setup-local-development-environment.md).

## Debugging {#debugging}

AEM as a Cloud Service viene eseguito su un&#39;infrastruttura cloud self-service, scalabile. Richiede agli sviluppatori AEM di comprendere ed eseguire il debug di vari facet di AEM as a Cloud Service, dalla generazione e distribuzione fino a ottenere i dettagli dell&#39;esecuzione delle applicazioni AEM. Per informazioni dettagliate, consulta [Debug AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html).
