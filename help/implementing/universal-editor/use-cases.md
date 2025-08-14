---
title: Casi d’uso e percorsi di apprendimento dell’editor universale
description: Scopri i casi d’uso principali di Universal Editor e come utilizzarlo al meglio e come implementarlo nei tuoi progetti.
exl-id: 398ad0e2-c299-4c49-9784-05c84c67bec2
feature: Developing
role: Admin, Architect, Developer
source-git-commit: bb149cd43158bfd1ceb43b04cc536c8c8291f968
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 0%

---

# Casi d’uso e percorsi di apprendimento dell’editor universale {#use-cases-learning-paths}

Scopri i casi d’uso principali di Universal Editor e come usarlo al meglio per saperne di più sul suo utilizzo e come implementarlo nei tuoi progetti.

## Panoramica {#overview}

Universal Editor è un editor visivo versatile che fa parte di Adobe Experience Manager Sites. Consente agli autori di eseguire la modifica di ciò che vedi è ciò che ottieni (WYSIWYG) di qualsiasi esperienza headless o headful.

Questo documento illustra in dettaglio questi due casi d’uso e mostra come saperne di più su di essi in modo da poter implementare l’Editor universale nel tuo progetto.

>[!TIP]
>
>Se non lo hai già fatto, consulta il documento [Introduzione all&#39;editor universale](/help/implementing/universal-editor/introduction.md) per una panoramica completa e un valore dell&#39;editor universale.

## Casi d’uso {#use-cases}

L’editor universale offre agli autori dei contenuti un editor visivo comodo e intuitivo, indipendentemente dal tipo di contenuto che creano. I due casi d’uso principali sono:

* [Authoring di WYSIWYG](#wysiwyg-authoring) - Utilizza la console AEM Sites per gestire i contenuti e creare pagine in AEM tramite l&#39;editor universale
* [Authoring headless](#headless-authoring): creazione di contenuti nella tua applicazione headless personalizzata tramite l&#39;editor universale.

### Authoring WYSIWYG {#wysiwyg-authoring}

Se conosci già AEM, puoi utilizzare la console Sites per creare e gestire le pagine e quindi modificarle con l’Editor universale.

In questo modo è possibile beneficiare degli strumenti disponibili nella console Sites, ad esempio la gestione delle pagine (copia, incolla, sposta) e dei flussi di lavoro, ma anche del moderno editor universale.

Se si tratta del tuo caso d’uso, come passaggio successivo, consulta i seguenti documenti per una panoramica completa su come iniziare a utilizzare Universal Editor in AEM.

1. [Guida introduttiva per sviluppatori per l&#39;authoring di WYSIWYG con Edge Delivery Services](https://www.aem.live/developer/ue-tutorial) - Introduzione al primo progetto Universal Editor in AEM
1. [Creazione di blocchi instrumentati per l&#39;utilizzo con Universal Editor](https://www.aem.live/developer/universal-editor-blocks) - Scopri come dotare di strumenti i blocchi per rendere modificabili i contenuti nell&#39;Universal Editor
1. [Modellazione dei contenuti per l&#39;authoring WYSIWYG con progetti Edge Delivery Services](https://www.aem.live/developer/component-model-definitions) - Scopri i dettagli della struttura dei blocchi per modellare in modo efficace i contenuti da utilizzare con l&#39;editor universale.

Dopo aver letto questi documenti, puoi tornare a questa pagina per scoprire il caso d’uso dell’authoring headless e il funzionamento generale dell’Editor universale.

### Authoring headless {#headless-authoring}

Se disponi già di un’app headless, puoi utilizzare l’Editor universale per creare contenuti per l’app e mantenerli come frammenti di contenuto in AEM. L’unico requisito è che l’app sia dotata di strumenti che consentano l’utilizzo dell’editor universale.

Se questo è il tuo caso d’uso, come passaggio successivo immediato, consulta il seguente documento per un esempio di app headless dotata di strumenti per l’utilizzo dell’editor universale.

* [App di esempio SecurBank per l’editor universale](/help/implementing/universal-editor/securbank.md)

Dopo aver letto il documento, puoi tornare a questa pagina per scoprire il caso d’uso dell’authoring di WYSIWYG e il funzionamento generale dell’Editor universale.

{{ue-headless-auth}}

## Funzionamento dell&#39;editor universale {#how-ue-works}

La potenza dell’editor universale è la capacità di creare qualsiasi contenuto sul posto, fornendo all’autore del contenuto un’interfaccia utente completamente intuitiva e unificata indipendentemente dal contenuto.

L’editor universale funziona nel modo seguente.

1. Uno sviluppatore strumentalizza l’app o la pagina per utilizzare l’Editor universale. Questa strumentazione indica all’editor il contenuto modificabile e come mantenerlo.
   * Se si segue la [Guida introduttiva per sviluppatori per l&#39;authoring di WYSIWYG con Edge Delivery Services](https://www.aem.live/developer/ue-tutorial), le pagine vengono automaticamente instrumentate.
   * Per l’authoring headless, l’app può essere facilmente dotata di strumenti.
1. L’autore del contenuto carica l’Editor universale, che a sua volta carica la pagina per la modifica. Poiché è dotata di strumenti, conosce il contenuto modificabile e come deve essere rappresentato e mantenuto.
1. L’autore del contenuto modifica il contenuto della pagina in un’interfaccia intuitiva di WYSIWYG, modificando direttamente la pagina.
1. Le modifiche vengono automaticamente riportate nell&#39;origine dati in modo permanente nell&#39;Editor universale.

Per ulteriori informazioni sull&#39;architettura di Universal Editor, vedere il documento [Architettura di Universal Editor](/help/implementing/universal-editor/architecture.md).

## Concetti relativi all’editor universale {#concepts}

Affinché una pagina o un’app possa essere modificata dall’editor universale, deve essere dotata di strumenti appropriati.

* [Attributi e tipi](/help/implementing/universal-editor/attributes-types.md) - Affinché un&#39;app o una pagina possa essere modificata dall&#39;editor universale, è necessario che sia dotata di strumenti appropriati. Ciò include l’inclusione dei metadati corretti in modo che l’editor possa modificare il contenuto dell’app.
* [Definizioni modello, campi e tipi di componente](/help/implementing/universal-editor/field-types.md) - Una volta che i metadati sono presenti per consentire la modifica di un componente, puoi definire quali campi e tipi di componente possono essere modificati nel pannello delle proprietà dell&#39;editor.
* [Eventi editor universale](/help/implementing/universal-editor/events.md) - Puoi personalizzare ulteriormente l&#39;app migliorando l&#39;esperienza di modifica nell&#39;app tramite l&#39;utilizzo di eventi generati dall&#39;editor universale sul contenuto o sulle interazioni dell&#39;interfaccia utente.

L’editor universale può anche essere adattato in base alle esigenze del progetto.

* [Personalizzazione dell&#39;editor universale](/help/implementing/universal-editor/customizing.md) - L&#39;esperienza dell&#39;editor può essere adattata filtrando vari aspetti dell&#39;editor o estendendo le funzionalità dell&#39;editor.
* [Estensione dell&#39;editor universale](/help/implementing/universal-editor/extending.md) - L&#39;interfaccia utente dell&#39;editor universale può essere estesa per espandere le funzionalità in base alle esigenze del progetto.
