---
title: Comprendere le richieste di contenuto di Cloud Service
description: Se hai acquistato licenze per richieste di contenuto da Adobe, scopri i tipi di richieste di contenuto che Adobe Experience Cloud as a Service misura e le varianze con gli strumenti di reporting di Analytics di un’organizzazione.
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f24b2672431ecf7b7b0ed11b6dc9b09344946239
workflow-type: tm+mt
source-wordcount: '1276'
ht-degree: 9%

---

# Comprendere le richieste di contenuto del Cloud Service

## Introduzione {#introduction}

Le richieste di contenuto si riferiscono alle richieste effettuate ad AEM Sites, comprese quelle relative a Edge Delivery Services o sistemi di caching forniti dal cliente come una rete per la distribuzione di contenuti. Queste richieste distribuiscono contenuti o dati in formato HTML tramite le visualizzazioni di pagina (ad esempio, pagine e frammenti di esperienza) o in formato JSON tramite chiamate API in modo headless. Le richieste di contenuto vengono conteggiate come visualizzazione di pagina o cinque chiamate API e vengono misurate all’ingresso del primo sistema di caching che riceve una richiesta di contenuto. Alcune richieste HTTP sono incluse o escluse ai fini del conteggio delle richieste di contenuto. L’elenco completo delle richieste HTTP incluse ed escluse e le relative definizioni tecniche sono disponibili nella documentazione.

## Informazioni sulle richieste di contenuto di Cloud Service {#understanding-cloud-service-content-requests}

Per i clienti che utilizzano la rete CDN preconfigurata, le richieste di contenuto del Cloud Service vengono misurate tramite la raccolta di dati lato server. Questa raccolta è abilitata tramite l’analisi del registro CDN. L’AEM (Adobe Experience Manager as a Cloud Service) raccoglie automaticamente le richieste di contenuto lato server al server Edge di. Analizza i file di registro generati dalla rete CDN di AEM as a Cloud Service. Questa procedura viene eseguita isolando dalla rete CDN le richieste che restituiscono il contenuto HTML `(text/html)` o JSON `(application/json)` e si basa su diverse regole di inclusione ed esclusione descritte di seguito. Una richiesta di contenuto si verifica indipendentemente dal fatto che il contenuto venga distribuito dalle cache CDN o restituito all’origine CDN (dispatcher dell’AEM).

<!-- REMOVED AS PER EMAIL REQUEST FROM SHWETA DUA, JULY 30, 2024 TO RICK BROUGH AND ALEXANDRU SARCHIZ   For customers employing their own CDN, client-side collection offers a more precise reflection of interactions, ensuring a reliable measure of website engagement via the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md) service. This gives customers advanced insights into their page traffic and performance. While it is beneficial for all customers, it offers a representative reflection of user interactions, ensuring a reliable measure of website engagement by capturing the number of page views from the client side. 

For customers that bring their own CDN on top of AEM as a Cloud Service, server-side reporting results in numbers that cannot be used to compare with the licensed content requests. With the [Real Use Monitoring](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md), Adobe can reflect a reliable measure of website engagement. -->

### Varianze nelle richieste di contenuto del Cloud Service {#content-requests-variances}

Le richieste di contenuto possono presentare varianze all’interno degli strumenti di reporting di Analytics di un’organizzazione, come riepilogato nella tabella seguente. In generale, evita di utilizzare strumenti di analisi che si basano su strumenti lato client per segnalare il numero di richieste di contenuto per un sito. Questi strumenti spesso perdono una grande parte del traffico perché dipendono dal consenso degli utenti per essere attivati. Gli strumenti di Analytics che raccolgono i dati lato server nei file di registro, o i rapporti CDN per i clienti che aggiungono la propria CDN oltre ad AEM as a Cloud Service, forniscono conteggi migliori.

