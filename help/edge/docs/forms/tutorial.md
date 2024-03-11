---
title: 'Guida introduttiva ai Edge Delivery Services AEM Forms: tutorial per sviluppatori '
description: Questa esercitazione ti aiuta a iniziare con un nuovo progetto Adobe Experience Manager Forms (AEM). Tra dieci o venti minuti sarà possibile creare moduli personalizzati.s
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: d91254b52c257a3758da200a2c74b736ca457884
workflow-type: tm+mt
source-wordcount: '1878'
ht-degree: 0%

---


# Guida introduttiva: tutorial per sviluppatori

Nell’era digitale di oggi, la creazione di moduli facili da usare è essenziale per qualsiasi organizzazione. AEM Forms Edge Delivery Services (EDS) consente di creare moduli utilizzando strumenti familiari come Google Docs e Microsoft Office.

Questi moduli inviano i dati direttamente a un file Microsoft Excel o Google Sheets, consentendo di utilizzare un ecosistema dinamico e API affidabili di Google Sheets, Microsoft Excel e Microsoft Sharepoint per elaborare facilmente i dati inviati o avviare un flusso di lavoro aziendale esistente.

AEM Forms fornisce un blocco, noto come blocco di Forms adattivo, per facilitare la creazione di moduli per l’acquisizione e l’archiviazione dei dati acquisiti. Puoi creare un nuovo progetto AEM preconfigurato con Adaptive Forms Block oppure aggiungere Adaptive Forms Block a un progetto AEM esistente.

Questa esercitazione di AEM Forms ti guida attraverso la creazione, l’anteprima e la pubblicazione di un modulo personalizzato con un nuovo progetto Adobe Experience Manager (AEM) Forms. Scoprirai anche come aggiungere il blocco Forms adattivo a un progetto AEM esistente.

