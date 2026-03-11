---
title: Risoluzione dei problemi relativi all’errore 502 nell’azione di invio personalizzata per Adaptive Forms
description: Scopri come identificare e risolvere 502 pagine di errore che si verificano quando si utilizzano azioni di invio personalizzate in Adaptive Forms (Componenti core). Questa guida spiega le cause comuni, ad esempio le eccezioni non gestite, e fornisce i passaggi di risoluzione.
feature: Adaptive Forms, Core Components
role: Developer
level: Intermediate
badgeSaas: label="AEM Forms" type="Positive" tooltip="Si applica ad AEM Forms)."
exl-id: a7469926-7059-4aca-90ff-2554d14c3944
source-git-commit: 89b0f2a8ca9d2f60365a5c3962b0b4e826f79b3e
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 2%

---

# Risoluzione dei problemi: pagina di errore 502 in Azione di invio personalizzata

Quando si utilizza Forms adattivo (Componenti core), è possibile che dopo l&#39;invio di un modulo che utilizza un&#39;azione di invio personalizzata venga visualizzata la pagina di errore **502 HTML**.

## Problema

**Errore:** quando un servizio Azione invio personalizzato non riesce, viene visualizzata una pagina di errore 502 HTML.

**Motivo:** questo problema si verifica se l&#39;azione di invio personalizzata genera un errore non gestito, ad esempio puntatore null, risposta API non valida o errore di runtime.

## Risoluzione

Per evitare la pagina di errore 502, racchiudi la logica di invio con blocchi try-catch per gestire correttamente gli errori.

Per i passaggi dettagliati, consulta [Creare un&#39;azione di invio personalizzata per Forms adattivo (Componenti core)](/help/forms/custom-submit-action-for-adaptive-forms-based-on-core-components.md).
