---
title: Configurazione dell’editor Rich Text per l’editor universale
description: Scopri come configurare l’editor Rich Text nell’editor universale.
feature: Developing
role: Admin, Developer
exl-id: 350eab0a-f5bc-49c0-8e4d-4a36a12030a1
source-git-commit: e1773cbc2293cd8afe29c3624b29d1e011ea7e10
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 1%

---

# Configurazione dell’editor Rich Text per l’editor universale {#configure-rte}

Scopri come configurare l’editor Rich Text nell’editor universale.

## Panoramica {#overview}

L’editor universale fornisce un editor Rich Text (RTE) sia nella posizione originale che nel pannello delle proprietà per consentire agli autori di applicare le modifiche di formattazione mentre modificano il testo.

L&#39;editor Rich Text è configurabile utilizzando i filtri dei componenti [.](/help/implementing/universal-editor/filtering.md) Questo documento descrive le opzioni di configurazione disponibili e alcuni esempi.

>[!NOTE]
>
>Quando avvii un progetto Universal Editor, tutte le funzioni Rich Text supportate dal backend (AEM con Edge Delivery o implementazione headless) sono automaticamente attive.
>
>* È possibile disattivare le opzioni non necessarie.
>* L’attivazione di opzioni non compatibili con il tipo di progetto non è supportata.

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

### Configurazione rientro {#indentation}

La funzione Rientro dispone di una configurazione a livello di funzionalità che controlla l&#39;ambito del comportamento di rientro, oltre a configurazioni delle singole azioni per collegamenti ed etichette.

```json
{
  "actions": {
    // Feature-level configuration
    "indentation": {
      "scope": "all"  // Controls what content can be indented (default: "all")
    },

    // Individual action configurations
    "indent": {
      "shortcut": "Tab",           // Custom keyboard shortcut
      "label": "Increase Indent"   // Custom button label
    },
    "outdent": {
      "shortcut": "Shift-Tab",     // Custom keyboard shortcut
      "label": "Decrease Indent"   // Custom button label
    }
  }
}
```

#### Opzioni ambito rientro {#indentation-options}

* `scope`: `all` (impostazione predefinita) - Il rientro/rientro si applica a tutto il contenuto:
   * Elenchi: annulla/annulla annidamento voci elenco
   * Paragrafi e intestazioni: Aumenta/diminuisce il livello di rientro generale
* `scope`: `lists` - Il rientro/rientro si applica solo agli elementi dell&#39;elenco:
   * Elenchi: annulla/annulla annidamento voci elenco
   * Paragrafi e intestazioni: nessun rientro (pulsanti disattivati per questi)

>[!NOTE]
>
>La nidificazione degli elenchi tramite i tasti TAB/MAIUSC+TAB funziona indipendentemente dalle impostazioni generali di rientro.

### Incolla testo semplice {#paste-as-text}

L&#39;azione dell&#39;editor `paste_text` abilita un flusso di lavoro standard Incolla come testo normale.

* **Scelta rapida predefinita:** Mod-Shift-v (Cmd+Shift+V su macOS, Ctrl+Shift+V su Windows/Linux)
* **Comportamento:** Incolla da testo/normale (la formattazione di origine viene ignorata)
   * Negli elenchi, le nuove righe creano nuove voci di elenco.

```json
{
  "toolbar": {
    "editor": ["removeformat", "paste_text"]
  },
  "actions": {
    "paste_text": {
      "shortcut": "Mod-Shift-v",
      "label": "Paste as Text"
    }
  }
}
```

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

### `wrapInPicture`{#wrapinpicture}

L&#39;opzione `wrapInPicture` per le immagini controlla la struttura HTML generata per il contenuto dell&#39;immagine.

#### wrapInPicture: false (impostazione predefinita) {#wrapinpicture-false}

```html
<img src="image.jpg" alt="Description" />
```

#### wrapInPicture: true {#wrapinpicture-true}

```html
<picture>
  <img src="image.jpg" alt="Description" />
</picture>
```

Utilizza `wrapInPicture: true` quando hai bisogno di:

* Supporto per immagini reattive con `<source>` elementi.
* Capacità di direzione dell&#39;arte.
* Funzionalità di immagine avanzate a prova di futuro.
* Struttura coerente degli elementi immagine.

>[!NOTE]
>
>Quando `wrapInPicture: true` è abilitato, le immagini possono essere migliorate con ulteriori elementi `<source>` per diversi formati e query multimediali, rendendole più flessibili per la progettazione reattiva.

### Collega opzioni di destinazione {#link-target}

L&#39;opzione `hideTarget` per i collegamenti controlla se l&#39;attributo `target` è incluso nei collegamenti generati e se la finestra di dialogo per la creazione dei collegamenti include un campo per la selezione della destinazione.

#### `hideTarget: false` (impostazione predefinita) {#hideTarget-false}

```html
<a href="https://example.com" target="_self">Link text</a>
<a href="https://example.com" target="_blank">External link</a>
```

#### `hideTarget: true` {#hideTarget-true}

```html
<a href="https://example.com">Link text</a>
```

### Disabilitazione dei collegamenti sulle immagini {#disableforimages}

L&#39;opzione `disableForImages` per i collegamenti controlla se gli utenti possono creare collegamenti su immagini ed elementi dell&#39;immagine. Questo vale sia per gli elementi `<img>` in linea che per gli elementi `<picture>` a livello di blocco.

#### `disableForImages: false` (impostazione predefinita) {#disableforimages-false}

Gli utenti possono selezionare le immagini e racchiuderle nei collegamenti.

```html
<!-- Inline image with link -->
<a href="https://example.com">
  <img src="image.jpg" alt="Description" />
</a>

<!-- Block-level picture with link -->
<a href="https://example.com">
  <picture>
    <img src="image.jpg" alt="Description" />
  </picture>
</a>
```

#### disableForImages: true {#disableforimages-true}

Il pulsante di collegamento è disattivato quando si seleziona un&#39;immagine o un&#39;immagine. Gli utenti possono creare collegamenti solo sul contenuto di testo.

```html
<!-- Images remain standalone without links -->
<img src="image.jpg" alt="Description" />

<picture>
  <img src="image.jpg" alt="Description" />
</picture>

<!-- Links work normally on text -->
<a href="https://example.com">Link text</a>
```

Utilizza `disableForImages: true` quando desideri:

* Mantenere la coerenza visiva impedendo le immagini collegate.
* Semplifica la struttura del contenuto separando le immagini dalla navigazione.
* Applica criteri per contenuto che limitano il collegamento delle immagini.
* Riduzione della complessità di accessibilità dei contenuti.

>[!NOTE]
>
>Questa impostazione influisce solo sulla possibilità di creare nuovi collegamenti sulle immagini. Non rimuove i collegamenti esistenti dalle immagini nel contenuto.

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
