---
title: Creare componenti personalizzati per un modulo EDS
description: Creare componenti personalizzati per un modulo EDS
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 2bbe3f95-d5d0-4dc7-a983-7a20c93e2906
source-git-commit: 9664495d17ad8a8101c886408bee1584b3d48f1e
workflow-type: tm+mt
source-wordcount: '2103'
ht-degree: 4%

---


# Creazione del componente Modulo personalizzato nel blocco di modulo adattivo

I moduli di Edge Delivery Services offrono funzionalità di personalizzazione e permettono agli sviluppatori front-end di creare componenti per moduli su misura. Questi componenti personalizzati si integrano direttamente nell’esperienza di authoring WYSIWYG, consentendo agli autori di moduli di aggiungerli, configurarli e gestirli facilmente nell’editor di moduli. I componenti personalizzati permettono agli autori di ottimizzare le funzionalità dei moduli. Inoltre, assicurano un processo di authoring fluido e intuitivo.

Questo documento illustra i passaggi necessari per creare componenti personalizzati assegnando uno stile ai componenti per moduli HTML nativi, migliorando l’esperienza utente e aumentando l’impatto visivo dei moduli stessi.

## Panoramica dell’architettura

Il componente personalizzato per il blocco Forms segue un pattern di architettura **MVC (Model-View-Controller)**:

### Modello

- Definito dallo schema JSON per ogni `field/component`.

- Le proprietà che possono essere create sono specificate nel file JSON corrispondente (consulta blocchi/moduli/modelli/componenti modulo).

- Queste proprietà sono disponibili per gli autori nel generatore di moduli e vengono passate al componente come parte della definizione del campo (fd).

### Visualizzazione

- La struttura di HTML per ogni tipo di campo è descritta in form-field-types (Tipi di campo modulo).

- Si tratta della struttura di base del componente che può essere estesa o modificata.

- La struttura HTML di base per ciascun componente OOTB è documentata in tipi di campo modulo.

### Logica controller/componente

- Implementato in JavaScript, come componente predefinito o personalizzato.  - Disponibile in `blocks/form/components` per i componenti personalizzati.

## Componenti preconfigurati

I componenti **preconfigurati** forniscono le basi per lo sviluppo personalizzato:

- Componenti inclusi in `blocks/form/models/form-components`.

- Ogni componente OOTB dispone di un file JSON che definisce le relative proprietà modificabili (ad esempio,` _text-input.json`,`_drop-down.json`).

- Queste proprietà sono disponibili per gli autori nel generatore di moduli e vengono passate al componente come parte della definizione del campo (fd).

- La struttura HTML di base per ciascun componente OOTB è documentata in tipi di campo modulo.

L’estensione di un componente OOTB esistente consente di riutilizzarne la struttura, il comportamento e le proprietà di base e al contempo di personalizzarlo in base alle tue esigenze.

- I componenti personalizzati devono estendersi da un set predefinito di componenti OOTB.

- Il sistema identifica il componente OOTB da estendere in base alla proprietà `viewType` nel JSON del campo.

- Il sistema gestisce un registro delle varianti di componenti personalizzati consentite. È possibile utilizzare solo le varianti elencate in questo registro, ad esempio `customComponents[]` in `mappings.js`.

- Durante il rendering di un modulo, il sistema controlla la proprietà variante o `:type/fd:viewType` e, se corrisponde a un componente personalizzato registrato, carica i file JS e CSS corrispondenti dalla cartella `blocks/form/components`.

- Il componente personalizzato viene quindi applicato alla struttura HTML di base del componente OOTB, consentendoti di migliorarne o escluderne il comportamento e l’aspetto.

## Struttura del componente personalizzato

Per creare componenti personalizzati, è possibile utilizzare **Scaffolder CLI** per configurare i file e le cartelle necessari per il componente e quindi aggiungere il codice per il componente personalizzato.

- I componenti personalizzati si trovano nella cartella `blocks/form/components`.

- Ogni componente personalizzato deve essere inserito nella propria cartella, denominata dopo il componente, ad esempio le schede. All’interno della cartella, i seguenti file dovrebbero essere:

   - **_cards.json** - Il file JSON che estende la definizione del componente OOTB, definisce le proprietà modificabili (modelli[]) e la struttura del contenuto al caricamento (definizioni[]).
   - **cards.js**: il file JavaScript che include la logica principale.
   - **cards.css** - facoltativo, per gli stili.

- Il nome della cartella e i file JS/CSS devono corrispondere.

### Riutilizzo ed estensione dei campi nei componenti personalizzati

Quando definisci i campi nel JSON del componente personalizzato (per qualsiasi gruppo di campi, base, convalida, guida, ecc.), segui le best practice per la manutenibilità e la coerenza:

