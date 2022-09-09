---
title: Funzioni e funzionalità principali di Adobe Experience Manager (AEM) Forms as a Cloud Service
description: "[!DNL AEM Forms] as a Cloud Service è una piattaforma per creare, gestire e pubblicare moduli e processi aziendali di classe enterprise."
exl-id: 3a90b0aa-369a-4350-9904-79ef656b0f9a
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 5%

---

<!-- # Introduction to [!DNL AEM Forms] as a Cloud Service {#overview}

Adobe Experience Manager Forms as a Cloud Service offers a cloud-native, Platform as a Service (PaaS) solution for businesses to create, manage, publish, and update complex digital forms while integrating submitted data with back-end processes, business rules, and saving data in an external data store. The service is always current, always available, and always learning.

You can use the service to create and rollout  interactive and engaging digital forms. For example, an organization is looking to digitize their customer enrollment journey. They have multiple data sources with existing customer data, they are looking to pre-populate forms, add e-sign their forms, and archive filled forms as PDF files. Besides, the organization has multiple print forms (PDF forms), they are also looking to convert all of their print forms to digital forms.

The organization can use [!DNL AEM Forms] as a Cloud Service to create digital forms, connect forms to existing data sources, integrate forms with [!DNL Adobe Sign] to add e-signatures to forms, and generate Document of Record (DoR) to archive filled forms as PDF files. The organization can also use the service to convert their existing PDF forms to digital forms. 

An organization can sign up for [!DNL AEM Forms] as a Cloud Service and start using all these features without waiting to buy and set up a local infrastructure. The service also frees the organizations from the cycle of upgrades as it is always up to date and always offers the latest feature.  -->

# Funzioni e funzionalità principali {#key-features}

[!DNL AEM Forms] as a Cloud Service offre diverse funzionalità native per il cloud, come un’architettura nativa per il cloud, il ridimensionamento automatico, tempi di inattività zero per gli aggiornamenti, una rete CDN (Content Delivery Network), un ambiente di sviluppo nativo per il cloud e la possibilità di self-service per gli ambienti tramite Cloud Manager. Puoi utilizzare il servizio per:

