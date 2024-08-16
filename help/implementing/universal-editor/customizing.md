---
title: Personalizzazione ed estensione dell’editor universale
description: Scopri i diversi punti di estensione e altre funzioni che consentono di personalizzare l’interfaccia utente di Universal Editor per soddisfare le esigenze degli autori di contenuti.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 34ae1d57e77e209e179aca5c556954dbfb170498
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 1%

---


# Personalizzazione ed estensione dell’editor universale {#customizing-extending}

Scopri i diversi punti di estensione e altre funzioni che consentono di personalizzare l’esperienza di authoring di Universal Editor per supportare le esigenze degli autori di contenuti.

## Panoramica {#overview}

L’editor universale consente due tipi di adattamento in base alle esigenze del progetto.

* [Personalizzazione dell&#39;editor universale](#customizing) - Le funzionalità standard dell&#39;editor universale possono essere adattate tramite diverse configurazioni di personalizzazione.
* [Estensione dell&#39;interfaccia utente dell&#39;editor universale](#extending) - È inoltre possibile estendere l&#39;interfaccia utente dell&#39;editor universale tramite App Builder per soddisfare le esigenze dei progetti.

Entrambi i tipi sono descritti nelle sezioni seguenti.

## Personalizzare l’Editor universale {#customizing}

Universal Editor offre diverse opzioni incorporate per personalizzarne le funzionalità.

### Disabilitazione della pubblicazione {#disable-publish}

Alcuni flussi di lavoro di authoring richiedono la revisione del contenuto prima della pubblicazione. In tali situazioni, l’opzione per pubblicare non deve essere disponibile per alcun autore.

Il pulsante **Publish** può quindi essere eliminato completamente in un&#39;app aggiungendo i metadati seguenti.

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```

### Filtraggio dei componenti {#filtering-components}

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

### Mostra e nascondi componenti in modo condizionale nella barra delle proprietà {#conditionally-hide}

Anche se uno o più componenti possono essere generalmente disponibili per gli autori, in alcune situazioni potrebbe non avere senso. In questi casi, è possibile nascondere i componenti nella barra delle proprietà aggiungendo un attributo `condition` ai campi [ del modello di componente.](/help/implementing/universal-editor/field-types.md#fields)

Le condizioni possono essere definite utilizzando lo schema [JsonLogic.](https://jsonlogic.com/) Se la condizione è true, il campo verrà visualizzato. Se la condizione è false, il campo verrà nascosto.

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

### URL di anteprima personalizzati {#custom-preview-urls}

Puoi specificare un URL di anteprima personalizzato tramite una metaconfigurazione `urn:adobe:aue:config:preview`, che si aprirà facendo clic sul pulsante **Apri pagina** nella barra degli strumenti in alto a destra dell&#39;editor [.](/help/sites-cloud/authoring/universal-editor/navigation.md#universal-editor-toolbar)

Questa opzione è particolarmente utile per le applicazioni con requisiti di anteprima specifici, ad esempio quelle [che utilizzano Edge Delivery Services con creazione WYSIWYG.](/help/edge/wysiwyg-authoring/authoring.md)

Per farlo, includi semplicemente l’URL di anteprima desiderato in un metatag dell’app instrumentata come nell’esempio seguente.

```html
<meta name="urn:adobe:aue:config:preview" content="https://wknd.site"/>
```

## Estensione dell’interfaccia utente dell’editor universale {#extending}

In qualità di servizio di Adobe Experience Cloud, l’interfaccia utente dell’editor universale può essere estesa utilizzando App Builder e Experience Manager.

Le estensioni dell’interfaccia utente sono applicazioni JavaScript create con Adobe App Builder che possono essere incorporate nelle applicazioni UI eseguite in Adobe Experience Cloud Unified Shell, ad esempio Universal Editor. Puoi aggiungere i tuoi pulsanti e le tue azioni al menu dell’intestazione e alla barra delle proprietà, nonché creare eventi personalizzati per Universal Editor.

Se desideri esplorare queste possibilità, consulta le seguenti risorse:

1. [Estensibilità interfaccia utente](https://developer.adobe.com/uix/docs/) - Questa è la documentazione per gli sviluppatori per l&#39;estensione dell&#39;interfaccia utente.
1. [Guide all&#39;estendibilità dell&#39;interfaccia utente](https://developer.adobe.com/uix/docs/guides/): istruzioni dettagliate su come sviluppare un&#39;estensione personalizzata
1. [Punti di estensione di Universal Editor](https://developer.adobe.com/uix/docs/services/aem-universal-editor/) - Documentazione del punto di estensione specifica di Universal Editor

>[!TIP]
>
>Se preferisci imparare da esempio, consulta l&#39;esercitazione sull&#39;estensibilità dell&#39;interfaccia utente dell&#39;AEM [.](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/developing/extensibility/ui/overview) Anche se si concentra sull&#39;estensione della console Frammenti di contenuto, i concetti per l&#39;implementazione di un&#39;estensione dell&#39;interfaccia utente nell&#39;editor universale sono gli stessi.

[Utilizzando Extension Manager in AEM Sites,](https://developer.adobe.com/uix/docs/extension-manager/) puoi abilitare o disabilitare le estensioni per singole istanze, accedere alle estensioni di prime parti di Adobe, incluse quelle per Universal Editor, e molto altro.
