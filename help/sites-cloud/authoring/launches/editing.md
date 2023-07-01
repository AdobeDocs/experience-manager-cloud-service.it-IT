---
title: Modifica dei lanci
description: Dopo aver creato un lancio per la pagina (o per un set di pagine), puoi modificarne il contenuto nella copia di lancio delle pagine.
exl-id: d3cd3383-e0a0-4019-9f97-8baa3be99e6e
source-git-commit: a01583483fa89f89b60277c2ce4e1c440590e96c
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 52%

---

# Modifica dei lanci {#editing-launches}

## Modifica delle pagine di un lancio {#editing-launch-pages}

Quando è stato creato un lancio per una pagina (o un set di pagine) puoi modificare il contenuto nella copia di lancio delle pagine.

1. Accedi a [Lancio da Riferimenti (console Sites)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) per visualizzare le azioni disponibili.
1. Seleziona **Vai alla pagina** per aprire la pagina per la modifica.

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

Puoi apportare modifiche nello stesso modo in cui puoi modificare una Live Copy standard; ad esempio:

* Facendo clic su un lucchetto chiuso si interrompe la sincronizzazione e si apportano nuovi aggiornamenti al contenuto del lancio. Una volta sbloccato (apri lucchetto), le modifiche non verranno sovrascritte da eventuali modifiche apportate nella stessa posizione all’interno del ramo di origine.
* **Sospendi** (e **Riprendi**) l’ereditarietà per una pagina specifica.

Consulta [Modifica del contenuto della Live Copy](/help/sites-cloud/administering/msm/creating-live-copies.md) per ulteriori informazioni.

## Confronto tra una pagina di lancio e la relativa pagina di origine {#comparing-a-launch-page-to-its-source-page}

Per tenere traccia delle modifiche apportate, puoi visualizzare il lancio in **Riferimenti** e confrontare la pagina del lancio con la relativa pagina di origine:

1. Nella console **Sites**, [passa alle pagine di origine del lancio e selezionane una](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Apri **[Riferimenti](/help/sites-cloud/authoring/getting-started/basic-handling.md#references)** e seleziona **Lanci**.
1. Seleziona il lancio specifico, quindi **Confronta con origine**:

   ![Confronto tra lancio e origine](/help/sites-cloud/authoring/assets/launches-compare.png)

1. Le due pagine (lancio e sorgente) vengono aperte una accanto all’altra.

   Per informazioni complete sull’utilizzo di questa funzione, consulta [Differenza di pagina](/help/sites-cloud/authoring/features/page-diff.md).

## Modifica delle pagine sorgente utilizzate {#changing-the-source-pages-used}

In qualsiasi momento è possibile aggiungere o rimuovere pagine da e verso la gamma di pagine di origine per un lancio:

1. Accedi e seleziona il lancio in uno dei seguenti modi:
   * La [console Lanci](/help/sites-cloud/authoring/launches/overview.md#the-launches-console):
      * Seleziona **Modifica**.
   * [Riferimenti (console Sites)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) per visualizzare le azioni disponibili:
      * Seleziona **Modifica lancio**.
      * Vengono visualizzate le pagine sorgente.
1. Apporta le modifiche necessarie, quindi conferma con **Salva**.

>[!NOTE]
>
>Per aggiungere pagine a un lancio, è necessario che si trovino al di sotto di una directory principale della lingua comune, ovvero all’interno di un singolo sito.

## Modifica di una configurazione di Launch {#editing-a-launch-configuration}

In qualsiasi momento è possibile modificare le proprietà per un lancio:

1. Accedi e seleziona il lancio in uno dei seguenti modi:
   * il [Console Launches](/help/sites-cloud/authoring/launches/overview.md#the-launches-console):
      * Seleziona **Proprietà**.
   * [Riferimenti (console Sites)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) per visualizzare le azioni disponibili:
      * Seleziona **Modifica proprietà**.
      * Vengono visualizzati i dettagli.
1. Apporta le modifiche necessarie, quindi conferma con **Salva**.
   * Consulta la sezione [Lanci - Ordine degli eventi](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events) per informazioni sullo scopo e sull’interazione dei campi **Data lancio** e **Production Ready**.

## Esplorazione dello stato di avvio di una pagina {#discovering-the-launch-status-of-a-page}

Lo stato viene visualizzato quando selezioni un lancio specifico dalla scheda Riferimenti (consulta [Lanci in Riferimenti (console Sites)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)).

![Esplorazione dello stato del lancio](/help/sites-cloud/authoring/assets/launches-status.png)
