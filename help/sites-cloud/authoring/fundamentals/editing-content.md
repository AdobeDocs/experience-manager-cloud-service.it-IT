---
title: Modifica del contenuto di una pagina
description: Una volta creata la pagina, è possibile aggiornarla modificandone i contenuti
exl-id: 8af0f621-14e8-4605-a51a-a3be21f19092
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '2978'
ht-degree: 94%

---


# Modifica del contenuto di una pagina{#editing-page-content}

Una volta creata la pagina (nuova o come parte di un lancio o una live copy) è possibile aggiornarla modificandone i contenuti.

Per aggiungere i contenuti si trascinano sulla pagina specifici [componenti](/help/sites-cloud/authoring/features/components-console.md), in base al tipo di contenuto, che possono quindi essere modificati, spostati o eliminati.

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

{{edge-delivery-authoring}}

## Barra degli strumenti della pagina {#page-toolbar}

Dalla barra degli strumenti della pagina è possibile accedere alle funzionalità appropriate, a seconda della configurazione della pagina.

![Barra degli strumenti della pagina](/help/sites-cloud/authoring/assets/editing-page-toolbar.png)

La barra degli strumenti permette di accedere a numerose opzioni. A seconda del contesto e della configurazione correnti, alcune opzioni potrebbero non essere disponibili.

