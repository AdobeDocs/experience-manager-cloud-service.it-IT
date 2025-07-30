---
title: 'Guida introduttiva a Edge Delivery Services per AEM Forms nell’editor universale: tutorial per sviluppatori'
description: Questo tutorial ti mostrerà come iniziare subito con un nuovo progetto Adobe Experience Manager Forms (AEM). Tra dieci o venti minuti, avrai creato i tuoi moduli di Edge Delivery Services nell’editor universale.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 24a23d98-1819-4d6b-b823-3f1ccb66dbd8
source-git-commit: 0e7375adb146c370a189127838d736290d1860ad
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Guida introduttiva a Edge Delivery Services per AEM Forms utilizzando l’editor universale (WYSIWYG)

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| Authoring basato sull’editor universale | Questo articolo |
| Authoring basato su documenti | [Fai clic qui](/help/edge/docs/forms/tutorial.md) |


<span class="preview"> Questa funzione è disponibile tramite il programma per i primi utilizzatori. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo ufficiale a <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> con il nome dell’organizzazione GitHub e il nome dell’archivio. Ad esempio, se l’URL dell’archivio è https://github.com/adobe/abc, il nome dell’organizzazione è adobe e il nome dell’archivio è abc.</span>

Nell’era digitale di oggi, i moduli facili da usare sono essenziali per qualsiasi organizzazione. I moduli di Edge Delivery Services vengono creati utilizzando l’Editor universale, che offre funzionalità WYSIWYG (what-you-see-is-what-you-get). Fornisce un’interfaccia moderna e intuitiva per l’authoring efficiente dei moduli.

