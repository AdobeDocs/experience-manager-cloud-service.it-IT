---
title: Note sulla versione 2023.06.0 degli strumenti di migrazione nell’AEM as a Cloud Service
description: Note sulla versione 2023.06.0 degli strumenti di migrazione nell’AEM as a Cloud Service
feature: Release Information
exl-id: 021b7472-d1e4-4ef6-a040-c612fed8d3c3
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 3%

---

# Note sulla versione 2023.06.0 degli strumenti di migrazione nell’AEM as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2023.06.0 degli strumenti di migrazione in AEM as a Cloud Service.

## Strumento Trasferimento contenuti {#ctt-release}

### Data di pubblicazione {#release-date-ctt}

La data di pubblicazione dello strumento Content Transfer v2.0.20 è il 8 giugno 2023.

### Novità {#what-is-new-ctt}

* Con questa versione è stato integrato un nuovo strumento di migrazione, Content Transformer (CT), con lo strumento Content Transfer (CTT). Il Content Transformer può rilevare e risolvere automaticamente i problemi relativi al contenuto segnalati da [Best Practices Analyzer (BPA)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=it) prima della migrazione dei contenuti dall’implementazione AEM corrente (on-premise o Managed Services) all’AEM as a Cloud Service.
I vantaggi offerti da Content Transformer sono:
   * Fail-safe: un pacchetto viene creato da Content Transformer ogni volta che apporta modifiche all’archivio per risolvere i problemi. Se necessario, puoi ripristinare lo stato precedente installando il pacchetto.
   * Facile da usare: Content Transformer è stato integrato con lo strumento Content Transfer ed è dotato di una semplice interfaccia utente intuitiva.
   * Risparmio di tempo: quando si dispone di un numero elevato di problemi di contenuto che rientrano in una categoria di pattern, è possibile risolverli tutti con diversi clic utilizzando Content Transformer, riducendo in modo significativo il tempo e la complessità della migrazione.
