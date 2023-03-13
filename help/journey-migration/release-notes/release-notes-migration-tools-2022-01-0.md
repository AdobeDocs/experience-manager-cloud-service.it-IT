---
title: Note sulla versione 2022.1.0 degli strumenti di migrazione in AEM as a Cloud Service
description: Note sulla versione 2022.1.0 degli strumenti di migrazione in AEM as a Cloud Service
feature: Release Information
exl-id: cbd0c316-bda3-48fb-89d6-a8f97bad1970
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 6%

---

# Note sulla versione 2022.1.0 degli strumenti di migrazione in AEM as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2022.1.0 degli strumenti di migrazione in AEM as a Cloud Service.

## Strumento Trasferimento contenuti {#ctt-release}

### Data di pubblicazione {#release-date-ctt}

La data di pubblicazione dello strumento Content Transfer v1.7.18 è il 18 gennaio 2022.

### Novità {#what-is-new-ctt}

* È stata aggiunta un’opzione alla fase di estrazione nello strumento Content Transfer (Trasferimento contenuti) per consentire agli utenti di disabilitare [pre-copia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) durante l’estrazione. Per velocità di estrazione ottimali, la pre-copia durante l’estrazione deve essere disabilitata per piccoli set di migrazione o se sono stati aggiunti solo pochi BLOB dall’ultima estrazione.

### Correzioni di bug {#bug-fixes-ctt}

* Sono state aggiornate le configurazioni predefinite per ridurre i timeout di esecuzione durante l’estrazione.
