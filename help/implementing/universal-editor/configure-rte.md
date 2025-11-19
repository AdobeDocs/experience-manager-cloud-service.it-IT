---
title: Configurazione dell’editor Rich Text per l’editor universale
description: Scopri come configurare l’editor Rich Text nell’editor universale.
feature: Developing
role: Admin, Developer
exl-id: 350eab0a-f5bc-49c0-8e4d-4a36a12030a1
source-git-commit: 0557379b8d70205043ed87e104d9576ed40a13ce
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 1%

---

# Configurazione dell’editor Rich Text per l’editor universale {#configure-rte}

Scopri come configurare l’editor Rich Text nell’editor universale.

>[!NOTE]
>
>Questa documentazione riguarda il nuovo editor Rich Text per l’editor universale, disponibile come funzionalità iniziale. Se ti interessa testare questa nuova funzionalità, [per ulteriori informazioni, consulta le note sulla versione.](/help/release-notes/universal-editor/current.md#new-rte)

## Panoramica {#overview}

L’editor universale fornisce un editor Rich Text (RTE) sia nella posizione originale che nel pannello delle proprietà per consentire agli autori di applicare le modifiche di formattazione mentre modificano il testo.

L&#39;editor Rich Text è configurabile utilizzando i filtri dei componenti [.](/help/implementing/universal-editor/filtering.md) Questo documento descrive le opzioni di configurazione disponibili e alcuni esempi.

## Struttura di configurazione {#structure}

La configurazione dell’editor Rich Text è costituita da due parti:

* [`toolbar`](#toolbar): la configurazione della barra degli strumenti controlla le opzioni di modifica disponibili nell&#39;interfaccia utente e la loro organizzazione.
* [`actions`](#actions): la configurazione delle azioni consente di personalizzare il comportamento e l&#39;aspetto delle singole azioni di modifica.

Queste configurazioni possono essere definite come parte di un [filtro componente](/help/implementing/universal-editor/filtering.md) con la proprietà `rte`.

```json
[
  {
    "id": "richtext",
    "rte": {
      "toolbar": {
        // Toolbar configuration
      },
      "actions": {
        // Action-specific configurations
      }
    },
    "components": [
      "richtext"
    ]
  }
]
```

## Configurazione barra degli strumenti {#toolbar}

La configurazione della barra degli strumenti controlla quali opzioni di modifica sono disponibili nell’interfaccia utente e come sono organizzate. Queste sono le sezioni disponibili

```json
{
  "toolbar": {
    // Text formatting options
    "format": ["bold", "italic", "underline", "strike"],
    // Text alignment options
    "alignment": ["left", "center", "right", "justify"],
    // Text direction options, right-to-left or left-to-right
    "direction": ["rtl", "ltr"],
    // Indentation controls
    "indentation": ["indent", "outdent"],
    // Block-level elements
    "blocks": ["paragraph", "h1", "h2", "h3", "h4", "h5", "h6", "code_block"],
    // List options
    "list": ["bullet_list", "ordered_list"],
    // Content insertion
    "insert": ["link", "unlink", "image"],
    // Superscript/subscript
    "sr_script": ["superscript", "subscript"],
    // Editor utilities
    "editor": ["removeformat"],
    // Section ordering (optional)
    "sections": ["format", "alignment", "list"]
  }
}
```

## Configurazione azioni {#actions}

La configurazione delle azioni ti consente di personalizzare il comportamento e l’aspetto delle singole azioni di modifica. Queste sono le sezioni disponibili.

### Azioni formato {#format}

Le azioni di formato vengono utilizzate per applicare la formattazione e supportare il passaggio da un tag HTML a un altro per scegliere tra varianti semantiche. Sono disponibili le seguenti sezioni.

```json
{
  "actions": {
    "bold": {
      "tag": "strong",      // Use <strong> instead of <b>
      "shortcut": "Mod-B",  // Custom keyboard shortcut
      "label": "Make Bold"  // Custom button label 
    },
    "italic": {
      "tag": "em",          // Use <em> instead of <i>
      "shortcut": "Mod-I",
      "label": "Italicize"
    },
    "strike": {
      "tag": "del"          // Use <del> instead of <s>
    }
  }
}
```

### Azioni elenco {#list}

Le azioni elenco supportano il wrapping del contenuto per controllare la struttura di HTML. Sono disponibili le seguenti sezioni.

```json
{
  "actions": {
    "bullet_list": {
      "wrapInParagraphs": true,    // <ul><li><p>content</p></li></ul>
      "shortcut": "Mod-Shift-8",   // Custom shortcut
      "label": "Bullet List"       // Custom label
    },
    "ordered_list": {
      "wrapInParagraphs": false,   // <ol><li>content</li></ol> (default)
      "shortcut": "Mod-Shift-9"
    }
  }
}
```

### Azioni collegamento {#link}

Le azioni di collegamento supportano il controllo degli attributi di destinazione per gestire il comportamento dei collegamenti. Sono disponibili le seguenti sezioni.

```json
{
  "actions": {
    "link": {
      "hideTarget": false,       // Show target attribute options (default)
      "shortcut": "Mod-K",       // Custom keyboard shortcut
      "label": "Insert Link"     // Custom button label
    },
    "unlink": {
      "shortcut": "Mod-Shift-K", // Custom keyboard shortcut
      "label": "Remove Link"     // Custom button label
    }
  }
}
```

#### Opzioni di configurazione del collegamento {#link-options}

* `hideTarget`: `false` (predefinito) - Include l&#39;attributo di destinazione nei collegamenti, consentendo `_self`, `_blank`, ecc.
* `hideTarget`: `true` - Escludi completamente l&#39;attributo di destinazione dai collegamenti

L&#39;azione `unlink` viene visualizzata solo quando il cursore si trova all&#39;interno di un collegamento esistente. Rimuove la formattazione del collegamento mantenendo il contenuto del testo.

### Azioni immagine {#image}

Le azioni relative alle immagini supportano il wrapping degli elementi immagine per generare un markup dinamico per le immagini. Sono disponibili le seguenti sezioni.

```json
{
  "actions": {
    "image": {
      "wrapInPicture": false,     // Use <img> tag (default)
      "shortcut": "Mod-Shift-I",  // Custom keyboard shortcut
      "label": "Insert Image"     // Custom button label
    }
  }
}
```

#### Opzioni di configurazione immagine {#image-options}

* `wrapInPicture`: `false` (predefinito) - Genera `<img>` elementi semplici
* `wrapInPicture`: `true` - Racchiudi immagini negli elementi `<picture>` per la progettazione reattiva

### Altre azioni {#other}

Tutte le altre azioni supportano la personalizzazione di base. Sono disponibili le seguenti sezioni.

```json
{
  "actions": {
    "h1": {
      "shortcut": "Mod-Alt-1",
      "label": "Large Heading"
    },
    "paragraph": {
      "shortcut": "Mod-Alt-0",
      "label": "Normal Text"
    },
    "link": {
      "shortcut": "Mod-K",
      "label": "Insert Link",
      "hideTarget": false    // Show target attribute options (default: false)
    }
  }
}
```

## Esempio completo {#example}

Di seguito è riportato un esempio di configurazione completa.

```json
[
  {
    "id": "richtext",
    "rte": {
      // Configure which tools appear in toolbar
      "toolbar": {
        "format": [
          "bold",
          "italic"
        ],
        "blocks": [
          "paragraph",
          "h1",
          "h2"
        ],
        "list": [
          "bullet_list",
          "ordered_list"
        ],
        "insert": [
          "link",
          "unlink"
        ],
        "sections": [
          "format",
          "blocks",
          "list",
          "insert"
        ]
      },
      // Customize individual action behavior
      "actions": {
        // Format actions with HTML tag choices
        "bold": {
          "tag": "strong",
          "shortcut": "Mod-B",
          "label": "Bold"
        },
        "italic": {
          "tag": "em",
          "shortcut": "Mod-I"
        },
        // List actions with content wrapping
        "bullet_list": {
          "wrapInParagraphs": true,
          "label": "Bullet List"
        },
        "ordered_list": {
          "wrapInParagraphs": false
        },
        // Link actions with target control
        "link": {
          "hideTarget": false,
          "shortcut": "Mod-K",
          "label": "Add Link"
        },
        "unlink": {
          "label": "Remove Link"
        },
        // Other actions with basic customization
        "h1": {
          "shortcut": "Mod-Alt-1",
          "label": "Main Heading"
        }
      }
    }
  }
]
```

## Dettagli opzione azione {#action-details}

Diverse opzioni hanno ulteriori dettagli importanti da tenere a mente.

### `wrapInParagraphs` {#wrapInParagraphs}

L&#39;opzione `wrapInParagraphs` per gli elenchi controlla la struttura HTML.

#### `wrapInParagraphs: false` (impostazione predefinita) {#wrapInParagraphs-false}

```html
<ul>
  <li>Simple text content</li>
  <li>Another item</li>
</ul>
```

#### `wrapInParagraphs: true` {#wrapInParagraphs-true}

```html
<ul>
  <li><p>Text wrapped in paragraphs</p></li>
  <li><p>Supports rich formatting within items</p></li>
</ul>
```

Utilizza `wrapInParagraphs: true` quando hai bisogno di:

* Formattazione avanzata all&#39;interno di voci di elenco
* Più paragrafi per voce di elenco
* Stile coerente a livello di blocco

### Collega opzioni di destinazione {#link-target}

L&#39;opzione `hideTarget` per i collegamenti controlla se l&#39;attributo `target` è incluso nei collegamenti generati e se la finestra di dialogo per la creazione dei collegamenti include un campo per la selezione della destinazione.

#### `hideTarget: false` (impostazione predefinita) {#hideTarget-false}

```html
<a href="https://example.com" target="_self">Link text</a>
<a href="https://example.com" target="_blank">External link</a>
```

### `hideTarget: true` {#hideTarget-true}

```html
<a href="https://example.com">Link text</a>
```

### Opzioni tag {#tag}

Le azioni di formato consentono il passaggio tra diverse varianti di HTML.

| Azione | Tag predefinito | Tag alternativi | Caso d’uso |
|---|---|---|---|
| `bold` | `<strong>` | `<b>` | Enfasi semantica e visiva |
| `italic` | `<em>` | `<i>` | Stile semantico e visivo |
| `strike` | `<del>` | `<s>` | Eliminazione visiva e semantica |

Scegliere i tag semantici (`<strong>`, `<em>`, `<del>`) per migliorare l&#39;accessibilità e SEO.

### Scelte rapide da tastiera {#keyboard-shortcuts}

I collegamenti utilizzano il formato `Mod-Key` in cui:

* `Mod` = `Cmd` su Mac, `Ctrl` su Windows/Linux
* Esempi: `Mod-B`, `Mod-Shift-8`, `Mod-Alt-1`
