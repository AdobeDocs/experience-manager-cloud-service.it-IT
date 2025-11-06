---
title: Eventi dell’editor universale
description: Scopri i diversi eventi inviati dall’editor universale che puoi utilizzare per reagire ai contenuti o alle modifiche dell’interfaccia utente nell’app remota.
exl-id: c9f7c284-f378-4725-a4e6-e4799f0f8175
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 100%

---

# Eventi dell’editor universale {#events}

Scopri i diversi eventi inviati dall’editor universale che puoi utilizzare per reagire ai contenuti o alle modifiche dell’interfaccia utente nell’app remota.

## Introduzione {#introduction}

Le applicazioni possono avere requisiti diversi per gli aggiornamenti di pagine o componenti. Di conseguenza, l’editor universale invia eventi definiti alle applicazioni remote. Nel caso in cui l’applicazione remota non disponga di un listener di evento personalizzato per l’evento inviato, viene eseguito un [listener di evento di fallback](#fallback-listeners) fornito dal pacchetto `universal-editor-cors`.

Tutti gli eventi vengono richiamati sull’elemento DOM interessato della pagina remota. Gli eventi si propagano fino all’elemento `BODY` in cui è registrato il listener di evento predefinito fornito dal pacchetto `universal-editor-cors`. Sono disponibili eventi per il contenuto e eventi per l’interfaccia utente.

Tutti gli eventi seguono una convenzione di denominazione.

* `aue:<content-or-ui>-<event-name>`

Ad esempio, `aue:content-update` e `aue:ui-select`

Gli eventi includono il payload della richiesta e della risposta e vengono attivati una volta che la chiamata corrispondente ha esito positivo. Per ulteriori dettagli sulle chiamate e esempi dei relativi payload, consulta il documento [Chiamate all’editor universale](/help/implementing/universal-editor/calls.md).

## Eventi aggiornamento contenuto {#content-events}

### aue:content-add {#content-add}

L’evento `aue:content-add` viene attivato quando un nuovo componente viene aggiunto a un contenitore.

Il payload è un contenuto del servizio dell’editor universale, con contenuto di fallback dalla definizione del componente.

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

L’evento `aue:content-details` viene attivato quando un componente viene caricato nel pannello delle proprietà.

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

L’evento `aue:content-move` viene attivato quando un componente viene spostato.

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

L’evento `aue:content-patch` viene attivato quando i dati di un componente vengono aggiornati nel pannello delle proprietà.

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

L’evento `aue:content-remove` viene attivato quando un componente viene rimosso da un contenitore.

Il payload è l’ID elemento del componente rimosso.

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

L’&#39;evento `aue:content-update` viene attivato quando le proprietà di un componente vengono aggiornate nel contesto.

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

Payload risposta

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

L’evento `aue:ui-preview` viene attivato quando la modalità di modifica della pagina viene modificata in **Anteprima**.

Il payload è vuoto per questo evento.

```json
{
    details: {}
}
```

### aue:ui-edit {#ui-edit}

L’evento `aue:ui-edit` viene attivato quando la modalità di modifica della pagina viene modificata in **Modifica**.

Il payload è vuoto per questo evento.

```json
{
    details: {}
}
```

### aue:ui-viewport-change {#ui-viewport-change}

L’evento `aue:ui-viewport-change` viene attivato quando si modifica la dimensione di visualizzazione.

Il payload è rappresentato dalle dimensioni di visualizzazione.

```json
{
    details: {
        height: number?;        // height of the viewport. Undefined when fullscreen
        width: number?;         // width of the viewport. Undefined when fullscreen
    }
}
```

### aue:initialized {#initialized}

L’evento `aue:initialized` viene attivato per comunicare alla pagina remota che è stata caricata correttamente nell’editor universale.

Il payload è vuoto per questo evento.

```json
{
    details: {}
}
```

## Listener eventi di fallback {#fallback-listeners}

### Aggiornamenti del contenuto {#content-update-fallbacks}

| Evento | Comportamento |
|---|---|
| `aue:content-add` | Ricaricamento pagina |
| `aue:content-details` | Nessuna azione |
| `aue:content-move` | Spostare il contenuto/la struttura del componente nell’area di destinazione |
| `aue:content-patch` | Ricaricamento pagina |
| `aue:content-remove` | Rimuovere l’elemento DOM |
| `aue:content-update` | Aggiornare `innerHTML` con il payload |

### Eventi interfaccia utente {#ui-event-fallbacks}

| Evento | Comportamento |
|---|---|
| `aue:ui-select` | Scorrere fino all’elemento selezionato |
| `aue:ui-preview` | Aggiungere `class="adobe-ue-preview"` al tag HTML |
| `aue:ui-edit` | Aggiungere `class=adobe-ue-edit"` al tag HTML |
| `aue:ui-viewport-change` | Nessuna azione |
| `aue:initialized` | Nessuna azione |

## Risorse aggiuntive {#additional-resources}

* [Chiamate all’editor universale](/help/implementing/universal-editor/calls.md)

