---
title: Introduzione al Percorso di onboarding as a Cloud Service AEM
description: Inizia qui per una panoramica del percorso guidato nel processo di onboarding di AEM as a Cloud Service.
exl-id: 892577db-05dc-49ff-bb2c-203efdb89c8c
source-git-commit: 75c0e8cbaa409fa48750e794c27ace98eda107d0
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 19%

---


# Percorso di onboarding {#onboarding-journey}

Congratulazioni per aver scelto AEM as a Cloud Service! Questo documento è il punto di partenza per un percorso guidato attraverso il processo di onboarding. Che tu stia distribuendo una nuova applicazione o ne esegua la migrazione, questo percorso di onboarding assicura che i team siano configurati e abbiano accesso a AEM as a Cloud Service.

## Introduzione {#introduction}

L&#39;onboarding è il processo durante il quale un amministratore di sistema designato imposta AEM as a Cloud Service per la tua organizzazione. Ciò include il provisioning iniziale delle risorse cloud e l’assegnazione di utenti a ruoli in base alle loro responsabilità lavorative. Di conseguenza, ogni membro è in grado di accedere e accedere alle risorse AEM as a Cloud Service.

![Percorso di onboarding](/help/journey-onboarding/assets/onboarding-journey.png)

Questa guida ti guida attraverso i più importanti argomenti relativi all’onboarding, in modo che al termine avrai a disposizione:

* Comprensione completa dei diversi termini, servizi e utenti coinvolti nel processo di onboarding.
* Preparare il tuo team affinché possa iniziare e seguire i primi passi per imparare a creare e sviluppare contenuti per la tua applicazione AEM as a Cloud Service.

Di conseguenza:

* Il team verrà configurato e avrà accesso alle risorse cloud.
* AEM gli autori avranno accesso a AEM as a Cloud Service e possono iniziare a creare contenuti.
* Gli sviluppatori AEM e i gestori di distribuzione avranno accesso a AEM as a Cloud Service e potranno iniziare a creare e distribuire applicazioni personalizzate.

## Concetti e obiettivi {#concepts}

Anche se può sembrare che ci sia molto da imparare quando si inizia con AEM as a Cloud Service, concettualmente ci sono solo pochi, pezzi logici.

* **Il Contratto** - È necessario avere familiarità con il contratto Adobe in quanto definisce gli aspetti del processo di onboarding.
* **Admin Console** - In questo caso gli utenti vengono gestiti e i ruoli vengono assegnati.
* **Cloud Manager** - Questo è lo strumento per impostare risorse come programmi e ambienti. È anche il luogo in cui accedi a Git e crei pipeline per gestire e distribuire il codice personalizzato.

Tali concetti saranno illustrati in dettaglio in questo percorso di onboarding. L&#39;obiettivo è che alla fine del percorso:

* Hanno concesso agli utenti necessari l’accesso ad AEMaaCS
* Configurare le prime risorse cloud per il progetto
* Scopri come distribuire il tuo primo codice e creare il tuo primo contenuto.

In pratica, il tuo nuovo progetto as a Cloud Service AEM ti permetterà di raggiungere il terreno.

## Pubblico {#audience}

Il percorso di onboarding è scritto specificatamente per **amministratore di sistema** del nuovo cliente a AEM as a Cloud Service e a AEM in generale. L’amministratore di sistema è la persona che viene contattata per la prima volta da Adobe dopo la firma del contratto as a Cloud Service AEM, e in genere è la prima persona ad accedere e impostare le risorse as a Cloud Service AEM. Se lo stai leggendo, è probabile che l&#39;amministratore di sistema sia l&#39;amministratore di sistema.

L’amministratore di sistema gestisce tutti gli aspetti degli utenti AEMaaCS della propria organizzazione, dall’accesso alle autorizzazioni. Tuttavia, l’amministratore di sistema deve interagire con altri utenti tipo lungo il percorso.

| Persona | Descrizione | Ruolo nel percorso |
|---|---|---|
| Amministratore di sistema | Target di questo percorso, fornisce il provisioning iniziale delle risorse cloud e l&#39;assegnazione degli utenti a ruoli appropriati in base alle loro responsabilità lavorative | Gestisce tutti gli aspetti degli utenti dall&#39;accesso alle autorizzazioni |
| Autore del contenuto | Crea e rivede il contenuto in AEM | Una volta ottenute le autorizzazioni dall’amministratore di sistema, gli autori possono iniziare a creare il proprio percorso creando contenuti |
| Sviluppatore | Sviluppa le applicazioni AEM che utilizzano contenuti provenienti da fonti diverse. | Una volta concesse le autorizzazioni dall&#39;amministratore di sistema, gli sviluppatori possono avviare il proprio percorso sviluppando soluzioni |
| Gestione distribuzione | Aggiunge o aggiorna un ambiente, esegue pipeline e distribuisce codice per AEM ambiente o qualità del codice. | Una volta concesse le autorizzazioni dall&#39;amministratore di sistema, i responsabili della distribuzione possono avviare il proprio percorso per la gestione delle distribuzioni |

