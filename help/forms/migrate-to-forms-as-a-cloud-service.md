---
title: Migrazione da AEM 6.5 Forms ad AEM Forms as a Cloud Service
description: Guida introduttiva del Percorso di migrazione all’AEM as a Cloud Service | Adobe Experience Manager. Migra da un [!DNL AEM Forms] (ambienti locali e AMS) per [!DNL AEM Forms] ambiente as a Cloud Service.
Keywords: 6.5 forms to cloud service, 6.5 forms to cs, migrate 6.5 forms to CS, migrate 6.5 forms to cloud service, upgrade 6.5 forms to CS, move 6.5 forms to CS, upgrade AEM 6.5 to CS, AEM Forms 6.5 to Cloud Service, AEM form migration to cloud service, Migration Journey to AEM as a Cloud Service | Adobe Experience Manager.
contentOwner: khsingh
feature: Adaptive Forms
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
role: User, Developer
level: Intermediate
topic: Migration
exl-id: 090e77ff-62ec-40cb-8263-58720f3b7558
source-git-commit: b2c8e739c4e1c5289ca263360f4f59b8a2c05f5b
workflow-type: tm+mt
source-wordcount: '1580'
ht-degree: 4%

---

# Migra da un [!DNL AEM Forms] (ambienti locali e AMS) per [!DNL AEM Forms] as a Cloud Service  {#Harden-your-AEM-Forms-as-a-Cloud-Service-environment}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/upgrade-aem-forms/upgrade.html) |
| AEM as a Cloud Service | Questo articolo |

È possibile migrare o aggiornare Forms adattivo, temi, modelli e configurazioni cloud da <!-- AEM 6.3 Forms AEM 6.4 Forms on OSGi and --> AEM 6.5 Forms su OSGi a [!DNL AEM] as a Cloud Service. Prima di eseguire la migrazione di queste risorse, utilizza l’utility di migrazione per convertire il formato utilizzato nelle versioni precedenti nel formato utilizzato in [!DNL AEM] as a Cloud Service.
Iniziamo con il percorso di migrazione a AEM as a Cloud Service | Adobe Experience Manager. Quando si esegue l&#39;utilità di migrazione, vengono aggiornate le risorse seguenti:

* Componenti personalizzati per Forms adattivo
* Modelli e temi Forms adattivi
* Configurazioni cloud
* Gli script dell’editor di codice vengono convertiti in funzioni riutilizzabili e applicati alle regole visive.

## Considerazioni per la migrazione a Forms as a Cloud Service {#consideration}

Per migrare da AEM 6.5 Forms ad AEM Cloud Service, è importante tenere conto dei seguenti punti:

* Il servizio consente di migrare i contenuti solo da [!DNL AEM Forms] in ambienti OSGi. Migrazione di contenuti da [!DNL AEM Forms] in JEE a un ambiente di Cloud Service non è supportato.

* (Solo per le versioni precedenti a AEM 6.5 Forms) I Forms adattivi basati su modelli e temi predefiniti disponibili in AEM 6.3 Forms o versione precedente non sono supportati in [!DNL AEM Forms] as a Cloud Service.

