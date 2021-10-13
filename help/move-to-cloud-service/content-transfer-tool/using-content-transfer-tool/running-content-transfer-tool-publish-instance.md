---
title: Esecuzione dello strumento Content Transfer (Trasferimento contenuti) su un’istanza di pubblicazione
description: Esecuzione dello strumento Content Transfer (Trasferimento contenuti) su un’istanza di pubblicazione
source-git-commit: 27e68cd282414da4cc23c3ba276b0fb3c330d49c
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 1%

---


# Esecuzione dello strumento Content Transfer (Trasferimento contenuti) su un’istanza di pubblicazione {#run-content-transfer-tool-publish-instance}

## Introduzione {#introduction}

Lo strumento Content Transfer (CTT) non esegue alcun tipo di analisi del contenuto prima di trasferire il contenuto dall’istanza sorgente all’istanza di destinazione. Ad esempio, CTT non distingue tra contenuto pubblicato e non pubblicato durante l’acquisizione di contenuto in un ambiente di pubblicazione. Qualsiasi contenuto sia specificato nel set di migrazione verrà acquisito nell’istanza di destinazione selezionata. L’utente può acquisire un set di migrazione in un’istanza Author o Publish o in entrambe. Si consiglia di installare CTT durante lo spostamento del contenuto in un’istanza Production nell’istanza Author di origine per spostare il contenuto nell’istanza Author di destinazione e, allo stesso modo, di installare CTT nell’istanza Publish di origine per spostare il contenuto nell’istanza Publish di destinazione.

>[!NOTE]
>Si consiglia di installare lo strumento Content Transfer (Trasferimento contenuti) durante lo spostamento del contenuto in un’istanza Publish nell’istanza Publish di origine per spostare il contenuto nell’istanza Publish di destinazione. Per ulteriori informazioni, consulta la sezione [Approccio consigliato](#recommended-approach) di seguito.

## Approccio consigliato {#recommended-approach}

Segui l’approccio consigliato come descritto di seguito:

* Utilizza la stessa versione del CTT utilizzata nell’istanza di authoring.

* È necessario migrare un solo nodo di pubblicazione. Deve essere rimosso dal load balancer prima di iniziare l’estrazione.

* Quando crei il set di migrazione, utilizza l’URL dell’ambiente AEMaaCS di authoring.

* Durante l’acquisizione per la pubblicazione, il livello di pubblicazione NON viene ridimensionato (a differenza dell’autore). Per precauzione, evitare operazioni di scrittura avviate dall’utente quali:

   * Distribuzione dei contenuti da AEM Author as a Cloud Service a Publish in tale ambiente
   * Sincronizzazione utente tra istanze di pubblicazione
