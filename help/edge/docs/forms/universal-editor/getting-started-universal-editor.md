---
title: Guida introduttiva di Edge Delivery Services per AEM Forms con Universal Editor
description: Scopri come creare e pubblicare moduli ad alte prestazioni utilizzando Edge Delivery Services con l’authoring WYSIWYG di Universal Editor.
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
exl-id: 24a23d98-1819-4d6b-b823-3f1ccb66dbd8
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '2116'
ht-degree: 1%

---


# Guida introduttiva di Edge Delivery Services per AEM Forms con Universal Editor

| Metodo di authoring | Guida |
|---------------------------------|-----------------------------------------------------------------------|
| **Editor universale (WYSIWYG)** | Questo articolo |
| **Authoring basato su documenti** | [Tutorial basato su documenti](/help/edge/docs/forms/tutorial.md) |

Edge Delivery Services per AEM Forms combina la distribuzione web ad alte prestazioni con l’authoring WYSIWYG in Universal Editor. Questa guida descrive come creare, personalizzare e pubblicare moduli a caricamento rapido.

## Cosa realizzerai

Entro la fine di questa esercitazione:

- Configurare un archivio GitHub con il blocco Forms adattivo
- Creazione di un sito AEM integrato con Edge Delivery Services
- Creare e pubblicare moduli con Universal Editor
- Configurare l’ambiente di sviluppo locale

## Scegli il percorso

Seleziona l’approccio che corrisponde allo scenario:

![Guida alla scelta del percorso](/help/edge/docs/forms/universal-editor/assets/choose-your-path.svg)
*Figura: guida visiva per aiutarti a scegliere il percorso di implementazione corretto*

