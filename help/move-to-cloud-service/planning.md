---
title: Fase di pianificazione
description: Fase di pianificazione
translation-type: tm+mt
source-git-commit: fdcad36713cdcd766d7d698a2e6c017dad1b03a0
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 91%

---


# Pianificazione {#planning-phase}

Prima di iniziare il percorso di transizione verso Cloud Service, devi acquisire familiarità con AEM as a Cloud Service, esaminare le modifiche rilevanti apportate al servizio e rivedere inoltre le funzioni che sono state sostituite o dichiarate obsolete.

## Modifiche di rilievo {#notable-changes}

AEM as a Cloud Service include molte nuove funzioni e opportunità per gestire i progetti AEM.

Tuttavia, esistono alcune differenze tra AEM On-Premise o in Adobe Managed Services e AEM as a Cloud Service.

Per informazioni sulle differenze più importanti, consulta [Modifiche di rilievo apportate ad AEM Cloud Service](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/release-notes/aem-cloud-changes.html).

## Funzioni obsolete {#deprecated-features}

Adobe valuta costantemente le funzionalità dei prodotti per reinventare o sostituire nel tempo le funzioni meno recenti con alternative più moderne al fine di migliorare il valore complessivo per il cliente, tenendo comunque in considerazione la compatibilità con le versioni precedenti.

Per ulteriori informazioni sulle funzioni e funzionalità dichiarate obsolete in Experience Manager as a Cloud Service, consulta [Funzioni obsolete](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/release-notes/deprecated-removed-features.html#deprecated-features).

## Informazioni sulla fase di pianificazione {#introduction}

Nella figura seguente sono illustrati i passaggi chiave della fase di pianificazione:

![immagine](/help/move-to-cloud-service/assets/planning-phaseimg1.png)

### Valutazione della preparazione a Cloud Service {#access-cloud-readiness}

Il primo passaggio nella fase di pianificazione consiste nel valutare il grado di preparazione al passaggio dalla versione esistente di AEM a Cloud Service e nel determinare le aree che richiederanno il refactoring per diventare compatibili con AEM as a Cloud Service.

Dovrai effettuare una valutazione completa del codice sorgente AEM corrente rispetto alle modifiche di rilievo e alle funzioni obsolete, al fine di determinare quanto lavoro richiede il percorso di transizione.

Puoi accelerare la fase di valutazione eseguendo il Cloud Readiness Analyzer (CRA) nella versione corrente AEM. Per ulteriori informazioni, consulta Panoramica [](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/cloud-readiness-analyzer/overview-cloud-readiness-analyzer.html)CRA.

>[!NOTE]
>Se disponi già dell’accesso a Cloud Manager e a un ambiente Cloud Service, è consigliabile eseguire il codice corrente in una pipeline di qualità del codice di Cloud Manager per valutare la compatibilità delle modifiche del codice necessarie con Cloud Service.

### Esame della pianificazione delle risorse {#review-resource-planning}

Dopo aver stimato il lavoro necessario per passare a Cloud Service, devi individuare le risorse, creare un team e assegnare ruoli e responsabilità per il processo di transizione.

### Definizione dei KPI {#establish-kpis}

Se in precedenza non sono stati definiti indicatori di prestazioni chiave (KPI, Key Performance Indicators), si consiglia di stabilirli per l’implementazione di Adobe Experience Manager (AEM), in modo da aiutare il team a concentrarsi su ciò che conta di più.

Per scoprire come scegliere i giusti KPI per gli obiettivi aziendali, consulta l’articolo sullo [sviluppo dei KPI](https://guided.adobe.com/welcome/aem/part6.html).