* Adobe Experience Manager Forms as a Cloud Service apporta alcune modifiche di rilievo alle funzioni esistenti rispetto agli ambienti Adobe Experience Manager 6.5 Forms (On-Premise e Adobe-Managed Service). Prima di procedere alla migrazione al servizio, [scopri queste modifiche rilevanti](notable-changes.md) e [differenze a livello di funzione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#viewing-report) per decidere la migrazione in base alle funzioni richieste dalla tua organizzazione.




<!-- 
## Difference with AEM 6.5 Forms 

| Feature         | Difference with AEM 6.5 Forms    |
|--------------|-----------|
| HTML5 Forms (Mobile Forms)     | The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms. |
| Adaptive Forms     | <li><b>XSD-Based Adaptive Forms:</b> The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms. </li> <li><b> Adaptive Form templates:</b> Use build pipeline and corresponding Git repository of your program to import existing Adaptive Form templates. </li><li><b>Rule editor:</b> AEM Forms as a Cloud Service provides a hardened [Rule editor](rule-editor.md#visual-rule-editor). The code editor is not available on Forms as a Cloud Service. The migration utility helps you migrate your forms that have custom rules (created in code editor). The utility converts such rules into custom functions supported on Forms as a Cloud Service. You can use the reusable functions with Rule editor to continue obtaining results obtained with rule scripts  The `onSubmitError` or `onSubmitSuccess` functions are now available as actions the Rule Editor. </li> <li><b>Drafts and submissions:</b> The service does not retain metadata for drafts and submitted Adaptive Forms. </li> <li><b> Prefill Service:</b> By default, the prefill service merges data with an Adaptive Form at client as opposed to merging data on Server in AEM 6.5 Forms. The feature helps improve the time required to prefill an Adaptive Form. You can always configure to run the merge action on the Adobe Experience Manager Forms Server. </li><li><b>Submit actions:</b> The **Email as PDF** action is not available. The **Email** submit action provide options to send attachments and attach Document of Record (DoR) with email. </li>|
| Form Data Model | <li>Forms data model supports only HTTP and HTTPs endpoints to submit data. </li><li>Forms as a Cloud Service allows to use Microsoft Azure Blob, Microsoft Sharepoint, Microsoft OneDrive, and services supporting general CRUD (Create, Read, Update, and Delete) operations as data stores. The service does not support JDBC connector, Mutual SSL for Rest connector, and x509 certificate-based authentication for SOAP data sources. </li>|
| Automated Forms Conversion Service     | The service does not provide meta-model for Automated Forms Conversion Service. You can [download it from Automated Forms Conversion Service documentation](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).|
|Configurations|<li>Email support only HTTP and HTTPs protocols, by default. [Contact the support team](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) to enable ports for sending emails and to enable SMTP protocol for your environment. </li> <li>If you use custom bundles, recompile your code with latest version of adobe-aemfd-docmanager before using these bundles with Forms as a Cloud Service.</li> |
| Document Manipulation APIs (Assembler Service)| The service does not support operations dependent on other services or applications: <li>Conversion of documents in a non-PDF format to a PDF format is not supported. For example, Microsoft Word to PDF, Microsoft Excel to PDF, and HTML to PDF are not supported</li><li>Adobe Distiller-based conversions are not supported. For example, PostScript(PS) to PDF</li><li>Forms Service-based conversions are not supported. For example, XDP to PDF Forms.</li><li>The service does not support converting a Signed PDF or Transparent PDF to another PDF format.</li>| -->

## Prerequisiti {#prerequisites}

Per garantire una transizione fluida da AEM Forms 6.5 all’ambiente as a Cloud Service AEM, è importante considerare i seguenti prerequisiti:

* Abilita [Forms - Registrazione digitale](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html?#editing-program) opzione su per il programma di Cloud Service Forms e [eseguire la pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=it).

  ![Risultato esecuzione di prova](assets/enable-add-on.png)

* In un ambiente di Cloud Service, l&#39;utility di migrazione funziona insieme allo strumento di mappatura utenti e allo strumento di trasferimento dei contenuti. L&#39;utilità di migrazione rende [!DNL AEM Forms] risorse compatibili con il Cloud Service e lo strumento content transfer esegue la migrazione dei contenuti dalle [!DNL AEM Forms] ambiente in un [!DNL AEM] ambiente as a Cloud Service. Prima di utilizzare l&#39;utilità di migrazione, apprendere il processo di [passaggio all’AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/home.html?lang=it). Il processo è costituito da due strumenti:
   * [Strumento di mappatura utenti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration): lo strumento di mappatura utenti consente di mappare gli utenti con gli account utente Adobe IMS corrispondenti.
   * [Strumento Content Transfer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration): lo strumento Content Transfer (Trasferimento contenuti) consente di preparare e trasferire i contenuti dall’ambiente esistente a un ambiente di Cloud Service. Consente agli utenti di effettuare facilmente l’aggiornamento da AEM Forms all’ambiente cloud.
* Account con privilegi di amministratore su [!DNL AEM Forms] as a Cloud Service e locale [!DNL AEM Forms] ambiente.
* Scarica e installa Best Practice Analyzer, Content Transfer Tool e [!DNL AEM Forms] Utilità di migrazione da [Portale di distribuzione software.](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html)

* Esegui il [Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration) e risolvere il problema segnalato. Per i possibili problemi relativi alla migrazione da Adobe Experience Manager Forms ad Adobe Experience Manager Forms as a Cloud Service, consulta [Rilevamento pattern AEM per Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#viewing-report).


<!-- * Download the latest [compatibility package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases) for your [!DNL AEM Forms] version. -->




## Migra [!DNL AEM 6.5 Forms] risorse per AEM Cloud Service {#use-the-migration-utility}

Effettua le seguenti operazioni per rendere [!DNL AEM Forms] risorse compatibili con il Cloud Service e trasferirle ad un [!DNL AEM] ambiente as a Cloud Service.

1. Creare un [clone](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/correct-method-to-clone-the-aem-environment/qaq-p/363487) del tuo esistente [!DNL AEM Forms] ambiente.

   >[!NOTE]
   >
   > Quando effettui la migrazione da 6.5 a Cloud Service, si consiglia di utilizzare l’ambiente clonato per eseguire lo strumento Content Transfer (Trasferimento contenuti) e l’utility di migrazione. Lo strumento Content Transfer e l’utility di migrazione apportano alcune modifiche al contenuto e alle risorse. Pertanto, non eseguire lo strumento Content Transfer (Trasferimento contenuti) e l’utility di migrazione in un ambiente di produzione.

1. Accedi all’ambiente clonato con privilegi di amministratore.

1. Esegui il [Strumento di mappatura utenti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration) per mappare gli utenti con gli account utente Adobe IMS corrispondenti. Per accedere a un’interfaccia utente devi disporre di account utente Adobe IMS [!DNL AEM Forms] istanza as a Cloud Service.

1. Scarica e installa [Strumento Content Transfer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration) e [!DNL AEM Forms] Utilità di migrazione as a Cloud Service da [Portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html) sull&#39;ambiente clonato. È possibile utilizzare Gestione pacchetti AEM per installare lo strumento e l&#39;utility.

1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Migrazione dei contenuti]**.

1. Apri **[!UICONTROL Prepara Forms per la migrazione]** Card. Il browser visualizza cinque opzioni:
   * **[!UICONTROL Migrazione risorse AEM Forms]**
   * **[!UICONTROL Migrazione dei componenti personalizzati di Forms adattivi]**
   * **[!UICONTROL Migrazione di modelli Forms adattivi]**
   * **[!UICONTROL Migrazione configurazioni AEM Forms Cloud]**
   * **[!UICONTROL Migrazione script editor di codice]**

1. Utilizza l’opzione uno dopo l’altro per rendere [!DNL AEM Forms] risorse compatibili con [!DNL AEM] as a Cloud Service:

   1. Tocca **[!UICONTROL Migrazione risorse AEM Forms]**, e nella schermata successiva, tocca **[!UICONTROL Avvia migrazione]**. Crea Forms adattivo e temi sul tuo [!DNL AEM Forms] ambiente compatibile con [!DNL AEM] as a Cloud Service.

   1. Tocca **[!UICONTROL Migrazione dei componenti personalizzati di Forms adattivi]** e nella pagina Migrazione componenti personalizzati, tocca **[!UICONTROL Avvia migrazione]**. Crea qualsiasi componente personalizzato sviluppato per Adaptive Forms e sovrapposizioni di componenti sul tuo [!DNL AEM Forms] ambiente compatibile con [!DNL AEM] as a Cloud Service.

   1. Tocca **[!UICONTROL Migrazione modello Forms adattivo]** e nella pagina Migrazione componenti personalizzati, tocca **[!UICONTROL Avvia migrazione]**. Crea modelli di modulo adattivo in `/apps` o `/conf` e creato utilizzando l’Editor di modelli AEM compatibile con [!DNL AEM] as a Cloud Service.

   1. Tocca **[!UICONTROL Migrazione configurazioni AEM Forms Cloud]** quindi, nella pagina Migrazione della configurazione, tocca **[!UICONTROL Avvia migrazione]**. Aggiorna e sposta i seguenti Cloud Service in una nuova posizione:

      * Cloud Service modello dati modulo
      * Cloud Service Google reCAPTCHA
      * [!DNL Adobe Sign] Servizio cloud
      * Cloud Service Adobe Fonts

   1. Tocca **[!UICONTROL Migrazione script editor di codice]**, specifica un percorso in cui salvare le funzioni riutilizzabili e tocca **[!UICONTROL Avvia migrazione].

   Il Cloud Service non supporta gli script dell&#39;editor di regole. Il **[!UICONTROL Migrazione script editor di codice]** lo strumento converte tutti gli script delle regole nell’ambiente in funzioni riutilizzabili e applica le funzioni riutilizzabili all’editor visivo nella posizione appropriata. Queste funzioni riutilizzabili vengono salvate sotto forma di librerie client e consentono di mantenere intatte le funzionalità esistenti. Lo strumento applica automaticamente le funzioni riutilizzabili generate al Forms adattivo corrispondente.

   Migrazione da AEM al Cloud Service, utilizzare [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#contentmanagement) per esportare le funzioni riutilizzabili (librerie client) in un pacchetto.

1. [Distribuisci](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#deploying-content-packages-via-cloud-manager-and-package-manager) il pacchetto delle funzioni riutilizzabili (librerie client), [codice personalizzato, componenti, configurazioni](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html#cloud-manager), le librerie personalizzate specifiche per le impostazioni locali [!DNL AEM] ambiente as a Cloud Service.

   <!-- 1. Install the latest [Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration) to your cloned [!DNL AEM Forms] environment. -->

1. Esegui il [Strumento Content Transfer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration). Quando si specificano i parametri **[!UICONTROL Crea set di migrazione]** , specifica il percorso di Forms adattivo, temi, modelli, modelli di dati dei moduli, Cloud Service, componenti personalizzati e altre risorse specifiche di AEM Forms per **[!UICONTROL Percorsi da includere]** opzione. Aggiunge specificato [!DNL AEM Forms] risorse al set di migrazione.

## Percorsi di varie risorse specifiche per AEM Forms

Durante la migrazione da AEM Forms 6.5 a Cloud Service, puoi individuare le risorse specifiche di AEM Forms all’indirizzo:

* **Forms adattivo**: i moduli adattivi sono disponibili all’indirizzo `/content/dam/formsanddocuments/`e `/content/forms/af`. Ad esempio, per un modulo adattivo denominato WKND Registration, aggiungi percorsi `/content/dam/formsanddocuments/wknd-registration` e `/content/forms/af/wknd-registration`.
* **Modello dati modulo**: tutti i modelli di dati del modulo sono disponibili all’indirizzo `/content/dam/formsanddocuments-fdm`. Esempio: `/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`.

* **Librerie client**: il percorso predefinito delle librerie client è `/etc/clientlibs/fd/theme`.

* **Modelli di modulo adattivo**: il percorso predefinito dei modelli è `/conf/<template folder>`. Ad esempio, per un modello con titolo percorso di aggiunta di base `/conf/ReferenceEditableTemplates/settings/wcm/templates/basic`.

* **Temi di moduli adattivi e librerie client**: il percorso predefinito dei temi è ` /content/dam/formsanddocuments-themes/` e il percorso predefinito delle librerie client è `/etc/clientlibs/fd/theme`. Ad esempio, per un modello con titolo Percorso aggiunta tema WKND ` /content/dam/formsanddocuments-themes/wkndtheme` e le librerie client per il tema in `/etc/clientlibs/reference-themes/wkndtheme-3-0`. Puoi anche avere temi e librerie client in altri percorsi personalizzati.

* **Configurazioni cloud**: le configurazioni cloud sono disponibili all’indirizzo `/conf/`. Ad esempio, la configurazione cloud del modello dati modulo si trova in `/conf/global/settings/cloudconfigs/fdm`.

* **Modello flusso di lavoro**: i modelli dei flussi di lavoro per l’AEM sono disponibili all’indirizzo `/conf/global/settings/workflow/models/`. Ad esempio, per un modello di flusso di lavoro denominato WKND Registration add path `/conf/global/settings/workflow/models/wknd-registration`

Puoi aggiungere i percorsi cartella di livello superiore elencati di seguito o specifici come descritto di seguito. Consente di migrare una determinata risorsa e tutte le risorse e i moduli contemporaneamente, quando si esegue l’aggiornamento a Cloud Service dai moduli AEM 6.5.

* `/content/dam/formsanddocuments-fdm`
* `/content/dam/formsanddocuments/themes`
* `/content/forms/af`
* `/etc/clientlibs/fd/theme`

Quando esegui la migrazione dei modelli di flussi di lavoro AEM da AEM Forms 6.5 a Cloud Service, specifica i percorsi seguenti:

* `/conf/global/settings/workflow/models/`
* `/conf/global/settings/workflow/launcher`
* `/var/workflow/models`

## Vedi successivo

* [Modifiche di rilievo per gli utenti esistenti di Adobe Experience Manager 6.5 Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/notable-changes.html)
* [Integrazione con AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/setup-forms-cloud-service.html)
* [Creare il primo modulo adattivo sul Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html?lang=it)

## Informazioni aggiuntive

L’utility di migrazione consente di migrare Forms adattivo in base ai componenti di base. Inoltre, Forms as a Cloud Service supporta i componenti core Adaptive Forms. In questo modo è possibile:

* [Creazione di un Forms adattivo indipendente basato su Componente core](/help/forms/creating-adaptive-form-core-components.md)
* [Creare un modulo adattivo basato su componenti core direttamente in una pagina di AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)

Per ulteriori informazioni su AEM Forms as a Cloud Service, consulta:

* [Introduzione al Cloud Service AEM Forms](/help/forms/home.md)
* [Innovazioni nel Cloud Service AEM Forms](/help/forms/latest-innovations.md)