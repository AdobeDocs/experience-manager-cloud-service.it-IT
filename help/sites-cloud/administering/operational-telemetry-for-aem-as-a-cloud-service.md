---
title: Telemetria operativa per AEM as a Cloud Service
description: Scopri la telemetria operativa, un servizio automatizzato che consente di monitorare la raccolta di dati lato client.
exl-id: 91fe9454-3dde-476a-843e-0e64f6f73aaf
feature: Administering
role: Admin
source-git-commit: 41d9fd628eec8ce757447bed13d50211e71785de
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 1%

---

# Servizio di telemetria operativa per AEM as a Cloud Service {#real-use-monitoring-service-for-aem-as-a-cloud-service}

>[!NOTE]
>
>Il servizio di telemetria operativa, la raccolta di dati lato client, è un servizio automatizzato. Non è richiesta alcuna configurazione del cliente.

>[!INFO]
>
>Il monitoraggio lato client funziona solo per i clienti con AEM (Adobe Experience Manager) Cloud Service versione **2024.5.16461** e successive.

## Panoramica {#overview}

Il servizio di telemetria operativa è una tecnologia di monitoraggio delle prestazioni che monitora in tempo reale il traffico lato client su un sito Web o un&#39;applicazione. Questo servizio si concentra sulla raccolta di metriche e dati chiave per ottimizzare le prestazioni monitorando il coinvolgimento dei siti web, anziché gli utenti stessi. Con la telemetria operativa, le metriche delle prestazioni chiave vengono tracciate dall’avvio dell’URL fino a quando la richiesta non viene trasmessa al browser.

## Chi può beneficiare del servizio di telemetria operativa? {#who-can-benefit-from-operational-telemetry-service}

La telemetria operativa aiuta i clienti e Adobe a comprendere come gli utenti finali interagiscono con i siti AEM. La telemetria operativa preserva la privacy dei visitatori attraverso una raccolta e un campionamento di dati limitati: viene monitorata solo una piccola parte di tutte le visualizzazioni di pagina.

## Campionamento dei dati del servizio di telemetria operativa {#operational-telemetry-service-data-sampling}

Le soluzioni di analisi web tradizionali tentano di raccogliere dati su ogni singolo visitatore. Il servizio di telemetria operativa di AEM acquisisce informazioni solo da una piccola frazione di visualizzazioni di pagina. Il servizio deve essere campionato e reso anonimo, anziché sostituire le funzioni di analisi. Per impostazione predefinita, le pagine hanno una proporzione di campionamento di 1:100. Al momento, gli operatori del sito non possono aumentare o diminuire la frequenza di campionamento. Per stimare con precisione il traffico totale, per ogni 100 visualizzazioni di pagina, i dati vengono raccolti da 1, fornendo un’approssimazione affidabile del traffico complessivo.

Quando si decide se raccogliere o meno i dati, la procedura avviene in modalità di visualizzazione pagina per pagina, rendendo praticamente impossibile tenere traccia delle interazioni tra più pagine. Per progettazione, la telemetria operativa non ha alcun concetto di visitatori o sessioni, ma solo di visualizzazioni di pagina.

## Quali dati vengono raccolti? {#what-data-is-being-collected}

Il servizio di telemetria operativa è progettato per ridurre al minimo la raccolta dei dati. Di seguito sono elencate tutte le informazioni raccolte tramite Telemetria operativa:

