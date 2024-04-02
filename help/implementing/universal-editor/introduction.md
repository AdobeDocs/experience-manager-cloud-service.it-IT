---
title: Introduzione all’editor universale
description: Scopri in che modo Universal Editor consente di modificare ciò che vedi è ciò che ottieni (WYSIWYG) di qualsiasi esperienza headless e headful. Scopri in che modo questo può aiutare gli autori di contenuto a fornire esperienze eccezionali, aumentare la velocità del contenuto e fornire agli sviluppatori un’esperienza di sviluppo all’avanguardia.
exl-id: d4fc2384-a0f5-4a6f-9572-62749786be4c
source-git-commit: b6548d39ce02006d91f1953c878e08a1c0903563
workflow-type: tm+mt
source-wordcount: '868'
ht-degree: 83%

---


# Introduzione all’editor universale {#introduction}

Scopri in che modo Universal Editor consente di modificare ciò che vedi è ciò che ottieni (WYSIWYG) di qualsiasi esperienza headless e headful. Scopri in che modo questo può aiutare gli autori di contenuto a fornire esperienze eccezionali, aumentare la velocità del contenuto e fornire agli sviluppatori un’esperienza di sviluppo all’avanguardia.

## Informazioni di base {#background}

Lo strumento più efficace per gli autori di contenuto AEM è stato l’editor pagina. L’editor pagina offre un’esperienza di authoring WYSIWYG intuitiva, visiva e contestuale che richiede una formazione minima e mostra agli autori esattamente come apparirà il contenuto.

Tuttavia, l’editor pagina può modificare solo il contenuto della pagina AEM, la struttura e i componenti in essa contenuti. Oggi, tuttavia, il contenuto proviene raramente da un’unica posizione. L’Editor universale offre la stessa esperienza di modifica diretta dell’editor pagina, ma per qualsiasi aspetto del contenuto in qualsiasi implementazione.

## Veramente universale {#universal}

L’Editor universale può essere utilizzato per qualsiasi implementazione, per qualsiasi contenuto e per qualsiasi aspetto del contenuto.

![Cosa lo rende universale](assets/universal.png)

### Qualsiasi implementazione {#any-implementation}

Poiché le esperienze possono essere create in tanti modi diversi, qualsiasi implementazione può utilizzare l’Editor universale, per consentire agli autori di eseguire modifiche nel contesto.

Gli utenti spesso pensano che un’implementazione headless limiti gli autori a modificare tutto il contenuto in un’interfaccia utente basata su moduli, ma questo non vale per l’Editor universale

I requisiti per un’implementazione che utilizza l’Editor universale sono molto semplici e supportano:

* **Qualsiasi architettura** : rendering lato server, rendering lato edge, rendering lato client e così via.
* **Qualsiasi framework** - AEM &quot;vanilla&quot; o qualsiasi framework di terze parti come React, Next.js, Angular e così via.
* **Qualsiasi hosting** - Può essere ospitato localmente su AEM o su un dominio remoto

### Qualsiasi contenuto {#any-content}

Un autore di contenuto deve avere la stessa potente esperienza di modifica precedentemente offerta dall’editor pagina AEM. Tuttavia, l’Editor universale consente agli autori di contenuto di modificare **qualsiasi** contenuto visivamente e nel contesto e supporta:

* **Strutture di pagina AEM** - `cq:Components` nidificati di `cq:Pages`, compresi i Frammenti di esperienza
* **Frammenti di contenuto AEM** - Modifica il contenuto dei Frammenti di contenuto visualizzati nel contesto dell’esperienza.
* **Documenti** - La bozza dei concetti ha mostrato che anche i documenti Word, Excel, Google Docs o Markdown possono essere modificati nello stesso modo (WIP).

### Qualsiasi aspetto {#any-aspect}

Per un autore di contenuto, il contenuto non riguarda solo le informazioni contenute, ma anche il rendering e la ricezione. Il contenuto viene fornito con metadati aggiuntivi e regole di strumentazione, che l’editor universale può comprendere e modificare, tra cui:

* **Applicazione di layout e stile** - Utilizzando un sistema di stili, l’operatore marketing e l’autore di contenuti possono applicare stili diversi al contenuto e creare layout diversi per il contenuto, ad esempio colonne, caroselli, schede, fisarmoniche e così via.

## Valore {#value}

Svincolando l’esperienza di modifica del contenuto da qualsiasi sistema di distribuzione del contenuto, l’editor diventa davvero universale e flessibile, consentendo all’autore del contenuto di fornire esperienze eccezionali, di aumentare la velocità del contenuto e di fornire un’esperienza di sviluppo all’avanguardia.

![Valore dell’Editor universale](assets/value.png)

* **Fornire esperienze eccezionali**: per consentire ai professionisti di creare un’esperienza coinvolgente per i visitatori, l’Editor universale consente loro di creare e modificare il contenuto nel contesto dell’anteprima. Questo consente di creare contenuti adatti alla progettazione dell’esperienza, in grado di costituire un percorso significativo per i visitatori.
* **Aumento della velocità del contenuto** - Per semplificare la gestione del flusso di lavoro dei professionisti, l’Editor universale consente di modificare il contenuto nell’anteprima per guidare i professionisti mostrando solo le opzioni pertinenti a tale contesto e rende il flusso di lavoro indipendente dalle origini del contenuto.
* **Esperienza per sviluppatori all’avanguardia** - Per supportare un panorama delle applicazioni eterogeneo nel mondo reale, l’Editor universale è completamente dissociato e indipendente dalla tecnologia, consentendo agli sviluppatori di utilizzare l’insieme di tecnologie preferito per implementare l’esperienza.

## Editor universale e Editor frammento di contenuto {#universal-editor-content-fragment-editor}

A prima vista, potrebbe sembrare che l’Editor universale e l’Editor frammento di contenuto forniscano funzionalità di modifica simili. Tuttavia, questi editor offrono funzionalità molto diverse e svolgono diversi compiti del professionista di marketing.

### Editor frammento di contenuto {#content-fragment-editor}

Un professionista del marketing desidera creare contenuto senza doversi preoccupare del layout, in modo che possa essere riutilizzato in numerosi contesti dell’esperienza.

* Il lavoro sottostante da realizzare è quello di scalare la strategia del contenuto.

### Editor universale {#universal-editor}

Un professionista del marketing desidera creare contenuto personalizzato in base al layout di un determinato contesto per offrire un’esperienza eccezionale.

* Il lavoro sottostante da realizzare è quello di entrare in contatto in modo convincente con i lettori.

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni sull’editor universale, consulta questi documenti.

* [Authoring del contenuto con l’Editor universale](/help/sites-cloud/authoring/universal-editor/authoring.md) - Scopri quanto è semplice e intuitivo per gli autori di contenuto creare contenuto utilizzando l’Editor universale.
* [Pubblicazione di contenuti con l’editor universale](/help/sites-cloud/authoring/universal-editor/publishing.md) - Scopri come l’Editor universale pubblica i contenuti e come le app possono gestire i contenuti pubblicati.
* [Guida introduttiva all’editor universale in AEM](getting-started.md): scopri come accedere all’editor universale e come iniziare a instrumentare la prima app AEM per utilizzarla.
* [Architettura dell’editor universale](architecture.md): scopri l’architettura dell’editor universale e il flusso di dati tra i suoi servizi e livelli.
* [Attributi e tipi](attributes-types.md): scopri gli attributi e i tipi di dati richiesti dall’editor universale.
* [Autenticazione dell’editor universale](authentication.md): scopri come l’editor universale effettua l’autenticazione.
