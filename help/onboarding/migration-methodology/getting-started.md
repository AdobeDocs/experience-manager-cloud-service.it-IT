---
title: Migrazione a  Experience Manager come Cloud Service
description: Migrazione a  Experience Manager come Cloud Service
translation-type: tm+mt
source-git-commit: dc2d529c6bbdb4e0fd963021e40bc333b321c95c
workflow-type: tm+mt
source-wordcount: '2117'
ht-degree: 8%

---


# Migrazione ad Adobe Experience Manager come Cloud Service {#Overview}

>[!CONTEXTUALHELP]
>id="aemcloud_migration_overview"
>title="Migrazione a AEM come servizio cloud"
>abstract="Illustra l&#39;approccio graduale consigliato per la transizione dei clienti da diverse installazioni di Experienci Manager  a  Experience Manager come Cloud Service e aiuta i clienti esistenti a fornire esperienze continue e connesse"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en" text="Novità e differenze"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en" text="Introduzione ad AEM as a Cloud Service."

Adobe Experience Manager (AEM) come Cloud Service offre una base ri-architettata per  Experience Manager, basata su un&#39;infrastruttura basata su container, uno sviluppo basato sulle API e un processo DevOps guidato, che consente ai professionisti del marketing e agli sviluppatori di essere sempre al passo con le innovazioni della gestione dell&#39;esperienza dei clienti.

Il Cloud Service unisce funzionalità avanzate ed estensibilità di Adobe Experience Manager con l&#39;agilità della moderna architettura nativa del cloud, consentendo ai marchi di soddisfare la sempre crescente domanda dei consumatori.

Questo unico pager delinea l&#39;approccio graduale consigliato ai clienti di transizione da diverse distribuzioni di Experienci Manager  a  Experience Manager come Cloud Service e aiuta i clienti esistenti a fornire esperienze connesse e continue su questa moderna piattaforma appositamente progettata per la gestione dell&#39;esperienza.

<!-- It primarily focuses on:
* Getting Started with Adobe Experience Manager as a Cloud Service
* Developer Journey in Adobe Experience Manager as a Cloud Service
* Moving to Adobe Experience Manager as a Cloud Service -->

<br>

## Guida introduttiva ad Adobe Experience Manager come Cloud Service {#getting-started}

