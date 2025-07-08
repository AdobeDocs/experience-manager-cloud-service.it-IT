---
title: 'Utilizzo delle versioni di una pagina  '
description: Scopri come creare, confrontare e ripristinare le versioni delle pagine in AEM.
exl-id: 33d8e43c-594d-4bba-9631-b2c42a1e910f
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: ebbf38563be65c28384276f7a0baa100f9f384b2
workflow-type: tm+mt
source-wordcount: '1620'
ht-degree: 90%

---

# Utilizzo delle versioni di una pagina   {#working-with-page-versions}

Il controllo delle versioni crea lo snapshot di una pagina in un determinato momento. Con il controllo delle versioni è possibile eseguire le azioni seguenti:

* Creare una versione di una pagina.
* Ripristina una versione precedente di una o più pagine per:
   * Annullare le modifiche apportate alle pagine.
   * Ripristinare le pagine eliminate.
   * Ripristinare una struttura (come appariva a una data e un’ora specificate).
* Visualizzare l&#39;anteprima di una versione.
* Confrontare la versione corrente della pagina con una versione precedente.
   * Vengono evidenziate le differenze nel testo e nelle immagini.
* Questa funzione utilizza le versioni delle pagine per determinare lo stato dell’ambiente di pubblicazione.

>[!NOTE]
>
>Nell’archivio AEM viene creata una versione solo del contenuto. Le risorse dinamiche come codice, CSS e JavaScript non dispongono di versioni.
>
>* Quando si visualizzano le versioni, il contenuto viene visualizzato con il codice, CSS e JavaScript correnti dell’archivio.
>* Durante il ripristino delle versioni, viene ripristinato solo il contenuto e vengono applicati il codice, i CSS e il JavaScript correnti dell’archivio.

## Creazione di una nuova versione   {#creating-a-new-version}

Puoi creare una versione della risorsa da:

