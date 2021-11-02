---
title: Pipeline CI-CD
description: Pipeline CI-CD
index: false
source-git-commit: 76cff84003576cf23eb1d23674ce6eaf082bbbb1
workflow-type: tm+mt
source-wordcount: '700'
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

## Pipeline di produzione {#prod-pipeline}

Una pipeline di produzione è una pipeline appositamente creata che include una serie di passaggi orchestrati per portare il codice sorgente completamente in produzione. I passaggi includono la creazione, la creazione di pacchetti, il test, la convalida e la distribuzione in tutti gli ambienti Stage. Inutile dire che una pipeline di produzione può essere aggiunta solo una volta creato un set di ambienti di produzione e di stage .

Per ulteriori informazioni, consulta Configurazione della pipeline di produzione .


## Pipeline non di produzione {#non-prod-pipeline}

Una pipeline non di produzione ha lo scopo di eseguire scansioni di qualità del codice o di distribuire il codice sorgente in un ambiente di sviluppo.

Per ulteriori informazioni, consulta Pipelines non di produzione e solo qualità del codice .

## Informazioni sulle pipeline CI-CD in Cloud Manager {#understand-pipelines}

La tabella seguente classifica le pipeline in Cloud Manager con il relativo utilizzo.

| Tipo di pipeline | Implementazione o qualità del codice | Codice sorgente | Quando utilizzare | Quando o perché dovrei usare? |
|--- |--- |--- |---|---|---|
| Produzione o non produzione | Implementazione | Front end | Per distribuire il codice front-end. Il codice front-end è qualsiasi codice che viene utilizzato come file statico. È separato dal codice dell’interfaccia utente gestito da AEM. Include i temi Sites, le SPA definite dal cliente, Firefly SPA e qualsiasi altra soluzione. Deve essere AEM versione. | Tempi di implementazione rapidi.<br> È possibile configurare più pipeline front-end ed eseguirle contemporaneamente per ogni ambiente. |
|  | Implementazione | Stack completo | Per implementare la configurazione back-end, front-end e HTTPD/dispatcher contemporaneamente. Nota: Si applicano alcune restrizioni. | Quando le pipeline di configurazione front-end o livello Web non sono ancora state adottate. |
|  | Implementazione | Configurazione a livello web | Per distribuire esclusivamente la configurazione HTTPD/dispatcher in pochi minuti.  Questa pipeline semplificata fornisce agli utenti che desiderano distribuire solo le modifiche alla configurazione del dispatcher, un metodo accelerato per farlo. Nota: Deve essere su AEM versione [version] | Tempi di implementazione rapidi. |



## Pipe front-end di Cloud Manager {#front-end}

Le pipeline front-end consentono ai team di semplificare il processo di progettazione e sviluppo, abilitando pipeline front-end accelerate per l’implementazione del codice front-end. Questa pipeline differenziata distribuisce JavaScript e CSS al livello di distribuzione AEM come tema, dando luogo a una nuova versione del tema a cui è possibile fare riferimento dalle pagine consegnate dal runtime di AEM. Il codice front-end è qualsiasi codice che viene utilizzato come file statico. È separato dal codice dell’interfaccia utente gestito da AEM. Include i temi Sites, le SPA definite dal cliente, Firefly SPA e qualsiasi altra soluzione.

>[!NOTE]
>Un utente connesso come ruolo di Deployment Manager può creare ed eseguire più pipeline front-end contemporaneamente. Esiste tuttavia un limite massimo di 300 gasdotti per programma (per tutti i tipi).

Esistono due tipi di pipeline front-end:

* Qualità del codice front-end
* Implementazione front-end

## Pipellini full-stack {#full-stack-pipeline}

La pipeline full Stack offre all’utente la possibilità di implementare la configurazione back-end, front-end e HTTPD/dispatcher contemporaneamente.  Distribuisce codice e contenuto nel runtime di AEM, incluso il codice front-end (JavaScript/CSS) incluso nel pacchetto come librerie client AEM. Può distribuire la configurazione del livello web se non è configurata una pipeline del livello web. Rappresenta la pipeline &quot;uber&quot;, offrendo agli utenti le opzioni per distribuire esclusivamente il codice Front End o la configurazione del dispatcher tramite rispettivamente la pipeline Front End e la pipeline di configurazione del livello Web.


Saranno applicate le seguenti restrizioni:

1. Per configurare o eseguire le pipeline, è necessario che un utente sia connesso come gestore distribuzione.

1. In qualsiasi momento, può essere disponibile una sola pipeline Stack completa per ogni ambiente.

1. L’utente può configurare la pipeline Full Stack per un ambiente in modo che ignori o meno la configurazione del dispatcher, Se la pipeline di configurazione corrispondente al livello Web per l’ambiente non esiste.

1. La pipeline di stack completa per un ambiente ignorerà la configurazione del dispatcher se esiste la pipeline di configurazione del livello Web corrispondente per l’ambiente.

Esistono due tipi di tubazioni full Stack:

* Pipeline di qualità del codice di stack completo
* Pipa di distribuzione full stack

