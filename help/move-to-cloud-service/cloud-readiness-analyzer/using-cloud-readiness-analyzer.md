---
title: Utilizzo di Cloud Ready Analyzer
description: Utilizzo di Cloud Ready Analyzer
translation-type: tm+mt
source-git-commit: 317dd08600df9c7127cf8502341f93758ac8ce0b
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# Utilizzo di Cloud Ready Analyzer {#using-cloud-readiness-analyzer}

## Considerazioni importanti per l&#39;utilizzo di Cloud Readiness Analyzer {#imp-considerations}

Seguite la sezione seguente per comprendere le considerazioni importanti durante l&#39;esecuzione di Cloud Readiness Analyzer (CRA):

* CRA è supportato sulle istanze AEM di origine con versione 6.1 e successive.
* CRA può essere eseguito su qualsiasi ambiente. Tuttavia, per aumentare il tasso di rilevamento ed evitare eventuali rallentamenti nelle istanze business critical, è consigliabile eseguirlo negli ambienti di pre-produzione dell&#39;autore di origine che sono il più vicino possibile a quelli di produzione nelle aree di personalizzazioni, configurazioni, contenuti e applicazioni utente. In alternativa, può essere eseguito anche su un clone dell’ambiente di pubblicazione.

## Disponibilità {#availability}

Il Cloud Readiness Analyzer (CRA) può essere scaricato come file zip dal portale di distribuzione del software. Puoi installare il pacchetto tramite Package Manager nella tua istanza sorgente Adobe Experience Manager (AEM).

>[!NOTE]
>Scarica Crea Cloud Readiness Analyzer (CRA) dall&#39;in sospeso.

## Esecuzione di Cloud Readiness Analyzer {#running-tool}

Segui questa sezione per apprendere come eseguire Cloud Reader Analyzer:

1. Seleziona Adobe Experience Manager e passa agli strumenti -> **Operazioni** -> **Cloud Readiness Analyzer**.

### Visualizzazione dei risultati {#viewing-the-results}

Esistono due modi per visualizzare l&#39;output del CRA:

1. Utilizzo del rapporto organizzato (disponibile nella versione 6.3 e successive di AEM)Per descrivere i livelli di importanza nel rapporto, fare riferimento a CRA Document Planning and Status (Pianificazione documento CRA e stato)

Per visualizzare l&#39;output del CRA (può essere utilizzato con AEM versione 6.1 e successiva):

1. Andate alla console Web di AEM sfogliando.

1. Selezionate Stato - Analizzatore di prontezza cloud come illustrato nell&#39;immagine seguente.