---
title: Pubblicazione dei contenuti da parte dell’Editor universale
description: Scopri in che modo Universal Editor pubblica i propri contenuti, in che modo si differenzia dal processo nella console Sites e le considerazioni da tenere in considerazione durante lo sviluppo di app personalizzate.
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 0ee6689460ac0ecc5c025fb6a940d69a16699c85
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 25%

---


# Pubblicazione dei contenuti da parte dell’Editor universale {#publishing}

Scopri in che modo Universal Editor pubblica i propri contenuti, in che modo si differenzia dal processo nella console Sites e le considerazioni da tenere in considerazione durante lo sviluppo di app personalizzate.

>[!TIP]
>
>Questo articolo descrive i dettagli del processo di pubblicazione dell’editor universale per lo sviluppatore. Per l&#39;autore del contenuto, [il processo di pubblicazione del contenuto è descritto qui.](/help/sites-cloud/authoring/universal-editor/publishing.md)

## Somiglianze con il processo della console Sites {#similarities}

Per gli utenti di [AEM Page Editor](/help/sites-cloud/authoring/page-editor/introduction.md) e [Sites Console,](/help/sites-cloud/authoring/sites-console/introduction.md) il processo di pubblicazione dei contenuti con Universal Editor funziona come di consueto: al momento della pubblicazione in AEM, i contenuti vengono replicati dal servizio di authoring al servizio di pubblicazione (o al [servizio di anteprima](/help/sites-cloud/authoring/sites-console/previewing-content.md), se disponibile e in base alle opzioni scelte dall&#39;autore per la pubblicazione).

## Differenze {#differences}

Ciò che rende la pubblicazione con Universal Editor un po&#39; diversa non è tanto l&#39;editor stesso, ma piuttosto l&#39;hosting esterno dell&#39;app reso possibile da Universal Editor.

Quando è ospitata esternamente, l’app web si preoccupa di garantire che il contenuto venga caricato dal servizio di authoring quando l’app viene aperta dagli autori nell’editor e dal servizio di pubblicazione quando i visitatori accedono all’app.

## Rilevamento del servizio nell’app {#detecting}

Per determinare se è necessario accedere al servizio di authoring o pubblicazione, è possibile utilizzare una semplice istruzione condizionale nell’app che consenta di scegliere l’endpoint di authoring o pubblicazione appropriato per la rilevazione dell’apertura nell’editor.

Un’altra opzione consiste nel distribuire l’app in due ambienti diversi configurati in modo diverso, in modo che uno recuperi il contenuto dal servizio di authoring e uno che lo recuperi dal servizio di pubblicazione. Per consentire agli autori di aprire l’URL pubblicato nell’editor universale, è possibile creare un piccolo script per &quot;convertire&quot; l’URL lato pubblicazione nel suo equivalente nell’ambiente di authoring (ad esempio, anteponendo un sottodominio `author`), in modo che gli autori vengano automaticamente reindirizzati.

## Riepilogo {#summary}

L’obiettivo dell’editor universale è di non imporre alcun modello particolare, in modo che l’implementazione possa raggiungere al meglio i suoi obiettivi in una modalità completamente separata, assicurando al tempo stesso che tutto risulti semplice e chiaro per l’implementazione.

Analogamente, Universal Editor non pone alcun requisito su come un particolare progetto debba determinare da quale servizio alla distribuzione del contenuto. Al contrario, offre diverse possibilità e consente al progetto di determinare quale soluzione soddisfa al meglio le proprie esigenze.

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni sui dettagli tecnici di Universal Editor, consulta questi documenti per gli sviluppatori.

* [Introduzione all’editor universale](/help/implementing/universal-editor/introduction.md): scopri come l’editor universale consente di modificare ogni aspetto di qualsiasi contenuto in qualsiasi implementazione per fornire esperienze eccezionali, velocizzare la preparazione dei contenuti e fornire un’esperienza di sviluppo all’avanguardia.
* [Guida introduttiva all’editor universale in AEM](/help/implementing/universal-editor/getting-started.md): scopri come accedere all’editor universale e come iniziare a instrumentare la prima app AEM per utilizzarla.
* [Architettura dell’editor universale](/help/implementing/universal-editor/architecture.md): scopri l’architettura dell’editor universale e il flusso di dati tra i suoi servizi e livelli.
* [Attributi e tipi](/help/implementing/universal-editor/attributes-types.md): scopri gli attributi e i tipi di dati richiesti dall’editor universale.
* [Autenticazione dell’editor universale](/help/implementing/universal-editor/authentication.md): scopri come l’editor universale effettua l’autenticazione.
