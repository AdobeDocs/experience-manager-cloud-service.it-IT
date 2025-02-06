---
title: Personalizzazione ed estensione dell’editor universale
description: Scopri i diversi punti di estensione e altre funzioni che consentono di personalizzare l’interfaccia utente di Universal Editor per soddisfare le esigenze degli autori di contenuti.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '579'
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

### Filtrare i componenti {#filtering-components}

È possibile limitare i componenti consentiti per contenitore nell’Editor universale utilizzando i filtri dei componenti. Per ulteriori informazioni, vedere il documento [Componenti filtro](/help/implementing/universal-editor/filtering.md).

### Mostra e nascondi componenti in modo condizionale nel pannello Proprietà {#conditionally-hide}

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

### URL di anteprima personalizzati {#custom-preview-urls}

È possibile specificare un URL di anteprima personalizzato tramite una metaconfigurazione `urn:adobe:aue:config:preview`, che verrà aperta quando si fa clic sul pulsante **Apri pagina** nella barra degli strumenti superiore destra dell&#39;editor [](/help/sites-cloud/authoring/universal-editor/navigation.md#universal-editor-toolbar).

Questo è particolarmente utile per le applicazioni con requisiti di anteprima specifici, ad esempio quelle [che utilizzano Edge Delivery Services con l&#39;authoring di WYSIWYG](/help/edge/wysiwyg-authoring/authoring.md).

Per farlo, includi semplicemente l’URL di anteprima desiderato in un metatag dell’app instrumentata come nell’esempio seguente.

```html
<meta name="urn:adobe:aue:config:preview" content="https://wknd.site"/>
```

## Estensione dell’interfaccia utente dell’editor universale {#extending}

In qualità di servizio di Adobe Experience Cloud, l’interfaccia utente dell’editor universale può essere estesa utilizzando App Builder e Experience Manager.

Le estensioni dell’interfaccia utente sono applicazioni JavaScript create con Adobe App Builder che possono essere incorporate in applicazioni UI eseguite in Adobe Experience Cloud Unified Shell, ad esempio Universal Editor. Puoi aggiungere pulsanti e azioni personalizzati al menu e al pannello delle proprietà dell’intestazione, nonché creare eventi personalizzati per Universal Editor.

Se desideri esplorare queste possibilità, consulta le seguenti risorse:

1. [Estensibilità interfaccia utente](https://developer.adobe.com/uix/docs/) - Questa è la documentazione per gli sviluppatori per l&#39;estensione dell&#39;interfaccia utente.
1. [Guide all&#39;estendibilità dell&#39;interfaccia utente](https://developer.adobe.com/uix/docs/guides/): istruzioni dettagliate su come sviluppare un&#39;estensione personalizzata
1. [Punti di estensione di Universal Editor](https://developer.adobe.com/uix/docs/services/aem-universal-editor/) - Documentazione del punto di estensione specifica di Universal Editor

>[!TIP]
>
>Se preferisci imparare da esempio, consulta l&#39;[esercitazione sull&#39;estensibilità dell&#39;interfaccia utente dell&#39;AEM](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/developing/extensibility/ui/overview). Anche se si concentra sull’estensione della console Frammenti di contenuto, i concetti per l’implementazione di un’estensione dell’interfaccia utente nell’Editor universale sono gli stessi.

[Utilizzando Extension Manager in AEM Sites](https://developer.adobe.com/uix/docs/extension-manager/), puoi abilitare o disabilitare le estensioni per singole istanze, accedere alle estensioni di prime parti di Adobe, incluse quelle per Universal Editor, e molto altro.
