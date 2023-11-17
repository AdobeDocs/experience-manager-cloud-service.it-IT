---
title: Operazioni di base
description: Acquisisci dimestichezza con AEM e il suo utilizzo di base
exl-id: ae87a63a-c6d3-4220-ab3d-07a20b21b93b
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '2943'
ht-degree: 91%

---


# Operazioni di base {#basic-handling}

Questo documento offre una panoramica delle operazioni di base nell’ambiente di authoring di AEM. Usa la console **Sites** come base.

>[!NOTE]
>
>* Alcune funzionalità non sono disponibili in tutte le console e in alcune console potrebbero essere disponibili funzionalità aggiuntive. In altre sezioni sono descritte più dettagliatamente le informazioni specifiche sulle singole console e sulle relative funzionalità.
>* AEM supporta l’utilizzo di scelte rapide da tastiera in numerose aree, in particolare per l’[utilizzo delle console](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) e la [modifica delle pagine](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md).

{{edge-delivery-authoring}}

## Interfaccia touch {#a-touch-enabled-ui}

L’interfaccia utente di AEM è dotata di funzionalità touch. L&#39;interfaccia touch consente di interagire con il software tramite gesti quali toccare, tenere premuto e scorrere. Poiché l’interfaccia utente di AEM è di tipo touch, puoi usare i gesti touch sui dispositivi abilitati, come il cellulare o il tablet. Tuttavia, sono disponibili anche le azioni del mouse su un dispositivo desktop tradizionale, che offrono flessibilità nella scelta della modalità di creazione dei contenuti.

## Primi passi {#first-steps}