* Il nome host del sito visitato, ad esempio: `experienceleague.adobe.com`
* Tipo di agente utente e sistema operativo utilizzati per visualizzare la pagina, ad esempio: `desktop:windows` o `mobile:ios`
* Ora della raccolta dati, ad esempio: `2021-06-26 06:00:02.596000 UTC (in order to preserve privacy, we round all minutes to the previous hour, so that only seconds and milliseconds are tracked)`
* URL della pagina visitata, ad esempio: `https://experienceleague.adobe.com/docs?lang=it`
* URL referente (URL della pagina collegata alla pagina corrente, se l’utente ha seguito un collegamento)
* ID della visualizzazione pagina generato in modo casuale, in un formato simile a: `2Ac6`
* Peso o inverso della frequenza di campionamento, ad esempio: `100`. Significa che viene registrata solo una visualizzazione pagina su cento
* Il punto di controllo, o nome, di un particolare evento nella sequenza di caricamento della pagina. Oppure, interagendo con esso come visitatore
* L’origine, o identificatore, dell’elemento DOM con cui l’utente interagisce per il punto di controllo indicato sopra. Ad esempio, potrebbe trattarsi di un’immagine
* La destinazione o il collegamento a una pagina o risorsa esterna con cui l’utente interagisce per il punto di controllo menzionato in precedenza. Esempio: `https://blog.adobe.com/jp/publish/2022/06/29/media_162fb947c7219d0537cce36adf22315d64fb86e94.png`
* Le metriche delle prestazioni [Core Web Vitals (CWV)](https://web.dev/articles/lcp) [LCP (Largest Contentful Paint)](https://web.dev/articles/lcp), [Interaction to Next Paint (INP)](https://web.dev/articles/inp) e [Cumulative Layout Shift (CLS)](https://web.dev/articles/cls) che descrivono la qualità dell&#39;esperienza del visitatore.

## Funzionamento della telemetria operativa per un cliente {#how-operational-telemetry-works-for-a-customer}

La telemetria operativa controlla automaticamente il traffico lato client. In qualità di cliente di Adobe, non è necessario eseguire ulteriori passaggi, in quanto questo servizio è perfettamente integrato nella configurazione esistente. Il servizio di telemetria operativa è già disponibile e consente di usufruire automaticamente dei vantaggi di questa nuova funzionalità. Il servizio di telemetria operativa non espone attualmente al monitoraggio alcuna metrica visualizzata dai clienti. Stiamo lavorando per offrirti questa funzionalità il prima possibile.

<!-- Alexandru: hiding temporarily, until we figure out where this needs to be linked to 

If you wish to leverage more insights with this new feature to optimize your digital experiences effortlessly, please see here (link to Row 99). -->

## Utilizzo della telemetria operativa in Adobe {#how-operational-telemetry-data-is-being-used}

I dati di telemetria operativa vengono utilizzati per i seguenti scopi:

* Identificare e correggere i colli di bottiglia delle prestazioni per le sedi dei clienti
* Per comprendere come AEM interagisce con altri script (ad esempio analisi, targeting o librerie esterne) sulla stessa pagina, per aumentare la compatibilità.
<!--
## Limitations and understanding variance in page views and performance metrics {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

Here are key considerations for customers to keep in mind when interpreting their Operational Telemetry data:

1. **Tracker blockers**

   * End-users employing tracker blockers or privacy extensions can impede Operational Telemetry data collection, as these tools restrict the tracking scripts' execution. This restriction may lead to underreported page views and user interactions, creating a discrepancy between actual site activity and the data captured by Operational Telemetry.

1. **Limitations in capturing headless API/JSON calls**

   * Operational Telemetry data service focuses on the client-side experience and doesn't capture the backend API or JSON calls made from a non-AEM headless app at this time. The exclusion of these calls from Operational Telemetry service data creates variances from the content requests measured by CDN Analytics.
-->

## Domande frequenti {#faq}

<!-- REMOVED THIS FAQ AS PER EMAIL REQUEST FROM SHWETA DUA, SEPTEMBER 4, 2024 TO THE DL-AEM-DOCS GROUP 
1. **Can customers integrate the Operational Telemetry service scripts with third-party systems like Dynatrace?**

   Yes.
-->

1. **Le metriche &quot;Interaction to next paint&quot; (Interazione con la vernice successiva), &quot;Time to first byte&quot; (Tempo al primo byte) e &quot;First contentful paint&quot; (Prima vernice di contenuto) vengono raccolte?**

   Vengono raccolte le interazioni con la vernice successiva (INP) e il valore TTFB (Time To First Byte).  Al momento non viene raccolta la prima pittura di contenuto.

1. **Il percorso `/.rum` è bloccato sul sito, come posso risolvere il problema?**

   Il percorso `/.rum` è necessario per il funzionamento della raccolta di telemetria operativa. Se utilizzi una rete CDN davanti all&#39;AEM as a Cloud Service di Adobe, accertati che il percorso `/.rum` inoltri alla stessa origine AEM degli altri contenuti AEM. E assicurati che non venga regolato in alcun modo. In alternativa, è possibile modificare l&#39;host da utilizzare per la telemetria operativa in `rum.hlx.page` impostando [una variabile di ambiente in Cloud Manager](/help/implementing/cloud-manager/environment-variables.md#add-variables) denominata `AEM_OPTEL_EXTERNAL` al valore `true`. Se in un secondo momento desideri tornare alle stesse richieste di dominio, rimuovi semplicemente di nuovo la variabile di ambiente.

1. **La raccolta di telemetria operativa viene conteggiata per le richieste di contenuto a scopo contrattuale?**

   La libreria Telemetria operativa e la raccolta Telemetria operativa non vengono considerate come richieste di contenuto e non aumentano il numero riportato di visualizzazioni di pagina o chiamate API. Inoltre, per i clienti che utilizzano una rete CDN preconfigurata con AEM as a Cloud Service, la [raccolta lato server](#serverside-collection) è la base per le richieste di contenuto.

1. **Come posso disabilitare la telemetria operativa?**

   Adobe consiglia di utilizzare la telemetria operativa per i suoi vantaggi significativi e per consentire ad Adobe di ottimizzare le esperienze digitali migliorando le prestazioni del sito web. Il servizio è progettato per essere semplice e non ha alcun impatto sulle prestazioni del sito web.

   Rinunciare potrebbe significare perdere l’opportunità di migliorare il coinvolgimento del traffico sul sito web. Se tuttavia si verificano problemi, è possibile disattivare la telemetria operativa [impostando una variabile di ambiente in Cloud Manager](/help/implementing/cloud-manager/environment-variables.md#add-variables) denominata `AEM_OPTEL_DISABLED` sul valore `true`. Per riattivare la telemetria operativa in un secondo momento, è sufficiente rimuovere nuovamente la variabile di ambiente.
