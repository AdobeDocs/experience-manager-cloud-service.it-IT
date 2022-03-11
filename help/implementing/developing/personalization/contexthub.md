---
title: ContextHub
description: ContextHub è un framework per la memorizzazione, la manipolazione e la presentazione dei dati contestuali
exl-id: 604477c6-d96a-441f-b5fc-5def93832478
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 1%

---

# ContextHub {#contexthub}

ContextHub è un framework per la memorizzazione, la manipolazione e la presentazione dei dati contestuali. La caratteristica principale è l&#39;offerta di [visualizzare i dati contestuali durante la simulazione e il passaggio tra vari utenti tipo.](/help/sites-cloud/authoring/personalization/contexthub.md)

ContextHub che consente di:

* [Presentare, visualizzare, cambiare personale e simulare l’esperienza utente](#presentation) durante la creazione di pagine utilizzando i dati contestuali.
* [Persistere i dati contestuali](#persistence) nel sito web come rappresentazione a livello di dati.
* [Gestire i segmenti](#segmentation) per il contesto selezionato.

L’API JavaScript lato client consente di accedere ai dati per la personalizzazione del contenuto.

## Presentazione {#presentation}

La [Barra degli strumenti di ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md) consente agli esperti di marketing e agli autori di visualizzare e manipolare i dati dell’archivio per simulare l’esperienza utente durante l’authoring delle pagine. La barra degli strumenti è costituita da gruppi di moduli di interfaccia utente che forniscono accesso a [archivi ContextHub,](#persistence) che persistono i dati ContextHub sul client.

Ciascun modulo dell’interfaccia utente di ContextHub è un’istanza di un tipo di modulo predefinito:

* ContextHub fornisce diversi [tipi di moduli di esempio](sample-modules.md).
* Utilizzare le console AEM per [aggiungere moduli di interfaccia utente](configuring-contexthub.md#adding-a-ui-module)e a [raggrupparli in modalità interfaccia utente](configuring-contexthub.md#adding-a-ui-mode).
* Gli sviluppatori possono [creare tipi di moduli personalizzati](extending-contexthub.md#creating-contexthub-ui-module-types).

Gli sviluppatori devono [aggiungi il componente ContextHub alla pagina](configuring-contexthub.md).

## Persistenza {#persistence}

ContextHub memorizza i dati contestuali persistenti sul client. L’API Javascript di ContextHub consente di accedere agli archivi per creare, aggiornare ed eliminare i dati in base alle necessità. ContextHub rappresenta un livello di dati sulle pagine.

Ogni archivio ContextHub è un&#39;istanza di un tipo di archivio predefinito:

* ContextHub fornisce diversi [tipi di archivio di esempio](sample-stores.md).
* Utilizzare le console AEM per [creare negozi](configuring-contexthub.md#creating-a-contexthub-store).
* Gli sviluppatori possono [creare tipi di archivio personalizzati](extending-contexthub.md#creating-custom-store-candidates).
* Gli sviluppatori possono [accesso ai dati dell&#39;archivio](adding-contexthub.md#interacting-with-contexthub-stores) via Javascript.

## Segmentazione {#segmentation}

ContextHub include un motore di segmentazione che gestisce i segmenti e determina quali segmenti vengono risolti per il contesto corrente. Sono definiti diversi segmenti. Puoi utilizzare l’API JavaScript per [determinare i segmenti risolti](adding-contexthub.md#determining-resolved-contexthub-segments).
