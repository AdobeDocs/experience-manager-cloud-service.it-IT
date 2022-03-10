---
title: Note sulla versione per Cloud Manager 2022.3.0 in Adobe Experience Manager as a Cloud Service
description: Queste sono le note sulla versione per Cloud Manager 2022.3.0 in AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 0749099acf98b09d0f83bfe86c2cc4558261c029
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 3%

---


# Note sulla versione per Cloud Manager 2022.3.0 in Adobe Experience Manager as a Cloud Service {#release-notes}

Questa pagina documenta le note sulla versione per Cloud Manager 2022.3.0 in AEM as a Cloud Service.

>[!NOTE]
>
>Fai riferimento a [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md) per le note sulla versione corrente per Adobe Experience Manager as a Cloud Service.

## Data di pubblicazione {#release-date}

La data di rilascio della versione 2022.3.0 di Cloud Manager in AEM 10 marzo 2022. La prossima versione è prevista per il 7 aprile 2022.

## Novità {#what-is-new}

* Per accedere AEM registro dell’ambiente è possibile utilizzare il ruolo Sviluppatore .

## Correzioni di bug {#bug-fixes}

* Un sottoinsieme di archivi Git creati manualmente presentava un valore di nome errato che impediva l’efficacia della funzione di riutilizzo degli artefatti di generazione. I nomi di tali archivi sono stati modificati e gli utenti vedranno il nome corretto nell’API/interfaccia utente di Cloud Manager.
* Gli artefatti di generazione da pipeline non di produzione sono stati riutilizzati in modo inappropriato sulle pipeline di stack complete di produzione.
* Quando si aggiunge o si modifica una pipeline di qualità del codice, le opzioni per gestire gli errori di metrica non vengono più visualizzate.
* Alcune configurazioni impreviste di variabili della pipeline potrebbero causare nel passaggio di compilazione.
