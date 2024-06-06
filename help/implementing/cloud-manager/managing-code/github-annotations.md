---
title: Annotazioni di controllo GitHub
description: Scopri in che modo i controlli GitHub annotano le PR negli archivi privati per fornirti un feedback utile.
exl-id: 15178de8-8a8a-4300-8510-88875ad0fc8c
source-git-commit: f7348d388918a31d255babcfb64b3dc547153d62
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# Annotazioni di controllo GitHub {#github-annotations}

Scopri in che modo i controlli GitHub annotano le PR negli archivi privati per fornirti un feedback utile.

## Panoramica {#overview}

Se sta usando [archivi privati](private-repositories.md) per il programma Cloud Manager, i controlli in GitHub vengono eseguiti automaticamente per ogni richiesta pull. Queste vengono annotate con informazioni utili per comprendere al più presto eventuali problemi con il codice.

![Esempio di annotazioni di controllo GitHub](assets/github-check-annotations.png)

[Qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md) problemi rilevati da [SonarQube](/help/implementing/cloud-manager/custom-code-quality-rules.md) sono chiaramente elencati.

![Esempio di annotazione del problema del codice](assets/github-check-annotations-example.png)

Viene fornita la riga di codice esatta con il problema e puoi fare clic su di essa per mostrare il codice pertinente. Queste annotazioni vengono fornite per tutti i problemi di codice, non solo per quelli modificati nella richiesta di pull.

![Esempio di annotazione del problema del codice](assets/github-check-annotations-example-code.png)

Tutte le righe con annotazioni vengono aggregate nel **File modificati** nella richiesta pull di GitHub. Le annotazioni per i file che non sono stati modificati nella richiesta di pull vengono visualizzate nella rispettiva sezione.

![Esempio di annotazioni nella scheda File modificati](assets/github-check-annotations-files-changed.png)

## Pipeline di qualità del codice {#code-quality-pipelines}

Il [qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md) I risultati sono visibili anche nella pipeline, che viene attivata automaticamente da Cloud Manager nella parte inferiore della sezione **Verifiche** scheda. È inoltre accessibile dalla **Dettagli** del controllo della richiesta di pull.

![Esempio di annotazioni](assets/github-check-annotations-code-quality.png)

![Esempio di annotazioni](assets/github-check-annotations-code-quality-2.png)

Puoi anche visualizzare i problemi sotto forma di CSV. Questa può essere recuperata da [visualizzazione dei dettagli dell’esecuzione della pipeline in Cloud Manager.](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details)
