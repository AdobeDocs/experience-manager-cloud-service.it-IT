---
title: Note sulla versione di anteprima di Universal Editor
description: Queste sono le note sulla versione di anteprima di Universal Editor.
feature: Release Information
role: Admin
exl-id: e8d031aa-4676-4e45-977b-e5dffcc404c4
source-git-commit: bbf371dbf8102611345f2d289a3eaba56ee1d87c
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Note sulla versione di anteprima di Universal Editor {#preview}

Queste sono le note sulla versione per la **versione di anteprima** di Universal Editor. Queste funzionalità sono attualmente disponibili nell&#39;**ambiente di anteprima** dell&#39;editor universale. Il rilascio di queste funzioni è previsto per il 12 marzo 2026.

Queste note sulla versione di **preview** sono fornite per comodità, in modo da sapere quali modifiche all&#39;editor universale sono in arrivo e puoi testarle [passando alla versione di anteprima.](/help/sites-cloud/authoring/universal-editor/navigation.md#user-properties)

>[!TIP]
>
>Per le **note sulla versione corrente** di Universal Editor, vedere il documento [Note sulla versione di Universal Editor.](/help/release-notes/universal-editor/current.md)

>[!NOTE]
>
>Il contenuto della versione effettiva e la data di rilascio sono soggetti a modifiche.

## Prossime funzionalità {#upcoming-features}

* Gli elementi nella barra a destra ora possono essere compressi nella schermata iniziale.
* Il selettore delle risorse ora supporta le definizioni dei filtri.
* Se non sono disponibili azioni per l&#39;elemento selezionato, il menu di scelta rapida non mostra più una freccia per accedere alle azioni.

## Prossimi miglioramenti {#upcoming-improvements}

* Se esiste una definizione di modello/filtro/componente, questa verrà recuperata quando si passa da un’app all’altra nell’editor.
* Se si rimuove un’immagine, non rimangono più tag immagine vuoti quando si utilizza DA come back-end.
* Le classi nei blocchi ora vengono gestite correttamente quando si utilizza DA come back-end.
* L’API aperta ora salva correttamente le risorse remote come oggetti.

## Prossima modifica necessaria {#breaking-change}

* Tutte le estensioni devono essere aggiornate a `@adobe/uix-guest` >= `1.1.7` per migliorare la stabilità.
