---
title: Quali sono le differenze tra AEM 6.5 Forms e AEM Cloud Services?
description: Confronta AEM 6.5 Forms e AEM Cloud Services e scopri le modifiche più importanti prima di eseguire l’aggiornamento o la migrazione a Cloud Service.
badgeSaas: label="AEM Forms" type="Positive" tooltip="Si applica ad AEM Forms)."
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
role: Admin, Developer, User
feature: Adaptive Forms
contentOwner: khsingh
source-git-commit: 89b0f2a8ca9d2f60365a5c3962b0b4e826f79b3e
workflow-type: tm+mt
source-wordcount: '1331'
ht-degree: 2%

---

# Differenza tra AEM 6.5 Forms (AMS e on-Prem) e AEM Forms as a Cloud Services (AEM CS Forms) {#notable-changes-for-existing-AEM-Forms-users}

Adobe Experience Manager Forms as a Cloud Service apporta alcune modifiche di rilievo alle funzioni esistenti rispetto agli ambienti Adobe Experience Manager Forms On-Premise e [!DNL Adobe-Managed Service]. Le differenze principali sono elencate di seguito:

## Funzionalità native per cloud

* Il servizio dispone di un&#39;architettura nativa per il cloud che consente il ridimensionamento automatico in base al carico, l&#39;azzeramento dei tempi di inattività per gli aggiornamenti, la distribuzione frequente e successiva di nuove funzioni e aggiornamenti e topologie ottimizzate per la massima resilienza ed efficienza.

* Il servizio non include azioni di invio che memorizzano i dati nelle istanze di Adobe Experience Manager Cloud Service, rendendolo super sicuro. I dati acquisiti tramite i moduli vengono inviati direttamente agli archivi dati configurati.

* È inclusa anche una rete CDN (Content Delivery Network) gratuita per distribuire ed eseguire il rendering dei moduli a un ritmo più rapido.


## Aggiornamenti al flusso di sviluppo

* Il servizio fornisce un SDK per sviluppare e testare il codice personalizzato in un ambiente locale (computer locale) prima di distribuirlo in un Cloud Service. Gli sviluppatori sviluppano e testano componenti personalizzati, temi, applicazioni per flussi di lavoro, configurazioni, modelli e altro ancora utilizzando SDK sui propri computer locali. Dopo aver eseguito il test del codice personalizzato nel relativo ambiente di sviluppo locale, il codice personalizzato viene distribuito in un [ambiente di sviluppo o di staging di Forms CS](/help/implementing/cloud-manager/deploy-code.md) per ulteriori test prima di essere promosso a un ambiente di produzione.

