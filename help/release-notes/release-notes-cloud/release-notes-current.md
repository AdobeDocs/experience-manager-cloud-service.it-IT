---
title: 'Adobe Experience Manager as a Cloud Service: note sulla versione 2020.7.0'
description: Note sulla versione 2020.7.0 di Experience Manager
translation-type: tm+mt
source-git-commit: f96a9b89bb704b8b8b8eb94cdb5f94cc42890ec8
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 17%

---


# Note sulla versione di AEM as a Cloud Service 2020.7.0 {#release-notes}

La sezione seguente illustra le note generali sulla versione di Experience Manager as a Cloud Service 2020.7.0.

## Novità di Cloud Manager {#cloud-manager}

Leggi questa sezione per scoprire le novità e gli aggiornamenti di Cloud Manager in AEM as a Cloud Service, versione 2020.7.0.

### Data di rilascio {#release-date}

La data di rilascio per [!UICONTROL Cloud Manager] versione 2020.7.0 è il 9 luglio 2020.

### Novità {#what-is-new-cloud-manager}

* La pagina degli ambienti è stata riprogettata.

* Gli ambienti con sospensione ora mostrano uno stato discreto in Cloud Manager quando sono attivati.

* Il numero di variabili ambientali per ambiente è stato aumentato a 200.

* Il contenitore di build di Cloud Manager ora supporta sia Java 8 che Java 11.

* Le pipeline di Cloud Manager ora supportano le variabili e i segreti del set di clienti.
Per ulteriori informazioni, vedere Variabili [](/help/onboarding/getting-access-to-aem-in-cloud/creating-aem-application-project.md#pipeline-variables) tubazione.

### Correzioni di bug {#bug-fixes-cm}

* Il collegamento da Cloud Manager a Developer Console non era correttamente attivo prima che gli ambienti fossero completamente creati.

* Il collegamento alla console per sviluppatori direttamente da Cloud Manager non consentiva di disattivare/attivare l&#39;ambiente di un programma sandbox.

* Le opzioni **Annulla** e **Salva** nella pagina di modifica della pipeline non di produzione non erano sempre visibili.

* Alcuni errori nel processo di qualità del codice potrebbero causare la mancata generazione corretta del file di registro.

* Quando si crea un nuovo programma, il nome suggerito a volte restituisce un duplicato di un nome di programma esistente.

* Non è stato possibile scaricare in modo coerente alcuni log delle fasi della pipeline di grandi dimensioni tramite l&#39;interfaccia utente.

* La convalida dei nomi dell&#39;ambiente presentava un errore &quot;off-by-one&quot;.

* In alcuni casi, la pagina Ambienti visualizzava segmenti di pubblicazione e dispatcher se non ne erano presenti.

### Problemi noti {#known-issues}

* A causa di una modifica nella modalità di calcolo della copertura del codice, la versione _minima_ del plugin Jacoco è ora 0.7.5.201505241946 (rilasciata a maggio 2015). I clienti che fanno esplicito riferimento a una versione precedente riceveranno un messaggio di errore nel processo di qualità del codice.

## Novità di Cloud Readiness Analyzer {#cloud-readiness-analyzer}

Segui questa sezione per saperne di più sulle novità e gli aggiornamenti per la release v1.0.2 di Cloud Readiness Analyzer.

### Correzioni di bug {#cra-bug-fixes}

* Impossibile eseguire la versione precedente di CRA  Adobe Experience Manager (AEM) 6.1. È stato aggiunto il supporto esplicito per consentire agli utenti del gruppo di amministratori.

   Per ulteriori informazioni, consultate [Installazione di CRA su AEM 6.1](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/cloud-readiness-analyzer/using-cloud-readiness-analyzer.html#installing-on-aem61) .

* La marca temporale di scadenza visualizzata nel rapporto di riepilogo non era corretta.

* CRA rilevava componenti personalizzati duplicati.

* In AEM 6.1, l’ispezione del contenuto è stata terminata prima di completare l’ispezione completa. È stata aggiunta la gestione delle eccezioni per consentire al controllo di saltare e continuare fino al completamento dell&#39;ispezione completa.

