---
title: Attributi e tipi di elementi
description: Scopri gli attributi e i tipi di dati richiesti dall’editor universale.
exl-id: 02795a31-244a-42b4-8297-2649125d7777
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 597315a7d569ebd62243322c543627b7a3535a6b
workflow-type: ht
source-wordcount: '554'
ht-degree: 100%

---


# Attributi e tipi {#attributes-types}

Scopri gli attributi e i tipi di dati richiesti dall’editor universale.

## Introduzione {#introduction}

Affinché un’app possa essere modificata dall’editor universale, deve essere dotata di strumentazione corretta. Ciò include l’inclusione dei metadati appropriati, in modo che l’editor possa modificare il contenuto dell’app. In questo documento vengono descritti nel dettaglio gli attributi e i tipi di questi metadati.

>[!NOTE]
>
>La convalida del contenuto viene eseguita lato server. L’editor universale funziona semplicemente con gli attributi dei dati. La convalida della rispettiva conformità al modello/struttura deve essere gestita a livello di API.

## Proprietà dati {#data-properties}

| Proprietà dati | Descrizione |
|---|---|
| `data-aue-resource` | Per l’URN della risorsa, consulta la sezione [Instrumenta la pagina del documento Guida introduttiva all’editor universale in AEM](getting-started.md#instrument-thepage) |
| `data-aue-prop` | Per l’attributo della risorsa, consulta la sezione [Instrumenta la pagina del documento Guida introduttiva all’editor universale in AEM](getting-started.md#instrument-thepage) |
| `data-aue-type` | [Tipo dell’elemento modificabile](#item-types) (ad esempio testo, immagine e riferimento) |
| `data-aue-filter` | Definisce:<br> - Quali funzionalità dell’editor Rich Text sono abilitate<br> - Quali componenti possono essere aggiunti a un contenitore<br> - Quali risorse possono essere aggiunte a un tipo di file multimediale |
| `data-aue-label` | Definisce un’etichetta personalizzata per un elemento selezionabile che viene visualizzata nell’editor |
| `data-aue-model` | Definisce un modello che viene utilizzato per la modifica basata su modulo nella barra delle proprietà |
| `data-aue-behavior` | Obsoleto. Una volta che è stato definito il comportamento di una strumentazione per consentire a testo, Rich Text e file multimediali autonomi di riprodurre i componenti in modo che possano essere spostati ed eliminati nella pagina, offrendo un unico valore potenziale di `component`. Questa proprietà viene ora ignorata e quando un elemento con `data-aue-resource` è figlio diretto di un contenitore viene automaticamente considerato un componente. |

## Tipi di elementi {#item-types}

| `data-aue-type` | Descrizione | `data-aue-resource` | `data-aue-prop` | `data-aue-filter` | `data-aue-label` | `data-aue-model` |
|---|---|---|---|---|---|---|
| `text` | Il testo può essere modificato all’interno dei tag di HTML, ma solo in formato di testo semplice e non in formattazione RTF, cosa che, ad esempio, viene comunemente utilizzata nei componenti del titolo | Facoltativo | Obbligatorio | n/d | Facoltativo | n/d |
| `richtext` | Il testo è modificabile utilizzando tutte le funzionalità di formattazione complete. L’editor Rich Text (RTE) viene visualizzato nel pannello di destra | Facoltativo | Obbligatorio | n/d | Facoltativo | n/d |
| `media` | L’elemento modificabile è una risorsa, ad esempio immagine o video | Facoltativo | Obbligatorio | Facoltativo<br>elenco di criteri di filtro per immagini o video trasmessi al selettore risorse | Facoltativo | n/d |
| `container` | L’elemento modificabile si comporta come contenitore per i componenti, cioè come Sistema paragrafo. | Dipende <br>vedi sotto | Dipende <br>vedi sotto | Facoltativo<br>un elenco di componenti consentiti | Facoltativo | n/d |
| `component` | L’elemento modificabile è un componente. Non aggiunge ulteriori funzionalità. È necessario per indicare parti mobili/eliminabili del DOM e per aprire il pannello delle proprietà e i relativi campi | Obbligatorio | n/d | n/d | Facoltativo | Facoltativo |
| `reference` | L’elemento modificabile è un riferimento, ad esempio frammento di contenuto, frammento di esperienza o prodotto | Dipende <br>vedi sotto | Dipende <br>vedi sotto | Facoltativo<br>elenco di criteri di filtro per frammento di contenuto, prodotto o frammento di esperienza trasmessi al selettore di riferimento | Facoltativo | Facoltativo |

`data-aue-resource` è sempre obbligatorio in quanto è la chiave primaria che indica dove vengono scritte le modifiche apportate al contenuto.

* Non è richiesta direttamente sul tag in cui è impostato il `data-aue-type`.
* Se non è impostato, verrà utilizzato l’attributo `data-aue-resource` dell’elemento principale più vicino.

`data-aue-prop` è obbligatorio ogni volta che si desidera apportare delle modifiche al contesto, ad eccezione di un contenitore in cui è facoltativo (se impostato, il contenitore è un frammento di contenuto e la proprietà punta a un campo con più riferimenti).

* La `data-aue-prop` è l’attributo per aggiornare la chiave primaria di `data-aue-resource`.
