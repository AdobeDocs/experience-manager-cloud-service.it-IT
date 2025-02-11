---
title: Note sulla versione 2054.01.16 dell’editor universale
description: Queste sono le note sulla versione 2025.01.16 dell’editor universale.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: ht
source-wordcount: '236'
ht-degree: 100%

---


# Note sulla versione 2025.01.16 dell’editor universale {#release-notes}

Queste sono le note sulla versione del 16 gennaio 2025 dell’editor universale.

>[!TIP]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Novità {#what-is-new}

* **Obsolescenza della libreria CORS &lt; 3.0.0** - Per garantire la compatibilità futura e migliorare la sicurezza, l’editor universale ora supporta esclusivamente la versione 3.0.0 o successiva della
  `@Adobe Express/universal-editor-cors` libreria.
   * La libreria viene ora distribuita esclusivamente tramite [`universal-editor-service.adobe.io/cors.js`](http://universal-editor-service.adobe.io/cors.js).
   * All’apertura di una pagina che utilizza versioni precedenti della libreria CORS, viene visualizzata una notifica di obsolescenza che chiede agli utenti di effettuare l’aggiornamento.
* **Punto dell’estensione per la pagina di destinazione**. [È stato introdotto un nuovo punto dell’estensione](/help/implementing/universal-editor/customizing.md#extending) per la visualizzazione delle estensioni nella barra laterale della pagina di destinazione dell’editor universale.
   * Ora gli sviluppatori possono specificare se le estensioni sono applicabili all’editor, alla pagina di destinazione o a entrambi, offrendo maggiore personalizzazione e usabilità.

## Altri miglioramenti {#other-improvements}

* **Sono stati corretti URL non validi negli elementi recenti nella pagina di destinazione**: è stato risolto un problema a causa del quale gli URL visualizzati nell’elenco “Recenti” nella pagina di destinazione dell’editor universale risultavano danneggiati.
* **Sincronizzazione tema in Unified Shell**. L’editor universale sincronizza ora in modo dinamico il tema con le impostazioni di Unified Shell del sistema e regola automaticamente tra le modalità chiara e scura.
   * Ciò assicura un aspetto visivo coerente tra i micro front-end, inclusi i selettori di frammenti e risorse.
