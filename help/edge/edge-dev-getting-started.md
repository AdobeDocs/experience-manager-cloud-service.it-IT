---
title: Guida introduttiva per sviluppatori per l’authoring di AEM con Edge Delivery Services
description: Questa guida ti aiuterà a essere subito operativo con un nuovo sito Adobe Experience Manager utilizzando Edge Delivery Services e l’Editor universale per l’authoring dei contenuti
feature: Edge Delivery Services
exl-id: a71184a7-c954-442e-b276-99edc6d2acd8
source-git-commit: bae9a5178c025b3bafa8ac2da75a1203206c16e1
workflow-type: ht
source-wordcount: '989'
ht-degree: 100%

---

# Authoring di AEM con Edge Delivery Services {#edge-dev-getting-started}

Questa guida ti aiuterà a essere subito operativo con un nuovo sito Adobe Experience Manager utilizzando Edge Delivery Services e l’Editor universale per l’authoring dei contenuti.

{{aem-authoring-edge-early-access}}

## Prerequisiti {#prerequisites}

Prima di iniziare questa guida, è necessario avere già familiarità con le nozioni di base di e avere accesso a Edge Delivery Services, quali:

* Il completamento di un [tutorial su Edge Delivery Service.](/help/edge/developer/tutorial.md)
* L’accesso a una [sandbox di AEM Cloud Service.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)
* L’[attivazione dell’Editor universlae nello stesso ambiente sandbox.](/help/implementing/universal-editor/getting-started.md)

## Scegliere l’editor giusto {#editor-choice}

AEM offre due diversi editor di contenuti; la possibilità di scegliere quale utilizzare dipende dalla tua situazione.

* **Editor universale**: questa dovrebbe essere la scelta predefinita per i nuovi siti.
* **Editor pagina AEM**: deve essere scelto per una migrazione AEM Sites esistente verso Edge Delivery Services.

Questa guida è incentrata sui Progetti AEM di Edge Delivery Services che utilizzano l’Editor universale. Per ulteriori dettagli sulla scleta dell’editor giusto e la migrazione di AEM Sites esistenti verso Edge Delivery Services, consulta il documento [Sviluppo per Edge Delivery Services](/help/edge/developing.md).

## Guida introduttiva all’authoring di AEM e a Edge Delivery Services {#getting-started}

