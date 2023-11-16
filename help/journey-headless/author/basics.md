---
title: Scopri le nozioni di base sull’authoring
description: Scopri cos’è e come funziona l’authoring per i CMS headless utilizzando frammenti di contenuto.
exl-id: 3eca973f-b210-41bb-98da-ecbd2bae9803
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 83%

---

# Nozioni di base sull’authoring per headless con AEM {#author-headless-basics}

## Percorso affrontato finora {#story-so-far}

All’inizio del [Percorso di authoring dei contenuti headless in AEM](overview.md), nell’[Introduzione](introduction.md) sono stati trattati i concetti e la terminologia di base relativi all’authoring per headless.

Questo articolo si basa su questi elementi per comprendere come creare contenuti personalizzati per il progetto headless AEM.

## Obiettivo {#objective}

* **Pubblico**: principiante
* **Obiettivo**: scopri le nozioni di base sull’authoring di CMS headless:
   * introduzione all’authoring con AEMaaCS
   * Introduzione ai frammenti di contenuto

## Operazioni di base {#basic-handling}

Prima di iniziare a gestire i frammenti di contenuto, ecco un’introduzione (molto) rapida all’utilizzo di AEM...ma niente sostituisce l’esperienza di accesso e di utilizzo del sistema.

### Authoring, Anteprima e Pubblicazione {#author-preview-publish}

Generalmente, l’installazione di AEM è costituita da tre ambienti:

* Autore
* Pubblicazione
* Anteprima

Accedi e utilizza l’ambiente di authoring per generare i contenuti. Quando è tutto pronto, pubblica il contenuto in modo che diventi disponibile. Per gli headless sarà disponibile in altre applicazioni, per le pagine web sarà disponibile ai lettori sul web.

Per ulteriori dettagli, consulta i concetti di authoring.

Dalla console **Frammenti di contenuto**, puoi anche pubblicare nel **Servizio di anteprima**, per il test e la visualizzazione in anteprima, prima della pubblicazione. Consulta Pubblicazione e anteprima di un frammento.

### Accesso {#signing-in}

Come per la maggior parte dei sistemi, è necessario effettuare l’accesso. In qualità di autore, ricevi:

* Nome utente (account)
* Password
* Collegamento per accedere alla schermata di accesso

Il tuo account sarà stato configurato con tutti i privilegi necessari. In caso di problemi, l’Adobe consiglia di contattare il team interno di supporto al progetto.

### Navigazione {#navigation}

La prima volta che esegui l’accesso a una piccola esercitazione online, verranno evidenziate alcune delle funzioni principali dell’interfaccia utente.

È quindi possibile utilizzare il pannello di navigazione per accedere alle aree chiave di AEM. Per i frammenti di contenuto viene utilizzata la console **Frammenti di contenuto** (per alcune azioni puoi usare anche la console **Risorse**).

Per aprire il pannello di navigazione, seleziona l’icona Adobe in alto a sinistra e l’icona a forma di piccola bussola.

<!--
The Navigation Panel can be opened by selecting Adobe icon at the top left, followed by the small compass icon:

![Navigation panel](/help/journey-headless/author/assets/headless-journey-author-navigation-01.png)
-->

>[!NOTE]
>Anche se i frammenti di contenuto sono una funzione di AEM **Sites**, vengono salvati come **Risorse**. Questo è un dettaglio tecnico che non dovrebbe influenzare l’utente, ma potrebbe essere utile da sapere.

Nella console puoi selezionare le cartelle nel pannello a sinistra per andare al frammento di contenuto. Puoi anche filtrare e/o eseguire ricerche.

![Console Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/assets/cf-managing-console-filter.png)

### Azioni, selezione, visualizzazione {#actions-selecting-viewing}

Nella barra degli strumenti della console **Frammenti di contenuto** è disponibile una scelta di azioni relative ai frammenti di contenuto:

<!-- ![Console actions](assets/cfm-managing-cf-console-01.png) -->

* **Apri in Assets**
* **Crea**
* La colonna **Riferimento da** fornisce inoltre un collegamento diretto per visualizzare tutti i riferimenti principali di tale frammento, compresi i riferimenti a frammenti di contenuto, frammenti di esperienza e pagine.
* Passando il puntatore del mouse sul nome della cartella verrà visualizzato il percorso JCR.

Dopo aver selezionato il frammento, saranno disponibili tutte le azioni appropriate:

<!-- ![Console actions - fragment selected](assets/cfm-managing-cf-console-selected-01.png) -->

* **Apri**
* **Pubblica** (e **Annulla pubblicazione**)
* **Copia**
* **Sposta**
* **Rinomina**
* **Elimina**

>[!NOTE]
>
>Azioni come Pubblica, Annulla pubblicazione, Elimina, Sposta, Rinomina, Copia, attivano un processo asincrono. L’avanzamento di tale processo può essere monitorato tramite l’interfaccia dei processi asincroni di AEM.

<!--
The **Assets** console has dedicated **Action Toolbars**, and **Quick Actions** that you can use after selecting a resource (for example, a folder or content fragment).

The Quick Actions are available for a single resource, see **Basel** in the example below:

![Quick Actions](/help/journey-headless/author/assets/headless-journey-author-navigation-05.png)

The Actions Toolbar provides access to the full range of actions - applicable for the current scenario. The actions available can change; for example, dependent on your location, or whether you have selected multiple resources:

![Action Toolbar](/help/journey-headless/author/assets/headless-journey-author-navigation-06.png)

You can select the format for viewing your resources with the View Selector:

![View Selector](/help/journey-headless/author/assets/headless-journey-author-navigation-03.png)

You can view additional information about items using the Rail Selector. This also gives access to additional actions.

![Left Rail](/help/journey-headless/author/assets/headless-journey-author-navigation-04.png)
-->

## Authoring dei frammenti di contenuto {#authoring-content-fragments}

Questa è stata una rapida introduzione all’interfaccia utente AEM, ma dovresti aver avuto l’occasione di provarla. Ora passiamo a quello che ti interessa di più: frammenti di contenuto per headless.

Dovremo passare dall’inizio alla fine delle operazioni, ma l’istanza potrebbe avere già cartelle e/o frammenti creati, che potrebbero trovarsi in posizioni diverse. I principi sono gli stessi.

### Organizzazione e navigazione {#organizing-and-navigating}

A meno che non siano disponibili pochissimi frammenti di contenuto, è consigliabile organizzarli in modo da poterli trovare nuovamente (insieme ad altri).

#### Creazione di una cartella {#creating-folder}

Per farlo, crea una serie di cartelle all’interno della sezione **File** della console **Risorse**. Seleziona l’opzione **Crea** (in alto a destra), seguita da **Cartella**:

![Opzione Crea cartella](/help/journey-headless/author/assets/headless-journey-author-folder-01.png)

Viene visualizzata una finestra di dialogo in cui puoi immettere i dettagli, quindi confermare con **Crea**:

![Finestra di dialogo Crea cartella](/help/journey-headless/author/assets/headless-journey-author-folder-02.png)

#### Utilizzo di percorsi e tag per limitare i modelli per frammenti di contenuto disponibili nella cartella {#tags-paths-for-models-in-folder}

Questa sezione è leggermente più avanzata. Non ne hai bisogno se hai appena iniziato a fare delle prove, ma è *molto* utile quando sono disponibili divesi frammenti. Quindi è bene conoscerla, anche se non la stai ancora usando.

L’architect di contenuti avrà creato tutti i modelli di frammento di contenuto necessari per il progetto corrente e forse anche altri progetti. Per semplificare le cose a te stesso e agli altri autori, puoi limitare l’elenco dei modelli disponibili per una cartella specifica.

Dopo aver creato la tua cartella è possibile aprire la cartella **Proprietà**. Qui ci sono varie schede con informazioni e dettagli di configurazione sulla cartella. In particolare per i frammenti di contenuto, puoi utilizzare la scheda **Criteri** per definire percorsi e/o tag specifici per questa cartella. Questo limita i modelli per frammenti di contenuto disponibili per l’utilizzo nella cartella, poiché i modelli per frammenti di contenuto devono soddisfare questi requisiti prima di poter essere utilizzati per generare frammenti in questa cartella.

![Crea proprietà cartella - Criteri](/help/journey-headless/author/assets/headless-journey-author-folder-04.png)

>[!NOTE]
>
>Per ulteriori informazioni, consulta Modelli per frammenti di contenuto - Consentire modelli per frammenti di contenuto nella cartella delle risorse.

Puoi quindi navigare tra queste cartelle per creare e modificare i frammenti di contenuto.

#### In caso - Configurazione cartella Cloud Services {#cloud-services-folder}

In caso...

