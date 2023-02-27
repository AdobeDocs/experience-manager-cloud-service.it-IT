---
title: Introduzione a [!DNL AEM Forms] as a Cloud Service
description: Scopri AEM Forms e come ti può aiutare a produrre documenti e contenuti di moduli pronti per l’azienda. Scopri Platform-as-a-Service (PaaS) e come gestire moduli digitali e processi aziendali di classe enterprise, nonché come collegare Forms alle origini dati correnti.
landing-page-description: Scopri come utilizzare i moduli in AEM as a Cloud Service.
exl-id: aa5ef10c-ba78-4a9d-8b2b-a72a7a306888
source-git-commit: 2f9c4d85c55ee63a769c0137d4a70b2126228d5b
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 5%

---

# Introduzione {#introduction}

Adobe [!DNL Experience Manager Forms as a Cloud Service] offre una soluzione nativa per il cloud, Platform as a Service (PaaS), che consente alle aziende di creare, gestire, pubblicare e aggiornare moduli digitali complessi, integrando i dati inviati con i processi back-end, le regole aziendali e il salvataggio dei dati in un archivio dati esterno. Il servizio è sempre corrente, sempre disponibile e sempre in formazione.

È possibile utilizzare il servizio per creare ed eseguire il rollout di moduli digitali interattivi e coinvolgenti. Ad esempio, prendete un&#39;organizzazione che sta cercando di digitalizzare il proprio percorso di iscrizione clienti. Hanno più origini dati con dati cliente esistenti. È in corso la precompilazione dei moduli, l’aggiunta di firme elettroniche e l’archiviazione dei moduli compilati come file di PDF. Inoltre, l&#39;organizzazione dispone di più moduli di stampa (PDF forms), e sta anche cercando di convertire tutti i moduli di stampa in moduli digitali.



L&#39;organizzazione può utilizzare [!DNL AEM Forms] as a Cloud Service per creare moduli digitali, collegare moduli a origini dati esistenti, integrare moduli con [!DNL Adobe Sign] aggiungere firme elettroniche ai moduli e generare documenti di record per archiviare i moduli inviati come file PDF. L’organizzazione può inoltre utilizzare il servizio per convertire i PDF forms esistenti in moduli digitali.

L&#39;organizzazione può utilizzare [!DNL AEM Forms] as a Cloud Service e ottieni tutte queste funzionalità nel cloud senza richiedere alcuna infrastruttura locale. Il servizio consente inoltre di liberare le organizzazioni da complessi cicli di aggiornamento in quanto è sempre aggiornato con le funzioni più recenti.

## Funzioni principali {#key-features}

<!-- 
>[!BEGINTABS]

>[!TAB Adaptive Forms]

Adaptive Forms allows businesses to create and manage interactive, data-driven forms for their websites and other digital channels responsive, mobile-friendly forms without. </br> </br> Adaptive Forms in AEM also include a drag-and-drop form builder, which enables non-technical users to easily create and customize forms using pre-built form components such as text boxes, dropdown menus, and date pickers. This enables faster form creation and eliminates the need for extensive coding and development. </br> </br> In addition, AEM Adaptive Forms offer several other features, including: <ul><li>Advanced workflows for routing, approval, and submission of form data Real-time validation and error checking to ensure data accuracy </li><li>Integration with third-party data sources and APIs for pre-filling form fields or validating data </li><li>Advanced analytics and reporting capabilities to track form usage, conversion rates, and other key metrics </li><li>Integration with Adobe Sign and DocuSign for e-signatures </li>

>[!TAB Automated Forms Conversion Service]

Automated Forms Conversion Service allows businesses to convert legacy PDF-based forms into interactive, digital forms that can be easily managed and distributed online. The service helps: <ul><li>Save manual effort required to convert print forms to adaptive forms.</li><li>Applies patterns and appropriate validations during conversion</li><li>Generate Document of Record during conversion </li><li>Group commonly occurring fields into reusable form fragments </li> <li>Enables Adobe Analytics during conversion</li>

>[!TAB Communications API (Document Services)]

