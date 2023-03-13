---
title: Note sulla versione 2021.12.0 degli strumenti di migrazione nell’AEM as a Cloud Service
description: Note sulla versione 2021.12.0 degli strumenti di migrazione nell’AEM as a Cloud Service
feature: Release Information
exl-id: 4155e1c0-cd40-4cbc-9d6c-b106d68a2db5
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 46%

---

# Note sulla versione 2021.12.0 degli strumenti di migrazione nell’AEM as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2021.12.0 degli strumenti di migrazione in AEM as a Cloud Service.

>[!NOTE]
>Per visualizzare le note sulla versione corrente di Adobe Experience Manager as a Cloud Service, fai clic [qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=it).

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

* È stata aggiunta un’opzione alla fase di acquisizione nello strumento Content Transfer (Trasferimento contenuti) per consentire agli utenti di disabilitare [pre-copia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) durante l’acquisizione. Per velocità di acquisizione ottimali, la pre-copia durante l’acquisizione deve essere disabilitata per piccoli set di migrazione o se sono stati aggiunti solo pochi BLOB dall’ultima acquisizione.
* La mappatura degli utenti è stata aggiornata per utilizzare l’API di gestione utenti migliorata, che consente di ottenere 2000 utenti alla volta, migliorando in modo significativo le prestazioni.
