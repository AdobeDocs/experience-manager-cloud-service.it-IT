---
title: Modalità Sviluppatore
seo-title: Developer Mode
description: La modalità Sviluppatore apre un pannello laterale con diverse schede che forniscono a uno sviluppatore informazioni sulla pagina corrente
seo-description: Developer mode opens a side panel with several tabs that provide a developer with information about the current page
exl-id: fbf11c0f-dc6e-43f3-bcf2-080eacc6ba99
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 1%

---

# Modalità Sviluppatore {#developer-mode}

Durante la modifica di pagine in AEM, diverse [modalità](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) sono disponibili, inclusa la modalità Sviluppatore . La modalità Sviluppatore apre un pannello laterale con diverse schede che forniscono a uno sviluppatore informazioni tecniche sulla pagina corrente.

Sono disponibili due schede:

* **[Componenti](#components)** per visualizzare informazioni sulla struttura e sulle prestazioni.
* **[Errori](#errors)** per vedere eventuali problemi.

Queste consentono a uno sviluppatore di:

* **Scopri** modalità di composizione delle pagine.
* **Debug:** cosa succede dove e quando, che a sua volta aiuta a risolvere i problemi.

>[!NOTE]
>
>Modalità sviluppatore:
>
>* Non è disponibile su dispositivi mobili o piccole finestre sul desktop (a causa di limitazioni di spazio).
>  * Questo si verifica quando la larghezza è inferiore a 1024 px.
>* È disponibile solo per gli utenti che sono membri del gruppo `administrators` gruppo.


## Apertura della modalità Sviluppatore {#opening-developer-mode}

La modalità Sviluppatore viene implementata come pannello laterale nell’editor di pagine. Per aprire il pannello, seleziona **Sviluppatore** dal selettore modalità nella barra degli strumenti dell’editor di pagine:

![Apertura della modalità sviluppatore](assets/developer-mode.png)

Il pannello è diviso in due schede:

* **[Componenti](#components)** - Viene visualizzata una struttura ad albero dei componenti, simile a [struttura contenuto](/help/sites-cloud/authoring/fundamentals/environment-tools.md#content-tree) per autori
* **[Errori](#errors)** - Quando si verificano dei problemi, vengono visualizzati i dettagli di ciascun componente.

### Scheda Componenti {#components}

![Scheda Componenti](assets/developer-mode-components-tab.png)

Viene visualizzata una struttura ad albero dei componenti che:

* Illustra la catena di componenti e modelli di cui è stato eseguito il rendering sulla pagina. La struttura ad albero può essere espansa per mostrare il contesto all’interno della gerarchia.
* Mostra il tempo di calcolo lato server necessario per eseguire il rendering del componente.
* Consente di espandere la struttura ad albero e selezionare componenti specifici all’interno della struttura. La selezione permette di accedere ai dettagli dei componenti; quali:
   * Percorso archivio
   * Collegamenti agli script (a cui si accede in CRXDE Lite)
   * Dettagli del componente come mostrato nella [Console Componenti](/help/sites-cloud/authoring/features/components-console.md)
* I componenti selezionati nella struttura ad albero sono indicati da un bordo blu nell’editor.

Questa scheda dei componenti consente di:

* Determina e confronta il tempo di rendering per componente.
* Visualizzare e comprendere la gerarchia.
* Comprendere e quindi migliorare il tempo di caricamento della pagina trovando componenti lenti.

Ciascuna voce di componente può avere le seguenti opzioni:

![Esempio di componente in modalità Sviluppatore](assets/developer-mode-component-example.png)

* **Visualizza dettagli:** Collegamento a un elenco che mostra:
   * Tutti gli script dei componenti utilizzati per il rendering del componente.
   * Percorso del contenuto dell’archivio per questo componente specifico.

      ![Visualizza dettagli](assets/developer-mode-view-details.png)

* **Modifica script:** Collegamento che apre lo script del componente in CRXDE Lite.

* **Visualizza dettagli componente:** Apre i dettagli del componente all’interno di [Console Componenti.](/help/sites-cloud/authoring/features/components-console.md)

Quando si espande una voce di un componente toccando o facendo clic sulla freccia è anche possibile visualizzare:

    * La gerarchia all’interno del componente selezionato.
    * Tempi di rendering del componente selezionato in isolamento, di tutti i singoli componenti nidificati al suo interno e del totale combinato.

### Scheda Errori {#errors}

![Scheda Errori](assets/developer-mode-errors-tab.png)

Speriamo che **Errori** La scheda sarà sempre vuota (come sopra), ma quando si verificano problemi, per ciascun componente possono essere visualizzati i seguenti dettagli:

* Un avviso se il componente scrive una voce nel registro degli errori, insieme ai dettagli dell’errore e indirizza i collegamenti al codice appropriato all’interno di CRXDE Lite.
* Un avviso se il componente apre una sessione di amministrazione.

Ad esempio, se viene chiamato un metodo non definito, l’errore risultante verrà visualizzato nella sezione **Errori** e la voce del componente nella struttura del **Componenti** La scheda viene inoltre contrassegnata con un indicatore quando si verifica un errore.
