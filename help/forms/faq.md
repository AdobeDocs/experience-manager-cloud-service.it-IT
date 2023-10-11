---
title: Domande frequenti per AEM Forms as a Cloud Service
description: Domande frequenti su Forms as a Cloud Service
contentOwner: khsingh
exl-id: 0b14b680-7da5-4e0b-bd6a-c379d148f9d7
index: false
source-git-commit: 7a65aa82792500616f971df52b8ddb6d893ab89d
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 3%

---

# Domande frequenti {#frequently-asked-questions}

* **Posso utilizzare l’editor di codice per creare regole?**
Puoi utilizzare l’Editor visivo per creare le regole. L’editor di codice non è disponibile su [!DNL Forms] as a Cloud Service. Se il modulo adattivo utilizza script di regole sviluppati utilizzando l’editor di codice, utilizza [Utilità di migrazione](migrate-to-forms-as-a-cloud-service.md) per convertire gli script di codice in funzioni personalizzate. È possibile utilizzare funzioni personalizzate con Visual Editor per continuare a ottenere i risultati ottenuti con l&#39;editor di codice.

* **È possibile creare un modulo adattivo basato su XFA sulle istanze di Cloud Service?**
Sì, puoi creare un modulo adattivo basato su XFA nell’istanza di Cloud Service. Tuttavia, il supporto per Adaptive Forms basato su XFA non è disponibile per AEM Forms as a Cloud Service SDK (Local development environment, ambiente di sviluppo locale). Se desideri utilizzare Adaptive Forms basato su XFA con l’SDK di AEM Forms as a Cloud Service, contatta il supporto Adobe con i dettagli del caso d’uso e i requisiti specifici.

<!-- * **Can I use an XDP as a Document of Record (DoR) template? Is Forms Designer included in AEM Forms as a Cloud Service license?** 

  Yes, you can use an XDP as a Document of Record template on Cloud Service instances. However, support to use XDP as a Document of Record template is not available for AEM Forms as a Cloud Service SDK (Local development environment). -->

* **È possibile migrare il contenuto da un sito locale o [!DNL Adobe-Managed Services] ambienti da [!DNL Forms] ambiente as a Cloud Service?**
Sì, puoi migrare il codice personalizzato, il contenuto e le risorse da On-Premise o [!DNL Adobe-Managed Services] ambienti da [!DNL Forms] ambiente as a Cloud Service. Per istruzioni dettagliate, consulta [Migrare a Forms as a Cloud Service](migrate-to-forms-as-a-cloud-service.md).

