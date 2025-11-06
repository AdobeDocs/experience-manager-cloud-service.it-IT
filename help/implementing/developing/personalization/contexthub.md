---
title: ContextHub
description: ContextHub è un framework per l’archiviazione, la manipolazione e la presentazione dei dati contestuali
exl-id: 604477c6-d96a-441f-b5fc-5def93832478
feature: Developing, Personalization
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 1%

---

# ContextHub {#contexthub}

ContextHub è un framework per l’archiviazione, la manipolazione e la presentazione dei dati contestuali. La funzionalità principale offre la possibilità di [visualizzare i dati contestuali durante la simulazione e il passaggio tra vari utenti tipo](/help/sites-cloud/authoring/personalization/contexthub.md).

ContextHub consente di:

* [Presenta, visualizza, cambia utente e simula l&#39;esperienza utente](#presentation) durante la creazione di pagine utilizzando dati contestuali.
* [Mantenere i dati contestuali](#persistence) sul sito Web come rappresentazione del livello dati.
* [Gestisci segmenti](#segmentation) per il contesto selezionato.

L’API JavaScript lato client ti consente di accedere ai dati per personalizzare il contenuto.

## Presentazione {#presentation}

La barra degli strumenti [ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md) consente agli addetti al marketing e agli autori di visualizzare e manipolare i dati dell&#39;archivio per simulare l&#39;esperienza utente durante la creazione delle pagine. La barra degli strumenti è costituita da gruppi di moduli di interfaccia utente che forniscono l&#39;accesso agli [archivi ContextHub](#persistence), che rendono persistenti i dati ContextHub sul client.

Ogni modulo dell’interfaccia utente ContextHub è un’istanza di un tipo di modulo predefinito:

* ContextHub fornisce diversi [tipi di moduli di esempio](sample-modules.md).
* Usa le console di AEM per [aggiungere moduli di interfaccia utente](configuring-contexthub.md#adding-a-ui-module) e per [raggrupparli in modalità interfaccia utente](configuring-contexthub.md#adding-a-ui-mode).
* Gli sviluppatori possono [creare tipi di moduli personalizzati](extending-contexthub.md#creating-contexthub-ui-module-types).

Gli sviluppatori devono [aggiungere il componente ContextHub alla pagina](configuring-contexthub.md).

## Persistenza {#persistence}

ContextHub archivia i dati contestuali persistenti sul client. L’API JavaScript di ContextHub consente di accedere agli store per creare, aggiornare ed eliminare i dati in base alle esigenze. ContextHub rappresenta un livello dati sulle pagine.

Ogni archivio ContextHub è un’istanza di un tipo di archivio predefinito:

* ContextHub fornisce diversi [tipi di archivio di esempio](sample-stores.md).
* Usa le console AEM per [creare store](configuring-contexthub.md#creating-a-contexthub-store).
* Gli sviluppatori possono [creare tipi di archivio personalizzati](extending-contexthub.md#creating-custom-store-candidates).
* Gli sviluppatori possono [accedere ai dati dell&#39;archivio](adding-contexthub.md#interacting-with-contexthub-stores) tramite JavaScript.

## Segmentazione {#segmentation}

ContextHub include un motore di segmentazione che gestisce i segmenti e determina quali segmenti vengono risolti per il contesto corrente. Sono definiti diversi segmenti. Puoi usare l&#39;API JavaScript per [determinare i segmenti risolti](adding-contexthub.md#determining-resolved-contexthub-segments).
