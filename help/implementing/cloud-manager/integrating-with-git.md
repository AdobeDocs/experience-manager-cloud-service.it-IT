---
title: Integrazione con Git
description: Integrazione con Git - Servizi cloud
translation-type: tm+mt
source-git-commit: 57206e36725e28051b2468d47da726e318bd763b

---


# Integrazione di Git con Adobe Cloud Manager {#git-integration}

Adobe Cloud Manager viene fornito con un unico repository git, utilizzato per distribuire il codice utilizzando i pipeline CI/CD di Cloud Manager. I clienti possono utilizzare il repository Git di Cloud Manager in modo immediato. I clienti possono anche integrare un repository Git locale o gestito **dai** clienti con Cloud Manager.

## Panoramica sull’integrazione Git {#git-integration-overview}

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

Questa serie video illustra diversi casi di utilizzo per l’integrazione di un repository git gestito dai clienti con Cloud Manager, tra cui:

* [Sincronizzazione iniziale](#initial-sync)
* [Strategia di riferimento](#branching-strategy)
* [Sviluppo del ramo delle funzioni](#feature-development)
* [Distribuzione di produzione](#production-deployment)
* [Sincronizzazione dei tag di rilascio](#sync-tags)

La serie video presuppone una conoscenza di base di git e gestione del controllo del codice sorgente. Per ulteriori informazioni su git, consulta le risorse [aggiuntive riportate di seguito](#additional-resources) .

>[!NOTE]
>
> I passaggi e le convenzioni di denominazione descritti in questa serie video rappresentano alcune best practice per l’utilizzo di un repository git gestito dai clienti e di Cloud Manager. Si prevede che le convenzioni e i flussi di lavoro illustrati saranno adattati per i singoli team di sviluppo.

## Sincronizzazione iniziale {#initial-sync}

Primi passi per la sincronizzazione di un repository Git gestito dai clienti con l&#39;archivio Git di Cloud Manager.

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## Strategia di riferimento {#branching-strategy}

Seguite il video seguente per apprendere le strategie di base per la ramificazione.

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## Sviluppo del ramo delle funzioni {#feature-development}

Utilizzate un ramo di funzionalità per isolare le modifiche di codice in un repository Git gestito dal cliente e sincronizzatelo con il repository Git di Cloud Manager per utilizzare una pipeline non di produzione per il test di qualità del codice e di convalida.

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## Distribuzione di produzione {#production-deployment}

Prepara il codice per una versione di produzione in un archivio git gestito dal cliente e sincronizza con il repository git di Cloud Manager per distribuirlo nell’area di visualizzazione e negli ambienti di produzione.

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## Sincronizzazione dei tag di rilascio {#sync-tags}

Sincronizzate i tag delle versioni rilasciate da un repository Git di Cloud Manager in un repository Git gestito dai clienti per fornire visibilità sul codice distribuito negli ambienti di produzione e di stage.

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## Additional Resources {#additional-resources}

* [Risorse GitHub](https://try.github.io)
* [Esercitazioni Git Atlassian](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)