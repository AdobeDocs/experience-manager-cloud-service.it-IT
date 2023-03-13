---
title: Note sulla versione 2022.5.0 degli strumenti di migrazione in AEM as a Cloud Service
description: Note sulla versione 2022.5.0 degli strumenti di migrazione in AEM as a Cloud Service
feature: Release Information
exl-id: 1aa49e85-1914-44d9-bcf7-0a1b03926df0
source-git-commit: 01c4a21b980918ba99ac174419d80b577bc96dda
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 15%

---

# Note sulla versione 2022.5.0 degli strumenti di migrazione in AEM as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2022.5.0 degli strumenti di migrazione in AEM as a Cloud Service.

## Analisi delle best practice {#bpa-release}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.30 è il 1° giugno 2022.

### Novità {#what-is-new-bpa}

* Possibilità di rilevare e segnalare l’utilizzo di widget per finestre di dialogo personalizzati utilizzando i widget per finestre di dialogo CoralUI e Classic. Si consiglia di convertire i widget per finestre di dialogo classici personalizzati da ExtJS a CoralUI. I widget per finestre di dialogo Coral personalizzati devono essere aggiornati a CoralUI3.
* Possibilità di rilevare e segnalare l’utilizzo e la versione di Assets Share Commons. Asset Share Commons 1.x non è supportato in AEM as a Cloud Service e deve essere aggiornato a 2.x.
* Possibilità di rilevare e segnalare il numero di nodi dalle versioni.
* Possibilità di rilevare e segnalare gli agenti di replica personalizzati o gli agenti di replica predefiniti che sono stati modificati.

### Correzioni di bug {#bug-fixes-bpa}

* BPA segnalava i risultati NCC (Non-compatible changes), UMI (Upgrade Misconfiguration Issue) e PCX (Page Complexity) falsi positivi. Questi sono stati corretti.
* BPA segnalava errori quando la lunghezza di un nome di nodo superava i 150 byte. Questo problema è stato risolto per rilevare tali errori solo quando il percorso del nodo principale è uguale o superiore a 350 byte.

## Strumento Trasferimento contenuti {#ctt-release}

### Data di pubblicazione {#release-date-ctt}

La data di pubblicazione dello strumento Content Transfer v2.0.10 è il 2 giugno 2022.

### Novità {#what-is-new-ctt}

* Lo strumento Content Transfer (CTT) è stato evoluto per funzionare con Cloud Acceleration Manager e semplificare l’intero processo di trasferimento dei contenuti. CTT ora si concentra sull’esecuzione di estrazioni di contenuto. Il servizio di acquisizione CTT è ora integrato in Cloud Acceleration Manager. I vantaggi offerti da questa evoluzione sono:
   * Modalità self-service per estrarre un set di migrazione in una sola volta e trasferirlo in più ambienti in parallelo.
   * Miglioramento dell’esperienza utente grazie a stati di caricamento, guardrail e gestione degli errori più efficienti.
   * I registri di acquisizione vengono mantenuti e sono sempre disponibili per la risoluzione dei problemi.

## Cloud Acceleration Manager {#cam-release}

### Data di pubblicazione {#release-date-cam}

La data di pubblicazione di Cloud Acceleration Manager è il 2 giugno 2022.

### Novità {#what-is-new-cam}

* Cloud Acceleration Manager ora consente agli utenti di avviare e gestire trasferimenti di contenuti per spostare i contenuti dall’istanza AEM di un cliente (On-Premise o Adobe Managed Services) all’AEM as a Cloud Service come parte di un progetto di migrazione. Fai riferimento a [Utilizzo della scheda Content Transfer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-implementation-phase.html#content-transfer) per ulteriori dettagli.
