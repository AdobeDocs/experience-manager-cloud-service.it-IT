---
title: Ereditarietà dei contenuti nell’editor universale
description: Scopri in che modo Universal Editor supporta l’ereditarietà dei contenuti per la gestione multisito e i lanci per supportare il riutilizzo e la localizzazione dei contenuti.
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 58c58243dc98a21161afe0976da4dcdc235da0d3
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 3%

---


# Ereditarietà dei contenuti nell’editor universale {#inheritance}

Scopri in che modo Universal Editor supporta l’ereditarietà dei contenuti per la gestione multisito e i lanci per supportare il riutilizzo e la localizzazione dei contenuti.

## Caso d’uso {#use-case}

Per molti utenti dell&#39;AEM, la creazione di una pagina è solo l&#39;inizio. Per ridimensionare il contenuto in modo efficace, in genere dopo la creazione della pagina sono necessari i seguenti passaggi:

1. **Traduci la pagina** utilizzando copie per lingua e flussi di lavoro di traduzione.
1. **Localizzare la pagina** utilizzando Gestione multisito per distribuire la pagina tradotta in mercati diversi.
1. **Crea nuove versioni** utilizzando i lanci per preparare le iterazioni future della pagina e attivare tali modifiche.

Questi passaggi possono accelerare la velocità dei contenuti e garantirne la coerenza. L’editor universale supporta l’ereditarietà dei contenuti, ovvero il meccanismo su cui si basano questi passaggi.

## Ereditarietà {#what-is-inheritance}

L’ereditarietà è il meccanismo in cui il contenuto può essere collegato in modo che la modifica di un elemento cambia automaticamente l’altro. I componenti ereditati possono essere il risultato di vari scenari, tra cui:

* [Gestione multisito (MSM)](/help/sites-cloud/administering/msm/overview.md)
* [Lanci](/help/sites-cloud/authoring/launches/overview.md)

MSM e Launches sono strumenti potenti per aiutarti a riutilizzare i contenuti. Le pagine possono essere copiate da una sorgente centrale (la blueprint) per consentire agli autori di apportare modifiche specifiche al contesto di tali copie, mentre il resto del contenuto rimane ereditato dalla blueprint. Questa funzione è estremamente utile per la localizzazione dei siti.

Per modificare parte del contenuto delle copie, gli autori interrompono l’ereditarietà sui componenti interessati in modo da garantire che le modifiche locali non vengano sovrascritte quando le copie vengono sincronizzate dalla blueprint.

## Ereditarietà dei contenuti e Editor universale {#universal-editor}

Quando una pagina fa parte di MSM o di un lancio e il contenuto viene modificato con l&#39;Editor universale, l&#39;editor disabilita automaticamente l&#39;ereditarietà per tutte le modifiche apportate dagli autori sulla pagina, garantendo che il contenuto modificato venga mantenuto quando gli aggiornamenti vengono sincronizzati dalla blueprint.

L’autore non deve fare clic su un pulsante o adottare altri passaggi per disabilitare l’ereditarietà prima di apportare modifiche locali. Non appena viene apportata una modifica, l’ereditarietà viene implicitamente annullata. Questo è in contrasto con l&#39;[Editor pagina.](/help/sites-cloud/authoring/page-editor/edit-content.md#inherited-components)

## Limitazioni {#limitations}

* Gli autori non possono ripristinare l’ereditarietà per i singoli componenti.
   * L&#39;ereditarietà può essere ripristinata solo per l&#39;intera pagina tramite la [console Panoramica Live Copy](/help/sites-cloud/administering/msm/live-copy-overview.md) o la [console Lanci.](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)
* Gli autori non dispongono di un feedback visivo per vedere quali componenti hanno la loro ereditarietà disabilitata e quali ancora la mantengono.
* Queste funzionalità sono attualmente limitate ai componenti nelle pagine e non sono ancora applicabili a [Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/overview.md), nonostante siano disponibili anche le funzionalità MSM e Launch.