Communications APIs are a set of RESTful APIs (Application Programming Interfaces) that enable businesses to automate the creation, management, and delivery of personalized, data-driven communications. </br> </br> These APIs also enable businesses to integrate their communications workflows with third-party systems and data sources, allowing them to create highly targeted and personalized messages that are triggered by specific events or user behaviors. Some key features of AEM Forms Communications APIs include:<ul><li> Dynamic content delivery: The APIs allow businesses to create and deliver dynamic content that is tailored to individual users based on their preferences, behaviors, and past interactions with the business.</li> <li>Personalized messaging: The APIs enable businesses to personalize their communications by including user-specific data such as names, addresses, and purchase history.</li><li>Integration with back-end systems: The APIs can be integrated with a wide range of back-end systems, including CRMs, databases, and marketing automation platforms.</li><li> Generate Pixel Perfect PDF documents: The APIs generate pixel-perfect PDF documents that are customized with user-specific data and content. This feature enables businesses to create highly professional and polished documents, such as invoices, contracts, and statements, that are delivered to users in PDF format.

>[!TAB Advanced Analytics]

The service provides OOTB support to connect with Adobe Analytics. Connecting forms with Adobe Analytics provides several benefits for businesses, including: <ul><li> Improved understanding of user behavior: By connecting forms with Adobe Analytics, businesses can gain a deeper understanding of how users are interacting with their forms. This includes insights into user engagement, conversion rates, drop-off points, and other key metrics that can help businesses identify areas for improvement and optimize their forms for better user experiences. </li><li>Better targeting of marketing efforts: By analyzing user behavior on forms, businesses can gain valuable insights into user preferences and interests. This information can be used to better target marketing efforts and create more effective campaigns that drive engagement and conversions. </li><li> Reduced error rate: By integrating forms with Adobe Analytics, you can find insights about field with most errors and improve data quality, leading to better decision-making and more accurate insights. </li><li> Improved ROI: By optimizing forms based on insights gained from Adobe Analytics, businesses can improve conversion rates and drive more revenue from their digital channels. This can lead to a higher return on investment (ROI) for marketing and digital initiatives, helping businesses to achieve their goals and drive growth.</li>


>[!ENDTABS] -->

| Moduli adattivi | API di comunicazione | Servizio automated forms conversion | Forms Workflow | E-Sign | Forms Analytics | Modello Dati |
|---|---|---|---|---|---| ---|
| Crea e gestisci moduli interattivi, dinamici, reattivi, facili da usare su dispositivi mobili e basati su dati per siti web, app e altri canali digitali e di stampa. | Puoi automatizzare la creazione, la gestione e la distribuzione di comunicazioni personalizzate basate su dati con API RESTful (interfacce di programmazione applicazioni) on-demand o a intervalli pianificati. | Converti i moduli legacy basati su PDF in Forms adattivo che possono essere facilmente gestiti e distribuiti online. | Automatizzare i processi aziendali che coinvolgono moduli e document services. Assegnare, instradare, esaminare e approvare moduli e documenti man mano che questi passano attraverso diverse fasi di un processo aziendale. | Effettua l’integrazione con Adobe Sign e DocuSign per inviare facilmente Forms e documenti agli utenti per la firma elettronica. | Utilizza Adobe Analytics per ottenere informazioni utili sul comportamento e sulle preferenze degli utenti. | Collega facilmente moduli e documenti con origini dati esterne per recuperare e inviare dati. |

