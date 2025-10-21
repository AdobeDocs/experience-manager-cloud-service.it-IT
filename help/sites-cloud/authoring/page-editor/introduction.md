---
title: Editor pagina di AEM
description: L’editor pagina di AEM è uno strumento utile per la creazione dei contenuti.
exl-id: da7d5933-f6c9-4937-a483-ec4352fba86b
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 0a458616afad836efae27e67dbe145fc44bee968
workflow-type: tm+mt
source-wordcount: '1431'
ht-degree: 39%

---


# Editor pagina di AEM {#editing-page-content}

Una volta creata la pagina nella console [**Sites**](/help/sites-cloud/authoring/sites-console/introduction.md), puoi modificarne il contenuto utilizzando l&#39;editor pagina di AEM, uno strumento utile per la creazione dei contenuti.

>[!NOTE]
>
>Durante la modifica di una pagina nella console [**Sites**](/help/sites-cloud/authoring/sites-console/introduction.md), la console aprirà l&#39;editor appropriato per il [modello](/help/sites-cloud/authoring/page-editor/templates.md) della pagina, ovvero l&#39;editor pagina descritto in questo documento o l&#39;[Editor universale](/help/sites-cloud/authoring/universal-editor/authoring.md).

>[!NOTE]
>
>Il tuo account necessita dei diritti di accesso e delle autorizzazioni appropriate per modificare le pagine. Se non disponi delle autorizzazioni necessarie, contatta l’amministratore di sistema.

{{traditional-aem}}

## Orientamento {#orientation}

L’editor pagina di AEM è composto principalmente da tre sezioni:

1. [Barra degli strumenti](#toolbar): consente di accedere rapidamente alla modifica della modalità della pagina e ad altre impostazioni di pagina.
1. [Pannello laterale](#side-panel) - Il pannello laterale consente di accedere ai componenti e alle risorse della pagina e ad altri strumenti di creazione.
1. [Editor](#editor) - Nell&#39;editor è possibile apportare modifiche al contenuto e visualizzarne l&#39;anteprima.

![Layout dell&#39;editor pagina](assets/page-editor-layout.png)

Per aggiungere i contenuti si trascinano sulla pagina specifici [componenti](/help/sites-cloud/authoring/components-console.md), in base al tipo di contenuto, che possono quindi essere modificati, spostati o eliminati.

### Barra degli strumenti {#page-toolbar}

La barra degli strumenti della pagina consente di accedere alle funzionalità appropriate per il contesto, a seconda della configurazione della pagina.

![Barra degli strumenti dell&#39;editor di pagine](assets/page-editor-toolbar.png)

#### Pannello laterale {#side-panel-button}

Verrà aperto/chiuso il [pannello laterale](/help/sites-cloud/authoring/page-editor/editor-side-panel.md), che contiene il Browser risorse, il Browser componenti e la Struttura contenuto.

![Icona del pannello laterale](assets/page-editor-side-panel-toggle.png)

#### Informazioni sulle pagine {#page-information}

Questo fornisce accesso a informazioni di pagina dettagliate, inclusi i dettagli e le azioni che possono essere eseguite sulla pagina, inclusa la visualizzazione e la modifica delle informazioni di pagina, la visualizzazione delle proprietà di pagina e la pubblicazione/annullamento della pubblicazione della pagina.

![Pulsante Informazioni pagina](assets/page-editor-page-information-icon.png)

**Informazioni pagina** apre un menu a discesa che fornisce dettagli sull&#39;ultima modifica e sull&#39;ultima pubblicazione della pagina selezionata. Sono disponibili azioni aggiuntive a seconda delle caratteristiche della pagina, del sito e dell’istanza.

* [Apri proprietà](/help/sites-cloud/authoring/sites-console/page-properties.md)
* [Rollout pagina](/help/sites-cloud/administering/msm/overview.md#msm-from-the-ui)
* [Avvia flusso di lavoro](/help/sites-cloud/authoring/workflows/applying.md#starting-a-workflow-from-the-page-editor)
* [Blocca pagina](/help/sites-cloud/authoring/page-editor/introduction.md#locking-unlocking)
* [Pubblica pagina](/help/sites-cloud/authoring/sites-console/publishing-pages.md#publishing-pages-1)
* [Annulla pubblicazione pagina](/help/sites-cloud/authoring/sites-console/publishing-pages.md#unpublishing-pages)
* [Modifica modello](/help/sites-cloud/authoring/page-editor/templates.md)
* [Visualizza come pubblicato](/help/sites-cloud/authoring/page-editor/introduction.md#view-as-published)
* [Visualizza in Amministrazione](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources)
* [Aiuto](/help/sites-cloud/authoring/basic-handling.md#accessing-help)
* [Promuovi lancio:](/help/sites-cloud/authoring/launches/promoting.md) (solo se la pagina è un lancio)

Inoltre, se necessario, **Informazioni pagina** può fornire accesso alle analisi e alle raccomandazioni.

#### Emulatore {#emulator}

In questo modo viene attivata o disattivata la barra degli strumenti dell&#39;[emulatore](/help/sites-cloud/authoring/page-editor/responsive-layout.md#selecting-a-device-to-emulate), utilizzata per emulare l&#39;aspetto della pagina su un altro dispositivo. Questa funzione viene abilitata automaticamente in modalità layout.

![Pulsante Emulatore](assets/page-editor-emulator.png)

#### ContextHub {#context-hub}

Verrà aperto [ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md). È disponibile solo in modalità **Anteprima**.

![Pulsante Context Hub](assets/page-editor-context-hub.png)

#### Titolo pagina {#page-title}

Questo è il titolo della pagina, rappresentato in lettere maiuscole come informazione.

![Titolo pagina](assets/page-editor-page-title.png)

#### Selettore modalità {#mode-selector}

Il selettore di modalità visualizza la [modalità](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector) corrente e consente di selezionare un&#39;altra modalità, ad esempio modifica, layout, timewarp o targeting.

![Pulsante Selettore modalità](assets/page-editor-mode-selector.png)

Esistono diverse modalità di modifica di una pagina che consentono di eseguire azioni diverse:

* [Modifica](/help/sites-cloud/authoring/page-editor/edit-content.md) - Modalità da utilizzare per la modifica del contenuto della pagina
* [Layout](/help/sites-cloud/authoring/page-editor/responsive-layout.md) - Consente di creare e modificare il layout dinamico a seconda del dispositivo (se la pagina si basa su un contenitore di layout)
* [Targeting](/help/sites-cloud/authoring/personalization/targeted-content.md) - Migliora la rilevanza dei contenuti tramite il targeting e la misurazione su tutti i canali
* [Timewarp](/help/sites-cloud/authoring/sites-console/page-versions.md#timewarp) - Visualizza lo stato di una pagina in un determinato momento
* [Stato Live Copy](/help/sites-cloud/authoring/page-editor/introduction.md#live-copy-status) - Consente una rapida panoramica dello stato della Live Copy e dei componenti che non sono ereditati
* [Modalità Sviluppatore](/help/implementing/developing/tools/developer-mode.md)
* [Anteprima](/help/sites-cloud/authoring/page-editor/introduction.md#previewing-pages) - Visualizza la pagina così come è visualizzata nell&#39;ambiente di pubblicazione; oppure per spostarti utilizzando i collegamenti presenti nel contenuto
* [Annota](/help/sites-cloud/authoring/page-editor/annotations.md) - Aggiungi o visualizza annotazioni nella pagina

>[!NOTE]
>
>* A seconda delle caratteristiche della pagina, alcune modalità potrebbero non essere disponibili.
>* L’accesso ad alcune modalità richiede le autorizzazioni/i privilegi appropriati.
>* La modalità Sviluppatore non è disponibile sui dispositivi mobili a causa di restrizioni di spazio.
>* La [scelta rapida da tastiera](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) (`Ctrl-Shift-M`) consente di passare da **Anteprima** alla modalità attualmente selezionata, ad esempio **Modifica**, **Layout** e così via.

#### Anteprima {#preview}

Il pulsante **Anteprima** abilita la modalità [anteprima](#preview-mode), in cui viene visualizzata la pagina così come verrà visualizzata al momento della pubblicazione.

![Pulsante Anteprima](assets/page-editor-preview.png)

#### Annotazioni {#annotate}

La modalità **Annota** consente di aggiungere [annotazioni](/help/sites-cloud/authoring/page-editor/annotations.md) alla pagina durante la revisione. Dopo la prima annotazione, l’icona viene sostituita da un numero che indica quante annotazioni sono presenti sulla pagina.

![Pulsante Annotazione](assets/page-editor-annotations.png)

### Pannello laterale {#side-panel}

Il pannello laterale consente di accedere a tre schede diverse.

* Browser componenti per aggiungere nuovi contenuti alla pagina
* Browser risorse per aggiungere nuove risorse alla pagina
* Struttura contenuto per sfogliare la struttura della pagina

![Pannello laterale dell&#39;editor di pagine](assets/page-editor-side-panel.png)

Per ulteriori informazioni, vedere il documento [Pannello laterale editor pagine](/help/sites-cloud/authoring/page-editor/editor-side-panel.md).

### Editor {#editor}

Nell’editor puoi apportare modifiche direttamente al contenuto della pagina. Il rendering della pagina viene eseguito come verrebbe visualizzato e puoi trascinare e rilasciare nuovi contenuti utilizzando le risorse o i browser dei componenti nel pannello laterale, nonché modificare i contenuti direttamente.

![Editor dell&#39;editor di pagine](assets/page-editor-editor.png)

## Modifica del contenuto {#editing-content}

Ora che conosci l’editor pagina, puoi modificare il contenuto.

Per ulteriori informazioni, vedere il documento [Modifica del contenuto con AEM Page Editor](/help/sites-cloud/authoring/page-editor/edit-content.md).

## Notifica di stato {#status-notification}

Se una pagina fa parte di un [flusso di lavoro](/help/sites-cloud/authoring/workflows/overview.md) o di più flussi di lavoro, queste informazioni vengono visualizzate in una barra di notifica sotto la barra degli strumenti durante la modifica della pagina.

![Notifica flusso di lavoro](assets/page-editor-editing-workflow-notification.png)

>[!NOTE]
>
>La barra di stato è visibile solo per gli account utente che dispongono dei diritti appropriati.

La notifica riporta il flusso di lavoro in esecuzione per la pagina. Se l’utente è coinvolto nella fase attuale del flusso di lavoro, sono anche disponibili opzioni per [modificare lo stato del flusso di lavoro](/help/sites-cloud/authoring/workflows/participating.md) e ottenere ulteriori informazioni sul flusso di lavoro, ad esempio:

* **Completa:** apre la finestra di dialogo **Completa elemento di lavoro**
* **Delega:** apre la finestra di dialogo **Completa elemento di lavoro**
* **Visualizza dettagli**: apre la finestra **Dettagli** del flusso di lavoro

Il completamento e la delega delle fasi del flusso di lavoro a partire dalla barra delle notifiche funzionano in modo analogo alla [partecipazione ai flussi di lavoro](/help/sites-cloud/authoring/workflows/participating.md) a partire dalla casella in entrata delle Notifiche.

Se la pagina è soggetta a più flussi di lavoro, il numero dei flussi di lavoro viene visualizzato all’estremità destra della notifica, insieme ai pulsanti freccia che consentono di scorrere i flussi di lavoro.

![Più notifiche flusso di lavoro](assets/page-editor-editing-workflow-notification-multiple.png)

## Stato della Live Copy   {#live-copy-status}

La modalità pagina **Stato Live Copy** offre una rapida panoramica dello stato della Live Copy e dei componenti che non vengono ereditati:

* Bordo verde: ereditato
* Bordo rosa: l’ereditarietà è stata annullata

Esempio:

![Esempio di visualizzazione stato Live Copy](assets/page-editor-editing-live-copy-status.png)

## Anteprima delle pagine {#previewing-pages}

Esistono due opzioni per visualizzare in anteprima una pagina:

* [Modalità anteprima](#preview-mode) - Anteprima rapida e diretta
* [Visualizza come pubblicato](#view-as-published) - Anteprima completa che apre la pagina in una nuova scheda

>[!TIP]
>
>* I collegamenti nel contenuto sono visibili, ma non accessibili in modalità **Modifica**.
>* Per effettuare la navigazione tramite i collegamenti, utilizza una delle opzioni di anteprima.
>* Utilizza la [scelta rapida da tastiera](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) `Ctrl-Shift-M` per passare dall’anteprima all’ultima modalità selezionata.

>[!NOTE]
>
>Il cookie della modalità WCM viene impostato per entrambe le opzioni di anteprima.

### Modalità Anteprima {#preview-mode}

Durante la modifica del contenuto è possibile visualizzare l’anteprima della pagina utilizzando la modalità di anteprima. Questa modalità:

* Nasconde vari meccanismi di modifica per fornire un’indicazione rapida di come apparirà la pagina una volta pubblicata.
* Consente di utilizzare i collegamenti per navigare.
* **Non** aggiorna il contenuto della pagina.

Durante l’authoring, la modalità di anteprima è disponibile utilizzando l’icona in alto a destra nell’editor di pagine:

![Pulsante Anteprima](assets/page-editor-preview.png)

### Visualizza come pubblicato {#view-as-published}

L’opzione **Visualizza come pubblicato**, è disponibile nel menu [Informazioni pagina](#page-information). Permette di aprire la pagina in una nuova scheda, aggiornando il contenuto e visualizzando la pagina esattamente come apparirebbe nell’ambiente di pubblicazione.

## Blocco e sblocco di una pagina {#locking-unlocking}

AEM consente di bloccare una pagina in modo che nessun altro possa modificarne il contenuto. Il blocco è utile quando si apportano numerose modifiche a una pagina specifica o quando è necessario bloccare una pagina per un breve periodo.

1. Seleziona l’icona **Informazioni pagina** per aprire il menu.
1. Seleziona l’opzione **Blocca pagina**.

Una volta bloccato, nella barra degli strumenti dell’editor pagina viene visualizzato un simbolo di blocco.

![Esempio di pagina bloccata](assets/page-editor-editing-locked-page.png)

Lo sblocco di una pagina è molto simile al [blocco della pagina](#locking-a-page). Una volta bloccata la pagina, le opzioni di blocco vengono sostituite da quelle di sblocco.

>[!CAUTION]
>
>* Il blocco di pagina può essere eseguito quando si impersona un utente. Tuttavia, una pagina bloccata in questo modo può essere sbloccata (dai clienti) solo utilizzando l’utente impersonato.
>* Non è consentito sbloccare le pagine bloccate impersonando l’utente che le ha boccate.
>* Se l’utente che ha bloccato la pagina non è disponibile per sbloccare la pagina, contatta l’Assistenza clienti per valutare le opzioni per rimuovere il blocco.

## Annullamento e ripristino di operazioni di modifica delle pagine {#undoing-and-redoing-page-edits}

Le icone seguenti consentono di annullare o ripristinare un’azione. Vengono visualizzate sulla barra degli strumenti quando necessario:

![Pulsanti Annulla e Ripristina](assets/page-editor-redo.png)

>[!TIP]
>
>* Per annullare le azioni di modifica della pagina è anche disponibile la [scelta rapida da tastiera](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md) `Ctrl-Z`.
>* Per ripristinare le azioni di modifica della pagina è anche disponibile la scelta rapida da tastiera `Ctrl-Y`.

>[!NOTE]
>
>Per informazioni sulle possibilità di annullare e ripristinare le modifiche apportate a una pagina, consulta il documento [Limitazioni per annullare e ripristinare](/help/sites-cloud/authoring/page-editor/undo-redo.md).
