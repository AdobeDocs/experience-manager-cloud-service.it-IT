---
title: Come possiamo effettuare la migrazione da Forms AEM 6.5 ad AEM Forms as a Cloud Service?
description: Guida introduttiva al Percorso di migrazione ad AEM as a Cloud Service | Adobe Experience Manager. Migra da un  [!DNL AEM Forms]  (ambienti locali e AMS) a  [!DNL AEM Forms] ambiente as a Cloud Service.
Keywords: 6.5 forms to cloud service, 6.5 forms to cs, migrate 6.5 forms to CS, migrate 6.5 forms to cloud service, upgrade 6.5 forms to CS, move 6.5 forms to CS, upgrade AEM 6.5 to CS, AEM Forms 6.5 to Cloud Service, AEM form migration to cloud service, Migration Journey to AEM as a Cloud Service | Adobe Experience Manager.
contentOwner: khsingh
feature: Adaptive Forms
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
role: User, Developer
level: Intermediate
topic: Migration
exl-id: 090e77ff-62ec-40cb-8263-58720f3b7558
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 1%

---

# Migrare da un [!DNL AEM Forms] (ambienti locali e AMS) a [!DNL AEM Forms] as a Cloud Service  {#Harden-your-AEM-Forms-as-a-Cloud-Service-environment}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/upgrade-aem-forms/upgrade.html?lang=it) |
| AEM as a Cloud Service | Questo articolo |

È possibile migrare o aggiornare Forms adattivo, temi, modelli e configurazioni cloud da <!-- AEM 6.3 Forms AEM 6.4 Forms on OSGi and --> AEM 6.5 Forms su OSGi a [!DNL AEM] as a Cloud Service. Prima di eseguire la migrazione di queste risorse, utilizzare l&#39;utilità di migrazione per convertire il formato utilizzato nelle versioni precedenti nel formato utilizzato in [!DNL AEM] as a Cloud Service.
Iniziamo con il percorso di migrazione ad AEM as a Cloud Service | Adobe Experience Manager. Quando si esegue l&#39;utilità di migrazione, vengono aggiornate le risorse seguenti:

* Componenti personalizzati per Forms adattivo
* Modelli e temi Forms adattivi
* Configurazioni cloud
* Gli script dell’editor di codice vengono convertiti in funzioni riutilizzabili e applicati alle regole visive.

## Considerazioni per la migrazione a Forms as a Cloud Service {#consideration}

Per migrare da AEM 6.5 Forms ad AEM Cloud Service, è importante tenere conto dei seguenti punti:

* Il servizio consente di migrare il contenuto solo da [!DNL AEM Forms] in ambienti OSGi. La migrazione del contenuto da [!DNL AEM Forms] in JEE a un ambiente di Cloud Service non è supportata.

* (Solo per le versioni precedenti a AEM 6.5 Forms) I Forms adattivi basati su modelli e temi predefiniti disponibili in AEM 6.3 Forms o versione precedente non sono supportati in [!DNL AEM Forms] as a Cloud Service.

