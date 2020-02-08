---
title: Creazione di concetti
description: Concetti di authoring in AEM
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# Authoring Concetti {#authoring-concepts}

Un’installazione AEM in genere consiste di almeno due ambienti:

* Authoring
* Pubblicazione

Questi interagiscono per rendere disponibile il contenuto sul sito Web in modo che i visitatori possano accedervi.

L’ambiente di authoring fornisce i meccanismi per creare, aggiornare e rivedere il contenuto prima di pubblicarlo:

* Un autore crea e rivede il contenuto. I contenuti possono essere di diversi tipi, ad esempio pagine, risorse, pubblicazioni, ecc.
* Questo contenuto verrà pubblicato sul sito Web.

![Diagramma dell’autore, dell’editore e dei dispatcher](/help/sites-cloud/authoring/assets/author-publish.png)

Nell’ambiente di authoring le funzionalità di AEM sono accessibili tramite l’interfaccia utente di authoring di AEM. Nell’ambiente di pubblicazione si progetta invece l’aspetto e il comportamento dell’interfaccia che si intende presentare ai visitatori.

>[!NOTE]
>
>AEM stesso viene utilizzato per pubblicare la documentazione di AEM.

## Ambiente di authoring {#author-environment}

L’autore utilizza il cosiddetto ambiente di **authoring**. che fornisce un&#39;interfaccia utente grafica (interfaccia utente grafica) di facile utilizzo per la creazione dei contenuti. Richiede all’autore di effettuare l’accesso, utilizzando un account a cui sono stati assegnati i diritti di accesso appropriati.

>[!NOTE]
>
>Per creare, modificare o pubblicare le risorse, è necessario utilizzare un account con diritti di accesso appropriati.

A seconda della configurazione dell’istanza in uso e dei diritti di accesso personali, è possibile eseguire varie attività sui contenuti, ad esempio:

* Generazione di nuovo contenuto o modifica di contenuto esistente su una pagina
* Utilizzo di modelli predefiniti per creare nuove pagine di contenuto
* Creazione, modifica e gestione delle risorse e delle raccolte
* Spostamento, copia ed eliminazione di pagine di contenuto, risorse ecc.
* Pubblicazione (o annullamento della pubblicazione) di pagine, risorse ecc.

Inoltre è possibile effettuare attività amministrative con cui gestire i contenuti:

* Flussi di lavoro che controllano la modalità di gestione delle modifiche, ad esempio l&#39;imposizione di una revisione prima della pubblicazione
* Progetti che coordinano singole attività

>[!NOTE]
>
>AEM è amministrato anche dall’ambiente di authoring.

## Ambiente di pubblicazione {#publish-environment}

When ready, your site&#39;s content is published to the **publish environment**. Qui le pagine del sito web vengono rese disponibili al pubblico di destinazione in base all’aspetto dell’interfaccia realizzata.

Per ulteriori informazioni sulla pubblicazione e l’annullamento della pubblicazione di pagine, vedere il documento [Publishing Pages.](/help/sites-cloud/authoring/fundamentals/publishing-pages.md)

## Dispatcher {#dispatcher}

To optimize performance for visitors to your website, the **[dispatcher](/help/implementing/dispatcher/overview.md)**implements load balancing and caching.
