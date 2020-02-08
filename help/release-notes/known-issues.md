---
title: Problemi noti
description: Note sulla versione specifiche dei problemi noti con Adobe Experience Manager come servizio Cloud
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# Problemi noti {#known-issues}

In questo articolo sono elencati i problemi noti di Adobe Experience Manager come offerta di servizi cloud. L&#39;elenco viene aggiornato e aggiornato con ogni versione continua di Experience Manager.

[Per ulteriori informazioni sui problemi noti, contattate il supporto](https://helpx.adobe.com/support/experience-manager.html) .

<!-- 
## Platform {#platform}

## Sites {#sites}
-->

## Assets {#assets}

<!-- Jira label: assets-cloud-known-issues -->

Alcuni problemi noti sono:

* **Schema** metadati: Il widget di valutazione delle risorse può causare un errore di compilazione JSP. Una soluzione consiste nel rimuovere il componente di valutazione delle risorse dallo schema di metadati. <!-- CQ-4282865 -->

Alcune limitazioni della funzionalità Risorse sono:

* Con Risorse AEM come servizio cloud, la funzionalità Risorse collegate funziona quando AEM 6.5 Sites viene implementato su AMS.

### Prossime funzionalità di Assets {#upcoming-assets-capabilities}

Alcune funzionalità di Risorse Adobe Experience Manager che dipendono dalle funzionalità di base, che non sono ancora disponibili in Experience Manager come architettura di distribuzione del servizio Cloud, devono essere abilitate in una fase successiva:

* Al momento la pubblicazione in Brand Portal non è abilitata. Potete estendere e implementare l’implementazione di [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) per i casi di utilizzo della distribuzione delle risorse.
* Al momento non è disponibile una funzionalità avanzata per l&#39;assegnazione di tag avanzati che sfrutta i servizi AI di I/O Adobe.
* Funzionalità non abilitate in questa fase a causa della dipendenza dalle API Commerce Integration Framework:
   * Modelli di flusso di lavoro per fotografie.
   * La scheda Informazioni prodotto nell’interfaccia utente delle proprietà della risorsa non è popolata.
* Funzionalità non abilitate in questa fase a causa della dipendenza dall&#39;integrazione di InDesign Server:
   * Modelli di risorse e cataloghi di risorse.
   * Anteprima di più pagine di file InDesign.

>[!MORELIKETHIS]
>
>* [Modifiche principali in AEM](aem-cloud-changes.md)
>* [Funzioni obsolete e rimosse](deprecated-removed-features.md)
>* [Note sulla versione](home.md)