Dopo aver completato [i prerequisiti](#prerequisites) e aver effettuato [la scelta di utilizzare l’Editor universale,](#editor-choice) puoi iniziare a utilizzare il tuo progetto.

### Creare un progetto GitHub {#create-github-project}

Prima devi creare un nuovo progetto su GitHub, basato sul modello di Adobe.

1. Passa a [`https://github.com/adobe-rnd/aem-boilerplate-xwalk`](https://github.com/adobe-rnd/aem-boilerplate-xwalk) e fai clic su **Usa questo modello** e seleziona **Crea un nuovo archivio**.

   * Per visualizzare questa opzione, devi aver effettuato l’accesso a GitHub.

   ![Copiare un progetto di archivio](assets/edge-dev-getting-started/use-template-project.png)

1. L’archivio viene assegnato all’utente per impostazione predefinita. Modifica questo stato in base alle esigenze, fornisci un nome e una descrizione all’archivio e fai clic su **Crea archivio**.

   ![Creazione dell’archivio](assets/edge-dev-getting-started/create-repo.png)

1. In una nuova scheda nello stesso browser, passa a [`https://github.com/apps/aem-code-sync`](https://github.com/apps/aem-code-sync) e fai clic su **Configura**.

   ![Sincronizzazione codice](assets/edge-dev-getting-started/configure-code-sync.png)

1. Fai clic su **Configura** per l’organizzazione in cui hai creato il nuovo archivio nel passaggio precedente.

   ![Scelta dell’organizzazione per la sincronizzazione del codice](assets/edge-dev-getting-started/code-sync-org.png)

1. Nella pagina GitHub della sincronizzazione del codice AEM in **Accesso archivio**, seleziona **Seleziona solo archivi**, seleziona l’archivio creato nel passaggio precedente e quindi fai clic su **Salva**.

   ![Concessione accesso alla sincronizzazione del codice AEM](assets/edge-dev-getting-started/grant-code-sync-acces.png)

1. Dopo aver installato la sincronizzazione del codice AEM, verrà visualizzata una schermata di conferma. Torna alla scheda del browser del nuovo archivio.

   ![Conferma dell’installazione della sincronizzazione del codice AEM](assets/edge-dev-getting-started/confirmation.png)

1. Fai clic sul file `fstab.yaml` per aprirlo e quindi sull’icona **Modifica questo file** per modificarlo.

   ![fstab.yaml](assets/edge-dev-getting-started/fstab.png)

1. Modifica il file `fstab.yaml` per aggiornare il punto di montaggio del progetto. Sostituisci l’URL predefinito dei Documenti Google con l’URL dell’istanza di authoring di AEM as a Cloud Service, quindi fai clic su **Conferma modifiche...**.

   * `https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main`
   * La modifica del punto di montaggio indica a Edge Delivery Services dove trovare il contenuto del sito.

   ![Aggiornamento fstab](assets/edge-dev-getting-started/fstab-update.png)

1. Aggiungi un messaggio di conferma come desiderato, quindi fai clic su **Conferma modifiche**, per confermarle direttamente nel ramo `main`.

   ![Conferma delle modifiche](assets/edge-dev-getting-started/commit-fstab-changes.png)

1. Torna alla directory principale dell’archivio e fai clic su `paths.yaml` e quindi sull’icona **Modifica questo file**.

   ![paths.yaml](assets/edge-dev-getting-started/paths.png)

1. Sostituisci le mappature predefinite con `/content/<site-name>/:/` e fai clic su **Conferma modifiche...**.

   * Fornisci il tuo `<site-name>`. Ne avrai bisogno in un passaggio successivo.
   * Le mappature spiegano a Edge Delivery Services come mappare il contenuto nell’archivio AEM all’URL del sito.

   ![Aggiornamento paths.yaml](assets/edge-dev-getting-started/paths-update.png)

1. Aggiungi un messaggio di conferma come desiderato, quindi fai clic su **Conferma modifiche**, per confermarle direttamente nel ramo `main`.

   ![Conferma delle modifiche](assets/edge-dev-getting-started/commit-fstab-changes.png)

### Creare e modificare un nuovo sito AEM {#create-aem-site}

Ora che disponi di un progetto GitHub, crea un nuovo sito AEM utilizzabile dal progetto.

>[!NOTE]
>
>Per modificare il sito con l’Editor universale, è necessario utilizzare un browser basato su Chromium.

1. Richiedi l’ultimo modello del sito di authoring AEM con Edge Delivery Services dai team tecnici di Adobe tramite il tuo [canale Slack del progetto.](/help/edge/docs/slack.md)

1. Accedi all’istanza di authoring AEM as a Cloud Service, passa alla console Sites e tocca o fai clic su **Crea** -> **Sito da modello**.

   ![Creare un nuovo sito dalla console](assets/edge-dev-getting-started/create-site-console.png)

1. Sulla scheda **Seleziona un modello di sito** della procedura guidata di creazuione del sito, fai clic sul pulsante **Importa** per importare un nuovo modello.

   ![Importazione di modelli](assets/edge-dev-getting-started/site-templates.png)

1. Carica il modello del sito di authoring AEM con Edge Delivery Services fornito dal team tecnici di Adobe.

1. Dopo aver creato il modello, verrà visualizzato nella procedura guidata. Tocca o fai clic per selezionarlo, quindi tocca o fai clic su **Avanti**.

   ![Seleziona modello](assets/edge-dev-getting-started/select-template.png)

1. Fornisci i campi seguenti e tocca o fai clic su **Crea**.

   * **Titolo sito**: aggiungi un titolo descrittivo per il sito.
   * **Titolo sito**: utilizza il `<site-name>` che hai definito nel [passaggio precedente.](#create-github-project)
   * **URL GitHub**: utilizza l’URL del progetto GitHub creato nel passaggio precedente.

   ![Dettagli del sito](assets/edge-dev-getting-started/create-site-details.png)

1. AEM conferma la creazione del sito con una finestra di dialogo. Tocca o fai clic su **OK** per chiudere.

   ![Conferma creazione del sito](assets/edge-dev-getting-started/site-creation-confirmation.png)

1. Nella console Sites, passa al `index.html` del nuovo sito creato e tocca o fai clic su **Modifica** nella barra degli strumenti.

   ![Modifica del nuovo sito](assets/edge-dev-getting-started/new-site.png)

1. L’Editor universale si aprirà in una nuova scheda. Potrebbe essere necessario toccare o fare clic su **Accedi con Adobe** per eseguire l’autenticazione e modificare la pagina.

   ![Editor universale](assets/edge-dev-getting-started/universal-editor.png)

È ora possibile modificare il sito utilizzando l’Editor universale. Per ulteriori informazioni, consulta la [documentazione dell’Editor universale](/help/sites-cloud/authoring/universal-editor/authoring.md).

### Pubblicazione del nuovo sito {#publishing}

Una volta terminata la modifica del nuovo sito tramite l’Editor universale, puoi pubblicare i tuoi contenuti.

1. Nella console Sites, seleziona tutte le pagine create per il nuovo sito e tocca o fai clic su **Pubblicazione rapida** nella barra degli strumenti.

   ![Selezione delle pagine da pubblicare](assets/edge-dev-getting-started/publishing.png)

1. Tocca o fai clic su **Pubblica** nella finestra di dialogo di conferma per avviare il processo.

   ![Finestra di dialogo Pubblica](assets/edge-dev-getting-started/publish-confirmation.png)

1. Apri una nuova scheda nello stesso browser e passa all’URL del nuovo sito.

   * `https://main--<site-name>--<owner>.hlx.page`

1. Visualizza il tuo contenuto pubblicato.

   ![Contenuto pubblicato](assets/edge-dev-getting-started/published-site.png)

## Passaggi successivi {#next-steps}

Ora che hai un progetto AEM in fase di elaborazione con Edge Delivery Services, puoi iniziare a creare e formattare i blocchi.

Per ulteriori informazioni, consulta la guida [Creazione di blocchi preparati per l’utilizzo con l’editor universale](/help/edge/create-block.md).
