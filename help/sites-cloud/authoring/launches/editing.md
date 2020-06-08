---
title: Modifica dei lanci
description: 'Quando è stato creato un lancio per una pagina (o per un insieme di pagine), è possibile modificare il contenuto nella copia di lancio della pagina (o delle pagine). '
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 93%

---


# Modifica dei lanci {#editing-launches}

## Modifica delle pagine di lancio {#editing-launch-pages}

Dopo aver creato un lancio per una pagina o un insieme di pagine, è possibile modificarne il contenuto nella copia di lancio.

1. Accedi a [Lancio da Riferimenti (console Sites)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) per visualizzare le azioni disponibili.
1. Seleziona **Vai a pagina** per aprire la pagina e modificarla.

### Modifica delle pagine di lanci soggette a Live Copy {#editing-launch-pages-subject-to-a-live-copy}

Se il lancio si basa su una Live Copy: <!--If your launch is based upon a [live copy](/help/sites-administering/msm.md) then you will:-->

* Consultate bloccare i simboli (piccoli lucchetti) quando modificate un componente (contenuto e/o proprietà).
* See the **Live Copy** tab in **Page Properties**

Una Live Copy viene utilizzata per sincronizzare il contenuto *dal* ramo di origine *al* ramo lancio, al fine di mantenere aggiornato il lancio con le modifiche apportate nell’origine.

È possibile apportare modifiche allo stesso modo in cui si può modificare una Live Copy standard, ad esempio:

* Facendo clic su un lucchetto chiuso si interrompe la sincronizzazione e saranno possibili nuovi aggiornamenti del contenuto nel lancio. Una volta sbloccato (lucchetto aperto), le modifiche non verranno sovrascritte da nessuna modifica apportata alla stessa posizione all&#39;interno del ramo sorgente.
* **Sospendi** (e **Riprendi**) l’ereditarietà per una pagina specifica.

Per ulteriori informazioni, consulta Modifica del contenuto per Live Copy. <!--See [Changing Live Copy Content](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) for further information.-->

## Confronto tra una pagina di lancio e la relativa pagina sorgente {#comparing-a-launch-page-to-its-source-page}

Per tenere traccia delle modifiche apportate, puoi visualizzare il lancio in **Riferimenti** e confrontare la pagina del lancio con la relativa pagina di origine:

1. Nella console **Sites**, [spostati sulla pagina di origine del lancio e selezionala](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Apri il pannello **[Riferimenti](/help/sites-cloud/authoring/getting-started/basic-handling.md#references)**e seleziona **Lanci**.
1. Seleziona il tuo specifico lancio, quindi **Confronta con origine**:

   ![Confronto tra avvio e origine](/help/sites-cloud/authoring/assets/launches-compare.png)

1. Le due pagine (di lancio e di origine) verranno aperte una accanto all&#39;altra.

   Per informazioni complete sull&#39;utilizzo di questa funzionalità, consulta [Differenze tra pagine](/help/sites-cloud/authoring/features/page-diff.md).

## Modifica delle pagine di origine utilizzate {#changing-the-source-pages-used}

In qualsiasi momento è possibile aggiungere o rimuovere pagine da e verso la gamma di pagine di origine per un lancio:

1. Accedi e seleziona il lancio in uno dei seguenti modi:
   * The [Launches console](/help/sites-cloud/authoring/launches/overview.md#the-launches-console):
      * Seleziona **Modifica**.
   * Da [Riferimenti (console Sites)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) per mostrare le azioni disponibili:
      * Seleziona **Modifica lancio**.
      * Vengono visualizzate le pagine di origine.
1. Apporta le modifiche necessarie, quindi conferma con **Salva**.

>[!NOTE]
>
>Per aggiungere pagine a un lancio, queste devono essere sotto una radice linguistica comune, cioè all&#39;interno di un singolo sito.

## Modifica di una configurazione di lancio {#editing-a-launch-configuration}

In qualsiasi momento è possibile modificare le proprietà per un lancio:

1. Accedi e seleziona il lancio in uno dei seguenti modi:
   * Dalla [console Lanci](/help/sites-cloud/authoring/launches/overview.md#the-launches-console):
      * Seleziona **Proprietà**.
   * Da [Riferimenti (console Sites)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) per mostrare le azioni disponibili:
      * Seleziona **Modifica proprietà**.
      * Verranno visualizzati i dettagli.
1. Apporta le modifiche necessarie, quindi conferma con **Salva**.
   * Consulta [Lanci - Ordine degli eventi](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events) per informazioni sullo scopo e l&#39;interazione dei campi **Data lancio** e **Produzione pronta**.

## Rilevamento dello stato del lancio di una pagina {#discovering-the-launch-status-of-a-page}

Lo stato viene visualizzato quando si seleziona un lancio specifico dalla scheda Riferimenti (consulta [Avvia in Riferimenti (Console Sites)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)).

![Rilevamento dello stato di avvio](/help/sites-cloud/authoring/assets/launches-status.png)
