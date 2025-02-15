---
title: Attributi e tipi di elementi
description: Scopri gli attributi di dati e i tipi di elementi richiesti dall’editor universale.
exl-id: 02795a31-244a-42b4-8297-2649125d7777
feature: Developing
role: Admin, Architect, Developer
source-git-commit: edef86c67becf3b8094196d39baa9e69d6c81777
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 46%

---


# Attributi e tipi {#attributes-types}

Scopri gli attributi di dati e i tipi di elementi richiesti dall’editor universale.

## Introduzione {#introduction}

Affinché un’app possa essere modificata dall’editor universale, deve essere dotata di strumentazione corretta. Ciò include l’inclusione dei metadati appropriati, in modo che l’editor possa modificare il contenuto dell’app. Questo documento descrive gli attributi e i tipi di elementi di tali metadati.

>[!NOTE]
>
>La convalida del contenuto viene eseguita lato server. L’editor universale funziona semplicemente con gli attributi dei dati. La verifica della loro conformità al modello/struttura deve essere effettuata a livello di API.

## Proprietà dati {#data-properties}

| Proprietà dati | Descrizione |
|---|---|
| `data-aue-resource` | Per l’URN della risorsa, consulta la sezione [Instrumenta la pagina del documento Guida introduttiva all’editor universale in AEM](getting-started.md#instrument-thepage) |
| `data-aue-prop` | Per l’attributo della risorsa, consulta la sezione [Instrumenta la pagina del documento Guida introduttiva all’editor universale in AEM](getting-started.md#instrument-thepage) |
| `data-aue-type` | [Tipo di elemento modificabile](#item-types) (ad esempio testo, immagine e riferimento) |
| `data-aue-filter` | Definisce:<br>- Quali funzionalità dell&#39;editor Rich Text sono abilitate<br>- Quali componenti possono essere aggiunti a un contenitore<br>- Quali risorse possono essere aggiunte a un tipo di supporto |
| `data-aue-label` | Definisce un’etichetta personalizzata per un elemento selezionabile che viene visualizzata nell’editor |
| `data-aue-model` | Definisce un modello utilizzato per la modifica basata su modulo nel pannello delle proprietà |
| `data-aue-behavior` | Definisce il comportamento [di una strumentazione](#behaviors). Ad esempio, testo o immagine autonomi possono simulare un componente per renderlo spostabile o eliminabile |

## Tipi di elementi {#item-types}

| `data-aue-type` | Descrizione | `data-aue-resource` | `data-aue-prop` | `data-aue-filter` | `data-aue-label` | `data-aue-model` | `data-aue-behavior` |
|---|---|---|---|---|---|---|---|
| `text` | Il testo può essere modificato all’interno dei tag di HTML, ma solo in formato di testo semplice e non in formattazione RTF, cosa che, ad esempio, viene comunemente utilizzata nei componenti del titolo | Facoltativo | Obbligatorio | n/d | Facoltativo | n/d | Facoltativo |
| `richtext` | Il testo è modificabile utilizzando tutte le funzioni RTF. L’editor Rich Text (RTE) viene visualizzato nel pannello di destra | Facoltativo | Obbligatorio | n/d | Facoltativo | n/d | Facoltativo |
| `media` | L’elemento modificabile è una risorsa, ad esempio immagine o video | Facoltativo | Obbligatorio | Facoltativo<br>elenco di criteri di filtro per immagini o video trasmessi al selettore risorse | Facoltativo | n/d | Facoltativo |
| `container` | L’elemento modificabile si comporta come contenitore per i componenti, cioè come Sistema paragrafo. | Dipende <br>vedi sotto | Dipende <br>vedi sotto | Facoltativo<br>un elenco di componenti consentiti | Facoltativo | n/d | n/d |
| `component` | L’elemento modificabile è un componente. Non aggiunge ulteriori funzionalità. È necessario per indicare parti mobili/eliminabili del DOM e per aprire il pannello delle proprietà e i relativi campi | Obbligatorio | n/d | n/d | Facoltativo | Facoltativo | n/d |
| `reference` | L’elemento modificabile è un riferimento, ad esempio Frammento di contenuto, Frammento di esperienza o Prodotto | Dipende <br>vedi sotto | Dipende <br>vedi sotto | Facoltativo<br>elenco di criteri di filtro per frammento di contenuto, prodotto o frammento di esperienza trasmessi al selettore di riferimento | Facoltativo | Facoltativo | n/d |

`data-aue-resource` è sempre obbligatorio in quanto è la chiave primaria che indica dove vengono scritte le modifiche apportate al contenuto.

* Non è richiesta direttamente sul tag in cui è impostato `data-aue-type`.
* Se non è impostato, verrà utilizzato l&#39;attributo `data-aue-resource` dell&#39;elemento padre più vicino.

`data-aue-prop` è obbligatorio ogni volta che si desidera eseguire una modifica nel contesto del, ad eccezione di un contenitore in cui è facoltativo (se impostato, il contenitore è un frammento di contenuto e il prop punta a un campo con più riferimenti).

* `data-aue-prop` è l&#39;attributo da aggiornare per la chiave primaria di `data-aue-resource`.

## Comportamenti {#behaviors}

| `data-aue-behavior` | Descrizione |
|---|---|
| `component` | Utilizzato per consentire l’utilizzo di componenti di testo, testo RTF e mimica multimediale autonomi in modo che possano essere spostati ed eliminabili nella pagina |
| `container` | Utilizzato per consentire ai contenitori di essere trattati come componenti propri in modo che siano spostabili ed eliminabili sulla pagina |
