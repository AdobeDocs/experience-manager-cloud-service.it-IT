---
title: Scopri come i microservizi di risorse possono elaborare le risorse digitali nel cloud
description: Elabora le risorse digitali tramite microservizi di elaborazione delle risorse scalabili e nativi basati sul cloud.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0686acbc61b3902c6c926eaa6424828db0a6421a
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 3%

---


# Panoramica dell’assimilazione e dell’elaborazione delle risorse con i microservizi {#asset-microservices-overview}

<!--
First half of content at https://git.corp.adobe.com/aklimets/project-nui/blob/master/docs/Project-Nui-Asset-Compute-Service.md is useful for this article.
TBD: Post-GA we will provide detailed information at \help\assets\asset-microservices-configure-and-use.md. However, for GA, all information is added, in short, in this article.
-->

Adobe Experience Manager come servizio Cloud fornisce un metodo nativo per sfruttare le applicazioni e le funzionalità di Experience Manager. Uno degli elementi chiave di questa nuova architettura è l&#39;assimilazione e l&#39;elaborazione delle risorse, basata sui microservizi di asset. I microservizi delle risorse forniscono un’elaborazione scalabile e resiliente delle risorse mediante i servizi cloud. Adobe gestisce i servizi cloud per una gestione ottimale dei diversi tipi di risorse e opzioni di elaborazione. I vantaggi principali dei microservizi di risorse native per il cloud sono:

* Architettura scalabile che consente un&#39;elaborazione senza soluzione di continuità per le operazioni che richiedono risorse.
* Indicizzazione ed estrazioni di testo efficienti che non influiscono sulle prestazioni degli ambienti Experience Manager.
* Riducete al minimo la necessità di flussi di lavoro per gestire l&#39;elaborazione delle risorse nell&#39;ambiente Experience Manager. Questo consente di liberare risorse, ridurre al minimo il carico su Experience Manager e fornisce scalabilità.
* Miglioramento della resilienza dell&#39;elaborazione delle risorse. I potenziali problemi nella gestione di file atipici, come file danneggiati o file di grandi dimensioni, non influiscono più sulle prestazioni della distribuzione.
* Configurazione semplificata dell’elaborazione delle risorse per gli amministratori.
* L’impostazione di elaborazione delle risorse è gestita e gestita da Adobe per fornire la configurazione più nota per la gestione di rappresentazioni, metadati ed estrazione del testo per vari tipi di file
* Laddove possibile, vengono utilizzati i servizi di elaborazione file nativi di Adobe, che forniscono output ad alta fedeltà e una gestione [efficiente dei formati](file-format-support.md)proprietari di Adobe.
* Possibilità di configurare il flusso di lavoro di post-elaborazione per aggiungere azioni e integrazioni specifiche per l’utente.

I microservizi delle risorse consentono di evitare la necessità di strumenti e metodi di rendering di terze parti (come la transcodifica ImageMagick e FFmpeg) e di semplificare le configurazioni, fornendo al contempo funzionalità pronte all’uso per i tipi di file più comuni.

## Architettura di alto livello {#asset-microservices-architecture}

Un diagramma di architettura di alto livello illustra gli elementi chiave dell’assimilazione delle risorse, dell’elaborazione e del flusso di risorse all’interno del sistema.

<!-- Proposed DRAFT diagram for asset microservices overview - see section "Asset processing - high-level diagram" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![Acquisizione ed elaborazione di risorse con](assets/asset-microservices-overview.png "microservizi di assetAcquisizione ed elaborazione di risorse con microservizi")

Le fasi chiave dell’assimilazione e dell’elaborazione mediante i microservizi di asset sono:

* I client, come i browser Web o Adobe Asset Link, inviano una richiesta di caricamento a Experience Manager e iniziano a caricare il binario direttamente nell’archivio cloud binario.
* Al termine del caricamento binario diretto, il client invia una notifica a Experience Manager.
* Experience Manager invia una richiesta di elaborazione ai microservizi di risorse. Il contenuto della richiesta dipende dalla configurazione dei profili di elaborazione in Experience Manager che specifica quali rappresentazioni generare.
* Il back-end Assets microservices riceve la richiesta e la invia a uno o più microservizi in base alla richiesta. Ogni microservizio accede al binario originale direttamente dal cloud store binario.
* I risultati dell&#39;elaborazione, come le rappresentazioni, vengono memorizzati nell&#39;archivio cloud binario.
* Experience Manager riceve una notifica del completamento dell&#39;elaborazione con puntatori diretti ai binari generati (rappresentazioni). Le rappresentazioni generate sono disponibili in Experience Manager per la risorsa caricata.

