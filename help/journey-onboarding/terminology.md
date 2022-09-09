---
title: Terminologia as a Cloud Service AEM
description: Prima di accedere ad AEMaaCS, è utile comprendere alcuni termini del sistema e la sua struttura di base.
exl-id: d02776a7-836a-4894-a5d5-ae88cc7e4e76
source-git-commit: 097c17b37cc308dc906cd4af7dc7c5d51862bdfa
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 18%

---

# Terminologia as a Cloud Service AEM {#terminology}

In questa parte del [percorso di bordo,](overview.md) imparerai alcuni dei termini di AEM as a Cloud Service e la sua struttura di base.

## Obiettivo {#objective}

Ora che si capisce cosa ha portato al processo di onboarding leggendo il documento [Preparazione all&#39;onboarding,](preparation.md) è utile comprendere alcuni termini del sistema e la sua struttura di base prima di effettuare l&#39;accesso.

AEM as a Cloud Service è uno strumento potente e flessibile e per utilizzare qualsiasi strumento si dovrebbe avere familiarità con la sua organizzazione e la terminologia e la lingua utilizzati per descriverlo. Questo documento riepiloga alcuni termini chiave da comprendere prima di iniziare a utilizzare il sistema.

Dopo aver letto questo documento capirete:

* I diversi livelli che compongono AEMaaCS.
* Nozioni di base su ogni livello.

## Struttura di AEMaaCS {#structure}

Ai fini del presente percorso di onboarding non è necessaria una comprensione completa della struttura di AEM as a Cloud Service. Ma la familiarità con i seguenti concetti renderà più facile seguire più avanti nel percorso.

![Struttura di Cloud Manager](/help/journey-sites/quick-site/assets/cloud-manager-structure.png)

* **TENANT**: per ogni cliente viene eseguito il provisioning con un tenant. Un tenant viene anche indicato come organizzazione IMS (ulteriori informazioni su IMS più avanti in questo percorso)
* **PROGRAMMI**: ogni tenant dispone di uno o più programmi che spesso riflettono le soluzioni concesse in licenza dal cliente.
* **AMBIENTI**: ogni programma dispone di più ambienti, ad esempio la produzione di contenuti live, uno per la gestione temporanea e uno per lo sviluppo.
* **ARCHIVIO** - Gli ambienti dispongono di uno o più archivi Git in cui vengono mantenuti l’applicazione e il codice front-end.
* **STRUMENTI E FLUSSI DI LAVORO**: le pipeline gestiscono la distribuzione del codice dagli archivi agli ambienti.

Un esempio è spesso utile per contestualizzare questa gerarchia.

* WKND Travel and Adventure Enterprises potrebbe essere un **tenant** che si occupa di media legati ai viaggi.
* Il tenant WKND Travel and Adventure Enterprises potrebbe avere due **programmi**:
   * Programma One Sites per la sua divisione WKND Magazine
   * Programma One Assets per la divisione WKND Media
* I programmi WKND Magazine e WKND Media avrebbero sia lo sviluppo, la gestione temporanea che la produzione **ambienti**.
* **Repository** vengono utilizzati per mantenere il codice personalizzato e le applicazioni per WKND Magazine e WKND Media.
* Varie **strumenti e flussi di lavoro** lavorare tra i repository per distribuire il codice utilizzando pipeline CI/CD, log di accesso, AEM di accesso, ecc.

## Novità {#what-is-next}

Ora che hai completato questa parte del percorso di onboarding AEM devi capire:

* I diversi livelli che compongono AEMaaCS.
* Nozioni di base su ogni livello.

Sviluppa questa conoscenza e continua il tuo percorso di onboarding AEM leggendo il documento successivo [Accesso all’Admin Console](admin-console.md): scopri come accedere alla console e verificare il tuo stato di amministratore di sistema.
