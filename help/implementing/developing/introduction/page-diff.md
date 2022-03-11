---
title: Sviluppo e differenze tra pagine
description: Scopri come funziona la funzione Differenze tra pagine e come può avere un impatto su uno sviluppatore
exl-id: 03c08616-2203-4b90-bed6-4836266e2507
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 11%

---

# Sviluppo e differenze tra pagine {#developing-and-page-diff}

## Panoramica delle funzioni {#feature-overview}

La creazione di contenuti è un processo iterativo. Per un authoring efficace, è necessario essere in grado di vedere cosa è cambiato da un’iterazione all’altro. La visualizzazione separata di due versioni di una pagina è inefficiente e soggetta a errori. Un autore desidera poter confrontare la pagina corrente con una versione precedente affiancata alle differenze evidenziate.

Le differenze tra pagine consentono a un utente di confrontare la pagina corrente con gli avvii, le versioni precedenti e così via. Per informazioni dettagliate su questa funzione utente, consulta [Differenze tra pagine](/help/sites-cloud/authoring/features/page-diff.md).

## Dettagli operazione {#operation-details}

Quando si confrontano le versioni di una pagina, la versione precedente che l’utente desidera confrontare viene ricreata da AEM in background per facilitare le differenze. È necessario per poter eseguire il rendering del contenuto [per un confronto affiancato](/help/sites-cloud/authoring/features/page-diff.md).

Questa operazione di ricreazione viene eseguita da AEM internamente ed è trasparente per l&#39;utente e non richiede alcun intervento. Tuttavia, un amministratore che visualizza l’archivio, ad esempio in CRX DE Lite, vedrebbe queste versioni ricreati all’interno della struttura del contenuto.

Quando si confronta il contenuto, l’intera struttura fino alla pagina da confrontare viene ricreata nella posizione seguente:

`/tmp/versionhistory/`

Un’attività di pulizia viene eseguita automaticamente per pulire questo contenuto temporaneo.

## Limitazioni  {#limitations}

La differenza si verifica lato client tramite il confronto DOM, rendendo il processo di diff semplice, tuttavia lo sviluppatore deve tenere in considerazione una serie di limitazioni.

* Questa funzione utilizza classi CSS che non hanno nomi separati nel Prodotto AEM. Se nella pagina sono incluse altre classi CSS personalizzate o classi CSS di terze parti con gli stessi nomi, la visualizzazione del confronto potrebbe essere interessata.

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* Poiché la differenza è lato client ed è eseguita al caricamento della pagina, non verranno prese in considerazione eventuali modifiche al DOM dopo l’esecuzione del servizio di diff lato client. Ciò può influire

   * Componenti che utilizzano AJAX per includere i contenuti
   * Applicazioni a pagina singola
   * Componenti basati su JavaScript che manipolano il DOM in base all’interazione dell’utente.
