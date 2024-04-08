---
title: Personalizzazione dell’esperienza di authoring di Universal Editor
description: Scopri i diversi punti di estensione e altre funzioni che consentono di personalizzare l’interfaccia utente di Universal Editor per soddisfare le esigenze degli autori di contenuti.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
source-git-commit: 11a244b7dd4810fbfec92b3effc362102e7322dc
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%

---


# Personalizzazione dell’esperienza di authoring di Universal Editor {#customizing-ue}

Scopri i diversi punti di estensione e altre funzioni che consentono di personalizzare l’esperienza di authoring di Universal Editor per supportare le esigenze degli autori di contenuti.

## Disabilitazione della pubblicazione {#disable-publish}

Alcuni flussi di lavoro di authoring richiedono la revisione del contenuto prima della pubblicazione. In tali situazioni, l’opzione per pubblicare non deve essere disponibile per alcun autore.

Il **Pubblica** può quindi essere soppresso completamente in un’app aggiungendo i seguenti metadati.

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```

## Filtraggio dei componenti {#filtering-components}

Quando utilizzi l’Editor universale, puoi limitare i componenti consentiti per componente contenitore. A questo scopo, devi introdurre un tag script aggiuntivo che punti alla definizione del filtro.

```html
<script type="application/vnd.adobe.aue.filter+json" src="/static/filter-definition.json"></script>
```

Una definizione di filtro potrebbe avere un aspetto simile al seguente, il che impedirebbe a un contenitore di aggiungere solo testo e immagini.

```json
[
  {
    "id": "container-filter",
     "components": ["text", "image"]
   }
]
```

Puoi quindi fare riferimento alla definizione del filtro dal componente contenitore aggiungendo la proprietà `data-aue-filter`, passando l’ID del filtro definito in precedenza.

```html
data-aue-filter="container-filter"
```

Impostazione di `components` attributo in una definizione di filtro a `null` consente tutti i componenti, come se non ci fosse alcun filtro.

```json
[
  {
    "id": "another-container-filter",
     "components": null
   }
]
```

## Mostra e nascondi componenti in modo condizionale nella barra delle proprietà {#conditionally-hide}

Anche se uno o più componenti possono essere generalmente disponibili per gli autori, in alcune situazioni potrebbe non avere senso. In questi casi, puoi nascondere i componenti nella barra delle proprietà aggiungendo un `condition` attribuire a [del modello di componente.](/help/implementing/universal-editor/field-types.md#fields)

Le condizioni possono essere definite utilizzando [Schema JsonLogic.](https://jsonlogic.com/) Se la condizione è true, il campo viene visualizzato. Se la condizione è false, il campo verrà nascosto.

### Modello di esempio {#sample-model}

```json
 {
    "id": "conditionally-revealed-component",
    "fields": [
      {
        "component": "boolean",
        "label": "Shall the text field be revealed?",
        "name": "reveal",
        "valueType": "boolean"
      },
      {
        "component": "text-input",
        "label": "Hidden text field",
        "name": "hidden-text",
        "valueType": "string",
        "condition": { "===": [{"var" : "reveal"}, true] }
      }
    ]
 }
```

#### Condizione False {#false}

![Campo di testo nascosto](assets/hidden.png)

#### Condition True {#true}

![Campo di testo visualizzato](assets/shown.png)