- Riutilizzare i campi standard/condivisi facendo riferimento a contenitori condivisi o definizioni di campi esistenti (ad esempio, `../form-common/_basic-input-placeholder-fields.json#/fields`, `../form-common/_basic- validation-fields.json#/fields`). In questo modo puoi ereditare tutte le opzioni standard senza duplicarle.

- Aggiungi esplicitamente solo campi nuovi o personalizzati nel contenitore. In questo modo lo schema rimane DRY e mirato.

- Rimuovi o evita di duplicare i campi già inclusi tramite riferimenti. Definisci solo campi univoci per la logica del componente.

- Fare riferimento ai contenitori della Guida e ad altri contenuti condivisi (ad esempio, `../form-common/_help-container.json`) come necessario per coerenza e manutenibilità.

>[!TIP]
>
> - Questo modello consente di aggiornare o estendere facilmente la logica in futuro e garantisce che i componenti personalizzati rimangano coerenti con il resto del sistema del modulo.
> - Prima di aggiungere nuovi contenitori o definizioni di campi condivisi, controlla sempre quelli esistenti.

### Definizione di nuove proprietà per i componenti personalizzati

- Se devi acquisire nuove proprietà per il componente personalizzato dagli autori, puoi farlo definendo un campo nell&#39;array `fields[]` del componente nel JSON del componente.

- Il componente personalizzato viene identificato utilizzando la proprietà :type, che può essere impostata come `fd:viewType` nel file JSON (ad esempio, `fd:viewType: cards`). Questo consente al sistema di riconoscere e caricare il componente personalizzato corretto e pertanto è obbligatorio per i componenti personalizzati

- Tutte le nuove proprietà aggiunte nella definizione JSON sono disponibili nella definizione del campo come proprietà. `<propertyName>` nella logica JS del componente

## API JavaScript del componente personalizzato

L’API JavaScript del componente personalizzato definisce come controllare il comportamento, l’aspetto e la reattività del componente del modulo personalizzato.

### Funzione Decorate

La funzione **decorate** è il punto di ingresso del componente personalizzato. Inizializza il componente, lo collega alla sua definizione JSON e consente di manipolarne la struttura e il comportamento HTML.

>[!NOTE]
>
> Il file JavaScript del componente personalizzato deve esportare una funzione predefinita come decorato:

#### Firma funzione:

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

- **Modifica l&#39;elemento**: aggiungi listener di eventi, aggiorna attributi o inserisci markup aggiuntivo.

- **Accedere alle proprietà JSON**: utilizzare `fd.properties.<propertyName>` per leggere i valori definiti nello schema JSON e applicarli nella logica del componente.

## Funzione Subscribe

La funzione **subscribe** consente al componente di reagire alle modifiche nei valori dei campi o agli eventi personalizzati. In questo modo il componente rimane sincronizzato con il modello dati del modulo e può aggiornare dinamicamente la sua interfaccia utente.

### Firma funzione:

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

- **Registra un callback**: chiamando **subscribe(element, formId, callback)** si registra il callback da eseguire ogni volta che i dati del campo cambiano.Utilizzare due parametri di callback:
   - **elemento**: l&#39;elemento HTML che rappresenta il campo.
   - **fieldModel**: oggetto che rappresenta le API evento e lo stato del campo.

- **Ascolta modifiche o eventi**: utilizza `fieldModel.subscribe((event) => { ... }, 'eventName')` per eseguire la logica ogni volta che un valore cambia o viene attivato un evento personalizzato. L’oggetto evento contiene dettagli sulle modifiche apportate.

## Creazione di un componente personalizzato

In questa sezione verrà illustrato il processo di creazione di un componente personalizzato **per** schede estendendo il componente pulsante di opzione OOTB.

![Componente personalizzato scheda](/help/edge/docs/forms/universal-editor/assets/cc-ue-card-component.png)

### &#x200B;1. Impostazione del codice

#### 1.1 File e cartelle

Il primo passaggio consiste nell’impostare i file necessari del componente personalizzato e collegarlo al codice nell’archivio. Questo processo viene eseguito automaticamente da **AEM Forms Scaffolder CLI**, rendendo più rapido lo scaffolding e il cablaggio dei file necessari.

