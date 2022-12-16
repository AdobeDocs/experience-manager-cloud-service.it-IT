---
title: Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2022.7.0
description: Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2022.7.0
feature: Release Information
exl-id: bc8f1a80-867e-423a-9c03-4a53b1ebc57c
source-git-commit: cc52dfac1e7495d6a792bc7525720695022db8eb
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 9%

---

# Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2022.7.0 {#release-notes}

Questa pagina illustra le note sulla versione per gli strumenti di migrazione in AEM as a Cloud Service 2022.7.0.

## Analisi delle best practice {#bpa-release}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.30 è il 27 luglio 2022.

### Novità {#what-is-new-bpa}

* BPA ora è in grado di rilevare e segnalare la dimensione totale dell&#39;indice Lucene migrabile che è Indice Lucene totale escluso `/oak:index/lucene` e `/oak:index/damAssetLucene`.
* È stato aggiunto un nuovo pattern in BPA per rilevare e creare rapporti sull’utilizzo di un dizionario i18n personalizzato. Translator.html non è disponibile AEM dizionario i18n as a Cloud Service e personalizzato deve essere distribuito da Git tramite la pipeline CI/CD di Cloud Manager.

### Correzioni di bug {#bug-fixes-bpa}

* BPA generava rapporti sulle rappresentazioni originali mancanti per i frammenti di contenuto. Poiché i frammenti di contenuto non dispongono di rappresentazioni, questo controllo viene ignorato per i frammenti di contenuto.
* L’opzione per filtrare i risultati di ACS Commons era mancante nell’interfaccia utente BPA. Questo problema è stato risolto.

## Strumento Trasferimento contenuti {#ctt-release}

### Data di pubblicazione {#release-date-ctt}

La data di rilascio dello strumento Content Transfer v2.0.12 è il 19 luglio 2022.

### Novità {#what-is-new-ctt}

* Gli utenti connessi tramite LDAP sono ora in grado di eseguire le funzioni Verifica dimensioni e Mappatura utente in CTT.
* Per facilitare il debug dei problemi di connessione SSL/TLS durante le estrazioni, gli utenti ora possono abilitare la registrazione SSL.
* Per facilitare il debug dei problemi di connettività all’origine, i nomi dei sottodomini vengono ora stampati nei registri quando la connessione ad Azure non riesce.
* Per facilitare il debug dei problemi durante la pre-copia, i registri AzCopy ora vengono aggiunti ai registri di estrazione quando la pre-copia non riesce.
* Per evitare risultati obsoleti di Check Size, gli utenti saranno in grado di eseguire nuovamente Check Size solo dopo il completamento di una precedente Check Size.

### Correzioni di bug {#bug-fixes-ctt}

* Dopo l’eliminazione e la ricreazione di un set di migrazione venivano visualizzati i registri di estrazione precedenti. Questo problema è stato risolto.
* Il pulsante Visualizza stato dell&#39;azione non era disponibile per i set di migrazione con stato STOPPED. Questo problema è stato risolto.
* Il pulsante Elimina azione non era disponibile per i set di migrazione con una chiave di estrazione scaduta. Questo problema è stato risolto.
* Correzione di più bug dell&#39;interfaccia utente.

## Cloud Acceleration Manager {#cam-release}

### Data di pubblicazione {#release-date-cam}

La data di rilascio di Cloud Acceleration Manager è il 15 luglio 2022.

### Novità {#what-is-new-cam}

* Cloud Acceleration Manager ora consente agli utenti di recuperare manualmente il token di migrazione per poter avviare un’acquisizione quando il recupero automatico non riesce. Il recupero automatico può non riuscire se i clienti hanno impostato un elenco di indirizzi IP che blocca CAM o se un utente non amministratore tenta di avviare un&#39;acquisizione. Fai riferimento a [Risoluzione dei problemi](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#troubleshooting) per ulteriori informazioni.
* Le tabelle lunghe nella pagina Complessità di migrazione ora sono comprimibili per facilitarne l’utilizzo.
