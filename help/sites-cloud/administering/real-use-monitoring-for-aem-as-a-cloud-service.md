---
title: Monitoraggio degli utenti reali per AEM as a Cloud Service
description: Scopri Real Use Monitoring (RUM), un servizio automatizzato che consente di monitorare la raccolta di dati lato client.
exl-id: 91fe9454-3dde-476a-843e-0e64f6f73aaf
feature: Administering
role: Admin
source-git-commit: e6a610c56b9ad7a684ea9f5ef72199d3bed28cc0
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 1%

---

# Servizio di monitoraggio Real Use per AEM as a Cloud Service {#real-use-monitoring-service-for-aem-as-a-cloud-service}

>[!NOTE]
>
>Real Use Monitoring Service, la raccolta di dati lato client, è un servizio automatizzato. Non è richiesta alcuna configurazione del cliente.

>[!INFO]
>
>Il monitoraggio lato client funziona solo per i clienti con AEM (Adobe Experience Manager) Cloud Service versione **2024.5.16461** e successive.

## Panoramica {#overview}

Il servizio RUM (Real Use Monitoring) è una tecnologia di monitoraggio delle prestazioni che monitora in tempo reale il traffico lato client su un sito Web o un’applicazione. Questo servizio si concentra sulla raccolta di metriche e dati chiave per ottimizzare le prestazioni monitorando il coinvolgimento dei siti web, anziché gli utenti stessi. Con RUM, le metriche delle prestazioni chiave vengono tracciate direttamente dall’avvio dell’URL fino a quando la richiesta non viene trasmessa al browser.

## Chi può trarre vantaggio da un servizio di monitoraggio Real Use? {#who-can-benefit-from-rum-service}

Real Use Monitoring aiuta i clienti e Adobe a comprendere come gli utenti finali interagiscono con i siti AEM. Monitoraggio Real Use consente di diagnosticare i problemi di prestazioni e di misurare l&#39;efficacia degli esperimenti. Il monitoraggio dell’utilizzo reale preserva la privacy dei visitatori attraverso il campionamento (viene monitorata solo una piccola parte di tutte le visualizzazioni di pagina) e non viene raccolta alcuna informazione personale identificabile (PII).

## Servizio di monitoraggio Real Use e privacy {#rum-service-and-privacy}

Il servizio Real Use Monitoring in AEM mantiene la privacy dei visitatori e riduce al minimo la raccolta dei dati. In qualità di visitatore, significa che il sito che stai visitando o che stai rendendo disponibile ad Adobe non raccoglie informazioni personali.

In qualità di operatore del sito, non è necessario alcun consenso aggiuntivo per abilitare il monitoraggio tramite questa funzione. Non esiste alcun modulo aggiuntivo a comparsa o di consenso che gli utenti finali possano accettare per abilitare RUM.

## Campionamento dei dati del servizio di monitoraggio Real Use {#rum-service-data-sampling}

Le soluzioni di analisi web tradizionali tentano di raccogliere dati su ogni singolo visitatore. Il servizio Real Use Monitoring (RUM) di AEM acquisisce informazioni solo da una piccola frazione di visualizzazioni di pagina. Il servizio deve essere campionato e reso anonimo, anziché sostituire le funzioni di analisi. Per impostazione predefinita, le pagine hanno una proporzione di campionamento di 1:100. Al momento, gli operatori del sito non possono aumentare o diminuire la frequenza di campionamento. Per stimare con precisione il traffico totale, per ogni 100 visualizzazioni di pagina, i dati vengono raccolti da 1, fornendo un’approssimazione affidabile del traffico complessivo.

Quando si decide se raccogliere o meno i dati, la procedura avviene in modalità di visualizzazione pagina per pagina, rendendo praticamente impossibile tenere traccia delle interazioni tra più pagine. Per progettazione, RUM non ha alcun concetto di visitatori o sessioni, ma solo di visualizzazioni di pagina.

## Quali dati vengono raccolti? {#what-data-is-being-collected}

Il servizio Real Use Monitoring è progettato per impedire la raccolta di informazioni personali. Di seguito sono elencate tutte le informazioni raccolte da RUM:

