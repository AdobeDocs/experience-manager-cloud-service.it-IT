---
title: Informazioni sulle richieste di contenuto di Cloud Service
description: Se hai acquistato licenze per richieste di contenuto da Adobe, scopri i tipi di richieste di contenuto che Adobe Experience Cloud as a Service misura e le varianze con gli strumenti di reporting di Analytics di un’organizzazione.
exl-id: 3666328a-79a7-4dd7-b952-38bb60f0967d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '2688'
ht-degree: 5%

---

# Richieste di contenuto Cloud Service

## Introduzione {#introduction}

Le richieste di contenuto di Cloud Service vengono misurate tramite la raccolta di dati lato server. La raccolta è abilitata tramite l’analisi del registro CDN.

>[!NOTE]
>Inoltre, per un numero limitato [Clienti early adopter](/help/release-notes/release-notes-cloud/release-notes-current.md#sites-early-adopter), la raccolta lato client verrà abilitata anche tramite la misurazione del servizio Real User Monitoring. Per ulteriori informazioni, consulta la documentazione in [questo articolo](#real-user-monitoring-for-aem-as-a-cloud-service).

## Informazioni sulle richieste di contenuto di Cloud Service {#understaing-cloud-service-content-requests}

Le richieste di contenuto vengono raccolte automaticamente lato server ai margini di Adobe Experience Manager as a Cloud Service, tramite l’analisi automatizzata dei file di registro provenienti dalla rete CDN as a Cloud Service dell’AEM. Questo viene fatto isolando le richieste che restituiscono HTML `(text/html)` o JSON `(application /Json)` contenuti della rete CDN e basati su diverse regole di inclusione ed esclusione descritte di seguito. Una richiesta di contenuto si verifica indipendentemente dal contenuto restituito distribuito dalle cache CDN o dal contenuto che ritorna all’origine della CDN (dispatcher AEM).

Il servizio Real User Monitoring, la raccolta lato client, offre un riflesso più preciso delle interazioni degli utenti, garantendo una misura affidabile del coinvolgimento del sito web. In questo modo i clienti possono ottenere informazioni avanzate sul traffico e sulle prestazioni delle loro pagine. Questo è utile per entrambi i clienti che utilizzano una rete CDN gestita da Adobe o una rete CDN gestita da un utente non Adobe. Inoltre, il reporting automatico del traffico può ora essere abilitato per i clienti che utilizzano una rete CDN gestita non basata su Adobi, eliminando in tal modo la necessità di condividere eventuali rapporti sul traffico con Adobe.

Per i clienti che utilizzano la propria rete CDN oltre a quella as a Cloud Service dall’AEM, la generazione rapporti lato server darà luogo a numeri che non possono essere utilizzati per confrontare con le richieste di contenuto concesse in licenza. Questi numeri dovranno essere misurati dal cliente al bordo della rete CDN esterna. Per questi clienti, la generazione di rapporti lato client e le prestazioni associate, il [Servizio dati RUM Adobe](#real-user-monitoring-for-aem-as-a-cloud-service) è l’opzione consigliata per gli Adobi. Consulta la [note sulla versione](/help/release-notes/release-notes-cloud/release-notes-current.md#sites-early-adopter) per informazioni su come effettuare il consenso.

## Raccolta lato server {#serverside-collection}

Esistono regole in vigore per escludere bot noti, tra cui servizi noti che visitano regolarmente il sito per aggiornare l’indice di ricerca o il servizio.

### Varianze delle richieste di contenuto del Cloud Service {#content-requests-variances}

Le richieste di contenuto possono presentare varianze con gli strumenti di reporting di Analytics di un’organizzazione, come riepilogato nella tabella seguente. In generale, *non* utilizza strumenti di analisi che raccolgono dati tramite strumenti lato client per creare rapporti sul numero di richieste di contenuto per un determinato sito, semplicemente perché spesso dipendono dal consenso dell’utente per essere attivati, perdendo quindi una frazione significativa del traffico. Gli strumenti di Analytics che raccolgono i dati lato server nei file di registro, o i rapporti CDN per i clienti che aggiungono la propria CDN oltre a AEM as a Cloud Service, forniranno conteggi migliori. Per la generazione di rapporti sulle visualizzazioni di pagina e sulle relative prestazioni, l’opzione consigliata è l’Adobe Adobe di RUM Data Service (Servizio dati RUM).

| Motivo della varianza | Spiegazione |
|---|---|
| Consenso utente finale | Gli strumenti di Analytics che si basano su strumenti lato client spesso dipendono dal consenso degli utenti all’attivazione. Questo potrebbe rappresentare la maggior parte del traffico che non viene tracciato. Per i clienti che desiderano misurare autonomamente le richieste di contenuto, si consiglia di utilizzare gli strumenti di analisi per raccogliere i dati lato server o i rapporti CDN. |
| Assegnazione dei tag | A tutte le pagine o chiamate API tracciate come richieste di contenuto di Adobe Experience Manager (AEM) potrebbero non essere assegnati tag di tracciamento Analytics. |
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

### Tipi di richieste di contenuto incluse {#included-content-requests}

| Tipo di richiesta | Richiesta contenuto | Descrizione |
| --- | --- | --- |
| Codice HTTP 100-299 | Inclusi | Si tratta di richieste regolari che forniscono contenuto completo o parziale. |
| Librerie HTTP per l&#39;automazione | Inclusi | Esempi:<br>· Amazon CloudFront<br>· Client Apache Http<br>· Client HTTP asincrono<br>· Assi<br>· Azureo<br>· Curl<br>· Recupero nodo GitHub<br>· Guscio<br>· Go-http-client<br>· Chrome headless<br>· Client Java™<br>· Jersey<br>· Node Oembed<br>· okhttp<br>· Richieste Python<br>· Reactor Netty<br>· Wget<br>· WinHTTP |
| Strumenti di monitoraggio e verifica stato | Inclusi | Questi vengono configurati dal cliente per monitorare un determinato aspetto del sito. Ad esempio, disponibilità o prestazioni reali degli utenti. Utilizzare `/system/probes/health` e non le pagine HTML effettive del sito.<br>Esempi:<br>· Amazon-Route53-Health-Check-Service<br>· EyeMonIT_bot_version_0.1_[(https://www.eyemon.it/)](https://www.eyemon.it/)<br>· Investis-Site24x7<br>· Mozilla/5.0+(compatibile; UptimeRobot/2.0; [https://uptimerobot.com/](https://uptimerobot.com/))<br>· ThousandEyes-Dragonfly-x1<br>· OmtrBot/1.0<br>· WebMon/2.0.0 |
| `<link rel="prefetch">` richieste | Inclusi | Per aumentare la velocità di caricamento della pagina successiva, i clienti possono fare in modo che il browser carichi un set di pagine prima che l’utente faccia clic sul collegamento, in modo che si trovino già nella cache. *Attenzione: questo sta aumentando notevolmente il traffico*- a seconda del numero di pagine preacquisite. |
| Traffico che blocca il reporting di Adobe Analytics o Google Analytics | Inclusi | È più comune che i visitatori dei siti abbiano installato software per la privacy (Ad-blocker e così via) che influiscono sulla precisione della Google Analytics o di Adobe Analytics. L’AEM as a Cloud Service conta le richieste sul primo punto di ingresso nell’infrastruttura gestita dall’Adobe e non sul lato client. |

Vedi anche [Dashboard delle licenze](/help/implementing/cloud-manager/license-dashboard.md).

### Tipi di richieste di contenuto escluse {#excluded-content-request}

| Tipo di richiesta | Richiesta contenuto | Descrizione |
| --- | --- | --- |
| Codice HTTP 500+ | Escluso | Sono stati restituiti errori al visitatore quando si verifica un errore in AEM as a Cloud Service o nel codice personalizzato del cliente. |
| Codice HTTP 400-499 | Escluso | Sono stati restituiti errori al visitatore se il contenuto non esiste (404) o si sono verificati altri problemi relativi al contenuto o alle richieste. |
| Codice HTTP 300-399 | Escluso | Si tratta di richieste valide che verificano se qualcosa è cambiato sul server o reindirizzano la richiesta a un’altra risorsa. Non contengono contenuto in sé, quindi non sono fatturabili. |
| Richieste indirizzate a /libs/* | Escluso | Richieste JSON interne dell’AEM, ad esempio il token CSRF non fatturabile. |
| Traffico da attacchi DDOS | Escluso | Protezione DDOS. L’AEM rileva automaticamente alcuni degli attacchi DDOS e li blocca. Gli attacchi DDOS rilevati non sono fatturabili. |
| Monitoraggio New Relic as a Cloud Service AEM | Escluso | Monitoraggio globale as a Cloud Service dell’AEM. |
| URL per i clienti per monitorare il programma di Cloud Service | Escluso | URL consigliato per monitorare esternamente la disponibilità.<br><br>`/system/probes/health` |
| Servizio di riscaldamento del pod as a Cloud Service dell&#39;AEM | Escluso | Agente utente: skyline-service-warm/1.* |
| Motori di ricerca noti, social network e librerie HTTP (contrassegnati da Fastly) | Escluso | Servizi noti visitano regolarmente il sito per aggiornare l’indice di ricerca o il servizio:<br><br>Esempi:<br>· AddSearchBot<br>· AhrefsBot<br>· Applebot<br>· Chiedi a Jeeves Corporate Spider<br>· Bingbot<br>· BingPreview<br>BLEXBot<br>· Incorporato<br>· Bytespider<br>· CrawlerKengo<br>· Facebookexternalhit<br>· Google AdsBot<br>· Google AdsBot Mobile<br>· Googlebot<br>· GoogleBot Mobile<br>· lmspider<br>· LucidWorks<br>MJ12bot<br>· Penna<br>· Pinterest<br>· SemrushBot<br>· Miglioramento del sito<br>· StashBot<br>· StatusCake<br>· YandexBot |
| Escludi chiamate Commerce integration framework | Escluso | Si tratta di richieste effettuate all’AEM che vengono inoltrate alla Commerce integration framework: l’URL inizia con `/api/graphql`- per evitare il doppio conteggio, non sono fatturabili per il Cloud Service. |
| Escludi `manifest.json` | Escluso | Manifest non è una chiamata API, è qui per fornire informazioni su come installare siti web sul desktop o sul telefono cellulare. L’Adobe non deve contare la richiesta JSON a `/etc.clientlibs/*/manifest.json` |
| Escludi `favicon.ico` | Escluso | Anche se il contenuto restituito non deve essere HTML o JSON, si osserva che in alcuni scenari come i flussi di autenticazione SAML, le favicon possono essere restituite come HTML, pertanto sono esplicitamente escluse dal conteggio. |

## Raccolta lato client {#cliendside-collection}

### Servizio Real User Monitoring per AEM as a Cloud Service {#real-user-monitoring-service-for-aem-as-a-cloud-service}

>[!INFO]
>
>Questa funzione è disponibile solo per il primo programma di adozione.
>Devi utilizzare la versione di AEM Cloud Service **2023.11.14227** e versioni successive per abilitare il servizio dati RUM.

### Panoramica {#overview}

Il servizio Real User Monitoring è un tipo di tecnologia di monitoraggio delle prestazioni che acquisisce e analizza in tempo reale le esperienze utente digitali di un sito web o di un’applicazione. Fornisce visibilità sulle prestazioni in tempo reale di un’applicazione web e informazioni accurate sull’esperienza dell’utente finale.

Il servizio Real User Monitoring fornisce informazioni approfondite sulle metriche delle prestazioni chiave, dall’avvio dell’URL fino al ritorno della richiesta al browser, il che aiuta gli sviluppatori a migliorare l’applicazione per facilitarne l’utilizzo per gli utenti finali.

### Chi può trarre vantaggio dal servizio Real User Monitoring? {#who-can-benefit-from-rum-service}

Il servizio dati RUM è utile per tutti i clienti che utilizzano Adobe o la propria rete CDN. Offre un riflesso più preciso delle interazioni degli utenti, garantendo una misura affidabile del coinvolgimento del sito web che riflette il numero di visualizzazioni di pagina sul lato client.

In particolare, per Adobe gli utenti CDN, tiene traccia con precisione delle interazioni degli utenti per un confronto diretto tra le visualizzazioni di pagina lato client e i registri CDN lato server.

I clienti che utilizzano la propria rete CDN possono beneficiare di rapporti sul traffico semplificati, in quanto Adobe ora integra direttamente queste Visualizzazioni pagina, eliminando la necessità di creare rapporti separati.

Inoltre, tutti i clienti possono ottenere informazioni approfondite sulle prestazioni delle pagine, per ottimizzare in modo efficace le loro esperienze digitali.

### Funzionamento del servizio Real User Monitoring {#understand-how-the-rum-service-works}

Adobe Experience Manager utilizza Real User Monitoring (RUM) per aiutare i clienti e gli Adobi a comprendere come i visitatori interagiscono con i siti basati su Adobe Experience Manager, diagnosticare i problemi di prestazioni e misurare l’efficacia degli esperimenti. RUM preserva la privacy dei visitatori attraverso il campionamento - solo una piccola parte di tutte le visualizzazioni di pagina sarà monitorata - e l&#39;esclusione giudiziosa di tutte le informazioni personali identificabili (PII).

### Servizio Real User Monitoring e privacy {#rum-service-and-privacy}

Il servizio Real User Monitoring di Adobe Experience Manager è progettato per preservare la privacy dei visitatori e ridurre al minimo la raccolta dei dati. In qualità di visitatore, ciò significa che nessuna informazione personale verrà raccolta dal sito che stai visitando o resa disponibile agli Adobi.

In qualità di operatore del sito, ciò significa che non è richiesto alcun consenso aggiuntivo per abilitare il monitoraggio tramite questa funzione.Pertanto, non ci sarà alcun pop-up aggiuntivo che gli utenti finali dovranno accettare per abilitare il monitoraggio RUM.

### Campionamento dei dati del servizio Real User Monitoring {#rum-service-data-sampling}

Le soluzioni di analisi web tradizionali tentano di raccogliere dati su ogni singolo visitatore. Il servizio Real User Monitoring di Adobe Experience Manager acquisisce informazioni solo da una piccola frazione di visualizzazioni di pagina. I dati del servizio Real User Monitoring devono essere campionati e resi anonimi, anziché essere sostituiti per le attività di analisi. Per impostazione predefinita, le pagine hanno una proporzione di campionamento di 1:100. Gli operatori del sito non possono configurare questo numero per aumentare o diminuire la frequenza di campionamento a partire da oggi. Per stimare con precisione il traffico totale, per ogni 100 visualizzazioni di pagina, raccogliamo dati dettagliati da una, fornendo un’approssimazione affidabile del traffico complessivo.&quot;

Poiché la decisione se raccogliere o meno i dati viene presa in base alla visualizzazione pagina per pagina, diventa praticamente impossibile tenere traccia delle interazioni tra più pagine. RUM non ha alcun concetto di visite, visitatori o sessioni, ma solo di visualizzazioni di pagina. Questo è progettato.

### Quali dati vengono raccolti {#what-data-is-being-collected}

Il servizio Real User Monitoring è progettato per impedire la raccolta di informazioni personali. Di seguito sono elencate tutte le informazioni che possono essere raccolte dal servizio Real User Monitoring di Adobe Experience Manager:

* Il nome host del sito visitato, ad esempio: `experienceleague.adobe.com`
* Tipo di agente utente generico utilizzato per visualizzare la pagina, ad esempio: desktop o dispositivo mobile
* L’ora della raccolta dei dati, ad esempio: `2021-06-26 06:00:02.596000 UTC (in order to preserve privacy, we round all minutes to the previous hour, so that only seconds and milliseconds are tracked)`
* L’URL della pagina visitata, ad esempio: `https://experienceleague.adobe.com/docs`
* URL referente (URL della pagina collegata alla pagina corrente, se l’utente ha seguito un collegamento)
* Un ID della visualizzazione pagina generato in modo casuale, in un formato simile a: `2Ac6`
* Peso o inverso della frequenza di campionamento, ad esempio: `100`. Ciò significa che verrà registrata solo una visualizzazione su cento
* Il punto di controllo, o il nome di un particolare evento nella sequenza di caricamento della pagina o di interazione con essa come visitatore
* L’origine o l’identificatore dell’elemento DOM con cui l’utente interagisce per il punto di controllo menzionato sopra. Ad esempio, potrebbe trattarsi di un’immagine
* La destinazione o il collegamento a una pagina o risorsa esterna con cui l’utente interagisce per il punto di controllo menzionato in precedenza. Esempio: `https://blog.adobe.com/jp/publish/2022/06/29/media_162fb947c7219d0537cce36adf22315d64fb86e94.png`
* Le metriche delle prestazioni Core Web Vitals (CWV), LCP (Largest Contentful Paint), FID (First Input Delay) e CLS (Cumulative Layout Shift) descrivono la qualità dell’esperienza del visitatore.

### Come impostare il servizio Real User Monitoring {#how-to-set-up-the-rum-service}

* Se desideri partecipare al nostro programma Early Adopter, invia un’e-mail a `aemcs-rum-adopter@adobe.com`, insieme al nome di dominio per l’ambiente di produzione, stage e sviluppo, dall’indirizzo e-mail associato al tuo Adobe ID. Il team di prodotto di Adobe abiliterà quindi il servizio dati del Monitoraggio degli utenti reali (RUM).
* Una volta completato, il team di prodotto di Adobe creerà un canale di collaborazione con il cliente.
* Il team di prodotto di Adobe ti contatterà per fornirti la chiave di dominio e l’URL del dashboard dati in cui puoi visualizzare le Visualizzazioni pagina e [Core Web Vitals (CWV)](https://web.dev/vitals/) metriche raccolte dalla raccolta del servizio Real User Monitoring lato client.
* Verrai quindi guidato su come utilizzare la chiave di dominio per accedere all’URL del dashboard dei dati e visualizzare le metriche.

### Utilizzo dei dati del Real User Monitoring Service {#how-rum-service-data-is-being-used}

I dati RUM sono utili per i seguenti scopi:

* Identificare e correggere i colli di bottiglia delle prestazioni per le sedi dei clienti
* Rapporti sul traffico automatici e semplificati che includono le visualizzazioni di pagina per i clienti che utilizzano la propria rete CDN, il che significa che non devono condividere alcun rapporto sul traffico con Adobe.
* Comprendere il modo in cui Adobe Experience Manager interagisce con altri script (ad esempio analisi, targeting o librerie esterne) sulla stessa pagina, per aumentare la compatibilità.

### Limitazioni e nozioni di base sulla varianza nelle visualizzazioni di pagina e nelle metriche delle prestazioni {#limitations-and-understanding-variance-in-page-views-and-performance-metrics}

Man mano che analizzerai questi dati, potrebbero esserci o meno discrepanze nelle visualizzazioni di pagina e in altre metriche delle prestazioni segnalate da Real User Monitoring (RUM). Queste varianze possono essere attribuite a diversi fattori inerenti al monitoraggio in tempo reale lato client. Di seguito sono riportate alcune considerazioni chiave che i clienti devono tenere presenti quando interpretano i dati RUM:

1. **Blocchi del tracciamento**

   * Gli utenti finali che utilizzano bloccanti del tracciamento o estensioni della privacy possono impedire la raccolta dei dati del servizio Real User Monitoring, in quanto questi strumenti limitano l’esecuzione degli script di tracciamento. Questa restrizione può portare a visualizzazioni di pagina e interazioni utente non riportate correttamente, creando una discrepanza tra l’attività effettiva del sito e i dati acquisiti da RUM.

1. **Limitazioni nell’acquisizione di chiamate API/JSON**

   * Il servizio dati RUM si concentra sull’esperienza lato client e al momento non acquisisce le chiamate API o JSON back-end. L’esclusione di queste chiamate dai dati del servizio di monitoraggio utente reale creerà varianze rispetto alle richieste di contenuto misurate da CDN Analytics.

### Domande frequenti {#faq}

1. **Come posso configurare i percorsi da includere o escludere nel monitoraggio?**

   I clienti potranno configurare i percorsi in modo da includere o escludere gli URL da monitorare impostando le variabili di ambiente nella configurazione in Cloud Manager utilizzando le seguenti variabili: `AEM_WEBVITALS_EXCLUDE` e `AEM_WEBVITALS_INCLUDE_PATHS`

   Per impostazione predefinita, l’impostazione &quot;include&quot; è configurata per la destinazione &quot;/content&quot;. È importante ricordare che i percorsi da configurare qui sono percorsi di contenuto all’interno del sistema, non i percorsi URL visualizzati nel browser. Questa distinzione è fondamentale per impostare e personalizzare con precisione la configurazione in base alle esigenze specifiche.

1. **Adobe sarebbe in grado di tenere traccia di tutte le visualizzazioni di pagina prima che l’interazione raggiunga la rete CDN gestita dal cliente o nel momento in cui l’interazione raggiunge la rete CDN gestita dal cliente?**

   Sì.

1. **I clienti saranno in grado di integrare gli script del servizio dati RUM con sistemi di terze parti come Dynatrace?**

   Sì.

1. **Vengono raccolte metriche di tipo &quot;Interaction to next paint&quot; (Interazione con la pittura successiva), &quot;Time to first byte&quot; (Tempo al primo byte) e &quot;First contentful paint&quot; (Prima pittura di contenuto)?**

   Vengono raccolte le interazioni con la vernice successiva (INP) e il tempo al primo byte (TTFB).  Al momento non viene raccolta la prima pittura di contenuto.
