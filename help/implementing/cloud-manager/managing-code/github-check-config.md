---
title: Configurazione verifica GitHub per archivi privati
description: Scopri come controllare le pipeline create automaticamente per convalidare ogni richiesta di pull in un archivio privato.
exl-id: 3ae3c19e-2621-4073-ae17-32663ccf9e7b
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 77%

---

# Configurazione verifica GitHub per archivi privati {#github-check-config}

Scopri come controllare le pipeline create automaticamente per convalidare ogni richiesta di pull in un archivio privato.

## Configurazione verifiche GitHub {#configuration}

Quando si utilizzano gli [archivi privati,](private-repositories.md#using) verrà creata automaticamente una [pipeline di qualità del codice full-stack](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md). Tale pipeline viene avviata ogni volta che la richiesta pull viene aggiornata.

È possibile verificare questi controlli creando un file `.cloudmanager/pr_pipelines.yml` nel ramo predefinito dell’archivio privato.

```yaml
github:
  shouldDeletePreviousComment: false
pipelines:
  - type: CI_CD
    template:
      programId: 1234
      pipelineId: 456
    namePrefix: Full Stack Code Quality Pipeline for PR 
    importantMetricsFailureBehavior: CONTINUE
```

| Parametro | Valori possibili | Predefiniti | Descrizione |
|---|---|---|---|
| `shouldDeletePreviousComment` | `true` oppure `false` | `false` | Se conservare solo l’ultimo commento con i risultati della scansione del codice nella sua richiesta di pull github o mantenere tutto |
| `type` | `CI_CD` | n/d | Definisce il comportamento di una pipeline CI/CD |
| `template.programID` | Numero intero | Non viene riutilizzata alcuna variabile di pipeline | Può essere utilizzato per riutilizzare [variabili della pipeline](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) che sono impostate su una delle pipeline esistenti create automaticamente da ciascuna PR. |
| `template.pipelineID` | Numero intero | Non viene riutilizzata alcuna variabile di pipeline | Può essere utilizzato per riutilizzare [variabili della pipeline](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) che sono impostate su una delle pipeline esistenti create automaticamente da ciascuna PR. |
| `namePrefix` | Stringa | `Full Stack Code Quality Pipeline for PR` | Utilizzata per impostare il nome della pipeline creata automaticamente |
| `importantMetricsFailureBehavior` | `CONTINUE` o `FAIL` o `PAUSE` | `CONTINUE` | Imposta il comportamento metrico importante della pipeline<br>`CONTINUE` = Se una metrica importante non riesce, la pipeline avanza automaticamente<br>`FAIL` = La pipeline termina con lo stato FAILED (NON RIUSCITO) se una metrica importante non riesce<br>`PAUSE` = Il passaggio di scansione del codice riceverà uno stato IN ATTESA quando una metrica importante non riesce e deve essere ripreso manualmente |
