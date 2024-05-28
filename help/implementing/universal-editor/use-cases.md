---
title: Casi d’uso e percorsi di apprendimento dell’editor universale
description: Scopri i casi d’uso principali di Universal Editor e come utilizzarlo al meglio e come implementarlo nei tuoi progetti.
source-git-commit: 45418e5fd431980b48eda83811d5544154027d84
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 0%

---


# Casi d’uso e percorsi di apprendimento dell’editor universale {#use-cases-learning-paths}

Scopri i casi d’uso principali di Universal Editor e come usarlo al meglio per saperne di più sul suo utilizzo e come implementarlo nei tuoi progetti.

## Panoramica {#overview}

Universal Editor è un editor visivo versatile che fa parte di Adobe Experience Manager Sites. Consente agli autori di eseguire la modifica WYSIWYG (What-you-see-is-what-you-get) di qualsiasi esperienza headless o headful.

Questo documento illustra in dettaglio questi due casi d’uso e mostra come saperne di più su di essi in modo da poter implementare l’Editor universale nel tuo progetto.

>[!TIP]
>
>Se non lo hai già fatto, controlla il documento [Introduzione all’editor universale](/help/implementing/universal-editor/introduction.md) per una panoramica e un valore completi di Universal Editor.

## Casi d’uso {#use-cases}

L’editor universale offre agli autori dei contenuti un editor visivo comodo e intuitivo, indipendentemente dal tipo di contenuto che creano. I due casi d’uso principali sono:

* [Authoring basato su AEM](#aem-authoring) : utilizza la console AEM Sites per gestire i contenuti e le pagine di authoring all’interno dell’AEM utilizzando l’editor universale
* [Authoring headless](#headless-authoring) : crea contenuti nella tua applicazione headless personalizzata utilizzando l’Editor universale.

### Authoring basato su AEM {#aem-authoring}

Se conosci l’AEM, puoi utilizzare la console Sites per creare e gestire le pagine e quindi modificarle con l’editor universale.

In questo modo è possibile beneficiare degli strumenti disponibili nella console Sites, ad esempio la gestione delle pagine (copia, incolla, sposta) e dei flussi di lavoro, ma anche del moderno editor universale.

Se questo è il tuo caso d’uso, come prossimo passo, consulta i seguenti documenti per una panoramica completa su come iniziare a utilizzare Universal Editor in AEM.

1. [Guida introduttiva per gli sviluppatori per l’authoring di AEM con Edge Delivery Services](/help/edge/aem-authoring/edge-dev-getting-started.md) - Introduzione al primo progetto Universal Editor in AEM
1. [Creazione di blocchi instrumentati per l’utilizzo con l’editor universale](/help/edge/aem-authoring/create-block.md) - Scopri come dotare di strumenti i blocchi per rendere i contenuti modificabili nell’Editor universale
1. [Modellazione dei contenuti per l’authoring AEM con progetti Edge Delivery Services](/help/edge/aem-authoring/content-modeling.md) - Scopri i dettagli della struttura dei blocchi per modellare in modo efficace i contenuti da utilizzare con Universal Editor.

Dopo aver letto questi documenti, puoi tornare a questa pagina per scoprire il caso d’uso dell’authoring headless e il funzionamento generale dell’Editor universale.

### Authoring headless {#headless-authoring}

Se disponi già di un’app headless, puoi utilizzare l’Editor universale per creare contenuti per l’app e mantenerli come frammenti di contenuto nell’AEM. L’unico requisito è che l’app sia dotata di strumenti che consentano l’utilizzo dell’editor universale.

Se questo è il tuo caso d’uso, come passaggio successivo immediato, consulta il seguente documento per un esempio di app headless dotata di strumenti per l’utilizzo dell’editor universale.

* [App di esempio SecurBank per l’editor universale](/help/implementing/universal-editor/securbank.md)

Dopo aver letto il documento, puoi tornare a questa pagina per scoprire il caso d’uso dell’authoring AEM e il funzionamento generale dell’Editor universale.

## Funzionamento dell&#39;editor universale {#how-ue-works}

La potenza dell’editor universale è la capacità di creare qualsiasi contenuto sul posto, fornendo all’autore del contenuto un’interfaccia utente completamente intuitiva e unificata indipendentemente dal contenuto.

L’editor universale funziona nel modo seguente.

1. Uno sviluppatore strumentalizza l’app o la pagina per utilizzare l’Editor universale. Questa strumentazione indica all’editor il contenuto modificabile e come mantenerlo.
   * Per l’authoring basato su AEM, le pagine create utilizzando il modello boilerplate vengono automaticamente instrumentate.
   * Per l’authoring headless, l’app può essere facilmente dotata di strumenti.
1. L’autore del contenuto carica l’Editor universale, che a sua volta carica la pagina per la modifica. Poiché è dotata di strumenti, conosce il contenuto modificabile e come deve essere rappresentato e mantenuto.
1. L’autore del contenuto modifica il contenuto della pagina in un’interfaccia WYSIWYG intuitiva, modificando direttamente.
1. L&#39;editor universale salva automaticamente le modifiche in AEM.

Per ulteriori informazioni sull&#39;architettura di Universal Editor, consultare il documento [Architettura di Universal Editor.](/help/implementing/universal-editor/architecture.md)

## Concetti relativi all’editor universale {#concepts}

Affinché una pagina o un’app possa essere modificata dall’editor universale, deve essere dotata di strumenti appropriati. Una volta dotata di strumenti, può essere ulteriormente adattata alle esigenze del progetto.

* [Attributi e tipi](/help/implementing/universal-editor/attributes-types.md) - Affinché un&#39;app o una pagina possa essere modificata dall&#39;editor universale, deve essere dotata di strumenti appropriati. Ciò include l’inclusione dei metadati corretti in modo che l’editor possa modificare il contenuto dell’app.
* [Definizioni di modelli, campi e tipi di componenti](/help/implementing/universal-editor/field-types.md) - Una volta che i metadati sono presenti per abilitare la modifica di un componente, puoi definire quali campi e tipi di componenti possono essere manipolati nella barra delle proprietà dell’editor. A tale scopo, crea un modello e crea un collegamento a tale modello dal componente.
* [Personalizzazione dell’esperienza di authoring di Universal Editor](/help/implementing/universal-editor/customizing.md) - Una volta che l’app o la pagina è completamente dotata di strumenti, l’esperienza dell’editor universale può essere ulteriormente adattata filtrando i componenti disponibili o estendendo le funzionalità dell’editor.
* [Eventi editor universale](/help/implementing/universal-editor/events.md) - Puoi personalizzare ulteriormente l’app reagendo agli eventi standard inviati da Universal per le modifiche al contenuto e all’interfaccia utente.
