---
title: Architettura AEM senza testa
description: Scopri l’architettura di alto livello per Adobe Experience Manager in quanto si relaziona a una distribuzione headless. Comprendi il ruolo dei servizi Author, Preview e Publish di AEM e il modello di implementazione consigliato per le applicazioni headless.
feature: Content Fragments,GraphQL API
source-git-commit: 64b2beb4af2297e19e39ad534856bce33ffcfcf8
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---


# Architettura AEM senza testa

Un ambiente AEM tipico è costituito da Author Service, Publish Service e da un servizio di anteprima opzionale.

* **Servizio Autore** è il luogo in cui gli utenti interni creano, gestiscono e visualizzano in anteprima i contenuti.

* **Servizio di pubblicazione** è considerato l’ambiente &quot;live&quot; ed è tipicamente ciò con cui gli utenti finali interagiscono. I contenuti, dopo essere stati modificati e approvati nel servizio Author, vengono distribuiti al servizio Publish. Il modello di implementazione più comune con AEM applicazioni headless consiste nella connessione della versione di produzione dell’applicazione a un servizio AEM Publish.

* **Servizio Anteprima** funziona come **Servizio di pubblicazione**. Tuttavia, viene reso disponibile solo agli utenti interni. Questo lo rende un sistema ideale per gli approvatori per rivedere le imminenti modifiche al contenuto prima di essere reso live per gli utenti finali.

* **Dispatcher** è un server web statico integrato con il modulo dispatcher AEM. Fornisce funzionalità di caching e un altro livello di sicurezza. La **Dispatcher** si siede di fronte alla **Pubblica** e **Anteprima** servizi.

All&#39;interno di un programma as a Cloud Service AEM è possibile avere più ambienti, Dev, Stage e Prod. Ogni ambiente ha il proprio unico **Autore**, **Pubblica** e **Anteprima** servizi. Ulteriori informazioni sulla gestione [ambienti qui](/help/implementing/cloud-manager/manage-environments.md)

## Modello di pubblicazione dell’autore

Il modello di implementazione più comune con AEM applicazioni headless consiste nella connessione della versione di produzione dell’applicazione a un servizio AEM Publish.

![Architettura di pubblicazione di authoring](assets/autho-publish-architecture-diagram.png)

Il diagramma riportato sopra mostra questo pattern di distribuzione comune.

1. A **Autore del contenuto** utilizza il servizio Author di AEM per creare, modificare e gestire i contenuti.
1. La **Autore del contenuto** e altri utenti interni possono visualizzare in anteprima il contenuto direttamente sul servizio Author. È possibile impostare una versione di anteprima dell’applicazione che si connette al servizio Author.
1. Una volta approvato, il contenuto può essere pubblicato nel servizio AEM Publish.
1. La **Dispatcher** è un livello davanti alla **Pubblica** servizio che può memorizzare in cache determinate richieste e fornisce un livello di sicurezza.
1. Gli utenti finali interagiscono con la versione Produzione dell’applicazione. L’applicazione Production si connette al servizio Publish tramite Dispatcher e utilizza le API GraphQL per richiedere e utilizzare i contenuti.

## Implementazione pubblicazione anteprima autore

Un’altra opzione per le distribuzioni headless consiste nell’incorporare un’ **Anteprima AEM** servizio. Con questo approccio, il contenuto può essere pubblicato prima nella **Anteprima** e una versione di anteprima dell&#39;applicazione headless può connettersi ad esso. Il vantaggio di questo approccio è che la **Anteprima** è possibile impostare il servizio con gli stessi requisiti e le stesse autorizzazioni di autenticazione del **Pubblica** per simulare più facilmente l&#39;esperienza di produzione.

![Architettura di anteprima e pubblicazione dell’autore](assets/author-preview-publish-architecture-diagram.png)

1. A **Autore del contenuto** utilizza il servizio Author di AEM per creare, modificare e gestire i contenuti.
1. Il contenuto viene pubblicato per la prima volta nel servizio Anteprima AEM.
1. È possibile impostare una versione di anteprima dell&#39;applicazione che si connette al servizio Preview.
1. Una volta rivisto e approvato il contenuto, questo può essere pubblicato nel servizio AEM Publish.
1. Gli utenti finali interagiscono con la versione Produzione dell’applicazione. L’applicazione Production si connette al servizio Publish tramite Dispatcher e utilizza le API GraphQL per richiedere e utilizzare i contenuti.

