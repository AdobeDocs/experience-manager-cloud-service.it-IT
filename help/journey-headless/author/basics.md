---
title: Scopri le nozioni di base sull’authoring
description: Scopri cos’è e come funziona l’authoring per i CMS headless utilizzando frammenti di contenuto.
exl-id: 3eca973f-b210-41bb-98da-ecbd2bae9803
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1712'
ht-degree: 85%

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

Un’installazione AEM è generalmente costituita da tre ambienti:

* Autore
* Pubblicazione
* Anteprima

Accedi e utilizza l’ambiente di authoring per generare i contenuti. Quando è tutto pronto, pubblica il contenuto in modo che diventi disponibile. Per gli headless sarà disponibile in altre applicazioni, per le pagine web sarà disponibile ai lettori sul web.

Per ulteriori dettagli, consulta i concetti di authoring.

Dalla sezione **Frammenti di contenuto** , puoi anche pubblicare in **Servizio di anteprima**, per il test e la visualizzazione in anteprima, prima della pubblicazione. Consulta Pubblicazione e anteprima di un frammento.

### Accesso {#signing-in}

Come per la maggior parte dei sistemi, è necessario accedere. In qualità di autore, ti vengono forniti:

* Nome utente (account)
* Password
* Collegamento per accedere alla schermata di accesso

Il tuo account sarà stato configurato con tutti i privilegi necessari. In caso di problemi, ti consigliamo di contattare il team di supporto per il progetto interno.

### Navigazione {#navigation}

La prima volta che esegui l’accesso a una piccola esercitazione online, verranno evidenziate alcune delle funzioni principali dell’interfaccia utente.

È quindi possibile utilizzare il pannello di navigazione per accedere alle aree chiave di AEM. Per i frammenti di contenuto, utilizza **Frammenti di contenuto** (per alcune azioni utilizzerai anche la **Risorse** console).

Per aprire il pannello di navigazione, seleziona l’icona Adobe in alto a sinistra e l’icona a forma di piccola bussola.

<!--
The Navigation Panel can be opened by selecting Adobe icon at the top left, followed by the small compass icon:

![Navigation panel](/help/journey-headless/author/assets/headless-journey-author-navigation-01.png)
-->

>[!NOTE]
>Anche se i frammenti di contenuto sono una funzione di AEM **Sites**, vengono salvati come **Risorse**. Questo è un dettaglio tecnico che non dovrebbe influenzare l’utente, ma potrebbe essere utile da sapere.

Nella console puoi selezionare le cartelle nel pannello a sinistra per andare al frammento di contenuto. Puoi anche filtrare e/o eseguire ricerche.

![Console Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/assets/cfc-console-filter.png)

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

Quindi, questa è stata una rapida introduzione all&#39;Interfaccia Utente (UI) dell&#39;AEM, ma si spera di avere avuto la possibilità di provarlo. Ora passiamo a quello che ti interessa di più: frammenti di contenuto per headless.

Dovremo passare dall’inizio alla fine delle operazioni, ma l’istanza potrebbe avere già cartelle e/o frammenti creati, che potrebbero trovarsi in posizioni diverse. I principi sono gli stessi.

### Organizzazione e navigazione {#organizing-and-navigating}

A meno che non siano disponibili pochissimi frammenti di contenuto, è consigliabile organizzarli in modo da poterli trovare nuovamente (insieme ad altri).

#### Creazione di una cartella {#creating-folder}

Per farlo, crea una serie di cartelle all’interno della sezione **File** della console **Risorse**. Seleziona l’opzione **Crea** (in alto a destra), seguita da **Cartella**:

![Opzione Crea cartella](/help/journey-headless/author/assets/headless-journey-author-folder-01.png)

Viene visualizzata una finestra di dialogo in cui puoi inserire i dettagli, quindi confermare con **Crea**:

![Finestra di dialogo Crea cartella](/help/journey-headless/author/assets/headless-journey-author-folder-02.png)

#### Utilizzo di percorsi e tag per limitare i modelli per frammenti di contenuto disponibili nella cartella {#tags-paths-for-models-in-folder}

Questa sezione è leggermente più avanzata. Non ne hai veramente bisogno se stai solo iniziando e provando le cose, ma è *molto* utile quando hai molti frammenti. Quindi è bene sapere su - anche se non lo si utilizza ancora abbastanza.

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

<!--
Creating a Content Fragment is very similar - you just use the **Content Fragment** option instead:

![Create Content Fragment option](/help/journey-headless/author/assets/headless-journey-author-content-fragment-01.png)

This time a wizard opens. The first step is to select the Content Fragment Model that your fragment is based on:

![Create Content Fragment - select Model](/help/journey-headless/author/assets/headless-journey-author-content-fragment-02.png)

After continuing with **Next** you can supply the details (**Basic** and **Advanced**) for your fragment:

![Create Content Fragment - provide Name](/help/journey-headless/author/assets/headless-journey-author-content-fragment-03.png)

Confirm with **Create** and you can then **Open** your fragment in the editor.
-->

### Modifica di un frammento {#editing-fragment}

È possibile aprire un frammento subito dopo averlo creato, oppure selezionandolo dalla console Frammenti di contenuto (anche dalla console Risorse).

La prima volta che l’editor viene aperto, viene visualizzato quanto segue:

