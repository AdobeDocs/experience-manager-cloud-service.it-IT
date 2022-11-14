---
title: Programmi e tipi di programmi
description: Scopri la gerarchia di Cloud Manager, le differenze tra i diversi tipi di programmi e come si adattano alla struttura gerarchica.
exl-id: 507df619-a5b5-419a-9e38-db77541425a2
source-git-commit: 74e17ccb93c97dd6881c9b63d9a2d784d3add430
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 100%

---


# Programmi e tipi di programmi {#understanding-programs}

Cloud Manager è basato su una gerarchia di entità. Sebbene i dettagli di tale gerarchia non siano fondamentali per poter svolgere le attività quotidiane in Cloud Manager, questa panoramica ti aiuterà a comprendere i programmi e a configurarne di personalizzati.

![Gerarchia di Cloud Manager](assets/program-types1.png)

* **TENANT**: il vertice della gerarchia. A ogni cliente viene fornito un tenant.
* **PROGRAMMI**: ogni tenant dispone di uno o più programmi, [che spesso riflettono le soluzioni concesse in licenza al cliente.](introduction-production-programs.md)
* **AMBIENTI**: ogni programma dispone di più ambienti, come ad esempio quello di produzione di contenuti live, quello di staging e quello di sviluppo.
   * Ogni programma può disporre di un solo ambiente di produzione ma averne diversi non di produzione.
* **ARCHIVIO**: i programmi dispongono di archivi Git in cui vengono mantenuti l’applicazione e il codice front-end degli ambienti.
* **STRUMENTI E FLUSSI DI LAVORO**: le pipeline gestiscono la distribuzione del codice dagli archivi agli ambienti, mentre altri strumenti consentono l’accesso ai registri, il monitoraggio e la gestione degli ambienti.

Un esempio è spesso utile per contestualizzare questa gerarchia.

* WKND Travel and Adventure Enterprises potrebbe essere un **tenant** che si occupa di media legati ai viaggi.
* Il tenant WKND Travel and Adventure Enterprises potrebbe avere due **programmi**: un programma Sites per WKND Magazine e un programma Assets per WKND Media.
* I programmi WKND Magazine e WKND Media potrebbero **ambienti** sia di sviluppo sia di staging e produzione.

## Archivio del codice sorgente {#source-code-repository}

I programmi di Cloud Manager vengono forniti automaticamente con il relativo archivio Git.

Per accedere all’archivio Git di Cloud Manager è necessario utilizzare un client Git con uno strumento da riga di comando, un client Git visivo indipendente o l’IDE scelto dall’utente, ad esempio Eclipse, IntelliJ o NetBeans.

Una volta configurato il client Git, puoi gestire l’archivio Git dall’interfaccia utente di Cloud Manager. Per informazioni su come gestire l’archivio Git con l’interfaccia utente di Cloud Manager, consulta il documento [Accesso a Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md).

Per iniziare a sviluppare l’applicazione AEM Cloud è necessario creare una copia locale del codice dell’applicazione estraendolo dall’archivio di Cloud Manager nel computer locale.

```java
$ git clone {URL}
```

Il flusso di lavoro corrisponde a quello standard di Git.

1. L’utente clona una copia locale dell’archivio Git.
1. L’utente apporta le modifiche nell’archivio del codice locale.
1. Una volta completata l’operazione, l’utente ripristina l’archivio Git remoto.

L’unica differenza consiste nel fatto che l’archivio Git remoto fa parte di Cloud Manager, che è chiaro per chi sviluppa.

## Tipi di programmi {#program-types}

L’utente può creare un programma di **produzione** o un programma **sandbox**.

* Un **programma di produzione** viene creato per abilitare il traffico in tempo reale per il sito.
   * Per ulteriori informazioni, consulta il documento [Introduzione ai programmi di produzione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md).
* I **programmi sandbox** vengono generalmente creati a scopi di formazione, esecuzione di demo, abilitazione, POC o documentazione.
   * Gli ambienti sandbox non sono concepiti per il traffico in tempo reale e presentano delle limitazioni non riscontrate nei programmi di produzione.
   * Gli ambienti sandbox includono Sites e Assets e vengono forniti automaticamente con un ramo Git che include il codice di esempio, un ambiente di sviluppo e una pipeline non di produzione.
   * Per ulteriori informazioni, consulta il documento [Introduzione ai programmi Sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md).
