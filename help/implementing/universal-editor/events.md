---
title: Eventi editor universale
description: Scopri i diversi eventi inviati dall’editor universale che puoi utilizzare per reagire ai contenuti o alle modifiche dell’interfaccia utente nell’app remota.
exl-id: c9f7c284-f378-4725-a4e6-e4799f0f8175
feature: Developing
role: Admin, Architect, Developer
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 2%

---

# Eventi editor universale {#events}

Scopri i diversi eventi inviati dall’editor universale che puoi utilizzare per reagire ai contenuti o alle modifiche dell’interfaccia utente nell’app remota.

## Introduzione {#introduction}

Le applicazioni possono avere requisiti diversi per gli aggiornamenti di pagine o componenti. Di conseguenza, Universal Editor invia eventi definiti alle applicazioni remote. Nel caso in cui l&#39;applicazione remota non disponga di un listener di eventi personalizzato per l&#39;evento inviato, viene eseguito un [listener di eventi di fallback](#fallback-listeners) fornito dal pacchetto `universal-editor-cors`.

Tutti gli eventi vengono richiamati sull’elemento DOM interessato della pagina remota. Fumetto di eventi fino all&#39;elemento `BODY` in cui è registrato il listener di eventi predefinito fornito dal pacchetto `universal-editor-cors`. Sono disponibili eventi per il contenuto e eventi per l’interfaccia utente.

Tutti gli eventi seguono una convenzione di denominazione.

* `aue:<content-or-ui>-<event-name>`

Ad esempio, `aue:content-update` e `aue:ui-select`

Gli eventi includono il payload della richiesta e della risposta e vengono attivati una volta che la chiamata corrispondente ha esito positivo. Per ulteriori dettagli sulle chiamate e esempi dei payload, consulta il documento [Chiamate all&#39;editor universale](/help/implementing/universal-editor/calls.md).

## Eventi aggiornamento contenuto {#content-events}

### aue:content-add {#content-add}

L&#39;evento `aue:content-add` viene attivato quando un nuovo componente viene aggiunto a un contenitore.

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

L&#39;evento `aue:content-details` viene attivato quando un componente viene caricato nel pannello delle proprietà.

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

### aue:content-move {#content-move}

L&#39;evento `aue:content-move` viene attivato quando un componente viene spostato.

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

### aue:content-patch {#content-patch}

L&#39;evento `aue:content-patch` viene attivato quando i dati di un componente vengono aggiornati nel pannello delle proprietà.

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

### aue:content-remove {#content-remove}

L&#39;evento `aue:content-remove` viene attivato quando un componente viene rimosso da un contenitore.

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

### aue:content-update {#content-update}

L&#39;evento `aue:content-update` viene attivato quando le proprietà di un componente vengono aggiornate nel contesto.

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

### aue:ui-preview {#ui-preview}

L&#39;evento `aue:ui-preview` viene attivato quando la modalità di modifica della pagina viene modificata in **Anteprima**.

Il payload è vuoto per questo evento.

```json
{
    details: {}
}
```

### aue:ui-edit {#ui-edit}

L&#39;evento `aue:ui-edit` viene attivato quando la modalità di modifica della pagina viene modificata in **Modifica**.

Il payload è vuoto per questo evento.

```json
{
    details: {}
}
```

### aue:ui-viewport-change {#ui-viewport-change}

L&#39;evento `aue:ui-viewport-change` viene attivato quando si modifica la dimensione del riquadro di visualizzazione.

Il payload è rappresentato dalle dimensioni del riquadro di visualizzazione.

```json
{
    details: {
        height: number?;        // height of the viewport. Undefined when fullscreen
        width: number?;         // width of the viewport. Undefined when fullscreen
    }
}
```

### aue:initialized {#initialized}

L&#39;evento `aue:initialized` viene attivato per comunicare alla pagina remota che è stata caricata correttamente nell&#39;editor universale.

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
| `aue:content-update` | Aggiorna `innerHTML` con il payload |

### Eventi interfaccia utente {#ui-event-fallbacks}

| Evento | Comportamento |
|---|---|
| `aue:ui-select` | Scorri fino all’elemento selezionato |
| `aue:ui-preview` | Aggiungi `class="adobe-ue-preview"` al tag HTML |
| `aue:ui-edit` | Aggiungi `class=adobe-ue-edit"` al tag HTML |
| `aue:ui-viewport-change` | Nessuna azione |
| `aue:initialized` | Nessuna azione |

## Risorse aggiuntive {#additional-resources}

* [Chiamate all’editor universale](/help/implementing/universal-editor/calls.md)