Probabilmente ti verrà offerta una cartella iniziale in cui puoi creare le tue cartelle. Come alcuni dettagli di configurazione devono essere applicati alla cartella principale (in genere da uno sviluppatore o da un amministratore di sistema). Questo probabilmente non ti interesserà, ma se necessario è possibile controllare la **Configurazione** nel **Cloud Services** della cartella **Proprietà**:

![Crea proprietà cartella - Configurazione](/help/journey-headless/author/assets/headless-journey-author-folder-03.png)

>[!NOTE]
>
>Per ulteriori informazioni, consulta Applicare la configurazione alla cartella Risorse.

### Creazione di un frammento di contenuto {#creating-fragment}

Nella console **Frammenti di contenuto** puoi utilizzare **Crea** per aprire la finestra di dialogo **Nuovo frammento di contenuto**:

![Console Frammenti di contenuto - Creazione di un nuovo frammento](/help/sites-cloud/administering/content-fragments/assets/cfc-console-create.png)

Specifica:

* **Dove si trova**
* **Modello per frammenti di contenuto**
* **Titolo**
* **Nome**
* **Descrizione**

Quindi conferma con **Crea** o con **Crea e apri**.

### Modifica di un frammento {#editing-fragment}

È possibile aprire un frammento subito dopo averlo creato, oppure selezionandolo dalla console Frammenti di contenuto (anche dalla console Risorse).

>[!NOTE]
>
>I frammenti di contenuto sono una funzione di Sites, ma vengono memorizzati come **Risorse**.
>
>Sono disponibili due editor per l’authoring dei frammenti di contenuto.
>
>* Il nuovo editor, accessibile principalmente da **Frammenti di contenuto** console.
>* L’editor originale, accessibile principalmente da **Risorse** console.

Quando l’editor si apre per la prima volta, visualizzi:

* barra degli strumenti superiore: per informazioni chiave e azioni
   * un collegamento alla Console Frammenti di contenuto (icona Home)
   * informazioni sul modello e sulla cartella
   * collegamenti a Anteprima; se per il modello è configurato il Pattern URL di anteprima predefinito
   * Pubblicare e annullare la pubblicazione delle azioni
   * un&#39;opzione per mostrare tutto **Riferimenti padre** (icona collegamento)
   * il frammento **Stato**, e le ultime informazioni salvate
   * un pulsante per passare all’editor originale (basato su Assets)
* pannello a sinistra: mostra **Varianti** per il frammento di contenuto e i relativi **Campi**:
   * questi collegamenti possono essere utilizzati per navigare nella struttura dei frammenti di contenuto
* pannello a destra: presenta schede che mostrano le proprietà (metadati) e i tag, informazioni sulla cronologia delle versioni e informazioni relative a eventuali copie per lingua
   * nel **Proprietà** è possibile aggiornare la scheda **Titolo** e **Descrizione** per il frammento, oppure **Variante**
* pannello centrale: mostra i campi e il contenuto effettivi della variante selezionata
   * consente di modificare il contenuto
   * se **Segnaposto scheda** I campi sono definiti all&#39;interno del modello che vengono visualizzati qui e possono essere utilizzati per la navigazione

Ad esempio, un frammento può:

* Richiedono più informazioni, alcune con un tipo specifico. Per i contenuti headless, i riferimenti sono fondamentali (informazioni su questi ultimi disponibili più avanti nel percorso).

* Consente di scrivere una lunga sezione di testo. Qui sono disponibili opzioni aggiuntive per la gestione e la formattazione del testo. Puoi anche aprire i singoli campi di testo in un editor a schermo intero (utilizzando l’icona a forma di piccolo schermo a destra)

![Editor frammento di contenuto - Alaska Spirits](/help/sites-cloud/administering/content-fragments/assets/cf-authoring-overview.png)

>[!NOTE]
>
>Per aiutare gli autori a completare alcuni campi correttamente, potrebbe essere necessaria una documentazione specifica per il progetto.
>
>Consulta Modelli per frammenti di contenuto - Tipi di dati e proprietà per dettagli generici.

Conferma gli aggiornamenti con **Salva** o **Salva e chiudi**.

>[!NOTE]
>
>Per ulteriori informazioni, consulta Varianti - Authoring di frammenti di contenuto.

#### Quello di cui (probabilmente) non devi preoccuparti {#what-you-probably-do-not-need-to-worry-about}

