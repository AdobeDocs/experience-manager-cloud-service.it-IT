---
title: Lanci
description: I lanci consentono di creare in modo efficiente contenuti da pubblicare in futuro. Consentono di apportare modifiche pronte per la pubblicazione futura, mantenendo le pagine correnti
exl-id: 3e410120-d08f-4d05-932f-07bc4440af2b
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 45%

---

# Lanci {#launches}

I lanci consentono di creare in modo efficiente contenuti da pubblicare in futuro.

Il lancio creato consente di preparare modifiche pronte alla pubblicazione futura (mantenendo le tue pagine correnti). Dopo aver modificato e aggiornato le pagine di lancio, le promuovi di nuovo all’origine, quindi attiva le pagine sorgente (livello superiore). La promozione duplica il contenuto del lancio nelle pagine di origine e può essere eseguita manualmente o automaticamente (a seconda dei campi impostati durante la creazione e la modifica del lancio).

Ad esempio, le pagine di prodotti stagionali del tuo negozio online vengono aggiornate trimestralmente in modo che i prodotti in questione siano in linea con la stagione corrente. Per prepararti al prossimo aggiornamento trimestrale, puoi creare un lancio delle pagine web appropriate. Nel corso del trimestre, le seguenti modifiche vengono accumulate nella copia di lancio:

* Modifiche apportate alle pagine sorgenti che si verificano in seguito alle consuete attività di manutenzione. Queste modifiche vengono duplicate automaticamente nelle pagine del lancio.
* Modifiche che vengono eseguite direttamente sulle pagine di lancio in preparazione al trimestre successivo.

È inoltre possibile effettuare le seguenti operazioni:

* Navigare nel contenuto del ramo lancio; se necessario, aggiungere o rimuovere pagine.
* Visualizzare in anteprima come il contenuto pubblicato apparirà in una certa data nel futuro.

Nel trimestre successivo, promuovi le pagine di lancio in modo da poter pubblicare le pagine sorgenti (mantenendo i contenuti aggiornati). Puoi promuovere tutte le pagine o solo quelle che hai modificato.

I lanci possono anche essere:

* Creato per più rami principali. Nonostante sia possibile creare il lancio per l&#39;intero sito (e apportare le modifiche desiderate), questa operazione potrebbe risultare poco pratica perché l&#39;intero sito dovrà essere copiato. Quando sono coinvolte centinaia o anche migliaia di pagine, i requisiti di sistema e le prestazioni sono influenzati sia dall’azione di copia che, in un secondo momento, dai confronti richiesti per le attività di promozione.
* Nidificato (un lancio all’interno di un lancio) per consentirti di creare un lancio da un lancio esistente in modo che gli autori possano sfruttare le modifiche già apportate, anziché dover apportare le stesse modifiche più volte per ogni lancio.

