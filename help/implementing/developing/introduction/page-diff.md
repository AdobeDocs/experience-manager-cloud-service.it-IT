---
title: Sviluppo e differenze tra pagine
description: Scopri come funziona la funzione Page Diff e come può influire su uno sviluppatore
exl-id: 03c08616-2203-4b90-bed6-4836266e2507
source-git-commit: 7260649eaab303ba5bab55ccbe02395dc8159949
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 6%

---

# Sviluppo e differenze tra pagine {#developing-and-page-diff}

## Panoramica delle funzioni {#feature-overview}

La creazione dei contenuti è un processo iterativo. Per un authoring efficace, è necessario essere in grado di vedere cosa è cambiato da un’iterazione all’altro. Visualizzare una versione di pagina e l’altra è inefficiente e soggetto a errori. L’autore vuole poter confrontare la pagina corrente con una versione precedente, evidenziando le differenze.

La differenza di pagina consente a un utente di confrontare la pagina corrente con lanci, versioni precedenti e così via. Per informazioni dettagliate su questa funzione utente, consulta [Differenza di pagina](/help/sites-cloud/authoring/features/page-diff.md).

## Dettagli operazione {#operation-details}

Quando si confrontano le versioni di una pagina, la versione precedente che l’utente desidera confrontare viene ricreata dall’AEM in background per facilitare la differenze. Questa versione precedente è necessaria per eseguire il rendering del contenuto [per il confronto affiancato](/help/sites-cloud/authoring/features/page-diff.md).

Questa operazione di ricreazione viene eseguita internamente dall&#39;AEM, è trasparente per l&#39;utente e non richiede alcun intervento. Tuttavia, un amministratore che visualizza l’archivio, ad esempio in CRXDE Lite, vedrebbe queste versioni ricreate all’interno della struttura del contenuto.

Quando si confronta il contenuto, l’intera struttura fino alla pagina da confrontare viene ricreata nella seguente posizione:

`/tmp/versionhistory/`

Un’attività di pulizia viene eseguita automaticamente per pulire questo contenuto temporaneo.

## Limitazioni {#limitations}

La differenza si verifica lato client tramite il confronto DOM, rendendo il processo di differenza semplice. Tuttavia, lo sviluppatore deve considerare diverse limitazioni.

* Questa funzione utilizza classi CSS che non fanno parte del namespace del prodotto AEM. Se nella pagina sono incluse altre classi CSS personalizzate o classi CSS di terze parti con gli stessi nomi, la visualizzazione delle differenze potrebbe esserne influenzata.

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* Poiché la differenza è lato client ed è in esecuzione al caricamento della pagina, eventuali modifiche apportate al DOM dopo l’esecuzione del servizio differenze lato client non vengono contabilizzate. Questo processo può influire sui seguenti elementi:

   * Componenti che utilizzano l’AJAX per includere i contenuti
   * Applicazioni a pagina singola
   * Componenti basati su JavaScript che manipolano il DOM in seguito all’interazione dell’utente.
