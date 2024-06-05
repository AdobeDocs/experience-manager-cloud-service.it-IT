---
title: Eventi editor universale
description: Scopri i diversi eventi inviati dall’editor universale che puoi utilizzare per reagire ai contenuti o alle modifiche dell’interfaccia utente nell’app remota.
exl-id: c9f7c284-f378-4725-a4e6-e4799f0f8175
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 2%

---

# Eventi editor universale {#events}

Scopri i diversi eventi inviati dall’editor universale che puoi utilizzare per reagire ai contenuti o alle modifiche dell’interfaccia utente nell’app remota.

## Introduzione {#introduction}

Le applicazioni possono avere requisiti diversi per gli aggiornamenti di pagine o componenti. Di conseguenza, Universal Editor invia eventi definiti alle applicazioni remote. Nel caso in cui l&#39;applicazione remota non disponga di un listener di eventi personalizzato per l&#39;evento inviato, un [listener di eventi di fallback](#fallback-listeners) fornite da `universal-editor-cors` pacchetto viene eseguito.

Tutti gli eventi vengono richiamati sull’elemento DOM interessato della pagina remota. Gli eventi si propagano fino al `BODY` in cui il listener di eventi predefinito fornito da `universal-editor-cors` pacchetto è registrato. Sono disponibili eventi per il contenuto e eventi per l’interfaccia utente.

Tutti gli eventi seguono una convenzione di denominazione.

* `aue:<content-or-ui>-<event-name>`

Ad esempio: `aue:content-update` e `aue:ui-select`

