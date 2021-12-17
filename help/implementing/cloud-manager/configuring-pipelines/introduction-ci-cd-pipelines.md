---
title: Pipeline CI-CD
description: Segui questa pagina per informazioni sulle pipeline CI-CD di Cloud Manager
index: true
source-git-commit: 3d48bd507305e7a1d3efa2b61123afdae1f52ced
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 0%

---


# Pipeline CI-CD di Cloud Manager {#intro-cicd}

## Introduzione {#introduction}

Una pipeline CI/CD in Cloud Manager può essere attivata da un qualche tipo di evento, ad esempio una richiesta di pull da un archivio di codice sorgente, ovvero una modifica del codice o una sorta di pianificazione regolare che corrisponda a una frequenza di rilascio.

>[!NOTE]
>Per configurare la pipeline, devi:
>* definire il trigger che avvierà la pipeline
>* definire i parametri che controllano la distribuzione di produzione
>* configurare i parametri del test delle prestazioni


In Cloud Manager sono disponibili due tipi di pipeline:

* [Pipeline di produzione](#prod-pipeline)
* [Pipeline non di produzione](#non-prod-pipeline)

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cd-config1.png)


## Pipeline di produzione {#prod-pipeline}

Una pipeline di produzione è una pipeline appositamente creata che include una serie di passaggi orchestrati per portare il codice sorgente completamente in produzione. I passaggi includono la creazione, la creazione di pacchetti, il test, la convalida e la distribuzione in tutti gli ambienti Stage. Inutile dire che una pipeline di produzione può essere aggiunta solo una volta creato un set di ambienti di produzione e di stage .

Fai riferimento a [Configurazione di una pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) per ulteriori dettagli.


## Pipeline non di produzione {#non-prod-pipeline}

Una pipeline non di produzione ha lo scopo di eseguire scansioni di qualità del codice o di distribuire il codice sorgente in un ambiente di sviluppo.

Fai riferimento a [Configurazione di una pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) per ulteriori dettagli.

## Informazioni sulle pipeline CI-CD in Cloud Manager {#understand-pipelines}

La tabella seguente riepiloga tutte le pipeline in Cloud Manager e il relativo utilizzo.

| Tipo di pipeline | Implementazione o qualità del codice | Codice sorgente | Quando utilizzare | Quando o perché dovrei usare? |
|--- |--- |--- |---|---|
| Produzione o non produzione | Implementazione | Front end | Tempi di implementazione rapidi.<br>È possibile configurare più pipeline front-end ed eseguirle contemporaneamente per ogni ambiente.<br>La build della pipeline Front End invia la build a uno storage. Quando viene servita una pagina HTML, può fare riferimento a file statici Frontend Code che verranno serviti dalla CDN utilizzando questa memorizzazione come origine. | Per distribuire esclusivamente codice front-end contenente una o più applicazioni dell’interfaccia utente lato client. Il codice front-end è qualsiasi codice che viene utilizzato come file statico. È separato dal codice dell’interfaccia utente gestito da AEM. Include i temi Sites, le SPA definite dal cliente, Firefly SPA e qualsiasi altra soluzione.<br>Deve essere AEM versione 2021.10.5933.20211012T154732Z<br>È necessario che Sites sia abilitato. |
| Produzione o non produzione | Implementazione | Stack completo | Quando le condutture front end non sono ancora state adottate.<br>Per i casi in cui il codice Front End deve essere distribuito esattamente nello stesso momento del codice del server AEM. | Per distribuire AEM codice server (contenuto immutabile, codice Java, configurazioni OSGi, configurazione HTTPD/dispatcher, reindirizzamento, contenuto mutabile, font), contenente una o più applicazioni server AEM tutte allo stesso tempo. |
| Non produzione | Qualità del codice | Front end | Avere la valutazione di Cloud Manager. la creazione è riuscita e la qualità del codice senza eseguire una distribuzione.<br>È possibile configurare ed eseguire più pipeline. | Esegui analisi della qualità del codice sul codice front-end. |
| Non produzione | Qualità del codice | Stack completo | Avere la valutazione di Cloud Manager. la creazione è riuscita e la qualità del codice senza eseguire una distribuzione.<br>È possibile configurare ed eseguire più pipeline. | Esegui la scansione della qualità del codice sull&#39;intero codice dello stack. |


Il diagramma seguente illustra le configurazioni della pipeline di Cloud Manager con archivio front-end tradizionale singolo o con configurazione dell’archivio front-end indipendente:

![](/help/implementing/cloud-manager/assets/configure-pipeline/cm-setup.png)

## Pipe front-end di Cloud Manager {#front-end}

Le pipeline front-end consentono ai team di semplificare il processo di progettazione e sviluppo, abilitando pipeline front-end accelerate per l’implementazione del codice front-end. Questa pipeline differenziata distribuisce JavaScript e CSS al livello di distribuzione AEM come tema, dando luogo a una nuova versione del tema a cui è possibile fare riferimento dalle pagine consegnate dal runtime di AEM. Il codice front-end è qualsiasi codice che viene utilizzato come file statico. È separato dal codice dell’interfaccia utente gestito da AEM. Include i temi Sites, le SPA definite dal cliente, Firefly SPA e qualsiasi altra soluzione.

>[!IMPORTANT]
>È necessario utilizzare AEM versione `2021.10.5933.20211012T154732Z ` per sfruttare le pipeline front-end.

>[!NOTE]
>Un utente connesso come ruolo di Deployment Manager può creare ed eseguire più pipeline front-end contemporaneamente. Esiste tuttavia un limite massimo di 300 gasdotti per programma (per tutti i tipi).

Possono essere di tipo Front End Code Quality o le pipeline di distribuzione Front End.

### Prima di configurare le pipeline front-end {#before-start}

Prima di iniziare a configurare le pipeline Front End, consulta [AEM Percorso di creazione di siti rapidi](/help/journey-sites/quick-site/overview.md) per un flusso di lavoro end-to-end tramite lo strumento di creazione rapida AEM facile da usare. Questo sito di documentazione ti aiuterà a semplificare lo sviluppo front-end del tuo sito AEM e a personalizzare rapidamente il tuo sito senza AEM conoscenza back-end.

### Configurare una pipeline front-end {#configure-front-end}

Per informazioni su come configurare la pipeline front-end, consulta:

* [Aggiunta di una pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [Aggiunta di una pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)

### Sviluppo di siti con la pipeline front-end {#developing-with-front-end-pipeline}

Con la pipeline front-end, viene data maggiore indipendenza agli sviluppatori front-end e il processo di sviluppo può ottenere una notevole velocità.

Fai riferimento a [presente documento](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) per come questo processo funziona insieme ad alcune considerazioni di cui tenere conto al fine di sfruttare appieno il potenziale di questo processo.

## Pipellini full-stack {#full-stack-pipeline}

La pipeline full Stack offre all’utente la possibilità di implementare la configurazione back-end, front-end e HTTPD/dispatcher contemporaneamente.  Distribuisce codice e contenuto nel runtime di AEM, incluso il codice front-end (JavaScript/CSS) incluso nel pacchetto come librerie client AEM. Può distribuire la configurazione del livello web se non è configurata una pipeline del livello web. Rappresenta la pipeline &quot;uber&quot;, offrendo agli utenti le opzioni per distribuire esclusivamente il codice Front End o la configurazione del dispatcher tramite rispettivamente la pipeline Front End e la pipeline di configurazione del livello Web.
Questi possono essere del tipo Stack completo - Qualità codice o Stack completo - pipeline di distribuzione.

Saranno applicate le seguenti restrizioni:

1. Per configurare o eseguire le pipeline, è necessario che un utente sia connesso come gestore distribuzione.

1. In qualsiasi momento, può essere disponibile una sola pipeline Stack completa per ogni ambiente.

1. L’utente può configurare la pipeline Full Stack per un ambiente in modo che ignori o meno la configurazione del dispatcher, Se la pipeline di configurazione corrispondente al livello Web per l’ambiente non esiste.

1. La pipeline di stack completa per un ambiente ignorerà la configurazione del dispatcher se esiste la pipeline di configurazione del livello Web corrispondente per l’ambiente.


### Configurare una pipeline di stack completa {#configure-full-stack}

Per informazioni su come configurare la pipeline a stack completo, consulta:

* [Aggiunta di una pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md#adding-production-pipeline)
* [Aggiunta di una pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#adding-non-production-pipeline)