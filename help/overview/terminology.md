---
title: Introduzione ad Adobe Experience Manager as a Cloud Service - Terminologia
description: Introduzione ad Adobe Experience Manager as a Cloud Service - Terminologia.
exl-id: a76f68f1-4f84-4844-a099-0952707cd96d
source-git-commit: e83ce89aedb3c5ea22243d0f86a528286e994338
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service - Terminologia {#adobe-experience-manager-as-a-cloud-service-terminology}

I termini seguenti sono utilizzati in riferimento ad Adobe Experience Manager (AEM) as a Cloud Service:

## Prodotti {#products}

| Prodotto | Descrizione |
|---|---|
| AEM as a Cloud Service | Soluzione nativa per il cloud che consente di sfruttare le applicazioni AEM. |
| AEM Assets as a Cloud Service | Funzionalità Digital Asset Management (DAM) incluse in una soluzione scalabile e nativa per il cloud, per inserire, elaborare e gestire le risorse digitali, garantendo l’integrazione con il più esteso ecosistema Adobe Experience Cloud e Adobe Creative Cloud. |
| AEM Sites as a Cloud Service | Istanza di AEM as a Cloud Service che include l’applicazione AEM Sites. |

## Istanze e pipeline {#instances-and-pipelines}

| Istanza | Descrizione |
|---|---|
| Pipeline Adobe | Meccanismo di pubblicazione dei contenuti dall’ambiente di authoring a quello di pubblicazione. |
| Livello di authoring AEM | Riferito all’ambiente di authoring per Sites e Assets. |
| Livello anteprima AEM | Descriva l’ambiente di anteprima per Sites. |
| Livello di pubblicazione AEM | Riferito all’ambiente di pubblicazione per Sites. |


<!-- This section of the table must be alphabetic -->

## Terminologia {#terminology}

| Termine | Descrizione |
|---|---|
| Immagine AEM | Artefatto distribuibile che contiene il codice prodotto AEM unitamente al codice cliente. |
| Microservizi per le risorse | Servizi di elaborazione delle risorse digitali basati su cloud che si prestano a diversi casi d’uso per l’elaborazione di risorse, ad esempio generazione di rendering, elaborazioni di PDF, gestione delle risorse secondarie, estrazione del testo e così via. Per ulteriori informazioni, consulta [Panoramica sui microservizi per le risorse](/help/assets/asset-microservices-overview.md). |
| Archivio Git di Cloud Manager | Archivio in cui sono memorizzati il codice e le impostazioni di configurazione dei clienti. |
| Provider cloud | AEM as a Cloud Service è in esecuzione su infrastrutture cloud pubbliche da più fornitori dietro le quinte (come Microsoft Azure o Amazon Web Services) per erogare il servizio in base allo SLA contrattuale. |
| Rete per la distribuzione di contenuti (CDN) | AEM as Cloud Service viene fornito con una rete CDN predefinita. Il suo scopo principale è ridurre la latenza distribuendo contenuti memorizzabili nella cache dai nodi della CDN al perimetro, vicino al browser. È completamente gestita e configurata per garantire prestazioni ottimali alle applicazioni AEM. |
| Archivio dei contenuti | Archivio in cui i contenuti vengono salvati in modo permanente. |
| Isolamento Enterprise | Funzione per cui ogni istanza di AEM as a Cloud Service è isolata dalle altre istanze. |
| Golden master | Livello di pubblicazione di AEM. |
| Motore di orchestrazione | Utilizzato in AEM as a Cloud Service per assicurarsi che tutti i servizi di authoring e pubblicazione vengano ridimensionati come e quando necessario. |
