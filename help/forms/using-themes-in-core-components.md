---
title: Creazione e utilizzo dei temi
description: È possibile utilizzare i temi per stilizzare e fornire un’identità visiva a un modulo adattivo utilizzando i componenti core. Puoi condividere un tema in un qualsiasi numero di Adaptive Forms.
source-git-commit: e3fa30d5be29b4070a09873e8ca20036a788486a
workflow-type: tm+mt
source-wordcount: '1669'
ht-degree: 5%

---


# Introduzione ai temi per i moduli adattivi tramite i componenti core {#introduction-to-themes-for-af-using-core-components}

È possibile creare e applicare temi per stilizzare un modulo adattivo utilizzando i componenti core. Un tema contiene dettagli di stile per i componenti e i pannelli. Gli stili includono proprietà quali colori di sfondo, colori dello stato, trasparenza, allineamento e dimensioni. Quando applichi un tema, lo stile specificato si riflette sui componenti corrispondenti. Il tema viene gestito in modo indipendente senza alcun riferimento a un modulo adattivo.

Quando [creare un modulo adattivo](/help/forms/creating-adaptive-form.md) utilizzando i componenti core, i temi predefiniti vengono visualizzati nella sezione **Stile** scheda . Per impostazione predefinita, solo la variabile **Canvas** theme è disponibile.

>[!NOTE]
>
>Un tema Modulo adattivo non deve essere confuso con [Modelli di moduli adattivi.](/help/forms/template-editor.md) I temi per i moduli adattivi contengono solo le informazioni sullo stile per un modulo adattivo. I modelli di modulo adattivo definiscono la struttura del modulo e il contenuto iniziale e contengono un tema per consentire la creazione di nuovi moduli [Modulo adattivo.](/help/forms/creating-adaptive-form.md)

## Utilizzo del tema Canvas in Adaptive Forms utilizzando i componenti core {#using-theme-in-adaptive-form}

I passaggi per applicare un tema a un modulo adattivo sono i seguenti:

1. Accedi alla tua istanza di authoring di AEM Forms.

1. Tocca **Adobe Experience Manager** > **Forms** > **Forms e documenti**.

1. Fai clic su **Crea** > **Forms adattivo**. Viene visualizzata la procedura guidata per la creazione del modulo adattivo.

1. Seleziona il modello del componente di base nella sezione **Origine** scheda .

   >[!NOTE]
   >
   > Quando crei un modulo adattivo con componenti core, il tema Area di lavoro viene visualizzato nella scheda Stile . Questo è l’unico tema pronto all’uso disponibile al momento. Ma puoi cambiare il tema a tuo piacimento e salvarlo per un uso futuro impostando una pipeline front-end.

1. Seleziona il tema Area di lavoro nel **Stile** scheda .
1. Fai clic su **Crea**.

I temi Modulo adattivo vengono utilizzati come parte di un modello Modulo adattivo per definire lo stile durante la creazione di un modulo adattivo.

## Personalizzare il tema {#customizing-theme}

Per personalizzare un tema,

* [impostare una pipeline in Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline)
* Configurare un utente con [ruolo collaboratore](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem.html).
* Dovresti avere un [conoscenza di base di Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git) e archivi Cloud Service Git.

