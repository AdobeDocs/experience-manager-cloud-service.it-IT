---
title: In che modo l’editor universale pubblica i contenuti
description: Scopri in che modo l’editor universale pubblica i contenuti, come si differenzia dal processo nella console Sites e le considerazioni da fare durante lo sviluppo di app personalizzate da utilizzare con l’editor.
feature: Developing
role: Admin, Developer
exl-id: 60f0bb4a-ee60-4f73-83ae-8568735474ad
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 100%

---

# In che modo l’editor universale pubblica i contenuti {#publishing}

Scopri in che modo l’editor universale pubblica i contenuti, come si differenzia dal processo nella console Sites e le considerazioni da fare durante lo sviluppo di app personalizzate da utilizzare con l’editor.

>[!TIP]
>
>Questo articolo descrive i dettagli del processo di pubblicazione dell’editor universale per lo sviluppatore. Per l’autore dei contenuti, [il processo di pubblicazione dei contenuti è descritto qui.](/help/sites-cloud/authoring/universal-editor/publishing.md)

## Somiglianze con il processo della console Sites {#similarities}

Per gli utenti dell’[editor pagina di AEM](/help/sites-cloud/authoring/page-editor/introduction.md) e della [console Sites,](/help/sites-cloud/authoring/sites-console/introduction.md) il processo di pubblicazione dei contenuti con l’editor universale funziona come di consueto: al momento della pubblicazione in AEM, i contenuti vengono replicati dal servizio di authoring al servizio di pubblicazione (o al [servizio di anteprima](/help/sites-cloud/authoring/sites-console/previewing-content.md), se disponibile e in base alle opzioni scelte dall’autore per la pubblicazione).

## Differenze {#differences}

Ciò che rende la pubblicazione con l’editor universale un po’ diversa, non è tanto l’editor stesso, ma piuttosto l’hosting esterno dell’app, reso possibile dall’editor universale.

Quando è ospitato esternamente, è compito della web app assicurare che il contenuto venga caricato dal servizio di authoring quando l’app viene aperta dagli autori all’interno dell’editor, e che venga caricato dal servizio di pubblicazione quando i visitatori possono accedere all’app.

## Rilevamento del servizio nell’app {#detecting}

Per determinare se il servizio di authoring o pubblicazione deve essere accessibile, nell’app puoi usare una semplice istruzione condizionale per scegliere l’endpoint di authoring o pubblicazione appropriato al momento di rilevare l’apertura nell’editor.

Un’altra opzione consiste nell’implementare l’app in due ambienti diversi configurati in maniera diversa, in modo che uno recuperi il contenuto dal servizio di authoring e un altro lo recuperi dal servizio di pubblicazione. Per consentire agli autori di aprire l’URL pubblicato nell’editor universale, è possibile creare un piccolo script per “convertire” l’URL lato pubblicazione al suo equivalente nell’ambiente di authoring (ad esempio, anteponendo un sottodominio `author`), in modo che gli autori vengano reindirizzati automaticamente.

## Riepilogo {#summary}

L’obiettivo dell’editor universale è di non imporre alcun modello particolare, in modo che l’implementazione possa raggiungere al meglio i suoi obiettivi in una modalità completamente separata, assicurando al tempo stesso che tutto risulti semplice e chiaro per l’implementazione.

Allo stesso modo, l’editor universale non detta i requisiti su come un particolare progetto debba determinare da quale servizio distribuire il contenuto. Al contrario, offre una serie di possibilità e permette al progetto di determinare quale soluzione sia la più adatta alle proprie esigenze.

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni sui dettagli tecnici dell’editor universale, consulta questi documenti per gli sviluppatori.

* [Introduzione all’editor universale](/help/implementing/universal-editor/introduction.md): scopri come l’editor universale consente di modificare ogni aspetto di qualsiasi contenuto in qualsiasi implementazione per fornire esperienze eccezionali, velocizzare la preparazione dei contenuti e fornire un’esperienza di sviluppo all’avanguardia.
* [Guida introduttiva all’editor universale in AEM](/help/implementing/universal-editor/getting-started.md): scopri come accedere all’editor universale e come iniziare a instrumentare la prima app AEM per utilizzarla.
* [Architettura dell’editor universale](/help/implementing/universal-editor/architecture.md): scopri l’architettura dell’editor universale e il flusso di dati tra i suoi servizi e livelli.
* [Attributi e tipi](/help/implementing/universal-editor/attributes-types.md): scopri gli attributi e i tipi di dati richiesti dall’editor universale.
* [Autenticazione dell’editor universale](/help/implementing/universal-editor/authentication.md): scopri come l’editor universale effettua l’autenticazione.
