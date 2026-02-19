---
title: Note sulla versione 2026.02.19 dell’editor universale
description: Queste sono le note sulla versione 2026.02.19 dell’editor universale.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 39137052e9fa409f7f5494be53fa7693aaa60b17
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 28%

---


# Note sulla versione 2026.02.19 dell’editor universale {#release-notes}

Queste sono le note sulla versione dell’Editor universale del 19 febbraio 2026.

>[!TIP]
>
>Se desideri testare le **prossime** funzionalità dell’editor universale prima che vengano rilasciate, consulta le [note sulla versione di anteprima dell’editor universale.](/help/release-notes/universal-editor/preview.md)

>[!TIP]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Novità {#what-is-new}

* Sono stati apportati miglioramenti all’editor Rich Text.
   * [È ora supportato nascondere gli elementi della barra degli strumenti nell&#39;editor Rich Text nel contesto](/help/implementing/universal-editor/configure-rte.md#common-action-options).
   * [Il ritorno a capo del testo nelle tabelle con paragrafi](/help/implementing/universal-editor/configure-rte.md#table-actions) è ora supportato.
   * [I tag di HTML non supportati](/help/implementing/universal-editor/configure-rte.md#unsupported-html) ora possono essere mantenuti dall&#39;editor Rich Text.
   * La logica dell’editor Rich Text viene ora gestita da un file separato.
   * È ora possibile creare [tabelle](/help/sites-cloud/authoring/universal-editor/authoring.md#formatting-options) e modificarle con l&#39;editor Rich Text.
* Se non viene impostata alcuna etichetta, viene ora utilizzato il titolo del componente della definizione del componente.
* `setEditorMode` è ora disponibile tramite estensioni.

## Funzioni per adozione anticipata {#early-adopter}

Se ti interessa testare le prossime funzionalità elencate di seguito e condividere i tuoi commenti, invia un’e-mail al tuo Customer Success Manager Adobe dall’indirizzo e-mail associato al tuo Adobe ID.

* La copia superficiale è stata implementata per i frammenti di contenuto.

## Altri miglioramenti {#other-improvements}

* Gli endpoint dell’editor Rich Text vengono ora gestiti per l’editor locale.
* La modifica dei campi nidificati non comporta più la sovrascrittura delle voci dei peer da tali strutture.
* I campi obbligatori dell’Editor Rich Text non possono più essere salvati come vuoti.
* La formattazione diretta non viene più applicata in modo errato quando si aggiungono collegamenti dopo la formattazione.
