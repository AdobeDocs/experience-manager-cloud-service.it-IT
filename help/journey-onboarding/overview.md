---
title: Introduzione al percorso di onboarding di AEM as a Cloud Service
description: Inizia qui per una panoramica del percorso guidato nel processo di onboarding di AEM as a Cloud Service.
exl-id: 892577db-05dc-49ff-bb2c-203efdb89c8c
source-git-commit: 5c5db0d133adfbbb678930ef27d8ade10fd0c3be
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 95%

---


# Percorso di onboarding {#onboarding-journey}

Congratulazioni per aver scelto AEM as a Cloud Service. Questo documento è il punto di partenza del percorso guidato nel processo di onboarding. Che tu debba distribuire una nuova applicazione o eseguire la migrazione di una esistente, con questo percorso di onboarding potrai configurare i team e consentire l’accesso a AEM as a Cloud Service.

## Introduzione {#introduction}

L’onboarding è il processo durante il quale l’amministratore di sistema designato configura AEM as a Cloud Service per l’organizzazione. Nelle operazioni sono inclusi il provisioning iniziale delle risorse cloud e l’assegnazione degli utenti ai ruoli in base alle rispettive responsabilità lavorative. In questo modo ogni membro può collegarsi e accedere alle risorse di AEM as a Cloud Service.

![Percorso di onboarding](/help/journey-onboarding/assets/onboarding-journey.png)

Questa guida affronta i più importanti argomenti relativi all’onboarding. Dopo aver concluso il percorso:

* Comprenderai a pieno i diversi termini, servizi e utenti coinvolti nel processo di onboarding.
* Avrai configurato il team per iniziare le operazioni e svolto i primi passaggi per imparare a creare e sviluppare contenuti per l’applicazione AEM as a Cloud Service.

Di conseguenza:

* Il team sarà configurato per accedere alle risorse cloud.
* Gli autori e le autrici AEM avranno accesso a AEM as a Cloud Service e potranno iniziare a creare contenuti.
* Il team di sviluppo AEM e gli utenti con ruolo di Responsabile dell’implementazione avranno accesso a AEM as a Cloud Service e potranno iniziare a creare e distribuire applicazioni personalizzate.

## Concetti e obiettivo {#concepts}

Sebbene possa sembrare che vi siano molte informazioni da apprendere quando si inizia con AEM as a Cloud Service, concettualmente i blocchi logici sono pochi.

* **Contratto**: è necessario avere familiarità con il contratto sottoscritto con Adobe in quanto definisce gli aspetti del processo di onboarding.
* **Admin Console**: l’ambiente dove si gestiscono gli utenti e si assegnano i ruoli.
* **Cloud Manager**: lo strumento per configurare risorse quali programmi e ambienti. Da Cloud Manager puoi accedere a Git e creare pipeline per gestire e distribuire il codice personalizzato.

Questi concetti sono descritti dettagliatamente in questo percorso di onboarding. L’obiettivo è che, alla fine del percorso, tu abbia:

* consentito agli utenti necessari l’accesso a AEMaaCS;
* configurato le prime risorse cloud per il progetto;
* scoperto come distribuire il codice per la prima volta e creato il primo contenuto.

In pratica, tutto ciò che serve per iniziare al meglio un nuovo progetto AEM as a Cloud Service.

## Pubblico {#audience}

Il percorso di onboarding è destinato specificatamente agli **amministratori di sistema** dei clienti che hanno poca esperienza con AEM as a Cloud Service e con AEM in generale. L’amministratore di sistema è la persona che viene contattata per la prima volta da Adobe dopo la firma del contratto per AEM as a Cloud Service e in genere è la prima persona ad accedere e configurare le risorse di AEM as a Cloud Service. Se stai leggendo questo documento, è probabile che l’amministratore di sistema sia tu.

L’amministratore di sistema gestisce tutti gli aspetti degli utenti di AEMaaCS dell’organizzazione, dall’accesso alle autorizzazioni. Tuttavia, l’amministratore di sistema deve interagire con altre persone durante il percorso.

| Persona | Descrizione | Ruolo nel percorso |
|---|---|---|
| Amministratore di sistema | Destinatario di questo percorso, fornisce il provisioning iniziale delle risorse cloud e assegna gli utenti ai ruoli appropriati in base alle rispettive responsabilità lavorative. | Gestione di tutti gli aspetti relativi agli utenti, dall’accesso alle autorizzazioni. |
| Autore di contenuti | Crea e rivede i contenuti in AEM. | Dopo aver ricevuto le autorizzazioni dall’amministratore di sistema, gli autori e le autrici possono iniziare il percorso per la creazione di contenuti. |
| Sviluppatore | Sviluppa le applicazioni AEM che utilizzano contenuti provenienti da fonti diverse. | Dopo aver ricevuto le autorizzazioni dall’amministratore di sistema, gli sviluppatori e le sviluppatrici possono iniziare il percorso per lo sviluppo di soluzioni. |
| Responsabile dell’implementazione | Aggiunge o aggiorna un ambiente, esegue le pipeline e distribuisce il codice nell’ambiente AEM o per la verifica della qualità del codice. | Dopo aver ricevuto le autorizzazioni dall’amministratore di sistema, i e le responsabili dell’implementazione possono iniziare il percorso per la gestione delle distribuzioni. |

