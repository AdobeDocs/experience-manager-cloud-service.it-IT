---
title: Monitoraggio degli utenti reali per AEM as a Cloud Service
description: Scopri come utilizzare il monitoraggio dell'uso reale (RUM) per acquisire e analizzare la esperienza di utilizzo digitale di un sito Web o di un applicazione in tempo reale.
exl-id: 91fe9454-3dde-476a-843e-0e64f6f73aaf
feature: Administering
role: Admin
source-git-commit: 8ccef0103ae7fb75171431eeb36f7352f6467d56
workflow-type: tm+mt
source-wordcount: '1302'
ht-degree: 0%

---

# Servizio di monitoraggio dell&#39;uso reale per AEM come Cloud Service {#real-use-monitoring-service-for-aem-as-a-cloud-service}

>[!NOTE]
>
>Il servizio Real Use Monitoring, la raccolta di dati lato client, è un servizio automatizzato. Non è richiesta alcuna configurazione del cliente.

>[!INFO]
>
>Il monitoraggio lato client funziona solo per i clienti con AEM Cloud Service versione **2024.5.16461** e successive.

## Panoramica {#overview}

Il servizio Real Use Monitoring (RUM) è una tecnologia di monitoraggio delle prestazioni che acquisisce e analizza le esperienze di utente digitale di un sito Web o di un applicazione in tempo reale. Fornisce visibilità sulle prestazioni in tempo reale di un applicazione web e fornisce informazione approfondita più approfondite sul esperienza di utilizzo finale. Il servizio si concentra sull&#39;ottimizzazione delle prestazioni monitorando le interazioni del sito Web, piuttosto che gli utenti stessi.

Con RUM, le metriche chiave delle prestazioni vengono tracciate dall&#39;inizio del URL fino a quando il richiesta viene restituito al browser. Aiuta gli sviluppatori a migliorare la applicazione per renderla facile da usare per gli utenti finali.

>[!INFO]
>
>&quot;Real User Monitoring&quot; è stato rinominato in &quot;Real Use Monitoring&quot; in quanto riflette meglio la vera essenza del servizio.

## Chi può beneficiare di un servizio di monitoraggio dell&#39;utilizzo reale? {#who-can-benefit-from-rum-service}

Il servizio Real Use Monitoring è vantaggioso per tutti i clienti. Offre un riflesso rappresentativo delle interazioni utente, garantendo un misurare affidabile del coinvolgimento del sito Web acquisendo il numero di visualizzazioni di pagina lato client.

Per tutti i clienti Adobe Systems, questo servizio fornisce preziose informazioni sulle interazioni utente. I clienti che utilizzano la propria CDN possono trarre vantaggio da una reportistica semplificata sulle traffico, poiché ora Adobe Systems integra direttamente il raccolta dei dati, eliminando la necessità di report separati durante i cicli di rinnovo.

## Comprendere il funzionamento del servizio di monitoraggio dell&#39;utilizzo reale {#understand-how-the-rum-service-works}

Adobe Experience Manager (AEM) utilizza il monitoraggio dell&#39;utilizzo reale (RUM) per aiutare i clienti e i Adobe Systems a capire come i visitatori interagiscono con AEM siti. Li aiuta a diagnosticare i problemi di prestazioni e a misurare l&#39;efficacia degli esperimenti. RUM preserva la privacy dei visitatori attraverso il campionamento - solo una piccola parte di tutte le visualizzazioni di pagina viene monitorata - e non vengono raccolte informazioni di identificazione personale (PII).

## Servizio di monitoraggio dell&#39;uso reale e privacy {#rum-service-and-privacy}

Il servizio Real Use Monitoring in AEM è progettato per preservare la privacy dei visitatori e ridurre al minimo la raccolta dei dati. Come visitatore, significa che il sito che stai visitando o messo a disposizione di Adobe Systems, non raccoglie alcuna informazione personale.

