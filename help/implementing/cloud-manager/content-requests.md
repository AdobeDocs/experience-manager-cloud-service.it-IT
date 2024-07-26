---
title: Informazioni sulle richieste di contenuto di Cloud Service
description: Se hai acquistato licenze per richieste di contenuto da Adobe, scopri i tipi di richieste di contenuto che Adobe Experience Cloud as a Service misura e le varianze con gli strumenti di reporting di Analytics di un’organizzazione.
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: af2985f29cb867162061bbac465b19637aa0ecad
workflow-type: tm+mt
source-wordcount: '1405'
ht-degree: 10%

---

# Richieste di contenuto Cloud Service

## Introduzione {#introduction}

Le richieste di contenuto sono richieste pervenute in AEM Sites (anche in relazione a Edge Delivery Services per AEM Sites) o in qualsiasi sistema di caching fornito dal cliente (come una rete per la distribuzione di contenuti) per distribuire contenuti o dati in formato HTML tramite visualizzazioni di pagina (ad esempio, pagine e frammenti di esperienza) o in formato JSON tramite chiamate API (in modo headless). Le richieste di contenuto vengono conteggiate come visualizzazione pagina o 5 chiamate API e vengono misurate all’ingresso del primo sistema di caching che riceve una richiesta di contenuto. Alcune richieste HTTP sono incluse o escluse ai fini del conteggio delle richieste di contenuto. L’elenco completo delle richieste HTTP incluse ed escluse e le relative definizioni tecniche sono disponibili nella documentazione.

## Informazioni sulle richieste di contenuto di Cloud Service {#understanding-cloud-service-content-requests}

Per i clienti che utilizzano la rete CDN preconfigurata, le richieste di contenuto del Cloud Service vengono misurate tramite la raccolta di dati lato server. Questa raccolta è abilitata tramite l’analisi del registro CDN. Le richieste di contenuto vengono raccolte automaticamente lato server ai margini di Adobe Experience Manager as a Cloud Service, tramite l’analisi automatizzata dei file di registro provenienti dalla rete CDN di AEM as a Cloud Service. Questa operazione viene eseguita isolando dal CDN le richieste che restituiscono il contenuto HTML `(text/html)` o JSON `(application/json)` e si basa su diverse regole di inclusione ed esclusione descritte di seguito. Una richiesta di contenuto si verifica indipendentemente dal contenuto restituito distribuito dalle cache CDN o dal contenuto che ritorna all’origine della CDN (dispatcher dell’AEM).

