---
title: Concetti relativi all’authoring e alla pubblicazione
description: Scopri i concetti di authoring in AEM utilizzando gli ambienti di authoring, anteprima e pubblicazione.
exl-id: ee9e4952-e075-4398-b31f-d7886153efff
source-git-commit: bbd845079cb688dc3e62e2cf6b1a63c49a92f6b4
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 29%

---


# Concetti relativi all’authoring e alla pubblicazione {#authoring-publishing}

Per un autore di contenuti, un’installazione as a Cloud Service all’AEM può essere considerata come tre livelli primari al livello più elementare

* Livello di authoring
* Anteprima livello
* Livello di pubblicazione

Questi livelli interagiscono per consentire di rendere i contenuti disponibili sul sito web in modo che i visitatori possano accedervi. Il flusso di lavoro di base è:

1. Gli autori dei contenuti creano i propri contenuti utilizzando il livello di authoring.
1. Gli autori dei contenuti rendono i propri contenuti disponibili ai revisori per l’anteprima utilizzando il livello di anteprima.
1. Quando il contenuto è pronto per il consumo pubblico, gli autori pubblicano il contenuto utilizzando il livello di pubblicazione.

I contenuti possono essere di diversi tipi, tra cui pagine, risorse e pubblicazioni. A discrezione dell’autore, l’anteprima del contenuto può essere saltata.

![Diagramma relativo a authoring, pubblicazione e dispatcher](assets/author-publish.jpg)

Per maggiori dettagli sull&#39;architettura tecnica di AEM as a Cloud Service, si rimanda al documento [Introduzione all’architettura di Adobe Experience Manager as a Cloud Service.](/help/overview/architecture.md)

{{edge-delivery-authoring}}

## Creazione di contenuti {#author-environment}

L’ambiente di authoring del livello di authoring fornisce un’interfaccia grafica utente facile da usare per la creazione dei contenuti. L’autore deve effettuare l’accesso, utilizzando un account a cui sono assegnati i diritti di accesso appropriati.

A seconda della configurazione dell’istanza e dei diritti di accesso personali, puoi eseguire molte attività sul contenuto, tra cui (tra le altre):

* Generazione di nuovi contenuti o modifica dei contenuti esistenti in una pagina
* Utilizzo di modelli predefiniti per creare pagine di contenuti
* Creazione, modifica e gestione delle risorse e delle raccolte
* Spostamento, copia ed eliminazione di pagine di contenuto e risorse.
* Pubblicazione (o annullamento della pubblicazione) di pagine e risorse.

Sono anche disponibili attività amministrative per la gestione dei contenuti:

* Flussi di lavoro che controllano la modalità di gestione dei cambiamenti, ad esempio per imporre la revisione prima della pubblicazione
* Progetti per coordinare singole attività

Nell’ambiente di authoring è anche possibile effettuare attività di amministrazione di AEM.

Consulta il documento [Guida rapida all’authoring](/help/sites-cloud/authoring/quick-start.md) panoramica del processo di authoring.

## Anteprima del contenuto {#previewing-content}

AEM offre anche un servizio di anteprima che consente a sviluppatori e autori di contenuti di visualizzare in anteprima l’esperienza finale di un sito web prima che raggiunga l’ambiente di pubblicazione e sia disponibile pubblicamente.

Consulta il documento [Anteprima del contenuto](/help/sites-cloud/authoring/sites-console/previewing-content.md) per ulteriori dettagli.

## Ambiente di pubblicazione {#publish-environment}

Quando è pronto, il contenuto del sito viene pubblicato nell’ambiente di pubblicazione del livello di pubblicazione. Qui le pagine del sito web vengono rese disponibili al pubblico previsto in base all’aspetto del modello di contenuto.

Consulta il documento [Pubblicazione delle pagine](/help/sites-cloud/authoring/sites-console/publishing-pages.md) per ulteriori informazioni sulla pubblicazione e sull’annullamento della pubblicazione di pagine.

## Dispatcher {#dispatcher}

Per ottimizzare le prestazioni per i visitatori del sito Web, il **[Dispatcher](/help/implementing/dispatcher/overview.md)** implementa il bilanciamento del carico e il caching sia per il livello di pubblicazione che per quello di anteprima.
