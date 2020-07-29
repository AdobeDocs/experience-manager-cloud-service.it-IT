---
title: 'Adobe Experience Manager as a Cloud Service: note sulla versione 2020.7.0'
description: 'Experience Manager: note sulla versione 2020.7.0 di '
translation-type: tm+mt
source-git-commit: 9e27ff9510fda5ed238a25b2d63d1d9a3099a8b5
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 87%

---


# AEM as a Cloud Service: note sulla versione di 2020.7.0 {#release-notes}

La sezione seguente illustra le note generali sulla versione di Experience Manager as a Cloud Service 2020.7.0.

## Novità di Cloud Manager {#cloud-manager}

Leggi questa sezione per scoprire le novità e gli aggiornamenti di Cloud Manager in AEM as a Cloud Service, versione 2020.7.0.

### Data di rilascio {#release-date}

La data di rilascio di [!UICONTROL Cloud Manager] versione 2020.7.0 è il 9 luglio 2020.

### Novità {#what-is-new-cloud-manager}

* La pagina degli ambienti è stata riprogettata.

* Ora in Cloud Manager gli ambienti che sono stati sospesi presentano uno stato discreto.

* In ogni ambiente, il numero di variabili dell’ambiente è stato aumentato a 200.

* Le pipeline di Cloud Manager ora supportano le variabili e i segreti del set di clienti.
Per ulteriori informazioni, vedere Variabili [](/help/onboarding/getting-access-to-aem-in-cloud/creating-aem-application-project.md#pipeline-variables) tubazione.

### Correzioni di bug {#bug-fixes-cm}

* Il collegamento tra Cloud Manager e Developer Console era erroneamente attivo prima che gli ambienti fossero completamente creati.

* Il collegamento diretto da Cloud Manager a Developer Console non mostrava l’opzione per sospendere/riattivare l’ambiente di un programma sandbox.

* Le opzioni **Annulla** e **Salva** nella pagina di modifica della pipeline non di produzione non erano sempre visibili.

* Alcuni errori nel processo di qualità del codice potevano causare la generazione non corretta del file di registro.

* Al momento della creazione di un nuovo programma, a volte il nome suggerito poteva essere un duplicato di nome di programma esistente.

* Tramite l’interfaccia utente non si potevano scaricare in modo coerente i log di alcuni fasi di pipeline di grandi dimensioni.

* La convalida dei nomi dell’ambiente presentava un errore con scostamento pari a uno.

* In alcuni casi, la pagina Ambienti mostrava segmenti di pubblicazione e dispatcher anche in loro assenza.

### Problemi noti {#known-issues}

* A causa di una modifica nella modalità di calcolo della copertura del codice, la versione _minima_ del plugin Jacoco è ora 0.7.5.201505241946 (rilasciata a maggio 2015). I clienti che fanno esplicito riferimento a una versione precedente riceveranno un messaggio di errore nel processo di qualità del codice.

## Novità di Cloud Readiness  Analyzer {#cloud-readiness-analyzer}

Leggi questa sezione per saperne di più sulle novità e sugli aggiornamenti di Cloud Readiness Analyzer v1.0.2.

### Correzioni di bug {#cra-bug-fixes}

* La versione precedente di Cloud Readiness Analyzer non poteva girare su Adobe Experience Manager (AEM) 6.1. È stato aggiunto il supporto esplicito per gli utenti del gruppo di amministratori.

   Per ulteriori informazioni, consulta [Installazione di Cloud Readiness Analyzer in AEM 6.1](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/moving/cloud-migration/cloud-readiness-analyzer/using-cloud-readiness-analyzer.html#installing-on-aem61).

* Nel rapporto di riepilogo veniva visualizzata una marca temporale di scadenza errata.

* Cloud Readiness Analyzer rilevava componenti personalizzati duplicati.

* In AEM 6.1, l’operazione di ispezione del contenuto veniva terminata prima di essere completata. È stata aggiunta una gestione delle eccezioni che consente all’ispettore di ignorare e continuare fino al completamento di tutta l’ispezione.