Per personalizzare un tema Canvas:
1. [Clona il tema Canvas](#1-download-canvas-theme-download-canvas-theme)
1. [Comprendere la struttura del tema](#2-understand-structure-of-the-canvas-theme-structure-of-canvas-theme)
1. [Cambia il nome in package.json e package_lock.json](#changename-packagelock-packagelockjson)
1. [Crea il ](#3-create-the-env-file-in-a-theme-folder-creating-env-file-theme-folder)
1. [Avvia il server proxy locale](#4-start-a-local-proxy-server-starting-a-local-proxy-server)
1. [Personalizzare il tema](#customize-the-theme-customizing-theme)
1. [Conferma le modifiche](#6-committing-the-changes-committing-the-changes)
1. [Distribuire la pipeline](#7-deploying-the-customized-theme-deploy-customized-theme)

### 1. Clona il tema Canvas {#download-canvas-theme}

Apri il prompt dei comandi ed esegui il seguente comando per clonare il tema canvas:

```
git clone https://github.com/adobe/aem-forms-theme-canvas
```

>[!NOTE]
>
> La scheda Stile della Creazione guidata modulo visualizza lo stesso nome del tema presente nel file package.json.

### 2. Comprendere la struttura del tema {#structure-of-canvas-theme}

Un tema Modulo adattivo è un pacchetto contenente le risorse CSS, JavaScript e statiche che definiscono lo stile del modulo e rispetta la struttura di un tema Modulo adattivo. Un tema Modulo adattivo presenta la seguente struttura tipica di un progetto front-end:

* `src/components`: File JavaScript e CSS specifici per AEM componenti core
* `src/resources`: file statici come icone, loghi e font
* `src/site`: File JavaScript e CSS applicabili all’intera pagina AEM Sites
* `src/theme.ts`: Il punto di ingresso principale del tema JavaScript e CSS
* `src\theme.scss`: File JavaScript e CSS applicabili all’intero tema

La `src/components` La cartella contiene file JavaScript e CSS specifici per tutti i componenti principali AEM come pulsante, casella di controllo, contenitore, piè di pagina, ecc. Puoi assegnare uno stile a un pulsante o a una casella di controllo modificando il file CSS specifico per il componente AEM.

![Modificare il tema](/help/forms/assets/theme_structure.png)

Per personalizzare il tema, puoi avviare il server proxy locale per visualizzare le personalizzazioni del tema in tempo reale in base al contenuto AEM effettivo.

### 4. Cambia il nome in package.json e package_lock.json del tema Canvas {#changename-packagelock-packagelockjson}

Aggiorna il nome e la versione del tema Canvas nel `package.json` e `package_lock.json` file.

>[!NOTE]
>
> I nomi non devono contenere `@aemforms` tag . Deve essere testo semplice come nome fornito dall’utente.

![Tema tela Pic](/help/forms/assets/changename_canvastheme.png)

### 3. Crea il file .env in una cartella theme {#creating-env-file-theme-folder}

Crea un `.env` nella cartella theme e aggiungi i seguenti parametri:

* **URL AEM**
AEM_URL=https://[istanza autore]

* **Nome del sito AEM**
AEM_ADAPTIVE_FORM=Nome_modulo

* **Porta proxy AEM**
AEM_PROXY_PORT=7000


![Struttura del tema dell&#39;area di lavoro](/help/forms/assets/env-file-canvas-theme.png)

### 4. Avviare un server proxy locale {#starting-a-local-proxy-server}

1. Dalla riga di comando, passa alla root del tema nel computer locale.
1. Esegui `npm install` e npm recupera le dipendenze e installa il progetto.
1. Esegui `npm run live` e il server proxy viene avviato.

   ![npm run live](/help/forms/assets/theme_proxy.png)


1. Tocca o fai clic su **ACCEDI LOCALMENTE (SOLO ATTIVITÀ AMMINISTRATORE)** e accedi con le credenziali utente proxy fornite dall&#39;amministratore AEM.

   ![Accesso locale](/help/forms/assets/local_signin.png)

   >[!NOTE]
   >
   > * Crea un utente locale per l&#39;accesso locale. Fornisci il ruolo di collaboratore per il designer del tema.
   > * Se specifichi l’URL AEM come `http://localhost:[port]/` in `.env` file del tema Canvas, viene reindirizzato direttamente al browser.


1. Una volta effettuato l’accesso, modifica l’URL nel browser in modo che indirizzi al percorso del contenuto di esempio fornito dall’amministratore AEM.

   * Ad esempio, se il percorso fornito è stato `/content/formname.html?wcmmode=disabled`, modifica l’URL in `http://localhost:[port]/content/forms/af/formname.html?wcmmode=disabled`

   ![Contenuto del campione proxy](/help/forms/assets/sample_af.png)

Passa a un modulo adattivo per visualizzare il tema Area di lavoro applicato a un modulo adattivo.

### 5. Personalizzare il tema {#customize-theme}

1. Nell’editor, apri il file `<your-theme-sources>/src/site/_variables.scss`.

   >[!NOTE]
   >
   > Puoi assegnare uno stile a tutti i componenti Modulo adattivo direttamente in un sito modificando il `site/_variables.scss` file.

1. Modifica la variabile per il `font colour` a `red`.

   ![Modificare il tema](/help/forms/assets/edit_theme.png)

   **Personalizzare lo stile dei diversi componenti AEM**

   È possibile assegnare uno stile ai diversi componenti di un modulo adattivo modificando il relativo file CSS nell’editor. Ci sono diverse cartelle CSS per ogni componente di base Modulo adattivo nella cartella Tema area di lavoro.

   ![Componente core](/help/forms/assets/theme-component.png)

   Per specificare gli stili per un componente specifico nell’editor di temi, puoi modificare il CSS in una cartella di temi. Ad esempio, se desideri modificare il colore del bordo di un campo casella di testo, apri il file CSS nell’editor e modificane il colore del bordo.

   ![Modifica CSS casella di testo](/help/forms/assets/edit_color_textbox.png)

1. Quando si salva il file, il server proxy riconosce la modifica tramite la riga `[Browsersync] File event [change]`.

   ![Browsersync proxy](/help/forms/assets/browser_sync.png)

1. Tornando al browser del server proxy locale, la modifica è immediatamente visibile.

   ![cambia tema AF](/help/forms/assets/edit_theme_af.png)

La finestra di progettazione dei temi visualizza in anteprima le modifiche nel server proxy locale e personalizza il tema in base ai requisiti per i diversi componenti AEM.

Prima di apportare le modifiche all’archivio Git AEM, devi accedere al tuo [Informazioni sull’archivio Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git).

### 6. Conferma le modifiche {#committing-the-changes}

Dopo aver apportato modifiche al tema e averlo testato con un server proxy locale, esegui il commit delle modifiche nell’archivio Git del tuo Cloud Service AEM Forms. Rende il tema personalizzato disponibile nell’ambiente del Cloud Service Forms per gli autori di Forms adattivi da utilizzare.

Prima di eseguire il commit delle modifiche nell’archivio Git del Cloud Service AEM Forms, è necessario un clone dell’archivio sul computer locale. Per duplicare l’archivio:

1. Crea un nuovo archivio di temi facendo clic sul pulsante **[!UICONTROL Repository]** opzione .

   ![crea nuovo repo tema](/help/forms/assets/createrepo_canvastheme.png)

1. Fai clic su **[!UICONTROL Aggiungi archivio]** e specifica **Nome archivio** in **Aggiungi archivio** finestra di dialogo. Fai clic su **[!UICONTROL Salva]**.

   ![Aggiungi repository tema canvas](/help/forms/assets/addcanvasthemerepo.png)

1. Fai clic su **[!UICONTROL Copia URL archivio]** per copiare l’URL dell’archivio creato.

   ![URL del tema Canvas](/help/forms/assets/copyurl_canvastheme.png)

1. Apri il prompt dei comandi e duplica l’archivio cloud creato sopra.

   ```
   git clone https://git.cloudmanager.adobe.com/aemforms/Canvasthemerepo/
   ```

1. Sposta i file dell’archivio dei temi che stai modificando nell’archivio cloud con un comando simile a
   `cp -r [source-theme-folder]/* [destination-cloud-repo]`
Ad esempio, utilizzare questo comando 
`cp -r [C:/cloned-git-canvas/*] [C:/cloned-repo]`
1. Nella directory dell’archivio cloud, esegui il commit dei file tema in cui hai spostato con i seguenti comandi.

   ```text
   git add .
   git commit -a -m "Adding theme files"
   git push
   ```

1. Le personalizzazioni vengono inviate all’archivio Git.

   ![Commit delle modifiche eseguito](/help/forms/assets/cmd_git_push.png)

Le personalizzazioni sono ora archiviate in modo sicuro nell’archivio Git.


### 7. Eseguire la pipeline front-end {#deploy-pipeline}

1. Crea la pipeline front-end per distribuire il tema personalizzato. Scopri [come impostare una pipeline front-line per distribuire un tema personalizzato](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline).
1. Esegui la pipeline front-end creata per distribuire la cartella tema personalizzata sotto la **[!UICONTROL Stile]** scheda di una procedura guidata per la creazione di un modulo adattivo.

>[!NOTE]
>
>In futuro, se apporti modifiche alla cartella del tema Canvas, dovrai ripetere la pipeline di cui sopra. Pertanto, è necessario ricordare il nome della pipeline.

## Esempio per personalizzare il tema {#example-to-customize-a-theme}

1. Accedi alla tua istanza di authoring di AEM Forms.
1. Apri un modulo adattivo creato utilizzando i componenti core.
1. Avviare il server proxy locale utilizzando il prompt dei comandi e fare clic su **ACCEDI LOCALMENTE (SOLO ATTIVITÀ AMMINISTRATORE)**.
1. Una volta effettuato l’accesso, verrai reindirizzato al browser e vedrai il tema applicato.
1. Scarica la [Tema canvas](https://github.com/adobe/aem-forms-theme-canvas) ed estrarre la cartella zip scaricata.
1. Apri la cartella zip estratta nell’editor desiderato.
1. Crea un `.env` nella cartella theme e aggiungi parametri: **URL AEM**, **AEM_ADAPTIVE_FORM** e **AEM_PROXY_PORT**.
1. Apri il file CSS della casella di testo nella cartella tema Canvas e modifica il colore del bordo in modo che venga detto `red` e salva le modifiche.
1. Riapri il browser e vedrai che le modifiche si riflettono immediatamente in un Modulo adattivo.
1. Sposta la cartella del tema canvas nell’archivio clonato.
1. Conferma le modifiche ed esegui la pipeline front-end.

Una volta eseguita la pipeline, il tema è disponibile nella scheda Stile .

## Best practice {#best-practices}

* **Evitare risorse da un altro tema**

   Quando modifichi un tema, puoi sfogliare e aggiungere risorse (come le immagini) da altri temi. Ad esempio, si sta modificando lo sfondo di una pagina. Ad esempio, quando selezioni **[!UICONTROL Pagina]** ![pulsante di modifica](assets/edit-button.png)> **[!UICONTROL Sfondo]** > **[!UICONTROL Aggiungi]** > **[!UICONTROL Immagine]**, viene visualizzata una finestra di dialogo che consente di sfogliare e aggiungere immagini in altri temi.

   Puoi riscontrare problemi con il tema corrente se una risorsa viene aggiunta da un altro tema e l’altro tema viene spostato o eliminato. È consigliabile evitare di sfogliare e aggiungere risorse da altri temi.

* **Modifica della larghezza del layout del pannello contenitore**

   Si sconsiglia di modificare la larghezza del layout del pannello contenitore. Quando si specifica la larghezza di un pannello contenitore, questo diventa statico e non si adatta a diversi schermi.

* **Uso dell’editor di moduli o di temi per lavorare con intestazione e piè di pagina**

   Utilizza l’editor di temi se desideri assegnare uno stile a intestazione e piè di pagina utilizzando opzioni di stile quali stile del font, sfondo e trasparenza.
Per fornire informazioni quali un’immagine logo, il nome dell’azienda nell’intestazione e le informazioni sul copyright nel piè di pagina, utilizzare le opzioni dell’editor moduli.
