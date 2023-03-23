---
title: Pubblicazione di contenuti con l’Editor visivo universale
description: Scopri in che modo Universal Visual Editor pubblica i contenuti e come le tue app possono gestire i contenuti pubblicati.
source-git-commit: 7eeebade0255263a240476bc32f9530574495751
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---


# Pubblicazione di contenuti con l’Editor visivo universale {#publishing}

Scopri in che modo Universal Visual Editor pubblica i contenuti e come le tue app possono gestire i contenuti pubblicati.

## Somiglianze con AEM {#similarities}

Per gli utenti di AEM, il processo di pubblicazione dei contenuti con l’Editor visivo universale funziona come di consueto: alla pubblicazione in AEM, il contenuto viene replicato dal livello di authoring al livello di pubblicazione.

## Differenze {#differences}

Ciò che rende la pubblicazione con Universal Visual Editor un po&#39; diversa non è tanto l&#39;editor stesso, ma piuttosto l&#39;hosting esterno dell&#39;app che l&#39;Universal Editor rende possibile.

Quando è ospitata esternamente, è compito dell’app web assicurarsi che il contenuto venga caricato dal livello di authoring quando l’app viene aperta dagli autori all’interno dell’editor e viene caricato dal livello di pubblicazione quando l’app è accessibile dai visitatori.

## Rilevamento del livello nell’app {#detecting}

Per determinare se il livello di authoring o pubblicazione deve essere accessibile, nell’app puoi usare una semplice istruzione condizionale per scegliere l’endpoint di authoring o pubblicazione appropriato al momento di rilevare l’apertura nell’editor.

Un’altra opzione consiste nell’implementare l’app in due ambienti diversi configurati in modo diverso, in modo che uno recuperi il contenuto dal livello di authoring e uno che lo recuperi dal livello di pubblicazione. Per consentire agli autori di aprire l’URL pubblicato nell’editor universale, è possibile creare un piccolo script per &quot;convertire&quot; l’URL lato pubblicazione al suo equivalente nell’ambiente di authoring (ad esempio, prependendo un `author` sottodominio), in modo che gli autori vengano reindirizzati automaticamente.

## Riepilogo {#summary}

L&#39;obiettivo dell&#39;editor universale è di non imporre alcun modello particolare, in modo che l&#39;implementazione possa raggiungere al meglio i suoi obiettivi in modo completamente disaccoppiato, mantenendo al tempo stesso tutto ciò che è semplice e diretto per l&#39;implementazione.

Allo stesso modo, l’Editor universale non richiede come un particolare progetto debba determinare da quale livello distribuire il contenuto. Permette al progetto di determinare quale soluzione è più adatta alle proprie esigenze.
