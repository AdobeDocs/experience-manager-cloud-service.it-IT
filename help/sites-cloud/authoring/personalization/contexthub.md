---
title: Visualizzare l’anteprima delle pagine utilizzando i dati di ContextHub
description: La barra degli strumenti di ContextHub visualizza dati dagli archivi di ContextHub, ti consente di modificare i dati archiviati ed è utile per visualizzare in anteprima il contenuto
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 89%

---


# Visualizzare l’anteprima delle pagine utilizzando i dati di ContextHub  {#previewing-pages-using-contexthub-data}

La barra degli strumenti di ContextHub mostra i dati provenienti dagli archivi di ContextHub e consente di modificare i dati store. La barra degli strumenti ContextHub è utile per visualizzare in anteprima il contenuto determinato dai dati di uno Store ContextHub.<!--The [ContextHub](/help/sites-developing/contexthub.md) toolbar displays data from ContextHub stores and enables you to change store data. The ContextHub toolbar is useful for previewing content that is determined by data in a ContextHub store.-->

La barra degli strumenti è composta da una serie di modalità di interfaccia utente che contengono uno o più moduli di interfaccia utente.

* Le modalità di interfaccia utente sono icone che vengono visualizzate sul lato sinistro della barra degli strumenti. Quando fai clic o tocchi un’icona, la barra degli strumenti rivela i moduli di interfaccia utente che contiene.
* I moduli di interfaccia utente visualizzano dati da uno o più archivi di ContextHub. Alcuni moduli di interfaccia utente ti consentono inoltre di manipolare i dati archiviati.

ContextHub installa varie modalità di interfaccia utente e moduli di interfaccia utente. L’amministratore può aver configurato ContextHub per visualizzarne di diversi.<!--ContextHub installs several UI modes and UI modules. Your administrator may have [configured ContextHub](/help/sites-administering/contexthub-config.md) to display different ones.-->

## Visualizzare la barra degli strumenti di ContextHub {#revealing-the-contexthub-toolbar}

La barra degli strumenti di ContextHub è disponibile nella modalità di anteprima. La barra degli strumenti è disponibile solo nelle istanze dell’autore e solo se l’amministratore l’ha abilitata.

![Barra degli strumenti ContextHub](/help/sites-cloud/authoring/assets/contexthub-toolbar.png)

1. Con la pagina aperta per la modifica, fai clic o tocca Anteprima nella barra degli strumenti.

   ![Pulsante Anteprima](/help/sites-cloud/authoring/assets/contexthub-preview-button.png)

1. Per visualizzare la barra degli strumenti, fai clic o tocca l’icona di ContextHub.

   ![Pulsante ContextHub](/help/sites-cloud/authoring/assets/contexthub-button.png)

## Funzioni dei moduli di interfaccia utente {#ui-module-features}

Ogni modulo di interfaccia utente fornisce un diverso insieme di funzioni, ma i seguenti tipi di funzioni sono comuni. Poiché i moduli di interfaccia utente sono estensibili, lo sviluppatore può implementare altre funzioni, a seconda delle necessità.

### Contenuto della barra degli strumenti {#toolbar-content}

I moduli di interfaccia utente possono visualizzare dati da uno o più archivi di ContextHub nella barra degli strumenti. I moduli dell’interfaccia utente utilizzano un’icona e un titolo per identificarsi.

![Personaggi ContextHub](/help/sites-cloud/authoring/assets/contexthub-persona-button.png)

### Contenuto a comparsa {#popup-content}

Alcuni moduli dell&#39;interfaccia utente visualizzano una sovrapposizione popup quando si fa clic su di essi o si tocca l&#39;utente. In genere, la finestra a comparsa contiene informazioni aggiuntive rispetto a quelle visualizzate nella barra degli strumenti.

![Informazioni sul profilo ContextHub](/help/sites-cloud/authoring/assets/contexthub-profile.png)

### Moduli a comparsa {#popup-forms}

La finestra a comparsa di un modulo può includere elementi modulo che ti consentono di modificare i dati nell’archivio di ContextHub. Se il contenuto della pagina viene determinato dai dati archiviati, puoi utilizzare il modulo e visualizzare le modifiche apportate al contenuto della pagina.

### Modalità a schermo intero {#fullscreen-mode}

Le finestre a comparsa possono includere un’icona su cui fare clic o toccare per espandere il contenuto a comparsa fino a coprire l’intera finestra del browser o schermata.

![Pulsante Schermo intero](/help/sites-cloud/authoring/assets/contexthub-fullscreen.png)
