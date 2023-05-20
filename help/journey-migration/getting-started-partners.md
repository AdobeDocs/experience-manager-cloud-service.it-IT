---
title: Guida alla migrazione a Experience Manager as a Cloud Service per i partner
description: Guida alla migrazione a Experience Manager as a Cloud Service per i partner
exl-id: 9d5a72b8-06af-4b82-ab20-e65aea7903b3
source-git-commit: d925310603961f1f3721c283fc247105459e9c0f
workflow-type: tm+mt
source-wordcount: '2122'
ht-degree: 21%

---

# Guida alla migrazione ad Adobe Experience Manager as a Cloud Service per i partner {#Overview}

>[!CONTEXTUALHELP]
>id="aemcloud_migration_overview"
>title="Migrazione ad AEM as a Cloud Service"
>abstract="Illustra il processo graduale consigliato per la transizione dei clienti da varie implementazioni di Experience Manager a Experience Manager as a Cloud Service e per aiutare i clienti esistenti a fornire esperienze continue e connesse"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html?lang=it" text="Novità e differenze"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/introduction.html?lang=it" text="Introduzione ad AEM as a Cloud Service."

Adobe Experience Manager (AEM) as a Cloud Service offre una base riprogettata per Experience Manager, basata su un’infrastruttura basata su contenitori, sviluppo basato su API e processo DevOps guidato, che consente agli addetti al marketing e agli sviluppatori di tenere sempre il passo con le innovazioni nella gestione dell’esperienza del cliente.

Il Cloud Service riunisce funzionalità avanzate ed estensibilità di Adobe Experience Manager con l’agilità della moderna architettura nativa per il cloud, consentendo ai marchi di soddisfare la domanda in continua evoluzione dei consumatori.

Questa pagina illustra il processo graduale consigliato per la transizione dei clienti da varie implementazioni di Experience Manager a Experience Manager as a Cloud Service e per aiutare i clienti esistenti a fornire esperienze continue e connesse su questa piattaforma moderna, specifica per la gestione delle esperienze.

<!-- It primarily focuses on:
* Getting Started with Adobe Experience Manager as a Cloud Service
* Developer Journey in Adobe Experience Manager as a Cloud Service
* Moving to Adobe Experience Manager as a Cloud Service -->

Per una rappresentazione generale del percorso di migrazione, vedere il diagramma seguente.

![immagine](/help/journey-migration/assets/migration-process.png)

## Guida introduttiva ad Adobe Experience Manager as a Cloud Service {#getting-started}

