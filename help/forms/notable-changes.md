---
title: Differenze tra AEM 6.5 Forms e AEM Cloud Services
description: Sei un utente di Experience Manager Forms e stai cercando di effettuare l’aggiornamento ad Adobe Experience Manager Forms as a Cloud Service? Confronta Forms AEM 6.5 e AEM Cloud Services e scopri le modifiche più importanti prima di eseguire l’aggiornamento o la migrazione al Cloud Service.
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
contentOwner: khsingh
source-git-commit: 1d16797f741fc9032356564061f2b6743d4c7936
workflow-type: tm+mt
source-wordcount: '1405'
ht-degree: 1%

---

# Modifiche di rilievo per gli utenti esistenti di Adobe Experience Manager 6.5 Forms  {#notable-changes-for-existing-AEM-Forms-users}

Adobe Experience Manager Forms as a Cloud Service apporta alcune modifiche di rilievo alle funzioni esistenti rispetto ad Adobe Experience Manager Forms On-Premise e [!DNL Adobe-Managed Service] ambienti. Le differenze principali sono elencate di seguito:

## Funzionalità native per cloud

* Il servizio dispone di un&#39;architettura nativa per il cloud che consente il ridimensionamento automatico in base al carico, l&#39;azzeramento dei tempi di inattività per gli aggiornamenti, la distribuzione frequente e successiva di nuove funzioni e aggiornamenti e topologie ottimizzate per la massima resilienza ed efficienza.

* Il servizio non include azioni di invio che memorizzano i dati nelle istanze del Cloud Service Adobe Experience Manager, rendendolo super sicuro. I dati acquisiti tramite i moduli vengono inviati direttamente agli archivi dati configurati.

* È inclusa anche una rete CDN (Content Delivery Network) gratuita per distribuire ed eseguire il rendering dei moduli a un ritmo più rapido.


## Aggiornamenti al flusso di sviluppo

* Il servizio fornisce un SDK per sviluppare e testare il codice personalizzato in un ambiente locale (computer locale) prima di distribuirlo a un Cloud Service. Gli sviluppatori sviluppano e testano componenti personalizzati, temi, applicazioni per flussi di lavoro, configurazioni, modelli e altro ancora utilizzando l’SDK sui loro computer locali. Dopo aver eseguito il test del codice personalizzato nel proprio ambiente di sviluppo locale, distribuisce il codice personalizzato in una [Ambiente di sviluppo Forms CS o ambiente stage](/help/implementing/cloud-manager/deploy-code.md) per ulteriori test prima di promuoverlo in un ambiente di produzione.

* Gli sviluppatori gestiscono in comune il codice per l’ambiente di sviluppo Cloud Service e locale [archivio Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/cloud-manager-repositories.html). Un archivio Git, basato su Archetipo AEM, viene creato automaticamente al momento della creazione di un programma as a Cloud Service AEM.

  ![](/help/forms/assets/git-repo-local-and-forms-cs.png)

* Il flusso di sviluppo per Forms as a Cloud Service è allineato con l’archetipo AEM per AEM Cloud Service. Tuttavia, sono necessarie alcune modifiche ai progetti Adobe Experience Manager Maven per renderli compatibili con AEM Cloud Service. Ad alto livello, l&#39;AEM richiede una separazione del contenuto e del codice in subpacchetti distinti per rispettare la ripartizione tra contenuto mutabile e immutabile. Utilizza il [Strumento Repository Modernizer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) per ristrutturare i pacchetti di progetto esistenti separando il contenuto e il codice in pacchetti distinti in modo che siano compatibili con la struttura di progetto definita per Adobe Experience Manager as a Cloud Service.

* Prima di utilizzare i bundle per i clienti con Forms as a Cloud Service, ricompila il codice personalizzato con l’ultima versione di adobe-aemfd-docmanager.

