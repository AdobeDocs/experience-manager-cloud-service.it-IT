---
title: Note sulla versione per Cloud Manager 2022.3.0 in Adobe Experience Manager as a Cloud Service
description: Queste sono le note sulla versione per Cloud Manager 2022.3.0 in AEM as a Cloud Service.
feature: Release Information
exl-id: d09d48c5-6e0a-4a6a-85e9-1a60fdd6e5bf
source-git-commit: 68586304724530f83649cffee76cefef3e1c8627
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Note sulla versione per Cloud Manager 2022.3.0 in Adobe Experience Manager as a Cloud Service {#release-notes}

Questa pagina documenta le note sulla versione per Cloud Manager 2022.3.0 in AEM as a Cloud Service.

>[!NOTE]
>
>Fai riferimento a [questa pagina](/help/release-notes/release-notes-cloud/release-notes-current.md) per le note sulla versione corrente per Adobe Experience Manager as a Cloud Service.

## Data di pubblicazione {#release-date}

La data di rilascio della versione 2022.3.0 di Cloud Manager in AEM as a Cloud Service è il 10 marzo 2022. La prossima versione è prevista per il 7 aprile 2022.

## Novità {#what-is-new}

* Per accedere al registro dell’ambiente AEM è necessario il ruolo Sviluppatore.

## Correzioni di bug {#bug-fixes}

* Un sottoinsieme di archivi Git creati manualmente presentava un valore di nome errato che impediva l’efficacia della funzione di riutilizzo degli artefatti di build. I nomi di tali archivi sono stati modificati e gli utenti vedranno il nome corretto nell’API/interfaccia utente di Cloud Manager.
* Gli artefatti di build da pipeline non di produzione venivano riutilizzati in modo inappropriato sulle pipeline full stack di produzione.
* Quando si aggiunge o si modifica una pipeline di qualità del codice, le opzioni per gestire gli errori di metrica non vengono più visualizzate.
* Alcune configurazioni impreviste di variabili della pipeline potrebbero verificarsi nel passaggio di compilazione.
