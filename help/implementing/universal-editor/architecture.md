---
title: Architettura dell’editor universale
description: Scopri l’architettura dell’Editor universale e il flusso di dati tra i suoi servizi e livelli.
source-git-commit: f454475b65da8f410812bbbe30ca5fc393be410a
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 1%

---


# Architettura dell’editor universale {#architecture}

Scopri l’architettura dell’Editor universale e il flusso di dati tra i suoi servizi e livelli.

## Blocchi predefiniti di architettura {#building-blocks}

L’editor universale è costituito da quattro elementi di base essenziali che interagiscono tra loro e consentono agli autori di contenuti di modificare qualsiasi aspetto di qualsiasi contenuto in qualsiasi implementazione, al fine di fornire esperienze eccezionali, velocizzare i contenuti e fornire un’esperienza di sviluppo all’avanguardia.

1. [Editor](#editors)
1. [App remota](#remote-app)
1. [Livello API](#api-layer)
1. [Livello di persistenza](#persistence-layer)

Questo documento delinea ciascuno di questi blocchi predefiniti e la modalità di scambio dei dati.

![Architettura dell’Editor universale](assets/architecture.png)

>[!TIP]
>
>Per visualizzare l’Editor universale e la relativa architettura in azione, consulta il documento [Guida introduttiva all’Editor universale in AEM](getting-started.md) per scoprire come accedere all’Editor universale e come iniziare a strumentalizzare la tua prima app AEM per utilizzarla.

### Editor {#editors}

* **Editor universale** - L’editor universale utilizza un DOM dotato di strumenti per consentire la modifica diretta dei contenuti. Vedi il documento [Attributi e tipi](attributes-types.md) per informazioni dettagliate sui metadati necessari. Vedere il documento [Guida introduttiva all’Editor universale in AEM](getting-started.md) per un esempio della strumentazione in AEM.
* **Barra delle proprietà** - Alcune proprietà dei componenti non possono essere modificate nel contesto, ad esempio il tempo di rotazione di un carosello o la scheda a soffietto deve essere sempre aperta o chiusa. Per consentire la modifica di tali informazioni sui componenti, nella barra laterale dell’editor viene fornito un editor basato su moduli.

### App remota {#remote-app}

Per rendere modificabile un’app in un contesto nell’editor universale, è necessario dotare lo strumento DOM. L’app remota deve eseguire il rendering di alcuni attributi nel DOM. Vedi il documento [Attributi e tipi](attributes-types.md) per informazioni dettagliate sui metadati necessari. Vedere il documento [Guida introduttiva all’Editor universale in AEM](getting-started.md) per un esempio della strumentazione in AEM.

L’editor universale si impegna per un SDK minimo, pertanto la strumentazione è responsabilità dell’implementazione remota dell’app.

### Livello API {#api-layer}

* **Dati contenuto** - Per l’editor universale, non è importante né il sistema sorgente dei dati di contenuto né il modo in cui vengono utilizzati. È importante solo definire e fornire gli attributi richiesti utilizzando dati modificabili contestuali.
* **Dati persistenti** - Per ogni dato modificabile è presente un identificatore URN. Questo URL viene utilizzato per indirizzare la persistenza al sistema e alla risorsa giusti.

### Livello di persistenza {#persistence-layer}

* **Modello per frammento di contenuto** - Per supportare la barra laterale per la modifica delle proprietà dei frammenti di contenuto, dell’Editor frammento di contenuto e degli editor basati su moduli, sono necessari modelli per componente e frammento di contenuto.
* **Contenuto** - Il contenuto può essere archiviato ovunque, ad esempio in AEM, Magento, ecc.

![Livello di persistenza](assets/persistence-layer.png)

## Servizio di editor universale e invio del sistema di back-end {#service}

L’editor universale invia tutte le modifiche al contenuto in un servizio centralizzato denominato servizio dell’editor universale. Questo servizio, in esecuzione su Adobe I/O Runtime, carica i plug-in disponibili nel Registro estensioni in base all&#39;URL fornito. Il plug-in è responsabile della comunicazione al back-end e della restituzione di una risposta unificata.

![Servizio editor universale](assets/universal-editor-service.png)

## Pipeline di rendering {#rendering-pipelines}

### Rendering lato server {#server-side}

![Rendering lato server](assets/server-side.png)

### Generazione statica del sito {#static-generation}

![Generazione statica del sito](assets/static-generation.png)

### Rendering lato client {#client-side}

![Rendering lato client](assets/client-side.png)

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni sull’editor universale, consulta questi documenti.

* [Introduzione all’editor universale](introduction.md) - Scopri come l’editor universale consente di modificare qualsiasi aspetto di qualsiasi contenuto in qualsiasi implementazione per fornire esperienze eccezionali, velocizzare i contenuti e fornire un’esperienza di sviluppo all’avanguardia.
* [Creazione di contenuti con l’editor universale](authoring.md) - Scopri quanto è semplice e intuitivo per gli autori di contenuti creare contenuti utilizzando l’Editor universale.
* [Guida introduttiva all’Editor universale in AEM](getting-started.md) - Scopri come accedere all’editor universale e come iniziare a strumentalizzare la tua prima app AEM per utilizzarla.
* [Attributi e tipi](attributes-types.md) - Scopri gli attributi e i tipi di dati richiesti dall’Editor universale.
* [Autenticazione dell’editor universale](authentication.md) - Scopri come l’editor universale si autentica.
