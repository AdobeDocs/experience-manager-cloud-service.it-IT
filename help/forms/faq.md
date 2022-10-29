---
title: Domande frequenti as a Cloud Service di Forms
description: Domande frequenti as a Cloud Service di Forms
contentOwner: khsingh
exl-id: 0b14b680-7da5-4e0b-bd6a-c379d148f9d7
index: false
source-git-commit: 6355a6241c5b53585b80b2c2bc00556297766b49
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 3%

---

# Domande frequenti {#frequently-asked-questions}

* **Posso utilizzare l&#39;Editor di codice per creare regole?**
È possibile utilizzare Visual Editor per creare le regole. L’editor di codice non è disponibile in [!DNL Forms] as a Cloud Service. Se il modulo adattivo utilizza script di regola sviluppati utilizzando l’editor di codice, utilizza il [Utilità di migrazione](migrate-to-forms-as-a-cloud-service.md) per convertire gli script di codice in funzioni personalizzate. È possibile utilizzare funzioni personalizzate con Visual Editor per continuare a ottenere i risultati ottenuti con Code Editor.

* **Posso creare un modulo adattivo basato su XFA sulle istanze di Cloud Service?**
Sì, è possibile creare un modulo adattivo basato su XFA su un&#39;istanza di Cloud Service. Tuttavia, il supporto per Forms adattivo basato su XFA non è disponibile per AEM Forms as a Cloud Service SDK (ambiente di sviluppo locale). Se desideri utilizzare Forms adattivo basato su XFA con l&#39;SDK as a Cloud Service di AEM Forms, contatta il supporto Adobe con i dettagli del caso d&#39;uso e i requisiti specifici.

<!-- * **Can I use an XDP as a Document of Record (DoR) template? Is Forms Designer included in AEM Forms as a Cloud Service license?** 

  Yes, you can use an XDP as a Document of Record template on Cloud Service instances. However, support to use XDP as a Document of Record template is not available for AEM Forms as a Cloud Service SDK (Local development environment). -->

* **Posso eseguire la migrazione del contenuto da un servizio on-premise o [!DNL Adobe-Managed Services] ambienti [!DNL Forms] Ambiente as a Cloud Service?**
Sì, puoi eseguire la migrazione del codice personalizzato, del contenuto e delle risorse da On-Premise o [!DNL Adobe-Managed Services] ambienti [!DNL Forms] Ambiente as a Cloud Service. Per istruzioni dettagliate, vedi [Migrazione a Forms as a Cloud Service](migrate-to-forms-as-a-cloud-service.md).

