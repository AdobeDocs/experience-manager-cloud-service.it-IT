---
title: Personalizzazione dell’editor universale
description: Scopri le diverse opzioni per personalizzare l’editor universale in modo da supportare le esigenze degli autori di contenuti.
exl-id: 8d6523c8-b266-4341-b301-316d5ec224d7
feature: Developing
role: Admin, Developer
source-git-commit: 42c82384a0683ca2baca522dc9b2d5153ce01b69
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 67%

---


# Personalizzazione dell’editor universale {#customizing}

Scopri le diverse opzioni per personalizzare l’editor universale in modo da supportare le esigenze degli autori di contenuti.

>[!TIP]
>
>L’editor universale offre anche molti [punti di estensione](/help/implementing/universal-editor/extending.md) che ti consentono di ampliarne le funzionalità per soddisfare le esigenze del progetto.

## Utilizzo dei tag di configurazione Meta {#meta-tags}

Alcuni flussi di lavoro di authoring potrebbero richiedere l’utilizzo di alcune funzioni dell’Editor universale e non di altre. Per supportare casi diversi, i metatag sono disponibili per configurare o disabilitare determinate funzioni o pulsanti dell’editor.

Utilizzare questo tag nella sezione `<head>` della pagina per disabilitare una o più funzionalità:

```html
<meta name="urn:adobe:aue:config:disable" content="..." />
```

Per disattivare più funzioni, fornisci un elenco di valori separato da virgole.

Di seguito sono riportati i valori supportati per `content`, ovvero le funzionalità che possono essere disabilitate con i metatag.

| Valore contenuto | Descrizione |
|---|---|
| `publish` | Disattiva tutte le funzionalità di [pubblicazione](/help/sites-cloud/authoring/universal-editor/publishing.md), ovvero il pulsante [pubblicazione](/help/sites-cloud/authoring/universal-editor/navigation.md#publish) e il pulsante [annullamento pubblicazione](/help/sites-cloud/authoring/universal-editor/navigation.md#ellipsis) |
| `publish-live` | Disabilita [pubblicazione](/help/sites-cloud/authoring/universal-editor/publishing.md) in tempo reale |
| `publish-preview` | Disabilita pubblicazione anteprima (se il [servizio di anteprima](/help/sites-cloud/authoring/sites-console/previewing-content.md) è disponibile) |
| `unpublish` | Disattiva il pulsante [annulla pubblicazione](/help/sites-cloud/authoring/universal-editor/publishing.md#unpublishing-content) |
| `copy` | Disattiva i [pulsanti Copia e Incolla](/help/sites-cloud/authoring/universal-editor/authoring.md#copy-paste) |
| `duplicate` | Disattiva il [pulsante Duplica](/help/sites-cloud/authoring/universal-editor/navigation.md#duplicate) |
| `header-open-page` | Disattiva il pulsante [apri pagina](/help/sites-cloud/authoring/universal-editor/navigation.md#open-page) |
| `dev-login` | Disabilita il pulsante di accesso [sviluppatore](/help/sites-cloud/authoring/universal-editor/navigation.md#local-developer-login) |

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
