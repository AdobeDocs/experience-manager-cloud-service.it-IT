---
title: Note sulla versione 2024.09 degli strumenti di migrazione in AEM as a Cloud Service
description: Note sulla versione 2024.09.0 degli strumenti di migrazione in AEM as a Cloud Service
feature: Release Information
exl-id: 52709511-eab2-47a7-8bea-1b707cd568a1
role: Admin
source-git-commit: 0c16f264826a46907afc33c91a021e7696f5b7a8
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 7%

---

# Note sulla versione 2024.09.0 degli strumenti di migrazione in AEM as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione degli strumenti di migrazione in AEM as a Cloud Service 2024.09.0.

## Strumento Trasferimento contenuti {#ctt-release}

### Data di pubblicazione {#release-date-ctt}

La data di pubblicazione dello strumento Content Transfer v3.0.20 è il 28 agosto 2024.

### Novità {#what-is-new-ctt}

* Gli utenti non verranno più acquisiti con questa versione e per questo motivo è stata rimossa la funzionalità facoltativa Mappatura utente.
* È stata aggiunta l’opzione di configurazione OSGI per disabilitare o abilitare la migrazione delle entità durante l’estrazione e l’acquisizione (l’impostazione predefinita è abilitarla)

### Correzioni di bug {#bug-fixes-ctt}

* CTT è stato migliorato per evitare un errore durante la rimozione della protezione di una chiave segreta nella configurazione di azcopy
* CTT ora gestisce correttamente qualsiasi errore durante la copia dei registri AzCopy nella fase di convalida
* Cambia directory di registro azcopy creata durante il processo di estrazione

## Analisi delle best practice {#bpa-release}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.52 è il 4 settembre 2024

### Novità {#what-is-new-bpa}

* È stato introdotto un nuovo modello per rilevare eventi basati su JCR nell’AEM

### Correzioni di bug {#bug-fixes-bpa}

* Sono stati corretti falsi positivi
* Maggiore robustezza per gestire le risposte reindirizzate dal dispatcher
* È stata corretta la mancata segnalazione dei risultati NCC per tutte le lingue in /apps/wcm/core/resources/language/
* è stato aggiunto un controllo per rilevare se una proprietà multipla di un nodo non ha valori

