---
title: Come si creano e utilizzano i temi in Adaptive Forms?
description: Puoi utilizzare i temi per assegnare uno stile e fornire un’identità visiva a un modulo adattivo utilizzando i Componenti core. Puoi condividere un tema in qualsiasi numero di Adaptive Forms.
keywords: temi per generazione moduli, componenti core per la creazione di stili per moduli adattivi, generatore di temi per moduli, creazione di stili per moduli adattivi, personalizzazione di temi, creazione di temi per moduli
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: 11c52b66-dbb1-4c47-a94d-322950cbdac1
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2806'
ht-degree: 4%

---

# Utilizzare i temi per assegnare uno stile ai Componenti core basati su Adaptive Forms{#themes-for-af-using-core-components}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/create-or-customize-themes-for-adaptive-forms-core-components.html?lang=it) |
| AEM as a Cloud Service | Questo articolo |

Puoi creare e applicare temi per assegnare uno stile a un modulo adattivo. Un tema contiene dettagli sullo stile dei componenti e dei pannelli. Gli stili includono proprietà quali i colori di sfondo, i colori degli stati, la trasparenza, l’allineamento e le dimensioni. Quando applichi un tema, lo stile specificato si riflette sui componenti corrispondenti. Un tema viene gestito in modo indipendente senza un riferimento a un modulo adattivo e può essere riutilizzato in più Forms adattivi.

In questo articolo, comprendiamo come progettare look personalizzati per Forms adattivo basato su componenti core utilizzando i temi.

## Temi disponibili per lo stile dei Componenti core

Forms as Cloud Service offre i seguenti temi elencati per i Componenti core basati su Adaptive Forms:

