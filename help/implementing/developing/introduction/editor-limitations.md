---
title: Limitazioni per l’editor
description: L’editor nell’interfaccia touch utilizza le sovrapposizioni per interagire con contenuti confinati in un iframe. Questa interazione crea alcune limitazioni sia nell’utilizzo dell’editor che per gli sviluppatori.
exl-id: 6a4f0e43-1076-4da9-95dc-9c5bf83e30d0
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 10%

---

# Limitazioni per l’editor {#editor-limitations}

L’editor nell’interfaccia touch utilizza le sovrapposizioni per interagire con contenuti confinati in un iframe. Questa interazione crea alcune limitazioni sia nell’utilizzo dell’editor che per gli sviluppatori. Questa pagina riepiloga queste limitazioni e fornisce soluzioni o soluzioni alternative, ove possibile.

## Limitazioni funzionali {#functional-limitations}

Un autore può incontrare le seguenti limitazioni funzionali quando utilizza l’editor per creare le pagine.

### Collegamenti non attivi {#links-not-active}

Quando [modifica di una pagina](/help/sites-cloud/authoring/fundamentals/editing-content.md), i collegamenti non sono attivi.

* [Passa a **Anteprima** modalità](/help/sites-cloud/authoring/fundamentals/editing-content.md#preview-mode) per spostarsi utilizzando i collegamenti presenti nel contenuto.

### Pagine struttura {#structure-pages}

Le pagine non possono essere denominate `structure`. Pagine denominate `structure` non sarà modificabile nell’editor pagina.

## Limitazioni CSS {#css-limitations}

Uno sviluppatore può incontrare le seguenti limitazioni con le interazioni dell’editor con i CSS.

### Elementi posizionati in modo assoluto {#absolutely-positioned-elements}

Gli elementi posizionati in modo assoluto possono causare problemi nella posizione della sovrapposizione.

* In questo caso, accertati che le dimensioni dell’elemento con posizione assoluta siano corrette perché l’editor creerà una sovrapposizione con le stesse dimensioni.

### unità vh {#vh-units}

`vh` le unità non sono supportate perché l&#39;altezza dell&#39;iframe deve essere regolata automaticamente da AEM.

### Immagini di sfondo fisse {#fixed-background-images}

Le immagini di sfondo fisse potrebbero non essere visualizzate come fisse durante lo scorrimento a causa del fatto che sono incorporate all&#39;interno di un iframe.

* Selezione **Visualizza pagina come pubblicata** nella barra dell’intestazione le azioni visualizzano la pagina correttamente.

### Altezza 100% {#height}

L’altezza del 100% non è supportata nell’elemento corpo di una pagina.

* È possibile una soluzione alternativa per implementare un corpo a schermo intero &quot;allungando&quot; l&#39;elemento corpo come segue:

```xml
body {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
}
```

### Riduzione dei margini {#margin-collapsing}

I problemi di compressione del margine possono essere visti se il primo elemento figlio dell&#39;elemento corpo ha un margine.

* La soluzione è quella di aggiungere un clearfix a livello di elemento corpo, come segue:

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```
