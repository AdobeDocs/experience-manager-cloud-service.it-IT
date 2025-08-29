---
title: Risoluzione dei problemi relativi all’errore 502 nell’azione di invio personalizzata per Adaptive Forms
description: Scopri come identificare e risolvere 502 pagine di errore che si verificano quando si utilizzano azioni di invio personalizzate in Adaptive Forms (Componenti core). Questa guida spiega le cause comuni, ad esempio le eccezioni non gestite, e fornisce i passaggi di risoluzione.
feature: Adaptive Forms, Core Components
role: Developer
level: Intermediate
source-git-commit: 03e46bb43e684a6b7057045cf298f40f9f1fe622
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 1%

---


# Risoluzione dei problemi: pagina di errore 502 in Azione di invio personalizzata

Quando si utilizza Forms adattivo (Componenti core), è possibile che dopo l&#39;invio di un modulo che utilizza un&#39;azione di invio personalizzata venga visualizzata la pagina di errore **502 HTML**.

## Problema

**Errore:** quando un servizio Azione invio personalizzato non riesce, viene visualizzata una pagina di errore 502 HTML.

**Motivo:** questo problema si verifica se l&#39;azione di invio personalizzata genera un errore non gestito, ad esempio puntatore null, risposta API non valida o errore di runtime.

## Risoluzione

Per evitare la pagina di errore 502, racchiudi la logica di invio con blocchi try-catch per gestire correttamente gli errori.

Per i passaggi dettagliati, consulta [Creare un&#39;azione di invio personalizzata per Forms adattivo (Componenti core)](/help/forms/custom-submit-action-for-adaptive-forms-based-on-core-components.md).
