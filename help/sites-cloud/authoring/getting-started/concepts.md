---
title: Concetti relativi all’authoring
description: Concetti relativi all’authoring in AEM
exl-id: ee9e4952-e075-4398-b31f-d7886153efff
source-git-commit: 1473c1ffccc87cb3a0033750ee26d53baf62872f
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 42%

---

# Authoring   Concetti  {#authoring-concepts}

Un’installazione di AEM è in genere costituita da almeno due ambienti:

* Autore
* Pubblicazione

Questi ambienti interagiscono tra loro e consentono di rendere i contenuti disponibili sul sito web e accessibili ai visitatori.

L’ambiente di authoring fornisce le funzioni necessarie per creare, aggiornare e rivedere i contenuti prima che vengano pubblicati:

* Un autore crea e rivede i contenuti. I contenuti possono essere di diversi tipi, tra cui pagine, risorse e pubblicazioni.
* e sono destinati a essere pubblicati sul sito web.

![Diagramma relativo a authoring, pubblicazione e dispatcher](/help/sites-cloud/authoring/assets/author-publish.png)

Nell’ambiente di authoring, le funzionalità dell’AEM sono rese disponibili tramite l’interfaccia utente di authoring dell’AEM. Per l’ambiente di pubblicazione, puoi progettare l’aspetto e il comportamento dell’interfaccia resa disponibile agli utenti.

## Ambiente di authoring {#author-environment}

L’autore lavora in ciò che è noto come **ambiente di authoring**. Questo ambiente fornisce un’interfaccia di facile utilizzo (interfaccia grafica utente (GUI o UI)) per la creazione dei contenuti. Richiede all&#39;autore di effettuare l&#39;accesso, utilizzando un account a cui siano stati assegnati i diritti di accesso appropriati.

>[!NOTE]
>
>Il tuo account necessita dei diritti di accesso appropriati per creare, modificare o pubblicare contenuti.

A seconda della configurazione dell’istanza e dei diritti di accesso personali, puoi eseguire molte attività sul contenuto, tra cui:

* Generazione di nuovi contenuti o modifica dei contenuti esistenti in una pagina
* Utilizzo di modelli predefiniti per creare pagine di contenuto
* Creazione, modifica e gestione delle risorse e delle raccolte
* Spostamento, copia ed eliminazione di pagine di contenuto e risorse.
* Pubblicazione (o annullamento) di pagine e risorse.

Sono inoltre disponibili attività amministrative che consentono di gestire il contenuto:

* Flussi di lavoro che controllano la modalità di gestione dei cambiamenti, ad esempio per imporre la revisione prima della pubblicazione
* Progetti per coordinare singole attività

>[!NOTE]
>
>Nell’ambiente di authoring è anche possibile effettuare attività di amministrazione di AEM.

## Anteprima del contenuto {#previewing-content}

AEM offre anche un servizio di anteprima Sites che consente a sviluppatori e autori di contenuti di visualizzare in anteprima l’esperienza finale di un sito web prima che raggiunga l’ambiente di pubblicazione e sia disponibile pubblicamente.

Ulteriori dettagli in [Anteprima del contenuto](/help/sites-cloud/authoring/fundamentals/previewing-content.md).

## Ambiente di pubblicazione {#publish-environment}

Quando è pronto, il contenuto del sito viene pubblicato nell’**ambiente di pubblicazione**. Qui le pagine del sito web vengono rese disponibili al pubblico di destinazione in base all’aspetto dell’interfaccia progettata.

Per ulteriori informazioni sulla pubblicazione e sull’annullamento della pubblicazione di pagine, consulta il documento [Pubblicazione di pagine](/help/sites-cloud/authoring/fundamentals/publishing-pages.md).

## Dispatcher {#dispatcher}

Per ottimizzare le prestazioni per i visitatori del sito Web, il **[Dispatcher](/help/implementing/dispatcher/overview.md)** implementa il bilanciamento del carico e il caching.
