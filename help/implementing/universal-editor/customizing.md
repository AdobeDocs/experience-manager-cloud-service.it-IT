---
title: Personalizzare l’Editor universale
description: Scopri le diverse opzioni per personalizzare l’Editor universale in modo da supportare le esigenze degli autori di contenuti.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 32b3a125d6370dd591252fde342843d5f9e33cf1
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 2%

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

## Disabilitazione di Apri pagina {#open-page}

Il pulsante **Apri pagina** può essere eliminato completamente in un&#39;app aggiungendo i metadati seguenti.

```html
<meta name="urn:adobe:aue:config:disable" content="header-open-page" />
```

## Disabilitazione del pulsante Duplica {#duplicate-button}

Alcuni flussi di lavoro di authoring potrebbero dover limitare la capacità dell’autore di contenuto di duplicare i componenti. Puoi disabilitare l&#39;[icona duplicata](/help/sites-cloud/authoring/universal-editor/navigation.md#duplicate) aggiungendo i seguenti metadati.

```html
<meta name="urn:adobe:aue:config:disable" content="duplicate"/>
```

## Modifica dell’endpoint {#custom-endpoint}

Se non desideri utilizzare il servizio Universal Editor, ospitato da Adobe, ma la tua versione ospitata, puoi impostarlo in un tag meta. Per informazioni dettagliate, consulta il documento [Guida introduttiva all&#39;editor universale in AEM](/help/implementing/universal-editor/getting-started.md##configuration-settings).

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

Per farlo, includi semplicemente l’URL di anteprima desiderato in un metatag dell’app instrumentata come nell’esempio seguente.

```html
<meta name="urn:adobe:aue:config:preview" content="https://wknd.site"/>
```
