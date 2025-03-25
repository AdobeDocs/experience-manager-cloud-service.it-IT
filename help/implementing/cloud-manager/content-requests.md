---
title: Comprendere le richieste di contenuto di Cloud Service
description: Se hai acquistato licenze per richieste di contenuto da Adobe, scopri i tipi di richieste di contenuto che Adobe Experience Cloud as a Service misura e le varianze con gli strumenti di reporting di analisi di un’organizzazione.
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: bd207a7c3e9e5e52202456fa95dd31293639725f
workflow-type: tm+mt
source-wordcount: '1464'
ht-degree: 3%

---

# Comprendere le richieste di contenuto di Cloud Service

## Introduzione {#introduction}

Le richieste di contenuto includono le richieste inviate ad AEM Sites. Queste richieste possono essere indirizzate tramite Edge Delivery Services o sistemi di caching forniti dal cliente, ad esempio una rete CDN (Content Delivery Network). Queste richieste forniscono dati strutturati in formato HTML o JSON e supportano le visualizzazioni di pagina (ad esempio, pagine e frammenti di esperienza) o i resi JSON tramite API in modo headless.

Il sistema conta le richieste di contenuto quando un utente visualizza una pagina utilizzando HTML o JSON. Misura la richiesta nel punto in cui il primo sistema di caching la riceve. Alcune richieste HTTP sono incluse o escluse ai fini del conteggio delle richieste di contenuto. Vedi l&#39;elenco completo delle [richieste di contenuto incluse](#included-content-requests) e [richieste di contenuto escluse](#excluded-content-request) HTTP.

## Informazioni sulle richieste di contenuto di Cloud Service {#understanding-cloud-service-content-requests}

Una *richiesta di pagina* fa riferimento a una richiesta HTTP che recupera il contenuto strutturato di base (ad esempio, HTML o JSON) necessario per eseguire il rendering dell&#39;esperienza della pagina principale. Non include le richieste di risorse, ad esempio immagini o script.

Per i clienti che utilizzano la rete CDN preconfigurata, AEM as a Cloud Service conta le richieste di contenuto come misurate a livello di server. Questa misurazione viene eseguita automaticamente e non si basa sul tracciamento delle analisi lato client.

AEM (Adobe Experience Manager) as a Cloud Service identifica le richieste di contenuto in base ai tipi di risposta generati dall’istanza di AEM e ricevuti dalla rete CDN. In particolare, vengono conteggiate le richieste che restituiscono HTML (`text/html`) o JSON (`application/json`). In genere, questi formati forniscono contenuti di pagina principali sia per il rendering tradizionale del sito che per la distribuzione headless.

Le richieste di risorse statiche come file JavaScript, fogli di stile CSS e immagini non vengono conteggiate come richieste di contenuto.

>[!NOTE]
>Se una richiesta API restituisce HTML o JSON che funge da contenuto a livello di pagina (ad esempio, nella distribuzione headless), può comunque essere conteggiata come richiesta di contenuto a seconda del contesto.

Le richieste di contenuto vengono misurate indipendentemente dal fatto che la risposta sia stata servita dalla cache CDN o inoltrata all’ambiente AEM di origine.

<!-- REMOVED AS PER EMAIL REQUEST FROM SHWETA DUA, JULY 30, 2024 TO RICK BROUGH AND ALEXANDRU SARCHIZ   For customers employing their own CDN, client-side collection offers a more precise reflection of interactions, ensuring a reliable measure of website engagement via the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md) service. This gives customers advanced insights into their page traffic and performance. While it is beneficial for all customers, it offers a representative reflection of user interactions, ensuring a reliable measure of website engagement by capturing the number of page views from the client side. 

For customers that bring their own CDN on top of AEM as a Cloud Service, server-side reporting results in numbers that cannot be used to compare with the licensed content requests. With the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md), Adobe can reflect a reliable measure of website engagement. -->

### Varianze nelle richieste di contenuto Cloud Service {#content-requests-variances}

Le richieste di contenuto possono presentare varianze all’interno degli strumenti di reporting di analisi di un’organizzazione, come riepilogato nella tabella seguente. In generale, evita di utilizzare strumenti di analisi che si basano su strumenti lato client per segnalare il numero di richieste di contenuto per un sito. Questi strumenti spesso perdono una grande parte del traffico perché dipendono dal consenso degli utenti per essere attivati. Gli strumenti di Analytics che raccolgono i dati lato server nei file di registro, o i rapporti CDN per i clienti che aggiungono la propria CDN oltre ad AEM as a Cloud Service, forniscono conteggi migliori.

