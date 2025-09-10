---
title: Guida introduttiva a Edge Delivery Services per moduli AEM utilizzando l’editor universale
description: Scopri come creare e pubblicare moduli ad alte prestazioni utilizzando Edge Delivery Services con l’authoring WYSIWYG dell’editor universale.
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
exl-id: 24a23d98-1819-4d6b-b823-3f1ccb66dbd8
source-git-commit: fd3c53cf5a6d1c097a5ea114a831ff626ae7ad7e
workflow-type: tm+mt
source-wordcount: '2608'
ht-degree: 96%

---


# Guida introduttiva a Edge Delivery Services per moduli AEM utilizzando l’editor universale

| Metodo di authoring | Guida |
|---------------------------------|-----------------------------------------------------------------------|
| **Editor universale (WYSIWYG)** | Questo articolo |
| **Authoring basato su documenti** | [Tutorial basato su documenti](/help/edge/docs/forms/tutorial.md) |

Edge Delivery Services per AEM Forms combina la distribuzione web ad alte prestazioni con l’authoring WYSIWYG nell’editor universale. Questa guida descrive come creare, personalizzare e pubblicare moduli rapidi da caricare.

## Che cosa imparerai

Alla fine di questo tutorial sarai in grado di:

- Configurare un archivio GitHub con il blocco di moduli adattivi
- Creare un sito AEM integrato con Edge Delivery Services
- Creare e pubblicare moduli con l’editor universale
- Configurare l’ambiente di sviluppo locale

## Scegliere il percorso

Seleziona l’approccio più adatto al tuo scenario:

![Guida decisionale alla scelta del percorso](/help/edge/docs/forms/universal-editor/assets/choose-your-path.svg)
*Figura: guida visiva per aiutarti a scegliere il percorso di implementazione corretto*

