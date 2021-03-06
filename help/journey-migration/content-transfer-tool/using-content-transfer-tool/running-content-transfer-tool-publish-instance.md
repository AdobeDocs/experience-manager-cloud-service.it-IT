---
title: Esecuzione dello strumento Content Transfer (Trasferimento contenuti) su un’istanza di pubblicazione
description: Esecuzione dello strumento Content Transfer (Trasferimento contenuti) su un’istanza di pubblicazione
exl-id: 01faab94-a939-4004-b094-e9eb8f67b96e
source-git-commit: 1fb4d0f2a3b3f9a27f5ab1228ec2d419149e0764
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 11%

---

# Esecuzione dello strumento Content Transfer (Trasferimento contenuti) su un’istanza di pubblicazione {#run-content-transfer-tool-publish-instance}

## Introduzione {#introduction}

Lo strumento Content Transfer (CTT) non esegue alcun tipo di analisi del contenuto prima di trasferire il contenuto dall’istanza sorgente all’istanza di destinazione. Ad esempio, CTT non distingue tra contenuto pubblicato e non pubblicato durante l’acquisizione di contenuto in un ambiente di pubblicazione. Qualsiasi contenuto sia specificato nel set di migrazione verrà acquisito nell’istanza di destinazione selezionata. L’utente può acquisire un set di migrazione in un’istanza Author o Publish o in entrambe.

>[!NOTE]
>Si consiglia di installare lo strumento Content Transfer (Trasferimento contenuti) durante lo spostamento del contenuto in un’istanza di produzione nell’istanza di authoring di origine per spostare il contenuto nell’istanza di authoring di destinazione e, analogamente, di installare lo strumento Content Transfer (Trasferimento contenuti) nell’istanza di pubblicazione di origine per spostare il contenuto nell’istanza di pubblicazione di destinazione. Vedi [Approccio consigliato](#recommended-approach) per ulteriori informazioni, consulta la sezione seguente.

## Approccio consigliato {#recommended-approach}

Segui l’approccio consigliato come descritto di seguito:

* Utilizza la stessa versione dello strumento Content Transfer (Trasferimento contenuti) utilizzato nell’istanza di authoring.

* È necessario migrare un solo nodo di pubblicazione. Deve essere rimosso dal load balancer prima di iniziare l’estrazione.

* Durante l’acquisizione per la pubblicazione, il livello di pubblicazione non viene ridimensionato (a differenza dell’autore).

   >[!IMPORTANT]
   >Per precauzione, evitare operazioni di scrittura avviate dall’utente, ad esempio:
   > * Distribuzione dei contenuti da AEM Author as a Cloud Service a Publish in tale ambiente
   > * Sincronizzazione utente tra istanze di pubblicazione

