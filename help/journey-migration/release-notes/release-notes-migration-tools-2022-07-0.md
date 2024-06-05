---
title: Note sulla versione 2022.7.0 degli strumenti di migrazione in AEM as a Cloud Service
description: Note sulla versione 2022.7.0 degli strumenti di migrazione in AEM as a Cloud Service
feature: Release Information
exl-id: bc8f1a80-867e-423a-9c03-4a53b1ebc57c
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 9%

---

# Note sulla versione 2022.7.0 degli strumenti di migrazione in AEM as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2022.7.0 degli strumenti di migrazione in AEM as a Cloud Service.

## Analisi delle best practice {#bpa-release}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.30 è il 27 luglio 2022.

### Novità {#what-is-new-bpa}

* BPA ora può rilevare e segnalare la dimensione totale dell’indice Lucene migrabile, che è l’indice Lucene totale escluse `/oak:index/lucene` e `/oak:index/damAssetLucene`.
* È stato aggiunto un nuovo pattern in BPA per rilevare e segnalare l’utilizzo di un dizionario i18n personalizzato. Translator.html non è disponibile in AEM as a Cloud Service e il dizionario i18n personalizzato deve essere distribuito da Git tramite la pipeline CI/CD di Cloud Manager.

### Correzioni di bug {#bug-fixes-bpa}

* BPA segnalava la mancanza di rappresentazioni originali per i frammenti di contenuto. Poiché i frammenti di contenuto non dispongono di rappresentazioni, questo controllo viene ora ignorato per i frammenti di contenuto.
* L’opzione per filtrare i risultati ACS Commons non era presente nell’interfaccia utente BPA. Questo problema è stato risolto.

## Strumento Trasferimento contenuti {#ctt-release}

### Data di pubblicazione {#release-date-ctt}

La data di pubblicazione dello strumento Content Transfer v2.0.12 è il 19 luglio 2022.

### Novità {#what-is-new-ctt}

* Gli utenti che hanno effettuato l’accesso tramite LDAP ora possono eseguire le funzioni Verifica dimensioni e Mappatura utenti in CTT.
* Per facilitare il debug dei problemi di connessione SSL/TLS durante le estrazioni, gli utenti ora possono abilitare la registrazione SSL.
* Per facilitare il debug dei problemi di connettività di origine, i nomi dei sottodomini vengono ora stampati nei registri quando la connessione ad Azure non riesce.
* Per facilitare il debug dei problemi durante la pre-copia, i registri AzCopy ora vengono aggiunti ai registri di estrazione quando la pre-copia non riesce.
* Per evitare di ottenere risultati non aggiornati in Dimensioni di controllo, gli utenti possono rieseguire Dimensioni di controllo solo dopo aver completato un controllo precedente.

### Correzioni di bug {#bug-fixes-ctt}

* I registri di estrazione precedenti venivano visualizzati dopo l’eliminazione e la ricreazione di un set di migrazione. Questo problema è stato risolto.
* Il pulsante di azione Visualizza avanzamento non era disponibile per i set di migrazione con stato ARRESTATO. Questo problema è stato risolto.
* Il pulsante Elimina azione non era disponibile per i set di migrazione con una chiave di estrazione scaduta. Questo problema è stato risolto.
* Sono stati corretti diversi bug dell’interfaccia utente.

## Cloud Acceleration Manager {#cam-release}

### Data di rilascio {#release-date-cam}

La data di pubblicazione di Cloud Acceleration Manager è il 15 luglio 2022.

### Novità {#what-is-new-cam}

* Cloud Acceleration Manager ora consente agli utenti di recuperare manualmente il token di migrazione per poter avviare un’acquisizione quando il recupero automatico non riesce. Il recupero automatico può non riuscire se i clienti hanno impostato un elenco IP consentiti che blocca CAM o se un utente non amministratore tenta di avviare un’acquisizione. Consulta [Risoluzione dei problemi](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#troubleshooting) per ulteriori informazioni.
* Le tabelle lunghe nella pagina Complessità di migrazione sono ora comprimibili per semplificare l’utilizzo.
