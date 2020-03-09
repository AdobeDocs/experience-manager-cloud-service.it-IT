---
title: Ambiente e strumenti di authoring
description: L’ambiente di authoring di AEM offre diversi metodi per organizzare e modificare i contenuti
translation-type: ht
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Ambiente e strumenti di authoring {#authoring-the-environment-and-tools}

L’ambiente di authoring di AEM offre diversi metodi per organizzare e modificare i contenuti. Gli strumenti forniti sono accessibili dalle varie console ed editor di pagina.

## Gestione del sito {#managing-your-site}

La console **Sites** consente di navigare nel sito web e di gestirlo utilizzando la barra dell’intestazione, la barra degli strumenti, le icone delle azioni (per la risorsa selezionata), le breadcrumb e, se selezionate, le barre laterali secondarie (ad esempio Timeline e Riferimenti).

Ad esempio, nella vista a colonne:

![Vista a colonne](/help/sites-cloud/authoring/assets/column-view.png)

## Modifica del contenuto di una pagina {#editing-page-content}

Puoi modificare una pagina con l’editor di pagina. Esempio:

`http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

![Editor pagina](/help/sites-cloud/authoring/assets/page-editor.png)

>[!NOTE]
>
>La prima volta che apri una pagina per la modifica, una serie di diapositive illustra le funzioni disponibili.
>
>Puoi saltare questa presentazione introduttiva e richiamarla in qualsiasi momento dal menu **Informazioni pagina**.

## Accedere all’Aiuto   {#accessing-help}

Durante la modifica di una pagina, l’**Aiuto** è accessibile dalle seguenti aree:

* Il selettore [**Informazioni pagina **](/help/sites-cloud/authoring/fundamentals/page-properties.md#page-properties), che mostra le diapositive introduttive (così come visualizzate al primo accesso all’editor)
* La finestra di dialogo di [configurazione](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) per i componenti specifici (utilizzando l’icona ? presente nella barra degli strumenti della finestra di dialogo), che mostra la guida sensibile al contesto

Ulteriori [risorse di aiuto sono disponibili dalle console](/help/sites-cloud/authoring/getting-started/basic-handling.md#accessing-help).

## Browser Componenti   {#components-browser}

I componenti sono gli elementi costitutivi dei contenuti AEM. Per creare la pagina dei contenuti con AEM, posiziona più componenti su una pagina e configurane le relative opzioni .

Il browser Componenti mostra tutti i componenti disponibili per la pagina corrente. Puoi trascinarli nella posizione desiderata, quindi modificarli per aggiungere i contenuti richiesti.

Il browser Componenti è una scheda che si trova nel pannello laterale, insieme al [browser Risorse](#assets-browser) e alla [struttura dei contenuti](#content-tree). Per aprire (o chiudere) il pannello laterale utilizza l’icona in alto a sinistra della barra degli strumenti:

![Icona del pannello laterale](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

All’apertura, il pannello laterale scivolerà in posizione da sinistra (se necessario seleziona la scheda **Componenti**). Quando la scheda è aperta, puoi passare ai componenti disponibili per la pagina.

L’aspetto effettivo e il comportamento dipendono dal tipo di dispositivo in uso:

* **Dispositivo mobile (ad es. iPad)**

   Il browser Componenti copre completamente la pagina in corso di modifica.

   Per aggiungere un componente alla pagina, tocca e tieni premuto il componente richiesto e spostalo verso destra: il browser Componenti si chiude e torna a essere visibile la pagina, dove potrai posizionare il componente.

   ![Browser componenti per dispositivi mobili](/help/sites-cloud/authoring/assets/component-browser-mobile.png)

* **Dispositivo desktop**

   Il browser Componenti si apre nella parte sinistra della finestra.

   Per aggiungere un componente alla pagina, fai clic sul componente richiesto e trascinalo nella posizione desiderata.

   ![Browser componenti per desktop](/help/sites-cloud/authoring/assets/component-browser-desktop.png)

   I componenti sono rappresentati da

   * Nome componente
   * Gruppo di componenti (in grigio)
   * Icona o abbreviazione
      * Le icone dei componenti standard sono monocromatiche.
      * Le abbreviazioni sono sempre i primi due caratteri del nome del componente.
   Dalla barra degli strumenti nella parte superiore del browser **Componenti**, puoi effettuare le seguenti operazioni:

   * Filtrare i componenti per nome
   * Limitare la visualizzazione a uno specifico gruppo selezionandolo dall’elenco a discesa
   Per una descrizione più dettagliata del componente, tocca o fai clic sull’icona delle informazioni accanto al componente nel browser **Componenti** (se disponibile). Ad esempio, per il **frammento di contenuto**:

   ![Informazioni sul browser Componenti](/help/sites-cloud/authoring/assets/component-browser-information.png)

   Per ulteriori informazioni sui componenti disponibili, consulta la sezione sulla [console Componenti](/help/sites-cloud/authoring/features/components-console.md).

>[!NOTE]
>
>Un dispositivo viene rilevato come mobile se la larghezza è inferiore a 1024 px. Ciò può applicarsi anche a una piccola finestra desktop.

## Browser Risorse {#assets-browser}

Il browser Risorse mostra tutte le risorse disponibili per la pagina corrente. <!--The assets browser shows all [assets](/help/assets/home.md) that are available for direct use on your current page.-->

Il browser Risorse è una scheda che si trova nel pannello laterale, insieme al [browser Componenti](#components-browser) e alla [struttura dei contenuti](#content-tree). Per aprire o chiudere il pannello laterale utilizza l’icona in alto a sinistra della barra degli strumenti:

![Icona del pannello laterale](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

All’apertura, il pannello laterale scivolerà in posizione da sinistra. Se necessario seleziona la scheda **Risorse**.

![Pulsante Browser risorse](/help/sites-cloud/authoring/assets/assets-browser-button.png)

Quando il browser Risorse è aperto, puoi sfogliare tutte le risorse disponibili per la pagina. Per espandere l’elenco, scorri in base alle necessità.

![Browser Risorse](/help/sites-cloud/authoring/assets/assets-browser.png)

Per aggiungere una risorsa alla pagina, selezionala e trascinala nella posizione desiderata. Questa può essere:

* Un componente esistente del tipo appropriato.
   * Ad esempio, puoi trascinare una risorsa di tipo immagine su un componente Immagine.
* Un [segnaposto](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-placeholder) nel sistema paragrafo per creare un nuovo componente di tipo appropriato.
   * Ad esempio, puoi trascinare una risorsa di tipo immagine nel sistema paragrafo per creare un componente Immagine.

>[!NOTE]
>
>Questo è disponibile per risorse e tipi di componenti specifici. Per ulteriori informazioni, consulta [Inserimento di un componente utilizzando il browser Risorse](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component-using-the-assets-browser).

Dalla barra degli strumenti nella parte superiore del browser Risorse è possibile filtrare le risorse in base ai seguenti criteri:

* Nome
* Percorso
* Tipo di risorsa come: immagini, video, documenti, paragrafi, frammenti di contenuto e frammenti esperienza
* Caratteristiche della risorsa, ad esempio orientamento e stile
   * Disponibile solo per alcuni tipi di risorsa

L’aspetto effettivo e il comportamento dipendono dal tipo di dispositivo in uso:

* **Dispositivo mobile**

   Il browser Risorse occupa completamente la pagina in corso di modifica.

   Per aggiungere una risorsa alla pagina, tocca e tieni premuto sulla risorsa richiesta e spostala verso destra: il browser Risorse si chiude e torna a essere visibile la pagina, dove potrai aggiungere la risorsa al componente richiesto.

   ![Browser risorse per dispositivi mobili](/help/sites-cloud/authoring/assets/assets-browser-mobile.png)

* **Dispositivo desktop**

   Il browser Risorse si apre nella parte sinistra della finestra.

   Per aggiungere una risorsa alla pagina, fai clic sulla risorsa richiesta e trascinala sul componente o nella posizione desiderata.

   ![Browser risorse sul desktop](/help/sites-cloud/authoring/assets/assets-browser-desktop.png)

>[!NOTE]
>
>Un dispositivo viene rilevato come mobile se la larghezza è inferiore a 1024 px (quindi anche una piccola finestra desktop).

Se devi apportare rapidamente una modifica a una risorsa, puoi avviare l’editor risorse direttamente dal browser Risorse facendo clic sull’icona Modifica accanto al nome della risorsa. <!--If you need to quickly make a change to an asset, you can start the [asset editor](/help/assets/manage-digital-assets.md) directly from the asset browser by clicking the edit icon shown next to the asset's name.-->

![Pulsante Modifica risorsa](/help/sites-cloud/authoring/assets/asset-edit-button.png)

## Struttura contenuto {#content-tree}

La scheda **Struttura contenuto** offre una panoramica di tutti i componenti nella pagina sotto forma di struttura gerarchica ad albero, che permette di vedere subito come è composta la pagina.

Struttura contenuto è una scheda che si trova nel pannello laterale, insieme ai browser Componenti e Risorse. Per aprire (o chiudere) il pannello laterale utilizza l’icona in alto a sinistra della barra degli strumenti:

![Pulsante Struttura contenuto](/help/sites-cloud/authoring/assets/content-tree-button.png)

Quando apri il pannello laterale, questo si apre scorrendo dal lato sinistro. Se necessario, seleziona la scheda **Struttura contenuto**. Una volta aperta è possibile visualizzare una struttura ad albero della pagina o del modello, che permette di capire come il contenuto è strutturato gerarchicamente. Inoltre, in una pagina complessa rende più facile passare tra i vari componenti della pagina.

![Struttura contenuto](/help/sites-cloud/authoring/assets/content-tree-editor.png)

Poiché una pagina può essere composta da numerosi componenti dello stesso tipo, la struttura del contenuto (componente) presenta un testo descrittivo (in grigio) dopo il nome del tipo di componente (in nero). Il testo descrittivo è composto dalle proprietà comuni del componente, come ad esempio il titolo o il testo.

I tipi di componente sono indicati nella lingua preferita dall&#39;utente, mentre il testo descrittivo del componente nella lingua della pagina.

Fai clic sulla freccia accanto a un componente per comprimere o espandere il livello.

![Freccia di espansione Struttura contenuto](/help/sites-cloud/authoring/assets/content-tree-chevron.png)

Fai clic sul componente per evidenziarlo nell’editor di pagine. Le azioni disponibili dipendono dallo stato della pagina:

* Ad esempio, una pagina base:

   ![Struttura contenuto evidenziata](/help/sites-cloud/authoring/assets/content-tree-highlighted.png)

   I componenti di una pagina di base avranno le consuete opzioni.

   Se il componente su cui fai clic nella struttura ad albero è modificabile, a destra del nome compare un’icona a forma di chiave inglese. Fai clic su questa icona per avviare direttamente la finestra di dialogo di modifica del componente.

   ![Pulsante modifica Struttura contenuto](/help/sites-cloud/authoring/assets/content-tree-edit.png)

* Una pagina che fa parte di una Live Copy, in cui i componenti vengono ereditati da un’altra pagina, dispone di una selezione ridotta di opzioni, comprese quelle di ereditarietà. <!--A page that is part of a [livecopy](/help/sites-administering/msm.md), where components are inherited from another page:-->

>[!NOTE]
>
>La struttura del contenuto non è disponibile quando si modifica una pagina su un dispositivo mobile (se la larghezza del browser è inferiore a 1024 px).

## Frammenti - Browser Contenuto associato {#fragments-associated-content-browser}

Se la pagina contiene frammenti di contenuto, avrai accesso anche al [browser Contenuto associato](/help/sites-cloud/authoring/fundamentals/content-fragments.md#using-associated-content).

## Riferimenti {#references}

I **riferimenti** mostrano i collegamenti alla pagina selezionata:

* Blueprint
* Lanci
* Live Copy
* Copie per lingua
* Collegamenti in entrata
* Uso del componente di riferimento: contenuto prestato e preso in prestito

Apri la console richiesta, quindi accedi alla risorsa desiderata e apri i **Riferimenti** utilizzando:

![Opzione Riferimenti](/help/sites-cloud/authoring/assets/references.png)

[Seleziona la risorsa richiesta](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) per visualizzare un elenco dei tipi di riferimenti relativi a tale risorsa:

![Dettagli riferimenti](/help/sites-cloud/authoring/assets/references-detail.png)

Seleziona il tipo di riferimento adeguato per ulteriori informazioni. In determinate situazioni sono disponibili azioni ulteriori quando viene selezionato un riferimento specifico, inclusi:

* **Collegamenti in entrata**: fornisce un elenco di pagine che fanno riferimento a una data pagina, insieme all’accesso diretto alla funzione di **Modifica** di una di queste pagine quando selezioni un collegamento specifico.
* Istanze di contenuto prestato o preso in prestito mediante il componente **Riferimento**: da qui puoi passare alla pagina di riferimento o a cui si fa riferimento.
* [Lanci](/help/sites-cloud/authoring/launches/overview.md): fornisce accesso ai lanci correlati.
* Live Copy visualizza i percorsi di tutte le Live Copy basate sulla risorsa selezionata. <!--[Live Copies](/help/sites-administering/msm.md) displays the paths of all live copies that are based on the selected resource.-->
* Blueprint fornisce dettagli e varie azioni <!--[Blueprint](/help/sites-administering/msm-best-practices.md), provides details and various actions-->
* Copie per lingua: fornisce dettagli e varie azioni. <!--[Languages Copies](/help/sites-administering/tc-manage.md#creating-translation-projects-using-the-references-panel), provides details and various actions-->

## Eventi - Timeline {#events-timeline}

Per le risorse appropriate (ad esempio, pagine dalla console **Sites** o risorse dalla console **Risorse**) è possibile [utilizzare la timeline per visualizzare le attività recenti relative agli elementi selezionati](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline).

Apri la console richiesta, quindi accedi alla risorsa desiderata e apri la **Timeline** utilizzando:

![Opzione Timeline](/help/sites-cloud/authoring/assets/timeline.png)

[Scegli la risorsa desiderata](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources), quindi seleziona **Mostra tutto** o **Attività** per ottenere un elenco delle azioni recenti relative alle risorse selezionate:

![Dettagli Timeline](/help/sites-cloud/authoring/assets/timeline-detail.png)

## Informazioni sulle pagine {#page-information}

Informazioni pagina (icona equalizzatore) mostra un menu che fornisce anche dettagli sull’ultima operazione di modifica e di pubblicazione. A seconda delle caratteristiche della pagina, del sito e delle istanze, potrebbero essere disponibili più o meno opzioni:

![Opzione Informazioni pagina](/help/sites-cloud/authoring/assets/page-information.png)

* [Apri proprietà](/help/sites-cloud/authoring/fundamentals/page-properties.md)
* Rollout pagina <!--[Rollout Page](/help/sites-administering/msm.md#msm-from-the-ui)-->
* [Avvia flusso di lavoro](/help/sites-cloud/authoring/workflows/applying.md#starting-a-workflow-from-the-page-editor)
* [Blocca pagina](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page)
* [Pubblica pagina](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#publishing-pages-1)
* [Annulla pubblicazione pagina](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages)
* [Modifica modello](/help/sites-cloud/authoring/features/templates.md)
* [Visualizza come pubblicato](/help/sites-cloud/authoring/fundamentals/editing-content.md#view-as-published)
* [Visualizza in Amministrazione](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)
* [Aiuto](/help/sites-cloud/authoring/getting-started/basic-handling.md#accessing-help)
* [Promuovi lancio:](/help/sites-cloud/authoring/launches/promoting.md) (solo se la pagina è un lancio)

Inoltre, da **Informazioni pagina** è possibile accedere ad analisi e consigli.

## Modalità pagina   {#page-modes}

Quando si modifica una pagina sono disponibili varie modalità che consentono di configurare diverse azioni:

* [Modifica](/help/sites-cloud/authoring/fundamentals/editing-content.md): modalità da utilizzare per modificare il contenuto della pagina.
* [Layout](/help/sites-cloud/authoring/features/responsive-layout.md): consente di creare e modificare il layout dinamico a seconda del dispositivo (se la pagina si basa su un contenitore di layout).
* [Impostazione destinazione](/help/sites-cloud/authoring/personalization/targeted-content.md): consente di incrementare la rilevanza dei contenuti tramite il targeting e la misurazione su tutti i canali.
* [Timewarp](/help/sites-cloud/authoring/features/page-versions.md#timewarp): consente di visualizzare lo stato delle pagine in un particolare momento.
* [Stato Live Copy](/help/sites-cloud/authoring/fundamentals/editing-content.md#live-copy-status): consente di visualizzare una panoramica rapida dello stato della live copy e dei componenti ereditati e non.
* [Anteprima](/help/sites-cloud/authoring/fundamentals/editing-content.md#previewing-pages): utilizzato per visualizzare l’aspetto che la pagina avrà nell’ambiente di pubblicazione o per spostarsi utilizzando i collegamenti presenti nel contenuto.
* [Annota](/help/sites-cloud/authoring/fundamentals/annotations.md): utilizzato per aggiungere o visualizzare annotazioni nella pagina.

Puoi accedere a questi elementi mediante l’icona nell’angolo in alto a destra, il cui aspetto dipende dalla modalità attualmente in uso:

![Modalità pagina](/help/sites-cloud/authoring/assets/page-modes.png)

>[!NOTE]
>
>* A seconda delle caratteristiche della pagina, alcune modalità possono non essere disponibili.
>* L’accesso ad alcune modalità richiede autorizzazioni o privilegi adeguati.
>* La modalità Sviluppatore non è disponibile su dispositivi mobili a causa di limitazioni di spazio.
>* La [scelta rapida da tastiera](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `Ctrl-Shift-M` consente di passare da **Anteprima** alla modalità attualmente selezionata (ad esempio **Modifica**, **Layout** e così via) e viceversa.
>



## Selezione del percorso {#path-selection}

Spesso per l’authoring è necessario selezionare un’altra risorsa, ad esempio quando si definisce un collegamento a un’altra pagina o risorsa o si seleziona un’immagine. Per selezionare facilmente un percorso, i [campi percorso](#path-fields) offrono una funzione di auto-completamento e il [browser Percorsi](#path-browser) consente una selezione più affidabile.

### Campi percorso   {#path-fields}

L’esempio utilizzato qui mostra il Componente immagine. Per ulteriori informazioni sull’utilizzo e la modifica dei componenti consulta [Componenti per l’authoring di pagine](/help/sites-cloud/authoring/fundamentals/components.md).

I campi percorso dispongono della funzione di completamento automatico e di look-ahead per rendere più facile individuare una risorsa.

Fai clic sul pulsante **Apri finestra di dialogo per selezione** nel campo percorso per aprire la finestra di dialogo del [browser Percorsi](#path-browser) e utilizzare opzioni di selezione più dettagliate.

![Pulsante Apri finestra di dialogo per selezione](/help/sites-cloud/authoring/assets/open-selection-dialog-button.png)

Oppure puoi iniziare a digitare nel campo percorso e AEM fornirà i percorsi corrispondenti mentre digiti.

![Pulsante Apri finestra di dialogo per selezione](/help/sites-cloud/authoring/assets/path-selection-completion.png)

### Browser Percorsi {#path-browser}

Il browser Percorsi è organizzato come la [vista a colonne](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view) della console Sites e permette di selezionare le risorse in modo più dettagliato.

![Browser Percorsi](/help/sites-cloud/authoring/assets/path-browser.png)

* Una volta che la risorsa è selezionata, il pulsante **Seleziona** in alto a destra nella finestra di dialogo diventa attivo. Tocca o fai clic su questo pulsante per confermare la selezione oppure su **Annulla** per annullare l’operazione.
* Se il contesto consente di selezionare più risorse, la selezione di una risorsa attiva il pulsante **Seleziona** e inoltre viene visualizzato il numero di risorse selezionate in alto a destra nella finestra. Fai clic sulla **X** accanto al numero per deselezionare tutte le risorse.
* Quando navighi attraverso la struttura ad albero, la posizione viene riportata nelle breadcrumb nella parte superiore della finestra di dialogo. Le breadcrumb possono anche essere utilizzate per passare rapidamente alla gerarchia delle risorse.
* In qualsiasi momento puoi usare il campo di ricerca nella parte superiore della finestra di dialogo. Fai clic sulla **X** nel campo di ricerca per cancellare la ricerca.
* Per limitare l’ambito della ricerca, puoi visualizzare le opzioni filtro e filtrare il risultato in base a un determinato percorso.

   ![Opzione Filtri](/help/sites-cloud/authoring/assets/filters-option.png)

## Scelte rapide da tastiera {#keyboard-shortcuts}

Sono disponibili alcune [scelte rapide da tastiera](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md).
