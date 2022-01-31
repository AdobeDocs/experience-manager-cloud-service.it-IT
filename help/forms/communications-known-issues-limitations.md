---
title: 'Problemi noti '
description: Best practice e limitazioni relative alle comunicazioni
source-git-commit: 06da7d2a5063e163aa1534bedbc79ae50ef27515
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 2%

---


# Domande frequenti, best practice, problemi noti e limitazioni {#best-practices-known-issues-and-limitations}

Prima di iniziare a utilizzare le API di comunicazione, consulta le domande frequenti e controlla i seguenti problemi e limitazioni noti:

## Problemi noti

- È possibile utilizzare un tipo di rendering specifico (PDF, STAMPA) una sola volta nell&#39;elenco delle opzioni di stampa. Ad esempio, non è possibile avere due opzioni PRINT ciascuna che specificano un tipo di rendering PCL.

- Per una configurazione batch, una sola istanza di combinazione di valori di OutputType(PDF, PRINT) e RenderType(PostScript, PCL, IPL, ZPL, ecc.) è consentito.

## Best practice  

- Adobe consiglia di ospitare l’archivio dei contenitori BLOB di file di dati nell’area cloud utilizzata da AEM Cloud Service.

## Domande frequenti {#faq}

**È possibile utilizzare una cartella controllata o altri meccanismi di archiviazione per memorizzare l&#39;input e l&#39;output?**

Al momento, è possibile utilizzare l’archiviazione Microsoft Azure per salvare i dati di input e i documenti generati. L’archiviazione di Microsoft Azure offre diverse opzioni per [automatizzare le operazioni di spostamento dei dati](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10).

**Un account di archiviazione Microsoft Azure è incluso con la licenza di Cloud Service Experience Manager Forms?**

L’account di archiviazione Microsoft Azure è indipendente dalla licenza del Cloud Service Experience Manager Forms.

**Le API di comunicazione memorizzano i dati sui server di Cloud Service Experience Manager Forms?**

I dati di input e output vengono salvati solo nell’archiviazione Microsoft Azure.

**Le API di comunicazione sono disponibili solo per il Cloud Service Experience Manager Forms? Posso ottenere funzionalità simili in ambiente on-premise?**

È possibile utilizzare il servizio AEM Forms Output per combinare un modello (XFA o PDF) con i dati dei clienti per generare documenti nei formati PDF, PS, PCL e ZPL.

Rispetto all&#39;ambiente on-premise, il Cloud Service offre ulteriori vantaggi in termini di scalabilità automatica ed efficienza in termini di costi.

<!--**Where is data processed?**

**Who has access to data?**

**Is data encrypted?**

**Where is data hosted?** -->

**È possibile eseguire più operazioni batch contemporaneamente?**
Sì, è possibile eseguire più operazioni batch contemporaneamente. Utilizzare sempre cartelle di origine e di destinazione diverse per ogni operazione per evitare conflitti.
