---
title: Authoring dei contenuti per Edge Delivery
description: Scopri come funziona l’authoring dei contenuti con Edge Delivery Services e come creare contenuti AEM con Edge Delivery Services.
feature: Edge Delivery Services
exl-id: 963ff71a-8176-4d9d-8240-dc429405d139
role: User
source-git-commit: 7ad9a959592f1e8cebbcad9a67d280d5b2119866
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 85%

---


# Authoring dei contenuti per Edge Delivery {#authoring-edge}

Con Edge Delivery Services, l’authoring è semplice, veloce e flessibile. Per creare contenuti per Edge Delivery Services, sono disponibili due opzioni:

* [Editor universale](#universal-editor) - Una moderna interfaccia WYSIWYG (What-you-see-is-what-you-get) per la creazione di contenuti all’interno dell’AEM
* [Authoring basato su documenti](#document-based): come Microsoft Word o documenti Google

## Authoring nell’Editor universale {#universal-editor}

Quando utilizzi Edge Delivery Services con AEM as a Cloud Service, l’elemento più importante da comprendere è che il contenuto che crei viene mantenuto in AEM as a Cloud Service.

![Funzionamento dell’authoring WYSIWYG con i Edge Delivery Services](assets/how-aem-edge-works.png)

1. [Ambiente di authoring WYSIWYG](/help/sites-cloud/authoring/quick-start.md) viene utilizzato per la gestione dei contenuti, ad esempio per creare nuove pagine, frammenti di esperienza, frammenti di contenuto e così via.
   * Sono disponibili tutte le funzioni di AEM, ad esempio flussi di lavoro, MSM, traduzione, lanci e così via.
1. [L’Editor universale](/help/sites-cloud/authoring/universal-editor/authoring.md) viene utilizzato per creare i contenuti gestiti in AEM.
   * L’Editor universale offre un’interfaccia utente nuova e moderna per l’authoring dei contenuti.
   * Per l’authoring, AEM esegue il rendering dell’HTML ma include gli script, gli stili, le icone e altre risorse di Edge Delivery Services.
   * Anche se viene utilizzato l’Editor universale, tutte le modifiche vengono mantenute in AEM.
   * L’Editor universale non dispone ancora del livello di parità con le funzioni dell’Editor pagina di AEM e alcune funzioni di AEM potrebbero non essere disponibili nell’Editor universale.
1. I contenuti creati con l’Editor universale e che vengono mantenuti in AEM vengono pubblicati in Edge Delivery Services.
   * Il contenuto rimane memorizzato in AEM.
   * AEM esegue il rendering dell’HTML semantico necessario per l’acquisizione.
   * Il contenuto viene pubblicato in Edge Delivery Services.
1. [Edge Delivery Services](/help/edge/developer/keeping-it-100.md) garantisce un punteggio Lighthouse del 100%.

I blocchi sono componenti fondamentali di una pagina distribuita da Edge Delivery Services. Gli autori possono scegliere tra i blocchi predefiniti forniti come standard da Adobe e quelli personalizzati per il progetto dagli sviluppatori.

L’Editor universale fornisce un’interfaccia grafica moderna e intuitiva per l’authoring dei contenuti mediante il trascinamento di blocchi.

![Trascinamento dei blocchi nell’Editor universale](assets/blocks.png)

I dettagli dei blocchi possono quindi essere configurati nella barra delle Proprietà.

![Configurazione delle proprietà del blocco](assets/block-properties.png)

Per informazioni dettagliate su come effettuare l’authoring con l’Editor universale, consulta il documento [Authoring dei contenuti con l’Editor universale.](/help/sites-cloud/authoring/universal-editor/authoring.md)

Consulta la sezione [Guida introduttiva per sviluppatori per l’authoring WYSIWYG con Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md) per scoprire come avviare un progetto personalizzato per l’authoring con AEM e Edge Delivery Services.

## Authoring basato su documenti  {#document-based}

Con l’authoring basato su documenti, puoi utilizzare origini diverse, ad esempio documenti Microsoft Word e Google. I documenti provenienti da queste origini diventano pagine del sito web. È possibile trasferire titoli, elenchi, immagini, elementi font e video dall’origine iniziale al tuo sito web. Puoi aggiungere metadati a scopo di SEO o utilizzare blocchi per lavorare con contenuti strutturati e aggiungere funzionalità.

Per ulteriori dettagli sull’authoring basato su documenti, consulta [questo documento nella documentazione di Edge Delivery Services.](/help/edge/docs/authoring.md)

