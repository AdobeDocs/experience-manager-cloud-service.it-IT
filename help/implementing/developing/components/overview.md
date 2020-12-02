---
title: Componenti Panoramica
description: I componenti sono unità modulari che offrono funzionalità specifiche per presentare i contenuti sul sito Web
translation-type: tm+mt
source-git-commit: 83c27daae4e8ae2ae6a8f115c9da9527971c6ecb
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 7%

---


# Panoramica dei componenti {#components-overview}

Questa pagina fornisce una panoramica dei componenti Adobe Experience Manager (AEM) come quelli [utilizzati per l&#39;authoring delle pagine](/help/sites-cloud/authoring/fundamentals/components.md).

## Cosa sono i componenti? {#what-are-components}

I componenti in AEM sono:

* Unità modulari che realizzano funzionalità specifiche per presentare i contenuti sul sito Web.
* Riutilizzabile.
* Sviluppato come unità indipendenti all’interno di una cartella del repository.
* Non hanno file di configurazione nascosti.
* Può contenere altri componenti.
* Può essere eseguito ovunque all&#39;interno di qualsiasi sistema AEM e può essere eseguito solo in base a componenti specifici.
* Avere un&#39;interfaccia utente standard.
* Avere un comportamento di modifica configurabile.
* Utilizzare le finestre di dialogo create utilizzando sottoelementi basati sui componenti dell&#39;interfaccia utente Granite.
* Sono sviluppati utilizzando [HTL](https://docs.adobe.com/content/help/it-IT/experience-manager-htl/using/overview.html).
* Può essere sviluppato per creare componenti personalizzati che estendono le funzionalità predefinite.

Poiché i componenti sono modulari, potete:

* Sviluppare un nuovo componente nell’istanza locale.
* Distribuitelo nell&#39;ambiente di test.
* Potrai distribuirli nel tuo ambiente di authoring dal vivo, in cui gli autori e/o gli amministratori possono aggiungere e configurare contenuti.
* Distribuitelo negli ambienti di pubblicazione dal vivo, dove vengono usati per eseguire il rendering dei contenuti per i visitatori del sito Web.

Ciascun componente AEM:

* È un tipo di risorsa.
* È un insieme di script che realizza completamente una funzione specifica.
* Può funzionare isolatamente, ovvero all&#39;interno di AEM o di un portale.

## AEM Core Components {#aem-core-components}

[I ](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/introduction.html) componenti core AEM sono una serie di componenti Web Content Management (WCM) standardizzati che consentono di AEM per velocizzare i tempi di sviluppo e ridurre i costi di manutenzione dei siti Web.

I componenti core sono forniti con AEM come Cloud Service e l&#39; [Esercitazione WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) illustra come implementare e utilizzare i componenti. I componenti sono forniti con tutto il codice sorgente e possono essere utilizzati come punti di partenza per componenti modificati o estesi.

### Visualizzazione dei componenti disponibili {#viewing-available-components}

Per una panoramica di tutti i componenti disponibili nell&#39;istanza di AEM, utilizzate la [console Componenti](/help/sites-cloud/authoring/features/components-console.md).

In alternativa, potete anche utilizzare CRXDE Lite per ottenere un elenco di tutti i componenti disponibili nella directory archivio.

1. In **[!UICONTROL CRXDE Lite]**, selezionare **[!UICONTROL Strumenti]** dalla barra degli strumenti, quindi **[!UICONTROL Query]**, che apre la scheda **[!UICONTROL Query]**.

1. Nella scheda **[!UICONTROL Query]**, selezionare `XPath` come **[!UICONTROL Tipo]**.

1. Nel campo di inserimento **[!UICONTROL Query]** immettete la stringa seguente:

   `//element(*, cq:Component)`

1. Fare clic su **[!UICONTROL Esegui]** per elencare i componenti.