Questa sezione spiega come creare, modificare e promuovere (e, se necessario, [eliminare](/help/sites-cloud/authoring/launches/creating.md#deleting-a-launch)) le pagine di lancio dall&#39;interno della console Sites o [dalla console Launches](#the-launches-console):

* [Creazione dei lanci](/help/sites-cloud/authoring/launches/creating.md)
* [Modifica dei lanci](/help/sites-cloud/authoring/launches/editing.md)
* [Gestione delle pagine in Launches](/help/sites-cloud/authoring/launches/managing-pages.md)
* [Utilizzo di Timewarp per visualizzare in anteprima i contenuti basati su Launches](/help/sites-cloud/authoring/launches/preview.md)
* [Promozione dei lanci](/help/sites-cloud/authoring/launches/promoting.md)

## Lanci: l’ordine degli eventi {#launches-the-order-of-events}

I lanci consentono di sviluppare in modo efficiente i contenuti per una versione futura di una o più pagine web attivate.

I lanci consentono di:

* Crea una copia delle pagine sorgente:
   * La copia è il lancio.
   * Le pagine sorgente di primo livello sono note come **Produzione**.
      * Le pagine sorgente possono essere ricavate da più rami (separati).

  ![Ordine di esercizio dei lanci](/help/sites-cloud/authoring/assets/launches-order.png)

* Modifica la configurazione del lancio:
   * Aggiungi o rimuovi pagine e/o rami da/verso il lancio.
   * Modifica le proprietà di lancio, come **Titolo**, **Data lancio** e il flag **Production Ready**.
* Puoi promuovere e pubblicare il contenuto manualmente o automaticamente:
   * Manualmente:
      * Promuovi il contenuto del lancio in **Target** (pagine sorgente) quando è pronto per la pubblicazione.
      * Pubblica il contenuto dalle pagine sorgente (dopo la promozione).
      * Promuovi tutte le pagine o solo le pagine modificate.
   * Automaticamente - questo implica le seguenti attività:
      * Il campo **Data** **lancio**(**Live**): può essere impostato durante la creazione o la modifica di un lancio.
      * Il **Produzione pronta** flag: può essere impostato solo durante la modifica di un lancio.
      * Se il **Produzione pronta** viene impostato, il lancio viene promosso automaticamente alle pagine di produzione nella **Launch**(**Live**) **data**. Dopo la promozione, le pagine di produzione vengono pubblicate automaticamente.\
        Se la data non è stata impostata, il flag non ha alcun effetto.
* Aggiorna parallelamente la pagina sorgente e la pagina di lancio:
   * Le modifiche alle pagine sorgente vengono implementate automaticamente nella copia lancio (se impostate con ereditarietà; ovvero, come Live Copy).
   * Le modifiche apportate alla copia di lancio possono essere effettuate senza interrompere gli aggiornamenti automatici o le pagine sorgenti.

  ![Azioni parallele](/help/sites-cloud/authoring/assets/launches-parallel.png)

* [Creare un lancio nidificato](/help/sites-cloud/authoring/launches/creating.md#creating-a-nested-launch) - un lancio all’interno di un lancio:
   * L’origine è un lancio esistente.
   * È possibile [promuovere un lancio nidificato](/help/sites-cloud/authoring/launches/promoting.md#promoting-a-nested-launch) a qualsiasi destinazione; può trattarsi di un lancio principale o delle pagine sorgente di livello superiore (Produzione).

  ![Un lancio nidificato](/help/sites-cloud/authoring/assets/launches-nested.png)

  >[!CAUTION]
  >
  >L’eliminazione del lancio rimuove il lancio stesso e tutti i lanci nidificati discendenti.

>[!NOTE]
>
>La creazione e la modifica dei lanci richiede diritti di accesso a `/content/launches`- come per il gruppo predefinito `content-authors`.
>
>In caso di problemi, contatta l’amministratore di sistema.

## Lanci in Riferimenti (console Sites) {#launches-in-references-sites-console}

1. In **Sites** , passa all&#39;origine dei lanci.
1. Apri **Riferimenti** e seleziona la pagina sorgente.
1. Seleziona **Lanci**, vengono elencati i lanci esistenti e l&#39;accesso al **Console Launches**:

   ![Riferimenti di Launches nella console Sites](/help/sites-cloud/authoring/assets/launches-references.png)

1. Tocca o fai clic sul lancio appropriato per visualizzare l’elenco delle azioni possibili:

   ![Azioni da intraprendere su Launches nella console Sites](/help/sites-cloud/authoring/assets/launches-references-actions.png)

## Console Lanci {#the-launches-console}

La console Lanci fornisce una panoramica dei lanci e consente di eseguire azioni su quelli elencati. Puoi accedere alla console da:

* La console **Strumenti**: **Strumenti**, **Sites**, **Lanci**.

* **Console Launches** nella parte inferiore della sezione **Launches** della barra **Riferimenti** quando navighi nel contenuto sorgente nella console Sites.

  ![Console Launches in Riferimenti dei lanci nella console Sites](/help/sites-cloud/authoring/assets/launches-references.png)

* Il pulsante **Launches** in alto a destra, quando navighi nel contenuto di un lancio nella console Sites:

  ![Opzione Launches nella console Sites](/help/sites-cloud/authoring/assets/launches-console-navigate-launch-content.png)

* O direttamente; ad esempio, con:
  `https://<host>:<port>/libs/launches/content/launches.html`
