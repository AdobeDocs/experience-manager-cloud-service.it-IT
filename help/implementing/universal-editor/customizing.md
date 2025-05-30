---
title: Personalizzare l’Editor universale
description: Scopri le diverse opzioni per personalizzare l’Editor universale in modo da supportare le esigenze degli autori di contenuti.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 98879fe30482e042da05a390e75d11c0adf7dba9
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 8%

---


# Personalizzare l’Editor universale {#customizing}

Scopri le diverse opzioni per personalizzare l’Editor universale in modo da supportare le esigenze degli autori di contenuti.

>[!TIP]
>
>Universal Editor offre anche molti [punti di estensione,](/help/implementing/universal-editor/extending.md) che ti consentono di espanderne le funzionalità per soddisfare le esigenze del progetto.

## Disabilitazione della pubblicazione {#disable-publish}

Alcuni flussi di lavoro di authoring richiedono la revisione del contenuto prima della pubblicazione. In tali situazioni, l’opzione per pubblicare non deve essere disponibile per alcun autore.

Il pulsante **Pubblica** può quindi essere eliminato completamente in un&#39;app aggiungendo i metadati seguenti.

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```

## Disabilitazione della pubblicazione in anteprima {#publish-preview}

Alcuni flussi di lavoro di authoring potrebbero impedire la pubblicazione nel [servizio di anteprima](/help/sites-cloud/authoring/sites-console/previewing-content.md) (se disponibile).

L&#39;opzione **Anteprima** nella finestra di pubblicazione può quindi essere soppressa completamente in un&#39;app aggiungendo i metadati seguenti.

```html
<meta name="urn:adobe:aue:config:disable" content="publish-preview"/>
```

## Filtrare i componenti {#filtering-components}

È possibile limitare i componenti consentiti per contenitore nell’Editor universale utilizzando i filtri dei componenti. Per ulteriori informazioni, vedere il documento [Componenti filtro](/help/implementing/universal-editor/filtering.md).

## Mostra e nascondi componenti in modo condizionale nel pannello Proprietà {#conditionally-hide}

Anche se uno o più componenti possono essere generalmente disponibili per gli autori, in alcune situazioni potrebbe non avere senso. In questi casi, è possibile nascondere i componenti nel pannello delle proprietà aggiungendo un attributo `condition` ai campi [ del modello di componente](/help/implementing/universal-editor/field-types.md#fields).

Le condizioni possono essere definite utilizzando lo schema [JsonLogic](https://jsonlogic.com/). Se la condizione è true, il campo viene visualizzato. Se la condizione è false, il campo verrà nascosto.

>[!BEGINTABS]

>[!TAB Modello di esempio]

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

>[!TAB Condizione False]

![Campo di testo nascosto](assets/hidden.png)

>[!TAB Condizione Vera]

![Campo di testo visualizzato](assets/shown.png)

>[!ENDTABS]

## URL di anteprima personalizzati {#custom-preview-urls}

È possibile specificare un URL di anteprima personalizzato tramite una metaconfigurazione `urn:adobe:aue:config:preview`, che verrà aperta quando si fa clic sul pulsante **Apri pagina** nella barra degli strumenti superiore destra dell&#39;editor [&#128279;](/help/sites-cloud/authoring/universal-editor/navigation.md#universal-editor-toolbar).

Ciò è particolarmente utile per le applicazioni con requisiti di anteprima specifici, ad esempio quelle [che utilizzano Edge Delivery Services con l’authoring WYSIWYG](/help/edge/wysiwyg-authoring/authoring.md).

Per farlo, includi semplicemente l’URL di anteprima desiderato in un metatag dell’app instrumentata come nell’esempio seguente.

```html
<meta name="urn:adobe:aue:config:preview" content="https://wknd.site"/>
```
