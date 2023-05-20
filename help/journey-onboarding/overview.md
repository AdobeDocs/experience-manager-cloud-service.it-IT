---
title: Introduzione al percorso di onboarding di AEM as a Cloud Service
description: Inizia qui per una panoramica del percorso guidato nel processo di onboarding di AEM as a Cloud Service.
exl-id: 892577db-05dc-49ff-bb2c-203efdb89c8c
source-git-commit: 98eff568686c72c626d2bf77d82e8c3f224eda42
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 58%

---


# Percorso di onboarding {#onboarding-journey}

Congratulazioni per aver scelto AEM as a Cloud Service. Questo documento è il punto di partenza del percorso guidato nel processo di onboarding. Che tu distribuisca una nuova applicazione o ne esegua la migrazione, questo percorso di onboarding garantisce che i team siano configurati e abbiano accesso a AEM as a Cloud Service.

## Introduzione {#introduction}

L’onboarding è il processo durante il quale l’amministratore di sistema designato configura AEM as a Cloud Service per l’organizzazione. Questo processo include il provisioning iniziale delle risorse cloud e l’assegnazione degli utenti ai ruoli in base alle loro responsabilità lavorative. Di conseguenza, ogni membro è in grado di accedere alle proprie risorse su AEM as a Cloud Service.

![Percorso di onboarding](/help/journey-onboarding/assets/onboarding-journey.png)

Questa guida descrive i più importanti argomenti relativi all’onboarding e spiega come:

* Comprenderai a pieno i diversi termini, servizi e utenti coinvolti nel processo di onboarding.
* Avrai configurato il team per iniziare le operazioni e svolto i primi passaggi per imparare a creare e sviluppare contenuti per l’applicazione AEM as a Cloud Service.

Di conseguenza:

* Il team sarà configurato e potrà accedere alle risorse cloud.
* Gli autori dell’AEM hanno accesso a AEM as a Cloud Service e possono iniziare a creare contenuti.
* Gli sviluppatori e i responsabili dell’implementazione dell’AEM possono accedere a AEM as a Cloud Service e iniziare a creare e distribuire applicazioni personalizzate.

## Concetti e obiettivo {#concepts}

Sebbene possa sembrare che vi siano molte informazioni da apprendere quando si inizia con AEM as a Cloud Service, concettualmente i blocchi logici sono pochi.

* **Il contratto** - È necessario avere familiarità con il contratto Adobe in quanto definisce gli aspetti del processo di onboarding.
* **Admin Console** : posizione in cui vengono gestiti gli utenti e assegnati i ruoli.
* **Cloud Manager** - Lo strumento per configurare risorse quali programmi e ambienti. Da Cloud Manager puoi accedere a Git e creare pipeline per gestire e distribuire il codice personalizzato.

Questi concetti sono descritti in dettaglio in questo percorso di onboarding. L’obiettivo è che, alla fine del percorso, tu abbia:

* aver concesso all’utilizzatore necessario l’accesso all’AEM as a Cloud Service.
* Hai impostato le prime risorse cloud per il progetto.
* scoperto come distribuire il codice per la prima volta e creato il primo contenuto.

Fondamentalmente, hai raggiunto il punto di partenza con il tuo nuovo progetto AEM as a Cloud Service!

## Pubblico {#audience}

Il percorso di onboarding è destinato specificatamente agli **amministratori di sistema** dei clienti che hanno poca esperienza con AEM as a Cloud Service e con AEM in generale. L’amministratore di sistema è la persona che viene contattata per la prima volta da Adobe dopo la firma del contratto as a Cloud Service dell’AEM. In genere è la prima persona ad accedere e configurare le tue risorse su AEM as a Cloud Service. Se stai leggendo questo argomento, è probabile che tu sia l’amministratore di sistema.

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
>Se hai poca esperienza con AEM as a Cloud Service e conosci AEM e stai eseguendo la migrazione da on-premise o Adobe Managed Services, assicurati di consultare [Percorso di migrazione as a Cloud Service AEM](/help/journey-migration/getting-started.md).

## Panoramica del percorso di onboarding {#overview}

I seguenti articoli descrivono in dettaglio i concetti fondamentali dell’onboarding e forniscono informazioni fondamentali su AEM as a Cloud Service. Sebbene tu possa accedere direttamente a una sezione specifica del percorso, molti concetti si basano su quelli degli articoli precedenti. Pertanto, se per te l’onboarding è un argomento nuovo, Adobe consiglia di partire dall’inizio e procedere in sequenza.

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
| 8 | [Assegnazione dei profili di prodotto di AEM](assign-profiles-aem.md) | Scopri come l’amministratore di sistema assegna i membri del gruppo ai profili di prodotto in AEM as a Cloud Service. | Amministratore di sistema |
| 9 | [Attività dei ruoli Sviluppatore e Responsabile dell’implementazione](developers.md) | Facoltativo: in qualità di sviluppatore, scopri come accedere e gestire Cloud Manager Git e come configurare le pipeline e distribuire il codice in Cloud Manager come utente con ruolo Responsabile dell’implementazione. | Ruoli Sviluppatore e Responsabile dell’implementazione |
| 10 | [Attività degli utenti AEM](aem-users.md) | Facoltativo - In qualità di autore AEM, scopri come accedere all’istanza AEM as a Cloud Service e acquisire familiarità con l’authoring dei contenuti per AEM as a Cloud Service. | Utenti AEM |

## Passaggio successivo {#what-is-next}

Ora puoi iniziare il percorso di onboarding di AEM as a Cloud Service. Ti invitiamo a passare alla parte successiva del percorso e a leggere l’articolo [Preparazione all’onboarding](preparation.md)

## Percorsi di documentazione AEM {#documentation-journeys}

[Un Percorso di documentazione](/help/journey-documentation/documentation-journeys.md) unisce molti argomenti e caratteristiche diversi e complicati. Fornisce una narrazione che aiuta un lettore che non ha mai visto l&#39;AEM a capire e risolvere un problema di business dall&#39;inizio alla fine, supponendo una conoscenza minima pregressa dell&#39;argomento o dell&#39;AEM.

I percorsi di documentazione sono progettati in base ai principi delle best practice, alla luce delle ultime ricerche condotte da Adobe, della comprovata esperienza nell’implementazione da parte di consulenti di Adobe e del feedback raccolto sui progetti dei clienti.

Se desideri conoscere i consigli dell’Adobe su come effettuare l’onboarding del team nella nuova applicazione AEM as a Cloud Service, inizia qui.

<!-- ERROR: Not Found (HTTP error 404)
## Additional Resources {#additional-resources}

The following are additional, optional resources if you would like to go beyond the content of the onboarding journey.

* [AEM Champion Tips and Tricks - Cloud Manager Onboarding Playbook](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/onboarding-playbook.md) - Watch this video to learn Cloud Manager onboarding tips and trick from an AEM champion. -->


