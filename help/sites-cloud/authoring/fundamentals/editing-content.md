---
title: Modifica del contenuto di una pagina
description: Una volta creata la pagina, puoi modificarne il contenuto per apportare gli aggiornamenti necessari
exl-id: 8af0f621-14e8-4605-a51a-a3be21f19092
source-git-commit: 635f4c990c27a7646d97ebd08b453c71133f01b3
workflow-type: tm+mt
source-wordcount: '3004'
ht-degree: 60%

---

# Modifica del contenuto di una pagina{#editing-page-content}

Una volta creata la pagina (nuova o come parte di un lancio o di una Live Copy), puoi modificare il contenuto per apportare gli aggiornamenti necessari.

Il contenuto viene aggiunto tramite [componenti](/help/sites-cloud/authoring/features/components-console.md) (in base al tipo di contenuto) che possono essere trascinati sulla pagina. che possono quindi essere modificati, spostati o eliminati.

>[!NOTE]
>
>Il tuo account deve disporre dei diritti di accesso e delle autorizzazioni adeguate per intervenire sulle pagine.
>
>Nell’eventualità di problemi, rivolgiti al tuo amministratore di sistema.
<!--
>Your account needs the [appropriate access rights](/help/sites-administering/security.md) and [permissions](/help/sites-administering/security.md#permissions) to edit pages.
-->

>[!NOTE]
>
>Se la pagina e/o il modello sono stati impostati in modo appropriato, è possibile utilizzare il [layout dinamico](/help/sites-cloud/authoring/features/responsive-layout.md) durante la modifica.

>[!TIP]
>
>In modalità **Modifica**, i collegamenti presenti nel contenuto sono visibili, ma **non accessibili**. Utilizza la modalità [Anteprima](#previewing-pages) se desideri navigare utilizzando i collegamenti presenti nel tuo contenuto.

## Barra degli strumenti della pagina {#page-toolbar}

Dalla barra degli strumenti della pagina è possibile accedere alle funzionalità appropriate, a seconda della configurazione della pagina.

![Barra degli strumenti della pagina](/help/sites-cloud/authoring/assets/editing-page-toolbar.png)

La barra degli strumenti offre l’accesso a numerose opzioni. A seconda del contesto e della configurazione correnti, alcune opzioni potrebbero non essere disponibili.

* **Attiva/Disattiva pannello laterale**

  Questo apre/chiude il pannello laterale, che contiene [Browser risorse](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser), [Browser componenti](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser), e [Struttura contenuto](/help/sites-cloud/authoring/fundamentals/environment-tools.md#content-tree).

  ![Icona del pannello laterale](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

* **Informazioni sulle pagine**

  Fornisce l&#39;accesso a [Informazioni pagina](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) menu che include i dettagli e le azioni che possono essere eseguite sulla pagina, tra cui la visualizzazione e la modifica delle informazioni sulla pagina, la visualizzazione delle proprietà della pagina e la pubblicazione/annullamento della pubblicazione della pagina.

  ![Pulsante Informazioni pagina](/help/sites-cloud/authoring/assets/page-information-icon.png)

* **Emulatore**

  Attiva/disattiva [barra degli strumenti emulatore](/help/sites-cloud/authoring/features/responsive-layout.md#selecting-a-device-to-emulate), utilizzato per emulare l’aspetto della pagina su un altro dispositivo. Questa funzione viene attivata automaticamente in modalità layout.

  ![Pulsante Emulatore](/help/sites-cloud/authoring/assets/emulator.png)

* **ContextHub**

  Apre [ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md). Disponibile solo in modalità Anteprima.

  ![Pulsante Context Hub](/help/sites-cloud/authoring/assets/context-hub.png)

* **Titolo pagina**

  Questo è puramente informativo.

  ![Titolo pagina](/help/sites-cloud/authoring/assets/page-title.png)

* **Selettore modalità**

  Visualizza il [modalità](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) e consente di selezionare un’altra modalità, ad esempio modifica, layout, timewarp o targeting.

  ![Pulsante Selettore modalità](/help/sites-cloud/authoring/assets/mode-selector.png)

* **Anteprima**

  Abilita [modalità anteprima](#preview-mode). In questo modo la pagina viene visualizzata così come verrà visualizzata al momento della pubblicazione.

  ![Pulsante Anteprima](/help/sites-cloud/authoring/assets/preview.png)

* **Annotazioni**

  Consente di aggiungere [annotazioni](/help/sites-cloud/authoring/fundamentals/annotations.md) alla pagina durante la revisione. Dopo la prima annotazione, l’icona passa a un numero che indica il numero di annotazioni sulla pagina.

  ![Pulsante Annotazione](/help/sites-cloud/authoring/assets/annotations.png)

### Notifica di stato {#status-notification}

Se una pagina fa parte di uno o più [flussi di lavoro](/help/sites-cloud/authoring/workflows/overview.md), queste informazioni vengono visualizzate in una barra di notifica nella parte superiore dello schermo durante la modifica della pagina.

![Notifica flusso di lavoro](/help/sites-cloud/authoring/assets/editing-workflow-notification.png)

>[!NOTE]
>
>La barra di stato è visibile solo agli account utente con i privilegi appropriati.

La notifica elenca il flusso di lavoro in esecuzione sulla pagina. Se l’utente è coinvolto nel passaggio del flusso di lavoro corrente, le opzioni per [influenzare lo stato del flusso di lavoro](/help/sites-cloud/authoring/workflows/participating.md) e sono disponibili anche ulteriori informazioni sul flusso di lavoro, ad esempio:

* **Completa:** apre la finestra di dialogo **Completa elemento di lavoro**
* **Delega:** apre la finestra di dialogo **Completa elemento di lavoro**
* **Visualizza dettagli**: apre la finestra **Dettagli** del flusso di lavoro

Il completamento e la delega delle fasi del flusso di lavoro a partire dalla barra delle notifiche funzionano in modo analogo alla [partecipazione ai flussi di lavoro](/help/sites-cloud/authoring/workflows/participating.md) a partire dalla casella in entrata delle Notifiche.

Se la pagina è soggetta a più flussi di lavoro, il numero dei flussi di lavoro viene visualizzato all’estremità destra della notifica, insieme ai pulsanti freccia che consentono di scorrere i flussi di lavoro.

![Più notifiche flusso di lavoro](/help/sites-cloud/authoring/assets/editing-workflow-notification-multiple.png)

## Segnaposto Componente {#component-placeholder}

Il segnaposto del componente è un indicatore che mostra dove si trova un componente quando lo rilasci, sopra il componente che si sta passando con il mouse.

* Quando aggiungi un nuovo componente alla pagina (trascinandolo dal browser dei componenti):

  ![Segnaposto per l’aggiunta di un nuovo componente a una pagina](/help/sites-cloud/authoring/assets/editing-component-placeholder.png)

* Quando si sposta un componente esistente:

  ![Segnaposto per lo spostamento di un componente esistente su una pagina](/help/sites-cloud/authoring/assets/editing-component-placeholder-existing.png)

## Inserimento di un componente {#inserting-a-component}

### Inserire un componente dal Browser Componenti {#inserting-a-component-from-the-components-browser}

È possibile aggiungere un nuovo componente utilizzando [browser componenti](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser). Il [segnaposto componente](#component-placeholder) mostra dove è posizionato il componente:

1. Assicurati che la pagina sia in [**modalità Modifica**.](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)
1. Apri il [browser Componenti](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser).
1. Trascina il componente di cui hai bisogno nella [posizione desiderata](#component-placeholder).
1. [Modifica](#edit-content) il componente.

>[!NOTE]
>
>Su un dispositivo mobile, il browser componenti occupa l’intera schermata. Dopo aver iniziato a trascinare un componente, il browser si chiude per mostrare nuovamente la pagina e inserire il componente.

### Inserimento di un Componente dal Sistema Paragrafo   {#inserting-a-component-from-the-paragraph-system}

È possibile aggiungere un nuovo componente utilizzando la casella **Trascina qui i componenti** del sistema paragrafo:

1. Assicurati che la pagina sia in [**modalità Modifica**.](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)
1. Esistono due modi per selezionare e aggiungere un nuovo componente dal sistema paragrafo:

   * Seleziona la **Inserisci componente** nella barra degli strumenti di un componente esistente o nella scheda **Trascina qui i componenti** casella.

     ![Inserire un componente](/help/sites-cloud/authoring/assets/editing-insert-component.png)

   * Se utilizzi un dispositivo desktop, puoi fare doppio clic sulla casella **Trascina qui i componenti**.

   * Viene visualizzata la finestra di dialogo **Inserisci nuovo componente**, che consente di selezionare il componente richiesto:

     ![Finestra di dialogo Inserisci nuovo componente](/help/sites-cloud/authoring/assets/editing-insert-component-selection.png)

1. Il componente selezionato viene aggiunto nella parte inferiore della pagina. [Modifica](#edit-content) il componente, se necessario.

### Inserimento di un componente utilizzando il browser Risorse   {#inserting-a-component-using-the-assets-browser}

È possibile aggiungere un nuovo componente alla pagina anche trascinando una risorsa dal [browser Risorse](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser). Questo determina la creazione automatica di un nuovo componente del tipo appropriato (e che include la risorsa).

Puoi configurare questo comportamento per l’installazione in uso. Per ulteriori dettagli, consulta la sezione su come Configurare un sistema di paragrafi in modo che il trascinamento di una risorsa crei uno specifico componente. <!--This behavior can be configured for your installation. See [Configuring a Paragraph System so that Dragging an Asset Creates a Component Instance](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) for further details.-->

Per creare un componente trascinando uno dei tipi di risorsa indicati sopra:

1. Assicurati che la pagina sia in [**modalità Modifica**.](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)
1. Apri [browser risorse](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser).
1. Trascina la risorsa richiesta nella posizione desiderata. Il [segnaposto componente](#component-placeholder) mostra dove è posizionato il componente.

   Nella posizione desiderata viene creato un componente appropriato per il tipo di risorsa, che contiene la risorsa selezionata.

1. [Modifica](#edit-content) il componente, se necessario.

>[!NOTE]
>
>Su un dispositivo mobile, il browser risorse occupa l’intera schermata. Dopo aver iniziato a trascinare una risorsa, il browser si chiude per mostrare nuovamente la pagina e inserire la risorsa.

Se sfogliando le risorse disponibili scopri che è necessario apportare una rapida modifica a una risorsa, puoi avviare il [editor risorse](/help/assets/manage-digital-assets.md) direttamente dal browser, facendo clic sull’icona di modifica accanto al nome della risorsa.

![Pulsante Modifica risorsa](/help/sites-cloud/authoring/assets/asset-edit-button.png)

## Barra degli strumenti del componente {#component-toolbar}

Selezionando un componente si aprirà la barra degli strumenti, che consente di accedere alle azioni disponibili per tale componente.

Le azioni disponibili per l’utente sono visualizzate come appropriato e non tutte le azioni possono essere descritte qui.

![Barra degli strumenti del componente](/help/sites-cloud/authoring/assets/editing-component-toolbar.png)

* **Modifica**

  [Dipende dal tipo di componente](/help/sites-cloud/authoring/fundamentals/components.md), questo consente di: [modificare il contenuto del componente](#edit-content). Spesso viene fornita una barra degli strumenti.

  Pulsante ![Modifica](/help/sites-cloud/authoring/assets/editing-component-toolbar-edit.png)

* **Configura**

  [Dipende dal tipo di componente](/help/sites-cloud/authoring/fundamentals/components.md), consente di modificare e configurare le proprietà del componente. Spesso viene aperta una finestra di dialogo.

  ![Pulsante Configura](/help/sites-cloud/authoring/assets/editing-component-toolbar-configure.png)

* **Copia**

  Il componente verrà copiato negli Appunti. Dopo l’azione Incolla, il componente originale rimane.

  ![Pulsante Copia](/help/sites-cloud/authoring/assets/editing-component-toolbar-copy.png)

* **Taglia**

  Il componente verrà copiato negli Appunti. Dopo l’azione Incolla, il componente originale viene rimosso.

  ![Pulsante Taglia](/help/sites-cloud/authoring/assets/editing-component-toolbar-cut.png)

* **Eliminare**

  Il componente verrà eliminato dalla pagina con la tua conferma.

  ![Pulsante Elimina](/help/sites-cloud/authoring/assets/editing-component-toolbar-delete.png)

* **Inserisci componente**

  Verrà aperta la finestra di dialogo per [aggiungi un nuovo componente](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component-from-the-paragraph-system).

  ![Pulsante Inserisci](/help/sites-cloud/authoring/assets/editing-component-toolbar-insert.png)

* **Incolla**

  Il componente verrà incollato dagli Appunti alla pagina. Se l&#39;originale rimane, dipende dal fatto se avete usato la copia o il taglio.

   * È possibile incollare nella stessa pagina o in una pagina diversa.
   * L’elemento incollato viene incollato sopra l’elemento in cui si seleziona l’azione Incolla.
   * L&#39;azione Incolla viene visualizzata solo se negli Appunti è presente del contenuto.

  ![Pulsante Incolla](/help/sites-cloud/authoring/assets/editing-component-toolbar-paste.png)

  >[!NOTE]
  >
  >Se si incolla in un&#39;altra pagina già aperta prima dell&#39;operazione Taglia/Copia, è necessario aggiornare la pagina per visualizzare il contenuto incollato.

* **Gruppo**

  Questo consente di selezionare più componenti contemporaneamente. Lo stesso può essere ottenuto su un dispositivo desktop da un **Ctrl+clic** o **Comando+clic**.

  ![Pulsante Gruppo](/help/sites-cloud/authoring/assets/editing-component-toolbar-group.png)

* **Elemento padre**

  Questa opzione consente di selezionare l’elemento padre del componente selezionato.

  ![Pulsante Elemento padre](/help/sites-cloud/authoring/assets/editing-component-toolbar-parent.png)

* **Layout**

  Questo consente di modificare [layout](/help/sites-cloud/authoring/fundamentals/editing-content.md#edit-component-layout) del componente selezionato. Questo si applica solo al componente selezionato e non attiva il [Modalità Layout](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) per l’intera pagina.

  ![Pulsante Layout](/help/sites-cloud/authoring/assets/editing-component-toolbar-layout.png)

* **Converti in variante di frammento di esperienza**

  Consente di creare un nuovo [Frammento esperienza](/help/sites-cloud/authoring/fundamentals/experience-fragments.md) dal componente selezionato o di aggiungerlo a un frammento di esperienza esistente.

  ![Pulsante Converti in frammento esperienza](/help/sites-cloud/authoring/assets/editing-component-toolbar-xf.png)

## Modifica contenuto {#edit-content}

Esistono due metodi per aggiungere e/o modificare contenuti nei componenti:

* Apri [finestra di dialogo del componente per la modifica](#component-edit-dialog).
* [Trascinare una risorsa](#drag-and-drop-assets-into-component) dal browser risorse per aggiungere direttamente il contenuto.

### Finestra di dialogo di modifica del componente   {#component-edit-dialog}

Per aprire un componente e modificarne il contenuto, utilizza l’icona [Modifica (a forma di matita) nella barra degli strumenti del componente](#component-toolbar).

Le opzioni di modifica effettive dipendono dal componente. Per alcuni componenti [tutte le azioni sono disponibili solo in modalità a schermo intero](#edit-content-full-screen-mode). Esempio:

* Componente testo

  ![Barra degli strumenti del componente testo](/help/sites-cloud/authoring/assets/editing-text-component-toolbar.png)

* Componente immagine

  ![Barra degli strumenti del componente immagine](/help/sites-cloud/authoring/assets/editing-image-component-toolbar.png)

  >[!NOTE]
  >
  >La modifica non funziona su un componente immagine vuoto.
  >
  >È necessario trascinare o caricare un’immagine sul componente prima di poter iniziare a modificarlo.

* Componente immagine - schermo intero

  [L’accesso alla modalità a tutto schermo](#edit-content-full-screen-mode) per il componente immagine consente di avere più spazio per modificare l’immagine oltre che per visualizzare opzioni di modifica aggiuntive, ad esempio **Launch Map (Avvia mappa)** e **Ripristina zoom**. Inoltre, lo schermo intero consente di selezionare i predefiniti di ritaglio.

  ![Modalità a tutto schermo del componente immagine](/help/sites-cloud/authoring/assets/editing-image-component-full-screen.png)

* Per componenti composti da più componenti di base verrà richiesto di confermare quale insieme di opzioni di modifica si desidera utilizzare:

### Trascinare risorse nel componente {#drag-and-drop-assets-into-component}

Per tipi di componenti specifici, come le immagini, per aggiornare il contenuto è possibile trascinare le risorse direttamente dal browser al componente.

## Modifica contenuto in Modalità a tutto schermo {#edit-content-full-screen-mode}

Per tutti i componenti è possibile accedere alla (e uscire dalla) modalità a tutto tramite:

![Pulsante Schermo intero](/help/sites-cloud/authoring/assets/editing-full-screen.png)

Per esempio, il componente **Testo**:

![Componente testo a schermo intero](/help/sites-cloud/authoring/assets/editing-text-full-screen.png)

>[!NOTE]
>
>Per alcuni componenti, la modalità a schermo intero includerà più opzioni rispetto all’editor locale di base.

## Spostamento di un componente {#moving-a-component}

Per spostare un componente paragrafo:

1. Seleziona il paragrafo da spostare con la pressione del tasto e del tasto o con il tasto e il tasto.
1. Trascinare il paragrafo nella nuova posizione. L&#39;AEM indica dove il paragrafo può essere depositato. Rilascialo nella posizione desiderata.

   ![Spostamento di un componente](/help/sites-cloud/authoring/assets/editing-moving-component.png)

1. Il paragrafo è stato spostato.

>[!TIP]
>
>Per spostare un componente puoi anche utilizzare [Taglia e Incolla](#component-toolbar).

## Modificare il layout del componente {#edit-component-layout}

Invece di passare più volte dalla modalità di modifica alla [modalità di layout](/help/sites-cloud/authoring/features/responsive-layout.md) per regolare le impostazioni di un componente, è possibile selezionare l’azione **Layout**. Questo permette di modificare rapidamente il layout di quello specifico componente, senza uscire dalla modalità di modifica.

1. In modalità **Modifica** nella console Sites, quando si seleziona un componente viene visualizzata la sua barra degli strumenti.

   ![Barra degli strumenti di un componente pagina](/help/sites-cloud/authoring/assets/editing-layout-toolbar.png)

   Tocca o fai clic sull’azione **Layout** per modificare il layout del componente.

   ![Pulsante Layout della barra degli strumenti del componente](/help/sites-cloud/authoring/assets/editing-component-toolbar-layout.png)

1. Una volta selezionata l’azione Layout:

   * Vengono visualizzati i quadratini di ridimensionamento per il componente.
   * La barra degli strumenti dell’emulatore viene visualizzata nella parte superiore dello schermo.
   * Le azioni Layout invece delle azioni di modifica standard vengono visualizzate nella barra degli strumenti del componente.

   ![Un componente in modalità layout](/help/sites-cloud/authoring/assets/editing-layout-mode.png)

   Ora puoi modificare il layout del componente, in modo analogo a come lo si modifica nella [modalità di layout](/help/sites-cloud/authoring/features/responsive-layout.md#defining-layouts-layout-mode).

1. Dopo aver apportato le modifiche necessarie, fai clic sul pulsante **Chiudi** nel menu Azioni del componente per interrompere la modifica del layout del componente. La barra degli strumenti del componente torna al normale stato di modifica.

   ![Barra degli strumenti di un componente pagina](/help/sites-cloud/authoring/assets/editing-layout-exit.png)

>[!TIP]
>
>L’azione Layout è limitata al componente selezionato. Ad esempio, se stai modificando il layout di un componente e fai clic su un altro componente, per il componente appena selezionato viene visualizzata la barra degli strumenti di modifica standard (non quella di layout), mentre le maniglie di ridimensionamento e la barra degli strumenti dell’emulatore sono nascosti.
>
>Se devi modificare il layout generale della pagina, influenzando più componenti, passa a [modalità di layout](/help/sites-cloud/authoring/features/responsive-layout.md).

## Componenti ereditati {#inherited-components}

L’ereditarietà è il meccanismo in cui il contenuto può essere inviato automaticamente da un componente all’altro. I componenti ereditati possono essere il risultato di vari scenari, tra cui:

* [Gestione multisito](/help/sites-cloud/administering/msm/overview.md)
* [Lanci](/help/sites-cloud/authoring/launches/overview.md) (se basati su Live Copy).

È possibile annullare l’ereditarietà, quindi riabilitarla. A seconda del componente, questo può essere disponibile dalla barra degli strumenti del componente, se il componente si trova in una pagina che fa parte di una Live Copy o di un lancio (basato su una Live Copy).

![Barra degli strumenti di un componente che mostra la relazione di ereditarietà](/help/sites-cloud/authoring/assets/editing-component-toolbar-inheritance.png)

Esempio:

* Annulla ereditarietà

  ![Pulsante Annulla ereditarietà](/help/sites-cloud/authoring/assets/editing-cancel-inheritance.png)

* Riattiva ereditarietà (se l’ereditarietà è già annullata)

  ![Pulsante Riattiva ereditarietà](/help/sites-cloud/authoring/assets/editing-reenable-inheritance.png)

* L’azione Rollout è disponibile anche nel blueprint o nella sorgente Live Copy

  ![Pulsante Rollout](/help/sites-cloud/authoring/assets/editing-rollout.png)

## Modificare il modello di pagina {#editing-the-page-template}

Per passare facilmente all’[Editor modelli](/help/sites-cloud/authoring/features/templates.md#editing-templates-template-authors), seleziona **Modifica modello** dal menu [Informazioni pagina](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information).

Puoi vedere facilmente su quale modello si basa la pagina quando la selezioni in [Vista a colonne](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view) o [Vista a elenco](/help/sites-cloud/authoring/getting-started/basic-handling.md#list-view).

## Stato della Live Copy   {#live-copy-status}

Il [Modalità pagina Stato Live Copy](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) consente di avere una rapida panoramica dello stato live copy e di sapere quali componenti vengono/non vengono ereditati:

* Bordo verde: ereditato
* Bordo rosa: ereditarietà annullata

Esempio:

![Esempio di visualizzazione stato Live Copy](/help/sites-cloud/authoring/assets/editing-live-copy-status.png)

## Aggiunta di annotazioni {#adding-annotations}

[Annotazioni](/help/sites-cloud/authoring/fundamentals/annotations.md) consenti ai revisori e ad altri autori di fornire feedback sui contenuti. Vengono spesso utilizzati a scopo di revisione e convalida.

## Anteprima delle pagine   {#previewing-pages}

Esistono due opzioni per visualizzare in anteprima una pagina:

* [Modalità Anteprima](#preview-mode): un’anteprima rapida disponibile dalla stessa posizione
* [Visualizza come pubblicato](#view-as-published) - anteprima completa che apre la pagina in una nuova scheda

>[!TIP]
>
>* I collegamenti nel contenuto sono visibili, ma non accessibili in modalità di modifica.
>* Per effettuare la navigazione tramite i collegamenti, utilizza una delle opzioni di anteprima.
>* Utilizza la [scelta rapida da tastiera](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `Ctrl-Shift-M` per passare dall’anteprima all’ultima modalità selezionata.

>[!NOTE]
>
>Il cookie della modalità WCM viene impostato per entrambe le opzioni di anteprima.

### Modalità Anteprima {#preview-mode}

Durante la modifica del contenuto è possibile visualizzare l’anteprima della pagina utilizzando [modalità](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes). Questa modalità:

* Nasconde vari meccanismi di modifica per fornire un’indicazione rapida di come apparirà la pagina una volta pubblicata.
* Consente di utilizzare i collegamenti per spostarsi.
* Does **non** aggiorna il contenuto della pagina.

Durante l’authoring, la modalità di anteprima è disponibile utilizzando l’icona in alto a destra nell’editor di pagine:

![Pulsante Anteprima](/help/sites-cloud/authoring/assets/preview.png)

### Visualizza come pubblicato {#view-as-published}

L’opzione **Visualizza come pubblicato**, è disponibile nel menu [Informazioni pagina](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information). La pagina viene aperta in una nuova scheda, il contenuto viene aggiornato e la pagina viene visualizzata esattamente come apparirà nell’ambiente di pubblicazione.

## Blocco di una pagina   {#locking-a-page}

AEM consente di bloccare una pagina in modo da impedire che i contenuti possano essere modificati. Questa funzione è utile quando si devono apportare numerose modifiche a una pagina oppure se occorre bloccarla per un breve periodo di tempo.

Una pagina può essere bloccata da:

* **Sites** console

   1. Seleziona la pagina con [modalità di selezione](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
   1. Seleziona l’icona del lucchetto.

      ![Pulsante Blocca](/help/sites-cloud/authoring/assets/lock.png)

* **Editor pagina**

   1. Seleziona la **Informazioni pagina** per aprire il menu.
   1. Seleziona la **Blocca pagina** opzione.

Una volta eseguito il blocco le informazioni di visualizzazione della console vengono aggiornate e, durante la modifica, un simbolo a forma di lucchetto viene visualizzato nella barra degli strumenti.

![Esempio di pagina bloccata](/help/sites-cloud/authoring/assets/editing-locked-page.png)

>[!CAUTION]
>
>Il blocco di pagina può essere eseguito quando si impersona un utente. Tuttavia, una pagina bloccata in questo modo può essere sbloccata (dai clienti) solo utilizzando l’utente impersonato.
>
>Non è consentito sbloccare le pagine bloccate impersonando l’utente che le ha boccate.
>
>Se l’utente che ha bloccato la pagina non è disponibile per sbloccare la pagina, contatta l’Assistenza clienti per valutare le opzioni per rimuovere il blocco.

## Sblocco di una pagina {#unlocking-a-page}

La procedura di sblocco di una pagina è molto simile a quella di [blocco](#locking-a-page): una volta che la pagina è bloccata, le opzioni di blocco vengono sostituite da quelle di sblocco.

Nel menu Informazioni pagina è presente l’opzione **Sblocca** e l’icona Blocca nella console Sites viene sostituita dall’icona **Sblocca**.

![Pulsante Sblocca](/help/sites-cloud/authoring/assets/unlock.png)

>[!CAUTION]
>
>Il blocco di pagina può essere eseguito quando si impersona un utente. Tuttavia, una pagina bloccata in questo modo può essere sbloccata (dai clienti) solo utilizzando l’utente impersonato.
>
>Non è consentito sbloccare le pagine bloccate impersonando l’utente che le ha boccate.
>
>Se l’utente che ha bloccato la pagina non è disponibile per sbloccare la pagina, contatta l’Assistenza clienti per valutare le opzioni per rimuovere il blocco.

<!--
>[!CAUTION]
>
>Locking a page can be performed when impersonating a user. However a page locked in this way can only then be unlocked by the user who was impersonated, or by a user with admin rights (a member of AEM Administrator IMS profile).
>
>Pages can not be unlocked by impersonating the user who locked the page.
-->

<!--
>Locking a page can be performed when [impersonating a user](/help/sites-administering/security.md#impersonating-another-user). However a page locked in this way can only then be unlocked by the user who was impersonated or by the admin user.
-->

## Annullamento e ripristino di operazioni di modifica delle pagine {#undoing-and-redoing-page-edits}

Le icone seguenti consentono di annullare o ripristinare un’azione. Vengono visualizzate sulla barra degli strumenti quando necessario:

![Pulsanti Annulla e Ripristina](/help/sites-cloud/authoring/assets/redo.png)

>[!TIP]
>
>* Per annullare le azioni di modifica della pagina è anche disponibile la [scelta rapida da tastiera](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `Ctrl-Z`.
>* Per ripristinare le azioni di modifica della pagina è anche disponibile la scelta rapida da tastiera `Ctrl-Y`.

>[!NOTE]
>
>Per informazioni sulle possibilità di annullare e ripristinare le modifiche apportate a una pagina, consulta [Annullamento e ripristino di operazioni di modifica delle pagine - La teoria](#undoing-and-redoing-page-edits-the-theory).

## Annullamento e ripristino di operazioni di modifica delle pagine - La teoria {#undoing-and-redoing-page-edits-the-theory}

In AEM vengono memorizzate una cronologia delle azioni eseguite e la relativa sequenza, in modo che le varie azioni possano essere annullate nell’ordine di esecuzione; inoltre è possibile utilizzare l’opzione Ripristina per riapplicare una o più azioni annullate.

Se è selezionato un elemento nella pagina del contenuto (ad esempio un componente di testo) il comando Annulla o Ripristina si riferisce all’elemento selezionato.

Il comportamento dei comandi Annulla e Ripristina è simile a quello di altri software. Puoi utilizzare i comandi per ripristinare lo stato recente della pagina web mentre ne stai valutando il contenuto. Se ad esempio si sposta un paragrafo di testo altrove nella pagina, è possibile ricorrere al comando Annulla per riportarlo nella posizione originale. Se in seguito si decide che la posizione precedente è migliore, utilizzare il comando Ripeti per annullare l&#39;operazione Annulla.

Ad esempio:

* Ripeti le azioni se non hai apportato alcuna modifica alla pagina da quando hai utilizzato Annulla.
* Annulla un massimo di 20 azioni di modifica (impostazione predefinita).
* Utilizza anche [Scelte rapide da tastiera](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) per annullare e ripetere.

Potete utilizzare le opzioni Annulla (Undo) e Ripristina (Redo) per i seguenti tipi di modifiche di pagina:

* Aggiunta, modifica, rimozione e spostamento di paragrafi
* Modifica diretta del contenuto dei paragrafi
* Copiare, tagliare e incollare elementi in una pagina

>[!NOTE]
>
>* Per annullare e ripristinare le modifiche apportate a file e immagini sono necessarie autorizzazioni speciali.
>* La cronologia delle modifiche apportate a file e immagini dura almeno dieci ore. Oltre tale limite, la possibilità di annullare le modifiche non è garantita. L’amministratore può modificare l’ora predefinita di dieci ore.
>* L’amministratore di sistema può configurare vari aspetti delle funzioni Annulla e Ripristina in base ai requisiti particolari del caso in questione.
<!--* Your system administrator can [configure various aspects of the Undo/Redo features](/help/sites-administering/config-undo.md) according to the requirements for your instance.-->