| Che cosa è diverso? | Panoramica dell’architettura |
|--------------------------|--------------------------|
| <ul><li>[Architettura moderna](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html)</li><li>[Aggiornamenti automatici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/aem-version-updates.html?lang=en#aem-version-updates)</li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)</li><li>[Risorse, servizi](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/asset-microservices-overview.html)</li><li>[Binari con accesso diretto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/asset-microservices-overview.html?lang=en#asset-upload-with-direct-binary-access)</li><li>[Separazione di codice e contenuto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=en#developing)</li><li>[Replica come servizio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/replication.html?lang=en)</li><li>[Admin Console, Group/User Membership e ACL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html)</li></ul> | <ul><li>[Introduzione all&#39;architettura AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-architecture.html?lang=en#underlying-technology)</li><li>[Stack ambiente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html)</li><li>[Livello di authoring](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[Pubblica livello](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-author-publish.html?lang=en#underlying-technology)</li><li>[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#content-delivery)</li><li>[CDN](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/cdn.html?lang=en#content-delivery) </li><li>[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)  (CI/CD)</li><li>[Gestione identità ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#onboarding-users-in-admin-console) tramite  [Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html)</li><li>[ Asset compute](https://experienceleague.adobe.com/docs/asset-compute/using/home.html)</li></ul> |

![AEM as a Cloud Service: architettura runtime](/help/core-concepts/assets/concepts-03.png "AEM as a Cloud Service - Architettura runtime")

<br>

## Percorso sviluppatore in Adobe Experience Manager come Cloud Service {#developer-journey}

### Sviluppo

Le basi dello sviluppo del codice sono simili in Adobe Experience Manager come Cloud Service rispetto alle soluzioni Adobe Experience Manager On Premise e Managed Services.

Gli sviluppatori scrivono il codice e lo sottopongono a test localmente, che vengono quindi inviati ad Adobe Experience Manager remoto come ambienti di Cloud Service.

Consultate le risorse di supporto autonomo sull&#39;implementazione per  Experience Manager come Cloud Service per apprendere come personalizzare il Experience Manager di  come distribuzione di Cloud Service.

| Impostazione sviluppo locale | Cose da sapere prima di iniziare |
|-----------|------------|
| <ol><li>Leggi la documentazione [Adobe Experience Manager SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing) per saperne di più.</li><li>Per informazioni su come installare Dispatcher SDK, vedere [Install Dispatcher SDK](https://video.tv.adobe.com/v/30601?captions=ita)</li><li>Per informazioni su come configurare Dispatcher SDK, vedere [Configurare Dispatcher SDK](https://video.tv.adobe.com/v/30602?captions=ita)</li><li>Leggi la documentazione [Local Development Setup](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up) per saperne di più</li><li>Configurazione dell&#39;accesso al Experience Manager  [guida dettagliata](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en#accessing)</li></ol> | <ol><li>[Nozioni di base sullo sviluppo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing)</li><li>[Linee guida per lo sviluppo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#developing)</li><li>[Informazioni  struttura del progetto Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=en#developing)</li><li>[Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)</li><li>[Blueprint Digital Foundation](https://solutionpartners.adobe.com/content/dam/spp_assets/restricted/community/community_31/digital_foundation_best_practices_and_documentation.zip)</li><li>[Sistema di stili](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/style-system.html?lang=en#authoring)</li><li>[Sovrapposizioni](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/overlays.html?lang=en#developing)</li><li>[ Experience Manager come riferimento API di Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/)</li></ol> |

>[!TIP]
> Vedere l&#39;esercitazione su come [Sviluppare e distribuire WKND sull&#39;SDK del Experience Manager  locale](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en)

### Distribuzione

Gli sviluppatori scrivono il codice e lo sottopongono a test localmente, che vengono quindi spinti AEM remoti come ambienti di Cloud Service.

Cloud Manager, uno strumento opzionale per la distribuzione dei contenuti per Managed Services, è richiesto. Questo è ora l&#39;unico meccanismo per distribuire il codice da AEM come ambienti di Cloud Service.

Consulta le risorse di supporto autonomo su come configurare e distribuire in AEM come ambienti di Cloud Service.

1. [Configurare le pipeline di CM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager)
   * Pipeline di produzione
   * Tubazioni non di produzione e di qualità del codice
2. [Distribuisci codice](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#using-cloud-manager)
3. [Informazioni sui risultati del test](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/overview-test-results.html?lang=en#using-cloud-manager)
4. **Accesso ai registri**
   * [tramite interfaccia di CM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=en#using-cloud-manager)
   * [tramite  Adobe i/o cli](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
5. [Operazioni e manutenzione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/home.html?lang=en)
   * [Configurazione OSGI](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#deploying)
   * [Backup e ripristino](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/backup.html?lang=en)

>[!TIP]
> Vedere l&#39;esercitazione su come [distribuire WKND a  Experience Manager Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/develop-wknd-tutorial.html?lang=en)

### Guida e risorse

1. [Suggerimenti e trucchi per il debug](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=en#debugging-aem-as-a-cloud-service)
2. [Console per sviluppatori](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html?lang=en#debugging)
3. [CRXDE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/crxde-lite.html?lang=en#debugging) (Disponibile solo negli ambienti SDK locali e  Experience Manager Cloud Dev)
4. [Registri e registrazioni](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)
   * [Registri](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging)  CM (testing di unità build, scansione del codice, immagine build, implementazione)
   * [ registri](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs.html?lang=en#debugging)  di Experience Manager Cloud Service (aemerror, aemaccess, aemrequest, aemdispatcher, httpderror, httpaccess)
   * Registri SDK locali (in host:port/crx-quickstart/logs)

>[!NOTE]
> Per ulteriore assistenza, potete effettuare le seguenti operazioni:
>1. [Contatta il team di supporto del Experience Manager ](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. Esplora [ Community e forum di Experience Manager](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)


<br>

## Spostamento in Adobe Experience Manager come Cloud Service {#move-to-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_move_to_cloud"
>title="Passaggio ad Adobe Experience Manager come Cloud Service"
>abstract="Questo unico pager delinea l&#39;approccio graduale consigliato ai clienti di transizione da diverse distribuzioni di Experienci Manager  a  Experience Manager come Cloud Service e aiuta i clienti esistenti a fornire esperienze connesse e continue su questa moderna piattaforma appositamente progettata per la gestione dell&#39;esperienza."

**Experience Manager come Cloud Service fornisce una base tecnologica scalabile, sicura e agile per  siti e risorse di Experience Manager, consentendo agli esperti di marketing e all&#39;IT di concentrarsi sulla fornitura di esperienze di impatto su larga scala.**

Con  Experience Manager come Cloud Service, i team possono concentrarsi sull&#39;innovazione invece di pianificare gli aggiornamenti dei prodotti. Le nuove funzionalità dei prodotti vengono testate in maniera approfondita e distribuite ai team senza interruzioni, in modo che possano sempre accedere all’applicazione all’avanguardia.

Il percorso di transizione verso Cloud Service prevede tre fasi: pianificazione, esecuzione e post-pubblicazione.
Per una transizione corretta e senza problemi, è necessario garantire una pianificazione adeguata e attenersi alle best practice descritte nella presente guida.

La figura seguente mostra un’illustrazione del percorso consigliato per la transizione a Cloud Service.

![immagine](/help/move-to-cloud-service/assets/home-img1.png)

<br>

### Pianificazione

Prima di iniziare il percorso di transizione verso il Cloud Service, è necessario acquisire familiarità con  Experience Manager come Cloud Service e rivedere le modifiche rilevanti apportate al  e rivedere anche le funzioni sostituite o obsolete.

<table>
<tr>
<td>Individuazione e valutazione dei progetti</td>
<td><ul><li>Fare riferimento a <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=en">Notevoli modifiche al Experience Manager  come Cloud Service</a> per comprendere le importanti differenze tra Adobe Experience Manager come Cloud Service e  Experience Manager 6.x.</li><li>Fare riferimento a <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/deprecated-removed-features.html?lang=en#deprecated-features">Funzioni obsolete</a> per ulteriori informazioni sulle funzioni e sulle funzionalità contrassegnate come obsolete.</li><li>[Solo per migrazioni Cloud Service] Valutazione della prontezza del Cloud Service: Eseguire l' <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration">Best Practices Analyzer(BPA)</a> sull'ambiente di origine </li><li>Completare una valutazione a fronte di modifiche rilevanti e funzionalità obsolete nel  Experience Manager CS</li></ul></td>
</tr>
<tr>
<td>Recensione</td>
<td><ul><li>In base all'individuazione, eseguire la stima dello sforzo e gli esercizi di risorse</li></ul></td>
</tr>
<tr>
<td>Misura</td>
<td><ul><li><a href="https://experienceleague.adobe.com/welcome/aem/part6.html">Stabilire KPI</a> progetto, criteri di successo e timeline del progetto</li></ul></td>
</tr>
</table>

>[!NOTE]
>Il report Best Practices Analyzer velocizza il processo di stima del tempo e dei costi necessari per passare al AEM come Cloud Service, fornendo informazioni che altrimenti dovrebbero essere raccolte e valutate manualmente.


<br>

### Esecuzione

Prima di avviare la fase di esecuzione di un progetto, è necessario essere collegati al Cloud Service. Devi anche familiarizzare con Cloud Manager. Questo è il meccanismo per distribuire il codice del progetto a un&#39;istanza di Experience Manager Cloud Service .

Cloud Manager consente alle organizzazioni di gestire autonomamente  Experience Manager nel Cloud. Include un&#39;integrazione continua e un framework di consegna continua ([CI/CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/overview/ci-cd-pipeline.html?lang=en#overview)) che consente ai team IT e ai partner di implementazione di accelerare la fornitura di personalizzazioni o aggiornamenti senza compromettere le prestazioni o la sicurezza.

#### Migrazione dei contenuti

1. [Strumento](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration)  di trasferimento dei contenuti: utilizzato per spostare il contenuto esistente da un&#39;istanza di AEM di origine (locale o AMS) all&#39;istanza di Cloud Service AEM di destinazione.
2. [Gestione](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#package-manager)  pacchetti: utilizzato per l&#39;importazione e l&#39;esportazione di contenuto variabile del repository.


#### Reagisci/ottimizza

| Guida introduttiva | Codice revisione e refattore | Recensione del dispatcher |
|---|---|---|
| <ul><li>[Configurazione sviluppatore locale](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=en#local-development-environment-set-up)</li><li>[Impostazione dispatcher locale](https://video.tv.adobe.com/v/30602/?captions=ita)</li><li>[Compilare il codice utilizzando l&#39;SDK API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing)</li><li>[Rivedi AEM linee guida per sviluppatori](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#developing)<ul><li>Attività in background e processi con esecuzione prolungata</li><li>Programmatori Sling</li><li>Utilizzo flusso di ingresso e altro</li></ul></li></ul> | <ul><li>Eseguire l&#39; [Best Practices Analyzer(BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration) sull&#39;ambiente di origine.[**Solo migrazione**]<ul><li>Considerazioni sulla struttura del progetto (basate su [Cloud Archetype](https://github.com/adobe/aem-project-archetype))<ul><li>Separazione del codice e del contenuto (variabile e non modificabile)</li><li>[Definizioni indice personalizzate](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#indexing)</li><li>[Custom runmode](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#runmodes)</li></ul></li></ul></li><li>Revisione ed esecuzione delle modifiche necessarie</li><li>[Implementazione ](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en) sull’SDK locale</li><li>Eseguire test del fumo tramite AEM SDK</li></ul> | <ul><li>Rivedere le [configurazioni del dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#local-validation-of-dispatcher-configuration) per il refactoring</li><li>Sfruttare lo strumento [Dispatcher Converter](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/dispatcher-transformation-utility-tools.html?lang=en#introduction-dispatcher), se appropriato. [**Solo migrazione**]</li><li>La verifica può essere eseguita utilizzando [Dispatcher SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html?lang=en#prerequisites)</li></ul> |

>[!TIP]
> Clienti Assets: Verifica e ridefinizione dei flussi di lavoro delle risorse tramite [strumenti di migrazione di Asset Cloud](https://github.com/adobe/aem-cloud-migration)


#### Distribuzione/Go-Live

1. [Distribuisci a Cloud ](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html?lang=en#managing-code) Managergit
2. Eseguire il codice cliente tramite la [pipeline di qualità di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use)
3. [Distribuisci in ambiente di sviluppo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/build-and-deployment.html?lang=en#debugging)
4. [**Migrazione**] soloTrasferimento dei contenuti tramite pacchetti o  [Content Transfer Tool](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md) (CTT)
5. Eseguire cicli di prova raccomandati (fumo, QA e altro)
6. Promozione alla pipeline di produzione di Cloud Manager
7. Convalida del test di fumo
8. Go-Live

<br>

### Post Go-Live

Nella fase di post-pubblicazione, devi assicurarti che i file temporanei vengano eliminati, esaminare le best practice per lo sviluppo continuo e gestire i registri.

>[!TIP]
> Sono disponibili strumenti per la risoluzione dei AEM come ambienti di Cloud Service
>1. [Console per sviluppatori](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=en#aem-as-a-cloud-service-development-tools)
>2. [CRX/DE Lite](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/crxde-lite.html?lang=en#debugging)
>3. [Gestione dei registri](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html?lang=en#using-cloud-manager)


<br>

### Strumenti e risorse

| Valutazione | Refactoring | Modernizzazione  Experience Manager | Migrazione dei contenuti |
|------------|-------------|---------------------------------|-------------------|
| <ul><li>[Best practice Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration)</li></li> | <ul><li>[Plugin esperienza unificata](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#refactoring-tools)</li></ul> | <ul><li>[Modelli statici in modelli modificabili](https://opensource.adobe.com/aem-modernize-tools/pages/tools/page-structure.html)</li><li>[Configurazioni di progettazione in policy](https://opensource.adobe.com/aem-modernize-tools/pages/tools/policy-importer.html) <li>[Componenti di base in componenti core](https://opensource.adobe.com/aem-modernize-tools/pages/tools/component.html)</li><li>[Interfaccia classica in interfaccia touch](https://opensource.adobe.com/aem-modernize-tools/pages/tools/dialog.html)</li></ul> | <ul><li>[Strumento Content Transfer (Trasferimento contenuti) ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#cloud-migration)</li><li>[Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#contentmanagement)</li></ul> |

>[!NOTE]
> Per ulteriore assistenza, potete effettuare le seguenti operazioni:
>1. [Contatta il team di supporto del Experience Manager ](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=en)
>2. Esplora [ Community e forum di Experience Manager](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/ct-p/adobe-experience-manager-community)