* **Attiva/Disattiva pannello laterale**

  Apre o chiude il pannello laterale, che contiene il [browser Risorse](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser), il [browser Componenti](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) e la [Struttura contenuti](/help/sites-cloud/authoring/fundamentals/environment-tools.md#content-tree).

  ![Icona del pannello laterale](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

* **Informazioni sulle pagine**

  Consente di accedere al menu [Informazioni pagina](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) che include i dettagli della pagina e le azioni che possono essere eseguite sulla pagina, ad esempio: visualizzare e modificare le informazioni, visualizzare le proprietà e pubblicare o annullare la pubblicazione della pagina.

  ![Pulsante Informazioni pagina](/help/sites-cloud/authoring/assets/page-information-icon.png)

* **Emulatore**

  Attiva o disattiva la [barra degli strumenti dell’emulatore](/help/sites-cloud/authoring/features/responsive-layout.md#selecting-a-device-to-emulate), che permette di simulare l’aspetto che avrà la pagina su un altro dispositivo. Questa barra è automaticamente attivata in modalità di layout.

  ![Pulsante Emulatore](/help/sites-cloud/authoring/assets/emulator.png)

* **ContextHub**

  Apre [ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md). Disponibile solo in modalità Anteprima.

  ![Pulsante Context Hub](/help/sites-cloud/authoring/assets/context-hub.png)

* **Titolo pagina**

  Questa sezione è solo a scopo informativo.

  ![Titolo pagina](/help/sites-cloud/authoring/assets/page-title.png)

* **Selettore modalità**

  Visualizza il [modalità](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) e consente di selezionare un’altra modalità, ad esempio modifica, layout, timewarp o targeting.

  ![Pulsante Selettore modalità](/help/sites-cloud/authoring/assets/mode-selector.png)

* **Anteprima**

  Abilita la [modalità Anteprima](#preview-mode). La pagina viene visualizzata così come apparirà una volta pubblicata.

  ![Pulsante Anteprima](/help/sites-cloud/authoring/assets/preview.png)

* **Annotazioni**

  Consente di aggiungere [annotazioni](/help/sites-cloud/authoring/fundamentals/annotations.md) alla pagina durante la revisione. Dopo la prima annotazione, l’icona viene sostituita da un numero che indica quante annotazioni sono presenti sulla pagina.

  ![Pulsante Annotazione](/help/sites-cloud/authoring/assets/annotations.png)

### Notifica di stato {#status-notification}

Se una pagina fa parte di uno o più [flussi di lavoro](/help/sites-cloud/authoring/workflows/overview.md), queste informazioni vengono visualizzate in una barra di notifica nella parte superiore dello schermo durante la modifica della pagina.

![Notifica flusso di lavoro](/help/sites-cloud/authoring/assets/editing-workflow-notification.png)

>[!NOTE]
>
>La barra di stato è visibile solo per gli account utente che dispongono dei diritti appropriati.

La notifica riporta il flusso di lavoro in esecuzione per la pagina. Se l’utente è coinvolto nella fase attuale del flusso di lavoro, sono anche disponibili opzioni per [modificare lo stato del flusso di lavoro](/help/sites-cloud/authoring/workflows/participating.md) e ottenere ulteriori informazioni sul flusso di lavoro, ad esempio:

* **Completa:** apre la finestra di dialogo **Completa elemento di lavoro**
* **Delega:** apre la finestra di dialogo **Completa elemento di lavoro**
* **Visualizza dettagli**: apre la finestra **Dettagli** del flusso di lavoro

Il completamento e la delega delle fasi del flusso di lavoro a partire dalla barra delle notifiche funzionano in modo analogo alla [partecipazione ai flussi di lavoro](/help/sites-cloud/authoring/workflows/participating.md) a partire dalla casella in entrata delle Notifiche.

Se la pagina è soggetta a più flussi di lavoro, il numero dei flussi di lavoro viene visualizzato all’estremità destra della notifica, insieme ai pulsanti freccia che consentono di scorrere i flussi di lavoro.

![Più notifiche flusso di lavoro](/help/sites-cloud/authoring/assets/editing-workflow-notification-multiple.png)

## Segnaposto Componente {#component-placeholder}

Il segnaposto del componente è un indicatore che mostra dove è posizionato un componente quando lo rilasci, sopra il componente su cui stai passando con il puntatore del mouse.

* Quando si aggiunge un nuovo componente alla pagina (trascinandolo dal browser componenti):

  ![Segnaposto per l’aggiunta di un nuovo componente a una pagina](/help/sites-cloud/authoring/assets/editing-component-placeholder.png)

* Quando si sposta un componente esistente:

  ![Segnaposto per lo spostamento di un componente esistente su una pagina](/help/sites-cloud/authoring/assets/editing-component-placeholder-existing.png)

## Inserimento di un componente {#inserting-a-component}

### Inserire un componente dal Browser Componenti {#inserting-a-component-from-the-components-browser}

Puoi aggiungere un nuovo componente utilizzando il [browser componenti](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser). Il [segnaposto componente](#component-placeholder) mostra dove è posizionato il componente:

1. Assicurati che la pagina sia in [**modalità Modifica**.](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)
1. Apri il [browser Componenti](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser).
1. Trascina il componente di cui hai bisogno nella [posizione desiderata](#component-placeholder).
1. [Modifica](#edit-content) il componente.

>[!NOTE]
>
>Su un dispositivo mobile, il browser componenti occuperà l’intero schermo. Dopo aver iniziato a trascinare un componente, il browser si chiude per mostrare nuovamente la pagina per permetterti di posizionarlo.

### Inserimento di un Componente dal Sistema Paragrafo   {#inserting-a-component-from-the-paragraph-system}

È possibile aggiungere un nuovo componente utilizzando la casella **Trascina qui i componenti** del sistema paragrafo:

1. Assicurati che la pagina sia in [**modalità Modifica**.](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)
1. Per selezionare e aggiungere un nuovo componente dal sistema paragrafo esistono due modi:

   * Seleziona l’opzione **Inserisci componente** (+) dalla barra degli strumenti di un componente esistente o dalla casella **Trascina qui i componenti**.

     ![Inserire un componente](/help/sites-cloud/authoring/assets/editing-insert-component.png)

   * Se utilizzi un dispositivo desktop, puoi fare doppio clic sul pulsante **Trascina qui i componenti** casella.

   * Il **Inserisci nuovo componente** viene visualizzata una finestra di dialogo che consente di selezionare il componente richiesto:

     ![Finestra di dialogo Inserisci nuovo componente](/help/sites-cloud/authoring/assets/editing-insert-component-selection.png)

1. Il componente selezionato viene aggiunto nella parte inferiore della pagina. Se necessario, [Modifica](#edit-content) il componente.

### Inserimento di un componente utilizzando il browser Risorse {#inserting-a-component-using-the-assets-browser}

È possibile aggiungere un nuovo componente alla pagina anche trascinando una risorsa dal [browser Risorse](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser). Questo determina la creazione automatica di un nuovo componente del tipo appropriato (e che include la risorsa).

Puoi configurare questo comportamento per l’installazione in uso. Per ulteriori dettagli, consulta la sezione su come Configurare un sistema di paragrafi in modo che il trascinamento di una risorsa crei uno specifico componente. <!--This behavior can be configured for your installation. See [Configuring a Paragraph System so that Dragging an Asset Creates a Component Instance](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) for further details.-->

Per creare un componente trascinando uno dei tipi di risorsa indicati sopra:

1. Assicurati che la pagina sia in [**modalità Modifica**.](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes)
1. Apri il [browser Risorse](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser).
1. Trascina la risorsa richiesta nella posizione desiderata. Il [segnaposto componente](#component-placeholder) mostra dove è posizionato il componente.

   Un componente, appropriato per il tipo di risorsa, viene creato nella posizione desiderata e include la risorsa selezionata.

1. Se necessario, [Modifica](#edit-content) il componente.

>[!NOTE]
>
>Su un dispositivo mobile, il browser Risorse occupa l’intero schermo. Quando inizi a trascinare una risorsa, il browser si chiuderà per mostrare nuovamente la pagina e permetterti di posizionarla.

Se sfogliando le risorse disponibili scopri che è necessario eseguire una rapida modifica a una risorsa, puoi avviare l’[editor risorse](/help/assets/manage-digital-assets.md) direttamente dal browser, facendo clic sull’icona di modifica accanto al nome della risorsa.

![Pulsante Modifica risorsa](/help/sites-cloud/authoring/assets/asset-edit-button.png)

## Barra degli strumenti del componente {#component-toolbar}

Selezionando un componente si apre la barra degli strumenti. Consente di accedere a varie azioni che possono essere eseguite sul componente.

Le azioni disponibili dipendono dal contesto; in questa sezione ne vengono descritte solo alcune.

![Barra degli strumenti del componente](/help/sites-cloud/authoring/assets/editing-component-toolbar.png)

* **Modifica**

  [In base al tipo di componente](/help/sites-cloud/authoring/fundamentals/components.md), questa azione consente di [modificare il contenuto del componente](#edit-content). Spesso è disponibile una barra degli strumenti.

  Pulsante ![Modifica](/help/sites-cloud/authoring/assets/editing-component-toolbar-edit.png)

* **Configura**

  [In base al tipo di componente](/help/sites-cloud/authoring/fundamentals/components.md), questa azione consente di modificare e configurare le proprietà del componente. In genere presenta una finestra di dialogo.

  ![Pulsante Configura](/help/sites-cloud/authoring/assets/editing-component-toolbar-configure.png)

* **Copia**

  Questa azione consente di copiare il componente negli Appunti. Dopo che il componente è stato incollato, quello originale non viene eliminato.

  ![Pulsante Copia](/help/sites-cloud/authoring/assets/editing-component-toolbar-copy.png)

* **Taglia**

  Questa azione consente di copiare il componente negli Appunti. Dopo che il componente è stato incollato, quello originale viene rimosso.

  ![Pulsante Taglia](/help/sites-cloud/authoring/assets/editing-component-toolbar-cut.png)

* **Eliminare**

  Questa azione elimina il componente dalla pagina, previa conferma.

  ![Pulsante Elimina](/help/sites-cloud/authoring/assets/editing-component-toolbar-delete.png)

* **Inserisci componente**

  Questa azione apre la finestra di dialogo per [aggiungere un nuovo componente](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component-from-the-paragraph-system).

  ![Pulsante Inserisci](/help/sites-cloud/authoring/assets/editing-component-toolbar-insert.png)

* **Incolla**

  Questa azione consente di incollare il componente dagli Appunti alla pagina. Il componente originale viene eliminato o meno a seconda dell’opzione Taglia o Copia utilizzata.

   * È possibile utilizzare Incolla per collocare i componenti sulla stessa pagina o su una pagina diversa.
   * L’elemento viene incollato sopra l’elemento in cui selezioni l’azione Incolla.
   * L’azione Incolla viene mostrata solo se è presente contenuto negli Appunti.

  ![Pulsante Incolla](/help/sites-cloud/authoring/assets/editing-component-toolbar-paste.png)

  >[!NOTE]
  >
  >Se si incolla in un’altra pagina che era già aperta prima dell’operazione Taglia/Copia, per visualizzare il contenuto incollato è necessario aggiornare la pagina.

* **Gruppo**

  Questo consente di selezionare più componenti contemporaneamente. È possibile eseguire la stessa azione su un dispositivo desktop tramite **Ctrl+clic** o **Comando+clic**.

  ![Pulsante Gruppo](/help/sites-cloud/authoring/assets/editing-component-toolbar-group.png)

* **Elemento padre**

  Questo consente di selezionare il componente principale del componente selezionato.

  ![Pulsante Elemento padre](/help/sites-cloud/authoring/assets/editing-component-toolbar-parent.png)

* **Layout**

  Questo ti consente di modificare [layout](/help/sites-cloud/authoring/fundamentals/editing-content.md#edit-component-layout) del componente selezionato. Ciò vale solo per il componente selezionato e non attiva la [Modalità di layout](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) per l’intera pagina.

  ![Pulsante Layout](/help/sites-cloud/authoring/assets/editing-component-toolbar-layout.png)

* **Converti in variante di frammento di esperienza**

  Questo ti consente di creare un nuovo [frammento esperienza](/help/sites-cloud/authoring/fundamentals/experience-fragments.md) dal componente selezionato o aggiungilo a un frammento di esperienza esistente.

  ![Pulsante Converti in frammento esperienza](/help/sites-cloud/authoring/assets/editing-component-toolbar-xf.png)

## Modifica contenuto {#edit-content}

Esistono due metodi per aggiungere e/o modificare contenuti nei componenti:

* Aprire la [finestra di dialogo del componente per la modifica](#component-edit-dialog).
* [Trascinare una risorsa](#drag-and-drop-assets-into-component) dal browser Risorse per aggiungere direttamente il contenuto.

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

* Componente immagine: a schermo intero

  [L’accesso alla modalità a schermo intero](#edit-content-full-screen-mode) per il componente immagine consente di avere più spazio per modificare l’immagine oltre che per visualizzare opzioni di modifica aggiuntive, ad esempio **Launch Map (Avvia mappa)** e **Ripristina zoom**. Inoltre, la modalità a schermo intero consente di selezionare i predefiniti di ritaglio.

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

1. Tocca o fai clic e tieni premuto per selezionare il paragrafo da spostare.
1. Trascina il paragrafo nella nuova posizione. In AEM viene indicato dove è possibile rilasciare il paragrafo. Rilascialo nella posizione desiderata.

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

   * Vengono visualizzate le maniglie di ridimensionamento del componente.
   * La barra degli strumenti dell’emulatore viene visualizzata nella parte superiore dello schermo.
   * La barra degli strumenti del componente presenta le azioni di layout al posto delle azioni di modifica standard.

   ![Un componente in modalità layout](/help/sites-cloud/authoring/assets/editing-layout-mode.png)

   Ora puoi modificare il layout del componente, in modo analogo a come lo si modifica nella [modalità di layout](/help/sites-cloud/authoring/features/responsive-layout.md#defining-layouts-layout-mode).

1. Dopo aver apportato le modifiche necessarie, fai clic sul pulsante **Chiudi** nel menu Azioni del componente per interrompere la modifica del layout del componente. La barra degli strumenti del componente torna al normale stato di modifica.

   ![Barra degli strumenti di un componente pagina](/help/sites-cloud/authoring/assets/editing-layout-exit.png)

>[!TIP]
>
>L’azione Layout è limitata al componente selezionato. Ad esempio, se stai modificando il layout di un componente e fai clic su un altro componente, per il componente appena selezionato viene visualizzata la barra degli strumenti di modifica standard (non la barra degli strumenti di layout), mentre le maniglie di ridimensionamento e la barra degli strumenti dell’emulatore scompaiono.
>
>Se devi modificare il layout globale della pagina, che iinteresserà più componenti, passa alla [modalità di layout](/help/sites-cloud/authoring/features/responsive-layout.md).

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

La [modalità di pagina Stato Live Copy](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) consente di avere una rapida panoramica dello stato della Live Copy e di sapere quali componenti vengono ereditati e quali no:

* Bordo verde: ereditato
* Bordo rosa: l’ereditarietà è stata annullata

Esempio:

![Esempio di visualizzazione stato Live Copy](/help/sites-cloud/authoring/assets/editing-live-copy-status.png)

## Aggiunta di annotazioni {#adding-annotations}

Le [Annotazioni](/help/sites-cloud/authoring/fundamentals/annotations.md) consentono a revisori e altri autori di fornire un feedback sui contenuti. Vengono spesso utilizzate a scopo di revisione e convalida.

## Anteprima delle pagine {#previewing-pages}

Esistono due opzioni per visualizzare in anteprima una pagina:

* [Modalità Anteprima](#preview-mode): un’anteprima rapida disponibile dalla stessa posizione
* [Visualizza come pubblicato](#view-as-published): anteprima completa che apre la pagina in una nuova scheda

>[!TIP]
>
>* In modalità Modifica, i collegamenti nel contenuto sono visibili, ma non accessibili.
>* Per effettuare la navigazione tramite i collegamenti, utilizza una delle opzioni di anteprima.
>* Utilizza la [scelta rapida da tastiera](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `Ctrl-Shift-M` per passare dall’anteprima all’ultima modalità selezionata.

>[!NOTE]
>
>Il cookie della modalità WCM viene impostato per entrambe le opzioni di anteprima.

### Modalità Anteprima {#preview-mode}

Quando si modifica il contenuto, è possibile visualizzare l’anteprima della pagina utilizzando la [modalità](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) anteprima. Questa modalità:

* Nasconde vari meccanismi di modifica per fornire un’indicazione rapida di come apparirà la pagina una volta pubblicata.
* Consente di utilizzare i collegamenti per navigare.
* **Non** aggiorna il contenuto della pagina.

Durante l’authoring, la modalità di anteprima è disponibile utilizzando l’icona in alto a destra dell’Editor pagina:

![Pulsante Anteprima](/help/sites-cloud/authoring/assets/preview.png)

### Visualizza come pubblicato {#view-as-published}

L’opzione **Visualizza come pubblicato**, è disponibile nel menu [Informazioni pagina](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information). Permette di aprire la pagina in una nuova scheda, aggiornando il contenuto e visualizzando la pagina esattamente come apparirebbe nell’ambiente di pubblicazione.

## Blocco di una pagina   {#locking-a-page}

AEM consente di bloccare una pagina in modo da impedire che i contenuti possano essere modificati. Questa funzione di blocco è utile quando si devono apportare numerose modifiche a una pagina specifica oppure se occorre bloccarla per un breve periodo di tempo.

Per bloccare una pagina è possibile utilizzare:

* La console **Sites**

   1. Seleziona la pagina con [modalità di selezione](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
   1. Seleziona l’icona del lucchetto.

      ![Pulsante Blocca](/help/sites-cloud/authoring/assets/lock.png)

* **Editor pagina**

   1. Seleziona l’icona **Informazioni pagina** per aprire il menu.
   1. Seleziona l’opzione **Blocca pagina**.

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
>Pages cannot be unlocked by impersonating the user who locked the page.
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

In AEM vengono memorizzate una cronologia delle azioni eseguite e la relativa sequenza, in modo che le varie azioni possano essere annullate nell’ordine di esecuzione e ripristinate per riapplicare una o più azioni annullate, se necessario.

Se è selezionato un elemento nella pagina del contenuto (ad esempio un componente di testo) il comando Annulla o Ripristina si riferisce all’elemento selezionato.

Il comportamento dei comandi Annulla e Ripristina è simile a quello di altri software. Puoi utilizzare i comandi per ripristinare lo stato recente della pagina web mentre ne stai valutando il contenuto. Se ad esempio si sposta un paragrafo di testo altrove nella pagina, è possibile ricorrere al comando Annulla per riportarlo nella posizione originale. Se successivamente constati che la posizione precedente era migliore, utilizza il comando Ripristina per “annullare l’annullamento”.

Ad esempio:

* Puoi ripristinare le azioni solo se dopo l’annullamento non sono state apportate altre modifiche alla pagina.
* Per impostazione predefinita, è possibile annullare fino a 20 azioni di modifica.
* Per annullare e ripristinare le azioni è possibile anche utilizzare le [scelte rapide da tastiera](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md).

I comandi Annulla e Ripristina possono essere utilizzati solo per i tipi di modifiche della pagina seguenti:

* Aggiunta, modifica, rimozione e spostamento di paragrafi
* Modifica locale del contenuto dei paragrafi
* Operazioni Copia, Taglia e Incolla per elementi all’interno di una pagina

>[!NOTE]
>
>* Per annullare e ripristinare le modifiche apportate a file e immagini sono necessarie autorizzazioni speciali.
>* La cronologia delle modifiche apportate ai file e alle immagini viene conservata per almeno dieci ore. Oltre tale limite, la possibilità di annullare le modifiche non è garantita. L’amministratore può cambiare il tempo predefinito di dieci ore.
>* L’amministratore di sistema può configurare vari aspetti delle funzioni Annulla e Ripristina in base ai requisiti particolari del caso in questione.
<!--* Your system administrator can [configure various aspects of the Undo/Redo features](/help/sites-administering/config-undo.md) according to the requirements for your instance.-->
