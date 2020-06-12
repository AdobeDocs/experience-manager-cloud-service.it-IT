---
title: Utilizzo di Cloud Ready Analyzer
description: Utilizzo di Cloud Ready Analyzer
translation-type: tm+mt
source-git-commit: 1739f81d4894f3e04cc4119f344a3bea5bd042d8
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 1%

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

   ![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-1.png)

1. Dopo aver fatto clic su **Cloud Readiness Analyzer**, lo strumento avvia la generazione del rapporto e, dopo pochi minuti, il rapporto di riepilogo è disponibile nell’istanza di AEM.

   >[!NOTE]
   >Sarà necessario scorrere la pagina verso il basso per visualizzare il rapporto completo.

   ![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-2.png)

### Visualizzazione dei risultati nel rapporto di riepilogo {#viewing-the-results}

>[!IMPORTANT]
>I report generati da Cloud Readiness Analyzer sono basati su Rilevatori di pattern. Per ulteriori informazioni, consultate Rilevatori [](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html) di pattern.

Quando scorri verso il basso la pagina per visualizzare il rapporto di riepilogo completo, puoi vedere le seguenti informazioni per ciascuna delle categorie evidenziate nel rapporto:

1. **Livello di importanza**

   Nella tabella seguente è illustrato il significato dei vari livelli di importanza Rilevatore pattern e Analisi prontezza cloud.

   | Livello di importanza | Descrizione |
   |--- |--- |
   | INFO/0 | Questa conclusione è fornita a scopo informativo. |
   | AVVISO/1 | Questo risultato potrebbe essere un problema di aggiornamento. Si raccomanda di effettuare ulteriori indagini. |
   | MAGGIORE/2 | Questo risultato potrebbe rappresentare un problema di aggiornamento da risolvere. |
   | CRITICO/3 | Questo risultato è molto probabile che sia un problema di aggiornamento che deve essere risolto per evitare la perdita di funzioni o prestazioni. |

1. **Descrizione** La descrizione fornisce informazioni sulla categoria segnalata.

1. **URL** documentazione L&#39;URL della documentazione consente di visualizzare la documentazione tecnica per il tipo associato.

1. **Messaggio** Una descrizione del risultato in un unico messaggio.

### Visualizzazione dei risultati in formato CSV {#viewing-the-results-csv}

Il rapporto di riepilogo è disponibile nell&#39;interfaccia utente di AEM. Potete scaricare il rapporto completo in un formato CSV (Comma Separated Value) utile durante il processo di refactoring.

Per generare un formato CSV del rapporto di riepilogo, effettuate le seguenti operazioni:

1. 
   1. Seleziona Adobe Experience Manager e passa agli strumenti -> **Operazioni** -> **Cloud Readiness Analyzer**.

1. Una volta che il rapporto è disponibile, fai clic su **CSV** per scaricare il rapporto completo di riepilogo in formato CSV (Comma Separated Value), come mostrato nella figura seguente.

![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-3.png)


#### Visualizzazione del rapporto nelle istanze di AEM 6.1 {#aem-instances-report}

Per scaricare il rapporto CSV per Adobe Experience Manager (AEM) 6.1, effettuate le seguenti operazioni:

1. Passa alla consoleConfigurazione **Web di** Adobe Experience Manager utilizzando `https://serveraddress:serverport/system/console/configMgr`.

1. Selezionate la scheda **Stato** e cercate **Rilevamento** pattern dall&#39;elenco a discesa, come illustrato nella figura riportata di seguito.

   ![image](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-4.png)

1. Potete scaricare il rapporto di riepilogo in una cartella zip o in un formato JSON.


