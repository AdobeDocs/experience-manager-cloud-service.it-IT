---
title: Introduzione al percorso di onboarding di AEM as a Cloud Service
description: Inizia qui per una panoramica del percorso guidato nel processo di onboarding di AEM as a Cloud Service.
exl-id: 892577db-05dc-49ff-bb2c-203efdb89c8c
recommendations: noDisplay
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 858a9c4b61fd3a80a257313e48816b067ca77175
workflow-type: tm+mt
source-wordcount: '1362'
ht-degree: 93%

---


# Percorso di onboarding {#onboarding-journey}

Congratulazioni per aver scelto AEM as a Cloud Service. Questo documento è il punto di partenza del percorso guidato nel processo di onboarding. Se stai implementando una nuova applicazione o stai eseguendo una migrazione, con questo percorso di onboarding puoi preparare i tuoi team. Ti consente di assicurarti che gli utenti possano accedere ad AEM as a Cloud Service.

## Introduzione {#introduction}

Adobe Experience Manager (AEM) offre flessibilità sia nell’approccio alla distribuzione dei contenuti che in quello all’authoring, consentendo ai team di scegliere il modello migliore in base alle proprie esigenze.

Utilizza [Edge Delivery Services](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/edge-delivery/overview) per l&#39;authoring rapido e iterativo e per velocizzare i contenuti, oppure utilizza il servizio di distribuzione tradizionale di pubblicazione per un modello di pubblicazione aziendale affidabile. Entrambi gli approcci consentono alle organizzazioni di fornire esperienze digitali eccezionali nel modo più adatto alle loro esigenze. Per iniziare a utilizzare Edge Delivery Services, esplorare la [Panoramica di Edge Delivery Services](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/edge-delivery/overview) e per ulteriori informazioni sulle opzioni di authoring moderne, vedere la [Guida all&#39;authoring](https://www.aem.live/docs/authoring-guide).

L’onboarding è il processo durante il quale l’amministratore di sistema designato configura AEM as a Cloud Service per l’organizzazione. Il procedimento include il provisioning iniziale delle risorse cloud e l’assegnazione degli utenti ai ruoli in base alle rispettive responsabilità lavorative. In questo modo, ogni membro può collegarsi e accedere alle proprie risorse in AEM as a Cloud Service.

![Percorso di onboarding](/help/journey-onboarding/assets/onboarding-journey.png).

Questa guida affronta i più importanti argomenti relativi all’onboarding. Dopo aver concluso il percorso:

* Comprenderai a pieno i diversi termini, servizi e utenti coinvolti nel processo di onboarding.
* Avrai configurato il team per iniziare le operazioni e svolto i primi passaggi per imparare a creare e sviluppare contenuti per l’applicazione AEM as a Cloud Service.

Di conseguenza:

* Il team sarà configurato e potrà accedere alle risorse cloud.
* Gli autoti AEM avranno accesso ad AEM as a Cloud Service e potranno iniziare a creare contenuti.
* Gli sviluppatori e i responsabili della distribuzione di AEM avranno accesso ad AEM as a Cloud Service e potranno iniziare a creare e distribuire applicazioni personalizzate.

## Concetti e obiettivo {#concepts}

<!-- Although there may appear to be a lot to learn when getting started with AEM as a Cloud Service, conceptually there are only a few, logical pieces.-->

Il percorso di onboarding per AEM as a Cloud Service è incentrato sui seguenti elementi principali:

