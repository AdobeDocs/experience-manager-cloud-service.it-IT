---
title: Utilizzo di Edge Delivery Services con progetti AEM esistenti
description: Scopri come sfruttare i vantaggi di Edge Delivery Services sui tuoi progetti AEM esistenti
feature: Edge Delivery Services
exl-id: f54aac3a-1d0c-4be0-9aa6-616217e0e458
source-git-commit: eef58b59cd528743702e3d436acec02dbba58211
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 100%

---

# Utilizzo di Edge Delivery Services con progetti AEM esistenti {#existing-projects}

Non occorre aspettare che un nuovo progetto AEM usufruisca di Edge Delivery Services. Edge Delivery Services può essere integrato nel progetto AEM esistente in modo da sfruttare immediatamente i vantaggi in termini di prestazioni.

## Limitazioni per l’editor pagina di AEM {#page-editor}

Prima dell’avvento di Edge Delivery Services, il contenuto gestito in AEM veniva modificato mediante l’Editor pagina di AEM. Se il progetto è stato iniziato prima dell’introduzione di Edge Delivery Services, viene quasi certamente utilizzato l’Editor pagina.

L’Editor pagina di AEM funziona solo con [Componenti AEM](/help/implementing/developing/components/overview.md) come i [Componenti core.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) Questi componenti sono incompatibili con Edge Delivery Services. Per questo motivo, sono necessarie due fasi per introdurre Edge Delivery Services in un progetto AEM esistente:

* [Fase 1 - Sostituzione del front-end](#replace-front-end)
* [Fase 2 - Passare all’Editor universale](#switch-ue)

## Fase 1 - Sostituzione del front-end {#replace-front-end}

Nella fase uno, puoi continuare a utilizzare la struttura, i componenti e gli strumenti di authoring del sito AEM esistente. Il rendering del sito web verrà ricreato utilizzando i blocchi mediante JavaScript e CSS e verrà distribuito tramite Edge Delivery Services.

Consulta la [sezione Creare](/help/edge/developer/block-collection.md) della documentazione di Edge Delivery Services per ulteriori dettagli sui blocchi e su come svilupparli per Edge Delivery Services.

Sarà necessario un convertitore su App Builder per convertire l’output HTML sottoposto a rendering di AEM e inviarlo a Edge Delivery Services.

![Convertitore di contenuto nel flusso di pubblicazione](assets/content-converter.png)

La fase due completa il processo eliminando la sovrapposizione tecnologica: Componenti core di AEM con HTL e Java su authoring di AEM, Blocchi basati su JS su Edge Delivery e un convertitore basato su nodeJS.

## Fase 2 - Passare all’Editor universale {#switch-ue}

In questa fase, l’Editor pagina di AEM viene sostituito con l’Editor universale. Poiché l’Editor universale può funzionare direttamente con i blocchi, i componenti core e il convertitore AEM non saranno più necessari.

## Come iniziare {#how-to-get-started}

Per accedere a questa funzione, contatta il tuo rappresentante Adobe.
