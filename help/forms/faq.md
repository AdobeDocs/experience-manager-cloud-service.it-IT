---
title: Domande frequenti su AEM Forms as a Cloud Service
description: Domande frequenti su Forms as a Cloud Service
contentOwner: khsingh
role: User
feature: Adaptive Forms, FAQ
index: false
exl-id: 0b14b680-7da5-4e0b-bd6a-c379d148f9d7
source-git-commit: 81951a9507ec3420cbadb258209bdc8e2b5e2942
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 89%

---

# Domande frequenti {#frequently-asked-questions}

* **È utilizzare l’editor di codice per creare regole?**
Per creare le regole, è possibile utilizzare l’editor visivo. L’editor di codice non è disponibile su [!DNL Forms] as a Cloud Service. Se il modulo adattivo utilizza script di regole sviluppati utilizzando l’editor di codice, utilizza l’[utilità di migrazione](migrate-to-forms-as-a-cloud-service.md) per convertire gli script di codice in funzioni personalizzate. È possibile utilizzare le funzioni personalizzate con l’editor visivo per continuare a ottenere i risultati ottenuti con l’editor di codice.

* **È possibile creare un modulo adattivo basato su XFA sulle istanze di Cloud Service?**
Sì, è possibile creare un modulo adattivo basato su XFA sull’istanza di Cloud Service. Tuttavia, il supporto per i moduli adattivi basati su XFA non è disponibile per l’SDK di AEM Forms as a Cloud Service (Ambiente di sviluppo locale). Se desideri utilizzare i moduli adattivi basati su XFA con l’SDK di AEM Forms as a Cloud Service, contatta il supporto Adobe con i dettagli del caso d’uso e i requisiti specifici.

<!-- * **Can I use an XDP as a Document of Record (DoR) template? Is Forms Designer included in AEM Forms as a Cloud Service license?** 

  Yes, you can use an XDP as a Document of Record template on Cloud Service instances. However, support to use XDP as a Document of Record template is not available for AEM Forms as a Cloud Service SDK (Local development environment). -->

* **È possibile migrare il contenuto da ambienti on-premise o da [!DNL Adobe-Managed Services] all’ambiente di [!DNL Forms] as a Cloud Service?**
Sì, è possibile migrare il codice personalizzato, il contenuto e le risorse da ambienti on-premise o da [!DNL Adobe-Managed Services] all’ambiente di [!DNL Forms] as a Cloud Service. Per istruzioni dettagliate, consulta [Migrare a Forms as a Cloud Service](migrate-to-forms-as-a-cloud-service.md).

