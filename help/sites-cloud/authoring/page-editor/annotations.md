---
title: Aggiunta di annotazioni di pagina
description: La modalità di annotazione consente di lasciare annotazioni e schizzi sulle pagine, in modo da facilitare il processo di revisione dei contenuti
exl-id: a9cb9745-8140-4795-a5f9-fb3a1a299bd8
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 72%

---

# Aggiunta di annotazioni di pagina {#adding-page-annotations}

La creazione di contenuti per la tua esperienza digitale richiede spesso discussioni e feedback prima della pubblicazione. Per facilitare questo processo di feedback, AEM consente di aggiungere annotazioni al contenuto.

Un’annotazione si presenta come uno schizzo o una nota semplice (pensa alle note adesiva) applicata alla pagina. L’annotazione consente di lasciare commenti o domande per altri autori e revisori.

>[!TIP]
>
>Sono disponibili anche i [commenti](/help/sites-cloud/authoring/basic-handling.md#timeline) per fornire feedback in una pagina.

Per la creazione e la visualizzazione delle annotazioni viene utilizzata una [modalità](/help/sites-cloud/authoring/page-editor/introduction.md#mode-selector) speciale.

>[!TIP]
>
>Se necessario, puoi anche sviluppare un [flusso di lavoro](/help/sites-cloud/authoring/workflows/overview.md) per inviare una notifica quando vengono aggiunte, aggiornate o eliminate delle annotazioni.

## Indicatore di annotazione {#annotation-indicator}

Le annotazioni non vengono visualizzate in modalità Modifica, ma il contrassegno in alto a destra della barra degli strumenti mostra il numero di annotazioni esistenti per la pagina corrente. Il contrassegno sostituisce l’icona Annotazioni predefinita, ma continua a fungere da collegamento rapido per attivare o disattivare la modalità Annota:

![Indicatore di annotazione](/help/sites-cloud/authoring/assets/annotation-indicator.png)

## Modalità Annota {#annotate-mode}

Le annotazioni sono visibili solo in modalità Annota.

1. Per accedere alla modalità Annota utilizza la relativa icona nella barra degli strumenti (in alto a destra) durante la modifica di una pagina:

   ![Pulsante Annotazione](/help/sites-cloud/authoring/assets/annotations.png)

   È ora possibile visualizzare tutte le annotazioni esistenti.

   ![Esempi di annotazione](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. Seleziona l’annotazione per aprirla e visualizzarne i dettagli.

   ![Dettagli annotazione](/help/sites-cloud/authoring/assets/annotation-adding.png)

1. Per uscire dalla modalità Annota e tornare alla modalità precedente, selezionare il pulsante x a destra della barra degli strumenti superiore.

## Aggiunta e modifica di annotazioni {#annotating-a-component}

Oltre a visualizzare le annotazioni, la modalità Annota consente di creare, modificare, spostare o eliminare le annotazioni nel contenuto

1. [Modalità Avvia annotazione](#annotate-mode) sulla pagina.

1. Per iniziare ad aggiungere annotazioni, seleziona l’icona Aggiungi annotazione (simbolo + a sinistra della barra degli strumenti).

1. Seleziona il componente richiesto (i componenti ai quali è possibile aggiungere annotazioni sono evidenziati da un bordo blu) per aggiungere l’annotazione e aprire la relativa finestra di dialogo:

   ![Aggiunta di un’annotazione](/help/sites-cloud/authoring/assets/annotation-adding.png)

   Utilizzando il campo e/o l’icona appropriata puoi effettuare le seguenti operazioni:

   * Inserisci il testo dell’annotazione.
   * Crea uno schizzo (linee e forme) per evidenziare un’area del componente.

     ![Pulsante Schizzo per l’annotazione](/help/sites-cloud/authoring/assets/annotation-sketch.png)

     Quando crei uno schizzo, il cursore si trasforma in un puntatore a croce. Puoi disegnare più linee distinte. La linea dello schizzo ha lo stesso colore dell’annotazione e può essere una freccia, un cerchio o un ovale.

   * Scegli o modifica il colore:

     ![Pulsante Campione colore per l’annotazione](/help/sites-cloud/authoring/assets/annotation-color-swatch.png)

1. Per chiudere la finestra di dialogo dell’annotazione, tocca o fai clic all’esterno della finestra di dialogo. Di seguito viene illustrata un’annotazione troncata con relativi schizzi:

   ![Schizzi per annotazione](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. Dopo aver modificato un’annotazione, puoi effettuare le seguenti operazioni:

   * Selezionare l&#39;indicatore di testo per aprire l&#39;annotazione. Una volta aperto, è possibile visualizzare il testo completo, apportare modifiche o [eliminare l&#39;annotazione](#deleting-annotations).
   * Riposiziona il marcatore di testo.
   * Selezionate una linea di sketch per selezionarlo e trascinarlo nella posizione desiderata.
   * Spostare o copiare un componente
      * Vengono spostate o copiate anche tutte le annotazioni e gli schizzi associati, mantenendo la stessa posizione in relazione al paragrafo.


>[!NOTE]
>
>Non è possibile aggiungere annotazioni a una pagina bloccata da un altro utente.

>[!NOTE]
>
>Nella definizione di un singolo tipo di componente è possibile specificare se l’aggiunta di annotazioni è supportata o meno per le istanze del componente.

## Eliminazione di annotazioni e schizzi {#deleting-annotations}

È possibile eliminare le annotazioni e gli schizzi associati.

1. [Avvia modalità annota](#annotate-mode) sulla pagina.

1. Selezionare l&#39;indicatore di testo per aprire l&#39;annotazione.

1. Seleziona l’icona Elimina.

   ![Elimina annotazione](/help/sites-cloud/authoring/assets/annotation-delete.png)

1. L’annotazione e tutti gli schizzi associati vengono eliminati.

>[!NOTE]
>
>Se si elimina un componente, vengono anche eliminate tutte le annotazioni e gli schizzi associati ad esso, indipendentemente dalla loro posizione sulla pagina.

## Eliminazione solo degli schizzi {#deleting-sketches}

Con tutti gli schizzi associati è possibile eliminare solo gli schizzi specifici invece dell’intera annotazione.

1. [Avvia Modalità annota](#annotate-mode) sulla pagina.

1. Selezionate lo sketch. AEM lo evidenzia con una casella blu più scura.

   ![Seleziona lo schizzo da eliminare](/help/sites-cloud/authoring/assets/annotation-sketch-delete.png)

1. Premi il tasto Canc sulla tastiera.

1. Lo schizzo viene eliminato, ma l’annotazione rimane invariata.

## Aggiunta di annotazioni ad altre risorse {#annotating-other-resources}

Oltre che ai componenti, puoi aggiungere annotazioni a numerose altre risorse:

* Aggiunta di annotazioni alle risorse [Aggiunta di annotazioni alle risorse](/help/assets/manage-digital-assets.md#annotating)
* Aggiunta di annotazioni alle risorse video [Aggiunta di annotazioni alle risorse video](/help/assets/manage-video-assets.md#annotate-video-assets)
