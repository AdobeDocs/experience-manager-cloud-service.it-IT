---
title: Modalità Sviluppatore
seo-title: Developer Mode
description: Modalità sviluppatore apre un pannello laterale con diverse schede che forniscono a uno sviluppatore informazioni sulla pagina corrente
seo-description: Developer mode opens a side panel with several tabs that provide a developer with information about the current page
exl-id: fbf11c0f-dc6e-43f3-bcf2-080eacc6ba99
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 1%

---

# Modalità Sviluppatore {#developer-mode}

Durante la modifica delle pagine in AEM, diversi [modalità](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) , inclusa la modalità Sviluppatore. La modalità Sviluppatore apre un pannello laterale con diverse schede che forniscono a uno sviluppatore informazioni tecniche sulla pagina corrente.

Sono disponibili due schede:

* **[Componenti](#components)** per visualizzare informazioni sulla struttura e sulle prestazioni.
* **[Errori](#errors)** per visualizzare eventuali problemi che si verificano.

Questi aiutano uno sviluppatore a:

* **Scoprire** come vengono composte le pagine.
* **Debug:** cosa succede dove e quando, il che a sua volta aiuta a risolvere i problemi.

>[!NOTE]
>
>Modalità sviluppatore:
>
>* Non è disponibile su dispositivi mobili o piccole finestre sul desktop (a causa di limitazioni di spazio).
>  * Ciò si verifica quando la larghezza è inferiore a 1024 px.
>* È disponibile solo per gli utenti che sono membri di `administrators` gruppo.


## Apertura modalità sviluppatore {#opening-developer-mode}

La modalità Sviluppatore viene implementata come pannello laterale nell’editor di pagine. Per aprire il pannello, seleziona **Sviluppatore** dal selettore modalità nella barra degli strumenti dell’editor pagina:

![Apertura della modalità sviluppatore](assets/developer-mode.png)

Il pannello è diviso in due schede:

* **[Componenti](#components)** : mostra una struttura ad albero dei componenti, simile alla [struttura contenuto](/help/sites-cloud/authoring/fundamentals/environment-tools.md#content-tree) per autori
* **[Errori](#errors)** - Quando si verificano dei problemi, vengono visualizzati i dettagli per ciascun componente.

### Scheda Componenti {#components}

![Scheda Componenti](assets/developer-mode-components-tab.png)

Viene mostrata una struttura ad albero componente che:

* Consente di definire la catena di componenti e modelli di cui è stato eseguito il rendering sulla pagina. La struttura può essere espansa per mostrare il contesto all’interno della gerarchia.
* Mostra il tempo di calcolo lato server necessario per eseguire il rendering del componente.
* Consente di espandere la struttura e selezionare componenti specifici all&#39;interno della struttura. La selezione consente di accedere ai dettagli dei componenti, ad esempio:
   * Percorso archivio
   * Collegamenti agli script (a cui si accede in CRXDE Lite)
   * Dettagli del componente come mostrato nella [Console Componenti](/help/sites-cloud/authoring/features/components-console.md)
* I componenti selezionati nella struttura sono indicati da un bordo blu nell’editor.

Questa scheda dei componenti consente di:

* Determina e confronta il tempo di rendering per componente.
* Visualizzare e comprendere la gerarchia.
* Scopri e quindi migliora il tempo di caricamento della pagina individuando i componenti lenti.

Ciascuna voce di componente può avere le seguenti opzioni:

![Esempio di componente in modalità sviluppatore](assets/developer-mode-component-example.png)

* **Visualizza dettagli:** Un collegamento a un elenco che mostra:
   * Tutti gli script dei componenti utilizzati per eseguire il rendering del componente.
   * Percorso del contenuto dell’archivio per questo componente specifico.

      ![Visualizza dettagli](assets/developer-mode-view-details.png)

* **Modifica script:** Un collegamento che apre lo script del componente in CRXDE Lite.

* **Visualizza dettagli componenti:** Apre i dettagli del componente all&#39;interno di [Console Componenti.](/help/sites-cloud/authoring/features/components-console.md)

Inoltre, l’espansione di una voce di componente toccando o facendo clic sulla freccia può mostrare:

    * Gerarchia all’interno del componente selezionato.
    * Tempi di rendering per il componente selezionato isolato, tutti i singoli componenti nidificati al suo interno e il totale combinato.

### Scheda Errori {#errors}

![Scheda Errori](assets/developer-mode-errors-tab.png)

Si spera che **Errori** La scheda sarà sempre vuota (come sopra), ma in caso di problemi possono essere visualizzati i seguenti dettagli per ciascun componente:

* Un avviso se il componente scrive una voce nel registro degli errori, insieme a dettagli dell’errore e collegamenti diretti al codice appropriato all’interno di CRXDE Lite.
* Un avviso se il componente apre una sessione di amministrazione.

Ad esempio, se si chiama un metodo non definito, l&#39;errore risultante verrà visualizzato nel **Errori** e la voce del componente nella struttura ad albero del **Componenti** verrà inoltre contrassegnata con un indicatore quando si verifica un errore.
