---
title: Lanci per pagine
description: Scopri come utilizzare Launches per le pagine in Adobe Experience Manager as a Cloud Service. I lanci consentono di sviluppare in modo efficiente i contenuti per una versione futura, mantenendo al contempo le pagine correnti.
exl-id: 3e410120-d08f-4d05-932f-07bc4440af2b
solution: Experience Manager Sites
feature: Authoring, Launches
role: User
source-git-commit: 20ad1d468ac0d8ec3933477f954120debe4e9240
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 73%

---

# Lanci per pagine {#launches-for-pages}

In Adobe Experience Manager (AEM) as a Cloud Service, Launches consente di sviluppare in modo efficiente contenuti per una versione futura.

Viene creato un *lancio* per consentire di apportare modifiche in preparazione alla pubblicazione futura, mantenendo al contempo il contenuto corrente. Per le pagine AEM, questo significa che stai modificando in modo efficace due versioni contemporaneamente: pagine attualmente pubblicate e una versione di tali pagine, da pubblicare in futuro. Una volta arrivato questo momento, puoi sostituire le pagine originali e pubblicare le nuove versioni.

>[!NOTE]
>
>Sono disponibili anche lanci per Frammenti di contenuto. I concetti di base sono gli stessi, ma esistono differenze nella loro gestione in AEM.
>
>Per informazioni dettagliate, consulta [Avvii per frammenti di contenuto](/help/sites-cloud/administering/content-fragments/launches-for-content-fragments.md).

Hai creato un *lancio*, quindi dopo aver modificato e aggiornato le tue *pagine di lancio* le hai *promosse* di nuovo al *Source*. Puoi quindi attivare queste *pagine Source* (livello principale). La promozione duplica il contenuto del lancio nelle pagine sorgente e può essere eseguita manualmente o automaticamente (a seconda dei campi impostati durante la creazione e la modifica del lancio).

Ad esempio, le pagine di prodotti stagionali del tuo negozio online vengono aggiornate trimestralmente in modo che i prodotti in questione siano in linea con la stagione corrente. Per prepararti al prossimo aggiornamento trimestrale, puoi creare un lancio delle pagine web appropriate. Nel corso del trimestre, nella copia del lancio vengono accumulate le seguenti modifiche:

* Modifiche apportate alle pagine sorgenti che si verificano in seguito alle consuete attività di manutenzione. Queste modifiche vengono duplicate automaticamente nelle pagine del lancio.
* Modifiche che vengono eseguite direttamente sulle pagine di lancio in preparazione del prossimo trimestre.

È inoltre possibile effettuare le seguenti operazioni:

* Navigare nel contenuto del ramo lancio; se necessario, aggiungere o rimuovere pagine.
* Visualizzare in anteprima come il contenuto pubblicato apparirà in una data specifica nel futuro.

Nel trimestre successivo, promuovi le pagine di lancio in modo da poter pubblicare le pagine sorgenti (mantenendo i contenuti aggiornati). Puoi promuovere tutte le pagine o solo quelle che hai modificato.

I lanci possono anche essere:

* creati per più rami principali. Anche se è possibile creare il lancio per l’intero sito (e apportare le modifiche), questo può non essere pratico in quanto l’intero sito deve essere copiato. Quando sono coinvolte centinaia o persino migliaia di pagine, i requisiti e le prestazioni di sistema sono influenzati sia dall’azione di copia che, in un secondo momento, dai confronti richiesti per le attività di promozione.
* Nidificato (un lancio all’interno di un lancio) per consentirti di creare un lancio da uno esistente, in modo che gli autori possano sfruttare le modifiche già apportate, anziché dover apportare le stesse modifiche più volte per ogni lancio.

