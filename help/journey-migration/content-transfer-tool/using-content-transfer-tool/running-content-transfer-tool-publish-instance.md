---
title: Esecuzione dello strumento Content Transfer (Trasferimento contenuti) su un’istanza di pubblicazione
description: Esecuzione dello strumento Content Transfer (Trasferimento contenuti) su un’istanza di pubblicazione
exl-id: 01faab94-a939-4004-b094-e9eb8f67b96e
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 11%

---

# Esecuzione dello strumento Content Transfer (Trasferimento contenuti) su un’istanza di pubblicazione {#run-content-transfer-tool-publish-instance}

## Introduzione {#introduction}

Lo strumento Content Transfer (CTT) non esegue alcun tipo di analisi del contenuto prima di trasferirlo dall’istanza sorgente all’istanza di destinazione. Ad esempio, CTT non distingue tra contenuto pubblicato e non pubblicato durante l’acquisizione del contenuto in un ambiente di pubblicazione. Qualsiasi contenuto specificato nel set di migrazione viene acquisito nell’istanza di destinazione selezionata. L’utente può acquisire un set di migrazione in un’istanza Author, Publish o entrambe.

>[!NOTE]
>Durante lo spostamento del contenuto in un’istanza di produzione, si consiglia di installare lo strumento Content Transfer (Trasferimento contenuti) nell’istanza di authoring di origine per spostare il contenuto nell’istanza di authoring di destinazione e, analogamente, di installare lo strumento Content Transfer (Trasferimento contenuti) nell’istanza di pubblicazione di origine per spostare il contenuto nell’istanza di pubblicazione di destinazione. Consulta [Approccio consigliato](#recommended-approach) per ulteriori dettagli.

## Approccio consigliato {#recommended-approach}

Segui l’approccio raccomandato come descritto di seguito:

* Utilizza la stessa versione dello strumento Content Transfer (Trasferimento contenuti) utilizzata nell’istanza di authoring.

* È necessario migrare un solo nodo di pubblicazione. Deve essere rimosso dal load balancer prima di iniziare l’estrazione.

* Durante l’acquisizione per la pubblicazione, il livello di pubblicazione non verrà ridotto (a differenza dell’authoring).

  >[!IMPORTANT]
  >Come precauzione, evita le operazioni di scrittura avviate dall&#39;utente, ad esempio:
  > * Distribuzione dei contenuti dall’autore as a Cloud Service dell’AEM alla pubblicazione in tale ambiente
  > * Sincronizzazione utenti tra istanze di pubblicazione
