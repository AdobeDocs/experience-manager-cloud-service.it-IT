---
title: Esecuzione dello strumento Content Transfer (Trasferimento contenuti) su un’istanza di pubblicazione
description: Esecuzione dello strumento Content Transfer (Trasferimento contenuti) su un’istanza di pubblicazione
exl-id: 01faab94-a939-4004-b094-e9eb8f67b96e
feature: Migration
role: Admin
source-git-commit: 4408f15ef85d0fc2c6a0e2b45038dc900d212187
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 11%

---

# Esecuzione dello strumento Content Transfer (Trasferimento contenuti) su un’istanza di pubblicazione {#run-content-transfer-tool-publish-instance}

## Introduzione {#introduction}

Lo strumento Content Transfer (CTT) non esegue alcun tipo di analisi del contenuto prima di trasferirlo dall’istanza sorgente all’istanza di destinazione. Ad esempio, CTT non distingue tra contenuto pubblicato e non pubblicato durante l’acquisizione del contenuto in un ambiente Publish. Qualsiasi contenuto specificato nel set di migrazione viene acquisito nell’istanza di destinazione selezionata. Un utente può acquisire un set di migrazione in un’istanza Author, Publish o in entrambe.

>[!NOTE]
>Durante lo spostamento del contenuto in un’istanza di produzione, si consiglia di installare lo strumento Content Transfer (Trasferimento contenuti) nell’istanza di authoring di origine per spostare il contenuto nell’istanza di authoring di destinazione e, analogamente, di installare lo strumento Content Transfer (Trasferimento contenuti) nell’istanza di Publish di origine per spostare il contenuto nell’istanza di Publish di destinazione. Per ulteriori dettagli, consulta la sezione [Approccio consigliato](#recommended-approach) di seguito.

## Approccio consigliato {#recommended-approach}

Segui l’approccio raccomandato come descritto di seguito:

* Utilizza la stessa versione dello strumento Content Transfer (Trasferimento contenuti) utilizzata nell’istanza di authoring.

* È necessario eseguire la migrazione di un solo nodo di pubblicazione. Deve essere rimosso dal load balancer prima di iniziare l’estrazione.

* Durante l’acquisizione per la pubblicazione, il livello di pubblicazione non verrà ridotto (a differenza dell’authoring).

  >[!IMPORTANT]
  >Come precauzione, evita le operazioni di scrittura avviate dall&#39;utente, ad esempio:
  > * Distribuzione dei contenuti da AEM as a Cloud Service Author a Publish in tale ambiente
  > * Sincronizzazione utenti tra istanze di pubblicazione
