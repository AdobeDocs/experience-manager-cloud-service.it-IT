---
title: Casi d’uso e percorsi di apprendimento dell’editor universale
description: Scopri i casi d’uso principali dell’editor universale e come utilizzarlo al meglio e implementarlo nei tuoi progetti.
exl-id: 398ad0e2-c299-4c49-9784-05c84c67bec2
feature: Developing
role: Admin, Architect, Developer
source-git-commit: bb149cd43158bfd1ceb43b04cc536c8c8291f968
workflow-type: ht
source-wordcount: '882'
ht-degree: 100%

---

# Casi d’uso e percorsi di apprendimento dell’editor universale {#use-cases-learning-paths}

Scopri i casi d’uso principali dell’editor universale e il modo migliore per saperne di più sul suo utilizzo e su come implementarlo nei tuoi progetti.

## Panoramica {#overview}

L’editor universale è un editor visivo versatile che fa parte di Adobe Experience Manager Sites. Consente agli autori di apportare modifiche in modalità WYSIWYG (what you see is what you get) a qualsiasi esperienza headless o headful.

Questo documento illustra in dettaglio questi due casi d’uso e mostra come saperne di più su di essi in modo da poter implementare l’editor universale nel tuo progetto.

>[!TIP]
>
>Se non lo hai già fatto, consulta il documento [Introduzione all’editor universale](/help/implementing/universal-editor/introduction.md) per avere una panoramica completa e comprendere il valore dell’editor universale.

## Casi d’uso {#use-cases}

L’editor universale offre agli autori di contenuti un editor visivo comodo e intuitivo, indipendentemente dal tipo di contenuto che creano. I due casi d’uso principali sono:

* [Authoring WYSIWYG](#wysiwyg-authoring): utilizza la console AEM Sites per gestire i contenuti e creare pagine in AEM tramite l’editor universale
* [Authoring headless](#headless-authoring): crea contenuti nella tua applicazione headless personalizzata tramite l’editor universale.

### Authoring WYSIWYG {#wysiwyg-authoring}

Se conosci già AEM, puoi utilizzare la console Sites per creare e gestire le pagine e quindi modificarle con l’editor universale.

In questo modo è possibile beneficiare degli strumenti disponibili nella console Sites, ad esempio la gestione delle pagine (copia, incolla, sposta) e dei flussi di lavoro, ma anche del moderno editor universale.

Se si tratta del tuo caso d’uso, come passaggio successivo, consulta i seguenti documenti per una panoramica completa su come iniziare a utilizzare l’editor universale in AEM.

1. [Guida introduttiva per sviluppatori sull’authoring WYSIWYG con Edge Delivery Services](https://www.aem.live/developer/ue-tutorial): introduzione al primo progetto con l’editor universale in AEM
1. [Creazione di blocchi dotati di strumenti per l’utilizzo con l’editor universale](https://www.aem.live/developer/universal-editor-blocks): scopri come dotare di strumenti i blocchi per rendere modificabili i contenuti nell’editor universale
1. [Modellazione dei contenuti per l’authoring WYSIWYG con progetti Edge Delivery Services](https://www.aem.live/developer/component-model-definitions): scopri i dettagli della struttura dei blocchi per modellare in modo efficace i contenuti da utilizzare con l’editor universale.

Dopo aver letto questi documenti, puoi tornare a questa pagina per scoprire il caso d’uso dell’authoring headless e il funzionamento generale dell’editor universale.

### Authoring headless {#headless-authoring}

Se disponi già di un’app headless, puoi utilizzare l’editor universale per creare contenuti per l’app e mantenerli come frammenti di contenuto in AEM. L’unico requisito è che l’app sia dotata di strumenti che consentono l’utilizzo dell’editor universale.

Se questo è il tuo caso d’uso, come passaggio successivo immediato, consulta il seguente documento per un esempio di app headless dotata di strumenti per l’utilizzo dell’editor universale.

* [App di esempio SecurBank per l’editor universale](/help/implementing/universal-editor/securbank.md)

Dopo aver letto il documento, puoi tornare a questa pagina per scoprire il caso d’uso dell’authoring WYSIWYG e il funzionamento generale dell’editor universale.

{{ue-headless-auth}}

## Funzionamento dell’editor universale {#how-ue-works}

La potenza dell’editor universale consiste nella capacità di creare qualsiasi contenuto in modo diretto, fornendo all’autore un’interfaccia utente completamente intuitiva e unificata indipendentemente dal contenuto.

L’editor universale funziona nel modo seguente.

1. Uno sviluppatore dota l’app o la pagina di strumenti per utilizzare l’editor universale. Questa strumentazione indica all’editor il contenuto modificabile e come mantenerlo.
   * Se segui la documentazione [Guida introduttiva per sviluppatori sull’authoring WYSIWYG con Edge Delivery Services](https://www.aem.live/developer/ue-tutorial), le pagine vengono automaticamente dotate di strumenti.
   * Per l’authoring headless, l’app può essere facilmente dotata di strumenti.
1. L’autore del contenuto carica l’editor universale, che a sua volta carica la pagina per la modifica. Grazie a questa strumentazione, l’editor riconosce il contenuto modificabile e come deve essere rappresentato e mantenuto.
1. L’autore del contenuto modifica direttamente il contenuto della pagina in un’interfaccia WYSIWYG intuitiva.
1. L’editor universale rende persistenti le modifiche riportandole automaticamente nell’origine dati.

Per ulteriori informazioni sull’architettura dell’editor universale, consulta il documento [Architettura dell’editor universale](/help/implementing/universal-editor/architecture.md).

## Concetti dell’editor universale {#concepts}

Affinché un’app possa essere modificata dall’editor universale, deve essere dotata di strumentazione corretta.

* [Attributi e tipi](/help/implementing/universal-editor/attributes-types.md): affinché un’app o una pagina possa essere modificata dall’editor universale, deve essere dotata di strumentazione corretta. Vanno inclusi anche i metadati appropriati, in modo che l’editor possa modificare il contenuto dell’app.
* [Definizioni modello, campi e tipi di componente](/help/implementing/universal-editor/field-types.md): quando sono presenti i metadati per consentire la modifica di un componente, puoi definire quali campi e tipi di componente possono essere modificati nel pannello delle proprietà dell’editor.
* [Eventi editor universale](/help/implementing/universal-editor/events.md): puoi personalizzare ulteriormente l’app migliorando l’esperienza di modifica al suo interno, sfruttando gli eventi generati dall’editor universale sul contenuto o le interazioni dell’interfaccia utente.

L’editor universale può anche essere adattato in base alle esigenze del progetto.

* [Personalizzazione dell’editor universale](/help/implementing/universal-editor/customizing.md) - L’esperienza con l’editor universale può essere adattata applicando filtri a vari aspetti dell’editor o estendendo le funzionalità dell’editor.
* [Estensione dell’editor universale](/help/implementing/universal-editor/extending.md) - L’interfaccia utente dell’editor universale può essere estesa per espanderne le funzionalità in base alle esigenze del progetto.
