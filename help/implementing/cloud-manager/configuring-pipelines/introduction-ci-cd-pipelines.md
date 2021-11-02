---
title: Pipeline CI-CD
description: Pipeline CI-CD
index: false
source-git-commit: 1887cc7374ece840b2dcca4482924b14c4793567
workflow-type: tm+mt
source-wordcount: '185'
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
