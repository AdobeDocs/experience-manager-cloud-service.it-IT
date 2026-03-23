---
title: Note sulla versione 2026.03.19 dell’editor universale
description: Queste sono le note sulla versione 2026.03.19 dell’editor universale.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 048e86fe7930173bb33de9252607e2910520b575
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 34%

---


# Note sulla versione 2026.03.19 dell’editor universale {#release-notes}

Queste sono le note sulla versione del 19 marzo 2026 di Universal Editor.

>[!TIP]
>
>Se desideri testare le **prossime** funzionalità dell’editor universale prima che vengano rilasciate, consulta le [note sulla versione di anteprima dell’editor universale.](/help/release-notes/universal-editor/preview.md)

>[!TIP]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Novità {#what-is-new}

* Gli elementi nelle proprietà ora sono compressi quando si torna alla schermata iniziale [.](/help/sites-cloud/authoring/universal-editor/navigation.md#home-button)
* [Il selettore risorse](/help/implementing/universal-editor/configure-assets-selector.md) ora supporta [le definizioni dei filtri.](/help/implementing/universal-editor/filtering.md)
* Se non sono disponibili azioni per l&#39;elemento selezionato, [nel menu di scelta rapida](/help/sites-cloud/authoring/universal-editor/authoring.md#context-menu) viene ora visualizzato un messaggio che indica tali azioni.

## Altri miglioramenti {#other-improvements}

* Se esiste una definizione di modello/filtro/componente, questa verrà recuperata quando si passa da un’app all’altra nell’editor.
* Se si rimuove un’immagine, non rimangono più tag immagine vuoti quando si utilizza DA come back-end.
* Le classi nei blocchi ora vengono gestite correttamente quando si utilizza DA come back-end.
* L’API aperta ora salva correttamente le risorse remote come oggetti.

## Modifica necessaria {#breaking-change}

* Tutte le estensioni devono essere aggiornate a `@adobe/uix-guest` >= `1.1.7` per migliorare la stabilità.
