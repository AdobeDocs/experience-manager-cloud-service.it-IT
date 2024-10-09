---
title: Configurazione verifica GitHub per archivi privati
description: Scopri come controllare le pipeline create automaticamente per convalidare ogni richiesta pull in un archivio privato.
exl-id: 3ae3c19e-2621-4073-ae17-32663ccf9e7b
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 6eabf593a7566129d32d9a5888cc480117bef51f
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 63%

---

# Configurazione verifica GitHub per archivi privati {#github-check-config}

Scopri come controllare le pipeline create automaticamente per convalidare ogni richiesta pull in un archivio privato.

## Configurazione delle verifiche GitHub {#configuration}

Quando si utilizzano gli [archivi privati,](private-repositories.md#using) viene creata automaticamente una [pipeline di qualità del codice full-stack](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md). Tale pipeline viene avviata ogni volta che la richiesta pull viene aggiornata.

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
| `shouldDeletePreviousComment` | `true` oppure `false` | `false` | Se conservare solo l’ultimo commento insieme ai risultati della scansione del codice in questa richiesta pull di GitHub o mantenerli tutti |
| `type` | `CI_CD` | n/d | Definisce il comportamento di una pipeline CI/CD |
| `template.programID` | Numero intero | Non viene riutilizzata alcuna variabile di pipeline | Puoi utilizzarlo per riutilizzare le [variabili pipeline](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) impostate su una pipeline esistente creata automaticamente da ogni richiesta pull. |
| `template.pipelineID` | Numero intero | Non viene riutilizzata alcuna variabile di pipeline | Puoi utilizzarlo per riutilizzare le [variabili pipeline](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) impostate su una pipeline esistente creata automaticamente da ogni richiesta pull. |
| `namePrefix` | Stringa | `Full Stack Code Quality Pipeline for PR` | Utilizzata per impostare il nome della pipeline creata automaticamente |
| `importantMetricsFailureBehavior` | `CONTINUE` o `FAIL` o `PAUSE` | `CONTINUE` | Imposta il comportamento della metrica importante della pipeline<br>`CONTINUE` = Se una metrica importante non riesce, la pipeline si sposta automaticamente in avanti<br>`FAIL` = La pipeline termina con uno stato FAILED se una metrica importante non riesce<br>`PAUSE` = Il passaggio di analisi del codice riceve uno stato WAITING quando una metrica importante non riesce e deve essere ripreso manualmente |
