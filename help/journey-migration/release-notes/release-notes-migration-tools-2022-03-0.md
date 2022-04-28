---
title: Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2022.3.0
description: Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2022.3.0
feature: Release Information
exl-id: ab43605d-d46e-43de-b71f-fab610609550
source-git-commit: 87e3291b4a72c24fc6cf8df488df305f1a078ea5
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 86%

---

# Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2022.3.0 {#release-notes}

Questa pagina illustra le note sulla versione per gli strumenti di migrazione AEM as a Cloud Service 2022.3.0.

## Analisi delle best practice {#bpa-release}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.26 è il 16 marzo 2022.

### Novità {#what-is-new-bpa}

* Possibilità di rilevare le risorse non elaborate. Se vengono rilevate risorse non elaborate, tali risorse devono essere impostate su elaborate o devono essere rimosse dal set di migrazione durante il trasferimento del contenuto per evitare problemi durante l’assimilazione del contenuto.
* Possibilità di rilevare se il contenuto ha più di 1000 URL personalizzati. L’utilizzo di un numero elevato di URL personalizzati non è consigliato in quanto sovraccarica i server Dispatcher e Publish.
* Possibilità di identificare i problemi relativi alle definizioni degli indici Oak e di rilevare le incompatibilità con AEM as a Cloud Service.
* Possibilità di rilevare e creare rapporti sull’utilizzo delle configurazioni di Externalizer. In AEM as a Cloud Service le configurazioni di Externalizer sono impostate da Cloud Manager, pertanto le configurazioni esistenti di Externalizer devono essere reimpostate per mantenere la compatibilità.

### Correzioni di bug {#bug-fixes-bpa}

* In alcuni scenari, l’esecuzione di BPA non è riuscita a causa di un errore di asserzione generato da FormsSelectiveFeaturesAnalysis. Questo problema è stato risolto.
* BPA riportava i risultati relativi al modello WRK come PRINCIPALE invece di CRITICO. Questo problema è stato risolto.
* BPA riportava erroneamente i risultati relativi alle definizioni dell’indice OAK in ui.apps come CRITICO. Questo problema è stato risolto..

## Strumento Trasferimento contenuti {#ctt-release}

### Data di pubblicazione {#release-date-ctt}

La data di pubblicazione dello strumento Content Transfer v1.9.0 è il 28 febbraio 2022.

### Novità {#what-is-new-ctt}

* Controllo dei limiti di dimensione: la funzione di controllo dimensioni dello strumento Content Transfer consente di ridurre i trasferimenti non riusciti. Con la funzione di controllo dimensioni, gli utenti possono 1) determinare se hanno spazio su disco sufficiente nella sottodirectory `crx-quickstart` prima dell’estrazione e 2) stimare le dimensioni del set di migrazione e verificare se è supportato. Se uno o entrambi questi controlli vengono violati, verrà visualizzato un avviso nell’interfaccia utente dello strumento Content Transfer. Con questo controllo puoi evitare errori di trasferimento dei contenuti e verificare in modo proattivo con l’Assistenza clienti di Adobe le opzioni di migrazione disponibili. Per ulteriori dettagli, consulta [Determinazione delle dimensioni del set di migrazione e dello spazio su disco](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=it#migration-set-size).