<!--
| | |
|---|---|
| Adaptive Forms | Adaptive Forms allows businesses to create and manage interactive, data-driven forms for their websites and other digital channels responsive, mobile-friendly forms without. </br> </br> Adaptive Forms in AEM also include a drag-and-drop form builder, which enables non-technical users to easily create and customize forms using pre-built form components such as text boxes, dropdown menus, and date pickers. This enables faster form creation and eliminates the need for extensive coding and development. </br> </br> In addition, AEM Adaptive Forms offer several other features, including: <ul><li>Advanced workflows for routing, approval, and submission of form data Real-time validation and error checking to ensure data accuracy </li><li>Integration with third-party data sources and APIs for pre-filling form fields or validating data </li><li>Advanced analytics and reporting capabilities to track form usage, conversion rates, and other key metrics </li><li>Integration with Adobe Sign and DocuSign for e-signatures </li>|
| Automated Forms Conversion Service | Automated Forms Conversion Service allows businesses to convert legacy PDF-based forms into interactive, digital forms that can be easily managed and distributed online. The service helps: <ul><li>Save manual effort required to convert print forms to adaptive forms.</li><li>Applies patterns and appropriate validations during conversion</li><li>Generate Document of Record during conversion </li><li>Group commonly occurring fields into reusable form fragments </li> <li>Enables Adobe Analytics during conversion</li>|
| Communications API (Document Services) | Communications APIs are a set of RESTful APIs (Application Programming Interfaces) that enable businesses to automate the creation, management, and delivery of personalized, data-driven communications. </br> </br> These APIs also enable businesses to integrate their communications workflows with third-party systems and data sources, allowing them to create highly targeted and personalized messages that are triggered by specific events or user behaviors. Some key features of AEM Forms Communications APIs include:<ul><li> Dynamic content delivery: The APIs allow businesses to create and deliver dynamic content that is tailored to individual users based on their preferences, behaviors, and past interactions with the business.</li> <li>Personalized messaging: The APIs enable businesses to personalize their communications by including user-specific data such as names, addresses, and purchase history.</li><li>Integration with back-end systems: The APIs can be integrated with a wide range of back-end systems, including CRMs, databases, and marketing automation platforms.</li><li> Generate Pixel Perfect PDF documents: The APIs generate pixel-perfect PDF documents that are customized with user-specific data and content. This feature enables businesses to create highly professional and polished documents, such as invoices, contracts, and statements, that are delivered to users in PDF format.|
|Advanced Analytics| The service provides OOTB support to connect with Adobe Analytics. Connecting forms with Adobe Analytics provides several benefits for businesses, including: <ul><li> Improved understanding of user behavior: By connecting forms with Adobe Analytics, businesses can gain a deeper understanding of how users are interacting with their forms. This includes insights into user engagement, conversion rates, drop-off points, and other key metrics that can help businesses identify areas for improvement and optimize their forms for better user experiences. </li><li>Better targeting of marketing efforts: By analyzing user behavior on forms, businesses can gain valuable insights into user preferences and interests. This information can be used to better target marketing efforts and create more effective campaigns that drive engagement and conversions. </li><li> Reduced error rate: By integrating forms with Adobe Analytics, you can find insights about field with most errors and improve data quality, leading to better decision-making and more accurate insights. </li><li> Improved ROI: By optimizing forms based on insights gained from Adobe Analytics, businesses can improve conversion rates and drive more revenue from their digital channels. This can lead to a higher return on investment (ROI) for marketing and digital initiatives, helping businesses to achieve their goals and drive growth.</li>|

-->

## Innovazioni più recenti {#latest-innovations}

>[!BEGINTABS]

