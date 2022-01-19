---
title: Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2022.1.0
description: Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2022.1.0
feature: Release Information
source-git-commit: fec3a69db3b05a6b750ebf718f32f599cac24d0c
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 10%

---


# Note sulla versione per gli strumenti di migrazione in AEM versione as a Cloud Service 2022.1.0 {#release-notes}

Questa pagina illustra le note sulla versione per gli strumenti di migrazione AEM as a Cloud Service 2022.1.0.

>[!NOTE]
>Per visualizzare le note sulla versione corrente per Adobe Experience Manager as a Cloud Service, fai clic su [qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=it).


## Strumento Content Transfer (Trasferimento contenuti)  {#ctt-release}

### Data di pubblicazione {#release-date-ctt}

La data di rilascio dello strumento Content Transfer (Trasferimento contenuti) v1.7.18 è il 18 gennaio 2022.

### Novità {#what-is-new-ctt}

* Passa alla fase di estrazione nello strumento Content Transfer (Trasferimento contenuti) per consentire agli utenti di disattivarla [pre-copia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) durante l&#39;estrazione. Per velocità di estrazione ottimali, la pre-copia durante l’estrazione deve essere disabilitata per i set di migrazione di piccole dimensioni o se sono stati aggiunti solo pochi BLOB dall’ultima estrazione.

### Correzioni di bug {#bug-fixes-ctt}

* Configurazioni predefinite aggiornate per ridurre i timeout di esecuzione durante l’estrazione.