>[!VIDEO](https://video.tv.adobe.com/v/3474752)

1. Apri il terminale e passa alla directory principale del progetto modulo.
2. Esegui i seguenti comandi:

```bash
npm install
npm run create:custom-component
```

![CLI scaffolder](/help/edge/docs/forms/universal-editor/assets/scaffolder-cli.png)

Essa:

- **Richiedi di denominare** il nuovo componente. Ad esempio, in questo caso utilizza le schede.
- **Chiedi di scegliere** un componente di base (seleziona un gruppo di opzioni)

In questo modo vengono creati tutti i file e le cartelle necessari, tra cui:

```
blocks/form/
└── components/
  └── cards/
    ├── cards.js
    └── cards.css
    └── _cards.json
```

E la collega con il resto del codice nell&#39;archivio come mostrato nell&#39;output della CLI.
Esegue automaticamente le seguenti funzionalità:

- Aggiunge schede ai filtri per consentirne l’aggiunta all’interno del blocco di modulo adattivo.
- Aggiorna il inserisco nell&#39;elenco Consentiti di `mappings.js` per includere il nuovo componente Schede.
- Registra la definizione del componente Schede nell&#39;elenco **Componenti personalizzati** in Universal Editor.

>[!NOTE]
>
> Puoi anche creare un componente personalizzato utilizzando il metodo manuale (legacy). Per informazioni dettagliate, consulta la sezione [Metodo manuale o legacy](#manual-or-legacy-method-to-create-custom-component) per creare un componente personalizzato.

#### 1.2 Utilizzo del componente nell’editor universale

1. **Aggiorna Universal Editor**: apri il modulo nell&#39;Universal Editor e aggiorna la pagina per assicurarti che venga caricato il codice più recente dall&#39;archivio.

2. **Aggiungi componente personalizzato**

   1. Fare clic sul pulsante **Aggiungi (+)** nell&#39;area di lavoro del modulo.
   2. Scorri fino alla sezione Componenti personalizzati.
   3. Seleziona il componente **Schede** appena creato per inserirlo nel modulo.

      ![Seleziona componente personalizzato](/help/edge/docs/forms/universal-editor/assets/select-custom-component.png)

Poiché non è presente alcun codice all&#39;interno di `cards.js`, il componente personalizzato viene riprodotto come gruppo radio.

#### 1.3 Anteprima e test in locale

Ora che il modulo contiene il componente personalizzato, è possibile inoltrare il modulo e apportarvi modifiche a livello locale e visualizzare le modifiche:

1. Vai al tuo terminale ed esegui `aem up`.

2. Aprire il server proxy avviato alle `http://localhost:3000/{path-to-your-form}` (esempio di percorso: `/content/forms/af/custom-component-form`)


### &#x200B;2. Implementazione del comportamento personalizzato per il componente personalizzato

#### 2.1 Personalizzazione dello stile del componente personalizzato

Aggiungiamo una **scheda** di classe al componente per la creazione dello stile e aggiungiamo un&#39;immagine per ogni radio. A tale scopo, utilizza il codice seguente.

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

Ora, il componente Schede viene visualizzato come segue:

![aggiungi css e js per schede](/help/edge/docs/forms/universal-editor/assets/add-card-css.png)

#### 2.2 Aggiunta di un comportamento dinamico tramite la funzione di abbonamento

Quando il menu a discesa viene modificato, le schede vengono recuperate e impostate nell&#39;enum del gruppo radio. Ma attualmente la visualizzazione non è in grado di gestire questo problema. Viene quindi eseguito il rendering come mostrato di seguito:

![funzione di abbonamento](/help/edge/docs/forms/universal-editor/assets/card-subscribe.png)

Quando viene chiamata API, imposta il campo Modello e deve ascoltare le modifiche ed eseguire di conseguenza il rendering della vista. Questa operazione viene eseguita utilizzando la funzione **subscribe**.

Convertiamo il codice di visualizzazione del passaggio precedente in una funzione e chiamiamolo all&#39;interno della funzione di sottoscrizione in `cards.js` come illustrato di seguito:

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

**Utilizza la funzione di abbonamento per ascoltare le modifiche all&#39;evento in cards.js**

Ora, quando cambi il menu a discesa, le schede si popolano come mostrato di seguito:

![funzione di abbonamento](/help/edge/docs/forms/universal-editor/assets/card-subscribe-final.png)

#### 2.3 Sincronizzazione degli aggiornamenti delle visualizzazioni con il modello dei campi

Per sincronizzare le modifiche della visualizzazione al campo Modello, è necessario impostare il valore della scheda selezionata. Quindi, aggiungi il seguente listener di eventi di modifica in cards.js come mostrato di seguito:

**Utilizzo dell&#39;API Field Model in cards.js**

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

Ora viene visualizzato il componente scheda personalizzato, come illustrato di seguito:

![Componente personalizzato scheda](/help/edge/docs/forms/universal-editor/assets/cc-ue-card-component.png)

### &#x200B;3. Commit e push delle modifiche

Dopo aver implementato JavaScript e CSS per il componente personalizzato e averlo verificato localmente, esegui il commit e invia le modifiche all’archivio Git.

```bash
git add . && git commit -m "Add card custom component" && git push
```

È stato creato un componente complesso per la selezione della scheda personalizzata in alcuni semplici passaggi.

+++ **Metodo manuale o legacy per creare il componente personalizzato**

Il modo precedente per farlo è seguire manualmente i passaggi descritti di seguito:

1. **Scegliere un componente OOTB** da estendere (ad esempio, pulsante, elenco a discesa, immissione di testo e così via). In questo caso, estendere il componente radio.

2. **Crea una cartella** in `blocks/form/components` con il nome del componente (schede in questo caso).

3. **Aggiungi un file JS** con lo stesso nome:
   - `blocks/form/components/cards/cards.js`.

4. (Facoltativo) **Aggiungi un file CSS** per gli stili personalizzati:
   - `blocks/form/components/cards/cards.css.`

5. **Definisci un nuovo file JSON** (ad esempio,` _cards.json`) nella stessa cartella del file JS **componente** (`blocks/form/components/cards/_cards.json`). Questo JSON deve estendere un componente esistente e nelle sue definizioni, imposta `fd:viewType` al nome del componente (in questo caso, schede):

   - Per tutti i gruppi di campi (di base, di convalida, della Guida, ecc.) aggiungi esplicitamente i campi personalizzati.

6. **Implementare la logica JS e CSS:**
   - Esporta una funzione predefinita come descritto in precedenza.
   - Utilizza il parametro **element** per modificare la struttura HTML di base.
   - Utilizza il parametro **fieldJson** se necessario per i dati del campo standard.
   - Utilizza la funzione **subscribe** per ascoltare le modifiche al campo o gli eventi personalizzati, se necessario.

     >[!NOTE]
     >
     >Implementa la logica JS e CSS per il componente personalizzato, come spiegato in precedenza.

7. Registra il componente come variante nel generatore di moduli e imposta la proprietà variante o
   `fd:viewType/:type` nel JSON al nome del componente, ad esempio, aggiungi il valore `fd:viewType` da `definitions[]` come schede all&#39;array dei componenti dell&#39;oggetto con `id="form`.

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

8. **Aggiorna mappings.js**: aggiungi il nome del componente all&#39;elenco **OOTBComponentDecorators** (per i componenti stile OOTB) o **customComponents** in modo che venga riconosciuto e caricato dal sistema.

   ```javascript
   let customComponents = ["cards"];
   const OOTBComponentDecorators = [];
   ```

9. **Aggiorna _form.json**: aggiungi il nome del componente all&#39;array `filters.components` in modo che possa essere eliminato nell&#39;interfaccia utente di creazione.

   ```javascript
   "filters": [
   {
       "id": "form",
       "components": [ "cards"]}
       ]
   ```

10. **Aggiorna _component-definition.json**: in `models/_component-definition.json` aggiorna l&#39;array all&#39;interno del gruppo con `id custom-components` con un oggetto nel modo seguente:

    ```javascript
    {
    "...":"../blocks/form/components/cards/_cards.json#/definitions"
    }
    ```

    In questo modo si fornisce il riferimento al nuovo componente Schede da creare con gli altri componenti

11. **Esegui lo script :json della build**: esegui `npm run build:json` per compilare e unire tutte le definizioni JSON dei componenti in un unico file da distribuire dal server. In questo modo lo schema del nuovo componente viene incluso nell’output unito.

12. Esegui il commit e invia le modifiche all’archivio Git.

Ora è possibile aggiungere il componente personalizzato al modulo.

+++

## Creare un componente composito

Un componente composito viene creato combinando più componenti.
Ad esempio, un componente composito di Termini e Condizioni è costituito da un pannello principale che contiene:

- Campo di testo normale per la visualizzazione dei termini

- Casella di controllo per acquisire il consenso dell&#39;utente

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

- **Mantieni incentrata la logica del componente**: aggiungi/sovrascrivi solo ciò che è necessario per il comportamento personalizzato

- **Sfruttare la struttura di base**: utilizzare il HTML OOTB come punto di partenza

- **Utilizza proprietà modificabili:** espone opzioni configurabili tramite lo schema JSON

- **Spazio dei nomi CSS**: evita conflitti di stili utilizzando nomi di classe univoci

## Riferimenti

- [tipi-campo-modulo](/help/edge/docs/forms/eds-form-field-properties.md): strutture e proprietà di base di HTML per tutti i tipi di campo.

- **blocchi/moduli/modelli/componenti modulo**: definizioni di proprietà OOTB e di componenti personalizzati.

- **blocchi/moduli/componenti**: posizione per i componenti personalizzati. Ad esempio: `blocks/form/components/countdown-timer/_countdown-timer.json` mostra come estendere un componente base e aggiungere nuove proprietà.
