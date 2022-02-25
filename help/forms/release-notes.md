---
title: '"[!DNL AEM Forms] Note sulla versione as a Cloud Service"'
description: '"[!DNL AEM Forms] Note sulla versione as a Cloud Service"'
exl-id: 35950b81-6e45-4a75-bd27-8c28fd68e42e
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '2024'
ht-degree: 17%

---


# [!DNL Experience Manager Forms] Nota sulla versione as a Cloud Service {#overview}

Adobe Experience Manager [!DNL AEM Forms] Gli as a Cloud Service ricevono miglioramenti continui. Per rimanere aggiornato sugli sviluppi più recenti, visita questa pagina regolarmente. Questa pagina fornisce informazioni su:

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
>Per le note sulla versione di tutti gli altri componenti AEM versione as a Cloud Service, consulta [Note sulla versione corrente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=it).

## 2021.10.0 {#sep-2021-10-0}

### Novità in [!DNL Forms] {#what-is-new-forms-oct-2021}

- **Analytics per Forms adattivo**: È ora possibile acquisire e tenere traccia del comportamento sia di accesso che di non accesso (anonimo) tramite Adobe Analytics per Adaptive Forms per raccogliere informazioni sugli utenti finali. Consente di prendere decisioni informate basate sui dati per migliorare l’esperienza dell’utente finale.

### Nuove funzioni disponibili in [!DNL Forms] canale prerelease {#prerelease-features-forms-oct-2021}

- **Esternalizzare i dati del flusso di lavoro AEM per un’elaborazione sicura**: è possibile memorizzare i dati dei flussi di lavoro AEM in elaborazione (dati variabili di flusso di lavoro AEM) contenenti elementi di dati personali sensibili (SPD) in un archivio gestito dal cliente per un’elaborazione sicura. Gli elementi dei dati e le variabili del flusso di lavoro non vengono memorizzati nell’archivio AEM e vengono recuperati su richiesta da un archivio gestito dal cliente durante l’elaborazione del flusso di lavoro.

### Funzioni beta di [!DNL Forms] {#sep-what-is-new-forms-oct-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**: [API di comunicazione](aem-forms-cloud-service-communications.md) consente di combinare un modello e dati XML per generare documenti di stampa in vari formati. Il servizio consente di generare documenti in modalità sincrona e batch. Le API consentono di creare applicazioni che permettono di:

   - Generare i documenti compilando i file modello (PDF e XDP) con i dati XML.
   - Generare moduli di output in vari formati, compresi flussi di stampa PDF non interattivi.

Puoi scrivere in [!DNL formscsbeta@adobe.com] per iscriversi al programma beta.

## 2021.9.0 {#sep-2021-09-0}

### Novità in [!DNL Forms] {#what-is-new-forms-sep-2021}

