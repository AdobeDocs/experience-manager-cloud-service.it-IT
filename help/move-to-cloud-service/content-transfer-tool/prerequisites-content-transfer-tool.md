---
title: Prerequisiti per lo strumento Content Transfer (Trasferimento contenuti)
description: Prerequisiti per lo strumento Content Transfer (Trasferimento contenuti)
source-git-commit: f70959efd9d0382c083ac05b9ccd63cf79947bc2
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---

# Prerequisiti per lo strumento Content Transfer (Trasferimento contenuti) {#prerequisites}

Nella tabella seguente sono riepilogati i prerequisiti per l’utilizzo dello strumento Content Transfer (Trasferimento contenuti).

Rivedi tutte le considerazioni elencate di seguito:

| Considerazioni | Cosa è attualmente supportato |
|--- |--- |
| Versione di AEM | Lo strumento Content Transfer (Trasferimento contenuti) può essere eseguito solo nelle versioni AEM 6.3 o successive. Per poter utilizzare lo strumento Content Transfer (Trasferimento contenuti) con AEM 6.2 o versioni precedenti, è necessario un aggiornamento locale dell’archivio dei contenuti a AEM 6.5. Non è necessario aggiornare il codice a AEM 6.5 per questo. |
| Dimensione dell’archivio segmenti | Lo strumento Content Transfer supporta attualmente fino a 83 GB su *Author* e fino a 31 GB su *Publish*. |
| Dimensione totale dell&#39;archivio dei contenuti <br>*(archivio contenuti + archivio dati)* | Lo strumento Content Transfer (Trasferimento contenuti) è progettato per trasferire contenuti fino a 10 TB. Attualmente non è supportato alcun valore superiore a 10 TB. Crea un ticket di assistenza con l’Assistenza clienti Adobe per discutere le opzioni per contenuti di dimensioni superiori a 10 TB. |
| Contenuto in percorsi immutabili | Lo strumento Content Transfer (Trasferimento contenuti) non funziona per la migrazione del contenuto in percorsi immutabili come `“/etc”`. <br>Per ulteriori informazioni sulla ristrutturazione dell’archivio e sui modelli di flusso di lavoro, consulta  [Ristrutturazione dell’archivio ](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=en#restructuring) comune . |

## Novità {#whats-next}

Dopo aver esaminato i prerequisiti, ora puoi imparare a eseguire lo strumento Content Transfer (Trasferimento contenuti). Per ulteriori informazioni, consulta [Utilizzo dello strumento Content Transfer (Trasferimento contenuti)](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md) .
