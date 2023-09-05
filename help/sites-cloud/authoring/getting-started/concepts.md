---
title: Concetti relativi all’authoring
description: Scopri i concetti di authoring in AEM utilizzando gli ambienti di authoring, anteprima e pubblicazione.
exl-id: ee9e4952-e075-4398-b31f-d7886153efff
source-git-commit: 31e6ec8e9977c8787e14481ee3a94df767262aec
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 96%

---

# Concetti relativi all’authoring {#authoring-concepts}

Un’installazione di AEM è in genere costituita da almeno due ambienti:

* Autore
* Pubblicazione

Questi ambienti interagiscono tra di loro e consentono di rendere i contenuti disponibili nel sito web e accessibili ai visitatori.

L’ambiente di authoring fornisce le funzioni necessarie per creare, aggiornare e rivedere i contenuti prima che vengano pubblicati:

* Un autore crea e rivede i contenuti. I contenuti possono essere di diversi tipi, tra cui pagine, risorse e pubblicazioni.
* e sono destinati a essere pubblicati sul sito web.

![Diagramma relativo a authoring, pubblicazione e dispatcher](/help/sites-cloud/authoring/assets/author-publish.png)

Nell’ambiente di authoring è possibile accedere alle funzionalità di AEM tramite l’interfaccia utente di authoring di AEM. Nell’ambiente di pubblicazione vengono invece progettati l’aspetto e il comportamento dell’interfaccia presentata agli utenti.

## Ambiente di authoring {#author-environment}

L’autore lavora in ciò che è noto come **ambiente di authoring**. Questo ambiente fornisce un’interfaccia di facile utilizzo (interfaccia grafica utente (GUI o UI)) per la creazione dei contenuti. L’autore deve effettuare l’accesso, utilizzando un account a cui sono assegnati i diritti di accesso appropriati.

>[!NOTE]
>
>Per creare, modificare o pubblicare contenuti, il tuo account deve disporre dei diritti di accesso appropriati.

A seconda della configurazione dell’istanza e dei diritti di accesso personali, puoi eseguire molte attività sul contenuto, tra cui (tra le altre):

* Generazione di nuovi contenuti o modifica dei contenuti esistenti in una pagina
* Utilizzo di modelli predefiniti per creare pagine di contenuti
* Creazione, modifica e gestione delle risorse e delle raccolte
* Spostamento, copia ed eliminazione di pagine di contenuto e risorse.
* Pubblicazione (o annullamento della pubblicazione) di pagine e risorse.

Sono anche disponibili attività amministrative per la gestione dei contenuti:

* Flussi di lavoro che controllano la modalità di gestione dei cambiamenti, ad esempio per imporre la revisione prima della pubblicazione
* Progetti per coordinare singole attività

>[!NOTE]
>
>Nell’ambiente di authoring è anche possibile effettuare attività di amministrazione di AEM.

## Anteprima del contenuto {#previewing-content}

AEM offre anche un servizio di anteprima di Sites che consente a sviluppatori e autori di contenuti di visualizzare in anteprima l’esperienza finale di un sito web prima che venga inserito in un ambiente di pubblicazione e divenga disponibile.

Ulteriori dettagli in [Anteprima del contenuto](/help/sites-cloud/authoring/fundamentals/previewing-content.md).

## Ambiente di pubblicazione {#publish-environment}

Quando è pronto, il contenuto del sito viene pubblicato nell’**ambiente di pubblicazione**. Qui le pagine del sito web vengono rese disponibili al pubblico di destinazione in base all’aspetto dell’interfaccia progettata.

Per ulteriori informazioni sulla pubblicazione e sull’annullamento della pubblicazione di pagine, consulta il documento [Pubblicazione di pagine](/help/sites-cloud/authoring/fundamentals/publishing-pages.md).

## Dispatcher {#dispatcher}

Per ottimizzare le prestazioni dal punto di vista dei visitatori del sito web, **[Dispatcher](/help/implementing/dispatcher/overview.md)** implementa funzioni di bilanciamento del carico e memorizzazione in cache.