* **[Crea un nuovo progetto AEM preconfigurato con Adaptive Forms Block](#create-a-new-eds-project-pre-configured-with-adaptive-forms-block)**
* **[Aggiungere un blocco Forms adattivo a un progetto AEM esistente](#add-adaptive-forms-block-to-an-existing-eds-project)**



## Prerequisiti

* Hai un account GitHub e conosci le nozioni di base su Git.
* Hai un account Google o Microsoft SharePoint.
* Scopri le nozioni di base di HTML, CSS e JavaScript.
* Node/npm è installato per lo sviluppo locale.

**Alzate la testa!** Questa esercitazione utilizza macOS, Chrome e Visual Studio Code. Anche se i passaggi possono essere adattati per altre impostazioni, le schermate e gli elementi specifici dell’interfaccia utente potrebbero variare in base al sistema operativo, al browser e all’editor di codice scelti.


## Crea un nuovo progetto AEM preconfigurato con Adaptive Forms Block

Il modello AEM Forms Boilerplate consente di iniziare rapidamente con un progetto AEM preconfigurato con il blocco Forms adattivo. È il modo più rapido e semplice per seguire le best practice dell’AEM e passare direttamente alla creazione dei moduli.

### Introduzione al modello di archivio standard AEM Forms

1. Crea un archivio GitHub per il progetto AEM. Per creare l’archivio:
   1. Vai a [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms).

      ![AEM Forms Boilerplate](/help/edge/assets/aem-forms-boilerplate.png)
   1. Fai clic su **Usa questo modello** e selezionare il **Creare un nuovo archivio** opzione. Viene visualizzata la schermata Crea nuovo archivio.

      ![Creare un nuovo archivio con AEM Forms Boilerplate](/help/edge/assets/create-new-repository-using-aem-forms-boilerplate.png)

   1. Nella schermata Crea nuovo repository, selezionare **proprietario**, e specificare **Nome archivio** . L’Adobe consiglia di impostare l’archivio su **Pubblico**. Quindi, seleziona la **pubblico** e fai clic su **Crea archivio**.

   ![Impostare l’archivio su public](/help/edge/assets/create-a-new-repo-keep-it-public.png)


1. Installa l’app GitHub AEM Code Sync nell’archivio. Per installare:
   1. Vai a [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new).
   1. Nella schermata Install AEM Code Sync (Installa sincronizzazione codice), selezionare **Seleziona solo archivi** e selezionare il repository appena creato. Fai clic su Salva.

   ![Impostare l’archivio su public](/help/edge/assets/install-aem-code-sync-app-for-your-repo.png)

   >[!NOTE]
   >
   >
   > Se utilizzi GitHub Enterprise con filtro IP, puoi aggiungere il seguente IP al inserisco nell&#39;elenco Consentiti di: 3.227.118.73

   Congratulazioni. Hai un nuovo sito web in esecuzione su `https://<branch>--<repo>--<owner>.hlx.page/`.

   * `<branch>` fa riferimento al ramo dell’archivio GitHub.
   * `<repository>` denota l’archivio GitHub.
   * `<owner>` fa riferimento al nome utente dell’account GitHub che ospita l’archivio GitHub.

   Ad esempio, se il nome del ramo è `main`, archivio è `wefinance`, e il proprietario è `wkndforms`, il sito web sarà operativo alle [https://main--wefinance--wkndforms.hlx.page/](https://main--wefinance--wkndforms.hlx.page/).



### Collega la tua origine di contenuto

L’archivio GitHub appena creato punta a [contenuto di esempio archiviato in una cartella di Google Drive](https://drive.google.com/drive/folders/17LSiMZC77N8tCJRW45TnHHGcG8V3SLG_). Questo contenuto di sola lettura rappresenta un ottimo punto di partenza per i moduli. Puoi copiarlo nella tua unità Google e personalizzarlo in base alle tue esigenze.

![Contenuto di esempio su Google Drive](/help/edge/assets/folder-with-sample-content.png)

Per copiare il contenuto di esempio nella tua cartella di contenuto e indirizzare l’archivio GitHub alla tua cartella di contenuto:

1. Crea una nuova cartella specifica per il contenuto AEM in Google Drive o Microsoft SharePoint. Questo documento utilizza una cartella creata in Microsoft SharePoint.

1. Condividi la cartella con l’utente di Adobe Experience Manager (helix@adobe.com).

   ![Utilizza l’opzione Gestisci accesso per condividere la cartella con l’utente AEM - SharePoint](/help/edge/assets/share-folder-with-aem-user.png)

   ![Utilizza l’opzione Gestisci accesso per condividere la cartella con l’utente AEM - Google Drive](/help/edge/assets/share-google-drive-folder.png)


   Assicurati di aver fornito all’utente di Adobe Experience Manager i diritti di modifica per la cartella.

   ![Condividi la cartella con l&#39;utente AEM e fornisci i diritti di modifica-SharePoint](/help/edge/assets/share-folder-with-aem-user-provide-editing-access.png)

   ![Condividi la cartella con l&#39;utente AEM e fornisci i diritti di modifica - Google Drive](/help/edge/assets/add-aem-user-google-folder.png)

1. Copia il [contenuto di esempio archiviato nella cartella Google Drive](https://drive.google.com/drive/folders/17LSiMZC77N8tCJRW45TnHHGcG8V3SLG_) nella cartella. Per copiare:

   1. Scaricare i file insieme o i singoli file.

      ![Scarica contenuto di esempio](/help/edge/assets/download-sample-content.png)

      Il `nav` e `footer` i file definiscono il layout di base delle pagine e si modificano raramente durante un progetto. Inoltre, dispongono di una struttura specifica diversa dalla maggior parte degli altri file di contenuto. Esaminando questi file si può capire come il contenuto viene organizzato nei progetti AEM.


   1. Caricare questi file nella cartella Microsoft SharePoint o Google Drive.

      ![Contenuto di esempio su Google Drive](/help/edge/assets/upload-sample-files-to-your-content-folder.png)

      Assicurati di copiare  `enquiry` dal contenuto di esempio alla cartella in Google Drive o Microsoft SharePoint. Contiene la struttura per un modulo di esempio.

1. Ora che hai configurato la cartella dei contenuti, puoi collegarla al progetto su GitHub che hai creato utilizzando AEM Forms Boilerplate in precedenza. Per connettersi:

   1. Vai all’archivio GitHub creato in precedenza utilizzando AEM Forms Boilerplate.
   1. Apri `fstab.yaml` per la modifica.
   1. Sostituisci il riferimento esistente con il percorso della cartella condivisa con l’utente AEM (helix@adobe.com).

      ![Contenuto di esempio su Google Drive](/help/edge/assets/replace-path-in-fstab-yaml-with-your-content-folder.png)


      Se si utilizza Microsoft SharePoint, il percorso della cartella utilizza il formato seguente:

      ```HTML
      https://<tenant>.sharepoint.com/sites/  <sp-site>/Shared%20Documents/<folder-name>
      ```

      Ad esempio:

      ```HTML
      https://adobe.sharepoint.com/sites/wkndforms/Shared%20Documents/wefinance
      ```

      Per ulteriori informazioni sulla gestione dei file con Microsoft SharePoint, consulta [Come utilizzare Adobe Sharepoint](https://www.aem.live/docs/setup-customer-sharepoint).



   1. Conferma l&#39;aggiornamento `fsatb.yaml` dopo aver aggiornato il riferimento e tutto sembra a posto. Se riscontri problemi di build, consulta [Risoluzione dei problemi di build di GitHub](#troubleshooting-github-build-issues).



      ![Conferma file fsatab.yaml aggiornato](/help/edge/assets/commit-updated-fstab-yaml.png)

      Consente di collegare la cartella dei contenuti al sito Web. Dopo aver aggiornato il riferimento, potresti riscontrare inizialmente errori &quot;404 Not Found&quot; (404 non trovato). Il contenuto non è ancora stato visualizzato in anteprima. Nella sezione successiva viene illustrato come iniziare a creare e visualizzare in anteprima i contenuti.



### Anteprima e pubblicazione dei contenuti

Dopo aver completato l’ultimo passaggio, la nuova origine di contenuto non è vuota, ma non sarà visibile sul sito web finché non viene promossa nell’anteprima o nelle fasi live. Attualmente, ciò potrebbe causare errori 404.

Per visualizzare in anteprima il contenuto non pubblicato:

1. Installare l’estensione Chrome denominata [AEM Sidekick](https://chrome.google.com/webstore/detail/helix-sidekick-beta/ccfggkjabjahcjoljmgmklhpaccedipo).

   ![Installa AEM Sidekick](/help/edge/assets/install-aem-sidekick.png)

   Dopo aver installato l’estensione su Chrome, non dimenticare di fissarla, per facilitarne la ricerca.

   ![Fissa AEM Sidekick](/help/edge/assets/pin-aem-sidekick.png)

1. Per impostare l’estensione Sidekick per Chrome, passa alla cartella precedentemente condivisa di Google Drive o Microsoft SharePoint e fai clic con il pulsante destro del mouse sull’icona dell’estensione nella barra degli strumenti del browser, quindi seleziona `Add this project`.

   ![AEM Sidekick: aggiungi un progetto](/help/edge/assets/aem-sidekick-add-a-project.png)

   Una volta installata l’estensione e aggiunto il progetto, puoi visualizzare in anteprima e pubblicare i contenuti dall’unità Google.

1. Selezionare tutti i documenti nella cartella Microsoft SharePoint o Google Drive. È possibile scegliere più documenti tenendo premuto il tasto Ctrl (Windows/Linux) o Cmd (Mac) mentre si fa clic su.

   ![Seleziona tutti i file](/help/edge/assets/select-all-files.png)

1. Fai clic sull’icona AEM Sidekick fissata alla barra delle estensioni Chrome. Viene visualizzata una barra degli strumenti. Puoi scegliere di visualizzare in anteprima o pubblicare il contenuto.

   Se hai copiato `index`, `nav`, `footer` e `enquiry` file, si tratta di documenti separati con i rispettivi cicli di anteprima e pubblicazione, quindi assicurati di visualizzarli in anteprima (e pubblicarli).

   Quando si visualizzano i file in anteprima, i documenti vengono visualizzati in nuove schede del browser. Per visualizzare in anteprima il modulo di esempio, vai al seguente URL:


   ```HTML
   https://<branch>--<repository>--<owner>.hlx.live
   ```

   * `<branch>` fa riferimento al ramo dell’archivio GitHub.
   * `<repository>` denota l’archivio GitHub.
   * `<owner>` fa riferimento al nome utente dell’account GitHub che ospita l’archivio GitHub.


   `https://<branch>--<repo>--<owner>.hlx.page/enquiry` URL.

   Ad esempio, se l’archivio del progetto è denominato &quot;wefinance&quot;, si trova sotto il proprietario dell’account &quot;wkndforms&quot; e stai utilizzando il ramo &quot;main&quot;, l’URL è:



   [https://main--wefinance--wkndforms.hlx.page](https://main--wefinance--wkndforms.hlx.page).

### Creare un modulo

Il contenuto di esempio include un foglio di &quot;richiesta&quot; che funge da modello per il modulo di &quot;richiesta&quot;. Ogni riga del foglio rappresenta un [campo modulo](/help/edge/docs/forms/form-components.md#available-components)e le intestazioni di colonna definiscono [proprietà campo](/help/edge/docs/forms/form-components.md#available-components). In questo modulo di esempio è possibile iniziare subito a creare il modulo.

![Modulo di interrogazione](/help/edge/assets/enquiry-form-microsoft-sharepoint.png)

Iniziamo con l’aggiornamento dell’etichetta di un campo. Apri il foglio &quot;Richiesta&quot; per la modifica, modifica l’etichetta del pulsante Invia in `Let's Chat` e utilizza AEM Sidekick per visualizzare in anteprima e pubblicare il file.

![Modulo di interrogazione](/help/edge/assets/enquiry-form-preview-publish.png)

Quando visualizzi l’anteprima o pubblichi il file, in una nuova scheda viene visualizzata una versione JSON del file. Copia l’URL di anteprima (.hlx.page) o di pubblicazione (.hlx.live) del file.

![JSON del foglio di calcolo del modulo](/help/edge/assets//preview-and-publish-enquiry-form.png)

Apri `enquiry` e sostituisci l’URL nel blocco di modulo con l’URL del file copiato nel passaggio precedente. Assicurati che l’URL sia un collegamento ipertestuale.

![File di interrogazione con URL .json dell’URL del foglio di calcolo](/help/edge/assets/enquiry-doc-to-embed-form.png)

Utilizza AEM Sidekick per visualizzare in anteprima e pubblicare il documento di richiesta.

![File di interrogazione con URL .json dell’URL del foglio di calcolo](/help/edge/assets/preview-and-publish-enquiry-document.png)


Per visualizzare in anteprima il modulo di richiesta aggiornato, vai al seguente URL:


```HTML
    https://<branch>--<repository>--<owner>.hlx.page/enquiry
       
```

L’etichetta del pulsante Invia viene aggiornata in `Let's Chat`.

![Modulo di interrogazione](/help/edge/assets/updated-form.png)

Per informazioni dettagliate sulla creazione e la pubblicazione di un nuovo modulo, passare alla sezione [creare un modulo](/help/edge/docs/forms/create-forms.md) guida.

### Inizia a sviluppare stile e funzionalità


Essere operativi in un ambiente di sviluppo AEM locale in tempi brevi:

1. Installare l’interfaccia della riga di comando AEM: l’interfaccia della riga di comando AEM semplifica le attività di sviluppo. Installiamolo a livello globale utilizzando npm:

   ```Bash
       npm install -g @adobe/aem-cli
   ```

1. Clona il progetto GitHub: clona l’archivio del progetto da GitHub utilizzando il seguente comando, sostituendo <owner> con il proprietario dell’archivio e <repo> con il nome dell’archivio:

   ```
   git clone https://github.com/<owner>/<repo>
   ```

1. Avvia l’ambiente locale: accedi alla directory del progetto e attiva l’istanza AEM locale con un singolo comando:

   ```
   cd <repo>
   aem up
   ```

Il blocco Forms adattivo `blocks/form` cartella è il parco giochi per lo stile e il codice dei moduli. Modifica qualsiasi `.css` o `.js` in questa directory e vedrai le modifiche immediatamente riflesse nel browser.

Sei pronto a mostrare la tua creazione? Utilizza Git per eseguire il commit e inviare le modifiche. Questo aggiorna gli ambienti di anteprima e produzione accessibili da questi URL (sostituisci i segnaposto con i dettagli del progetto):

Anteprima: `https://<branch>--<repo>--<owner>.hlx.page/`
Produzione: `https://<branch>--<repo>--<owner>.hlx.live/`
Congratulazioni! L&#39;ambiente di sviluppo locale è stato configurato e le modifiche sono state implementate.



## Aggiungere un blocco Forms adattivo al progetto AEM esistente


>[!VIDEO](https://video.tv.adobe.com/v/3427789)

Se disponi di un progetto AEM esistente, puoi integrare il blocco di Forms adattivo nel progetto corrente per iniziare a creare i moduli. Per integrare:

1. Clona nel computer l’archivio Adaptive Forms Block: https://github.com/adobe-rnd/aem-boilerplate-forms.

1. All&#39;interno della cartella scaricata, individua `blocks/form` cartella. Copia questa cartella. Ora è possibile passare alla pagina locale del progetto AEM `blocks` e incollare qui la cartella del modulo copiata.

1. Apporta queste modifiche al progetto AEM su GitHub.


Tutto qui. Il blocco Forms adattivo fa ora parte del progetto AEM. Puoi iniziare a creare e aggiungere moduli alle pagine AEM.


## Risoluzione dei problemi di build di GitHub

Garantire un processo di generazione GitHub fluido affrontando potenziali problemi:

* **Errore nel percorso del modulo di risoluzione:**
Se viene visualizzato l&#39;errore &quot;Impossibile risolvere il percorso del modulo &quot;&#39;../../scripts/lib-franklin.js&#39;&quot;, passare alla [Progetto EDS]file /blocks/forms/form.js. Aggiorna l’istruzione di importazione sostituendo il file lib-franklin.js con il file aem.js.

* **Gestisci errori di stampa:**
In caso di errori di stampa, è possibile ignorarli. Apri [Progetto EDS]/package.json e modificare lo script &quot;lint&quot; da `"lint": "npm run lint:js && npm run lint:css"` a `"lint": "echo 'skipping linting for now'"`. Salva il file e conferma le modifiche nel progetto GitHub.


## Consulta anche

* [Creare un modulo utilizzando Google Sheets o Microsoft Excel](/help/edge/docs/forms/create-forms.md)
* [Inviare i moduli direttamente ai fogli di Microsoft Excel o Google](/help/edge/docs/forms/submit-forms.md)
* [Modificare l’aspetto dei moduli](/help/edge/docs/forms/style-theme-forms.md)

