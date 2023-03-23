---
title: Attributi e tipi
description: Scopri gli attributi e i tipi di dati richiesti da Universal Editor.
source-git-commit: 0e66c379e10d275610d85a699da272dc0c32a9a8
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 7%

---


# Attributi e tipi {#attributes-types}

Scopri gli attributi e i tipi di dati richiesti da Universal Editor.

## Introduzione {#introduction}

Affinché un’app possa essere modificata dall’editor universale, deve essere strumentata correttamente. Ciò include l&#39;inclusione dei metadati appropriati, in modo che l&#39;editor possa modificare il contenuto dell&#39;app. In questo documento vengono descritti gli attributi e i tipi di metadati.

>[!NOTE]
>
>La convalida del contenuto viene eseguita sul lato server. L’editor universale funziona semplicemente con gli attributi dei dati. La convalida che soddisfa il modello/struttura deve essere gestita a livello di API.

## Proprietà dati {#data-properties}

| Proprietà dati | Descrizione |
|---|---|
| `itemid` | Eseguire l’URL della risorsa, consulta la sezione . [Strumento la pagina del documento Guida introduttiva all&#39;editor universale in AEM](getting-started.md#instrument-thepage) |
| `itemprop` | Attributo della risorsa, consulta la sezione . [Strumento la pagina del documento Guida introduttiva all&#39;editor universale in AEM](getting-started.md#instrument-thepage) |
| `itemtype` | Tipo di elemento modificabile (ad esempio testo, immagine, riferimento, ecc.) |
| `data-editor-itemfilter` | Definisce quali riferimenti possono essere utilizzati |
| `data-editor-itemlabel` | Definisce un&#39;etichetta personalizzata per un elemento selezionabile visualizzato nell&#39;editor <br>Nel caso `itemmodel` è impostata, l’etichetta viene recuperata tramite il modello |
| `data-editor-itemmodel` | Definisce un modello che verrà utilizzato per la modifica basata su modulo nella barra delle proprietà |
| `data-editor-behavior` | Definisce il comportamento di una strumentazione, ad esempio il testo o l&#39;immagine stand alone può anche imitare un componente per renderlo mobile o detraibile |

## Tipi di articoli {#item-types}

| `itemtype` | Descrizione | `itemid` | `itemprop` | `data-editor-itemfilter` | `data-editor-itemlabel` | `data-editor-itemmodel` | `data-editor-behvior` |
|---|---|---|---|---|---|---|---|
| `text` | Il testo può essere modificato all’interno dei tag di HTML, ma solo in formato testo semplice, senza formattazione RTF disponibile, questo viene comunemente utilizzato nei componenti titolo, ad esempio | Facoltativo | Obbligatorio | n/d | Facoltativo | n/d | Facoltativo |
| `richtext` | Il testo è modificabile con funzionalità Rich Text. L’editor Rich Text viene visualizzato nel pannello di destra | Facoltativo | Obbligatorio | n/d | Facoltativo | n/d | Facoltativo |
| `media` | Il modificabile è una risorsa, ad esempio immagine o video | Facoltativo | Obbligatorio | Facoltativo<br>elenco di criteri di filtro immagini o video passati al selettore risorse | Facoltativo | n/d | Facoltativo |
| `container` | Il modificabile si comporta come contenitore per i componenti, come Sistema paragrafo. | Dipende <br>vedi sotto | Dipende <br>vedi sotto | Facoltativo<br>un elenco dei componenti consentiti | Facoltativo | n/d | n/d |
| `component` | Il modificabile è un componente. Non aggiunge funzionalità aggiuntive, sarà necessario per indicare parti mobili/eliminabili del DOM e per aprire la barra delle proprietà e i relativi campi | Obbligatorio | n/d | n/d | Facoltativo | Facoltativo | n/d |
| `reference` | La modificabile è un riferimento, ad esempio frammento di contenuto, frammento di esperienza o prodotto | Dipende <br>vedi sotto | Dipende <br>vedi sotto | Facoltativo<br>elenco di criteri di filtro per frammenti di contenuto, prodotti o frammenti esperienza passati al selettore di riferimento | Facoltativo | Facoltativo | n/d |

A seconda del caso d’uso `itemprop` o `itemid` può essere richiesto o meno. Esempio:

* `itemid` è richiesto se esegui una query sui frammenti di contenuto tramite GraphQL e desideri rendere l’elenco modificabile nel contesto.
* `itemprop` è richiesto se un componente esegue il rendering del contenuto di un frammento di contenuto a cui si fa riferimento e si desidera aggiornare il riferimento all’interno del componente.

## Comportamenti {#behaviors}

| `data-editor-behavior` | Descrizione |
|---|---|
| `component` | Può essere utilizzato per consentire ai componenti di testo indipendente, richtext e mimica dei contenuti multimediali di essere spostabili e modificabili anche sulla pagina |

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni sull’editor universale, consulta questi documenti.

* [Introduzione all’editor universale](introduction.md) - Scopri come l’editor universale consente di modificare qualsiasi aspetto di qualsiasi contenuto in qualsiasi implementazione per fornire esperienze eccezionali, velocizzare i contenuti e fornire un’esperienza di sviluppo all’avanguardia.
* [Creazione di contenuti con l’editor universale](authoring.md) - Scopri quanto è semplice e intuitivo per gli autori di contenuti creare contenuti utilizzando l’Editor universale.
* [Pubblicazione di contenuti con l’editor universale](publishing.md) - Scopri in che modo Universal Visual Editor pubblica i contenuti e come le tue app possono gestire i contenuti pubblicati.
* [Guida introduttiva all’Editor universale in AEM](getting-started.md) - Scopri come accedere all’editor universale e come iniziare a strumentalizzare la tua prima app AEM per utilizzarla.
* [Architettura dell’editor universale](architecture.md) - Scopri l’architettura dell’Editor universale e il flusso di dati tra i suoi servizi e livelli.
* [Autenticazione dell’editor universale](authentication.md) - Scopri come l’editor universale si autentica.
