---
title: Migrazione ad Experience Manager come Cloud Service
description: Migrazione ad Experience Manager come Cloud Service
exl-id: 4d1addcf-b22d-41a3-ba5c-e5c42244e5cd
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '2115'
ht-degree: 10%

---

# Migrazione ad Adobe Experience Manager as a Cloud Service {#Overview}

>[!CONTEXTUALHELP]
>id="aemcloud_migration_overview"
>title="Migrazione a AEM as a cloud Service"
>abstract="Illustra l’approccio graduale consigliato per la transizione dei clienti da varie implementazioni di Experience Manager ad Experience Manager come Cloud Service e aiuta i clienti esistenti a fornire esperienze continue e connesse"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en" text="Novità e differenze"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en" text="Introduzione ad AEM as a Cloud Service."

Adobe Experience Manager (AEM) as a Cloud Service offre una base ri-architettata per Experience Manager, basata su un’infrastruttura basata su contenitori, uno sviluppo basato su API e un processo guidato DevOps, che consente agli esperti di marketing e agli sviluppatori di mantenere sempre il passo con le innovazioni di gestione dell’esperienza dei clienti.

Il Cloud Service unisce funzionalità avanzate ed estensibilità di Adobe Experience Manager all’architettura nativa per il cloud moderna, consentendo ai brand di soddisfare la domanda dei consumatori in continua evoluzione.

Questo unico pager delinea l’approccio graduale consigliato per la transizione dei clienti da varie implementazioni di Experience Manager ad Experience Manager come Cloud Service e aiuta i clienti esistenti a fornire esperienze continue e connesse su questa piattaforma moderna e appositamente progettata per la gestione delle esperienze.

<!-- It primarily focuses on:
* Getting Started with Adobe Experience Manager as a Cloud Service
* Developer Journey in Adobe Experience Manager as a Cloud Service
* Moving to Adobe Experience Manager as a Cloud Service -->

<br>

## Guida introduttiva ad Adobe Experience Manager as a Cloud Service {#getting-started}

