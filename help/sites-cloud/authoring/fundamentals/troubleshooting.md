---
title: Risoluzione di problemi AEM nell’ambiente di authoring
description: Alcuni problemi che potrebbero verificarsi durante l’utilizzo di AEM
exl-id: b9c0584d-255e-486d-b829-09e07499ecd2
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: ht
source-wordcount: '235'
ht-degree: 100%

---

# Risoluzione di problemi AEM nell’ambiente di authoring  {#troubleshooting-aem-when-authoring}

Nella seguente sezione vengono descritti alcuni problemi che potresti riscontrare durante l’utilizzo di AEM e vengono proposte possibili soluzioni.

## La vecchia versione della pagina è ancora nel sito pubblicato {#old-page-version-still-on-published-site}

* **Problema**:
   * Hai apportato delle modifiche a una pagina e l’hai replicata sul sito pubblicato, ma nel sito pubblicato viene ancora visualizzata la *vecchia* versione della pagina.
* **Motivo**:
   * Questo può dipendere da diverse cause. In genere si tratta di un problema di cache (del browser locale o del Dispatcher), ma a volte può dipendere da un problema relativo alla coda di replica.
* **Soluzioni**:
   * Esistono diverse possibilità:
   * Verifica che la pagina sia stata replicata correttamente. Controlla lo stato della pagina e, se necessario, lo stato della coda di replica.
   * Cancella la cache del browser locale e accedi di nuovo alla pagina.
   * Aggiungi `?` alla fine dell’URL della pagina, ad esempio:
      * `http://<host>:<port>/sites.html/content?`
      * In questo modo la pagina viene richiesta direttamente da AEM senza passare dal Dispatcher. Se viene visualizzata la pagina aggiornata, significa che è necessario cancellare la cache del Dispatcher.
   * In caso di problemi relativi alla coda di replica, rivolgiti all’amministratore di sistema.

## Azioni per componenti non visibili sulla barra degli strumenti {#component-actions-not-visible-on-toolbar}

* **Problema**:
   * Non tutte le azioni disponibili per i componenti sono visibili quando si modifica il contenuto di una pagina nell’ambiente di authoring.
* **Motivo**:
   * In rari casi, un’azione precedente potrebbe pregiudicare il funzionamento della barra degli strumenti.
* **Soluzione**:
   * Aggiorna la pagina.