| Motivo della varianza | Spiegazione |
|---|---|
| Consenso utente finale | Gli strumenti di Analytics che si basano su strumentazione lato client spesso dipendono dal consenso dell’utente all’attivazione. Questo flusso di lavoro potrebbe rappresentare la maggior parte del traffico che non viene tracciato. Per i clienti che desiderano misurare autonomamente le richieste di contenuto, Adobe consiglia di utilizzare gli strumenti di analisi per raccogliere dati dai rapporti lato server o CDN. |
| Assegnazione dei tag | A tutte le pagine o chiamate API tracciate come richieste di contenuto di Adobe Experience Manager potrebbe non essere applicato il tag tracciamento Analytics. |
| Regole di gestione dei tag | Le impostazioni delle regole di gestione dei tag possono comportare diverse configurazioni di raccolta dati su una pagina, con conseguente combinazione di discrepanze con il tracciamento delle richieste di contenuto. |
| Bot | I bot sconosciuti che AEM non ha pre-identificato e rimosso possono causare discrepanze nel tracciamento. |
| Suite per rapporti | Le pagine all’interno della stessa istanza di AEM possono generare rapporti per suite di rapporti di Analytics diverse. Questo processo può dividere i dati tra più suite, a seconda della configurazione. |
| Strumenti di monitoraggio e sicurezza di terze parti | Gli strumenti di monitoraggio e sicurezza (ad esempio, controllori di uptime o scanner di vulnerabilità) possono richiedere pagine, generando richieste di contenuto lato server non visibili nei rapporti di Analytics. |
| Accesso API | Le richieste alle pagine o ai contenuti AEM tramite API (ad esempio, tramite Adobe Experience Manager as a Headless CMS) vengono comunque conteggiate come richieste di contenuto, ma non attivano il tracciamento di Analytics. |
| Richieste di prelettura | La preacquisizione (ad esempio, utilizzando un service worker o una funzione edge) può aumentare i volumi di traffico richiedendo le pagine in anticipo. Queste richieste sono conteggiate lato server ma non eseguono il codice di analisi lato client. |
| DDOS | Adobe utilizza il filtro per rilevare e bloccare molti attacchi DDoS. Tuttavia, alcune richieste di attacco possono ancora essere conteggiate come richieste di contenuto prima dell’applicazione dei filtri. |
| Blocchi del traffico | Le funzioni di privacy nel browser o i firewall aziendali possono bloccare il caricamento degli script di analisi. Questi utenti generano ancora richieste di contenuto lato server. |
| Firewall | I firewall aziendali o regionali possono impedire alle chiamate di Analytics di raggiungere i server Adobe, causando una sottogenerazione dei rapporti in Analytics mentre i conteggi lato server rimangono invariati. |

Per informazioni su come visualizzare e tenere traccia dell&#39;utilizzo delle richieste di contenuto rispetto ai limiti di licenza, consulta la [Dashboard delle licenze](/help/implementing/cloud-manager/license-dashboard.md).

## Regole di raccolta lato server {#serverside-collection}

AEM as a Cloud Service applica regole lato server per contare le richieste di contenuto. Queste regole includono la logica per escludere bot noti (come i crawler dei motori di ricerca) e il traffico non utente come i servizi di monitoraggio che eseguono regolarmente il ping del sito.

Nelle tabelle seguenti sono elencati i tipi di richieste di contenuto incluse ed escluse, con brevi descrizioni di ciascuna.

### Tipi di richieste di contenuto incluse {#included-content-requests}

>[!NOTE]
>Se una richiesta API restituisce una risposta HTML, può essere classificata come richiesta di contenuto, a seconda del relativo contesto di utilizzo. Le richieste API che restituiscono dati non dell’interfaccia utente sono in genere escluse.

