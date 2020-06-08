---
title: Concetti relativi all’authoring
description: Concetti relativi all’authoring in AEM
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 100%

---


# Authoring   Concetti {#authoring-concepts}

Un’installazione di AEM è in genere costituita da almeno due ambienti:

* Autore
* Pubblicazione

Questi interagiscono tra di loro e consentono di rendere i contenuti disponibili nel sito web e accessibili ai visitatori.

L’ambiente di authoring fornisce le funzioni necessarie per creare, aggiornare e rivedere i contenuti prima che vengano pubblicati:

* Un autore crea e rivede i contenuti. I contenuti possono essere di vari tipi, ad esempio pagine, risorse, pubblicazioni e così via,
* e sono destinati a essere pubblicati sul sito web.

![Diagramma relativo a authoring, pubblicazione e dispatcher](/help/sites-cloud/authoring/assets/author-publish.png)

Nell’ambiente di authoring è possibile accedere alle funzionalità di AEM tramite l’interfaccia di authoring di AEM. Nell’ambiente di pubblicazione vengono invece progettati l’aspetto e il comportamento dell’interfaccia presentata agli utenti.

>[!NOTE]
>
>Anche la documentazione di AEM è stata pubblicata con AEM.

## Ambiente di authoring {#author-environment}

L’autore utilizza il cosiddetto **ambiente di authoring**, che fornisce un’interfaccia, grafica o normale, di facile utilizzo per la creazione dei contenuti. L’autore deve effettuare l’accesso, utilizzando un account a cui sono stati assegnati i diritti di accesso appropriati.

>[!NOTE]
>
>Per creare, modificare o pubblicare le risorse, è necessario utilizzare un account con diritti di accesso appropriati.

A seconda della configurazione dell’istanza in uso e dei diritti di accesso personali, è possibile eseguire varie attività sui contenuti, ad esempio:

* Generazione di nuovi contenuti o modifica dei contenuti esistenti in una pagina
* Utilizzo di modelli predefiniti per creare nuove pagine di contenuti
* Creazione, modifica e gestione delle risorse e delle raccolte
* Spostamento, copia ed eliminazione di pagine di contenuto, risorse e così via
* Pubblicazione (o annullamento della pubblicazione) di pagine, risorse e così via.

Sono inoltre disponibili attività amministrative per la gestione dei contenuti:

* Flussi di lavoro che controllano la modalità di gestione dei cambiamenti, ad esempio per imporre la revisione prima della pubblicazione
* Progetti per coordinare singole attività

>[!NOTE]
>
>Nell’ambiente di authoring è anche possibile effettuare attività di amministrazione di AEM.

## Ambiente di pubblicazione {#publish-environment}

Quando è pronto, il contenuto del sito viene pubblicato nell’**ambiente di pubblicazione**. Qui le pagine del sito web vengono rese disponibili al pubblico di destinazione in base all’aspetto dell’interfaccia progettata.

Per ulteriori informazioni sulla pubblicazione e sull’annullamento della pubblicazione di pagine, consulta il documento [Pubblicazione di pagine](/help/sites-cloud/authoring/fundamentals/publishing-pages.md).

## Dispatcher {#dispatcher}

Per ottimizzare le prestazioni dal punto di vista dei visitatori del sito web, vengono usati **[dispatcher](/help/implementing/dispatcher/overview.md)**che implementano funzioni di bilanciamento del carico e memorizzazione in cache.
