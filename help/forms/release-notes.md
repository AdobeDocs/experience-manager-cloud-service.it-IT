---
title: Note sulla versione di AEM Forms as a Cloud Service
description: Scopri nuove funzioni, versioni beta, informazioni precedenti al rilascio e altro ancora per AEM Forms as a Cloud Service.
exl-id: 35950b81-6e45-4a75-bd27-8c28fd68e42e
source-git-commit: 8074c0e9566b679830a56094bc9b47cb22f4bb4a
workflow-type: tm+mt
source-wordcount: '2028'
ht-degree: 16%

---


# [!DNL Experience Manager Forms] Nota sulla versione as a Cloud Service {#overview}

Adobe Experience Manager [!DNL AEM Forms] as a Cloud Service riceve miglioramenti su base continuativa. Per rimanere aggiornato sugli sviluppi più recenti, visita questa pagina regolarmente. Questa pagina fornisce informazioni su:

- Nuove funzioni
- Miglioramenti
- Funzioni pre-release
- Funzioni beta
- Correzioni di bug
- Funzionalità obsolete
- Istruzioni speciali
- Modifiche programmate per il futuro

>[!NOTE]
>
>Per le note sulla versione di tutti gli altri componenti di rilascio as a Cloud Service per AEM, consulta [Note sulla versione corrente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=it).

## 2021.10.0 {#sep-2021-10-0}

### Novità in [!DNL Forms] {#what-is-new-forms-oct-2021}

- **Analytics per Forms adattivo**: ora puoi acquisire e tenere traccia del comportamento degli utenti connessi e non (anonimi) tramite Adobe Analytics for Adaptive Forms per raccogliere informazioni approfondite sull’utente finale. Consente di prendere decisioni informate basate sui dati per migliorare l’esperienza dell’utente finale.

### Nuove funzioni disponibili nel canale prerelease di [!DNL Forms] {#prerelease-features-forms-oct-2021}

- **Esternalizzare i dati del flusso di lavoro AEM per un’elaborazione sicura**: è possibile memorizzare i dati dei flussi di lavoro AEM in elaborazione (dati variabili di flusso di lavoro AEM) contenenti elementi di dati personali sensibili (SPD) in un archivio gestito dal cliente per un’elaborazione sicura. Gli elementi dei dati e le variabili del flusso di lavoro non vengono memorizzati nell’archivio AEM e vengono recuperati su richiesta da un archivio gestito dal cliente durante l’elaborazione del flusso di lavoro.

### Funzioni beta di [!DNL Forms] {#sep-what-is-new-forms-oct-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**: [API di comunicazione](aem-forms-cloud-service-communications.md) consente di combinare un modello e dati XML per generare documenti di stampa in vari formati. Il servizio consente di generare documenti in modalità sincrona e batch. Le API consentono di creare applicazioni che permettono di:

   - Generare i documenti compilando i file modello (PDF e XDP) con i dati XML.
   - Generare moduli di output in vari formati, compresi flussi di stampa PDF non interattivi.

Puoi scrivere a [!DNL formscsbeta@adobe.com] per iscriversi al programma beta.

## 2021.9.0 {#sep-2021-09-0}

### Novità in [!DNL Forms] {#what-is-new-forms-sep-2021}

