---
title: Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2022.3.0
description: Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2022.3.0
feature: Release Information
source-git-commit: c497424271ea960d22a30b4a6c66432935ec820d
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 7%

---


# Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2022.3.0 {#release-notes}

Questa pagina illustra le note sulla versione per gli strumenti di migrazione AEM as a Cloud Service 2022.3.0.

## Analisi delle best practice {#bpa-release}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.26 è il 16 marzo 2022.

### Novità {#what-is-new-bpa}

* Possibilità di rilevare le risorse non elaborate. Se vengono rilevate risorse non elaborate, queste risorse devono essere impostate su elaborate o devono essere rimosse dal set di migrazione durante il trasferimento del contenuto per evitare problemi durante l’assimilazione del contenuto.
* Possibilità di rilevare se il contenuto ha più di 1000 URL personalizzati. L’utilizzo di un numero elevato di URL personalizzati non è una best practice in quanto carica un carico sui server Dispatcher e Publish .
* Possibilità di identificare i problemi relativi alle definizioni degli indici Oak e di rilevare le incompatibilità con AEM as a Cloud Service.
* Possibilità di rilevare e creare rapporti sull’utilizzo delle configurazioni di Externalizer. In AEM configurazioni as a Cloud Service di Externalizer sono impostate da Cloud Manager, pertanto le configurazioni esistenti di Externalizer devono essere reimpostate per mantenere la compatibilità.

### Correzioni di bug {#bug-fixes-bpa}

* In alcuni scenari, l&#39;esecuzione di BPA non è riuscita a causa di un errore di asserzione generato da FormsSelectiveFeaturesAnalysis. Questo problema è stato risolto.
* BPA riferiva i risultati relativi al modello WRK come PRINCIPALE invece che CRITICO. Questo problema è stato risolto.
* BPA segnalava erroneamente i risultati relativi alle definizioni dell&#39;indice OAK in ui.apps come CRITICAL. Questo problema è stato risolto.

## Strumento Trasferimento contenuti {#ctt-release}

### Data di pubblicazione {#release-date-ctt}

La data di rilascio dello strumento Content Transfer (Trasferimento contenuti) v1.9.0 è il 28 febbraio 2022.

### Novità {#what-is-new-ctt}

* Controlla le dimensioni delle protezioni : la funzione di controllo dello strumento di trasferimento dei contenuti consente di ridurre i trasferimenti di contenuto non riusciti.  Con la funzione di controllo dimensioni, gli utenti possono 1) determinare se hanno spazio su disco sufficiente nel `crx-quickstart` sottodirectory prima dell’estrazione e 2) stimare le dimensioni del set di migrazione e verificare se è supportato. Se uno o entrambi questi controlli vengono violati, gli utenti visualizzeranno gli avvisi nell’interfaccia utente del CTT. Con questa soluzione puoi evitare errori di trasferimento dei contenuti e discutere in modo proattivo le opzioni di migrazione con l’Assistenza clienti di Adobe. Fai riferimento a [Determinazione delle dimensioni del set di migrazione e dello spazio su disco](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en#migration-set-size) per ulteriori dettagli.