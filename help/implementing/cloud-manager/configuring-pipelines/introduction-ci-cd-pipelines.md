---
title: Pipeline CI/CD
description: Scopri le pipeline CI/CD di Cloud Manager e come utilizzarle per distribuire il codice in modo efficiente.
index: true
exl-id: 40d6778f-65e0-4612-bbe3-ece02905709b
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 89%

---


# Pipeline CI/CD di Cloud Manager {#intro-cicd}

Scopri le pipeline CI/CD di Cloud Manager e come utilizzarle per distribuire il codice in modo efficiente.

## Introduzione {#introduction}

Una pipeline CI/CD in Cloud Manager è un meccanismo che consente di generare il codice da un archivio sorgente e distribuirlo in un ambiente. È possibile attivare le pipeline da un evento, ad esempio una richiesta pull da un archivio del codice sorgente (ovvero una modifica del codice) o da una pianificazione regolare, in modo che corrisponda a una cadenza di pubblicazione.

Per configurare una pipeline è necessario:

* Definire il trigger per l’avvio della pipeline.
* Definire i parametri che controllano la distribuzione nell’ambiente di produzione.
* Configurare i parametri di test delle prestazioni.

Cloud Manager offre due tipi di pipeline:

* [Pipeline di produzione](#prod-pipeline)
* [Pipeline non di produzione](#non-prod-pipeline)

![Tipi di pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cd-config1.png)

## Pipeline di produzione {#prod-pipeline}

Una pipeline di produzione è una pipeline dedicata che include una serie di passaggi orchestrati per distribuire il codice sorgente per l’utilizzo in produzione. Tra i passaggi sono previsti la prima generazione, la creazione di pacchetti, i test, la convalida e la distribuzione in tutti gli ambienti di staging. Pertanto, una pipeline di produzione può essere aggiunta solo dopo aver creato un set di ambienti di produzione e di staging.

>[!TIP]
>
>Consulta [Configurazione di una pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) per ulteriori dettagli.

## Pipeline non di produzione {#non-prod-pipeline}

Una pipeline non di produzione serve principalmente per eseguire controlli di qualità del codice o per distribuire il codice sorgente in un ambiente di sviluppo.

>[!TIP]
>
>Consulta [Configurazione di una pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) per ulteriori dettagli.

## Origini del codice {#code-sources}

Oltre ai tipi di produzione e non di produzione, le pipeline possono essere differenziate in base al tipo di codice che distribuiscono.

* **[Pipeline full stack](#full-stack-pipeline)**: distribuiscono simultaneamente le build del codice back-end e front-end contenenti una o più applicazioni server di AEM con configurazioni HTTPD/Dispatcher
* **[Configurare le pipeline](#config-deployment-pipeline)** : in pochi minuti puoi configurare e distribuire le regole del filtro del traffico, incluse le regole WAF
* **[Pipeline front-end](#front-end)**: distribuiscono le build del codice front-end contenenti una o più applicazioni dell’interfaccia utente lato client
* **[Pipeline di configurazione a livello web](#web-tier-config-pipelines)**: distribuiscono le configurazioni HTTPD/Dispatcher

Ulteriori informazioni su queste pipeline sono riportate più avanti in questo documento.

### Informazioni sulle pipeline CI/CD in Cloud Manager {#understand-pipelines}

La tabella seguente riepiloga le pipeline disponibili in Cloud Manager e i relativi utilizzi.

| Tipo di pipeline | Distribuzione o qualità del codice | Codice sorgente | Scopo | Note |
|--- |--- |--- |---|---|
| Di produzione o non di produzione | Distribuzione | Full stack | Distribuisce simultaneamente le build del codice back-end e front-end con le configurazioni HTTPD/Dispatcher | Quando è necessario distribuire il codice front-end in contemporanea al codice del server AEM.<br>Quando non sono ancora state implementate le pipeline front-end o di configurazione a livello web. |
| Di produzione o non di produzione | Distribuzione | Front-end | Distribuisce la build del codice front-end contenente una o più applicazioni dell’interfaccia utente lato client | Supporta più pipeline front-end simultanee<br>Distribuzioni molto più rapide rispetto al tipo full stack |
| Di produzione o non di produzione | Distribuzione | Configurazione a livello web | Distribuisce le configurazioni HTTPD/Dispatcher | Distribuzione in pochi minuti |
| Di produzione o non di produzione | Distribuzione | Configurazione | Distribuisce le regole di filtro del traffico | Distribuzione in pochi minuti |
| Non di produzione | Qualità del codice | Full stack | Esegue controlli di qualità del codice full stack senza una distribuzione | Supporta più pipeline |
| Non di produzione | Qualità del codice | Front-end | Esegue controlli di qualità del codice front-end senza una distribuzione | Supporta più pipeline |
| Non di produzione | Qualità del codice | Configurazione a livello web | Esegue controlli di qualità del codice su configurazioni dispatcher senza una distribuzione | Supporta più pipeline |
| Non di produzione | Qualità del codice | Configurazione | Distribuisce le regole di filtro del traffico |  |

Il diagramma seguente illustra le configurazioni delle pipeline di Cloud Manager con archivio tradizionale front-end singolo o indipendente.

![Configurazioni delle pipeline di Cloud Manager](/help/implementing/cloud-manager/assets/configure-pipeline/cm-setup.png)

## Pipeline full stack {#full-stack-pipeline}

Le pipeline full stack distribuiscono contemporaneamente il codice back-end, il codice front-end e le configurazioni a livello web per il runtime di AEM.

* Codice back-end: contenuti non modificabili come codice Java, configurazioni OSGi, repoinit e contenuti modificabili
* Codice front-end: risorse dell’interfaccia utente dell’applicazione come JavaScript, CSS e font
* Configurazione a livello web: configurazioni HTTPD/Dispatcher

La pipeline full stack rappresenta una pipeline “completa” che esegue tutte le operazioni in un’unica soluzione, offrendo al contempo agli utenti la possibilità di distribuire esclusivamente le configurazioni del codice front-end o Dispatcher rispettivamente tramite la pipeline front-end e le pipeline di configurazione a livello web.

Le pipeline full stack creano pacchetti del codice front-end (JavaScript/CSS) come [librerie client di AEM](/help/implementing/developing/introduction/clientlibs.md).

Le pipeline full stack possono distribuire configurazioni a livello web se non è stata configurata una [pipeline di configurazione a livello web](#web-tier-config-pipelines).

Si applicano le seguenti restrizioni.

* Per configurare o eseguire le pipeline è necessario che l’utente con il ruolo **Responsabile dell’implementazione** abbia eseguito l’accesso.
* In qualsiasi momento può essere presente una sola pipeline full stack per ogni ambiente.

Inoltre, se scegli di introdurre una [pipeline di configurazione a livello web](#web-tier-config-pipelines), è bene tenere presente il comportamento della pipeline full stack.

* In presenza di una pipeline a livello web corrispondente, la pipeline full stack di un ambiente ignora la configurazione Dispatcher.
* Se la pipeline di configurazione a livello web corrispondente per l’ambiente non esiste, l’utente può configurare la pipeline full stack per includere o ignorare la configurazione Dispatcher.

Le pipeline full stack possono essere di qualità del codice o di distribuzione.

### Configurazione delle pipeline full stack {#configure-full-stack}

Per informazioni su come configurare le pipeline full stack, consulta i seguenti documenti:

* [Aggiunta di una pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#full-stack-code)
* [Aggiunta di una pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code)

## Configurare le pipeline {#config-deployment-pipeline}

Con una pipeline di configurazione è possibile configurare e distribuire in pochi minuti le regole del filtro del traffico, incluse le regole WAF.

Consulta [Regole del filtro del traffico, incluse le regole WAF](/help/security/traffic-filter-rules-including-waf.md) per scoprire come gestire le configurazioni nell’archivio in modo che vengano distribuite correttamente.

### Configurazione delle pipeline di configurazione {#configure-config-deployment}

Per informazioni su come configurare le pipeline di configurazione, consulta i seguenti documenti:

* [Aggiunta di una pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#targeted-deployment)
* [Aggiunta di una pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#targeted-deployment)

## Pipeline front-end {#front-end}

Per codice front-end si intende qualsiasi codice utilizzato come file statico. È separato dal codice dell’interfaccia utente fornito da AEM e può includere temi del sito, applicazioni SPA definite dal cliente, SPA e altre soluzioni.

Grazie alle pipeline front-end i team possono semplificare il processo di progettazione e sviluppo con una distribuzione più rapida del codice front-end in modo asincrono rispetto allo sviluppo back-end. Questa pipeline dedicata distribuisce JavaScript e CSS al livello di distribuzione AEM come tema, dando luogo a una nuova versione del tema a cui è possibile fare riferimento dalle pagine di AEM.

>[!NOTE]
>
>Gli utenti con ruolo **Responsabile dell’implementazione** possono creare ed eseguire più pipeline front-end contemporaneamente.
>
>Tuttavia, il limite massimo è di 300 pipeline per programma (per tutti i tipi).

Le pipeline front-end possono essere pipeline per qualità del codice o per distribuzione.

### Prima di configurare le pipeline front-end {#before-start}

Prima di configurare le pipeline front-end, consulta la sezione [Percorso Creazione rapida sito di AEM](/help/journey-sites/quick-site/overview.md) per una guida end-to-end all’intuitivo strumento di AEM per la creazione rapida dei siti. Questo percorso aiuta a semplificare lo sviluppo front-end e consente di personalizzare rapidamente il sito senza alcuna conoscenza del back-end di AEM.

### Configurazione di una pipeline front-end {#configure-front-end}

Per informazioni su come configurare le pipeline front-end, consulta:

* [Aggiunta di una pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [Aggiunta di una pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)

### Sviluppo di Sites con la pipeline front-end {#developing-with-front-end-pipeline}

Con le pipeline front-end, i team di sviluppo front-end acquisiscono maggiore indipendenza e il processo di sviluppo può essere accelerato.

Per informazioni sul funzionamento di questo processo e alcune considerazioni per sfruttare al massimo il suo potenziale, consulta [Sviluppo di Sites con la pipeline front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md).

## Pipeline di configurazione a livello web {#web-tier-config-pipelines}

Le pipeline di configurazione a livello web consentono di distribuire la configurazione HTTPD/Dispatcher esclusivamente nel runtime di AEM, separandola dalle altre modifiche al codice. Si tratta di una pipeline semplificata che offre agli utenti che desiderano distribuire solo le modifiche alla configurazione del dispatcher un metodo accelerato per farlo in pochi minuti.

>[!TIP]
>
>Con le pipeline di configurazione a livello web puoi scegliere se archiviare la configurazione web nella stessa posizione di origine della pipeline full stack o in una posizione diversa, a seconda della struttura più adatta al tuo progetto.

Si applicano le seguenti restrizioni.

* Per utilizzare le pipeline di configurazione a livello web è necessario aver installato AEM versione `2021.12.6151.20211217T120950Z` o successiva.
* Per utilizzare le pipeline di configurazione a livello web è necessario fornire il [consenso alla modalità flessibile degli strumenti Dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug).
* Per configurare o eseguire le pipeline è necessario che l’utente con il ruolo **Responsabile dell’implementazione** abbia eseguito l’accesso.
* In qualsiasi momento può essere presente una sola pipeline di configurazione a livello web per ogni ambiente.
* L’utente non può configurare una pipeline di configurazione a livello web quando è in esecuzione la pipeline full stack corrispondente.
* La struttura a livello web deve rispettare la struttura della modalità flessibile, come definito nel documento [Dispatcher nel cloud](/help/implementing/dispatcher/disp-overview.md#validation-debug).

Inoltre, è bene tenere presente il comportamento della [pipeline full stack](#full-stack-pipeline) quando si introduce una pipeline a livello web.

* Se per un ambiente non è stata configurata una pipeline di configurazione a livello web, l’utente può effettuare una selezione durante la configurazione della pipeline full stack corrispondente per includere o ignorare la configurazione Dispatcher durante l’esecuzione e la distribuzione.
* Dopo aver configurato una pipeline di configurazione a livello web per un ambiente, la corrispondente pipeline full stack (se presente) ignora la configurazione dispatcher durante l’esecuzione e la distribuzione.
* Dopo aver eliminato la pipeline di configurazione a livello web, la pipeline full stack corrispondente viene reimpostata per distribuire le configurazioni Dispatcher durante l’esecuzione.

Le pipeline di configurazione a livello web possono essere di tipo qualità del codice o distribuzione del codice.

### Configurazione delle pipeline a livello web {#configure-web-tier}

Per informazioni su come configurare le pipeline a livello web, consulta i seguenti documenti:

* [Aggiunta di una pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#targeted-deployment)
* [Aggiunta di una pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#targeted-deployment)

## Panoramica video dei tipi di pipeline {#video}

Guarda questo breve video per una breve panoramica sui tipi di pipeline.

>[!VIDEO](https://video.tv.adobe.com/v/342363)
