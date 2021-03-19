---
title: Note sulla versione di Cloud Manager in AEM as a Cloud Service 2020.8.0
description: Note sulla versione di Cloud Manager in AEM as a Cloud Service 2020.8.0
feature: Informazioni sulla versione
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 2%

---


# Note sulla versione di Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.8.0 {#release-notes}

Questa pagina illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2020.8.0.

## Data di rilascio {#release-date}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2020.8.0 è il 6 agosto 2020.

## Novità {#whats-new-cloud-manager}

* Verifica del contenuto è una funzione abilitata nelle pipeline di produzione di Cloud Manager Sites. La configurazione della pipeline di produzione per i programmi con Sites ora include una terza scheda denominata **Verifica del contenuto**. Ogni volta che viene eseguita una pipeline di produzione, nella pipeline verrà incluso un nuovo passaggio di Verifica del contenuto dopo un test funzionale personalizzato che valuterà il sito in base a una serie di dimensioni, tra cui prestazioni, SEO (Search Engine Optimization), accessibilità, best practice e PWA (Progressive Web App).


   >[!NOTE]
   >La funzione di audit del contenuto è stata successivamente rinominata in Audit esperienze.

   Per ulteriori informazioni, consulta [Test di audit esperienza](/help/implementing/cloud-manager/experience-audit-testing.md) .

* Gli ambienti creati di recente nei programmi Assets ora verranno configurati automaticamente con Smart Content Services.

* Gli ambienti sospesi possono essere disattivati dalla pagina **Panoramica** di Cloud Manager.

* Possibilità di eseguire controlli di esperienza sulle pagine, con tecnologia Google Lighthouse. Come parte della pipeline di Cloud Manager, è possibile controllare e convalidare fino a 25 pagine in base ai KPI di esperienza e visualizzare i punteggi nell’interfaccia utente di Cloud Manager.

### Correzioni di bug {#bug-fixes-cm}

* Alcuni plug-in SonarQube superflui e indesiderati venivano eseguiti come parte della scansione Code Quality.

* Nella pagina di esecuzione della pipeline, il nome del ramo non era formattato correttamente.

* In alcuni casi, le esecuzioni completate della pipeline non sono state registrate correttamente come completate, impedendo così nuove esecuzioni della pipeline.

* Le esecuzioni delle pipeline verrebbero occasionalmente bloccate a causa di problemi di comunicazione interni.**

* Al momento del provisioning di una nuova organizzazione, ad alcuni utenti con ruoli amministrativi diversi dagli amministratori di sistema è stato erroneamente concesso l’accesso a Cloud Manager.

* In determinate condizioni, il processo di indicizzazione dell&#39;aggiornamento è stato avviato più volte in parallelo, causando un errore di distribuzione.

* La descrizione comandi sulle schede del programma non era corretta in modo coerente.

* L&#39;interfaccia utente ha erroneamente consentito il tentativo di eseguire operazioni in un ambiente durante l&#39;eliminazione.

* C&#39;è stata una mancata corrispondenza dei colori nella pagina **Panoramica** di Cloud Manager.

### Problemi noti {#known-issues-cm}

* Sono incluse pagine non valide che riportano il punteggio medio di Verifica del contenuto al di sotto di quello che dovrebbe essere.

* La scheda Verifica del contenuto visualizza in modo errato l’URL di base utilizzando il dominio dell’autore invece del dominio di pubblicazione.

* Per attivare il passaggio Verifica contenuto, gli utenti devono modificare la pipeline e, facoltativamente, aggiungere pagine. Se non viene aggiunta alcuna pagina, la home page verrà sottoposta a controllo.