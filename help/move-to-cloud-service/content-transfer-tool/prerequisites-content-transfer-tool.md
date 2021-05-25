---
title: Prerequisiti per lo strumento Content Transfer (Trasferimento contenuti)
description: Prerequisiti per lo strumento Content Transfer (Trasferimento contenuti)
source-git-commit: c760b97cdb565244cf20f5193de3e3ebab1579ad
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 1%

---

# Prerequisiti per lo strumento Content Transfer (Trasferimento contenuti) {#prerequisites}

La tabella seguente riepiloga i prerequisiti prima di utilizzare lo strumento Content Transfer (Trasferimento contenuti). Rivedi tutte le considerazioni elencate di seguito:

| Considerazioni | Cosa è attualmente supportato |
|--- |--- |
| Versione di AEM | Lo strumento Content Transfer (Trasferimento contenuti) può essere eseguito solo nelle versioni AEM 6.3 o successive. Per poter utilizzare lo strumento Content Transfer (Trasferimento contenuti) con AEM 6.2 o versioni precedenti, è necessario un aggiornamento locale dell’archivio dei contenuti a AEM 6.5. Non è necessario aggiornare il codice a AEM 6.5 per questo. |
| Dimensione dell’archivio segmenti | Lo strumento Content Transfer supporta attualmente fino a 83 GB su *Author* e fino a 31 GB su *Publish*. |
| Dimensione totale dell’archivio dei contenuti (archivio dei contenuti + archivio dei dati) | Lo strumento Content Transfer (Trasferimento contenuti) è progettato per trasferire contenuti fino a 10 TB. Attualmente non è supportato alcun valore superiore a 10 TB. Crea un ticket di assistenza con l’Assistenza clienti Adobe per discutere le opzioni per contenuti di dimensioni superiori a 10 TB. |
| Contenuto in percorsi immutabili | Lo strumento Content Transfer (Trasferimento contenuti) non funziona per la migrazione del contenuto in percorsi immutabili come `“/etc”`. Per ulteriori informazioni sulla ristrutturazione dell&#39;archivio e sui modelli di flusso di lavoro, consulta [Ristrutturazione del repository comune](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=en#restructuring) . |