---
title: Modifiche apportate tra AEM 6.5 Forms e AEM Cloud Services
description: 'Sei un utente di Experience Manager Forms e vuoi effettuare l’aggiornamento ad Adobe Experience Manager Forms as a Cloud Service? Scopri le modifiche più importanti prima di eseguire l’aggiornamento o la migrazione al Cloud Service.  '
contentOwner: khsingh
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 3%

---

# Modifiche di rilievo per gli utenti Adobe Experience Manager Forms esistenti  {#notable-changes-for-existing-AEM-Forms-users}

Adobe Experience Manager Forms as a Cloud Service apporta alcune modifiche di rilievo alle funzioni esistenti rispetto ad Adobe Experience Manager FormsOn-Premise e [!DNL Adobe-Managed Service] ambienti. Le differenze chiave sono elencate di seguito:

* Il servizio fornisce un ambiente di sviluppo locale e nativo per il cloud. Puoi utilizzare un [ambiente di sviluppo locale](setup-local-development-environment.md) per sviluppare e testare il codice personalizzato, i componenti, i modelli, i temi, Adaptive Forms e altre risorse prima di distribuire queste risorse in un ambiente cloud. Aiuta ad accelerare il processo di sviluppo.
* [!DNL AEM] come Cloud Service viene fornito con una rete CDN integrata. Il suo scopo principale è ridurre la latenza distribuendo contenuti memorizzabili nella cache dai nodi della CDN al perimetro, vicino al browser. È completamente gestita e configurata per garantire prestazioni ottimali alle applicazioni AEM.
* Un ambiente nativo per il cloud non dispone di console Web (gestione della configurazione). È possibile utilizzare [[!DNL AEM Forms] SDK as a Cloud Service per generare configurazioni](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) e la pipeline CI/CD a [distribuire la configurazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) all&#39;istanza di Cloud Service.

