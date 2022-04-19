---
title: Pipeline CI/CD
description: Scopri le pipeline CI/CD di Cloud Manager e come possono essere utilizzate per distribuire il codice in modo efficiente.
index: true
exl-id: 40d6778f-65e0-4612-bbe3-ece02905709b
source-git-commit: 6c246444f48440c64af0951e75f2071c00e477fa
workflow-type: tm+mt
source-wordcount: '1377'
ht-degree: 1%

---

# Pipeline CI/CD di Cloud Manager {#intro-cicd}

Scopri le pipeline CI/CD di Cloud Manager e come possono essere utilizzate per distribuire il codice in modo efficiente.

## Introduzione {#introduction}

Una pipeline CI/CD in Cloud Manager è un meccanismo per creare il codice da un archivio sorgente e distribuirlo in un ambiente. Una pipeline può essere attivata da un evento, ad esempio una richiesta di pull da un archivio del codice sorgente (cioè una modifica del codice), o da una pianificazione regolare, in modo che corrisponda a una frequenza di rilascio.

Per configurare una pipeline, devi:

* Definisci il trigger che avvierà la pipeline.
* Definisci i parametri che controllano la distribuzione di produzione.
* Configura i parametri del test delle prestazioni.

Cloud Manager offre due tipi di pipeline:

