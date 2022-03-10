---
title: Note sulla versione per Cloud Manager 2022.3.0 in Adobe Experience Manager as a Cloud Service
description: Queste sono le note sulla versione per Cloud Manager 2022.3.0 in AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 428bba062fcfb44ebfbbf3c1d05ce1a4634fb429
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 2%

---


# Note sulla versione per Cloud Manager 2022.3.0 in Adobe Experience Manager as a Cloud Service {#release-notes}

Questa pagina documenta le note sulla versione per Cloud Manager 2022.3.0 in AEM as a Cloud Service.

>[!NOTE]
>
>Fai riferimento a [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md) per le note sulla versione corrente per Adobe Experience Manager as a Cloud Service.

## Data di pubblicazione {#release-date}

La data di rilascio della versione 2022.3.0 di Cloud Manager in AEM 10 marzo 2022. La prossima versione è prevista per il 7 aprile 2022.

## Novità {#what-is-new}

* Un utente con **Sviluppatore** Il ruolo ora può accedere al registro dell&#39;ambiente AEM.
* [La `reliability_rating` metrica critica](/help/implementing/cloud-manager/code-quality-testing.md) è stato disattivato.
* Ora un utente può ordinare le colonne nel **Tubi** in Cloud Manager.

## Correzioni di bug {#bug-fixes}

* Un sottoinsieme di archivi git creati manualmente presentava valori di nome non corretti che ne influenzavano l’utilizzo [la funzione di riutilizzo degli artefatti di build.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) I nomi di tali archivi sono stati modificati e gli utenti vedranno il nome corretto nell’API/interfaccia utente di Cloud Manager.
* [Quando aggiungi o modifichi una pipeline di qualità del codice,](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) la **Comportamento di errori di metrica importanti** le opzioni non vengono più visualizzate.
* Le configurazioni impreviste delle variabili della pipeline non causano più errori nel passaggio di compilazione.
