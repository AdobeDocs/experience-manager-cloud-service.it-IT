---
title: Creare componenti personalizzati per un modulo EDS
description: Creare componenti personalizzati per un modulo EDS
feature: Edge Delivery Services
role: Admin, Developer
exl-id: 2bbe3f95-d5d0-4dc7-a983-7a20c93e2906
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2103'
ht-degree: 99%

---


# Creazione del componente Modulo personalizzato nel blocco di moduli adattivi

I moduli di Edge Delivery Services offrono funzionalità di personalizzazione e permettono agli sviluppatori front-end di creare componenti per moduli su misura. Questi componenti personalizzati si integrano direttamente nell’esperienza di authoring WYSIWYG, consentendo agli autori di moduli di aggiungerli, configurarli e gestirli facilmente nell’editor di moduli. I componenti personalizzati permettono agli autori di ottimizzare le funzionalità dei moduli. Inoltre, assicurano un processo di authoring fluido e intuitivo.

Questo documento illustra i passaggi necessari per creare componenti personalizzati assegnando uno stile ai componenti per moduli HTML nativi, migliorando l’esperienza utente e aumentando l’impatto visivo dei moduli stessi.

## Panoramica dell’architettura

Il componente personalizzato per il blocco moduli segue un pattern di architettura **MVC (Model-View-Controller)**:

### Modello

- Definito dallo schema JSON per ciascun `field/component`.

- Le proprietà che supportano la modalità di authoring sono specificate nel file JSON corrispondente (consulta blocchi/modulo/modelli/componenti modulo).

- Queste proprietà sono disponibili per gli autori nel generatore di moduli e vengono passate al componente come parte della definizione del campo (fd).

### Visualizzazione

- La struttura HTML per ogni tipo di campo è descritta in tipi di campo modulo.

- Questa è la struttura di base del componente che può essere estesa o modificata.

- La struttura HTML di base per ciascun componente integrato è documentata nei tipi di campo modulo.

### Logica controller/componente

- Implementata in JavaScript, come componente integrato o personalizzato.  - Si trova in `blocks/form/components` per i componenti personalizzati.

## Componenti integrati

I componenti **integrati** forniscono le basi per lo sviluppo personalizzato:

- I componenti integrati si trovano in `blocks/form/models/form-components`.

- Ciascun componente integrato dispone di un file JSON che definisce le relative proprietà modificabili dall’autore (ad esempio,` _text-input.json`,`_drop-down.json`).

- Queste proprietà sono disponibili per gli autori nel generatore di moduli e vengono passate al componente come parte della definizione del campo (fd).

- La struttura HTML di base per ciascun componente integrato è documentata nei tipi di campo modulo.

L’estensione di un componente integrato esistente consente di riutilizzarne la struttura di base, il comportamento e le proprietà, nonché personalizzarlo in base alle esigenze.

- I componenti personalizzati devono estendersi da un set predefinito di componenti integrati.

- Il sistema identifica quale componente integrato estendere in base alla proprietà `viewType` nel JSON del campo.

- Il sistema gestisce un registro delle varianti di componenti personalizzati consentite. È possibile utilizzare solo le varianti elencate in questo registro, ad esempio `customComponents[]` in `mappings.js`.

- Durante il rendering di un modulo, il sistema controlla la proprietà variante o `:type/fd:viewType` e, se corrisponde a un componente personalizzato registrato, carica i corrispondenti file JS e CSS dalla cartella `blocks/form/components`.

- Il componente personalizzato viene quindi applicato alla struttura HTML di base del componente integrato, consentendoti di migliorarne o sostituirne il comportamento e l’aspetto.

## Struttura del componente personalizzato

Per creare componenti personalizzati, puoi utilizzare **CLI Scaffolder** per configurare i file e le cartelle richiesti per il componente e quindi aggiungere il codice per il componente personalizzato.

- I componenti personalizzati si trovano nella cartella `blocks/form/components`.