OK, questa potrebbe sembrare una sezione leggermente ambigua, ma appena aperto l’Editor frammento di contenuto e iniziato ad esplorarlo, visualizzerai diverse opzioni che (probabilmente) non sono applicabili al tuo percorso headless come Autore del contenuto. Questo è solo un rapido resoconto di ciò che dovresti essere in grado di ignorare nel contesto headless:

* **Modelli per frammenti di contenuto**

  Puoi visualizzare il nome del modello per frammenti di contenuto nel pannello di destra dell’editor. Questo è anche un collegamento che ti porta all’editor modelli.
I modelli per frammenti di contenuto sono di fatto vitali per i frammenti di contenuto quando definiscono la struttura utilizzata. Tuttavia, la creazione e la modifica di tali elementi è (in genere) responsabilità di un’altra persona, l’architect di contenuti.

  >[!NOTE]
  >
  >Per ulteriori informazioni, consulta il Percorso Architect di contenuti AEM headless.

### Pubblicazione {#publishing}

<!-- needs more details -->

Una volta completato il frammento, puoi **Pubblicare** in modo che sia disponibile per le applicazioni headless.

Le azioni di pubblicazione sono disponibili nell’editor:

![Editor frammento di contenuto - Frammento personale](/help/journey-headless/author/assets/headless-journey-author-content-fragment-06.png)

>[!NOTE]
>
>Puoi anche pubblicare il frammento dalla console **Risorse** o **Frammenti di contenuto**.

## Passaggio successivo {#whats-next}

Ora che hai imparato le nozioni di base, il passo successivo è [Scopri come utilizzare i riferimenti](references.md). Questo introduce e illustra i vari riferimenti disponibili e come creare livelli di struttura con i Riferimenti ai frammenti, una parte chiave dell’authoring per gli oggetti headless.

## Risorse aggiuntive {#additional-resources}

* [Concetti relativi all’authoring](/help/sites-cloud/authoring/getting-started/concepts.md)

* [Operazioni di base](/help/sites-cloud/authoring/getting-started/basic-handling.md) - questa pagina si basa principalmente sulla console **Sites**, ma molte delle funzioni sono anche rilevanti per l’authoring **Frammenti di contenuto** nella console **Risorse**.

   * [Pannello di navigazione](/help/sites-cloud/authoring/getting-started/basic-handling.md#navigation-panel)

   * [Intestazione](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header)

   * [Barra degli strumenti delle azioni](/help/sites-cloud/authoring/getting-started/basic-handling.md#actions-toolbar)

   * [Azioni rapide](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)

   * [Visualizzazione e selezione delle risorse](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)

   * [Selettore della barra](/help/sites-cloud/authoring/getting-started/basic-handling.md#rail-selector)

* [Utilizzo di frammenti di contenuto](/help/sites-cloud/administering/content-fragments/overview.md)

   * [Gestione dei frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing.md)

   * [Applica la configurazione alla cartella Risorse](/help/sites-cloud/administering/content-fragments/setup.md#apply-the-configuration-to-your-folder)

   * [Creazione di un frammento di contenuto](/help/sites-cloud/administering/content-fragments/managing.md#creating-a-content-fragment)

   * [Authoring dei frammenti di contenuto](/help/sites-cloud/administering/content-fragments/authoring.md)

   * Pubblicazione

      * Dall’editor, oppure dalla console **Risorse**

         * [Pubblicazione rapida](/help/assets/manage-publication.md#quick-publish)

         * [Gestisci pubblicazione](/help/assets/manage-publication.md#manage-publication)

      * Dalla console **Frammenti di contenuto**

         * [Pubblicazione e anteprima di un frammento di contenuto](/help/sites-cloud/administering/content-fragments/managing.md#publishing-and-previewing-a-fragment)

   * [Modelli per frammenti di contenuto](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)

      * [Modelli per frammenti di contenuto - Tipi di dati](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types)

      * [Modelli per frammenti di contenuto - Proprietà](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#properties)

      * [Modelli per frammenti di contenuto - Consentire modelli per frammenti di contenuto nella cartella delle risorse](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#allowing-content-fragment-models-assets-folder)

* [Frammenti di contenuto - editor originale, dalla console Assets](/help/assets/content-fragments/content-fragments-variations.md)

* Guide introduttive
   * [Creazione di una configurazione headless per la cartella delle risorse](/help/headless/setup/create-assets-folder.md)

* Percorso Architect di contenuti AEM headless

* Percorso di traduzione headless di AEM