Questa guida all’onboarding illustra l’intero processo di onboarding come amministratore di sistema. I ruoli di utenti, sviluppatori e gestori di distribuzione AEM vengono brevemente descritti come parti aggiuntive e facoltative del percorso.

>[!TIP]
>
>Se hai poca esperienza con AEM as a Cloud Service, ma conosci già AEM e stai eseguendo la migrazione da on-premise o Adobe Managed Services, assicurati di controllare la [AEM Percorso di migrazione as a Cloud Service.](/help/journey-migration/getting-started.md)

## Panoramica del Percorso di onboarding {#overview}

I seguenti articoli descrivono in dettaglio i concetti di base dell’onboarding e forniscono informazioni fondamentali su AEM as a Cloud Service. Anche se puoi passare direttamente a una parte specifica del percorso, molti concetti si basano su quelli degli articoli precedenti. Pertanto, se non hai ancora effettuato l’onboarding, ti consigliamo di iniziare dall’inizio e di procedere in sequenza.

| # | Articolo | Descrizione | Pubblico |
|---|---|---|---|
| 0 | Percorso di onboarding | Questo documento | Amministratore di sistema |
| 1 | [Preparazione all’onboarding](preparation.md) | Prima dell&#39;inizio del processo di onboarding, è necessario che l&#39;amministratore di sistema comprenda una serie di passaggi preparatori prima di effettuare l&#39;accesso al sistema. | Amministratore di sistema |
| 2 | [Terminologia di AEM as a Cloud Service](terminology.md) | Prima di accedere ad AEMaaCS per la prima volta, è utile comprendere alcuni termini del sistema e la sua struttura di base. | Amministratore di sistema |
| 3 | [L’Admin Console](admin-console.md) | Scopri l’Admin Console, come effettuare l’accesso e come verificare il tuo profilo come amministratore di sistema. | Amministratore di sistema |
| 4 | [Assegnazione dei profili di prodotto di Cloud Manager](assign-profiles-cloud-manager.md) | Esamina i profili di prodotto di Cloud Manager e scopri come assegnare i membri del team ai profili di prodotto di Cloud Manager. | Amministratore di sistema |
| 5 | [Accesso a Cloud Manager](cloud-manager.md) | Scopri come accedere a Cloud Manager per configurare le risorse del progetto. | Amministratore di sistema |
| 6 | [Creare un programma](create-program.md) | Scopri come creare un programma utilizzando Cloud Manager. | Amministratore di sistema |
| 7 | [Creare ambienti](create-environments.md) | Scopri come creare un ambiente utilizzando Cloud Manager. | Amministratore di sistema |
| 8 | [Assegnazione di profili di prodotto AEM](assign-profiles-aem.md) | Scopri come l’amministratore di sistema assegna i membri del team a AEM i profili di prodotto as a Cloud Service. | Amministratore di sistema |
| 9 | [Attività del Responsabile degli sviluppatori e del Responsabile della distribuzione](developers.md) | Facoltativo - Scopri come, in qualità di sviluppatore, puoi accedere e gestire Cloud Manager Git e come configurare le pipeline e distribuire il codice in Cloud Manager in quanto gestore dell’implementazione. | Sviluppatori e gestori di distribuzione |
| 10 | [Attività dell’utente di AEM](aem-users.md) | Facoltativo - Scopri come, in qualità di autore AEM, puoi accedere AEM’istanza as a Cloud Service e acquisire familiarità con i contenuti di authoring per AEM as a Cloud Service. | Utenti AEM |

## Novità {#what-is-next}

È ora possibile avviare il percorso di onboarding as a Cloud Service AEM. Ti invitiamo a continuare nella parte successiva del percorso e a leggere l&#39;articolo [Preparazione all&#39;onboarding](preparation.md)

## Percorsi di documentazione AEM {#documentation-journeys}

[Un percorso di documentazione](/help/journey-documentation/documentation-journeys.md) unisce molti argomenti e caratteristiche diversi e forse complicati, fornendo un resoconto che aiuta il lettore, che potrebbe essere un nuovo utente di AEM, a capire e risolvere un problema di business dall’inizio alla fine, supponendo una conoscenza minima pregressa dell’argomento o di AEM.

I percorsi di documentazione sono progettati in base ai principi delle best practice, alla luce delle ultime ricerche condotte da Adobe, della comprovata esperienza nell’implementazione da parte di consulenti di Adobe e del feedback raccolto sui progetti dei clienti.

Se desideri sapere come Adobe consiglia di eseguire l’onboarding del team sulla nuova applicazione as a Cloud Service di AEM, ecco da dove iniziare!