* Utilizzare [Utility di migrazione AEM Forms as a Cloud Service](/help/forms/migrate-to-forms-as-a-cloud-service.md) per preparare ed eseguire la migrazione di Forms adattivo, temi, modelli e configurazioni cloud da <!-- AEM 6.3 Forms--> AEM 6.4 Forms su OSGi e AEM 6.5 Forms su OSGi a [!DNL AEM] as a Cloud Service. Utilizzare [Archivio Git del programma](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) per importare modelli di moduli adattivi esistenti.

* Per impostazione predefinita, le e-mail supportano solo i protocolli HTTP e HTTP. [Contatta il team di supporto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) per abilitare le porte per l’invio di e-mail e il protocollo SMTP per il tuo ambiente.

## Localizzazione

* La convenzione URL di Forms adattivo localizzato ora supporta la specifica di una lingua nell’URL. La nuova convenzione URL consente di memorizzare nella cache i moduli localizzati su una rete CDN o Dispatcher. In un ambiente di Cloud Service, utilizza il formato URL `http://host:port/content/forms/af/<afName>.<locale>.html` per richiedere una versione localizzata di un modulo adattivo anziché `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`.

* L’Adobe consiglia di utilizzare il caching di Dispatcher o CDN. Consente di migliorare la velocità di rendering dei moduli precompilati.


## Moduli adattivi