Questa sezione spiega come creare, modificare e promuovere (e, se necessario, [eliminare](/help/sites-cloud/authoring/launches/creating.md#deleting-a-launch)) le pagine di lancio dall&#39;interno della console Sites o [dalla console Launches](#the-launches-console):

* [Creazione dei lanci](/help/sites-cloud/authoring/launches/creating.md)
* [Modifica dei lanci](/help/sites-cloud/authoring/launches/editing.md)
* [Gestione delle pagine in Launches](/help/sites-cloud/authoring/launches/managing-pages.md)
* [Utilizzo di Timewarp per visualizzare in anteprima i contenuti basati su Launches](/help/sites-cloud/authoring/launches/preview.md)
* [Promozione dei lanci](/help/sites-cloud/authoring/launches/promoting.md)

## Lanci: l’ordine degli eventi {#launches-the-order-of-events}

I lanci consentono di sviluppare in modo efficiente i contenuti per una versione futura di una o più pagine web attivate.

I lanci ti consentono di:

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
      * Promuovi il contenuto del lancio fino al **Target** (pagine sorgente) quando è pronto per la pubblicazione.
      * Pubblica il contenuto dalle pagine sorgente (dopo la promozione).
      * Promuovi tutte le pagine o solo le pagine modificate.
   * Automaticamente - questo implica le seguenti attività:
      * Il campo **Data** **lancio**(**Live**): può essere impostato durante la creazione o la modifica di un lancio.
      * Il flag **Pronto per la produzione** può essere impostato solo durante la modifica di un lancio.
      * Se l flag **Ponto per la produzione** è impostato, il lancio verrà promosso automaticamente sulle pagine di produzione alla **data** di **Lancio**(**Live**) specificata. Dopo la promozione, le pagine di produzione vengono pubblicate automaticamente.\
        Se la data non è stata impostata, il flag non ha alcun effetto.
* Aggiorna parallelamente la pagina sorgente e la pagina di lancio:
   * Le modifiche apportate alle pagine sorgente vengono automaticamente implementate nella copia lancio (se impostate con ereditarietà; ovvero come Live Copy).
   * Le modifiche apportate alla copia di lancio possono essere effettuate senza interrompere gli aggiornamenti automatici o le pagine sorgenti.

  ![Azioni parallele](/help/sites-cloud/authoring/assets/launches-parallel.png)

* [Creare un lancio nidificato](/help/sites-cloud/authoring/launches/creating.md#creating-a-nested-launch) ovvero un lancio all’interno di un lancio:
   * L’origine è un lancio esistente.
   * È possibile [promuovere un lancio nidificato](/help/sites-cloud/authoring/launches/promoting.md#promoting-a-nested-launch) per qualsiasi target; può trattarsi di un lancio principale o delle pagine sorgente di livello superiore (Produzione).

  ![Un lancio nidificato](/help/sites-cloud/authoring/assets/launches-nested.png)

  >[!CAUTION]
  >
  >L’eliminazione del lancio rimuove il lancio stesso e tutti i lanci nidificati discendenti.

>[!NOTE]
>
>La creazione e la modifica dei lanci richiede diritti di accesso a `/content/launches`- come per il gruppo predefinito `content-authors`.
>
>Per qualsiasi problema riscontrato, contatta l’amministratore del sistema.

## Lanci nei Riferimenti (console Sites) {#launches-in-references-sites-console}

1. Nella console **Sites**, passa all’orginie dei lanci.
1. Apri la barra **Riferimenti** e seleziona la pagina sorgente.
1. Selezionando **Lanci**, verranno elencati i lanci esistenti e l’accesso alla **Console Lanci**:

   ![Riferimenti di lanci nella console Sites](/help/sites-cloud/authoring/assets/launches-references.png)

1. Seleziona il lancio appropriato per visualizzare l’elenco delle azioni possibili:

   ![Azioni da intraprendere su Launches nella console Sites](/help/sites-cloud/authoring/assets/launches-references-actions.png)

## La console Lanci {#the-launches-console}

>[!NOTE]
>
>Questa console è solo per i lanci per le pagine.
>
>Per gestire i frammenti di contenuto, vedi [Avvii per frammenti di contenuto](/help/sites-cloud/administering/content-fragments/launches-for-content-fragments.md).

La console Lanci fornisce una panoramica dei lanci e consente di agire su quelli elencati.

![Console Lanci: gestisci contenuto](/help/sites-cloud/authoring/assets/launches-navigate-launches-console.png)

Puoi accedere alla console da:

* Console **Strumenti**: **Strumenti**, **Generale**, **Avvii**.

* **Console Launches** nella parte inferiore della sezione **Launches** della barra **Riferimenti** quando navighi nel contenuto sorgente nella console Sites.

  ![Console Launches in Riferimenti dei lanci nella console Sites](/help/sites-cloud/authoring/assets/launches-references.png)

* Il pulsante **Launches** in alto a destra, quando navighi nel contenuto di un lancio nella console Sites:

  ![Opzione Launches nella console Sites](/help/sites-cloud/authoring/assets/launches-console-navigate-launch-content.png)
