---
title: Visualizzare l’anteprima delle pagine utilizzando i dati di ContextHub
description: La barra degli strumenti di ContextHub visualizza dati dagli archivi di ContextHub, ti consente di modificare i dati archiviati ed è utile per visualizzare in anteprima il contenuto
exl-id: 9c0536c5-900e-4814-9e31-f9fee5adc17c
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: ht
source-wordcount: '368'
ht-degree: 100%

---

# Visualizzare l’anteprima delle pagine utilizzando i dati di ContextHub  {#previewing-pages-using-contexthub-data}

La barra degli strumenti di ContextHub mostra i dati provenienti dagli archivi di ContextHub e consente di modificare i dati store. La barra degli strumenti ContextHub è utile per visualizzare in anteprima il contenuto determinato dai dati di uno Store ContextHub.

La barra degli strumenti è composta da una serie di modalità di interfaccia utente che contengono uno o più moduli di interfaccia utente.

* Le modalità di interfaccia utente sono icone che vengono visualizzate sul lato sinistro della barra degli strumenti. Quando fai clic o tocchi un’icona, la barra degli strumenti rivela i moduli di interfaccia utente che contiene.
* I moduli di interfaccia utente visualizzano dati da uno o più archivi di ContextHub. Alcuni moduli di interfaccia utente ti consentono inoltre di manipolare i dati archiviati.

ContextHub installa varie modalità di interfaccia utente e moduli di interfaccia utente. L’amministratore può aver [configurato ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md) per visualizzarne di diversi.

## Visualizzare la barra degli strumenti di ContextHub {#revealing-the-contexthub-toolbar}

La barra degli strumenti di ContextHub è disponibile nella modalità di anteprima. La barra degli strumenti è disponibile solo nelle istanze dell’autore e solo se l’amministratore l’ha abilitata.

![Barra degli strumenti di ContextHub](/help/sites-cloud/authoring/assets/contexthub-toolbar.png)

1. Con la pagina aperta per la modifica, fai clic o tocca Anteprima nella barra degli strumenti.

   ![Pulsante Anteprima](/help/sites-cloud/authoring/assets/contexthub-preview-button.png)

1. Per visualizzare la barra degli strumenti, fai clic o tocca l’icona di ContextHub.

   ![Pulsante ContextHub](/help/sites-cloud/authoring/assets/contexthub-button.png)

## Funzioni dei moduli di interfaccia utente {#ui-module-features}

Ogni modulo di interfaccia utente fornisce un diverso insieme di funzioni, ma i seguenti tipi di funzioni sono comuni. Poiché i moduli di interfaccia utente sono estensibili, lo sviluppatore può implementare altre funzioni, a seconda delle necessità.

### Contenuto della barra degli strumenti {#toolbar-content}

I moduli di interfaccia utente possono visualizzare dati da uno o più archivi di ContextHub nella barra degli strumenti. I moduli di interfaccia utente utilizzano un’icona e un titolo per identificarsi. 

![Persone ContextHub](/help/sites-cloud/authoring/assets/contexthub-persona-button.png)

### Contenuto a comparsa {#popup-content}

Alcuni moduli di interfaccia utente visualizzano una finestra a comparsa quando l’utente fa clic su di essi o li seleziona mediante un tocco. In genere, la finestra a comparsa contiene informazioni aggiuntive rispetto a quelle visualizzate nella barra degli strumenti.

![Informazioni sul profilo ContextHub](/help/sites-cloud/authoring/assets/contexthub-profile.png)

### Moduli a comparsa {#popup-forms}

La finestra a comparsa di un modulo può includere elementi modulo che ti consentono di modificare i dati nell’archivio di ContextHub. Se il contenuto della pagina viene determinato dai dati archiviati, puoi utilizzare il modulo e visualizzare le modifiche apportate al contenuto della pagina.

### Modalità a schermo intero {#fullscreen-mode}

Le finestre a comparsa possono includere un’icona su cui fare clic o toccare per espandere il contenuto a comparsa fino a coprire l’intera finestra del browser o schermata.

![Pulsante Schermo intero](/help/sites-cloud/authoring/assets/contexthub-fullscreen.png)