* **Editor regole:** AEM Forms as a Cloud Service offre una [Editor regole](rule-editor.md#visual-rule-editor). L’editor di codice non è disponibile su Forms as a Cloud Service.

  Il [utilità di migrazione](/help/forms/migrate-to-forms-as-a-cloud-service.md) consente di migrare i moduli con regole personalizzate (create nell’editor di codice). L’utility converte tali regole in funzioni personalizzate supportate su Forms as a Cloud Service. È possibile utilizzare le funzioni riutilizzabili con l’editor di regole per continuare a ottenere i risultati ottenuti con gli script di regole. Il `onSubmitError` o `onSubmitSuccess` Le funzioni sono ora disponibili come azioni nell’Editor regole.

* **Servizio preriempimento:** Per impostazione predefinita, il servizio di precompilazione unisce i dati con un modulo adattivo sul client, invece di unire i dati sul server in Forms con AEM 6.5. Questa funzione consente di migliorare il tempo necessario per la precompilazione di un modulo adattivo. Puoi sempre configurare per eseguire l’azione di unione sul server Adobe Experience Manager Forms.

* **Inviare azioni:** Il **E-mail** azione di invio fornisce opzioni per l’invio di allegati e allega un documento Record (DoR) all’e-mail. Puoi utilizzarlo al posto del **Invia e-mail come PDF** disponibile nel Forms AEM 6.5.

* **Servizio automated forms conversion**: il servizio non fornisce un metamodello per il servizio di Automated forms conversion. È possibile [scarica dalla documentazione di Automated forms conversion Service](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).

* **Forms adattivo basato su XSD:** È possibile utilizzare il modello XDP per progettare un modello per Document for Record. Il servizio non supporta Forms adattivo basato su XFA

* **Componenti**: puoi utilizzare [Componenti core Forms adattivi](/help/forms/creating-adaptive-form-core-components.md) per progettare i moduli. Questi componenti sono basati sui componenti core WCM, seguono gli standard BEM e possono essere facilmente personalizzati. Il servizio non supporta l’esperienza di firma interna ai moduli e non include i componenti Riepilogo e Verifica per il modulo adattivo

## Portale Forms

* È possibile utilizzare i componenti Ricerca e elenco, Bozze e invio e Collegamento di Forms Portal per elencare i moduli per gli utenti connessi. Il supporto per l’utilizzo anonimo di Forms Portal non è disponibile come funzionalità integrata (OOTB). È possibile personalizzare Forms Portal per abilitare la visualizzazione dei moduli per gli utenti non connessi.

* Il servizio non mantiene i metadati per le bozze e i Forms adattivi inviati.

## Document Services:

Forms as a Cloud Service fornisce API RESTful per generazione e manipolazione di documenti. Puoi utilizzare queste API per generare o modificare i documenti su richiesta o in batch, a seconda delle necessità:

* **Document Services: API per la generazione di documenti (servizio di output)**: in una singola chiamata API o in un batch, è possibile utilizzare un solo modello con più file XML DATI. L’utilizzo di più modelli con più file di dati in una singola chiamata API non è supportato.

* **API per la manipolazione dei documenti (servizio Assembler)**:

   * Le operazioni che si basano su applicazioni o servizi basati su documenti non sono disponibili. Ad esempio, Microsoft Word per PDF, Microsoft Excel per PDF e HTML per PDF, PostScript (PS) per PDF, XDP per PDF forms non sono supportati. Queste operazioni si basano rispettivamente su Microsoft Office, Adobe Acrobat, Adobe Distiller e Forms Document Service.

   * Converti i documenti in formato non PDF in formato PDF prima di utilizzarli con le API Communications Document Manipulation. Se ad esempio i documenti sono in formato Microsoft Office, HTML, PostScript (PS) o XDP, convertire i documenti in formato PDF prima di utilizzarli con i documenti PDF. È possibile utilizzare [ConvertPDF](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/using-convertpdf-service.html) servizio per tali conversioni.

* È possibile utilizzare un ambiente Forms AEM 6.5 per la firma digitale, la crittografia, l&#39;estensione del Reader, l&#39;invio alla stampante, Convert PDF e il servizio Forms con codice a barre.


## Integrazione dei dati (modello dati modulo)

* Il servizio fornisce inoltre supporto per il connettore JDBC, Microsoft Dynamics, SalesForce, servizi Web basati su SOAP e servizi che supportano OData.

* Puoi anche collegare il profilo utente AEM per recuperare e aggiornare le informazioni utente.

* Il modello dati di Forms supporta solo endpoint HTTP e HTTPS per inviare dati. Il servizio non supporta SSL reciproco per il connettore REST e l&#39;autenticazione basata su certificato x509 per le origini dati SOAP.

* Forms as a Cloud Service consente di utilizzare Microsoft Azure Blob, Microsoft Sharepoint, Microsoft OneDrive e i servizi che supportano le operazioni CRUD (Create, Read, Update, Delete) generali come archivi di dati. Sono supportate sia le specifiche API 2.0 che le specifiche API 3.0 aperte.


## E-Sign

* Il servizio fornisce un’integrazione OOTB con Adobe Sign e supporta DocuSign per le firme elettroniche.

* Il servizio supporta anche i ruoli di Adobe Sign. Puoi configurare i ruoli nell’editor di Forms adattivo per gli utenti aziendali per configurare facilmente i flussi di lavoro di firma.


## Moduli HTML5

* È possibile utilizzare un ambiente Forms AEM 6.5 per:

   * esegui il rendering dei moduli basati su XDP come HTML5 Forms. Il servizio non supporta HTML5 Forms (Mobile Forms).

   * acquisire i dati offline e sincronizzarli alla successiva connessione in linea con [AEM Forms Workspace](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-aem-forms-workspace/introduction-html-workspace.html) app.

## Comunicazioni interattive

* Puoi utilizzare le API di comunicazione per produrre documenti personalizzati on-demand o in batch su Forms as a Cloud Service. Puoi utilizzare un ambiente Forms AEM 6.5 per comunicazioni interattive e casi d’uso dell’interfaccia utente degli agenti.

## Vedere Successivo

* [Migrazione da un ambiente AEM Forms (on-premise e ambienti AMS) ad AEM Forms as a Cloud Service](/help/forms/migrate-to-forms-as-a-cloud-service.md)
* [Pagina Aggiungi o crea un Forms adattivo ad AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Creare un modulo adattivo (componenti core)](/help/forms/creating-adaptive-form-core-components.md)

## Informazioni aggiuntive

* [Introduzione ad AEM Forms as a Cloud Service](/help/forms/home.md)
* [Configurare un ambiente di sviluppo locale e un progetto di sviluppo iniziale](/help/forms/setup-local-development-environment.md)
