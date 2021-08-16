---
title: AEM Percorso di authoring dei contenuti headless
description: Introduzione alle funzioni avanzate, flessibili e headless di Adobe Experience Manager as a Cloud Service e modalità di creazione di contenuti per il progetto.
index: false
hide: true
hidefromtoc: true
source-git-commit: 41ad9e8ee77ae4494d28026b5ad9da45c06eaeaf
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 1%

---


# Authoring per headless con AEM - Introduzione {#author-headless-introduction}

In questa parte del [AEM Percorso di authoring di contenuti headless](overview.md), puoi imparare i concetti e la terminologia di base necessari per comprendere come Cloud Service l’authoring di contenuti per la distribuzione di contenuti headless con Adobe Experience Manager (AEM).

## Obiettivo {#objective}

* **Pubblico**: Principiante
* **Obiettivo**: Introduce i concetti e la terminologia relativi all’authoring headless.

## Sistema di gestione dei contenuti (CMS) {#content-management-system}

Che cos’è un sistema di gestione dei contenuti?

Un sistema di gestione dei contenuti (CMS, Content Management System) è esattamente ciò che dice - un sistema informatico utilizzato per gestire i contenuti. Questo è un po&#39; generale, quindi per essere più precisi, viene (in genere) utilizzato per gestire i contenuti che si desidera rendere disponibili sul tuo sito web.

## CMS headless {#headless-cms}

Headless è un termine utilizzato per descrivere i sistemi che staccano efficacemente il contenuto dal modo in cui vengono visualizzati sul web.

Tradizionalmente, si gestiva il contenuto in un CMS e lo stesso CMS sarebbe responsabile del rendering di tale contenuto sulle pagine web.

Ora, headless significa che il set di contenuti può essere gestito nel CMS e quindi utilizzato da una o più applicazioni (indipendenti).

Ciò significa che i contenuti possono essere inviati a qualsiasi dispositivo, in una vasta gamma di formati. Questo rende l&#39;intero processo molto più flessibile, e significa anche che non è necessario preoccuparsi del layout e della formattazione.

>[!NOTE]
>
>Per ulteriori informazioni sui dettagli tecnici di Headless CMS, consulta Informazioni sullo sviluppo headless di CMS.

## Adobe Experience Manager as a Cloud Service {#aem-cloud-service}

Allora cosa è AEM?

Innanzitutto, AEM è un sistema di gestione dei contenuti con un&#39;ampia gamma di funzioni personalizzabili per soddisfare le tue esigenze.

Questo significa che può essere utilizzato come:

* CMS headless
   * Per gli headless, il contenuto può essere creato come **Frammenti di contenuto**.
Si tratta di elementi indipendenti di contenuto a cui è possibile accedere direttamente da una serie di applicazioni, in quanto dispongono di una struttura predefinita basata su **Modelli di frammento di contenuto**.
Ciò significa che i contenuti possono raggiungere una vasta gamma di dispositivi, in una vasta gamma di formati e con un&#39;ampia gamma di funzionalità.
Inoltre, questi frammenti possono essere utilizzati anche per la creazione di pagine web AEM, se lo desideri.

* CMS &quot;tradizionale&quot;
   * Il contenuto viene creato per le pagine web utilizzando una serie di componenti che definiscono come verrà eseguito il rendering del contenuto sul sito web. Anche qui AEM è estremamente flessibile in quanto il team di progetto può sviluppare componenti personalizzati.

## Modellazione dei contenuti {#content-modeling}

Quindi la modellazione dei contenuti (nota anche come modellazione dei dati) è un altro termine tecnico - perché dovrebbe interessarti in qualità di autore?

Affinché le applicazioni headless possano accedere ai contenuti e utilizzarli, il contenuto deve avere una struttura predefinita. Sarebbe possibile avere i contenuti come forma libera, ma renderebbe la vita *molto* complicata per le applicazioni.

In sostanza, il processo di definizione della struttura del contenuto da rispettare prevede la progettazione di un modello, denominato modellazione dei dati.

Per AEM il ruolo Architetto contenuto (spesso una persona diversa) eseguirà la modellazione dei dati per progettare un intervallo di **Modelli di frammento di contenuto**, che potrai quindi utilizzare come base per il contenuto utilizzando **Frammenti di contenuto**.

>[!NOTE]
>
>Per ulteriori informazioni sulla modellazione dei dati, consulta il Percorso AEM architetto di contenuti headless .

## Novità {#whats-next}

Dopo aver appreso i concetti e la terminologia, il passaggio successivo è [Scopri le nozioni di base sull’authoring di frammenti di contenuto](basics.md). Viene introdotta la gestione di base delle AEM e la creazione di frammenti di contenuto.

## Risorse aggiuntive {#additional-resources}

* AEM Percorso di sviluppatori headless
   * [Scopri lo sviluppo di CMS Headless](/help/journey-headless/developer/learn-about.md)
   * [Scopri come modellare il contenuto](/help/journey-headless/developer/model-your-content.md)

* percorso di architetti di contenuti headless AEM

* AEM Percorso di traduzione dei contenuti headless