AEM Forms fornisce un blocco, noto come Blocco di moduli adattivi, per facilitare la creazione di moduli di Edge Delivery Services per l’acquisizione e l’archiviazione dei dati. È possibile [creare un nuovo progetto AEM preconfigurato con Blocco moduli adattivi](#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) oppure [aggiungere il Blocco moduli adattivi a un progetto AEM esistente](#add-adaptive-forms-block-to-your-existing-aem-project).

![Flusso di lavoro archivio Github](/help/edge/assets/repo-workflow.png){width=auto}

Questo tutorial ti consente di creare, visualizzare in anteprima e pubblicare un modulo personalizzato con un progetto di sito Adobe Experience Manager nuovo o esistente mediante l’authoring WYSIWYG dell’editor universale.

## Prerequisiti

* Hai un account GitHub e conosci le nozioni di base su Git.
* Comprendi le nozioni di base di HTML, CSS e JavaScript.
* Hai Node/npm installato per lo sviluppo locale.

## Crea un nuovo progetto AEM preconfigurato con Blocco moduli adattivi

Il modello standard di AEM Forms consente di iniziare rapidamente un progetto AEM preconfigurato con il Blocco moduli adattivi. È il modo più rapido e semplice per seguire le best practice di AEM e passare direttamente alla creazione dei moduli.

### Introduzione al modello di archivio standard di AEM Forms

1. Crea un archivio GitHub per il progetto AEM. Per creare l’archivio:
   1. Passa a [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms).

      ![AEM Forms standard](/help/edge/docs/forms/assets/eds-form-boilerplate.png)
   1. Fai clic su **Usa questo modello** e seleziona l’opzione **Crea un nuovo archivio**.

      ![Creare un nuovo archivio con il modello standard per AEM Forms](/help/edge/docs/forms/assets/use-eds-form-template.png)

      Viene visualizzata la schermata **Crea nuovo archivio**.

   1. Nella schermata **Crea nuovo archivio**, seleziona il **proprietario** e specifica **Nome archivio**. Adobe consiglia di impostare l’archivio su **Pubblico**. Quindi, seleziona l’opzione **pubblico** e fai clic su **Crea archivio**.

      ![Impostare l’archivio su pubblico](/help/edge/docs/forms/assets/name-eds-repo.png)

1. Installa l’app GitHub della sincronizzazione del codice AEM nell’archivio. Per installare:
   1. Passa a [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new).
   1. Nella schermata **Installa sincronizzazione codice AEM**, seleziona **Seleziona solo archivi** e seleziona quello appena creato. Fai clic su **Salva**.

   ![Impostare l’archivio su pubblico](/help/edge/docs/forms/assets/aem-code-sync-up.png)

1. Ora collega l’archivio GitHub creato utilizzando il Modello di archivio standard per AEM Forms al tuo ambiente di authoring di progetti AEM. Per connettersi:

   1. vai all’archivio GitHub che hai creato in precedenza utilizzando moduli AEM ricorrenti.
   1. Aggiungi il file **fstab.yaml** nella cartella principale.

      ![apri file fstab.yaml](/help/edge/docs/forms/assets/open-fstab.png)

   1. Aggiungi il punto di montaggio del progetto al file **fstab.yaml**. Aggiungi l’URL dell’istanza di authoring di AEM as a Cloud Service.
      `https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main`

      ![modifica file fstab.yaml](/help/edge/docs/forms/assets/edit-fstab-file.png)

   1. Esegui il commit del file **fstab.yaml**, dopo aver aggiunto il riferimento e tutto sembra a posto.

      ![conferma le modifiche](/help/edge/docs/forms/assets/commit-fstab-changes.png)

      Se riscontri problemi di build, consulta [Risoluzione dei problemi di build di GitHub](#troubleshooting-github-build-issues).

### Creare un nuovo progetto AEM

Ora che disponi di un progetto GitHub, puoi procedere con la creazione e la pubblicazione di un nuovo progetto AEM nell’istanza di authoring di AEM as a Cloud Service.

1. Per creare un nuovo progetto AEM:

   1. Accedi all’istanza di authoring di AEM as a Cloud Service e seleziona **Sites**.

      ![seleziona Sites](/help/edge/assets/select-sites.png)

   1. Fai clic su **Crea** > **Sito da modello**.

      ![create-sites](/help/edge/docs/forms/assets/create-sites.png)

   1. Seleziona il modello Sito Edge Delivery Services e fai clic su **Avanti**.

      ![select-site-template](/help/edge/docs/forms/assets/select-site-template.png)

      >[!NOTE]
      >
      > * Se il modello Sito Edge Delivery Services non è disponibile nell’istanza di authoring, fai clic sul pulsante Importa per caricare il modello.
      > * È possibile scaricare i modelli per siti Edge Delivery Services da [GitHub](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases).

   1. Immetti i seguenti dettagli per creare un nuovo progetto AEM:
      * **Titolo sito**: aggiungi un titolo descrittivo per il sito.
      * **Titolo sito**: utilizza il `site-name` che hai definito nel passaggio precedente.
      * **URL GitHub**: utilizza l’URL del progetto GitHub creato nel passaggio precedente.

      ![crea sito AEM](/help/edge/docs/forms/assets/create-aem-site.png)

   1. Viene visualizzata la finestra di dialogo **Crea sito**. Fai clic su **OK**.

      ![fai clic su ok](/help/edge/docs/forms/assets/click-ok-aem-site.png)

      In pochi minuti viene creato il nuovo progetto AEM.

   1. Passa al progetto AEM appena creato nella console Sites e fai clic su **Modifica**.
In questo caso, la pagina `index.html` viene utilizzata a scopo illustrativo.

      ![modifica sito AEM](/help/edge/docs/forms/assets/edit-site.png)

      Il progetto AEM si apre nell’editor universale in una nuova scheda, che abilita l’authoring in modalità WYSIWYG. È ora possibile modificare il progetto AEM.

      ![Il sito si apre nell’editor universale](/help/edge/docs/forms/assets/site-in-universal-editor.png)

1. Pubblicare il progetto AEM creato

   Una volta terminata la modifica del progetto AEM, è il momento di pubblicarlo. Per pubblicarlo:

   1. Nella console Sites, seleziona tutte le pagine del progetto AEM e fai clic su **Pubblicazione rapida**.

      ![pubblicare il progetto AEM Sites](/help/edge/docs/forms/assets/publish-sites.png)

   1. Viene visualizzata la finestra di dialogo di conferma **Pubblicazione rapida**. Fai clic su **Pubblica** per avviare il processo di pubblicazione.

      ![Finestra di dialogo di conferma per Pubblicazione rapida](/help/edge/docs/forms/assets/quick-publish.png)

      In alternativa, è possibile pubblicare le pagine dei progetti AEM direttamente dall’interfaccia utente dell’editor universale.

      ![Finestra di dialogo di conferma per Pubblicazione rapida](/help/edge/docs/forms/assets/qui.png)

   Congratulazioni Hai un nuovo sito web in esecuzione su `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`.

   * `<branch>` fa riferimento al ramo dell’archivio GitHub.
   * `<repository>` denota l’archivio GitHub.
   * `<owner>` fa riferimento al nome utente dell’account GitHub che ospita l’archivio GitHub.
   * `<site-name>` fa riferimento al nome del sito creato.

   Ad esempio, se il nome del ramo è `main`, l’archivio è `edsforms`, il proprietario è `wkndforms` e `site-name` è `eds-forms`, il sito web sarà operativo e funzionante all’indirizzo `https://main--edsforms--wkndforms.aem.page/content/eds-forms/`

   >[!NOTE]
   >
   > * Per visualizzare la pagina `index.html` del progetto AEM, utilizza l’URL: `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`
   > * Per visualizzare pagine diverse da `index page` del progetto AEM, utilizza l’URL: `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/<site-page-name>`

Puoi iniziare a [creare e aggiungere moduli al progetto AEM](#add-edge-delivery-services-forms-to-aem-project).

## Aggiungere un blocco per moduli adattivi al progetto AEM esistente

Se disponi di un progetto AEM esistente, puoi integrare il blocco di moduli adattivi nel progetto corrente per iniziare a creare il modulo.

>[!NOTE]
>
>
> Questo passaggio si applica ai progetti generati con il [XWalk standard AEM](https://github.com/adobe-rnd/aem-boilerplate-xwalk). Se hai creato il progetto AEM utilizzando [AEM Forms standard](https://github.com/adobe-rnd/aem-boilerplate-forms), puoi saltare questo passaggio.

Per integrare:

1. Passa alla cartella dell’archivio di progetto AEM nel sistema locale.

1. Copia e incolla le cartelle e i file seguenti dal [ modello AEM standard](https://github.com/adobe-rnd/aem-boilerplate-forms) nel tuo progetto AEM:

   * Cartella [blocco modulo](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/blocks/form)
   * File [form-editor-support.js](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.js)
   * File [form-editor-support.css](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.css)
1. Passa al file `/scripts/editor-support.js` nel progetto AEM e aggiornalo con il file[editor-support.js nel modello standard AEM](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/editor-support.js)
1. Passa a `/models/_section.json` nel progetto AEM e aggiungi “modulo” e “modulo adattivo incorporato” all’array dei componenti dell’oggetto `filters`:

   ```
       "filters": [
       {
     "id": "section",
     "components": [
       .
       .
       .
       "form",
       "embed-adaptive-form"
     ]
    }]
   ```

1. (Facoltativo) Passa a `/.eslintignore` nel progetto AEM e aggiungi le seguenti righe di codice:

   ```
   blocks/form/rules/formula/*
   blocks/form/rules/model/*
   blocks/form/rules/functions.js
   scripts/editor-support.js
   scripts/editor-support-rte.js
   ```

1. (Facoltativo) Passa a `/.eslintrc.js` nel progetto AEM e aggiungi le righe di codice sottostanti nell’oggetto `rules`:

   ```
   'xwalk/max-cells': ['error', {
     '*': 4, // default limit for all models
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
     tnc: 12,
   }],
   'xwalk/no-orphan-collapsible-fields': 'off', // Disable until enhancement is done for Forms properties
   ```

1. Apri il terminale ed esegui i seguenti comandi:

   ```
   npm i
   npm run build:json
   ```

   >[!NOTE]
   >
   > Prima di inviare le modifiche all’archivio di progetto AEM su GitHub, assicurati che i file `component-definition.json`, `component-models.json` e `component-filters.json` che si trovano al livello principale del progetto AEM siano aggiornati con gli oggetti relativi al modulo.

1. Conferma e implementa queste modifiche al progetto AEM su GitHub.

   <!--
    1. **Update ESLint configuration file**
    2. Navigate to the `../.eslintignore` file in your AEM Project and add the following line of codes to prevent errors related to the Form Block rule engine:
        
            blocks/form/rules/formula/*
            blocks/form/rules/model/*
       * [form-common](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/models/form-common)  folder
       * [form-components](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/models/form-components) folder
    
     3. **Update component definitions and models files**
       1. Navigate to the `../models/_component-definition.json` file in your AEM Project and update it with the changes from the [_component-definition.json file in the AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/models/_component-definition.json#L39-L48).
    
    3. Navigate to the `../models/_component-models.json` file in your AEM Project and update it with the changes from the [_component-models.json file in the AEM Forms Boilerplate](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/models/_component-models.json#L24-L26) -->

Tutto qui. Il blocco di moduli adattivi fa ora parte del progetto AEM. Puoi [iniziare a creare e aggiungere moduli al progetto AEM](#add-edge-delivery-services-forms-to-aem-site-project).

## Creare moduli utilizzando WYSIWYG

Puoi aprire il progetto AEM nell’editor universale per l’authoring WYSIWYG, dove puoi modificare il progetto e aggiungere la sezione Modulo adattivo per includere i moduli Edge Delivery Services nelle pagine del progetto AEM.

1. Aggiungi la sezione Modulo adattivo alla pagina del progetto AEM. Per aggiungere:
   1. Passa al progetto AEM nella console Sites, seleziona la pagina del sito da modificare e fai clic su **Modifica**. La pagina del progetto AEM viene aperta nell’editor universale per la modifica.
In questo caso, la pagina `index.html` viene utilizzata a scopo illustrativo.
   1. Apri la Struttura contenuto e passa alla sezione in cui desideri aggiungere la sezione Modulo adattivo.
   1. Fai clic sull’icona **[!UICONTROL Aggiungi]** e seleziona il componente **[!UICONTROL Modulo adattivo]** dall’elenco dei componenti.

   ![struttura contenuto](/help/edge/docs/forms/assets/add-adaptive-form-block.png)

   La sezione Modulo adattivo è stata aggiunta. È ora possibile iniziare ad aggiungere i componenti del modulo alla pagina Progetto AEM.

1. Aggiungi componenti del modulo alla sezione Modulo adattivo aggiunta. Per aggiungere componenti del modulo:
   1. Passa alla sezione Modulo adattivo aggiunto nella Struttura contenuto.

      ![blocco modulo adattivo aggiunto](/help/edge/docs/forms/assets/adative-form-block.png)


   1. Fai clic sull’icona **[!UICONTROL Aggiungi]** e aggiungi i componenti desiderati dall’elenco **Componenti modulo adattivo**.

      ![aggiungi componente](/help/edge/docs/forms/assets/add-component.png)

      È inoltre possibile trascinare i componenti dei Moduli adattivi richiesti, in quanto l’editor universale offre una funzione di trascinamento intuitiva.

   1. Seleziona il componente Modulo adattivo aggiunto e aggiornane le proprietà utilizzando **[!UICONTROL Proprietà]**.

      ![apri proprietà](/help/edge/docs/forms/assets/component-properties.png)

   1. Visualizza l’anteprima del modulo.
La schermata seguente mostra il modulo creato nel progetto AEM utilizzando l’authoring WYSIWYG:

      ![modulo aggiunto](/help/edge/docs/forms/assets/added-form-aem-sites.png)

      Quando l’anteprima risulta soddisfacente, l’utente può procedere alla pubblicazione della pagina.

      >[!NOTE]
      >
      > È importante pubblicare nuovamente la pagina del progetto AEM dopo aver apportato modifiche; in caso contrario, gli aggiornamenti non saranno visibili nel browser.

1. Pubblicare nuovamente la pagina del progetto AEM.

   1. Fai clic su **Pubblica** per pubblicare nuovamente la pagina del progetto AEM dopo aver aggiunto il modulo.

      ![pubblica modulo](/help/edge/docs/forms/assets/publish-form.png)

   1. Viene visualizzata la finestra di dialogo di conferma di **Pubblicazione**. Fai clic su **Pubblica** per avviare la pubblicazione.

      ![pubblica modulo1](/help/edge/docs/forms/assets/publish-form1.png)

      Dopo aver fatto clic sul pulsante **Pubblica**, viene visualizzato il messaggio `Publish started successfully`.

      ![pubblica modulo2](/help/edge/docs/forms/assets/publish-form2.png)

   È ora possibile visualizzare la pagina del progetto AEM con il modulo Edge Delivery Services aggiunto al seguente URL:
   `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`.

   Ad esempio, se il nome del ramo è `main`, l’archivio è `edsforms`, il proprietario è `wkndforms` e il nome del sito è `eds-forms`, l’URL sarà:
   `https://main--edsforms--wkndforms.aem.page/content/eds-forms/`

   ![indice pagina](/help/edge/docs/forms/assets/publish-index-page.png)

Puoi assegnare uno stile ai moduli di Edge Delivery Services modificando i file `.css` e `.js` nel blocco moduli adattivi e [configurando un ambiente di sviluppo AEM locale](#set-up-local-aem-development-environment) per visualizzare le modifiche istantaneamente nel browser.

>[!NOTE]
>
> È inoltre possibile [creare un modulo autonomo nell’editor universale e pubblicarlo in Edge Delivery Services](/help/edge/docs/forms/universal-editor/create-forms.md).

## Configurare un ambiente di sviluppo AEM locale

Puoi configurare un ambiente di sviluppo AEM locale per sviluppare stili e componenti personalizzati a livello locale. Per essere operativi con un ambiente di sviluppo AEM locale:

1. **Installa AEM CLI**: AEM CLI semplifica le attività di sviluppo. Installalo a livello globale utilizzando npm:

   ```Bash
       npm install -g @adobe/aem-cli
   ```

1. **Clona il progetto GitHub**: clona l’archivio del progetto da GitHub utilizzando il seguente comando, sostituendolo <owner> con il proprietario dell’archivio e <repo> con il nome dell’archivio:

   ```
   git clone https://github.com/<owner>/<repo>
   ```

1. **Avvia l’ambiente locale**: passa alla directory del progetto e attiva l’istanza AEM locale con un singolo comando:

   ```
   cd <repo>
   aem up
   ```

È possibile apportare modifiche locali nella cartella Blocco moduli adattivi `blocks/form` per la formattazione e la codifica dei moduli. Modifica i file `.css` o `.js` all’interno di questa directory e le modifiche saranno immediatamente applicate nel browser.

Una volta completate le modifiche, utilizza i comandi Git per confermarle e inviarle. Questo aggiorna gli ambienti di anteprima e di produzione accessibili tramite questi URL (sostituisci i segnaposto con i dettagli del progetto):

Anteprima: `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>`

Produzione: `https://<branch>--<repo>--<owner>.aem.live/content/<site-name>`


## Risoluzione dei problemi di compilazione di GitHub

Assicurati un processo di compilazione di GitHub senza intoppi affrontando potenziali problemi:

* **Gestire errori di stampa:**
in caso di errori di stampa, è possibile ignorarli. Apri il file [Progetto EDS]/package.json e modifica lo script “lint” da `"lint": "npm run lint:js && npm run lint:css"` a `"lint": "echo 'skipping linting for now'"`. Salva il file e conferma le modifiche nel progetto GitHub.

* **Errore del percorso del modulo di risoluzione**
Se riscontri l’errore “Impossibile risolvere il percorso del modulo ”‘/scripts/lib-franklin.js’, passa al file [Progetto EDS]/blocks/forms/form.js. Aggiorna l’istruzione di importazione sostituendo il file lib-franklin.js con il file aem.js.

## Consulta anche

{{universal-editor-see-also}}