* **Contratto**: rivedi il contratto Adobe per comprendere i dettagli chiave del processo di onboarding.
* **Experience Hub**: utilizza [experience.adobe.com](https://experience.adobe.com/) come punto di ingresso centrale per le funzionalità di AEM. Experience Hub si adatta alla all’utente tipo e ai diritti in modo da poter lavorare in modo efficiente. Da qui, passa a:
   * **Admin Console**: gestisci gli utenti e assegna i ruoli.
   * **Cloud Manager**: configura programmi e ambienti, accedi a Git e crea pipeline per gestire e distribuire il codice personalizzato.
   * **Sites**: crea, gestisci e distribuisci esperienze digitali. (Diritto basato su licenza)
   * **Risorse**: organizza, archivia e distribuisci le risorse digitali. (Diritto basato su licenza)
   * **Moduli**: crea e gestisci moduli adattivi e dinamici. (Diritto basato su licenza)

Tali concetti sono descritti dettagliatamente in questo percorso di onboarding. L’obiettivo è che, alla fine del percorso, tu possa:

* concedere agli utenti l’accesso necessario ad AEM as a Cloud Service;
* configurare le prime risorse cloud per il progetto;
* sapere come distribuire il codice per la prima volta e creare il primo contenuto.

In sostanza, tutto ciò che serve per iniziare al meglio un nuovo progetto AEM as a Cloud Service.

## Pubblico {#audience}

Il percorso di onboarding è destinato specificatamente all’**amministratore di sistema** delle organizzazioni che hanno poca esperienza con AEM as a Cloud Service e con AEM in generale. Dopo aver sottoscritto il contratto di AEM as a Cloud Service, l’amministratore di sistema è la persona che viene contattata per prima da Adobe. In genere, è la prima persona ad accedere e configurare le risorse su AEM as a Cloud Service. Se stai leggendo questo argomento, è molto probabile che tu sia l’amministratore di sistema.

L’amministratore di sistema gestisce tutti gli aspetti degli utenti di AEMaaCS dell’organizzazione, dall’accesso alle autorizzazioni. Tuttavia, l’amministratore di sistema deve interagire con altre persone durante il percorso.

| Persona | Descrizione | Ruolo nel percorso |
| --- | --- | --- |
| Amministratore di sistema | La destinazione di questo percorso fornisce il provisioning iniziale delle risorse cloud e assegna gli utenti ai ruoli appropriati in base alle rispettive responsabilità lavorative. | Il ruolo assiste nella gestione di tutti gli aspetti relativi agli utenti, dall’accesso alle autorizzazioni. |
| Autore di contenuti | Crea e rivede i contenuti in AEM. | Dopo che l’amministratore di sistema ha concesso le autorizzazioni, gli autori possono iniziare il percorso per la creazione di contenuti. |
| Sviluppatore | Sviluppa le applicazioni AEM che utilizzano contenuti provenienti da fonti diverse. | Dopo l’amministratore di sistema ha concesso le autorizzazioni, gli sviluppatori possono iniziare il percorso per lo sviluppo di soluzioni. |
| Responsabile dell’implementazione | Aggiunge o aggiorna un ambiente, esegue le pipeline e distribuisce il codice nell’ambiente AEM o per la verifica della qualità del codice. | Dopo che l’amministratore di sistema ha concesso le autorizzazioni, i manager dell’implementazione possono iniziare il percorso per la gestione delle distribuzioni. |

Questa guida all’onboarding descrive l’intero processo di onboarding come amministratore di sistema. I ruoli Utenti di AEM, Sviluppatore e Responsabile dell’implementazione sono brevemente descritti come parti aggiuntive e facoltative del percorso.

>[!TIP]
>
>Se stai usando AEM as a Cloud Service per la prima volta, ma hai familiarità con AEM e stai eseguendo la migrazione da On-Premise o da Adobe Managed Services, consulta [Percorso di migrazione ad AEM as a Cloud Service](/help/journey-migration/getting-started.md).

## Panoramica del percorso di onboarding {#overview}

I seguenti articoli descrivono in dettaglio i concetti fondamentali dell’onboarding e forniscono informazioni fondamentali su AEM as a Cloud Service. Sebbene tu possa accedere direttamente a una sezione specifica del percorso, molti concetti si basano su quelli degli articoli precedenti. Perciò, se non possiedi alcuna conoscenza del processo di onboarding, Adobe consiglia di partire dall’inizio e di avanzare progressivamente.

| | Articolo | Descrizione | Pubblico |
| --- | --- | --- | --- |
| 0 | Percorso di onboarding | Questo documento | Amministratore di sistema |
| 1 | [Preparazione all’onboarding](preparation.md) | Prima dell’inizio del processo di onboarding e di effettuare l’accesso al sistema è necessario che l’amministratore comprenda una serie di passaggi preparatori. | Amministratore di sistema |
| 2 | [Terminologia di AEM as a Cloud Service](terminology.md) | Prima di accedere a AEMaaCS per la prima volta è utile comprendere alcuni termini del sistema e la relativa struttura di base. | Amministratore di sistema |
| 3 | [Admin Console](admin-console.md) | Scopri Admin Console, come effettuare l’accesso e come verificare il tuo profilo come amministratore di sistema. | Amministratore di sistema |
| 4 | [Assegnazione dei profili di prodotto di Cloud Manager](assign-profiles-cloud-manager.md) | Esamina i profili di prodotto di Cloud Manager e scopri come assegnarli ai membri del gruppo. | Amministratore di sistema |
| 5 | [Accesso a Experience Hub](/help/experience-hub.md) | Utilizza Experience Hub, che funge da punto di ingresso unificato e personalizzato per l’ecosistema AEM. | Utenti AEM |
| 6 | [Accesso a Cloud Manager](cloud-manager.md) | Scopri come accedere a Cloud Manager per configurare le risorse del progetto. | Amministratore di sistema |
| 7 | [Creazione di un programma](create-program.md) | Scopri come creare un programma con Cloud Manager. | Amministratore di sistema |
| 8 | [Creazione di ambienti](create-environments.md) | Scopri come creare un ambiente con Cloud Manager. | Amministratore di sistema |
| 9 | [Assegnazione dei profili di prodotto di AEM](assign-profiles-aem.md) | Scopri come l’amministratore di sistema assegna i membri del gruppo ai profili di prodotto in AEM as a Cloud Service. | Amministratore di sistema |
| 10 | [Attività dei ruoli Sviluppatore e Responsabile dell’implementazione](developers.md) | Facoltativo - In qualità di sviluppatore, scopri come accedere e gestire Cloud Manager Git. Come Manager di implementazione, scopri come configurare le pipeline e distribuire il codice in Cloud Manager. | Ruoli Sviluppatore e Responsabile dell’implementazione |
| 11 | [Attività degli utenti AEM](aem-users.md) | Facoltativo: scopri come accedere all’istanza di AEM as a Cloud Service come autore o autrice AEM e come acquisire familiarità con l’authoring dei contenuti per AEM as a Cloud Service. | Utenti AEM |

## Passaggio successivo {#what-is-next}

Ora puoi iniziare il percorso di onboarding di AEM as a Cloud Service. Ti invitiamo a continuare con la sezione successiva del percorso e a leggere l’articolo [Preparazione all’onboarding](preparation.md)

## Percorsi di documentazione AEM {#documentation-journeys}

[Un percorso di documentazione](/help/journey-documentation/documentation-journeys.md) unisce molti argomenti e caratteristiche diversi e complicati. Fornisce un resoconto che aiuta chi utilizza AEM per la prima volta a capire e risolvere un problema di business dall’inizio alla fine, supponendo una conoscenza minima pregressa dell’argomento o di AEM.

I percorsi di documentazione sono progettati in base ai principi delle best practice. Sono ispirati alle ultime ricerche condotte da Adobe, alla comprovata esperienza nell’implementazione da parte dei consulenti Adobe e al feedback raccolto sui progetti dei nostri clienti.

Se desideri conoscere i consigli di Adobe su come procedere all’onboarding del team nella nuova applicazione AEM as a Cloud Service, inizia da qui.

## Risorse aggiuntive {#additional-resources}

Di seguito sono riportate risorse aggiuntive e opzionali utili per andare oltre il contenuto del percorso di onboarding.

* [Onboarding per AEM as a Cloud Service](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/migration/moving-to-aem-as-a-cloud-service/onboarding): questo breve video offre una panoramica del processo di onboarding del Cloud Service per AEM.
