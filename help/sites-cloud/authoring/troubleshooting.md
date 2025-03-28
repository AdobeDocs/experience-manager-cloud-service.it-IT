---
title: Risoluzione di problemi AEM nell’ambiente di authoring
description: Alcuni problemi che potresti riscontrare durante l’utilizzo dell’AEM
exl-id: b9c0584d-255e-486d-b829-09e07499ecd2
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 72%

---

# Risoluzione di problemi AEM nell’ambiente di authoring  {#troubleshooting-aem-when-authoring}

Nella seguente sezione vengono descritti alcuni problemi che potresti riscontrare durante l’utilizzo di AEM e vengono proposte possibili soluzioni.

## La vecchia versione della pagina è ancora nel sito pubblicato {#old-page-version-still-on-published-site}

* **Problema**:
   * Hai apportato delle modifiche a una pagina e l’hai replicata sul sito pubblicato, ma nel sito pubblicato viene ancora visualizzata la *vecchia* versione della pagina.
* **Motivo**:
   * Questo può avere diverse cause, il più delle volte la cache (sia nel browser locale che in Dispatcher), anche se a volte può essere un problema con la coda di replica.
* **Soluzioni**:
   * Esistono varie possibilità:
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
   * In rari casi, un’azione precedente potrebbe influire sulla barra degli strumenti.
* **Soluzione**:
   * Aggiorna la pagina.