| Motivo della varianza | Spiegazione |
|---|---|
| Consenso utente finale | Gli strumenti di Analytics che si basano su strumentazione lato client spesso dipendono dal consenso dell’utente all’attivazione. Questo flusso di lavoro potrebbe rappresentare la maggior parte del traffico che non viene tracciato. Per i clienti che desiderano misurare autonomamente le richieste di contenuto, si consiglia di utilizzare gli strumenti di analisi per raccogliere i dati lato server o i rapporti CDN. |
| Assegnazione dei tag | A tutte le pagine o chiamate API tracciate come richieste di contenuto di Adobe Experience Manager potrebbe non essere applicato il tag tracciamento Analytics. |
| Regole di gestione dei tag | Le impostazioni delle regole di gestione dei tag possono comportare diverse configurazioni di raccolta dati su una pagina, con conseguente combinazione di discrepanze con il tracciamento delle richieste di contenuto. |
| Bot | I bot sconosciuti che l’AEM non ha pre-identificato e rimosso possono causare discrepanze nel tracciamento. |
| Suite per rapporti | Le pagine che fanno parte della stessa istanza di AEM e dello stesso dominio possono inviare dati a suite per rapporti di Analytics diverse. |
| Strumenti di monitoraggio e sicurezza di terze parti | Gli strumenti di monitoraggio e sicurezza possono generare richieste di contenuto per AEM che non vengono monitorate nei rapporti di Analytics. |
| Accesso API | L’accesso a livello di programmazione a pagine o API Adobe Experience Manager può generare richieste di contenuto per AEM che non vengono tracciate nei rapporti di Analytics. |
| Richieste di prelettura | L’utilizzo di un servizio di prelettura per precaricare le pagine al fine di aumentare la velocità può causare un aumento significativo del traffico delle richieste di contenuto. |
| DDOS | Sebbene Adobe effettui tentativi di rilevare e filtrare automaticamente il traffico dagli attacchi DDOS, non c’è alcuna garanzia che tutti i possibili attacchi DDOS vengano rilevati. |
| Blocchi del traffico | L’utilizzo di un blocco del tracciamento in un browser può far sì che il tracciamento di alcune richieste non venga eseguito. |
| Firewall | I firewall possono bloccare il tracciamento di Analytics. Questo scenario è più frequente con i firewall aziendali. |

Vedi anche [Dashboard delle licenze](/help/implementing/cloud-manager/license-dashboard.md).

## Regole di raccolta lato server {#serverside-collection}

Esistono regole in vigore per escludere bot noti, tra cui servizi noti che visitano regolarmente il sito per aggiornare l’indice di ricerca o il servizio.

### Tipi di richieste di contenuto incluse {#included-content-requests}

| Tipo di richiesta | Richiesta contenuto | Descrizione |
| --- | --- | --- |
| Codice HTTP 100-299 | Inclusi | Richieste regolari che forniscono contenuto completo o parziale. |
| Librerie HTTP per l&#39;automazione | Inclusi | Esempi:<br>· Amazon CloudFront<br>· Apache Http Client<br>· Asynchronous HTTP Client<br>· Axios<br>· Azureus<br>· Curl<br>· GitHub Node Fetch<br>· Guzzle<br>· Go-http-client<br>· Headless Chrome<br>· Java™ Client<br>· Jersey<br>· Node Oembed<br>· okhttp<br>· Python Requests<br>· Reactor Netty<br> <br>· WinHTTP<br>· HTTP rapido<br>· Recupero nodo GitHub<br>· Reactor Netty |
| Strumenti di monitoraggio e verifica stato | Inclusi | Impostato dal cliente per monitorare un determinato aspetto del sito. Ad esempio, disponibilità o prestazioni reali degli utenti. Se eseguono il targeting di endpoint specifici come `/system/probes/health` per i controlli di integrità, Adobe consiglia di utilizzare l&#39;endpoint `/system/probes/health` e non le pagine HTML effettive del sito. [Vedi di seguito](#excluded-content-request)<br>Esempi:<br>· `Amazon-Route53-Health-Check-Service`<br>· EyeMonIT_bot_version_0.1_[(https://eyemonit.com/)](https://eyemonit.com/)<br>· Investis-Site24x7<br>· Mozilla/5.0+(compatibile; UptimeRobot/2.0; [https://uptimerobot.com/](https://uptimerobot.com/))<br>· ThousandEyes-Dragonfly-x1<br>· OmtrBot/1.0<br>· WebMon/2.0.0 |
| `<link rel="prefetch">` richieste | Inclusi | Per aumentare la velocità di caricamento della pagina successiva, i clienti possono fare in modo che il browser carichi un set di pagine prima che l’utente faccia clic sul collegamento, in modo che si trovino già nella cache. *Attenzione: questo approccio aumenta notevolmente il traffico*, a seconda di quante di queste pagine vengono preacquisite. |
| Traffico che blocca il reporting di Adobe Analytics o Google Analytics | Inclusi | È più comune che i visitatori dei siti abbiano installato software per la privacy (Ad-blocker e così via) che influiscono sulla precisione della Google Analytics o di Adobe Analytics. AEM as a Cloud Service conta le richieste sul primo punto di ingresso nell’infrastruttura gestita da Adobe e non sul lato client. |

