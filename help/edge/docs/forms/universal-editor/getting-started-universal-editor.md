---
title: Guida introduttiva ai Edge Delivery Services per AEM Forms in Universal Editor - Tutorial per sviluppatori
description: Questo tutorial ti mostrerà come essere subito operativo con un nuovo progetto di Adobe Experience Manager Forms (AEM). Tra dieci o venti minuti, avrai creato il tuo Forms di Edge Delivery Services in Universal Editor.
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: c27b8e413c060de601a72a669d86c4add2a4167d
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 23%

---


# Guida introduttiva ai Edge Delivery Services per AEM Forms con Universal Editor (WYSIWYG)

Nell’era digitale di oggi, i moduli di facile utilizzo sono essenziali per tutte le organizzazioni. I Forms di Edge Delivery Services vengono creati utilizzando l’Editor universale, che offre funzionalità WYSIWYG (what-you-see-is-what-you-get). Fornisce un’interfaccia moderna e intuitiva per un’authoring efficiente dei moduli.

AEM Forms fornisce un blocco, noto come Forms Block adattivo, per facilitare la creazione di Edge Delivery Services Forms per l’acquisizione e l’archiviazione dei dati. È possibile [creare un nuovo progetto AEM preconfigurato con il blocco Forms adattivo](#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) o [aggiungere il blocco Forms adattivo a un progetto AEM esistente](#add-adaptive-forms-block-to-your-existing-aem-project).

Questa esercitazione consente di creare, visualizzare in anteprima e pubblicare un modulo personalizzato con un progetto di sito Adobe Experience Manager nuovo o esistente mediante l&#39;authoring WYSIWYG di Universal Editor.


## Prerequisiti

* Hai un account GitHub e conosci le nozioni di base su Git.
* Hai un account Google o Microsoft SharePoint.
* Comprendi le nozioni di base di HTML, CSS e JavaScript.
* Hai Node/npm installato per lo sviluppo locale.

## Crea un nuovo progetto AEM preconfigurato con Blocco moduli adattivi

Il modello standard di AEM Forms consente di iniziare rapidamente un progetto AEM preconfigurato con il Blocco moduli adattivi. È il modo più rapido e semplice per seguire le best practice dell’AEM e passare direttamente alla creazione dei moduli.

### Introduzione al modello di archivio standard di AEM Forms

1. Crea un archivio GitHub per il progetto AEM. Per creare l’archivio:
   1. Passa a [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms).

      ![AEM Forms standard](/help/edge/docs/forms/assets/eds-form-boilerplate.png)
   1. Fare clic sull&#39;opzione **Usa questo modello** e selezionare l&#39;opzione **Crea nuovo repository**.

      ![Creare un nuovo archivio con AEM Forms standard](/help/edge/docs/forms/assets/use-eds-form-template.png)

      Viene visualizzata la schermata **Crea nuovo repository**.

   1. Nella schermata **Crea nuovo repository**, selezionare **proprietario** e specificare **nome repository**. Adobe consiglia di impostare l&#39;archivio su **Public**. Quindi, seleziona l’opzione **pubblico** e fai clic su **Crea archivio**.

      ![Impostare l’archivio su pubblico](/help/edge/docs/forms/assets/name-eds-repo.png)

1. Installa l’app GitHub della sincronizzazione del codice AEM nell’archivio. Per installare:
   1. Passa a [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new).
   1. Nella schermata **Installa sincronizzazione codice AEM**, seleziona l&#39;opzione **Seleziona solo archivi** e seleziona l&#39;archivio appena creato. Fai clic su **Salva**.

   ![Impostare l’archivio su pubblico](/help/edge/docs/forms/assets/aem-code-sync-up.png)

1. Ora collega l’archivio GitHub creato utilizzando AEM Forms Boilerplate al tuo ambiente di authoring di progetti AEM. Per connettersi:

   1. vai all’archivio GitHub che hai creato in precedenza utilizzando moduli AEM ricorrenti.
   1. Apri il file **fstab.yaml** per la modifica.

      ![apri file fstab.yaml](/help/edge/docs/forms/assets/open-fstab.png)

   1. Modifica il file **fstab.yaml** per aggiornare il punto di montaggio del progetto. Sostituisci l’URL con l’URL dell’istanza di authoring di AEM as a Cloud Service.
      `https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main`

      ![modifica file fstab.yaml](/help/edge/docs/forms/assets/edit-fstab-file.png)

   1. Esegui il commit del file **fstab.yaml** aggiornato, dopo aver aggiornato il riferimento e tutto sembra a posto.

      ![conferma le modifiche](/help/edge/docs/forms/assets/commit-fstab-changes.png)

      Se riscontri problemi di build, consulta [Risoluzione dei problemi di build di GitHub](#troubleshooting-github-build-issues).

### Crea un nuovo progetto AEM

Ora che disponi di un progetto GitHub, puoi procedere con la creazione e la pubblicazione di un nuovo progetto AEM nell’istanza di authoring di AEM as a Cloud Service.
1. Per creare un nuovo progetto AEM:

   1. Accedi all&#39;istanza di authoring di AEM as a Cloud Service e seleziona **Sites**.

      ![seleziona siti](/help/edge/assets/select-sites.png)

   1. Fai clic su **Crea** > **Sito da modello**.

      ![create-sites](/help/edge/docs/forms/assets/create-sites.png)

   1. Selezionare il modello del sito Edge Delivery Services e fare clic su **Avanti**.

      ![select-site-template](/help/edge/docs/forms/assets/select-site-template.png)

      >[!NOTE]
      >
      > * Se il modello Sito Edge Delivery Services non è disponibile nell&#39;istanza di creazione, fare clic sul pulsante Importa per caricare il modello.
      > * È possibile scaricare i modelli di Edge Delivery Services del sito da [GitHub](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases).

   1. Immetti i seguenti dettagli per creare un nuovo progetto AEM:
      * **Titolo sito**: aggiungi un titolo descrittivo per il sito.
      * **Titolo sito** - Utilizza `site-name` definito nel passaggio precedente.
      * **URL GitHub**: utilizza l’URL del progetto GitHub creato nel passaggio precedente.

      ![crea sito AEM](/help/edge/docs/forms/assets/create-aem-site.png)

   1. Viene visualizzata la finestra di dialogo **Crea sito**. Fare clic su **OK**.

      ![fai clic su ok](/help/edge/docs/forms/assets/click-ok-aem-site.png)

      In pochi minuti viene creato il nuovo progetto AEM.

   1. Passa al progetto AEM appena creato nella console Sites e fai clic su **Modifica**.
In questo caso, la pagina `index.html` viene utilizzata a scopo illustrativo.

      ![modifica sito AEM](/help/edge/docs/forms/assets/edit-site.png)

      Il progetto AEM si apre nell’Editor universale in una nuova scheda, che abilita l’authoring WYSIWYG. Ora puoi modificare il progetto AEM.

      ![Il sito verrà aperto in Universal Editor](/help/edge/docs/forms/assets/site-in-universal-editor.png)

1. Publish il progetto AEM creato

   Una volta terminata la modifica del progetto AEM, pubblicalo. Per pubblicare:

   1. Nella console Sites, seleziona tutte le pagine del progetto AEM e fai clic su **Publish rapido**.

      ![pubblica progetto AEM Sites](/help/edge/docs/forms/assets/publish-sites.png)

   1. Viene visualizzata la finestra di dialogo di conferma **Publish** veloce. Fare clic su **Publish** per avviare il processo di pubblicazione.

      ![Finestra di conferma rapida di Publish](/help/edge/docs/forms/assets/quick-publish.png)

      In alternativa, è possibile pubblicare le pagine dei progetti AEM direttamente dall&#39;interfaccia utente di Universal Editor.

      ![Finestra di conferma rapida di Publish](/help/edge/docs/forms/assets/qui.png)

   Congratulazioni Hai un nuovo sito web in esecuzione su `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`.

   * `<branch>` fa riferimento al ramo dell’archivio GitHub.
   * `<repository>` denota l’archivio GitHub.
   * `<owner>` fa riferimento al nome utente dell’account GitHub che ospita l’archivio GitHub.
   * `<site-name>` fa riferimento al nome del sito creato.

   Ad esempio, se il nome del ramo è `main`, l&#39;archivio è `edsforms`, il proprietario è `wkndforms` e il `site-name` è `eds-forms`, il sito Web sarà operativo alle `https://main--edsforms--wkndforms.aem.page/content/eds-forms/`

   >[!NOTE]
   >
   > * Per visualizzare la pagina `index.html` del progetto AEM, utilizzare l&#39;URL: `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`
   > * Per visualizzare pagine diverse da `index page` del progetto AEM, utilizzare l&#39;URL: `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/<site-page-name>`

Ora puoi iniziare a [creare e aggiungere moduli al progetto AEM](#add-edge-delivery-services-forms-to-aem-project).

## Aggiungere un blocco Forms adattivo al progetto AEM esistente

Se disponi di un progetto AEM esistente, puoi integrare il blocco di moduli adattivi nel progetto corrente per iniziare a creare i moduli.

>[!NOTE]
>
>
> Questo passaggio si applica ai progetti generati con [AEM ricorrenti](https://github.com/adobe-rnd/aem-boilerplate-xwalk). Se hai creato il progetto AEM utilizzando [moduli AEM ricorrenti](https://github.com/adobe-rnd/aem-boilerplate-forms), puoi saltare questo passaggio.

Per integrare:

1. Clona l&#39;archivio GitHub Adaptive Forms Block: [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms) nel computer.
1. All&#39;interno della cartella scaricata, trovare la cartella `blocks/form` e copiarla.
1. Clona l’archivio GitHub del progetto AEM sul computer.
1. Passare alla cartella `blocks` nell&#39;archivio progetti AEM locale e incollare la cartella del modulo copiata.
1. Apporta queste modifiche all’archivio dei progetti AEM su GitHub.

Tutto qui. Il blocco Forms adattivo fa ora parte del progetto AEM. Puoi [iniziare a creare e aggiungere moduli al progetto AEM](#add-edge-delivery-services-forms-to-aem-site-project).

## Creare AEM Forms con WYSIWYG

Puoi aprire il progetto AEM nell’editor universale per la creazione di WYSIWYG, dove puoi modificare il progetto e aggiungere la sezione Modulo adattivo per includere i moduli Edge Delivery Services nelle pagine del progetto AEM.

1. Aggiungi la sezione Modulo adattivo alla pagina del progetto AEM. Per aggiungere:
   1. Passa al progetto AEM nella console Sites e fai clic su **Modifica**. La pagina Progetto AEM viene visualizzata in Universal Editor per la modifica.
In questo caso, la pagina `index.html` viene utilizzata a scopo illustrativo.
   1. Apri la struttura Contenuto e passa alla posizione in cui desideri aggiungere la sezione Modulo adattivo.
   1. Fai clic sull&#39;icona **[!UICONTROL Aggiungi]** e seleziona il componente **[!UICONTROL Modulo adattivo]** dall&#39;elenco dei componenti.

   ![struttura contenuto](/help/edge/docs/forms/assets/add-adaptive-form-block.png)

   La sezione Modulo adattivo viene aggiunta nella posizione specificata. È ora possibile iniziare ad aggiungere i componenti del modulo alla pagina Progetto AEM.

1. Aggiungi componenti modulo alla sezione Modulo adattivo aggiunta. Per aggiungere componenti modulo:
   1. Passa alla sezione Modulo adattivo aggiunto nella struttura Contenuto.

      ![blocco modulo adattivo aggiunto](/help/edge/docs/forms/assets/adative-form-block.png)


   1. Fai clic sull’icona **[!UICONTROL Aggiungi]** e aggiungi i componenti desiderati dall’elenco **Componenti modulo adattivo**.

      ![aggiungi componente](/help/edge/docs/forms/assets/add-component.png)

      È inoltre possibile trascinare i componenti Forms adattivi richiesti, in quanto Universal Editor offre una funzione di trascinamento intuitiva.

   1. Seleziona il componente Modulo adattivo aggiunto per aggiornarne le proprietà utilizzando **[!UICONTROL Proprietà]**.

      ![apri proprietà](/help/edge/docs/forms/assets/component-properties.png)

      La schermata seguente mostra il modulo creato nel progetto AEM utilizzando l’authoring WYSIWYG:

      ![modulo aggiunto](/help/edge/docs/forms/assets/added-form-aem-sites.png)

   >[!NOTE]
   >
   > È importante pubblicare nuovamente la pagina del progetto AEM dopo aver apportato modifiche; in caso contrario, gli aggiornamenti non saranno visibili nel browser.

1. Ripubblica la pagina del progetto AEM.

   1. Fai clic su **Publish** per pubblicare nuovamente la pagina del progetto AEM dopo l&#39;aggiunta del modulo.

      ![pubblica modulo](/help/edge/docs/forms/assets/publish-form.png)

   1. Viene visualizzata la finestra di dialogo di conferma di **Publish**. Fare clic su **Publish** per avviare la pubblicazione.

      ![pubblica modulo1](/help/edge/docs/forms/assets/publish-form1.png)

      Dopo aver fatto clic sul pulsante **Publish**, viene visualizzato il messaggio `Publish started successfully`.

      ![pubblica modulo2](/help/edge/docs/forms/assets/publish-form2.png)

   È ora possibile visualizzare la pagina Progetto AEM con il modulo Edge Delivery Services aggiunto al seguente URL:
   `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`.

   Ad esempio, se il nome del ramo è `main`, l&#39;archivio è `edsforms`, il proprietario è `wkndforms` e il nome del sito è `eds-forms`, l&#39;URL sarà:
   `https://main--edsforms--wkndforms.aem.page/content/eds-forms/`

   ![indice pagina](/help/edge/docs/forms/assets/publish-index-page.png)

Puoi assegnare uno stile al Forms dei Edge Delivery Services modificando i file `.css` e `.js` nel blocco Forms adattivo e [configurando un ambiente di sviluppo AEM locale](#set-up-local-aem-development-environment) per visualizzare le modifiche istantaneamente nel browser.

## Configurare l’ambiente locale di sviluppo AEM

Puoi impostare un ambiente di sviluppo AEM locale per sviluppare stili e componenti personalizzati a livello locale. Per essere operativi in un ambiente di sviluppo AEM locale:

1. **Installare AEM CLI**: AEM CLI semplifica le attività di sviluppo. Installalo a livello globale utilizzando npm:

   ```Bash
       npm install -g @adobe/aem-cli
   ```

1. **Clona il progetto GitHub**: clona l&#39;archivio dei progetti AEM da GitHub utilizzando il comando seguente, sostituendo <owner> con il proprietario dell’archivio e <repo> con il nome dell’archivio:

   ```
   git clone https://github.com/<owner>/<repo>
   ```

1. **Avvia l&#39;ambiente locale**: passa alla directory del progetto e avvia l&#39;istanza AEM locale con un singolo comando:

   ```
   cd <repo>
   aem up
   ```

È possibile apportare modifiche locali nella cartella Blocco di Forms adattivo `blocks/form` per la formattazione e la codifica dei moduli. Modificare i file `.css` o `.js` in questa directory e verificare che le modifiche si riflettono immediatamente nel browser.

Una volta completate le modifiche, utilizza i comandi Git per eseguire il commit e inviarle. Questo aggiorna gli ambienti di anteprima e produzione, accessibili dai seguenti URL (sostituisci i segnaposto con i dettagli del progetto):

Anteprima:`https://<branch>--<repo>--<owner>.aem.page/content/<site-name>`
Produzione: `https://<branch>--<repo>--<owner>.aem.live/content/<site-name>`


## Risoluzione dei problemi di compilazione di GitHub

Assicurati un processo di compilazione di GitHub senza intoppi affrontando potenziali problemi:

* **Gestire errori di stampa:**
in caso di errori di stampa, è possibile ignorarli. Apri il file [Progetto EDS]/package.json e modifica lo script “lint” da `"lint": "npm run lint:js && npm run lint:css"` a `"lint": "echo 'skipping linting for now'"`. Salva il file e conferma le modifiche nel progetto GitHub.

<!-- * **Resolve Module Path Error:**
    If you encounter the error "Unable to resolve path to module "'../../scripts/lib-franklin.js'", navigate to the [EDS Project]/blocks/forms/form.js file. Update the import statement by replacing the lib-franklin.js file with the aem.js file. -->
