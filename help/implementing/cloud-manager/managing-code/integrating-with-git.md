---
title: Utilizzo di Git con Cloud Manager
description: Scopri come utilizzare gli archivi Git di Cloud Manager e come integrare con Cloud Manager un proprio archivio Git gestito dai clienti on-premise.
exl-id: 57e71b8a-4546-4d7f-825c-a1637d08e608
source-git-commit: a9303c659730022b7417fc9082dedd26d7cbccca
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 3%

---

# Utilizzo di Git con Cloud Manager {#git-integration}

Adobe Cloud Manager viene fornito con un unico archivio Git utilizzato per distribuire il codice utilizzando le pipeline CI/CD di Cloud Manager.

Puoi utilizzare l’archivio Git di Cloud Manager fin dall’inizio, ma puoi anche scegliere di integrare un archivio Git gestito dal cliente con Cloud Manager.

## Panoramica dell’integrazione Git {#git-integration-overview}

Questa serie video esplora diversi casi d’uso durante l’integrazione di un archivio Git gestito dal cliente con Cloud Manager, tra cui:

* [Sincronizzazione iniziale](#initial-sync)
* [Strategia di diramazione di base](#branching-strategy)
* [Sviluppo di diramazioni](#feature-development)
* [Distribuzione di produzione](#production-deployment)
* [Sincronizzazione dei tag di rilascio](#sync-tags)

La serie video si basa su una conoscenza di base della gestione di Git e del controllo del codice sorgente. Consulta la sezione [risorse aggiuntive di seguito](#additional-resources) per ulteriori dettagli su git.

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

I passaggi e le convenzioni di denominazione descritti in questa serie video rappresentano alcune best practice per l’utilizzo di un archivio Git gestito dal cliente in Cloud Manager. Si prevede che le convenzioni e i flussi di lavoro descritti siano adattati per casi d’uso individuali.

## Sincronizzazione iniziale {#initial-sync}

In questo video, scopri i primi passaggi per sincronizzare un archivio Git gestito dal cliente con l’archivio Git di Cloud Manager.

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## Strategia di diramazione di base {#branching-strategy}

In questo video, scopri le strategie di base per il ramo.

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## Sviluppo di diramazioni {#feature-development}

Utilizza un ramo di funzionalità per isolare le modifiche di codice in un archivio Git gestito dal cliente e sincronizzalo con l’archivio Git di Cloud Manager per utilizzare una pipeline non di produzione per il test di qualità del codice e di convalida.

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## Distribuzione di produzione {#production-deployment}

Prepara il codice per una versione di produzione in un archivio Git gestito dal cliente e sincronizza con l’archivio Git di Cloud Manager per distribuire in ambienti di staging e produzione.

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## Sincronizzazione dei tag di rilascio {#sync-tags}

Sincronizza i tag di rilascio da un archivio Git di Cloud Manager in un archivio Git gestito dal cliente per fornire visibilità sul codice distribuito negli ambienti di staging e produzione.

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## Risorse aggiuntive {#additional-resources}

* [Risorse GitHub](https://try.github.io)
* [Tutorials Git Atlassian](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Foglio di riferimento Git](https://education.github.com/git-cheat-sheet-education.pdf)
