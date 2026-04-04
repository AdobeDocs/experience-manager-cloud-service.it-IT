---
title: Personalizzazione dei temi dei moduli adattivi tramite l’Editor tema
description: Scopri come utilizzare l’Editor temi per creare e personalizzare temi visivi per Forms adattivo basato su componenti core in Adobe Experience Manager.
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: 4a541c11-38e9-4dbc-8464-38be6b1ee94d
source-git-commit: fa8035f826a4d08c18bc0d2b7664015c6fc82698
workflow-type: tm+mt
source-wordcount: '1951'
ht-degree: 1%

---

# Personalizzazione dei temi dei moduli {#customizing-form-themes}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/themes.html?lang=it) |
| AEM as a Cloud Service | Questo articolo |

L’Editor temi in Adobe Experience Manager (AEM) Forms è un’interfaccia visiva che consente di creare e personalizzare i temi per il Forms adattivo senza scrivere il codice manualmente. Un tema definisce l&#39;aspetto dei componenti e dei pannelli del modulo, inclusi i colori di sfondo, gli stili dei caratteri, i bordi, le dimensioni e la spaziatura. Quando applichi un tema, gli stili specificati si riflettono sui componenti corrispondenti e puoi riutilizzare lo stesso tema in più Forms adattivi.

L’Editor tema elimina la necessità di un utente sviluppatore dedicato per lo stile di base dei moduli. Con una conoscenza pratica del CSS, puoi applicare stili ai moduli utilizzando la barra laterale visiva o scrivere sostituzioni CSS avanzate direttamente all’interno dell’editor.

## Prerequisiti {#prerequisites}

* Autori in Adobe Experience Manager Forms.
* Comprensione di base dei principi di stile CSS. Per un riferimento CSS completo, vedere il riferimento CSS [Documenti Web MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference).

## Passare alla directory dei temi {#navigate-to-themes}

1. Accedi all’istanza Autore di AEM.
1. Passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Temi]**.

   Nella directory Temi vengono visualizzati tutti i temi disponibili, inclusi quelli standard forniti da AEM Canvas, insieme ai temi personalizzati creati dall&#39;utente o dall&#39;organizzazione.

### Crea un nuovo tema {#create-a-new-theme}

1. Nella directory Temi selezionare la cartella in cui si desidera memorizzare il nuovo tema.
1. Fai clic su **[!UICONTROL Crea]** > **[!UICONTROL Tema]**.

   ![Crea nuovo tema](/help/forms/assets/custom-theme-create.png)

1. Nella finestra di dialogo **[!UICONTROL Crea tema]**, specifica i dettagli seguenti:
   * **[!UICONTROL Titolo]**: titolo descrittivo del tema.
   * **[!UICONTROL Nome]**: nome del nodo per il tema.
   * **[!UICONTROL Modulo adattivo per visualizzare in anteprima il tema]**: per un tema Componente core, seleziona un modulo adattivo basato su Componente core. **[!UICONTROL Utilizza modulo adattivo predefinito]** utilizza un modulo adattivo di base, non componenti core. Il modulo selezionato viene visualizzato nell’area di lavoro dell’Editor temi per l’anteprima in tempo reale durante la modifica.
   * **[!UICONTROL Descrizione]** *(facoltativo)*: breve descrizione del tema.
   * **[!UICONTROL Contenitore configurazione]** *(Facoltativo)*: Contenitore configurazione che contiene i dettagli della configurazione dei caratteri di Adobe.
   * **[!UICONTROL Tag]** *(Facoltativo)*: Tag associati al tema per l&#39;identificazione e la ricerca.
1. Fai clic su **[!UICONTROL Crea]**.

   ![configurazione tema personalizzato](/help/forms/assets/custom-theme-name.png)

   Il tema viene creato. Ora puoi fare clic su **[!UICONTROL Modifica]** per aprirlo nell&#39;Editor temi.

### Modifica un tema esistente {#edit-an-existing-theme}

1. Nella directory **Temi** selezionare il tema che si desidera modificare.
1. Fai clic su **[!UICONTROL Modifica]** nella barra delle azioni per aprire il tema nell&#39;Editor temi.

   ![Modifica di un tema](/help/forms/assets/custom-theme-edit.png)

### Carica un tema {#upload-a-theme}

Puoi importare un pacchetto di temi (ad esempio, uno esportato da un altro ambiente) nella directory Themes:

1. Nella directory **Themes**, fai clic su **[!UICONTROL Create]** > **[!UICONTROL File Upload]**.
1. Cerca di selezionare il pacchetto tema (file ZIP) sul tuo computer, quindi fai clic su **[!UICONTROL Carica]**.

   ![Carica tema - Crea menu con opzione Carica file](/help/forms/assets/custom-theme-upload.png)

Il tema caricato viene visualizzato nella directory Temi e può essere modificato come qualsiasi altro tema.

### Scaricare un tema {#download-a-theme}

Puoi esportare un tema come pacchetto (file ZIP) per riutilizzarlo in un altro ambiente AEM Forms o per eseguirne il backup:

1. Nella directory **Temi**, selezionare uno o più temi (utilizzare le caselle di controllo sulle schede dei temi).
1. Fai clic su **[!UICONTROL Scarica]** nella barra delle azioni. Può essere visualizzata una finestra di dialogo con i dettagli dei temi selezionati.
1. Conferma o fai clic su **[!UICONTROL Scarica]** nella finestra di dialogo. Il pacchetto del tema viene scaricato nel computer come file ZIP.

   ![Scarica tema - seleziona il tema e fai clic su Scarica](/help/forms/assets/custom-theme-download.png)

Puoi caricare questo file ZIP in un secondo momento utilizzando [Carica un tema](#upload-a-theme) nello stesso ambiente o in un altro.

## Interfaccia dell’Editor tema {#understand-the-theme-editor}

Quando apri un tema nell’Editor tema, vengono visualizzate due aree principali:

![Editor temi](/help/forms/assets/custom-theme-editor.png)

* **Area di lavoro** (lato destro): visualizza un&#39;anteprima del modulo adattivo collegato al tema. Tutte le modifiche di stile si riflettono qui immediatamente, in modo da poter vedere l’impatto delle modifiche in tempo reale.
* **Barra laterale** (lato sinistro): contiene il pannello **Selettori** in cui sono elencati tutti i componenti di un modulo con stile in una struttura ad albero, ad esempio Pagina, Modulo, Campo, Pulsante, Pannello, Immagine, hCaptcha e reCaptcha.

### Barra degli strumenti Area di lavoro {#canvas-toolbar}

![Barra degli strumenti dell&#39;area di lavoro dell&#39;Editor temi con opzioni Attiva/Disattiva pannello laterale, Annulla, Ripeti, Emulatore, Modifica/Anteprima e Tema](/help/forms/assets/custom-theme-toolbar-utilities.png)

Da sinistra a destra, la barra degli strumenti fornisce:
* **A: attiva/disattiva pannello laterale**: mostra/nascondi la barra laterale dei selettori. Utilizza questa opzione per ingrandire l’area di anteprima del modulo quando vuoi evidenziare l’area di lavoro, oppure per mostrare nuovamente la barra laterale quando devi selezionare o assegnare uno stile ai componenti.
* **B: Opzioni tema** (elenco a discesa): apre un menu con quattro opzioni. Fai clic su di esso quando hai bisogno di modificare il modulo di anteprima, visualizzare CSS, gestire gli stili salvati o ricevere aiuto nell’editor. Quando apri il menu a discesa Opzioni tema, puoi vedere:

  ![Il menu a discesa Opzioni tema mostra Configura, Visualizza CSS tema, Gestisci stili e Guida](/help/forms/assets/custom-theme-configure.png)

   * **[!UICONTROL Configura]**: cambia il modulo visualizzato nell&#39;area di lavoro in un modulo adattivo diverso. Usa questa opzione per controllare l’aspetto del tema in un altro modulo senza uscire dall’editor.
     ![Configura modulo adattivo per anteprima tema](/help/forms/assets/custom-theme-switch-af.png)
   * **[!UICONTROL Visualizza CSS tema]**: aprire una finestra di dialogo con il CSS compilato completo per il tema. Per visualizzare CSS solo per il componente attualmente selezionato, utilizza invece **[!UICONTROL Visualizza CSS]** nella barra laterale (utile per il debug o la copia delle regole).
     ![Visualizza CSS finale](/help/forms/assets/custom-theme-view-css.png)
   * **[!UICONTROL Gestisci stili]**: apri la finestra di dialogo per salvare, denominare e riutilizzare gli stili di testo e immagine. Gli stili salvati possono essere applicati ad altri componenti; gli stili utilizzati di recente possono anche essere visualizzati per un riutilizzo rapido.
   * **[!UICONTROL Guida]**: avvia la presentazione guidata da immagini dell&#39;Editor temi.
* **C: Annulla / Ripristina**: ripristina o riapplica le ultime modifiche di stile. Utile se si tenta di applicare uno stile e si desidera tornare indietro senza perdere altre modifiche.
* **D: emulatore**: selezionare un dispositivo o un punto di interruzione (ad esempio Desktop, Tablet o Mobile) per visualizzare in anteprima il modulo con le dimensioni dello schermo specificate. L’anteprima del modulo viene ridimensionata in modo da corrispondere al punto di interruzione selezionato. Tutti gli stili impostati durante l&#39;impostazione di un punto di interruzione vengono applicati solo a tale punto, in modo da poter definire stili reattivi. Per ulteriori dettagli, vedere [Stile per schermi di dimensioni diverse](#styling-for-different-screen-sizes).
* **E: Modifica / Anteprima**: passaggio tra due modalità. **Modifica** è l&#39;impostazione predefinita: è possibile fare clic sui componenti nell&#39;area di lavoro per selezionarli e modificarne lo stile nella barra laterale. **Anteprima** mostra il modulo come un utente finale lo vedrebbe senza i bordi di selezione, le etichette dei componenti o la barra laterale dello stile, in modo da poter controllare l&#39;aspetto e il comportamento del modulo a tema prima di pubblicarlo.

<!--
**3. Bottom of the sidebar: Simulate Error and Simulate Success**

When you style components by state (for example, Error or Success), you can preview that look without submitting the form. In AEM Forms as a Cloud Service, **Simulate Error** and **Simulate Success** are available at the **bottom of the left sidebar**. Scroll down in the sidebar if you don’t see them; they appear when you have a component selected and let you toggle the preview to match the Error or Success state.

* **Simulate Error**: Show the form as if a field failed validation, so you can see your **[!UICONTROL Error]** state styling.
* **Simulate Success**: Show the form as if validation passed, so you can see your **[!UICONTROL Success]** state styling.

Toggle these on or off as you adjust styles for each state. For more on styling by state, see [Style by component state](#style-by-state).
-->

### Personalizzare lo stile di un componente

È possibile selezionare un componente a cui applicare uno stile in due modi:
* **Dall&#39;area di lavoro**: fare clic direttamente su un componente nel modulo, ad esempio un campo di testo, un pulsante o un elenco a discesa. L’elemento selezionato viene evidenziato con un bordo e sopra di esso viene visualizzata un’etichetta del componente (ad esempio, &quot;Widget di input testo&quot;). Le opzioni di stile per tale componente vengono visualizzate nella barra laterale.

  ![Modifica tema da area di lavoro](/help/forms/assets/custom-theme-field-level.png)

* **Dal pannello Selettori**: utilizza la struttura ad albero nella barra laterale a sinistra per eseguire il drill-down di componenti specifici. Espandere ad esempio **[!UICONTROL Campo]** > **[!UICONTROL Widget]** > **[!UICONTROL Input di testo]** per impostare il widget della casella di testo in modo specifico.

  ![Modifica tema dal pannello Selettore](/help/forms/assets/custom-theme-selector.png)

#### Applicare stili a un componente {#apply-styles-to-a-component}

Una volta selezionato un componente, la barra laterale mostra le proprietà di stile disponibili organizzate nelle seguenti categorie:

* **[!UICONTROL Dimensioni e posizione]**: controllo dell&#39;allineamento, delle dimensioni, della spaziatura, del margine, della larghezza, dell&#39;altezza e dell&#39;indice Z.
* **[!UICONTROL Testo]**: configurare famiglia di caratteri, peso, colore, dimensione, altezza delle linee, allineamento, spaziatura tra lettere, decorazione del testo e trasformazione. Per un elenco completo delle proprietà di testo CSS supportate, consulta la [documentazione di testo CSS MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_text).
* **[!UICONTROL Sfondo]**: impostare un colore di sfondo, un&#39;immagine o una sfumatura. Consulta la [documentazione sugli sfondi CSS MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_backgrounds_and_borders).
* **[!UICONTROL Bordo]**: definire la larghezza, lo stile, il raggio e il colore del bordo.
* **[!UICONTROL Effetti]**: aggiungere opacità, metodi di fusione e ombre.

Per applicare uno stile:

1. Seleziona il componente dall’area di lavoro o dal pannello Selettori.
1. Imposta le proprietà visive desiderate nella barra laterale. Ad esempio, scegli un **[!UICONTROL Colore di sfondo]** e regola il **[!UICONTROL Colore carattere]**.
1. Fai clic sull&#39;icona del segno di spunta **[!UICONTROL OK]** per confermare la modifica della proprietà.

   ![Applicazione dello stile](/help/forms/assets/custom-theme-applying-style.png)

<!--
#### Style by component state {#style-by-state}

Components can have different visual states (for example, default, focus, hover, disabled, error, success). You can style each state separately so the form looks correct during user interaction and validation.

1. Select the component from the canvas or the Selectors panel.
1. In the sidebar, use the **[!UICONTROL State]** dropdown to choose the state you want to style (for example, **[!UICONTROL Default]**, **[!UICONTROL Focus]**, **[!UICONTROL Hover]**, **[!UICONTROL Disabled]**, **[!UICONTROL Error]**, or **[!UICONTROL Success]**).
1. Set the styling properties (Background, Border, Text, and so on) for that state.
1. Click **[!UICONTROL OK]** to confirm.

   ![State dropdown in sidebar for styling Default, Focus, Error, Success, and other states](/help/forms/assets/custom-theme-state-dropdown.png)

The styles you define apply only when the component is in the selected state. For example, if you set a red border and red background for the **[!UICONTROL Error]** state, the field shows that styling when validation fails. If your environment supports it, use **Simulate Error** or **Simulate Success** at the bottom of the sidebar to preview how the component looks in those states without submitting the form.
-->

### Stile a livello di modulo {#form-level-styling}

Lo stile a livello di modulo viene applicato a tutti i componenti dello stesso tipo. Ad esempio, se selezioni **[!UICONTROL Campo]** nel pannello **Selettori** e imposti un colore di sfondo su blu, ogni campo del modulo (caselle di testo, caselle numeriche, selettori data e menu a discesa) eredita tale sfondo blu.

**Esempio:** Per impostare un colore di sfondo uniforme per tutti i campi del modulo:

1. Nel pannello **Selettori**, seleziona **[!UICONTROL Campo]**.
1. Nella barra laterale, impostare **[!UICONTROL Colore sfondo]** su blu.
1. Fai clic su **[!UICONTROL OK]**.

   ![Stile livello modulo](/help/forms/assets/custom-theme-form-level-styling.png)

Tutti i componenti campo nel modulo ora presentano uno sfondo blu.

### Stile a livello di componente {#component-level-styling}

Lo stile a livello di componente è destinato a un tipo di componente specifico, ignorando qualsiasi stile più ampio a livello di modulo. Se ad esempio si desidera che solo il widget Casella di testo abbia un colore di sfondo diverso mentre tutti gli altri campi rimangono blu, il widget Casella di testo verrà impostato in modo specifico.

**Esempio:** Per impostare uno sfondo verde e un carattere viola solo sul widget casella di testo:

1. Nel pannello Selettori, espandi **[!UICONTROL Campo]** > **[!UICONTROL Widget]** > **[!UICONTROL Input di testo]**.
1. Impostare **[!UICONTROL Colore carattere]** su viola.
   ![Stile livello campo](/help/forms/assets/custom-theme-field-level-styling1.png)
1. Impostare **[!UICONTROL Colore sfondo]** su verde.
   ![Stile livello campo](/help/forms/assets/custom-theme-field-level-styling2.png)
1. Fai clic su **[!UICONTROL OK]**.

Il widget Casella di testo ora visualizza uno sfondo verde con testo viola, mentre tutti gli altri campi rimangono blu a partire dallo stile del modulo.

>[!NOTE]
>
> **Lo stile a livello di componente ha sempre la priorità sullo stile a livello di modulo.** Quando uno stile è definito a entrambi i livelli, il selettore a livello di componente più specifico sostituisce il selettore a livello di modulo più ampio. Segue le [regole di specificità CSS standard](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity). Ad esempio, se impostate uno sfondo blu su tutti i campi (a livello di modulo) e uno sfondo verde sul widget casella di testo (a livello di componente), la casella di testo visualizza uno sfondo verde.

## Stile per schermi di dimensioni diverse {#styling-for-different-screen-sizes}

Puoi definire stili diversi per dispositivi di dimensioni diverse, in modo che il tema sia reattivo. La barra degli strumenti dell&#39;Editor temi mostra **opzioni dispositivo** (ad esempio, iPhone 5, iPad, Desktop, Tablet, Schermo più piccolo) per visualizzare in anteprima e formattare il modulo con quella dimensione di schermo.

1. Nella barra degli strumenti dell&#39;area di lavoro utilizzare l&#39;**emulatore di dispositivi**: fare clic su una delle etichette dei dispositivi, ad esempio **[!UICONTROL Desktop]**, **[!UICONTROL Tablet]**, **[!UICONTROL iPad]**, **[!UICONTROL Schermo più piccolo]**. Un righello sopra il modulo mostra la larghezza in pixel del dispositivo selezionato.
1. Con il dispositivo selezionato, utilizza la barra laterale per impostare o regolare gli stili. Gli stili sono validi solo per la visualizzazione del dispositivo selezionata.
1. Passa a un altro dispositivo e definisci gli stili necessari.
1. Fare clic su **[!UICONTROL OK]** e salvare il tema al termine.

   ![Emulatore di dispositivo nell&#39;Editor temi - opzioni righello e dispositivo (desktop, tablet, iPad, schermo più piccolo)](/help/forms/assets/custom-theme-emulator.png)

Lo stesso tema può quindi avere spaziatura, dimensioni dei caratteri o stili correlati al layout diversi per dispositivo, in base al comportamento dell&#39;[Editor tema di AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/themes.html?lang=it) per lo stile reattivo.

## Utilizzare sostituzioni CSS avanzate {#use-advanced-css-overrides}

Per gli stili che non sono disponibili tramite la barra laterale visiva, puoi scrivere CSS personalizzati direttamente nell’editor.

1. Seleziona il componente.
1. Nella barra laterale, espandi la sezione **[!UICONTROL Advanced]**.
1. Scrivi le regole CSS personalizzate nell&#39;area **[!UICONTROL Sovrascrittura CSS]**. In caso di conflitto, queste regole sostituiscono tutte le proprietà impostate tramite i controlli visivi.

Per un riferimento completo alle proprietà CSS, vedi il riferimento CSS [Documenti Web MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference).

### Aggiungere pseudo elementi CSS {#add-css-pseudo-elements}

La sezione **[!UICONTROL Advanced]** supporta anche pseudo-elementi CSS come `::before` e `::after`. Consentono di inserire contenuto o stili decorativi intorno a un componente senza modificare la struttura del modulo. Ad esempio, per aggiungere un indicatore visivo prima di un componente Casella di testo:

1. Selezionare il componente, ad esempio `CMP Textbox`.
1. Espandi la sezione **[!UICONTROL Advanced]**.
1. Nei campi di pseudo-elemento `::before`, aggiungi proprietà CSS come:

   ```css
   color: #B10DC9;
   ```

   ![Prima di CSS](/help/forms/assets/custom-theme-before-css.png)

1. Nei campi di pseudo-elemento `::after`, aggiungi proprietà CSS come:

   ```css
   color: #006400;
   ```

   ![Dopo CSS](/help/forms/assets/custom-theme-after-css.png)


Questi pseudo-elementi seguono il comportamento CSS standard. Per un riferimento completo, vedi [Pseudo-elementi CSS MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements).

## Best practice {#best-practices}

* **Utilizzare il pannello Selettori per un targeting preciso**: quando si applicano gli stili agli elementi nidificati, ad esempio un&#39;etichetta di campo o una descrizione lunga, utilizzare il pannello Selettori a sinistra anziché fare clic sull&#39;area di lavoro. In questo modo il selettore CSS corretto viene generato con la specificità corretta.
* **Evita risorse da altri temi**: quando modifichi un tema, non sfogliare e non aggiungere risorse (come immagini) da altri temi. Se il tema di origine viene spostato o eliminato, il tema corrente si interrompe.
* **Non modificare la larghezza del layout del pannello del contenitore**: specificando una larghezza fissa nei pannelli del contenitore, questi diventano statici e non possono essere adattati a schermi di dimensioni diverse.

## Consulta anche {#see-also}

{{see-also}}