* [Barra Timeline](#creating-a-new-version-timeline)
* Opzione [Crea](#creating-a-new-version-create-with-a-selected-resource) (quando è selezionata una risorsa)

### Creazione di una nuova versione - Timeline {#creating-a-new-version-timeline}

1. Passa alla pagina per la quale desideri creare una versione.
1. Seleziona la pagina in [modalità di selezione](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources).
1. Apri la barra **Timeline**.
1. Seleziona i puntini di sospensione accanto al campo del commento per visualizzare le opzioni:

   ![Versioni nella barra Timeline](/help/sites-cloud/authoring/assets/versions-timeline-rail.png)

1. Seleziona **Salva come versione**.
1. Immetti un’**Etichetta** e un **Commento**, se necessario.

   ![Aggiunta dell’etichetta per una versione](/help/sites-cloud/authoring/assets/versions-add-label.png)

1. Conferma la nuova versione selezionando **Crea**.

   Le informazioni nella timeline vengono aggiornate per indicare che si tratta di una nuova versione.

### Creazione di una nuova versione - Con una risorsa selezionata {#creating-a-new-version-create-with-a-selected-resource}

1. Passa alla pagina per la quale desideri creare una versione.
1. Seleziona la pagina in [modalità di selezione](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources).
1. Seleziona l’opzione **Crea** dalla barra degli strumenti.
1. Viene aperta la stessa finestra di dialogo. Puoi immettere un’**Etichetta** e un **Commento**, se necessario.
1. Conferma la nuova versione selezionando **Crea**.

Viene aperta la timeline con le informazioni aggiornate per indicare che si tratta di una nuova versione.

## Ripristino delle versioni {#reinstating-versions}

Dopo aver creato una versione della pagina, esistono diversi metodi per ripristinare una versione precedente:

* L&#39;opzione **Ripristina questa versione** dalla barra [Timeline](/help/sites-cloud/authoring/basic-handling.md#timeline)

  Ripristinare una versione precedente di una pagina selezionata.

* L&#39;opzione **Ripristina** dalla [barra delle azioni](/help/sites-cloud/authoring/basic-handling.md#actions-toolbar) in alto

   * **Ripristina versione**

     Ripristina le versioni delle pagine specificate nella cartella attualmente selezionata. Può inoltre includere il ripristino delle pagine precedentemente eliminate.

   * **Ripristina struttura**

     Ripristina una versione dell’intera struttura in base a una data e un’ora specificate. Può anche includere pagine precedentemente eliminate.

>[!NOTE]
>
>Durante il ripristino di una pagina, la versione creata fa parte di un nuovo ramo.
>
>Per maggiore chiarezza:
>
>1. Crea versioni di qualsiasi pagina.
>1. Le etichette iniziali e i nomi dei nodi di versione sono 1.0, 1.1, 1.2 e così via.
>1. Ripristina la prima versione, ovvero la 1.0.
>1. Crea di nuovo le versioni.
>1. Le etichette e i nomi dei nodi generati sono ora 1.0.0, 1.0.1, 1.0.2 e così via.

### Ripristina una versione {#revert-to-a-version}

Per **ripristinare** la pagina selezionata in una versione precedente:

1. Passa alla pagina di cui desideri ripristinare una versione precedente.
1. Seleziona la pagina in [modalità di selezione](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources).
1. Apri la colonna **Timeline** e seleziona **Mostra tutti** o **Versioni**. Vengono elencate le versioni disponibili per la pagina selezionata.
1. Seleziona la versione da ripristinare. Vengono visualizzate le opzioni disponibili:

   ![Ripristina questa versione](/help/sites-cloud/authoring/assets/versions-revert.png)

1. Seleziona **Ripristina questa versione**. La versione selezionata viene ripristinata e le informazioni nella timeline vengono aggiornate.

### Ripristina versione {#restore-version}

Questo metodo può essere utilizzato per ripristinare versioni di pagine specifiche all’interno della cartella corrente. Può inoltre includere il ripristino di pagine precedentemente eliminate:

1. Vai alla cartella richiesta e [selezionala](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources).

1. Seleziona **Ripristina**, quindi **Ripristina versione** dalla [barra delle azioni](/help/sites-cloud/authoring/basic-handling.md#actions-toolbar) in alto.

   >[!NOTE]
   >
   >Se:
   >
   >* hai selezionato una singola pagina che non ha mai avuto pagine secondarie,
   >* o nessuna delle pagine della cartella dispone di versioni,
   >
   >La visualizzazione diventa vuota perché non sono presenti versioni applicabili.

1. Sono elencate le versioni disponibili:

   ![Ripristina versione - Elenco di tutte le pagine della cartella](/help/sites-cloud/authoring/assets/versions-restore-version-01.png)

1. Per una pagina specifica, utilizza il selettore a discesa in **RIPRISTINA VERSIONE** per selezionare la versione richiesta per la pagina.

   ![Ripristina versione - Seleziona versione](/help/sites-cloud/authoring/assets/versions-restore-version-02.png)

1. Nella visualizzazione principale, seleziona la pagina da ripristinare:

   ![Ripristina versione - Seleziona pagina](/help/sites-cloud/authoring/assets/versions-restore-version-03.png)

1. Seleziona **Ripristina** per la versione della pagina selezionata da ripristinare come versione corrente.

>[!NOTE]
>
>L’ordine in cui selezioni una pagina richiesta e la relativa versione è intercambiabile.

### Ripristina albero {#restore-tree}

Questo metodo può essere utilizzato per ripristinare una versione di una struttura a una data e a un’ora specificate. Può includere pagine precedentemente eliminate:

1. Vai alla cartella richiesta e [selezionala](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources).

1. Seleziona **Ripristina**, quindi **Ripristina struttura** dalla [barra delle azioni](/help/sites-cloud/authoring/basic-handling.md#actions-toolbar) in alto. Viene visualizzata la versione più recente della struttura:

   ![Ripristina struttura](/help/sites-cloud/authoring/assets/versions-restore-tree-01.png)

1. Utilizza il selettore data e ora in **Versioni più recenti alla data** per poter selezionare un’altra versione della struttura, quella da ripristinare.

1. Imposta il contrassegno **Pagine non versionate salvate** se necessario:

   * Se è attiva (selezionata), tutte le pagine senza versione vengono mantenute e non sono interessate dal ripristino.

   * Se è inattiva (deselezionata), tutte le pagine non versionate vengono rimosse in quanto non esistevano nella struttura versionata.

1. Seleziona **Ripristina** per la versione selezionata della struttura da ripristinare come versione *attuale*.

## Anteprima di una versione   {#previewing-a-version}

Puoi visualizzare l’anteprima di una versione specifica:

1. Passa alla pagina che desideri confrontare.
1. Seleziona la pagina in [modalità di selezione](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources).
1. Apri la colonna **Timeline** e seleziona **Mostra tutti** o **Versioni**.
1. Vengono elencate le versioni della pagina. Seleziona la versione da visualizzare in anteprima:

   ![Anteprima versione](/help/sites-cloud/authoring/assets/versions-revert.png)

1. Seleziona **Anteprima**. La pagina viene visualizzata in una nuova scheda.

   >[!CAUTION]
   >
   >Se una pagina è stata spostata, non è più possibile eseguire un’anteprima delle versioni create prima dello spostamento.
   >
   >Se riscontri problemi con un’anteprima, controlla la [Timeline](/help/sites-cloud/authoring/basic-handling.md#timeline), per constatare se la pagina da visualizzare è stata spostata.

## Confronto di una versione con la pagina corrente {#comparing-a-version-with-current-page}

Per mettere a confronto una versione precedente con la pagina corrente:

1. Passa alla pagina che desideri confrontare.
1. Seleziona la pagina in [modalità di selezione](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources).
1. Apri la colonna **Timeline** e seleziona **Mostra tutti** o **Versioni**.
1. Vengono elencate le versioni della pagina. Seleziona la versione da confrontare:

   ![Confronto delle versioni](/help/sites-cloud/authoring/assets/versions-revert.png)

1. Seleziona **Confronta con corrente**. La [pagina di confronto](/help/sites-cloud/authoring/sites-console/page-diff.md) si apre e visualizza le differenze.

## Timewarp   {#timewarp}

Timewarp è una funzione progettata per simulare lo stato *di pubblicazione* di una pagina in specifici momenti nel passato.

Poiché la creazione di contenuti è un processo continuo e collaborativo, lo scopo di Timewarp è consentire agli autori di tenere traccia del sito web pubblicato nel tempo, in modo da comprendere in che modo è cambiato il contenuto. Questa funzione utilizza le versioni delle pagine per determinare lo stato dell’ambiente di pubblicazione.

Per utilizzare questa funzione:

* il sistema cerca la versione della pagina che era attiva al momento selezionato.
* In altre parole, la versione mostrata era stata creata/attivata *prima* del momento temporale selezionato in Timewarp.
* Quando si passa a una pagina che è stata successivamente eliminata, questa viene riprodotta purché nell’archivio siano disponibili ancora le precedenti versioni di tale pagina.
* Se non viene individuata alcuna versione pubblicata, Timewarp ripristina lo stato corrente della pagina nell’ambiente di authoring (in modo da evitare un errore 404 di pagina non trovata, che impedirebbe la navigazione).

>[!NOTE]
>
>Timewarp funziona ed è destinato all’utilizzo per le pagine AEM, ovvero versioni per cronologia e lanci per i futuri stati dei contenuti.
>
>Non funziona per i lanci nidificati o quando vengono utilizzati frammenti di esperienza.

>[!TIP]
>
>[Timewarp può essere utilizzato anche con Launches per visualizzare anteprime](/help/sites-cloud/authoring/launches/preview.md).

### Utilizzo di Timewarp {#using-timewarp}

Timewarp è una [modalità](/help/sites-cloud/authoring/page-editor/introduction.md#page-modes) dell’editor pagina. Per avviarlo, è sufficiente cambiarlo come si farebbe con qualsiasi altra modalità.

1. Avvia l&#39;editor per la pagina in cui desideri avviare Timewarp, quindi seleziona **Timewarp** nella selezione della modalità.

   ![Modalità Timewarp](/help/sites-cloud/authoring/assets/versions-timewarp-mode.png)

1. Nella finestra di dialogo, imposta una data e un’ora di destinazione e fai clic su **Imposta data**. Se non si seleziona un’ora, per impostazione predefinita viene utilizzata l’ora corrente.

   ![Data di destinazione in Timewarp](/help/sites-cloud/authoring/assets/versions-timewarp-target.png)

1. La pagina viene visualizzata in base al set di date. La modalità Timewarp è indicata dalla barra di stato blu nella parte superiore della finestra. Utilizza i collegamenti nella barra di stato per selezionare una nuova data di destinazione o uscire dalla modalità Timewarp.

   ![In modalità Timewarp](/help/sites-cloud/authoring/assets/versions-timewarp.png)

### Limitazioni di Timewarp {#timewarp-limitations}

Timewarp semplifica al massimo la riproduzione di una pagina in un determinato momento. Tuttavia, a causa delle complessità dell’authoring continuo di contenuti in AEM, questo non è sempre possibile. Tieni presenti queste limitazioni quando utilizzi Timewarp.

* **Timewarp funziona in base alle pagine pubblicate**: Timewarp funziona correttamente solo se la pagina è stata già pubblicata. In caso contrario viene mostrata la pagina corrente nell’ambiente di authoring.
* **Timewarp utilizza le versioni di pagina**: se passi a una pagina che è stata rimossa o eliminata dall’archivio, questa verrà riprodotta correttamente se nell’archivio sono ancora disponibili versioni precedenti della pagina.
* **Le versioni rimosse influiscono su Timewarp**: se dalla directory archivio sono state rimosse delle versioni, Timewarp non può mostrare la visualizzazione corretta.
* **Timewarp è di sola lettura**: non è possibile modificare la versione precedente della pagina, ma solo visualizzarla. Se desideri ripristinare la versione precedente, devi farlo manualmente utilizzando la funzione di [ripristino](#revert-to-a-version).
* **Timewarp si basa sul contenuto della pagina**: se sono stati modificati alcuni elementi per il rendering del sito web, ad esempio codice, css e risorse, la visualizzazione sarà diversa da quella originale. Per tali elementi non viene creata una versione nell’archivio.
* Timewarp non funziona per i lanci nidificati o quando vengono utilizzati frammenti di esperienza.

>[!CAUTION]
>
>Timewarp è uno strumento appositamente pensato per aiutare gli autori a comprendere e creare i propri contenuti. Non deve essere utilizzato come registro di controllo o per fini legali.
