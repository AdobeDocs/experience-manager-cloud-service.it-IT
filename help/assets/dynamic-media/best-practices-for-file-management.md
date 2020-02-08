---
title: Best practice per l’organizzazione delle risorse digitali per l’utilizzo dei profili
description: Suggerimenti e procedure ottimali per denominare, organizzare e gestire i metadati per i file di risorse digitali.
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# Procedure ottimali per l’organizzazione delle risorse digitali per l’utilizzo dei profili {#best-practices-for-organizing-your-digital-assets-for-using-profiles}

Un concetto importante per l’utilizzo dei profili in Risorse AEM è che vengono assegnati alle cartelle. All’interno di un profilo sono disponibili impostazioni sotto forma di profili di metadati, nonché profili video o profili immagine. Queste impostazioni elaborano il contenuto di una cartella insieme a una delle sottocartelle. Di conseguenza, il modo in cui denominate file e cartelle, le modalità di disposizione delle sottocartelle e la gestione dei file all’interno di tali cartelle hanno un impatto significativo sul modo in cui tali risorse vengono elaborate da un profilo.

Utilizzando strategie di denominazione di file e cartelle coerenti e appropriate, oltre a buone pratiche in materia di metadati, potete sfruttare al meglio la raccolta di risorse digitali e assicurarvi che i file corretti vengano elaborati dal profilo corretto.

Consultate [Profili per elaborazione di video, metadati e immagini](processing-profiles.md).

Di seguito sono riportati consigli per organizzare i file di risorse digitali.

* Organizzate i file in base ai metadati aggiunti al posto delle cartelle in cui risiedono. A questo scopo potete aggiungere profili di metadati.

   * Consultate Profili [metadati.](/help/assets/metadata-profiles.md)
   * Consultate [Metadati per la gestione](/help/assets/manage-metadata.md)delle risorse digitali.

* Nella maggior parte dei casi, la raccolta di risorse digitali è in continuo aumento. Pertanto, è importante (in precedenza) formalizzare l’uso dei metadati, la struttura delle cartelle e la denominazione dei file tra tutte le risorse caricate. La standardizzazione di questi elementi assicura che, con l&#39;aumento del numero di risorse digitali, sia possibile applicare profili di elaborazione alle cartelle con maggiore precisione e coerenza.
* Utilizzate le cartelle solo per imporre una struttura di memorizzazione coerente alle risorse digitali. Ad esempio, le strutture di cartelle che consentono di definire meglio i profili da assegnare possono includere:

   * **Cartelle** di sviluppo - contiene le risorse digitali su cui state lavorando.
   * **Cartelle** client: contiene risorse digitali basate sui nomi dei client o dei progetti.
   * **Cartelle** master - contiene risorse digitali originali.
   * **Cartelle** di rappresentazione - contiene rappresentazioni e copie delle risorse digitali originali.
   * **Cartelle** Dimensione file: contiene risorse digitali basate su file di piccole, medie o grandi dimensioni.
   * **Cartelle** di gestione temporanea: contiene risorse digitali pronte per la pubblicazione sul sito Web.
   * **Cartelle** di tipo mime: contiene risorse digitali specifiche per i tipi di mime quali immagini, documenti e contenuti multimediali.
   * **Archivia cartelle** - contiene le risorse digitali ritirate.
   * **Cartelle** basate su data: contiene risorse digitali basate su una data di creazione o un’ultima modifica.

* Create una directory di cartelle che probabilmente non verrà modificata in modo che i profili assegnati non vengano interrotti.
* Se una risorsa è già pubblicata, utilizzate AEM per spostare la risorsa in un’altra cartella e ripubblicatela dalla nuova posizione, il percorso originale della risorsa pubblicata è ancora disponibile, insieme alla nuova risorsa pubblicata. La risorsa pubblicata originale, tuttavia, è &quot;persa&quot; in AEM e non può essere annullata la pubblicazione. Di conseguenza, è consigliabile annullare la pubblicazione delle risorse prima di spostarle in un’altra cartella.