* [Creare un Forms adattivo](creating-adaptive-form.md#strong-create-an-adaptive-form-strong) che esegue automaticamente il rendering per il dispositivo e il browser di un utente.

   ![Moduli adattivi](assets/rule-editor-example.gif)

* [Creare PDF forms perfetti in pixel](use-forms-designer.md#create-an-adaptive-form) sembra quasi carta.

* Utilizzo [servizio automated forms conversion](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/introduction.html?lang=it) per convertire un modulo PDF in un modulo adattivo. Consente di accelerare la digitalizzazione e la modernizzazione delle esperienze di acquisizione dei dati della tua organizzazione.

   ![servizio automated forms conversion](assets/pdf-to-adaptive-form-gitx50.gif)

* [Creazione di processi aziendali](aem-forms-workflow-step-reference.md#create-form-centric-workflows). Ad esempio, è possibile creare e attivare un flusso di lavoro di approvazione e rifiuto all’invio di un modulo adattivo.

Oltre a quanto sopra [!DNL AEM Forms] In as a Cloud Service sono disponibili le seguenti funzionalità:

* Interfaccia grafica di facile utilizzo per consentire agli utenti aziendali di importare, gestire, visualizzare in anteprima e pubblicare facilmente i moduli
* Una directory di moduli reattivi con potenti funzioni di ricerca utilizzando parole chiave, tag e metadati
* Rilevamento dinamico del dispositivo e della posizione di un utente per eseguire il rendering del modulo in modo appropriato tra canali web e mobili
* [Integrazione con Adobe Sign](adobe-sign-integration-adaptive-forms.md) Servizi o Scribble di firmare elettronicamente documenti contenenti informazioni riservate
* Capacità di [collegare il servizio a vari tipi di origini dati](data-integration.md#create-an-adaptive-form) per inviare e recuperare dati. Il servizio supporta l’invio e il recupero di dati da servizi web RESTful, servizi web basati su SOAP e servizi abilitati per OData.
* Integrazione con AEM Sites. Consente di incorporare un modulo adattivo in una pagina AEM Sites. È inoltre possibile integrare un modulo adattivo in qualsiasi pagina web.
* Possibilità di creare un documento di record (DoR) per registrare le informazioni fornite e inviate in un modulo adattivo in modo da potervi fare riferimento in un secondo momento. Un DoR è una versione PDF di un modulo. Include sia un modello che i dati. Il servizio fornisce un modello DoR e strumenti predefiniti per sviluppare un modello personalizzato.
* Possibilità di creare Forms adattivo per produrre dati conformi allo schema. Consente di inviare i dati acquisiti a processi e origini dati esistenti senza alcuna o minima modifica.
* Possibilità di creare un servizio di precompilazione per compilare un modulo con dati cliente esistenti in base a un criterio. Aiuta a velocizzare il processo di compilazione del modulo e a ridurre il tasso di abbandono.


<!-- 

## Enterprise-class forms {#enterprise-class-forms}

You can create enterprise class forms (Adaptive Forms) and deliver beautiful, interactive, responsive, and personalized experiences to your customers. These forms change behavior and appearance based on the underlying device. You can also use themes and templates with Adaptive Forms to mandate a uniform structure and appearance for all the forms of an organization or a department.

![Creating custom patterns for fields in CrxDe](assets/adaptive-form.png)

## Automatic conversion of PDF forms to Adaptive Forms {#automatic-conversion-of-pdf-forms-to-adaptive-forms}

You can use Automated Forms Conversion service to convert a PDF Form to an Adaptive Form. It helps you accelerate digitization and modernization of data capture experiences of your organization.

![Creating custom patterns for fields in CrxDe](assets/pdf-to-adaptive-form-gitx50.gif)

## Data Integration {#data-integration}

You can connect the service to various types of data sources to send and retrieve data. The service supports sending and retrieving data from RESTful web services, SOAP-based web services, and OData enabled services.

![Build dynamism and interactivity to Adaptive Forms](assets/rule-editor-example.gif)

## Integration with [!DNL Adobe Sign] {#integration-with-adobe-sign}

 You can integrate the service with [!DNL Adobe Sign] and add [!DNL Adobe Sign] fields to an Adaptive Form. It allows your users to e-sign an Adaptive Form and use [!DNL Adobe Sign] with AEM Workflows. You can use AEM Workflows to develop a business logic and send forms and documents to recipients for signatures based on the business logic.

![Creating custom patterns for fields in CrxDe](assets/adobe-sign.png)


## Integration with [!DNL AEM Sites] {#integration-with-aem-sites}

You can embed an adaptive form in an AEM Sites or an external webpage. The service provides a component out of the box to integrate an adaptive forms to an AEM Sites page.

![integrate an adaptive forms to an AEM Sites page](assets/integrate.png)

## Business Processes Automation {#bpa}

You can use AEM Workflows to create business processes and automate operations. For example, You can create and trigger an approval and rejection workflow on submission of an Adaptive Form. 

![Create and trigger an approval and rejection workflow](assets/workflow.png)

## Document of Record {#dor}

You can create a Document of Record (DoR) to keep a record of the information that you provide and submit in an Adaptive Form so that you can refer to it later. A DoR is a PDF version of a form. It includes both a template and data. The service provides a default DoR template and tools to develop a custom template.

![Build dynamism and interactivity to Adaptive Forms](assets/designer.png)

## Rule editor {#rule-editor}

Rule editor empowers you to build dynamism and interactivity to Adaptive Forms. These rules define actions to trigger on form objects based on preset conditions, user inputs, and user actions on the form. It helps  streamline the form filling experience while ensuring accuracy and speed.
  
![Creating custom patterns for fields in CrxDe](assets/form-data-model.png)


## WYSIWYG editors {#wysiwyg-editor} 

The service provides several WYSIWYG editors: Adaptive Forms editor, Theme editor, and Template editor. These help you create and edit forms and related assets in WYSIWYG manner. The editors also provide out-of-the-box options to simulate views for popular mobile devices, tablets, and desktop screen configurations.

![Creating custom patterns for fields in CrxDe](assets/emulators.png)

## Schema-compliant data {#schema-complaint-data}

You can create Adaptive Forms to produce schema-compliant data. It helps you submit captured data to existing processes and data sources without any or minimal modifications.

![Build dynamism and interactivity to Adaptive Forms](assets/display-validation-error.gif)

## Prefill a form

You can create a prefill service to fill a form with existing customer data based on a criteria. It helps fasten the form filling process and reduce the abandon rate.

## Submit Actions

A Submit Action allows you to persist and process captured data. The service provides several Submit Actions out-of-the-box. You can use these Submit Actions to send submitted data to a REST endpoint, database, or an AEM Workflow. You can also email submitted data along with attachments and Document of Record(DoR). You can also develop a custom Submit Action to perform an action specific to your business.

* **Emulators:** You can view an Adaptive Form in an in-built emulator. It helps you simulate how an Adaptive Form appears on different devices to an end user. It provides out-of-the-box options to simulate views for popular mobile devices, tablets, and desktop screen configurations. 

In addition to standard [!DNL AEM Forms] features, [!DNL AEM Forms] as a Cloud Service provides several cloud-native capabilities such as a cloud-native architecture, auto-scaling, zero downtime for upgrades, a CDN (Content Delivery Network), cloud-native development environment, and ability to self-Service the environments via Cloud Manager. -->
