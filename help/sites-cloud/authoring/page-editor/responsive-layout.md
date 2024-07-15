---
title: Layout reattivo
description: AEM consente di realizzare un layout dinamico per le pagine
exl-id: 87202742-5bed-4e87-a427-456a1a0e72cc
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1740'
ht-degree: 78%

---

# Layout reattivo {#responsive-layout}

AEM consente di avere un layout dinamico per le pagine utilizzando il componente **Contenitore di layout**.

Questo fornisce un sistema paragrafo che consente di posizionare i componenti all’interno di una griglia reattiva. Questa griglia può ridisporre il layout in base alle dimensioni e al formato del dispositivo o della finestra. Il componente viene utilizzato insieme alla modalità [**Layout**](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector), che consente di creare e modificare il layout reattivo in base al dispositivo.

Il contenitore layout:

* Consente di eseguire l’aggancio orizzontale alla griglia, oltre alla possibilità di posizionare i componenti affiancati nella griglia e di definire quando devono essere compressi o ridisposti.
* Utilizza punti di interruzione predefiniti (ad esempio, per telefono, tablet e così via) per consentire di definire il comportamento richiesto dei contenuti per i dispositivi e l’orientamento correlati.
   * Ad esempio, puoi personalizzare la dimensione del componente o specificare se può essere visualizzato su dispositivi specifici.
* Può essere nidificato per consentire il controllo delle colonne.

L’utente può quindi vedere come viene eseguito il rendering del contenuto per dispositivi specifici utilizzando l’emulatore.

AEM consente di realizzare il layout dinamico per le pagine utilizzando una combinazione di meccanismi:

