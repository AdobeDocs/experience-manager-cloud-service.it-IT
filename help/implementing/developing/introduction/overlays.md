---
title: Sovrapposizioni per Adobe Experience Manager as a Cloud Service
description: AEM as a Cloud Service utilizza il principio delle sovrapposizioni per estendere e personalizzare le console e altre funzionalità
exl-id: 24bdb1a9-6d77-43c7-a75e-28e6e0fd7608
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 2%

---

# Sovrapposizioni in AEM as a Cloud Service {#overlays-in-aem}

Adobe Experience Manager as a Cloud Service utilizza il principio delle sovrapposizioni per estendere e personalizzare le console e altre funzionalità (ad esempio, l’authoring delle pagine).

Sovrapposizione è un termine che può essere utilizzato in molti contesti. In questo contesto, estendere AEM as a Cloud Service significa sovrapporsi alle funzionalità predefinite e imporre le tue definizioni su di esse per personalizzare la funzionalità standard.

In un&#39;istanza standard, la funzionalità predefinita si trova in `/libs` e si consiglia di definire la sovrapposizione (personalizzazioni) nel ramo `/apps` (utilizzando un [percorso di ricerca](#search-paths) per risolvere le risorse).

* L&#39;interfaccia utente touch utilizza le sovrapposizioni relative a [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html):

   * Metodo

      * Ricostruire la struttura `/libs` appropriata in `/apps`.

        Questa ristrutturazione non richiede una copia 1:1 perché [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) viene utilizzato per fare un riferimento incrociato alle definizioni originali richieste. Sling Resource Merger fornisce servizi per l’accesso e l’unione di risorse con meccanismi di differenze.

      * In `/apps`, apportare le modifiche.

   * Vantaggi

      * Più affidabile per le modifiche in `/libs`.
      * Ridefinisci solo ciò che è richiesto.

>[!CAUTION]
>
>[Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) e i metodi correlati possono essere utilizzati solo con [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html). Questa regola significa che la creazione di una sovrapposizione con una struttura di ossatura è appropriata solo per l&#39;interfaccia utente standard touch.

Le sovrapposizioni sono il metodo consigliato per molte modifiche. Ad esempio, puoi configurare le console o creare la categoria di selezione nel browser Risorse nel pannello laterale (utilizzato per la creazione delle pagine). Sono necessari in quanto:

* **Nel ramo `/libs`, *non apportare modifiche***
Qualsiasi modifica apportata potrebbe andare persa, poiché questo ramo potrebbe subire modifiche ogni volta che vengono applicati aggiornamenti all’istanza.

* Concentrano le modifiche in un&#39;unica posizione, semplificando il monitoraggio, la migrazione, il backup o il debug delle modifiche in base alle esigenze.

## Percorsi di ricerca {#search-paths}

AEM utilizza un percorso di ricerca per trovare una risorsa, eseguendo prima la ricerca, per impostazione predefinita, nel ramo `/apps` e quindi nel ramo `/libs`. Questo meccanismo indica che la sovrapposizione in `/apps` (e le personalizzazioni ivi definite) ha la priorità.

Per le sovrapposizioni, la risorsa distribuita è un aggregato delle risorse e delle proprietà recuperate, a seconda dei percorsi di ricerca definiti nella configurazione OSGi.
