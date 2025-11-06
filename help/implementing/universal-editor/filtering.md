---
title: Filtrare i componenti
description: Scopri come limitare i componenti consentiti per contenitore nell’editor universale, utilizzando i filtri dei componenti.
feature: Developing
role: Admin, Developer
exl-id: eeae8d7c-c563-4d9b-8c54-1098a4e98c18
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 100%

---

# Filtrare i componenti {#filtering-components}

Scopri come limitare i componenti consentiti per contenitore nell’editor universale, utilizzando i filtri dei componenti.

## Filtri {#filters}

Quando utilizzi l’editor universale, puoi limitare i componenti consentiti a livello di componente contenitore. A questo scopo, devi introdurre un tag di script aggiuntivo che punti alla definizione del filtro.

```html
<script type="application/vnd.adobe.aue.filter+json" src="/static/filter-definition.json"></script>
```

L&#39;esempio seguente è una definizione di filtro per limitare un contenitore alla sola aggiunta di testo e immagini.

```json
[
  {
    "id": "container-filter",
     "components": ["text", "image"]
   }
]
```

È quindi possibile fare riferimento alla definizione di filtro dal componente contenitore aggiungendo la proprietà `data-aue-filter`, passando l&#39;ID del filtro definito in precedenza.

```html
data-aue-filter="container-filter"
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

>[!TIP]
>
>Scopri altre opzioni di personalizzazione ed estensione disponibili per l’editor universale nei documenti:
>
>* [Personalizzare l’editor universale](/help/implementing/universal-editor/customizing.md)
>* [Navigazione nell’editor universale](/help/implementing/universal-editor/extending.md)
