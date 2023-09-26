---
title: Panoramica dei componenti
description: I componenti sono unità modulari che realizzano funzionalità specifiche per presentare i contenuti sul sito web
exl-id: 0fdc99e7-2103-448d-8217-d5d52c94acea
source-git-commit: 78ead5f15c2613d9c3bed3025b43423a66805c59
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 67%

---

# Panoramica dei componenti {#components-overview}

Questa pagina fornisce una panoramica dei componenti di Adobe Experience Manager (AEM) come quelli [utilizzati per l’authoring delle pagine](/help/sites-cloud/authoring/fundamentals/components.md).

## Cosa sono i Componenti? {#what-are-components}

* Unità modulari che realizzano funzionalità specifiche per presentare i contenuti sul sito web.
* Riutilizzabile.
* Sviluppati come unità autonome all’interno di una cartella dell’archivio.
* Non sono presenti file di configurazione nascosti.
* Possono contenere altri componenti.
* Possono essere eseguiti ovunque all&#39;interno di qualsiasi sistema AEM e possono anche essere limitati per funzionare con componenti specifici.
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

[Componenti core dell’AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) sono un set di componenti WCM (Web Content Management) standardizzati per l’AEM che consentono di velocizzare i tempi di sviluppo e ridurre i costi di manutenzione dei siti web.

I Componenti core sono forniti con AEM as a Cloud Service e il [Tutorial WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) illustra come implementarli e utilizzarli. I componenti sono forniti con tutto il codice sorgente e possono essere utilizzati così come sono o come punti di partenza per i componenti modificati o estesi.

### Visualizzazione dei componenti disponibili {#viewing-available-components}

Per una panoramica di tutti i componenti disponibili nell’istanza AEM, utilizza [Console Componenti](/help/sites-cloud/authoring/features/components-console.md).

In alternativa, è possibile utilizzare CRXDE Lite per ottenere un elenco di tutti i componenti disponibili nell’archivio.

1. In **[!UICONTROL CRXDE Lite]**, seleziona **[!UICONTROL Strumenti]** dalla barra degli strumenti, quindi **[!UICONTROL Query]**, che apre la scheda **[!UICONTROL Query]**.

1. Nella scheda **[!UICONTROL Query]**, seleziona `XPath` come **[!UICONTROL Tipo]**.

1. In **[!UICONTROL Query]** campo di input, immettere la seguente stringa:

   `//element(*, cq:Component)`

1. Fai clic su **[!UICONTROL Esegui]** e i componenti verranno elencati.
