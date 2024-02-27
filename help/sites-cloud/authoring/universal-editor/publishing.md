---
title: Pubblicazione di contenuti con l’editor universale
description: Scopri in che modo l’editor universale pubblica i contenuti e come le tue app possono gestire i contenuti pubblicati.
exl-id: aee34469-37c2-4571-806b-06c439a7524a
source-git-commit: 58d85886ef04b548c09e3ef9308fe596dd3eda38
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 69%

---


# Pubblicazione di contenuti con l’editor universale {#publishing}

Scopri in che modo l’editor universale pubblica i contenuti e come le tue app possono gestire i contenuti pubblicati.

{{universal-editor-status}}

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

## Risorse aggiuntive {#additional-resources}

Per informazioni su come creare contenuti con l’editor universale, consulta questo documento.

* [Authoring dei contenuti con l’editor universale](authoring.md): scopri quanto è semplice e intuitivo per gli autori di contenuto creare contenuto utilizzando l’editor universale.

Per ulteriori informazioni sui dettagli tecnici di Universal Editor, consulta questi documenti per gli sviluppatori.

* [Introduzione all’editor universale](/help/implementing/universal-editor/introduction.md): scopri come l’editor universale consente di modificare ogni aspetto di qualsiasi contenuto in qualsiasi implementazione per fornire esperienze eccezionali, velocizzare la preparazione dei contenuti e fornire un’esperienza di sviluppo all’avanguardia.
* [Guida introduttiva all’editor universale in AEM](/help/implementing/universal-editor/getting-started.md): scopri come accedere all’editor universale e come iniziare a instrumentare la prima app AEM per utilizzarla.
* [Architettura dell’editor universale](/help/implementing/universal-editor/architecture.md): scopri l’architettura dell’editor universale e il flusso di dati tra i suoi servizi e livelli.
* [Attributi e tipi](/help/implementing/universal-editor/attributes-types.md): scopri gli attributi e i tipi di dati richiesti dall’editor universale.
* [Autenticazione dell’editor universale](/help/implementing/universal-editor/authentication.md): scopri come l’editor universale effettua l’autenticazione.
