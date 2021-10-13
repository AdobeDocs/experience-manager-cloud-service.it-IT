---
title: Esecuzione dello strumento Content Transfer (Trasferimento contenuti) su un’istanza di pubblicazione
description: Esecuzione dello strumento Content Transfer (Trasferimento contenuti) su un’istanza di pubblicazione
source-git-commit: 65847fc03770fe973c3bfee4a515748f7e487ab6
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 1%

---


# Esecuzione dello strumento Content Transfer (Trasferimento contenuti) su un’istanza di pubblicazione {#run-content-transfer-tool-publish-instance}

## Introduzione {#introduction}

Lo strumento Content Transfer (CTT) non esegue alcun tipo di analisi del contenuto prima di trasferire il contenuto dall’istanza sorgente all’istanza di destinazione. Ad esempio, CTT non distingue tra contenuto pubblicato e non pubblicato durante l’acquisizione di contenuto in un ambiente di pubblicazione. Qualsiasi contenuto sia specificato nel set di migrazione verrà acquisito nell’istanza di destinazione selezionata. L’utente può acquisire un set di migrazione in un’istanza Author o Publish o in entrambe.

>[!NOTE]
>Si consiglia di installare lo strumento Content Transfer (Trasferimento contenuti) durante lo spostamento del contenuto in un’istanza di produzione nell’istanza di authoring di origine per spostare il contenuto nell’istanza di authoring di destinazione e, analogamente, di installare lo strumento Content Transfer (Trasferimento contenuti) nell’istanza di pubblicazione di origine per spostare il contenuto nell’istanza di pubblicazione di destinazione. Per ulteriori informazioni, consulta la sezione [Approccio consigliato](#recommended-approach) di seguito.

## Approccio consigliato {#recommended-approach}

Segui l’approccio consigliato come descritto di seguito:

* Utilizza la stessa versione dello strumento Content Transfer (Trasferimento contenuti) utilizzato nell’istanza di authoring.

* È necessario migrare un solo nodo di pubblicazione. Deve essere rimosso dal load balancer prima di iniziare l’estrazione.

* Quando crei il set di migrazione, utilizza l’URL dell’autore AEM l’ambiente as a Cloud Service.

* Durante l’acquisizione per la pubblicazione, il livello di pubblicazione NON viene ridimensionato (a differenza dell’autore). Per precauzione, evitare operazioni di scrittura avviate dall’utente quali:

   * Distribuzione dei contenuti da AEM Author as a Cloud Service a Publish in tale ambiente
   * Sincronizzazione utente tra istanze di pubblicazione
