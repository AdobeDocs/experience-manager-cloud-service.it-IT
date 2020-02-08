---
title: Risoluzione di problemi AEM nell’ambiente di creazione
description: Alcuni problemi che potrebbero verificarsi durante l’utilizzo di AEM
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Risoluzione di problemi AEM nell’ambiente di creazione {#troubleshooting-aem-when-authoring}

Nella seguente sezione vengono descritti alcuni problemi che potresti riscontrare durante l’utilizzo di AEM e vengono proposte possibili soluzioni.

## La vecchia versione della pagina è ancora nel sito pubblicato {#old-page-version-still-on-published-site}

* **Problema**:
   * You have made changes to a page and published the page to the publish site, but the *old* version of the page is still being shown on the publish site.
* **Motivo**:
   * Questo può dipendere da diverse cause. In genere si tratta di un problema di cache (del browser locale o del Dispatcher), ma a volte può dipendere da un problema relativo alla coda di replica.
* **Soluzioni**:
   * Esistono diverse possibilità:
   * Verifica che la pagina sia stata replicata correttamente. Controllate lo stato della pagina e, se necessario, lo stato della coda di replica.
   * Cancella la cache del browser locale e accedi di nuovo alla pagina.
   * Add `?` to the end of the page URL. For example:
      * `http://<host>:<port>/sites.html/content?`
      * Questo fa sì che la pagina venga richiesta direttamente da AEM senza passare dal Dispatcher. Se viene visualizzata la pagina aggiornata, significa che è necessario cancellare la cache del Dispatcher.
   * In caso di problemi relativi alla coda di replica, rivolgetevi al vostro amministratore di sistema.

## Azioni per componenti non visibili sulla barra degli strumenti {#component-actions-not-visible-on-toolbar}

* **Problema**:
   * Non tutte le azioni disponibili per i componenti sono visibili quando si modifica il contenuto di una pagina nell’ambiente di creazione.
* **Motivo**:
   * In rari casi, un’azione precedente potrebbe pregiudicare il funzionamento della barra degli strumenti.
* **Soluzione**:
   * Aggiorna la pagina.
