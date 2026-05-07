---
title: Note sulla versione di Universal Editor 2026.05.07
description: Queste sono le note sulla versione 2026.05.07 di Universal Editor.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 4f66cd6048d7a78bea33c0f9c21017983b9032d5
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 12%

---


# Note sulla versione di Universal Editor 2026.05.07 {#release-notes}

Queste sono le note sulla versione del 7 maggio 2026 di Universal Editor.

>[!TIP]
>
>Se desideri testare le **prossime** funzionalità dell’editor universale prima che vengano rilasciate, consulta le [note sulla versione di anteprima dell’editor universale.](/help/release-notes/universal-editor/preview.md)

>[!TIP]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina.](/help/release-notes/release-notes-cloud/release-notes-current.md)

## Novità {#what-is-new}

* È ora possibile [trascinare i componenti nell&#39;editor per spostarli.](/help/sites-cloud/authoring/universal-editor/authoring.md#drag-and-drop-move)
* È stato introdotto un service worker per ridurre la latenza tra l’interfaccia utente di Universal Editor e i sistemi back-end.
* Tutti gli adattatori per i frammenti di contenuto (AEM 6.5, OpenAPI e GraphQL) ora includono i filtri per il selettore delle risorse per garantire coerenza e consentire agli utenti di selezionare solo le risorse consentite.
* L&#39;intento `content:patch` è ora specificato.
* Per facilitare l’accessibilità, sono stati definiti il flusso di authoring e i punti di riferimento.

## Altri miglioramenti imminenti {#other-improvements}

* Le asserzioni di tipo non necessarie in `assignImageDimensionFields` sono state rimosse.
* È stato risolto un problema a causa del quale la gestione lato server dell&#39;operazione `add` ripeteva il valore stringa, considerandolo come un oggetto invece che come una patch.
