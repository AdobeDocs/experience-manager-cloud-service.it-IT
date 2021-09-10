---
title: Integrazione con Git
description: Integrazione con Git - Cloud Services
exl-id: 57e71b8a-4546-4d7f-825c-a1637d08e608
source-git-commit: 21669a29fbfd1072b637f407f5220825c4d1edbb
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 2%

---

# Integrazione di Git con Adobe Cloud Manager {#git-integration}

Adobe Cloud Manager viene fornito con un unico archivio Git utilizzato per distribuire il codice utilizzando le pipeline CI/CD di Cloud Manager. I clienti possono utilizzare l’archivio Git di Cloud Manager preconfigurato. I clienti possono anche scegliere di integrare un archivio Git on-premise o gestito dal cliente **con Cloud Manager.**

## Panoramica dell’integrazione Git {#git-integration-overview}

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

Questa serie video illustra diversi casi d’uso relativi all’integrazione di un archivio Git gestito dal cliente con Cloud Manager, tra cui:

* [Sincronizzazione iniziale](#initial-sync)
* [Strategia di diramazione di base](#branching-strategy)
* [Sviluppo di diramazioni](#feature-development)
* [Distribuzione di produzione](#production-deployment)
* [Sincronizzazione dei tag di rilascio](#sync-tags)

La serie video si basa su una conoscenza di base della gestione di Git e del controllo del codice sorgente. Per ulteriori informazioni su Git, consulta le [risorse aggiuntive sottostanti](#additional-resources) .

>[!NOTE]
>
>I passaggi e le convenzioni di denominazione descritti in questa serie video rappresentano alcune best practice per l’utilizzo di un archivio Git gestito dal cliente e di Cloud Manager. Si prevede che le convenzioni e i flussi di lavoro descritti saranno adattati per i singoli team di sviluppo.

## Sincronizzazione iniziale {#initial-sync}

Primi passaggi per sincronizzare un archivio Git gestito dal cliente con l’archivio Git di Cloud Manager.

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## Strategia di diramazione di base {#branching-strategy}

Segui il video seguente per scoprire le strategie di base per la ramificazione.

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## Sviluppo di diramazioni {#feature-development}

Utilizza un ramo di funzionalità per isolare le modifiche di codice in un archivio Git gestito dal cliente e sincronizzalo con l’archivio Git di Cloud Manager per utilizzare una pipeline non di produzione per il test di qualità del codice e di convalida.

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## Distribuzione di produzione {#production-deployment}

Prepara il codice per una versione di produzione in un archivio Git gestito dal cliente e sincronizza con l’archivio Git di Cloud Manager per distribuire in ambienti di staging e produzione.

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## Sincronizzazione dei tag di rilascio {#sync-tags}

Sincronizza i tag di rilascio da un archivio Git di Cloud Manager in un archivio Git gestito dal cliente per fornire visibilità sul codice distribuito negli ambienti di stage e produzione.

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## Risorse aggiuntive {#additional-resources}

* [Risorse GitHub](https://try.github.io)
* [Tutorials Git Atlassian](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Foglio di riferimento Git](https://education.github.com/git-cheat-sheet-education.pdf)