* Adobe Experience Manager Forms as a Cloud Service apporta alcune modifiche di rilievo alle funzioni esistenti rispetto agli ambienti Adobe Experience Manager 6.5 Forms (On-Premise e Adobe-Managed Service). Prima di procedere con la migrazione al servizio, [scopri queste modifiche rilevanti](notable-changes.md) e le [differenze a livello di funzionalità](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=it#viewing-report) per decidere di eseguire la migrazione in base alle funzionalità richieste dalla tua organizzazione.




<!-- 
## Difference with AEM 6.5 Forms 

| Feature         | Difference with AEM 6.5 Forms    |
|--------------|-----------|
| HTML5 Forms (Mobile Forms)     | The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms. |
| Adaptive Forms     | <li><b>XSD-Based Adaptive Forms:</b> The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms. </li> <li><b> Adaptive Form templates:</b> Use build pipeline and corresponding Git repository of your program to import existing Adaptive Form templates. </li><li><b>Rule editor:</b> AEM Forms as a Cloud Service provides a hardened [Rule editor](rule-editor.md#visual-rule-editor). The code editor is not available on Forms as a Cloud Service. The migration utility helps you migrate your forms that have custom rules (created in code editor). The utility converts such rules into custom functions supported on Forms as a Cloud Service. You can use the reusable functions with Rule editor to continue obtaining results obtained with rule scripts  The `onSubmitError` or `onSubmitSuccess` functions are now available as actions the Rule Editor. </li> <li><b>Drafts and submissions:</b> The service does not retain metadata for drafts and submitted Adaptive Forms. </li> <li><b> Prefill Service:</b> By default, the prefill service merges data with an Adaptive Form at client as opposed to merging data on Server in AEM 6.5 Forms. The feature helps improve the time required to prefill an Adaptive Form. You can always configure to run the merge action on the Adobe Experience Manager Forms Server. </li><li><b>Submit actions:</b> The **Email as PDF** action is not available. The **Email** submit action provide options to send attachments and attach Document of Record (DoR) with email. </li>|
| Form Data Model | <li>Forms data model supports only HTTP and HTTPs endpoints to submit data. </li><li>Forms as a Cloud Service allows to use Microsoft Azure Blob, Microsoft Sharepoint, Microsoft OneDrive, and services supporting general CRUD (Create, Read, Update, and Delete) operations as data stores. The service does not support JDBC connector, Mutual SSL for Rest connector, and x509 certificate-based authentication for SOAP data sources. </li>|
| Automated Forms Conversion Service     | The service does not provide meta-model for Automated Forms Conversion Service. You can [download it from Automated Forms Conversion Service documentation](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=it#default-meta-model).|
|Configurations|<li>Email support only HTTP and HTTPs protocols, by default. [Contact the support team](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=it#sending-email) to enable ports for sending emails and to enable SMTP protocol for your environment. </li> <li>If you use custom bundles, recompile your code with latest version of adobe-aemfd-docmanager before using these bundles with Forms as a Cloud Service.</li> |
| Document Manipulation APIs (Assembler Service)| The service does not support operations dependent on other services or applications: <li>Conversion of documents in a non-PDF format to a PDF format is not supported. For example, Microsoft Word to PDF, Microsoft Excel to PDF, and HTML to PDF are not supported</li><li>Adobe Distiller-based conversions are not supported. For example, PostScript(PS) to PDF</li><li>Forms Service-based conversions are not supported. For example, XDP to PDF Forms.</li><li>The service does not support converting a Signed PDF or Transparent PDF to another PDF format.</li>| -->

## Prerequisiti {#prerequisites}

Per garantire una transizione fluida da AEM Forms 6.5 all’ambiente AEM as a Cloud Service, è importante considerare i seguenti prerequisiti:

* Abilita l&#39;opzione [Forms - Registrazione digitale](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html?lang=it&#editing-program) per il tuo programma di Cloud Service Forms ed [esegui la pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html?lang=it).

  ![Risultato esecuzione di prova](assets/enable-add-on.png)

* In un ambiente di Cloud Service, l&#39;utility di migrazione funziona insieme allo strumento Content Transfer (Trasferimento contenuti). L&#39;utilità di migrazione rende le risorse [!DNL AEM Forms] compatibili con il Cloud Service e lo strumento di trasferimento dei contenuti esegue la migrazione dei contenuti dall&#39;ambiente [!DNL AEM Forms] a un ambiente as a Cloud Service [!DNL AEM]. Prima di utilizzare l&#39;utilità di migrazione, apprendere il processo di [passaggio ad AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/home.html?lang=it). Il processo utilizza il seguente strumento:
   * [Strumento Content Transfer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=it&#cloud-migration): lo strumento Content Transfer consente di preparare e trasferire il contenuto dall&#39;ambiente esistente a un ambiente di Cloud Service. Consente agli utenti di effettuare facilmente l’aggiornamento da AEM Forms all’ambiente cloud.
* Account con privilegi di amministratore per l&#39;as a Cloud Service [!DNL AEM Forms] e l&#39;ambiente [!DNL AEM Forms] locale.
* Scaricare e installare Best Practice Analyzer, Content Transfer Tool e l&#39;utilità di migrazione [!DNL AEM Forms] da [Software Distribution Portal](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html).

* Esegui lo strumento [Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=it#cloud-migration) e correggi il problema segnalato. Per i possibili problemi relativi alla migrazione da Adobe Experience Manager Forms ad Adobe Experience Manager Forms as a Cloud Service, vedi [Rilevamento pattern AEM per Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=it#viewing-report).


<!-- * Download the latest [compatibility package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=it#aem-65-forms-releases) for your [!DNL AEM Forms] version. -->




## Migra [!DNL AEM 6.5 Forms] risorse ad AEM Cloud Service {#use-the-migration-utility}

Eseguire la procedura seguente per rendere le risorse [!DNL AEM Forms] compatibili con il Cloud Service e trasferirle in un ambiente as a Cloud Service [!DNL AEM].

1. Crea un [clone](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/correct-method-to-clone-the-aem-environment/qaq-p/363487?profile.language=it) dell&#39;ambiente [!DNL AEM Forms] esistente.

   >[!NOTE]
   >
   > Quando effettui la migrazione da 6.5 a Cloud Service, si consiglia di utilizzare un ambiente clonato per eseguire lo strumento Content Transfer (Trasferimento contenuti) e l’utility di migrazione. Lo strumento Content Transfer e l’utility di migrazione apportano alcune modifiche al contenuto e alle risorse. Pertanto, non eseguire lo strumento Content Transfer (Trasferimento contenuti) o l’utilità di migrazione in un ambiente di produzione.

1. Accedi all’ambiente clonato con privilegi di amministratore.

1. As a Cloud Service Scaricare e installare [l&#39;utilità di trasferimento dei contenuti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=it&#cloud-migration) e l&#39;utilità di migrazione [!DNL AEM Forms] da [Portale di distribuzione software](https://experience.adobe.com/#/downloads/content/software-distribution/it/aemcloud.html) nell&#39;ambiente clonato. È possibile utilizzare Gestione pacchetti AEM per installare lo strumento e l&#39;utility.

1. Passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Migrazione contenuti]**.

1. Apri la scheda **[!UICONTROL Prepara Forms per la migrazione]**. Il browser visualizza cinque opzioni:
   * **[!UICONTROL Migrazione AEM Forms Assets]**
   * **[!UICONTROL Migrazione componenti personalizzati Forms adattivi]**
   * **[!UICONTROL Migrazione modelli Forms adattivi]**
   * **[!UICONTROL Migrazione configurazioni cloud AEM Forms]**
   * **[!UICONTROL Migrazione dello script dell&#39;editor di codice]**

1. Utilizza l&#39;opzione uno dopo l&#39;altro per rendere le risorse [!DNL AEM Forms] compatibili con [!DNL AEM] as a Cloud Service:

   1. Seleziona **[!UICONTROL AEM Forms Assets Migration]** e nella schermata successiva seleziona **[!UICONTROL Start Migration]**. Rende Forms adattivo e i temi nell&#39;ambiente [!DNL AEM Forms] compatibili con [!DNL AEM] as a Cloud Service.

   1. Seleziona **[!UICONTROL Migrazione componenti personalizzati Forms adattivi]** e nella pagina Migrazione componenti personalizzati seleziona **[!UICONTROL Avvia migrazione]**. Rende qualsiasi componente personalizzato sviluppato per Adaptive Forms e le sovrapposizioni di componenti nell&#39;ambiente [!DNL AEM Forms] compatibili con l&#39;as a Cloud Service [!DNL AEM].

   1. Seleziona **[!UICONTROL Migrazione modello Forms adattivo]** e nella pagina di migrazione dei componenti personalizzati seleziona **[!UICONTROL Avvia migrazione]**. I modelli per moduli adattivi in `/apps` o `/conf` e creati con l&#39;Editor modelli AEM sono compatibili con [!DNL AEM] as a Cloud Service.

   1. Seleziona **[!UICONTROL Migrazione configurazioni AEM Forms Cloud]**, quindi nella pagina Migrazione configurazione seleziona **[!UICONTROL Avvia migrazione]**. Aggiorna e sposta i seguenti Cloud Service in una nuova posizione:

      * Cloud Service modello dati modulo
      * Cloud Service Google reCAPTCHA
      * [!DNL Adobe Sign] Cloud Service
      * Cloud Service Adobe Fonts

   1. Seleziona **[!UICONTROL Migrazione script editor di codice]**, specifica un percorso per il salvataggio delle funzioni riutilizzabili e seleziona **[!UICONTROL Avvia migrazione].

   Il Cloud Service non supporta gli script dell&#39;editor di regole. Lo strumento **[!UICONTROL Migrazione degli script dell&#39;editor di codice]** converte tutti gli script delle regole nel tuo ambiente in funzioni riutilizzabili e applica le funzioni riutilizzabili all&#39;editor visivo nella posizione appropriata. Queste funzioni riutilizzabili vengono salvate sotto forma di librerie client e consentono di mantenere intatte le funzionalità esistenti. Lo strumento applica automaticamente le funzioni riutilizzabili generate al Forms adattivo corrispondente.

   Migrazione tramite modulo AEM al Cloud Service, utilizzare [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=it#contentmanagement) per esportare le funzioni riutilizzabili (librerie client) in un pacchetto.

1. as a Cloud Service [Distribuisci](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=it#deploying-content-packages-via-cloud-manager-and-package-manager) nell&#39;ambiente [!DNL AEM] il pacchetto delle funzioni riutilizzabili (librerie client), [codice personalizzato, componenti, configurazioni](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html?lang=it#cloud-manager), librerie personalizzate specifiche per le impostazioni locali.

   <!-- 1. Install the latest [Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=it&#cloud-migration) to your cloned [!DNL AEM Forms] environment. -->

1. Esegui lo [strumento Content Transfer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=it&#cloud-migration). Durante la specifica dei parametri nella schermata **[!UICONTROL Crea set di migrazione]**, specifica il percorso di Forms adattivo, temi, modelli, Modello dati modulo (FDM), Cloud Service, Componenti personalizzati e altre risorse specifiche di AEM Forms per l&#39;opzione **[!UICONTROL Percorsi da includere]**. Aggiunge [!DNL AEM Forms] risorse specificate al set di migrazione.

## Percorsi di varie risorse specifiche per AEM Forms

Durante la migrazione da AEM Forms 6.5 a Cloud Service, puoi individuare le risorse specifiche di AEM Forms all’indirizzo:

* **Forms adattivo**: è possibile trovare i moduli adattivi alle `/content/dam/formsanddocuments/` e `/content/forms/af`. Ad esempio, per un modulo adattivo denominato WKND Registration, aggiungi i percorsi `/content/dam/formsanddocuments/wknd-registration` e `/content/forms/af/wknd-registration`.
* **Modello dati modulo**: tutti i modelli dati del modulo (FDM) sono disponibili in `/content/dam/formsanddocuments-fdm`. Esempio: `/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`.

* **Librerie client**: il percorso predefinito delle librerie client è `/etc/clientlibs/fd/theme`.

* **Modelli per moduli adattivi**: il percorso predefinito dei modelli è `/conf/<template folder>`. Ad esempio, per un modello con titolo Percorso aggiunta di base `/conf/ReferenceEditableTemplates/settings/wcm/templates/basic`.

* **Temi modulo adattivo e librerie client**: il percorso predefinito dei temi è ` /content/dam/formsanddocuments-themes/` e il percorso predefinito delle librerie client è `/etc/clientlibs/fd/theme`. Ad esempio, per un modello con titolo WKND Theme, aggiungi il percorso ` /content/dam/formsanddocuments-themes/wkndtheme` e le librerie client per il tema in `/etc/clientlibs/reference-themes/wkndtheme-3-0`. Puoi anche avere temi e librerie client in altri percorsi personalizzati.

* **Configurazioni cloud**: le configurazioni cloud sono disponibili in `/conf/`. Ad esempio, la configurazione cloud di Form Data Model (FDM) è in `/conf/global/settings/cloudconfigs/fdm`.

* **Modello flusso di lavoro**: è possibile trovare modelli di flusso di lavoro AEM in `/conf/global/settings/workflow/models/`. Ad esempio, per un modello di flusso di lavoro denominato WKND Registration, aggiungere il percorso `/conf/global/settings/workflow/models/wknd-registration`

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

* [Modifiche di rilievo per gli utenti esistenti di Adobe Experience Manager 6.5 Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/notable-changes.html?lang=it)
* [Integrazione in AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/setup-forms-cloud-service.html?lang=it)
* [Crea il tuo primo modulo adattivo nel Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html?lang=it)

## Informazioni aggiuntive

L’utility di migrazione consente di migrare Forms adattivo in base ai componenti di base. Inoltre, Forms as a Cloud Service supporta i componenti core Adaptive Forms. In questo modo è possibile:

* [Creazione di un Forms adattivo indipendente basato su Componente core](/help/forms/creating-adaptive-form-core-components.md)
* [Creare un modulo adattivo basato su componenti core direttamente in una pagina AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)

Per ulteriori informazioni su AEM Forms as a Cloud Service, consulta:

* [Introduzione al Cloud Service AEM Forms](/help/forms/home.md)
* [Innovazioni nel Cloud Service AEM Forms](/help/forms/latest-innovations.md)