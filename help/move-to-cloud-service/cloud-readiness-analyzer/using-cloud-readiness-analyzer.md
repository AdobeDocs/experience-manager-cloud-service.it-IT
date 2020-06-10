---
title: Utilizzo di Cloud Ready Analyzer
description: Utilizzo di Cloud Ready Analyzer
translation-type: tm+mt
source-git-commit: 3d818278c53f3d3b4c5b53aa5b78d06d876bf05f
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---


# Utilizzo di Cloud Ready Analyzer {#using-cloud-readiness-analyzer}

## Considerazioni importanti per l&#39;utilizzo di Cloud Readiness Analyzer {#imp-considerations}

Seguite la sezione seguente per comprendere le considerazioni importanti durante l&#39;esecuzione di Cloud Readiness Analyzer (CRA):

* CRA è supportato sulle istanze AEM di origine con versione 6.1 e successive.
* CRA può essere eseguito su qualsiasi ambiente.

   >[!NOTE]
   >Per aumentare il tasso di rilevamento ed evitare rallentamenti in casi business critical, si consiglia di eseguire CRA negli ambienti di staging dell&#39;autore di origine che sono il più vicino possibile a quelli di produzione nelle aree di personalizzazioni, configurazioni, contenuti e applicazioni utente. In alternativa, può essere eseguito anche su un clone dell’ambiente di pubblicazione.

## Disponibilità {#availability}

Il Cloud Readiness Analyzer (CRA) può essere scaricato come file zip dal portale di distribuzione del software. Puoi installare il pacchetto tramite Package Manager nella tua istanza sorgente Adobe Experience Manager (AEM).

>[!NOTE]
>Scarica Crea Cloud Readiness Analyzer (CRA) da *in sospeso*.

## Esecuzione di Cloud Readiness Analyzer {#running-tool}

Segui questa sezione per apprendere come eseguire Cloud Reader Analyzer:

1. Seleziona Adobe Experience Manager e passa agli strumenti -> **Operazioni** -> **Cloud Readiness Analyzer**.

### Visualizzazione dei risultati {#viewing-the-results}

Esistono due modi per visualizzare l&#39;output del CRA:

1. Utilizzo del rapporto organizzato

   >[!NOTE]
   >Il rapporto organizzato è disponibile su AEM versione 6.3 e successive.

Fare riferimento a CRA Document Planning and Status (Pianificazione documento CRA e Stato) per descrivere i livelli di importanza nel rapporto

1. Visualizzazione dell&#39;output del CRA (utilizzabile con AEM versione 6.1 e successive):

   1. Andate alla console Web di AEM sfogliando.

   1. Selezionate Stato - Analizzatore di prontezza cloud come illustrato nell&#39;immagine seguente.

#### Comprendere i livelli di importanza nel rapporto {#importance-levels}

Nella tabella seguente è illustrato il significato dei vari livelli di importanza Rilevatore pattern e Analisi prontezza cloud.

| Livello di importanza | Descrizione |
|--- |--- |
| INFO/0 | Questa conclusione è fornita a scopo informativo. |
| AVVISO/1 | Questo risultato potrebbe essere un problema di aggiornamento. Si raccomanda di effettuare ulteriori indagini. |
| MAGGIORE/2 | Questo risultato potrebbe rappresentare un problema di aggiornamento da risolvere. |
| CRITICO/3 | Questo risultato è molto probabile che sia un problema di aggiornamento che deve essere risolto per evitare la perdita di funzioni o prestazioni. |