* La convenzione URL di Forms adattivo localizzato ora supporta la specifica di impostazioni internazionali nell’URL. La nuova convenzione URL consente di memorizzare nella cache i moduli localizzati su un’istanza di Dispatcher o CDN. Nell’ambiente di Cloud Service, utilizza il formato URL `http://host:port/content/forms/af/<afName>.<locale>.html` per richiedere una versione localizzata di un modulo adattivo anziché `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. Adobe consiglia di utilizzare Dispatcher o la memorizzazione in cache CDN. Consente di migliorare la velocità di rendering dei moduli precompilati.
* Il servizio di precompilazione unisce i dati con un modulo adattivo su un client. Consente di migliorare il tempo necessario per la precompilazione di un modulo adattivo. È sempre possibile configurare l’esecuzione dell’azione di unione su Adobe Experience Manager FormsServer.
* Per impostazione predefinita, le e-mail supportano solo i protocolli HTTP e HTTP. [Contatta il team di supporto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) per abilitare le porte per l’invio di e-mail e per abilitare il protocollo SMTP per l’ambiente.
* Adobe Experience Manager Forms as a Cloud Service introduce molte nuove funzioni e possibilità nei progetti AEM. Tuttavia, sono necessarie alcune modifiche per rendere i progetti Adobe Experience Manager Maven compatibili con AEM Cloud Service. Ad alto livello, AEM richiede una separazione di contenuto e codice in pacchetti secondari distinti per rispettare la suddivisione tra contenuto mutabile e immutabile. Utilizza la [Modernizzatore dell&#39;archivio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) strumento per ristrutturare i pacchetti di progetto esistenti separando il contenuto e il codice in pacchetti discreti in modo che siano compatibili con la struttura di progetto definita per Adobe Experience Manager as a Cloud Service.

<!--  If your Cloud Configuration contains a secret (password), create a separate Cloud Configuration for every Author instance (Developer, Stage, and Production). If a Cloud Configuration is also required on Publish instances, publish/replicate a separate Cloud Configuration for every Publish instance (Developer, Stage, and Production). 

* When you create a Cloud Configuration that contains a secret, each Cloud Service instance (Developer, Stage, and Production) uses its own encryption key to encrypt the password before storing it. So, manually create such Cloud Configuration for every Cloud Service instance (Developer, Stage, and Production). Also, do not store secrets used in a Cloud Configuration to your Cloud Manager Git repository.

* Use [!DNL Cloud Manager] [APIs to convert and provide your passwords as secrets](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#setting-values-via-api). Do not store plain text password or secrets on your environments. -->

* Utilizzo di configurazioni specifiche per l’ambiente per valori di configurazione OSGi segreti, come password, chiavi API private o qualsiasi altro valore. Non possono essere archiviati in Git per motivi di sicurezza. [Utilizza configurazioni specifiche per l’ambiente segreto per memorizzare il valore per i segreti su tutti gli ambienti Adobe Experience Manager as a Cloud Service, inclusi Stage e Produzione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#when-to-use-secret-environment-specific-configuration-values).

Per un elenco completo delle modifiche in Adobe Experience Manager as a Cloud Service, vedi [Novità e differenze](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html).

<!-- ## Feature comparison {#comparison}

[!DNL AEM Forms] as a Cloud Service and Experience Manager 6.5 Forms share a common set of features: Adaptive Forms, data integration, integration with [!DNL Adobe Sign], themes, templates, and forms management interface are identical. You can easily port your existing Adaptive Forms from an Experience Manager 6.5 Forms or an earlier version to [!DNL AEM Forms] as a Cloud Service.

### Features of AEM 6.5 Forms and [!DNL AEM Forms] as a Cloud Service {#feature-comparison}

The following table lists the major features of Experience Manager 6.5 Forms and provides information about whether the feature is partially or fully supported in [!DNL AEM Forms] as a Cloud Service, with a link to more information about the feature. The table also lists extra features available in [!DNL AEM Forms] as a Cloud Service.


| Feature/Capability | AEM 6.5 Forms | [!DNL AEM Forms] as a Cloud Service |
| - | - | - |
| Adaptive Forms | &#x2611; | &#x2611; |
| Data Integration | &#x2611; | &#x2611;(With some changes) |
| Automated Forms Conversion Service | &#x2611; | &#x2611; |
| Integration with Adobe Sign | &#x2611; | &#x2611;(With some changes) |
| Themes and Templates | &#x2611; | &#x2611; ([With some changes](themes.md#difference-in-themes))|
| Rule editor | &#x2611; | &#x2611; (With some changes) |
| Forms Portal | &#x2611; | --- |
| Integration with Adobe Analytics | &#x2611; | &#x2612; |
| Document Security | &#x2611; | &#x2612; | -->

<!-- ## New features {#comparison} -->



## Miglioramenti principali {#whats-new}

<!-- [!DNL AEM Forms] as a Cloud Service offers benefits like auto-scaling, cost-effectiveness, zero downtime for upgrades, and cloud-native development environment and more. The list does not stop here. The following features are are start and are available only for [!DNL AEM Forms] as a Cloud Service: -->

Le seguenti funzioni e miglioramenti sono disponibili solo in [!DNL AEM Forms] as a Cloud Service:

**Editor di regole visive ottimizzato**
Il servizio fornisce un [Editor di regole visive](rule-editor.md#visual-rule-editor). Il servizio ha aggiunto le seguenti funzionalità all&#39;editor di regole di Visual per facilitare la scrittura di regole capaci:

* [Nuovi eventi di invio](working-with-adobe-sign.md#available-operator-types-and-events-in-rule-editor): `Navigation`, `Step Completion`, `Successful Submission`e `Error`

* [Nuovo tipo di dati `scope`](rule-editor.md#custom-functions). È possibile utilizzare `scope` tipo di dati in una funzione personalizzata per passare l’intero ambito di un modulo.

* Possibilità di utilizzo [@this per specificare un JSDoc in una funzione personalizzata](rule-editor.md#custom-functions). Consente di richiamare una funzione personalizzata utilizzando @this in un componente attivo.

* Possibilità di aggiungere condizioni per le regole basate su proprietà.

**Componenti core**
La [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) sono un set di componenti WCM (Web Content Management) standardizzati che consentono di AEM per velocizzare i tempi di sviluppo e ridurre i costi di manutenzione. [!DNL AEM Forms] Supporti as a Cloud Service **[!UICONTROL Contenitore AEM Forms]** Componente core. Puoi utilizzare il componente per incorporare un modulo adattivo in una pagina AEM Sites.

**Archetipo AEM per Forms as a Cloud Service**
[Archetipo AEM](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-27) aiuta a iniziare a sviluppare [!DNL AEM Forms] as a Cloud Service. Puoi utilizzare Archetype versione 27 o successiva per creare un modello di progetto compatibile con [!DNL AEM Forms] Ambiente as a Cloud Service. Archetype include anche alcuni temi e modelli di esempio per aiutarti a iniziare rapidamente.

**Flusso di informazioni sicuro e migliorato tra i moduli e Sign**
[Integrazione adattiva di Forms e Adobe Sign](working-with-adobe-sign.md) offerta al Cloud Service di invio simultaneo di dati e attività di firma. L’invio dei moduli è indipendente dallo stato della firma e consente di inviare i moduli più rapidamente. Oltre a ciò, il servizio non salva alcun dato sulle istanze del Cloud Service rendendo il processo di firma super sicuro.

**Strumenti per Best practice Analyzer e migrazione**
Best Practices Analyzer fornisce una valutazione dell&#39;implementazione AEM corrente. Esegui lo strumento prima di [migrazione ad Forms as a Cloud Service](migrate-to-forms-as-a-cloud-service.md). Valuta la disponibilità a passare da una distribuzione Adobe Experience Manager (AEM) esistente a AEM as a Cloud Service.

Il servizio fornisce anche un [esperienza di migrazione migliorata](migrate-to-forms-as-a-cloud-service.md) per facilitare la migrazione da [!DNL AEM 6.4 Forms] e [!DNL AEM 6.5 Forms] a [!DNL AEM Forms] as a Cloud Service.

**Rendering dei moduli più rapidi e convalide lato server più rapide**
Il servizio utilizza la cache CDN e Dispatcher per fornire rappresentazioni più veloci e convalide lato server per Adaptive Forms.

**CAPTCHA migliorato**
Ora puoi [convalida CAPTCHA](captcha-adaptive-forms.md) sia per l’invio di moduli adattivi che per una logica di business. Puoi anche aggiungere condizioni per convalidare il CAPTCHA in un’azione dell’utente e mostrare o nascondere il componente CAPTCHA in un modulo adattivo in base alle regole.

Il componente CAPTCHA fornisce un’integrazione preconfigurata con Google reCAPTCHA. Puoi anche configurare altri servizi CAPTCHA per il componente, se necessario.

**Pagine master multiple per il documento di record**
È ora possibile utilizzare una pagina master diversa per ogni pagina di un documento di record e controllare il posizionamento di un pannello Modulo adattivo su un documento di record con opzioni di impaginazione.

**Aggiungi colonne a tabelle headless**
È possibile aggiungere ed eliminare colonne alle tabelle senza intestazioni. Le intestazioni nascoste vengono aggiunte a tali tabelle per facilitare l’aggiunta e l’eliminazione di colonne. Queste intestazioni sono visibili durante l’authoring ma rimangono nascoste nel modulo pubblicato. Le tabelle senza intestazioni si trovano principalmente in Adattivo Forms creato utilizzando il servizio Automated forms conversion.

**Azioni di invio migliorate**
È possibile utilizzare [Invia e-mail](configuring-submit-actions.md#send-email#send-email) Invia azione per inviare un PDF Document of Record (DoR) come allegato.

**Raggruppa e-mail per flusso di lavoro**
Puoi scegliere di [invia e-mail di notifica](aem-forms-workflow-step-reference.md#assign-task-step) dal passaggio Assegna attività a una singola persona o a un gruppo.

**Passaggio del modello dati del modulo di chiamata avanzato**
È ora possibile specificare il percorso della cartella per l’opzione Relativo al payload degli argomenti del servizio di input in un passaggio Invoke Form Data Model. Consente di mappare un file presente nella cartella specificata all’argomento del servizio senza specificare il nome esatto del file.

**Miglioramento della leggibilità dei file di traduzione**
In Forms as a Cloud Service, l’ordine di lettura dei campi e dei pannelli di un modulo adattivo e delle chiavi dei messaggi dei file di traduzione corrispondenti (file XLIFF) ha una struttura simile. Aiuta a migliorare la velocità di traduzione manuale.

<!-- ## Feature comparison {#feature-comparison}

[!DNL AEM Forms] as a Cloud Service and [!DNL AEM 6.5 Forms] share some features like Adaptive Forms, Data Integration, and Forms Portal. You can easily port your existing Adaptive Forms from an [!DNL AEM 6.5 Forms] or an earlier version to [!DNL AEM Forms] as a Cloud Service.

### Features of [!DNL AEM 6.5 Forms] and [!DNL AEM Forms] as a Cloud Service {#aem-6.5-vs-aem-forms-as-a-cloud-service}

The following table lists the major features of [!DNL AEM 6.5 Forms] and provides information about the features coming soon to [!DNL AEM Forms] as a Cloud Service:

| Feature/Capability | AEM 6.5 Forms  | [!DNL AEM Forms] as a Cloud Service |
|---|---|---|
| Cloud-native architecture | &#x2612; | &#x2611;  |
| Auto-scaling based on load | &#x2612; | &#x2611;  |
| Zero downtime for upgrades | &#x2612; | &#x2611;  |
| Feature roll-out frequency | Quarterly | Agile*  |
| CDN (content delivery network) included | &#x2612; | &#x2611;  |
| Topologies optimized for maximum resilience and efficiency | &#x2612; | &#x2611;  |
| Cloud-native development environment | &#x2612; | &#x2611;  |
| Self-Service via Cloud Manager | &#x2612; | &#x2611;  |
| Automated upgrades with Continuous Integration and Continuous Delivery (CI/CD)| &#x2611; | &#x2611;  |
| Adaptive Forms | &#x2611; | &#x2611; |
| Data Integration | &#x2611; | &#x2611; |
| Automated Forms Conversion Service | &#x2611; | &#x2611; |
| Integration with [!DNL Adobe Sign] | &#x2611; | &#x2611; |
| Integration with [!DNL AEM Sites] | &#x2611; | &#x2611; |
| Enhanced Visual Rule editor | &#x2612; | &#x2611; |
| Forms Portal | &#x2611; | Coming Soon |
| Integration with [!DNL Adobe Analytics] | &#x2611; | Coming Soon |
| Integration with [!DNL Adobe Target] | &#x2611; | Coming Soon |
| Document Security | &#x2611; | &#x2612; |

`*` New features every month and bug fix updates on daily basis.

For a comprehensive list of changes in AEM as a Cloud Service, See [What is New and What is Different](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/overview/what-is-new-and-different.html) and [Notable changes in [!DNL AEM Forms] as a Cloud Service](notable-changes.md) -->
