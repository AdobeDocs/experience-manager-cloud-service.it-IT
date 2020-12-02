---
title: Procedure ottimali per l’organizzazione delle risorse digitali per l’utilizzo di profili immagine o video per file multimediali dinamici
description: Suggerimenti e procedure ottimali per la denominazione, l’organizzazione e la gestione di file di immagini e risorse video per file multimediali dinamici.
translation-type: tm+mt
source-git-commit: 68cf71054b1cd7dfb2790122ba4c29854ffdf703
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---


# Procedure ottimali per l’organizzazione delle risorse digitali per l’utilizzo dei profili immagine o video{#best-practices-for-organizing-your-digital-assets-for-using-profiles}

Un concetto importante per l’utilizzo dei profili immagine per file multimediali dinamici o dei profili video è che vengono assegnati alle cartelle. All’interno di un profilo sono disponibili le impostazioni per un’immagine o un video. Queste impostazioni elaborano il contenuto di una cartella insieme a una delle relative sottocartelle. Di conseguenza, il modo in cui denominate file e cartelle, come vengono disposte le sottocartelle e come vengono gestiti i file all’interno di tali cartelle ha un impatto significativo sul modo in cui tali risorse vengono elaborate dal profilo.

Utilizzando strategie di denominazione di file e cartelle coerenti e appropriate, oltre a buone pratiche in materia di metadati, potete sfruttare al meglio la raccolta di risorse digitali e assicurarvi che i file corretti vengano elaborati dal profilo corretto.

Consultate [Il profilo immagine multimediale dinamico e i profili video](about-image-video-profiles.md).

Di seguito sono riportati consigli per l’organizzazione dei file di risorse digitali.

* Organizzate i file in base ai metadati aggiunti al posto delle cartelle in cui risiedono. A questo scopo potete aggiungere profili di metadati.

   * Vedere [Profili metadati.](/help/assets/metadata-profiles.md)
   * Consultate [Metadati per Digital Asset Management](/help/assets/manage-metadata.md).

* Nella maggior parte dei casi, la raccolta di risorse digitali è in continuo aumento. Pertanto, è importante (in precedenza) formalizzare l’uso dei metadati, la struttura delle cartelle e la denominazione dei file tra tutte le risorse caricate. La standardizzazione di questi elementi assicura che, con l&#39;aumento del numero di risorse digitali, sia possibile applicare profili di elaborazione alle cartelle con maggiore precisione e coerenza.
* Utilizzate le cartelle solo per imporre una struttura di memorizzazione coerente alle risorse digitali. Ad esempio, le strutture di cartelle che consentono di definire meglio i profili da assegnare possono includere quanto segue:

   * **Cartelle**  di sviluppo - contiene le risorse digitali su cui state lavorando.
   * **Cartelle**  client: contiene risorse digitali basate su client o nomi di progetti.
   * **Cartelle**  sorgente principali - contiene le risorse digitali sorgente originali.
   * **Cartelle**  di rappresentazione - contiene rappresentazioni e copie delle risorse digitali originali.
   * **Cartelle**  Dimensione file: contiene risorse digitali basate su file di piccole, medie o grandi dimensioni.
   * **Cartelle**  di gestione temporanea contiene risorse digitali pronte per la pubblicazione sul sito Web.
   * **Cartelle**  di tipo mime: contiene risorse digitali specifiche per i tipi mime, ad esempio immagini, documenti e contenuti multimediali.
   * **Archivia cartelle**  - contiene le risorse digitali ritirate.
   * **Cartelle**  basate su data: contiene risorse digitali basate su una data di creazione o l’ultima data di modifica.

* Create una directory di cartelle che probabilmente non verrà modificata in modo che i profili assegnati non vengano interrotti.
* Se una risorsa è già pubblicata, usate AEM per spostare la risorsa in un’altra cartella e ripubblicarla dalla nuova posizione, il percorso originale della risorsa pubblicata è ancora disponibile, insieme alla nuova risorsa pubblicata. La risorsa pubblicata originale, tuttavia, è &quot;perduta&quot; in AEM e non può essere annullata la pubblicazione. Di conseguenza, è consigliabile annullare la pubblicazione delle risorse prima di spostarle in un’altra cartella.