In qualità di operatore del sito, non sono necessari opt-in aggiuntivi per abilitare il monitoraggio tramite questa funzione. Non ci sono ulteriori finestra a comparsa o moduli di consenso che gli utenti finali possono accettare per abilitare RUM.

## Campionamento dei dati del servizio di monitoraggio dell&#39;uso reale {#rum-service-data-sampling}

Le soluzioni analisi web tradizionali cercano di raccogliere dati su ogni singolo visitatore. Il servizio RUM di AEM acquisisce solo informazioni da una piccola frazione di visualizzazioni di pagina. Il servizio è pensato per essere campionato e reso anonimo piuttosto che sostituire analisi. Per impostazione predefinita, le pagine hanno un rapporto di campionamento 1:100. Al momento gli operatori del sito non possono aumentare o diminuire la frequenza di campionamento. Per stimare con precisione il traffico totale, per ogni 100 visualizzazioni di pagina vengono raccolti dati da 1, fornendo un&#39;approssimazione affidabile del traffico complessivo.

Poiché la decisione se i dati vengono raccolti, viene effettuata in base alla visualizzazione pagina per pagina e diventa praticamente impossibile tracciare le interazioni tra più pagine. Per progettazione, RUM non ha il concetto di visitatori o sessioni, ma solo di visualizzazioni di pagina.

## Quali dati vengono raccolti {#what-data-is-being-collected}

Il servizio di monitoraggio dell&#39;uso reale è progettato per impedire la raccolta di informazioni di identificazione personale. La serie completa di informazioni raccolte da RUM è elencata di seguito:

* Il nome host del sito visitato, ad esempio: `experienceleague.adobe.com`
* L&#39;utente generale tipo di agente e sistema operativo utilizzato per visualizzare la pagina, ad esempio: `desktop:windows``mobile:ios`
* L&#39;ora in cui i dati raccolta, ad esempio: `2021-06-26 06:00:02.596000 UTC (in order to preserve privacy, we round all minutes to the previous hour, so that only seconds and milliseconds are tracked)`
* Il URL della pagina visitata, per istanza: `https://experienceleague.adobe.com/docs`
* Il Referrer URL (il URL della pagina che collegava alla pagina corrente, se il utente seguito da un collegare)
* Un ID generato casualmente della visualizzazione pagina, in un formato simile a: `2Ac6`
* Il peso o l&#39;inverso della frequenza di campionamento, ad esempio: `100`. Significa che viene registrata solo una visualizzazione di pagina su cento
* Il checkpoint, o nome, di un particolare evento nella sequenza di caricamento della pagina. Oppure, interagire con esso come visitatore
* L&#39;origine, o identificatore, dell&#39;elemento DOM con cui il utente interagisce per il checkpoint di cui sopra. Ad istanza, potrebbe trattarsi di un&#39;immagine
* Il destinazione o collegare a una pagina o a una risorsa esterna con cui il utente interagisce per il checkpoint di cui sopra. Esempio: `https://blog.adobe.com/jp/publish/2022/06/29/media_162fb947c7219d0537cce36adf22315d64fb86e94.png`
* Le metriche delle prestazioni CWV (Core Web Vitals), tra cui LCP (Largest Contentful Paint), FID (First Input Delay), CLS (Cumulative Layout Shift) e TTFB (Time To First Byte) che descrivono la qualità dell&#39;esperienza del visitatore.

## Come funziona il monitoraggio dell&#39;uso reale per un cliente {#how-rum-works-for-a-customer}

Real Use Monitoring monitora automaticamente le traffico lato client per fornire informazioni preziose. Come cliente Adobe Systems, non è necessario eseguire ulteriori passaggi, poiché questo servizio è perfettamente integrato nella configurazione esistente. Con la rollout Disponibilità generale (GA), beneficiate automaticamente di questa nuova funzione.

<!-- Alexandru: hiding temporarily, until we figure out where this needs to be linked to 