Immediatamente dopo aver effettuato l’accesso, si aprirà il pannello di [navigazione](#navigation-panel). Selezionando una delle opzioni, si apre la rispettiva console.

![Pannello di navigazione](/help/sites-cloud/authoring/assets/navigation.png)

Per illustrare l’utilizzo di base di AEM, in questo documento viene utilizzata la console **Sites**. Seleziona il **Sites** per iniziare.

## Navigazione nel prodotto  {#product-navigation}

Ogni volta che un utente accede per la prima volta a una console, viene avviato un tutorial relativo alla navigazione nel prodotto. Prenditi un minuto per effettuare la selezione e ottenere una buona panoramica della gestione di base dell’AEM.

![Esercitazione sulla navigazione](/help/sites-cloud/authoring/assets/tutorial.png)

Seleziona **Successivo** per passare alla pagina successiva della panoramica. Seleziona **Chiudi** oppure seleziona all’esterno della finestra di dialogo della panoramica da chiudere.

Se non visualizzi tutte le diapositive o non selezioni l’opzione **Non mostrare più**, al prossimo accesso a una console la panoramica viene riavviata.

## Navigazione globale {#global-navigation}

Puoi spostarti tra le diverse console utilizzando il pannello di navigazione globale. Viene attivato come elenco a discesa a schermo intero quando selezioni il collegamento Adobe Experience Manager in alto a sinistra dello schermo.

Per chiudere il pannello di navigazione globale e tornare alla posizione precedente, tocca o fai clic su **Chiudi**.

![Barra superiore del pannello di navigazione](/help/sites-cloud/authoring/assets/navigation-bar.png)

La navigazione globale presenta due pannelli, rappresentati da icone sul lato sinistro dello schermo:

* **[Navigazione](#navigation-panel)**: rappresentata da una bussola  e il pannello predefinito al momento dell’accesso ad AEM
* **[Strumenti](#tools-panel)**: rappresentati da un martello

Le opzioni disponibili in questi pannelli sono descritte di seguito.

### Pannello di navigazione  {#navigation-panel}

Pannello di navigazione:

![Pannello di navigazione](/help/sites-cloud/authoring/assets/navigation.png)

Il titolo della scheda del browser si aggiorna per riflettere la posizione in cui ci si sposta nelle console e nel contenuto.

Nel pannello di navigazione sono disponibili le console seguenti:

| Console | Scopo |
|---|---|
| Progetti | La console Progetti consente di accedere direttamente ai progetti. [I progetti sono dashboard virtuali](/help/sites-cloud/authoring/projects/overview.md) che possono essere utilizzati per creare un team. Potrai quindi fornire al team l’accesso a risorse, flussi di lavoro e attività, facilitando la collaborazione verso un obiettivo comune. |
| Sites | Le console Sites ti permettono di [creare, visualizzare e gestire siti web](/help/sites-cloud/authoring/fundamentals/organizing-pages.md) in esecuzione sull’istanza AEM. Da questa console puoi creare, modificare, copiare, spostare ed eliminare pagine di siti web, avviare flussi di lavoro e pubblicare pagine. |
| Frammenti esperienza | Un [frammento di esperienza](/help/sites-cloud/authoring/fundamentals/experience-fragments.md) è un’esperienza autonoma che può essere riutilizzata su tutti i canali, supporta le varianti e non richiede di copiare e incollare le esperienze o parti di esse. |
| Assets | La console Assets consente di importare e gestire le [risorse digitali quali immagini, video, documenti e file audio](/help/assets/overview.md). Puoi usare queste risorse da qualunque sito web in esecuzione nell’istanza di AEM. Puoi anche creare e gestire [Frammenti di contenuto](/help/assets/content-fragments/content-fragments.md) dalla console Assets. |
| Personalizzazione | Questa console fornisce un set di strumenti per la [creazione e modifica di contenuti mirati e la presentazione di esperienze personali](/help/sites-cloud/authoring/personalization/overview.md). |
| Frammenti di contenuto | I [Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/overview.md) ti consentono di progettare, creare, curare e pubblicare contenuti indipendenti dalle pagine. Consentono di preparare contenuti strutturati pronti per l’uso in più posizioni/su più canali, ideali sia per l’authoring delle pagine che per la distribuzione headless. |

## Pannello Strumenti {#tools-panel}

Nel pannello Strumenti è presente un pannello laterale contenente una serie di categorie, che raggruppa le console simili della tipologia Strumenti. Le console Strumenti permettono di accedere a console e strumenti specifici per la gestione dei siti web, delle risorse digitali e di altri aspetti dell’archivio dei contenuti. <!--The [Tools consoles](/help/sites-administering/tools-consoles.md) provide access to several specialized tools and consoles that help you administer your websites, digital assets, and other aspects of your content repository.-->

![Pannello Strumenti](/help/sites-cloud/authoring/assets/tools-panel.png)

## Intestazione {#the-header}

L’intestazione di è sempre presente nella parte superiore dello schermo. Anche se la maggior parte delle opzioni presenti nell’intestazione rimangono invariate ovunque ti trovi nel sistema, alcune dipendono dal contesto.

![Intestazione di navigazione](/help/sites-cloud/authoring/assets/navigation-bar.png)

* [Navigazione globale](#global-navigation)

  Seleziona il collegamento **Adobe Experience Manager** per spostarti tra le diverse console.

  ![Navigazione globale](/help/sites-cloud/authoring/assets/global-navigation.png)

* [Ricerca](/help/sites-cloud/authoring/getting-started/search.md)

  ![Icona Ricerca](/help/sites-cloud/authoring/assets/search-icon.png)

  È anche possibile utilizzare il [tasto di scelta rapida](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) `/` (barra obliqua) per richiamare la ricerca da qualsiasi console.

* [Soluzioni](https://www.adobe.com/it/experience-cloud.html)

  ![Pulsante Soluzioni](/help/sites-cloud/authoring/assets/solutions.png)

* [Aiuto](#accessing-help)

  ![Pulsante Aiuto](/help/sites-cloud/authoring/assets/help.png)

* [Notifiche](/help/sites-cloud/authoring/getting-started/inbox.md)

  ![Pulsante Notifiche](/help/sites-cloud/authoring/assets/notifications.png)

  Questa icona viene contrassegnata con il numero di notifiche incomplete attualmente assegnate.

* [Proprietà utente](/help/sites-cloud/authoring/getting-started/account-environment.md)

  ![Pulsante Proprietà utente](/help/sites-cloud/authoring/assets/user-properties.png)

* [Selettore della barra](#rail-selector)

  ![Pulsante del selettore della barra](/help/sites-cloud/authoring/assets/rail-selector.png)

  Le opzioni visualizzate dipendono dalla console corrente. Ad esempio, in **Sites** puoi selezionare solo il contenuto (opzione predefinita), la timeline, i riferimenti o il pannello laterale del filtro.

  ![Esempio di selettore della barra](/help/sites-cloud/authoring/assets/rail-selector-example.png)

* Breadcrumb

  ![Breadcrumb nella barra di navigazione](/help/sites-cloud/authoring/assets/breadcrumbs-navigation.png)

  Situate al centro della barra, le breadcrumb mostrano sempre la descrizione dell’elemento attualmente selezionato e consentono di spostarsi all’interno di una console specifica. Nella console **Sites** puoi spostarti tra i vari livelli del sito web.

  Fai clic sul testo della breadcrumb per visualizzare un elenco a discesa dei livelli della gerarchia dell’elemento attualmente selezionato. Fare clic su una voce per passare alla posizione desiderata.

  ![Esempio di breadcrumb espanso](/help/sites-cloud/authoring/assets/breadcrumbs-example.png)

* Pulsante **Crea**

  ![Pulsante Crea](/help/sites-cloud/authoring/assets/create.png)

  Dopo che hai fatto clic, le opzioni visualizzate sono adatte alla console/al contesto.

* [Viste](#viewing-and-selecting-resources)

  L’icona di visualizzazione si trova all’estrema destra della barra degli strumenti di AEM. Inoltre, indica la vista corrente e ne consente la modifica. Ad esempio, la visualizzazione predefinita **Vista a colonne** presenta questa icona:

  ![Pulsante Viste](/help/sites-cloud/authoring/assets/views-button.png)

  Puoi alternare tra le viste a colonne, a schede e a elenco. La vista a elenco mostra anche le impostazioni di visualizzazione.

  ![Viste](/help/sites-cloud/authoring/assets/view.png)

  >[!NOTE]
  >
  >L’opzione **Impostazioni vista** è disponibile solo in modalità **Vista a elenco**.

* Navigazione tramite tastiera

  Potete navigare in un sito web utilizzando solo la tastiera. In questa modalità, si utilizza la funzionalità standard del browser per il tasto **TAB** (o **OPZ+TAB**) per spostarsi tra gli elementi della pagina che possono essere attivati.

  Nella console di **Sites** è stata aggiunta l’opzione per **passare al contenuto principale**. L’opzione diventa visibile quando ci si sposta tra le opzioni di intestazione, la navigazione diventa più veloce e consente di saltare gli elementi standard nella barra degli strumenti (prodotto) per passare direttamente al contenuto principale.

  ![Passa al contenuto principale](/help/sites-cloud/authoring/assets/skip-to-main-content.png)

## Accedere all’Aiuto   {#accessing-help}

Sono disponibili diverse risorse di Aiuto:

* **Barra degli strumenti della console**

  A seconda della posizione, il **Aiuto** apre le risorse appropriate:

  ![Icona Aiuto](/help/sites-cloud/authoring/assets/help-console.png)

* **Navigazione**

  La prima volta che accedi al sistema, compare [una serie di diapositive introduttive su come navigare in AEM](#product-navigation).

  ![Esercitazione](/help/sites-cloud/authoring/assets/tutorial.png)

* **Editor pagina**

  La prima volta che modifichi una pagina, compare una serie di diapositive introduttive sull’editor pagina.

  ![Esercitazione sull’editor](/help/sites-cloud/authoring/assets/editor-tutorial.png)

  Esamina questa panoramica come faresti con la [panoramica di navigazione del prodotto](#product-navigation) la prima volta che accedi a una console.

  Dal menu [**Informazioni sulle pagine** puoi selezionare **Aiuto**](/help/sites-cloud/authoring/fundamentals/environment-tools.md#accessing-help) per accedervi di nuovo in un secondo tempo.

* **Console Strumenti**

  Dalla console **Strumenti** è possibile inoltre accedere alle **Risorse** esterne:

   * **Documentazione:** visualizza la documentazione per la gestione esperienza web
   * **Risorse per sviluppatori:** risorse per sviluppatori e download

  >[!NOTE]
  >
  >Puoi accedere in qualsiasi momento ai tasti di scelta rapida, semplicemente utilizzando il tasto di scelta rapida `?` (punto interrogativo) all’interno della console.
  >
  >Per una panoramica di tutte le scelte rapide da tastiera, consulta la documentazione seguente:
  >
  >* [Scelte rapide da tastiera per la modifica delle pagine](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)
  >* [Scelte rapide da tastiera per le console](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)

## Barra delle azioni  {#actions-toolbar}

Ogni volta che viene selezionata una risorsa (ad esempio una pagina o una risorsa), le icone indicano diverse azioni, con testo descrittivo nella barra degli strumenti. Queste azioni dipendono da:

* La console corrente
* Il contesto attuale
* Se sei o meno in modalità [Selezione](#viewing-and-selecting-resources)

L’azione disponibile nella barra degli strumenti varia per riflettere le azioni che puoi eseguire sugli oggetti specifici selezionati.

La modalità di [selezione di una risorsa](#viewing-and-selecting-resources) dipende dalla vista.

A causa del poco spazio disponibile in alcune finestre, la barra può facilmente superare lo spazio a disposizione. In questo caso compaiono altre opzioni. Tocca o fai clic sui tre puntini (**...**) per aprire un menu a discesa contenente tutte le azioni che non rientrano nella barra. Ad esempio, dopo la selezione di una pagina nella console **Sites**:

![Opzioni aggiuntive](/help/sites-cloud/authoring/assets/additional-options.png)

>[!NOTE]
>
>Le singole icone disponibili sono documentate in relazione alla console, alla funzione o allo scenario appropriato.

## Azioni rapide  {#quick-actions}

Nella [Vista a schede](#card-view) alcune azioni sono disponibili come icone di scelta rapida, oltre che dalla barra degli strumenti. Le icone delle azioni rapide sono disponibili per un singolo elemento alla volta ed evitano di dover preselezionare le opzioni.

La azioni rapide sono visibili con un tocco prolungato (su dispositivo touch) sulla scheda di una risorsa. Le azioni rapide disponibili possono dipendere dalla console e dal contesto. Ad esempio, di seguito sono riportate le azioni rapide per una pagina nella console **Sites**:

![Opzioni aggiuntive](/help/sites-cloud/authoring/assets/quick-actions.png)

## Visualizzazione e selezione delle risorse {#viewing-and-selecting-resources}

In tutte le viste la visualizzazione, la navigazione e la selezione funzionano allo stesso modo, ma con lievi variazioni a seconda della vista attiva.

Puoi visualizzare, navigare e selezionare (per ulteriori azioni) le risorse in una qualsiasi delle viste disponibili, selezionabili dall’icona in alto a destra:

* [Vista a colonne](#column-view)
* [Vista a schede](#card-view)
* [Vista a elenco ](#list-view)

>[!NOTE]
>
>Per impostazione predefinita, AEM Assets non visualizza le rappresentazioni originali delle risorse nell’interfaccia utente come miniature in nessuna delle viste. Se sei un amministratore, puoi utilizzare le sovrapposizioni per configurare AEM Assets in modo da visualizzare le rappresentazioni originali come miniature.

### Selezionare le risorse  {#selecting-resources}

La selezione di una specifica risorsa dipende dalla combinazione della vista e del dispositivo utilizzati:

| Visualizzazione | Seleziona Touch | Seleziona Desktop | Deseleziona Touch | Deseleziona Desktop |
|---|---|---|---|---|
| Colonna | Tocca la miniatura | Fai clic sulla miniatura | Tocca la miniatura | Fai clic sulla miniatura |
| Scheda | Tocca e tieni premuto sulla scheda | Passa il puntatore del mouse, quindi utilizza l’azione rapida con il segno di spunta | Tocca la scheda | Fai clic sulla scheda |
| Elenco | Tocca la miniatura | Fai clic sulla miniatura | Tocca la miniatura | Fai clic sulla miniatura |

#### Seleziona tutto {#select-all}

Per selezionare tutti gli elementi in qualsiasi vista, fai clic sull’opzione **Seleziona tutto** nell’angolo in alto a destra della console.

* Nella **Vista a schede**, vengono selezionate tutte le schede.
* Nella **Vista a elenco**, vengono selezionati tutti gli elementi dell’elenco.
* Nella **Vista a colonne**, vengono selezionati tutti gli elementi nella colonna più a sinistra.

![Seleziona tutto](/help/sites-cloud/authoring/assets/select-all.png)

#### Deselezionare tutti gli elementi {#deselecting-all}

In tutti i casi in cui selezioni elementi, il numero degli elementi selezionati viene visualizzato in alto a destra nella barra degli strumenti.

Per deselezionare tutti gli elementi e uscire dalla modalità di selezione, puoi fare una delle seguenti operazioni:

* Tocca o fai clic sulla **X** accanto al conteggio.
* Utilizzo del tasto **Esc**

![Deseleziona tutto](/help/sites-cloud/authoring/assets/deselect-all.png)

In tutte le viste, tutti gli elementi possono essere deselezionati con il tasto Esc, se utilizzi un dispositivo desktop.

#### Esempio di selezione {#selecting-example}

1. Ad esempio, nella vista a schede:

   ![Selezione della Vista a schede](/help/sites-cloud/authoring/assets/card-view-select.png)

1. Dopo la selezione di una risorsa, l’intestazione superiore è coperta dalla [barra delle azioni](#actions-toolbar), che permette di accedere alle azioni applicabili alla risorsa selezionata.

   Per uscire dalla modalità di selezione, seleziona la **X** in alto a destra oppure premi **Esc**.

### Vista a colonne {#column-view}

![Vista a colonne](/help/sites-cloud/authoring/assets/column-view.png)

La vista a colonne consente la navigazione visiva di una struttura di contenuti tramite una serie di colonne in cascata. Questa visualizzazione consente di visualizzare e scorrere la struttura ad albero del sito web.

Quando si seleziona una risorsa nella prima colonna a sinistra, vengono visualizzate le risorse secondarie in una colonna a destra. Quando si seleziona una risorsa nella colonna a destra, vengono visualizzate le risorse secondarie in un’altra colonna a destra, e così via.

* Per spostarti verso l’alto o il basso nella struttura ad albero, tocca o fai clic sul nome della risorsa o sulla freccia a destra del nome.

   * Il nome della risorsa e la freccia vengono evidenziati quando tocchi o fai clic su tali elementi.
   * Gli elementi secondari della risorsa che hai toccato o su cui hai fatto clic vengono visualizzati nella colonna a destra di tale risorsa.
   * Se selezioni un nome di risorsa senza elementi secondari, i relativi dettagli vengono visualizzati nella colonna finale.

* Quando tocchi o fai clic sulla miniatura, la risorsa viene selezionata.

   * Quando una risorsa è selezionata, sulla miniatura compare un segno di spunta e il nome della risorsa viene evidenziato.
   * I dettagli della risorsa selezionata sono visualizzati nella colonna finale.
   * La barra degli strumenti delle azioni diventa disponibile.

  Quando una pagina viene selezionata nella vista a colonne, viene visualizzata nella colonna finale con i seguenti dettagli:

   * Titolo pagina
   * Nome pagina (parte dell’URL della pagina)
   * Modello su cui si basa la pagina
   * Dettagli di modifica
   * Lingua della pagina
   * Dettagli di pubblicazione e anteprima

### Vista a schede {#card-view}

![Vista a schede](/help/sites-cloud/authoring/assets/card-view.png)

* La vista a schede mostra le schede informative per ogni elemento al livello corrente, che forniscono informazioni quali:

   * Una rappresentazione visiva del contenuto della pagina
   * Il titolo della pagina
   * Date importanti (ad esempio ultima modifica, ultima pubblicazione)
   * Se la pagina è bloccata, nascosta o fa parte di una Live Copy
   * Se appropriato, quando devi agire come parte di un flusso di lavoro
      * Alle voci della [Casella in entrata](/help/sites-cloud/authoring/getting-started/inbox.md) possono essere correlati dei marcatori che indicano le azioni necessarie.

* In questa vista sono disponibili anche [azioni rapide](#quick-actions), per effettuare selezioni ed eseguire le operazioni più comuni, come la modifica.

  ![Azioni rapide](/help/sites-cloud/authoring/assets/quick-actions.png)

* Per spostarti verso il basso nella struttura, tocca o fai clic sulle schede (facendo attenzione a evitare le azioni rapide); per tornare verso l’alto utilizza le [breadcrumb nell’intestazione](#the-header).

### Vista a elenco  {#list-view}

![Vista a elenco](/help/sites-cloud/authoring/assets/list-view.png)

* Nella vista a elenco sono elencate le informazioni di ogni risorsa al livello corrente.
* Per spostarti verso il basso nella struttura, tocca o fai clic sul nome delle risorse; per tornare verso l’alto utilizza le [breadcrumb nell’intestazione](#the-header).
* Per selezionare tutti gli elementi nell’elenco, utilizza la casella di selezione in alto a sinistra nell’elenco.

  ![Vista a elenco seleziona tutto](/help/sites-cloud/authoring/assets/list-view-select-all.png)

   * Quando tutti gli elementi dell’elenco sono selezionati, viene selezionata la casella di controllo.

      * Seleziona la casella di controllo per deselezionare tutti.

   * Se sono selezionati solo alcuni elementi, viene visualizzato un segno meno.

      * Seleziona la casella di controllo per selezionare tutti.
      * Seleziona nuovamente la casella di controllo per deselezionare tutti.

* Per seleziona le colonne da visualizzare utilizza l’opzione **Impostazioni vista** sotto il pulsante Viste. È possibile visualizzare le colonne seguenti:

   * **Nome**: nome della pagina, utile in un ambiente di authoring multilingue poiché fa parte dell’URL della pagina e non viene modificato indipendentemente dalla lingua
   * **Modificato**: data dell’ultima modifica e dell’utente che l’ha eseguita
   * **Pubblicato**: stato della pubblicazione
   * **Anteprima**: stato anteprima
   * **Modello**: modello su cui si basa la pagina
   * **Flusso di lavoro**: flusso di lavoro attualmente applicato alla pagina. Ulteriori informazioni sono disponibili quando passi sopra con il mouse o apri la Timeline.
   * **Dati analitici della pagina**
   * **Visitatori univoci**
   * **Tempo sulla pagina**

     ![Seleziona colonne](/help/sites-cloud/authoring/assets/select-columns.png)

  Per impostazione predefinita, la colonna **Nome** è visualizzata e costituisce una porzione dell’URL della pagina. In alcuni casi, l’autore potrebbe dover accedere a pagine in una lingua diversa; poiché il nome della pagina di solito non cambia, può essere di grande aiuto se si tratta di una lingua che l’autore non conosce.

* Cambia l’ordine degli elementi utilizzando la barra verticale punteggiata all’estrema destra di ciascun elemento dell’elenco.

  >[!NOTE]
  >
  >La modifica dell’ordine funziona solo all’interno di una cartella ordinata il cui valore `jcr:primaryType` è impostato su `sling:OrderedFolder`.

  ![Ordine delle colonne](/help/sites-cloud/authoring/assets/column-order.png)

  Selezionare la barra di selezione verticale e trascinare l&#39;elemento in una nuova posizione nell&#39;elenco.

  ![Ordinare un elenco](/help/sites-cloud/authoring/assets/order-list.png)

## Selettore della barra {#rail-selector}

Il **selettore della barra** è disponibile in alto a sinistra nella finestra e visualizza opzioni che dipendono dalle console correnti.

![Selettore della barra espanso](/help/sites-cloud/authoring/assets/rail-selector-expanded.png)

Ad esempio, in **Sites** puoi selezionare solo il contenuto (opzione predefinita), la struttura, la timeline, i riferimenti, i dettagli del sito o il pannello laterale dei filtri.

Se selezioni solo il contenuto, appare solo l’icona della barra. Quando selezioni qualsiasi altra opzione, il nome è visualizzato accanto all’icona della barra.

>[!NOTE]
>
>Sono disponibili [scelte rapide da tastiera](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) per passare rapidamente da un’opzione all’altra della barra.

### Struttura contenuto {#content-tree}

La struttura del contenuto può essere utilizzata per spostarsi rapidamente nella gerarchia del sito all’interno del pannello laterale e visualizzare molte informazioni sulle pagine nella cartella corrente.

Mediante il pannello laterale della struttura del contenuto, insieme alla vista a elenco o a schede, gli utenti possono visualizzare facilmente la struttura gerarchica del progetto ed esplorare in modo più semplice la struttura del contenuto, e visualizzare informazioni dettagliate sulla pagina nella vista a elenco.

![Struttura contenuto](/help/sites-cloud/authoring/assets/content-tree.png)

>[!NOTE]
>
>Una volta selezionata una voce nella visualizzazione gerarchica, puoi spostarti rapidamente nella gerarchia attraverso i tasti freccia.
>
>Per ulteriori informazioni, consulta [scelte rapide da tastiera](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md).

### Timeline {#timeline}

Con la timeline puoi visualizzare e/o attivare gli eventi della risorsa selezionata. Per aprire la colonna della timeline, utilizza il selettore della barra a sinistra:

![Struttura della timeline](/help/sites-cloud/authoring/assets/timeline.png)

La colonna della timeline consente di:

* Visualizzare vari eventi relativi all’elemento selezionato.

   * I tipi di evento possono essere selezionati dall’elenco a discesa:

      * Commenti
      * [Annotazioni](/help/sites-cloud/authoring/fundamentals/annotations.md)
      * [Attività](/help/sites-cloud/authoring/personalization/activities.md)
      * [Lanci](/help/sites-cloud/authoring/launches/overview.md)
      * [Versioni](/help/sites-cloud/authoring/features/page-versions.md)
      * [Flussi di lavoro](/help/sites-cloud/authoring/workflows/overview.md)
         * Ad eccezione dei flussi di lavoro transitori, in quanto per tali flussi non vengono conservate informazioni sulla cronologia <!--With the exception of [transient workflows](/help/sites-developing/workflows.md#transient-workflows) as no history information is saved for these-->
      * Mostra tutto

* Aggiungere o visualizzare commenti sulla voce selezionata. La casella **Commento** è visualizzata in fondo all’elenco degli eventi. Per registrare un commento, digitalo e premi Invio. Il commento verrà visualizzato quando selezioni **Commenti** o **Mostra tutto**.

* Alcune console offrono funzionalità aggiuntive. Ad esempio, nella console Sites è possibile:

   * [Salvare una versione](/help/sites-cloud/authoring/features/page-versions.md)
   * [Avviare un flusso di lavoro](/help/sites-cloud/authoring/workflows/applying.md)

Queste opzioni sono accessibili tramite la freccia accanto al campo **Commento**.

![Campo Commento](/help/sites-cloud/authoring/assets/comments.png)

### Riferimenti {#references}

**I riferimenti mostrano eventuali collegamenti alla risorsa selezionata.** Ad esempio, nella console **Sites**, i [riferimenti](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references) per le pagine mostrano:

* [Lanci](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)
* [Live Copy](/help/sites-cloud/administering/msm/overview.md#openingthelivecopyoverviewfromreferences)
* [Copie per lingua](/help/sites-cloud/administering/translation/preparation.md#seeing-the-status-of-language-roots)
* Riferimenti ai contenuti:

   * Collegamenti da altre pagine alla pagina selezionata
   * Contenuti presi in prestito da e/o prestati alla pagina selezionata dal componente Riferimento

![Esempio di riferimenti](/help/sites-cloud/authoring/assets/references-example.png)

### Sito {#site}

**Sito** mostra i dettagli dei siti [creati utilizzando un modello del sito](/help/sites-cloud/administering/site-creation/create-site.md).

![Barra del sito](../assets/site-rail.png)

Consulta il documento [Utilizzo della barra del sito per gestire il tema del sito](/help/sites-cloud/administering/site-creation/site-rail.md) per ulteriori dettagli su come utilizzare la barra per gestire il [tema del sito](/help/sites-cloud/administering/site-creation/site-themes.md).

>[!TIP]
>
>Per una descrizione end-to-end del processo di creazione di un sito da un modello e personalizzazione del relativo tema, consulta [Percorso di creazione rapida dei siti](/help/journey-sites/quick-site/overview.md).

### Filtro {#filter}

Questo apre un pannello simile a [ricerca](/help/sites-cloud/authoring/getting-started/search.md) con i filtri di posizione appropriati già impostati, che consentono di filtrare ulteriormente il contenuto da visualizzare.

![Esempio di filtro](/help/sites-cloud/authoring/assets/filter.png)