Questa guida all’onboarding descrive l’intero processo di onboarding come amministratore di sistema. I ruoli Utenti di AEM, Sviluppatore e Responsabile dell’implementazione sono brevemente descritti come parti aggiuntive e facoltative del percorso.

>[!TIP]
>
>Se hai poca esperienza con AEM as a Cloud Service ma conosci già AEM e stai eseguendo la migrazione da on-premise o Adobe Managed Services, assicurati di consultare il documento [Percorso di migrazione di AEM as a Cloud Service.](/help/journey-migration/getting-started.md)

## Panoramica del percorso di onboarding {#overview}

I seguenti articoli descrivono in dettaglio i concetti fondamentali dell’onboarding e forniscono informazioni fondamentali su AEM as a Cloud Service. Sebbene tu possa accedere direttamente a una sezione specifica del percorso, molti concetti si basano su quelli degli articoli precedenti. Pertanto, se per te l’onboarding è un argomento nuovo, ti consigliamo di partire dall’inizio e di procedere in sequenza.

| # | Articolo | Descrizione | Pubblico |
|---|---|---|---|
| 0 | Percorso di onboarding | Questo documento | Amministratore di sistema |
| 1 | [Preparazione all’onboarding](preparation.md) | Prima dell’inizio del processo di onboarding e di effettuare l’accesso al sistema è necessario che l’amministratore comprenda una serie di passaggi preparatori. | Amministratore di sistema |
| 2 | [Terminologia di AEM as a Cloud Service](terminology.md) | Prima di accedere a AEMaaCS per la prima volta è utile comprendere alcuni termini del sistema e la relativa struttura di base. | Amministratore di sistema |
| 3 | [Admin Console](admin-console.md) | Scopri Admin Console, come effettuare l’accesso e come verificare il tuo profilo come amministratore di sistema. | Amministratore di sistema |
| 4 | [Assegnazione dei profili di prodotto di Cloud Manager](assign-profiles-cloud-manager.md) | Scopri i profili di prodotto di Cloud Manager e come assegnarli ai membri del gruppo. | Amministratore di sistema |
| 5 | [Accesso a Cloud Manager](cloud-manager.md) | Scopri come accedere a Cloud Manager per configurare le risorse del progetto. | Amministratore di sistema |
| 6 | [Creazione di un programma](create-program.md) | Scopri come creare un programma con Cloud Manager. | Amministratore di sistema |
| 7 | [Creazione di ambienti](create-environments.md) | Scopri come creare un ambiente con Cloud Manager. | Amministratore di sistema |
| 8 | [Assegnazione dei profili di prodotto di AEM](assign-profiles-aem.md) | Scopri come assegnare i membri del gruppo ai profili di prodotto di AEM as a Cloud Service come amministratore di sistema. | Amministratore di sistema |
| 9 | [Attività dei ruoli Sviluppatore e Responsabile dell’implementazione](developers.md) | Facoltativo: scopri come accedere e gestire l’archivio Git di Cloud Manager come utente con ruolo Sviluppatore e come configurare le pipeline e distribuire il codice in Cloud Manager come utente con ruolo Responsabile dell’implementazione. | Ruoli Sviluppatore e Responsabile dell’implementazione |
| 10 | [Attività degli utenti AEM](aem-users.md) | Facoltativo: scopri come accedere all’istanza di AEM as a Cloud Service come autore o autrice AEM e come acquisire familiarità con l’authoring dei contenuti per AEM as a Cloud Service. | Utenti AEM |

## Passaggio successivo {#what-is-next}

Ora puoi iniziare il percorso di onboarding di AEM as a Cloud Service. Ti invitiamo a continuare con la sezione successiva del percorso e a leggere l’articolo [Preparazione all’onboarding](preparation.md)

## Percorsi di documentazione AEM {#documentation-journeys}

[Un percorso di documentazione](/help/journey-documentation/documentation-journeys.md) unisce molti argomenti e caratteristiche diversi e forse complicati, fornendo un resoconto che aiuta il lettore, che potrebbe essere un nuovo utente di AEM, a capire e risolvere un problema di business dall’inizio alla fine, supponendo una conoscenza minima pregressa dell’argomento o di AEM.

I percorsi di documentazione sono progettati in base ai principi delle best practice, alla luce delle ultime ricerche condotte da Adobe, della comprovata esperienza nell’implementazione da parte di consulenti di Adobe e del feedback raccolto sui progetti dei clienti.

Se desideri conoscere i consigli di Adobe su come procedere all’onboarding del team nella nuova applicazione AEM as a Cloud Service, inizia da qui.

## Risorse aggiuntive {#additional-resources}

Di seguito sono riportate ulteriori risorse facoltative, se desideri andare oltre il contenuto del percorso di onboarding.

* [Suggerimenti e trucchi per AEM Champion - Playbook di Onboarding di Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/onboarding-playbook.md) - Guarda questo video per imparare i suggerimenti di onboarding di Cloud Manager e il trucco da un campione AEM.
