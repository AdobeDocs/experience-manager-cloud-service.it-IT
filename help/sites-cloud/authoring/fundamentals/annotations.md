---
title: Aggiunta di annotazioni pagina
description: Molti componenti direttamente correlati ai contenuti consentono di aggiungere un’annotazione
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Aggiunta di annotazioni pagina {#adding-page-annotations}

Quando si aggiunge del contenuto alle pagine di un sito web è spesso necessario discuterne con i colleghi prima di pubblicarlo. Per facilitare questa fase, molti componenti direttamente correlati al contenuto (a differenza, ad esempio, dei componenti per il layout) supportano l’inserimento di annotazioni.

Un’annotazione inserisce sulla pagina uno schizzo o una nota colorata. Può contenere commenti o domande inseriti da un utente e destinati ad altri autori o revisori.

>[!NOTE]
>
>Sono disponibili anche i [commenti](/help/sites-cloud/authoring/getting-started/basic-handling.md#timeline) per fornire feedback in una pagina.

## Annotazioni {#annotations}

Per la creazione e la visualizzazione delle annotazioni viene utilizzata una [modalità](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-modes) speciale.

>[!CAUTION]
>
>Se eliminate una risorsa (ad es. un componente), vengono anche eliminate tutte le annotazioni e gli schizzi associati a tale risorsa, indipendentemente dalla loro posizione sulla pagina nel suo insieme.

>[!NOTE]
>
>A seconda delle esigenze è anche possibile sviluppare un flusso di lavoro per inviare notifiche quando vengono aggiunte, aggiornate o eliminate delle annotazioni.

### Annotazione di un componente {#annotating-a-component}

La modalità Annota consente di creare, modificare, spostare o eliminare le annotazioni nei contenuti:

1. Per accedere alla modalità Annota utilizza la relativa icona nella barra degli strumenti (in alto a destra) durante la modifica di una pagina:

   ![Pulsante Annotazione](/help/sites-cloud/authoring/assets/annotations.png)

   È ora possibile visualizzare tutte le annotazioni esistenti.

   >[!NOTE]
   >
   >Per uscire dalla modalità Annotazione tocca o fai clic sull’icona Annota (simbolo x) a destra della barra degli strumenti superiore.

1. Tocca o fai clic sull’icona Aggiungi annotazione (simbolo + a sinistra della barra degli strumenti) per iniziare ad aggiungere annotazioni.

   >[!NOTE]
   >
   >Per interrompere l’aggiunta di annotazioni (e tornare alla visualizzazione) tocca o fai clic sull’icona Annulla (simbolo x in un cerchio bianco) a sinistra della barra degli strumenti superiore.

1. Tocca o fai clic sul componente richiesto (i componenti ai quali è possibile aggiungere annotazioni saranno evidenziati da un bordo blu) per aggiungere l’annotazione e aprire la relativa finestra di dialogo:

   ![Aggiunta di un&#39;annotazione](/help/sites-cloud/authoring/assets/annotation-adding.png)

   Puoi usare il campo e/o l’icona appropriata per effettuare le seguenti operazioni:

   * Inserisci il testo dell’annotazione.
   * Create uno sketch (linee e forme) per evidenziare un’area del componente.

      ![Pulsante Sketch annotazione](/help/sites-cloud/authoring/assets/annotation-sketch.png)

      Quando create uno sketch, il cursore diventa una crocetta. È possibile disegnare più linee distinte. La linea dello sketch assume il colore dell’annotazione e può essere una freccia, un cerchio o un ovale.

   * Scegli o modifica il colore:

      ![Pulsante campione colore annotazione](/help/sites-cloud/authoring/assets/annotation-color-swatch.png)

   * Elimina l’annotazione.

      ![Pulsante di eliminazione annotazione](/help/sites-cloud/authoring/assets/annotation-delete.png)

1. Per chiudere la finestra di dialogo dell’annotazione, tocca o fai clic all’esterno della finestra di dialogo. Di seguito viene illustrata un’annotazione troncata (la prima parola) con relativi schizzi:

   ![sketch di annotazione](/help/sites-cloud/authoring/assets/annotation-sketches.png)

1. Dopo aver modificato un’annotazione, puoi effettuare le seguenti operazioni:

   * Tocca o fai clic sul marcatore di testo per aprire l’annotazione. Una volta aperta l’annotazione, è possibile visualizzare il testo completo, apportare modifiche o eliminare l’annotazione.

      * Gli schizzi non possono essere eliminati in modo indipendente dall’annotazione.
   * Riposizionamento del marcatore di testo.
   * Toccate o fate clic su una linea di uno schizzo per selezionarlo e trascinatelo nella posizione desiderata.
   * Sposta o copia un componente

      * Vengono spostate o copiate anche tutte le annotazioni e gli schizzi associati, mantenendo la stessa posizione in relazione al paragrafo.


1. Per uscire dalla modalità Annotazione e tornare alla modalità precedente, tocca o fai clic sull’icona Annota (simbolo x) a destra della barra degli strumenti superiore.

>[!NOTE]
>
>Non è possibile aggiungere annotazioni a una pagina che è stata bloccata da un altro utente.

>[!NOTE]
>
>Nella definizione di un singolo tipo di componente è possibile specificare se l’aggiunta di annotazioni è supportata o meno per le istanze del componente.

## Indicatore di annotazione {#annotation-indicator}

Le annotazioni non vengono visualizzate in modalità di modifica, ma il contrassegno in alto a destra della barra degli strumenti mostra il numero di annotazioni esistenti per la pagina corrente. Il contrassegno sostituisce l’icona Annotazioni predefinita, ma continua a fungere da collegamento rapido per attivare o disattivare la modalità Annota:

![Indicatore di annotazione](/help/sites-cloud/authoring/assets/annotation-indicator.png)

## Aggiunta di annotazioni ad altre risorse {#annotating-other-resources}

Oltre ai componenti, potete inserire note su una varietà di risorse:

* Annotazione delle risorse [Annotazione delle risorse](/help/assets/manage-digital-assets.md#annotating)
* Annotazione delle risorse video [Annotazione delle risorse video](/help/assets/manage-video-assets.md#annotate-video-assets)
