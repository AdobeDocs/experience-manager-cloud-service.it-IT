---
title: Utilizzare Git con Cloud Manager
description: Scopri come utilizzare gli archivi Git di Cloud Manager e come integrare un archivio Git personalizzato e gestito dal cliente on-premise con Cloud Manager.
exl-id: 57e71b8a-4546-4d7f-825c-a1637d08e608
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 100%

---

# Utilizzare Git con Cloud Manager {#git-integration}

Adobe Cloud Manager viene fornito con un unico archivio Git utilizzato per distribuire il codice attraverso le pipeline CI/CD di Cloud Manager.

Puoi utilizzare l’archivio Git di Cloud Manager con le impostazioni predefinite, ma anche scegliere di integrare un archivio Git gestito dal cliente con Cloud Manager.

## Panoramica dell’integrazione Git {#git-integration-overview}

Questa serie di video analizza diversi casi d’uso relativi all’integrazione di un archivio Git gestito dal cliente con Cloud Manager, tra cui:

* [Sincronizzazione iniziale](#initial-sync)
* [Strategia di base per la ramificazione](#branching-strategy)
* [Sviluppo dei rami delle funzioni](#feature-development)
* [Implementazione nell’ambiente di produzione](#production-deployment)
* [Sincronizzazione dei tag della versione](#sync-tags)

La serie di video presume una conoscenza di base di Git e della gestione del controllo del codice sorgente. Per ulteriori informazioni su Git, consulta la sezione [Risorse aggiuntive in basso](#additional-resources).

>[!VIDEO](https://video.tv.adobe.com/v/37354?captions=ita)

I passaggi e le convenzioni di denominazione descritti in questa serie di video rappresentano alcune best practice per l’utilizzo di un archivio Git gestito dal cliente in Cloud Manager. Le convenzioni e i flussi di lavoro descritti devono essere adattati ai casi d’uso individuali.

## Sincronizzazione iniziale {#initial-sync}

In questo video scoprirai i primi passaggi per sincronizzare un archivio Git gestito dal cliente con l’archivio Git di Cloud Manager.

>[!VIDEO](https://video.tv.adobe.com/v/37352/?captions=ita&quality=12)

## Strategia di diramazione di base {#branching-strategy}

In questo video scoprirai le strategie di base per la ramificazione.

>[!VIDEO](https://video.tv.adobe.com/v/37351/?captions=ita&quality=12)

## Sviluppo di rami delle funzioni {#feature-development}

Usa un ramo della funzione per isolare le modifiche apportate al codice in un archivio Git gestito dal cliente e sincronizzale con l’archivio Git di Cloud Manager, per utilizzare una pipeline di non produzione a scopi di test di qualità del codice e di convalida.

>[!VIDEO](https://video.tv.adobe.com/v/37349/?captions=ita&quality=12)

## Distribuzione in produzione {#production-deployment}

Prepara il codice per una versione di produzione in un archivio Git gestito dal cliente e sincronizzalo con l’archivio Git di Cloud Manager, per l’implementazione negli ambienti di staging e di produzione.

>[!VIDEO](https://video.tv.adobe.com/v/37348/?captions=ita&quality=12)

## Sincronizzare i tag della versione {#sync-tags}

Sincronizza i tag della versione da un archivio Git di Cloud Manager in un archivio Git gestito dal cliente, per fornire visibilità sul codice implementato negli ambienti di staging e di produzione.

>[!VIDEO](https://video.tv.adobe.com/v/37346/?captions=ita&quality=12)

## Risorse aggiuntive {#additional-resources}

* [Risorse GitHub](https://docs.github.com/en/get-started/getting-started-with-git/set-up-git)
* [Tutorial Atlassian Git](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Scheda di riferimento rapido di Git](https://education.github.com/git-cheat-sheet-education.pdf)