| Cos&#39;è diverso? | Panoramica dell’architettura |
|--------------------------|--------------------------|
| <ul><li>[Architettura moderna](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/architecture.html)</li><li>[Aggiornamenti automatici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html)</li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=it)</li><li>[Microservizi per le risorse](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/asset-microservices-overview.html)</li><li>[Binari ad accesso diretto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/asset-microservices-overview.html?lang=en)</li><li>[Separazione di codice e contenuto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=en)</li><li>[Replica come servizio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/replication.html?lang=it)</li><li>[Admin Console, appartenenza a gruppi/utenti e ACL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html)</li></ul> | <ul><li>[Introduzione all’architettura dell’AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-architecture.html?lang=en#underlying-technology)</li><li>[Stack ambiente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/architecture.html)</li><li>[Livello di authoring](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[Livello di pubblicazione](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=en)</li><li>[CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html?lang=en) </li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=it) (CI/CD)</li><li>[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=it) tramite [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html)</li><li>[Servizio Asset compute](https://experienceleague.adobe.com/docs/asset-compute/using/home.html)</li></ul> |

![AEM as a Cloud Service: architettura runtime](/help/overview/assets/concepts-03.png "AEM as a Cloud Service - Architettura runtime")

<br>

## Percorso di sviluppatori in Adobe Experience Manager as a Cloud Service {#developer-journey}

### Sviluppo

Le nozioni di base sullo sviluppo del codice in Adobe Experience Manager as a Cloud Service sono simili a quelle delle soluzioni Adobe Experience Manager On Premise e Managed Services.

Gli sviluppatori scrivono il codice e lo testano localmente, che viene quindi inviato agli ambienti Adobe Experience Manager as a Cloud Service remoti.

Consulta le risorse di supporto autonomo sull’implementazione per Experience Manager as a Cloud Service per scoprire come personalizzare la distribuzione Experience Manager as a Cloud Service.

| Configurazione dello sviluppo locale | Aspetti da considerare prima di iniziare |
|-----------|------------|
| <ol><li>Revisione [SDK di Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en) per ulteriori informazioni.</li><li>Osserva [Installare l’SDK di Dispatcher](https://video.tv.adobe.com/v/30601) per scoprire come installare l’SDK di Dispatcher</li><li>Osserva [Configurare l’SDK di Dispatcher](https://video.tv.adobe.com/v/30602) per informazioni su come configurare l’SDK di Dispatcher</li><li>Revisione [Configurazione dello sviluppo locale](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up) documentazione per ulteriori informazioni</li><li>Configurazione dell’accesso a Experience Manager [procedura dettagliata](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en#accessing)</li></ol> | <ol><li>[Elementi di base per lo sviluppo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en)</li><li>[Linee guida per lo sviluppo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=en)</li><li>[Informazioni sulla struttura del progetto Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html?lang=en)</li><li>[Componenti di base](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it)</li><li>[Blueprint Digital Foundation](https://solutionpartners.adobe.com/content/dam/solution/en/spp_assets/restricted/community/community_31/digital_foundation_best_practices_and_documentation.zip)</li><li>[Sistema di stili](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/authoring/features/style-system.html?lang=en)</li><li>[Sovrapposizioni](/help/implementing/developing/introduction/overlays.md)</li><li>[Experience Manager di riferimento API as a Cloud Service](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/)</li></ol> |

>[!TIP]
> Guarda il tutorial su come [Sviluppare e distribuire WKND sull’SDK dell’Experience Manager locale](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=it)

### Distribuzione

Gli sviluppatori scrivono e testano localmente il codice, che viene quindi inviato agli ambienti AEM as a Cloud Service remoti.

Cloud Manager, che era uno strumento opzionale per la distribuzione dei contenuti per Managed Services, è necessario. Questo è ora l’unico meccanismo per distribuire il codice negli ambienti AEM as a Cloud Service.

Consulta le risorse di supporto autonomo su come configurare e distribuire in ambienti AEM as a Cloud Service.

1. [Configurare le pipeline CM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/cicd-pipelines/introduction-ci-cd-pipelines.html?lang=en)
   * Pipeline di produzione
   * Pipeline non di produzione e destinate solo alla qualità del codice
2. [Distribuisci codice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html?lang=en)
3. [Risultati dei test](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/test-results/overview-test-results.html?lang=en)
4. **Accesso ai registri**
   * [tramite interfaccia utente CM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs.html?lang=en)
   * [tramite cli di i/o Adobe](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
5. [Operazioni e manutenzione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/home.html?lang=en)
   * [Configurazione della configurazione OSGI](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html?lang=en)
   * [Backup e ripristino](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/backup.html?lang=en)

>[!TIP]
> Guarda il tutorial su come [Distribuire WKND in Experience Manager Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=it)

### Aiuto e risorse

1. [Suggerimenti e trucchi per il debug](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=en#debugging-aem-as-a-cloud-service)
2. [Console per sviluppatori](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=en#debugging)
3. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=en) (disponibile solo negli ambienti SDK locali e Experience Manager Cloud Dev)
4. [Registri e registrazione](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
   * [Registri CM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging) (build-unit-testing, scansione del codice, build-image, distribuzione)
   * [Registri di Experience Manager Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging) (aemerror, aemaccess, aemrequest, aemdispatcher, httpderror, httpaccess)
   * Registri SDK locali (sotto host:port/crx-quickstart/logs)

>[!NOTE]
> Per ulteriori informazioni, è possibile:
>1. [Contatta il team di supporto Experience Manager](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. Esplora [Community e forum Experienci Manager](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)


<br>

## Passare ad Adobe Experience Manager as a Cloud Service {#move-to-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_move_to_cloud"
>title="Passare ad Adobe Experience Manager as a Cloud Service"
>abstract="Questa pagina illustra il processo graduale consigliato per la transizione dei clienti da varie implementazioni di Experience Manager a Experience Manager as a Cloud Service e per aiutare i clienti esistenti a fornire esperienze continue e connesse su questa piattaforma moderna, specifica per la gestione delle esperienze."

**Experience Manager as a Cloud Service fornisce una base tecnologica scalabile, sicura e agile per Experience Manager Sites e Assets, consentendo agli addetti al marketing e all’IT di concentrarsi sulla distribuzione di esperienze d’impatto su larga scala.**

Con Experience Manager as a Cloud Service, i team possono concentrarsi sull’innovazione invece di pianificare gli aggiornamenti dei prodotti. Le nuove funzioni dei prodotti vengono testate in modo approfondito e distribuite ai team senza interruzioni, in modo che possano sempre accedere all’applicazione all’avanguardia.

Il percorso di transizione verso Cloud Service prevede tre fasi: pianificazione, esecuzione e post-pubblicazione.
Per una transizione corretta e senza problemi, è necessario garantire una pianificazione adeguata e attenersi alle best practice descritte nella presente guida.

La figura seguente mostra una rappresentazione di alto livello della transizione consigliata da percorso a Cloud Service.

![immagine](/help/journey-migration/assets/home-img1.png)

<br>

### Pianificazione

Prima di iniziare la transizione da percorso a Cloud Service, è necessario acquisire familiarità con Experience Manager as a Cloud Service, esaminare le modifiche rilevanti apportate e rivedere anche le funzioni che sono state sostituite o dichiarate obsolete.

<table>
<tr>
<td>Individuazione e valutazione dei progetti</td>
<td><ul><li>Fai riferimento a <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/aem-cloud-changes.html?lang=it">Modifiche di rilievo apportate all'Experience Manager as a Cloud Service</a> comprendere le differenze importanti tra Adobe Experience Manager as a Cloud Service e l’Experience Manager 6.x.</li><li>Fai riferimento a <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/deprecated-removed-features.html?lang=en">Funzioni obsolete</a> per ulteriori informazioni sulle funzionalità contrassegnate come obsolete.</li><li>[Solo per le migrazioni di Cloud Service] Valutazione della preparazione del Cloud Service: eseguire il comando <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en">Best Practices Analyzer (BPA)</a> nell’ambiente di origine </li><li>Completa una valutazione in relazione a modifiche di rilievo e funzioni obsolete in Experience Manager CS</li></ul></td>
</tr>
<tr>
<td>Recensione</td>
<td><ul><li>In base all'individuazione, eseguire la stima dello sforzo e gli esercizi di risorse</li></ul></td>
</tr>
<tr>
<td>Misura</td>
<td><ul><li><a href="https://experienceleague.adobe.com/welcome/aem/part6.html">Stabilire i KPI del progetto</a>, criteri di successo e timeline di progetto</li></ul></td>
</tr>
</table>

>[!NOTE]
>Il rapporto Best Practices Analyzer (Analisi delle best practice) consente di valutare più rapidamente il tempo e i costi necessari per la transizione all’AEM as a Cloud Service, fornendo informazioni che altrimenti dovrebbero essere raccolte e valutate manualmente.


<br>

### Esecuzione

Prima di avviare la fase di esecuzione di un progetto, devi aver effettuato l’onboarding al Cloud Service. È inoltre necessario acquisire familiarità con Cloud Manager. Questo è il meccanismo per distribuire il codice del progetto in un’istanza Experience Manager Cloud Service.

Cloud Manager consente alle organizzazioni di gestire autonomamente gli Experienci Manager nel Cloud. Include un&#39;integrazione continua e una distribuzione continua ([CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/overview/ci-cd-pipelines.html?lang=en)) che consente ai team IT e ai partner di implementazione di accelerare la distribuzione di personalizzazioni o aggiornamenti senza compromettere le prestazioni o la sicurezza.

#### Migrazione dei contenuti

1. [Strumento Content Transfer](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration) : utilizzato per spostare il contenuto esistente da un’istanza AEM di origine (on-premise o AMS) all’istanza AEM Cloud Service di destinazione.
2. [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#package-manager) : utilizzato per importare ed esportare il contenuto mutabile dell’archivio.


#### Refactoring/Ottimizzazione

| Guida introduttiva | Revisione e refactoring del codice | Revisione di Dispatcher |
|---|---|---|
| <ul><li>[Configurazione sviluppo locale](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up)</li><li>[Configurazione del Dispatcher locale](https://video.tv.adobe.com/v/30602/)</li><li>[Compilare il codice utilizzando SDK API jar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en)</li><li>[Rivedere le linee guida per lo sviluppo dell’AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=en)<ul><li>Attività in background e processi con esecuzione prolungata</li><li>Utilità di pianificazione Sling</li><li>Utilizzo del flusso di ingresso e altro ancora</li></ul></li></ul> | <ul><li>Esegui il [Best Practices Analyzer (BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en) nell’ambiente di origine.[**Solo migrazione**]<ul><li>Considerazioni sulla struttura del progetto (basate su [Archetipo cloud](https://github.com/adobe/aem-project-archetype))<ul><li>Separazione di codice e contenuto (mutabile e immutabile)</li><li>[Definizioni di indice personalizzate](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=en)</li><li>[Modalità di esecuzione personalizzate](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html?lang=en)</li></ul></li></ul></li><li>Rivedere ed eseguire le modifiche necessarie</li><li>[Distribuisci](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en) nell’SDK locale</li><li>Eseguire il test del fumo tramite l’SDK per AEM</li></ul> | <ul><li>Revisione [Configurazioni del Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=en) per il refactoring</li><li>Utilizzare [Dispatcher Converter](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/dispatcher-transformation-utility-tools.html?lang=en) se del caso. [**Solo migrazione**]</li><li>I test possono essere eseguiti utilizzando [SDK di Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#prerequisites)</li></ul> |

>[!TIP]
> Clienti Assets : Rivedi e riesegui il factoring dei flussi di lavoro delle risorse tramite [Migrazione Asset Cloud](https://github.com/adobe/aem-cloud-migration) utensili


#### Implementazione/Go-Live

1. [Implementare in Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/git-integration.html?lang=en) Git
2. Eseguire il codice cliente tramite [Pipeline di qualità di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-quality-testing.html?lang=en)
3. [Implementazione nell’ambiente di sviluppo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging)
4. [**Solo migrazione**] Trasferimento dei contenuti tramite pacchetti o [Strumento Content Transfer](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md)(CTT)
5. Eseguire i cicli di prova raccomandati (fumo, controllo qualità e altro)
6. Promuovi alla pipeline di produzione di Cloud Manager
7. Convalida del test antifumo
8. Pubblicazione

<br>

### Post-pubblicazione

Nella fase di post-pubblicazione, devi assicurarti che i file temporanei vengano eliminati, esaminare le best practice per lo sviluppo continuo e gestire i registri.

>[!TIP]
> Sono disponibili strumenti per la risoluzione dei problemi relativi all’ambiente AEM as a Cloud Service
>1. [Console per sviluppatori](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html?lang=en)
>2. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html?lang=en)
>3. [Gestione dei registri](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs.html?lang=en)


<br>

### Strumenti e risorse

| Valutazione | Refactoring | Modernizzazione Experience Manager | Migrazione dei contenuti |
|------------|-------------|---------------------------------|-------------------|
| <ul><li>[Analisi delle best practice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en)</li></li> | <ul><li>[Plug-in esperienza unificata](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/refactoring-tools/unified-experience.html?lang=en)</li></ul> | <ul><li>[Modelli statici in modelli modificabili](https://opensource.adobe.com/aem-modernize-tools/pages/structure.html)</li><li>[Configurazioni di progettazione in criteri](https://opensource.adobe.com/aem-modernize-tools/pages/policy.html) <li>[Componenti di base in Componenti core](https://opensource.adobe.com/aem-modernize-tools/pages/component.html)</li><li>[Interfaccia utente classica in interfaccia utente touch](https://opensource.adobe.com/aem-modernize-tools/pages/all-in-one.html)</li></ul> | <ul><li>[Strumento trasferimento contenuti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=it)</li><li>[Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#contentmanagement)</li></ul> |

>[!NOTE]
> Per ulteriori informazioni, è possibile:
>1. [Contatta il team di supporto Experience Manager](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. Esplora [Community e forum Experienci Manager](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)

