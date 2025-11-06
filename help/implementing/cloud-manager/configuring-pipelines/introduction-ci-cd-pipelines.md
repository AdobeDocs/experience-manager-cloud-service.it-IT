---
title: Introduzione alle pipeline CI/CD
description: Scopri le pipeline CI/CD di Cloud Manager e come utilizzarle per distribuire il codice in modo efficiente.
index: true
exl-id: 40d6778f-65e0-4612-bbe3-ece02905709b
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1546'
ht-degree: 32%

---


# Pipeline CI/CD di Cloud Manager {#intro-cicd}

Scopri le pipeline CI/CD (Continuous Integration/Continuous Delivery) di Cloud Manager e come utilizzarle per distribuire il codice in modo efficiente.

## Introduzione alle pipeline CI/CD {#introduction}

Una pipeline CI/CD in Cloud Manager è un meccanismo che consente di generare il codice da un archivio sorgente e distribuirlo in un ambiente. Un evento attiva una pipeline, ad esempio una richiesta pull da un archivio del codice sorgente come Git (ovvero una modifica del codice). Oppure può essere attivata su una pianificazione regolare per corrispondere a una cadenza di rilascio.

Per configurare una pipeline, è necessario effettuare le seguenti operazioni:

* Definisci il trigger che avvia la pipeline.
* Definisci i parametri che controllano la distribuzione di produzione.
* Configurare i parametri di test delle prestazioni.

Cloud Manager offre due tipi di pipeline:

