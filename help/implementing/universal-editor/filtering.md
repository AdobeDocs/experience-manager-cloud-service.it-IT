---
title: Filtraggio dei componenti
description: Scopri come limitare i componenti consentiti per contenitore nell’Editor universale utilizzando i filtri dei componenti.
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 48c1a109c060db4ce19bf645723357008d51c572
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---


# Filtraggio dei componenti {#filtering-components}

Scopri come limitare i componenti consentiti per contenitore nell’Editor universale utilizzando i filtri dei componenti.

## Filtri {#filters}

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

È quindi possibile fare riferimento alla definizione del filtro dal componente contenitore aggiungendo la proprietà `data-aue-filter`, passando l&#39;ID del filtro definito in precedenza.

```html
data-aue-filter="container-filter"
```

L&#39;impostazione dell&#39;attributo `components` in una definizione di filtro su `null` consente tutti i componenti, come se non ci fosse alcun filtro.

```json
[
  {
    "id": "another-container-filter",
     "components": null
   }
]
```

>[!TIP]
>
>Scopri le altre opzioni di personalizzazione ed estensione disponibili per l&#39;editor universale nel documento [Personalizzazione ed estensione dell&#39;editor universale.](/help/implementing/universal-editor/customizing.md)