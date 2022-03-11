---
title: Struttura dell’interfaccia AEM
description: L’interfaccia utente AEM presenta diversi principi di base ed è composta da diversi elementi chiave
exl-id: ac211716-d699-4fdb-a286-a0a1122c86c5
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 3%

---

# Struttura dell’interfaccia AEM {#structure-of-the-aem-ui}

L’interfaccia utente AEM presenta diversi principi di base ed è composta da diversi elementi chiave:

## Console {#consoles}

### Layout di base e ridimensionamento {#basic-layout-and-resizing}

L’interfaccia utente è adatta sia ai dispositivi mobili che a quelli desktop, ma AEM invece di creare due stili, utilizza uno stile che funziona per tutti gli schermi e i dispositivi.

Tutti i moduli utilizzano lo stesso layout di base, AEM può essere visualizzato come segue:

![Console AEM Sites](assets/ui-sites-console.png)

Il layout aderisce a uno stile di progettazione reattivo e si adatta alle dimensioni del dispositivo o della finestra in uso.

Ad esempio, quando la risoluzione è inferiore a 1024 px (come su un dispositivo mobile), il display viene regolato di conseguenza:

![Vista mobile della console Sites](assets/ui-sites-mobile.png)

### Barra intestazione {#header-bar}

![Barra di intestazione AEM](assets/ui-header-bar.png)

La barra dell’intestazione mostra gli elementi globali, tra cui:

* Logo e prodotto/soluzione specifico attualmente in uso; per AEM si tratta anche di un collegamento alla navigazione globale
* Ricerca
* Icona per accedere alle risorse dell’Aiuto
* Icona per accedere ad altre soluzioni
* Indicatore di eventuali avvisi o elementi della casella in entrata in attesa (e accesso a)
* Icona utente e collegamento alla gestione del profilo

### Barra degli strumenti {#toolbar}

La barra degli strumenti è contestuale agli strumenti relativi alla posizione e alle superfici, utili per controllare la visualizzazione o le risorse nella pagina seguente. La barra degli strumenti è specifica per il prodotto, ma esiste una certa comunanza tra gli elementi.

In qualsiasi posizione la barra degli strumenti mostra le azioni attualmente disponibili:

![Barra degli strumenti di AEM Sites](assets/ui-sites-toolbar.png)

Dipende anche dal fatto che una risorsa sia attualmente selezionata o meno:

![Barra degli strumenti di AEM Sites selezionata](assets/ui-sites-toolbar-selected.png)

### Barra a sinistra {#left-rail}

La barra a sinistra può essere aperta o nascosta in base alle esigenze:

* **Solo contenuto**
* **Struttura contenuto**
* **Timeline**
* **Riferimenti**
* **Filtro**

Il valore predefinito è **Solo contenuto** (barra nascosta).

![Barra a sinistra](assets/ui-left-rail.png)

## Authoring delle pagine {#page-authoring}

Durante l’authoring delle pagine, le aree strutturali sono le seguenti:

### Frame di contenuto {#content-frame}

Viene eseguito il rendering del contenuto della pagina nel frame del contenuto. La cornice contenuto è completamente indipendente dall’editor, per garantire che non ci siano conflitti dovuti a CSS o javascript.

La cornice contenuto si trova nella sezione destra della finestra, sotto la barra degli strumenti.

![Cornice contenuto](assets/ui-content-frame.png)

### Frame editor {#editor-frame}

Il frame dell&#39;editor abilita le funzioni di modifica.

La cornice dell’editor è un contenitore (astratto) per tutti gli elementi di authoring delle pagine. Si trova sopra la cornice del contenuto e include:

* Barra degli strumenti superiore
* Pannello laterale
* Tutte le sovrapposizioni
* Qualsiasi altro elemento di authoring delle pagine; ad esempio, la barra degli strumenti del componente

