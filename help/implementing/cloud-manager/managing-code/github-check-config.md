---
title: Controlli della richiesta pull per archivi privati
description: Scopri come controllare le pipeline create automaticamente per convalidare ogni richiesta pull in un archivio privato.
exl-id: 3ae3c19e-2621-4073-ae17-32663ccf9e7b
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 30%

---

# Controlli delle richieste di pull per archivi privati {#github-check-config}

Scopri come controllare le pipeline create automaticamente per convalidare ogni richiesta pull in un archivio privato.

## Configurazione dei controlli dell’archivio privato {#configuration}

Quando si utilizzano gli [archivi privati,](private-repositories.md#using) viene creata automaticamente una [pipeline di qualità del codice full-stack](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md). Tale pipeline viene avviata ogni volta che la richiesta pull viene aggiornata.

È possibile controllare questi controlli creando un file di configurazione `.cloudmanager/pr_pipelines.yml` nel ramo predefinito dell&#39;archivio privato.

```yaml
pullRequest:
  shouldDeletePreviousComment: false
  shouldSkipCheckAnnotations: false
pipelines:
  - type: CI_CD
    template:
      programId: 1234
      pipelineId: 456
    namePrefix: Full Stack Code Quality Pipeline for PR
    importantMetricsFailureBehavior: CONTINUE
```

| Parametro | Valori possibili | Predefiniti | Descrizione |
| --- | --- | --- | --- |
| `shouldDeletePreviousComment` | `true` oppure `false` | `false` | Specifica se conservare solo l’ultimo commento con i risultati della scansione del codice in questa richiesta pull GitHub o mantenere tutto. Impostandolo su `false` (impostazione predefinita) i commenti precedenti non vengono eliminati. |
| `shouldSkipCheckAnnotations` | `true` oppure `false` | `false` | Indica se devono essere presenti o meno annotazioni aggiuntive nella richiesta di pull di GitHub. Impostandolo su `false` (impostazione predefinita), le annotazioni di controllo non vengono ignorate e vengono incluse nel feedback. |
| `type` | `CI_CD` | n/d | Definisce il comportamento delle configurazioni della pipeline CI/CD (Continuous Integration/Continuous Deployment). |
| `template.programId` | Numero intero | Non viene riutilizzata alcuna variabile di pipeline | Puoi utilizzarlo per riutilizzare le [variabili pipeline](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) impostate su una pipeline esistente creata automaticamente da ogni richiesta pull. |
| `template.pipelineId` | Numero intero | Non viene riutilizzata alcuna variabile di pipeline | Puoi utilizzarlo per riutilizzare le [variabili pipeline](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) impostate su una pipeline esistente creata automaticamente da ogni richiesta pull. |
| `namePrefix` | Stringa | `Full Stack Code Quality Pipeline for PR` | Utilizzato per impostare il prefisso del nome della pipeline creata automaticamente. |
| `importantMetricsFailureBehavior` | `CONTINUE` o `FAIL` o `PAUSE` | `CONTINUE` | Imposta il comportamento della metrica importante della pipeline<br>`CONTINUE` = Se una metrica importante non riesce, la pipeline si sposta automaticamente in avanti<br>`FAIL` = La pipeline termina con uno stato FAILED se una metrica importante non riesce<br>`PAUSE` = Il passaggio di analisi del codice riceve uno stato WAITING quando una metrica importante non riesce e deve essere ripreso manualmente |