<!-- You can use package manager or Experience Manager UI to [export and import Forms and related assets](import-export-forms-templates.md), use the migration utility to make your existing assets compatible with [!DNL Forms] as a Cloud Service, use the [Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#best-practices-analyzer) tool to find the features and APIs that require changes and updated before migration, and use the [Content Transfer Tools](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/home.html) to move your custom code without refactoring it. -->

* **Dove è possibile trovare la documentazione di riferimento API [!DNL Java™] per AEM [!DNL Forms] as a Cloud Service?**
È possibile scaricare la documentazione di riferimento API Java™ da [!DNL Maven Central Repository]. Per scaricarla:
   1. Passa a [[!DNL Maven Central Repository]](https://mvnrepository.com/artifact/com.adobe.aem/aem-forms-sdk-api).
   1. Individua e apri la pagina contenente la versione più recente di [!DNL Experience Manager Forms] SDK.
   1. Fai clic sull’opzione Visualizza tutto per visualizzare tutti i file.
   1. Scarica ed estrai il file `aem-forms-sdk-api-<version>-javadocs`.jar.
   1. Apri il file index.html per visualizzare la documentazione di riferimento API.

* **Dove è possibile trovare il riferimento API [!DNL JavaScript™] per i moduli adattivi?**
È possibile scaricare la documentazione di riferimento API [!DNL JavaScript™] da [!DNL  Maven Central Repository]. Per scaricarla:
   1. Apri [[!DNL Maven Central Repository]](https://mvnrepository.com/artifact/com.adobe.aem/aem-forms-sdk-api).
   1. Individua e apri la pagina contenente la versione più recente di [!DNL Experience Manager Forms] SDK.
   1. Fai clic sull’opzione Visualizza tutto per visualizzare tutti i file.
   1. Scarica ed estrai il file `aem-forms-sdk-api-<version>-jsdoc.jar`.
   1. Apri il file index.html per visualizzare la documentazione di riferimento API.

* **È possibile continuare a utilizzare i temi e i modelli esistenti?**
Sì, è possibile continuare a utilizzare i temi creati con AEM 6.4 Forms e AEM 6.5 Forms dopo aver utilizzato l’[utilità di migrazione](migrate-to-forms-as-a-cloud-service.md) per spostarli in [!DNL AEM Forms] as a Cloud Service.

  È possibile anche creare un progetto basato sull’[Archetipo](setup-local-development-environment.md#forms-cloud-service-local-development-environment) di [!DNL AEM Forms] as a Cloud Service e utilizzare i temi e i modelli di esempio inclusi.

* **È possibile produrre dati conformi allo schema?**
Sì, è possibile creare modelli adattivi per produrre dati conformi allo schema.

<!-- * **Can I pass custom parameters to the prefill service?**
Custom parameters are planned for an upcoming release. -->

* **È possibile memorizzare nella cache il contenuto protetto?**
Per impostazione predefinita, la funzione di memorizzazione in cache del contenuto protetto è disabilitata. Per attivare la funzione, è possibile eseguire le istruzioni fornite in [Memorizzazione in cache del contenuto protetto](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=it).

* **Il modulo adattivo localizzato non è il rendering di una versione localizzata? Quale potrebbe essere la causa e come risolvere il problema?**

  La convenzione URL dei moduli adattivi localizzati consente ora di specificare le impostazioni internazionali della lingua nell’URL. La nuova convenzione URL consente di memorizzare i moduli localizzati nella cache di Dispatcher o della rete CDN. Nell’ambiente di Cloud Service, utilizza il formato URL `http://host:port/content/forms/af/<afName>.<locale>.html` per richiedere una versione localizzata di un modulo adattivo anziché `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. Adobe consiglia di utilizzare la memorizzare nella cache di Dispatcher o della rete CDN. Questo consente di migliorare la velocità di rendering dei moduli precompilati.

* **Se un modulo adattivo è stato aggiornato, la versione aggiornata non è disponibile per l’uso da parte da parte della clientela?**
Per impostazione predefinita, la rete CDN aggiorna la cache ogni 5 minuti. Attendi 5 minuti e verifica la presenza della versione aggiornata.

* **È possibile utilizzare il passaggio di Firma in un modulo adattivo per creare un’esperienza di firma nel browser?**
No, il passaggio di Firma non è disponibile per [!DNL Forms] as a Cloud Service. Rimuovi il passaggio Firma nei moduli adattivi. Invece del passaggio di Firma, consenti agli utenti di firmare un modulo adattivo dopo l’invio. Consente di continuare a fornire un’esperienza di firma nel browser.

* **È possibile utilizzare il passaggio di verifica in un modulo adattivo?**
No, il passaggio di verifica non è disponibile per [!DNL Forms] as a Cloud Service. Rimuovi il passaggio di verifica dai moduli adattivi esistenti prima di spostarli in un ambiente Cloud Service.

* **È possibile aggiungere grafici a un modulo adattivo?**
Sì, puoi aggiungere grafici ai moduli adattivi. I moduli adattivi forniscono un componente grafico. È possibile utilizzarlo per aggiungere grafici a un modulo adattivo.

* **È possibile collegare un modello di dati modulo (FDM) a un modello di database relazionale?**
È possibile collegare un modello dati modulo (FDM) a [!DNL RESTful web services], [!DNL SOAP-based web services], [!DNL OData services], e profilo utente di Experience Manager come origini dati. Il supporto per la connessione di un modello di dati modulo (FDM) con un database relazionale non è disponibile.

* **È possibile utilizzare certificati personalizzati con il modello dati modulo (FDM) per l&#39;autenticazione?**
Il modello dati modulo (FDM) non fornisce un metodo per utilizzare certificati personalizzati per l’autenticazione. Pertanto, i certificati personalizzati come x509 e SSL bidirezionale non sono supportati.

* **È possibile utilizzare l’azione di invio Forms Portal per i moduli adattivi?**

  Puoi modificare il Forms adattivo esistente per utilizzare [Invia all’endpoint REST](configuring-submit-actions.md#submit-to-rest-endpoint), [Invia e-mail](configuring-submit-actions.md#send-email), [Invia utilizzando il modello dati modulo (FDM)](configuring-submit-actions.md#submit-using-form-data-model), e [Richiama un flusso di lavoro AEM](configuring-submit-actions.md#invoke-an-aem-workflow) Inviare azioni. Forms Portal e l’azione di invio da Forms Portal non sono ancora disponibili. Per informazioni sulla disponibilità delle funzioni, consulta le note sulla versione mensili.

* **È possibile utilizzare l’app [!DNL AEM Forms] con [!DNL AEM Forms] as a Cloud Service?**

  Forms adattivo offre un design responsive. Questi moduli modificano l’aspetto, la progettazione e l’interattività in base al dispositivo sottostante. Puoi continuare a utilizzare i moduli adattivi sui dispositivi mobili e controllare le note sulla versione mensili per verificare la disponibilità delle funzioni.

* **Quali funzioni non fanno parte della versione iniziale con disponibilità generale?**
Forms Portal, l’app [!DNL AEM Forms], l’integrazione con Adobe Analytics e l’integrazione con Adobe Target non fanno parte della versione iniziale con disponibilità generale. Per informazioni sulle nuove funzioni, consulta le note sulla versione mensili.

* **Ho progettato uno [Schema JSON per creare un modulo adattivo](adaptive-form-json-schema-form-model.md). Lo schema JSON definisce gli eventi per alcuni componenti di moduli adattivi. AEM Forms as a Cloud Service supporta tali eventi?**
Crea il modulo adattivo basato sullo schema JSON nell’ambiente Forms Experience Manager 6.5 e utilizza l’[utilità di migrazione](migrate-to-forms-as-a-cloud-service.md) per migrare tali moduli adattivi ad AEM Forms as a Cloud Service. L’utilità converte tali eventi in librerie client così sarà possibile continuare a utilizzare i moduli adattivi con gli eventi in un ambiente di Cloud Service.

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