| Tipo di richiesta | Richiesta contenuto | Descrizione |
| --- | --- | --- |
| Codice HTTP 100-299 | Inclusi | Include le richieste riuscite che restituiscono contenuti HTML o JSON completi o parziali.<br>Codice HTTP 206: queste richieste forniscono solo una parte del contenuto completo. Ad esempio, un video o un’immagine di grandi dimensioni. Le richieste di contenuto parziale sono incluse quando distribuiscono parte di una risposta HTML o JSON utilizzata nel rendering del contenuto della pagina. |
| Librerie HTTP per l&#39;automazione | Inclusi | Richieste effettuate da strumenti o librerie che recuperano il contenuto della pagina. Gli esempi includono: <br>· Amazon CloudFront<br>· Apache Http Client<br>· Asynchronous HTTP Client<br>· Axios<br>· Azureus<br>· Curl<br>· GitHub Node Fetch<br>· Guzzle<br>· Go-http-client<br>· Headless Chrome<br>· Java™ Client<br>· Jersey<br>· Node Oembed<br>· okhttp<br>· Python Requests<br>· Reactor Netty<br>· Wget<br>· WinHTTP<br>· Fast HTTP<br>· GitHub Node Fetch<br>· Reactor Netty |
| Strumenti di monitoraggio e verifica stato | Inclusi | Richieste utilizzate per monitorare lo stato o la disponibilità delle pagine.<br>Consulta [Tipi di richieste di contenuto escluse](#excluded-content-request).<br>Gli esempi includono:<br>· `Amazon-Route53-Health-Check-Service`<br>· EyeMonIT_bot_version_0.1_[(https://eyemonit.com/)](https://eyemonit.com/)<br>· Investis-Site24x7<br>· Mozilla/5.0+(compatibile; UptimeRobot/2.0; [https://uptimerobot.com/](https://uptimerobot.com/))<br>· ThousandEyes-Dragonfly-x1<br>· OmtrBot/1.0<br>· WebMon/2.0.0 |
| `<link rel="prefetch">` richieste | Inclusi | Quando i clienti precaricano o recuperano preventivamente il contenuto (ad esempio, con `<link rel="prefetch">`), il sistema conta tali richieste lato server. Tieni presente che questo approccio può aumentare il traffico, a seconda di quante di queste pagine vengono preacquisite. |
| Traffico che blocca il reporting di Adobe Analytics o Google Analytics | Inclusi | È più comune che i visitatori dei siti abbiano installato software per la privacy (Ad-blocker e così via) che influiscono sulla precisione di Google Analytics o Adobe Analytics. AEM as a Cloud Service conta le richieste sul primo punto di ingresso nell’infrastruttura gestita da Adobe e non sul lato client. |

Vedi anche [Dashboard delle licenze](/help/implementing/cloud-manager/license-dashboard.md).

### Tipi di richieste di contenuto escluse {#excluded-content-request}

| Tipo di richiesta | Richiesta contenuto | Descrizione |
| --- | --- | --- |
| Codice HTTP 500+ | Escluso | Sono stati restituiti errori al visitatore quando si verifica un errore in AEM as a Cloud Service o nel codice personalizzato del cliente. |
| Codice HTTP 400-499 | Escluso | Sono stati restituiti errori al visitatore se il contenuto non esiste (404) o si sono verificati altri problemi relativi al contenuto o alle richieste. |
| Codice HTTP 300-399 | Escluso | Richieste valide che verificano se qualcosa è cambiato sul server o reindirizzano la richiesta a un’altra risorsa. Non contengono contenuto in sé, quindi non sono fatturabili. |
| Richieste indirizzate a `/libs/`* | Escluso | Richieste JSON interne di AEM, ad esempio il token CSRF non fatturabile. |
| Traffico da attacchi DDOS | Escluso | Protezione DDOS. AEM rileva automaticamente alcuni degli attacchi DDOS e li blocca. Gli attacchi DDOS rilevati non sono fatturabili. |
| Monitoraggio di AEM as a Cloud Service New Relic | Escluso | Monitoraggio globale di AEM as a Cloud Service. |
| URL per i clienti per monitorare il proprio programma Cloud Service | Escluso | Adobe consiglia di utilizzare l&#39;URL per monitorare la disponibilità o il controllo dello stato esternamente.<br><br>`/system/probes/health` |
| Servizio di riscaldamento AEM as a Cloud Service Pod | Escluso |
| Agente: skyline-service-warm/1.* |
| Motori di ricerca noti, social network e librerie HTTP (contrassegnati da Fastly) | Escluso | Servizi noti che visitano regolarmente il sito per aggiornare l&#39;indice o il servizio di ricerca:<br><br>Esempi:<br>· AddSearchBot<br>· AhrefsBot<br>· Applebot<br>· Chiedi a Jeeves Corporate Spider<br>· Bingbot<br>· BingPreview<br>· BLEXBot<br>· BuiltWith<br>· Bytespider<br>· CrawlerKengo<br>· Facebookexternalhit<br>· Google Google AdsBot<br> AdsBot Mobile<br>· Googlebot<br>· Googlebot Mobile<br>· lmspider<br>· LucidWorks<br>· `MJ12bot`<br>· Pinterest<br>· SemrushBot<br>· SiteImprove<br>· StashBot<br>· StatusCake<br>· YandexBot<br>· ContentKing<br>· Claudebot |
| Escludere le chiamate Commerce integration framework | Escluso | Le richieste effettuate ad AEM che vengono inoltrate a Commerce integration framework, l&#39;URL inizia con `/api/graphql`, per evitare un doppio conteggio, non sono fatturabili per Cloud Service. |
| Escludi `manifest.json` | Escluso | Il manifesto non è una chiamata API. È qui per fornire informazioni su come installare siti web su un desktop o un telefono cellulare. Adobe non deve contare la richiesta JSON a `/etc.clientlibs/*/manifest.json` |
| Escludi `favicon.ico` | Escluso | Anche se il contenuto restituito non deve essere HTML o JSON, si è osservato che alcuni scenari come i flussi di autenticazione SAML restituiscono favicon come HTML. Di conseguenza, le favicon sono esplicitamente escluse dal conteggio. |