- **Utilizzare i ruoli di Adobe Sign in un modulo adattivo**: Adobe Sign per i livelli di servizio business ed enterprise ha la possibilità di espandere i ruoli dei destinatari del contratto, oltre a Firmatario, per soddisfare meglio i requisiti del flusso di lavoro. Ora puoi [consentire a ogni destinatario dell’accordo di configurare il proprio ruolo in un modulo adattivo](working-with-adobe-sign.md#addsignerstoanadaptiveform), con Firmatario come ruolo predefinito.

- **Analytics per Forms adattivo**: ora è possibile acquisire e [tracciare il comportamento degli utenti finali tramite Adobe Analytics](integrate-aem-forms-with-adobe-analytics.md) per Adaptive Forms per raccogliere informazioni approfondite sull’utente finale. Consente di prendere decisioni informate basate sui dati per migliorare l’esperienza dell’utente finale.

- **Facile connessione di AEM Forms con Microsoft Dynamics e Salesforce**: il servizio fornisce la configurazione dell’origine dati predefinita e i modelli dati per Microsoft Dynamics e Salesforce, rendendoli [per gli sviluppatori, configurare Microsoft Dynamics e Salesforce come origini dati per un modulo adattivo in modo più semplice e veloce](configure-msdynamics-salesforce.md).

- **Firma elettronica di un modulo adattivo tramite DocuSign:** [È possibile utilizzare DocuSign per apporre la firma elettronica a un modulo adattivo](integrate-docusign-adaptive-forms.md). Il servizio fornisce un’azione di invio personalizzata per utilizzare DocuSign con un modulo adattivo.

### Funzioni beta di [!DNL Forms] {#sep-what-is-new-forms-prerelease}

- **Connettore di archiviazione unificata:** Utilizza il connettore di archiviazione unificata per esternalizzare i dati in-process negli archivi gestiti dal cliente. Ad esempio, puoi memorizzare i dati dei flussi di lavoro AEM in elaborazione (dati sulle variabili di flusso di lavoro AEM) che contengono dati personali sensibili (SPD) in un archivio gestito dal cliente.
  <!--* Enable Forms Portal’s save and resume functionality and store adaptive forms drafts in a customer-managed data repository.-->

- **[!DNL AEM Forms as a Cloud Service - Communications]**: [API di comunicazione](aem-forms-cloud-service-communications.md) consente di combinare modelli XDP e dati XML per generare documenti di stampa in vari formati. Il servizio consente di generare documenti in modalità sincrona. Le API consentono di creare applicazioni che permettono di:
   - Generare i documenti compilando i file modello con dati XML.
   - Generare moduli di output in vari formati, compresi flussi di stampa PDF non interattivi.
   - Generare file di PDF di stampa da un modulo XFA PDF e Adobe Acrobat Form.

Puoi scrivere a [!DNL formscsbeta@adobe.com] per iscriversi al programma beta.

### Limitazioni {#limitations}

- Adobe Analytics può tenere traccia delle metriche dei moduli solo per gli utenti autenticati.

<!--

### New features available in [!DNL Forms] prerelease channel {#prerelease-features-forms-sep-2021}

* **Forms Portal:**  In a typical forms-centric portal deployment scenario, forms development and portal development are two disjoint activities. While Form Designers design and store forms in a repository, Web Developers create a web application to list forms and handle submission of forms. Forms are copied over to the web tier as there is no communication between the forms repository and the web application.

  Such scenarios often result in management issues and production delays. For example, if there is a newer version of a form available in the repository, you need to replace the form on the web tier, modify the web application, and redeploy the form on the public site. Redeploying the web application might cause some server downtime. Typically, the server downtime is a planned activity and therefore the changes cannot be pushed to the public site instantaneously.

  AEM Forms provides portal components that reduce management overheads and production delays. The components equip Web Developers to create and customize a forms portal on websites authored using Adobe Experience Manager (AEM). The form portal components allow you to add the following functionality:

  * List forms in customized layouts. Out of the box, List view and Card view are provided.

  * List published adaptive forms on an AEM Sites page.

  * Enable searching of forms based on a various criteria, such as form properties, metadata, and tags.

  * Lists drafts and submissions related to Adaptive Form created by end user.

  -->

## 2021.8.0 {#aug-2021-08-0}

### Novità in [!DNL Forms] {#what-is-new-forms-aug-2021}

<!-- * Automated Forms Conversion service can [convert PDF Forms in Italian and Portuguese language](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) to Adaptive Forms. -->

- Il progetto dell’archetipo dell’AEM per Forms as a Cloud Service ora include [modelli di dati per moduli per Microsoft Dynamics e Salesforce](setup-local-development-environment.md).

- **Documento di record basato su Acroform**: AEM Forms as a Cloud Service supporta l’utilizzo di [Adobe Acrobat Form PDF (Acroform PDF)](generate-document-of-record-for-non-xfa-based-adaptive-forms.md) come modello per documento record oltre al modello di modulo basato su XFA.

- **Connettore per l’archivio dati di Microsoft Azure**: ora è possibile [connettere il modello dati modulo al sistema di archiviazione Microsoft Azure](configure-azure-storage.md). Consente di recuperare e archiviare i dati dei moduli adattivi come BLOB nell’archiviazione di Microsoft Azure.

### Funzione beta di [!DNL Forms] {#aug-what-is-new-forms-prerelease}

- **Connettore di archiviazione unificata:** Utilizza il connettore di archiviazione unificata per esternalizzare i dati in-process negli archivi gestiti dal cliente. Ad esempio

   - Abilita la funzionalità di salvataggio e ripristino di Forms Portal e archivia le bozze di moduli adattivi in un archivio dati gestito dal cliente.
   - Archiviare dati di processo dei flussi di lavoro AEM (dati sulle variabili di flusso di lavoro AEM) contenenti dati personali sensibili (SPD) in un archivio gestito dal cliente.

- **[!DNL AEM Forms as a Cloud Service - Communications]**: [API di comunicazione](aem-forms-cloud-service-communications.md) consente di combinare modelli XDP e dati XML per generare documenti di stampa in vari formati. Il servizio consente di generare documenti in modalità sincrona. Le API consentono di creare applicazioni che permettono di:
   - Generare i documenti compilando i file modello con dati XML.
   - Generare moduli di output in vari formati, compresi flussi di stampa PDF non interattivi.
   - Generare file di PDF di stampa da un modulo XFA PDF e Adobe Acrobat Form.

Puoi scrivere a [!DNL formscsbeta@adobe.com] per iscriversi al programma beta.

### Nuove funzioni disponibili nel canale prerelease di [!DNL Forms] {#prerelease-features-forms-aug-2021}

- **Utilizzare i ruoli di Adobe Sign in un modulo adattivo**: Adobe Sign per i livelli di servizio business ed enterprise ha la possibilità di espandere i ruoli dei destinatari del contratto, oltre a Firmatario, per soddisfare meglio i requisiti del flusso di lavoro. Ora puoi [consentire a ogni destinatario dell’accordo di configurare il proprio ruolo in un modulo adattivo](working-with-adobe-sign.md#addsignerstoanadaptiveform), con Firmatario come ruolo predefinito.

- **Analytics per Forms adattivo**: ora puoi acquisire e tenere traccia del comportamento degli utenti finali tramite Adobe Analytics for Adaptive Forms per raccogliere informazioni approfondite sugli utenti finali. Consente di prendere decisioni informate basate sui dati per migliorare l’esperienza dell’utente finale.

- **Facile connessione di AEM Forms con Microsoft Dynamics e Salesforce**: il servizio fornisce la configurazione dell’origine dati predefinita e i modelli dati per Microsoft Dynamics e Salesforce, rendendoli [per gli sviluppatori, configurare Microsoft Dynamics e Salesforce come origini dati per un modulo adattivo in modo più semplice e veloce](configure-msdynamics-salesforce.md).

## 2021.7.0 {#july-2021-07-0}

### Novità in [!DNL Forms] {#july-what-is-new-forms}

- È ora possibile utilizzare il servizio di Automated forms conversion per [convertire PDF forms in francese, tedesco e spagnolo](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) ai moduli adattivi.
- È stato aggiunto un pannello separato all’editor modelli per visualizzare gli errori relativi ai componenti dei moduli adattivi. Consente di consolidare tutti gli errori dei moduli adattivi in un’unica posizione e di ridurre i tempi di risoluzione.

### Nuove funzioni disponibili nel canale prerelease di [!DNL Forms] {#july-prerelease-features-forms}

- **Documento di record basato su Acroform**: puoi anche [utilizzare Adobe Acrobat Form PDF (Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) come modello per documento record oltre al modello di modulo basato su XFA.

- **Connettore per l’archivio dati di Microsoft Azure**: ora è possibile [connettere il modello dati modulo al sistema di archiviazione Microsoft Azure](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html). Consente di recuperare e archiviare i dati dei moduli adattivi come BLOB nell’archiviazione di Microsoft Azure.

- **Variable Data Externalizer**: puoi salvare i dati delle variabili del flusso di lavoro AEM su un sistema di archiviazione esterno gestito dalla tua organizzazione.

### Funzione beta di [!DNL Forms] {#july-what-is-new-forms-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**: [API di comunicazione](aem-forms-cloud-service-communications.md) consente di combinare modelli XDP e dati XML per generare documenti di stampa in vari formati. Il servizio consente di generare documenti in modalità sincrona. Le API consentono di creare applicazioni che permettono di:
   - Generare i documenti compilando i file modello con dati XML.
   - Generare moduli di output in vari formati, compresi flussi di stampa PDF non interattivi.
   - Generare file di PDF di stampa da un modulo XFA PDF e Adobe Acrobat Form.

## 2021.6.0 {#july-2021-06-0}

### Novità in [!DNL Forms] {#june-what-is-new-forms}

- È stata aggiunta la possibilità di filtrare colonne personalizzate nella casella in entrata AEM.
- È stata aggiunta la possibilità di utilizzare l’editor di temi e il livello di stile dell’editor di moduli adattivi per assegnare uno stile al componente captcha.
- Sono state migliorate la velocità e la precisione per il rilevamento automatico delle sezioni logiche nei PDF forms sorgente e la conversione di tali sezioni nei corrispondenti pannelli dei moduli adattivi.
- È stata aggiunta l’azione Sposta per spostare un file PDF o XDP da una cartella a un’altra.

### Funzione beta di [!DNL Forms] {#june-what-is-new-forms-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**: API di comunicazione consente di combinare modelli XDP e dati XML per generare documenti di stampa in vari formati. Il servizio consente di generare documenti in modalità sincrona. Le API consentono di creare applicazioni che permettono di:

   - Generare documenti di modulo finali compilando i file modello con dati XML.
   - Generare moduli di output in vari formati, compresi flussi di stampa PDF non interattivi.
   - Genera PDF di stampa da un modulo XFA PDF e Adobe Acrobat Form (AcroForm).

- **Variable Data Externalizer**: puoi salvare i dati delle variabili del flusso di lavoro AEM su un sistema di archiviazione esterno gestito dalla tua organizzazione.

Puoi scrivere a [!DNL formscsbeta@adobe.com] per iscriversi al programma beta.

### Bug corretti in [!DNL Forms] {#june-forms-bugs-fixed}

- Quando un campo viene convalidato prima dell’invio dei dati al servizio back-end tramite Form Data Model (FDM), le convalide hanno esito positivo ma il servizio Form Data Model non riesce a richiamare la post-convalida.
- Quando invii un modulo contenente un campo di caricamento HTML standard da un dispositivo Apple iOS, a volte il contenuto del file non viene inviato e viene ricevuto un file da 0 byte all’altra estremità. Apple iOS 15.1 fornisce una correzione per il problema.

## 2021.5.0 {#may-2021-05-0}

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novità in [!DNL Forms] {#may-what-is-new-forms}

- **Aiuto contestuale**: è stata aggiunta una guida contestuale per l’editor di moduli adattivi, l’editor di modelli e l’editor di temi per aiutare gli autori a comprendere meglio le varie funzioni degli editor.
- **Messaggi di errore nel browser Proprietà**: sono stati aggiunti messaggi di errore per ogni proprietà nel browser Proprietà adattive di Forms. Questi messaggi aiutano a comprendere i valori consentiti per un campo.

### Prossima funzione beta di [!DNL Forms] {#may-what-is-new-forms-prerelease}

Output as a Cloud Service: il servizio di output consente di combinare modelli XDP e dati XML per generare documenti di stampa in vari formati. Il servizio consente di generare documenti in modalità batch sincrona e asincrona. Il servizio di output consente di creare applicazioni che consentono di:

- Generare documenti di modulo finali compilando i file modello con dati XML.
- Generare moduli di output in vari formati, compresi flussi di stampa PDF non interattivi.
- Genera PDF di stampa da PDF modulo XFA.

Per registrarti al programma beta, scrivi a formscsbeta@adobe.com.

### Bug corretti in [!DNL Forms] {#may-forms-bugs-fixed}

- In un passaggio Assegna attività di Flussi di lavoro AEM Forms, quando sostituisci l’icona predefinita dei pulsanti di azione con un’icona a forma di corallo, il flusso di lavoro smette di funzionare e registra un’eccezione. Il flusso di lavoro funziona come previsto quando vengono utilizzate le icone predefinite.
- Nel livello di layout, quando modifichi il numero di colonne, apri il livello di modifica e trascini alcuni componenti in un pannello, le caselle blu quadrate iniziano a comparire nell’area del contenuto dell’editor di moduli adattivi e l’editor non risponde.
- Il messaggio di errore relativo all’opzione di un editor di regole nel fornire l’URL di una risorsa adattiva o esterna è troppo lungo e non è di facile utilizzo.

## 2021.4.0 {#april-2021-04-0}

### Novità in [!DNL Forms] {#april-what-is-new-forms}

- **Utilizzare il metodo di autenticazione tramite documento ufficiale in Adaptive Forms abilitato per Adobe Sign**

  Basato su algoritmi avanzati di apprendimento automatico, il processo tramite documento ufficiale di Adobe Sign consente alle aziende di tutto il mondo di garantire un’autenticazione di alta qualità dell’identità del destinatario. Ora puoi utilizzare il metodo di autenticazione tramite documento ufficiale in Adaptive Forms abilitato per Adobe Sign.

  Il Government ID è un metodo di autenticazione dell’identità avanzato che indica al destinatario di [caricare l’immagine di un documento di identità ufficiale (patente di guida, carta d’identità, passaporto)](https://helpx.adobe.com/in/sign/using/adobesign-authentication-government-id.html)e quindi valuta il documento per assicurarne l&#39;autenticità.

- **Supporto all’utilizzo dell’esperienza di firma interna ai moduli per l’invio asincrono dei moduli adattivi**

  È ora possibile utilizzare l’esperienza di firma interna ai moduli per l’invio asincrono di moduli adattivi. È inoltre possibile incorporare un modulo adattivo in un [!DNL Experience Manager Sites] e utilizza l’esperienza di firma interna ai moduli per inviare moduli adattivi.

- **Supporto per l’utilizzo di una variabile per specificare un allegato durante la precompilazione di un Modulo adattivo per una fase Assegna attività**

  Durante la precompilazione di un modulo adattivo per una fase Assegna attività, è ora possibile utilizzare una variabile relativa al tipo di documento per selezionare un allegato di input per il modulo adattivo.

- **Supporto per l’utilizzo dell’opzione letterale per impostare il valore per una variabile di tipo JSON**

  È possibile utilizzare l’opzione letterale per impostare il valore di una variabile di tipo JSON nel passaggio Imposta variabile di un flusso di lavoro AEM. L’opzione letterale ti consente di specificare un JSON sotto forma di stringa.

- **Utilizzare l’ambiente di sviluppo locale per creare un documento di record (DoR)**

  Puoi utilizzare un XDP come modello per un documento di record nelle istanze di Cloud Service e nell’SDK as a Cloud Service di AEM Forms (ambiente di sviluppo locale). In precedenza, il supporto era limitato solo alle istanze di Cloud Service.

### Correzioni di bug in [!DNL Forms] {#april-bug-fixes-forms}

- Quando un modulo adattivo configurato per non generare il documento di record viene inviato a un flusso di lavoro AEM configurato per generare il documento di record, non viene visualizzato alcun messaggio di errore e l’operazione non viene inviata.
