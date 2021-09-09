---
title: Sovrapposizioni per Adobe Experience Manager as a Cloud Service
description: AEM come Cloud Service utilizza il principio delle sovrapposizioni per estendere e personalizzare le console e altre funzionalità
exl-id: 24bdb1a9-6d77-43c7-a75e-28e6e0fd7608
source-git-commit: ac760e782f80ee82a9b0604ef64721405fc44ee4
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 2%

---

# Sovrapposizioni in AEM as a Cloud Service {#overlays-in-aem}

Adobe Experience Manager as a Cloud Service utilizza il principio delle sovrapposizioni per consentire di estendere e personalizzare le console e altre funzionalità (ad esempio, la creazione delle pagine).

La sovrapposizione è un termine che può essere utilizzato in molti contesti. In questo contesto (estensione di AEM come Cloud Service) una sovrapposizione significa prendere la funzionalità predefinita e imporre le proprie definizioni su di essa (per personalizzare la funzionalità standard).

In un&#39;istanza standard la funzionalità predefinita viene mantenuta in `/libs` ed è consigliabile definire la sovrapposizione (personalizzazioni) sotto il ramo `/apps` (utilizzando un [percorso di ricerca](#search-paths) per risolvere i problemi relativi alle risorse).

* L’interfaccia utente touch utilizza le sovrapposizioni relative a [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html):

   * Metodo

      * Ricostruire la struttura `/libs` appropriata in `/apps`.

         Questa operazione non richiede una copia 1:1, in quanto il [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) viene utilizzato per fare riferimento incrociato alle definizioni originali richieste. Sling Resource Merger fornisce servizi per l’accesso e l’unione delle risorse tramite meccanismi di differenziazione (differenze).

      * Apporta eventuali modifiche in `/apps`.
   * Vantaggi

      * Più resistente alle modifiche in `/libs`.
      * Ridefinisci solo ciò che è effettivamente richiesto.


>[!CAUTION]
>
>I metodi [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) e i metodi correlati possono essere utilizzati solo con [Granite](https://www.adobe.io/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html). Ciò significa che la creazione di una sovrapposizione con una struttura dell’ossatura è appropriata solo per l’interfaccia utente standard abilitata per il tocco.

Le sovrapposizioni sono il metodo consigliato per molte modifiche, ad esempio per configurare le console o creare la categoria di selezione nel browser delle risorse nel pannello laterale (utilizzato per la creazione di pagine). Sono richiesti come:

* ***non deve* apportare modifiche al ramo `/libs`**Eventuali modifiche apportate potrebbero andare perse, in quanto questo ramo è soggetto a modifiche ogni volta che gli aggiornamenti vengono applicati all&#39;istanza.

* Concentrano le modifiche in un&#39;unica posizione; semplificando il monitoraggio, la migrazione, il backup e/o il debug delle modifiche, a seconda delle necessità.

## Percorsi di ricerca {#search-paths}

AEM utilizza un percorso di ricerca per trovare una risorsa, cercando (per impostazione predefinita) prima il ramo `/apps` e poi il ramo `/libs`. Questo meccanismo significa che la sovrapposizione in `/apps` (e le personalizzazioni ivi definite) avrà priorità.

Per le sovrapposizioni la risorsa consegnata è un aggregato delle risorse e delle proprietà recuperate, a seconda dei percorsi di ricerca definiti nella configurazione OSGi.
