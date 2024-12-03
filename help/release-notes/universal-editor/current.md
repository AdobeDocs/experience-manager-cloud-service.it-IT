---
title: Note sulla versione 2024.12.02 dell’editor universale
description: Queste sono le note sulla versione 2024.12.02 dell’editor universale.
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 2aae8c63358680758e4f5324f38dea1bc2c47155
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 16%

---


# Note sulla versione 2024.12.02 dell’editor universale {#release-notes}

Queste sono le note sulla versione del 2 dicembre 2024 di Universal Editor.

>[!TIP]
>
>Per le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, consulta [questa pagina.](/help/release-notes/release-notes-cloud/release-notes-current.md)

## Novità {#what-is-new}

* **Navigazione tramite tastiera della struttura contenuto**: [La struttura contenuto,](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode) disponibile nel pannello laterale, è ora completamente accessibile tramite tastiera.
   * Gli autori possono navigare e interagire con gli elementi della visualizzazione struttura utilizzando controlli da tastiera standard, in conformità alle [linee guida WCAG 2.1](/help/sites-cloud/authoring/page-editor/accessible-content.md) per l&#39;accessibilità.
   * Questo miglioramento garantisce che tutti gli elementi interattivi all’interno della struttura siano utilizzabili da tastiera, migliorando l’inclusività per gli utenti che si affidano alla navigazione da tastiera.
* **Deselezione degli elementi modificabili**: gli autori possono ora deselezionare gli elementi modificabili precedentemente selezionati nella pagina.
   * Questo elimina le distrazioni quando gli autori desiderano visualizzare la pagina senza bordi di selezione attivi.
* **Selettore frammenti**: nelle istanze di AEM as a Cloud Service, i riferimenti ai frammenti ora aprono il selettore frammenti come selettore contenuto, fornendo funzionalità migliorate come il rispetto dei modelli di frammenti di contenuto consentiti, la ricerca di frammenti di contenuto e un’esperienza complessiva migliorata.
   * Ciò è in linea con le altre interfacce utente di Adobe e migliora la coerenza.
   * [Per gli ambienti AEM 6.5,](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction) il selettore di contenuti esistente rimane in uso.
* **Descrizione contenitore**: [Il componente contenitore](/help/implementing/universal-editor/field-types.md#container) utilizzato nel pannello [proprietà,](/help/sites-cloud/authoring/universal-editor/navigation.md#properties-panel-properties-rail) per fare riferimento al contenuto, ora supporta un attributo descrizione, visualizzato sopra i campi contenitore.
   * Questa aggiunta migliora la chiarezza fornendo agli autori il contesto dei campi raggruppati che stanno modificando.

## Altri miglioramenti {#other-improvements}

* **Sincronizzazione campi Rich Text**: è stata migliorata la sincronizzazione del contenuto non elaborato e di cui è stato eseguito il rendering all&#39;interno dei campi Rich Text nel pannello delle proprietà, risolvendo i problemi all&#39;interno dei progetti di Edge Delivery Services in cui il contenuto Rich Text e la rappresentazione di cui è stato eseguito il rendering possono differire.
* **Eventi modalità di modifica**: l&#39;editor universale ora emette in modo affidabile eventi modalità di modifica, anche dopo il ricaricamento delle app remote.
