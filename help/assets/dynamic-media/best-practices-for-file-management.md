---
title: Best practice per organizzare le risorse digitali per l’utilizzo dei profili immagine o video di Dynamic Media
description: '"Suggerimenti e best practice per la denominazione, l’organizzazione e la gestione dei file di immagini e delle risorse video di Dynamic Media."'
contentOwner: Rick Brough
feature: Asset Management,Image Profiles,Video Profiles
topic: Business Practitioner
role: Administrator,Business Practitioner
exl-id: 82ab5432-088c-4442-a9db-9f4e0184febf
translation-type: tm+mt
source-git-commit: 6b232ab512a6faaf075faa55c238dfb10c00b100
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# Best practice per organizzare le risorse digitali per l’utilizzo dei profili immagine o video{#best-practices-for-organizing-your-digital-assets-for-using-profiles}

Un concetto importante per l&#39;utilizzo dei profili immagine o video di Dynamic Media è che vengono assegnati alle cartelle. All’interno di un profilo sono riportate le impostazioni per un’immagine o un video. Queste impostazioni elaborano il contenuto di una cartella insieme a una delle relative sottocartelle. Pertanto, il modo in cui denomini file e cartelle, disponi sottocartelle e gestisci i file all’interno di queste cartelle ha un impatto sul modo in cui tali risorse vengono elaborate dal profilo.

Utilizzando strategie di denominazione dei file e delle cartelle coerenti e appropriate, insieme a buone pratiche in materia di metadati, puoi sfruttare al massimo la tua raccolta di risorse digitali e garantire che i file giusti vengano elaborati dal profilo giusto.

Consulta [Informazioni sul profilo immagine e sui profili video di Dynamic Media](about-image-video-profiles.md).

Di seguito sono riportati alcuni suggerimenti sulle best practice per organizzare i file di risorse digitali.

* Organizza i file in base ai metadati aggiunti al loro interno anziché alle cartelle in cui risiedono. Puoi seguire questa procedura aggiungendo profili di metadati.

   * Consulta [Profili metadati](/help/assets/metadata-profiles.md).
   * Consulta [Metadati per Digital Asset Management](/help/assets/manage-metadata.md).

* Di solito, la tua raccolta di risorse digitali cresce sempre di più. Pertanto, è importante, in precedenza, formalizzare l’uso dei metadati, la struttura delle cartelle e la denominazione dei file tra tutte le risorse caricate. La standardizzazione su questi elementi assicura che, con l’aumento del pool di risorse digitali, sia possibile applicare profili di elaborazione alle cartelle con maggiore precisione e coerenza.
* Utilizza solo le cartelle per imporre una struttura di archiviazione coerente per le risorse digitali. Ad esempio, le strutture di cartelle che consentono di definire meglio i profili da assegnare possono includere i seguenti elementi:

   * **Cartelle di sviluppo** : contiene le risorse digitali su cui stai lavorando.
   * **Cartelle client** : contiene risorse digitali basate su client o nomi di progetto.
   * **Cartelle sorgente principali**  - contiene risorse digitali originali di origine.
   * **Cartelle di rappresentazione**  - contiene rappresentazioni e copie delle risorse digitali originali di origine.
   * **Cartelle di dimensioni file** : contiene risorse digitali basate su file di piccole, medie o grandi dimensioni.
   * **Cartelle di staging** : contiene risorse digitali pronte per la pubblicazione live sul sito web.
   * **Cartelle di tipo MIME** : contiene risorse digitali specifiche per i tipi MIME quali immagini, documenti e elementi multimediali.
   * **Archivia cartelle**  - contiene risorse digitali in pensione.
   * **Cartelle basate su data** : contiene risorse digitali in base a una data di creazione o a un’ultima data di modifica.

* Crea una directory di cartelle che probabilmente non verrà modificata in modo che i profili assegnati non si interrompano.
* Supponiamo che una risorsa sia già stata pubblicata e quindi utilizzi Adobe Experience Manager per spostare la risorsa in un’altra cartella e ripubblicarla dalla nuova posizione. La posizione originale della risorsa pubblicata è ancora disponibile, insieme alla nuova risorsa ripubblicata. La risorsa pubblicata originale, tuttavia, è &quot;persa&quot; in Experience Manager e non può essere annullata. Pertanto, come best practice, annulla la pubblicazione delle risorse prima di spostarle in un’altra cartella.
