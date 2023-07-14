---
title: Console Frammenti di contenuto
description: Scopri come gestire i frammenti di contenuto dalla console Frammenti di contenuto.
landing-page-description: Scopri come gestire i frammenti di contenuto dalla console Frammenti di contenuto. La console è incentrata sull’utilizzo di volumi elevati di frammenti di contenuto per casi d’uso headless, ma viene utilizzata anche per l’authoring delle pagine.
feature: Content Fragments
role: User
exl-id: 0e6e3b61-a0ca-44b8-914d-336e29761579
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 94%

---

# Console Frammenti di contenuto  {#content-fragments-console}

Scopri in che modo la console Frammenti di contenuto può ottimizzare l’accesso ai frammenti di contenuto, consentendoti di creare, cercare e gestire i frammenti eseguendo azioni amministrative quali pubblicare, annullare le pubblicazioni e copiare.

La console Frammenti di contenuto è dedicata a gestione, ricerca e creazione di frammenti di contenuto. È stata ottimizzata per l’utilizzo in un contesto headless, ma anche durante la creazione di frammenti di contenuto da usare nell’authoring delle pagine.

>[!NOTE]
>
>In questa console vengono visualizzati solo i frammenti di contenuto. Non visualizza altri tipi di risorse, come immagini e video.

>[!NOTE]
>
>L’accesso ai frammenti di contenuto attualmente è possibile tramite:
>
>* la presente console di **Frammenti di contenuto**;
>* la console **Assets** - vedi [Gestione dei frammenti di contenuto](/help/assets/content-fragments/content-fragments-managing.md)

>[!NOTE]
>
>Una selezione di [scelte rapide da tastiera è disponibile per questa console](/help/sites-cloud/administering/content-fragments/content-fragments-console-keyboard-shortcuts.md).

>[!NOTE]
>
>Se necessario, il team del progetto può personalizzare la console. Per ulteriori dettagli, consulta [Personalizzazione della console Frammenti di contenuto](/help/implementing/developing/extending/content-fragment-console-customizing.md).

È possibile accedere direttamente alla console Frammenti di contenuto dal livello superiore della navigazione globale:

![Navigazione globale - Console Frammenti di contenuto](assets/cfc-global-navigation.png)

## Struttura e gestione di base della console {#basic-structure-handling-content-fragments-console}

Selezionando **Frammenti di contenuto** verrà aperta la console in una nuova scheda.

![Console Frammenti di contenuto - Panoramica](assets/cfc-console-overview.png)

Nella console puoi osservare tre aree principali:

* Barra degli strumenti superiore
   * Fornisce le funzionalità standard di AEM
   * Mostra anche la tua organizzazione IMS
* Pannello a sinistra
   * Qui puoi nascondere o visualizzare la struttura delle cartelle
   * Puoi selezionare un ramo specifico della struttura
   * Può essere ridimensionato per mostrare le cartelle nidificate
