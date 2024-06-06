---
title: Monitoraggio dell’uso reale per AEM as a Cloud Service
description: Scopri come utilizzare il monitoraggio in tempo reale (RUM, Real Use Monitoring) per acquisire e analizzare l’esperienza dell’utente digitale di un sito web o di un’applicazione in tempo reale.
source-git-commit: a15f973c21044e16751401bd0ffb256a4d0fb17d
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 0%

---


>[!NOTE]
>Siamo entusiasti di annunciare [Rollout GA](/help/release-notes/release-notes-cloud/release-notes-current.md#real-use-monitoring) per il servizio Real Use Monitoring, la raccolta di dati lato client. Si tratta di un servizio automatizzato e non è richiesta alcuna configurazione del cliente.

# Servizio di monitoraggio per uso reale per AEM as a Cloud Service {#real-use-monitoring-service-for-aem-as-a-cloud-service}

>[!INFO]
>
>Il monitoraggio lato client funziona solo per i clienti con versione AEM Cloud Service **2024.5.16461** e superiore.

## Panoramica {#overview}

Il servizio Real Use Monitoring (RUM) è una tecnologia di monitoraggio delle prestazioni che acquisisce e analizza in tempo reale le esperienze utente digitali di un sito web o di un’applicazione. Fornisce visibilità sulle prestazioni in tempo reale di un’applicazione web e approfondisce l’esperienza dell’utente finale. Real User Monitoring è stato rinominato &quot;Real Use Monitoring&quot; perché riflette meglio la vera essenza del servizio, che si concentra sull&#39;ottimizzazione delle prestazioni monitorando il coinvolgimento dei siti web, piuttosto che gli utenti stessi.

Con RUM, le metriche delle prestazioni chiave vengono tracciate dall’avvio dell’URL fino a quando la richiesta non viene trasmessa al browser, il che aiuta gli sviluppatori a migliorare l’applicazione per facilitarne l’utilizzo per gli utenti finali.

## Chi Può Beneficiare Del Servizio Di Monitoraggio Reale? {#who-can-benefit-from-rum-service}

Il servizio di monitoraggio Real Use è utile per tutti i clienti. Offre un riflesso rappresentativo delle interazioni degli utenti, garantendo una misura affidabile del coinvolgimento del sito web acquisendo il numero di visualizzazioni di pagina lato client.

Per tutti gli Adobi di clienti, questo servizio fornisce informazioni preziose sulle interazioni degli utenti. I clienti che utilizzano la propria rete CDN possono beneficiare di rapporti sul traffico semplificati, in quanto Adobe ora integra direttamente la raccolta dei dati, eliminando la necessità di creare rapporti separati durante i cicli di rinnovo.

Desideri sfruttare appieno il potenziale del tuo sito web, utilizzando lo strumento di visualizzazione Adobe Early Adopter RUM Explorer per ottenere informazioni utili sul coinvolgimento del sito web? Questo strumento può fornire informazioni approfondite sulle prestazioni della pagina, tra cui metriche sul numero di clic, Core Web Vitals (CWV), conversioni e mappe di percorso dei clienti. Utilizzando queste informazioni avanzate, puoi perfezionare le tue esperienze digitali per soddisfare le esigenze degli utenti in modo più efficace. Se desiderate saperne di più e ottenere l&#39;accesso, inviateci un&#39;email all&#39;indirizzo `rum-explorer@adobe.com`.

## Comprendere il funzionamento del servizio di monitoraggio Real Use {#understand-how-the-rum-service-works}

Adobe Experience Manager utilizza Real Use Monitoring (RUM) per aiutare i clienti e gli Adobi a comprendere come i visitatori interagiscono con i siti Adobe Experience Manager, per diagnosticare i problemi di prestazioni e per misurare l’efficacia degli esperimenti. RUM preserva la privacy dei visitatori attraverso il campionamento (viene monitorata solo una piccola porzione di tutte le visualizzazioni di pagina) e non vengono raccolte informazioni personali identificabili (PII, personally identifiable information).

## Servizio di monitoraggio per uso reale e privacy {#rum-service-and-privacy}

Il servizio Real Use Monitoring di Adobe Experience Manager è progettato per preservare la privacy dei visitatori e ridurre al minimo la raccolta dei dati. In qualità di visitatore, ciò significa che nessuna informazione personale viene raccolta dal sito che stai visitando o resa disponibile agli Adobi.

In qualità di operatore del sito, non è necessario alcun consenso aggiuntivo per abilitare il monitoraggio tramite questa funzione. Non esiste alcun modulo aggiuntivo a comparsa o di consenso che gli utenti finali possano accettare per abilitare RUM.

## Campionamento dei dati del servizio di monitoraggio Real Use {#rum-service-data-sampling}

Le soluzioni di analisi web tradizionali tentano di raccogliere dati su ogni singolo visitatore. Il servizio RUM di Adobe Experience Manager acquisisce informazioni solo da una piccola frazione di visualizzazioni di pagina. Il servizio deve essere campionato e reso anonimo, anziché sostituire le funzioni di analisi. Per impostazione predefinita, le pagine hanno una proporzione di campionamento di 1:100. Al momento, gli operatori del sito non possono aumentare o diminuire la frequenza di campionamento. Per stimare con precisione il traffico totale, per ogni 100 visualizzazioni di pagina, i dati vengono raccolti da 1, fornendo un’approssimazione affidabile del traffico complessivo.

Poiché la decisione se raccogliere o meno i dati viene presa in base alla visualizzazione pagina per pagina, diventa praticamente impossibile tenere traccia delle interazioni tra più pagine. Per progettazione, RUM non ha alcun concetto di visitatori o sessioni, ma solo di visualizzazioni di pagina.

## Quali dati vengono raccolti {#what-data-is-being-collected}

Il servizio Real Use Monitoring è progettato per impedire la raccolta di informazioni personali. Di seguito sono elencate tutte le informazioni che possono essere raccolte da RUM:

* Il nome host del sito visitato, ad esempio: `experienceleague.adobe.com`
* Il tipo di agente utente e il sistema operativo utilizzati per visualizzare la pagina, ad esempio: `desktop:windows` o `mobile:ios`
* L’ora della raccolta dei dati, ad esempio: `2021-06-26 06:00:02.596000 UTC (in order to preserve privacy, we round all minutes to the previous hour, so that only seconds and milliseconds are tracked)`
* L’URL della pagina visitata, ad esempio: `https://experienceleague.adobe.com/docs`
* URL referente (URL della pagina collegata alla pagina corrente, se l’utente ha seguito un collegamento)
* Un ID della visualizzazione pagina generato in modo casuale, in un formato simile a: `2Ac6`
* Peso o inverso della frequenza di campionamento, ad esempio: `100`. Ciò significa che viene registrata solo una visualizzazione su cento
* Il punto di controllo, o il nome di un particolare evento nella sequenza di caricamento della pagina o di interazione con essa come visitatore
* L’origine o l’identificatore dell’elemento DOM con cui l’utente interagisce per il punto di controllo menzionato sopra. Ad esempio, potrebbe trattarsi di un’immagine
* La destinazione o il collegamento a una pagina o risorsa esterna con cui l’utente interagisce per il punto di controllo menzionato in precedenza. Esempio: `https://blog.adobe.com/jp/publish/2022/06/29/media_162fb947c7219d0537cce36adf22315d64fb86e94.png`
* Le metriche delle prestazioni Core Web Vitals (CWV), tra cui LCP (Largest Contentful Paint), FID (First Input Delay), CLS (Cumulative Layout Shift) e TTFB (Time To First Byte), descrivono la qualità dell’esperienza del visitatore.

## Funzionamento del monitoraggio Real Use per un cliente {#how-rum-works-for-a-customer}

Real Use Monitoring monitora automaticamente il traffico lato client per fornire informazioni utili. In qualità di cliente Adobe, non è necessario eseguire ulteriori passaggi, in quanto questo servizio è perfettamente integrato nella configurazione esistente. Con il rollout Disponibilità generale (GA), potrai beneficiare automaticamente di questa nuova funzione.

<!-- Alexandru: hiding temporarily, until we figure out where this needs to be linked to 

If you wish to leverage more insights with this new feature to optimize your digital experiences effortlessly, please see here (link to Row 99). -->

## Utilizzo dei dati del servizio di monitoraggio Real Use {#how-rum-service-data-is-being-used}

I dati RUM sono utili per i seguenti scopi:

* Identificare e correggere i colli di bottiglia delle prestazioni per le sedi dei clienti
* Per semplificare la ricerca automatica del traffico che include le visualizzazioni di pagina.
* Comprendere il modo in cui Adobe Experience Manager interagisce con altri script (ad esempio analisi, targeting o librerie esterne) sulla stessa pagina, per aumentare la compatibilità.

## Limitazioni e nozioni di base sulla varianza nelle visualizzazioni di pagina e nelle metriche delle prestazioni {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

Poiché analizzerai i dati RUM, potrebbero esserci varianze nelle Visualizzazioni di pagina e in altre metriche delle prestazioni. Queste varianze possono essere attribuite a diversi fattori inerenti al monitoraggio in tempo reale lato client. Di seguito sono riportate alcune considerazioni chiave che i clienti devono tenere presenti quando interpretano i dati RUM:

1. **Blocchi del tracciamento**

   * Gli utenti finali che utilizzano bloccanti del tracciamento o estensioni della privacy possono impedire la raccolta dati RUM, in quanto questi strumenti limitano l’esecuzione degli script di tracciamento. Questa restrizione può portare a visualizzazioni di pagina e interazioni utente non riportate correttamente, creando una discrepanza tra l’attività effettiva del sito e i dati acquisiti da RUM.

1. **Limitazioni nell’acquisizione di chiamate API/JSON headless**

   * Il servizio dati RUM si concentra sull’esperienza lato client e al momento non acquisisce le chiamate API o JSON back-end effettuate da un’app headless non AEM. L’esclusione di queste chiamate dai dati del servizio RUM creerà varianze rispetto alle richieste di contenuto misurate da CDN Analytics.

## Domande frequenti {#faq}


1. **I clienti saranno in grado di integrare gli script di servizio RUM con sistemi di terze parti come Dynatrace?**

   Sì.

1. **Vengono raccolte metriche di tipo &quot;Interaction to next paint&quot; (Interazione con la pittura successiva), &quot;Time to first byte&quot; (Tempo al primo byte) e &quot;First contentful paint&quot; (Prima pittura di contenuto)?**

   Vengono raccolte le interazioni con la vernice successiva (INP) e il tempo al primo byte (TTFB).  Al momento non viene raccolta la prima pittura di contenuto.

1. **Il `/.rum` percorso bloccato sul sito. Come risolvere il problema?**

   Il `/.rum` percorso richiesto per il funzionamento della raccolta RUM.  Se disponi di una rete CDN davanti a quella che Adobe fornisce come parte di AEM as a Cloud Service, devi assicurarti che il `/.rum` il percorso porta alla stessa origine dell’AEM del resto del contenuto dell’AEM.

1. **La raccolta RUM viene conteggiata nelle richieste di contenuto per scopi contrattuali?**

   Né la libreria RUM né la raccolta RUM vengono considerate richieste di contenuto e non aumenta il numero riportato di visualizzazioni di pagina o chiamate API. Inoltre, per i clienti che utilizzano una rete CDN preconfigurata con AEM as a Cloud Service, [raccolta lato server](#serverside-collection) è la base per le richieste di contenuto.

1. **Come posso rinunciare?**

Si consiglia vivamente di utilizzare il Real Use Monitoring (RUM) per i suoi vantaggi significativi e per consentirti di ottimizzare le tue esperienze digitali. Può offrire informazioni preziose che possono contribuire a migliorare le prestazioni del sito web.Il servizio è progettato per essere semplice e non ha alcun impatto sulle prestazioni del sito web.

Rinunciare significa perdere queste informazioni. Tuttavia, in caso di problemi, contatta l’assistenza Adobe.
