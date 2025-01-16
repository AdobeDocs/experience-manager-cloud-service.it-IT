---
title: Note sulla versione 2054.01.16 dell’editor universale
description: Queste sono le note sulla versione 2025.01.16 dell’editor universale.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 14bc45917f56ecf358278848e7e830afb1fedccd
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 19%

---


# Note sulla versione 2025.01.16 dell’editor universale {#release-notes}

Queste sono le note sulla versione del 16 gennaio 2025 di Universal Editor.

>[!TIP]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina.](/help/release-notes/release-notes-cloud/release-notes-current.md)

## Novità {#what-is-new}

* **Deprecazione della libreria CORS &lt; 3.0.0** - Per garantire la compatibilità futura e migliorare la sicurezza, l&#39;Editor universale ora supporta esclusivamente la versione 3.0.0 o successiva della
  Libreria `@Adobe Express/universal-editor-cors`.
   * La libreria viene ora distribuita esclusivamente tramite [`universal-editor-service.adobe.io/cors.js`.](http://universal-editor-service.adobe.io/cors.js)
   * All’apertura di una pagina che utilizza versioni precedenti della libreria CORS, viene visualizzata una notifica di obsolescenza alla quale gli utenti dovranno effettuare l’aggiornamento.
* **Punto di estensione per la pagina di destinazione** - [È stato introdotto un nuovo punto di estensione](/help/implementing/universal-editor/customizing.md#extending) per la visualizzazione delle estensioni nella barra laterale della pagina di destinazione dell&#39;editor universale.
   * Ora gli sviluppatori possono specificare se le estensioni sono applicabili all’editor, alla pagina di destinazione o a entrambi, offrendo maggiore personalizzazione e usabilità.

## Altri miglioramenti {#other-improvements}

* **Sono stati corretti URL non validi negli elementi recenti nella pagina di destinazione**. È stato risolto un problema a causa del quale gli URL visualizzati nell&#39;elenco &quot;Recenti&quot; nella pagina di destinazione dell&#39;editor universale risultavano danneggiati.
* **Sincronizzazione tema in Unified Shell** - L&#39;editor universale sincronizza ora in modo dinamico il tema con le impostazioni di Unified Shell del sistema e regola automaticamente tra le modalità chiara e scura.
   * Ciò assicura un aspetto visivo coerente tra i micro front-end, inclusi i selettori di frammenti e risorse.
