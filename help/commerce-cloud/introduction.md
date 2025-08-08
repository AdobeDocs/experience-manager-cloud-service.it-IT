---
title: Introduzione e panoramica
description: Comprendere le diverse opzioni della vetrina
thumbnail: introducing-aem-commerce.jpg
exl-id: 29410f76-a63f-4b0a-b817-2ed724ad1a3c
feature: Commerce Integration Framework
role: Admin
source-git-commit: ecb2638cfa65a0a2a24779723bdb301f9d3f1268
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 1%

---


# Content and Commerce {#content-commerce}

Con l&#39;aumento delle aspettative dei clienti per esperienze di e-commerce basate su intenti e ad alte prestazioni, i brand sono sotto pressione per fornire più contenuti in modo più rapido, senza sacrificare la qualità. Con Adobe Experience Manager, i brand possono scalare e innovare più rapidamente per creare esperienze di e-commerce coinvolgenti e acquisire più traffico e una spesa online in crescita.

Adobe Experience Manager offre potenti strumenti per creare e gestire esperienze cliente personalizzate e ricche di contenuti. Integrando AEM con una soluzione commerce, ad esempio Adobe Commerce, Salesforce Commerce, SAP Commerce Cloud o qualsiasi altra soluzione, i brand possono unificare contenuti e soluzioni commerce per offrire percorsi di acquisto fluidi su tutti i canali.

## Panoramica degli approcci storefront {#overview}

AEM può supportarti in base alla tua situazione e alle tue preferenze. Per scegliere l’approccio più adatto alle tue esigenze, segui le istruzioni riportate di seguito.

* [Usa Edge Delivery Services (scelta consigliata)](#edge)
* [Usa la tua vetrina (integrazione headless di AEM)](#own-storefront)
* [Utilizza AEM CIF storefront](#cif)

### Usa Edge Delivery Services (consigliato) {#edge}

Se la tua azienda desidera la vetrina più veloce e adatta all&#39;intelligenza artificiale sul Web e i tuoi sviluppatori desiderano un&#39;esperienza di sviluppo all&#39;avanguardia, utilizza [Edge Delivery Services.](../edge/overview.md) Edge Delivery Services soddisfa tutti i requisiti attuali e futuri. A seconda del back-end e della soluzione, sono disponibili diverse opzioni:

#### &#x200B;1. Integrazione con Adobe Commerce as a Cloud Service {#acaacs}

Adobe consiglia di utilizzare Edge Delivery e [Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=it) come punto di partenza. La vetrina è dotata di una piattaforma integrata con i servizi e le API di Adobe Commerce e offre una varietà di componenti aggiuntivi Commerce per costruire rapidamente una vetrina.

Buona vestibilità: esperienza tipica della vetrina con Adobe Commerce as a Cloud Service

#### &#x200B;2. Integrazione con Adobe Commerce Optimizer (per qualsiasi soluzione di terze parti) {#aco}

Se desideri integrare la tua soluzione commerce esistente e migliorare le prestazioni del catalogo, Adobe consiglia di utilizzare [Adobe Commerce Optimizer](https://experienceleague.adobe.com/it/docs/commerce-learn/tutorials/adobe-commerce-optimizer/overview) come livello di integrazione moderno. Commerce Optimizer migliora la tua soluzione commerce con servizi SaaS ad alte prestazioni per la catalogazione e la merchandizzazione. Come per Adobe Commerce as a Cloud Service, [Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=it) è pronto all&#39;uso.

Sono disponibili integrazioni alle soluzioni commerciali come Salesforce Commerce. Contatta il tuo rappresentante Adobe.

Buona vestibilità: tipica esperienza di vetrina con una soluzione di e-commerce esistente

#### &#x200B;3. Integrazione personalizzata {#custom}

Adobe consiglia inoltre di utilizzare Edge Delivery Services se desideri creare un’integrazione personalizzata. Puoi iniziare da zero o riutilizzare i componenti commerce JS-framework esistenti (ad esempio, per la parte transazionale) nella vetrina Edge Delivery. In questo modo, i vostri clienti potranno godere di un&#39;esperienza di acquisto incredibilmente rapida e di facile utilizzo, e potrete al contempo riutilizzare i vostri investimenti per aumentare il TTV. Il punto di partenza è il [Edge Delivery Boilerplate](https://www.aem.live/developer/tutorial) predefinito.

Buona vestibilità: basso valore dalla vetrina Edge Deliery

### Usa la tua vetrina (integrazione headless di AEM) {#own-storefront}

Hai una vetrina esistente (ad esempio, creata con React JS) e desideri utilizzare Adobe Experience Manager per la gestione e la distribuzione dei contenuti (frammenti di contenuto), le risorse e la modifica nel contesto (Editor universale). Il punto di partenza per un&#39;integrazione è [Introduzione a Adobe Experience Manager as a Headless CMS](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/headless/introduction) e il componente aggiuntivo [CIF](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/content-and-commerce/storefront/authoring/enrich-product-associated-content). Il componente aggiuntivo CIF consente un’integrazione diretta dei dati dei prodotti in AEM (cerca, sfoglia e trova prodotti nell’interfaccia utente di AEM) da utilizzare per creare esperienze specifiche per l’e-commerce.

### vetrina AEM CIF {#cif}

L’architettura di riferimento e i consigli di Adobe consiste nell’utilizzare Edge Delivery Services. La vetrina CIF con i suoi componenti core CIF di AEM è ora in modalità di manutenzione e non deve essere utilizzata in nuovi progetti. Per maggiori informazioni, consulta la [documentazione di CIF.](/help/commerce-cloud/cif-introduction.md)

>[!NOTE]
>
>I clienti esistenti che desiderano sfruttare le nuove funzionalità di AEM/Commerce devono spostare il sito web in Edge Delivery. Un pattern comune consiste nello spostare solo un sottoinsieme di pagine in Edge Delivery ed eseguire pagine Edge Delivery e CIF in modalità affiancata. È inoltre possibile sostituire i componenti CIF di AEM con i nuovi [componenti aggiuntivi di Commerce](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/all/introduction/?lang=it) per sfruttare le nuove funzionalità di Commerce.
