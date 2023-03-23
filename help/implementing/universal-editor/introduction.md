---
title: Introduzione all’editor visivo universale
description: Scopri in che modo l’Editor visivo universale (anche editor universale) consente la modifica WYSIWYG (What-you-see-is-what-you-get) di qualsiasi esperienza headless e headful. Scopri in che modo può aiutare gli autori di contenuti a fornire esperienze eccezionali, velocizzare i contenuti e fornire agli sviluppatori un’esperienza di sviluppo all’avanguardia.
source-git-commit: 0e66c379e10d275610d85a699da272dc0c32a9a8
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 0%

---


# Introduzione all’editor visivo universale {#introduction}

Scopri in che modo l’Editor visivo universale (anche editor universale) consente la modifica WYSIWYG (What-you-see-is-what-you-get) di qualsiasi esperienza headless e headful. Scopri in che modo può aiutare gli autori di contenuti a fornire esperienze eccezionali, velocizzare i contenuti e fornire agli sviluppatori un’esperienza di sviluppo all’avanguardia.

## Informazioni di base {#background}

Lo strumento più efficace per l’autore di contenuti AEM è stato l’editor di pagine. L’editor pagina offre un’esperienza di authoring WYSIWYG intuitiva, visiva e contestuale che richiede una formazione minima e mostra agli autori esattamente come apparirà il contenuto.

Tuttavia, l’editor pagina può modificare solo AEM contenuto della pagina, la struttura e i componenti in essa contenuti. Oggi, tuttavia, i contenuti provengono raramente da un&#39;unica posizione. L’editor universale offre la stessa esperienza di modifica diretta dell’editor di pagine, ma per qualsiasi aspetto di contenuto in qualsiasi implementazione.

## Veramente universale {#universal}

L’Editor universale può essere utilizzato per qualsiasi implementazione, per qualsiasi contenuto e per qualsiasi aspetto del contenuto.

![Cosa lo rende universale](assets/universal.png)

### Qualsiasi implementazione {#any-implementation}

Poiché le esperienze possono essere create in diversi modi, qualsiasi implementazione può sfruttare l’Editor universale per consentire agli autori di eseguire modifiche contestuali.

Gli utenti spesso pensano che un’implementazione headless limiti gli autori a modificare tutti i contenuti in un’interfaccia utente basata su moduli, ma questo non vale per l’editor universale

I requisiti per un’implementazione che sfrutta l’Editor universale sono molto semplici e supportano:

* **Qualsiasi architettura** - Rendering lato server, rendering lato server, rendering lato client, ecc.
* **Qualsiasi quadro** - Vaniglia AEM, o qualsiasi framework di terze parti come React, Next.js, Angular, ecc.
* **Qualsiasi hosting** - Può essere ospitato localmente su AEM o su un dominio remoto

### Qualsiasi contenuto {#any-content}

Un autore di contenuti deve avere la stessa potente esperienza di modifica precedentemente offerta dall’editor di pagine AEM. Tuttavia, l’editor universale consente agli autori di contenuti di modificare **qualsiasi** contenuto visivo e contestuale e supporta:

* **AEM strutture di pagina** - Nidificato `cq:Components` di `cq:Pages`, compresi i frammenti esperienza
* **Frammenti di contenuto AEM** - Modifica il contenuto dei frammenti di contenuto visualizzato nel contesto dell’esperienza.
* **Documenti** - La prova dei concetti ha mostrato che anche i documenti Word, Excel, Google Docs o Markdown possono essere modificati nello stesso modo (questo è WIP).

### Qualsiasi aspetto {#any-aspect}

Per un autore di contenuti, il contenuto non riguarda solo le informazioni contenute, ma anche il rendering e la ricezione. Il contenuto viene fornito con metadati aggiuntivi e regole di strumentazione, che l’Editor universale può comprendere e modificare, tra cui:

