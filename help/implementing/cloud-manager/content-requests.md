---
title: Informazioni sulle richieste di contenuto di Cloud Service
description: Se hai acquistato licenze per richieste di contenuto da Adobe, scopri i tipi di richieste di contenuto che Adobe Experience Cloud as a Service misura e le varianze con gli strumenti di reporting di Analytics di un’organizzazione.
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
source-git-commit: 25a4a6b9ae09cb71f50317990af1718db1e14355
workflow-type: tm+mt
source-wordcount: '1171'
ht-degree: 12%

---

# Richieste di contenuto Cloud Service

## Varianze delle richieste di contenuto del Cloud Service{#content-requests-variances}

Le richieste di contenuto possono presentare varianze con gli strumenti di reporting di Analytics di un’organizzazione, come riepilogato nella tabella seguente. In generale, gli strumenti di Analytics che raccolgono dati tramite la strumentazione lato client <b>non deve essere utilizzato</b> per generare rapporti sul numero di richieste di contenuto per un determinato sito, semplicemente perché spesso dipendono dal consenso dell’utente finale per essere attivate, perdendo quindi una frazione significativa del traffico. Gli strumenti di Analytics che raccolgono i dati lato server nei file di registro, o i rapporti CDN per i clienti che aggiungono la propria CDN oltre a AEM as a Cloud Service, forniranno conteggi migliori. Per la generazione di rapporti sulle visualizzazioni di pagina e sulle relative prestazioni, l’opzione consigliata è l’Adobe Adobe di RUM Data Service (Servizio dati RUM).

| Motivo della varianza | Spiegazione |
|---|---|
| Consenso utente finale | Gli strumenti di Analytics che si basano su strumenti lato client spesso dipendono dal consenso dell’utente finale per essere attivati. Questo potrebbe rappresentare la maggior parte del traffico che non viene tracciato. Per i clienti che desiderano misurare autonomamente le richieste di contenuto, si consiglia di utilizzare gli strumenti di analisi per raccogliere i dati lato server o i rapporti CDN. |
| Assegnazione dei tag | A tutte le pagine o chiamate API tracciate come richieste di contenuto di Adobe Experience Manager (AEM) potrebbero non essere assegnati tag di tracciamento Analytics. |
| Regole di gestione dei tag | Le impostazioni delle regole di gestione dei tag possono comportare diverse configurazioni di raccolta dati su una pagina, con conseguente combinazione di discrepanze con il tracciamento delle richieste di contenuto. |
| Bot | I bot sconosciuti che non sono stati pre-identificati e rimossi da AEM possono causare discrepanze nel tracciamento. |
| Suite per rapporti | Le pagine che fanno parte della stessa istanza di AEM e dello stesso dominio possono inviare dati a suite per rapporti di Analytics diverse. |
| Strumenti di monitoraggio e sicurezza di terze parti | Gli strumenti di monitoraggio e sicurezza possono generare richieste di contenuto per AEM che non vengono monitorate nei rapporti di Analytics. |
| Accesso API | L’accesso a livello di programmazione a pagine o API Adobe Experience Manager può generare richieste di contenuto per AEM che non vengono tracciate nei rapporti di Analytics. |
| Richieste di prelettura | L’utilizzo di un servizio di prelettura per precaricare le pagine al fine di aumentare la velocità può causare un aumento significativo del traffico delle richieste di contenuto. |
| DDOS | Sebbene Adobe si impegni al massimo a rilevare e filtrare automaticamente il traffico dagli attacchi DDOS, non c’è alcuna garanzia che tutti i possibili attacchi DDOS vengano rilevati. |
| Blocchi del traffico | L’utilizzo di un blocco del tracciamento in un browser può far sì che il tracciamento di alcune richieste non venga eseguito. |
| Firewall | I firewall possono bloccare il tracciamento di Analytics. Questo scenario è più frequente con i firewall aziendali. |

Vedi anche [Dashboard delle licenze](/help/implementing/cloud-manager/license-dashboard.md).

## Informazioni sulle richieste di contenuto di Cloud Service {#about-content-request}

Le richieste di contenuto vengono tracciate automaticamente ai margini di Adobe Experience Manager (AEM) as a Cloud Service, tramite l’analisi automatizzata dei file di registro provenienti dalla rete CDN as a Cloud Service dall’AEM, isolando le richieste che restituiscono contenuto HTML (text/html) o JSON (application/json) dalla rete CDN e in base a una serie di regole di inclusione e esclusione descritte di seguito. Una richiesta di contenuto si verifica indipendentemente dal contenuto restituito distribuito dalle cache CDN o che ritorna all’origine della CDN (dispatcher AEM).

Per i clienti che utilizzano una propria rete CDN oltre a quella as a Cloud Service per AEM, questo tracciamento risulterà in numeri che non possono essere utilizzati per confrontare con le richieste di contenuto concesse in licenza e che dovranno essere misurati dal cliente al margine della rete CDN esterna.

Esistono regole in vigore per escludere bot noti, tra cui servizi noti che visitano regolarmente il sito per aggiornare l’indice di ricerca o il servizio.

### Tipi di richieste di contenuto incluse{#included-content-requests}

