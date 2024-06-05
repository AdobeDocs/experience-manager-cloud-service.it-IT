---
title: Note sulla versione 2023.09.0 degli strumenti di migrazione in AEM as a Cloud Service
description: Note sulla versione 2023.09.0 degli strumenti di migrazione in AEM as a Cloud Service
feature: Release Information
exl-id: 484a60d4-a439-43d6-a23e-4a3b45ef4160
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 4%

---

# Note sulla versione 2023.09.0 degli strumenti di migrazione in AEM as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2023.09.0 degli strumenti di migrazione in AEM as a Cloud Service.

## Strumento Trasferimento contenuti {#ctt-release}

### Data di pubblicazione {#release-date-ctt}

La data di pubblicazione dello strumento Content Transfer v3.0.0 è il 7 settembre 2023.

### Novità {#what-is-new-ctt}

Lo strumento Content Transfer (Trasferimento contenuti) è stato migliorato per offrire i seguenti vantaggi:

* È stato ridotto il tempo di trasferimento durante la migrazione di un sottoinsieme di un archivio di contenuti utilizzando AzCopy per copiare solo gli ID BLOB richiesti invece di copiare tutti gli ID BLOB.
* Miglioramenti più rapidi dei contenuti differenziali con l’aggiornamento Oak.
* È stata migliorata la robustezza separando il processo di indicizzazione dal processo di acquisizione dei contenuti. In caso di indicizzazione non riuscita, il contenuto non deve essere nuovamente acquisito. Solo l’indicizzazione si riavvia automaticamente, risparmiando tempo e fatica.
