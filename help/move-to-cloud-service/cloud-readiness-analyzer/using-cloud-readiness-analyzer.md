---
title: Utilizzo di Cloud Ready Analyzer
description: Utilizzo di Cloud Ready Analyzer
translation-type: tm+mt
source-git-commit: 47773a56f8bb24342281068a8c4d03d6edfb9277
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---


# Utilizzo di Cloud Ready Analyzer {#using-cloud-readiness-analyzer}

## Considerazioni importanti per l&#39;utilizzo di Cloud Readiness Analyzer {#imp-considerations}

Seguite la sezione seguente per comprendere le considerazioni importanti durante l&#39;esecuzione di Cloud Readiness Analyzer (CRA):

* CRA è supportata nelle istanze AEM di origine con versione 6.1 e superiore
* CRA può essere eseguita in qualsiasi ambiente (preferibilmente in ambiente *Stage* )

   >[!NOTE]
   >Per aumentare il tasso di rilevamento ed evitare rallentamenti in casi business critical, si consiglia di eseguire CRA negli ambienti di staging dell&#39;autore di origine che sono il più vicino possibile a quelli di produzione nelle aree di personalizzazioni, configurazioni, contenuti e applicazioni utente. In alternativa, può essere eseguito anche su un clone dell’ambiente *Pubblica* .

## Disponibilità {#availability}

Cloud Readiness Analyzer può essere scaricato come file zip dal portale di distribuzione software. Puoi installare il pacchetto tramite Package Manager nella tua istanza sorgente Adobe Experience Manager (AEM).

>[!NOTE]
>Scaricate Cloud Readiness Analyzer dal portale di distribuzione software *in sospeso*.

## Esecuzione di Cloud Readiness Analyzer {#running-tool}

Segui questa sezione per apprendere come eseguire Cloud Reader Analyzer:

1. Seleziona Adobe Experience Manager e passa agli strumenti -> **Operazioni** -> **Cloud Readiness Analyzer**.

### Visualizzazione dei risultati {#viewing-the-results}

>[!IMPORTANT]
>I report generati da Cloud Readiness Analyzer sono basati su Rilevatori di pattern. Per ulteriori informazioni, consultate Rilevatori [](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html) di pattern.

Esistono due modi per visualizzare l&#39;output da Cloud Readiness Analyzer:

1. **Utilizzo del rapporto organizzato**

   >[!NOTE]
   >Il rapporto organizzato è disponibile su AEM versione 6.3 e successive.

   Oppure,

1. **Visualizzazione dell&#39;output del CRA**

   Per visualizzare l&#39;output da Cloud Readiness Analyzer, effettuate le operazioni seguenti:

   >[!NOTE]
   >I passaggi indicati di seguito sono applicabili alla versione 6.1 e successiva di AEM.

   1. Passa alla console **Web di** AEM tramite `https://serveraddress:serverport/system/console/configMgr`.

   1. Selezionate **Stato - Rilevatore** pattern come illustrato nella figura riportata di seguito.

#### Visualizzazione del rapporto nelle istanze di AEM 6.1 {#aem-instances-report}

È possibile scaricare il rapporto CSV per AEM 6.1. Questo è in sospeso.

#### Comprendere i livelli di importanza nel rapporto {#importance-levels}

Nella tabella seguente è illustrato il significato dei vari livelli di importanza Rilevatore pattern e Analisi prontezza cloud.

| Livello di importanza | Descrizione |
|--- |--- |
| INFO/0 | Questa conclusione è fornita a scopo informativo. |
| AVVISO/1 | Questo risultato potrebbe essere un problema di aggiornamento. Si raccomanda di effettuare ulteriori indagini. |
| MAGGIORE/2 | Questo risultato potrebbe rappresentare un problema di aggiornamento da risolvere. |
| CRITICO/3 | Questo risultato è molto probabile che sia un problema di aggiornamento che deve essere risolto per evitare la perdita di funzioni o prestazioni. |