* Un elenco di icone a sinistra permette di accedere a varie aree di funzionalità. L’editor si apre nella scheda **Variazioni**, in questo punto avviene la maggior parte delle modifiche. Potresti anche essere interessato alle schede **Annotazioni** e **Metadati**.

* Intestazione con informazioni sul frammento e accesso a varie azioni.

* L’area di modifica principale dipende dal modello utilizzato per creare il frammento.

Come esempi:

* Frammento che richiede solo più informazioni, alcune con un tipo specifico. Per i contenuti headless, i riferimenti sono fondamentali; informazioni su questi sono disponibili più avanti nel percorso.

  ![Editor frammento di contenuto - Frammento personale](/help/journey-headless/author/assets/headless-journey-author-content-fragment-04.png)

* Frammento che consente di scrivere una lunga sezione di testo. Qui sono disponibili opzioni aggiuntive per la gestione e la formattazione del testo. Puoi anche aprire i singoli campi di testo in un editor a schermo intero (utilizzando l’icona a forma di piccolo schermo a destra)

  ![Editor frammento di contenuto - Alaska Spirits](/help/journey-headless/author/assets/headless-journey-author-content-fragment-05.png)

>[!NOTE]
>
>Per aiutare gli autori a completare alcuni campi correttamente, potrebbe essere necessaria una documentazione specifica per il progetto.
>
>Consulta Modelli per frammenti di contenuto - Tipi di dati e proprietà per dettagli generici.

Conferma gli aggiornamenti con **Salva** o **Salva e chiudi**.

>[!NOTE]
>
>Per ulteriori informazioni, consulta Varianti - Authoring di frammenti di contenuto.

#### Di cosa non deve (probabilmente) preoccuparsi {#what-you-probably-do-not-need-to-worry-about}

Questa sezione potrebbe sembrare un po’ strana, ma dopo aver aperto l’Editor frammento di contenuto e aver iniziato a esplorare puoi vedere diverse opzioni che (probabilmente) non si applicano al percorso headless come autore di contenuti. Questo è solo un rapido resoconto di ciò che dovresti essere in grado di ignorare nel contesto headless:

* **Modelli per frammenti di contenuto**

  Il nome del modello di frammento di contenuto verrà visualizzato nella parte superiore dell’editor, direttamente sotto il nome del frammento. Questo è anche un collegamento che ti porta all’editor modelli.
I modelli per frammenti di contenuto sono di fatto vitali per i frammenti di contenuto quando definiscono la struttura utilizzata. Tuttavia, la creazione e la modifica di tali elementi è (in genere) responsabilità di un’altra persona, l’architect di contenuti.

  >[!NOTE]
  >
  >Per ulteriori informazioni, consulta il Percorso Architect di contenuti AEM headless.

* **Contenuto associato**

  Questo è abbastanza ovvio in quanto è una scheda nell&#39;editor.

  I frammenti di contenuto sono disponibili in AEM in diverse versioni. Originariamente erano disponibili per l’uso “tradizionale” durante l’authoring delle pagine....e sono ancora utilizzati in questo contesto. Questo può comportare l’associazione di risorse (ad esempio immagini) che, pur non essendo incorporate nel frammento, devono essere disponibili all’autore durante la creazione di una pagina.

* **Anteprima**

  Questa è un’altra scheda nell’editor e fornisce una vista tecnica, destinata principalmente agli sviluppatori.

* **Aggiorna i riferimenti di pagina**

  Questa azione è disponibile dal **...** (puntini di sospensione). Non è interessante per gli autori headless in quanto si riferisce all’authoring delle pagine.

### Pubblicazione {#publishing}

<!-- needs more details -->

Una volta completato il frammento, puoi **Pubblicare** in modo che sia disponibile per le applicazioni headless.

Le azioni di pubblicazione sono disponibili nell’editor:

![Editor frammento di contenuto - Frammento personale](/help/journey-headless/author/assets/headless-journey-author-content-fragment-06.png)

>[!NOTE]
>
>Puoi anche pubblicare il frammento da **Risorse** o **Frammenti di contenuto** console.

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

* [Utilizzo di frammenti di contenuto](/help/sites-cloud/administering/content-fragments/content-fragments.md)

   * [Gestione dei frammenti di contenuto](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md)

   * [Applica la configurazione alla cartella Risorse](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

   * [Creazione di un frammento di contenuto](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#creating-a-content-fragment)

   * [Varianti - Authoring di frammenti di contenuto](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md)

   * Pubblicazione

      * Dall’editor, oppure **Risorse** console

         * [Pubblicazione rapida](/help/assets/manage-publication.md#quick-publish)

         * [Gestisci pubblicazione](/help/assets/manage-publication.md#manage-publication)

      * Dalla sezione **Frammenti di contenuto** Console

         * [Pubblicazione e anteprima di un frammento di contenuto](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#publishing-and-previewing-a-fragment)

   * [Modelli per frammenti di contenuto](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)

      * [Modelli per frammenti di contenuto - Tipi di dati](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#data-types)

      * [Modelli per frammenti di contenuto - Proprietà](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#properties)

      * [Modelli per frammenti di contenuto - Consentire modelli per frammenti di contenuto nella cartella delle risorse](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)

* Guide introduttive
   * [Creazione di una configurazione headless per la cartella delle risorse](/help/headless/setup/create-assets-folder.md)

* Percorso Architect di contenuti AEM headless

* Percorso di traduzione headless di AEM