Per i clienti che utilizzano la propria rete CDN, la raccolta lato client offre un riflesso più preciso delle interazioni, garantendo una misura affidabile del coinvolgimento del sito web tramite il servizio [Monitoraggio dell&#39;uso reale](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md). In questo modo i clienti possono ottenere informazioni avanzate sul traffico e sulle prestazioni delle loro pagine. Pur essendo utile per tutti i clienti, offre un riflesso rappresentativo delle interazioni degli utenti, garantendo una misura affidabile del coinvolgimento del sito web acquisendo il numero di visualizzazioni di pagina dal lato client.

Per i clienti che utilizzano la propria rete CDN oltre ad AEM as a Cloud Service, il reporting lato server restituisce numeri che non possono essere utilizzati per confrontare con le richieste di contenuto concesse in licenza. Con il [Monitoraggio Real Use](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md), Adobe può riflettere una misura affidabile del coinvolgimento del sito Web.


### Varianze delle richieste di contenuto del Cloud Service {#content-requests-variances}

Le richieste di contenuto possono presentare varianze all’interno degli strumenti di reporting di Analytics di un’organizzazione, come riepilogato nella tabella seguente. In generale, *non* utilizza strumenti di analisi che raccolgono dati tramite strumenti lato client per generare rapporti sul numero di richieste di contenuto per un determinato sito, semplicemente perché spesso dipendono dal consenso dell&#39;utente ad essere attivati, perdendo così una frazione significativa del traffico. Gli strumenti di Analytics che raccolgono i dati lato server nei file di registro, o i rapporti CDN per i clienti che aggiungono la propria CDN oltre ad AEM as a Cloud Service, forniranno conteggi migliori. Per la generazione di rapporti sulle visualizzazioni di pagina e sulle relative prestazioni, l&#39;opzione consigliata di Adobe è [Adobe RUM Data Service](/help/sites-cloud/administering/real-use-monitoring-for-aem-as-a-cloud-service.md).

| Motivo della varianza | Spiegazione |
|---|---|
| Consenso utente finale | Gli strumenti di Analytics che si basano su strumentazione lato client spesso dipendono dal consenso dell’utente all’attivazione. Questo potrebbe rappresentare la maggior parte del traffico che non viene tracciato. Per i clienti che desiderano misurare autonomamente le richieste di contenuto, si consiglia di utilizzare gli strumenti di analisi per raccogliere i dati lato server o i rapporti CDN. |
| Assegnazione dei tag | A tutte le pagine o chiamate API tracciate come richieste di contenuto di Adobe Experience Manager potrebbe non essere applicato il tag tracciamento Analytics. |
| Regole di gestione dei tag | Le impostazioni delle regole di gestione dei tag possono comportare diverse configurazioni di raccolta dati su una pagina, con conseguente combinazione di discrepanze con il tracciamento delle richieste di contenuto. |
| Bot | I bot sconosciuti che non sono stati pre-identificati e rimossi da AEM possono causare discrepanze nel tracciamento. |
| Suite per rapporti | Le pagine che fanno parte della stessa istanza di AEM e dello stesso dominio possono inviare dati a suite per rapporti di Analytics diverse. |
| Strumenti di monitoraggio e sicurezza di terze parti | Gli strumenti di monitoraggio e sicurezza possono generare richieste di contenuto per AEM che non vengono monitorate nei rapporti di Analytics. |
| Accesso API | L’accesso a livello di programmazione a pagine o API Adobe Experience Manager può generare richieste di contenuto per AEM che non vengono tracciate nei rapporti di Analytics. |
| Richieste di prelettura | L’utilizzo di un servizio di prelettura per precaricare le pagine al fine di aumentare la velocità può causare un aumento significativo del traffico delle richieste di contenuto. |
| DDOS | Adobe tenta di rilevare e filtrare automaticamente il traffico dagli attacchi DDOS, ma non garantisce che tutti i possibili attacchi DDOS vengano rilevati. |
| Blocchi del traffico | L’utilizzo di un blocco del tracciamento in un browser può far sì che il tracciamento di alcune richieste non venga eseguito. |
| Firewall | I firewall possono bloccare il tracciamento di Analytics. Questo scenario è più frequente con i firewall aziendali. |

Vedi anche [Dashboard delle licenze](/help/implementing/cloud-manager/license-dashboard.md).

## Regole di raccolta lato server {#serverside-collection}

Esistono regole in vigore per escludere bot noti, tra cui servizi noti che visitano regolarmente il sito per aggiornare l’indice di ricerca o il servizio.

### Tipi di richieste di contenuto incluse {#included-content-requests}

| Tipo di richiesta | Richiesta contenuto | Descrizione |
| --- | --- | --- |
| Codice HTTP 100-299 | Inclusi | Si tratta di richieste regolari che forniscono contenuto completo o parziale. |
| Librerie HTTP per l&#39;automazione | Inclusi | Esempi:<br>· Amazon CloudFront<br>· Apache Http Client<br>· Asynchronous Http Client<br>· Axios<br>· Azureus<br>· Curl<br>· GitHub Node Fetch<br>· Guzzle<br>· Go-http-client<br>· Headless Chrome<br>· Java™ Client<br>· Jersey<br>· Node Oembed<br>· okhttp<br>· Python Requests<br>· Reactor NWetty<br> get<br>· WinHTTP |
| Strumenti di monitoraggio e verifica stato | Inclusi | Questi vengono configurati dal cliente per monitorare un determinato aspetto del sito. Ad esempio, disponibilità o prestazioni reali degli utenti. Se questi endpoint sono specifici come /system/probes/health per i controlli di integrità, è consigliabile utilizzare l&#39;endpoint `/system/probes/health` e non le pagine HTML effettive del sito.[Vedi di seguito](#excluded-content-request)<br>Esempi:<br>· Amazon-Route53-Health-Check-Service<br>· EyeMonIT_bot_version_0.1_[(https://www.eyemon.it/)](https://www.eyemon.it/)<br>· Investis-Site24x7<br>· Mozilla/5.0+(compatibile; UptimeRobot/2.0; [https://uptimerobot.com/](https://uptimerobot.com/))<br>· ThousandEyes-Dragonfly-x1<br>· OmtrBot/1.0<br>· WebMon/2.0.0 |
| `<link rel="prefetch">` richieste | Inclusi | Per aumentare la velocità di caricamento della pagina successiva, i clienti possono fare in modo che il browser carichi un set di pagine prima che l’utente faccia clic sul collegamento, in modo che si trovino già nella cache. *Attenzione: questo sta aumentando in modo significativo il traffico*, a seconda di quante di queste pagine vengono preacquisite. |
| Traffico che blocca il reporting di Adobe Analytics o Google Analytics | Inclusi | È più comune che i visitatori dei siti abbiano installato software per la privacy (Ad-blocker e così via) che influiscono sulla precisione della Google Analytics o di Adobe Analytics. AEM as a Cloud Service conta le richieste sul primo punto di ingresso nell’infrastruttura gestita da Adobe e non sul lato client. |

Vedi anche [Dashboard delle licenze](/help/implementing/cloud-manager/license-dashboard.md).

### Tipi di richieste di contenuto escluse {#excluded-content-request}

| Tipo di richiesta | Richiesta contenuto | Descrizione |
| --- | --- | --- |
| Codice HTTP 500+ | Escluso | Sono stati restituiti errori al visitatore quando si verifica un errore in AEM as a Cloud Service o nel codice personalizzato del cliente. |
| Codice HTTP 400-499 | Escluso | Sono stati restituiti errori al visitatore se il contenuto non esiste (404) o si sono verificati altri problemi relativi al contenuto o alle richieste. |
| Codice HTTP 300-399 | Escluso | Si tratta di richieste valide che verificano se qualcosa è cambiato sul server o reindirizzano la richiesta a un’altra risorsa. Non contengono contenuto in sé, quindi non sono fatturabili. |
| Richieste indirizzate a /libs/* | Escluso | Richieste JSON interne dell’AEM, ad esempio il token CSRF non fatturabile. |
| Traffico da attacchi DDOS | Escluso | Protezione DDOS. L’AEM rileva automaticamente alcuni degli attacchi DDOS e li blocca. Gli attacchi DDOS rilevati non sono fatturabili. |
| Monitoraggio di AEM as a Cloud Service New Relic | Escluso | Monitoraggio globale di AEM as a Cloud Service. |
| URL per i clienti per monitorare il programma di Cloud Service | Escluso | È consigliabile utilizzare l&#39;URL per monitorare esternamente la disponibilità o il controllo dello stato.<br><br>`/system/probes/health` |
| Servizio di riscaldamento AEM as a Cloud Service Pod | Escluso |
| Agente: skyline-service-warm/1.* |
| Motori di ricerca noti, social network e librerie HTTP (contrassegnati da Fastly) | Escluso | Servizi noti che visitano regolarmente il sito per aggiornare l&#39;indice o il servizio di ricerca:<br><br>Esempi:<br>· AddSearchBot<br>· AhrefsBot<br>· Applebot<br>· Chiedi a Jeeves Corporate Spider<br>· Bingbot<br>· BingPreview<br>· BLEXBot<br>· BuiltWith<br>· Bytespider<br>· CrawlerKengo<br>· Facebookexternalhit<br>· Google Google AdsBot<br> dsBot Mobile<br>· Googlebot<br>· Googlebot Mobile<br>· lmspider<br>· LucidWorks<br>· MJ12bot<br>· PKingdom<br>· Pinterest<br>· SemrushBot<br>· SiteImprove<br>· StashBot<br>· StatusCake<br>· YandexBot |
| Escludi chiamate Commerce integration framework | Escluso | Si tratta di richieste effettuate all&#39;AEM che vengono inoltrate alla Commerce integration framework (l&#39;URL inizia con `/api/graphql`) per evitare un doppio conteggio, non sono fatturabili per il Cloud Service. |
| Escludi `manifest.json` | Escluso | Manifest non è una chiamata API, è qui per fornire informazioni su come installare siti web sul desktop o sul telefono cellulare. L&#39;Adobe non deve contare la richiesta JSON a `/etc.clientlibs/*/manifest.json` |
| Escludi `favicon.ico` | Escluso | Anche se il contenuto restituito non deve essere HTML o JSON, si osserva che in alcuni scenari come i flussi di autenticazione SAML, le favicon possono essere restituite come HTML, pertanto sono esplicitamente escluse dal conteggio. |
