---
title: Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2022.5.0
description: Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2022.5.0
feature: Release Information
source-git-commit: 48dd6b3184cdde06b902eae35fac42515f606e77
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 5%

---

# Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2022.5.0 {#release-notes}

Questa pagina illustra le note sulla versione per gli strumenti di migrazione in AEM as a Cloud Service 2022.5.0.

## Analisi delle best practice {#bpa-release}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.30 è il 1° giugno 2022.

### Novità {#what-is-new-bpa}

* Possibilità di rilevare e segnalare l’utilizzo di widget di dialogo personalizzati utilizzando i widget di dialogo CoralUI e Classic. Si consiglia di convertire i widget di dialogo Classic personalizzati da ExtJS a CoralUI. I widget della finestra di dialogo Coral personalizzati devono essere aggiornati a CoralUI3.
* Possibilità di rilevare e segnalare l’utilizzo e la versione di Assets Share Commons. Asset Share Commons 1.x non è supportato su AEM as a Cloud Service e deve essere aggiornato a 2.x.
* Possibilità di rilevare e segnalare il numero di nodi dalle versioni.
* Possibilità di rilevare e creare rapporti sugli agenti di replica personalizzati o sugli agenti di replica preconfigurati modificati.

### Correzioni di bug {#bug-fixes-bpa}

* BPA segnalava i risultati NCC (modifiche non compatibili), UMI (problema di configurazione errata dell’aggiornamento) e PCX (complessità pagina) che sono falsi positivi. Questi sono stati corretti.
* BPA segnalava errori quando una qualsiasi lunghezza del nome di nodo superava i 150 byte. È stato corretto per rilevare tali errori solo quando il percorso padre del nodo è uguale o superiore a 350 byte.

## Strumento Trasferimento contenuti {#ctt-release}

### Data di pubblicazione {#release-date-ctt}

La data di rilascio dello strumento Content Transfer v2.0.10 è il 2 giugno 2022.

### Novità {#what-is-new-ctt}

* Lo strumento Content Transfer (CTT) è stato sviluppato per lavorare con Cloud Acceleration Manager e semplificare l’intero processo di trasferimento dei contenuti. Il CTT ora si concentra sull’esecuzione di estrazioni di contenuto. Il servizio di acquisizione CTT è ora integrato in Cloud Acceleration Manager. I vantaggi offerti da questa evoluzione sono:
   * Modalità self-service per estrarre un set di migrazione una volta e trasferirlo in più ambienti in parallelo.
   * È stata migliorata l’esperienza dell’utente grazie a stati di caricamento migliori, protezioni e gestione degli errori.
   * I registri di acquisizione vengono mantenuti e sono sempre disponibili per la risoluzione dei problemi.

## Cloud Acceleration Manager {#cam-release}

### Data di pubblicazione {#release-date-cam}

La data di rilascio di Cloud Acceleration Manager è il 2 giugno 2022.

### Novità {#what-is-new-cam}

* Cloud Acceleration Manager ora consente agli utenti di avviare e gestire i trasferimenti di contenuto per spostare il contenuto dall’istanza AEM di un cliente (On-Premise o Adobe Managed Services) all’AEM as a Cloud Service come parte di un progetto di migrazione. Fai riferimento a [Utilizzo della scheda di trasferimento dei contenuti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-implementation-phase.html#content-transfer) per ulteriori dettagli.
