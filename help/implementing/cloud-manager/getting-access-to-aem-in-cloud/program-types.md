---
title: Programmi e tipi di programmi
description: Scopri la gerarchia di Cloud Manager e come i diversi tipi di programmi si adattano alla sua struttura e come si differenziano.
exl-id: 507df619-a5b5-419a-9e38-db77541425a2
source-git-commit: 74e17ccb93c97dd6881c9b63d9a2d784d3add430
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---


# Programmi e tipi di programmi {#understanding-programs}

Cloud Manager si basa su una gerarchia di entità. I dettagli di questo non sono fondamentali per il tuo lavoro quotidiano in Cloud Manager, ma una panoramica vi aiuterà a comprendere i programmi e a impostarne uno proprio.

![Gerarchia di Cloud Manager](assets/program-types1.png)

* **TENDA** - Questa è la parte superiore della gerarchia. A ogni cliente viene eseguito il provisioning con un tenant.
* **PROGRAMMI** - Ogni tenant dispone di uno o più programmi, [che spesso riflettono le soluzioni concesse in licenza dal cliente.](introduction-production-programs.md)
* **AMBIENTI** - Ogni programma dispone di più ambienti, ad esempio la produzione di contenuti live, uno per la gestione temporanea e uno per lo sviluppo.
   * Ogni programma può avere un solo ambiente di produzione, ma più ambienti non di produzione.
* **ARCHIVIO** - I programmi dispongono di archivi git in cui l’applicazione e il codice front-end vengono mantenuti per gli ambienti.
* **STRUMENTI E FLUSSI DI LAVORO** - Le pipeline gestiscono la distribuzione del codice dagli archivi agli ambienti, mentre altri strumenti consentono l’accesso ai registri, al monitoraggio e alla gestione dell’ambiente.

Un esempio è spesso utile per contestualizzare questa gerarchia.

* WKND Viaggi e Avventura Le aziende potrebbero essere un **inquilino** che si concentra sui supporti correlati ai viaggi.
* Il tenant WKND Travel and Adventure Enterprises potrebbe avere due **programmi**: un programma Sites per WKND Magazine e un programma Assets per WKND Media.
* I programmi WKND Magazine e WKND Media avrebbero sia sviluppo che stage e produzione **ambienti**.

## Archivio del codice sorgente {#source-code-repository}

Un programma Cloud Manager viene fornito automaticamente con il proprio archivio Git.

Per accedere all’archivio Git di Cloud Manager, gli utenti dovranno utilizzare un client Git con uno strumento a riga di comando, un client Git visivo indipendente o l’IDE scelto dall’utente, ad esempio Eclipse, IntelliJ o NetBeans.

Una volta configurato un client Git, puoi gestire l’archivio Git dall’interfaccia utente di Cloud Manager. Per informazioni su come gestire Git utilizzando l’interfaccia utente di Cloud Manager, consulta il documento [Accesso a Git.](/help/implementing/cloud-manager/managing-code/accessing-repos.md)

Per iniziare a sviluppare l’applicazione AEM Cloud, è necessario creare una copia locale del codice dell’applicazione estraendolo dall’archivio di Cloud Manager in una posizione sul computer locale.

```java
$ git clone {URL}
```

Il flusso di lavoro è quindi un flusso di lavoro git standard.

1. Un utente clona una copia locale dell’archivio Git.
1. L’utente apporta modifiche nell’archivio del codice locale.
1. Quando è pronto, l’utente ripristina l’archivio Git remoto.

L’unica differenza è che l’archivio Git remoto fa parte di Cloud Manager, che è trasparente per lo sviluppatore.

## Tipi di programmi {#program-types}

Un utente può creare un **produzione** o un programma **sandbox** programma.

* A **programma di produzione** viene creato per abilitare il traffico live per il sito.
   * Fare riferimento al documento [Introduzione ai programmi di produzione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md) per ulteriori dettagli.
* A **programma sandbox** viene generalmente creato per scopi di formazione, esecuzione di demo, abilitazione, POC o documentazione.
   * Un ambiente sandbox non è destinato a trasportare traffico live e avrà delle restrizioni che un programma di produzione non applicherà.
   * Includerà Sites e Assets e verrà fornito automaticamente con un ramo git che include codice di esempio, un ambiente di sviluppo e una pipeline non di produzione.
   * Fare riferimento al documento [Introduzione ai programmi sandbox](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md) per ulteriori dettagli.
