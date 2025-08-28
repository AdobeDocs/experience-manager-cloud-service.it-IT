---
title: 'Guida introduttiva a Edge Delivery Services per AEM Forms: tutorial per sviluppatori'
description: Questo tutorial ti mostrerà come essere subito operativo con un nuovo progetto di Adobe Experience Manager Forms (AEM). Ti basteranno 10-20 minuti per creare i tuoi moduli personalizzati.
feature: Edge Delivery Services
exl-id: bb7e93ee-0575-44e1-9c5e-023284c19490
role: Admin, Architect, Developer
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: ht
source-wordcount: '1921'
ht-degree: 100%

---

# Guida introduttiva: tutorial per sviluppatori

Nell’era digitale di oggi, la creazione di moduli facili da usare è essenziale per qualsiasi organizzazione. Edge Delivery Services per AEM Forms consente di creare moduli utilizzando strumenti noti come Documenti Google e Microsoft Office.

Questi moduli inviano i dati direttamente a un file Microsoft Excel o Fogli Google, consentendo di utilizzare un ecosistema dinamico e API affidabili di Fogli Google, Microsoft Excel e Microsoft SharePoint per elaborare facilmente i dati inviati o avviare un flusso di lavoro aziendale esistente.

AEM Forms fornisce un blocco, noto come blocco di moduli adattivi, per facilitare la creazione di moduli per l’acquisizione e l’archiviazione dei dati acquisiti. Puoi [creare un nuovo progetto AEM preconfigurato con un blocco per moduli adattivi](#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) <!--or [add the Adaptive Forms Block to an existing AEM project](#add-adaptive-forms-block-to-your-existing-aem-project)-->.

Questa esercitazione di AEM Forms ti guida attraverso la creazione, l’anteprima e la pubblicazione di un modulo personalizzato con un nuovo progetto Adobe Experience Manager (AEM) Forms.

## Prerequisiti

- Hai un account GitHub e conosci le nozioni di base su Git.
- Hai un account Google o Microsoft SharePoint.
- Comprendi le nozioni di base di HTML, CSS e JavaScript.
- Hai Node/npm installato per lo sviluppo locale.

**Attenzione!** Questo tutorial utilizza macOS, Chrome e Visual Studio Code. Anche se i passaggi possono essere adattati per altre impostazioni, le schermate e gli elementi specifici dell’interfaccia utente potrebbero variare in base al sistema operativo, al browser e all’editor di codice scelti.


## Crea un nuovo progetto AEM preconfigurato con Blocco moduli adattivi

Il modello standard di AEM Forms consente di iniziare rapidamente un progetto AEM preconfigurato con il Blocco moduli adattivi. È il modo più rapido e semplice per seguire le best practice di AEM e passare direttamente alla creazione dei moduli.

### Introduzione al modello di archivio standard di AEM Forms

1. Crea un archivio GitHub per il progetto AEM. Per creare l’archivio:
   1. Passa a [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms).

      ![AEM Forms standard](/help/edge/docs/forms/assets/eds-form-boilerplate.png)
   1. Fai clic su **Usa questo modello** e seleziona l’opzione **Crea un nuovo archivio**. Viene visualizzata la schermata Crea nuovo archivio.

      ![Creare un nuovo archivio con AEM Forms standard](/help/edge/docs/forms/assets/use-eds-form-template.png)

   1. Nella schermata Crea nuovo archivio, seleziona **proprietario** e specifica **Nome archivio**. Adobe consiglia di impostare l’archivio su **Pubblico**. Quindi, seleziona l’opzione **pubblico** e fai clic su **Crea archivio**.

   ![Impostare l’archivio su pubblico](/help/edge/assets/create-a-new-repo-keep-it-public.png)


1. Installa l’app GitHub della sincronizzazione del codice AEM nell’archivio. Per installare:
   1. Passa a [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new).
   1. Nella schermata Installa sincronizzazione codice AEM, seleziona **Seleziona solo archivi** e seleziona quello appena creato. Fai clic su Salva.

   ![Impostare l’archivio su pubblico](/help/edge/assets/install-aem-code-sync-app-for-your-repo.png)

   >[!NOTE]
   >
   >
   > Se utilizzi GitHub Enterprise con filtro IP, puoi aggiungere il seguente IP all’elenco Consentiti: 3.227.118.73

   Congratulazioni Hai un nuovo sito web in esecuzione su `https://<branch>--<repo>--<owner>.aem.page/`.

   - `<branch>` fa riferimento al ramo dell’archivio GitHub.
   - `<repository>` denota l’archivio GitHub.
   - `<owner>` fa riferimento al nome utente dell’account GitHub che ospita l’archivio GitHub.

   Ad esempio, se il nome del ramo è `main`, l’archivio è `wefinance` e il proprietario è `wkndforms`, il sito web sarà operativo e funzionante all’indirizzo `https://main--wefinance--wkndforms.aem.page`
&lt;!—(https://main--wefinance--wkndform.aem.page)-->

### Collegare l’origine del proprio contenuto

<!--Your newly created GitHub repository points to [example content stored in a Google Drive folder](https://drive.google.com/drive/folders/1bvjfi6TqpYA7DvbX6kKc-m7FgHuJ4RUQ). This read-only content provides a great starting point for your forms. Feel free to copy it into your own Google Drive and customize it to fit your needs.

![Sample Content on Google Drive](/help/edge/assets/folder-with-sample-content.png)-->

Per copiare il contenuto di esempio nella cartella del contenuto e indirizzarvi l’archivio GitHub:

1. crea una nuova cartella specifica per il contenuto AEM in Google Drive o Microsoft SharePoint. Questo documento utilizza una cartella creata in Microsoft SharePoint.

1. Condividi la cartella con l’utente di Adobe Experience Manager (forms@adobe.com).

   ![Utilizza l’opzione Gestisci accesso per condividere la cartella con l’utente AEM - SharePoint](/help/edge/assets/share-folder-with-aem-user.png)

   ![Utilizza l’opzione Gestisci accesso per condividere la cartella con l’utente AEM - Google Drive](/help/edge/assets/share-google-drive-folder.png)


   Assicurati di aver fornito all’utente di Adobe Experience Manager le autorizzazioni di modifica per la cartella.

   ![Condividi la cartella con l’utente AEM e fornisci le autorizzazioni di modifica-SharePoint](/help/edge/assets/share-folder-with-aem-user-provide-editing-access.png){width=50%}

   ![Condividi la cartella con l’utente AEM e fornisci le autorizzazioni di modifica - Google Drive](/help/edge/assets/add-aem-user-google-folder.png){width=50%}

1. Copia il [contenuto di esempio](/help/edge/assets/wefinance1.zip) nella cartella. Per copiare:

   1. Decomprimi la cartella scaricata e copia il contenuto.

      ![Scarica contenuto di esempio](/help/edge/assets/download-sample-content.png)

      I file `nav` e `footer` definiscono il layout di base delle pagine e cambiano raramente durante un progetto. Inoltre, dispongono di una struttura specifica diversa dalla maggior parte degli altri file di contenuto. Esaminando questi file capirai come il contenuto viene organizzato nei progetti AEM.


   1. Carica questi file nella cartella Microsoft SharePoint o Google Drive.

      ![Contenuto di esempio su Google Drive](/help/edge/assets/upload-sample-files-to-your-content-folder.png)

      Assicurati di copiare il foglio `enquiry` dal contenuto di esempio nella cartella su Google Drive o Microsoft SharePoint. Questo contiene la struttura per un modulo di esempio.

1. Ora che hai configurato la cartella dei contenuti, puoi collegarla al progetto su GitHub che hai creato utilizzando precedentemente moduli AEM ricorrenti. Per connettersi:

   1. vai all’archivio GitHub che hai creato in precedenza utilizzando moduli AEM ricorrenti.
   1. Aggiungi il file `fstab.yaml` nella cartella principale.
   1. Aggiungi il riferimento con il percorso della cartella condivisa con l’utente AEM (forms@adobe.com).

      ![Contenuto di esempio su Google Drive](/help/edge/assets/replace-path-in-fstab-yaml-with-your-content-folder.png)


      Se utilizzi Microsoft SharePoint, il percorso della cartella utilizza il formato seguente:

      ```HTML
      https://<tenant>.SharePoint.com/sites/<sp-site>/Shared%20Documents/<folder-name>
      ```

      Ad esempio,

      ```HTML
      https://adobe.SharePoint.com/sites/wkndforms/Shared%20Documents/wefinance
      ```

      Per ulteriori informazioni sulla gestione dei file con Microsoft SharePoint, consulta [Come usare Adobe SharePoint](https://www.aem.live/docs/setup-customer-sharepoint).


   1. Conferma l’aggiornamento del file `fsatb.yaml` dopo aver aggiunto il riferimento e tutto sembra a posto. Se riscontri problemi di build, consulta [Risoluzione dei problemi di build di GitHub](#troubleshooting-github-build-issues).

      ![Conferma l’aggiornamento del file fsatab.yaml](/help/edge/assets/commit-updated-fstab-yaml.png)

      Questo consente di collegare la cartella dei contenuti al sito web. Dopo aver aggiornato il riferimento, potresti riscontrare inizialmente gli errori “404 non trovato”. Questo perché il contenuto non è ancora stato visualizzato in anteprima. Nella sezione successiva viene illustrato come iniziare a creare e visualizzare in anteprima i contenuti.

### Visualizzare in anteprima e pubblicare il contenuto

Dopo aver completato l’ultimo passaggio, la nuova origine di contenuto non è vuota, ma non sarà visibile sul sito web finché non viene promossa nell’anteprima o nelle fasi live. Attualmente, ciò potrebbe causare errori 404.

Per visualizzare in anteprima il contenuto non pubblicato:

1. installa l’estensione Chrome denominata [AEM Sidekick](https://chrome.google.com/webstore/detail/helix-sidekick-beta/ccfggkjabjahcjoljmgmklhpaccedipo).

   ![Installare AEM Sidekick](/help/edge/assets/install-aem-sidekick.png)

   Dopo aver installato l’estensione su Chrome, non dimenticare di fissarla, per facilitarne la ricerca.

   ![Fissare AEM Sidekick](/help/edge/assets/pin-aem-sidekick.png)

1. Per impostare l’estensione Sidekick per Chrome, passa alla cartella di Google Drive o Microsoft SharePoint precedentemente condivisa e fai clic con il pulsante destro del mouse sull’icona dell’estensione nella barra degli strumenti del browser, quindi seleziona `Add this project`.

   ![AEM Sidekick: aggiungere un progetto](/help/edge/assets/aem-sidekick-add-a-project.png)

   Una volta installata l’estensione e aggiunto il progetto, puoi visualizzare in anteprima e pubblicare il contenuto da Google Drive.

1. Seleziona tutti i documenti nella cartella Microsoft SharePoint o Google Drive. È possibile scegliere più documenti tenendo premuto il tasto Ctrl (Windows/Linux) o Comando (Mac) mentre fai clic.

   ![Selezionare tutti i file](/help/edge/assets/select-all-files.png)

1. Fai clic sull’icona AEM Sidekick fissata nella barra delle estensioni di Chrome. Viene visualizzata una barra degli strumenti sulla schermata. Puoi scegliere di visualizzare in anteprima o pubblicare il contenuto.

   Se hai copiato i file `index`, `nav`, `footer` e `enquiry`, questi sono tutti documenti separati con i rispettivi cicli di anteprima e pubblicazione, quindi assicurati di visualizzare in anteprima (e pubblicare) ognuno di questi.

   Quando si visualizzano i file in anteprima, i documenti vengono visualizzati in nuove schede del browser. Per visualizzare in anteprima il modulo di esempio, passa al seguente URL:


   ```HTML
   https://<branch>--<repository>--<owner>.aem.live
   ```

   - `<branch>` fa riferimento al ramo dell’archivio GitHub.
   - `<repository>` denota l’archivio GitHub.
   - `<owner>` fa riferimento al nome utente dell’account GitHub che ospita l’archivio GitHub.


   URL `https://<branch>--<repo>--<owner>.aem.page/enquiry`

   Ad esempio, se l’archivio del progetto è denominato “wefinance”, si trova sotto il proprietario dell’account “wkndform” e stai utilizzando il ramo “main” e il nome del modulo come `enquiry`, l’URL è:`https://main--wefinance--wkndform.aem.live/enquiry`.
&lt;!—(https://main--wefinance--wkndform.aem.live/enquiry).-->

### Creare un modulo

Il contenuto di esempio include un foglio “enquiry” che funge da modello per il modulo “enquiry”. Ogni riga del foglio rappresenta un [campo modulo](/help/edge/docs/forms/form-components.md#available-components) e le intestazioni della colonna definiscono le [proprietà del campo](/help/edge/docs/forms/form-components.md#available-components). Questo modulo di esempio offre un punto di partenza per iniziare a creare il modulo.

![Modulo di richiesta](/help/edge/docs/forms/assets/enquiry-form-microsoft-sharepoint.png)

>[!IMPORTANT]
>
>**Il foglio in cui è stato creato il modulo presenta restrizioni relative al nome. Solo `helix-default` e `shared-aem` possono essere utilizzati come nomi per il foglio.**

Iniziamo con l’aggiornamento dell’etichetta di un campo. Apri il foglio “enquiry” per la modifica, cambia l’etichetta del pulsante Invia in `Let's Talk` e utilizza AEM Sidekick per visualizzare in anteprima e pubblicare il file.

![Modulo di richiesta](/help/edge/assets/enquiry-form-preview-publish.png)

Quando visualizzi in anteprima o pubblichi il file, una versione JSON del file viene visualizzata in una nuova scheda. Copia l’URL di anteprima (.aem.page) o di pubblicazione (.aem.live) del file.

![JSON del foglio di calcolo del modulo](/help/edge/assets/preview-and-publish-enquiry-form.png)

Apri il file `enquiry` e sostituisci l’URL nel blocco del modulo con l’URL del file copiato nel passaggio precedente. Assicurati che l’URL sia un collegamento ipertestuale.

![File di richiesta con l’URL .json dell’URL del foglio di calcolo](/help/edge/assets/enquiry-doc-to-embed-form.png)

Utilizza AEM Sidekick per visualizzare in anteprima e pubblicare il documento di richiesta.

![File di richiesta con l’URL .json dell’URL del foglio di calcolo](/help/edge/assets/preview-and-publish-enquiry-document.png)


Per visualizzare in anteprima il modulo di richiesta aggiornato, passa al seguente URL:


```HTML
    https://<branch>--<repository>--<owner>.aem.page/enquiry
       
```

L’etichetta del pulsante Invia viene aggiornata in `Let's Talk`.

![Modulo di richiesta](/help/edge/assets/updated-form.png)

&lt;!—(https://main--wefinance--wkndform.aem.live/enquiry)-->

URL: `https://main--wefinance--wkndform.aem.live/enquiry`
&lt;!—(https://main--wefinance--wkndform.aem.live/enquiry)-->


Per informazioni dettagliate sulla creazione e la pubblicazione di un nuovo modulo, consulta la guida [creare un modulo](/help/edge/docs/forms/create-forms.md).

### Inizia a sviluppare stile e funzionalità


Per essere operativi con un ambiente di sviluppo AEM locale in tempi brevi:

1. installa AEM CLI: AEM CLI semplifica le attività di sviluppo. Installalo a livello globale utilizzando npm:

   ```Bash
       npm install -g @adobe/aem-cli
   ```

1. Clona il progetto GitHub: clona l’archivio del progetto da GitHub utilizzando il seguente comando, sostituendo `<owner>` con il proprietario dell’archivio e `<repo>` con il nome dell’archivio:

   ```
   git clone https://github.com/<owner>/<repo>
   ```

1. Avvia l’ambiente locale: passa alla directory del progetto e attiva l’istanza AEM locale con un singolo comando:

   ```
   cd <repo>
   aem up
   ```

La cartella `blocks/form` del blocco di moduli adattivi è un ambiente playground per lo stile e il codice dei moduli. Modifica qualsiasi file `.css` o `.js` all’interno di questa directory e vedrai le modifiche immediatamente applicate nel browser.

Vuoi mostrare la creazione? Utilizza Git per confermare e implementare le modifiche. Questo aggiorna gli ambienti di anteprima e di produzione accessibili tramite questi URL (sostituisci i segnaposto con i dettagli del progetto):

Anteprima:`https://<branch>--<repo>--<owner>.aem.page/`
Produzione: `https://<branch>--<repo>--<owner>.aem.live/`

Congratulazioni L’ambiente di sviluppo locale è stato configurato correttamente e le modifiche sono state implementate.

## Aggiungere un blocco di moduli adattivi al progetto AEM esistente

<!--
>[!VIDEO](https://video.tv.adobe.com/v/3427789)-->

Se disponi di un progetto AEM esistente, puoi integrare il blocco di moduli adattivi nel progetto corrente per iniziare a creare il modulo.

>[!NOTE]
>
>
> Questo passaggio si applica ai progetti generati con il [XWalk standard AEM](https://github.com/adobe/aem-boilerplate). Se hai creato il progetto AEM utilizzando [moduli AEM standard](https://github.com/adobe-rnd/aem-boilerplate-forms), puoi saltare questo passaggio.

Per integrare:

1. Passa alla cartella dell’archivio di progetto AEM nel sistema locale.

1. Copia e incolla le cartelle e i file seguenti dal [ modello AEM standard](https://github.com/adobe-rnd/aem-boilerplate-forms) nel tuo progetto AEM:

   - Cartella [blocco modulo](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/blocks/form)
   - File [form-editor-support.js](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.js)
   - File [form-editor-support.css](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.css)
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

Tutto qui. Il blocco di moduli adattivi fa ora parte del progetto AEM. Puoi iniziare a creare e aggiungere moduli alle pagine AEM.

## Risoluzione dei problemi di compilazione di GitHub

Assicurati un processo di compilazione di GitHub senza intoppi affrontando potenziali problemi:

- **Errore del percorso del modulo di risoluzione**
Se riscontri l’errore “Impossibile risolvere il percorso del modulo ”‘/scripts/lib-franklin.js’, passa al file [Progetto EDS]/blocks/forms/form.js. Aggiorna l’istruzione di importazione sostituendo il file lib-franklin.js con il file aem.js.

- **Gestire errori di stampa:**
in caso di errori di stampa, è possibile ignorarli. Apri il file [Progetto EDS]/package.json e modifica lo script “lint” da `"lint": "npm run lint:js && npm run lint:css"` a `"lint": "echo 'skipping linting for now'"`. Salva il file e conferma le modifiche nel progetto GitHub.

