---
title: Struttura dell’interfaccia AEM
description: L’interfaccia utente di AEM presenta diversi principi di base ed è composta da diversi elementi chiave
exl-id: ac211716-d699-4fdb-a286-a0a1122c86c5
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 3%

---

# Struttura dell’interfaccia AEM {#structure-of-the-aem-ui}

L’interfaccia utente di AEM presenta diversi principi di base ed è composta da diversi elementi chiave:

## Console {#consoles}

### Layout e ridimensionamento di base {#basic-layout-and-resizing}

L’interfaccia utente supporta sia i dispositivi mobili che quelli desktop; tuttavia, invece di creare due stili, AEM utilizza uno stile che funziona per tutti gli schermi e i dispositivi.

Tutti i moduli utilizzano lo stesso layout di base:

![Console AEM Sites](assets/ui-sites-console.png)

Il layout aderisce a uno stile di progettazione reattivo e si adatta alle dimensioni del dispositivo, della finestra o di entrambi, che si sta utilizzando.

Ad esempio, quando la risoluzione scende al di sotto di 1024 pixel (come su un dispositivo mobile), il display viene regolato di conseguenza:

![Visualizzazione mobile della console Sites](assets/ui-sites-mobile.png)

### Barra intestazione {#header-bar}

![Barra di intestazione di AEM](assets/ui-header-bar.png)

La barra dell’intestazione mostra gli elementi globali, tra cui:

* Il logo e il prodotto/soluzione specifico attualmente in uso. Per AEM, questo elemento costituisce anche un collegamento alla navigazione globale
* Ricerca
* Icona per accedere alle risorse della guida
* Icona per accedere ad altre soluzioni
* Indicatore e accesso a tutti gli avvisi o gli elementi della casella in entrata che ti aspettano
* L’icona utente, insieme a un collegamento per la gestione del profilo

### Barra degli strumenti {#toolbar}

La barra degli strumenti è contestuale alla posizione e mette in superficie gli strumenti rilevanti per il controllo della vista o delle risorse nella pagina seguente. La barra degli strumenti è specifica per il prodotto, ma presenta alcune caratteristiche in comune con gli elementi.

In qualsiasi posizione, la barra degli strumenti mostra le azioni attualmente disponibili:

![barra degli strumenti di AEM Sites](assets/ui-sites-toolbar.png)

Dipende anche dalla selezione di una risorsa:

![Barra degli strumenti di AEM Sites selezionata](assets/ui-sites-toolbar-selected.png)

### Barra a sinistra {#left-rail}

La barra a sinistra può essere aperta/nascosta come richiesto per mostrare:

* **Solo contenuto**
* **Struttura contenuto**
* **Timeline**
* **Riferimenti**
* **Filtro**

Il valore predefinito è **Solo contenuto** (barra nascosta).

![Barra a sinistra](assets/ui-left-rail.png)

## Authoring delle pagine {#page-authoring}

Quando si creano le pagine, le aree strutturali sono le seguenti.

### Frame del contenuto {#content-frame}

Il rendering del contenuto della pagina viene eseguito nel frame del contenuto. Il frame del contenuto è indipendente dall’editor, per garantire che non vi siano conflitti dovuti a CSS o JavaScript.

La cornice di contenuto si trova nella sezione destra della finestra, sotto la barra degli strumenti.

![Cornice contenuto](assets/ui-content-frame.png)

### Frame dell&#39;editor {#editor-frame}

Il frame dell&#39;editor abilita le funzioni di modifica.

Il frame dell’editor è un contenitore (astratto) per tutti gli elementi di authoring delle pagine. Si trova sopra la cornice del contenuto e include:

* Barra degli strumenti superiore
* Pannello laterale
* Tutte le sovrapposizioni
* Qualsiasi altro elemento di creazione pagina, ad esempio la barra degli strumenti del componente

![Frame editor](assets/ui-editor-frame.png)

### Pannello laterale {#side-panel}

Contiene tre schede predefinite. Le schede **Assets** e **Components** consentono di selezionare tali elementi e trascinarli dal pannello e rilasciarli sulla pagina. La scheda **Struttura contenuto** consente di controllare la gerarchia del contenuto nella pagina.

Il pannello laterale è nascosto per impostazione predefinita. Se questa opzione è selezionata, viene visualizzata sul lato sinistro o, se la larghezza della finestra è inferiore a 1024 pixel, scorre in avanti per coprire l’intera finestra come, ad esempio, su un dispositivo mobile.