* Il nome host del sito visitato, ad esempio: `experienceleague.adobe.com`
* Tipo di agente utente e sistema operativo utilizzati per visualizzare la pagina, ad esempio: `desktop:windows` o `mobile:ios`
* Ora della raccolta dati, ad esempio: `2021-06-26 06:00:02.596000 UTC (in order to preserve privacy, we round all minutes to the previous hour, so that only seconds and milliseconds are tracked)`
* URL della pagina visitata, ad esempio: `https://experienceleague.adobe.com/docs`
* URL referente (URL della pagina collegata alla pagina corrente, se l’utente ha seguito un collegamento)
* ID della visualizzazione pagina generato in modo casuale, in un formato simile a: `2Ac6`
* Peso o inverso della frequenza di campionamento, ad esempio: `100`. Significa che viene registrata solo una visualizzazione pagina su cento
* Il punto di controllo, o nome, di un particolare evento nella sequenza di caricamento della pagina. Oppure, interagendo con esso come visitatore
* L’origine, o identificatore, dell’elemento DOM con cui l’utente interagisce per il punto di controllo indicato sopra. Ad esempio, potrebbe trattarsi di un’immagine
* La destinazione o il collegamento a una pagina o risorsa esterna con cui l’utente interagisce per il punto di controllo menzionato in precedenza. Esempio: `https://blog.adobe.com/jp/publish/2022/06/29/media_162fb947c7219d0537cce36adf22315d64fb86e94.png`
* Le metriche delle prestazioni [Core Web Vitals (CWV)](https://web.dev/articles/lcp) [LCP (Largest Contentful Paint)](https://web.dev/articles/lcp), [Interaction to Next Paint (INP)](https://web.dev/articles/inp) e [Cumulative Layout Shift (CLS)](https://web.dev/articles/cls) che descrivono la qualità dell&#39;esperienza del visitatore.

## Funzionamento del monitoraggio Real Use per un cliente {#how-rum-works-for-a-customer}

Real Use Monitoring controlla automaticamente il traffico lato client. In qualità di cliente di Adobe, non è necessario eseguire ulteriori passaggi, in quanto questo servizio è perfettamente integrato nella configurazione esistente. Con il servizio Real Use Monitoring (RUM) disponibile a livello generale , potrai beneficiare automaticamente di questa nuova funzione. Il servizio di monitoraggio Real Use (Uso reale) non espone attualmente al monitoraggio alcuna metrica visualizzata dal cliente. Stiamo lavorando per offrirti questa funzionalità il prima possibile.

<!-- Alexandru: hiding temporarily, until we figure out where this needs to be linked to 

If you wish to leverage more insights with this new feature to optimize your digital experiences effortlessly, please see here (link to Row 99). -->

## Utilizzo del monitoraggio in tempo reale in Adobe {#how-rum-data-is-being-used}

I dati di monitoraggio per uso reale vengono utilizzati per i seguenti scopi:

* Identificare e correggere i colli di bottiglia delle prestazioni per le sedi dei clienti
* Per comprendere come AEM interagisce con altri script (ad esempio analisi, targeting o librerie esterne) sulla stessa pagina, per aumentare la compatibilità.
<!--
## Limitations and understanding variance in page views and performance metrics {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

Here are key considerations for customers to keep in mind when interpreting their RUM data:

1. **Tracker blockers**

   * End-users employing tracker blockers or privacy extensions can impede RUM data collection, as these tools restrict the tracking scripts' execution. This restriction may lead to underreported page views and user interactions, creating a discrepancy between actual site activity and the data captured by RUM.

1. **Limitations in capturing headless API/JSON calls**

   * RUM data service focuses on the client-side experience and doesn't capture the backend API or JSON calls made from a non-AEM headless app at this time. The exclusion of these calls from RUM service data creates variances from the content requests measured by CDN Analytics.
-->

## Domande frequenti {#faq}

<!-- REMOVED THIS FAQ AS PER EMAIL REQUEST FROM SHWETA DUA, SEPTEMBER 4, 2024 TO THE DL-AEM-DOCS GROUP 
1. **Can customers integrate the RUM service scripts with third-party systems like Dynatrace?**

   Yes.
-->

1. **Le metriche &quot;Interaction to next paint&quot; (Interazione con la vernice successiva), &quot;Time to first byte&quot; (Tempo al primo byte) e &quot;First contentful paint&quot; (Prima vernice di contenuto) vengono raccolte?**

   Vengono raccolte le interazioni con la vernice successiva (INP) e il valore TTFB (Time To First Byte).  Al momento non viene raccolta la prima pittura di contenuto.

1. **Il percorso `/.rum` è bloccato sul sito, come posso risolvere il problema?**

   Il percorso `/.rum` è necessario per il funzionamento della raccolta RUM. Se utilizzi una rete CDN davanti all&#39;AEM as a Cloud Service di Adobe, accertati che il percorso `/.rum` inoltri alla stessa origine AEM degli altri contenuti AEM. E assicurati che non venga regolato in alcun modo.

1. **La raccolta RUM viene conteggiata nelle richieste di contenuto per scopi contrattuali?**

   La libreria RUM e la raccolta RUM non vengono conteggiate come richieste di contenuto e non aumentano il numero riportato di visualizzazioni di pagina o chiamate API. Inoltre, per i clienti che utilizzano una rete CDN preconfigurata con AEM as a Cloud Service, la [raccolta lato server](#serverside-collection) è la base per le richieste di contenuto.

1. **Come posso rinunciare?**

   Adobe consiglia di utilizzare il Monitoraggio utilizzo reale (RUM) per i suoi vantaggi significativi e per consentire ad Adobe di ottimizzare le esperienze digitali migliorando le prestazioni del sito web. Il servizio è progettato per essere semplice e non ha alcun impatto sulle prestazioni del sito web.

   Rinunciare potrebbe significare perdere l’opportunità di migliorare il coinvolgimento del traffico sul sito web. Tuttavia, in caso di problemi, contatta il supporto Adobe.