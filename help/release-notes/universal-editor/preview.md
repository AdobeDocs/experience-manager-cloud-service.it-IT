---
title: Note sulla versione di anteprima di Universal Editor
description: Queste sono le note sulla versione di anteprima di Universal Editor.
feature: Release Information
role: Admin
exl-id: e8d031aa-4676-4e45-977b-e5dffcc404c4
source-git-commit: f3ba70f276ab534e0becea47390fe58bf8a825d2
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---


# Note sulla versione di anteprima di Universal Editor {#preview}

Queste sono le note sulla versione per la **versione di anteprima** di Universal Editor. Queste funzionalità sono attualmente disponibili nell&#39;**ambiente di anteprima** dell&#39;editor universale. Il rilascio di queste funzioni è previsto per il 7 maggio 2026.

Queste note sulla versione di **preview** sono fornite per comodità, in modo da sapere quali modifiche all&#39;editor universale sono in arrivo e puoi testarle [passando alla versione di anteprima.](/help/sites-cloud/authoring/universal-editor/navigation.md#user-properties)

>[!TIP]
>
>Per le **note sulla versione corrente** di Universal Editor, vedere il documento [Note sulla versione di Universal Editor.](/help/release-notes/universal-editor/current.md)

>[!NOTE]
>
>Il contenuto della versione effettiva e la data di rilascio sono soggetti a modifiche.

## Prossime funzionalità {#upcoming-features}

* È stato introdotto un service worker per ridurre la latenza tra l’interfaccia utente di Universal Editor e i sistemi back-end.
* Tutti gli adattatori per i frammenti di contenuto (AEM 6.5, OpenAPI e GraphQL) ora includono i filtri per il selettore delle risorse per garantire coerenza e consentire agli utenti di selezionare solo le risorse consentite.
* L&#39;intento `content:patch` è ora specificato.
* Per facilitare l’accessibilità, sono stati definiti il flusso di authoring e i punti di riferimento.

## Altri miglioramenti imminenti {#other-improvements}

* Le asserzioni di tipo non necessarie in `assignImageDimensionFields` sono state rimosse.
* È stato risolto un problema a causa del quale la gestione lato server dell&#39;operazione `add` ripeteva il valore stringa, considerandolo come un oggetto invece che come una patch.