* [Pipe di produzione](#prod-pipeline)
* [Pipeline non di produzione](#non-prod-pipeline)

![Tipi di gasdotti](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cd-config1.png)

## Panoramica video {#video}

Per una rapida panoramica dei tipi di pipeline, guarda questo breve video.

>[!VIDEO](https://video.tv.adobe.com/v/342363)

## Pipe di produzione {#prod-pipeline}

Una pipeline di produzione è una pipeline appositamente creata che include una serie di passaggi orchestrati per distribuire il codice sorgente per l’utilizzo di produzione. I passaggi includono la prima creazione, la creazione di pacchetti, il test, la convalida e la distribuzione in tutti gli ambienti di staging. Pertanto, una pipeline di produzione può essere aggiunta solo una volta creato un set di ambienti di produzione e di staging.

>[!TIP]
>
>Consulta il documento [Configurazione di una pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) per ulteriori dettagli.

## Pipeline non di produzione {#non-prod-pipeline}

Una pipeline non di produzione serve principalmente per eseguire scansioni di qualità del codice o per distribuire il codice sorgente in un ambiente di sviluppo.

>[!TIP]
>
>Consulta il documento [Configurazione di una pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) per ulteriori dettagli.

## Origini del codice {#code-sources}

Oltre alla produzione e alla non produzione, le pipeline possono essere differenziate in base al tipo di codice che distribuiscono.

* **[Pipellini full-stack](#full-stack-pipeline)** - Distribuzione simultanea di build di codice back-end e front-end contenenti una o più applicazioni server AEM insieme alle configurazioni di HTTPD/Dispatcher
* **[Pipeline front-end](#front-end)** - Distribuzione di build di codice front-end contenenti una o più applicazioni dell’interfaccia utente lato client
* **[Pipe di configurazione a livello web](#web-tier-config-pipelines)** - Implementazione delle configurazioni di HTTPD/Dispatcher

Questi sono descritti in dettaglio più avanti in questo documento.

### Informazioni sulle pipeline CI-CD in Cloud Manager {#understand-pipelines}

La tabella seguente riepiloga tutte le pipeline disponibili in Cloud Manager e i relativi utilizzi.

| Tipo di pipeline | Implementazione o qualità del codice | Codice sorgente | Scopo | Note |
|--- |--- |--- |---|---|
| Produzione o non produzione | Implementazione | Pieno stack | Distribuisce simultaneamente build di codice back-end e front-end insieme alle configurazioni di HTTPD/Dispatcher | Quando il codice front-end deve essere distribuito simultaneamente con AEM codice server.<br>Quando le pipeline front-end o le pipeline di configurazione del livello web non sono ancora state adottate. |
| Produzione o non produzione | Implementazione | Front-end | Implementa la build del codice front-end contenente una o più applicazioni dell’interfaccia utente lato client | Supporta più pipeline front-end simultanee<br>Implementazioni molto più veloci di quelle a stack completo |
| Produzione o non produzione | Implementazione | Configurazione a livello web | Implementa le configurazioni di HTTPD/Dispatcher | Implementazioni in minuti |
| Non produzione | Qualità del codice | Pieno stack | Esegue la scansione della qualità del codice su codice full-stack senza una distribuzione | Supporta più pipeline |
| Non produzione | Qualità del codice | Front-end | Esegue la scansione della qualità del codice sul codice front-end senza una distribuzione | Supporta più pipeline |
| Non produzione | Qualità del codice | Configurazione a livello web | Esegue la scansione della qualità del codice sulle configurazioni del dispatcher senza una distribuzione | Supporta più pipeline |

Il diagramma seguente illustra le configurazioni della pipeline di Cloud Manager con repository front-end tradizionale singolo o indipendente.

![Configurazioni della pipeline di Cloud Manager](/help/implementing/cloud-manager/assets/configure-pipeline/cm-setup.png)

## Pipeline full-stack {#full-stack-pipeline}

Le pipeline full-stack distribuiscono il codice back-end, il codice front-end e le configurazioni del livello web per AEM runtime contemporaneamente.

* Codice back-end: contenuto immutabile come codice Java, configurazioni OSGi, reindirizzamento e contenuto modificabile
* Codice front-end: risorse dell’interfaccia utente dell’applicazione come JavaScript, CSS, font
* Configurazione a livello web - Configurazioni HTTPD/Dispatcher

La pipeline full-stack rappresenta una pipeline &quot;uber&quot; che esegue tutte le operazioni in una sola volta, mentre offre agli utenti le opzioni per distribuire esclusivamente le configurazioni del codice front-end o del Dispatcher tramite rispettivamente la pipeline front-end e le pipeline di configurazione del livello web.

Codice front-end del pacchetto pipeline full-stack (JavaScript/CSS) come [AEM librerie client.](/help/implementing/developing/introduction/clientlibs.md)

Le pipeline full-stack possono distribuire configurazioni di livello web se un [pipeline di configurazione livello web](#web-tier-config-pipelines) non è configurato.

Si applicano le seguenti restrizioni.

* Un utente deve essere registrato con il **Gestione distribuzione** per configurare o eseguire le pipeline.
* In qualsiasi momento, può essere disponibile una sola pipeline full-stack per ogni ambiente.

Inoltre, tieni presente il comportamento della pipeline a stack intero se scegli di introdurre una [pipeline di configurazione del livello web.](#web-tier-config-pipelines)

* La pipeline con stack completo per un ambiente ignorerà la configurazione di Dispatcher se esiste la pipeline di configurazione del livello web corrispondente.
* Se la pipeline di configurazione del livello web corrispondente per l’ambiente non esiste, l’utente può configurare la pipeline a stack intero includendo o ignorando la configurazione di Dispatcher.

Le pipeline full-stack possono essere pipeline di qualità del codice o distribuzione.

## Pipeline front-end {#front-end}

Per codice front-end si intende qualsiasi codice utilizzato come file statico. È separato dal codice dell’interfaccia utente gestito da AEM e può includere temi del sito, SPA definiti dal cliente, SPA Firefly e altre soluzioni.

Le pipeline front-end consentono ai team di semplificare il processo di progettazione e sviluppo consentendo una distribuzione più rapida del codice front-end in modo asincrono rispetto allo sviluppo back-end. Questa pipeline dedicata distribuisce JavaScript e CSS al livello di distribuzione AEM come tema, dando luogo a una nuova versione del tema a cui è possibile fare riferimento dalle pagine consegnate da AEM.

>[!IMPORTANT]
>
>È necessario utilizzare AEM versione `2021.10.5933.20211012T154732Z ` o versioni successive con AEM Sites abilitato per l’utilizzo di pipeline front-end.

>[!NOTE]
>
>Un utente con **Gestione distribuzione** Il ruolo può creare ed eseguire più pipeline front-end contemporaneamente.
>
>Esiste tuttavia un limite massimo di 300 gasdotti per programma (per tutti i tipi). che possono essere di qualità del codice front-end o pipeline di distribuzione front-end.

Le pipeline front-end possono essere pipeline di qualità del codice o implementazioni.

### Prima di configurare le pipeline front-end {#before-start}

Prima di configurare le pipeline front-end, controlla la [AEM Percorso di creazione di siti rapidi](/help/journey-sites/quick-site/overview.md) per una guida end-to-end attraverso lo strumento di facile utilizzo AEM creazione rapida di siti. Questo percorso ti aiuterà a semplificare lo sviluppo front-end e ti permetterà di personalizzare rapidamente il tuo sito senza alcuna conoscenza AEM back-end.

### Configurare una pipeline front-end {#configure-front-end}

Per informazioni su come configurare le pipeline front-end, consulta i seguenti documenti.

* [Aggiunta di una pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [Aggiunta di una pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)

### Sviluppo di siti con la pipeline front-end {#developing-with-front-end-pipeline}

Con le condutture front-end, viene data maggiore indipendenza agli sviluppatori front-end e il processo di sviluppo può essere accelerato.

Fare riferimento al documento [Sviluppo di siti con la pipeline front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) per come questo processo funziona insieme ad alcune considerazioni di cui tenere conto al fine di sfruttare appieno il potenziale di questo processo.

### Configurazione di pipeline a stack completo {#configure-full-stack}

Per informazioni su come configurare le pipeline full-stack, consulta i seguenti documenti.

* [Aggiunta di una pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [Aggiunta di una pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)


## Pipe di configurazione a livello web {#web-tier-config-pipelines}

Le pipeline di configurazione a livello web consentono la distribuzione esclusiva della configurazione HTTPD/Dispatcher al runtime AEM disaccoppiandola da altre modifiche del codice. Si tratta di una pipeline semplificata che fornisce agli utenti che desiderano distribuire solo le modifiche alla configurazione del dispatcher, un metodo accelerato per farlo in pochi minuti.

>[!TIP]
>
>Con le pipeline di configurazione a livello web, puoi scegliere se memorizzare la configurazione web nella stessa posizione di origine della pipeline di stack completa o in una posizione diversa, a seconda della struttura più adatta al tuo progetto.

Si applicano le seguenti restrizioni.

* È necessario utilizzare AEM versione `2021.12.6151.20211217T120950Z` o più recente per sfruttare le pipeline di configurazione a livello web.
* Devi [consenso alla modalità flessibile degli strumenti del dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug) per sfruttare le pipeline di configurazione a livello web.
* Un utente deve essere registrato con il **Gestione distribuzione** per configurare o eseguire le pipeline.
* In qualsiasi momento, può essere presente una sola pipeline di configurazione del livello web per ogni ambiente.
* L’utente non può configurare una pipeline di configurazione del livello web quando è in esecuzione la pipeline a stack intero corrispondente.
* La struttura del livello web deve rispettare la struttura della modalità flessibile, come definita nel documento [Dispatcher nel cloud.](/help/implementing/dispatcher/disp-overview.md#validation-debug)

Inoltre, tieni presente quanto segue [tubazione piena](#full-stack-pipeline) si comporta quando viene introdotta una pipeline di livello web.

* Se una pipeline di configurazione del livello web non è stata configurata per un ambiente, l’utente può effettuare una selezione durante la configurazione della pipeline completa dello stack corrispondente per includere o ignorare la configurazione del Dispatcher durante l’esecuzione e la distribuzione.
* Una volta configurata una pipeline di configurazione del livello web per un ambiente, la relativa pipeline a stack intero (se presente) corrispondente ignorerà la configurazione del dispatcher durante l’esecuzione e la distribuzione.
* Una volta eliminata la pipeline di configurazione del livello web, la relativa pipeline a stack intero verrà reimpostata per distribuire le configurazioni di Dispatcher durante la relativa esecuzione.

Le pipeline di configurazione a livello Web possono essere di tipo qualità o distribuzione del codice.

### Configurazione delle pipeline di configurazione a livello web {#configure-web-tier-config-pipelines}

Per informazioni su come configurare le pipeline di configurazione del livello web, consulta i seguenti documenti.

* [Aggiunta di una pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [Aggiunta di una pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)