* Componente [**Contenitore di layout**](#adding-a-layout-container-and-its-content-edit-mode)

  Questo componente è disponibile nel [browser dei componenti](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser) e fornisce un sistema paragrafo a griglia che consente di aggiungere e posizionare i componenti all’interno di una griglia dinamica. Può essere impostato anche come sistema paragrafo predefinito sulla tua pagina.

* [**Modalità Layout**](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector)

  Una volta che il Contenitore di layout è collocato nella pagina, è possibile utilizzare la modalità di **Layout** per posizionare i contenuti all’interno della griglia dinamica.

* [**Emulatore**](#selecting-a-device-to-emulate)
Questo consente di creare e modificare siti web dinamici il cui layout si riorganizza in base alle dimensioni del dispositivo o della finestra, ridimensionando i componenti in modo interattivo. L’utente può quindi visualizzare come viene eseguito il rendering del contenuto utilizzando l’emulatore.

Con questi meccanismi basati su una griglia dinamica è possibile:

* Utilizzare i punti di interruzione per definire layout di contenuto diversi in base alla larghezza del dispositivo (a seconda del tipo e dell’orientamento del dispositivo).
* Utilizzare questi stessi punti di interruzione e layout di contenuti per assicurare che il contenuto sia dinamico rispetto alle dimensioni della finestra del browser sul desktop.
* Utilizzare l’ancoraggio orizzontale sulla griglia per posizionarvi i componenti, ridimensionarli, definire quando dovrebbero venire compressi o ridisposti in modo da risultare affiancati o sovrapposti.
* Nascondere componenti per layout di dispositivo specifici.
* Gestire il controllo delle colonne.

A seconda del progetto, il Contenitore di layout può essere utilizzato come sistema paragrafo predefinito per le pagine o come componente disponibile per essere aggiunto alla pagina tramite il browser componenti (o entrambi).

>[!TIP]
>
>L&#39;Adobe fornisce [documentazione GitHub](https://adobe-marketing-cloud.github.io/aem-responsivegrid/) del layout reattivo come riferimento per gli sviluppatori front-end, consentendo loro di utilizzare la griglia AEM al di fuori dell&#39;AEM, ad esempio, durante la creazione di modelli statici di HTML per un futuro sito AEM.

>[!NOTE]
>
>L’uso dei meccanismi di cui sopra è abilitato mediante la configurazione del modello. Per ulteriori informazioni, vedere il documento [Configurazione del layout dinamico](/help/sites-cloud/administering/responsive-layout.md).

## Definizioni di layout, emulazione del dispositivo e punti di interruzione {#layout-definitions-device-emulation-and-breakpoints}

Quando si crea il contenuto del sito web è importante assicurarsi che venga visualizzato in modo adatto al dispositivo utilizzato.

AEM consente di definire layout dipendenti dalla larghezza del dispositivo:

* L’emulatore consente di emulare questi layout su una serie di dispositivi. Oltre al tipo di dispositivo, anche l’orientamento impostato dall’opzione **Ruota dispositivo** può influenzare il punto di interruzione che viene selezionato quando cambia la larghezza.
* I punti di interruzione sono i punti che separano le definizioni di layout.
   * Essi definiscono a tutti gli effetti la larghezza massima (in pixel) di qualsiasi dispositivo che utilizza un layout specifico.
   * I punti di interruzione sono normalmente applicabili a una gamma di dispositivi, in base alla larghezza del relativo schermo.
   * La portata di un punto di interruzione si estende a sinistra fino al punto di interruzione successivo.
   * Non è possibile selezionare specificatamente un punto di interruzione: la selezione di un dispositivo e di un orientamento comporterà la selezione automatica del punto di interruzione adeguato.

Il dispositivo **Desktop** è privo di una larghezza specifica e fa riferimento al punto di interruzione predefinito (ovvero tutto quanto si trova oltre l’ultimo punto di interruzione configurato).

>[!NOTE]
>
>È teoricamente possibile definire punti di interruzione per ogni singolo dispositivo, ma questo rende decisamente più macchinose la definizione e la manutenzione dei layout.

Quando utilizzi l’emulatore, selezioni un dispositivo specifico per l’emulazione e la definizione del layout e viene evidenziato anche il relativo punto di interruzione. Tutte le modifiche apportate al layout sono applicabili ad altri dispositivi a cui si applica il punto di interruzione. Ovvero, qualsiasi dispositivo posizionato a sinistra del marcatore del punto di interruzione attivo, ma prima del marcatore del punto di interruzione successivo.

Ad esempio, quando si seleziona il dispositivo **iPhone 6 Plus** (definito con una larghezza di 540 pixel) per l’emulazione e il layout, viene attivato anche il punto di interruzione **Telefono** (definito come 768 pixel). Qualsiasi modifica apportata al layout per **iPhone 6** è applicabile ad altri dispositivi nel punto di interruzione **Telefoni**, ad esempio **iPhone 5** (definito come 320 pixel).

![Emulatori](/help/sites-cloud/authoring/assets/responsive-layout-emulators.png)

## Selezione di un dispositivo da emulare {#selecting-a-device-to-emulate}

1. Apri la pagina desiderata per la modifica. Ad esempio:

   `http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

1. Seleziona l’icona **Emulatore** sulla barra degli strumenti in alto:

   ![Pulsante Emulatore](/help/sites-cloud/authoring/assets/emulator.png)

1. Viene visualizzata la barra degli strumenti dell’emulatore.

   ![Barra degli strumenti dell’emulatore](/help/sites-cloud/authoring/assets/responsive-layout-emulator-toolbar.png)

   La barra degli strumenti dell’emulatore mostra le seguenti opzioni di layout aggiuntive:

   * **Ruota dispositivo** - Consente di ruotare l&#39;orientamento di un dispositivo da verticale a orizzontale e viceversa.

   ![Pulsante Ruota dispositivo in orizzontale](/help/sites-cloud/authoring/assets/responsive-layout-rotate-device-landscape-button.png)
   ![Pulsante Ruota dispositivo in verticale](/help/sites-cloud/authoring/assets/responsive-layout-rotate-device-portrait-button.png)

   * **Seleziona il dispositivo**: consente di definire un dispositivo specifico da emulare da un elenco (ved. il passaggio successivo).

   ![Pulsante Seleziona il dispositivo](/help/sites-cloud/authoring/assets/responsive-layout-select-device-button.png)

1. Per selezionare un dispositivo specifico da emulare è possibile effettuare le seguenti operazioni:

   * Utilizza l’icona Seleziona dispositivo e scegli da un selettore a discesa.
   * Seleziona l’indicatore del dispositivo nella barra degli strumenti dell’emulatore.

   ![Menu a discesa Seleziona il dispositivo](/help/sites-cloud/authoring/assets/responsive-layout-select-device-dropdown.png)

1. Una volta che un dispositivo specifico è stato selezionato è possibile:

   * Visualizzare il marcatore attivo per il dispositivo selezionato, ad esempio **iPad.**
   * Visualizzare il marcatore attivo per il [punto di interruzione](#layout-definitions-device-emulation-and-breakpoints) adeguato, ad esempio **Tablet**.
   * La linea punteggiata blu rappresenta la *piega* per il dispositivo selezionato (qui un **iPhone 6 Plus** in orizzontale).

   ![La piega](/help/sites-cloud/authoring/assets/responsive-layout-fold.png)

   * La piega può anche essere considerata l’interruzione di riga della pagina (da non confondere con i [punti di interruzione](#layout-definitions-device-emulation-and-breakpoints)) per il contenuto. Viene visualizzato per comodità, per mostrare quale parte del contenuto l’utente vede sul dispositivo prima di scorrere.
   * La linea per la piega non viene visualizzata se l&#39;altezza del dispositivo emulato è superiore alle dimensioni dello schermo.
   * La piega è indicata per comodità dell’autore e non viene visualizzata nella pagina pubblicata.

## Aggiunta di un contenitore di layout e del relativo contenuto (modalità di modifica) {#adding-a-layout-container-and-its-content-edit-mode}

Un **Contenitore di layout** è un sistema paragrafo che:

* Include altri componenti.
* Definisce il layout.
* Risponde alle modifiche.

>[!NOTE]
>
>Se non è già disponibile, il **Contenitore di layout** deve essere [attivato in modo esplicito per un sistema paragrafo/pagina.](/help/sites-cloud/administering/responsive-layout.md)

1. Il **Contenitore di layout** è disponibile come componente standard nel [browser componenti](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser). Da qui puoi trascinarlo nella posizione desiderata sulla pagina, dopodiché potrai vedere il segnaposto **Trascina qui i componenti**.
1. È quindi possibile aggiungere componenti al Contenitore di layout. Questi componenti includeranno il contenuto vero e proprio:

   ![Contenitore di layout](/help/sites-cloud/authoring/assets/responsive-layout-add-to-layout-container.png)

## Selezione e intervento su un Contenitore di layout (modalità di modifica) {#selecting-and-taking-action-on-a-layout-container-edit-mode}

Come con altri componenti, puoi selezionare e quindi agire (tagliare, copiare, eliminare) su un Contenitore di layout (in modalità **Modifica**):

>[!CAUTION]
>
>Poiché un contenitore di layout è un sistema paragrafo, l’eliminazione del componente comporta l’eliminazione sia della griglia di layout che di tutti i componenti (e del relativo contenuto) presenti all’interno del contenitore.

1. Se passi il mouse sul segnaposto della griglia o lo selezioni, viene visualizzato il menu Azioni.

   ![Aggiungi al Contenitore di layout](/help/sites-cloud/authoring/assets/responsive-layout-container.png)

   È necessario selezionare l’opzione **Elemento padre**.

   ![Pulsante Elemento padre](/help/sites-cloud/authoring/assets/responsive-layout-parent-button.png)

1. Se il componente layout è nidificato, selezionando l’opzione **Elemento principale** viene presentata una selezione a discesa che consente di selezionare il contenitore di layout nidificato o i relativi elementi principali.

   Quando passi il cursore del mouse sui nomi dei contenitori nel menu a discesa, sulla pagina vengono visualizzati i relativi contorni.

   * Il contenitore di layout nidificato inferiore presenta un contorno blu.
   * Ogni contenitore successivo presenta un contorno di una tonalità di blu più chiara.

   ![Contenitori nidificati](/help/sites-cloud/authoring/assets/responsive-layout-nested.png)

1. L’intera griglia viene evidenziata con il relativo contenuto. Viene visualizzata la barra degli strumenti delle azioni, da cui è possibile selezionare un’azione, ad esempio **Elimina.**

## Definire un layout (modalità Layout) {#defining-layouts-layout-mode}

>[!NOTE]
>
>È possibile definire un layout distinto per ogni [punto di interruzione](#layout-definitions-device-emulation-and-breakpoints) (come determinato dal tipo di dispositivo e dall’orientamento emulati).

Per configurare il layout di una griglia dinamica implementato con il contenitore di layout è necessario utilizzare la modalità **Layout**.

La modalità **Layout** può essere avviata in due modi.

* Utilizzando il menu [modalità nella barra degli strumenti](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector) e selezionando la modalità **Layout**
   * Seleziona la modalità **Layout** esattamente come si fa per passare alla modalità **Modifica** o **Impostazione destinazione**.
   * La modalità **Layout** rimane persistente; si esce dalla modalità **Layout** solo quando si seleziona un’altra modalità mediante il selettore di modalità.
* Quando [si modifica un singolo componente.](/help/sites-cloud/authoring/page-editor/edit-content.md#editing-component-layout)
   * Utilizzando l’opzione **Layout** nel menu azione rapida del componente, puoi passare alla modalità **Layout**.
   * La modalità **Layout** persiste quando si modifica il componente e torna alla modalità **Modifica** quando è attivo un altro componente.

In modalità layout è possibile eseguire varie azioni su una griglia:

* Ridimensiona i componenti di contenuto utilizzando i punti blu. Il ridimensionamento viene sempre eseguito con la funzione Aggancia alla griglia. Durante il ridimensionamento, viene visualizzata la griglia di sfondo per facilitare l’allineamento:

  ![Ridimensionare i componenti](/help/sites-cloud/authoring/assets/responsive-layout-resizing.png)

  >[!NOTE]
  >
  >Proporzioni e rapporti relativi vengono mantenuti al ridimensionamento di componenti come le **immagini**.

* Seleziona un componente di contenuto; la barra degli strumenti consente di:
   * **Elemento padre** - Consente di selezionare l&#39;intero componente Contenitore di layout per intervenire su di esso nel complesso.
   * **Mobile in nuova riga:** il componente viene spostato su una nuova riga, in base allo spazio disponibile all’interno della griglia.
   * **Nascondi componente:** il componente viene reso invisibile (può essere ripristinato dalla barra degli strumenti del Contenitore di layout).

  ![Nascondi componente](/help/sites-cloud/authoring/assets/responsive-layout-hide.png)

* In modalità **Layout** è possibile selezionare **Trascinare qui i componenti** per selezionare l&#39;intero componente. Per questa modalità viene visualizzata la barra degli strumenti.

  La barra degli strumenti dispone di opzioni diverse a seconda dello stato del componente di layout e dei componenti a esso appartenenti. Esempio:

   * **Elemento padre:** consente di selezionare il componente principale.

     ![Pulsante Elemento padre](/help/sites-cloud/authoring/assets/responsive-layout-parent-button.png)

   * **Mostra componenti nascosti**: rende visibili tutti i componenti o singoli componenti. Il numero indica quanti sono componenti attualmente nascosti. Il contatore mostra il numero di componenti nascosti.

     ![Pulsante Mostra componenti nascosti](/help/sites-cloud/authoring/assets/responsive-layout-show-button.png)

   * **Ripristina layout punto di interruzione**: ripristina il layout predefinito. Non viene imposto alcun layout personalizzato.

     ![Pulsante Ripristina layout punto di interruzione](/help/sites-cloud/authoring/assets/responsive-layout-revert-button.png)

   * **Mobile in nuova riga:** consente di alzare il componente di una posizione, se lo spazio è sufficiente.

     ![Pulsante Mobile in una nuova riga](/help/sites-cloud/authoring/assets/responsive-layout-float-button.png)

   * **Nascondi componente:** consente di nascondere il componente corrente.

     ![Pulsante Nascondi componente](/help/sites-cloud/authoring/assets/responsive-layout-hide-button.png)

  >[!NOTE]
  >
  >Nell’esempio in alto le azioni Mobile e Nascondi sono disponibili, perché questo Contenitore di layout è nidificato all’interno di un Contenitore di layout principale.

   * **Mostra componenti**
Seleziona i componenti principali per visualizzare la barra degli strumenti delle azioni con l’opzione **Mostra componenti nascosti**. In questo esempio, due componenti sono nascosti.

     ![Mostra componenti](/help/sites-cloud/authoring/assets/responsive-layout-unhide.png)

  Selezionando l’opzione **Mostra componenti nascosti**, i componenti che sono attualmente nascosti nelle posizioni originali vengono visualizzati in blu.

  ![Pulsante Ripristina tutto](/help/sites-cloud/authoring/assets/responsive-layout-restore-all.png)

  Selezionando **Ripristina tutto**, tutti i componenti nascosti diventano visibili.