If you wish to leverage more insights with this new feature to optimize your digital experiences effortlessly, please see here (link to Row 99). -->

## Come vengono utilizzati i dati del servizio di monitoraggio dell&#39;uso reale {#how-rum-service-data-is-being-used}

I dati RUM sono utili per i seguenti scopi:

* Per identificare e correggere i colli di bottiglia delle prestazioni per i siti dei clienti
* Semplificare la ricerca automatica di traffico che include le visualizzazioni di pagina.
* Comprendere in che modo AEM interagisce con altri script (ad esempio analisi, targeting o librerie esterni) sulla stessa pagina, aumentare la compatibilità.

## Limitazioni e comprensione della varianza nelle visualizzazioni Pagina e nelle metriche delle prestazioni {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

Quando si analizzano i dati RUM, potrebbero verificarsi variazioni nelle visualizzazioni di pagina e in altre metriche delle prestazioni. Queste varianze possono essere attribuite a diversi fattori inerenti al monitoraggio in tempo reale lato client. Ecco alcune considerazioni chiave che i clienti devono tenere a mente quando interpretano i loro dati RUM:

1. **Bloccanti tracker**

   * Gli utenti finali che utilizzano tracker blocker o estensioni della privacy possono impedire l&#39;raccolta dei dati RUM, poiché questi strumenti limitano l&#39;esecuzione degli script di tracciamento. Questa restrizione può lead a visualizzazioni di pagina e interazioni utente sottostimate, creando una discrepanza tra l&#39;attività effettiva del sito e i dati acquisiti da RUM.

1. **Limitazioni nell&#39;acquisizione di chiamate API/JSON headless**

   * Al momento, il servizio dati RUM si concentra sull&#39;esperienza lato client e non acquisisce le chiamate API back-end o JSON effettuate da un&#39;app headless non AEM. L&#39;esclusione di queste chiamate dai dati del servizio RUM crea varianze dalle richieste di contenuto misurate da CDN Analytics.

## Domande frequenti {#faq}


1. **I clienti possono integrare gli script del servizio RUM con sistemi di terze parti like Dynatrace?**

   Sì.

1. **Le metriche &quot;Interazione con il disegno successivo&quot;, &quot;Tempo al primo byte&quot; e &quot;Primo colore contento&quot; vengono raccolte metriche Web?**

   Vengono raccolte l&#39;interazione con il disegno successivo (INP) e il TTFB (Time To First Byte).  La prima vernice contenta non viene raccolta in questo momento.

1. **Il `/.rum` percorso è bloccato sul mio sito, come devo risolverlo?**

   Il `/.rum` percorso è necessario affinché RUM raccolta funzioni. Se hai una rete CDN davanti a ciò che Adobe Systems fornisce come parte di AEM come Cloud Service, assicurati che il `/.rum` percorso prosegua verso la stessa origine AEM del resto del tuo AEM contenuto. E, assicurati che non sia regolato in alcun modo.

1. **I raccolta RUM contano ai fini delle richieste di contenuto ai fini contrattuali?**

   Il libreria RUM e il raccolta RUM non vengono conteggiati come richieste contenuto e non aumentano il numero riportato di visualizzazioni di pagina o chiamate API. Inoltre, per i clienti che utilizzano CDN pronta all&#39;uso con AEM come Cloud Service, [la raccolta](#serverside-collection) lato server è la base per le richieste di contenuto.

1. **Come posso rinunciare?**

   Adobe Systems consiglia di utilizzare il Real Use Monitoring (RUM) per i suoi vantaggi significativi e per il fatto che può consentire di ottimizzare le esperienze digitali. Può offrire informazioni preziose che possono aiutare a migliorare le prestazioni del sito web. Il servizio è progettato per essere senza soluzione di continuità e non ha alcun impatto sulle prestazioni del tuo sito web.

   Rinunciare significa perdere queste informazioni. Tuttavia, se riscontri problemi, contatta Adobe Systems supporto.
