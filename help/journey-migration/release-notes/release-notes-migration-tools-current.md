---
title: Note sulla versione 2024.07 degli strumenti di migrazione in AEM as a Cloud Service
description: Note sulla versione 2024.07.0 degli strumenti di migrazione in AEM as a Cloud Service
feature: Release Information
exl-id: 52709511-eab2-47a7-8bea-1b707cd568a1
role: Admin
source-git-commit: 4f01ca0076248442fe93161bbc8b98bffb64551b
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 8%

---

# Note sulla versione 2024.07.0 degli strumenti di migrazione in AEM as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione degli strumenti di migrazione in AEM as a Cloud Service 2024.07.0.

## Strumento Trasferimento contenuti {#ctt-release}

### Data di pubblicazione {#release-date-ctt}

La data di pubblicazione dello strumento Content Transfer v3.0.16 è luglio 2024.

### Novità {#what-is-new-ctt}

* Caricamento automatico dei registri di estrazione CTT in caso di errori.
* Ora gli utenti possono eseguire correttamente l’acquisizione al momento del rinnovo della chiave di estrazione.
* È stato aggiunto il supporto per l’esecuzione di estrazioni CTT utilizzando una chiave di accesso e una chiave segreta di Azure con AzureDataStore.
* Ora gli utenti ricevono il messaggio di errore corretto quando viene utilizzata una chiave non valida per creare un set di migrazione.

## Analisi delle best practice {#bpa-release}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.50 è maggio 2024.

### Correzioni di bug {#bug-fixes-bpa}

* Best Practices Analyzer ora rileva tutti i nodi di dimensioni superiori a 16 MB
* È stata risolta una situazione di tipo &quot;race condition&quot; che causava occorrenze sproradiche di reperti NCC.
