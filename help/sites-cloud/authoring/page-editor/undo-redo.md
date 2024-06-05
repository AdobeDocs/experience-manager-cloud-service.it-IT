---
title: Limitazioni per Annulla e Ripristina
description: Scopri le limitazioni delle opzioni Annulla e Ripristina nell’editor pagina dell’AEM.
exl-id: 87773f47-5116-4966-9ba4-5deedb7c4fa6
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 92%

---

# Limitazioni per Annulla e Ripristina {#undo-redo}

In AEM vengono memorizzate una cronologia delle azioni eseguite e la relativa sequenza, in modo che le varie azioni possano essere annullate nell’ordine di esecuzione e ripristinate per riapplicare una o più azioni annullate, se necessario.

Se è selezionato un elemento nella pagina del contenuto (ad esempio un componente di testo) il comando Annulla o Ripristina si riferisce all’elemento selezionato.

Il comportamento dei comandi Annulla e Ripristina è simile a quello di altri software. Puoi utilizzare i comandi per ripristinare lo stato recente della pagina web mentre ne stai valutando il contenuto. Se ad esempio si sposta un paragrafo di testo altrove nella pagina, è possibile ricorrere al comando Annulla per riportarlo nella posizione originale. Se successivamente constati che la posizione precedente era migliore, utilizza il comando Ripristina per “annullare l’annullamento”.

Ad esempio:

* Puoi ripristinare le azioni solo se dopo l’annullamento non sono state apportate altre modifiche alla pagina.
* Per impostazione predefinita, è possibile annullare fino a 20 azioni di modifica.
* Per annullare e ripristinare le azioni è possibile anche utilizzare le [scelte rapide da tastiera](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md).

I comandi Annulla e Ripristina possono essere utilizzati solo per i tipi di modifiche della pagina seguenti:

* Aggiunta, modifica, rimozione e spostamento di paragrafi
* Modifica locale del contenuto dei paragrafi
* Operazioni Copia, Taglia e Incolla per elementi all’interno di una pagina

>[!NOTE]
>
>* Per annullare e ripristinare le modifiche apportate a file e immagini sono necessarie autorizzazioni speciali.
>* La cronologia delle modifiche apportate ai file e alle immagini viene conservata per almeno dieci ore. Oltre tale limite, la possibilità di annullare le modifiche non è garantita. L’amministratore può cambiare il tempo predefinito di dieci ore.
>* L’amministratore di sistema può configurare vari aspetti delle funzioni Annulla e Ripristina in base ai requisiti particolari del caso in questione.
