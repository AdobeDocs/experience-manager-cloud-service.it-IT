---
title: Utilizzo dei flussi di lavoro
description: I flussi di lavoro in AEM consentono di automatizzare le serie di passaggi che vengono eseguite su una pagina o su una risorsa.
exl-id: ed157646-abb3-45c6-bafd-7889bd93fdf3
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: ht
source-wordcount: '180'
ht-degree: 100%

---

# Utilizzo dei flussi di lavoro {#working-with-workflows}

I flussi di lavoro in AEM consentono di automatizzare le serie di passaggi che vengono eseguite su una (o più) pagine e/o risorse.

Ad esempio, per la pubblicazione, un editor deve rivedere il contenuto prima che l’amministratore del sito attivi la pagina. Un flusso di lavoro che automatizza questo esempio avvisa ogni partecipante quando è il momento di eseguire il lavoro richiesto:

1. L’autore applica il flusso di lavoro alla pagina.
1. L’editor riceve una richiesta di lavoro per esaminare il contenuto della pagina. Al termine, indica che il lavoro richiesto è stato completato.
1. L’amministratore del sito riceve quindi una richiesta di lavoro per l’attivazione della pagina. Al termine, indica che il lavoro richiesto è stato completato.

In genere:

* Gli autori dei contenuti applicano i flussi di lavoro alle pagine e partecipano ai flussi di lavoro.
* I flussi di lavoro utilizzati sono specifici per i processi aziendali dell’organizzazione.

Le pagine seguenti trattano:

* [Applicazione dei flussi di lavoro alle pagine](/help/sites-cloud/authoring/workflows/applying.md)
* [Partecipazione ai flussi di lavoro](/help/sites-cloud/authoring/workflows/participating.md)
