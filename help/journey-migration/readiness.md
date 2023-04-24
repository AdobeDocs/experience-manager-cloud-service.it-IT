---
title: Fase di preparazione
description: Scopri i passaggi necessari per assicurarti che l’installazione AEM sia pronta per essere spostata nel cloud
exl-id: 3bc8c037-d82a-4455-bce6-3c80c359a4ae
source-git-commit: 13cb8ae059f0a77e517d2e64eae96a08f88ac075
workflow-type: tm+mt
source-wordcount: '2079'
ht-degree: 8%

---

# Fase di preparazione {#readiness-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_planning"
>title="Pianificazione della transizione"
>abstract="Prima di iniziare il percorso di transizione verso Cloud Service, devi acquisire familiarità con AEM as a Cloud Service, esaminare le modifiche rilevanti apportate al servizio e rivedere inoltre le funzioni che sono state sostituite o dichiarate obsolete."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=it" text="Analisi delle best practice"

In questa fase del AEM Percorso di migrazione as a Cloud Service, acquisisci familiarità con AEM as a Cloud Service, esamina le modifiche di rilievo introdotte e illustra gli elementi necessari per pianificare una migrazione con successo al cloud.

## Percorso affrontato finora {#story-so-far}

Il documento precedente, [Guida introduttiva al passaggio a AEM as a Cloud Service](/help/journey-migration/getting-started.md), delinea un elenco delle fasi da seguire per migrare a AEM as a Cloud Service, nonché i vantaggi di farlo.

## Obiettivo {#objective}

Questo documento ti aiuta a capire quali fattori devi considerare per essere sicuro che l’installazione di AEM sia pronta per essere spostata nel cloud:

* Scopri le modifiche di rilievo e le funzioni obsolete
* Come pianificare la migrazione a AEM as a Cloud Service

## Rivedi le modifiche di rilievo nell’architettura as a Cloud Service AEM {#notable-changes-in-aem-cloud-service-architecture}

AEM as a Cloud Service include molte nuove funzioni e opportunità per gestire i progetti AEM.

Oltre a questi miglioramenti, sono state introdotte diverse differenze tra le installazioni on-premise di AEM e Adobe Managed Services, rispetto a AEM as a Cloud Service.

L’elenco degli elementi nella tabella seguente è il sottoinsieme delle modifiche più rilevanti per una migrazione a AEM as a Cloud Service. È possibile consultare l’elenco completo delle modifiche di rilievo [qui](/help/release-notes/aem-cloud-changes.md).

