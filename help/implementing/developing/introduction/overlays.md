---
title: Sovrapposizioni per Adobe Experience Manager come Cloud Service
description: AEM come Cloud Service utilizza il principio delle sovrapposizioni per estendere e personalizzare le console e altre funzionalità
translation-type: tm+mt
source-git-commit: 8028682f19ba6ba7db6b60a2e5e5f5843f7ac11f
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 2%

---


# Sovrapposizioni in AEM as a Cloud Service {#overlays-in-aem}

Adobe Experience Manager come Cloud Service utilizza il principio delle sovrapposizioni per estendere e personalizzare le console e altre funzionalità (ad esempio, l’authoring delle pagine).

<!--
Adobe Experience Manager as a Cloud Service uses the principle of overlays to allow you to extend and customize the [consoles](/help/sites-developing/customizing-consoles-touch.md) and other functionality (for example, [page authoring](/help/sites-developing/customizing-page-authoring-touch.md)).
-->

Sovrapposizione è un termine che può essere utilizzato in molti contesti. In questo contesto (estendendo AEM come Cloud Service) una sovrapposizione significa prendere la funzionalità predefinita e imporre le proprie definizioni su di essa (per personalizzare la funzionalità standard).

In un&#39;istanza standard la funzionalità predefinita è mantenuta in `/libs` ed è consigliabile definire la sovrapposizione (personalizzazioni) sotto il ramo `/apps` (utilizzando un percorso di ricerca [](#search-paths) per risolvere le risorse).

* L&#39;interfaccia touch utilizza le sovrapposizioni relative a [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html):

   * Metodo

      * Ricostruire la struttura `/libs` appropriata in `/apps`.

         Questa operazione non richiede una copia 1:1, in quanto la [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) viene utilizzata per fare riferimento incrociato alle definizioni originali richieste. Sling Resource Merger fornisce servizi per l&#39;accesso e l&#39;unione delle risorse mediante meccanismi diversi (differenziazione).

      * Apportate eventuali modifiche in `/apps`.
   * Vantaggi

      * Più robusto alle modifiche in `/libs`.
      * Ridefinisci solo ciò che è effettivamente richiesto.


<!-- Still links to reference material in 6.5 -->

>[!CAUTION]
>
>La [Fusione risorse Sling](/help/implementing/developing/introduction/sling-resource-merger.md) e i metodi correlati possono essere utilizzati solo con [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). Ciò significa che la creazione di una sovrapposizione con una struttura di ossatura è appropriata solo per l’interfaccia touch standard.

Le sovrapposizioni sono il metodo consigliato per molte modifiche, ad esempio per configurare le console o creare la categoria di selezione nel browser delle risorse nel pannello laterale (utilizzato per l’authoring delle pagine). Sono richiesti come:

<!--
Overlays are the recommended method for many changes, such as [configuring your consoles](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) or [creating your selection category to the asset browser in the side panel](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) (used when authoring pages). They are required as:
-->

* ***non è necessario* apportare modifiche al ramo `/libs`**Eventuali modifiche apportate potrebbero andare perse, in quanto questo ramo potrebbe subire modifiche ogni volta che gli aggiornamenti vengono applicati all&#39;istanza.

* Consentono di concentrare le modifiche in un&#39;unica posizione; facilitando il monitoraggio, la migrazione, il backup e/o il debug delle modifiche, se necessario.

## Percorsi di ricerca {#search-paths}

AEM utilizza un percorso di ricerca per trovare una risorsa, cercando (per impostazione predefinita) prima il ramo `/apps`, quindi il ramo `/libs`. Questo meccanismo significa che la sovrapposizione in `/apps` (e le personalizzazioni ivi definite) avrà priorità.

Per le sovrapposizioni, la risorsa consegnata è un insieme di risorse e proprietà recuperate, a seconda dei percorsi di ricerca definiti nella configurazione OSGi.

<!--
## Example of Usage {#example-of-usage}

Some examples are covered when:

* [Customizing the Consoles](/help/sites-developing/customizing-consoles-touch.md)
* [Customizing Page Authoring](/help/sites-developing/customizing-page-authoring-touch.md)
-->