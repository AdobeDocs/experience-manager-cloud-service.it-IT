---
title: Problemi noti
description: Note sulla versione specifiche per i problemi noti relativi ad Adobe Experience Manager as a Cloud Service
translation-type: ht
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# Problemi noti {#known-issues}

In questo articolo sono elencati i problemi noti relativi all’offerta Adobe Experience Manager as a Cloud Service. L’elenco viene rivisto e aggiornato a ogni versione di Experience Manager.

Per ulteriori informazioni sui problemi noti, [contatta il supporto](https://helpx.adobe.com/it/support/experience-manager.html).

<!-- 
## Platform {#platform}

## Sites {#sites}
-->

## Assets {#assets}

<!-- Jira label: assets-cloud-known-issues -->

Alcuni problemi noti sono:

* **Schema metadati**: il widget di valutazione delle risorse può causare un errore di compilazione JSP. Una soluzione consiste nel rimuovere il componente di valutazione delle risorse dallo schema metadati. <!-- CQ-4282865 -->

Alcune limitazioni della funzionalità Assets sono:

* Con AEM Assets as a Cloud Service, la funzionalità Risorse collegate viene eseguita quando AEM 6.5 Sites viene implementato in AMS.

### Funzionalità di Assets disponibili in futuro {#upcoming-assets-capabilities}

In futuro verranno attivate alcune funzionalità di Adobe Experience Manager Assets che dipendono dalle funzionalità di base e che non sono ancora disponibili nell’architettura di distribuzione di Experience Manager as a Cloud Service:

* Al momento la pubblicazione in Brand Portal non è abilitata. Puoi estendere e distribuire l’implementazione di [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) per i casi d’uso relativi alla distribuzione delle risorse.
* Al momento non è disponibile una versione migliorata della funzionalità per l’assegnazione di tag avanzati che sfrutta i servizi di intelligenza artificiale di Adobe I/O.
* Funzionalità non attivate in questa fase a causa della dipendenza da API di Commerce Integration Framework:
   * Modelli di flusso di lavoro per servizio fotografico.
   * La scheda Informazioni prodotto nell’interfaccia delle proprietà della risorsa non è compilata.
* Funzionalità non attivate in questa fase a causa della dipendenza dall’integrazione di InDesign Server:
   * Modelli di risorse e cataloghi di risorse.
   * Anteprima multipagina di file InDesign.

>[!MORELIKETHIS]
>
>* [Modifiche principali apportate in AEM](aem-cloud-changes.md)
>* [Funzioni obsolete e rimosse](deprecated-removed-features.md)
>* [Note sulla versione](home.md)