* [Pipeline di produzione](#prod-pipeline)
* [Pipeline non di produzione](#non-prod-pipeline)

![Tipi di pipeline](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cd-config1.png)

## Pipeline di produzione {#prod-pipeline}

Una pipeline di produzione è una pipeline dedicata che include una serie di passaggi orchestrati per distribuire il codice sorgente per l’utilizzo in produzione. Tra i passaggi sono previsti la prima generazione, la creazione di pacchetti, i test, la convalida e la distribuzione in tutti gli ambienti di staging. Pertanto, una pipeline di produzione può essere aggiunta solo dopo la creazione di un set di ambienti di produzione e di staging.

>[!TIP]
>
>Consulta [Configurare una pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md).

## Pipeline non di produzione {#non-prod-pipeline}

Una pipeline non di produzione serve principalmente per eseguire controlli di qualità del codice o per distribuire il codice sorgente in un ambiente di sviluppo.

>[!TIP]
>
>Consulta [Configurare una pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md).

## Origini del codice {#code-sources}

Le pipeline possono anche differire per il tipo di codice che distribuiscono, oltre che per gli ambienti di produzione e non di produzione.

* **[Pipeline full stack](#full-stack-pipeline)**: distribuiscono simultaneamente le build del codice back-end e front-end contenenti una o più applicazioni server di AEM con configurazioni HTTPD/Dispatcher.
* **[Pipeline di configurazione](#config-deployment-pipeline)** - Puoi distribuire rapidamente le configurazioni per funzionalità quali l&#39;inoltro del registro e le attività di manutenzione correlate all&#39;eliminazione. Include inoltre varie configurazioni CDN (Content Delivery Network), ad esempio le regole del filtro del traffico, incluse le regole del firewall per l’applicazione web (WAF). Inoltre, puoi gestire le trasformazioni di richieste e risposte, i selettori di origine, i reindirizzamenti lato client, le pagine di errore, le chiavi CDN, le chiavi API di eliminazione e l’autenticazione di base. Per ulteriori informazioni, vedere [Utilizzare pipeline di configurazione](/help/operations/config-pipeline.md).
* **[Pipeline front-end](#front-end)**: distribuiscono le build del codice front-end contenenti una o più applicazioni dell&#39;interfaccia utente lato client.
* **[Pipeline di configurazione a livello web](#web-tier-config-pipelines)** - Distribuisce le configurazioni HTTPD/Dispatcher.

Questi tipi di pipeline sono descritti in dettaglio più avanti in questo documento.

### Comprendere le pipeline CI/CD in Cloud Manager {#understand-pipelines}

La tabella seguente riepiloga le pipeline disponibili in Cloud Manager e i relativi utilizzi.

| Tipo di pipeline | Distribuzione o qualità del codice | Codice Source | Scopo | Note |
| --- | --- | --- | --- | ---|
| Produzione o non produzione | Distribuzione | Full stack | Distribuisce simultaneamente le build del codice back-end e front-end con le configurazioni HTTPD/Dispatcher | Utilizzato quando il codice front-end deve essere distribuito contemporaneamente al codice server di AEM. Utilizzato quando non sono ancora state adottate le pipeline front-end o di configurazione a livello web. |
| Produzione o non produzione | Distribuzione | Front-end | Distribuisce la build del codice front-end contenente una o più applicazioni dell’interfaccia utente lato client | Supporta più pipeline front-end simultanee<br>Distribuzioni molto più veloci rispetto a quelle full-stack. |
| Produzione o non produzione | Distribuzione | Configurazione a livello web | Distribuisce le configurazioni HTTPD/Dispatcher | Distribuzione in pochi minuti |
| Produzione o non produzione | Distribuzione | Configurazione | Distribuisce [configurazione per una serie di funzionalità](/help/operations/config-pipeline.md) relative a CDN, inoltro log ed eliminazione di attività di manutenzione | Distribuzione in pochi minuti |
| Non produzione | Qualità del codice | Full stack | Esegue controlli di qualità del codice full stack senza una distribuzione | Supporta più pipeline |
| Non di produzione | Qualità del codice | Front-end | Esegue controlli di qualità del codice front-end senza una distribuzione | Supporta più pipeline |
| Non di produzione | Qualità del codice | Configurazione a livello web | Esegue controlli di qualità del codice su configurazioni Dispatcher senza una distribuzione | Supporta più pipeline |

Il diagramma seguente illustra le configurazioni delle pipeline di Cloud Manager con archivio tradizionale front-end singolo o indipendente.

![Configurazioni delle pipeline di Cloud Manager](/help/implementing/cloud-manager/assets/configure-pipeline/cm-setup.png)

## Pipeline full stack {#full-stack-pipeline}

Le pipeline full stack distribuiscono contemporaneamente il codice back-end, il codice front-end e le configurazioni a livello web nel runtime di AEM.

* Codice back-end: contenuti non modificabili come codice Java, configurazioni OSGi, repoinit e contenuti modificabili
* Codice front-end: risorse dell’interfaccia utente dell’applicazione come JavaScript, CSS e font
* Configurazione a livello web: configurazioni HTTPD/Dispatcher

La pipeline full stack rappresenta una pipeline &quot;completa&quot;. Gestisce tutto simultaneamente, consentendo inoltre agli utenti di distribuire separatamente il codice front-end o le configurazioni Dispatcher. Questa distribuzione avviene rispettivamente tramite la pipeline front-end e le pipeline di configurazione a livello web.

Le pipeline full stack creano pacchetti del codice front-end (JavaScript/CSS) come [librerie client di AEM](/help/implementing/developing/introduction/clientlibs.md).

Le pipeline full stack possono distribuire configurazioni a livello web se non è stata configurata una [pipeline di configurazione a livello web](#web-tier-config-pipelines).

Si applicano le seguenti restrizioni.

* Per configurare o eseguire le pipeline è necessario che l’utente con il ruolo **Responsabile dell’implementazione** abbia eseguito l’accesso.
* In qualsiasi momento può essere presente una sola pipeline full stack per ogni ambiente.

Inoltre, se scegli di introdurre una [pipeline di configurazione a livello web](#web-tier-config-pipelines), è bene tenere presente il comportamento della pipeline full stack.

* La pipeline full stack per un ambiente ignora la configurazione Dispatcher se esiste la pipeline di configurazione a livello web corrispondente.
* Se la pipeline di configurazione a livello web corrispondente per l’ambiente non esiste, l’utente può configurare la pipeline full stack per includere o ignorare la configurazione Dispatcher.

Le pipeline full stack possono essere di qualità del codice o di distribuzione.

### Configurare le pipeline full stack {#configure-full-stack}

Consulta [Aggiungere una pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#full-stack-code).
Consulta [Aggiungere una pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code).

## Configurare le pipeline {#config-deployment-pipeline}

Utilizzando una pipeline di configurazione, puoi distribuire rapidamente le impostazioni per l’inoltro del registro, le attività di manutenzione relative all’eliminazione e varie configurazioni CDN, comprese le regole del filtro del traffico (come le regole di WAF (Web Application Firewall)). Inoltre, puoi gestire le trasformazioni di richieste e risposte, i selettori di origine, i reindirizzamenti lato client, le pagine di errore, le chiavi CDN gestite dal cliente, le chiavi API di eliminazione e l’autenticazione di base.

Consulta [Utilizzare le pipeline di configurazione](/help/operations/config-pipeline.md) per un elenco completo delle funzioni supportate e per scoprire come gestire le configurazioni nel tuo archivio in modo che vengano distribuite correttamente.

>[!NOTE]
>
>Le pipeline di configurazione di Edge Delivery non dispongono di ambienti di sviluppo, staging e produzione separati. In AEM as a Cloud Service, le modifiche passano attraverso i livelli di sviluppo, stage e produzione. Al contrario, una pipeline di configurazione di Edge Delivery applica la propria configurazione direttamente a tutti i domini di Edge Delivery Sites registrati in Cloud Manager. Per ulteriori informazioni, consulta [Aggiungere una pipeline di Edge Delivery](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md).


### Configurare le pipeline di configurazione {#configure-config-deployment}

Consulta [Aggiungere una pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#targeted-deployment).
Consulta [Aggiungere una pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#targeted-deployment).

## pipeline front-end {#front-end}

Per codice front-end si intende qualsiasi codice utilizzato come file statico. È separato dal codice dell’interfaccia utente fornito da AEM e può includere temi del sito, applicazioni SPA definite dal cliente, SPA e altre soluzioni.

Le pipeline front-end consentono ai team di semplificare il processo di progettazione e sviluppo consentendo una distribuzione accelerata del codice front-end, asincrona rispetto allo sviluppo back-end. Questa pipeline dedicata distribuisce JavaScript e CSS al livello di distribuzione AEM come tema, dando luogo a una nuova versione del tema, a cui è possibile fare riferimento dalle pagine distribuite da AEM.

>[!NOTE]
>
>Gli utenti con ruolo **Responsabile dell’implementazione** possono creare ed eseguire più pipeline front-end contemporaneamente.
>
>Tuttavia, il limite massimo è di 300 pipeline per programma (per tutti i tipi).

Le pipeline front-end possono essere pipeline per qualità del codice o per distribuzione.

### Prima di configurare le pipeline front-end {#before-start}

Prima di configurare le pipeline front-end, consulta la sezione [Percorso Creazione rapida sito di AEM](/help/journey-sites/quick-site/overview.md) per una guida end-to-end all’intuitivo strumento di AEM per la creazione rapida dei siti. Questo percorso consente di semplificare lo sviluppo front-end e di personalizzare rapidamente il sito senza alcuna conoscenza del back-end di AEM.

### Configurare una pipeline front-end {#configure-front-end}

Consulta [Aggiungere una pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline).
Consulta [Aggiungere una pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline).

### Sviluppare Sites con la pipeline front-end {#developing-with-front-end-pipeline}

Con le pipeline front-end, i team di sviluppo front-end acquisiscono maggiore indipendenza e il processo di sviluppo può essere accelerato.

Consulta [Sviluppa siti con la pipeline front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) per informazioni sul funzionamento del processo e alcune considerazioni per sfruttare al massimo il potenziale.

## Pipeline di configurazione a livello web {#web-tier-config-pipelines}

Le pipeline di configurazione a livello web consentono la distribuzione esclusiva della configurazione HTTPD/Dispatcher nel runtime di AEM, separandola dalle altre modifiche al codice. Si tratta di una pipeline semplificata che offre agli utenti che desiderano implementare solo le modifiche alla configurazione di Dispatcher un metodo accelerato per farlo in pochi minuti.

>[!TIP]
>
>Le pipeline di configurazione a livello web consentono di memorizzare la configurazione web nella stessa posizione di origine o in una posizione diversa della pipeline full stack, a seconda di ciò che si adatta meglio alla struttura del progetto.

Si applicano le seguenti restrizioni.

* Utilizza AEM versione `2021.12.6151.20211217T120950Z` o successiva per utilizzare le pipeline di configurazione a livello web.
* [Accedi alla modalità flessibile degli strumenti di Dispatcher](/help/implementing/dispatcher/disp-overview.md#validation-debug) per utilizzare le pipeline di configurazione a livello web.
* Per configurare o eseguire le pipeline è necessario che l’utente con il ruolo **Responsabile dell’implementazione** abbia eseguito l’accesso.
* In qualsiasi momento può essere presente una sola pipeline di configurazione a livello web per ogni ambiente.
* L’utente non può configurare una pipeline di configurazione a livello web quando è in esecuzione la pipeline full stack corrispondente.
* La struttura a livello web deve rispettare la struttura della modalità flessibile, come definito nel documento [Dispatcher nel cloud](/help/implementing/dispatcher/disp-overview.md#validation-debug).

Inoltre, è bene tenere presente il comportamento della [pipeline full stack](#full-stack-pipeline) quando si introduce una pipeline a livello web.

* Se per un ambiente non è impostata una pipeline di configurazione a livello web, l’utente può scegliere di includere o ignorare la configurazione di Dispatcher durante la configurazione della pipeline full stack. Questa selezione viene effettuata durante l’esecuzione e la distribuzione.
* Una volta configurata una pipeline di configurazione a livello web per un ambiente, la corrispondente pipeline full stack (se presente) ignora la configurazione Dispatcher durante l’esecuzione e la distribuzione.
* Dopo aver eliminato la pipeline di configurazione a livello web, la pipeline full stack corrispondente viene reimpostata per distribuire le configurazioni Dispatcher durante l’esecuzione.

Le pipeline di configurazione a livello web possono essere di tipo `Code quality` o `Deployment`.

### Configurare le pipeline a livello web {#configure-web-tier}

Consulta [Aggiungere una pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#targeted-deployment).
Consulta [Aggiungere una pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#targeted-deployment).

## Panoramica video dei tipi di pipeline {#video}

Per una rapida panoramica dei tipi di pipeline, guarda il video seguente (2 minuti e 26 secondi).

>[!VIDEO](https://video.tv.adobe.com/v/342363)
