---
title: Definizione del componente
description: Comprendi in dettaglio il contratto JSON tra la definizione del componente e l’editor universale.
feature: Developing
role: Admin, Architect, Developer
exl-id: e1bb1a54-50c0-412a-a8fd-8167c6f47d2b
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 1%

---

# Definizione del componente {#component-definition}

Comprendi in dettaglio il contratto JSON tra la definizione del componente e l’editor universale.

## Panoramica {#overview}

Il file `component-definition.json` definisce i componenti disponibili per gli autori di contenuto per il progetto. Questo documento spiega in dettaglio lo scopo di questo file e come viene utilizzato da Universal Editor per presentare agli autori i componenti per l’authoring delle pagine.

>[!TIP]
>
>Per una panoramica del processo di modellazione del contenuto, vedere il documento [Modellazione del contenuto per l&#39;authoring WYSIWYG con progetti di Edge Delivery Services](/help/edge/wysiwyg-authoring/content-modeling.md).

>[!TIP]
>
>Non è necessario creare un file `component-definition.json` personalizzato da zero. Il boilerplate del progetto utilizzato per [avviare il progetto](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) contiene un [file `component-definition.json` perfettamente funzionante](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-definition.json) che puoi adattare in base alle tue esigenze.

## Esempio di definizione del componente {#example}

Di seguito è riportato un esempio di `component-definition.json` completo ma semplice.

```json
{
  "groups": [
    {
      "title": "General Components",
      "id": "general",
      "components": [
        {
          "title": "Text",
          "id": "text",
          "plugins": {
            "aem": {
              "page": {
                "resourceType": "wknd/components/text",
                "template": {
                  "text": "Default Text"
                }
              }
            },
            "aem65": {
              "page": {
                "resourceType": "wknd/components/text",
                "template": {
                  "text": "Default Text"
                }
              }
            }
          }
        },
      }
   ]
}
```

## `groups` {#groups}

`groups` definisce i gruppi di componenti visualizzati dall&#39;autore nell&#39;Editor universale quando si fa clic sull&#39;icona **Aggiungi** nel pannello delle proprietà dell&#39;editor per [aggiungere un nuovo componente a una pagina](/help/sites-cloud/authoring/universal-editor/authoring.md#adding-components). I gruppi consentono di organizzare i componenti. I gruppi comuni possono essere **Componenti generali** e **Componenti avanzati**.

* `title` definisce la descrizione testuale del gruppo visualizzato nell&#39;interfaccia utente dell&#39;editor.
* `id` identifica in modo univoco il gruppo.

## `components` {#components}

`components` definisce quali componenti appartengono a un gruppo.

* `title` definisce la descrizione testuale del componente visualizzato nell&#39;interfaccia utente.
* `id` identifica in modo univoco il componente.
   * Il [modello di componente](/help/implementing/universal-editor/field-types.md#model-structure) dello stesso `id` definisce i campi del componente.
   * Poiché è univoco, può essere utilizzato, ad esempio, in una [definizione di filtro](/help/implementing/universal-editor/filtering.md) per determinare quali componenti possono essere aggiunti a un contenitore.

## `plugins` {#plugins}

`plugins` definisce quale plug-in è responsabile della persistenza del componente. I plug-in più comuni includono:

* `aem` per AEM as a Cloud Service.
* `aem5` per AEM 6.5.
* `xwalk` per l&#39;authoring di AEM as a Cloud Service WYSIWYG.

## `page` oppure `cf` {#page-cf}

Una volta definito `plugin`, devi indicare se è correlato alla pagina o al frammento.

* `page` indica che il componente è contenuto nella pagina corrente.
* `cf` indica che il componente è correlato al contenuto all&#39;interno di un [frammento di contenuto](/help/assets/content-fragments/content-fragments.md).

### `page` {#page}

Se il componente è contenuto nella pagina, puoi fornire le seguenti informazioni.

* `name` definisce un nome facoltativo salvato nel JCR per il componente appena creato.
   * Solo informativo e non generalmente visualizzato nell&#39;interfaccia utente come `title` è.
* `resourceType` definisce il [Sling](/help/implementing/developing/introduction/sling-cheatsheet.md) `resourceType` utilizzato per il rendering del componente.
* `template` definisce la chiave o i valori facoltativi da scrivere automaticamente nel componente appena creato.
   * Utile per testo esplicativo, campione o segnaposto.

### `cf` {#cf}

Se il componente è correlato al contenuto all’interno di un frammento di contenuto, puoi fornire le seguenti informazioni.

* `name` definisce un nome facoltativo salvato nel JCR per il componente appena creato.
   * Solo informativo e non generalmente visualizzato nell&#39;interfaccia utente come `title` è.
* `cfModel` definisce il modello [Frammento di contenuto](/help/assets/content-fragments/content-fragments-models.md) per il componente appena creato.
* `cfFolder` definisce in quale cartella deve essere creato il frammento di contenuto.
* `title` definisce il titolo del nuovo frammento di contenuto.
* `description` definisce una descrizione del nuovo frammento di contenuto.
* `template` definisce la chiave o i valori facoltativi da scrivere automaticamente nel nuovo frammento di contenuto creato.
   * Utile per testo esplicativo, campione o segnaposto.

### `cf` può essere implicito {#cf-implied}

Se la pagina è [instrumentata](/help/implementing/universal-editor/getting-started.md#instrument-page) per puntare a un campo di riferimento, verrà utilizzato `cf`.

```html
<div data-aue-resource="urn:aem:/content" data-aue-type="container" data-aue-prop="field"></div>
```

In questo caso, `cf` viene considerato, perché `data-aue-prop` punta a un campo di riferimento. Senza `data-aue-prop`, l&#39;editor universale assumerà `page`, perché in tal caso i componenti non sono collegati tramite un campo di riferimento.

```html
<div data-aue-resource="urn:aem:/content" data-aue-type="container"></div>
```

I componenti sono semplicemente sottonodi sotto la risorsa.
