---
title: Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2022.2.0
description: Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2022.2.0
feature: Release Information
exl-id: b1cd871d-c71e-4902-a97e-2c859f6a4da4
source-git-commit: c497424271ea960d22a30b4a6c66432935ec820d
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 79%

---

# Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2022.2.0 {#release-notes}

Questa pagina illustra le note sulla versione per gli strumenti di migrazione AEM as a Cloud Service 2022.2.0.

## Analisi delle best practice {#bpa-release}

### Data di pubblicazione {#release-date-bpa}

La data di pubblicazione di Best Practices Analyzer v2.1.24 è il 1° febbraio 2022.

### Novità {#what-is-new-bpa}

* Possibilità di rilevare e segnalare il numero di risorse con e senza tag avanzati.
* Possibilità di rilevare e segnalare la versione di Componenti core comunemente utilizzata.
* Possibilità di rilevare e creare rapporti sul tipo di livello di origine (Autore o Pubblicazione) in cui è stato eseguito BPA.

### Correzioni di bug {#bug-fixes-bpa}

* La logica di dimensionamento BPA è stata resa più rapida ed efficiente.
* In alcuni scenari, BPA non incrementava il conteggio analizzato al momento dell’esecuzione. Questo problema è stato risolto.

## Strumento Trasferimento contenuti {#ctt-release}

### Data di pubblicazione {#release-date-ctt}

La data di pubblicazione dello strumento Trasferimento contenuti v1.8.6 è il 3 febbraio 2022.

### Novità {#what-is-new-ctt}

* Convalida del contenuto: gli utenti possono determinare in modo affidabile se tutti i contenuti estratti dallo strumento Trasferimento contenuti sono stati correttamente acquisiti nell’istanza di destinazione. Per utilizzare questa funzione, è necessario abilitarla nella `System Console` dell’ambiente AEM sorgente. Fai riferimento a [Guida introduttiva alla convalida dei trasferimenti di contenuto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html?lang=it#getting-started) per ulteriori dettagli.

### Correzioni di bug {#bug-fixes-ctt}

* Alcuni utenti non venivano mappati perché la mappatura utente faceva distinzione tra maiuscole e minuscole. Questo problema è stato risolto. La mappatura utente non fa più distinzione tra maiuscole e minuscole.