* Gli sviluppatori gestiscono il codice per Cloud Service e l&#39;ambiente di sviluppo locale in un [archivio Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/cloud-manager-repositories.html?lang=it) comune. Un archivio Git, basato su Archetipo AEM, viene creato automaticamente al momento della creazione di un programma AEM as a Cloud Service.

  ![creazione automatica dell&#39;archivio Git nel programma AEM as a cloud service](/help/forms/assets/git-repo-local-and-forms-cs.png)

* Il flusso di sviluppo per Forms as a Cloud Service è allineato con l’archetipo di AEM per AEM Cloud Service. Tuttavia, sono necessarie alcune modifiche ai progetti Adobe Experience Manager Maven per renderli compatibili con AEM Cloud Service. Ad alto livello, AEM richiede una separazione di contenuto e codice in pacchetti secondari discreti per rispettare la suddivisione tra contenuti mutabili e immutabili. Utilizzare lo strumento [Repository Modernizer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html?lang=it) per ristrutturare i pacchetti di progetto esistenti separando il contenuto e il codice in pacchetti distinti in modo che siano compatibili con la struttura di progetto definita per Adobe Experience Manager as a Cloud Service.

* Prima di utilizzare i bundle per i clienti con Forms as a Cloud Service, ricompila il codice personalizzato con l’ultima versione di adobe-aemfd-docmanager.

* Utilizza l&#39;[utilità di migrazione di AEM Forms as a Cloud Service](/help/forms/migrate-to-forms-as-a-cloud-service.md) per preparare ed eseguire la migrazione di Forms adattivo, temi, modelli e configurazioni cloud da <!-- AEM 6.3 Forms--> AEM 6.4 Forms su OSGi e AEM 6.5 Forms su OSGi a [!DNL AEM] as a Cloud Service. Utilizza l&#39;archivio [Git del programma](/help/implementing/cloud-manager/managing-code/managing-repositories.md) per importare modelli di moduli adattivi esistenti.

* Per impostazione predefinita, le e-mail supportano solo i protocolli HTTP e HTTP. [Contatta il team di supporto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=it#sending-email) per abilitare le porte per l&#39;invio di e-mail e l&#39;abilitazione del protocollo SMTP per l&#39;ambiente.

## Localizzazione

* La convenzione URL di Forms adattivo localizzato ora supporta la specifica di una lingua nell’URL. La nuova convenzione URL consente di memorizzare nella cache i moduli localizzati su una rete Dispatcher o CDN. In un ambiente Cloud Service, utilizza il formato URL `http://host:port/content/forms/af/<afName>.<locale>.html` per richiedere una versione localizzata di un modulo adattivo invece di `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`.

* Adobe consiglia di utilizzare la memorizzare nella cache di Dispatcher o della rete CDN. Consente di migliorare la velocità di rendering dei moduli precompilati.


## Moduli adattivi

* **Editor regole:** AEM Forms as a Cloud Service fornisce un [Editor regole](rule-editor.md#visual-rule-editor) indurito. L’editor di codice non è disponibile in Forms as a Cloud Service.

  L&#39;utilità di [migrazione](/help/forms/migrate-to-forms-as-a-cloud-service.md) consente di migrare i moduli con regole personalizzate (creati nell&#39;editor di codice). L’utility converte tali regole in funzioni personalizzate supportate in Forms as a Cloud Service. È possibile utilizzare le funzioni riutilizzabili con l’editor di regole per continuare a ottenere i risultati ottenuti con gli script di regole. Le funzioni `onSubmitError` o `onSubmitSuccess` sono ora disponibili come azioni nell&#39;editor di regole.

<!--* **Prefill Service:** By default, the prefill service merges data with an Adaptive Form at client as opposed to merging data on Server in AEM 6.5 Forms. The feature helps improve the time required to prefill an Adaptive Form. You can always configure to run the merge action on the Adobe Experience Manager Forms Server.-->

* **Servizio di precompilazione:** il servizio di precompilazione recupera i dati dal server e li unisce per precompilare il Forms adattivo sul lato client. Questa funzione consente di migliorare il tempo necessario per compilare un modulo adattivo. È sempre possibile configurare il [servizio di precompilazione](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/adaptive-forms/prefill-service-adaptive-forms-article-use.html?lang=it) per eseguire l&#39;azione di unione sul server Adobe Experience Manager Forms.

* **Azioni di invio:** L&#39;azione di invio **E-mail** fornisce opzioni per l&#39;invio di allegati e l&#39;allegato del documento record (DoR) con l&#39;e-mail. Puoi utilizzarlo al posto dell&#39;azione **Invia e-mail come PDF** disponibile in AEM 6.5 Forms.

* **Servizio di conversione moduli automatica**: il servizio non fornisce un metamodello per il servizio di conversione moduli automatica. Puoi [scaricarlo dalla documentazione del Servizio di conversione automatica dei moduli](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=it#default-meta-model).

* **Forms adattivo basato su XSD:** È possibile utilizzare il modello XDP per progettare un modello per il documento per il record. Il servizio non supporta Forms adattivo basato su XFA

* **Componenti**: il servizio non supporta l&#39;esperienza di firma interna ai moduli e non include i componenti Riepilogo e Verifica per il modulo adattivo.

* **Interfaccia della procedura guidata:** È possibile utilizzare l&#39;interfaccia [della procedura guidata](/help/forms/creating-adaptive-form-core-components.md) per configurare rapidamente le opzioni comuni e creare facilmente un modulo adattivo.

## Portale dei moduli

* Il servizio non mantiene i metadati per le bozze e i Forms adattivi inviati.

## Servizi documentali:

Forms as a Cloud Service fornisce API RESTful per la generazione e la manipolazione di documenti. Puoi utilizzare queste API per generare o modificare i documenti su richiesta o in batch, a seconda delle necessità:

* **Servizi basati su documenti: API per la generazione di documenti (servizio di output)**: in una singola chiamata o batch API è possibile utilizzare un solo modello con più file XML DATI. L’utilizzo di più modelli con più file di dati in una singola chiamata API non è supportato.

* **API per la manipolazione dei documenti (servizio Assembler)**:

   * Le operazioni che si basano su applicazioni o servizi basati su documenti non sono disponibili. Ad esempio, Microsoft® da Word a PDF, Microsoft® da Excel a PDF e da HTML a PDF, PostScript (PS) a PDF, XDP a PDF forms non sono supportati. Queste operazioni si basano rispettivamente su Microsoft® Office, Adobe Acrobat, Adobe Distiller e Forms Document Service.

   * Converti i documenti in formato non PDF in un formato PDF prima di utilizzare quelli con le API Communications Document Manipulation. Ad esempio, se i documenti sono in formato Microsoft® Office, HTML, PostScript (PS), XDP, convertire tali documenti in formato PDF prima di utilizzarli con i documenti PDF. È possibile utilizzare il servizio [ConvertPDF](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/using-convertpdf-service.html?lang=it) per tali conversioni.

   * È possibile utilizzare un ambiente AEM 6.5 Forms per la firma digitale, la crittografia, l&#39;estensione Reader, l&#39;invio alla stampante, la conversione di PDF e il servizio Forms con codice a barre.


## Integrazione dei dati (modello dati modulo)

* Il servizio fornisce inoltre supporto per il connettore JDBC, Microsoft® Dynamics, Salesforce, servizi Web basati su SOAP e servizi che supportano OData.

* Puoi anche collegare il profilo utente di AEM per recuperare e aggiornare le informazioni utente.

* Il modello dati di Forms supporta solo endpoint HTTP e HTTPS per inviare dati. Il servizio non supporta SSL reciproco per il connettore REST e l’autenticazione basata su certificato x509 per le origini dati SOAP.

* Forms as a Cloud Service consente di utilizzare Microsoft® Azure Blob, Microsoft® Sharepoint, Microsoft® OneDrive e i servizi che supportano operazioni CRUD (Create, Read, Update, Delete) generali come archivi di dati; sono supportate sia le specifiche Open API 2.0 che Open API 3.0.


## E-Sign

* Il servizio fornisce un’integrazione OOTB con Adobe Sign e supporta DocuSign per le firme elettroniche.

* Il servizio supporta anche i ruoli Adobe Sign. Puoi configurare i ruoli nell’editor di Forms adattivo per gli utenti aziendali per configurare facilmente i flussi di lavoro di firma.


## Moduli HTML5

* È possibile utilizzare un ambiente Forms di AEM 6.5 per:

   * esegui il rendering dei moduli basati su XDP come HTML5 Forms. Il servizio non supporta HTML5 Forms.

   * acquisisci i dati offline e sincronizzali alla prossima connessione con l&#39;app [AEM Forms Workspace](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-aem-forms-workspace/introduction-html-workspace.html?lang=it).

## Comunicazioni interattive

* Puoi utilizzare le API di comunicazione per produrre documenti personalizzati on-demand o in batch su Forms as a Cloud Service. Puoi utilizzare un ambiente Forms AEM 6.5 per comunicazioni interattive e casi d’uso dell’interfaccia utente degli agenti.

## Consulta anche

* [Migrazione da un ambiente AEM Forms (locale e AMS) ad AEM Forms as a Cloud Service](/help/forms/migrate-to-forms-as-a-cloud-service.md)
* [Pagina Aggiungi o crea un Forms adattivo ad AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Creare un modulo adattivo (componenti core)](/help/forms/creating-adaptive-form-core-components.md)
* [Introduzione ad AEM Forms as a Cloud Service](/help/forms/home.md)
* [Configurare un ambiente di sviluppo locale e un progetto di sviluppo iniziale](/help/forms/setup-local-development-environment.md)


<!--

## Additional Information

* [Introduction to AEM Forms as a Cloud Service](/help/forms/home.md)
* [Set up a local development environment and initial development project](/help/forms/setup-local-development-environment.md)

-->
