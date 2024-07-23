---
title: Scelta di un metodo di authoring
description: Scopri importanti considerazioni per decidere come creare i contenuti in AEM per aiutarti a prendere la decisione migliore per gli autori di contenuti.
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 15eef2d3790d1c0cf5414ca55b191de5b644fed0
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# Scelta di un metodo di authoring {#authoring-methods}

Scopri importanti considerazioni per decidere come creare i contenuti in AEM per aiutarti a prendere la decisione migliore per gli autori di contenuti.

## Panoramica delle considerazioni {#overview}

La flessibilità dell’AEM garantisce che le tue esigenze di authoring siano soddisfatte indipendentemente da come scegli l’authoring basato su documenti o l’authoring WYSIWYG. Per iniziare le proprie considerazioni, considera i fatti riportati di seguito.

* **Coinvolgi sempre gli autori dei contenuti nella decisione.** - Gli autori dei contenuti sono i tuoi esperti e la loro conoscenza è fondamentale.
* **È possibile implementare più metodi di authoring.** - Anche se Adobe consiglia di iniziare con semplicità e stratificare la complessità in base alle esigenze, più metodi di authoring possono funzionare insieme in un unico progetto.
* **Puoi sempre cambiare il tuo metodo di creazione dopo il fatto.** - A prescindere da ciò che decidi di non essere bloccato. Passare da un metodo all’altro è semplice e immediato con l’assistenza degli strumenti di migrazione automatizzata di Adobe.
* **Non devi decidere prima dell&#39;implementazione, ma piuttosto come parte dell&#39;implementazione.** - L&#39;AEM è un prodotto unificato, quindi questa importante decisione non deve far parte delle negoziazioni contrattuali. Quando compri l&#39;AEM, li ottieni tutti. Si tratta piuttosto di una decisione presa durante l’implementazione.

Adobe può aiutarti a determinare quale metodo (o metodi) meglio si adatta ai tuoi requisiti come parte dell’implementazione.

## Una dimensione non adatta a tutte {#one-size}

Ogni implementazione dell&#39;AEM ha i propri flussi di lavoro e obiettivi. Un progetto può includere un semplice modello di authoring con autori di contenuti responsabili delle proprie pubblicazioni. Mentre un altro potrebbe avere una rete complessa di collaboratori e approvazioni.

![Flussi di lavoro di authoring diversi](assets/authoring-workflows.png)

Progetti diversi possono avere casi d’uso diversi (e multipli).

![Casi d&#39;uso](assets/use-cases.png)

L&#39;Adobe è consapevole di ciò e pertanto non offre un approccio unico per tutti. AEM è l&#39;unica soluzione che offre diversi approcci per la distribuzione dei contenuti e la creazione dei contenuti in base alle esigenze.

Per determinare l’approccio migliore, è necessario prendere in considerazione quattro elementi.

1. [Disponi di una preferenza per la consegna dei contenuti?](#content-delivery)
1. [Hai una preferenza per l’authoring dei contenuti?](#content-authoring)
1. [Qual è il tuo obiettivo del progetto?](#project-goals)
1. [Quali sono le sfide per l&#39;authoring che stai affrontando oggi?](#authoring-challenges)

## Preferenze di distribuzione dei contenuti {#content-delivery}

La prima considerazione da tenere in considerazione è come distribuire i contenuti. Edge Delivery Services offre siti fulminei, ma forse la tua attenzione è focalizzata sulla consegna headless. La seguente struttura decisionale può aiutarti a considerare le tue opzioni.

![Struttura delle decisioni per la distribuzione dei contenuti](assets/content-delivery-decision-tree.png)

Questo può aiutarti a decidere se è necessario:

* [AEM come CMS headless](/help/headless/introduction.md) utilizzando l&#39;Editor frammento di contenuto e/o l&#39;Editor universale.
* Edge Delivery Services AEM che utilizzano la [modifica basata su documento](/help/edge/docs/authoring.md) o la [creazione WYSIWYG con Universal Editor.](/help/edge/wysiwyg-authoring/authoring.md)

## Preferenze di authoring dei contenuti {#content-authoring}

La considerazione successiva dovrebbe essere come creare i contenuti. La seguente struttura decisionale può aiutarti a considerare le tue opzioni.

![Struttura decisionale per l&#39;authoring dei contenuti](assets/content-authoring-decision-tree.png)

Questo può aiutarti a decidere se è necessario:

* Edge Delivery Services AEM che utilizzano la [modifica basata su documento.](/help/edge/docs/authoring.md)
* [Authoring WYSIWYG con Universal Editor.](/help/edge/wysiwyg-authoring/authoring.md)

## Obiettivi progetto {#project-goals}

Che aspetto ha il successo nell’authoring? Come si definisce il successo del progetto?

* Forse è necessario consentire a più persone di creare contenuti, ma si desidera evitare la formazione su un nuovo set di strumenti. (ad esempio l&#39;authoring basato su documenti).
* Potrebbe essere necessario aumentare la quantità di contenuti generati. (ad esempio l&#39;authoring basato su documenti).
* Forse è necessario concentrarsi sul layout del contenuto visivo, ma ridurre al minimo la necessità di conoscenze di codifica. (Pensate all&#39;authoring WYSIWYG.)

Obiettivi di progetto chiaramente definiti all’inizio dell’implementazione ti aiuteranno a prendere una decisione informata sul metodo di authoring.

## Sfide relative all’authoring {#authoring-challenges}

Infine, considera le sfide specifiche che devi affrontare oggi nell’authoring dei contenuti.

* Forse devi affrontare la duplicazione del lavoro con contenuti creati al di fuori del CMS, che poi deve essere importato o copiato e incollato. (ad esempio l&#39;authoring basato su documenti).
* Forse è necessario ridurre il tempo necessario per istruire gli autori su come utilizzare un CMS. (ad esempio l&#39;authoring basato su documenti).
* È possibile che gli autori debbano modificare spesso il layout visivo dei contenuti, richiedendo un costante supporto da parte degli sviluppatori. (Pensate all&#39;authoring WYSIWYG.)