<!-- You can use package manager or Experience Manager UI to [export and import Forms and related assets](import-export-forms-templates.md), use the migration utility to make your existing assets compatible with [!DNL Forms] as a Cloud Service, use the [Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#best-practices-analyzer) tool to find the features and APIs that require changes and updated before migration, and use the [Content Transfer Tools](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/home.html) to move your custom code without refactoring it. -->

* **Dove posso AEM [!DNL Forms] as a Cloud Service [!DNL Java™] Documentazione di riferimento API?**
Puoi scaricare la documentazione di riferimento API Java™ da [!DNL Maven Central Repository]. Per scaricare:
   1. Passa a [[!DNL Maven Central Repository]](https://mvnrepository.com/artifact/com.adobe.aem/aem-forms-sdk-api).
   1. Individua e apri la pagina contenente la versione più recente di [!DNL Experience Manager Forms] SDK.
   1. Fare clic sull&#39;opzione Visualizza tutto per visualizzare tutti i file.
   1. Scarica ed estrai `aem-forms-sdk-api-<version>-javadocs`.jar.
   1. Apri il file index.html per visualizzare la documentazione di riferimento API.

* **Dove posso trovare [!DNL JavaScript™] Riferimento API per Adaptive Forms?**
È possibile scaricare [!DNL JavaScript™] Documentazione di riferimento API da[!DNL  Maven Central Repository]. Per scaricare:
   1. Apri [[!DNL Maven Central Repository]](https://mvnrepository.com/artifact/com.adobe.aem/aem-forms-sdk-api).
   1. Individua e apri la pagina contenente la versione più recente di [!DNL Experience Manager Forms] SDK.
   1. Fare clic sull&#39;opzione Visualizza tutto per visualizzare tutti i file.
   1. Scarica ed estrai `aem-forms-sdk-api-<version>-jsdoc.jar`.
   1. Apri il file index.html per visualizzare la documentazione di riferimento API.

* **Posso continuare a utilizzare temi e modelli esistenti?**
Sì, puoi continuare a utilizzare i temi creati con AEM 6.4 Forms e Forms 6.5 dopo aver utilizzato il [Utilità di migrazione](migrate-to-forms-as-a-cloud-service.md) per spostarle in [!DNL AEM Forms] as a Cloud Service.

   Puoi anche creare un progetto basato su [!DNL AEM Forms] as a Cloud Service [Archetipo](setup-local-development-environment.md#forms-cloud-service-local-development-environment) e utilizza temi e modelli di esempio inclusi.

* **Posso produrre dati conformi allo schema?**
Sì, è possibile creare Adaptive Forms per produrre dati conformi allo schema.

<!-- * **Can I pass custom parameters to the prefill service?**
Custom parameters are planned for an upcoming release. -->

* **Posso memorizzare in cache il contenuto protetto?**
Per impostazione predefinita, la memorizzazione nella cache delle funzioni di contenuto protetto è disabilitata. Per abilitare la funzione, puoi eseguire le istruzioni fornite in [Memorizzazione in cache di contenuti protetti](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=it).

* **Ho una forma adattiva localizzata; non è il rendering della versione localizzata? Quale potrebbe essere la causa e come risolverla?**

   La convenzione URL di Forms adattivo localizzato ora supporta la specifica di impostazioni internazionali nell’URL. La nuova convenzione URL consente di memorizzare nella cache i moduli localizzati su un’istanza di Dispatcher o CDN. Nell’ambiente di Cloud Service, utilizza il formato URL `http://host:port/content/forms/af/<afName>.<locale>.html` per richiedere una versione localizzata di un modulo adattivo anziché `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. Adobe consiglia di utilizzare Dispatcher o la memorizzazione in cache CDN. Consente di migliorare la velocità di rendering dei moduli precompilati.

* **Ho aggiornato un modulo adattivo; la versione aggiornata non è disponibile per i clienti da utilizzare?**
Per impostazione predefinita, CDN aggiorna la cache ogni 5 minuti, attende 5 minuti, quindi controlla la versione aggiornata.

* **È possibile utilizzare il passaggio Firma in un modulo adattivo per creare un’esperienza di firma nel browser?**
No, il passaggio Firma non è disponibile per [!DNL Forms] as a Cloud Service. Rimuovi il passaggio Firma nel tuo Adaptive Forms. Invece del passaggio Firma , consenti agli utenti di firmare un modulo adattivo dopo l’invio. Consente di continuare a fornire un’esperienza di firma nel browser.

* **Posso utilizzare il passaggio Verifica in un modulo adattivo?**
No, il passaggio Verifica non è disponibile per [!DNL Forms] as a Cloud Service. Rimuovi il passaggio di verifica dal Forms adattivo esistente prima di spostare tali moduli in un ambiente di Cloud Service.

* **Posso aggiungere grafici a un modulo adattivo?**
Sì, è possibile aggiungere grafici a Adattivo Forms. Adaptive Forms fornisce un componente grafico. Può essere utilizzato per aggiungere grafici a un modulo adattivo.

* **È possibile collegare un modello dati modulo a un modello di database relazionale?**
È possibile collegare un modello dati modulo a [!DNL RESTful web services], [!DNL SOAP-based web services], [!DNL OData services], ed Experience Manager del profilo utente come origini dati. Il supporto per la connessione di un modello dati modulo a un database relazionale non è disponibile.

* **Posso utilizzare certificati personalizzati con Form Data Model per l’autenticazione?**
Il modello dati modulo non fornisce un metodo per utilizzare certificati personalizzati per l’autenticazione. Pertanto, i certificati personalizzati come x509 e SSL a 2 vie non sono supportati.

* **Posso utilizzare Forms Portal per inviare un’azione Adaptive Forms?**

   È possibile modificare il Forms adattivo esistente per utilizzare [Invia all’endpoint REST](configuring-submit-actions.md#submit-to-rest-endpoint), [Invia e-mail](configuring-submit-actions.md#send-email), [Invia utilizzando il modello dati del modulo](configuring-submit-actions.md#submit-using-form-data-model)e [Richiamare un flusso di lavoro AEM](configuring-submit-actions.md#invoke-an-aem-workflow) Invia azioni. L’azione di invio di Forms Portal e Forms Portal non è ancora disponibile. Controlla le note sulle versioni mensili per verificare la disponibilità delle funzioni.

* **Posso usare [!DNL AEM Forms] app con [!DNL AEM Forms] as a Cloud Service?**

   Forms adattivo offre un design responsive. Questi moduli modificano l’aspetto, la progettazione e l’interattività in base al dispositivo sottostante. Puoi continuare a utilizzare Adaptive Forms su dispositivi mobili tenendo d&#39;occhio le note sulle versioni mensili per la disponibilità delle funzioni.

* **Quali funzioni non fanno parte della versione iniziale GA?**
Portale Forms, [!DNL AEM Forms] app, integrazione con Adobe Analytics e integrazione con Adobe Target non fanno parte della versione iniziale GA. Per informazioni sulle nuove funzioni, consulta le note sulle versioni mensili.

* **Ho progettato un [Schema JSON per creare un modulo adattivo](adaptive-form-json-schema-form-model.md). Lo schema JSON definisce gli eventi per alcuni componenti di moduli adattivi. AEM Forms as a Cloud Service supporta gli eventi?**
Crea il modulo adattivo in base allo schema JSON nell’ambiente Forms di Experience Manager 6.5 e utilizza il [Utilità di migrazione](migrate-to-forms-as-a-cloud-service.md) per migrare tale Adaptive Forms ad AEM Forms as a Cloud Service. L&#39;utility converte tali eventi in librerie client e puoi continuare a utilizzare Adaptive Forms con gli eventi in un ambiente di Cloud Service.

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


