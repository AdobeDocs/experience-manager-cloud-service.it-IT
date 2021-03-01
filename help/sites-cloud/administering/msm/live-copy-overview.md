---
title: Console Panoramica di Live Copy
description: Scopri le nozioni di base della console Panoramica di Live Copy per comprendere rapidamente lo stato delle Live Copy al fine di sincronizzare i contenuti.
translation-type: tm+mt
source-git-commit: 4fc4dbe2386d571fa39fd6d10e432bb2fc060da1
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 1%

---


# Console panoramica Live Copy {#live-copy-overview-console}

La console **Panoramica Live Copy** consente di:

* Visualizza/gestisci l’ereditarietà in un sito.
   * Visualizza la struttura della blueprint e la struttura Live Copy corrispondente, insieme al relativo stato di ereditarietà
   * Modificare lo stato di ereditarietà, ad esempio sospendere e riprendere
   * Visualizzare le proprietà blueprint e Live Copy
* Esegui azioni di rollout.

## Apertura della panoramica Live Copy {#opening-the-live-copy-overview}

Puoi aprire la Panoramica della Live Copy da:

* [Pannello laterale Riferimenti di una pagina blueprint (console Sites)](#opening-live-copy-overview-references-for-a-blueprint-page)
* [Proprietà di una pagina blueprint](#opening-live-copy-overview-properties-of-a-blueprint-page)

### Riferimenti a una pagina blueprint {#references-to-a-blueprint-page}

Il **Panoramica Live Copy** può essere aperto dal pannello laterale **Riferimenti** della console **Sites** :

1. Nella console **Sites** , [individua e seleziona la pagina blueprint.](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)
1. Apri la barra **[Riferimenti](/help/sites-cloud/authoring/getting-started/basic-handling.md#references)** e seleziona **Live Copy**.

   ![Live Copy dalla barra dei riferimenti](../assets/live-copy-references.png)

   >[!TIP]
   >
   >È inoltre possibile aprire prima i riferimenti e quindi selezionare la blueprint.

1. Seleziona **Panoramica Live Copy** per mostrare e utilizzare la panoramica di tutte le Live Copy relative alla blueprint selezionata.
1. Utilizza **Chiudi** per uscire e tornare alla console **Sites**.

### Proprietà di una pagina blueprint {#properties-of-a-blueprint-page}

La **Panoramica Live Copy** può essere aperta quando si visualizzano le proprietà di una pagina blueprint:

1. Apri **Proprietà** per la pagina blueprint appropriata.
1. Apri la scheda **Blueprint** : l’opzione **Panoramica Live Copy** verrà visualizzata nella barra degli strumenti superiore:

   ![Scheda Proprietà blueprint](../assets/live-copy-blueprint-tab.png)

1. Seleziona **Panoramica Live Copy** per mostrare e utilizzare la panoramica di tutte le Live Copy relative al modello corrente.

1. Utilizza **Chiudi** per uscire e tornare alla console **Sites**.

## Utilizzo della panoramica Live Copy {#using-the-live-copy-overview}

La finestra **Panoramica Live Copy** fornisce una panoramica dello stato delle Live Copy relative alla pagina selezionata.

![Finestra Panoramica di Live Copy](../assets/live-copy-overview.png)

Un rollout dipende dalle azioni di sincronizzazione definite nella specifica configurazione di rollout. Alcune azioni dipendono dalle modifiche al contenuto. Tuttavia, esistono anche molte azioni che non dipendono da modifiche al contenuto, ma dipendono da eventi come l’attivazione della pagina. Tali eventi non modificano il contenuto, ma modificano le proprietà interne correlate al contenuto.

I campi di stato dipendono anche dalle azioni di sincronizzazione definite nella specifica configurazione di rollout e indicano se sono state eseguite tali azioni al blueprint o alla Live Copy dall’ultimo rollout riuscito. Un campo di stato riflette solo le azioni nella specifica configurazione di rollout. Se non è mai stato eseguito il rollout di successo su una Live Copy, lo stato viene sempre visualizzato aggiornato.

Ad esempio, una configurazione di rollout è definita come `targetActivate`. Pertanto, un rollout dipenderà solo dagli eventi di attivazione. Il campo di stato indica solo se si sono verificati eventi di attivazione dall’ultimo rollout riuscito.

La **Panoramica Live Copy** può essere utilizzata anche per eseguire azioni sulla Live Copy:

1. Apri la **Panoramica Live Copy**.
1. Seleziona la pagina blueprint o Live Copy richiesta e la barra degli strumenti verrà aggiornata per mostrare le azioni disponibili. Le [azioni](overview.md#terms-used) disponibili dipendono dalla selezione di una pagina [blueprint](#actions-for-a-blueprint-page) o [Live Copy](#actions-for-a-live-copy-page).

### Azioni per una pagina blueprint {#actions-for-a-blueprint-page}

Quando selezioni una pagina blueprint, sono disponibili le seguenti azioni:

![Azioni di panoramica Live Copy per una blueprint](../assets/live-copy-overview-actions-blueprint.png)

* **Modifica** : consente di aprire la pagina blueprint da modificare.
* **[Rollout](overview.md#rollout-and-synchronize)**  - Esegui un rollout per inviare le modifiche dalla sorgente alla Live Copy.

### Azioni per una pagina Live Copy {#actions-for-a-live-copy-page}

Quando selezioni una pagina Live Copy, sono disponibili le seguenti azioni:

![Azioni di panoramica Live Copy per una Live Copy](../assets/live-copy-overview-actions.png)

* **Modifica** : apri la pagina Live Copy per la modifica.
* **[Stato relazione](#relationship-status)**  - Visualizza informazioni sullo stato e sull&#39;ereditarietà.
* **[Sincronizza](overview.md#rollout-and-synchronize)**  - Sincronizza una Live Copy per estrarre le modifiche dalla sorgente alla Live Copy.
* **[Ripristina](creating-live-copies.md#resetting-a-live-copy-page)** : consente di ripristinare una pagina Live Copy per rimuovere tutte le cancellazioni di ereditarietà e ripristinare lo stato della pagina nello stesso della pagina sorgente.
* **[Sospendi](overview.md#suspending-and-cancelling-inheritance-and-synchronization)** : disattiva temporaneamente la relazione in tempo reale tra una Live Copy e la relativa pagina blueprint.
* **[Riprendi](creating-live-copies.md#resuming-inheritance-for-a-page)**  - Riprendi ti consente di ripristinare una relazione sospesa.
* **[Stacca](overview.md#detaching-a-live-copy)** : rimuove definitivamente la relazione live tra una Live Copy e la relativa pagina blueprint.

## Stato di relazione {#relationship-status}

La console **Stato di relazione** dispone di due schede che forniscono una serie di funzionalità.

* [Stato di relazione](#relationship-status-tab)
* [Live Copy ](#live-copy-tab)

### Stato di relazione {#relationship-status-tab}

Questa scheda fornisce informazioni dettagliate sullo stato della relazione tra blueprint e Live Copy.

![Scheda Stato relazione](../assets/live-copy-relationship-status.png)

### Live Copy  {#live-copy-tab}

Questa scheda ti consente di visualizzare e modificare la configurazione della Live Copy.

![Scheda Live Copy](../assets/live-copy-relationship-status-live-copy.png)