![Frame dell&#39;editor](assets/ui-editor-frame.png)

### Pannello laterale {#side-panel}

Contiene tre schede predefinite. La **Risorse** e **Componenti** le schede consentono di selezionare tali elementi e trascinarli dal pannello e rilasciarli sulla pagina. La **Struttura contenuto** consente di controllare la gerarchia del contenuto della pagina.

Il pannello laterale è nascosto per impostazione predefinita. Se selezionata, la finestra verrà visualizzata sul lato sinistro o scivolerà lungo per coprire l&#39;intera finestra quando la dimensione della finestra è inferiore a 1024 px; come, ad esempio, su un dispositivo mobile.

![Pannello laterale](assets/ui-side-panel.png)

### Pannello laterale - Risorse {#side-panel-assets}

Nella scheda Risorse puoi selezionare un intervallo di risorse. Puoi anche filtrare un termine specifico o selezionare un gruppo.

![Scheda Risorse](assets/ui-side-panel-assets.png)

### Pannello laterale - Gruppi di risorse {#side-panel-asset-groups}

Nella scheda Risorse è disponibile un elenco a discesa che puoi utilizzare per selezionare i gruppi di risorse specifici.

![Gruppi di risorse](assets/ui-side-panel-asset-groups.png)

### Pannello laterale - Componenti {#side-panel-components}

Nella scheda Componenti puoi selezionare uno dei diversi componenti disponibili. Puoi anche filtrare un termine specifico o selezionare un gruppo.

![Scheda Componenti](assets/ui-side-panel-components.png)

### Pannello laterale - Struttura contenuto {#side-panel-content-tree}

Nella scheda Struttura contenuto è possibile visualizzare la gerarchia del contenuto della pagina. Facendo clic su una voce nella scheda si passa all’elemento nella pagina nell’editor e lo si seleziona.

![Struttura contenuto](assets/ui-side-panel-content-tree.png)

### Sovrapposizioni {#overlays}

Sovrappongono il frame del contenuto e vengono utilizzati dal [livelli](#layer) realizzare la meccanica su come interagire (in modo completamente trasparente) con i componenti e i loro contenuti.

Le sovrapposizioni sono presenti nel frame dell’editor (con tutti gli altri elementi di authoring delle pagine), anche se sovrappongono i componenti appropriati nel frame del contenuto.

![Sovrapposizioni](assets/ui-overlays.png)

### Livello {#layer}

Un livello è un bundle indipendente di funzionalità che può essere attivato per:

* Fornire una visualizzazione diversa della pagina
* Consente di manipolare e/o interagire con una pagina

I livelli forniscono funzionalità sofisticate per l’intera pagina, anziché azioni specifiche su un singolo componente.

AEM include diversi livelli già implementati per l’authoring delle pagine; ad esempio, modificare, visualizzare in anteprima e annotare i livelli.

>[!NOTE]
>
>I livelli sono un concetto potente che influisce sulla visualizzazione e sull’interazione dell’utente con il contenuto della pagina. Quando si sviluppano i propri livelli, è necessario assicurarsi che il livello si ripulisca quando viene lasciato.

### Selettore livello {#layer-switcher}

Lo switcher di livello consente di scegliere il livello da utilizzare. Una volta chiuso, indica il livello attualmente in uso.

Il commutatore di livello è disponibile come un menu a discesa dalla barra degli strumenti (nella parte superiore della finestra, all’interno della cornice dell’editor).

![Selettore livello](assets/ui-layer-switcher.png)

### Barra degli strumenti del componente {#component-toolbar}

Ogni istanza di un componente mostra la relativa barra degli strumenti quando viene fatto clic su (una volta o con un doppio clic lento). La barra degli strumenti contiene le azioni specifiche (ad esempio copia, incolla, editor aperto) disponibili per l’istanza del componente sulla pagina.

A seconda dello spazio disponibile, le barre degli strumenti dei componenti sono posizionate nell’angolo superiore o inferiore destro del componente appropriato.

![Barra degli strumenti del componente](assets/ui-component-toolbar.png)

## Ulteriori informazioni {#further-information}

<!--For more details about the concepts around the touch-enabled UI, continue to the article [Concepts of the AEM Touch-Enabled UI](/help/sites-developing/touch-ui-concepts.md).-->

Per ulteriori informazioni tecniche consulta la sezione [Set di documentazione JS](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html) per l’editor pagina.