![Pannello laterale](assets/ui-side-panel.png)

### Pannello laterale - Assets {#side-panel-assets}

Nella scheda Assets puoi selezionare una delle risorse disponibili. Puoi anche filtrare in base a un termine specifico o selezionare un gruppo.

![Scheda Assets](assets/ui-side-panel-assets.png)

### Pannello laterale - Gruppi di risorse {#side-panel-asset-groups}

Nella scheda Assets è disponibile un elenco a discesa che puoi utilizzare per selezionare i gruppi di risorse specifici.

![Gruppi di risorse](assets/ui-side-panel-asset-groups.png)

### Pannello laterale - Componenti {#side-panel-components}

Nella scheda Componenti puoi selezionare uno dei componenti disponibili. Puoi anche filtrare in base a un termine specifico o selezionare un gruppo.

![Scheda Componenti](assets/ui-side-panel-components.png)

### Pannello laterale - Struttura contenuto {#side-panel-content-tree}

Nella scheda Struttura contenuto è possibile visualizzare la gerarchia del contenuto della pagina. Facendo clic su una voce nella scheda, si passa a e si seleziona l’elemento nella pagina all’interno dell’editor.

![Struttura contenuto](assets/ui-side-panel-content-tree.png)

### Sovrapposizioni {#overlays}

Sovrappone il frame del contenuto e vengono utilizzati dai [livelli](#layer) per realizzare i meccanismi con cui puoi interagire in modo trasparente con i componenti e i relativi contenuti.

Le sovrapposizioni sono live nel frame dell’editor (con tutti gli altri elementi di authoring della pagina), anche se in realtà sovrappongono i componenti appropriati nel frame del contenuto.

![Sovrapposizioni](assets/ui-overlays.png)

### Layer {#layer}

Un livello è un bundle indipendente di funzionalità che può essere attivato per:

* Fornisci una visualizzazione diversa della pagina
* Consente di manipolare e/o interagire con una pagina

I livelli forniscono funzionalità avanzate per l’intera pagina, anziché azioni specifiche per un singolo componente.

AEM viene fornito con diversi livelli già implementati per l’authoring delle pagine, inclusi ad esempio i livelli Modifica, Anteprima e Annota.

>[!NOTE]
>
>I livelli sono un concetto potente che influisce sulla visualizzazione e sull’interazione dell’utente con il contenuto della pagina. Quando sviluppate i vostri livelli, assicuratevi che il livello si ripulisca quando esce.

### Switcher livello {#layer-switcher}

Il selettore livello consente di scegliere il livello da utilizzare. Quando è chiuso, indica il livello attualmente in uso.

Il selettore livelli è disponibile come elenco a discesa dalla barra degli strumenti (nella parte superiore della finestra, all’interno del frame dell’editor).

![Selettore livello](assets/ui-layer-switcher.png)

### Barra degli strumenti del componente {#component-toolbar}

Ogni istanza di un componente mostra la propria barra degli strumenti quando viene selezionata (una volta o con un doppio clic lento). La barra degli strumenti contiene le azioni specifiche (ad esempio, copia, incolla, open-editor) disponibili per l’istanza del componente nella pagina.

A seconda dello spazio disponibile, le barre degli strumenti del componente sono posizionate nell’angolo superiore o inferiore destro del componente appropriato.

![Barra degli strumenti del componente](assets/ui-component-toolbar.png)

## Ulteriori informazioni {#further-information}

<!--For more details about the concepts around the touch-enabled UI, continue to the article [Concepts of the AEM Touch-Enabled UI](/help/sites-developing/touch-ui-concepts.md).-->

Per ulteriori informazioni tecniche, consulta il [set di documentazione JS](https://developer.adobe.com/experience-manager/reference-materials/6-5/jsdoc/ui-touch/editor-core/index.html) per l&#39;editor pagina.

### Unified Shell {#unified-shell}

Consulta [AEM as a Cloud Service su Unified Shell](/help/overview/aem-cloud-service-on-unified-shell.md) se utilizzi Unified Shell come interfaccia utente di AEM.

Se hai bisogno di effettuare, o hai già fatto, qualsiasi personalizzazione, Unified Shall può essere disabilitato:

* [dall’interfaccia utente](/help/overview/aem-cloud-service-on-unified-shell.md#disabling-unified-shell)

* dal codice del progetto, da:

   * il `/conf/global/setting/unifiedshell`

      * impostazione della proprietà `Boolean` `enable` su `false`