* **Applicazione di layout e stile** - Utilizzando un sistema di stili, il professionista del marketing e l’autore di contenuti possono applicare stili diversi ai loro contenuti e creare layout diversi per i contenuti, come colonne, caroselli, schede, pannello a soffietto, ecc.

## Valore {#value}

Separando l’esperienza di modifica dei contenuti da qualsiasi sistema di distribuzione dei contenuti, l’editor diventa davvero universale e flessibile, consentendo all’autore dei contenuti di fornire esperienze eccezionali, di velocizzare i contenuti e di fornire un’esperienza di sviluppo all’avanguardia.

![Valore dell’editor universale](assets/value.png)

* **Fornire esperienze eccezionali** - Per consentire ai professionisti di creare un’esperienza coinvolgente per i visitatori, l’editor universale consente ai professionisti di creare e modificare il contenuto nel contesto dell’anteprima. Questo consente loro di creare contenuti adatti alla progettazione dell’esperienza e che costituiscono un percorso significativo per i visitatori.
* **Aumento della velocità dei contenuti** - Per semplificare il flusso di lavoro di gestione dei professionisti, l’editor universale consente di modificare i contenuti nell’anteprima per guidare i professionisti, mostrando solo le opzioni pertinenti a tale contesto e rende il flusso di lavoro indipendente dalle origini di contenuto.
* **Esperienza per sviluppatori all’avanguardia** - Per supportare un panorama delle applicazioni eterogeneo nel mondo reale, Universal Editor è completamente disaccoppiato e non si basa sulla tecnologia, consentendo agli sviluppatori di utilizzare il proprio stack di tecnologia preferito per implementare l&#39;esperienza.

## Editor visivo universale e Editor frammento di contenuto {#universal-editor-content-fragment-editor}

A prima vista, potrebbe sembrare che l’Editor visivo universale e l’Editor frammento di contenuto forniscano funzionalità di modifica simili. Tuttavia, questi editor offrono funzionalità molto diverse e svolgono diversi lavori del professionista del marketing.

### Editor frammento di contenuto {#content-fragment-editor}

Un professionista del marketing desidera creare contenuti senza doversi preoccupare del layout, in modo che possano essere riutilizzati in numerosi contesti dell’esperienza.

* Il lavoro sottostante da eseguire è quello di scalare la strategia dei contenuti.

### Editor visivo universale {#universal-editor}

Un professionista del marketing desidera creare contenuti personalizzati in base al layout di un determinato contesto per offrire un’esperienza eccezionale.

* Il lavoro sottostante da realizzare è quello di entrare in contatto in modo convincente con i lettori.

## Mappa stradale {#road-map}

È importante notare che l’editor universale è un lavoro in corso e che alcune delle funzionalità descritte in questo documento sono una visione dell’editor finale e non necessariamente rappresentative delle sue attuali capacità.

Contatta il tuo contatto Adobe per maggiori informazioni sulle prossime funzionalità previste per l’Editor Universale.

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni sull’editor universale, consulta questi documenti.

* [Creazione di contenuti con l’editor universale](authoring.md) - Scopri quanto è semplice e intuitivo per gli autori di contenuti creare contenuti utilizzando l’Editor universale.
* [Pubblicazione di contenuti con l’editor universale](publishing.md) - Scopri in che modo Universal Visual Editor pubblica i contenuti e come le tue app possono gestire i contenuti pubblicati.
* [Guida introduttiva all’Editor universale in AEM](getting-started.md) - Scopri come accedere all’editor universale e come iniziare a strumentalizzare la tua prima app AEM per utilizzarla.
* [Architettura dell’editor universale](architecture.md) - Scopri l’architettura dell’Editor universale e il flusso di dati tra i suoi servizi e livelli.
* [Attributi e tipi](attributes-types.md) - Scopri gli attributi e i tipi di dati richiesti dall’Editor universale.
* [Autenticazione dell’editor universale](authentication.md) - Scopri come l’editor universale si autentica.