- Ciascun componente personalizzato deve essere inserito nella relativa cartella, con il nome del componente, ad esempio schede. All’interno della cartella, i seguenti file dovrebbero essere:

   - **_cards.json**: il file JSON che estende la definizione del componente integrato, definisce le proprietà che supportano la modalità di authoring (modelli[]) e la struttura del contenuto al caricamento (definizioni[]).
   - **cards.js**: il file JavaScript che include la logica principale.
   - **cards.css**: facoltativo, per gli stili.

- Il nome della cartella e i file JS/CSS devono corrispondere.

### Riutilizzo ed estensione dei campi nei componenti personalizzati

Quando definisci i campi nel JSON del componente personalizzato (per qualsiasi gruppo di campi, base, convalida, guida, ecc.), segui le best practice per manutenibilità e coerenza:

- Riutilizza i campi standard/condivisi facendo riferimento a contenitori condivisi o definizioni di campi esistenti (ad esempio, `../form-common/_basic-input-placeholder-fields.json#/fields`, `../form-common/_basic- validation-fields.json#/fields`). In questo modo puoi ereditare tutte le opzioni standard senza duplicarle.

- Aggiungi esplicitamente solo campi nuovi o personalizzati nel contenitore. In questo modo lo schema rimane provato e mirato.

- Rimuovi o evita di duplicare i campi già inclusi tramite riferimenti. Definisci solo campi univoci per la logica del componente.

- Fai riferimento ai contenitori della Guida e ad altri contenuti condivisi (ad esempio, `../form-common/_help-container.json`) come necessario per coerenza e manutenibilità.

>[!TIP]
>
> - Questo modello consente di aggiornare o estendere facilmente la logica in futuro e garantisce che i componenti personalizzati rimangano coerenti con il resto del sistema del modulo.
> - Prima di aggiungere nuovi contenitori condivisi o definizioni di campi, controlla sempre quelli esistenti.

### Definizione di nuove proprietà per i componenti personalizzati

- Se devi acquisire nuove proprietà per il componente personalizzato dagli autori, puoi farlo definendo un campo nell’array `fields[]` del componente nel JSON del componente.

- Il componente personalizzato viene identificato utilizzando la proprietà :type, che può essere impostata come `fd:viewType` nel file JSON (ad esempio, `fd:viewType: cards`). Questo consente al sistema di riconoscere e caricare il componente personalizzato corretto e pertanto è obbligatorio per i componenti personalizzati

- Tutte le nuove proprietà aggiunte nella definizione JSON sono disponibili nella definizione del campo come proprietà. `<propertyName>` nella logica JS del componente

## API JavaScript del componente personalizzato

L’API JavaScript del componente personalizzato definisce come controllare il comportamento, l’aspetto e la reattività del componente del modulo personalizzato.

### Funzione Decora

La funzione **decora** è il punto di ingresso del componente personalizzato. Inizializza il componente, lo collega alla sua definizione JSON e consente di manipolarne la struttura HTML e il comportamento.

>[!NOTE]
>
> Il file JavaScript del componente personalizzato deve esportare una funzione predefinita come decora:

#### Funzione Firma:

```javascript
export default function decorate(element, fieldJson, container, formId) 
{
  // element: The HTML structure of the OOTB component you are extending
  // fieldJson: The JSON field definition (all authorable properties)
  // container: The parent element (fieldset or form)
  // formId: The id of the form

  // ... your logic here ...
}
```

Può:

- **Modificare l’elemento**: aggiungi listener di eventi, aggiorna attributi o inserisci markup aggiuntivo.

- **Accedere alle proprietà JSON**: utilizza `fd.properties.<propertyName>` per leggere i valori definiti nello schema JSON e applicarli nella logica del componente.

## Funzione Abbonati

La funzione **abbonati** consente al componente di reagire alle modifiche nei valori dei campi o agli eventi personalizzati. In questo modo il componente rimane sincronizzato con il modello dati del modulo e può aggiornare dinamicamente la relativa interfaccia utente.

### Funzione Firma:

```javascript
import { subscribe } from '../../rules/index.js';
export default function decorate(fieldDiv, fieldJson, container, formId) {
  // Access custom properties defined in the JSON
  const { initialText, finalText, time } = fieldJson?.properties;

  // ... setup logic ...

  subscribe(fieldDiv, formId, (_fieldDiv, fieldModel) => {
    fieldModel.subscribe(() => {
      // React to custom event (e.g., resetCardOption)
      // ... logic ...
    }, 'resetCardOption');
  });
}
```

