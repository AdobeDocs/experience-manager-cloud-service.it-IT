---
title: Struttura dell’interfaccia AEM
description: L’interfaccia utente AEM presenta diversi principi di base ed è composta da diversi elementi chiave
translation-type: tm+mt
source-git-commit: 0799a817095558edd49b53ddc915c9474181fef7
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 2%

---


# Struttura dell’interfaccia AEM {#structure-of-the-aem-ui}

L’interfaccia AEM presenta diversi principi di base ed è composta da diversi elementi chiave:

## Console {#consoles}

### Layout di base e ridimensionamento {#basic-layout-and-resizing}

L’interfaccia utente è destinata sia ai dispositivi mobili che a quelli desktop, ma AEM creare due stili utilizza uno stile che funziona per tutti gli schermi e i dispositivi.

Tutti i moduli utilizzano lo stesso layout di base, AEM può essere visto come:

![della console AEM Sites](assets/ui-sites-console.png)

Il layout aderisce a uno stile di progettazione reattivo e si adatta alle dimensioni del dispositivo/finestra in uso.

Ad esempio, quando la risoluzione è inferiore a 1024 px (come su un dispositivo mobile), il display viene regolato di conseguenza:

![Vista mobile della console Siti](assets/ui-sites-mobile.png)

### Barra intestazione {#header-bar}

![Barra di intestazione AEM](assets/ui-header-bar.png)

La barra di intestazione mostra gli elementi globali, tra cui:

* Il logo e il prodotto/soluzione specifico attualmente in uso; per AEM questo collegamento viene creato anche un collegamento alla navigazione globale
* Ricerca
* Icona per accedere alle risorse della guida
* Icona per accedere ad altre soluzioni
* Indicatore di (e accesso a) eventuali avvisi o elementi in entrata in attesa
* L&#39;icona utente, insieme a un collegamento alla gestione del profilo

### Barra degli strumenti {#toolbar}

La barra degli strumenti è contestuale agli strumenti relativi alla posizione e alle superfici, utili per controllare la visualizzazione o le risorse nella pagina sottostante. La barra degli strumenti è specifica per il prodotto, ma gli elementi sono comuni.

In qualsiasi punto della barra degli strumenti sono visualizzate le azioni attualmente disponibili:

![barra degli strumenti AEM Sites](assets/ui-sites-toolbar.png)

Dipende anche dalla selezione di una risorsa:

![barra degli strumenti AEM Sites selezionata](assets/ui-sites-toolbar-selected.png)

### Barra a sinistra {#left-rail}

La barra a sinistra può essere aperta o nascosta come richiesto per mostrare:

* **Solo contenuto**
* **Struttura contenuto**
* **Timeline**
* **Riferimenti**
* **Filtro**

Il valore predefinito è Solo **** contenuto (barra laterale nascosta).

![Barra a sinistra](assets/ui-left-rail.png)

## Authoring delle pagine {#page-authoring}

Durante l’authoring delle pagine, le aree strutturali sono le seguenti:

### Cornice contenuto {#content-frame}

Il contenuto della pagina viene rappresentato nella cornice contenuto. La cornice contenuto è completamente indipendente dall&#39;editor, per garantire che non vi siano conflitti dovuti a CSS o javascript.

La cornice contenuto si trova nella sezione destra della finestra, sotto la barra degli strumenti.

![Cornice contenuto](assets/ui-content-frame.png)

### Editor Frame {#editor-frame}

Il frame dell&#39;editor abilita le funzioni di modifica.

La cornice dell’editor è un contenitore (astratto) per tutti gli elementi di authoring delle pagine. Vive sopra la cornice contenuto e include:

* Barra degli strumenti superiore
* Pannello laterale
* Tutte le sovrapposizioni
* Qualsiasi altro elemento di authoring delle pagine; ad esempio, la barra degli strumenti del componente

![Editor, fotogramma](assets/ui-editor-frame.png)

### Pannello laterale {#side-panel}

Contiene tre schede predefinite. Le schede **Risorse** e **Componenti** consentono di selezionare tali elementi e trascinarli dal pannello per poi rilasciarli sulla pagina. La scheda Struttura **** contenuto consente di esaminare la gerarchia del contenuto della pagina.

