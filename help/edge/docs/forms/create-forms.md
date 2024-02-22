---
title: Guida introduttiva del servizio di consegna Edge di AEM Forms
description: Forme perfette, veloce! ⚡ authoring basato su documento di AEM Forms Edge Delivery = velocità sorprendente e moduli compatibili con SEO per utenti e motori di ricerca più felici.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: bd8c4fbfd7f740baa6abd7a91fb8d1dcdaff6c28
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---


# Creare un modulo su AEM Forms Edge Delivery Service

Nell’era digitale di oggi, la creazione di moduli facili da usare è essenziale per qualsiasi organizzazione. AEM Forms Edge Delivery consente di creare moduli utilizzando strumenti familiari come Word o Google Docs.

Questi moduli inviano i dati direttamente a un file Microsoft Excel o Google Sheets, consentendo di utilizzare un ecosistema dinamico e API affidabili di Google Sheets, Microsoft Excel e Microsoft Sharepoint per elaborare facilmente i dati inviati o avviare un flusso di lavoro aziendale esistente.


## Prerequisiti

Prima di iniziare, assicurati di aver completato i seguenti passaggi:

* Imposta e clona il progetto Edge Delivery Service (EDS). Consulta [tutorial per sviluppatori](https://www.aem.live/developer/tutorial) per i dettagli. La cartella locale del progetto Edge Delivery Service (EDS) viene indicata come `[EDS Project repository]` in questo documento.
* Clona il [Archivio Forms Block](https://github.com/adobe/afb). Contiene il codice per eseguire il rendering del modulo su una pagina Web EDS. La cartella locale dell’archivio Forms Block viene indicata come `[Forms Block repository]` in questo documento.
* Assicurati di avere accesso a Google Sheets o Microsoft SharePoint.


## Creare un modulo

+++ Passaggio 1: aggiungi il blocco Form al progetto Edge Delivery Service (EDS).

AEM Forms Edge Delivery include un blocco Modulo per facilitare la creazione di moduli per l’acquisizione e l’archiviazione dei dati acquisiti. Per includere il blocco del modulo nel progetto del servizio di consegna Edge:

1. Accedi a `[Forms Block repository]/blocks` e copia `forms` cartella.

1. Accedi a `[EDS Project repository]/blocks/` e incolla `forms` cartella.

   >[!VIDEO](https://video.tv.adobe.com/v/3427487?quality=12&learn=on)

1. Archivia `form` cartella e i file sottostanti al progetto del servizio di consegna Edge su GitHub.

   Il blocco Form viene aggiunto all’archivio dei progetti EDS su Github. Assicurati che la build Github non abbia esito negativo:

   * Se riscontri un errore di tipo &quot;Impossibile risolvere il percorso del modulo &quot;&#39;../../scripts/lib-franklin.js&#39;&quot;, apri la `[EDS Project]/blocks/forms/form.js` file. Nell&#39;istruzione import sostituire `lib-franklin.js` file con `aem.js` file.

   * In caso di errori di colorazione, è possibile ignorarli. Per ignorare i controlli di linting, aprire `[EDS Project]\package.json` e aggiorna lo script &quot;lint&quot; da `"lint": "npm run lint:js && npm run lint:css"` a `"lint": "echo 'skipping linting for now'"`. Salva il file e esegui il commit nel progetto GitHub.

È ora possibile creare un modulo e aggiungerlo al sito.

+++

+++ Passaggio 2: creare un modulo utilizzando Microsoft Excel o Foglio Google.

Anziché processi complessi, è possibile creare facilmente un modulo utilizzando un foglio di calcolo. È possibile iniziare aggiungendo le righe e le intestazioni di colonna a un foglio di calcolo, in cui ogni riga definisce un campo modulo e ogni intestazione di colonna definisce le proprietà dei campi modulo corrispondenti.

Ad esempio, nel foglio di calcolo seguente, le righe definiscono i campi per un `contact us` l&#39;intestazione di modulo e colonna definisce le proprietà dei campi corrispondenti.

![contattaci foglio di calcolo](/help/edge/assets/contact-us-form-spreadsheet.png)

Per creare un modulo:

1. Apri la cartella del progetto AEM Edge Delivery su Microsoft SharePoint o Google Drive.

1. Crea una cartella di lavoro di Microsoft Excel o un foglio di Google ovunque sotto la directory di progetto AEM Edge Delivery. Ad esempio, crea un foglio di calcolo denominato `contact-us` nella directory del progetto AEM Edge Delivery su Google Drive.

1. Assicurati che il foglio sia condiviso con l’utente AEM (ad esempio `helix@adobe.com`) [configurato per il progetto](https://www.aem.live/docs/setup-customer-sharepoint) e l’utente dispone delle autorizzazioni di modifica per il foglio.

1. Aprire il foglio di calcolo creato e impostare il nome del foglio predefinito su &quot;shared-default&quot;.

   ![rinominare il foglio predefinito in &quot;shared-default&quot;](/help/edge/assets/rename-sheet-to-shared-default.png)

1. Per aggiungere i campi del modulo, aggiungi le righe e le intestazioni di colonna al `shared-default` , in cui ogni riga definisce un campo modulo e ogni intestazione di colonna definisce [proprietà](/help/edge/docs/forms/eds-form-field-properties)) dei campi modulo corrispondenti.

   Per iniziare rapidamente, puoi copiare il contenuto della [contattaci foglio di calcolo](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link) nel foglio di calcolo.

   >[!VIDEO](https://video.tv.adobe.com/v/3427468?quality=12&learn=on)

1. Utilizzare [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) per visualizzare in anteprima e pubblicare il foglio.

   ![Utilizza AEM Sidekick per visualizzare in anteprima e pubblicare il foglio](/help/edge/assets/preview-form.png)

   In anteprima e pubblicazione, il browser apre nuove schede che visualizzano il contenuto del foglio in formato JSON. Assicurati di prendere nota dell’URL live, in quanto è necessario per il rendering del modulo in un secondo momento.

   Il formato dell’URL è:

   ```JSON
   https://<branch>--<repository>--<owner>.hlx.live/<form>.json
   
   For example, https://main--portal--wkndforms.hlx.live/contact-us.json
   ```

+++

+++ Passaggio 3: visualizza l’anteprima del modulo utilizzando la pagina del servizio di consegna Edge (EDS).


A questo punto è stato aggiunto il blocco modulo al progetto EDS e ne è stata preparata la struttura. Ora, per visualizzare l’anteprima del modulo:

1. Vai all’account Microsoft SharePoint o Google Drive e apri la directory del progetto AEM Edge Delivery.

1. Aprire un file documento per incorporarvi il modulo. Ad esempio, apri il file di indice. È inoltre possibile creare un nuovo file di documento.

1. Passare alla posizione desiderata all&#39;interno del documento in cui si desidera aggiungere il modulo.

1. Aggiungi al file un blocco denominato &quot;Modulo&quot;, simile a quello visualizzato di seguito.

   ![](/help/edge/assets/form-block-in-sites-page-example.png)

   Nella seconda riga, includi come collegamento ipertestuale l’URL registrato nella sezione precedente. Utilizza l’URL di anteprima (.page URL) a scopo di sviluppo o test oppure l’URL di pubblicazione (.live) per la produzione.

   >[!IMPORTANT]
   >
   >
   > Assicurati che l’URL sia collegato tramite collegamento ipertestuale anziché presentato come testo normale.


1. Utilizzare [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) per visualizzare l&#39;anteprima della pagina. Nella pagina viene ora visualizzato il modulo.

   Ad esempio, questo è il modulo basato su [contattaci foglio di calcolo](https://docs.google.com/spreadsheets/d/12jvYjo1a3GOV30IqPY6_7YaCQtUmzWpFhoiOHDcjB28/edit?usp=drive_link):


   ![Un esempio di modulo EDS](/help/edge/assets/eds-form.png)

   A questo punto, compilare il modulo e fare clic sul pulsante Invia, si verifica un errore simile al seguente, perché il foglio di calcolo non è ancora impostato per accettare i dati.

   ![errore durante l’invio del modulo](/help/edge/assets/form-error.png)

+++


## Passaggio successivo

[Preparare il foglio di calcolo](/help/edge/docs/forms/submit-forms.md) per iniziare ad accettare i dati all’invio del modulo.



## Vedi altro

* [Proprietà del campo modulo](/help/edge/docs/forms/eds-form-field-properties)
* [Creare e visualizzare in anteprima un modulo](/help/edge/docs/forms/create-forms.md)
* [Abilita modulo per l’invio di dati](/help/edge/docs/forms/submit-forms.md)
* [Pubblicare un modulo nella pagina Sites](/help/edge/docs/forms/publish-eds-forms.md)
* [Aggiungere convalide ai campi modulo](/help/edge/docs/forms/validate-forms.md)
* [Modificare i temi e lo stile del modulo](/help/edge/docs/forms/style-theme-forms.md)
