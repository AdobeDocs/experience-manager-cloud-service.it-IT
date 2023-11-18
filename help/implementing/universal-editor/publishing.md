---
title: Pubblicazione di contenuti con l’editor universale
description: Scopri come l’Editor universale pubblica i contenuti e come le app possono gestire i contenuti pubblicati.
exl-id: aee34469-37c2-4571-806b-06c439a7524a
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 55%

---


# Pubblicazione di contenuti con l’editor universale {#publishing}

Scopri come l’Editor universale pubblica i contenuti e come le app possono gestire i contenuti pubblicati.

## Somiglianze con AEM {#similarities}

Per gli utenti di AEM, il processo di pubblicazione dei contenuti con Universal Editor funziona come di consueto: al momento della pubblicazione nell’AEM, i contenuti vengono replicati dal livello di authoring a quello di pubblicazione.

## Differenze {#differences}

Ciò che rende la pubblicazione con Universal Editor un po&#39; diversa non è tanto l&#39;editor stesso, ma piuttosto l&#39;hosting esterno dell&#39;app reso possibile da Universal Editor.

Quando è ospitata esternamente, è compito della web app assicurare che il contenuto venga caricato dal livello di authoring quando l’app viene aperta dagli autori all’interno dell’editor, e che venga caricato dal livello di pubblicazione quando i visitatori possono accedere all’app.

## Rilevamento del livello nell’app {#detecting}

Per determinare se il livello di authoring o pubblicazione deve essere accessibile, nell’app puoi usare una semplice istruzione condizionale per scegliere l’endpoint di authoring o pubblicazione appropriato al momento di rilevare l’apertura nell’editor.

Un’altra opzione consiste nell’implementare l’app in due ambienti diversi configurati in maniera diversa, in modo che uno recuperi il contenuto dal livello di authoring e un altro lo recuperi dal livello di pubblicazione. Per consentire agli autori di aprire l’URL pubblicato nell’editor universale, è possibile creare un piccolo script per &quot;convertire&quot; l’URL lato pubblicazione nel relativo equivalente nell’ambiente di authoring (ad esempio, anteponendo un `author` sottodominio), in modo che gli autori vengano automaticamente reindirizzati.

## Riepilogo {#summary}

L’obiettivo dell’editor universale è di non imporre alcun modello particolare, in modo che l’implementazione possa raggiungere al meglio i suoi obiettivi in una modalità completamente separata, assicurando al tempo stesso che tutto risulti semplice e chiaro per l’implementazione.

Allo stesso modo, l’editor universale non detta i requisiti su come un particolare progetto debba determinare da quale livello distribuire il contenuto. Al contrario, offre diverse possibilità e consente al progetto di determinare quale soluzione soddisfa al meglio le proprie esigenze.