Questo è il flusso di base dell’assimilazione e dell’elaborazione delle risorse. Se configurato, Experience Manager può anche avviare un modello di flusso di lavoro personalizzato per eseguire la post-elaborazione della risorsa. Ad esempio, esegui passaggi personalizzati specifici per il tuo ambiente, ad esempio recuperare informazioni da un sistema aziendale e aggiungere proprietà alle risorse.

Il flusso di assimilazione e di elaborazione sono concetti chiave dell’architettura dei microservizi di risorse per Experience Manager.

* **Accesso** binario diretto: Le risorse vengono trasportate (e caricate) nel Cloud Binary Store una volta configurato per gli ambienti Experience Manager, quindi AEM, i microservizi delle risorse, e infine i client possono accedervi direttamente per svolgere il proprio lavoro. Questo riduce al minimo il carico sulle reti e la duplicazione dei binari archiviati
* **Elaborazione** esternalizzata: L’elaborazione delle risorse viene effettuata al di fuori dell’ambiente AEM e ne salva le risorse (CPU, memoria) per fornire le principali funzionalità di gestione delle risorse digitali e supportare il lavoro interattivo con il sistema per gli utenti finali

## Caricamento delle risorse con accesso binario diretto {#asset-upload-with-direct-binary-access}

I client Experience Manager, che fanno parte dell&#39;offerta di prodotti, supportano tutti i caricamenti con accesso binario diretto per impostazione predefinita. tra cui il caricamento tramite l’interfaccia Web, il collegamento a risorse Adobe e l’app desktop AEM.

Potete utilizzare strumenti di caricamento personalizzati, che funzionano direttamente con le API HTTP AEM. Potete utilizzare queste API direttamente, oppure utilizzare ed estendere i seguenti progetti open-source che implementano il protocollo di caricamento:

* [Libreria di caricamento open-source](https://github.com/adobe/aem-upload)
* [Open-source, strumento da riga di comando](https://github.com/adobe/aio-cli-plugin-aem)

Per ulteriori informazioni, consultate [caricare le risorse](add-assets.md).

## Aggiunta post-elaborazione di risorse personalizzata {#add-custom-asset-post-processing}

Anche se la maggior parte dei clienti deve soddisfare tutte le proprie esigenze di elaborazione delle risorse dai microservizi configurabili, alcuni potrebbero richiedere un’ulteriore elaborazione delle risorse. Ciò è particolarmente vero se le risorse devono essere elaborate in base alle informazioni provenienti da altri sistemi tramite integrazioni. In casi come questo, è possibile utilizzare flussi di lavoro post-elaborazione personalizzati.

I flussi di lavoro post-elaborazione sono normali modelli di flussi di lavoro AEM, creati e gestiti nell’editor flussi di lavoro AEM. I clienti possono configurare i flussi di lavoro per eseguire ulteriori fasi di elaborazione su una risorsa, compreso l’utilizzo dei passaggi di flusso di lavoro out-of-the-box disponibili e dei flussi di lavoro personalizzati.

Adobe Experience Manager può essere configurato per attivare automaticamente i flussi di lavoro di post-elaborazione al termine dell’elaborazione delle risorse.

<!-- TBD asgupta, Engg: Create some asset-microservices-data-flow-diagram.
-->

>[!MORELIKETHIS]
>
>* [Introduzione all’utilizzo dei microservizi per le risorse](asset-microservices-configure-and-use.md)
>* [Formati di file supportati](file-format-support.md)
>* [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html)
>* [App desktop AEM](https://docs.adobe.com/content/help/it-IT/experience-manager-desktop-app/using/introduction.html)
>* [Documentazione Apache Oak sull&#39;accesso binario diretto](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html)

