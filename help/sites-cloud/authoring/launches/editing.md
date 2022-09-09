---
title: Modifica dei lanci
description: Quando è stato creato un lancio per una pagina (o per un insieme di pagine), è possibile modificare il contenuto nella copia di lancio della pagina (o delle pagine).
exl-id: d3cd3383-e0a0-4019-9f97-8baa3be99e6e
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 100%

---

# Modifica dei lanci {#editing-launches}

## Modifica delle pagine di lancio {#editing-launch-pages}

Dopo aver creato un lancio per una pagina o un insieme di pagine, è possibile modificarne il contenuto nella copia di lancio.

1. Accedi a [Lancio da Riferimenti (console Sites)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) per visualizzare le azioni disponibili.
1. Seleziona **Vai a pagina** per aprire la pagina e modificarla.

Quando modifichi la pagina, nella barra degli strumenti superiore viene visualizzata un’indicazione insieme alle opzioni **Esci** e **Naviga**:

![Lascia e naviga all’avvio dall’Editor pagina](/help/sites-cloud/authoring/assets/launches-edit-01.png)

>[!NOTE]
>
>Non puoi spostare una pagina all’interno di un lancio. Il tentativo di eseguire questa azione attiva un messaggio di avviso:
>
>* Attenzione: questa pagina è l’origine di un lancio. Lo spostamento della pagina non è consentito.


### Modifica delle pagine di lanci soggette a Live Copy {#editing-launch-pages-subject-to-a-live-copy}

Se il lancio si basa su una [Live Copy](/help/sites-cloud/administering/msm/overview.md):

* saranno visibili simboli a forma di piccoli lucchetti quando si modifica un componente (contenuto e/o proprietà);
* sarà visibile la scheda **Live Copy** in **Proprietà pagina**.

Una Live Copy viene utilizzata per sincronizzare il contenuto *dal* ramo di origine *al* ramo lancio, al fine di mantenere aggiornato il lancio con le modifiche apportate nell’origine.

È possibile apportare modifiche allo stesso modo in cui si può modificare una Live Copy standard, ad esempio:

* Facendo clic su un lucchetto chiuso si interrompe la sincronizzazione e saranno possibili nuovi aggiornamenti del contenuto nel lancio. Una volta sbloccato (lucchetto aperto), le modifiche non verranno sovrascritte da nessuna modifica apportata alla stessa posizione all&#39;interno del ramo sorgente.
* **Sospendi** (e **Riprendi**) l’ereditarietà per una pagina specifica.

Per ulteriori informazioni, consulta [Modifica del contenuto per Live Copy](/help/sites-cloud/administering/msm/creating-live-copies.md).

## Confronto tra una pagina di lancio e la relativa pagina sorgente {#comparing-a-launch-page-to-its-source-page}

Per tenere traccia delle modifiche apportate, puoi visualizzare il lancio in **Riferimenti** e confrontare la pagina del lancio con la relativa pagina di origine:

1. Nella console **Sites**, [passa alle pagine di origine del lancio e selezionane una](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Apri il pannello **[Riferimenti](/help/sites-cloud/authoring/getting-started/basic-handling.md#references)** e seleziona **Lanci**.
1. Seleziona il tuo specifico lancio, quindi **Confronta con origine**:

   ![Confronto tra lancio e origine](/help/sites-cloud/authoring/assets/launches-compare.png)

1. Le due pagine (di lancio e di origine) verranno aperte una accanto all&#39;altra.

   Per informazioni complete sull&#39;utilizzo di questa funzionalità, consulta [Differenze tra pagine](/help/sites-cloud/authoring/features/page-diff.md).

## Modifica delle pagine di origine utilizzate {#changing-the-source-pages-used}

In qualsiasi momento è possibile aggiungere o rimuovere pagine da e verso la gamma di pagine di origine per un lancio:

1. Accedi e seleziona il lancio in uno dei seguenti modi:
   * La [console Lanci](/help/sites-cloud/authoring/launches/overview.md#the-launches-console):
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
   * Consulta la sezione [Lanci - Ordine degli eventi](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events) per informazioni sullo scopo e sull’interazione dei campi **Data lancio** e **Production Ready**.

## Rilevamento dello stato del lancio di una pagina {#discovering-the-launch-status-of-a-page}

Lo stato viene visualizzato quando si seleziona un lancio specifico dalla scheda Riferimenti (consulta [Avvia in Riferimenti (Console Sites)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)).

![Esplorazione dello stato del lancio](/help/sites-cloud/authoring/assets/launches-status.png)
