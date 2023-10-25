---
title: Fase di preparazione
description: Scopri i passaggi necessari per assicurarti che l’installazione dell’AEM sia pronta per essere spostata sul cloud.
exl-id: 3bc8c037-d82a-4455-bce6-3c80c359a4ae
source-git-commit: a9aa82c8258e6a5f43680069c65518093c0baf8d
workflow-type: tm+mt
source-wordcount: '2066'
ht-degree: 7%

---

# Fase di preparazione {#readiness-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_planning"
>title="Pianificazione della transizione"
>abstract="Prima di iniziare la transizione a Cloud Service, prendi dimestichezza con AEM as a Cloud Service. Esamina le modifiche di rilievo apportate e le funzioni sostituite o dichiarate obsolete."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=it" text="Analisi delle best practice"

In questa fase del Percorso di Migrazione as a Cloud Service dell’AEM, imparerai a conoscere gli as a Cloud Service dell’AEM. Puoi rivedere le modifiche di rilievo introdotte e capire cosa serve per pianificare una migrazione di successo al cloud.

## Percorso affrontato finora {#story-so-far}

Il documento precedente, [Guida introduttiva al passaggio a AEM as a Cloud Service](/help/journey-migration/getting-started.md), illustra un elenco di fasi da seguire per la migrazione a AEM as a Cloud Service. Vengono inoltre illustrati i vantaggi della migrazione.

## Obiettivo {#objective}

Questo documento consente di comprendere quali fattori è necessario considerare per assicurarsi che l’installazione dell’AEM sia pronta per essere spostata sul cloud:

* Scopri le modifiche di rilievo e le funzioni obsolete
* Come pianificare la migrazione a AEM as a Cloud Service

## Revisione delle modifiche di rilievo apportate all’architettura as a Cloud Service dell’AEM {#notable-changes-in-aem-cloud-service-architecture}

AEM as a Cloud Service offre molte nuove funzioni e possibilità per gestire i tuoi progetti AEM.

Oltre a questi miglioramenti, sono state introdotte diverse differenze tra le installazioni on-premise di AEM e Managed Services Adobe, rispetto a AEM as a Cloud Service.

L’elenco delle voci nella tabella seguente è il sottoinsieme delle modifiche più rilevanti per la migrazione all’AEM as a Cloud Service. Puoi consultare l’elenco completo delle modifiche di rilievo [qui](/help/release-notes/aem-cloud-changes.md).