<!-- You can use package manager or Experience Manager UI to [export and import Forms and related assets](import-export-forms-templates.md), use the migration utility to make your existing assets compatible with [!DNL Forms] as a Cloud Service, use the [Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#best-practices-analyzer) tool to find the features and APIs that require changes and updated before migration, and use the [Content Transfer Tools](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/home.html) to move your custom code without refactoring it. -->

* **Dove posso trovare l&#39;AEM? [!DNL Forms] as a Cloud Service [!DNL Java™] Documentazione di riferimento API?**
Puoi scaricare la documentazione di riferimento dell’API Java™ da [!DNL Maven Central Repository]. Per scaricare:
   1. Passa a [[!DNL Maven Central Repository]](https://mvnrepository.com/artifact/com.adobe.aem/aem-forms-sdk-api).
   1. Individua e apri la pagina contenente la versione più recente di [!DNL Experience Manager Forms] SDK
   1. Fare clic sull&#39;opzione Visualizza tutto per visualizzare tutti i file.
   1. Scarica ed estrai il file `aem-forms-sdk-api-<version>-javadocs`.jar.
   1. Apri il file index.html per visualizzare la documentazione di riferimento dell’API.

* **Dove posso trovare [!DNL JavaScript™] Riferimento API per Forms adattivo?**
Puoi scaricare [!DNL JavaScript™] Documentazione di riferimento API da[!DNL  Maven Central Repository]. Per scaricare:
   1. Apri [[!DNL Maven Central Repository]](https://mvnrepository.com/artifact/com.adobe.aem/aem-forms-sdk-api).
   1. Individua e apri la pagina contenente la versione più recente di [!DNL Experience Manager Forms] SDK
   1. Fare clic sull&#39;opzione Visualizza tutto per visualizzare tutti i file.
   1. Scarica ed estrai il file `aem-forms-sdk-api-<version>-jsdoc.jar`.
   1. Apri il file index.html per visualizzare la documentazione di riferimento dell’API.

* **Posso continuare a utilizzare i temi e i modelli esistenti?**
Sì, puoi continuare a utilizzare i temi creati con AEM 6.4 Forms e AEM 6.5 Forms dopo aver utilizzato [Utilità di migrazione](migrate-to-forms-as-a-cloud-service.md) per spostarli in [!DNL AEM Forms] as a Cloud Service.

  Puoi anche creare un progetto basato su [!DNL AEM Forms] as a Cloud Service [Archetipo](setup-local-development-environment.md#forms-cloud-service-local-development-environment) e utilizza i temi e i modelli di esempio inclusi.

* **Posso produrre dati conformi allo schema?**
Sì, puoi creare un Forms adattivo per produrre dati conformi allo schema.

<!-- * **Can I pass custom parameters to the prefill service?**
Custom parameters are planned for an upcoming release. -->

* **Posso memorizzare in cache contenuto protetto?**
Per impostazione predefinita, la memorizzazione nella cache delle funzioni di contenuto protetto è disabilitata. Per attivare la funzione, è possibile eseguire le istruzioni fornite in [Caching di contenuto protetto](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=it).

* **Dispongo di un modulo adattivo localizzato; non viene eseguito il rendering della versione localizzata? Quale potrebbe essere la causa e come risolverla?**

  La convenzione URL di Forms adattivo localizzato ora supporta la specifica di una lingua nell’URL. La nuova convenzione URL consente di memorizzare nella cache i moduli localizzati su una rete CDN o Dispatcher. In ambiente di Cloud Service, utilizza il formato URL `http://host:port/content/forms/af/<afName>.<locale>.html` per richiedere una versione localizzata di un modulo adattivo anziché `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. L’Adobe consiglia di utilizzare il caching di Dispatcher o CDN. Consente di migliorare la velocità di rendering dei moduli precompilati.

* **Ho aggiornato un modulo adattivo; la versione aggiornata non è disponibile per l’uso da parte dei clienti?**
Per impostazione predefinita, la rete CDN aggiorna la cache dopo ogni 5 minuti, attendi 5 minuti e verifica la versione aggiornata.

* **Posso utilizzare il passaggio Firma in un Modulo adattivo per creare un’esperienza di firma nel browser?**
No, il passaggio Firma non è disponibile per [!DNL Forms] as a Cloud Service. Rimuovi il passaggio Firma nel Forms adattivo. Invece del passaggio Firma, consenti agli utenti di firmare un modulo adattivo dopo l’invio. Ti aiuta a continuare a fornire un’esperienza di firma nel browser.

* **Posso utilizzare il passaggio di verifica in un modulo adattivo?**
No, il passaggio di verifica non è disponibile per [!DNL Forms] as a Cloud Service. Rimuovi il passaggio di verifica dal Forms adattivo esistente prima di spostare tali moduli in un ambiente di Cloud Service.

* **Posso aggiungere grafici a un modulo adattivo?**
Sì, puoi aggiungere grafici ad Adaptive Forms. Forms adattivo fornisce un componente grafico. Puoi utilizzarlo per aggiungere grafici a un modulo adattivo.

* **È possibile collegare un modello di dati modulo a un modello di database relazionale?**
È possibile collegare un modello dati modulo a [!DNL RESTful web services], [!DNL SOAP-based web services], [!DNL OData services], e profilo utente di Experience Manager come origini dati. Il supporto per la connessione di un modello dati modulo a un database relazionale non è disponibile.

* **È possibile utilizzare certificati personalizzati con il modello dati modulo per l&#39;autenticazione?**
Il modello dati modulo non fornisce un metodo per utilizzare certificati personalizzati per l&#39;autenticazione. Pertanto, i certificati personalizzati come x509 e SSL a 2 vie non sono supportati.

* **Posso utilizzare l’azione di invio Forms Portal per Forms adattivo?**

  Puoi modificare il Forms adattivo esistente per utilizzare [Invia all’endpoint REST](configuring-submit-actions.md#submit-to-rest-endpoint), [Invia e-mail](configuring-submit-actions.md#send-email), [Invia utilizzando il modello dati modulo](configuring-submit-actions.md#submit-using-form-data-model), e [Richiama un flusso di lavoro AEM](configuring-submit-actions.md#invoke-an-aem-workflow) Inviare azioni. L’azione di invio Forms Portal e Forms Portal non è ancora disponibile. Per informazioni sulla disponibilità delle funzioni, consulta le note sulla versione mensili.

* **Posso utilizzare [!DNL AEM Forms] app con [!DNL AEM Forms] as a Cloud Service?**

  Forms adattivo offre un design responsive. Questi moduli modificano l’aspetto, la progettazione e l’interattività in base al dispositivo sottostante. Puoi continuare a utilizzare Adaptive Forms sui dispositivi mobili e controllare le note sulla versione mensili per verificare la disponibilità delle funzioni.

* **Quali funzioni non fanno parte della versione GA iniziale?**
Forms Portal [!DNL AEM Forms] L’app, l’integrazione con Adobe Analytics e l’integrazione con Adobe Target non fanno parte della versione GA iniziale. Per informazioni sulle nuove funzioni, consulta le note sulla versione mensili.

* **Ho progettato un [Schema JSON per creare un modulo adattivo](adaptive-form-json-schema-form-model.md). Lo schema JSON definisce gli eventi per alcuni componenti di moduli adattivi. AEM Forms as a Cloud Service supporta gli eventi?**
Creare il modulo adattivo basato sullo schema JSON nell’ambiente Forms Experience Manager 6.5 e utilizzare [Utility di migrazione](migrate-to-forms-as-a-cloud-service.md) per migrare tali Forms adattivi ad AEM Forms as a Cloud Service. L’utility converte tali eventi in librerie client e puoi continuare a utilizzare Forms adattivo con gli eventi in un ambiente di Cloud Service.

<!-- 

* **Is there any AEM Forms as a Cloud Service connector for Microsoft Power Automate?**

  Yes, Adobe provides an Adobe Experience Manager connector to access [Adobe Experience Manager Forms - Communication capabilities](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html) through Microsoft Power Automate. You can create a PDF document that is based on a form design and XML form data or create PostScript (PS), Printer Command Language (PCL), Zebra Printing Language (ZPL) and other Printer Definition Language documents. 

  You can get started with Adobe Experience Manager easily with just a few steps:

  1. Generate the Service credentials: Use Adobe Experience Manager Developer Console to [generate](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?#generate-service-credentials) the service credentials.  
  
  1. Setup your connection: Add your service credentials to the Adobe Experience Manager Connector. You can get crdential from service credential JSON and copy these credential details to your one-time connection setup:

    * AEM Server
    * Organization ID 
    * Client ID
    * Client Secret
    * Technical Account ID
    * Meta Scopes
    * Private Key - base64 encoded keys are accepted
    * Adobe IMS Host URL

    <br> 
    
    ![Use your Service Credential JSON for credential details](assets/forms-aem-pa-connector-connection.png)

    A sample Service Credential JSON file fields mapped to Adobe Experience Manager connector for Microsoft Power Automate.

    -->


