---
title: Filtri
description: Scopri come definire i filtri per limitare le opzioni disponibili nell’editor, ad esempio i componenti disponibili, le opzioni dell’editor Rich Text e la selezione delle risorse.
feature: Developing
role: Admin, Developer
exl-id: eeae8d7c-c563-4d9b-8c54-1098a4e98c18
source-git-commit: 8d9d162ec5bba99afb1ae86252a49a9880be4e68
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 15%

---


# Filtri {#filters}

Scopri come definire i filtri per limitare le opzioni disponibili nell’editor, ad esempio i componenti disponibili, le opzioni dell’editor Rich Text e la selezione delle risorse.

## Configurazione dei filtri {#configuring-filters}

Quando si utilizza l’Editor universale, è possibile limitare le opzioni consentite per determinate funzionalità definendo un filtro. Un filtro è un elenco di elementi o azioni disponibili per il contesto specifico. Ad esempio, puoi filtrare i componenti disponibili per l&#39;inserimento in un contenitore, [filtrare le opzioni disponibili nell&#39;editor Rich Text](/help/implementing/universal-editor/configure-rte.md) e [filtrare le risorse disponibili](/help/implementing/universal-editor/configure-assets-selector.md) nel selettore delle risorse.

Tutti i filtri devono essere definiti in modo simile.

1. [Aggiungi tag script per puntare alla definizione del filtro](#add-tag)
1. [Definire il filtro](#define-filter)
1. [Fai riferimento al filtro](#reference-filter)

Prendiamo un esempio di filtraggio dei componenti per componente contenitore.

## Definizione filtro di riferimento {#add-tag}

Introduce innanzitutto un tag script aggiuntivo, che punta alla definizione del filtro.

Nel nostro esempio, per filtrare i componenti consentiti per contenitore, il tag potrebbe essere simile al seguente.

```html
<script type="application/vnd.adobe.aue.filter+json" src="/static/filter-definition.json"></script>
```

## Definire il filtro {#define-filter}

Una definizione di filtro contiene JSON con un ID univoco per il filtro e i criteri di filtro.

Per filtrare i componenti consentiti per contenitore, nell’esempio potrebbe presentarsi l’aspetto seguente, che limita la possibilità di aggiungere solo testo e immagini in un contenitore.

```json
[
  {
    "id": "container-filter",
    "components": ["text", "image"]
   }
]
```

In una definizione di filtro, se l’attributo `components` viene impostato su `null`, vengono consentiti tutti i componenti, come se non ci fosse alcun filtro.

```json
[
  {
    "id": "another-container-filter",
     "components": null
   }
]
```

## Fai riferimento al filtro {#reference-filter}

Per utilizzare il filtro, è necessario fare riferimento alla definizione del filtro. Per farlo, segui questi passaggi:

* Facendo riferimento al filtro dal componente contenitore aggiungendo la proprietà `data-aue-filter`, viene passato l&#39;ID del filtro.

  ```html
  data-aue-filter="container-filter"
  ```

* Facendo riferimento al filtro dalla definizione del componente [, ](/help/implementing/universal-editor/component-definition.md) passa l&#39;ID del filtro.

  ```json
  {
     "title":"My Container",
     "id":"my-container",
     "model": "my-model",
     "filter": "container-filter",
     ...
  }
  ```

## Risorse aggiuntive {#additional-resources}

Scopri altre opzioni di personalizzazione ed estensione disponibili per l’editor universale nei documenti:

* [Configurazione dell’editor Rich Text per l’editor universale](/help/implementing/universal-editor/configure-rte.md)
* [Configurazione dei filtri per il selettore Assets](/help/implementing/universal-editor/configure-assets-selector.md)
* [Personalizzazione dell’editor universale](/help/implementing/universal-editor/customizing.md)
* [Estensione dell’editor universale](/help/implementing/universal-editor/extending.md)
