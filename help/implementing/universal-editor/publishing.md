---
title: Pubblicazione di contenuti con l’editor visivo universale
description: Scopri in che modo l’editor visivo universale pubblica i contenuti e come le tue app possono gestire i contenuti pubblicati.
source-git-commit: 7eeebade0255263a240476bc32f9530574495751
workflow-type: ht
source-wordcount: '367'
ht-degree: 100%

---


# Pubblicazione di contenuti con l’editor visivo universale {#publishing}

Scopri in che modo l’editor visivo universale pubblica i contenuti e come le tue app possono gestire i contenuti pubblicati.

## Somiglianze con AEM {#similarities}

Per gli utenti di AEM, il processo di pubblicazione dei contenuti con l’editor visivo universale funziona come di consueto: alla pubblicazione in AEM, il contenuto viene replicato dal livello di authoring al livello di pubblicazione.

## Differenze {#differences}

Ciò che rende la pubblicazione con l’editorì visivo universale un po’ diversa, non è tanto l’editor stesso, ma piuttosto l’hosting esterno dell’app, reso possibile dall’editor universale.

Quando è ospitata esternamente, è compito della web app assicurare che il contenuto venga caricato dal livello di authoring quando l’app viene aperta dagli autori all’interno dell’editor, e che venga caricato dal livello di pubblicazione quando i visitatori possono accedere all’app.

## Rilevamento del livello nell’app {#detecting}

Per determinare se il livello di authoring o pubblicazione deve essere accessibile, nell’app puoi usare una semplice istruzione condizionale per scegliere l’endpoint di authoring o pubblicazione appropriato al momento di rilevare l’apertura nell’editor.

Un’altra opzione consiste nell’implementare l’app in due ambienti diversi configurati in maniera diversa, in modo che uno recuperi il contenuto dal livello di authoring e un altro lo recuperi dal livello di pubblicazione. Per consentire agli autori di aprire l’URL pubblicato nell’editor universale, è possibile creare un piccolo script per “convertire” l’URL lato pubblicazione al suo equivalente nell’ambiente di authoring (ad esempio, anteponendo un sottodominio `author`), in modo che gli autori vengano reindirizzati automaticamente.

## Riepilogo {#summary}

L’obiettivo dell’editor universale è di non imporre alcun modello particolare, in modo che l’implementazione possa raggiungere al meglio i suoi obiettivi in una modalità completamente separata, assicurando al tempo stesso che tutto risulti semplice e chiaro per l’implementazione.

Allo stesso modo, l’editor universale non detta i requisiti su come un particolare progetto debba determinare da quale livello distribuire il contenuto. Al contrario, offre una serie di possibilità e permette al progetto di determinare quale soluzione sia la più adatta alle proprie esigenze.
