---
title: Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2022.2.0
description: Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2022.2.0
feature: Release Information
source-git-commit: 8876702f1a172282fd1ff46387ade2a45e187fed
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 7%

---


# Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2022.2.0 {#release-notes}

Questa pagina illustra le note sulla versione per gli strumenti di migrazione AEM as a Cloud Service 2022.2.0.

## Analisi delle best practice {#bpa-release}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.24 è il 10 febbraio 2022.

### Novità {#what-is-new-bpa}

* Possibilità di rilevare e segnalare il numero di risorse con e senza tag avanzati.
* Possibilità di rilevare e creare rapporti sulla versione del componente core utilizzato.
* Possibilità di rilevare e creare rapporti sul tipo di livello di origine (Autore o Pubblicazione) in cui è stato eseguito BPA.

### Correzioni di bug {#bug-fixes-bpa}

* La logica di dimensionamento BPA è stata resa più rapida ed efficiente.
* In alcuni scenari, BPA non incrementa il conteggio analizzato al momento dell&#39;esecuzione. Questo problema è stato risolto.

## Strumento Content Transfer (Trasferimento contenuti)  {#ctt-release}

### Data di pubblicazione {#release-date-ctt}

La data di rilascio dello strumento Content Transfer (Trasferimento contenuti) v1.8.6 è il 3 febbraio 2022.

### Novità {#what-is-new-ctt}

* Convalida del contenuto : gli utenti possono determinare in modo affidabile se tutti i contenuti estratti dallo strumento Content Transfer (Trasferimento contenuti) sono stati correttamente acquisiti nell’istanza di destinazione. Per utilizzare questa funzione, è necessario abilitarla nella `System Console` dell&#39;ambiente AEM sorgente. Fai riferimento a [Convalida dei trasferimenti di contenuto - Guida introduttiva](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html?lang=en#getting-started) per ulteriori dettagli.

### Correzioni di bug {#bug-fixes-ctt}

* Alcuni utenti non sono stati mappati perché la mappatura utente faceva distinzione tra maiuscole e minuscole. Questo problema è stato risolto. La mappatura utente non fa più distinzione tra maiuscole e minuscole.

