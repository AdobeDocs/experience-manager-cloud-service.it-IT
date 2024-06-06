---
title: Configurazione controllo GitHub per archivi privati
description: Scopri come controllare le pipeline create automaticamente per convalidare ogni richiesta di pull in un archivio privato.
source-git-commit: 73bd693d47f37b453209208816dfed15d65e9e09
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 7%

---


# Configurazione controllo GitHub per archivi privati {#github-check-config}

Scopri come controllare le pipeline create automaticamente per convalidare ogni richiesta di pull in un archivio privato.

## Configurazione dei controlli GitHub {#configuration}

Quando si utilizza [archivi privati,](private-repositories.md#using) a [pipeline di qualità del codice full stack](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) verrà creato automaticamente. Tale pipeline viene avviata ogni volta che la richiesta pull viene aggiornata.

È possibile controllare questi controlli creando un `.cloudmanager/pr_pipelines.yml` nel ramo predefinito dell’archivio privato.

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
| `template.programID` | Intero | Non viene riutilizzata alcuna variabile di pipeline | Può essere utilizzato per riutilizzare [variabili della pipeline](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) che sono impostati su una delle pipeline esistenti create automaticamente da ogni PR. |
| `template.pipelineID` | Intero | Non viene riutilizzata alcuna variabile di pipeline | Può essere utilizzato per riutilizzare [variabili della pipeline](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) che sono impostati su una delle pipeline esistenti create automaticamente da ogni PR. |
| `namePrefix` | Stringa | `Full Stack Code Quality Pipeline for PR` | Utilizzato per impostare il nome della pipeline creata automaticamente |
| `importantMetricsFailureBehavior` | `CONTINUE` o `FAIL` o `PAUSE` | `CONTINUE` | Imposta il comportamento metrico importante della pipeline<br>`CONTINUE` = Se una metrica importante non riesce, la pipeline avanza automaticamente<br>`FAIL` = La pipeline termina con lo stato FAILED (NON RIUSCITO) se una metrica importante non riesce<br>`PAUSE` = Il passaggio di scansione del codice riceverà uno stato IN ATTESA quando una metrica importante non riesce e deve essere ripreso manualmente |
