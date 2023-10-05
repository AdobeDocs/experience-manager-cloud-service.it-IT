---
title: Note sulla versione 2023.09.0 degli strumenti di migrazione in AEM as a Cloud Service
description: Note sulla versione 2022.09.0 degli strumenti di migrazione in AEM as a Cloud Service
feature: Release Information
exl-id: 52709511-eab2-47a7-8bea-1b707cd568a1
source-git-commit: c89ca7320d8f31d2545cadf98f39e577337b8918
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 4%

---

# Note sulla versione 2023.09.0 degli strumenti di migrazione in AEM as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2022.09.0 degli strumenti di migrazione in AEM as a Cloud Service.

## Strumento Trasferimento contenuti {#ctt-release}

### Data di pubblicazione {#release-date-ctt}

La data di pubblicazione dello strumento Content Transfer v3.0.0 è il 7 settembre 2023.

### Novità {#what-is-new-ctt}

Lo strumento Content Transfer (Trasferimento contenuti) è stato notevolmente migliorato per offrire i seguenti vantaggi:
* Riduzione del tempo di trasferimento durante la migrazione di un sottoinsieme di un archivio di contenuti grazie a AzCopy per copiare solo gli ID BLOB richiesti invece di copiare tutti gli ID BLOB
* Miglioramenti più rapidi dei contenuti differenziali con l’aggiornamento Oak
* È stata migliorata la robustezza separando il processo di indicizzazione dal processo di acquisizione dei contenuti. In caso di indicizzazione non riuscita, il contenuto non dovrà essere nuovamente acquisito. Solo l’indicizzazione si riavvia automaticamente, risparmiando tempo e fatica
