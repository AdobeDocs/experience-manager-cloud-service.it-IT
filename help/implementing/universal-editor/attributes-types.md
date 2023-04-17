---
title: Attributi e tipi
description: Scopri gli attributi e i tipi di dati richiesti dall’editor universale.
source-git-commit: 0e66c379e10d275610d85a699da272dc0c32a9a8
workflow-type: ht
source-wordcount: '661'
ht-degree: 100%

---


# Attributi e tipi {#attributes-types}

Scopri gli attributi e i tipi di dati richiesti dall’editor universale.

## Introduzione {#introduction}

Affinché un’app possa essere modificata dall’editor universale, deve essere dotata di strumentazione corretta. Ciò include l’inclusione dei metadati appropriati, in modo che l’editor possa modificare il contenuto dell’app. In questo documento vengono descritti gli attributi e i tipi di questi metadati.

>[!NOTE]
>
>La convalida del contenuto viene eseguita lato server. L’editor universale funziona semplicemente con gli attributi dei dati. La convalida che soddisfa il modello/struttura deve essere gestita a livello di API.

## Proprietà dati {#data-properties}

| Proprietà dati | Descrizione |
|---|---|
| `itemid` | Per l’URN della risorsa, consulta la sezione [Instrumenta la pagina del documento Guida introduttiva all’editor universale in AEM](getting-started.md#instrument-thepage) |
| `itemprop` | Per l’attributo della risorsa, consulta la sezione [Instrumenta la pagina del documento Guida introduttiva all’editor universale in AEM](getting-started.md#instrument-thepage) |
| `itemtype` | Tipo di elemento modificabile (ad esempio testo, immagine, riferimento, ecc.) |
| `data-editor-itemfilter` | Definisce quali riferimenti possono essere utilizzati |
| `data-editor-itemlabel` | Definisce un’etichetta personalizzata per un elemento selezionabile visualizzato nell’editor. <br>Nel caso in cui`itemmodel` sia impostata, l’etichetta viene recuperata tramite il modello. |
| `data-editor-itemmodel` | Definisce un modello che verrà utilizzato per la modifica basata su modulo nella barra delle proprietà |
| `data-editor-behavior` | Definisce il comportamento di una strumentazione, ad esempio testo o immagini indipendenti possono anche imitare un componente per renderlo mobile o eliminabile. |

## Tipi di elementi {#item-types}

| `itemtype` | Descrizione | `itemid` | `itemprop` | `data-editor-itemfilter` | `data-editor-itemlabel` | `data-editor-itemmodel` | `data-editor-behvior` |
|---|---|---|---|---|---|---|---|
| `text` | Il testo può essere modificato all’interno dei tag di HTML, ma solo in formato di testo semplice e non in formattazione RTF, cosa che, ad esempio, viene comunemente utilizzata nei componenti del titolo | Facoltativo | Obbligatorio | n/d | Facoltativo | n/d | Facoltativo |
| `richtext` | Il testo è modificabile utilizzando tutte le funzioni RTF. L’editor Rich Text (RTE) viene visualizzato nel pannello di destra | Facoltativo | Obbligatorio | n/d | Facoltativo | n/d | Facoltativo |
| `media` | L’elemento modificabile è una risorsa, ad esempio immagine o video | Facoltativo | Obbligatorio | Facoltativo<br>elenco di criteri di filtro per immagini o video trasmessi al selettore risorse | Facoltativo | n/d | Facoltativo |
| `container` | L’elemento modificabile si comporta come contenitore per i componenti, cioè come Sistema paragrafo. | Dipende <br>vedi sotto | Dipende <br>vedi sotto | Facoltativo<br>un elenco di componenti consentiti | Facoltativo | n/d | n/d |
| `component` | L’elemento modificabile è un componente. Non aggiunge ulteriori funzionalità, sarà necessario per indicare parti mobili/eliminabili del DOM e per aprire la barra delle proprietà e i relativi campi | Obbligatorio | n/d | n/d | Facoltativo | Facoltativo | n/d |
| `reference` | L’elemento modificabile è un riferimento, ad esempio frammento di contenuto, frammento di esperienza o prodotto. | Dipende <br>vedi sotto | Dipende <br>vedi sotto | Facoltativo<br>elenco di criteri di filtro per frammento di contenuto, prodotto o frammento di esperienza trasmessi al selettore di riferimento | Facoltativo | Facoltativo | n/d |

A seconda del caso d’uso `itemprop` o `itemid` può essere richiesto o meno. Ad esempio:

* `itemid` è richiesto se esegui una query sui frammenti di contenuto tramite GraphQL e desideri rendere l’elenco modificabile nel contesto.
* `itemprop` è richiesto se un componente esegue il rendering del contenuto di un frammento di contenuto a cui si fa riferimento e si desidera aggiornare il riferimento all’interno del componente.

## Comportamenti {#behaviors}

| `data-editor-behavior` | Descrizione |
|---|---|
| `component` | Può essere utilizzato per consentire ai componenti di testo indipendente, RTF e di mimica dei contenuti multimediali di essere anche mobili e eliminabili nella pagina |

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni sull’editor universale, consulta questi documenti.

* [Introduzione all’editor universale](introduction.md): scopri come l’editor universale consente di modificare qualsiasi aspetto di qualsiasi contenuto in qualsiasi implementazione per fornire esperienze eccezionali, aumentare la velocità del contenuto e fornire un’esperienza di sviluppo all’avanguardia.
* [Authoring dei contenuti con l’editor universale](authoring.md): scopri quanto è semplice e intuitivo per gli autori di contenuto creare contenuto utilizzando l’editor universale.
* [Pubblicazione di contenuto con l’editor universale](publishing.md): scopri in che modo l’editor visivo universale pubblica il contenuto e come le app possono gestire il contenuto pubblicato.
* [Guida introduttiva all’editor universale in AEM](getting-started.md): scopri come accedere all’editor universale e come iniziare a instrumentare la prima app AEM per utilizzarla.
* [Architettura dell’editor universale](architecture.md): scopri l’architettura dell’editor universale e come avviene il flusso di dati tra i suoi servizi e livelli.
* [Autenticazione dell’editor universale](authentication.md): scopri come l’editor universale effettua l’autenticazione.
