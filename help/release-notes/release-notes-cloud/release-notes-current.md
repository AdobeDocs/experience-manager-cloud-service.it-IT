---
title: Note sulla versione [!DNL Adobe Experience Manager] di Cloud Service per la versione 2020.8.0.
description: '[!DNL Adobe Experience Manager] come Cloud Service - Note sulla versione 2020.8.0.'
translation-type: tm+mt
source-git-commit: 85f5262c2af7502e98fcb60b51b9b13d2c2c0f2c
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 6%

---


# Release Notes for [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0 {#release-notes}

La sezione seguente illustra le note generali sulla versione di Experience Manager as a Cloud Service 2020.8.0.

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* È ora disponibile la funzionalità della console prodotto. Questo consente agli esperti di marketing/autori di AEM di visualizzare e navigare tra le categorie e i prodotti memorizzati nel back-end del commercio. È inoltre disponibile il supporto per le proprietà di categorie e prodotti nella console Prodotti.

* Sono stati migliorati i selettori prodotto e categoria per consentire agli addetti al marketing di selezionare il prodotto tramite SKU o di selezionare la categoria tramite l&#39;ID categoria.

## Cloud Manager {#cloud-manager}

### Data di rilascio {#release-date-cm}

The Release Date for [!UICONTROL Cloud Manager] Version 2020.8.0 is August 06, 2020.

### Novità {#what-is-new-cloud-manager}

* Content Audit è una funzione abilitata nelle pipeline di produzione di siti di Cloud Manager. La configurazione della pipeline di produzione per i programmi con Siti ora include una terza scheda denominata Controllo **** contenuto. Ogni volta che viene eseguita una pipeline di produzione, verrà inclusa una nuova fase di controllo dei contenuti nella pipeline dopo il test funzionale personalizzato che valuterà il sito rispetto a una serie di dimensioni, tra cui prestazioni, SEO (ottimizzazione motore di ricerca), accessibilità, best practice e PWA (app Web progressiva).

   Refer to [Content Audit Testing](/help/implementing/developing/introduction/understand-test-results.md#content-audit-testing) for more details.

* Gli ambienti creati di recente nei programmi Assets ora verranno configurati automaticamente con Smart Content Services.

* Gli ambienti con sospensione possono essere disattivati dalla pagina **Panoramica** di Cloud Manager.

* Sono ora supportati i repository privati con binding di autenticazione.

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

