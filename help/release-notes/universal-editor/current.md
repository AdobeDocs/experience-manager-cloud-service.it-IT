---
title: Note sulla versione di Universal Editor 2024.09.3
description: Queste sono le note sulla versione 2024.09.3 di Universal Editor.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: b70acef8dc259fff3041617abe0a89f7eb73dfab
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 1%

---


# Note sulla versione di Universal Editor 2024.09.3 {#release-notes}

Queste sono le note sulla versione del 3 settembre 2024 di Universal Editor.

>[!TIP]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina.](/help/release-notes/release-notes-cloud/release-notes-current.md)

## Novità {#what-is-new}

* **`rootPath`ora disponibile per il selettore contenuto**: è ora possibile fornire al selettore contenuto un `rootPath` per presentare all&#39;utente una selezione mirata di contenuti quando si utilizzano i tipi di campo [Contenuto AEM,](/help/implementing/universal-editor/field-types.md#aem-content) [Frammento contenuto,](/help/implementing/universal-editor/field-types.md#content-fragment) e [Frammento esperienza](/help/implementing/universal-editor/field-types.md#experience-fragment).
   * La selezione del contenuto è quindi limitata al contenuto nel percorso specificato e alle eventuali sottodirectory.

## Programma di adozione anticipata per il supporto della versione 6.5 {#early-adoption}

L’Editor universale è ora disponibile per i casi d’uso headless quando si utilizza AEM 6.5 come parte di un programma per utenti iniziali.

Se ti interessa testare questa nuova funzione e condividere i tuoi commenti, invia un’e-mail al tuo rappresentante dell’Adobe dall’indirizzo e-mail associato al tuo Adobe ID.

## Correzioni di bug {#bug-fixes}

* **Trascina e rilascia tra contenitori**: [Lo spostamento di componenti tra contenitori diversi tramite trascinamento](/help/sites-cloud/authoring/universal-editor/authoring.md#reordering-components) rispetta ora [filtri componenti](/help/implementing/universal-editor/customizing.md#filtering-components) sia nell&#39;origine che nella destinazione.