| Tipo di richiesta | Richiesta contenuto | Descrizione |
| --- | --- | --- |
| Codice HTTP 100-299 | Incluso | Si tratta di richieste regolari che forniscono contenuto completo o parziale. |
| Librerie HTTP per l&#39;automazione | Incluso | Esempi:<br>· Amazon CloudFront<br>· Client Apache Http<br>· Client HTTP asincrono<br>· Assi<br>· Azureo<br>· Curl<br>· Recupero nodo GitHub<br>· Guscio<br>· Go-http-client<br>· Chrome headless<br>· Client Java™<br>· Jersey<br>· Node Oembed<br>· okhttp<br>· Richieste Python<br>· Reactor Netty<br>· Wget<br>· WinHTTP |
| Strumenti di monitoraggio e verifica stato | Incluso | Questi vengono configurati dal cliente per monitorare un determinato aspetto del sito. Ad esempio, disponibilità o prestazioni reali degli utenti. Utilizzare `/system/probes/health` e non le pagine HTML effettive del sito.<br>Esempi:<br>· Amazon-Route53-Health-Check-Service<br>· EyeMonIT_bot_version_0.1_[(https://www.eyemon.it/)](https://www.eyemon.it/)<br>· Investis-Site24x7<br>· Mozilla/5.0+(compatibile; UptimeRobot/2.0; [https://uptimerobot.com/](https://uptimerobot.com/))<br>· ThousandEyes-Dragonfly-x1<br>· OmtrBot/1.0<br>· WebMon/2.0.0 |
| `<link rel="prefetch">` richieste | Incluso | Per aumentare la velocità di caricamento della pagina successiva, i clienti possono fare in modo che il browser carichi un set di pagine prima che l’utente faccia clic sul collegamento, in modo che si trovino già nella cache. *Attenzione: questo sta aumentando notevolmente il traffico*- a seconda del numero di pagine preacquisite. |
| Traffico che blocca il reporting di Adobe Analytics o Google Analytics | Incluso | È più comune che i visitatori dei siti abbiano installato software per la privacy (Ad-blocker e così via) che influiscono sulla precisione della Google Analytics o di Adobe Analytics. L’AEM as a Cloud Service conta le richieste sul primo punto di ingresso nell’infrastruttura gestita dall’Adobe e non sul lato client. |

Vedi anche [Dashboard delle licenze](/help/implementing/cloud-manager/license-dashboard.md).

### Tipi di richieste di contenuto escluse{#excluded-content-request}

| Tipo di richiesta | Richiesta contenuto | Descrizione |
| --- | --- | --- |
| Codice HTTP 500+ | Escluso | Sono stati restituiti errori al visitatore quando si verifica un errore in AEM as a Cloud Service o nel codice personalizzato del cliente. |
| Codice HTTP 400-499 | Escluso | Sono stati restituiti errori al visitatore se il contenuto non esiste (404) o si sono verificati altri problemi relativi al contenuto o alle richieste. |
| Codice HTTP 300-399 | Escluso | Si tratta di richieste valide che verificano se qualcosa è cambiato sul server o reindirizzano la richiesta a un’altra risorsa. Non contengono contenuto in sé, quindi non sono fatturabili. |
| Richieste indirizzate a /libs/* | Escluso | Richieste JSON interne dell’AEM, ad esempio il token CSRF non fatturabile. |
| Traffico da attacchi DDOS | Escluso | Protezione DDOS. L’AEM rileva automaticamente alcuni degli attacchi DDOS e li blocca. Gli attacchi DDOS rilevati non sono fatturabili.<br><br>Tipi DDOS rilevati automaticamente:<br>· DDOSBlockedCiphersSHA<br>· DDOSBlockedPattern<br>· DDOSSuspiciousRequest |
| Monitoraggio New Relic as a Cloud Service AEM | Escluso | Monitoraggio globale as a Cloud Service dell’AEM. |
| URL per i clienti per monitorare il programma di Cloud Service | Escluso | URL consigliato per monitorare esternamente la disponibilità.<br><br>`/system/probes/health` |
| Servizio di riscaldamento del pod as a Cloud Service dell&#39;AEM | Escluso | Agente utente: skyline-service-warm/1.* |
| Motori di ricerca noti, social network e librerie HTTP (contrassegnati da Fastly) | Escluso | Servizi noti visitano regolarmente il sito per aggiornare l’indice di ricerca o il servizio:<br><br>Esempi:<br>· AddSearchBot<br>· AhrefsBot<br>· Applebot<br>· Chiedi a Jeeves Corporate Spider<br>· Bingbot<br>· BingPreview<br>BLEXBot<br>· Incorporato<br>· Bytespider<br>· CrawlerKengo<br>· Facebookexternalhit<br>· Google AdsBot<br>· Google AdsBot Mobile<br>· Googlebot<br>· GoogleBot Mobile<br>· lmspider<br>· LucidWorks<br>MJ12bot<br>· Penna<br>· Pinterest<br>· SemrushBot<br>· Miglioramento del sito<br>· StashBot<br>· StatusCake<br>· YandexBot |
| Escludi chiamate Commerce integration framework | Escluso | Si tratta di richieste effettuate all’AEM che vengono inoltrate alla Commerce integration framework: l’URL inizia con `/api/graphql`- per evitare il doppio conteggio, non sono fatturabili per il Cloud Service. |
| Escludi `manifest.json` | Escluso | Manifest non è una chiamata API, è qui per fornire informazioni su come installare siti web sul desktop o sul telefono cellulare. L’Adobe non deve contare la richiesta JSON a `/etc.clientlibs/*/manifest.json` |
| Escludi `favicon.ico` | Escluso | Anche se il contenuto restituito non deve essere HTML o JSON, si osserva che in alcuni scenari come i flussi di autenticazione SAML, le favicon possono essere restituite come HTML, pertanto sono esplicitamente escluse dal conteggio. |
