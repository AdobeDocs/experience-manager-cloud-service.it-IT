---
title: ContextHub
description: ContextHub è un framework per la memorizzazione, la manipolazione e la presentazione dei dati contestuali
translation-type: tm+mt
source-git-commit: b8bc27b51eefcfcfa1c23407a4ac0e7ff068081e
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 1%

---


# ContextHub {#contexthub}

ContextHub è un framework per la memorizzazione, la manipolazione e la presentazione dei dati contestuali. La sua funzione principale consiste nell&#39;offrire la possibilità di [visualizzare i dati contestuali durante la simulazione e il passaggio tra diverse persone.](/help/sites-cloud/authoring/personalization/contexthub.md)

ContextHub che consente di:

* [Presenta, visualizza, cambia personale e simula l’esperienza](#presentation) dell’utente durante la creazione di pagine tramite dati contestuali.
* [Mantenere i dati](#persistence) contestuali sul sito Web come rappresentazione del livello di dati.
* [Gestisci i segmenti](#segmentation) per il contesto selezionato.

L&#39;API Javascript lato client consente di accedere ai dati per la personalizzazione del contenuto.

## Presentazione {#presentation}

La barra degli strumenti [](/help/sites-cloud/authoring/personalization/contexthub.md) ContextHub consente agli esperti di marketing e agli autori di visualizzare e manipolare i dati dell&#39;archivio per simulare l&#39;esperienza utente durante l&#39;authoring delle pagine. La barra degli strumenti è composta da gruppi di moduli dell&#39;interfaccia utente che forniscono l&#39;accesso agli store [ContextHub,](#persistence) che persistono i dati ContextHub sul client.

Ciascun modulo dell’interfaccia utente ContextHub è un’istanza di tipo di modulo predefinito:

* ContextHub offre diversi tipi [di moduli di](sample-modules.md)esempio.
* Utilizzate AEM console per [aggiungere moduli](configuring-contexthub.md#adding-a-ui-module)dell&#39;interfaccia utente e per [raggrupparli in modalità](configuring-contexthub.md#adding-a-ui-mode)di interfaccia.
* Gli sviluppatori possono [creare tipi](extending-contexthub.md#creating-contexthub-ui-module-types)di moduli personalizzati.

Gli sviluppatori devono [aggiungere il componente ContextHub alla pagina](configuring-contexthub.md).

## Persistenza {#persistence}

ContextHub memorizza i dati contestuali persistenti sul client. L&#39;API ContextHub Javascript consente di accedere agli store per creare, aggiornare ed eliminare i dati secondo necessità. ContextHub rappresenta pertanto un livello dati sulle pagine.

Ciascun archivio ContextHub è un&#39;istanza di un tipo di store predefinito:

* ContextHub fornisce diversi tipi [di archivio di](sample-stores.md)esempio.
* Utilizzate AEM console per [creare store](configuring-contexthub.md#creating-a-contexthub-store).
* Gli sviluppatori possono [creare tipi](extending-contexthub.md#creating-custom-store-candidates)di store personalizzati.
* Gli sviluppatori possono [accedere ai dati](adding-contexthub.md#interacting-with-contexthub-stores) dell&#39;archivio tramite Javascript.

## Segmentazione {#segmentation}

ContextHub include un motore di segmentazione che gestisce i segmenti e determina quali segmenti vengono risolti per il contesto corrente. Sono definiti diversi segmenti. Puoi utilizzare l&#39;API Javascript per [determinare i segmenti](adding-contexthub.md#determining-resolved-contexthub-segments)risolti.