- **Utilizzare i ruoli Adobe Sign in un modulo adattivo**: Adobe Sign per i livelli di servizio aziendali e aziendali ha la possibilità di espandere i ruoli per i destinatari del contratto, oltre al solo firmatario, in modo da soddisfare meglio i requisiti del flusso di lavoro. Ora puoi [abilitare ogni destinatario dell&#39;accordo a configurare il proprio ruolo in un modulo adattivo](working-with-adobe-sign.md#addsignerstoanadaptiveform), con il ruolo predefinito Firma .

- **Analytics per Forms adattivo**: Ora puoi acquisire e [tracciamento del comportamento dell’utente finale tramite Adobe Analytics](integrate-aem-forms-with-adobe-analytics.md) per Adattivo Forms per raccogliere informazioni sugli utenti finali. Consente di prendere decisioni informate basate sui dati per migliorare l’esperienza dell’utente finale.

- **Facile connessione di AEM Forms con Microsoft Dynamics e Salesforce**: Il servizio fornisce la configurazione e i modelli di dati preconfigurati dell’origine dati per Microsoft Dynamics e Salesforce, che lo rendono [più rapido e semplice per gli sviluppatori per configurare Microsoft Dynamics e Salesforce come origini dati per un modulo adattivo](configure-msdynamics-salesforce.md).

- **Firma elettronica di un modulo adattivo utilizzando DocuSign:** [È possibile utilizzare DocuSign per apporre la firma elettronica a un modulo adattivo](integrate-docusign-adaptive-forms.md). Il servizio fornisce un’azione di invio personalizzata per utilizzare DocuSign con un modulo adattivo.

### Funzioni beta di [!DNL Forms] {#sep-what-is-new-forms-prerelease}

- **Connettore di archiviazione unificata:** Utilizzare Unified Storage Connector per esternalizzare i dati in-process negli archivi gestiti dai clienti. Ad esempio, è possibile archiviare i dati dei flussi di lavoro AEM in elaborazione (AEM dati variabili di flusso di lavoro) contenenti dati personali sensibili (SPD) in un archivio gestito dal cliente.

   <!--* Enable Forms Portal’s save and resume functionality and store adaptive forms drafts in a customer-managed data repository.-->

- **[!DNL AEM Forms as a Cloud Service - Communications]**: [API di comunicazione](aem-forms-cloud-service-communications.md) consente di combinare modelli XDP e dati XML per generare documenti di stampa in vari formati. Il servizio consente di generare documenti in modalità sincrona. Le API consentono di creare applicazioni che permettono di:
   - Generare i documenti compilando i file modello con dati XML.
   - Generare moduli di output in vari formati, compresi flussi di stampa PDF non interattivi.
   - Generare file PDF di stampa da un modulo XFA PDF e Adobe Acrobat Form.

Puoi scrivere in [!DNL formscsbeta@adobe.com] per iscriversi al programma beta.

### Limitazioni  {#limitations}

- Adobe Analytics può tenere traccia delle metriche del modulo solo per gli utenti autenticati.

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

- Il progetto Archetype AEM per Forms as a Cloud Service ora include [modelli di dati per moduli per Microsoft Dynamics e Salesforce](setup-local-development-environment.md).

- **Documento di record basato su Acroform**: AEM Forms as a Cloud Service supporta l’utilizzo di [Adobe Acrobat Form PDF (Acroform PDF)](generate-document-of-record-for-non-xfa-based-adaptive-forms.md) come modello per il modello di modulo Document of Record oltre a basato su XFA.

- **Connettore dell’archivio dati di Microsoft Azure**: Ora puoi [collega il modello dati del modulo all’archiviazione di Microsoft Azure](configure-azure-storage.md). Consente di recuperare e archiviare dati adattivi del modulo in Microsoft Azure Storage as a BLOB.

### Funzione beta di [!DNL Forms] {#aug-what-is-new-forms-prerelease}

- **Connettore di archiviazione unificata:** Utilizzare Unified Storage Connector per esternalizzare i dati in-process negli archivi gestiti dai clienti. Ad esempio

   - Abilita la funzionalità di salvataggio e ripresa di Forms Portal e archivia le bozze dei moduli adattivi in un archivio dati gestito dal cliente.
   - Archiviare i dati dei flussi di lavoro AEM in-process (AEM dati variabili di flusso di lavoro) contenenti dati personali sensibili (SPD) in un archivio gestito dal cliente.

- **[!DNL AEM Forms as a Cloud Service - Communications]**: [API di comunicazione](aem-forms-cloud-service-communications.md) consente di combinare modelli XDP e dati XML per generare documenti di stampa in vari formati. Il servizio consente di generare documenti in modalità sincrona. Le API consentono di creare applicazioni che permettono di:
   - Generare i documenti compilando i file modello con dati XML.
   - Generare moduli di output in vari formati, compresi flussi di stampa PDF non interattivi.
   - Generare file PDF di stampa da un modulo XFA PDF e Adobe Acrobat Form.

Puoi scrivere in [!DNL formscsbeta@adobe.com] per iscriversi al programma beta.

### Nuove funzioni disponibili in [!DNL Forms] canale prerelease {#prerelease-features-forms-aug-2021}

- **Utilizzare i ruoli Adobe Sign in un modulo adattivo**: Adobe Sign per i livelli di servizio aziendali e aziendali ha la possibilità di espandere i ruoli per i destinatari del contratto, oltre al solo firmatario, in modo da soddisfare meglio i requisiti del flusso di lavoro. Ora puoi [abilitare ogni destinatario dell&#39;accordo a configurare il proprio ruolo in un modulo adattivo](working-with-adobe-sign.md#addsignerstoanadaptiveform), con il ruolo predefinito Firma .

- **Analytics per Forms adattivo**: È ora possibile acquisire e tenere traccia del comportamento dell’utente finale tramite Adobe Analytics for Adaptive Forms per raccogliere informazioni sull’utente finale. Consente di prendere decisioni informate basate sui dati per migliorare l’esperienza dell’utente finale.

- **Facile connessione di AEM Forms con Microsoft Dynamics e Salesforce**: Il servizio fornisce la configurazione e i modelli di dati preconfigurati dell’origine dati per Microsoft Dynamics e Salesforce, che lo rendono [più rapido e semplice per gli sviluppatori per configurare Microsoft Dynamics e Salesforce come origini dati per un modulo adattivo](configure-msdynamics-salesforce.md).

## 2021.7.0 {#july-2021-07-0}

### Novità in [!DNL Forms] {#july-what-is-new-forms}

- Ora puoi utilizzare il servizio Automated forms conversion per [convertire i PDF forms in francese, tedesco e spagnolo](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) ai moduli adattivi.
- È stato aggiunto un pannello separato all’editor modelli per visualizzare gli errori relativi ai componenti per moduli adattivi. Consente di consolidare tutti gli errori dei moduli adattivi in un&#39;unica posizione e di ridurre i tempi di risoluzione.

### Nuove funzioni disponibili in [!DNL Forms] canale prerelease {#july-prerelease-features-forms}

- **Documento di record basato su Acroform**: È inoltre possibile [utilizzare Adobe Acrobat Form PDF (Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) come modello per il modello di modulo Document of Record oltre a basato su XFA.

- **Connettore dell’archivio dati di Microsoft Azure**: Ora puoi [collega il modello dati del modulo all’archiviazione di Microsoft Azure](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html). Consente di recuperare e archiviare dati adattivi del modulo in Microsoft Azure Storage as a BLOB.

- **Esternalizzatore dati variabile**: È possibile salvare i dati delle variabili AEM flusso di lavoro su un sistema di storage esterno gestito dalla propria organizzazione.

### Funzione beta di [!DNL Forms] {#july-what-is-new-forms-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**: [API di comunicazione](aem-forms-cloud-service-communications.md) consente di combinare modelli XDP e dati XML per generare documenti di stampa in vari formati. Il servizio consente di generare documenti in modalità sincrona. Le API consentono di creare applicazioni che permettono di:
   - Generare i documenti compilando i file modello con dati XML.
   - Generare moduli di output in vari formati, compresi flussi di stampa PDF non interattivi.
   - Generare file PDF di stampa da un modulo XFA PDF e Adobe Acrobat Form.

## 2021.6.0 {#july-2021-06-0}

### Novità in [!DNL Forms] {#june-what-is-new-forms}

- È stata aggiunta la possibilità di filtrare colonne personalizzate nella casella in entrata AEM.
- È stata aggiunta la possibilità di utilizzare l’editor di temi e il livello di stile dell’editor di moduli adattivi per personalizzare lo stile del componente captcha.
- Velocità e precisione migliorate per rilevare automaticamente le sezioni logiche nei PDF forms sorgente e convertirle in corrispondenti pannelli di moduli adattivi.
- È stata aggiunta l’azione Sposta per spostare un file PDF o XDP da una cartella all’altra.

### Funzione beta di [!DNL Forms] {#june-what-is-new-forms-prerelease}

- **[!DNL AEM Forms as a Cloud Service - Communications]**: Le API di comunicazione consentono di combinare modelli XDP e dati XML per generare documenti di stampa in vari formati. Il servizio consente di generare documenti in modalità sincrona. Le API consentono di creare applicazioni che permettono di:

   - Generare documenti modulo finali compilando i file modello con dati XML.
   - Generare moduli di output in vari formati, compresi flussi di stampa PDF non interattivi.
   - Generare PDF di stampa da un modulo XFA PDF e Adobe Acrobat Form (AcroForm).

- **Esternalizzatore dati variabile**: È possibile salvare i dati delle variabili AEM flusso di lavoro su un sistema di storage esterno gestito dalla propria organizzazione.

Puoi scrivere in [!DNL formscsbeta@adobe.com] per iscriversi al programma beta.

### Bug fissati in [!DNL Forms] {#june-forms-bugs-fixed}

- Quando un campo viene convalidato prima dell’invio di dati al servizio back-end tramite Form Data Model (FDM), le convalide hanno esito positivo, ma il servizio Form Data Model non riesce ad avviare la convalida post-convalida.
- Quando si invia un modulo contenente un campo di caricamento HTML standard da un dispositivo Apple iOS, a volte il contenuto del file non viene inviato e viene ricevuto un file a 0 byte dall’altro lato. Apple iOS 15.1 fornisce una correzione al problema.

## 2021.5.0 {#may-2021-05-0}

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novità in [!DNL Forms] {#may-what-is-new-forms}

- **Aiuto contestuale**: È stata aggiunta l’aiuto contestuale per l’editor di moduli adattivi, l’editor di modelli e l’editor di temi, per aiutare gli autori a comprendere meglio le varie funzioni degli editor.
- **Messaggi di errore nel browser Proprietà**: Sono stati aggiunti messaggi di errore per ciascuna proprietà nel browser Proprietà adattive Forms. Questi messaggi consentono di comprendere i valori consentiti per un campo.

### Prossima funzionalità beta di [!DNL Forms] {#may-what-is-new-forms-prerelease}

Output as a Cloud Service: Il servizio di output consente di combinare i modelli XDP e i dati XML per generare documenti di stampa in vari formati. Il servizio consente di generare documenti in modalità batch sincrona e asincrona. Il servizio di output consente di creare applicazioni che consentono di:

- Generare documenti modulo finali compilando i file modello con dati XML.
- Generare moduli di output in vari formati, compresi flussi di stampa PDF non interattivi.
- Genera PDF di stampa da PDF modulo XFA.

Puoi scrivere su formscsbeta@adobe.com per iscriverti al programma beta.

### Bug fissati in [!DNL Forms] {#may-forms-bugs-fixed}

- In una fase Assegna attività dei flussi di lavoro AEM Forms, quando sostituisci l&#39;icona predefinita dei pulsanti di azione con un&#39;icona coral, il flusso di lavoro smette di funzionare e registra un&#39;eccezione. Il flusso di lavoro funziona come previsto quando si utilizzano le icone predefinite.
- Nel livello di layout, quando si modifica il numero di colonne, si apre il livello di modifica e si trascina alcuni componenti in un pannello, le caselle blu quadrate iniziano a comparire nell’area contenuto dell’editor di moduli adattivi e l’editor non risponde.
- Il messaggio di errore di un’opzione dell’editor di regole relativa alla fornitura dell’URL di una risorsa adattiva o esterna è troppo lungo e non è di facile utilizzo.

## 2021.4.0 {#april-2021-04-0}

### Novità in [!DNL Forms] {#april-what-is-new-forms}

- **Utilizzare il metodo di autenticazione dell&#39;identità ID governativo in Forms adattivo abilitato per Adobe Sign**

   Basato su algoritmi avanzati di apprendimento automatico, il processo ID governativo di Adobe Sign consente alle aziende di tutto il mondo di garantire un’autenticazione di alta qualità dell’identità del destinatario. Ora puoi utilizzare il metodo di autenticazione dell&#39;identità governativa in Forms adattivo abilitato per Adobe Sign.

   ID governativo è un metodo di autenticazione dell&#39;identità premium che istruisce il destinatario a [caricare l’immagine di un documento d’identità rilasciato dal governo (patente di guida, ID nazionale, passaporto)](https://helpx.adobe.com/in/sign/using/adobesign-authentication-government-id.html), quindi valuta il documento per assicurarne l&#39;autenticità.

- **Supporto per l’utilizzo dell’esperienza di firma nei moduli per l’invio asincrono di moduli adattivi**

   È ora possibile utilizzare l’esperienza di firma all’interno del modulo per gli invii asincroni di moduli adattivi. È inoltre possibile incorporare un modulo adattivo in un [!DNL Experience Manager Sites] e utilizzare l’esperienza di firma in-form per l’invio di moduli adattivi.

- **Supporto per l&#39;utilizzo di una variabile per specificare un allegato durante la precompilazione di un modulo adattivo per un passaggio Assegna attività**

   Durante la precompilazione di un modulo adattivo per un passaggio Assegna attività, è ora possibile utilizzare una variabile del tipo di documento per selezionare un allegato di input per il modulo adattivo.

- **Supporto per l’utilizzo dell’opzione letterale per impostare il valore per una variabile di tipo JSON**

   Puoi utilizzare l’opzione letterale per impostare il valore per una variabile di tipo JSON nel passaggio della variabile set di un flusso di lavoro AEM. L’opzione letterale ti consente di specificare un JSON sotto forma di stringa.

- **Utilizzare l&#39;ambiente di sviluppo locale per creare un documento di record (DoR)**

   Puoi utilizzare un XDP come modello Documento di record nelle istanze di Cloud Service e AEM Forms as a Cloud Service SDK (ambiente di sviluppo locale). In precedenza, il supporto era limitato solo alle istanze di Cloud Service.

### Correzioni di bug in [!DNL Forms] {#april-bug-fixes-forms}

- Quando un modulo adattivo configurato per non generare un documento di record viene inviato a un flusso di lavoro AEM configurato per generare un documento di record, non viene visualizzato alcun messaggio di errore e l’attività non viene inviata.
