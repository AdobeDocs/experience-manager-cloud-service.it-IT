---
title: Note sulla versione di Universal Editor 2024.08.13
description: Queste sono le note sulla versione 2024.08.13 di Universal Editor.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: c66621eb336b8e6eb5ceb1056c089c190fcd1c34
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---


# Note sulla versione di Universal Editor 2024.08.13 {#release-notes}

Queste sono le note sulla versione di Universal Editor del 13 agosto 2024.

>[!TIP]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina.](/help/release-notes/release-notes-cloud/release-notes-current.md)

## Novità {#what-is-new}

* **Tipi di dati personalizzati**: adatta l&#39;editor alle tue esigenze di dati univoci con la possibilità di [creare campi personalizzati all&#39;interno del pannello delle proprietà.](https://developer.adobe.com/uix/docs/services/aem-universal-editor/api/item-types-renderers/)
   * Che tu stia sviluppando un selettore di prodotti personalizzato per i casi d’uso di e-commerce o compilando un elenco a discesa con i valori provenienti dai tuoi backend, questa funzione ti offre il controllo necessario sui dati utilizzati dagli autori per comporre i contenuti.
* **Trascinamento selezione tra contenitori**: maggiore flessibilità nella composizione del layout con la possibilità di [spostare i componenti tra contenitori diversi tramite trascinamento](/help/sites-cloud/authoring/universal-editor/authoring.md#reordering-components) nel pannello [Struttura contenuto.](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode)
* **Integrazione GitHub ottimizzata**: è stata introdotta la memorizzazione in cache per le risposte GitHub, velocizzando notevolmente il recupero dei tag e di `universal-editor-cors-library`, con conseguente esperienza utente più veloce e fluida.
* **Convalida del token IMS configurabile**: per aumentare la flessibilità nella gestione dei token, la convalida del token IMS [è ora facoltativa.](/help/implementing/universal-editor/local-dev.md#setting-up-service)
   * Questa opzione di configurazione consente di disabilitare la convalida in base alle esigenze, semplificando le impostazioni del gateway cloud.
* **Integrazione Splunk**: la registrazione Splunk è stata integrata nel [servizio Editor universale per lo sviluppo locale,](/help/implementing/universal-editor/local-dev.md#setting-up-service) migliorando il monitoraggio e la diagnostica.
   * Questa integrazione garantisce un tracciamento efficiente dei registri, operazioni più semplici e una risoluzione più rapida dei problemi.

## Correzioni di bug {#bug-fixes}

* **Feedback di pubblicazione avanzato**: se la pubblicazione non riesce a causa di autorizzazioni insufficienti, il feedback fornito all&#39;utente durante la pubblicazione è stato migliorato per visualizzare un avviso chiaro, anziché indicare semplicemente un errore.
* **Gestione URL migliorata**: sono stati risolti i problemi di codifica/decodifica URL errata che causavano errori di pubblicazione.
* **Gestione accurata dei dati**: è stato risolto un problema a causa del quale i numeri in virgola mobile non venivano memorizzati correttamente come numeri interi, garantendo una gestione precisa dei dati nel contenuto.
* **Sicurezza e stabilità**: le vulnerabilità di sicurezza nelle immagini Docker sono state corrette e la copertura dei test per i componenti critici come il selettore dei componenti e le breadcrumb è stata implementata, garantendo un&#39;esperienza di editor più sicura, stabile e affidabile.