Per impostazione predefinita, il pannello laterale è nascosto. Se selezionata, la finestra viene visualizzata sul lato sinistro oppure scorrerà per coprire l’intera finestra quando la dimensione della finestra è inferiore a 1024 px; ad esempio su un dispositivo mobile.

![Pannello laterale](assets/ui-side-panel.png)

### Pannello laterale - Risorse {#side-panel-assets}

Nella scheda Risorse puoi selezionare una delle risorse disponibili. Potete anche filtrare un termine specifico o selezionare un gruppo.

![Scheda Risorse](assets/ui-side-panel-assets.png)

### Pannello laterale - Gruppi di risorse {#side-panel-asset-groups}

Nella scheda Risorse è disponibile un elenco a discesa che consente di selezionare i gruppi di risorse specifici.

![Gruppi di risorse](assets/ui-side-panel-asset-groups.png)

### Pannello laterale - Componenti {#side-panel-components}

Nella scheda Componenti è possibile selezionare uno dei componenti disponibili. Potete anche filtrare un termine specifico o selezionare un gruppo.

![Scheda Componenti](assets/ui-side-panel-components.png)

### Pannello laterale - Struttura contenuto {#side-panel-content-tree}

Nella scheda Struttura contenuto è possibile visualizzare la gerarchia del contenuto della pagina. Facendo clic su una voce nella scheda si passa a e si seleziona l&#39;elemento nella pagina all&#39;interno dell&#39;editor.

![Struttura contenuto](assets/ui-side-panel-content-tree.png)

### Sovrapposizioni {#overlays}

Questi elementi sovrappongono la cornice contenuto e vengono utilizzati dai [livelli](#layer) per comprendere la tecnica di interazione (completamente trasparente) con i componenti e il relativo contenuto.

Le sovrapposizioni sono live nella cornice dell’editor (con tutti gli altri elementi di authoring delle pagine), anche se sovrappongono effettivamente i componenti appropriati nella cornice contenuto.

![Sovrapposizioni](assets/ui-overlays.png)

### Livello {#layer}

Un livello è un pacchetto indipendente di funzionalità che può essere attivato per:

* Fornire una visualizzazione diversa della pagina
* Consentono di manipolare e/o interagire con una pagina

I livelli forniscono funzionalità sofisticate per l’intera pagina, anziché azioni specifiche su un singolo componente.

AEM sono disponibili diversi livelli già implementati per l’authoring delle pagine; ad esempio, potete modificare, visualizzare in anteprima e annotare i livelli.

>[!NOTE]
>
>I livelli sono un concetto potente che influisce sulla visualizzazione e l&#39;interazione dell&#39;utente con il contenuto della pagina. Quando sviluppate i vostri livelli, dovete assicurarvi che il livello si pulisca quando viene estratto.

### Commutatore livello {#layer-switcher}

Lo switcher di livello consente di scegliere il livello da usare. Una volta chiuso, indica il livello attualmente in uso.

Lo switcher di livello è disponibile come elenco a discesa dalla barra degli strumenti (nella parte superiore della finestra, all’interno della cornice dell’editor).

![Switcher livello](assets/ui-layer-switcher.png)

### Barra degli strumenti del componente {#component-toolbar}

Ogni istanza di un componente visualizzerà la propria barra degli strumenti quando viene fatto clic (una volta o con un doppio clic lento). La barra degli strumenti contiene le azioni specifiche (ad esempio, copia, incolla, editor aperto) disponibili per l’istanza del componente sulla pagina.

A seconda dello spazio disponibile, le barre degli strumenti dei componenti sono posizionate nell’angolo superiore o inferiore destro del componente appropriato.

![Barra degli strumenti del componente](assets/ui-component-toolbar.png)

## Ulteriori informazioni {#further-information}

<!--For more details about the concepts around the touch-enabled UI, continue to the article [Concepts of the AEM Touch-Enabled UI](/help/sites-developing/touch-ui-concepts.md).-->

Per ulteriori informazioni tecniche, consultate la documentazione [JS impostata](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html) per l&#39;editor pagina.