>[!TAB &#x200B; Forms adattivo headless]

||| |—|—| |![](https://experienceleague.corp.adobe.com/docs/experience-manager-headless-adaptive-forms/assets/how-headless-adaprive-forms-work.png?lang=en)| Creazione e gestione [moduli web headless](https://experienceleague.corp.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) nella piattaforma Adobe Experience Manager. Consente agli sviluppatori di creare, pubblicare e gestire moduli interattivi a cui è possibile accedere e interagire tramite API, anziché tramite un’interfaccia utente grafica tradizionale. <br/> <br/> Questi moduli sono progettati per essere inviati senza la necessità di un’interfaccia modulo HTML tradizionale. In altre parole, consentono di inviare i dati del modulo a livello di programmazione tramite un’API o un codice di backend senza richiedere elementi di modulo visibili sul front-end. <br/> <br/> I moduli headless sono utili in vari scenari, ad esempio per la creazione di applicazioni a pagina singola, applicazioni web progressive o applicazioni per dispositivi mobili, in cui l’interfaccia di un modulo HTML tradizionale potrebbe non essere necessaria o non essere pratica. Consentendo agli sviluppatori di inviare i dati dei moduli direttamente tramite API o codice backend, i moduli headless semplificano i flussi di lavoro e migliorano le prestazioni complessive delle applicazioni web.|




>[!TAB Componenti core]

||| |—|—| |![](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/assets/sample-core-components-based-adaptive-form.png?lang=en) | [Componenti core adattabili di Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features) sono un set di 24 componenti open-source compatibili con BEM basati sulle basi dei componenti core di Adobe Experience Manager WCM. Sono progettati appositamente per la creazione di Forms adattivo, moduli che si adattano al dispositivo, al browser e alle dimensioni dello schermo dell&#39;utente. <br/> <br/> Questi componenti possono essere utilizzati per creare esperienze eccezionali di acquisizione e registrazione dei dati fornendo un’ampia gamma di opzioni per i campi modulo, compresi campi di testo, caselle di controllo, menu a discesa e altro ancora. Includono anche funzioni quali convalida, logica condizionale e progettazione reattiva, che possono essere utilizzate per creare moduli facili da usare e intuitivi. <br/> <br/>  Inoltre, poiché questi componenti sono open-source, gli sviluppatori possono personalizzare ed estendere facilmente i componenti in base alle esigenze specifiche della propria organizzazione. Inoltre, questi componenti sono basati sulla metodologia BEM, che ne garantisce la scalabilità e la manutenzione.|



>[!TAB &#x200B; del connettore Microsoft PowerAutomate]

||| |—|—| |![](https://powerusers.microsoft.com/t5/image/serverpage/image-id/182924i17C4BEA1C045D731/image-size/large/is-moderation-mode/true?v=1.0&amp;px=999)| AEM Forms Power Automate Connector consente di integrare Adobe Experience Manager (AEM) Forms con Microsoft Power Automate (noto in precedenza come Microsoft Flow). Power Automate è un servizio basato su cloud che consente di creare flussi di lavoro automatizzati tra diverse applicazioni e servizi.  <br/> <br/> Con AEM Connettore automatico alimentazione modulo è possibile creare flussi di lavoro che si attivano automaticamente in base all’invio di un Modulo adattivo. Ad esempio, è possibile creare un flusso di lavoro che invia automaticamente una notifica e-mail a una persona specifica quando un utente invia un modulo o crea un’attività in Microsoft Planner al completamento di un modulo da parte dell’utente.  <br/> <br/> AEM Forms Power Automate Connector è un potente strumento che consente di automatizzare e integrare il Forms adattivo con altre applicazioni e servizi che si collegano con Microsoft Power Automate, consentendoti di lavorare con una più ampia gamma di strumenti. Puoi creare flussi di lavoro personalizzati in base alle tue esigenze, con la possibilità di aggiungere azioni, condizioni e attivatori personalizzati. Inoltre, Power Automate fornisce analisi e rapporti dettagliati, che consentono di monitorare e ottimizzare i flussi di lavoro nel tempo.|


>[!TAB Connettori di storage Microsoft: OneDrive e Sharepoint]

||| |—|—| |![](/help/forms/assets/onedrive-and-sharepoint.jpg)|I connettori di archiviazione Microsoft di AEM Forms per OneDrive e SharePoint sono connettori che consentono di integrare Adobe Experience Manager (AEM) Forms con Microsoft OneDrive e SharePoint. Questi connettori consentono di archiviare e gestire i dati e i documenti di AEM Forms all’interno delle soluzioni di storage basate su cloud di Microsoft. <br/> <br/> Questi connettori consentono di archiviare e gestire i dati e i documenti AEM Forms in Microsoft OneDrive. Con questo connettore, puoi caricare file di dati e allegati su OneDrive e SharePoint direttamente da AEM Forms. <br/> <br/> L&#39;utilizzo dei connettori di archiviazione Microsoft AEM Forms per OneDrive e SharePoint offre diversi vantaggi: <ul><li> **Integrazione**: Questi connettori consentono di integrare AEM Forms con soluzioni di storage basate su cloud Microsoft, per sfruttare la potenza di queste piattaforme. </li> <li> **Collaborazione**: OneDrive e SharePoint sono piattaforme di collaborazione che consentono ai membri del team di lavorare insieme su file e documenti. Integrando AEM Forms con queste piattaforme, puoi migliorare la collaborazione e il lavoro di squadra. </li> <li> **Sicurezza**: OneDrive e SharePoint offrono solide funzioni di sicurezza che garantiscono la memorizzazione e l&#39;accesso sicuro dei dati e dei documenti. </li> <br/> Nel complesso, i connettori di storage AEM Forms Microsoft per OneDrive e SharePoint sono potenti strumenti che consentono di archiviare e gestire i dati e i documenti AEM Forms nelle soluzioni di storage basate su cloud Microsoft, migliorando la collaborazione e la sicurezza.|


>[!ENDTABS]

<!--

| | |
|---|---|
| Adaptive Forms | Adaptive Forms allows businesses to create and manage interactive, data-driven forms for their websites and other digital channels responsive, mobile-friendly forms without. </br> </br> Adaptive Forms in AEM also include a drag-and-drop form builder, which enables non-technical users to easily create and customize forms using pre-built form components such as text boxes, dropdown menus, and date pickers. This enables faster form creation and eliminates the need for extensive coding and development. </br> </br> In addition, AEM Adaptive Forms offer several other features, including: <ul><li>Advanced workflows for routing, approval, and submission of form data Real-time validation and error checking to ensure data accuracy </li><li>Integration with third-party data sources and APIs for pre-filling form fields or validating data </li><li>Advanced analytics and reporting capabilities to track form usage, conversion rates, and other key metrics </li><li>Integration with Adobe Sign and DocuSign for e-signatures </li>|
| Automated Forms Conversion Service | Automated Forms Conversion Service allows businesses to convert legacy PDF-based forms into interactive, digital forms that can be easily managed and distributed online. The service helps: <ul><li>Save manual effort required to convert print forms to adaptive forms.</li><li>Applies patterns and appropriate validations during conversion</li><li>Generate Document of Record during conversion </li><li>Group commonly occurring fields into reusable form fragments </li> <li>Enables Adobe Analytics during conversion</li>|
| Communications API (Document Services) | Communications APIs are a set of RESTful APIs (Application Programming Interfaces) that enable businesses to automate the creation, management, and delivery of personalized, data-driven communications. </br> </br> These APIs also enable businesses to integrate their communications workflows with third-party systems and data sources, allowing them to create highly targeted and personalized messages that are triggered by specific events or user behaviors. Some key features of AEM Forms Communications APIs include:<ul><li> Dynamic content delivery: The APIs allow businesses to create and deliver dynamic content that is tailored to individual users based on their preferences, behaviors, and past interactions with the business.</li> <li>Personalized messaging: The APIs enable businesses to personalize their communications by including user-specific data such as names, addresses, and purchase history.</li><li>Integration with back-end systems: The APIs can be integrated with a wide range of back-end systems, including CRMs, databases, and marketing automation platforms.</li><li> Generate Pixel Perfect PDF documents: The APIs generate pixel-perfect PDF documents that are customized with user-specific data and content. This feature enables businesses to create highly professional and polished documents, such as invoices, contracts, and statements, that are delivered to users in PDF format.|
|Advanced Analytics| The service provides OOTB support to connect with Adobe Analytics. Connecting forms with Adobe Analytics provides several benefits for businesses, including: <ul><li> Improved understanding of user behavior: By connecting forms with Adobe Analytics, businesses can gain a deeper understanding of how users are interacting with their forms. This includes insights into user engagement, conversion rates, drop-off points, and other key metrics that can help businesses identify areas for improvement and optimize their forms for better user experiences. </li><li>Better targeting of marketing efforts: By analyzing user behavior on forms, businesses can gain valuable insights into user preferences and interests. This information can be used to better target marketing efforts and create more effective campaigns that drive engagement and conversions. </li><li> Reduced error rate: By integrating forms with Adobe Analytics, you can find insights about field with most errors and improve data quality, leading to better decision-making and more accurate insights. </li><li> Improved ROI: By optimizing forms based on insights gained from Adobe Analytics, businesses can improve conversion rates and drive more revenue from their digital channels. This can lead to a higher return on investment (ROI) for marketing and digital initiatives, helping businesses to achieve their goals and drive growth.</li>|

Adaptive Forms enable organizations to quickly design and deploy responsive, mobile-friendly forms without the need for extensive coding or development. With Adaptive Forms, businesses can create complex, multi-step forms with conditional logic, validations, and integrations with back-end systems such as CRMs and databases.

Adaptive Forms in AEM also include a drag-and-drop form builder, which enables non-technical users to easily create and customize forms using pre-built form components such as text boxes, dropdown menus, and date pickers. This enables faster form creation and eliminates the need for extensive coding and development.

In addition, AEM Adaptive Forms offer several other features, including:

Advanced workflows for routing, approval, and submission of form data
Real-time validation and error checking to ensure data accuracy
Integration with third-party data sources and APIs for pre-filling form fields or validating data
Advanced analytics and reporting capabilities to track form usage, conversion rates, and other key metrics
Overall, AEM Adaptive Forms provide businesses with a powerful tool for creating and managing complex, interactive forms that can be easily integrated into their digital experiences. |




| Feature/Capability | [!DNL AEM Forms] as a Cloud Service | AEM 6.5 Forms  | 
|---|---|---|
| Cloud-native architecture | &#x2611;  | &#x2612; |
| Auto-scaling based on load | &#x2611;  | &#x2612; |
| Zero downtime for upgrades | &#x2611;  | &#x2612; |
| Feature roll-out frequency | Agile*  | Quarterly |
| CDN (content delivery network) included | &#x2611;  | &#x2612; | 
| Topologies optimized for maximum resilience and efficiency| &#x2611;  | &#x2612; | 
| Cloud-native development environment | &#x2611;  | &#x2612; | 
| Self-Service via Cloud Manager | &#x2611;  | &#x2612; | 
| Automated upgrades with Continuous Integration and Continuous Delivery (CI/CD) | &#x2611;  | &#x2612; | 
| Adaptive Forms | &#x2611; | &#x2611; | 
| Data Integration with multiple data sources| &#x2611; | &#x2611; | 
| Communications APIs (Document Services) | &#x2611;* | &#x2611; | 
| Automated Forms Conversion Service | &#x2611; | &#x2611; | 
| Integration with [!DNL Micosoft Power Automate] | &#x2611; | &#x2612; | 
| Integration with [!DNL Adobe Sign] | &#x2611; | &#x2611; | 
| Integration with [!DNL AEM Sites] | &#x2611; | &#x2611; | 
| Integration with [!DNL Adobe Launch] | &#x2611; | &#x2611; | 
| Integration with [!DNL Adobe Analytics] | &#x2611; | &#x2611; | 
| Easy connectivity with Microsoft Dynamics and Salesforce | &#x2611; | &#x2612; |
| Custom submit action for with [!DNL DocuSign] | &#x2611; | &#x2612; | 
| Microsoft Azure data store connector | &#x2611; | &#x2612; |
| Hardened Rule editor | &#x2611; | &#x2612; | 
| Forms Portal | &#x2611; | &#x2611; | 
| AEM Workflows | &#x2611; | &#x2611; | 
| Document of Record | &#x2611; | &#x2611; | 
| Adaptive Forms Wizard | &#x2611; | &#x2612; | 
| Custom XCI for Document of Record| &#x2611; | &#x2612; |
| Invisible Captcha | &#x2611; | &#x2611; |
| Reusable Form Data Model configurations | &#x2611; | &#x2611; |
| Acroform-based Document of Record | &#x2611; | &#x2611; | 
| Government ID based identity authentication for Adobe Sign enabled Adaptive Forms | &#x2611; | &#x2611; | 
| Document Security | &#x2612; | &#x2611; |


* [Notable changes in comparison to AEM 6.5 Forms](notable-changes.md)
* [Frequently asked questions](faq.md)

-->