* Pannello principale/destro; da qui puoi:
   * Visualizzare l’elenco di tutti i frammenti di contenuto nel ramo selezionato della struttura:
      * La posizione è indicata dalle breadcrumb; puoi utilizzarle anche per modificare la posizione
      * Vengono visualizzati i frammenti di contenuto della cartella selezionata e tutte le cartelle secondarie:
         * [Vari campi di informazioni](#selectuse-available-columns) su un frammento di contenuto forniscono collegamenti con cui, a seconda del campo, è possibile:
            * Aprire il frammento appropriato nell’editor
            * Mostrare informazioni sui riferimenti
            * Mostrare informazioni sulle versioni linguistiche del frammento
      * Posizionando il cursore del mouse sulle intestazioni di colonna, viene visualizzato un selettore di azioni a discesa e dei cursori di larghezza. Queste ti consentono di effettuare le seguenti operazioni:
         * Ordinare: selezionando l’azione appropriata per ordine crescente o decrescente. 
In questo modo l’intera tabella viene ordinata in base a tale colonna. L’ordinamento è disponibile solo nelle colonne appropriate.
         * Ridimensiona la colonna: utilizzando i cursori di azione o di larghezza

## Azioni {#actions}

Nella console sono disponibili diverse azioni utilizzabili direttamente o dopo aver selezionato un frammento specifico:

* Varie azioni sono [disponibili direttamente dalla console](#available-actions)
* È possibile [selezionare uno o più frammenti di contenuto per visualizzare le azioni disponibili](#actions-selected-content-fragment)

### Azioni (non selezionate) {#actions-unselected}

Alcune azioni sono disponibili dalla console senza selezionare un frammento di contenuto specifico:

* **[Creare](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#creating-a-content-fragment)** un nuovo frammento di contenuto
* [Filtrare](#filtering-fragments) i frammenti di contenuto in base a una selezione di predicati e salvare il filtro per utilizzi futuri
* [Ricercare](#searching-fragments) i frammenti di contenuto
* [Personalizzare la vista tabella per mostrare le colonne di informazioni selezionate](#select-available-columns)
* Utilizzare **Apri in Assets** per aprire direttamente la posizione corrente nella console **Assets**

  >[!NOTE]
  >
  >La console **Assets** viene utilizzata per accedere alle risorse, ad esempio immagini, video e così via.  È possibile accedere a questa console:
  >
  >* utilizzando il collegamento **Apri in Assets** (nella console Frammenti di contenuto);
  >* direttamente dal riquadro di navigazione globale

### Azioni per un frammento di contenuto (selezionato) {#actions-selected-content-fragment}

Quando si seleziona un frammento specifico, viene aperta una barra degli strumenti incentrata sulle azioni disponibili per tale frammento. Puoi anche selezionare più frammenti; la selezione delle azioni viene regolata di conseguenza.

![Console Frammenti di contenuto; barra degli strumenti per un frammento selezionato](assets/cfc-fragment-toolbar.png)

* **Apri**
* **[Pubblica](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#publishing-and-previewing-a-fragment)** (e **[Annulla pubblicazione](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#unpublishing-a-fragment)**)
* **Copia**
* **Sposta**
* **Rinomina**
* **[Elimina](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#deleting-a-fragment)**

>[!NOTE]
>
>Azioni come Pubblica, Annulla pubblicazione, Elimina, Sposta, Rinomina, Copia, attivano un processo asincrono. L’avanzamento di tale processo può essere monitorato tramite l’interfaccia dei processi asincroni di AEM.

## Informazioni fornite sui frammenti di contenuto {#information-content-fragments}

Il pannello principale (vista tabella) della console, a destra, fornisce una serie di informazioni sui frammenti di contenuto. Alcuni elementi forniscono anche collegamenti diretti a ulteriori azioni e/o informazioni:

* **Nome**
   * Fornisce un collegamento per aprire il frammento nell’editor.
* **Modello**
   * Fornisce un collegamento per aprire il frammento nell’editor.
* **Cartella**
   * Fornisce un collegamento per aprire la cartella nella console.
Passando il puntatore del mouse sul nome della cartella verrà visualizzato il percorso JCR.
* **Stato**
   * Solo informazioni
* **Anteprima**
   * Solo informazioni:
      * **In sincronizzazione**: il frammento di contenuto è in sincronizzazione nei servizi di **authoring** e **anteprima**.
      * **Fuori sincronizzazione**: il frammento di contenuto è fuori sincronizzazione nei servizi di **authoring** e **anteprima**. È necessario **Pubblica** in **Anteprima** per garantire che le due istanze tornino ad essere sincronizzate.
      * vuoto: il frammento di contenuto non esiste nel servizio di **Anteprima**.
* **Modificato**
   * Solo informazioni
* **Modificato da**
   * Solo informazioni
* **Pubblicazione**
   * Solo informazioni
* **Pubblicato da**
   * Solo informazioni
* **Con riferimento da**

   * Fornisce un collegamento che apre una finestra di dialogo in cui sono elencati tutti i riferimenti principali di quel frammento, compresi i frammenti di contenuto, frammenti di esperienza e pagine. Per aprire un riferimento specifico, fai clic sul **Titolo** nella finestra di dialogo.

     ![Console Frammenti di contenuto - Finestra di dialogo Riferimenti](assets/cfc-console-references-dialog.png)

* **Lingua**

   * Indica la lingua del frammento di contenuto e il numero totale di copie per lingua associate al frammento di contenuto.

     ![Console Frammenti di contenuto - Indicatore della lingua](assets/cfc-console-language-indicator.png)

      * Tocca o fai clic sul numero per aprire una finestra di dialogo in cui sono visualizzate tutte le copie per altre lingue. Per aprire una copia di una specifica lingua, fai clic sul **Titolo** nella finestra di dialogo.

        ![Console Frammenti di contenuto - Finestra di dialogo Lingua](assets/cfc-console-languages-dialog.png)

## Selezionare le colonne disponibili {#select-available-columns}

Come per altre console, puoi configurare le colonne visibili e disponibili da utilizzare:

![Console Frammenti di contenuto - Configurazione delle colonne](assets/cfc-console-column-icon.png)

Presenta un elenco di colonne che puoi nascondere o mostrare:

![Console Frammenti di contenuto - Configurazione delle colonne](assets/cfc-console-column-selection.png)

## Filtrare i frammenti {#filtering-fragments}

Il pannello Filtro offre:

* una selezione di predicati; è possibile selezionare uno o più predicati e combinarli per creare il filtro
* l’opportunità di salvare la configurazione mediante il comando **Salva**
* l’opzione di recuperare un filtro di ricerca salvato per il riutilizzo

![Console Frammenti di contenuto - Filtro](assets/cfc-console-filter.png)

### Filtro rapido {#fast-filtering}

Puoi anche selezionare un predicato facendo clic su un valore di colonna specifico nell’elenco. Puoi selezionare uno o più valori per combinare i predicati.

Ad esempio, seleziona **Pubblicato** nella colonna **Stato**:

>[!NOTE]
>
>Il filtro rapido è supportato solo per le colonne **Modello**, **Stato**, **Modificato da** e **Pubblicato da**.

![Console Frammenti di contenuto - Filtro](assets/cfc-console-fast-filter-01.png)

Dopo la selezione, viene visualizzato come predicato di filtro e l’elenco viene filtrato di conseguenza:

![Console Frammenti di contenuto - Filtro](assets/cfc-console-fast-filter-02.png)

## Ricerca di frammenti {#searching-fragments}

La casella di ricerca supporta la ricerca full-text. Immetti i termini di ricerca nella casella di ricerca:

![Console Frammenti di contenuto - Ricerca](assets/cfc-console-search-01.png)

Fornirà i risultati selezionati:

![Console Frammenti di contenuto - Risultati della ricerca](assets/cfc-console-search-02.png)

La casella di ricerca consente inoltre di accedere rapidamente a **Frammenti di contenuto recenti** e **Ricerche salvate**:

![Console Frammenti di contenuto - Recenti e salvati](assets/cfc-console-search-03.png)
