---
title: Personalizzazione ed estensione dell’editor universale
description: Scopri i diversi punti di estensione e altre funzioni che consentono di personalizzare l’interfaccia utente di Universal Editor per soddisfare le esigenze degli autori di contenuti.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
source-git-commit: bdd67fb383bf20399eacaf9b9c086ea8468ea742
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 1%

---


# Personalizzazione ed estensione dell’editor universale {#customizing-extending}

Scopri i diversi punti di estensione e altre funzioni che consentono di personalizzare l’esperienza di authoring di Universal Editor per supportare le esigenze degli autori di contenuti.

## Panoramica {#overview}

L’editor universale consente due tipi di adattamento in base alle esigenze del progetto.

* [Personalizzazione dell’editor universale](#customizing) - La funzionalità standard di Universal Editor può essere adattata tramite diverse configurazioni di personalizzazione.
* [Estensione dell’interfaccia utente dell’editor universale](#extending) - L’interfaccia utente dell’Editor universale può essere estesa utilizzando App Builder per soddisfare le esigenze dei progetti.

Entrambi i tipi sono descritti nelle sezioni seguenti.

## Personalizzare l’Editor universale {#customizing}

Universal Editor offre diverse opzioni incorporate per personalizzarne le funzionalità.

### Disabilitazione della pubblicazione {#disable-publish}

Alcuni flussi di lavoro di authoring richiedono la revisione del contenuto prima della pubblicazione. In tali situazioni, l’opzione per pubblicare non deve essere disponibile per alcun autore.

Il **Pubblica** può quindi essere soppresso completamente in un’app aggiungendo i seguenti metadati.

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

### Mostra e nascondi componenti in modo condizionale nella barra delle proprietà {#conditionally-hide}

Anche se uno o più componenti possono essere generalmente disponibili per gli autori, in alcune situazioni potrebbe non avere senso. In questi casi, puoi nascondere i componenti nella barra delle proprietà aggiungendo un `condition` attribuire a [del modello di componente.](/help/implementing/universal-editor/field-types.md#fields)

Le condizioni possono essere definite utilizzando [Schema JsonLogic.](https://jsonlogic.com/) Se la condizione è true, il campo viene visualizzato. Se la condizione è false, il campo verrà nascosto.

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

>[!TAB Condition True]

![Campo di testo visualizzato](assets/shown.png)

>[!ENDTABS]

## Estensione dell’interfaccia utente dell’editor universale {#extending}

In qualità di servizio di Adobe Experience Cloud, l’interfaccia utente dell’editor universale può essere estesa utilizzando App Builder e Experience Manager.

Le estensioni dell’interfaccia utente sono applicazioni JavaScript create con Adobe App Builder che possono essere incorporate nelle applicazioni dell’interfaccia utente eseguite in Adobe Experience Cloud Unified Shell, ad esempio Universal Editor. Puoi aggiungere i tuoi pulsanti e le tue azioni al menu dell’intestazione e alla barra delle proprietà, nonché creare eventi personalizzati per Universal Editor.

Se desideri esplorare queste possibilità, consulta le seguenti risorse:

1. [Estensibilità dell’interfaccia utente](https://developer.adobe.com/uix/docs/) : questa è la documentazione per gli sviluppatori relativa all’estensione dell’interfaccia utente.
1. [Guide all’estensibilità dell’interfaccia utente](https://developer.adobe.com/uix/docs/guides/) - Istruzioni dettagliate su come sviluppare un’estensione personalizzata
1. [Punti di estensione di Universal Editor](https://developer.adobe.com/uix/docs/services/aem-universal-editor/) - Documentazione del punto di estensione specifico per l’editor universale

>[!TIP]
>
>Se preferisci imparare con un esempio, consulta la sezione [Esercitazione sull’estensibilità dell’interfaccia utente dell’AEM.](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/developing/extensibility/ui/overview) Anche se si concentra sull’estensione della console Frammenti di contenuto, i concetti per l’implementazione di un’estensione dell’interfaccia utente nell’Editor universale sono gli stessi.

[Utilizzando Extension Manager in AEM Sites,](https://developer.adobe.com/uix/docs/extension-manager/) puoi abilitare o disabilitare le estensioni per singole istanze, accedere alle estensioni di prime parti di Adobe, comprese quelle per Universal Editor e molto altro.