<table>
<thead>
  <tr>
    <th>Cosa è cambiato?</th>
    <th>Riferimento</th>
    <th>Takeaway chiave</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Separa i filtri mutabili e immutabili nei pacchetti corrispondenti</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/aem-cloud-changes.html?lang=it">Modifiche di rilievo as a Cloud Service dall’AEM</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html#mutable-vs-immutable">Struttura dei progetti AEM per AEM as a Cloud Service</a></td>
    <td>Un singolo pacchetto che può essere distribuito in AEM as a Cloud Service può avere pacchetti secondari, principalmente per contenere contenuti mutabili e immutabili separati nei propri pacchetti.</td>
  </tr>
  <tr>
    <td>Repo iniziale</td>
    <td><a href="https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language">Documentazione di Apache Sling RepoInit</a></td>
    <td>Gli script Repoinit rappresentano la best practice per creare strutture di nodi iniziali, utenti, gruppi o utenti di servizi. Poiché questi script possono essere indirizzati in base alla modalità di esecuzione e gestibili tramite la distribuzione del pacchetto di codice, forniscono molta flessibilità per eseguire le attività di inizializzazione dell’archivio.</td>
  </tr>
  <tr>
    <td>Non sono consentite modalità di esecuzione personalizzate</td>
    <td></td>
    <td>Sono supportate solo le modalità di esecuzione preconfigurate con AEM as a Cloud Service.<br>Quando vengono aggiunti ulteriori ambienti di sviluppo, tutti si collegano alla modalità di esecuzione "dev".</td>
  </tr>
  <tr>
    <td>L’esecuzione della pipeline di Cloud Manager è l’unico modo per distribuire</td>
    <td></td>
    <td>In AEM as a Cloud Service, l’accesso a /system/console non è consentito, pertanto tutte le configurazioni OSGi devono far parte del codice e devono essere distribuite come codice.<br>Le configurazioni OSGi sono disponibili in modalità di sola lettura per la visualizzazione tramite Console sviluppatori tramite Cloud Manager</td>
  </tr>
  <tr>
    <td>Gli agenti di replica vengono sostituiti da Sling Content Distribution</td>
    <td></td>
    <td>Il concetto di agente di replica è sostituito da Distribuzione dei contenuti di Sing. Se sono presenti personalizzazioni che utilizzano agenti di replica, è necessario riprogettarle.<br>Replica inversa non supportata</td>
  </tr>
  <tr>
    <td>CRX/DE e Gestione pacchetti</td>
    <td></td>
    <td>CRX/DE è consentito solo nell’ambiente di sviluppo.<br>Gestione pacchetti è accessibile su tutte le istanze di authoring, ma i pacchetti che verranno distribuiti devono contenere solo contenuto mutabile ( ad esempio: /content o /conf)</td>
  </tr>
  <tr>
    <td>CDN integrata e ottieni la tua CDN</td>
    <td></td>
    <td>AEM as a Cloud Service include la rete CDN per tutti gli ambienti ottimizzata per la maggior parte dei casi d’uso.<br>Se desideri impostare una tua rete CDN, devi inviare una richiesta all’assistenza Adobe affinché venga approvata.<br>Se approvata, la rete CDN punta a Fastly e non a istanze AEM in alcun ambiente.</td>
  </tr>
  <tr>
    <td>Processi con esecuzione prolungata</td>
    <td></td>
    <td>Evita processi con tempi di esecuzione lunghi, come pianificatori Sling o processi Cron, in quanto le istanze AEM in esecuzione nei contenitori possono andare e venire in qualsiasi momento.<br>Rifletti su queste funzionalità per scaricarle in Adobe Developer.</td>
  </tr>
  <tr>
    <td>Passa a operazioni asincrone</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/asynchronous-jobs.html?lang=en#configuring-asynchronous-msm-operations">Configurazione delle operazioni asincrone</a></td>
    <td>Per migliorare le prestazioni complessive degli ambienti, alcune operazioni vengono eseguite in modalità asincrona. I processi asincroni vengono messi in coda ed eseguiti quando sono disponibili risorse di sistema.</td>
  </tr>
  <tr>
    <td>Strategie di autenticazione e integrazione basate su token</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#the-server-to-server-flow">Generazione dei token di accesso per le API lato server</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication">Tutorial sull’autenticazione basata su token</a></td>
    <td>È comune che sistemi esterni all'AEM stiano cercando di eseguire operazioni HTTP all'interno dell'AEM.<br>L’approccio consigliato consiste nell’attuare le strategie qui descritte piuttosto che fare affidamento sulla creazione di username locali con password nell’AEM.</td>
  </tr>
  <tr>
    <td>I/O file/utilizzo disco</td>
    <td></td>
    <td>Non c’è garanzia di quanto spazio su disco sia allocato e le istanze nei contenitori vanno e vengono. Pertanto, non è consigliabile utilizzare operazioni di I/O dei file per scrivere o leggere dal disco collegato all'istanza AEM.</td>
  </tr>
  <tr>
    <td>Flusso di lavoro Aggiorna risorsa DAM</td>
    <td><a href="https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html?lang=en">Servizio Asset compute</a></td>
    <td>I passaggi di elaborazione dei contenuti multimediali che fanno parte del flusso di lavoro Risorsa di aggiornamento DAM ora sono sostituiti dal servizio Asset compute</td>
  </tr>
  <tr>
    <td>Metodi di caricamento delle risorse e passaggi supportati del processo di flusso di lavoro in AEM as a Cloud Service</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/developer-reference-material-apis.html?lang=en#post-processing-workflows-steps">Carica confronti API e passaggi del processo WF supportati</a></td>
    <td>In AEM as a Cloud Service, durante il caricamento o il download di una risorsa, questa viene trasmessa direttamente all’interno o all’esterno dell’archiviazione binaria. <br>Non tutti i passaggi del processo del flusso di lavoro sono supportati in AEMaaCS.</td>
  </tr>
  <tr>
    <td>Moduli di avvio per flusso di lavoro</td>
    <td></td>
    <td>Rimuovi dal codice tutti i moduli di avvio dei flussi di lavoro che attivano Flusso di lavoro per risorse di aggiornamento DAM predefinito o personalizzato. <br>Tutte le risorse caricate in AEM as a Cloud Service verranno elaborate dal servizio di elaborazione delle risorse. Per i passaggi personalizzati, consulta <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use.html?lang=en#post-processing-workflows"> Flussi di lavoro di post-elaborazione</a> su come impostare e configurare flussi di lavoro di post-elaborazione.</td>
  </tr>
  <tr>
    <td>Passaggi rappresentazione personalizzata</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use.html?lang=en">Profili di elaborazione</a></td>
    <td>Eventuali generazioni di rappresentazioni personalizzate, conversioni di immagini o codifiche video devono essere scaricate nel servizio di elaborazione delle risorse creando i profili di elaborazione corrispondenti.</td>
  </tr>
  <tr>
    <td>Ricerca e indicizzazione dei contenuti</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html?lang=en">Modifiche alla ricerca e all’indicizzazione dei contenuti</a></td>
    <td>Vi sono notevoli cambiamenti nell’elaborazione sottostante degli indici e nel momento in cui viene avviata.<br>Comprendi e riesegui il factoring degli indici Oak prima di gestirli nel codice distribuito.</td>
  </tr>
  <tr>
    <td>Non tutte le attività di manutenzione sono configurabili</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/maintenance.html?lang=en">Attività di manutenzione as a Cloud Service AEM</a></td>
    <td>Con AEM as a Cloud Service è possibile configurare solo alcune attività di manutenzione.</td>
  </tr>
  <tr>
    <td>Modifiche all’archivio di pubblicazione</td>
    <td></td>
    <td>Non sono consentite modifiche dirette all’archivio di pubblicazione, ad eccezione di quelle apportate in /home. Si consiglia sempre di distribuire eventuali modifiche apportate all’autore. Tutte le modifiche al codice e alla configurazione devono essere distribuite tramite la pipeline di Cloud Manager corrispondente.</td>
  </tr>
  <tr>
    <td>Configurazioni e caching del Dispatcher</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=en">Dispatcher nel cloud</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/caching.html?lang=en#other-content">Gestione cache<br></td>
    <td>Le configurazioni del Dispatcher devono seguire una struttura specifica.<br>Le configurazioni devono essere gestite come parte del codice e distribuite tramite la pipeline di Cloud Manager.</td>
  </tr>
  <tr>
    <td>Backup e ripristino</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/backup.html?lang=en">Backup e ripristino as a Cloud Service AEM</a></td>
    <td></td>
  </tr>
  <tr>
    <td>Modifiche all’autenticazione</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=it">Supporto IMS per AEM as a Cloud Service</td>
    <td>Se in precedenza utilizzavi l’integrazione SAML 2.0 sia per l’authoring che per la pubblicazione prima di passare al Cloud Service, la modifica principale è che AEM as a Cloud Service Author si integra solo con Adobe IMS. Tuttavia, il livello di pubblicazione as a Cloud Service dall’AEM può ancora utilizzare SAML o altre integrazioni di autenticazione. AEM as a Cloud Service offre il supporto per l’autenticazione IMS solo per gli utenti con privilegi di autore, amministratore e sviluppatore, L’autenticazione IMS non offre supporto per gli utenti finali esterni dei siti dei clienti, come i visitatori del sito.</td>
  </tr>
