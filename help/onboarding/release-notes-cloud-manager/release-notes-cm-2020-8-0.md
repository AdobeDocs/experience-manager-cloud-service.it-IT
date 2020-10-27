---
title: Note sulla versione per Cloud Manager in AEM come versione di Cloud Service 2020.8.0
description: Note sulla versione per Cloud Manager in AEM come versione di Cloud Service 2020.8.0
translation-type: tm+mt
source-git-commit: ca690144a8254d5ffba354f0f96d9ef1c5202533
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 1%

---


# Release Notes for Cloud Manager in Adobe Experience Manager as a Cloud Service 2020.8.0 {#release-notes}

In questa pagina sono delineate le Note sulla versione di Marketing Cloud Manager in AEM come Cloud Service 2020.8.0.

## Data di rilascio {#release-date}

La data di rilascio per Cloud Manager in AEM come Cloud Service 2020.8.0 è il 6 agosto 2020.

## Novità {#whats-new-cloud-manager}

* Content Audit è una funzione abilitata nelle pipeline di produzione di siti di Cloud Manager. La configurazione della pipeline di produzione per i programmi con Siti ora include una terza scheda denominata Controllo **** contenuto. Ogni volta che viene eseguita una pipeline di produzione, verrà inclusa una nuova fase di controllo dei contenuti nella pipeline dopo il test funzionale personalizzato che valuterà il sito rispetto a una serie di dimensioni, tra cui prestazioni, SEO (ottimizzazione motore di ricerca), accessibilità, best practice e PWA (app Web progressiva).


   >[!NOTE]
   >L&#39;audit dei contenuti è stato successivamente rinominato in Experience Audit.

   Per ulteriori informazioni, consulta Test [di audit](/help/implementing/cloud-manager/experience-audit-testing.md) esperienza.

* Gli ambienti creati di recente nei programmi Assets ora verranno configurati automaticamente con Smart Content Services.

* Gli ambienti con sospensione possono essere disattivati dalla pagina **Panoramica** di Cloud Manager.

* Possibilità di eseguire verifiche dell’esperienza sulle pagine, con tecnologia Google Lighthouse. Come parte della pipeline di Cloud Manager, è possibile controllare e convalidare fino a 25 pagine in base ai KPI dell&#39;esperienza e visualizzare i punteggi nell&#39;interfaccia di Cloud Manager.

### Correzioni di bug {#bug-fixes-cm}

* Alcuni plug-in SonarQube non necessari e indesiderati venivano eseguiti come parte della scansione Code Quality.

* Nella pagina di esecuzione della pipeline, il nome del ramo non era formattato correttamente.

* In alcuni casi, le esecuzioni completate della pipeline non sono state registrate come completate, impedendo così nuove esecuzioni della pipeline.

* Le esecuzioni delle tubazioni si *bloccavano* occasionalmente a causa di problemi di comunicazione interni.

* Al momento del provisioning di una nuova organizzazione, ad alcuni utenti con ruoli amministrativi diversi dagli amministratori di sistema veniva erroneamente concesso l&#39;accesso a Cloud Manager.

* In alcune condizioni, il processo di indicizzazione degli aggiornamenti è stato avviato più volte in parallelo e ciò ha comportato un errore di distribuzione.

* La descrizione comandi sulle schede del programma non era corretta in modo coerente.

* L&#39;interfaccia utente ha erroneamente consentito di tentare operazioni in un ambiente durante l&#39;eliminazione.

* C&#39;è stata una mancata corrispondenza di colore nella pagina **Panoramica** di Cloud Manager.

### Problemi noti {#known-issues-cm}

* Sono incluse pagine non valide che riportano il punteggio medio di controllo dei contenuti al di sotto di quanto dovrebbero essere.

* La scheda Controllo contenuto visualizza erroneamente l&#39;URL di base utilizzando il dominio dell&#39;autore invece del dominio di pubblicazione.

* Per attivare il passaggio Controllo contenuto, gli utenti devono modificare la pipeline e, facoltativamente, aggiungere pagine. Se non viene aggiunta alcuna pagina, la pagina iniziale verrà sottoposta a controllo.