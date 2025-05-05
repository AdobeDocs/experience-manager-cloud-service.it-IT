---
title: Note sulla versione 2022.3.0 degli strumenti di migrazione in AEM as a Cloud Service
description: Note sulla versione 2022.3.0 degli strumenti di migrazione in AEM as a Cloud Service
feature: Release Information
exl-id: ab43605d-d46e-43de-b71f-fab610609550
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 34%

---

# Note sulla versione 2022.3.0 degli strumenti di migrazione in AEM as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione degli strumenti di migrazione in AEM as a Cloud Service 2022.3.0.

## Analisi delle best practice {#bpa-release}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.26 è il 16 marzo 2022.

### Novità {#what-is-new-bpa}

* Possibilità di rilevare le risorse non elaborate. Se vengono rilevate risorse non elaborate, queste devono essere impostate su elaborate o rimosse dal set di migrazione durante il trasferimento del contenuto per evitare problemi durante l’acquisizione del contenuto.
* Possibilità di rilevare se il contenuto ha più di 1000 URL personalizzati. L’utilizzo di un numero elevato di URL personalizzati non è consigliato in quanto sovraccarica i server Dispatcher e Publish.
* Possibilità di identificare i problemi relativi alle definizioni degli indici Oak e di rilevare le incompatibilità con AEM as a Cloud Service.
* Possibilità di rilevare e creare rapporti sull’utilizzo delle configurazioni di Externalizer. In AEM as a Cloud Service Externalizer, le configurazioni sono impostate da Cloud Manager. Pertanto, le configurazioni esistenti di Externalizer devono essere reimpostate per mantenere la compatibilità.

### Correzioni di bug {#bug-fixes-bpa}

* In alcuni scenari, l’esecuzione di BPA non è riuscita a causa di un errore di asserzione generato da FormsSelectiveFeaturesAnalysis.
* BPA riportava i risultati relativi al modello WRK come PRINCIPALE invece di CRITICO.
* BPA riportava erroneamente i risultati relativi alle definizioni dell’indice Oak in ui.apps come CRITICO.

## Strumento Trasferimento contenuti {#ctt-release}

### Data di pubblicazione {#release-date-ctt}

La data di pubblicazione dello strumento Content Transfer v1.9.0 è il 28 febbraio 2022.

### Novità {#what-is-new-ctt}

* Controllo dei limiti di dimensione: la funzione di controllo dimensioni dello strumento Content Transfer consente di ridurre i trasferimenti non riusciti. Con la funzione di controllo dimensioni, gli utenti possono determinare se dispongono di spazio su disco sufficiente nella sottodirectory `crx-quickstart` prima dell&#39;estrazione. Inoltre, può stimare le dimensioni del set di migrazione e verificare se è supportato. Se uno o entrambi questi controlli sono violati, gli utenti visualizzano avvisi nell&#39;interfaccia utente CTT. Con questo controllo puoi evitare errori di trasferimento dei contenuti e verificare in modo proattivo con l’Assistenza clienti di Adobe le opzioni di migrazione disponibili. Per ulteriori dettagli, vedere [Determinazione delle dimensioni del set di migrazione e dello spazio su disco](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=it#migration-set-size).