</tbody>
</table>

## Funzioni obsolete {#deprecated-features}

Adobe valuta costantemente le funzionalità dei prodotti per reinventare o sostituire nel tempo le funzioni meno recenti con alternative più moderne al fine di migliorare il valore complessivo per il cliente, tenendo comunque in considerazione la compatibilità con le versioni precedenti.

L’Adobe consiglia di consultare [Funzioni obsolete](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/deprecated-removed-features.html#deprecated-features) acquisire familiarità con le funzioni e le funzionalità contrassegnate come obsolete in Experience Manager as a Cloud Service. Scopri l’impatto sull’implementazione dell’AEM.

## Pianifica una revisione dell’installazione dell’AEM {#review-planning}

Dopo aver appreso le modifiche introdotte con AEM as a Cloud Service, è ora di iniziare a pianificare una revisione dell’installazione esistente. In questo modo è possibile misurare il livello di modifiche necessarie per spostarlo nel cloud.

La figura seguente mostra i passaggi chiave della fase di revisione:

![immagine](/help/journey-migration/assets/planning-phaseimg1.png)

Quindi, esplora in dettaglio il significato di ciascuno di questi passaggi.

### Valutazione della preparazione a Cloud Service {#assess-cloud-readiness}

Il primo passaggio consiste nel valutare se sei pronto a passare dalla versione esistente di AEM al Cloud Service e nel determinare le aree che richiedono il refactoring per essere compatibili con AEM as a Cloud Service.

Effettua una valutazione completa del tuo attuale codice sorgente AEM rispetto alle modifiche di rilievo e alle funzioni obsolete, per determinare il livello di impegno previsto nel percorso di transizione.

Il numero di risultati può influenzare direttamente le tempistiche e il successo complessivo del progetto. Pertanto, Adobe consiglia di scoprirne il più possibile in modo da poter pianificare la consegna. In alternativa, avvia le conversazioni in modo da poter riprogettare qualsiasi personalizzazione necessaria per essere in linea con le best practice as a Cloud Service per l’AEM.

**Best Practice Analyzer**

Puoi accelerare la valutazione eseguendo Best Practices Analyzer rispetto alla versione corrente dell’AEM. Per accelerare la pianificazione della valutazione è fondamentale avere una buona conoscenza del funzionamento.

Per saperne di più su come funziona, consulta [Best Practices Analyzer](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) documentazione.

**Creare un rapporto di valutazione della preparazione al cloud**

Il prossimo passo è la creazione di un rapporto basato su tutte le conoscenze acquisite finora. Puoi creare il rapporto generando i rapporti di Best Practices Analyzer dalle istanze Stage e Production, [quindi caricali in Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#readiness-phase-cam) per un rapporto digeribile di elementi actionable.

Un report tipico deve contenere i seguenti input:

* Documentazione che descrive il set di funzioni di una particolare installazione AEM
* Dettagli sulle configurazioni personalizzate e sul codice dell’AEM
* Configurazioni del Dispatcher di produzione
* Configurazioni CDN (se presenti)

**Socializzare il rapporto**

Una volta completati i rapporti di Best Practices Analyzer, condividili con i team pertinenti in modo da poter confermare i risultati e pianificare i passaggi successivi. A seconda delle preferenze, è inoltre possibile distribuire una versione stampata del report utilizzando [Anteprima di stampa](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#print-preview-cam).

### Esame della pianificazione delle risorse {#review-resource-planning}

Dopo aver stimato il livello di impegno necessario per passare al Cloud Service, è necessario identificare le risorse, creare un team e definire ruoli e responsabilità per il processo di transizione.

### Definizione dei KPI {#establish-kpis}

Se in precedenza non sono stati definiti indicatori di prestazioni chiave (KPI, Key Performance Indicators), si consiglia di stabilirli per l’implementazione dell’AEM, in modo da aiutare il team a concentrarsi su ciò che conta di più.

Consulta [Sviluppo di KPI](https://experienceleague.adobe.com/welcome/aem/part6.html) in questo modo puoi imparare a scegliere i giusti KPI per gli obiettivi aziendali.

## Passaggio successivo {#what-is-next}

Una volta compresa la portata delle modifiche necessarie per passare a AEM as a Cloud Service, è il momento di [Prepara il codice e il contenuto cloud](/help/journey-migration/implementation.md) prima di eseguire effettivamente la migrazione.

## Risorse aggiuntive {#additional-resources}

* [Guida introduttiva di Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/using-cam/getting-started-cam.md) - Una guida completa su come utilizzare Cloud Acceleration Manager per velocizzare il passaggio al cloud.
* [AEM as a Cloud Service: Introduzione, architettura e pensiero diverso](https://experienceleague.adobe.com/?launch=ExperienceManager-D-1-2021.1.migration&amp;recommended=ExperienceManager-D-1-2021.1.migration&amp;lang=en#dashboard/learning)
* [AEM a Home Cloud Service](/help/overview/home.md) - Panoramica della documentazione di Experience Manager as a Cloud Service.
* [Panoramica di AEM as a Cloud Service](/help/overview/home.md) : questa guida fornisce una panoramica di Experience Manager as a Cloud Service, con un’introduzione, terminologia e architettura.
* [Percorso di onboarding](/help/journey-onboarding/overview.md): questa guida fornisce un riepilogo di come iniziare a utilizzare Experience Manager as a Cloud Service, incluso come ottenere l’accesso e configurare il team.
