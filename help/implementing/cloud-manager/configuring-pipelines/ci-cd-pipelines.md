---
title: Pipeline CI-CD
description: Pipeline CI-CD
index: false
source-git-commit: b8b4d0b9e7e1dfc6809d2e193a2c2fd2438ecdb6
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# Pipeline CI-CD di Cloud Manager {#intro-cicd}

In Cloud Manager sono disponibili due tipi di pipeline:

* [Pipeline di produzione](#prod-pipeline)
* [Pipeline non di produzione](#non-prod-pipeline)

## Pipeline di produzione {#prod-pipeline}

Una pipeline di produzione è una pipeline appositamente creata che include una serie di passaggi orchestrati per portare il codice sorgente completamente in produzione. I passaggi includono la creazione, la creazione di pacchetti, il test, la convalida e la distribuzione in tutti gli ambienti Stage. Inutile dire che una pipeline di produzione può essere aggiunta solo una volta creato un set di ambienti di produzione e di stage .

>[!NOTE]
>Per ulteriori informazioni, consulta Configurazione della pipeline di produzione .


## Pipeline non di produzione {#non-prod-pipeline}

Una pipeline non di produzione ha lo scopo di eseguire scansioni di qualità del codice o di distribuire il codice sorgente in un ambiente di sviluppo.

>[!NOTE]
>Per ulteriori informazioni, consulta Pipelines non di produzione e solo qualità del codice .

La qualità del codice e dell’implementazione supportati nelle pipeline di produzione e non di produzione in Cloud Manager sono suddivisi in due tipi diversi:

* Front end
* Stack completo

La tabella seguente riepiloga le condutture:


>[!NOTE]
>Una pipeline CI/CD in Cloud Manager viene attivata da un evento, ad esempio una richiesta di pull da un archivio del codice sorgente, ovvero una modifica del codice o una pianificazione regolare corrispondente a una frequenza di rilascio.
>
>Per configurare la pipeline, devi:
>* definire il trigger che avvierà la pipeline
>* definire i parametri che controllano la distribuzione di produzione
>* configurare i parametri del test delle prestazioni