Gli eventi includono il payload della richiesta e della risposta e vengono attivati una volta che la chiamata corrispondente ha esito positivo. Per ulteriori dettagli sulle chiamate e esempi dei loro payload, consulta il documento [Chiamate dell&#39;editor universale.](/help/implementing/universal-editor/calls.md)

## Eventi aggiornamento contenuto {#content-events}

### aue:aggiungere contenuti {#content-add}

Il `aue:content-add` L&#39;evento viene attivato quando un nuovo componente viene aggiunto a un contenitore.

Il payload è un contenuto del servizio Universal Editor, con contenuto di fallback dalla definizione del componente.

```json
{
    details: {
        request: request payload;   // what is sent to the service
        response: {                 // what is returned by the service
            resource: string;       // newly created content resource
            updates: [{
                resource: string;   // resource to update
                type: string;       // type of instrumentation
                content?: string;   // content to replace
            }]
        }
    }
}
```

### aue:content-details {#content-details}

Il `aue:content-details` L&#39;evento viene attivato quando un componente viene caricato nella barra delle proprietà.

Il payload è il contenuto del componente e, facoltativamente, il relativo schema.

```json
{
    details: {
        content: object             // content object
        model: [object]             // model object
        request: request payload;   // what is sent to the service
        response: response payload; // what is returned by the service
    }
}
```

### aue:spostamento contenuto {#content-move}

Il `aue:content-move` viene attivato quando un componente viene spostato.

Il payload è il componente, il contenitore di origine e il contenitore di destinazione.

```json
{
    details: {
        from: string;                   // container we move the component from
        component: string;              // component we move
        to: string;                     // container we move the component to
        before: string;                    // before which component shall we place the component
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service
    }
}
```

### aue:patch di contenuto {#content-patch}

Il `aue:content-patch` L&#39;evento viene attivato quando i dati di un componente vengono aggiornati nella barra delle proprietà.

Il payload è una patch JSON delle proprietà aggiornate.

```json
{
    details: {
        patch: {
            name: string;               // attribute which is updated
            value: string;              // new value which is stored to the attribute
        },
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service
    }
}
```

### aue:rimuovi-contenuto {#content-remove}

Il `aue:content-remove` L&#39;evento viene attivato quando un componente viene rimosso da un contenitore.

Il payload è l’ID dell’elemento rimosso.

```json
{
    details: {
        resource: string;               // the resource which got removed
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service
    }
}
```

### aue:aggiornamento-contenuto {#content-update}

Il `aue:content-update` L&#39;evento viene attivato quando le proprietà di un componente vengono aggiornate nel contesto.

Il payload è il valore aggiornato.

```json
{
    details: {
        value: string;                  // updated value
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service 
    }
}
```

### Trasmissione dei payload {#passing-payloads}

Per tutti gli eventi di aggiornamento del contenuto, il payload richiesto e il payload di risposta vengono trasmessi nell’evento. Ad esempio, per una chiamata di aggiornamento:

Payload richiesta:

```json
{
  "connections": [
    {
      "name": "aemconnection",
      "protocol": "aem",
      "uri": "https://author-p7452-e12433.adobeaemcloud.com"
    }
  ],
  "target": {
    "resource": "urn:aemconnection:/content/dam/wknd-shared/en/magazine/arctic-surfing/aloha-spirits-in-northern-norway/jcr:content/data/master",
    "type": "text",
    "prop": "title"
  },
  "value": "Alhoa Spirit Northern Norway!"
}
```

Payload di risposta

```json
{
    "updates": [
        {
            "resource": "urn:aemconnection:/content/dam/wknd-shared/en/magazine/arctic-surfing/aloha-spirits-in-northern-norway/jcr:content/data/master",
            "prop": "title",
            "type": "text"
        }
    ]
}
```

## Eventi interfaccia utente {#ui-events}

### aue:pubblicazione tramite interfaccia utente {#ui-publish}

Il `aue:ui-publish` l&#39;evento viene attivato quando il contenuto viene pubblicato (con la chiamata al `BODY` livello).

Il payload è un elenco di ID elemento e del loro stato di pubblicazione.

### aue:selezione tramite interfaccia utente {#ui-select}

Il `aue:ui-select` viene attivato quando si seleziona un componente.

Il payload è l’ID dell’elemento, le proprietà dell’elemento e il tipo di elemento del componente selezionato.

```json
{
    details: {
        resource: string;       // resource of the selected
        prop: string;           // prop of the selected
        type: string;           // type of the selected
        selected: boolean;      // was selected or unselected
    }
}
```

### aue:anteprima interfaccia utente {#ui-preview}

Il `aue:ui-preview` l&#39;evento viene attivato quando la modalità di modifica della pagina viene modificata in **Anteprima**.

Il payload è vuoto per questo evento.

```json
{
    details: {}
}
```

### aue:modifica tramite interfaccia utente {#ui-edit}

Il `aue:ui-edit` l&#39;evento viene attivato quando la modalità di modifica della pagina viene modificata in **Modifica**.

Il payload è vuoto per questo evento.

```json
{
    details: {}
}
```

### aue:ui-viewport-change {#ui-viewport-change}

Il `aue:ui-viewport-change` L&#39;evento viene attivato quando si modifica la dimensione del riquadro di visualizzazione.

Il payload è rappresentato dalle dimensioni del riquadro di visualizzazione.

```json
{
    details: {
        height: number?;        // height of the viewport. Undefined when fullscreen
        width: number?;         // width of the viewport. Undefined when fullscreen
    }
}
```

### aue:inizializzato {#initialized}

Il `aue:initialized` viene attivato per comunicare alla pagina remota che è stata caricata correttamente nell&#39;editor universale.

Il payload è vuoto per questo evento.

```json
{
    details: {}
}
```

## Listener di eventi di fallback {#fallback-listeners}

### Aggiornamenti del contenuto {#content-update-fallbacks}

| Evento | Comportamento |
|---|---|
| `aue:content-add` | Ricaricamento pagina |
| `aue:content-details` | Nessuna azione |
| `aue:content-move` | Spostare il contenuto/la struttura del componente nell’area di destinazione |
| `aue:content-patch` | Ricaricamento pagina |
| `aue:content-remove` | Rimuovere l’elemento DOM |
| `aue:content-update` | Aggiornare il `innerHTML` con il payload |

### Eventi interfaccia utente {#ui-event-fallbacks}

| Evento | Comportamento |
|---|---|
| `aue:ui-publish` | Nessuna azione |
| `aue:ui-select` | Scorri fino all’elemento selezionato |
| `aue:ui-preview` | Aggiungi `class="adobe-ue-preview"` al tag HTML |
| `aue:ui-edit` | Aggiungi `class=adobe-ue-edit"` al tag HTML |
| `aue:ui-viewport-change` | Nessuna azione |
| `aue:initialized` | Nessuna azione |

## Risorse aggiuntive {#additional-resources}

* [Chiamate all’editor universale](/help/implementing/universal-editor/calls.md)

