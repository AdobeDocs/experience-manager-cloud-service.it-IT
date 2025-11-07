---
title: Guida alla migrazione a Experience Manager as a Cloud Service per i partner
description: Guida alla migrazione a Experience Manager as a Cloud Service per i partner
exl-id: 9d5a72b8-06af-4b82-ab20-e65aea7903b3
feature: Migration
role: Admin
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 18%

---

# Guida alla migrazione a Adobe Experience Manager as a Cloud Service per i partner {#Overview}

>[!CONTEXTUALHELP]
>id="aemcloud_migration_overview"
>title="Migrazione ad AEM as a Cloud Service"
>abstract="Illustra il processo graduale consigliato per la transizione dei clienti da varie implementazioni di Experience Manager a Experience Manager as a Cloud Service e per aiutare i clienti esistenti a fornire esperienze continue e connesse"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html?lang=it" text="Novità e differenze"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/introduction.html?lang=it" text="Introduzione ad AEM as a Cloud Service."

Adobe Experience Manager (AEM) as a Cloud Service offre un’architettura aggiornata per Experience Manager. Questa base si basa su un’infrastruttura basata su contenitori, su uno sviluppo basato su API e su un processo DevOps guidato. Questo consente agli addetti al marketing e agli sviluppatori di stare al passo con le innovazioni nella gestione della customer experience.

Cloud Service riunisce funzionalità avanzate ed estensibilità di Adobe Experience Manager con l&#39;agilità della moderna architettura nativa per il cloud, consentendo ai brand di soddisfare la domanda in continua evoluzione dei consumatori.

Questa pagina illustra l’approccio graduale consigliato per la transizione dei clienti dalle precedenti implementazioni di Experience Manager ad Experience Manager as a Cloud Service. La nuova piattaforma appositamente progettata consente di offrire esperienze connesse e continue.

<!-- It primarily focuses on:
* Getting Started with Adobe Experience Manager as a Cloud Service
* Developer Journey in Adobe Experience Manager as a Cloud Service
* Moving to Adobe Experience Manager as a Cloud Service -->

Per una rappresentazione generale del percorso di migrazione, vedere il diagramma seguente.

![Rappresentazione generale del percorso di migrazione](/help/journey-migration/assets/migration-process.png)

## Guida introduttiva ad Adobe Experience Manager as a Cloud Service {#getting-started}

