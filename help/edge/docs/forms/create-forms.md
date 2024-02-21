---
title: Guida introduttiva del servizio di consegna Edge di AEM Forms
description: Forme perfette, veloce! ⚡ authoring basato su documento di AEM Forms Edge Delivery = velocità sorprendente e moduli compatibili con SEO per utenti e motori di ricerca più felici.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: f37a99cd5cbfb745cb591e3be2a46a5f52139cb2
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---


# Creare un modulo su AEM Forms Edge Delivery Service

Nell’era digitale di oggi, la creazione di moduli facili da usare è essenziale per qualsiasi organizzazione. AEM Forms Edge Delivery consente di creare moduli utilizzando strumenti familiari come Word o Google Docs.

Questi moduli inviano i dati direttamente a un file Microsoft Excel o Google Sheets, consentendo di utilizzare un ecosistema dinamico e API affidabili di Google Sheets, Microsoft Excel e Microsoft Sharepoint per elaborare facilmente i dati inviati o avviare un flusso di lavoro aziendale esistente.

## Prerequisiti

* Hai un account Github.
* Accesso a Google Sheets o Microsoft SharePoint.
* Scopri le nozioni di base di Git, HTML, CSS e JavaScript.
* Nodo e NPM installati per lo sviluppo locale.

## Prima di iniziare