Può:

- **Registrare un callback**: chiamando **abbonati(elemento, formId, callback)** registra il callback da eseguire ogni volta che i dati del campo cambiano.Utilizza due parametri di callback:
   - **elemento**: l’elemento HTML che rappresenta il campo.
   - **fieldModel**: oggetto che rappresenta lo stato del campo e le API evento.

- **Rilevare modifiche o eventi**: utilizza `fieldModel.subscribe((event) => { ... }, 'eventName')` per eseguire la logica ogni volta che un valore cambia o viene attivato un evento personalizzato. L’oggetto evento contiene dettagli sulle modifiche apportate.

## Creazione di un componente personalizzato

In questa sezione imparerai il processo di creazione di un **componente personalizzato schede** estendendo il componente pulsante di scelta integrato.

![Componente personalizzato scheda](/help/edge/docs/forms/universal-editor/assets/cc-ue-card-component.png)

### &#x200B;1. Configurazione del codice

#### 1.1 File e cartelle

Il primo passaggio consiste nel configurare i file necessari del componente personalizzato e collegarlo al codice nell’archivio. Questo processo viene eseguito automaticamente dal **CLI di AEM Forms Scaffolder**, rendendo più rapido lo scaffolding e il collegamento dei file necessari.

>[!VIDEO](https://video.tv.adobe.com/v/3474752)

1. Apri il terminale e passa alla directory principale del progetto del modulo.
2. Esegui i comandi seguenti:

```bash
npm install
npm run create:custom-component
```

![CLI di Scaffolder](/help/edge/docs/forms/universal-editor/assets/scaffolder-cli.png)

Questo:

- **Richiederà di denominare** il nuovo componente. Ad esempio, in questo caso utilizza schede.
- **Chiederà di scegliere** un componente di base (seleziona un gruppo di pulsanti di scelta)

In questo modo vengono creati tutti i file e le cartelle necessari, tra cui:

```
blocks/form/
└── components/
  └── cards/
    ├── cards.js
    └── cards.css
    └── _cards.json
```

E lo collega con il resto del codice nell’archivio come mostrato nell’output della CLI.
Esegue automaticamente le seguenti funzionalità:

- Aggiunge schede ai filtri per consentirne l’aggiunta all’interno del blocco di modulo adattivo.
- Aggiorna l’elenco Consentiti di `mappings.js` in modo da includere il nuovo componente Schede.
- Registra la definizione del componente Schede nell’elenco **Componenti personalizzati** nell’editor universale.

>[!NOTE]
>
> È possibile anche creare un componente personalizzato utilizzando il metodo manuale (precedente). Per maggiori dettagli, consulta il [Metodo manuale o precedente](#manual-or-legacy-method-to-create-custom-component) per creare un componente personalizzato.

#### 1.2 Utilizzo del componente nell’editor universale

1. **Aggiornare l’editor universale**: apri il modulo nell’editor universale e aggiorna la pagina per assicurarti che venga caricato il codice più recente dall’archivio.

2. **Aggiungere il componente personalizzato**

   1. Fai clic sul pulsante **Aggiungi (+)** nell’area di lavoro del modulo.
   2. Scorri fino alla sezione Componenti personalizzati.
   3. Seleziona il **componente Schede** appena creato per inserirlo nel modulo.

      ![Selezionare il componente personalizzato](/help/edge/docs/forms/universal-editor/assets/select-custom-component.png)

Poiché non è presente alcun codice all’interno di `cards.js`, il componente personalizzato viene riprodotto come gruppo di pulsanti di scelta.

#### 1.3 Anteprima e test in locale

Ora che il modulo contiene il componente personalizzato, puoi eseguire il proxy del modulo, apportarvi modifiche in locale e visualizzarle:

1. Vai al tuo terminale ed esegui `aem up`.

2. Apri il server proxy avviato in `http://localhost:3000/{path-to-your-form}` (esempio di percorso: `/content/forms/af/custom-component-form`)


### &#x200B;2. Implementazione del comportamento personalizzato per il componente personalizzato

#### 2.1 Attribuzione dello stile al componente personalizzato

Aggiungiamo una **scheda** di classe al componente per l’attribuzione dello stile e un’immagine per ogni pulsante di scelta. A tale scopo, utilizza il codice seguente.

**Personalizza lo stile del componente utilizzando card.js**

```javascript
import { createOptimizedPicture } from '../../../../scripts/aem.js';

export default function decorate(element, fieldJson, container, formId) {
  element.classList.add('card');

  element.querySelectorAll('.radio-wrapper').forEach((radioWrapper) => {
    const image = createOptimizedPicture(
      'https://main--afb--jalagari.hlx.live/lab/images/card.png',
      'card-image'
    );
    radioWrapper.appendChild(image);
  });

  return element;
}
```

**Aggiungi comportamento runtime utilizzando cards.css**

```javascript
.card .radio-wrapper {
  min-width: 320px; /* or whatever width fits your design */
  max-width: 340px;
  background: #fff;
  border-radius: 16px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
  flex: 0 0 auto;
  scroll-snap-align: start;
  padding: 24px 16px;
  margin-bottom: 0;
  position: relative;
  transition: box-shadow 0.2s;
  display: flex;
  align-items: flex-start;
  gap: 12px;
}
```

Ora, il componente schede viene visualizzato come segue:

![aggiungi css e js schede](/help/edge/docs/forms/universal-editor/assets/add-card-css.png)

#### 2.2 Aggiungere un comportamento dinamico tramite la funzione Abbonati

Quando il menu a discesa viene modificato, le schede vengono recuperate e impostate nell’enum del gruppo di pulsanti di scelta. Ma attualmente la visualizzazione non gestisce questa situazione. Viene quindi eseguito il rendering come mostrato di seguito:

![funzione abbonati](/help/edge/docs/forms/universal-editor/assets/card-subscribe.png)

Quando viene chiamata l’API, imposta il campo Modello e deve rilevare le modifiche ed eseguire di conseguenza il rendering della vista. Questa azione viene eseguita utilizzando la **funzione abbonati**.

Convertiamo il codice di visualizzazione del passaggio precedente in una funzione e chiamiamolo all’interno della funzione abbonati in `cards.js` come illustrato di seguito:

```javascript
import { createOptimizedPicture } from '../../../../scripts/aem.js';
import { subscribe } from '../../rules/index.js';

function createCard(element, enums) {
  element.querySelectorAll('.radio-wrapper').forEach((radioWrapper, index) => {
    if (enums[index]?.name) {
      let label = radioWrapper.querySelector('label');

      if (!label) {
        label = document.createElement('label');
        radioWrapper.appendChild(label);
      }

      label.textContent = enums[index]?.name;
    }

    const image = createOptimizedPicture(
      enums[index]?.image || 'https://main--afb--jalagari.hlx.page/lab/images/card.png',
      'card-image'
    );

    radioWrapper.appendChild(image);
  });
}

export default function decorate(element, fieldJson, container, formId) {
  element.classList.add('card');
  createCard(element, fieldJson.enum);

  subscribe(element, formId, (fieldDiv, fieldModel) => {
    fieldModel.subscribe((e) => {
      const { payload } = e;

      payload?.changes?.forEach((change) => {
        if (change?.propertyName === 'enum') {
          createCard(element, change.currentValue);
        }
      });
    });
  });

  return element;
}
```

**Utilizzare la funzione abbonati per rilevare le modifiche all’evento in cards.js**

Ora, quando cambi il menu a discesa, le schede si popolano come mostrato di seguito:

![funzione abbonati](/help/edge/docs/forms/universal-editor/assets/card-subscribe-final.png)

#### 2.3 Sincronizzazione degli aggiornamenti delle visualizzazioni con il modello di campo

Per sincronizzare le modifiche della visualizzazione al modello di campo, è necessario impostare il valore della scheda selezionata. Quindi, aggiungi il seguente listener di eventi di modifica in cards.js come mostrato di seguito:

**Utilizzo dell’API modello di campo in cards.js**

```javascript
import { createOptimizedPicture } from '../../../../scripts/aem.js';
import { subscribe } from '../../rules/index.js';

function createCard(element, enums) {
  element.querySelectorAll('.radio-wrapper').forEach((radioWrapper, index) => {
    if (enums[index]?.name) {
      let label = radioWrapper.querySelector('label');

      if (!label) {
        label = document.createElement('label');
        radioWrapper.appendChild(label);
      }

      label.textContent = enums[index]?.name;
    }

    // Attach index to input element for later reference
    radioWrapper.querySelector('input').dataset.index = index;

    const image = createOptimizedPicture(
      enums[index]?.image || 'https://main--afb--jalagari.hlx.page/lab/images/card.png',
      'card-image'
    );

    radioWrapper.appendChild(image);
  });
}

export default function decorate(element, fieldJson, container, formId) {
  element.classList.add('card');
  createCard(element, fieldJson.enum);

  subscribe(element, formId, (fieldDiv, fieldModel) => {
    fieldModel.subscribe((e) => {
      const { payload } = e;

      payload?.changes?.forEach((change) => {
        if (change?.propertyName === 'enum') {
          createCard(element, change.currentValue);
        }
      });
    });

    element.addEventListener('change', (e) => {
      e.stopPropagation();
      const value = fieldModel.enum?.[parseInt(e.target.dataset.index, 10)];
      fieldModel.value = value.name;
    });
  });

  return element;
}
```

Ora mostra il componente scheda personalizzato, come illustrato di seguito:

![Componente personalizzato scheda](/help/edge/docs/forms/universal-editor/assets/cc-ue-card-component.png)

### &#x200B;3. Confermare e inviare modifiche

Dopo aver implementato JavaScript e CSS per il componente personalizzato e averlo verificato in locale, conferma e invia le modifiche all’archivio Git.

```bash
git add . && git commit -m "Add card custom component" && git push
```

Hai creato correttamente un componente complesso e personalizzato di selezione della scheda in pochi semplici passaggi.

+++ **Metodo manuale o precedente per creare il componente personalizzato**

Il modo precedente per farlo è seguire manualmente i passaggi descritti di seguito:

1. **Scegli un componente integrato** da estendere (ad esempio, pulsante, a discesa, immissione di testo e così via). In questo caso, estendi il componente pulsante di scelta.

2. **Crea una cartella** in `blocks/form/components` con il nome del componente (schede in questo caso).

3. **Aggiungi un file JS** con lo stesso nome:
   - `blocks/form/components/cards/cards.js`.

4. (Facoltativo) **Aggiungi un file CSS** per gli stili personalizzati:
   - `blocks/form/components/cards/cards.css.`

5. **Definisci un nuovo file JSON** (ad esempio,` _cards.json`) nella stessa cartella del **file JS componente** (`blocks/form/components/cards/_cards.json`). Questo JSON deve estendere un componente esistente e nelle relative definizioni, imposta `fd:viewType` al nome del componente (in questo caso, schede):

   - Per tutti i gruppi di campi (di base, convalida, guida, ecc.) aggiungi esplicitamente i campi personalizzati.

6. **Implementa la logica JS e CSS:**
   - Esporta una funzione predefinita come descritto in precedenza.
   - Utilizza il parametro **elemento** per modificare la struttura HTML di base.
   - Utilizza il parametro **fieldJson** se necessario per i dati del campo standard.
   - Utilizza la funzione **abbonati** per rilevare le modifiche del campo o gli eventi personalizzati, se necessario.

     >[!NOTE]
     >
     >Implementa la logica JS e CSS per il componente personalizzato, come spiegato in precedenza.

7. Registra il componente come variante nel generatore di moduli e imposta la proprietà variante o
   `fd:viewType/:type` nel JSON al nome del componente, ad esempio, aggiungi il valore `fd:viewType` da `definitions[]` come schede all’array dei componenti dell’oggetto con `id="form`.

   ```
       {
     "definitions": [
       {
         "title": "Cards",
         "id": "cards",
         "plugins": {
           "xwalk": {
             "page": {
               "resourceType": "core/fd/components/form/radiobutton/v1/radiobutton",
               "template": {
                 "jcr:title": "Cards",
                 "fieldType": "radio-button",
                 "fd:viewType": "cards",
                 "enabled": true,
                 "visible": true
               }
             }
           }
         }
       }
     ]
   }
   ```

8. **Aggiorna mappings.js**: aggiungi il nome del componente all’elenco **OOTBComponentDecorators** (per i componenti di stile integrato) o **customComponents** in modo che venga riconosciuto e caricato dal sistema.

   ```javascript
   let customComponents = ["cards"];
   const OOTBComponentDecorators = [];
   ```

9. **Aggiorna _form.json**: aggiungi il nome del componente all’array `filters.components` in modo che possa essere interrotto nell’interfaccia utente di creazione.

   ```javascript
   "filters": [
   {
       "id": "form",
       "components": [ "cards"]}
       ]
   ```

10. **Aggiorna _component-definition.json**: in `models/_component-definition.json` aggiorna l’array all’interno del gruppo con `id custom-components` con un oggetto nel modo seguente:

    ```javascript
    {
    "...":"../blocks/form/components/cards/_cards.json#/definitions"
    }
    ```

    In questo modo, viene fornito il riferimento al nuovo componente schede da creare con gli altri componenti

11. **Esegui lo script:json della build**: esegui `npm run build:json` per compilare e unire tutte le definizioni JSON dei componenti in un unico file trasmesso dal server. In questo modo lo schema del nuovo componente viene incluso nell’output unito.

12. Conferma e invia le modifiche all’archivio Git.

Ora puoi aggiungere il componente personalizzato al modulo.

+++

## Creare un componente personalizzato

Un componente composito viene creato combinando più componenti.
Ad esempio, un componente composito di Termini e condizioni è costituito da un pannello principale che contiene:

- un campo di testo normale per la visualizzazione dei termini

- una casella di controllo per acquisire il consenso dell’utente

Questa struttura di composizione è definita come un modello all’interno del file JSON del rispettivo componente. L’esempio seguente mostra come definire un modello per un componente Termini e condizioni:

```javascript
{
  "definitions": [
    {
      "title": "Terms and conditions",
      "id": "tnc",
      "plugins": {
        "xwalk": {
          "page": {
            "resourceType": "core/fd/components/form/termsandconditions/v1/termsandconditions",
            "template": {
              "jcr:title": "Terms and conditions",
              "fieldType": "panel",
              "fd:viewType": "tnc",
              "text": {
                "value": "Text related to the terms and conditions come here.",
                "sling:resourceType": "core/fd/components/form/text/v1/text",
                "fieldType": "plain-text",
                "textIsRich": true
              },
              "approvalcheckbox": {
                "name": "approvalcheckbox",
                "jcr:title": "I agree to the terms & conditions.",
                "sling:resourceType": "core/fd/components/form/checkbox/v1/checkbox",
                "fieldType": "checkbox",
                "required": true,
                "type": "string",
                "enum": [
                  "true"
                ]
              }
            }
          }
        }
      }
    }
  ],
  ...
}
```

## Best practice

Tieni presente quanto segue prima di creare un componente personalizzato:

- **Mantieni incentrata la logica del componente**: aggiungi/sostituisci solo ciò che è necessario per il comportamento personalizzato

- **Sfrutta la struttura di base**: utilizza l’HTML integrato come punto di partenza

- **Utilizza proprietà che supportano la modalità di authoring:** esponi opzioni configurabili tramite lo schema JSON

- **Crea uno spazio dei nomi per i tuoi CSS**: evita conflitti di stili utilizzando nomi di classe univoci

## Riferimenti

- [tipi-campo-modulo](/help/edge/docs/forms/eds-form-field-properties.md): strutture e proprietà di base di HTML per tutti i tipi di campo.

- **blocchi/moduli/modelli/componenti modulo**: definizioni di proprietà di componenti integrati e personalizzati.

- **blocchi/modulo/componenti**: posizione per i componenti personalizzati. Ad esempio: `blocks/form/components/countdown-timer/_countdown-timer.json` mostra come estendere un componente base e aggiungere nuove proprietà.