<table>
<thead>
  <tr>
    <th>Cosa è cambiato?</th>
    <th>Riferimento</th>
    <th>Aree principali</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Filtri separabili e immutabili nei pacchetti corrispondenti</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=en">Modifiche di rilievo AEM as a Cloud Service</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html#mutable-vs-immutable">AEM struttura del progetto per AEM as a Cloud Service</a></td>
    <td>Un singolo pacchetto che può essere distribuito in AEM as a Cloud Service può avere pacchetti secondari, principalmente per contenere contenuti mutabili e immutabili separati nei propri pacchetti.</td>
  </tr>
  <tr>
    <td>Inizio repository</td>
    <td><a href="https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language">Documentazione di Apache Sling RepoInit</a></td>
    <td>Gli script di reindirizzamento sono la best practice per creare strutture di nodo iniziali, utenti, gruppi o utenti di servizi. Poiché questi script possono essere indirizzati in modalità di esecuzione e gestibili tramite la distribuzione del pacchetto di codice, offrono molta flessibilità per eseguire le attività di inizializzazione dell'archivio.</td>
  </tr>
  <tr>
    <td>Le modalità di esecuzione personalizzate non sono consentite</td>
    <td></td>
    <td>Sono supportate solo le modalità di esecuzione fornite con AEM as a Cloud Service.<br>Quando vengono aggiunti ulteriori ambienti di sviluppo, tutti si collegano alla modalità di esecuzione "dev".</td>
  </tr>
  <tr>
    <td>L’esecuzione della pipeline di Cloud Manager è l’unico modo per distribuire</td>
    <td></td>
    <td>In AEM as a Cloud Service, l'accesso a /system/console non è consentito, pertanto tutte le configurazioni OSGi devono far parte del codice e devono essere distribuite come codice.<br>Le configurazioni OSGi sono disponibili in modalità di sola lettura per la visualizzazione tramite Developer Console tramite Cloud Manager</td>
  </tr>
  <tr>
    <td>Gli agenti di replica sono sostituiti da Distribuzione dei contenuti Sling</td>
    <td></td>
    <td>Il concetto dell’agente di replica viene sostituito da Distribuzione dei contenuti di Sing. Se esistono personalizzazioni che sfruttano gli agenti di replica, è necessario riprogettarle.<br>La replica inversa non è supportata</td>
  </tr>
  <tr>
    <td>CRX/DE e Package Manager</td>
    <td></td>
    <td>CRX/DE è consentito solo nell'ambiente di sviluppo.<br>Package Manager è accessibile su tutte le istanze dell’autore, ma i pacchetti che verranno distribuiti devono contenere solo contenuti modificabili (ad esempio: /content o /conf)</td>
  </tr>
  <tr>
    <td>CDN integrato e Ottieni la tua CDN</td>
    <td></td>
    <td>AEM as a Cloud Service include la rete CDN per tutti gli ambienti ottimizzata per la maggior parte dei casi d’uso.<br>Se desideri configurare la tua CDN, devi inviare una richiesta al supporto Adobe affinché venga approvata.<br>Se viene approvato, la rete CDN punta a Flast e non a AEM istanze in alcun ambiente.</td>
  </tr>
  <tr>
    <td>Processi lunghi</td>
    <td></td>
    <td>Evita di eseguire processi con esecuzione prolungata, ad esempio programmi Sling o lavori Cron, in quanto le istanze AEM in esecuzione nei contenitori possono andare e venire in qualsiasi momento.<br>Ripensa queste funzionalità per scaricarle nell’Adobe I/O.</td>
  </tr>
  <tr>
    <td>Passa alle operazioni asincrone</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/asynchronous-jobs.html?lang=en#configuring-asynchronous-msm-operations">Configurazione delle operazioni asincrone</a></td>
    <td>Per migliorare le prestazioni complessive degli ambienti, alcune operazioni vengono eseguite in modalità asincrona. I processi asincroni verranno messi in coda ed eseguiti quando sono disponibili risorse di sistema.</td>
  </tr>
  <tr>
    <td>Strategie di autenticazione e integrazione basate su token</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/generating-access-tokens-for-server-side-apis.html?lang=en#the-server-to-server-flow">Generazione di token di accesso per API lato server</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication">Tutorial sull’autenticazione basata su token</a></td>
    <td>È comune che i sistemi esterni a AEM stiano tentando di eseguire operazioni HTTP all'interno di AEM.<br>L’approccio consigliato consiste nell’implementare le strategie descritte qui anziché affidarsi alla creazione di nomi utente locali con password in AEM.</td>
  </tr>
  <tr>
    <td>File IO / Utilizzo disco</td>
    <td></td>
    <td>Poiché non è garantita la quantità di spazio su disco allocato e le istanze nei contenitori vanno e vengono, non è consigliabile utilizzare le operazioni di I/O file per scrivere o leggere dal disco collegato all'istanza AEM.</td>
  </tr>
  <tr>
    <td>Flusso di lavoro Aggiorna risorsa DAM</td>
    <td><a href="https://experienceleague.adobe.com/docs/asset-compute/using/introduction.html?lang=en">Servizio Asset compute</a></td>
    <td>I passaggi di elaborazione dei file multimediali che fanno parte del flusso di lavoro Risorsa di aggiornamento DAM vengono ora sostituiti dal servizio Asset compute</td>
  </tr>
  <tr>
    <td>Metodi di caricamento delle risorse e passaggi del processo di flusso di lavoro supportati in AEM as a Cloud Service</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/developer-reference-material-apis.html?lang=en#post-processing-workflows-steps">Caricare confronti API e passaggi di processo WF supportati</a></td>
    <td>In AEM as a Cloud Service, durante il caricamento o il download di una risorsa, la risorsa viene trasmessa in streaming direttamente all’interno o all’esterno dell’archiviazione binaria.</br>Non tutti i passaggi del processo del flusso di lavoro sono supportati in AEMaaCS.</td>
  </tr>
  <tr>
    <td>Moduli di avvio per flusso di lavoro</td>
    <td></td>
    <td>Rimuovi dal codice tutti i moduli di avvio del flusso di lavoro che attivano OOTB o il flusso di lavoro personalizzato Aggiorna risorsa DAM .</br>Tutte le risorse caricate in AEM as a Cloud Service verranno elaborate dal servizio di elaborazione delle risorse. Per i passaggi personalizzati, fai riferimento a <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-microservices-configure-and-use.html?lang=en#post-processing-workflows"> Flussi di lavoro post-elaborazione</a> su come impostare e configurare flussi di lavoro di post-elaborazione.</td>
  </tr>
  <tr>
    <td>Passaggi di rendering personalizzati</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/manage/asset-microservices-configure-and-use.html?lang=en#manage">Profili di elaborazione</a></td>
    <td>Qualsiasi generazione di rendering personalizzata, conversioni di immagini o codifiche video deve essere scaricata nel servizio Asset Processing (Elaborazione risorse) creando i profili di elaborazione corrispondenti.</td>
  </tr>
  <tr>
    <td>Ricerca e indicizzazione dei contenuti</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en">Modifiche alla funzione di ricerca e indicizzazione dei contenuti</a></td>
    <td>L'elaborazione sottostante degli indici e quando viene attivata sono state apportate modifiche considerevoli.<br>Comprendere completamente e reimpostare gli indici Oak prima di gestirli nel codice che distribuirai.</td>
  </tr>
  <tr>
    <td>Non tutte le attività di manutenzione sono configurabili</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/maintenance.html?lang=en">AEM attività di manutenzione as a Cloud Service</a></td>
    <td>È possibile configurare solo alcune attività di manutenzione con AEM as a Cloud Service.</td>
  </tr>
  <tr>
    <td>Modifiche all’archivio di pubblicazione</td>
    <td></td>
    <td>Non sono consentite modifiche dirette all’archivio di pubblicazione, eccetto quelle in /home. È sempre consigliabile apportare le modifiche all’autore e distribuirle. Tutte le modifiche al codice e alla configurazione devono essere distribuite tramite la pipeline di Cloud Manager corrispondente.</td>
  </tr>
  <tr>
    <td>Configurazioni del Dispatcher e memorizzazione in cache</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#content-delivery">Dispatcher nel cloud</a><br><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/caching.html?lang=en#other-content">Gestione cache<br></td>
    <td>Le configurazioni del Dispatcher devono seguire una struttura specifica.<br>Le configurazioni devono essere gestite come parte del codice e distribuite tramite la pipeline di Cloud Manager.</td>
  </tr>
  <tr>
    <td>Backup e ripristino</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/backup.html?lang=en">Backup e ripristino as a Cloud Service AEM</a></td>
    <td></td>
  </tr>
  <tr>
    <td>Modifiche all'autenticazione</td>
    <td><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=it">Supporto IMS per AEM as a Cloud Service</td>
    <td>Se in precedenza utilizzavi l’integrazione SAML 2.0 sia per l’authoring che per la pubblicazione prima di passare al Cloud Service, la modifica principale è che AEM Author as a Cloud Service si integra solo con Adobe IMS. Tuttavia, AEM livello di pubblicazione as a Cloud Service può ancora sfruttare SAML o altre integrazioni di autenticazione. AEM as a Cloud Service offre il supporto per l’autenticazione IMS solo per gli utenti con privilegi di autore, amministratore e sviluppatore, L’autenticazione IMS non offre supporto per gli utenti finali esterni dei siti dei clienti, come i visitatori del sito.</td>
  </tr>
