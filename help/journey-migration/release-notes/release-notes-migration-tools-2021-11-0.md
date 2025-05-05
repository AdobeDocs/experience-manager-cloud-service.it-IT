---
title: Note sulla versione 2021.11.0 degli strumenti di migrazione in AEM as a Cloud Service
description: Note sulla versione 2021.11.0 degli strumenti di migrazione in AEM as a Cloud Service
feature: Release Information
exl-id: 668c0c66-88f5-4d74-9a2a-3bdc63b0bba7
role: Admin
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 4%

---

# Note sulla versione 2021.11.0 degli strumenti di migrazione in AEM as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione degli strumenti di migrazione in AEM as a Cloud Service 2021.11.0.

>[!NOTE]
>
>Per le ultime note sulla versione, consulta [Note sulla versione corrente di Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Strumento Trasferimento contenuti {#ctt-release}

### Data di pubblicazione {#release-date-ctt}

La data di pubblicazione dello strumento Content Transfer v1.7.2 è il 1° novembre 2021.

### Novità {#what-is-new-ctt}

* È stato aggiunto il supporto per un passaggio facoltativo di [pre-copia](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=it) da utilizzare con lo strumento Content Transfer quando l&#39;istanza AEM di origine è configurata per utilizzare File Data Store per velocizzare in modo significativo la fase di estrazione.

* Sono stati aggiunti ulteriori messaggi descrittivi alla fase di acquisizione nell’interfaccia dello strumento Content Transfer (Trasferimento contenuti) per indicare quando sono in corso i passaggi di indicizzazione e ripristino del mongo.
