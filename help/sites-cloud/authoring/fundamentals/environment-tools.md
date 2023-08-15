---
title: Ambiente e strumenti di authoring
description: L’ambiente di authoring di AEM offre diversi metodi per organizzare e modificare i contenuti
exl-id: cc3bd4cf-93bd-429d-9a2a-4a02a7b42f7c
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '2150'
ht-degree: 57%

---

# Ambiente e strumenti di authoring {#authoring-the-environment-and-tools}

L’ambiente di authoring di AEM offre diversi metodi per organizzare e modificare i contenuti. Gli strumenti disponibili sono accessibili da varie console ed editor di pagina.

## Gestione del sito {#managing-your-site}

Il **Sites** console consente di navigare nel sito web e di gestirlo mediante la barra intestazione, la barra degli strumenti, le icone delle azioni (per la risorsa selezionata), le breadcrumb e, se selezionate, le barre laterali secondarie (ad esempio Timeline e Riferimenti).

Ad esempio, nella vista a colonne:

![Vista a colonne](/help/sites-cloud/authoring/assets/column-view.png)

## Modifica del contenuto di una pagina {#editing-page-content}

Puoi modificare una pagina con l’editor pagina. Esempio:

`http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

![Editor pagina](/help/sites-cloud/authoring/assets/page-editor.png)

>[!NOTE]
>
>La prima volta che apri una pagina per la modifica, una serie di diapositive ti forniranno una panoramica delle funzioni.
>
>Se necessario, puoi saltare la presentazione e ripeterla in qualsiasi momento selezionando una delle seguenti opzioni **Informazioni pagina** menu.

## Accedere all’Aiuto   {#accessing-help}

Durante la modifica di una pagina, l’**Aiuto** è accessibile dalle seguenti aree:

* Il selettore [**Informazioni pagina**](/help/sites-cloud/authoring/fundamentals/page-properties.md#page-properties), che mostra le diapositive introduttive (così come visualizzate al primo accesso all’editor)
* La finestra di dialogo di [configurazione](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-toolbar) per i componenti specifici (utilizzando l’icona ? presente nella barra degli strumenti della finestra di dialogo), che mostra la guida sensibile al contesto

Ulteriori informazioni [le risorse relative alla guida sono disponibili nelle console](/help/sites-cloud/authoring/getting-started/basic-handling.md#accessing-help).

## Browser Componenti   {#components-browser}

I componenti sono gli elementi costitutivi dei contenuti AEM. Posiziona più componenti su una pagina e configurane le opzioni per creare la pagina dei contenuti con AEM.

Il browser Componenti mostra tutti i componenti disponibili per la pagina corrente. Questi possono essere trascinati nella posizione appropriata, quindi modificati per aggiungere il contenuto.

Il browser Componenti è una scheda che si trova nel pannello laterale, insieme al [browser Risorse](#assets-browser) e alla [struttura dei contenuti](#content-tree). Per aprire (o chiudere) il pannello laterale utilizza l’icona in alto a sinistra della barra degli strumenti:

![Icona del pannello laterale](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

Quando apri il pannello laterale, questo si apre scorrendo dal lato sinistro (seleziona la **Componenti** (se necessario). Una volta aperta, è possibile sfogliare tutti i componenti disponibili per la pagina.

L&#39;aspetto e la gestione effettivi dipendono dal tipo di dispositivo in uso:

* **Dispositivo mobile (ad esempio iPad)**

  Il browser Componenti copre completamente la pagina in fase di modifica.

  Per aggiungere un componente alla pagina, tocca e tieni premuto il componente richiesto e spostalo verso destra (il browser componenti si chiude per mostrare nuovamente la pagina), dove puoi posizionare il componente.

  ![Browser componenti per dispositivi mobili](/help/sites-cloud/authoring/assets/component-browser-mobile.png)

* **Dispositivo desktop**

  Il browser Componenti viene aperto sul lato sinistro della finestra.

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
   * Limita la visualizzazione a un gruppo specifico utilizzando la selezione a discesa.

  Per una descrizione più dettagliata del componente, tocca o fai clic sull’icona delle informazioni posta accanto al componente nel browser **Componenti** (se disponibile). Ad esempio, per il **frammento di contenuto**:

  ![Informazioni sul browser Componenti](/help/sites-cloud/authoring/assets/component-browser-information.png)

  Per ulteriori informazioni sui componenti disponibili, consulta la sezione sulla [console Componenti](/help/sites-cloud/authoring/features/components-console.md).

>[!NOTE]
>
>Un dispositivo viene rilevato come mobile se la larghezza è inferiore a 1024 px. Questo può essere anche il caso di una piccola finestra del desktop.

## Browser Risorse {#assets-browser}

Il browser Risorse mostra tutto [risorse](/help/assets/home.md) che sono disponibili per l’uso diretto nella pagina corrente.

Il browser Risorse è una scheda che si trova nel pannello laterale, insieme al [browser Componenti](#components-browser) e alla [struttura dei contenuti](#content-tree). Per aprire o chiudere il pannello laterale utilizza l’icona in alto a sinistra della barra degli strumenti:

![Icona del pannello laterale](/help/sites-cloud/authoring/assets/side-panel-toggle.png)

All’apertura, il pannello laterale scivolerà in posizione da sinistra. Se necessario seleziona la scheda **Risorse**.

![Pulsante Browser risorse](/help/sites-cloud/authoring/assets/assets-browser-button.png)

Quando il browser Risorse è aperto, puoi sfogliare tutte le risorse disponibili per la pagina. Se necessario, per espandere l&#39;elenco viene utilizzato lo scorrimento infinito.

![Browser Risorse](/help/sites-cloud/authoring/assets/assets-browser.png)

Per aggiungere una risorsa alla pagina, selezionala e trascinala nella posizione desiderata. Può trattarsi di:

* Un componente esistente del tipo appropriato.
   * Ad esempio, puoi trascinare una risorsa di tipo immagine su un componente Immagine.
* Un [segnaposto](/help/sites-cloud/authoring/fundamentals/editing-content.md#component-placeholder) nel sistema paragrafo per creare un nuovo componente di tipo appropriato.
   * Ad esempio, puoi trascinare una risorsa di tipo immagine nel sistema paragrafo per creare un componente Immagine.

>[!NOTE]
>
>Questa funzione è disponibile per risorse e tipi di componenti specifici. Consulta [Inserimento di un componente tramite il browser Risorse](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component-using-the-assets-browser) per ulteriori dettagli.

Dalla barra degli strumenti nella parte superiore del browser Risorse puoi filtrare le risorse in base a:

* Nome
* Percorso
* Tipo di risorsa come: immagini, video, documenti, paragrafi, frammenti di contenuto e frammenti esperienza
* Caratteristiche della risorsa, ad esempio orientamento e stile
   * Disponibile solo per alcuni tipi di risorse

L&#39;aspetto e la gestione effettivi dipendono dal tipo di dispositivo in uso:

* **Dispositivo mobile**

  Il browser Risorse copre completamente la pagina in fase di modifica.

  Per aggiungere una risorsa alla pagina, tocca e tieni premuto sulla risorsa richiesta, quindi spostala verso destra: il browser Risorse si chiude per mostrare di nuovo la pagina, dove puoi aggiungere la risorsa al componente richiesto.

  ![Browser risorse per dispositivi mobili](/help/sites-cloud/authoring/assets/assets-browser-mobile.png)

* **Dispositivo desktop**

  Il browser Risorse viene aperto sul lato sinistro della finestra.

  Per aggiungere una risorsa alla pagina, fai clic sulla risorsa richiesta e trascinala sul componente o sulla posizione desiderata.

  ![Browser risorse sul desktop](/help/sites-cloud/authoring/assets/assets-browser-desktop.png)

>[!NOTE]
>
>Un dispositivo mobile viene rilevato quando la larghezza è inferiore a 1024 px, ovvero anche su una piccola finestra del desktop.

Se devi apportare rapidamente una modifica a una risorsa, puoi avviare [l’editor risorse](/help/assets/manage-digital-assets.md) direttamente dal browser Risorse facendo clic sull&#39;icona Modifica accanto al nome della risorsa.

![Pulsante Modifica risorsa](/help/sites-cloud/authoring/assets/asset-edit-button.png)

## Struttura contenuto {#content-tree}

Il **Struttura contenuto** offre una panoramica di tutti i componenti della pagina in una gerarchia, per consentirti di visualizzare rapidamente come viene composta la pagina.

Struttura contenuto è una scheda che si trova nel pannello laterale, insieme ai browser Componenti e Risorse. Per aprire (o chiudere) il pannello laterale utilizza l’icona in alto a sinistra della barra degli strumenti:

![Pulsante Struttura contenuto](/help/sites-cloud/authoring/assets/content-tree-button.png)

Quando apri il pannello laterale, questo si apre scorrendo dal lato sinistro. Se necessario, seleziona la scheda **Struttura contenuto**. Una volta aperta è possibile visualizzare una struttura ad albero della pagina o del modello, che permette di capire come il contenuto è strutturato gerarchicamente. Inoltre, in una pagina complessa, consente di spostarsi più facilmente tra i componenti della pagina.

![Struttura contenuto](/help/sites-cloud/authoring/assets/content-tree-editor.png)

Poiché una pagina può essere composta da numerosi componenti dello stesso tipo, la struttura del contenuto (componente) presenta un testo descrittivo (in grigio) dopo il nome del tipo di componente (in nero). Il testo descrittivo proviene da proprietà comuni del componente, ad esempio titolo o testo.

I tipi di componente vengono visualizzati nella lingua dell’utente, mentre il testo della descrizione del componente proviene dalla lingua della pagina.

Facendo clic sulla freccia accanto a un componente, questo livello viene compresso o espanso.

![Freccia di espansione Struttura contenuto](/help/sites-cloud/authoring/assets/content-tree-chevron.png)

Facendo clic sul componente, questo viene evidenziato nell’editor pagina. Le azioni disponibili dipendono dallo stato della pagina:

* Ad esempio, una pagina di base:

  ![Struttura contenuto evidenziata](/help/sites-cloud/authoring/assets/content-tree-highlighted.png)

  I componenti di una pagina di base avranno le consuete opzioni.

  Se il componente su cui fai clic nella struttura ad albero è modificabile, a destra del nome compare un’icona a forma di chiave inglese. Facendo clic su questa icona si avvia direttamente la finestra di dialogo di modifica del componente.

  ![Pulsante modifica Struttura contenuto](/help/sites-cloud/authoring/assets/content-tree-edit.png)

* Oppure una pagina che fa parte di una [live copy](/help/sites-cloud/administering/msm/overview.md), dove i componenti vengono ereditati da un’altra pagina, ad esempio.

>[!NOTE]
>
>La struttura del contenuto non è disponibile quando si modifica una pagina su un dispositivo mobile (se la larghezza del browser è inferiore a 1024 px).

## Frammenti - Browser Contenuto associato {#fragments-associated-content-browser}

Se la pagina contiene frammenti di contenuto, avrai accesso anche al [browser Contenuto associato](/help/sites-cloud/authoring/fundamentals/content-fragments.md#using-associated-content).

## Riferimenti {#references}

**Riferimenti** mostra le connessioni alla pagina selezionata:

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
* [Live Copy](/help/sites-cloud/administering/msm/overview.md) visualizza i percorsi di tutte le Live Copy basate sulla risorsa selezionata.
* [Blueprint](/help/sites-cloud/administering/msm/best-practices.md) fornisce dettagli e varie azioni
* [Copie per lingua](/help/sites-cloud/administering/translation/managing-projects.md#creating-translation-projects-using-the-references-panel): fornisce dettagli e varie azioni

## Eventi - Timeline {#events-timeline}

Per le risorse appropriate (ad esempio, pagine dalla console **Sites** o risorse dalla console **Assets**) è possibile utilizzare la [timeline per visualizzare le attività recenti relative agli elementi selezionati](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline).

Apri la console richiesta, quindi accedi alla risorsa desiderata e apri la **Timeline** utilizzando:

![Opzione Timeline](/help/sites-cloud/authoring/assets/timeline.png)

[Scegli la risorsa desiderata](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources), quindi seleziona **Mostra tutto** o **Attività** per ottenere un elenco delle azioni recenti relative alle risorse selezionate:

![Dettagli Timeline](/help/sites-cloud/authoring/assets/timeline-detail.png)

## Informazioni sulle pagine {#page-information}

Informazioni pagina (icona equalizzatore) mostra un menu che fornisce anche dettagli sull’ultima operazione di modifica e di pubblicazione. A seconda delle caratteristiche della pagina, del sito e delle istanze, potrebbero essere disponibili più o meno opzioni:

![Opzione Informazioni pagina](/help/sites-cloud/authoring/assets/page-information.png)

* [Apri proprietà](/help/sites-cloud/authoring/fundamentals/page-properties.md)
* [Rollout pagina](/help/sites-cloud/administering/msm/overview.md#msm-from-the-ui)
* [Avvia flusso di lavoro](/help/sites-cloud/authoring/workflows/applying.md#starting-a-workflow-from-the-page-editor)
* [Blocca pagina](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page)
* [Pubblica pagina](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#publishing-pages-1)
* [Annulla pubblicazione pagina](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages)
* [Modifica modello](/help/sites-cloud/authoring/features/templates.md)
* [Visualizza come pubblicato](/help/sites-cloud/authoring/fundamentals/editing-content.md#view-as-published)
* [Visualizza in Amministrazione](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)
* [Aiuto](/help/sites-cloud/authoring/getting-started/basic-handling.md#accessing-help)
* [Promuovi lancio:](/help/sites-cloud/authoring/launches/promoting.md) (solo se la pagina è un lancio)

Inoltre, **Informazioni pagina** può fornire accesso ad analytics e alle raccomandazioni, quando appropriato.

## Modalità pagina   {#page-modes}

Esistono diverse modalità di modifica di una pagina che consentono di eseguire azioni diverse:

* [Modifica](/help/sites-cloud/authoring/fundamentals/editing-content.md) : modalità da utilizzare per la modifica del contenuto della pagina.
* [Layout](/help/sites-cloud/authoring/features/responsive-layout.md) : consente di creare e modificare il layout dinamico a seconda del dispositivo (se la pagina si basa su un contenitore di layout)
* [Targeting](/help/sites-cloud/authoring/personalization/targeted-content.md) - aumentare la rilevanza dei contenuti attraverso il targeting e la misurazione su tutti i canali.
* [Timewarp](/help/sites-cloud/authoring/features/page-versions.md#timewarp) : consente di visualizzare lo stato di una pagina in un determinato momento.
* [Stato Live Copy](/help/sites-cloud/authoring/fundamentals/editing-content.md#live-copy-status) : consente di ottenere una rapida panoramica dello stato della live copy e dei componenti che non vengono ereditati.
* [Modalità Sviluppatore](/help/implementing/developing/tools/developer-mode.md)
* [Anteprima](/help/sites-cloud/authoring/fundamentals/editing-content.md#previewing-pages) : utilizzato per visualizzare l’aspetto che la pagina ha nell’ambiente di pubblicazione o per spostarsi utilizzando i collegamenti presenti nel contenuto.
* [Annota](/help/sites-cloud/authoring/fundamentals/annotations.md): utilizzato per aggiungere o visualizzare annotazioni nella pagina.

Puoi accedere a questi elementi mediante l’icona nell’angolo in alto a destra, il cui aspetto dipende dalla modalità attualmente in uso:

![Modalità pagina](/help/sites-cloud/authoring/assets/page-modes.png)

>[!NOTE]
>
>* A seconda delle caratteristiche della pagina, alcune modalità potrebbero non essere disponibili.
>* L’accesso ad alcune modalità richiede le autorizzazioni/i privilegi appropriati.
>* La modalità Sviluppatore non è disponibile sui dispositivi mobili a causa di restrizioni di spazio.
>* La [scelta rapida da tastiera](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) (`Ctrl-Shift-M`) consente di passare da **Anteprima** alla modalità attualmente selezionata (ad esempio **Modifica**, **Layout** e così via) e viceversa.
>

## Selezione del percorso {#path-selection}

Spesso per l’authoring è necessario selezionare un’altra risorsa, ad esempio quando si definisce un collegamento a un’altra pagina o risorsa o si seleziona un’immagine. Per selezionare facilmente un percorso: [campi percorso](#path-fields) offerta di completamento automatico e il [browser percorsi](#path-browser) consente una selezione più solida.

### Campi percorso   {#path-fields}

L’esempio utilizzato qui mostra il Componente immagine. Per ulteriori informazioni sull&#39;utilizzo e la modifica dei componenti, consulta [Componenti per l’authoring delle pagine](/help/sites-cloud/authoring/fundamentals/components.md).

I campi percorso dispongono della funzione di completamento automatico e di look-ahead per rendere più facile individuare una risorsa.

Fai clic sul pulsante **Apri finestra di dialogo per selezione** nel campo percorso per aprire la finestra di dialogo del [browser Percorsi](#path-browser) e utilizzare opzioni di selezione più dettagliate.

![Pulsante Apri finestra di dialogo per selezione](/help/sites-cloud/authoring/assets/open-selection-dialog-button.png)

Oppure puoi iniziare a digitare nel campo percorso e AEM fornirà i percorsi corrispondenti mentre digiti.

![Pulsante Apri finestra di dialogo per selezione](/help/sites-cloud/authoring/assets/path-selection-completion.png)

### Browser Percorsi {#path-browser}

Il browser Percorsi è organizzato come la [vista a colonne](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view) della console Sites e permette di selezionare le risorse in modo più dettagliato.

![Browser Percorsi](/help/sites-cloud/authoring/assets/path-browser.png)

* Una volta selezionata una risorsa, **Seleziona** in alto a destra nella finestra di dialogo diventa attivo. Tocca o fai clic per confermare la selezione oppure **Annulla** per interrompere.
* Se il contesto consente la selezione di più risorse, la scelta di una risorsa attiva anche il pulsante **Seleziona**, ma aggiunge anche un conteggio del numero di risorse selezionate nella parte superiore destra della finestra. Per deselezionare tutti gli elementi, fai clic sulla **X** accanto al numero.
* Quando ti sposti nella struttura, la posizione si riflette nelle breadcrumb nella parte superiore della finestra di dialogo. Queste breadcrumb possono essere utilizzate anche per passare rapidamente all’interno della gerarchia delle risorse.
* In qualsiasi momento puoi utilizzare il campo di ricerca nella parte superiore della finestra di dialogo. Fai clic su **X** nel campo di ricerca per cancellare la ricerca.
* Per limitare l’ambito della ricerca, puoi visualizzare le opzioni filtro e filtrare il risultato in base a un determinato percorso.

  ![Opzione Filtri](/help/sites-cloud/authoring/assets/filters-option.png)

## Scelte rapide da tastiera {#keyboard-shortcuts}

Sono disponibili alcune [scelte rapide da tastiera](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md).
