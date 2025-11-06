---
title: Panoramica dei componenti
description: I componenti sono unità modulari che realizzano funzionalità specifiche per presentare i contenuti sul sito web
exl-id: 0fdc99e7-2103-448d-8217-d5d52c94acea
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 66%

---

# Panoramica dei componenti {#components-overview}

Questa pagina fornisce una panoramica dei componenti di Adobe Experience Manager (AEM) come quelli [utilizzati per l’authoring delle pagine](/help/sites-cloud/authoring/page-editor/components.md).

## Cosa sono i Componenti? {#what-are-components}

* Unità modulari che realizzano funzionalità specifiche per presentare i contenuti sul sito web.
* Riutilizzabile.
* Sviluppati come unità autonome all’interno di una cartella dell’archivio.
* Non sono presenti file di configurazione nascosti.
* Possono contenere altri componenti.
* Possono essere eseguiti ovunque all’interno di qualsiasi sistema AEM e possono anche essere limitati per l’esecuzione con componenti specifici.
* Hanno un’interfaccia utente standard.
* Hanno un comportamento di modifica configurabile.
* Utilizza finestre di dialogo create utilizzando sottoelementi basati su componenti dell’interfaccia utente Granite.
* Vengono sviluppati utilizzando [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=it).
* Possono essere sviluppati per creare componenti personalizzati che estendono la funzionalità predefinita.

Poiché i componenti sono modulari, puoi:

* Sviluppare un nuovo componente nell’istanza locale.
* Distribuirlo nell’ambiente di test.
* Distribuirlo nel tuo ambiente di authoring live, dove gli autori e/o gli amministratori possono aggiungere e configurare contenuti.
* Distribuiscilo negli ambienti di pubblicazione live, dove viene utilizzato per eseguire il rendering dei contenuti per i visitatori del tuo sito web.

Ogni componente AEM:

* È un tipo di risorsa.
* È un insieme di script che realizzano completamente una funzione specifica.
* Può funzionare in isolamento, ovvero all’interno di AEM o di un portale.

## Componenti core AEM {#aem-core-components}

[I componenti core di AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) sono un insieme di componenti WCM (Web Content Management) standardizzati di AEM che consentono di velocizzare i tempi di sviluppo e ridurre i costi di manutenzione dei siti Web.

I Componenti core sono forniti con AEM as a Cloud Service e il [Tutorial WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) illustra come implementarli e utilizzarli. I componenti sono forniti con tutto il codice sorgente e possono essere utilizzati così come sono o come punti di partenza per i componenti modificati o estesi.

### Visualizzazione dei componenti disponibili {#viewing-available-components}

Per una panoramica di tutti i componenti disponibili nell&#39;istanza di AEM, utilizza la [console Componenti](/help/sites-cloud/authoring/components-console.md).

In alternativa, è possibile utilizzare CRXDE Lite per ottenere un elenco di tutti i componenti disponibili nell’archivio.

1. In **[!UICONTROL CRXDE Lite]**, seleziona **[!UICONTROL Strumenti]** dalla barra degli strumenti, quindi **[!UICONTROL Query]**, che apre la scheda **[!UICONTROL Query]**.

1. Nella scheda **[!UICONTROL Query]**, seleziona `XPath` come **[!UICONTROL Tipo]**.

1. Nel campo di input **[!UICONTROL Query]** immettere la stringa seguente:

   `//element(*, cq:Component)`

1. Fai clic su **[!UICONTROL Esegui]** e i componenti verranno elencati.
