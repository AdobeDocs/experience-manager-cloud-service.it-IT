---
title: Personalizzazione dell’interfaccia utente
description: Scopri i diversi punti di estensione che ti consentono di personalizzare l’interfaccia utente di Universal Editor per supportare le esigenze degli autori di contenuti.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
source-git-commit: 1bc65e65e6ce074a050e21137ce538b5c086665f
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---


# Personalizzazione dell’interfaccia utente {#customizing-ui}

Scopri i diversi punti di estensione che ti consentono di personalizzare l’interfaccia utente di Universal Editor per supportare le esigenze degli autori di contenuti.

## Disabilitazione della pubblicazione {#disable-publish}

Alcuni flussi di lavoro di authoring richiedono la revisione del contenuto prima della pubblicazione. In tali situazioni, l’opzione per pubblicare non deve essere disponibile per alcun autore.

Il **Pubblica** Il pulsante può quindi essere eliminato completamente in un’app aggiungendo i seguenti metadati.

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
