---
title: Pipeline CI-CD
description: Segui questa pagina per informazioni sulle pipeline CI-CD di Cloud Manager
index: false
source-git-commit: 65898bd90e057cf5d646c5183ba6d2c8bdcac06e
workflow-type: tm+mt
source-wordcount: '826'
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

![](/help/implementing/cloud-manager/assets/configure-pipeline/ci-cdpipeline-overview.png)

## Pipeline di produzione {#prod-pipeline}

Una pipeline di produzione è una pipeline appositamente creata che include una serie di passaggi orchestrati per portare il codice sorgente completamente in produzione. I passaggi includono la creazione, la creazione di pacchetti, il test, la convalida e la distribuzione in tutti gli ambienti Stage. Inutile dire che una pipeline di produzione può essere aggiunta solo una volta creato un set di ambienti di produzione e di stage .

Fai riferimento a [Configurazione di una pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) per ulteriori dettagli.


## Pipeline non di produzione {#non-prod-pipeline}

Una pipeline non di produzione ha lo scopo di eseguire scansioni di qualità del codice o di distribuire il codice sorgente in un ambiente di sviluppo.

Fai riferimento a [Configurazione di una pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) per ulteriori dettagli.

## Informazioni sulle pipeline CI-CD in Cloud Manager {#understand-pipelines}

La tabella seguente riepiloga tutte le pipeline in Cloud Manager e il relativo utilizzo.

| Tipo di pipeline | Implementazione o qualità del codice | Codice sorgente | Quando utilizzare | Quando o perché dovrei usare? |
|--- |--- |--- |---|---|---|
| Produzione o non produzione | Implementazione | Front end | Per distribuire il codice front-end. Il codice front-end è qualsiasi codice che viene utilizzato come file statico. È separato dal codice dell’interfaccia utente gestito da AEM. Include i temi Sites, le SPA definite dal cliente, Firefly SPA e qualsiasi altra soluzione. Deve essere AEM versione. | Tempi di distribuzione rapidi<br> È possibile configurare più pipeline front-end ed eseguirle contemporaneamente in base all’ambiente |
|  | Implementazione | Stack completo | Per implementare la configurazione back-end, front-end e HTTPD/dispatcher contemporaneamente. Si applicano alcune restrizioni. | Quando le condutture front end non sono ancora state adottate. |
| Non produzione | Qualità del codice | Front end | Esegui analisi della qualità del codice sul codice front-end | Tempi di distribuzione rapidi<br> È possibile configurare ed eseguire più pipeline |
|  | Qualità del codice | Stack completo | Esegui la scansione della qualità del codice sull&#39;intero codice dello stack | Tempi di distribuzione rapidi<br> È possibile configurare ed eseguire più pipeline |

Il diagramma seguente illustra le configurazioni della pipeline di Cloud Manager con archivio front-end tradizionale singolo o con configurazione dell’archivio front-end indipendente:

![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-configurations.png)

## Pipe front-end di Cloud Manager {#front-end}

Le pipeline front-end consentono ai team di semplificare il processo di progettazione e sviluppo, abilitando pipeline front-end accelerate per l’implementazione del codice front-end. Questa pipeline differenziata distribuisce JavaScript e CSS al livello di distribuzione AEM come tema, dando luogo a una nuova versione del tema a cui è possibile fare riferimento dalle pagine consegnate dal runtime di AEM. Il codice front-end è qualsiasi codice che viene utilizzato come file statico. È separato dal codice dell’interfaccia utente gestito da AEM. Include i temi Sites, le SPA definite dal cliente, Firefly SPA e qualsiasi altra soluzione.

>[!NOTE]
>Un utente connesso come ruolo di Deployment Manager può creare ed eseguire più pipeline front-end contemporaneamente. Esiste tuttavia un limite massimo di 300 gasdotti per programma (per tutti i tipi).

Possono essere di tipo Front End Code Quality o le pipeline di distribuzione Front End.

### Prima di configurare le pipeline front-end {#before-start}

Prima di iniziare a configurare le pipeline front-end, vedere AEM Percorso di creazione rapida di siti per un flusso di lavoro end-to-end tramite lo strumento di creazione rapida AEM facile da utilizzare. Questo sito di documentazione ti aiuterà a semplificare lo sviluppo front-end del tuo sito AEM e a personalizzare rapidamente il tuo sito senza AEM conoscenza back-end.

### Configurare la pipeline front-end {#configure-front-end}

Per informazioni su come configurare la pipeline front-end, consulta:

* Aggiunta di una pipeline di produzione
* Aggiunta di una pipeline non di produzione

## Pipellini full-stack {#full-stack-pipeline}

La pipeline full Stack offre all’utente la possibilità di implementare la configurazione back-end, front-end e HTTPD/dispatcher contemporaneamente.  Distribuisce codice e contenuto nel runtime di AEM, incluso il codice front-end (JavaScript/CSS) incluso nel pacchetto come librerie client AEM. Può distribuire la configurazione del livello web se non è configurata una pipeline del livello web. Rappresenta la pipeline &quot;uber&quot;, offrendo agli utenti le opzioni per distribuire esclusivamente il codice Front End o la configurazione del dispatcher tramite rispettivamente la pipeline Front End e la pipeline di configurazione del livello Web.

Saranno applicate le seguenti restrizioni:

1. Per configurare o eseguire le pipeline, è necessario che un utente sia connesso come gestore distribuzione.

1. In qualsiasi momento, può essere disponibile una sola pipeline Stack completa per ogni ambiente.

1. L’utente può configurare la pipeline Full Stack per un ambiente in modo che ignori o meno la configurazione del dispatcher, Se la pipeline di configurazione corrispondente al livello Web per l’ambiente non esiste.

1. La pipeline di stack completa per un ambiente ignorerà la configurazione del dispatcher se esiste la pipeline di configurazione del livello Web corrispondente per l’ambiente.

Questi possono essere del tipo Stack completo - Qualità codice o Stack completo - pipeline di distribuzione.

### Configurare la pipeline di stack completa {#configure-full-stack}

Per informazioni su come configurare la pipeline a stack completo, consulta:

* Aggiunta di una pipeline di produzione
* Aggiunta di una pipeline non di produzione