| Che cosa è diverso? | Panoramica dell’architettura |
|--------------------------|--------------------------|
| <ul><li>[Architettura moderna](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html)</li><li>[Aggiornamenti automatici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/aem-version-updates.html?lang=en#aem-version-updates)</li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=it)</li><li>[Microservizi per le risorse](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/asset-microservices-overview.html)</li><li>[Binari ad accesso diretto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/asset-microservices-overview.html?lang=en#asset-upload-with-direct-binary-access)</li><li>[Separazione del codice e del contenuto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=en#developing)</li><li>[Replica as a Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/replication.html?lang=it)</li><li>[Admin Console, Group/User Membership e ACL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html)</li></ul> | <ul><li>[Introduzione all’architettura AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-architecture.html?lang=en#underlying-technology)</li><li>[Stack ambiente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html)</li><li>[Livello di authoring](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[Livello di pubblicazione](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#content-delivery)</li><li>[CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/cdn.html?lang=en#content-delivery) </li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)  (CI/CD)</li><li>[Gestione delle identità ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#onboarding-users-in-admin-console) tramite  [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html)</li><li>[Servizio Asset compute](https://experienceleague.adobe.com/docs/asset-compute/using/home.html)</li></ul> |

![AEM as a Cloud Service: architettura runtime](/help/core-concepts/assets/concepts-03.png "AEM as a Cloud Service - Architettura runtime")

<br>

## Percorso per sviluppatori in Adobe Experience Manager as a Cloud Service {#developer-journey}

### Sviluppo

Le basi dello sviluppo del codice sono simili in Adobe Experience Manager as a Cloud Service rispetto alle soluzioni Adobe Experience Manager On Premise e Managed Services .

Gli sviluppatori scrivono il codice e lo testano localmente, che viene quindi inviato a Adobe Experience Manager remoto come ambiente di Cloud Service.

Consulta le risorse di supporto autonomo sull’implementazione, ad Experience Manager come Cloud Service, per scoprire come personalizzare il tuo Experience Manager come implementazione di Cloud Service.

| Configurazione dello sviluppo locale | Cose da sapere prima di iniziare |
|-----------|------------|
| <ol><li>Per ulteriori informazioni, consulta la documentazione [SDK per Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing) .</li><li>Guarda [Installare Dispatcher SDK](https://video.tv.adobe.com/v/30601) per informazioni su come installare Dispatcher SDK</li><li>Guarda [Configurare Dispatcher SDK](https://video.tv.adobe.com/v/30602) per informazioni su come configurare Dispatcher SDK</li><li>Consulta la documentazione [Local Development Setup](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up) per ulteriori informazioni</li><li>Configurazione dell&#39;accesso all&#39;Experience Manager [procedura dettagliata](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en#accessing)</li></ol> | <ol><li>[Nozioni di base sullo sviluppo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing)</li><li>[Linee guida per lo sviluppo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#developing)</li><li>[Struttura del progetto Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=en#developing)</li><li>[Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it)</li><li>[Blueprint Digital Foundation](https://solutionpartners.adobe.com/content/dam/spp_assets/restricted/community/community_31/digital_foundation_best_practices_and_documentation.zip)</li><li>[Sistema di stili](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/style-system.html?lang=en#authoring)</li><li>[Sovrapposizioni](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/overlays.html?lang=en#developing)</li><li>[Riferimento API per Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service-javadoc/)</li></ol> |

>[!TIP]
> Vedi l&#39;esercitazione su come [Sviluppare e distribuire WKND sull&#39;SDK di Experience Manager locale](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en)

### Distribuzione

Gli sviluppatori scrivono il codice e lo testano localmente, che viene quindi inviato a AEM remote come ambienti di Cloud Service.

Cloud Manager, uno strumento opzionale per la distribuzione dei contenuti per Managed Services, è necessario. Questo è ora l’unico meccanismo per distribuire il codice in AEM come ambienti di Cloud Service.

Consulta le risorse di supporto autonomo su come configurare e distribuire in AEM come ambienti di Cloud Service.

1. [Configurare le pipeline CM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager)
   * Pipeline di produzione
   * Solo pipeline non di produzione e di qualità del codice
2. [Distribuisci codice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#using-cloud-manager)
3. [Risultati dei test](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/overview-test-results.html?lang=en#using-cloud-manager)
4. **Accesso ai registri**
   * [tramite interfaccia utente CM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=en#using-cloud-manager)
   * [tramite i/o Adobe](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
5. [Operazioni e manutenzione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/home.html?lang=en)
   * [Configurazione di OSGI](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#deploying)
   * [Backup e ripristino](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/backup.html?lang=en)

>[!TIP]
> Vedi l&#39;esercitazione su come [distribuire WKND ad Experience Manager Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/develop-wknd-tutorial.html?lang=en)

### Aiuto e risorse

1. [Suggerimenti per il debug](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=en#debugging-aem-as-a-cloud-service)
2. [Console per sviluppatori](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=en#debugging)
3. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/crxde-lite.html?lang=en#debugging) (Disponibile solo negli ambienti SDK locali e Experience Manager Cloud Dev)
4. [Registri e registrazioni](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
   * [Registri CM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging)  (testing di unità build, scansione del codice, creazione-immagine, distribuzione)
   * [Registri di Experience Manager Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)  (aemerror, aemaccess, aemrequest, aemdispatcher, httpderror, httpaccess)
   * Registri SDK locali (sotto host:port/crx-quickstart/logs)

>[!NOTE]
> Per ulteriore assistenza, puoi effettuare le seguenti operazioni:
>1. [Contatta il team di supporto Experience Manager](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. Esplora [Community Experience Manager e forum](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)


<br>

## Passaggio ad Adobe Experience Manager as a Cloud Service {#move-to-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_move_to_cloud"
>title="Passaggio ad Adobe Experience Manager as a Cloud Service"
>abstract="Questo unico pager delinea l’approccio graduale consigliato per la transizione dei clienti da varie implementazioni di Experience Manager ad Experience Manager come Cloud Service e aiuta i clienti esistenti a fornire esperienze continue e connesse su questa piattaforma moderna e appositamente progettata per la gestione delle esperienze."

**Experience Manager as a Cloud Service fornisce una base tecnologica scalabile, sicura e agile per Sites e Assets di Experience Manager, consentendo agli addetti al marketing e all’IT di concentrarsi sulla fornitura di esperienze d’impatto su vasta scala.**

Con l’Experience Manager come Cloud Service, i tuoi team possono concentrarsi sull’innovazione invece di pianificare gli aggiornamenti dei prodotti. Le nuove funzionalità dei prodotti vengono testate in maniera approfondita e distribuite ai team senza interruzioni, in modo che possano sempre accedere all’applicazione all’avanguardia.

Il percorso di transizione verso Cloud Service prevede tre fasi: pianificazione, esecuzione e post-pubblicazione.
Per una transizione corretta e senza problemi, è necessario garantire una pianificazione adeguata e attenersi alle best practice descritte nella presente guida.

La figura seguente mostra un’illustrazione del percorso consigliato per la transizione a Cloud Service.

![immagine](/help/move-to-cloud-service/assets/home-img1.png)

<br>

### Pianificazione

Prima di iniziare il percorso di transizione al Cloud Service, è necessario acquisire familiarità con l’Experience Manager come Cloud Service e rivedere le modifiche rilevanti apportate al , nonché esaminare le funzioni sostituite o obsolete.

<table>
<tr>
<td>Individuazione e valutazione dei progetti</td>
<td><ul><li>Per informazioni sulle differenze importanti tra Adobe Experience Manager as a Cloud Service e Experience Manager 6.x, consulta <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=en">Modifiche di rilievo apportate ad Experience Manager as a Cloud Service</a> .</li><li>Per ulteriori informazioni sulle funzioni e le funzionalità contrassegnate come obsolete, consulta <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/deprecated-removed-features.html?lang=en#deprecated-features">Funzioni obsolete</a> .</li><li>[Solo per le migrazioni Cloud Service] Valutazione della preparazione al Cloud Service : Esegui <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration">Best Practices Analyzer(BPA)</a> nell'ambiente di origine </li><li>Completa una valutazione delle modifiche di rilievo e delle funzioni obsolete in Experience Manager CS</li></ul></td>
</tr>
<tr>
<td>Recensione</td>
<td><ul><li>In base al rilevamento, eseguire la stima dello sforzo e gli esercizi di risorse</li></ul></td>
</tr>
<tr>
<td>Misura</td>
<td><ul><li><a href="https://experienceleague.adobe.com/welcome/aem/part6.html">Stabilire KPI</a> di progetto, criteri di successo e timeline del progetto</li></ul></td>
</tr>
</table>

>[!NOTE]
>Il rapporto di Best Practices Analyzer (Analisi di best practice) velocizza il processo di stima dei tempi e dei costi necessari per la transizione a AEM come Cloud Service, fornendo informazioni che altrimenti dovrebbero essere raccolte e valutate manualmente.


<br>

### Esecuzione

Prima di avviare la fase di esecuzione di un progetto, devi essere integrato nel Cloud Service. Devi anche acquisire familiarità con Cloud Manager. Questo è il meccanismo per distribuire il codice del progetto in un’istanza di Experience Manager Cloud Service.

Cloud Manager consente alle organizzazioni di gestire autonomamente Experience Manager nel cloud. Include un framework di integrazione continua e consegna continua ([CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/overview/ci-cd-pipeline.html?lang=en#overview)) che consente ai team IT e ai partner di implementazione di accelerare la distribuzione di personalizzazioni o aggiornamenti senza compromettere prestazioni o sicurezza.

#### Migrazione dei contenuti

1. [Strumento](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration)  Content Transfer (Trasferimento contenuti): utilizzato per spostare il contenuto esistente da un’istanza di AEM di origine (on-premise o AMS) all’istanza di Cloud Service AEM di destinazione.
2. [Gestione](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#package-manager)  pacchetti: utilizzato per importare ed esportare contenuti mutabili dell&#39;archivio.


#### Refactoring/ottimizzazione

| Guida introduttiva | Revisione e codice di refactoring | Revisione di Dispatcher |
|---|---|---|
| <ul><li>[Impostazione sviluppo locale](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up)</li><li>[Configurazione del Dispatcher locale](https://video.tv.adobe.com/v/30602/)</li><li>[Compila il codice utilizzando l’SDK API jar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing)</li><li>[Rivedere AEM linee guida per lo sviluppo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#developing)<ul><li>Attività in background e processi con esecuzione lunga</li><li>Programmatori Sling</li><li>Utilizzo del flusso di ingresso e altro ancora</li></ul></li></ul> | <ul><li>Esegui [Best Practices Analyzer(BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration) nell&#39;ambiente di origine.[**Solo migrazione**]<ul><li>Considerazioni sulla struttura del progetto (basate su [Cloud Archetype](https://github.com/adobe/aem-project-archetype))<ul><li>Separazione di codice e contenuto (variabile e immutabile)</li><li>[Definizioni di indici personalizzate](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#indexing)</li><li>[Modalità di esecuzione personalizzate](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#runmodes)</li></ul></li></ul></li><li>Rivedi ed esegui le modifiche necessarie</li><li>[](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en) Implementazione sull’SDK locale</li><li>Eseguire test del fumo tramite AEM SDK</li></ul> | <ul><li>Rivedi [Configurazioni del dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#local-validation-of-dispatcher-configuration) per il refactoring</li><li>Utilizza lo strumento [Dispatcher Converter](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/dispatcher-transformation-utility-tools.html?lang=en#introduction-dispatcher) , se necessario. [**Solo migrazione**]</li><li>Il test può essere eseguito utilizzando [Dispatcher SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#prerequisites)</li></ul> |

>[!TIP]
> Clienti Assets : Rivedi e refattori i flussi di lavoro delle risorse utilizzando gli strumenti [Migrazione di Asset Cloud](https://github.com/adobe/aem-cloud-migration)


#### Distribuzione/Go-Live

1. [Distribuzione a Cloud ](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html?lang=en#managing-code) Manager
2. Esegui il codice cliente tramite la [pipeline di qualità di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use)
3. [Distribuisci nell&#39;ambiente di sviluppo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging)
4. [**Trasferimento**] solo dei contenuti mediante pacchetti o strumento  [Content Transfer (CTT)](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md)
5. Eseguire cicli di prova raccomandati (fumo, controllo qualità e altro)
6. Promozione alla pipeline di produzione di Cloud Manager
7. Convalida della prova del fumo
8. Go-Live

<br>

### Post-pubblicazione

Nella fase di post-pubblicazione, devi assicurarti che i file temporanei vengano eliminati, esaminare le best practice per lo sviluppo continuo e gestire i registri.

>[!TIP]
> Sono disponibili strumenti per la risoluzione dei problemi relativi agli ambienti AEM come Cloud Service
>1. [Console per sviluppatori](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#aem-as-a-cloud-service-development-tools)
>2. [CRX/DE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/crxde-lite.html?lang=en#debugging)
>3. [Gestione dei registri](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=en#using-cloud-manager)


<br>

### Strumenti e risorse

| Valutazione | Refactoring | Modernizzazione degli Experienci Manager | Migrazione dei contenuti |
|------------|-------------|---------------------------------|-------------------|
| <ul><li>[Analisi delle best practice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration)</li></li> | <ul><li>[Plug-in esperienza unificato](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#refactoring-tools)</li></ul> | <ul><li>[Modelli statici in modelli modificabili](https://opensource.adobe.com/aem-modernize-tools/pages/tools/page-structure.html)</li><li>[Configurazioni di progettazione in policy](https://opensource.adobe.com/aem-modernize-tools/pages/tools/policy-importer.html) <li>[Componenti di base in componenti core](https://opensource.adobe.com/aem-modernize-tools/pages/tools/component.html)</li><li>[Interfaccia classica in interfaccia touch](https://opensource.adobe.com/aem-modernize-tools/pages/tools/dialog.html)</li></ul> | <ul><li>[Strumento Content Transfer (Trasferimento contenuti) ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#cloud-migration)</li><li>[Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#contentmanagement)</li></ul> |

>[!NOTE]
> Per ulteriore assistenza, puoi effettuare le seguenti operazioni:
>1. [Contatta il team di supporto Experience Manager](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. Esplora [Community Experience Manager e forum](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)