| **Percorso A: Nuovo Progetto** | **Percorso B: Progetto Esistente** |
|----------------------------------------|-------------------------------------------|
| Inizia con un modello preconfigurato | Aggiungere moduli al progetto AEM corrente |
| **Ideale per:** nuove implementazioni | **Ideale per:** AEM Sites esistente |
| **Informazioni ottenute:** Blocco Forms preconfigurato | **Informazioni ottenute:** Forms aggiunto al sito esistente |
| **Passaggi:** Installazione → modello → Forms | **Passaggi:** Integrazione → Configurazione → Forms |
| [Inizia con il percorso A](#path-a-create-new-project-with-forms) | [Inizia con il percorso B](#path-b-add-forms-to-existing-project) |

## Prerequisiti

Prima di iniziare, assicurati di avere i seguenti elementi:

### Accesso richiesto

- **Account GitHub** con autorizzazione per la creazione di archivi
- Accesso di authoring **AEM as a Cloud Service**

### Requisiti tecnici

- **Nozioni di base su Git**: operazioni di clonazione, commit e push
- **Tecnologie web**: nozioni di base su HTML, CSS e JavaScript
- **Node.js** (versione 16+ consigliata) per lo sviluppo locale
- Gestione pacchetti **npm** o **yarn**

### Conoscenza consigliata

- Nozioni di base sui concetti di AEM Sites
- Familiarità con i principi di progettazione dei moduli
- Esperienza con gli editor di WYSIWYG

>[!TIP]
>
> Ti avvicini ora ad AEM? Inizia con la [Guida introduttiva di AEM Sites](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/sites/authoring/quick-start).

## Percorso A: Creare un nuovo progetto con Forms

**Ideale per:** nuove implementazioni o prove di concetti

AEM Forms Boilerplate fornisce un modello preconfigurato con Adaptive Forms Block integrato.

### Panoramica dei passaggi

1. Configurare un archivio GitHub dal modello
2. Installare AEM Code Sync
3. Configurare la connessione al progetto AEM
4. Creare e pubblicare un sito AEM
5. Aggiungere moduli tramite l’Editor universale

Passiamo ad ogni passaggio:

+++Passaggio 1: creare l’archivio GitHub dal modello

1. **Accedi al modello standard di AEM Forms**
   - Vai a [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms)

   ![Modello standard AEM Forms](/help/edge/docs/forms/assets/eds-form-boilerplate.png)
   *Figura: repository AEM Forms Boilerplate con blocco Forms adattivo preconfigurato*

2. **Crea il tuo archivio**
   - Fai clic su **Usa questo modello** > **Crea un nuovo archivio**

   ![Crea archivio da modello](/help/edge/docs/forms/assets/use-eds-form-template.png)
   *Figura: utilizzo del modello per creare un nuovo repository*

3. **Configura impostazioni archivio**
   - **Proprietario**: seleziona il tuo account o organizzazione GitHub
   - **Nome archivio**: scegliere un nome descrittivo (ad esempio, `my-forms-project`)
   - **Visibilità**: Seleziona **Pubblico** (consigliato per Edge Delivery Services)
   - Fai clic su **Crea archivio**

   ![Configurazione archivio](/help/edge/docs/forms/assets/name-eds-repo.png)
   *Figura: configurazione del nuovo archivio con visibilità pubblica*

**Convalida:** verifica di disporre di un nuovo archivio GitHub basato sul modello standard di AEM Forms.

+++

+++Passaggio 2: installare AEM Code Sync

AEM Code Sync sincronizza automaticamente le modifiche apportate ai contenuti tra l’ambiente di authoring AEM e l’archivio GitHub.

1. **Installa l&#39;app GitHub**
   - Vai a [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new)

2. **Configurare le autorizzazioni di accesso**
   - Seleziona **Solo archivi**
   - Scegli il nuovo archivio creato
   - Fai clic su **Salva**

   ![Installazione di AEM Code Sync](/help/edge/docs/forms/assets/aem-code-sync-up.png)
   *Figura: installazione di AEM Code Sync con autorizzazioni specifiche per l&#39;archivio*

**Checkpoint:** AEM Code Sync è ora installato e ha accesso al tuo archivio.

+++

+++Passaggio 3: configurare l’integrazione di AEM

Il file `fstab.yaml` collega l&#39;archivio GitHub all&#39;ambiente di authoring AEM per la sincronizzazione dei contenuti.

1. **Accedi al tuo repository**
   - Vai all’archivio GitHub appena creato
   - Dovresti visualizzare i file Boilerplate di AEM Forms

2. **Crea il file fstab.yaml**
   - Fai clic su **Aggiungi file** > **Crea nuovo file** nella directory principale
   - Denomina il file `fstab.yaml`

   ![Creazione del file fstab.yaml](/help/edge/docs/forms/assets/open-fstab.png)
   *Figura: creazione del file di configurazione fstab.yaml*

3. **Aggiungi i dettagli della connessione AEM**

   Copia e incolla la seguente configurazione, sostituendo i segnaposto:

   ```yaml
   mountpoints:
     /: https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main
   ```

   **Sostituisci:**
   - `<aem-author>`: URL dell&#39;autore di AEM as a Cloud Service (ad esempio, `author-p12345-e67890.adobeaemcloud.com`)
   - `<owner>`: nome utente o organizzazione GitHub
   - `<repository>`: nome del repository

   **Esempio:**

   ```yaml
   mountpoints:
     /: https://author-p12345-e67890.adobeaemcloud.com/bin/franklin.delivery/mycompany/my-forms-project/main
   ```

   ![Modifica del file fstab.yaml](/help/edge/docs/forms/assets/edit-fstab-file.png)
   *Figura: configurazione del punto di montaggio per l&#39;integrazione AEM*

4. **Eseguire il commit della configurazione**
   - Aggiungi un messaggio di commit: &quot;Aggiungi configurazione integrazione AEM&quot;
   - Fare clic su **Conferma nuovo file**

   ![Commit delle modifiche fstab](/help/edge/docs/forms/assets/commit-fstab-changes.png)
   *Figura: commit della configurazione fstab.yaml*

**Convalida:** Conferma la connessione dell&#39;archivio GitHub ad AEM.

>[!NOTE]
>
>Problemi di build? Consulta [Risoluzione dei problemi di compilazione GitHub](#troubleshooting-github-build-issues).

+++

+++Passaggio 4: crea un sito AEM connesso all’archivio GitHub.

1. **Accedi alla console AEM Sites**
   - Accedi all’istanza di authoring di AEM as a Cloud Service
   - Passa a **Sites**

   ![Console AEM Sites](/help/edge/assets/select-sites.png)
   *Figura: accesso alla console AEM Sites*

2. **Avvia creazione sito**
   - Fai clic su **Crea** > **Sito da modello**

   ![Crea opzione sito](/help/edge/docs/forms/assets/create-sites.png)
   *Figura: creazione di un nuovo sito dal modello*

3. **Seleziona il modello Edge Delivery Services**
   - Scegli il modello **Sito Edge Delivery Services**
   - Fai clic su **Avanti**

   ![Selezione modello sito](/help/edge/docs/forms/assets/select-site-template.png)
   *Figura: selezione del modello di sito Edge Delivery Services*

   >[!NOTE]
   >
   >**Modello non disponibile?** Se non vedi il modello Edge Delivery Services:
   >
   >1. Fai clic su **Importa** per caricare il modello
   >2. Scarica modelli da [Versioni GitHub](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases)

4. **Configura il sito**

   Immettere le seguenti informazioni:

   | Campo | Valore | Esempio |
   |-----------------|-----------------------------|-----------------------------------------|
   | **Titolo sito** | Nome descrittivo del sito | &quot;Il mio progetto Forms&quot; |
   | **Nome sito** | Nome descrittivo dell’URL | &quot;my-forms-project&quot; |
   | **URL GitHub** | URL archivio | `https://github.com/mycompany/my-forms-project` |

   ![Configurazione sito](/help/edge/docs/forms/assets/create-aem-site.png)
   *Figura: configurazione del nuovo sito AEM con integrazione GitHub*

5. **Creazione completa del sito**
   - Verifica le impostazioni
   - Fai clic su **Crea**.

   ![Conferma creazione sito](/help/edge/docs/forms/assets/click-ok-aem-site.png)
   *Figura: conferma creazione sito*

   **Operazione completata.** Il sito AEM è stato creato e connesso a GitHub.

6. **Apri in Universal Editor**
   - Nella console Sites, individua il nuovo sito
   - Seleziona la pagina `index`
   - Fai clic su **Modifica**

   ![Modifica sito in Universal Editor](/help/edge/docs/forms/assets/edit-site.png)
   *Figura: apertura del sito per la modifica*

   L’Editor universale si apre in una nuova scheda, che fornisce funzionalità di authoring WYSIWYG.

   ![Interfaccia editor universale](/help/edge/docs/forms/assets/site-in-universal-editor.png)
   *Figura: il sito è stato aperto in Universal Editor per la modifica in WYSIWYG*

**Convalida:** verifica che il sito AEM sia pronto per l&#39;authoring dei moduli.

+++

+++Passaggio 5: Pubblicare Il Sito

La pubblicazione rende il tuo sito disponibile su Edge Delivery Services per l’accesso globale.

1. **Pubblicazione rapida dalla console Sites**
   - Torna alla console AEM Sites
   - Seleziona le pagine del sito (o seleziona tutto con Ctrl+A)
   - Fai clic su **Pubblicazione rapida**

   ![Pubblicazione del sito AEM](/help/edge/docs/forms/assets/publish-sites.png)
   *Figura: selezione delle pagine per la pubblicazione rapida*

2. **Conferma pubblicazione**
   - Nella finestra di dialogo di conferma, fai clic su **Pubblica**

   ![Finestra di dialogo Pubblicazione rapida](/help/edge/docs/forms/assets/quick-publish.png)
   *Figura: conferma dell&#39;azione di pubblicazione*

   **Alternativa:** Puoi anche pubblicare direttamente da Universal Editor utilizzando il pulsante Pubblica.

   ![Pubblica da Universal Editor](/help/edge/docs/forms/assets/qui.png)
   *Figura: pubblicazione diretta da Universal Editor*

3. **Accedi al tuo sito attivo**

   Il tuo sito è ora attivo in:

   ```
   https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/
   ```

   **Spiegazione struttura URL:**
   - `<branch>`: ramo GitHub (in genere `main`)
   - `<repo>`: nome del repository
   - `<owner>`: nome utente o organizzazione GitHub
   - `<site-name>`: nome del sito AEM

   **Esempio:**

   ```
   https://main--my-forms-project--mycompany.aem.page/content/my-forms-project/
   ```

**Convalida:** Verifica che il tuo sito sia attivo su Edge Delivery Services.

>[!TIP]
>
> **Modelli URL:**
>
> - **Home page:** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`
> - **Altre pagine:** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/<page-name>`

**Avanti:** [Crea il primo modulo](#create-your-first-form)

+++

## Percorso B: Aggiungere Forms a un progetto esistente

**Ideale per:** AEM Sites esistente con Edge Delivery Services

Se disponi già di un progetto AEM che utilizza Edge Delivery Services, puoi aggiungere funzionalità di moduli integrando il blocco di Forms adattivo.

### Prerequisiti per il percorso B

- Progetto AEM esistente creato con [AEM Boilerplate XWalk](https://github.com/adobe-rnd/aem-boilerplate-xwalk)
- Configurazione dell’ambiente di sviluppo locale
- Accesso Git all’archivio del progetto

**Utilizzo di AEM Forms Boilerplate?** Se il progetto è stato creato con [AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms), i moduli sono già integrati. Passa a [Crea il primo modulo](#create-your-first-form).

Passiamo ad ogni passaggio:

### Panoramica dei passaggi

1. Copiare file di blocco Forms adattivi
2. Aggiorna configurazione progetto
3. Configurare le regole ESLint
4. Generare e confermare le modifiche

+++Passaggio 1: copiare i file di blocco di Forms

1. **Accedi al progetto locale**

   ```bash
   cd /path/to/your/aem-project
   ```

2. **Scarica i file richiesti da AEM Forms Boilerplate**

   Copia questi file dall&#39;[archivio AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms):

   | Sorgente | Destinazione | Scopo |
   |------------------------------------------------------------------------|----------------------------|----------------------------|
   | [`blocks/form/`](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/blocks/form) | `blocks/form/` | Funzionalità modulo core |
   | [`scripts/form-editor-support.js`](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.js) | `scripts/form-editor-support.js` | Integrazione con Universal Editor |
   | [`scripts/form-editor-support.css`](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.css) | `scripts/form-editor-support.css` | Stile dell’editor |

3. **Supporto dell&#39;editor di aggiornamenti**
   - Sostituisci il file `/scripts/editor-support.js` con [editor-support.js di AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/editor-support.js)

**Convalida:** Verificare che i file del blocco del modulo siano presenti nel progetto.

+++

+++Passaggio 2: Aggiornare la configurazione del componente

1. **Aggiorna modello sezione**

   Apri `/models/_section.json` e aggiungi i componenti del modulo ai filtri:

   ```json
   {
        "filters": [
        {
      "id": "section",
      "components": [
           "text",
           "image",
           "button",
        "form",
        "embed-adaptive-form"
      ]
       }
     ]
   }
   ```

   **Funzionamento:** abilita i componenti modulo nel selettore di componenti di Universal Editor.

**Convalida:** I componenti modulo di conferma vengono visualizzati nell&#39;editor universale.

+++

+++Passaggio 3: configurare ESLint (facoltativo)

**Perché questo passaggio:** impedisce gli errori di evidenziazione dai file specifici del modulo e configura le regole di convalida appropriate.

1. **Aggiorna .eslintignore**

   Aggiungi queste righe a `/.eslintignore`:

   ```bash
   # Form block rule engine files
    blocks/form/rules/formula/*
    blocks/form/rules/model/*
    blocks/form/rules/functions.js
    scripts/editor-support.js
    scripts/editor-support-rte.js
   ```

2. **Aggiorna .eslintrc.js**

   Aggiungi queste regole all&#39;oggetto `rules` in `/.eslintrc.js`:

   ```javascript
   {
     "rules": {
       // Existing rules...
   
       // Form component cell limits
    'xwalk/max-cells': ['error', {
         '*': 4, // default limit
      form: 15,
      wizard: 12,
      'form-button': 7,
      'checkbox-group': 20,
      checkbox: 19,
      'date-input': 21,
      'drop-down': 19,
      email: 22,
      'file-input': 20,
      'form-fragment': 15,
      'form-image': 7,
      'multiline-input': 23,
      'number-input': 22,
      panel: 17,
      'radio-group': 20,
      'form-reset-button': 7,
      'form-submit-button': 7,
      'telephone-input': 20,
      'text-input': 23,
      accordion: 14,
      modal: 11,
      rating: 18,
      password: 20,
         tnc: 12
       }],
   
       // Disable this rule for forms
       'xwalk/no-orphan-collapsible-fields': 'off'
     }
   }
   ```

**Convalida:** Verificare che ESLint funzioni con i componenti del modulo.

+++

+++Passaggio 4: generare e distribuire

1. **Installare dipendenze e build**

   ```bash
   # Install any new dependencies
   npm install
   
   # Build component definitions
   npm run build:json
   ```

   **Funzionamento:**
   - Aggiorna `component-definition.json` con i componenti modulo
   - Genera `component-models.json` con modelli modulo
   - Crea `component-filters.json` con regole di filtro

2. **Verifica file generati**

   Verifica che questi file nella directory principale del progetto contengano oggetti correlati a un modulo:
   - `component-definition.json`
   - `component-models.json`
   - `component-filters.json`

3. **Commit e push delle modifiche**

   ```bash
   git add .
   git commit -m "Add Adaptive Forms Block integration"
   git push origin main
   ```

**Convalida:** Verificare che il progetto includa funzionalità modulo.

+++

**Avanti:** [Crea Il Primo Modulo](#create-your-first-form)

## Creare il primo modulo

**Si applica a:** utenti sia percorso A che percorso B

Ora che il progetto è configurato con funzionalità di modulo, creiamo il primo modulo utilizzando l’interfaccia WYSIWYG di Universal Editor.

### Panoramica del processo di creazione dei moduli

1. **Aggiungi il blocco modulo adattivo** alla pagina
2. **Aggiungi componenti modulo** (input testo, pulsanti, ecc.)
3. **Configura proprietà componente**
4. **Anteprima e verifica** il modulo
5. **Pubblica** la pagina aggiornata

Passiamo ad ogni passaggio:

+++Passaggio 1: aggiungere un blocco di modulo adattivo

1. **Apri la pagina in Universal Editor**
   - Passa alla console **Sites** in AEM
   - Selezionare la pagina in cui si desidera aggiungere un modulo, ad esempio `index`
   - Fai clic su **Modifica**

   La pagina viene aperta in Universal Editor per la modifica con WYSIWYG.

2. **Aggiungere il componente Modulo adattivo**
   - Apri il pannello **Struttura contenuto** (barra laterale a sinistra)
   - Passare a una sezione in cui si desidera aggiungere il modulo
   - Fai clic sull&#39;icona **Aggiungi** (+)
   - Seleziona **Modulo adattivo** dall&#39;elenco dei componenti

   ![Aggiunta del blocco del modulo adattivo](/help/edge/docs/forms/assets/add-adaptive-form-block.png)
   *Figura: aggiunta di un blocco di modulo adattivo alla pagina*

**Convalida:** Verificare di disporre di un contenitore di moduli vuoto.

+++

+++Passaggio 2: Aggiungere componenti modulo

1. **Passa al blocco del modulo**
   - Nella struttura del contenuto, individua la sezione Modulo adattivo appena aggiunta

   ![Blocco modulo adattivo aggiunto](/help/edge/docs/forms/assets/adative-form-block.png)
   *Figura: blocco modulo adattivo nella struttura contenuto*

2. **Aggiungi componenti modulo**

   È possibile aggiungere componenti in due modi:

   **Metodo A: fare clic per aggiungere**
   - Fai clic sull&#39;icona **Aggiungi** (+) nella sezione del modulo
   - Seleziona componenti dall&#39;elenco **Componenti modulo adattivo**

   **Metodo B: trascinamento**
   - Trascina i componenti direttamente dal pannello dei componenti al modulo

   ![Aggiunta di componenti modulo](/help/edge/docs/forms/assets/add-component.png)
   *Figura: aggiunta di componenti al modulo*

   **Componenti iniziali consigliati:**
   - Input testo (per nome, e-mail)
   - Area di testo (per i messaggi)
   - Pulsante Invia

3. **Configura proprietà componente**
   - Seleziona un componente modulo
   - Utilizza il pannello **Proprietà** (barra laterale a destra) per configurare:
      - Etichette e segnaposto
      - Regole di convalida
      - Impostazioni campo obbligatorie

   ![Pannello Proprietà Componente](/help/edge/docs/forms/assets/component-properties.png)
   *Figura: configurazione delle proprietà del componente*

4. **Anteprima modulo**

   Il modulo avrà un aspetto simile al seguente:

   ![Anteprima modulo completata](/help/edge/docs/forms/assets/added-form-aem-sites.png)
   *Figura: modulo di esempio creato con Universal Editor*

**Convalida:** Verificare che il modulo sia pronto per la pubblicazione.

>[!IMPORTANT]
>
> Ricordati di pubblicare la pagina dopo aver apportato modifiche per visualizzare gli aggiornamenti nel browser.

+++

+++Passaggio 3: Pubblicare Il Modulo

1. **Pubblica da Universal Editor**
   - Fai clic sul pulsante **Pubblica** in Universal Editor

   ![Modulo di pubblicazione](/help/edge/docs/forms/assets/publish-form.png)
   *Figura: pubblicazione del modulo da Universal Editor*

2. **Conferma pubblicazione**
   - Nella finestra di dialogo di conferma, fai clic su **Pubblica**

   ![Conferma pubblicazione](/help/edge/docs/forms/assets/publish-form1.png)
   *Figura: conferma dell&#39;azione di pubblicazione*

   Verrà visualizzato un messaggio di conferma della pubblicazione.

   ![Pubblicazione completata](/help/edge/docs/forms/assets/publish-form2.png)
   *Figura: conferma pubblicazione completata*

3. **Visualizza il tuo modulo live**

   Il modulo è ora disponibile in:

   ```
   https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/
   ```

   **URL di esempio:**

   ```
   https://main--my-forms-project--mycompany.aem.page/content/my-forms-project/
   ```

   ![Pagina Live Form](/help/edge/docs/forms/assets/publish-index-page.png)
   *Figura: la pagina del modulo pubblicato in Edge Delivery Services*

**Congratulazioni!** Il modulo è ora attivo e pronto per raccogliere gli invii.

+++

### Passaggi successivi

Dopo aver creato un modulo di lavoro, è possibile:

- **Personalizza lo stile** modificando i file CSS e JavaScript
- **Aggiungi funzionalità modulo avanzate** come regole di convalida e logica condizionale
- **Configura lo sviluppo locale** per un&#39;iterazione più veloce
- **Crea moduli autonomi** per casi d&#39;uso specifici

>[!TIP]
>
> **Ulteriori informazioni:** [Creare moduli autonomi in Universal Editor](/help/edge/docs/forms/universal-editor/create-forms.md)

## Configurare l’ambiente di sviluppo locale

**Ideale per:** sviluppatori che desiderano personalizzare lo stile e il comportamento dei moduli

Un ambiente di sviluppo locale consente di apportare modifiche e di visualizzarle immediatamente senza passare attraverso il ciclo di pubblicazione.

+++Configurazione di AEM CLI e sviluppo locale

1. **Installa AEM CLI**

   AEM CLI semplifica le attività di sviluppo locale:

   ```bash
   npm install -g @adobe/aem-cli
   ```

2. **Clona l&#39;archivio**

   ```bash
   git clone https://github.com/<owner>/<repo>
   cd <repo>
   ```

   Sostituisci `<owner>` e `<repo>` con i tuoi dettagli GitHub effettivi.

3. **Avvia il server di sviluppo locale**

   ```bash
   aem up
   ```

   Verrà avviato un server locale con funzionalità di ricaricamento a caldo.

4. **Personalizzazioni**

   - Modificare i file nella directory `blocks/form/` per lo stile e il comportamento dei moduli
   - Modifica `form.css` per lo stile
   - Aggiorna `form.js` per il comportamento

   **Visualizza modifiche all&#39;istante** nel browser in `http://localhost:3000`

5. **Distribuisci le modifiche**

   ```bash
   git add .
   git commit -m "Custom form styling"
   git push origin main
   ```

   Le modifiche saranno disponibili all&#39;indirizzo:
   - **Anteprima:** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>`
   - **Produzione:** `https://<branch>--<repo>--<owner>.aem.live/content/<site-name>`

+++


## Risoluzione dei problemi

### Problemi comuni e soluzioni

+++Problemi relativi alla build di GitHub

**Problema:** errori di compilazione o di puntamento

**Soluzione 1: Gestire Gli Errori Di Linting**

Se si verificano errori di evidenziazione:

1. Apri `package.json` nella directory principale del progetto
2. Trova lo script `lint`:

   ```json
   "scripts": {
     "lint": "npm run lint:js && npm run lint:css"
   }
   ```

3. Disabilita temporaneamente l&#39;evidenziazione:

   ```json
   "scripts": {
     "lint": "echo 'skipping linting for now'"
   }
   ```

4. Eseguire il commit e inviare le modifiche

**Soluzione 2: errori nel percorso del modulo**

Se vedi &quot;Impossibile risolvere il percorso del modulo &#39;/scripts/lib-franklin.js&#39;&quot;:

1. Passa a `blocks/form/form.js`
2. Aggiornare l&#39;istruzione di importazione:

   ```javascript
   // Change this:
   import { ... } from '/scripts/lib-franklin.js';
   
   // To this:
   import { ... } from '/scripts/aem.js';
   ```

+++

+++Problemi relativi all’editor universale

**Problema:** componenti modulo non visualizzati nell&#39;editor universale

**Soluzioni:**

- Verificare che AEM Code Sync sia installato e in esecuzione
- Verifica che `fstab.yaml` abbia l&#39;URL di authoring AEM corretto
- Assicurati che l’istanza di AEM disponga dell’accesso anticipato abilitato
- Conferma l&#39;inclusione di `component-definition.json` componenti modulo

**Problema:** modifiche non visibili dopo la pubblicazione

**Soluzioni:**

- Attesa dell’aggiornamento della cache CDN
- Controlla la cache del browser (prova la modalità in incognito/privata)
- Verifica che sia utilizzato il formato URL corretto

+++

+++Problemi relativi alla funzionalità dei moduli

**Problema:** invii modulo non funzionanti

**Soluzioni:**

- Assicurati di disporre di un componente pulsante Invia
- Verifica configurazione URL azione modulo
- Verificare le regole di convalida del modulo
- Esegui prima il test in modalità anteprima

**Problema:** problemi di stile

**Soluzioni:**

- Controlla percorsi file CSS in `blocks/form/`
- Cancella cache del browser
- Verificare la sintassi CSS
- Test nell’ambiente di sviluppo locale

+++

