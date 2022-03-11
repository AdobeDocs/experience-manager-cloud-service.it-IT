---
title: Sovrapposizioni per Adobe Experience Manager as a Cloud Service
description: AEM as a Cloud Service utilizza il principio delle sovrapposizioni per estendere e personalizzare le console e altre funzionalità
exl-id: 24bdb1a9-6d77-43c7-a75e-28e6e0fd7608
source-git-commit: ac760e782f80ee82a9b0604ef64721405fc44ee4
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 2%

---

# Sovrapposizioni in AEM as a Cloud Service {#overlays-in-aem}

Adobe Experience Manager as a Cloud Service utilizza il principio delle sovrapposizioni per estendere e personalizzare le console e altre funzionalità (ad esempio, la creazione delle pagine).

La sovrapposizione è un termine che può essere utilizzato in molti contesti. In questo contesto (estensione AEM as a Cloud Service) una sovrapposizione implica l’utilizzo delle funzionalità predefinite e l’imposizione di definizioni personalizzate su di esse (per personalizzare la funzionalità standard).

In un&#39;istanza standard, la funzionalità predefinita è mantenuta in `/libs` e si consiglia di definire la sovrapposizione (personalizzazioni) in `/apps` (utilizzando un [percorso di ricerca](#search-paths) per risolvere le risorse).

* L’interfaccia touch utilizza [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)Sovrapposizioni relative a:

   * Metodo

      * Ricostruire l&#39;appropriato `/libs` struttura `/apps`.

         Questa operazione non richiede una copia 1:1, in quanto [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) viene utilizzato per fare riferimento incrociato alle definizioni originali richieste. Sling Resource Merger fornisce servizi per l’accesso e l’unione delle risorse tramite meccanismi di differenziazione (differenze).

      * Apporta le modifiche in `/apps`.
   * Vantaggi

      * Più robusto per le modifiche in `/libs`.
      * Ridefinisci solo ciò che è effettivamente richiesto.


>[!CAUTION]
>
>La [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) e i relativi metodi possono essere utilizzati solo con [Granite](https://www.adobe.io/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html). Ciò significa che la creazione di una sovrapposizione con una struttura dell’ossatura è appropriata solo per l’interfaccia utente standard abilitata per il tocco.

Le sovrapposizioni sono il metodo consigliato per molte modifiche, ad esempio per configurare le console o creare la categoria di selezione nel browser delle risorse nel pannello laterale (utilizzato per la creazione di pagine). Sono richiesti come:

* You ***non deve* apporta modifiche nel `/libs` filiale **Eventuali modifiche apportate potrebbero andare perse, in quanto questo ramo è soggetto a modifiche ogni volta che gli aggiornamenti vengono applicati all&#39;istanza.

* Concentrano le modifiche in un&#39;unica posizione; semplificando il monitoraggio, la migrazione, il backup e/o il debug delle modifiche, a seconda delle necessità.

## Percorsi di ricerca {#search-paths}

AEM utilizza un percorso di ricerca per trovare una risorsa, cercando (per impostazione predefinita) prima il `/apps` e quindi `/libs` ramo. Questo meccanismo significa che la sovrapposizione `/apps` (e le personalizzazioni qui definite) avranno priorità.

Per le sovrapposizioni la risorsa consegnata è un aggregato delle risorse e delle proprietà recuperate, a seconda dei percorsi di ricerca definiti nella configurazione OSGi.