* [Tema Area di lavoro](https://github.com/adobe/aem-forms-theme-canvas)
* [Tema WKND](https://github.com/adobe/aem-forms-theme-wknd)
* [Tema EASEL](https://github.com/adobe/aem-forms-theme-easel)

## Comprendere la struttura dei temi

Un tema è un pacchetto che include componenti di stile come file CSS, file JavaScript e risorse (come le icone) che definiscono lo stile del Forms adattivo. Un tema Modulo adattivo segue un’organizzazione specifica, costituita dai seguenti componenti:

* `src/theme.scss`: questa cartella include il file CSS che ha un ampio impatto sull&#39;intero tema. Funge da posizione centralizzata per definire e gestire lo stile e il comportamento del tema. Apportando modifiche a questo file, puoi apportare modifiche applicate universalmente a tutto il tema, influenzando l’aspetto e le funzionalità sia delle pagine Forms adattive che delle pagine AEM Sites.

* `src/site`: questa cartella contiene file CSS applicati alla pagina di un intero sito AEM. Questi file sono costituiti da codice e stili che influiscono sulle funzionalità e sul layout generali della pagina del sito AEM. Tutte le modifiche apportate qui vengono applicate a tutte le pagine del sito. [Quando utilizzarlo?]

* `src/components`: i file CSS in questa cartella sono progettati per i singoli componenti core di AEM. Ogni cartella dedicata per un componente include un file `.scss` con lo stile di quel particolare componente all&#39;interno di un modulo adattivo. Ad esempio, il file /src/components/accordion/_accordion.scss contiene informazioni sullo stile del componente Pannello a soffietto di Forms adattivo.

  ![struttura tema basata su modulo adattivo](/help/forms/assets/theme_structure.png)

* `src/resources`: questa cartella contiene file statici come icone, loghi e font. Queste risorse vengono utilizzate per migliorare gli elementi visivi e la progettazione complessiva del tema.

## Creare un tema

Forms as Cloud Service fornisce i temi di stile per moduli adattivi per Forms basati su Componenti core, elencati di seguito.

* [Tema Area di lavoro](https://github.com/adobe/aem-forms-theme-canvas)
* [Tema WKND](https://github.com/adobe/aem-forms-theme-wknd)
* [Tema EASEL](https://github.com/adobe/aem-forms-theme-easel)

Puoi [personalizzare uno di questi temi per creare un nuovo tema](#customize-a-theme-core-components).

![Flusso di lavoro di personalizzazione tema](/help/forms/assets/workflow-of-customization-of-theme.png)

## Personalizzare un tema {#customize-a-theme-core-components}

La personalizzazione di un tema si riferisce al processo di modifica, formattazione e personalizzazione dell’aspetto di un tema. Quando si personalizza un tema, è possibile modificarne gli elementi di progettazione, il layout, i colori, la composizione tipografica e, a volte, il codice sottostante. Consente di creare un aspetto univoco e personalizzato per il sito web o l’applicazione, mantenendo la struttura e le funzionalità di base fornite dal tema.

### Prerequisiti {#prerequisites-to-customize}

* Acquisisci familiarità con [la configurazione di una pipeline in Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=it#setup-pipeline) e avere conoscenze di base su come impostare una pipeline ti aiuta a gestire e distribuire in modo efficiente le personalizzazioni dei temi.
* Scopri come [configurare un utente con il ruolo di collaboratore](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem.html?lang=it). Le informazioni su come configurare un utente con il ruolo di collaboratore consentono di concedere le autorizzazioni necessarie per la personalizzazione del tema.
* Installa la versione più recente di [Apache Maven](https://maven.apache.org/download.cgi). Apache Maven è uno strumento di automazione della build comunemente utilizzato per i progetti Java™. L’installazione della versione più recente garantisce che tu disponga delle dipendenze necessarie per la personalizzazione del tema.
* Installa un editor di testo normale. Microsoft® Visual Studio Code. L&#39;utilizzo di un editor di testo normale come Microsoft® Visual Studio Code fornisce un ambiente semplice per la modifica e la modifica dei file dei temi.

### Configurare l’ambiente

* Installa la versione più recente per abilitare i componenti core Adaptive Forms per il tuo ambiente AEM Cloud Service.
* Configura una [pipeline di distribuzione front-end](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/enable-frontend-pipeline-devops/create-frontend-pipeline.html?lang=it) per l&#39;ambiente Cloud Service. In alternativa, puoi configurare la pipeline in un secondo momento, dando la flessibilità di assegnare la priorità ai test e perfezionando il tema prima di impostare la pipeline di distribuzione.

<!-- 
To deploy your themes to a Forms as a Cloud Service environment, first test theme on a local development environment to address any issues. Once the theme is tested, configure the front-end deployment pipeline, which is responsible for deploying the themes.

These themes are deployed to a Forms as a Cloud Service environment via the front-end pipeline. You can configure the pipeline later also, after testing the theme on a local development environment. 

-->

Dopo aver appreso i prerequisiti e configurato l’ambiente di sviluppo, sei pronto per iniziare a personalizzare o formattare il tema in base alle tue esigenze specifiche.

### Personalizzare un tema {#steps-to-customize-a-theme-core-components}

La personalizzazione di un tema è un processo in più fasi. Per personalizzare il tema, esegui i passaggi nell’ordine elencato:

1. [Clona un tema](#download-a-theme-core-components)
1. [Imposta il nome di un tema](#set-name-of-theme)
1. [Personalizzare un tema](#customize-the-theme)
1. [Testare un tema](#test-the-theme)
1. [Distribuire un tema](#deploy-the-theme)

Gli esempi forniti nel documento sono basati sul tema **Canvas**, ma è importante notare che è possibile clonare qualsiasi tema e personalizzarlo utilizzando le stesse istruzioni. Queste istruzioni sono applicabili a qualsiasi tema, consentendo di modificare i temi in base alle esigenze specifiche.

Iniziamo con un processo per creare un’esperienza con il marchio per il Forms adattivo basato su Componenti core utilizzando i temi?

#### &#x200B;1. Clonare un tema {#download-a-theme-core-components}

Per clonare un tema per Forms adattivo basato su Componenti core, scegli uno dei seguenti temi:

* [Tema Area di lavoro](https://github.com/adobe/aem-forms-theme-canvas)
* [Tema WKND](https://github.com/adobe/aem-forms-theme-wknd)
* [Tema EASEL](https://github.com/adobe/aem-forms-theme-easel)

Per clonare un tema, attenersi alle istruzioni riportate di seguito.

1. Apri il prompt dei comandi o la finestra del terminale nell’ambiente di sviluppo locale.

1. Eseguire il comando `git clone` per clonare un tema.

   ```
      git clone [Path of Git Repository of the theme]
   ```

   Sostituisci il [percorso dell&#39;archivio Git del tema] con l&#39;URL effettivo dell&#39;archivio Git corrispondente del tema

   Ad esempio, per clonare il tema Canvas, eseguire il comando seguente:

   ```
      git clone https://github.com/adobe/aem-forms-theme-canvas
   ```

   Dopo aver eseguito correttamente il comando, nella cartella `aem-forms-theme-canvas` del computer è disponibile una copia locale del tema.


#### &#x200B;2. Impostare il nome di un tema {#set-name-of-theme}

1. Apri la cartella dei temi nell’IDE. Ad esempio, per aprire la cartella `aem-forms-theme-canvas` nell&#39;editor di codice di Visual Studio.

1. Passare alla cartella `aem-forms-theme-canvas`.

1. Esegui il comando seguente:

   ```
      code .
   ```

   ![Apri la cartella dei temi in un editor di testo normale](/help/forms/assets/aem-forms-theme-folder-in-vs-code.png)

   La cartella viene aperta nel codice di Visual Studio.

1. Apri il file `package.json` per la modifica.

1. Impostare i valori per gli attributi `name` e `version`.

   ![Immagine di modifica nome tema area di lavoro](/help/forms/assets/changename_canvastheme.png)

   >[!NOTE]
   >
   > * L&#39;attributo name viene utilizzato per identificare in modo univoco il tema e il nome specificato viene visualizzato nella scheda **Style** della **Creazione guidata modulo**.
   > * È possibile selezionare un nome per il tema in base alla scelta, ad esempio `mytheme` o `customtheme`. Tuttavia, per questo caso, è stato specificato il nome `aem-forms-wknd-theme`.

1. Apri il file `package-lock.json` per la modifica.
1. Impostare i valori per gli attributi `name` e `version`. Verificare che i valori per gli attributi `name` e `version` nel file `Package-lock`.json corrispondano a quelli nel file `Package.json`.

   ![Immagine di modifica nome tema area di lavoro](/help/forms/assets/changename_canvastheme-package-lock.png)

1. (Facoltativo) Aprire il file `ReadMe` per modificare e aggiornare il nome del tema.

   ![Immagine di modifica nome tema area di lavoro](/help/forms/assets/changename_canvastheme-readme-file.png)

1. Salvare e chiudere i file.

**Considerazioni durante l&#39;impostazione del nome del tema**

* È obbligatorio rimuovere `@aemforms` dal nome del tema nel file `Package.json` e nel file `Package-lock.json`. Se non si rimuove `@aemforms` dal nome del tema personalizzato, si verifica un errore della pipeline front-end durante la distribuzione del tema.
* Si consiglia di aggiornare il tema `version` nel file `Package.json` e nel file `Package-lock.json` per riflettere con precisione le modifiche e i miglioramenti apportati nel tempo al tema.
* Per informazioni importanti sull&#39;utilizzo, sulle istruzioni di installazione e su altri dettagli rilevanti, si consiglia di aggiornare il nome del tema nel file `ReadMe`.

#### &#x200B;3. Personalizzare un tema {#customize-the-theme}

È possibile personalizzare singoli componenti o apportare modifiche a livello di tema utilizzando le variabili globali di un tema. Eventuali modifiche apportate alle variabili globali influiscono su tutti i singoli componenti. Ad esempio, è possibile utilizzare le variabili globali per modificare il colore del bordo di tutti i componenti di un modulo adattivo e un colore di riempimento luminoso per impostare CTA (Call to action) utilizzando il componente pulsante:

* [Impostare gli stili del livello tema](#theme-customization-global-level)

* [Impostare gli stili a livello di componente](#component-based-customization)

##### Impostare gli stili del livello tema{#theme-customization-global-level}

Il file `variable.scss` contiene le variabili globali del tema. Aggiornando queste variabili, puoi apportare modifiche relative allo stile a livello di tema. Per applicare gli stili a livello di tema, effettua le seguenti operazioni:

1. Apri il file `<your-theme-sources>/src/site/_variables.scss` per la modifica.
1. Modifica il valore di qualsiasi proprietà. Il colore predefinito dell&#39;errore, ad esempio, è `red`. Per modificare il colore dell&#39;errore da `red` a `blue`, modificare il codice esadecimale del colore di `$errorvariable`. Ad esempio, `$error: #196ee5`.
1. Salva e chiudi il file.

   ![Modificare il tema](/help/forms/assets/edit_theme.png)

Analogamente, è possibile utilizzare il file `variable.scss` per impostare la famiglia e il tipo di carattere, i colori del tema e del carattere, la dimensione del carattere, la spaziatura del tema, l&#39;icona di errore, gli stili del bordo del tema e altre variabili che influiscono su più componenti del modulo adattivo.

##### Impostare gli stili a livello di componente {#component-based-customization}

Puoi anche modificare il font, il colore, le dimensioni e altre proprietà CSS di un componente core Modulo adattivo specifico. Ad esempio, pulsante, casella di controllo, contenitore, piè di pagina e altro ancora. Puoi assegnare uno stile a un pulsante o a una casella di controllo modificando il file CSS del componente specifico in modo da allinearlo allo stile della tua organizzazione. Per personalizzare uno stile di un componente:

1. Aprire il file `<your-theme-sources>/src/components/<component>/<component.scss>` per la modifica. Ad esempio, per modificare il colore del carattere del componente pulsante, aprire il file `<your-theme-sources>/src/components/button/button.scss`.
1. Modifica il valore di qualsiasi in base alle tue esigenze. Ad esempio, per cambiare il colore del componente Pulsante al passaggio del mouse su `green`, modificare il valore della proprietà `color: $white` nella classe `cmp-adaptiveform-button__widget:hover` in codice esadecimale `#12B453` o in qualsiasi altra sfumatura di `green`. Il codice finale è simile al seguente:

   ```
   .cmp-adaptiveform-button__widget:hover {
   background: $dark-gray;
   color: #12B453;
   }
   ```

1. Salva e chiudi il file.

   ![Modifica CSS casella di testo](/help/forms/assets/edit_color_textbox.png)

   >[!NOTE]
   >
   > Quando uno stile viene definito sia a livello di tema che a livello di componente, lo stile definito a livello di componente ha la priorità.

#### &#x200B;4. Testare un tema personalizzato {#test-the-theme}

Per visualizzare in anteprima e testare le modifiche nell’ambiente locale e personalizzare il tema in base ai requisiti per i diversi componenti di AEM, effettua le seguenti operazioni:

* 4.1 [Configurare un ambiente locale per il test](#rename-env-file-theme-folder)
* 4.2 [Verifica il tema utilizzando l&#39;ambiente locale](#start-a-local-proxy-server)

##### 4.1. Configurare un ambiente locale per il test {#rename-env-file-theme-folder}

1. Apri la cartella dei temi nell’IDE. Aprire ad esempio la cartella `aem-forms-theme-canvas` nell&#39;editor di codice di Visual Studio.
1. Rinomina il file `env_template` in `.env` nella cartella dei temi e aggiungi i seguenti parametri:

   ```
   * **AEM url**
   AEM_URL=https://[author-instance] 
   
   * **AEM Adaptive form name**
   AEM_ADAPTIVE_FORM=Form_name
   
   * **AEM proxy port**
   AEM_PROXY_PORT=7000
   ```

   Ad esempio, l&#39;URL del modulo è `http://localhost:4502/editor.html/content/forms/af/contactusform.html`. Quindi, i valori di:

   * URL_AEM = `http://localhost:4502/`
   * AEM_ADAPTIVE_FORM = `contactusform`

1. Salva il file.

   ![Struttura Tema Area Di Lavoro](/help/forms/assets/env-file-canvas-theme.png)

##### 4.2 Testare il tema utilizzando un ambiente locale {#start-a-local-proxy-server}

1. Passa alla cartella principale della cartella dei temi. In questo caso, il nome della cartella dei temi è `aem-forms-theme-canvas`.
1. Apri il prompt dei comandi o il terminale.
1. Eseguire `npm install` per installare le dipendenze.
1. Esegui `npm run live` per visualizzare in anteprima il modulo con il tema aggiornato nel browser locale.

   >[!NOTE]
   >
   > Se si verifica un errore durante l&#39;esecuzione del comando `npm run live`, eseguire i comandi seguenti prima del comando `npm run live`:
   >
   > * `npm install parcel --save-dev`
   > * `npm i @parcel/transformer-sass`

Questa è una distribuzione a caldo. Pertanto, ogni volta che si apportano modifiche e si salvano i file `_variables.scss` e `button.scss`, il server seleziona automaticamente le modifiche e visualizza in anteprima l&#39;output più recente. La riga `[Browsersync] File event [change]` indica che il server ha riconosciuto le modifiche più recenti e sta distribuendo le modifiche nell&#39;ambiente locale.

![Browsersync proxy](/help/forms/assets/browser_sync.png)

Dopo aver seguito gli esempi relativi allo stile di un modulo adattivo (componenti core) a livello di tema e di componente per le personalizzazioni dei temi, i messaggi di errore di un modulo adattivo vengono modificati nel colore `blue`, mentre il colore dell&#39;etichetta del componente pulsante diventa `green` al passaggio del mouse.

**Anteprima stile livello tema**

![Esempio: colore dell&#39;errore impostato su blu](/help/forms/assets/theme-level-changes.png)

**Anteprima dello stile a livello di componente**

![Esempio: colore al passaggio del mouse impostato su verde](/help/forms/assets/button-customization.png)

La personalizzazione di un tema consente di progettare look personalizzati per Forms adattivo basato su Componenti core in base ai requisiti organizzativi.

###### Test del tema per i moduli in hosting in un ambiente Cloud Service

Puoi anche testare il tema per il modulo adattivo ospitato nell’istanza as a Cloud Service di AEM Forms. Per configurare e impostare l’ambiente locale per il test dei temi con Adaptive Forms ospitato sull’istanza cloud, effettua le seguenti operazioni:

1. Apri la cartella dei temi nell’IDE. Aprire ad esempio la cartella `aem-forms-theme-canvas` nell&#39;editor di codice di Visual Studio.
1. Rinominare il file `env_template` nel file `.env` e aggiungere i seguenti parametri:

   ```
   * **AEM url**
   AEM_URL=https://[author-instance] 
   
   * **AEM Adaptive form name**
   AEM_ADAPTIVE_FORM=Form_name
   
   * **AEM proxy port**
   AEM_PROXY_PORT=7000
   ```

   Ad esempio, l&#39;URL del modulo nell&#39;ambiente cloud è `https://author-XXXX.adobeaemcloud.com/editor.html/content/forms/af/contactusform.html`. Quindi, i valori di:

   * URL_AEM = `https://author-XXXX-cmstg.adobeaemcloud.com/`
   * AEM_ADAPTIVE_FORM = `contactusform`
1. Salva il file.
1. Crea un utente locale.

   >[!NOTE]
   >
   > Per creare un utente locale:
   >
   > * Vai alla **[!UICONTROL Home di AEM]** > **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Utenti]**.
   > * Verificare che l&#39;utente sia membro del gruppo `forms-users`.

1. Passa alla cartella principale della cartella dei temi. In questo caso, il nome della cartella dei temi è `aem-forms-theme-canvas`.
1. Eseguire `npm run live` e si viene reindirizzati a un browser locale.
1. Fare clic su `SIGN IN LOCALLY (ADMIN TASKS ONLY)` e accedere utilizzando le credenziali dell&#39;utente locale.

Puoi visualizzare in anteprima il modulo adattivo con le modifiche più recenti. Una volta apportate le modifiche desiderate in una cartella dei temi, distribuisci il tema nell’ambiente AEM Cloud Service utilizzando la pipeline front-end.

#### &#x200B;5. Distribuire un tema {#deploy-the-theme}

Per distribuire il tema nell’ambiente Cloud Service utilizzando la pipeline front-end:

* 5.1 [Crea un archivio per il tema](#create-a-new-theme-repo)
* 5.2 [Invia le modifiche all&#39;archivio](#committing-the-changes)
* 5.3 [Eseguire la pipeline front-end](#run-a-frontend-pipeline)

##### 5.1 Creare un archivio per il tema{#create-a-new-theme-repo}

Per distribuire il tema è necessario un repository. Accedi al tuo [archivio AEM Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=it#accessing-git) e aggiungi un nuovo archivio per il tema.

1. Creare un nuovo archivio per un tema facendo clic su **[!UICONTROL Archivi]** > **[!UICONTROL Aggiungi archivio]**.

   ![crea nuovo archivio tema](/help/forms/assets/createrepo_canvastheme.png)


1. Specificare il **Nome repository** nella finestra di dialogo **Aggiungi repository**. Ad esempio, il nome fornito è `custom-canvas-theme-repo`.
1. Fai clic su **[!UICONTROL Salva]**.

   ![Aggiungi archivio temi canvas](/help/forms/assets/addcanvasthemerepo.png)

1. Fare clic su **[!UICONTROL Copia URL repository]** per copiare l&#39;URL del repository.

   ![URL tema quadro](/help/forms/assets/copyurl_canvastheme.png)

   >[!NOTE]
   > 
   >* È possibile utilizzare un singolo archivio per più temi.
   >* Per distribuire temi diversi, devi creare pipeline front-end separate.
   >* È possibile, ad esempio, utilizzare lo stesso repository, come `custom-canvas-theme-repo`, per i temi Canvas, WKND e EASEL. Tuttavia, per distribuire i temi, è necessario creare pipeline front-end separate. Le personalizzazioni future per un tema specifico vengono distribuite utilizzando la pipeline front-end corrispondente.

##### 5.2. Inviare le modifiche all’archivio {#committing-the-changes}

Ora, invia le modifiche all’archivio dei temi del tuo Cloud Service AEM Forms.

1. Passa alla cartella principale della cartella dei temi.  In questo caso, il nome della cartella dei temi è `aem-forms-theme-canvas`.
1. Apri il prompt dei comandi o il terminale.
1. Esegui il comando seguente nell&#39;ordine elencato:

   ```
   git remote add [alias-name-for-repository] [URL of repository]
   git add .
   git commit
   git push [name-for-createdrepository]
   ```

   Ad esempio:

   ```
   git remote add canvascloudthemerepo https://git.cloudmanager.adobe.com/stage-aemformsdev/customcanvastheme/
   git add .
   git commit
   git push canvascloudthemerepo 
   ```

   ![Commit delle modifiche eseguito](/help/forms/assets/cmd_git_push.png)



##### 5.3 Eseguire la pipeline front-end {#run-a-frontend-pipeline}

Il tema viene distribuito utilizzando la [pipeline front-end](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/enable-frontend-pipeline-devops/create-frontend-pipeline.html?lang=it). Per distribuire il tema, effettua le seguenti operazioni:

1. Accedi al tuo archivio AEM Cloud Manager.
1. Fai clic sul pulsante **[!UICONTROL Aggiungi]** nella sezione **[!UICONTROL Pipeline]**.
1. Seleziona **[!UICONTROL Aggiungi pipeline non di produzione]** o **[!UICONTROL Aggiungi pipeline di produzione]** in base all&#39;ambiente Cloud Service. Ad esempio, in questo caso è selezionata l&#39;opzione **[!UICONTROL Aggiungi pipeline di produzione]**.
1. Nella finestra di dialogo **[!UICONTROL Aggiungi pipeline di produzione]** come parte dei passaggi **[!UICONTROL Configurazione]**, specifica il nome per la pipeline. Ad esempio, il nome della pipeline è `customcanvastheme`.
1. Fai clic su **[!UICONTROL Continua]**.
1. Selezionare la **[!UICONTROL distribuzione di destinazione]** > le **[!UICONTROL opzioni del codice front-end]** in
**[!UICONTROL Codice Source]** passaggi.
1. Seleziona i valori **[!UICONTROL Archivio]** e **[!UICONTROL Ramo Git]** che contengono le modifiche più recenti. Ad esempio, qui il nome dell&#39;archivio selezionato è `custom-canvas-theme-repo` e il ramo Git è `main`.
1. Selezionare **[!UICONTROL Posizione codice]** come `/`, se le modifiche sono presenti nella cartella principale.
1. Fai clic su **[!UICONTROL Salva]**.
   ![crea pipeline front-end](/help/forms/assets/canvas-theme-frontendpipeline.gif)

   Al termine dell’installazione della pipeline, la scheda call-to-action viene aggiornata.

1. Fate clic con il pulsante destro del mouse sulla tubazione creata.
1. Fare clic su **[!UICONTROL Esegui]**.

   ![run-a-pipleine](/help/forms/assets/canvas-theme-run-pipeline.png)

Una volta completata la build, il tema diventa disponibile nell’istanza di authoring per l’utilizzo. Viene visualizzato nella scheda **[!UICONTROL Stile]** della procedura guidata di creazione dei moduli adattivi durante la creazione di un modulo adattivo.

![tema personalizzato disponibile nella scheda stile](/help/forms/assets/custom-theme-style-tab.png)

Il tema personalizzato consente di creare un’esperienza con il marchio per un Forms adattivo basato su Componenti core.

## Applicare un tema a un modulo adattivo {#using-theme-in-adaptive-form}

I passaggi per applicare un tema a un modulo adattivo sono i seguenti:

1. Accedi all’istanza Autore di AEM Forms.

1. Seleziona **Adobe Experience Manager** > **Moduli** > **Moduli e documenti**.

1. Fai clic su **Crea** > **Forms adattivo**. Viene visualizzata la procedura guidata per la creazione di un modulo adattivo.

1. Selezionare il modello di componente di base nella scheda **Source**.
1. Selezionare il tema nella scheda **Stile**.
1. Fai clic su **Crea**.

I temi per moduli adattivi vengono utilizzati come parte di un modello di modulo adattivo per definire lo stile durante la creazione di un modulo adattivo.

## Best practice {#best-practices}

* **Evitare risorse da un altro tema**

  Quando modifichi un tema, puoi sfogliare e aggiungere risorse (come immagini) da altri temi. Ad esempio, stai modificando lo sfondo di una pagina. Ad esempio, quando selezioni **[!UICONTROL Pagina]** ![pulsante di modifica](assets/edit-button.png)> **[!UICONTROL Sfondo]** > **[!UICONTROL Aggiungi]** > **[!UICONTROL Immagine]**, viene visualizzata una finestra di dialogo che consente di sfogliare e aggiungere immagini in un altro tema.

  Se una risorsa viene aggiunta da un altro tema e l’altro tema viene spostato o eliminato, puoi riscontrare dei problemi con il tema corrente. Si consiglia di evitare di sfogliare e aggiungere risorse da altri temi.

* **Modifica della larghezza del layout del pannello contenitore**

  La modifica della larghezza del layout del pannello contenitore non è consigliata. Quando si specifica la larghezza di un pannello contenitore, questo diventa statico e non si adatta a visualizzazioni diverse.

## Domande frequenti {#faq}

**Q:** Quale personalizzazione ha priorità quando si eseguono personalizzazioni in una cartella dei temi a livello globale e di componente?

**Ans:** Quando si eseguono personalizzazioni a livello globale e di componente, la personalizzazione a livello di componente ha la priorità.

<!--

## See next

* [Set layout of forms for different screen sizes and device types](/help/sites-cloud/authoring/page-editor/responsive-layout.md)
* [Generate Document of Record for Adaptive Forms (Core Components](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
* [Create an Adaptive Forms with Repeatable sections](/help/forms/create-forms-repeatable-sections.md)
* [Sample themes templates and form data models](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=it)

-->


## Consulta anche {#see-also}

{{see-also}}

* [Impostare il layout dei moduli per dimensioni di schermo e tipi di dispositivi diversi](/help/sites-cloud/authoring/page-editor/responsive-layout.md)
* [Generare un documento di record per Forms adattivo (componenti core)](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
* [Creare un Forms adattivo con sezioni ripetibili](/help/forms/create-forms-repeatable-sections.md)
* [Modelli di temi di esempio e modelli di dati modulo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=it)