</tbody>
</table>

## Funzioni obsolete {#deprecated-features}

Adobe valuta costantemente le funzionalità dei prodotti per reinventare o sostituire nel tempo le funzioni meno recenti con alternative più moderne al fine di migliorare il valore complessivo per il cliente, tenendo comunque in considerazione la compatibilità con le versioni precedenti.

Si consiglia di consultare la [Funzioni obsolete](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/deprecated-removed-features.html#deprecated-features) per acquisire familiarità con le funzioni e le funzionalità contrassegnate come obsolete in Experience Manager as a Cloud Service e conoscere l’impatto sulla distribuzione AEM.

## Pianificare una revisione dell&#39;installazione AEM {#review-planning}

Una volta che ti sei abituato alle modifiche introdotte con AEM as a Cloud Service, è il momento di iniziare a pianificare una revisione dell&#39;installazione esistente, al fine di misurare il livello di modifiche necessarie per spostarla nel cloud.

La figura seguente illustra i passaggi chiave della fase di revisione:

![immagine](/help/journey-migration/assets/planning-phaseimg1.png)

Ora esploreremo nel dettaglio cosa significa ciascuno di questi passaggi.

### Valutazione della preparazione a Cloud Service {#assess-cloud-readiness}

Il primo passo è quello di valutare la vostra disponibilità a passare dalla versione AEM esistente al Cloud Service e determinare le aree che richiederanno il refactoring per essere compatibili con AEM as a Cloud Service.

Per determinare il livello di sforzo previsto nel percorso di transizione, dovrai effettuare una valutazione completa del codice sorgente AEM corrente rispetto alle modifiche di rilievo e alle funzioni obsolete.

Il numero di risultati influenzerà direttamente le tempistiche e il successo complessivo del progetto. Pertanto, si consiglia di individuare il più possibile la pianificazione della consegna o di avviare le conversazioni necessarie per riprogettare le personalizzazioni necessarie per essere in linea con AEM best practice as a Cloud Service.

**Best practice Analyzer**

Puoi accelerare la valutazione eseguendo Best Practices Analyzer (Analisi delle best practice) rispetto alla versione corrente AEM. Avere una buona comprensione di come funziona è fondamentale per accelerare la vostra pianificazione della valutazione.

Per saperne di più sul funzionamento, consulta la sezione [Analisi delle best practice](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) documentazione.

**Creare un rapporto di valutazione della preparazione al cloud**

Il passo successivo è la creazione di una relazione basata su tutte le conoscenze finora acquisite. A tale scopo, è possibile generare rapporti di Best Practices Analyzer dalle istanze Stage e Production, [quindi caricarli in Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#readiness-phase-cam) per un rapporto digeribile sugli elementi utilizzabili.

Un rapporto tipico deve contenere i seguenti dati:

* Documentazione che descrive in dettaglio il set di funzioni della vostra specifica installazione AEM
* Dettagli sulle configurazioni e sul codice personalizzati AEM
* Configurazioni del Dispatcher di produzione
* Configurazioni CDN (se presenti)

**Socializzare il rapporto**

Una volta completati i rapporti di Best Practices Analyzer, condividili con i team interessati per confermare i risultati e pianificare i passaggi successivi. A seconda delle preferenze, è anche possibile distribuire una versione stampata del rapporto utilizzando [Anteprima di stampa](/help/journey-migration/cloud-acceleration-manager/using-cam/cam-readiness-phase.md#print-preview-cam).

### Esame della pianificazione delle risorse {#review-resource-planning}

Dopo aver stimato il livello di impegno necessario per passare al Cloud Service, devi identificare le risorse, creare un team e mappare ruoli e responsabilità per il processo di transizione.

### Definizione dei KPI {#establish-kpis}

Se in precedenza non sono stati definiti indicatori prestazioni chiave (KPI, Key Performance Indicators), è consigliabile stabilire KPI per l’implementazione di AEM per aiutare il team a concentrarsi su ciò che conta di più.

Vedi [Sviluppo di KPI](https://guided.adobe.com/welcome/aem/part6.html) per scoprire come scegliere i giusti KPI per gli obiettivi aziendali.

## Passaggio successivo {#what-is-next}

Una volta compreso l&#39;ambito delle modifiche necessarie per passare a AEM as a Cloud Service, è il momento di [Preparare il codice e il cloud dei contenuti](/help/journey-migration/implementation.md) prima di eseguire effettivamente la migrazione.

## Risorse aggiuntive {#additional-resources}

* [Guida introduttiva di Cloud Acceleration Manager](/help/journey-migration/cloud-acceleration-manager/using-cam/getting-started-cam.md) - Guida completa sull’utilizzo di Cloud Acceleration Manager per velocizzare il passaggio al cloud
* [AEM as a Cloud Service: Introduzione, architettura e pensiero diversi](https://experienceleague.adobe.com/?launch=ExperienceManager-D-1-2021.1.migration&amp;recommended=ExperienceManager-D-1-2021.1.migration&amp;lang=en#dashboard/learning)
* [AEM una casa di Cloud Service](/help/overview/home.md) - Per una panoramica della documentazione as a Cloud Service di Experience Manager, inizia qui.
* [Panoramica AEM as a Cloud Service](/help/overview/home.md) - Questa guida fornisce una panoramica di Experience Manager as a Cloud Service, con un’introduzione, una terminologia e un’architettura.
* [Percorso di onboarding](/help/journey-onboarding/overview.md)- Questa guida fornisce un riepilogo di come iniziare a utilizzare Experience Manager as a Cloud Service, incluso come ottenere l’accesso e configurare il team
