---
title: Annotazioni verifica GitHub
description: Scopri in che modo i controlli GitHub annotano le PR negli archivi privati per fornire un feedback utile.
exl-id: 15178de8-8a8a-4300-8510-88875ad0fc8c
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 100%

---


# Annotazioni verifica GitHub {#github-annotations}

Scopri in che modo i controlli GitHub annotano le PR negli archivi privati per fornire un feedback utile.

## Panoramica {#overview}

Se stai usando [archivi privati](private-repositories.md) per il programma Cloud Manager, i controlli in GitHub vengono eseguiti automaticamente per ogni richiesta pull. Queste vengono annotate con informazioni utili per comprendere eventuali problemi con il codice il prima possibile.

![Esempio di annotazioni di controllo GitHub](assets/github-check-annotations.png)

I problemi di [Qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md) rilevati da [SonarQube](/help/implementing/cloud-manager/custom-code-quality-rules.md) sono elencati in modo chiaro.

![Esempio di annotazione del problema del codice](assets/github-check-annotations-example.png)

Viene fornita la riga di codice esatta con il problema e puoi fare clic su di essa per mostrare il codice pertinente. Queste annotazioni vengono fornite per tutti i problemi di codice, non solo per quelli modificati nella richiesta pull.

![Esempio di annotazione del problema del codice](assets/github-check-annotations-example-code.png)

Tutte le righe con annotazioni vengono aggregate nella scheda **File modificati** nella richiesta pull di GitHub. Le annotazioni per i file che non sono stati modificati nella richiesta pull vengono visualizzate nella rispettiva sezione.

![Esempio di annotazioni nella scheda File modificati](assets/github-check-annotations-files-changed.png)

## Pipeline di qualità del codice {#code-quality-pipelines}

I risultati della [qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md) sono visibili anche nella pipeline, che viene attivata automaticamente da Cloud Manager nella parte inferiore della scheda **Controlli**. È inoltre accessibile dai **Dettagli** del controllo della richiesta pull.

![Esempio di annotazioni](assets/github-check-annotations-code-quality.png)

![Esempio di annotazioni](assets/github-check-annotations-code-quality-2.png)

Puoi anche visualizzare i problemi in formato CSV. Questo può essere recuperato [visualizzando i dettagli dell’esecuzione della pipeline in Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details).