| Cos&#39;è diverso? | Panoramica dell’architettura |
|--------------------------|--------------------------|
| <ul><li>[Architettura moderna](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/architecture.html?lang=it)</li><li>[Aggiornamenti automatici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html?lang=it)</li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=it)</li><li>[Microservizi risorse](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/asset-microservices-overview.html?lang=it)</li><li>[File binari ad accesso diretto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/asset-microservices-overview.html?lang=it)</li><li>[Separazione di codice e contenuto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=it)</li><li>[Replica come servizio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/replication.html?lang=it)</li><li>[Admin Console, appartenenza a gruppi/utenti e ACL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=it)</li></ul> | <ul><li>[Introduzione all&#39;architettura di AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-architecture.html?lang=it#underlying-technology)</li><li>[Stack ambiente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/architecture.html?lang=it)</li><li>[Livello di creazione](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=it#underlying-technology)</li><li>[Livello di pubblicazione](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=it#underlying-technology)</li><li>[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=it)</li><li>[CDN](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn) </li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=it) (CI/CD)</li><li>[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=it) tramite [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=it)</li><li>[Servizio Asset Compute](https://experienceleague.adobe.com/docs/asset-compute/using/home.html?lang=it)</li></ul> |

![AEM as a Cloud Service: architettura runtime](/help/overview/assets/concepts-03.png "AEM as a Cloud Service - Architettura runtime")

<br>

## Percorso di sviluppatori in Adobe Experience Manager as a Cloud Service {#developer-journey}

### Sviluppo

Le nozioni di base sullo sviluppo del codice in Adobe Experience Manager as a Cloud Service sono simili a quelle delle soluzioni Adobe Experience Manager On Premise e Managed Services.

Gli sviluppatori scrivono il codice e lo sottopongono a test localmente, quindi lo inviano agli ambienti Adobe Experience Manager as a Cloud Service remoti.

Per informazioni su come personalizzare l’implementazione di Experience Manager as a Cloud Service, consulta le risorse di supporto autonomo sull’implementazione di Experience Manager as a Cloud Service.

| Configurazione dello sviluppo locale | Aspetti da considerare prima di iniziare |
|-----------|------------|
| <ol><li>Consulta la documentazione di [Adobe Experience Manager SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=it) per ulteriori informazioni.</li><li>Guarda [Installare Dispatcher SDK](https://video.tv.adobe.com/v/30601) per scoprire come installare Dispatcher SDK</li><li>Guarda [Configurare Dispatcher SDK](https://video.tv.adobe.com/v/30602) per informazioni su come configurare Dispatcher SDK</li><li>Consulta la documentazione [Local Development Setup](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=it#local-development-environment-set-up) per ulteriori informazioni</li><li>Configurazione dell&#39;accesso a Experience Manager [procedura dettagliata](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=it#accessing)</li></ol> | <ol><li>[Elementi di base per lo sviluppo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=it)</li><li>[Linee guida per lo sviluppo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=it)</li><li>[Informazioni sulla struttura dei progetti Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=it)</li><li>[Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it)</li><li>[Blueprint Digital Foundation](https://solutionpartners.adobe.com/content/dam/solution/en/spp_assets/restricted/community/community_31/digital_foundation_best_practices_and_documentation.zip)</li><li>[Sistema di stili](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/style-system.html?lang=it)</li><li>[Sovrapposizioni](/help/implementing/developing/introduction/overlays.md)</li><li>[Riferimento API di Experience Manager as a Cloud Service](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/)</li></ol> |

>[!TIP]
> Guarda il tutorial su come [sviluppare e distribuire WKND su Experience Manager SDK locale](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=it)

### Implementazione

Gli sviluppatori scrivono il codice e lo sottopongono a test localmente, quindi lo inviano agli ambienti AEM as a Cloud Service remoti.

È ora necessario Cloud Manager, uno strumento opzionale per la distribuzione dei contenuti di Managed Services. È l’unico meccanismo per distribuire il codice negli ambienti AEM as a Cloud Service.

Consulta le risorse di supporto autonomo su come configurare e distribuire in ambienti AEM as a Cloud Service.

1. [Configura pipeline CM](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/introduction-ci-cd-pipelines)

   * Pipeline di produzione
   * Pipeline non di produzione e destinate solo alla qualità del codice

1. [Distribuisci codice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=it)
1. [Informazioni sui risultati dei test](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/test-results/overview-test-results.html?lang=it)
1. **Accesso ai registri**

   * [tramite interfaccia utente CM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs.html?lang=it)
   * [tramite Adobe i/o cli](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=it#debugging)

1. [Operazioni e manutenzione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/home.html?lang=it)

   * [Configurazione della configurazione OSGI](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html?lang=it)
   * [Backup e ripristino](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/backup.html?lang=it)

>[!TIP]
> Guarda il tutorial su come [distribuire WKND in Experience Manager Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=it)

### Aiuto e risorse

1. [Suggerimenti e trucchi per il debug](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=it#debugging-aem-as-a-cloud-service)
1. [Console per sviluppatori](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=it#debugging)
1. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=it) (disponibile solo negli ambienti SDK e Experience Manager Cloud Dev locali)
1. [Registri e registrazione](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=it#debugging)

   * [Registri CM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=it#debugging) (build-unit-testing, code-scanning, build-image, deploy)
   * [Registri Experience Manager Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=it#debugging) (aemerror, aemaccess, aemrequest, aemdispatcher, httpderror, httpaccess)
   * Registri SDK locali (sotto host:port/crx-quickstart/logs)

>[!NOTE]
>
> Per ulteriore assistenza, è possibile:
>
>1. [Contatta il team di supporto Experience Manager](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=it)
>1. Esplora [Community e forum di Experience Manager](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community?lang=it)

<br>

## Passare ad Adobe Experience Manager as a Cloud Service {#move-to-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_move_to_cloud"
>title="Passare ad Adobe Experience Manager as a Cloud Service"
>abstract="Questa pagina illustra il processo graduale consigliato per la transizione dei clienti da varie implementazioni di Experience Manager a Experience Manager as a Cloud Service e per aiutare i clienti esistenti a fornire esperienze continue e connesse su questa piattaforma moderna, specifica per la gestione delle esperienze."

**Experience Manager as a Cloud Service fornisce una base tecnologica scalabile, sicura e agile per Experience Manager Sites e Assets, consentendo agli addetti al marketing e all&#39;IT di concentrarsi sulla distribuzione di esperienze d&#39;impatto su larga scala.**

Con Experience Manager as a Cloud Service, i team possono concentrarsi sull’innovazione invece di pianificare gli aggiornamenti di prodotto. Le nuove funzioni dei prodotti vengono testate in modo approfondito e distribuite ai team senza interruzioni, in modo che possano sempre accedere all’applicazione all’avanguardia.

Il percorso di transizione verso Cloud Service prevede tre fasi: pianificazione, esecuzione e post-pubblicazione.
Per una transizione corretta e senza problemi, è necessario garantire una pianificazione adeguata e attenersi alle best practice descritte nella presente guida.

La figura seguente mostra una rappresentazione di alto livello del percorso di transizione consigliato a Cloud Service.

![Rappresentazione di alto livello del percorso di transizione consigliato a Cloud Service](/help/journey-migration/assets/home-img1.png)

<br>

### Pianificazione

Prima di iniziare il percorso di transizione verso Cloud Service, è necessario:

* acquisire familiarità con Experience Manager as a Cloud Service
* rivedere le modifiche di rilievo apportate
* esaminare le feature sostituite o dichiarate obsolete

<table>
<tr>
<td>Individuazione e valutazione dei progetti</td>
<td><ul><li>Consulta <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/aem-cloud-changes.html?lang=it">Modifiche di rilievo apportate ad Experience Manager as a Cloud Service</a> per comprendere le importanti differenze tra Adobe Experience Manager as a Cloud Service e Experience Manager 6.x.</li><li>Per ulteriori informazioni sulle funzionalità contrassegnate come obsolete, vedere <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/deprecated-removed-features.html?lang=it">Funzioni obsolete</a>.</li><li>[Solo per le migrazioni Cloud Service] Valutazione della fattibilità di Cloud Service: esegui <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=it">Best Practices Analyzer(BPA)</a> nell'ambiente di origine </li><li>Completa una valutazione in relazione a modifiche di rilievo e funzioni obsolete in Experience Manager CS</li></ul></td>
</tr>
<tr>
<td>Rivedere</td>
<td><ul><li>In base all'individuazione, eseguire la stima dello sforzo e gli esercizi di risorse</li></ul></td>
</tr>
<tr>
<td>Misura</td>
<td><ul><li><a href="https://experienceleague.adobe.com/welcome/aem/part6.html">Stabilire i KPI del progetto</a>, i criteri di successo e le tempistiche del progetto</li></ul></td>
</tr>
</table>

>[!NOTE]
>Il rapporto di Best Practices Analyzer (Analisi delle best practice) consente di valutare più rapidamente il tempo e i costi necessari per la transizione ad AEM as a Cloud Service, fornendo informazioni che altrimenti dovrebbero essere raccolte e valutate manualmente.


<br>

### Esecuzione

Prima di avviare la fase di esecuzione di un progetto, devi aver effettuato l’onboarding in Cloud Service. È inoltre necessario acquisire familiarità con Cloud Manager. Questo è il meccanismo per distribuire il codice del progetto in un’istanza Experience Manager Cloud Service.

Cloud Manager consente alle organizzazioni di gestire autonomamente Experience Manager nel cloud. Include un framework di integrazione continua e distribuzione continua ([CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/overview/ci-cd-pipelines.html?lang=it)) che consente ai team IT e ai partner di implementazione di accelerare la distribuzione di personalizzazioni o aggiornamenti senza compromettere le prestazioni o la sicurezza.

#### Migrazione dei contenuti

1. [Strumento Content Transfer](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=it#migration): utilizzato per spostare il contenuto esistente da un&#39;istanza AEM di origine (on-premise o AMS) all&#39;istanza AEM Cloud Service di destinazione.
1. [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=it#package-manager): utilizzato per importare ed esportare contenuto modificabile dell&#39;archivio.


#### Refactoring/Ottimizzazione

| Guida introduttiva | Revisione e refactoring del codice | Revisione Dispatcher |
|---|---|---|
| <ul><li>[Configurazione sviluppo locale](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=it#local-development-environment-set-up)</li><li>[Installazione locale di Dispatcher](https://video.tv.adobe.com/v/30602/)</li><li>[Compila il codice utilizzando SDK API jar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=it)</li><li>[Rivedi le linee guida per lo sviluppo di AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=it)<ul><li>Attività in background e processi con esecuzione prolungata</li><li>Utilità di pianificazione Sling</li><li>Utilizzo del flusso di ingresso e altro ancora</li></ul></li></ul> | <ul><li>Esegui [Best Practices Analyzer(BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=it) nell&#39;ambiente di origine.[**Solo migrazione**]<ul><li>Considerazioni sulla struttura del progetto (in base a [Archetipo cloud](https://github.com/adobe/aem-project-archetype))<ul><li>Separazione di codice e contenuto (mutabile e immutabile)</li><li>[Definizioni indice personalizzate](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=it)</li><li>[Modalità di esecuzione personalizzate](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html?lang=it)</li></ul></li></ul></li><li>Rivedere ed eseguire le modifiche necessarie</li><li>[Distribuisci](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=it) nel SDK locale</li><li>Eseguire il test del fumo tramite AEM SDK</li></ul> | <ul><li>Rivedi [Configurazioni Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=it) per il refactoring</li><li>Usare lo strumento [Dispatcher Converter](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/dispatcher-transformation-utility-tools.html?lang=it) dove appropriato. [**Solo migrazione**]</li><li>I test possono essere eseguiti utilizzando [Dispatcher SDK](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools#prerequisites)</li></ul> |

>[!TIP]
> Clienti Assets: rivedi e refactoring dei flussi di lavoro Assets tramite gli strumenti [Asset Cloud Migration](https://github.com/adobe/aem-cloud-migration)


#### Implementazione/Go-Live

1. [Implementa in Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/git-integration.html?lang=it) Git
2. Esegui il codice cliente tramite [Pipeline di qualità Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-quality-testing.html?lang=it)
3. [Distribuisci nell&#39;ambiente di sviluppo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=it#debugging)
4. **Solo migrazione** Trasferimento dei contenuti tramite pacchetti o [Strumento Trasferimento contenuti](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md)(CTT)
5. Eseguire i cicli di prova raccomandati (fumo, controllo qualità e altro)
6. Promuovi alla pipeline di produzione Cloud Manager
7. Convalida del test antifumo
8. Pubblicazione

<br>

### Post-pubblicazione

Nella fase di post-pubblicazione, devi assicurarti che i file temporanei vengano eliminati, esaminare le best practice per lo sviluppo continuo e gestire i registri.

>[!TIP]
>
> Sono disponibili strumenti per la risoluzione dei problemi relativi all’ambiente AEM as a Cloud Service
>
>1. [Console per sviluppatori](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=it)
>1. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=it)
>1. [Gestione dei registri](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs.html?lang=it)

<br>

### Strumenti e risorse

| Valutazione | Refactoring | Modernizzazione Experience Manager | Migrazione dei contenuti |
|------------|-------------|---------------------------------|-------------------|
| <ul><li>[Analisi delle best practice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=it)</li></li> | <ul><li>[Plug-in esperienza unificato](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/unified-experience.html?lang=it)</li></ul> | <ul><li>[Modelli statici in modelli modificabili](https://opensource.adobe.com/aem-modernize-tools/pages/structure.html)</li><li>[Configurazioni di progettazione in criteri](https://opensource.adobe.com/aem-modernize-tools/pages/policy.html) <li>[Componenti Foundation in Componenti core](https://opensource.adobe.com/aem-modernize-tools/pages/component.html)</li><li>[Interfaccia classica in interfaccia touch](https://opensource.adobe.com/aem-modernize-tools/pages/all-in-one.html)</li></ul> | <ul><li>[Strumento Content Transfer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=it)</li><li>[Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=it#contentmanagement)</li></ul> |

>[!NOTE]
>
> Per ulteriore assistenza, è possibile:
>
>1. [Contatta il team di supporto Experience Manager](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=it)
>1. Esplora [Community e forum di Experience Manager](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community?lang=it)
