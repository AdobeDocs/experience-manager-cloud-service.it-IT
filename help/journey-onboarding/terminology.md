---
title: Terminologia di AEM as a Cloud Service
description: Prima di accedere a AEMaaCS è utile comprendere alcuni termini del sistema e la relativa struttura di base.
exl-id: d02776a7-836a-4894-a5d5-ae88cc7e4e76
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: ht
source-wordcount: '463'
ht-degree: 100%

---

# Terminologia di AEM as a Cloud Service {#terminology}

In questa parte del [percorso di onboarding](overview.md) è riportata parte della terminologia di AEM as a Cloud Service e la relativa struttura di base.

## Obiettivo {#objective}

Ora che hai compreso le fasi preliminari del processo di onboarding leggendo il documento [Preparazione all’onboarding](preparation.md), prima di effettuare l’accesso è utile comprendere alcuni termini del sistema e la relativa struttura di base.

AEM as a Cloud Service è uno strumento potente e flessibile. Per utilizzarlo è necessario conoscere la sua struttura, la terminologia e il linguaggio impiegati per descriverlo. Questo documento riepiloga alcuni termini chiave da comprendere prima di iniziare a utilizzare il sistema.

Dopo aver letto questo documento, comprenderai

* I diversi livelli che compongono AEMaaCS.
* Le nozioni di base su ogni livello.

## Struttura di AEMaaCS {#structure}

Ai fini del presente percorso di onboarding non è necessario comprendere completamente la struttura di AEM as a Cloud Service. Tuttavia, avere familiarità con i concetti riportati di seguito faciliterà l’avanzamento nel percorso.

![Struttura di Cloud Manager](/help/journey-sites/quick-site/assets/cloud-manager-structure.png)

* **TENANT**: a ogni cliente viene fornito un tenant. I tenant vengono indicati anche come organizzazioni IMS (ulteriori informazioni su IMS sono riportate più avanti in questo percorso)
* **PROGRAMMI**: ogni tenant dispone di uno o più programmi che spesso riflettono le soluzioni concesse in licenza al cliente.
* **AMBIENTI**: ogni programma dispone di più ambienti, come ad esempio quello di produzione di contenuti live, quello di staging e quello di sviluppo.
* **ARCHIVIO**: gli ambienti dispongono di uno o più archivi Git in cui vengono conservati l’applicazione e il codice front-end.
* **STRUMENTI E FLUSSI DI LAVORO**: le pipeline gestiscono la distribuzione del codice dagli archivi agli ambienti.

Un esempio è spesso utile per contestualizzare questa gerarchia.

* WKND Travel and Adventure Enterprises potrebbe essere un **tenant** che si occupa di media legati ai viaggi.
* Il tenant WKND Travel and Adventure Enterprises potrebbe avere due **programmi**:
   * Programma One Sites per la divisione WKND Magazine
   * Programma One Assets per la divisione WKND Media
* Entrambi i programmi WKND Magazine e WKND Media includono **ambienti** di sviluppo, staging e produzione.
* Gli **archivi** vengono utilizzati per conservare le applicazioni e il codice personalizzato per WKND Magazine e WKND Media.
* Vari **strumenti e flussi di lavoro** operano negli archivi per distribuire il codice con le pipeline CI/CD, accedere ai registri, accedere ad AEM e così via.

## Passaggio successivo {#what-is-next}

Ora che hai completato questa parte del percorso di onboarding di AEM, dovresti conoscere:

* I diversi livelli che compongono AEMaaCS.
* Le nozioni di base su ogni livello.

Sviluppa le tue conoscenze e continua il percorso di onboarding di AEM leggendo il prossimo documento, [Accesso ad Admin Console](admin-console.md), dove verrà illustrato come accedere alla Console e verificare lo stato di amministratore di sistema.