* Imposta e clona il progetto Edge Delivery Service (EDS). Consulta [tutorial per sviluppatori](https://www.aem.live/developer/tutorial) per i dettagli.
* Clona il [Archivio Forms Block](https://github.com/adobe/afb). Include il blocco Form necessario per il rendering del modulo.

![Guida introduttiva di Edge Delivery Forms](/help/edge/assets/getting-started-with-eds-forms.png)

## Aggiungere il blocco Form al progetto EDS (Edge Delivery Service) {#add-forms-block-to-an-eds-project}

AEM Forms Edge Delivery include un blocco Modulo per facilitare la creazione di moduli per l’acquisizione e l’archiviazione dei dati acquisiti. Per includere il blocco del modulo nel progetto del servizio di consegna Edge:

1. Vai alla cartella del progetto Edge Delivery Service (EDS) nell’ambiente di sviluppo locale.


   ```Shell
   cd [EDS Project folder]
   ```

1. Crea una cartella denominata `form` nella directory del progetto EDS. Ad esempio, nella directory del progetto EDS denominato `Portal`, crea una cartella denominata `form`.

   ```Shell
   mkdir form
   ```


1. Aggiungi il [Blocco Forms](https://github.com/adobe/afb/tree/main/blocks/form) nella cartella &#39;form&#39;.

   ```shell
   cp -R <source:path of the form block> <destination: path of the form folder created in the previous step>
   
   For example
   
   cp -R Documents/afb/blocks/form Documents/portal/blocks/
   ```

1. Archivia la cartella &quot;form&quot; e i file sottostanti nel progetto del servizio di consegna Edge su GitHub.

   ```Shell
   git add .
   git commit -m "Added form block"
   git push origin
   ```

   È ora possibile eseguire il rendering di un modulo EDS.

   >[!NOTE]
   >
   > * Se la richiesta di pull o la build del progetto eds non riesce e si verifica un errore relativo all’importazione di `franklin-lib.js` , aggiorna l&#39;istruzione import in modo che faccia riferimento al file `aem.js` anziché il file `franklin-lib.js` file.
   > * In caso di errori di colorazione, è possibile ignorarli. Per ignorare i controlli di puntamento, passa al file package.json e aggiorna lo script &quot;lint&quot; da `"lint": "npm run lint:js && npm run lint:css"` a `"lint": "echo 'skipping linting for now'"`. Quindi, esegui il commit delle modifiche nel file package.json.

## Creare un modulo utilizzando Microsoft Excel o Google Sheet {#create-a-form-for-an-eds-project}

Può essere utile consentire agli sviluppatori di siti web di creare moduli e scegliere quali informazioni raccogliere dai visitatori del sito web. Invece di processi complessi, gli autori possono facilmente impostare un modulo utilizzando un foglio di calcolo. Devono aggiungere le intestazioni di colonna corrette e quindi utilizzare un blocco di modulo per visualizzarlo sul sito web senza problemi. Per creare un modulo:

1. Crea una cartella di lavoro di Microsoft Excel o un foglio di Google ovunque sotto la directory di progetto AEM Edge Delivery su Microsoft SharePoint o Google Drive.

1. Assicurati che l’utente AEM (ad esempio `helix@adobe.com`) configurato per il progetto dispone delle autorizzazioni di modifica per il foglio.

1. Aprire la cartella di lavoro creata e impostare il nome del foglio predefinito su &quot;shared-default&quot;.

   ![rinominare il foglio predefinito in &quot;shared-default&quot;](/help/edge/assets/rename-sheet-to-helix-default.png)

1. Copia il contenuto del [contattaci foglio di calcolo](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link) nel tuo foglio di calcolo.

   ![contattaci foglio di calcolo](/help/edge/assets/contact-us-form-spreadsheet.png)

1. Utilizzare [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) per visualizzare in anteprima e pubblicare il foglio.

   In anteprima e pubblicazione, il browser apre nuove schede che visualizzano il contenuto del foglio in formato JSON. Assicurati di prendere nota dell’URL live, in quanto è necessario per il rendering del modulo in un secondo momento.

   Il formato dell’URL è:

   ```shell
   https://<branch>--<repository>--<owner>.hlx.live/<form>.json
   
   For example, https://main--portal--wkndforms.hlx.live/contact-us.json
   ```

## Visualizzare l’anteprima del modulo utilizzando la pagina del servizio di consegna Edge (EDS) {#add-a-form-to-your-eds-page}

Finora è stato attivato il blocco del modulo per il progetto EDS e preparata la struttura del modulo. A questo punto, per includere il modulo nella pagina EDS ed eseguirne il rendering:

1. Vai alla directory del progetto di consegna Edge dell’AEM su Microsoft SharePoint o Google Drive.

1. Per aggiungere il modulo a una pagina, apri il corrispondente file doc. Ad esempio, apri il file di indice.

1. Passare alla posizione desiderata all&#39;interno del documento in cui si desidera aggiungere il modulo.

1. Aggiungi al file un blocco denominato &quot;Modulo&quot;, simile a quello visualizzato di seguito.

   ![](/help/edge/assets/form-block-in-sites-page-example.png)

   Nella seconda riga, includi come collegamento ipertestuale l’URL annotato nella sezione precedente.

1. Utilizzare [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) per visualizzare in anteprima e pubblicare la pagina. Viene eseguito il rendering del modulo.

   Ad esempio, questo è il modulo basato su [contattaci foglio di calcolo](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link):


   ![contattaci (modulo EDS)](/help/edge/assets/eds-form.png)

   Il blocco modulo esegue il rendering del modulo ma non è ancora pronto per accettare i dati. Facendo clic sul pulsante Invia si verifica un errore simile al seguente:

   ![errore durante l’invio del modulo](/help/edge/assets/form-error.png)

   [Preparare il foglio per accettare i dati](/help/edge/docs/forms/submit-forms.md). È possibile inviare i dati al foglio post preparandolo ad accettare i dati.


## Vedi altro

* [Creare e visualizzare in anteprima un modulo](/help/edge/docs/forms/create-forms.md)
* [Abilita modulo per l’invio di dati](/help/edge/docs/forms/submit-forms.md)
* [Pubblicare un modulo nella pagina Sites](/help/edge/docs/forms/publish-eds-forms.md)
* [Aggiungere convalide ai campi modulo](/help/edge/docs/forms/validate-forms.md)
* [Modificare i temi e lo stile del modulo](/help/edge/docs/forms/style-theme-forms.md)