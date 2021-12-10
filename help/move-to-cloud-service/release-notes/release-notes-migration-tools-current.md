---
title: Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2021.12.0
description: Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2021.12.0
feature: Release Information
source-git-commit: 58dcf083ebf4cd2546213ba574f0f9c547aef008
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 7%

---


# Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2021.12.0 {#release-notes}

Questa pagina illustra le note sulla versione per gli strumenti di migrazione in AEM as a Cloud Service 2021.12.0.

>[!NOTE]
>Per visualizzare le note sulla versione corrente per Adobe Experience Manager as a Cloud Service, fai clic su [qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=it).

## Analisi delle best practice {#bpa-release}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.22 è il 10 dicembre 2021.

### Novità {#what-is-new-bpa}

* Possibilità di rilevare e segnalare la versione di ACS commons utilizzata.
* Possibilità di rilevare e segnalare il numero di utenti e sottogruppi in un gruppo.
* Possibilità di rilevare e segnalare i valori delle proprietà dei nodi in MongoDB che superano i 16 MB.

### Correzioni di bug {#bug-fixes-bpa}

* Il rilevamento dei componenti di Foundation è stato perfezionato per ridurre i falsi negativi.
* Per i clienti AEM Forms, messaggistica BPA riguardante `EMAIL_PDF_SUBMIT_ACTION` non disponibile su AEM as a Cloud Service è stato corretto.


## Strumento Content Transfer (Trasferimento contenuti)  {#ctt-release}

### Data di pubblicazione {#release-date-ctt}

La data di rilascio dello strumento Content Transfer (Trasferimento contenuti) v1.7.10 è l’8 dicembre 2021.

### Novità {#what-is-new-ctt}

* Passa alla fase di acquisizione nello strumento Content Transfer (Trasferimento contenuti) per consentire agli utenti di disattivarla [pre-copia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) durante l&#39;ingestione. Per una velocità di acquisizione ottimale, la pre-copia durante l’acquisizione deve essere disabilitata per i set di migrazione di piccole dimensioni o se sono stati aggiunti solo pochi BLOB dall’ultima acquisizione.
* La mappatura utente è stata aggiornata per utilizzare l&#39;API User Management migliorata che consente di ottenere 2000 utenti alla volta, migliorando significativamente le prestazioni.
