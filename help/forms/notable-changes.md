---
title: Differenze tra AEM 6.5 Forms e AEM Cloud Services
description: Sei un utente di Experience Manager Forms e vuoi effettuare l’aggiornamento ad Adobe Experience Manager Forms as a Cloud Service? Confronta AEM 6.5 Forms e AEM Cloud Services e scopri le modifiche più importanti prima di eseguire l’aggiornamento o la migrazione al Cloud Service.
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
contentOwner: khsingh
source-git-commit: 54a1ae1cc030030e44612b502b70c9b567144538
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Modifiche di rilievo per gli utenti Forms esistenti di Adobe Experience Manager 6.5  {#notable-changes-for-existing-AEM-Forms-users}

Adobe Experience Manager Forms as a Cloud Service apporta alcune modifiche di rilievo alle funzioni esistenti rispetto ad Adobe Experience Manager Forms On-Premise e [!DNL Adobe-Managed Service] ambienti. Le differenze chiave sono elencate di seguito:

## Funzionalità native per cloud

* Il servizio dispone di un&#39;architettura nativa per il cloud che consente il ridimensionamento automatico in base al carico, tempi di inattività zero per gli aggiornamenti, frequenti e dopo l&#39;implementazione di nuove funzioni e aggiornamenti e topologie ottimizzate per la massima resilienza ed efficienza.

* Il servizio non include azioni di invio che memorizzano i dati nelle istanze di Adobe Experience Manager Cloud Service, rendendoli super sicuri. I dati acquisiti tramite moduli vengono inviati direttamente agli archivi dati configurati.

* È inoltre inclusa una rete CDN (content delivery network) gratuita per distribuire ed eseguire il rendering dei moduli a un ritmo più veloce.


## Aggiornamenti al flusso di sviluppo

* Il servizio fornisce un SDK per sviluppare e testare il codice personalizzato in un ambiente locale (computer locale) prima di distribuire il codice a un Cloud Service. Gli sviluppatori sviluppano e testano componenti personalizzati, temi, applicazioni di flussi di lavoro, configurazioni, modelli e altro ancora utilizzando l’SDK sui propri computer locali. Dopo aver testato il codice personalizzato nel loro ambiente di sviluppo locale, distribuiscono il codice personalizzato in un [Ambiente Forms CS o ambiente stage](/help/implementing/cloud-manager/deploy-code.md) per ulteriori test prima di promuoverlo in un ambiente di produzione.

* Gli sviluppatori mantengono il codice per l’ambiente di sviluppo Cloud Service e locale in una comune [archivio git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/cloud-manager-repositories.html). Un archivio Git, basato su AEM Archetype, viene creato automaticamente alla creazione di un programma as a Cloud Service AEM.

   ![](/help/forms/assets/git-repo-local-and-forms-cs.png)

* Il flusso di sviluppo per Forms as a Cloud Service è allineato con AEM Archetype per AEM Cloud Service. Tuttavia, sono necessarie alcune modifiche per rendere i progetti Adobe Experience Manager Maven compatibili con AEM Cloud Service. Ad alto livello, AEM richiede una separazione di contenuto e codice in pacchetti secondari distinti per rispettare la suddivisione tra contenuto mutabile e immutabile. Utilizza la [Strumento Repository Modernizer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) per ristrutturare i pacchetti di progetto esistenti separando il contenuto e il codice in pacchetti discreti in modo che siano compatibili con la struttura di progetto definita per Adobe Experience Manager as a Cloud Service.

* Prima di utilizzare i bundle dei clienti con Forms as a Cloud Service, ricompila il codice personalizzato con l&#39;ultima versione di adobe-aemfd-docmanager.

* Utilizzo [Utility di migrazione as a Cloud Service di AEM Forms](/help/forms/migrate-to-forms-as-a-cloud-service.md) per preparare e migrare le configurazioni adattive di Forms, temi, modelli e cloud da <!-- AEM 6.3 Forms--> AEM 6.4 Forms su OSGi e AEM Forms 6.5 su OSGi a [!DNL AEM] as a Cloud Service. Utilizzo [Archivio Git del programma](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) per importare i modelli di moduli adattivi esistenti.

* Per impostazione predefinita, l’e-mail supporta solo i protocolli HTTP e HTTP. [Contatta il team di supporto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) per abilitare le porte per l’invio di e-mail e per abilitare il protocollo SMTP per l’ambiente.

## Localizzazione

* La convenzione URL di Forms adattivo localizzato ora supporta la specifica di impostazioni internazionali nell’URL. La nuova convenzione URL consente di memorizzare nella cache i moduli localizzati su un’istanza di Dispatcher o CDN. In un ambiente di Cloud Service, utilizza il formato URL `http://host:port/content/forms/af/<afName>.<locale>.html` per richiedere una versione localizzata di un modulo adattivo anziché `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`.

* Adobe consiglia di utilizzare Dispatcher o la memorizzazione in cache CDN. Consente di migliorare la velocità di rendering dei moduli precompilati.


## Moduli adattivi

* **Editor di regole:** AEM Forms as a Cloud Service fornisce un [Editor di regole](rule-editor.md#visual-rule-editor). L&#39;editor di codice non è disponibile su Forms as a Cloud Service.

   La [utility di migrazione](/help/forms/migrate-to-forms-as-a-cloud-service.md) consente di migrare i moduli con regole personalizzate (create nell’editor di codice). L&#39;utility converte tali regole in funzioni personalizzate supportate su Forms as a Cloud Service. È possibile utilizzare le funzioni riutilizzabili con l&#39;editor di regole per continuare a ottenere i risultati ottenuti con gli script di regole. La `onSubmitError` o `onSubmitSuccess` Le funzioni sono ora disponibili come azioni nell’editor di regole.

* **Servizio di precompilazione:** Per impostazione predefinita, il servizio di precompilazione unisce i dati con un modulo adattivo sul client anziché con l’unione dei dati sul server in Forms 6.5 AEM. Questa funzione consente di migliorare il tempo necessario per precompilare un modulo adattivo. È sempre possibile configurare l&#39;esecuzione dell&#39;azione di unione sul server Adobe Experience Manager Forms.

* **Azioni di invio:** La **E-mail** l’azione di invio fornisce opzioni per l’invio di allegati e allega documento di record (DoR) con e-mail. Puoi utilizzarla al posto del **Invia e-mail come PDF** disponibile in Forms 6.5 AEM.

* **Servizio automated forms conversion**: Il servizio non fornisce un metamodello per il servizio di Automated forms conversion. È possibile [scaricarlo dalla documentazione di Automated forms conversion Service](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).

* **Forms adattivo basato su XSD:** È possibile utilizzare XDP-template per progettare un template per Document for Record. Il servizio non supporta Forms adattivo basato su XFA

* **Componenti**: È possibile utilizzare [Componenti core Forms adattabili](/help/forms/creating-adaptive-form-core-components.md) per progettare i moduli. Questi componenti sono basati su componenti core WCM, seguono gli standard BEM e possono essere facilmente personalizzati. Il servizio non supporta l’esperienza di firma in-form e non include i componenti Riepilogo e Verifica per il modulo adattivo

## Portale Forms

* Puoi utilizzare i componenti Ricerca e filtro, Bozze e Invio e Collegamento di Forms Portal per elencare i moduli per gli utenti registrati. Il supporto per l’uso anonimo di Forms Portal non è disponibile come standard (OOTB). Puoi personalizzare il portale Forms per abilitare la visualizzazione dei moduli per gli utenti non connessi.

* Il servizio non conserva i metadati per le bozze e invia Adaptive Forms.

## Document Services:

Forms as a Cloud Service fornisce API RESTful per generazione di documenti e manipolazione documenti. Puoi utilizzare queste API per generare o manipolare documenti su richiesta o in batch, a seconda delle necessità:

* **Servizi documenti: API per la generazione di documenti (servizio di output)**: In una singola chiamata API o batch, puoi utilizzare un solo modello con più file XML DATI. L’utilizzo di più modelli con più file di dati in una singola chiamata API non è supportato.

* **API di manipolazione documenti (servizio Assembler)**:

   * Le operazioni basate su document services o applicazioni non sono disponibili. Ad esempio, Microsoft Word in PDF, Microsoft Excel in PDF e HTML in PDF, PostScript (PS) in PDF e XDP in PDF forms non sono supportati. Queste operazioni si basano rispettivamente su Microsoft Office, Adobe Acrobat, Adobe Distiller e Forms Document Service.

   * Convertire i documenti in formato non PDF in un formato PDF prima di utilizzare quelli con le API di manipolazione dei documenti di comunicazione. Ad esempio, se i documenti sono in formato Microsoft Office, HTML, PostScript (PS) e XDP, convertire questi documenti in formato PDF prima di utilizzarli con i documenti PDF. È possibile utilizzare [ConvertPDF](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/using-convertpdf-service.html) servizio per tali conversioni.

* È possibile utilizzare un ambiente Forms AEM 6.5 per la firma digitale, la crittografia, l’estensione del Reader, l’invio alla stampante, il servizio Convert PDF e il servizio Forms con codice a barre.


## Integrazione dei dati (modello dati modulo)

* Il servizio fornisce inoltre il supporto per il connettore JDBC, Microsoft Dynamics, SalesForce, servizi web basati su SOAP e servizi che supportano OData.

* È inoltre possibile connettersi AEM profilo utente per recuperare e aggiornare le informazioni utente.

* Il modello dati Forms supporta solo endpoint HTTP e HTTPS per l’invio dei dati. Il servizio non supporta SSL reciproco per il connettore REST e l’autenticazione basata su certificato x509 per le origini dati SOAP.

* Forms as a Cloud Service consente di utilizzare Microsoft Azure Blob, Microsoft Sharepoint, Microsoft OneDrive e i servizi che supportano le operazioni generali CRUD (creazione, lettura, aggiornamento ed eliminazione) come archivi di dati, sono supportate sia la specifica API aperta 2.0 che la specifica API aperta 3.0.


## E-Sign

* Il servizio fornisce un’integrazione OOTB con Adobe Sign e supporta DocuSign per le firme elettroniche.

* Il servizio supporta anche i ruoli di Adobe Sign. È possibile configurare i ruoli nell’editor di Forms adattivo per gli utenti aziendali in modo da configurare facilmente i flussi di lavoro di firma.


## Moduli HTML5

* È possibile utilizzare un ambiente Forms AEM 6.5 per:

   * esegui il rendering dei moduli basati su XDP come HTML5 Forms. Il servizio non supporta HTML5 Forms (Mobile Forms).

   * acquisisci i dati offline e sincronizzali la prossima volta che ritorni online con [AEM Forms Workspace](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-aem-forms-workspace/introduction-html-workspace.html) app.

## Comunicazioni interattive

* Puoi utilizzare le API di comunicazione per produrre documenti personalizzati on-demand o in batch su Forms as a Cloud Service. È possibile utilizzare un ambiente Forms AEM 6.5 per i casi d’uso delle comunicazioni interattive e dell’interfaccia utente dell’agente.


