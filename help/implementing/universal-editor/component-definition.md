---
title: Definizione del componente
description: Informazioni dettagliate sul contratto JSON tra la definizione del componente e l’editor universale.
feature: Developing
role: Admin, Developer
exl-id: e1bb1a54-50c0-412a-a8fd-8167c6f47d2b
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 100%

---

# Definizione del componente {#component-definition}

Informazioni dettagliate sul contratto JSON tra la definizione del componente e l’editor universale.

## Panoramica {#overview}

Il file `component-definition.json` definisce i componenti disponibili per gli autori dei contenuti per il progetto. Questo documento spiega in dettaglio lo scopo di questo file e come viene utilizzato dall’editor universale per presentare agli autori i componenti per l’authoring delle pagine.

>[!TIP]
>
>Per una panoramica del processo di modellazione del contenuto, consulta il documento [Modellazione del contenuto per l’authoring di WYSIWYG con progetti Edge Delivery Services.](https://www.aem.live/developer/component-model-definitions)

>[!TIP]
>
>Non è necessario creare un file `component-definition.json` personalizzato da zero. Il progetto standard utilizzato per [avviare il progetto](https://www.aem.live/developer/ue-tutorial) contiene un [file `component-definition.json` perfettamente funzionante](https://github.com/adobe-rnd/aem-boilerplate-xwalk/blob/main/component-definition.json) che puoi adattare in base alle tue esigenze.

## Definizione del componente di esempio {#example}

Di seguito è riportato un esempio di `component-definition.json` completo, ma semplice.

```json
{
  "groups":[
    {
      "title":"General Components",
      "id":"general",
      "components":[
        {
          "title":"Text",
          "id":"text",
          "model": "text",
          "filter": "texts",
          "plugins":{
            "aem":{
              "page":{
                "resourceType":"wknd/components/text",
                "template":{
                  "text":"Default Text",
                  "name":"Text"
                }
              }
            },
            "aem65":{
              "page":{
                "resourceType":"wknd/components/text",
                "template":{
                  "text":"Default Text",
                  "name":"Text"
                }
              }
            }
          }
        }
      ]
    }
  ]
}
```

## `groups` {#groups}

`groups` definisce i gruppi di componenti visualizzati dall’autore nell’editor universale quando si fa clic sull’icona **Aggiungi** nel pannello delle proprietà dell’editor per [aggiungere un nuovo componente a una pagina](/help/sites-cloud/authoring/universal-editor/authoring.md#adding-components). I gruppi consentono di organizzare i componenti. I gruppi comuni possono essere **Componenti generali** e **Componenti avanzati**.

* `title` definisce la descrizione testuale del gruppo mostrato nell’interfaccia utente dell’editor.
* `id` identifica in modo univoco il gruppo.

## `components` {#components}

`components` definisce quali componenti appartengono a un gruppo.

* `title` definisce la descrizione testuale del componente mostrato nell’interfaccia utente.
* `id` identifica in modo univoco il componente.
   * Il [modello di componente](/help/implementing/universal-editor/field-types.md#model-structure) dello stesso `id` definisce i campi del componente.
   * Poiché è univoco, può essere utilizzato, ad esempio, in una [definizione di filtro](/help/implementing/universal-editor/filtering.md) per determinare quali componenti possono essere aggiunti a un contenitore.
* `model` definisce quale [modello](/help/implementing/universal-editor/field-types.md#model-structure) viene utilizzato con il componente.
   * Il modello viene così mantenuto centralmente nella definizione di componente e non è necessario [specificarlo nella strumentazione.](/help/implementing/universal-editor/field-types.md#instrumentation)
   * In questo modo, inoltre, sarà possibile spostare i componenti tra contenitori diversi.
* `filter` definisce quale [filtro](/help/implementing/universal-editor/filtering.md) deve essere utilizzato con il componente.

## `plugins` {#plugins}

`plugins` definisce quale plug-in è responsabile della persistenza del componente. I plug-in più comuni includono:

* `aem` per [AEM as a Cloud Service.](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service)
* `aem65` per [AEM 6.5.](https://experienceleague.adobe.com/it/docs/experience-manager-65) e [AEM 6.5 LTS](https://experienceleague.adobe.com/it/docs/experience-manager-65-lts)
* `xwalk` per [Authoring con AEM Sites per Edge Delivery Services.](https://www.aem.live/developer/ue-tutorial)

## `page` oppure `cf` {#page-cf}

Una volta definito il `plugin`, devi indicare se è correlato alla pagina o al frammento.

* `page` indica che il componente è contenuto nella pagina corrente.
* `cf` indica che il componente è correlato al contenuto all’interno di un [frammento di contenuto](/help/assets/content-fragments/content-fragments.md).

### `page` {#page}

Se il componente è contenuto nella pagina, puoi fornire le seguenti informazioni.

* `resourceType` definisce lo [Sling](/help/implementing/developing/introduction/sling-cheatsheet.md) `resourceType` utilizzato per il rendering del componente.
* `template` definisce la chiave o i valori facoltativi da scrivere automaticamente nel componente appena creato e definisce quale filtro e/o modello applicare al componente.
   * Utile per testi esplicativi, di esempio o segnaposto.

#### `template` {#template}

Fornendo coppie chiave/valore facoltative, `template` può scriverle automaticamente nel nuovo componente. È, inoltre, possibile specificare i seguenti valori facoltativi.

### `cf` {#cf}

Se il componente è correlato al contenuto all’interno di un frammento di contenuto, puoi fornire le seguenti informazioni.

* `name` definisce un nome facoltativo salvato nel JCR per il componente appena creato.
   * Solo informativo e non generalmente mostrato nell’interfaccia utente come lo è il `title`.
* `cfModel` definisce il modello di [frammento di contenuto](/help/assets/content-fragments/content-fragments-models.md) per il componente appena creato.
* `cfFolder` definisce in quale cartella deve essere creato il frammento di contenuto.
* `title` definisce il titolo del nuovo frammento di contenuto.
* `description` definisce una descrizione del nuovo frammento di contenuto.
* `template` definisce una chiave o valori facoltativi da scrivere automaticamente nel frammento di contenuto appena creato.
   * Utile per testi esplicativi, di esempio o segnaposto.

### `cf` Può essere implicito {#cf-implied}

Se la pagina è [strumentata](/help/implementing/universal-editor/getting-started.md#instrument-page) per puntare a un campo di riferimento, `cf` verrà presupposto.

```html
<div data-aue-resource="urn:aem:/content" data-aue-type="container" data-aue-prop="field"></div>
```

In questo caso, `cf` è presupposto poiché `data-aue-prop` punta a un campo di riferimento. Senza `data-aue-prop`, l’editor universale presupporrà `page`, poiché in tal caso i componenti non sono collegati tramite un campo di riferimento.

```html
<div data-aue-resource="urn:aem:/content" data-aue-type="container"></div>
```

I componenti sono semplicemente sottonodi al di sotto della risorsa.