| **Percorso A: nuovo progetto** | **Percorso B: progetto esistente** |
|----------------------------------------|-------------------------------------------|
| Inizia con un modello preconfigurato | Aggiungi moduli al progetto AEM corrente |
| **Ideale per:** nuove implementazioni | **Ideale per:** siti AEM esistenti |
| **Che cosa ottieni:** blocco moduli preconfigurato | **Che cosa ottieni:** moduli aggiunti al sito esistente |
| **Passaggi:** Modello → Configurazione → Moduli | **Passaggi:** Integrazione → Configurazione → Moduli |
| [Inizia con il percorso A](#path-a-create-new-project-with-forms) | [Inizia con il percorso B](#path-b-add-forms-to-existing-project) |

## Prerequisiti

Per garantire un’esperienza fluida e di successo con Edge Delivery Services per AEM Forms utilizzando l’editor universale, rivedi e conferma i seguenti prerequisiti prima di procedere:

### Requisiti di accesso

- **Account GitHub**: per creare nuovi archivi è necessario disporre di un account GitHub con autorizzazioni. Questo è essenziale per gestire il codice di origine del progetto e collaborare con il team.
- **Accesso all’authoring di AEM as a Cloud Service**: assicurati di disporre dell’accesso a livello di authoring al tuo ambiente AEM as a Cloud Service. Questo accesso è necessario per creare, modificare e pubblicare i moduli.

### Requisiti tecnici

- **Familiarità con Git**: acquisisci dimistechezza nell’eseguire operazioni Git di base quali la clonazione degli archivi, l’impegno delle modifiche e l’invio degli aggiornamenti. Queste competenze sono fondamentali per il controllo delle origini e la collaborazione nel progetto.
- **Conoscenze delle tecnologie web**: è consigliabile essere in grado di consiglia di utilizzare HTML, CSS e JavaScript. Queste tecnologie sono alla base della personalizzazione dei moduli e della risoluzione dei problemi.
- **Node.js (versione 16 o successiva)**: Node.js è necessario per lo sviluppo locale e per l’esecuzione di strumenti di creazione. Assicurati che nel sistema sia installata la versione 16 o successiva.
- **Gestione pacchetti (npm o yarn)**: per gestire le dipendenze e gli script del progetto sarà necessario npm (Gestione pacchetti nodi) o yarn.

### Esperienza pregressa consigliata

- **Concetti di AEM Sites**: una conoscenza di base di AEM Sites, inclusa la struttura del sito e l’authoring dei contenuti, ti aiuterà a navigare e integrare i moduli in modo efficace.
- **Principi di progettazione di moduli**: se hai familiarità con le best practice per la progettazione di moduli, quali usabilità, accessibilità e convalida dei dati, potrai creare moduli efficaci e di facile utilizzo.
- **Esperienza con editor WYSIWYG**: se hai esperienza con gli editor WYSIWYG (What You See Is What You Get) potrai sfruttare meglio le funzionalità di authoring visivo dell’editor universale.

>[!TIP]
>
> Nessuna esperienza con AEM? Inizia con la [Guida introduttiva a AEM Sites](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/sites/authoring/quick-start).

## Percorso A: creare un nuovo progetto con moduli

**Consigliato per:** nuovi progetti, iniziative pilota o di prova di concetto

Sfrutta i moduli standard di AEM per accelerare la configurazione del progetto. Questo standard offre un modello pronto all’uso che integra perfettamente il blocco di moduli adattivi, consentendo di creare e implementare rapidamente i moduli all’interno del sito AEM.

### Panoramica

Per avviare correttamente il nuovo progetto con moduli integrati:

1. Crea un archivio GitHub utilizzando il modello standard di moduli AEM.
2. Configura la sincronizzazione del codice AEM per automatizzare la sincronizzazione dei contenuti tra AEM e l’archivio.
3. Configura la connessione tra il progetto GitHub e l’ambiente AEM.
4. Stabilire e pubblicare un nuovo sito AEM.
5. Aggiungi e gestisci i moduli tramite l’editor universale.

Le sezioni seguenti ti guideranno nei dettagli di ogni passaggio, garantendo un’esperienza di configurazione del progetto fluida ed efficiente.

+++Passaggio 1: creare l’archivio GitHub dal modello

1. **Accedi al modello standard di moduli AEM**
   - Passa a [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms)

   ![Modello standard di moduli AEM](/help/edge/docs/forms/assets/eds-form-boilerplate.png)
   *Figura: archivio standard di moduli AEM con blocco di moduli adattivi preconfigurato*

2. **Creare l’archivio**
   - Fai clic su **Utilizza questo modello** > **Crea un nuovo archivio**

   ![Creare un archivio da un modello](/help/edge/docs/forms/assets/use-eds-form-template.png)
   *Figura: utilizzo del modello per creare un nuovo archivio*

3. **Configurare le impostazioni dell’archivio**
   - **Proprietario**: seleziona l’account GitHub o l’organizzazione
   - **Nome archivio**: scegli un nome descrittivo (ad esempio, `my-forms-project`)
   - **Visibilità**: seleziona **Pubblico** (consigliato per Edge Delivery Services)
   - Fai clic su **Crea archivio**

   ![Configurazione archivio](/help/edge/docs/forms/assets/name-eds-repo.png)
   *Figura: configurazione del nuovo archivio con visibilità pubblica*

**Convalida:** conferma di disporre di un nuovo archivio GitHub basato sul modello standard di moduli AEM.

+++

+++Passaggio 2: installare AEM Code Sync

La sincronizzazione del codice AEM sincronizza automaticamente le modifiche apportate al contenuto tra l’ambiente di authoring AEM e l’archivio GitHub.

1. **Installare l’app GitHub**
   - Passa a [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new)

2. **Configurare le autorizzazioni di accesso**
   - Seleziona **Seleziona solo archivi**
   - Scegli il nuovo archivio creato
   - Fai clic su **Salva**

   ![Installazione della sincronizzazione del codice AEM](/help/edge/docs/forms/assets/aem-code-sync-up.png)
   *Figura: installazione di sincronizzazione del codice AEM con autorizzazioni specifiche per l’archivio*

**Punti di controllo:** la sincronizzazione del codice AEM è ora installata e ha accesso al tuo archivio.

+++

+++Passaggio 3: configurare l’integrazione di AEM

Il file `fstab.yaml` connette l’archivio GitHub all’ambiente di authoring AEM per la sincronizzazione del contenuto.

1. **Passa al tuo archivio**
   - Passa all’archivio GitHub appena creato
   - Dovresti visualizzare i file standard dei moduli AEM

2. **Creare il file fstab.yaml**
   - Fai clic su **Aggiungi file** > **Crea nuovo file** nella directory principale
   - Denominare il file `fstab.yaml`

   ![Creare il file fstab.yaml](/help/edge/docs/forms/assets/open-fstab.png)
   *Figura: creazione del file di configurazione fstab.yaml*

3. **Aggiungere i dettagli della connessione AEM**

   Copia e incolla la seguente configurazione, sostituendo i segnaposto:

   ```yaml
   mountpoints:
     /: 
     url: https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main
     type: "markup" 
     suffix: ".html" 
   ```

   **Sostituisci:**
   - `<aem-author>`: URL di authoring di AEM as a Cloud Service (ad esempio, `author-p12345-e67890.adobeaemcloud.com`)
   - `<owner>`: nome utente o organizzazione GitHub
   - `<repository>`: nome dell’archivio

   **Esempio:**

   ```yaml
   mountpoints:
     /: https://author-p12345-e67890.adobeaemcloud.com/bin/franklin.delivery/mycompany/my-forms-project/main
   ```

   ![Modifica del file fstab.yaml](/help/edge/docs/forms/assets/edit-fstab-file.png)
   *Figura: configurazione del punto di montaggio per l’integrazione di AEM*

4. **Impegna la configurazione**
   - Aggiungi un messaggio di impegno: “Aggiungi configurazione integrazione di AEM”
   - Fai clic su **Impegna nuovo file**

   ![Impegno delle modifiche fstab](/help/edge/docs/forms/assets/commit-fstab-changes.png)
   *Figura: impegno della configurazione fstab.yaml*

**Convalida:** conferma la connessione tra l’archivio GitHub e AEM.

>[!NOTE]
>
> Problemi di creazione? Consulta [Risoluzione dei problemi di creazione di GitHub](#troubleshooting-github-build-issues).

+++

+++Passaggio 4: creare un sito AEM connesso all’archivio GitHub.

1. **Accedi alla console AEM Sites**
   - Accedi all’istanza di authoring di AEM as a Cloud Service
   - Passa a **Sites**

   ![Console AEM Sites](/help/edge/assets/select-sites.png)
   *Figura: accesso alla console AEM Sites*

2. **Inizia la creazione del sito**
   - Fai clic su **Crea** > **Sito da modello**.

   ![Crea opzione per sito](/help/edge/docs/forms/assets/create-sites.png)
   *Figura: creazione di un nuovo sito da modello*

3. **Seleziona il modello di Edge Delivery Services**
   - Scegli il modello **Sito di Edge Delivery Services**
   - Fai clic su **Avanti**

   ![Selezione del modello per siti](/help/edge/docs/forms/assets/select-site-template.png)
   *Figura: selezione del modello per siti di Edge Delivery Services*

   >[!NOTE]
   >
   >**Modello non disponibile?** Se non visualizzi il modello di Edge Delivery Services:
   >
   >1. Fai clic su **Importa** per caricare il modello
   >2. Scaricare modelli dalle [versioni GitHub](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases)

4. **Configurare il sito**

   Immetti le seguenti informazioni:

   | Campo | Valore | Esempio |
   |-----------------|-----------------------------|-----------------------------------------|
   | **Titolo del sito** | Nome descrittivo per il sito | “Il mio progetto di moduli” |
   | **Nome del sito** | Nome dell’URL descrittivo | “my-forms-project” |
   | **URL GitHub** | L’URL dell’archivio | `https://github.com/mycompany/my-forms-project` |

   ![Configurazione del sito](/help/edge/docs/forms/assets/create-aem-site.png)
   *Figura: configurazione del nuovo sito AEM con l’integrazione GitHub*

5. **Completare la creazione del sito**
   - Rivedi le impostazioni
   - Fai clic su **Crea**.

   ![Conferma creazione sito](/help/edge/docs/forms/assets/click-ok-aem-site.png)
   *Figura: conferma creazione sito*

   **Completato correttamente** Il sito AEM ora è stato creato e connesso a GitHub.

6. **Apri nell’editor universale**
   - Nella console Sites, individua il nuovo sito
   - Seleziona la pagina `index`
   - Fai clic su **Modifica**

   ![Modifica il sito nell’editor universale](/help/edge/docs/forms/assets/edit-site.png)
   *Figura: apertura del sito per la modifica*

   L’editor universale si apre in una nuova scheda, che fornisce funzionalità di authoring WYSIWYG.

   ![Interfaccia dell’editor universale](/help/edge/docs/forms/assets/site-in-universal-editor.png)
   *Figura: il sito aperto nell’editor universale per la modifica in WYSIWYG*

**Convalida:** conferma che il sito AEM sia pronto per l’authoring del modulo.

+++

+++Passaggio 5: pubblicare il sito

La pubblicazione rende il tuo sito disponibile su Edge Delivery Services per l’accesso globale.

1. **Pubblicazione rapida dalla console Sites**
   - Torna alla console AEM Sites
   - Seleziona le pagine del sito (o seleziona tutto con Ctrl+A)
   - Fai clic su **Pubblicazione rapida**

   ![Pubblicazione sito AEM](/help/edge/docs/forms/assets/publish-sites.png)
   *Figura: selezione delle pagine per la pubblicazione rapida*

2. **Conferma pubblicazione**
   - Nella finestra di dialogo di conferma, fai clic su **Pubblica**

   ![Finestra di dialogo di pubblicazione rapida](/help/edge/docs/forms/assets/quick-publish.png)
   *Figura: conferma dell’azione di pubblicazione*

   **Alternativa:** puoi anche pubblicare direttamente dell’editor universale utilizzando il pulsante Pubblica.

   ![Pubblica dall’editor universale](/help/edge/docs/forms/assets/qui.png)
   *Figura: pubblicazione diretta dall’editor universale*

3. **Accedi al tuo sito attivo**

   Il tuo sito è ora attivo all’indirizzo:

   ```
   https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/
   ```

   **Spiegazione struttura URL:**
   - `<branch>`: ramo GitHub (in genere `main`)
   - `<repo>`: nome dell’archivio
   - `<owner>`: nome utente o organizzazione GitHub
   - `<site-name>`: nome del sito AEM

   **Esempio:**

   ```
   https://main--my-forms-project--mycompany.aem.page/content/my-forms-project/
   ```

**Convalida:** conferma che il sito sia attivo su Edge Delivery Services.

>[!TIP]
>
> **Pattern dell’URL:**
>
> - **Pagina Home:** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`
> - **Altre pagine:** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/<page-name>`

**Avanti:** [crea il primo modulo](#create-your-first-form)

+++

## Percorso B: aggiungere moduli a un progetto esistente

**Ideale per:** siti AEM esistente con Edge Delivery Services

Se disponi già di un progetto AEM che utilizza Edge Delivery Services, puoi aggiungere funzionalità dei moduli integrando il blocco di moduli adattivi.

### Prerequisiti per il percorso B

Per procedere con l’integrazione dei moduli nel progetto AEM esistente, assicurati di soddisfare i seguenti prerequisiti:

- Possiedi un progetto AEM esistente creato con [XWalk standard di AEM](https://github.com/adobe-rnd/aem-boilerplate-xwalk).
- Hai configurato un [ambiente di sviluppo locale](#set-up-local-development-environment)
- Possiedi l’accesso a Git nell’archivio del progetti, che ti consente di clonare, modificare e inviare le modifiche in base alle esigenze.

>[!NOTE]
>
> Se il progetto è stato originariamente configurato utilizzando [moduli standard di AEM](https://github.com/adobe-rnd/aem-boilerplate-forms), la funzionalità del modulo è già inclusa. In questo caso, è possibile passare alla sezione [Crea il primo modulo](#create-your-first-form).

La guida seguente fornisce un approccio strutturato per aggiungere funzionalità di modulo al progetto esistente. Ogni fase è progettata per garantire un’integrazione diretta e funzionalità ottimale nell’ambiente di editor universale.

### Panoramica

Completerai i seguenti passaggi di alto livello:

1. Copia i file del blocco moduli adattivi nel progetto.
2. Aggiorna la configurazione del progetto per riconoscere e supportare i componenti del modulo.
3. Imposta le regole ESLint per adattarle ai nuovi file e modelli di codifica.
4. Crea il progetto e impegna le modifiche nell’archivio.

+++Passaggio 1: copiare i file di blocco di Forms

1. **Passa al progetto locale**

   ```bash
   cd /path/to/your/aem-project
   ```

2. **Scarica i file richiesti dai moduli standard di AEM**

   Copia questi file dall’[archivio di moduli standard di AEM](https://github.com/adobe-rnd/aem-boilerplate-forms):

   | Origine | Destinazione | Scopo |
   |------------------------------------------------------------------------|----------------------------|----------------------------|
   | [`blocks/form/`](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/blocks/form) | `blocks/form/` | Funzionalità modulo core |
   | [`scripts/form-editor-support.js`](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.js) | `scripts/form-editor-support.js` | Integrazione editor universale |
   | [`scripts/form-editor-support.css`](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.css) | `scripts/form-editor-support.css` | Stile dell’editor |

3. **Aggiornare il supporto dell’editor**
   - Sostituisci il file `/scripts/editor-support.js` con quello [editor-support.js dello standard di moduli di AEM](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/editor-support.js)

**Convalida:** conferma che i file del blocco del modulo siano presenti nel progetto.

+++

+++Passaggio 2: Aggiornare la configurazione del componente

1. **Aggiornare il modello della sezione**

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

   **Come funziona:** abilita i componenti del modulo nel selettore di componenti dell’editor universale.

**Convalida:** conferma i componenti del modulo che vengono visualizzati nell’editor universale.

+++

+++Passaggio 3: configurare ESLint (facoltativo)

**Perché questo passaggio:** impedisce gli errori di stampa da file specifici del modulo e configura le regole di convalida appropriate.

1. **Aggiornare .eslintignore**

   Aggiungi queste righe a `/.eslintignore`:

   ```bash
   # Form block rule engine files
   blocks/form/rules/formula/*
   blocks/form/rules/model/*
   blocks/form/rules/functions.js
   scripts/editor-support.js
   scripts/editor-support-rte.js
   ```

2. **Aggiornare .eslintrc.js**

   Aggiungi queste regole all’oggetto `rules` in `/.eslintrc.js`:

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

**Convalida:** conferma che ESLint funzioni con i componenti del modulo.

+++

+++Passaggio 4: generare e distribuire

1. **Installare le dipendenze e generare**

   ```bash
   # Install any new dependencies
   npm install
   
   # Build component definitions
   npm run build:json
   ```

   **Come funziona:**
   - Aggiorna `component-definition.json` con i componenti del modulo
   - Genera `component-models.json` con i modelli del modulo
   - Crea `component-filters.json` con regole di filtro

2. **Verifica dei file generati**

   Verifica che questi file nella directory principale del progetto contengano oggetti correlati a un modulo:
   - `component-definition.json`
   - `component-models.json`
   - `component-filters.json`

3. **Impegnare e inviare delle modifiche**

   ```bash
   git add .
   git commit -m "Add Adaptive Forms Block integration"
   git push origin main
   ```

**Convalida:** conferma che il progetto includa funzionalità del modulo.

+++

**Avanti:** [crea il primo modulo](#create-your-first-form)

## Creare il primo modulo

**Chi deve seguire questa sezione:**\
Questa sezione è pertinente per gli utenti che seguono il Percorso A (nuovo progetto) o il Percorso B (progetto esistente).

Con il progetto ora predisposto per la creazione di moduli, puoi creare il primo modulo utilizzando l’ambiente di authoring WYSIWYG intuitivo dell’editor universale. I passaggi seguenti forniscono un approccio strutturato alla progettazione, configurazione e pubblicazione di un modulo all’interno del sito AEM.

### Panoramica

Il processo di creazione di un modulo nell’editor universale consiste in diverse fasi chiave:

1. **Inserire il blocco del modulo adattivo**\
   Inizia aggiungendo il blocco di modulo adattivo alla pagina scelta.

2. **Aggiungere componenti del modulo**\
   Compilare il modulo inserendo componenti quali campi di testo, pulsanti e altri elementi di input.

3. **Configurare le proprietà del componente**\
   Regola le impostazioni e le proprietà di ciascun componente in base ai requisiti del modulo.

4. **Anteprima e test del modulo**\
   Utilizza la funzionalità di anteprima per convalidare l’aspetto e il comportamento del modulo prima della pubblicazione.

5. **Pubblicare la pagina aggiornata**\
   Una volta completata l’operazione, pubblica la pagina per rendere il modulo disponibile agli utenti finali.

Le sezioni seguenti ti guideranno nel dettaglio attraverso tutti questi passaggi, per garantire un’esperienza di creazione del modulo fluida ed efficace.

+++Passaggio 1: aggiungere un blocco di modulo adattivo

1. **Apri il modulo nell’editor universale**
   - Passa alla console **Sites** in AEM
   - Seleziona la pagina in cui desideri aggiungere un modulo (ad esempio, `index`)
   - Fai clic su **Modifica**

   La pagina viene aperta nell’editor universale per la modifica in WYSIWYG.

2. **Aggiungere il componente del modulo adattivo**
   - Apri il pannello **Struttura contenuto** (barra laterale a sinistra)
   - Passa a una sezione in cui desideri aggiungere il modulo
   - Fai clic sull’icona **Aggiungi** (+)
   - Seleziona **Modulo adattivo** dall’elenco dei componenti

   Seleziona ![Blocco modulo adattivo](/help/edge/docs/forms/assets/add-adaptive-form-block.png)
   *Figura: aggiunta di un blocco di modulo adattivo alla pagina*

**Convalida:** conferma di disporre di un contenitore di modulo vuoto.

+++

+++Passaggio 2: Aggiungere componenti modulo

1. **Passa al blocco modulo**
   - Nella struttura contenuto, individua la sezione Modulo adattivo appena aggiunta

   ![Blocco modulo adattivo aggiunto](/help/edge/docs/forms/assets/adative-form-block.png)
   *Figura: blocco modulo adattivo nella struttura contenuto*

2. **Aggiungere i componenti del modulo**

   Puoi aggiungere i componenti in due modi:

   **Metodo A: fai clic per aggiungere**
   - Fai clic sull’icona **Aggiungi** (+) nella sezione del modulo
   - Seleziona i componenti dall’elenco **Componenti del modulo adattivo**.

   **Metodo B: trascinamento**
   - Trascina i componenti direttamente dal pannello dei componenti al modulo

   ![Aggiunta dei componenti al modulo](/help/edge/docs/forms/assets/add-component.png)
   *Figura: aggiunta di componenti al modulo*

   **Componenti consigliati per iniziare**
   - Input di testo (per nome, e-mail)
   - Area di testo (per messaggi)
   - Pulsante Invia

3. **Configurare le proprietà del componente**
   - Seleziona un componente del modulo
   - Utilizza il pannello **Proprietà** (barra laterale a destra) per configurare:
      - Etichette e segnaposto
      - Regole di convalida
      - Impostazioni di campo obbligatorie

   ![Pannello delle proprietà del componente](/help/edge/docs/forms/assets/component-properties.png)
   *Figura: configurazione delle proprietà del componente*

4. **Anteprima del modulo**

   Il modulo avrà un aspetto simile a questo:

   ![Anteprima modulo completata](/help/edge/docs/forms/assets/added-form-aem-sites.png)
   *Figura: modulo di esempio creato con l’editor universale*

**Convalida:** conferma che il modulo sia pronto per la pubblicazione.

>[!IMPORTANT]
>
> Ricordati di pubblicare la pagina dopo aver apportato le modifiche per visualizzare gli aggiornamenti nel browser.

+++

+++Passaggio 3: pubblicare il modulo

1. **Pubblicare dall’editor universale**
   - Fai clic sul pulsante **Pubblica** nell’editor universale

   ![Pubblicazione del modulo](/help/edge/docs/forms/assets/publish-form.png)
   *Figura: pubblicazione del modulo dall’editor universale*

2. **Confermare la pubblicazione**
   - Nella finestra di dialogo di conferma, fai clic su **Pubblica**

   ![Conferma pubblicazione](/help/edge/docs/forms/assets/publish-form1.png)
   *Figura: conferma dell’azione di pubblicazione*

   Visualizzerai un messaggio di avvenuta conferma della pubblicazione.

   ![Pubblicazione completata](/help/edge/docs/forms/assets/publish-form2.png)
   *Figura: conferma pubblicazione avvenuta correttamente*

3. **Visualizzare il modulo attivo**

   Il modulo è ora attivo all’indirizzo:

   ```
   https://<branch>--<repo>--<owner>.aem.live/content/<site-name>/
   ```

   **URL di esempio:**

   ```
   https://main--my-forms-project--mycompany.aem.live/content/my-forms-project/
   ```

   ![Pagina del modulo attivo](/help/edge/docs/forms/assets/publish-index-page.png)
   *Figura: hai pubblicato la pagina del modulo in Edge Delivery Services*

**Congratulazioni.** Il modulo è ora attivo e pronto per raccogliere gli invii.

+++

### Passaggi successivi

Ora che possiedi un modulo funzionante, puoi:

- **Personalizzare lo stile** modificando i file CSS e JavaScript
- **Aggiungere funzioni di modulo avanzate** come regole di convalida e logica condizionale
- **Configurare lo sviluppo locale** per un’iterazione più rapida
- **Creare moduli autonomi** per casi d’uso specifici

>[!TIP]
>
> **Ulteriori informazioni:** [creare moduli autonomi nell’editor universale](/help/edge/docs/forms/universal-editor/create-forms.md)

## Configurare l’ambiente di sviluppo locale

**Ideale per:** sviluppatori che desiderano personalizzare lo stile e il comportamento dei moduli

Un ambiente di sviluppo locale consente di apportare modifiche e di visualizzarle immediatamente senza passare attraverso il ciclo di pubblicazione.

+++Configurazione di AEM CLI e sviluppo locale

1. **Installare AEM CLI**

   AEM CLI semplifica le attività di sviluppo locale:

   ```bash
       npm install -g @adobe/aem-cli
   ```

2. **Clonare l’archivio**

   ```bash
   git clone https://github.com/<owner>/<repo>
   cd <repo>
   ```

   Sostituisci `<owner>` e `<repo>` con i tuoi dettagli GitHub effettivi.

3. **Avviare il server di sviluppo locale**

   ```bash
   aem up
   ```

   Verrà avviato un server locale con funzionalità di hot-reloading.

4. **Eseguire le personalizzazioni**

   - Modifica i file nella directory `blocks/form/` per lo stile e il comportamento dei moduli
   - Modifica `form.css` per lo stile
   - Aggiorna `form.js` per il comportamento

   **Visualizza le modifiche immediatamente** nel browser all’indirizzo `http://localhost:3000`

5. **Implementare le modifiche**

   ```bash
   git add .
   git commit -m "Custom form styling"
   git push origin main
   ```

   Le modifiche saranno disponibili all’indirizzo:
   - **Anteprima:** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>`
   - **Produzione:** `https://<branch>--<repo>--<owner>.aem.live/content/<site-name>`

+++


## Risoluzione di problemi

### Problemi comuni e soluzioni

+++Problemi relativi alla build GitHub

**Problema:** errori di creazione o di linting

**Soluzione 1: gestire gli errori di linting**

Se si verificano errori di linting:

1. Apri `package.json` nella directory principale del progetto
2. Trova lo script `lint`:

   ```json
   "scripts": {
     "lint": "npm run lint:js && npm run lint:css"
   }
   ```

3. Disabilita temporaneamente il linter:

   ```json
   "scripts": {
     "lint": "echo 'skipping linting for now'"
   }
   ```

4. impegna e invia le modifiche

**Soluzione 2: errori di percorso del modulo**

Se visualizzi “Impossibile risolvere il percorso al modulo &#39;/scripts/lib-franklin.js&#39;”:

1. Passa a `blocks/form/form.js`
2. Aggiorna l’istruzione di importazione:

   ```javascript
   // Change this:
   import { ... } from '/scripts/lib-franklin.js';
   
   // To this:
   import { ... } from '/scripts/aem.js';
   ```

+++

+++Problemi relativi alla funzionalità dei moduli

**Problema:** gli invii del modulo non funzionano

**Soluzioni:**

- Assicurati di disporre di un componente pulsante Invia
- Verifica la configurazione dell’URL di azione del modulo
- Verifica le regole di convalida del modulo
- Testa prima in modalità anteprima

**Problema:** problemi di stile

**Soluzioni:**

- Verifica i percorsi del file CSS in `blocks/form/`
- Cancella la cache del browser
- Verifica la sintassi CSS
- Testa nell’ambiente di sviluppo locale

+++

+++Problemi relativi all’editor universale

**Problema:** i componenti del modulo non vengono visualizzati nell’editor universale

**Soluzioni:**

- Verifica che la sincronizzazione del codice AEM sia installata e in esecuzione
- Verifica che `fstab.yaml` disponga dell’URL di authoring AEM corretto
- Assicurati che l’istanza di AEM disponga dell’accesso anticipato abilitato
- Conferma che `component-definition.json` includa i componenti del modulo

**Problema:** modifiche non visibili dopo la pubblicazione

**Soluzioni:**

- Attendi l’aggiornamento della cache CDN
- Controlla la cache del browser (prova la modalità in incognito/privata)
- Verifica che sia utilizzato il formato URL corretto

+++



