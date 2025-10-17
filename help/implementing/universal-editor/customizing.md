---
title: Personalizzazione dell’editor universale
description: Scopri le diverse opzioni per personalizzare l’editor universale in modo da supportare le esigenze degli autori di contenuti.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
feature: Developing
role: Admin, Architect, Developer
source-git-commit: a72b4b7921a1a379bcd089682c02b0519fe3af8a
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 78%

---


# Personalizzazione dell’editor universale {#customizing}

Scopri le diverse opzioni per personalizzare l’editor universale in modo da supportare le esigenze degli autori di contenuti.

>[!TIP]
>
>L’editor universale offre anche molti [punti di estensione](/help/implementing/universal-editor/extending.md) che ti consentono di ampliarne le funzionalità per soddisfare le esigenze del progetto.

## Disabilitazione della pubblicazione {#disable-publish}

Alcuni flussi di lavoro di authoring richiedono la revisione del contenuto prima della pubblicazione. In tali situazioni, l’opzione per pubblicare non deve essere disponibile per nessun autore.

Il pulsante **Pubblica** può quindi essere eliminato completamente da un’app aggiungendo i metadati seguenti.

```html
<meta name="urn:adobe:aue:config:disable" content="publish"/>
```

## Disabilitazione della pubblicazione nell’anteprima {#publish-preview}

Alcuni flussi di lavoro di authoring potrebbero impedire la pubblicazione nell’[anteprima](/help/sites-cloud/authoring/sites-console/previewing-content.md) (se disponibile).

L’opzione **Anteprima** nella finestra di pubblicazione può quindi essere eliminata completamente da un’app aggiungendo i metadati seguenti.

```html
<meta name="urn:adobe:aue:config:disable" content="publish-preview"/>
```

## Disabilitazione della pubblicazione su LiveLive {#publish-live}

Alcuni flussi di lavoro di authoring potrebbero impedire la pubblicazione nel servizio live.

L&#39;opzione **Live** nella finestra di pubblicazione può quindi essere soppressa completamente in un&#39;app aggiungendo i seguenti metadati.

```html
<meta name="urn:adobe:aue:config:disable" content="publish-live"/>
```

## Disabilitazione dell’annullamento della pubblicazione {#unpublish}

Alcuni flussi di lavoro di authoring richiedono un processo di approvazione prima che venga annullata la pubblicazione del contenuto. In tali situazioni, l’opzione per annullare la pubblicazione non deve essere disponibile per alcun autore.

Il pulsante **Annulla pubblicazione** può quindi essere eliminato completamente in un&#39;app aggiungendo i metadati seguenti.

```html
<meta name="urn:adobe:aue:config:disable" content="unpublish"/>
```

## Disabilitazione del pulsante Apertura della pagina {#open-page}

Il pulsante **Apertura della pagina** può essere eliminato completamente da un’app aggiungendo i metadati seguenti.

```html
<meta name="urn:adobe:aue:config:disable" content="header-open-page" />
```

## Disabilitazione del pulsante Duplica {#duplicate-button}

Alcuni flussi di lavoro di authoring potrebbero dover limitare la capacità dell’autore di contenuto di duplicare i componenti. Puoi disabilitare l’[icona di duplicazione](/help/sites-cloud/authoring/universal-editor/navigation.md#duplicate) aggiungendo i seguenti metadati.

```html
<meta name="urn:adobe:aue:config:disable" content="duplicate"/>
```

## Disabilitazione di Copia e Incolla {#copy-paste}

Alcuni flussi di lavoro di authoring potrebbero dover limitare la possibilità dell’autore di contenuto di copiare e incollare componenti. È possibile disabilitare le [icone Copia e Incolla](/help/sites-cloud/authoring/universal-editor/authoring.md#copy-paste) aggiungendo i metadati seguenti.

```html
<meta name="urn:adobe:aue:config:disable" content="copy"/>
```

## Modifica dell’endpoint {#custom-endpoint}

Se non desideri utilizzare il servizio editor universale, ospitato da Adobe, ma la tua versione ospitata, puoi impostarlo in un meta tag. Per informazioni dettagliate, consulta il documento [Guida introduttiva all’editor universale in AEM](/help/implementing/universal-editor/getting-started.md##configuration-settings).

## Filtrare i componenti {#filtering-components}

Puoi limitare i componenti consentiti per contenitore nell’editor universale utilizzando i filtri dei componenti. Per ulteriori informazioni, consulta il documento [Filtrare i componenti](/help/implementing/universal-editor/filtering.md).

## Mostra e nascondi componenti in modo condizionale nel pannello Proprietà {#conditionally-hide}

Anche se, generalmente, uno o più componenti possono essere disponibili per gli autori, in alcune situazioni potrebbe non avere senso. In questi casi, puoi nascondere i componenti nel pannello delle proprietà aggiungendo un attributo `condition` ai campi [ del modello del componente ](/help/implementing/universal-editor/field-types.md#fields).

Le condizioni possono essere definite utilizzando lo [schema JsonLogic](https://jsonlogic.com/). Se la condizione è vera, il campo viene visualizzato. Se la condizione è falsa, il campo viene nascosto.

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

>[!TAB Condizione falsa]

![Campo di testo nascosto](assets/hidden.png)

>[!TAB Condizione vera]

![Campo di testo mostrato](assets/shown.png)

>[!ENDTABS]

## URL di anteprima personalizzati {#custom-preview-urls}

Puoi specificare un URL di anteprima personalizzato tramite una metaconfigurazione `urn:adobe:aue:config:preview` che viene aperta quando fai clic sul pulsante **Apri pagina** nella barra degli strumenti in alto a destra dell’editor [](/help/sites-cloud/authoring/universal-editor/navigation.md#universal-editor-toolbar).

A tal fine, includi semplicemente l’URL di anteprima desiderato in un metatag dell’app dotata di strumenti come nell’esempio seguente.

```html
<meta name="urn:adobe:aue:config:preview" content="https://wknd.site"/>
```
