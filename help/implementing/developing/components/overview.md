---
title: Panoramica dei componenti
description: I componenti sono unità modulari che realizzano funzionalità specifiche per presentare i contenuti sul sito web
exl-id: 0fdc99e7-2103-448d-8217-d5d52c94acea
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 100%

---

# Panoramica dei componenti {#components-overview}

Questa pagina fornisce una panoramica dei componenti di Adobe Experience Manager (AEM) come quelli [utilizzati per l’authoring delle pagine](/help/sites-cloud/authoring/fundamentals/components.md).

## Cosa sono i Componenti? {#what-are-components}

I componenti in AEM sono:

* Unità modulari che realizzano funzionalità specifiche per presentare i contenuti sul sito web.
* Riutilizzabili.
* Sviluppati come unità autonome all’interno di una cartella dell’archivio.
* Non sono presenti file di configurazione nascosti.
* Possono contenere altri componenti.
* Possono essere eseguiti ovunque all’interno di qualsiasi sistema AEM e possono essere limitati all’esecuzione in base a componenti specifici.
* Hanno un’interfaccia utente standard.
* Hanno un comportamento di modifica configurabile.
* Utilizzano le finestre di dialogo create utilizzando elementi secondari basati sui componenti dell’interfaccia utente Granite.
* Sono sviluppati utilizzando [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=it).
* Possono essere sviluppati per creare componenti personalizzati che estendono la funzionalità predefinita.

Poiché i componenti sono modulari, puoi:

* Sviluppare un nuovo componente nell’istanza locale.
* Distribuirlo nell’ambiente di test.
* Distribuirlo nel tuo ambiente di authoring live, dove gli autori e/o gli amministratori possono aggiungere e configurare contenuti.
* Distribuirlo negli ambienti di pubblicazione live, dove viene utilizzata per il rendering dei contenuti per i visitatori del sito web.

Ogni componente AEM:

* È un tipo di risorsa.
* È un insieme di script che realizzano completamente una funzione specifica.
* Può funzionare in isolamento, ovvero all’interno di AEM o di un portale.

## Componenti core AEM {#aem-core-components}

[I Componenti core AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) sono un set di componenti di Gestione contenuti web (Web Content Management, WCM) standardizzati di AEM che consentono di velocizzare i tempi di sviluppo e ridurre i costi di manutenzione dei siti web.

I Componenti core sono forniti con AEM as a Cloud Service e il [Tutorial WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) illustra come implementarli e utilizzarli. I componenti sono forniti con tutto il codice sorgente e possono essere utilizzati così come sono o come punti di partenza per i componenti modificati o estesi.

### Visualizzazione dei componenti disponibili {#viewing-available-components}

Per una panoramica di tutti i componenti disponibili nell’istanza di AEM, utilizza la funzione [Console Componenti](/help/sites-cloud/authoring/features/components-console.md).

In alternativa, è possibile utilizzare CRXDE Lite per ottenere un elenco di tutti i componenti disponibili nell’archivio.

1. In **[!UICONTROL CRXDE Lite]**, seleziona **[!UICONTROL Strumenti]** dalla barra degli strumenti, quindi **[!UICONTROL Query]**, che apre la scheda **[!UICONTROL Query]**.

1. Nella scheda **[!UICONTROL Query]**, seleziona `XPath` come **[!UICONTROL Tipo]**.

1. Nel campo di inserimento **[!UICONTROL Query]**, immetti la stringa seguente:

   `//element(*, cq:Component)`

1. Fai clic su **[!UICONTROL Esegui]** e i componenti verranno elencati.
