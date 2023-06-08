---
title: Creazione e utilizzo di temi
description: Puoi utilizzare i temi per formattare e fornire un’identità visiva a un modulo adattivo utilizzando i componenti core. Puoi condividere un tema in qualsiasi numero di Adaptive Forms.
exl-id: 11c52b66-dbb1-4c47-a94d-322950cbdac1
source-git-commit: f22554450d2eb1f4948f749ba00f78b568ee308f
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 5%

---

# Temi in Forms adattivo (componenti core) {#themes-for-af-using-core-components}

Puoi creare e applicare temi per formattare un modulo adattivo utilizzando i componenti core. Un tema contiene dettagli sullo stile dei componenti e dei pannelli. Gli stili includono proprietà quali i colori di sfondo, i colori degli stati, la trasparenza, l&#39;allineamento e le dimensioni. Quando applicate un tema, lo stile specificato viene riflesso sui componenti corrispondenti. Il tema viene gestito in modo indipendente senza un riferimento a un modulo adattivo.

Quando [creare un modulo adattivo](/help/forms/creating-adaptive-form.md) utilizzando i Componenti core, i temi predefiniti vengono visualizzati sotto **Stile** scheda. Per impostazione predefinita, solo il **Area di lavoro** Il tema è disponibile.

>[!NOTE]
>
>Un tema per moduli adattivi non deve essere confuso con [Modelli per moduli adattivi.](/help/forms/template-editor.md) I temi per moduli adattivi contengono solo le informazioni sullo stile di un modulo adattivo. I modelli per moduli adattivi definiscono la struttura del modulo e il contenuto iniziale e contengono un tema per consentire la creazione di nuovi [Modulo adattivo.](/help/forms/creating-adaptive-form.md)

## Utilizzo del tema Canvas in Adaptive Forms tramite i componenti core {#using-theme-in-adaptive-form}

I passaggi per applicare il tema a un modulo adattivo sono i seguenti:

1. Accedi all’istanza Autore di AEM Forms.

1. Tocca **Adobe Experience Manager** > **Forms** > **Forms e documenti**.

1. Clic **Crea** > **Forms adattivo**. Viene visualizzata la procedura guidata per la creazione di un modulo adattivo.

1. Seleziona il modello di componente core in **Sorgente** scheda.

   >[!NOTE]
   >
   > Quando crei un modulo adattivo con componenti core, il tema Area di lavoro viene visualizzato nella scheda Stile. Questo è l’unico tema predefinito attualmente disponibile. Ma puoi cambiare il tema a tuo piacimento e salvarlo per un utilizzo futuro impostando una pipeline front-end.

1. Seleziona il tema dell’area di lavoro nel **Stile** scheda.
1. Fai clic su **Crea**.

I temi per moduli adattivi vengono utilizzati come parte di un modello di modulo adattivo per definire lo stile durante la creazione di un modulo adattivo.

## Personalizzare il tema {#customizing-theme}

Per personalizzare un tema:

* [configurare una pipeline in Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline)
* Configurare un utente con [ruolo collaboratore](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem.html).
* Dovresti avere un [conoscenza di base di Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git) e archivi Git di Cloud Service.

Per personalizzare un tema Area di lavoro:

1. [Clonare il tema Canvas](#1-download-canvas-theme-download-canvas-theme)
1. [Comprendere la struttura del tema](#2-understand-structure-of-the-canvas-theme-structure-of-canvas-theme)
1. [Modificare il nome in package.json e package_lock.json](#changename-packagelock-packagelockjson)
1. [Creare ](#3-create-the-env-file-in-a-theme-folder-creating-env-file-theme-folder)
1. [Avvia il server proxy locale](#4-start-a-local-proxy-server-starting-a-local-proxy-server)
1. [Personalizzare il tema](#customize-the-theme-customizing-theme)
1. [Eseguire il commit delle modifiche](#6-committing-the-changes-committing-the-changes)
1. [Distribuire la pipeline](#7-deploying-the-customized-theme-deploy-customized-theme)

### 1. Clonare il tema Canvas {#download-canvas-theme}

Apri il prompt dei comandi ed esegui il comando seguente per clonare il tema dell’area di lavoro:

```
git clone https://github.com/adobe/aem-forms-theme-canvas
```

>[!NOTE]
>
> Nella scheda Stile della Creazione guidata modulo viene visualizzato lo stesso nome tema del file package.json.

### 2. Comprendere la struttura del tema {#structure-of-canvas-theme}

Un tema per moduli adattivi è un pacchetto contenente le risorse CSS, JavaScript e statiche che definiscono lo stile del modulo e ne rispettano la struttura. Un tema Modulo adattivo presenta la seguente struttura, tipica di un progetto front-end:

* `src/components`: file JavaScript e CSS specifici per i componenti core AEM
* `src/resources`: file statici come icone, loghi e font
* `src/site`: file JavaScript e CSS applicabili all’intera pagina AEM Sites
* `src/theme.ts`: il punto di ingresso principale del tema JavaScript &amp; CSS
* `src\theme.scss`: file JavaScript e CSS applicabili all’intero tema

Il `src/components` La cartella contiene file JavaScript e CSS specifici per tutti i componenti core AEM come pulsante, casella di controllo, contenitore, piè di pagina, ecc. Puoi assegnare uno stile al pulsante o alla casella di controllo modificando il file CSS specifico del componente AEM.

![Modificare il tema](/help/forms/assets/theme_structure.png)

Per personalizzare il tema, puoi avviare il server proxy locale per visualizzare le personalizzazioni del tema in tempo reale in base al contenuto effettivo dell’AEM.

### 3. Modifica il nome in package.json e package_lock.json del tema dell’area di lavoro {#changename-packagelock-packagelockjson}

Aggiornare il nome e la versione del tema Canvas nel `package.json` e `package_lock.json` file.

>[!NOTE]
>
> I nomi non devono avere `@aemforms` tag. Deve essere un testo semplice come nome fornito dall’utente.

![Immagine tema area di lavoro](/help/forms/assets/changename_canvastheme.png)

### 4. Creare il file .env in una cartella dei temi {#creating-env-file-theme-folder}

Creare un `.env` nella cartella theme e aggiungi i seguenti parametri:

* **URL AEM**
AEM_URL=https://[author-instance]

* **Nome del sito AEM**
AEM_ADAPTIVE_FORM=Nome_modulo

* **Porta proxy AEM**
AEM_PROXY_PORT=7000


![Struttura tema area di lavoro](/help/forms/assets/env-file-canvas-theme.png)

### 5. Avviare un server proxy locale {#starting-a-local-proxy-server}

1. Dalla riga di comando, passa alla root del tema nel computer locale.
1. Esegui `npm install` e npm recupera le dipendenze e installa il progetto.
1. Esegui `npm run live` e il server proxy viene avviato.

   ![npm run live](/help/forms/assets/theme_proxy.png)


1. Tocca o fai clic su **ACCESSO LOCALE (SOLO ATTIVITÀ AMMINISTRATORE)** e accedere con le credenziali utente proxy fornite dall&#39;amministratore AEM.

   ![Accesso locale](/help/forms/assets/local_signin.png)

   >[!NOTE]
   >
   > * Crea un utente locale per l&#39;accesso locale. Fornisci il ruolo di collaboratore per il designer del tema.
   > * Se specifichi l’URL AEM come `http://localhost:[port]/` nel `.env` file del tema Canvas, verrai reindirizzato direttamente al browser.


1. Una volta effettuato l’accesso, modifica l’URL nel browser in modo che indirizzi al percorso del contenuto di esempio fornito dall’amministratore AEM.

   * Ad esempio, se il percorso fornito è stato `/content/formname.html?wcmmode=disabled`, modifica l’URL in `http://localhost:[port]/content/forms/af/formname.html?wcmmode=disabled`

   ![Contenuto del campione proxy](/help/forms/assets/sample_af.png)

Passa a un modulo adattivo per vedere il tema Area di lavoro applicato a un modulo adattivo.

### 6. Personalizzare il tema {#customize-theme}

1. Nell’editor, apri il file `<your-theme-sources>/src/site/_variables.scss`.

   >[!NOTE]
   >
   > Puoi assegnare uno stile a tutti i componenti del modulo adattivo direttamente in un sito modificando il `site/_variables.scss` file.

1. Modifica la variabile per `font colour` a `red`.

   ![Modificare il tema](/help/forms/assets/edit_theme.png)

   **Personalizzare lo stile dei diversi componenti dell’AEM**

   Puoi assegnare uno stile ai diversi componenti di un modulo adattivo modificandone il file CSS nell’editor. Nella cartella Tema dell’area di lavoro sono presenti diverse cartelle CSS per ogni componente core Modulo adattivo.

   ![Componente core](/help/forms/assets/theme-component.png)

   Per specificare gli stili per un componente specifico nell’editor temi, puoi modificare il CSS in una cartella temi. Se ad esempio si desidera modificare il colore del bordo di un campo casella di testo, aprire il file CSS nell&#39;editor e modificarne il colore.

   ![Modifica CSS casella di testo](/help/forms/assets/edit_color_textbox.png)

1. Quando si salva il file, il server proxy riconosce la modifica tramite la riga `[Browsersync] File event [change]`.

   ![Browsersync proxy](/help/forms/assets/browser_sync.png)

1. Tornando al browser del server proxy locale, la modifica è immediatamente visibile.

   ![cambia tema AF](/help/forms/assets/edit_theme_af.png)

Il designer del tema visualizza in anteprima le modifiche nel server proxy locale e personalizza il tema in base ai requisiti per i diversi componenti AEM.

Prima di eseguire il commit delle modifiche nell’archivio Git dell’AEM, devi accedere al tuo [Informazioni sull’archivio Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git).

### 7. Eseguire il commit delle modifiche {#committing-the-changes}

Dopo aver apportato modifiche al tema e averlo testato con un server proxy locale, esegui il commit delle modifiche nell’archivio Git del Cloud Service AEM Forms. Rende il tema personalizzato disponibile nell’ambiente del Cloud Service Forms per l’utilizzo da parte di autori di Forms adattivi.

Prima di eseguire il commit delle modifiche nell’archivio Git del Cloud Service AEM Forms, è necessario clonare l’archivio nel computer locale. Per clonare l’archivio:

1. Creare un nuovo archivio temi facendo clic sul pulsante **[!UICONTROL Archivi]** opzione.

   ![crea nuovo archivio tema](/help/forms/assets/createrepo_canvastheme.png)

1. Clic **[!UICONTROL Aggiungi archivio]** e specificare **Nome archivio** nel **Aggiungi archivio** . Fai clic su **[!UICONTROL Salva]**.

   ![Aggiungi archivio tema Canvas](/help/forms/assets/addcanvasthemerepo.png)

1. Clic **[!UICONTROL Copia URL archivio]** per copiare l’URL dell’archivio creato.

   ![URL tema area di lavoro](/help/forms/assets/copyurl_canvastheme.png)

1. Apri il prompt dei comandi e clona l’archivio cloud creato in precedenza.

   ```
   git clone https://git.cloudmanager.adobe.com/aemforms/Canvasthemerepo/
   ```

1. Sposta i file dell’archivio dei temi che stai modificando nell’archivio cloud con un comando simile a
   `cp -r [source-theme-folder]/* [destination-cloud-repo]`
Ad esempio, utilizzare questo comando 
`cp -r [C:/cloned-git-canvas/*] [C:/cloned-repo]`
1. Nella directory dell’archivio cloud, esegui il commit dei file dei temi spostati in con i seguenti comandi.

   ```text
   git add .
   git commit -a -m "Adding theme files"
   git push
   ```

1. Le personalizzazioni vengono inviate all’archivio Git.

   ![Commit delle modifiche eseguito](/help/forms/assets/cmd_git_push.png)

Le personalizzazioni vengono ora memorizzate in modo sicuro nell’archivio Git.


### 8. Eseguire la pipeline front-end {#deploy-pipeline}

1. Crea la pipeline front-end per distribuire il tema personalizzato. Scopri [come impostare una pipeline front-line per distribuire il tema personalizzato](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#setup-pipeline).
1. Esegui la pipeline front-end creata per distribuire la cartella dei temi personalizzata nel **[!UICONTROL Stile]** di una procedura guidata per la creazione di moduli adattivi.

>[!NOTE]
>
>In futuro, se apporti modifiche alla cartella del tema Canvas, dovrai eseguire nuovamente la pipeline precedente. Pertanto, è necessario ricordare il nome della pipeline.

## Esempio per personalizzare il tema {#example-to-customize-a-theme}

1. Accedi all’istanza Autore di AEM Forms.
1. Apri un modulo adattivo creato utilizzando i componenti core.
1. Avviare il server proxy locale utilizzando il prompt dei comandi e fare clic su **ACCESSO LOCALE (SOLO ATTIVITÀ AMMINISTRATORE)**.
1. Una volta effettuato l’accesso, vieni reindirizzato al browser e visualizzi il tema applicato.
1. Scarica il file [Tema area di lavoro](https://github.com/adobe/aem-forms-theme-canvas) ed estrarre la cartella zip scaricata.
1. Apri la cartella zip estratta nell’editor preferito.
1. Creare un `.env` nella cartella dei temi e aggiungi i parametri: **URL AEM**, **MODULO_ADATTIVO_AEM** e **PORTA_PROXY_AEM**.
1. Apri il file CSS della casella di testo nella cartella del tema dell’area di lavoro e modifica il colore del bordo in &quot;Pronuncia&quot; `red` e salva le modifiche.
1. Riapri il browser e osserva che le modifiche si riflettono immediatamente in un modulo adattivo.
1. Sposta la cartella del tema dell’area di lavoro nell’archivio clonato.
1. Apporta le modifiche ed esegue la pipeline front-end.

Una volta eseguita la pipeline, il tema è disponibile nella scheda Stile.

## Best practice {#best-practices}

* **Evitare risorse da un altro tema**

   Quando modifichi un tema, puoi sfogliare e aggiungere risorse (come immagini) da altri temi. Ad esempio, stai modificando lo sfondo di una pagina. Ad esempio, quando selezioni **[!UICONTROL Pagina]** ![edit-button](assets/edit-button.png)> **[!UICONTROL Sfondo]** > **[!UICONTROL Aggiungi]** > **[!UICONTROL Immagine]**, viene visualizzata una finestra di dialogo che consente di sfogliare e aggiungere immagini in un altro tema.

   Se una risorsa viene aggiunta da un altro tema e l’altro tema viene spostato o eliminato, puoi riscontrare dei problemi con il tema corrente. Si consiglia di evitare di sfogliare e aggiungere risorse da altri temi.

* **Modifica della larghezza del layout del pannello contenitore**

   La modifica della larghezza del layout del pannello contenitore non è consigliata. Quando si specifica la larghezza di un pannello contenitore, questo diventa statico e non si adatta a visualizzazioni diverse.

* **Utilizzo dell’editor di moduli o dell’editor temi per l’utilizzo di intestazione e piè di pagina**

   Utilizzare l&#39;editor tema se si desidera applicare uno stile a intestazione e piè di pagina utilizzando opzioni di stile quali stile, sfondo e trasparenza del carattere.
Se si desidera fornire informazioni quali un&#39;immagine del logo, il nome della società nell&#39;intestazione e le informazioni sul copyright nel piè di pagina, utilizzare le opzioni dell&#39;editor di moduli.
