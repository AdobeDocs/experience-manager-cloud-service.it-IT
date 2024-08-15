---
title: Note sulla versione 2021.12.0 degli strumenti di migrazione in AEM as a Cloud Service
description: Note sulla versione 2021.12.0 degli strumenti di migrazione in AEM as a Cloud Service
feature: Release Information
exl-id: 4155e1c0-cd40-4cbc-9d6c-b106d68a2db5
role: Admin
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 38%

---

# Note sulla versione 2021.12.0 degli strumenti di migrazione in AEM as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione di AEM as a Cloud Service 2021.12.0 per gli strumenti di migrazione.

>[!NOTE]
>
>Per le ultime note sulla versione, consulta [Note sulla versione corrente di Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Analisi delle best practice {#bpa-release}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.22 è il 1 dicembre 2021.

### Novità {#what-is-new-bpa}

* Possibilità di rilevare e segnalare la versione di ACS comunemente utilizzata.
* Possibilità di rilevare e segnalare il numero di utenti e sottogruppi in un gruppo.
* Possibilità di rilevare e segnalare i valori delle proprietà dei nodi in MongoDB che superano i 16 MB.

### Correzioni di bug {#bug-fixes-bpa}

* Il rilevamento dei componenti di Foundation è stato perfezionato per ridurre i falsi negativi.
* Per i clienti AEM Forms, la messaggistica BPA riguardante `EMAIL_PDF_SUBMIT_ACTION` non disponibile su AEM as a Cloud Service è stata corretta.


## Strumento Trasferimento contenuti {#ctt-release}

### Data di pubblicazione {#release-date-ctt}

La data di pubblicazione dello strumento Content Transfer v1.7.10 è il 8 dicembre 2021.

### Novità {#what-is-new-ctt}

* È stata aggiunta un&#39;opzione alla fase di acquisizione nello strumento Content Transfer (Trasferimento contenuti) per consentire agli utenti di disabilitare la [pre-copia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html) durante l&#39;acquisizione. Per velocità di acquisizione ottimali, la pre-copia durante l’acquisizione deve essere disabilitata per piccoli set di migrazione o se sono stati aggiunti solo pochi BLOB dall’ultima acquisizione.
* La mappatura degli utenti è stata aggiornata per utilizzare l’API di gestione utenti migliorata, che consente di ottenere 2000 utenti alla volta, migliorando in modo significativo le prestazioni.
