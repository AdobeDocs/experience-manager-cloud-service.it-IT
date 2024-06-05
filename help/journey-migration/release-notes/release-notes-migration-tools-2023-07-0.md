---
title: Note sulla versione 2023.07.0 degli strumenti di migrazione nell’AEM as a Cloud Service
description: Note sulla versione 2023.07.0 degli strumenti di migrazione nell’AEM as a Cloud Service
feature: Release Information
exl-id: 2f787321-f156-480d-bbe8-1a6d04f110c5
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 6%

---

# Note sulla versione 2023.07.0 degli strumenti di migrazione nell’AEM as a Cloud Service {#release-notes}

Questa pagina illustra le note sulla versione 2023.07.0 degli strumenti di migrazione in AEM as a Cloud Service.

## Analisi delle best practice {#bpa-release}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.42 è il 6 luglio 2023.

### Novità {#what-is-new-bpa}

* A questa versione di Best Practices Analyzer sono stati aggiunti diversi modelli di best practice. Comprendono:
   * Identificazione della configurazione minima dell&#39;attività di manutenzione
   * Rilevamento di query con tempi di esecuzione lunghi/pesanti
   * Rilevamento di un numero elevato di flussi di lavoro di authoring in esecuzione o in stato non aggiornato
   * Rilevamento della configurazione del processo Sling OSGI Apache
   * Rilevamento delle cache Guava personalizzate

### Correzioni di bug {#bug-fixes-bpa}

* Il BPA è stato migliorato per evitare errori di generazione di rapporti con un numero elevato di risultati.
* Il BPA è stato migliorato per rilevare i caratteri di escape nei percorsi al fine di evitare errori di acquisizione dei contenuti durante la migrazione dei contenuti a AEM as a Cloud Service.