Vedi anche [Dashboard delle licenze](/help/implementing/cloud-manager/license-dashboard.md).

### Tipi di richieste di contenuto escluse {#excluded-content-request}

| Tipo di richiesta | Richiesta contenuto | Descrizione |
| --- | --- | --- |
| Codice HTTP 500+ | Escluso | Sono stati restituiti errori al visitatore quando si verifica un errore in AEM as a Cloud Service o nel codice personalizzato del cliente. |
| Codice HTTP 400-499 | Escluso | Sono stati restituiti errori al visitatore se il contenuto non esiste (404) o si sono verificati altri problemi relativi al contenuto o alle richieste. |
| Codice HTTP 300-399 | Escluso | Richieste valide che verificano se qualcosa è cambiato sul server o reindirizzano la richiesta a un’altra risorsa. Non contengono contenuto in sé, quindi non sono fatturabili. |
| Richieste indirizzate a /libs/* | Escluso | Richieste JSON interne dell’AEM, ad esempio il token CSRF non fatturabile. |
| Traffico da attacchi DDOS | Escluso | Protezione DDOS. L’AEM rileva automaticamente alcuni degli attacchi DDOS e li blocca. Gli attacchi DDOS rilevati non sono fatturabili. |
| Monitoraggio di AEM as a Cloud Service New Relic | Escluso | Monitoraggio globale di AEM as a Cloud Service. |
| URL per i clienti per monitorare il programma di Cloud Service | Escluso | Adobe consiglia di utilizzare l&#39;URL per monitorare la disponibilità o il controllo dello stato esternamente.<br><br>`/system/probes/health` |
| Servizio di riscaldamento AEM as a Cloud Service Pod | Escluso |
| Agente: skyline-service-warm/1.* |
| Motori di ricerca noti, social network e librerie HTTP (contrassegnati da Fastly) | Escluso | Servizi noti che visitano regolarmente il sito per aggiornare l&#39;indice o il servizio di ricerca:<br><br>Esempi:<br>· AddSearchBot<br>· AhrefsBot<br>· Applebot<br>· Chiedi a Jeeves Corporate Spider<br>· Bingbot<br>· BingPreview<br>· BLEXBot<br>· BuiltWith<br>· Bytespider<br>· CrawlerKengo<br>· Facebookexternalhit<br>· Google Google AdsBot<br> dsBot Mobile<br>· Googlebot<br>· Googlebot Mobile<br>· lmspider<br>· LucidWorks<br>· `MJ12bot`<br>· Pinterest<br>· SemrushBot<br>· SiteImprove<br>· StashBot<br>· StatusCake<br>· YandexBot<br>· Claudebot |
| Escludi chiamate Commerce integration framework | Escluso | Le richieste effettuate all&#39;AEM che vengono inoltrate alla Commerce integration framework (l&#39;URL inizia con `/api/graphql`) per evitare un doppio conteggio, non sono fatturabili per il Cloud Service. |
| Escludi `manifest.json` | Escluso | Il manifesto non è una chiamata API. È qui per fornire informazioni su come installare siti web su un desktop o un telefono cellulare. Adobe non deve contare la richiesta JSON a `/etc.clientlibs/*/manifest.json` |
| Escludi `favicon.ico` | Escluso | Anche se il contenuto restituito non deve essere HTML o JSON, si è osservato che alcuni scenari come i flussi di autenticazione SAML restituiscono favicons come HTML. Di conseguenza, le favicon sono esplicitamente escluse dal conteggio. |
| Proxy CDN a un altro back-end | Escluso | Le richieste indirizzate a diversi backend non AEM utilizzando la tecnica [CDN Origin Selectors](/help/implementing/dispatcher/cdn-configuring-traffic.md#origin-selectors) sono escluse in quanto non raggiungono l&#39;AEM. |
