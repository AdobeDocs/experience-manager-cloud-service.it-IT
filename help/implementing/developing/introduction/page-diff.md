---
title: Sviluppo e Page Diff
description: Come funziona la funzione Page Diff e come può avere un impatto sullo sviluppatore
translation-type: tm+mt
source-git-commit: fee73b5f5ba69422494efe554ac5aa62c046ad86
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 11%

---


# Sviluppo e Page Diff {#developing-and-page-diff}

## Panoramica delle funzioni {#feature-overview}

La creazione di contenuti è un processo iterativo. Per un authoring efficace, è necessario essere in grado di vedere cosa è cambiato da un’iterazione all’altro. La visualizzazione separata di due versioni di una pagina è inefficiente e soggetta a errori. Un autore desidera poter confrontare la pagina corrente con una versione precedente, affiancando le differenze evidenziate.

Le differenze di pagina consentono a un utente di confrontare la pagina corrente con gli avvii, le versioni precedenti e così via. Per informazioni dettagliate su questa funzione utente, consultate [Page Diff](/help/sites-cloud/authoring/features/page-diff.md)(Differenza pagina).

## Dettagli operazione {#operation-details}

Quando si confrontano le versioni di una pagina, la versione precedente che l&#39;utente desidera confrontare viene ricreata AEM in background per facilitare la diff. Questo è necessario per poter eseguire il rendering del contenuto [per il confronto](/help/sites-cloud/authoring/features/page-diff.md)affiancato.

Questa operazione di ricreazione viene eseguita da AEM internamente ed è trasparente per l&#39;utente e non richiede alcun intervento. Tuttavia, un amministratore che visualizza l&#39;archivio, ad esempio in CRX DE Lite, visualizzerà queste versioni ricreato all&#39;interno della struttura del contenuto.

Quando si confronta il contenuto, l&#39;intera struttura fino alla pagina da confrontare viene ricreata nel seguente percorso:

`/tmp/versionhistory/`

Un&#39;attività di pulizia viene eseguita automaticamente per ripulire il contenuto temporaneo.

## Autorizzazioni  {#permissions}

La diff si verifica sul lato client tramite il confronto DOM, rendendo il processo di diff semplice, ma ci sono una serie di limitazioni che devono essere considerate dallo sviluppatore.

* Questa funzione utilizza classi CSS che non hanno un nome con spazio sul prodotto AEM. Se nella pagina sono incluse altre classi CSS personalizzate o classi CSS di terze parti con gli stessi nomi, la visualizzazione della diff potrebbe essere interessata.

   * `html-added`
   * `html-removed`
   * `cq-component-added`
   * `cq-component-removed`
   * `cq-component-moved`
   * `cq-component-changed`

* Poiché la diff è lato client ed è eseguita al caricamento della pagina, eventuali modifiche al DOM dopo l&#39;esecuzione del servizio diff lato client non verranno prese in considerazione. Ciò può incidere

   * Componenti che utilizzano AJAX per includere il contenuto
   * Applicazioni a pagina singola
   * Componenti basati su JavaScript che modificano il DOM in base all’interazione dell’utente.
