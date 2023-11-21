---
title: ContextHub
description: ContextHub è un framework per l’archiviazione, la manipolazione e la presentazione dei dati contestuali
exl-id: 604477c6-d96a-441f-b5fc-5def93832478
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 1%

---

# ContextHub {#contexthub}

ContextHub è un framework per l’archiviazione, la manipolazione e la presentazione dei dati contestuali. La sua funzione principale è offrire la possibilità di [visualizzare i dati contestuali durante la simulazione e il passaggio tra diversi utenti tipo](/help/sites-cloud/authoring/personalization/contexthub.md).

ContextHub consente di:

* [Presentare, visualizzare, cambiare persona e simulare l’esperienza utente](#presentation) durante l’authoring di pagine utilizzando dati contestuali.
* [Mantenere i dati contestuali](#persistence) sul sito web come rappresentazione del livello dati.
* [Gestire i segmenti](#segmentation) per il contesto selezionato.

L’API JavaScript lato client ti consente di accedere ai dati per personalizzare il contenuto.

## Presentazione {#presentation}

Il [Barra degli strumenti di ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md) consente agli addetti al marketing e agli autori di visualizzare e manipolare i dati dell’archivio per simulare l’esperienza utente durante l’authoring delle pagine. La barra degli strumenti è costituita da gruppi di moduli di interfaccia utente che forniscono accesso a [Archivi ContextHub,](#persistence) che rendono persistenti i dati ContextHub sul client.

Ogni modulo dell’interfaccia utente ContextHub è un’istanza di un tipo di modulo predefinito:

* ContextHub fornisce diversi [tipi di moduli di esempio](sample-modules.md).
* Utilizzare le console AEM per [aggiungere moduli di interfaccia utente](configuring-contexthub.md#adding-a-ui-module), e a [raggrupparli in modalità interfaccia utente](configuring-contexthub.md#adding-a-ui-mode).
* Gli sviluppatori possono [creare tipi di moduli personalizzati](extending-contexthub.md#creating-contexthub-ui-module-types).

Gli sviluppatori devono: [aggiungere il componente ContextHub alla pagina](configuring-contexthub.md).

## Persistenza {#persistence}

ContextHub archivia i dati contestuali persistenti sul client. L’API JavaScript di ContextHub consente di accedere agli store per creare, aggiornare ed eliminare i dati in base alle esigenze. ContextHub rappresenta un livello dati sulle pagine.

Ogni archivio ContextHub è un’istanza di un tipo di archivio predefinito:

* ContextHub fornisce diversi [tipi di archivio di esempio](sample-stores.md).
* Utilizzare le console AEM per [crea store](configuring-contexthub.md#creating-a-contexthub-store).
* Gli sviluppatori possono [creare tipi di store personalizzati](extending-contexthub.md#creating-custom-store-candidates).
* Gli sviluppatori possono [accedere ai dati dell’archivio](adding-contexthub.md#interacting-with-contexthub-stores) tramite JavaScript.

## Segmentazione {#segmentation}

ContextHub include un motore di segmentazione che gestisce i segmenti e determina quali segmenti vengono risolti per il contesto corrente. Sono definiti diversi segmenti. È possibile utilizzare l’API JavaScript per: [determinare i segmenti risolti](adding-contexthub.md#determining-resolved-contexthub-segments).
