---
title: Sovrapposizioni per  Adobe Experience Manager come Cloud Service
description: AEM come Cloud Service utilizza il principio delle sovrapposizioni per estendere e personalizzare le console e altre funzionalità
translation-type: tm+mt
source-git-commit: e9fa89753289563edd59e3d75413c90efe3ff0b2
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---


# Overlays in AEM as a Cloud Service {#overlays-in-aem}

 Adobe Experience Manager come Cloud Service utilizza il principio delle sovrapposizioni per estendere e personalizzare le console e altre funzionalità (ad esempio, l’authoring delle pagine).

<!--
Adobe Experience Manager as a Cloud Service uses the principle of overlays to allow you to extend and customize the [consoles](/help/sites-developing/customizing-consoles-touch.md) and other functionality (for example, [page authoring](/help/sites-developing/customizing-page-authoring-touch.md)).
-->

Sovrapposizione è un termine che può essere utilizzato in molti contesti. In questo contesto (estensione di AEM come Cloud Service) una sovrapposizione implica l’uso della funzionalità predefinita e l’imposizione di definizioni personalizzate su di essa (per personalizzare la funzionalità standard).

In un’istanza standard la funzionalità predefinita è mantenuta in `/libs` ed è consigliabile definire la sovrapposizione (personalizzazioni) sotto il `/apps` ramo. AEM usa un percorso di ricerca per trovare una risorsa, eseguendo prima la ricerca nel `/apps` ramo e poi nel `/libs` ramo (il percorso di [ricerca può essere configurato](#configuring-the-search-paths)). Questo meccanismo significa che la sovrapposizione (e le personalizzazioni qui definite) avranno priorità.

* L’interfaccia touch utilizza sovrapposizioni [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html):

   * Metodo

      * Ricostruire la struttura appropriata sotto `/libs` `/apps`.

         Questa operazione non richiede una copia 1:1. La fusione [delle risorse](/help/implementing/developing/introduction/sling-resource-merger.md) Sling viene utilizzata per fare riferimento incrociato alle definizioni originali richieste. Sling Resource Merger fornisce servizi per l&#39;accesso e l&#39;unione delle risorse mediante meccanismi diversi (differenziazione).

      * Apportate eventuali modifiche in `/apps`.
   * Vantaggi

      * Più robusto ai cambiamenti in `/libs`.
      * Ridefinisci solo ciò che è effettivamente richiesto.


<!-- Still links to reference material in 6.5 -->

>[!CAUTION]
>
>La fusione [di risorse](/help/implementing/developing/introduction/sling-resource-merger.md) Sling e i metodi correlati possono essere utilizzati solo con [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). Ciò significa che la creazione di una sovrapposizione con una struttura di ossatura è appropriata solo per l’interfaccia touch standard.

Le sovrapposizioni sono il metodo consigliato per molte modifiche, ad esempio per configurare le console o creare la categoria di selezione nel browser delle risorse nel pannello laterale (utilizzato per l’authoring delle pagine). Sono richiesti come:

<!--
Overlays are the recommended method for many changes, such as [configuring your consoles](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) or [creating your selection category to the asset browser in the side panel](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) (used when authoring pages). They are required as:
-->

* Non ***è necessario *apportare modifiche al`/libs`ramo **Eventuali modifiche apportate potrebbero andare perdute, in quanto questo ramo può subire modifiche ogni volta che:

   * aggiornare l&#39;istanza
   * applica un hotfix
   * installare un pacchetto di funzioni

* Consentono di concentrare le modifiche in un&#39;unica posizione; facilitando il monitoraggio, la migrazione, il backup e/o il debug delle modifiche, a seconda delle necessità.

## Configurazione dei percorsi di ricerca {#configuring-the-search-paths}

Per le sovrapposizioni, la risorsa consegnata è un insieme di risorse e proprietà recuperate, a seconda dei percorsi di ricerca che è possibile definire:

* Il percorso **di ricerca di Resource** Resolver come definito nella configurazione [](/help/implementing/deploying/configuring-osgi.md) OSGi per **Apache Sling Resource Resolver Factory**.

   * L&#39;ordine superiore dei percorsi di ricerca indica le rispettive priorità.
   * In un’installazione standard le impostazioni predefinite principali sono `/apps`, `/libs` pertanto il contenuto di `/apps` ha una priorità maggiore di quella di `/libs` (ovvero *sovrappone* ).

* Due utenti di servizi necessitano dell&#39;accesso JCR:READ alla posizione in cui sono memorizzati gli script. Tali utenti sono: components-search-service (utilizzato dai com.day.cq.wcm.coreto access/cache components) e sling-scripting (utilizzato da org.apache.sling.servlets.resolver per trovare servlet).
* È inoltre necessario configurare la seguente configurazione in base al punto in cui vengono inseriti gli script (in questo esempio in /etc, /libs o /apps).

   ```
   PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
   resource.resolver.searchpath=["/etc","/apps","/libs"]
   resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
   ```

* Infine, deve essere configurato anche Servlet Resolver (in questo esempio per aggiungere anche /etc)

   ```
   PID = org.apache.sling.servlets.resolver.SlingServletResolver
   servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
   ```

<!--
## Example of Usage {#example-of-usage}

Some examples are covered when:

* [Customizing the Consoles](/help/sites-developing/customizing-consoles-touch.md)
* [Customizing Page Authoring](/help/sites-developing/customizing-page-authoring-touch.md)
-->