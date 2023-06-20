---
title: Utilizzo di Git con Cloud Manager
description: Scopri come utilizzare gli archivi Git di Cloud Manager e come integrare un archivio Git personalizzato e gestito dal cliente on-premise con Cloud Manager.
exl-id: 57e71b8a-4546-4d7f-825c-a1637d08e608
source-git-commit: bceec9ea6858b1c4c042ecd96f13ae5cac1bbee5
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 73%

---

# Utilizzo di Git con Cloud Manager {#git-integration}

Adobe Cloud Manager viene fornito con un unico archivio Git utilizzato per distribuire il codice attraverso le pipeline CI/CD di Cloud Manager.

Puoi utilizzare l’archivio Git di Cloud Manager con le impostazioni predefinite, ma anche scegliere di integrare un archivio Git gestito dal cliente con Cloud Manager.

## Panoramica dell’integrazione di Git {#git-integration-overview}

Questa serie di video analizza diversi casi d’uso relativi all’integrazione di un archivio Git gestito dal cliente con Cloud Manager, tra cui:

* [Sincronizzazione iniziale](#initial-sync)
* [Strategia di base per la ramificazione](#branching-strategy)
* [Sviluppo dei rami delle funzioni](#feature-development)
* [Implementazione nell’ambiente di produzione](#production-deployment)
* [Sincronizzazione dei tag della versione](#sync-tags)

La serie di video presume una conoscenza di base di Git e della gestione del controllo del codice sorgente. Per ulteriori informazioni su Git, consulta la sezione [Risorse aggiuntive in basso](#additional-resources).

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

I passaggi e le convenzioni di denominazione descritti in questa serie di video rappresentano alcune best practice per l’utilizzo di un archivio Git gestito dal cliente in Cloud Manager. Le convenzioni e i flussi di lavoro descritti devono essere adattati ai casi d’uso individuali.

## Sincronizzazione iniziale {#initial-sync}

In questo video scoprirai i primi passaggi per sincronizzare un archivio Git gestito dal cliente con l’archivio Git di Cloud Manager.

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## Strategia di base per la ramificazione {#branching-strategy}

In questo video scoprirai le strategie di base per la ramificazione.

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## Sviluppo dei rami delle funzioni {#feature-development}

Utilizza un ramo della funzione per isolare le modifiche al codice in un archivio Git gestito dal cliente e sincronizzalo con l’archivio Git di Cloud Manager per utilizzare una pipeline non di produzione per i test di qualità del codice e convalida.

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## Implementazione nell’ambiente di produzione {#production-deployment}

Prepara il codice per una versione di produzione in un archivio Git gestito dal cliente e sincronizzalo con l’archivio Git di Cloud Manager per la distribuzione negli ambienti di staging e produzione.

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## Sincronizzazione dei tag della versione {#sync-tags}

Sincronizza i tag della versione da un archivio Git di Cloud Manager in un archivio Git gestito dal cliente per fornire visibilità sul codice distribuito negli ambienti di staging e produzione.

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## Risorse aggiuntive {#additional-resources}

* [Risorse GitHub](https://try.github.io)
* [Tutorial Atlassian Git](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Scheda di riferimento rapido di Git](https://education.github.com/git-cheat-sheet-education.pdf)
