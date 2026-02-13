---
title: Note sulla versione di anteprima di Universal Editor
description: Queste sono le note sulla versione di anteprima di Universal Editor.
feature: Release Information
role: Admin
exl-id: e8d031aa-4676-4e45-977b-e5dffcc404c4
source-git-commit: 374c8045043f67f06d4ae68aef499bb594f1c08c
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Note sulla versione di anteprima di Universal Editor {#preview}

Queste sono le note sulla versione per la **versione di anteprima** di Universal Editor. Queste funzionalità sono attualmente disponibili nell&#39;**ambiente di anteprima** dell&#39;editor universale. Il rilascio di queste funzioni è previsto per il 19 febbraio 2026.

Queste note sulla versione di **preview** sono fornite per comodità, in modo da sapere quali modifiche all&#39;editor universale sono in arrivo e puoi testarle [passando alla versione di anteprima.](/help/sites-cloud/authoring/universal-editor/navigation.md#user-properties)

>[!TIP]
>
>Per le **note sulla versione corrente** di Universal Editor, vedere il documento [Note sulla versione di Universal Editor.](/help/release-notes/universal-editor/current.md)

>[!NOTE]
>
>Il contenuto della versione effettiva e la data di rilascio sono soggetti a modifiche.

## Nuove funzioni in arrivo {#what-is-new}

* Sono stati apportati miglioramenti all’editor Rich Text.
   * È ora supportato nascondere gli elementi della barra degli strumenti nell’editor Rich Text nel contesto.
   * È ora supportato il ritorno a capo del testo all’interno di tabelle con paragrafi.
   * I tag dell’editor Rich Text non supportati ora vengono mantenuti.
   * La logica dell’editor Rich Text viene ora gestita da un file separato.
   * È ora possibile creare e modificare le tabelle utilizzando l’editor Rich Text.
* Se non viene impostata alcuna etichetta, viene ora utilizzato il titolo del componente della definizione del componente.
* `setEditorMode` è ora disponibile tramite estensioni.

## Prossimi miglioramenti {#other-improvements}

* La funzionalità di copia e incolla tra pagine è stata corretta.
* `universal-editor-extensibility` è stato spostato in `universal-editor`.
* Il numero di richieste all’endpoint delle estensioni è stato ridotto.
* La disinstallazione di RemoteApp è stata ridotta da tre a uno.
* Gli endpoint dell’editor Rich Text vengono ora gestiti per l’editor locale.
* La modifica dei campi nidificati non comporta più la sovrascrittura delle voci dei peer da tali strutture.
* I campi obbligatori dell’Editor Rich Text non possono più essere salvati come vuoti.
* La formattazione diretta non viene più applicata in modo errato quando si aggiungono collegamenti dopo la formattazione.
