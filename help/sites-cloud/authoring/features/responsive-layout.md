---
title: Layout reattivo
description: AEM consente di realizzare un layout reattivo per le pagine
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Layout reattivo {#responsive-layout}

AEM consente di creare un layout reattivo per le pagine mediante il componente **Contenitore di layout**.

Questo fornisce un sistema paragrafo che consente di posizionare i componenti all’interno di una griglia reattiva. Con questa griglia è possibile riorganizzare il layout in base alla dimensione e al formato del dispositivo o della finestra. The component is used in conjunction with the [**Layout **mode](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes), which allows you to create and edit your responsive layout dependent on device.

Il Contenitore di layout:

* Fornisce ancoraggio orizzontale sulla griglia, unitamente alla possibilità di posizionare componenti affiancati sulla griglia e definire quando dovrebbero venire compressi/ridisposti.
* Utilizza punti di interruzione predefiniti (ad es. per smartphone, tablet ecc.) per definire il comportamento del contenuto per i relativi dispositivi e orientamenti.
   * Ad esempio, puoi personalizzare le dimensioni del componente o specificare se il componente può essere visualizzato su dispositivi specifici.
* Può essere nidificato per abilitare il controllo delle colonne.

L’utente può quindi visualizzare quale sarà l’aspetto dei contenuti per dispositivi specifici utilizzando l’emulatore.

AEM consente di realizzare il layout reattivo per le pagine utilizzando una combinazione di meccanismi:

* [**Componente Contenitore **](#adding-a-layout-container-and-its-content-edit-mode)layout

   Questo componente è disponibile nel browser [dei](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) componenti e fornisce un sistema paragrafo a griglia che consente di aggiungere e posizionare i componenti all’interno di una griglia reattiva. Può essere impostato anche come sistema paragrafo predefinito sulla pagina.

* [**Modalità Layout **](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)

   Once the layout container is positioned on your page you can use the **Layout** mode to position content within the responsive grid.

* [**Emulatore **](#selecting-a-device-to-emulate)Consente di creare e modificare siti web reattivi il cui layout si riorganizza in base alle dimensioni del dispositivo/finestra, ridimensionando i componenti in modo interattivo. L’utente può quindi visualizzare quale sarà l’aspetto dei contenuti utilizzando l’emulatore.

Con questi meccanismi basati su una griglia reattiva è possibile:

* Utilizzare i punti di interruzione per definire il layout di contenuti diversi in base alla larghezza del dispositivo (in relazione al tipo di dispositivo e all’orientamento).
* Utilizzare questi stessi punti di interruzione e layout di contenuti per assicurare che il contenuto sia reattivo rispetto alle dimensioni della finestra del browser sul desktop.
* Utilizzare l’ancoraggio orizzontale sulla griglia per posizionare i componenti sulla griglia, ridimensionarli, definire quando dovrebbero venire compressi o ridisposti in modo da essere affiancati o sovrapposti.
* Nascondere componenti per layout di dispositivo specifici.
* Gestire il controllo delle colonne.

A seconda del progetto, il Contenitore di layout potrebbe essere utilizzato come sistema paragrafo predefinito per le pagine o come componente disponibile per essere aggiunto alla pagina tramite il Browser componenti (o entrambi).

>[!TIP]
>
>Adobe provides [GitHub documentation](https://adobe-marketing-cloud.github.io/aem-responsivegrid/) of the responsive layout as a reference that can be given to front-end developers allowing them to use the AEM grid outside of AEM, for example when creating static HTML mock-ups for a future AEM site.

>[!NOTE]
>
>L’uso dei meccanismi di cui sopra è abilitato mediante la configurazione del modello. See Configuring Responsive Layout for further information. <!-- Use of the above mechanisms is enabled by configuration on the template. See [Configuring Responsive Layout](/help/sites-administering/configuring-responsive-layout.md) for further information.-->

## Definizioni di layout, emulazione del dispositivo e punti di interruzione {#layout-definitions-device-emulation-and-breakpoints}

Quando si crea il contenuto del sito web è importante assicurarsi che venga visualizzato in modo adatto al dispositivo utilizzato.

AEM consente di definire layout dipendenti dalla larghezza del dispositivo:

* L’emulatore consente di emulare i layout su una gamma di dispositivi. In addition to the device type, the orientation, selected by the **Rotate device** option, can impact the breakpoint selected as the width changes.
* I punti di interruzione sono i punti che separano le definizioni di layout.
   * Essi definiscono a tutti gli effetti la larghezza massima (in pixel) di qualsiasi dispositivo che utilizza un layout specifico.
   * I punti di interruzione sono normalmente applicabili a una gamma di dispositivi, in base alla larghezza del relativo schermo.
   * La portata di un punto di interruzione si estende a sinistra fino al punto di interruzione successivo.
   * Non è possibile selezionare specificatamente un punto di interruzione: la selezione di un dispositivo e di un orientamento comporterà la selezione automatica del punto di interruzione adeguato.

Il dispositivo **Desktop** è privo di una larghezza specifica e fa riferimento al punto di interruzione predefinito (ovvero tutto quanto si trova oltre l’ultimo punto di interruzione configurato).

>[!NOTE]
>
>È teoricamente possibile definire punti di interruzione per ogni singolo dispositivo, ma questo rende decisamente più macchinose la definizione e la manutenzione dei layout.

Quando utilizzi l’emulatore e selezioni un dispositivo specifico per l’emulazione, la definizione del layout e il relativo punto di interruzione vengono evidenziati. Eventuali modifiche apportate al layout verranno riconosciute per altri dispositivi su cui si applica il punto di interruzione, ovvero qualsiasi dispositivo disponibile a sinistra del marcatore del punto di interruzione attivo, ma prima del marcatore del punto di interruzione successivo.

Ad esempio, se selezioni il dispositivo **iPhone 6 Plus** (con una larghezza di 540 pixel) per l’emulazione e il layout, verrà attivato anche il punto di interruzione **Telefono** (definito con 768 pixel). Tutte le modifiche di layout apportate per **iPhone 6** diverranno applicabili per altri dispositivi nel punto di interruzione **Telefoni**, come **iPhone 5** (definito con 320 pixel).

![Emulatori](/help/sites-cloud/authoring/assets/responsive-layout-emulators.png)

## Selecting a Device to Emulate {#selecting-a-device-to-emulate}

1. Apri la pagina desiderata per la modifica. Ad esempio:

   `http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

1. Seleziona l’icona **Emulatore** sulla barra degli strumenti in alto:

   ![Pulsante emulatore](/help/sites-cloud/authoring/assets/emulator.png)

1. Viene aperta la barra degli strumenti emulatore.

   ![Barra degli strumenti emulatore](/help/sites-cloud/authoring/assets/responsive-layout-emulator-toolbar.png)

   La barra degli strumenti emulatore mostra le seguenti opzioni di layout aggiuntive:

   * **Ruota dispositivo** - Consente di ruotare un dispositivo dall&#39;orientamento verticale all&#39;orientamento orizzontale e viceversa.
   ![Pulsante Ruota orizzontale del dispositivo](/help/sites-cloud/authoring/assets/responsive-layout-rotate-device-landscape-button.png)
   ![Pulsante Ruota dispositivo in verticale](/help/sites-cloud/authoring/assets/responsive-layout-rotate-device-portrait-button.png)

   * **Seleziona il dispositivo**: consente di definire un dispositivo specifico da emulare da un elenco (ved. il passaggio successivo).
   ![Seleziona il pulsante Dispositivo](/help/sites-cloud/authoring/assets/responsive-layout-select-device-button.png)

1. Per selezionare un dispositivo specifico da emulare è possibile:

   * Utilizzare l’icona Seleziona il dispositivo e scegliere il dispositivo dal selettore a discesa.
   * Toccare o fare clic sull’indicatore del dispositivo nella barra degli strumenti dell’emulatore.
   ![Seleziona dispositivo, menu a discesa](/help/sites-cloud/authoring/assets/responsive-layout-select-device-dropdown.png)

1. Una volta che un dispositivo specifico è stato selezionato è possibile:

   * See the active marker for the selected device, such as **iPad.**
   * See the active marker for the appropriate [breakpoint](#layout-definitions-device-emulation-and-breakpoints) such as **Tablet.**
   * The blue dotted line represents the *fold* for the selected device (here an **iPhone 6 Plus** in landscape).
   ![La piega](/help/sites-cloud/authoring/assets/responsive-layout-fold.png)

   * La piega può essere anche considerata l’interruzione di riga della pagina (da non confondere con i [punti di interruzione](#layout-definitions-device-emulation-and-breakpoints)) per il contenuto. Questa è visualizzata per comodità, per mostrare quale parte del contenuto è visibile all’utente sul dispositivo prima di scorrere in basso.
   * La riga della piega non viene visualizzata se l’altezza del dispositivo emulato è superiore alle dimensioni dello schermo.
   * La piega è indicata per comodità dell’autore e non viene visualizzata nella pagina pubblicata.


## Adding a Layout Container and its Content (Edit mode) {#adding-a-layout-container-and-its-content-edit-mode}

Un **Contenitore di layout** è un sistema paragrafo che:

* Include altri componenti.
* Definisce il layout.
* Risponde alle modifiche.

>[!NOTE]
>
>Se non è già disponibile, il Contenitore **di** layout deve essere attivato esplicitamente per un sistema paragrafo/pagina. <!-- If not already available, the **Layout Container** must be explicitly [activated for a paragraph system/page](/help/sites-administering/configuring-responsive-layout.md).-->

1. Il **Contenitore di layout** è disponibile come componente standard nel [browser Componenti](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser). Da qui puoi trascinarlo nella posizione desiderata sulla pagina; verrà quindi visualizzato il segnaposto **Trascina qui i componenti**.
1. È quindi possibile aggiungere componenti al Contenitore di layout. Questi componenti includeranno il contenuto vero e proprio:

   ![Contenitore di layout](/help/sites-cloud/authoring/assets/responsive-layout-add-to-layout-container.png)

## Selezione e intervento su un Contenitore di layout (modalità di modifica) {#selecting-and-taking-action-on-a-layout-container-edit-mode}

Come con altri componenti, puoi selezionare e quindi intervenire (opzioni Copia, Taglia, Elimina) su un Contenitore di layout (in modalità di **modifica**):

>[!CAUTION]
>
>Dato che un Contenitore di layout è un sistema paragrafo, la sua eliminazione comporta l’eliminazione della griglia di layout e di tutti i componenti (e relativo contenuto) inclusi all’interno del contenitore.

1. Se passi il cursore del mouse o tocchi il segnaposto di una griglia, viene visualizzato il menu delle azioni.

   ![Aggiungi al Contenitore di layout](/help/sites-cloud/authoring/assets/responsive-layout-container.png)

   You need to select the **Parent** option.

   ![Pulsante Parent](/help/sites-cloud/authoring/assets/responsive-layout-parent-button.png)

1. Se il componente del layout è nidificato, seleziona l’opzione **Elemento padre** per avere una selezione a discesa, che consente di selezionare il contenitore nidificato del layout o il relativo elemento padre.

   Quando passi il cursore del mouse sui nomi dei contenitori nel menu a discesa, sulla pagina vengono visualizzati i relativi contorni.

   * Il contenitore di layout nidificato più basso sarà evidenziato in blu.
   * Ogni contenitore successivo sarà in una tonalità più chiara di blu.
   ![Contenitori nidificati](/help/sites-cloud/authoring/assets/responsive-layout-nested.png)

1. In questo modo viene messa evidenziata l’intera griglia con il relativo contenuto. The action toolbar will be shown, from where you can select an action such as **Delete.**

## Defining Layouts (Layout mode) {#defining-layouts-layout-mode}

>[!NOTE]
>
>È possibile definire un layout distinto per ogni [punto di interruzione](#layout-definitions-device-emulation-and-breakpoints) (come determinato dal tipo di dispositivo e dall’orientamento emulati).

To configure the layout of a responsive grid implemented with the Layout Container you need to use the **Layout** mode.

La modalità **Layout** può essere avviata in due modi.

* By using the [mode menu in the toolbar](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) and choosing **Layout** mode
   * Select the **Layout** mode just as you would switch to **Edit** mode or **Targeting** mode.
   * **La modalità Layout** rimane persistente e non si esce dalla modalità **Layout** finché non si seleziona un’altra modalità tramite il selettore della modalità.
* Quando [si modifica un singolo componente.](/help/sites-cloud/authoring/fundamentals/editing-content.md#edit-component-layout)
   * Utilizzando l’opzione **Layout** nel menu Azioni rapide del componente è possibile passare alla modalità **Layout**.
   * La modalità **Layout** persiste quando si modifica il componente e torna alla modalità **Modifica** quando è attivo un altro componente.

In modalità Layout puoi eseguire diverse azioni su una griglia:

* Ridimensionare i componenti di contenuto utilizzando i punti blu. Il ridimensionamento sarà sempre con ancoraggio sulla griglia. Quando si esegue un’operazione di ridimensionamento, verrà visualizzata la griglia di sfondo per facilitare l’allineamento:

   ![Ridimensionare i componenti](/help/sites-cloud/authoring/assets/responsive-layout-resizing.png)

   >[!NOTE]
   >
   >Proporzioni e rapporti relativi saranno mantenuti al ridimensionamento di componenti come le **immagini**.

* Facendo clic/toccando un componente di contenuti la barra degli strumenti consente di:
   * **Elemento padre** - Consente di selezionare l&#39;intero componente Contenitore di layout per intervenire sull&#39;intero componente.
   * **Mobile in nuova riga** : il componente viene spostato su una nuova riga, a seconda dello spazio disponibile all’interno della griglia.
   * **Nascondi componente** : il componente viene reso invisibile (può essere ripristinato dalla barra degli strumenti del Contenitore di layout).
   ![Nascondi componente](/help/sites-cloud/authoring/assets/responsive-layout-hide.png)

* In **Layout** mode you can tap/click on the **Drag components here** to select the entire component. Viene quindi visualizzata la barra degli strumenti per questa modalità.

   La barra degli strumenti presenta opzioni diverse a seconda dello stato del componente del layout e dei componenti che ne fanno parte. Esempio:

   * **Elemento padre** - Seleziona il componente principale.

      ![Pulsante Parent](/help/sites-cloud/authoring/assets/responsive-layout-parent-button.png)

   * **Mostra componenti** nascosti - Mostra tutti i componenti o singoli componenti. Il numero indica quanti componenti nascosti sono attualmente presenti. Il contatore indica quanti componenti sono nascosti.

      ![Pulsante Mostra componenti nascosti](/help/sites-cloud/authoring/assets/responsive-layout-show-button.png)

   * **Ripristina layout** punto di interruzione: consente di tornare al layout predefinito. Ciò significa che non verrà imposto alcun layout personalizzato.

      ![Pulsante Ripristina layout punto di interruzione](/help/sites-cloud/authoring/assets/responsive-layout-revert-button.png)

   * **Mobile in nuova riga** - Se lo spazio disponibile lo consente, sposta il componente verso l’alto di una posizione.

      ![Mobile in un nuovo pulsante di riga](/help/sites-cloud/authoring/assets/responsive-layout-float-button.png)

   * **Nascondi componente** - Nasconde il componente corrente.

      ![Nascondi pulsante componente](/help/sites-cloud/authoring/assets/responsive-layout-hide-button.png)
   >[!NOTE]
   >
   >Nell’esempio in alto le azioni Mobile e Nascondi sono disponibili, perché questo Contenitore di layout è nidificato all’interno di un Contenitore di layout principale.

   * **Mostra componenti** Seleziona i componenti principali per visualizzare la barra degli strumenti delle azioni con l’opzione **Mostra componenti nascosti**. In questo esempio, due componenti sono nascosti. 

      ![Scopri i componenti](/help/sites-cloud/authoring/assets/responsive-layout-unhide.png)
   Selezionando l’opzione **Mostra componenti nascosti**, i componenti che sono attualmente nascosti nelle posizioni originali vengono visualizzati in blu.

   ![Pulsante Ripristina tutto](/help/sites-cloud/authoring/assets/responsive-layout-restore-all.png)

   Selezionando **Ripristina tutto**, tutti i componenti nascosti diventano visibili.
