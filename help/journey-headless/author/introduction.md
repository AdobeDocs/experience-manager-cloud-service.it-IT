---
title: Authoring per AEM come CMS headless - Introduzione
description: Introduzione all’utilizzo delle funzioni di Adobe Experience Manager as a Cloud Service as a Headless CMS per la creazione di contenuti per il progetto.
exl-id: 62061d73-6fdb-440b-a7dd-b0d530d49186
source-git-commit: 00ec09f327bc2f382d263970e690ed067aaa1355
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 2%

---

# Authoring per AEM come CMS headless - Introduzione {#architect-headless-introduction}

In questa parte del [AEM Percorso di authoring dei contenuti headless](overview.md), è possibile apprendere i concetti e la terminologia di base necessari per comprendere il contenuto di authoring quando si utilizza Adobe Experience Manager (AEM) as a Cloud Service come CMS headless. Ciò comporta la strutturazione e la creazione di contenuti per la distribuzione headless.

Obiettivo

* **Pubblico**: Principiante
* **Obiettivo**: Introduce i concetti e la terminologia relativi all’authoring headless.

## Sistema di gestione dei contenuti (CMS) {#objective}

* **Che cos’è un sistema di gestione dei contenuti?**
* **Un sistema di gestione dei contenuti (CMS, Content Management System) è esattamente ciò che dice - un sistema informatico utilizzato per gestire i contenuti. Questo è un po&#39; generale, quindi per essere più precisi, viene (in genere) utilizzato per gestire i contenuti che si desidera rendere disponibili sul tuo sito web.**

## CMS headless {#full-stack}

Headless è un termine utilizzato per descrivere i sistemi che staccano efficacemente il contenuto dal modo in cui vengono visualizzati sul web.

![Tradizionalmente, si gestiva il contenuto in un CMS e lo stesso CMS sarebbe responsabile del rendering di tale contenuto sulle pagine web.](/help/journey-headless/developer/assets/full-stack.png)

Ora, headless significa che il set di contenuti può essere gestito nel CMS e quindi utilizzato da una o più applicazioni (indipendenti).

* Ciò significa che i contenuti possono essere inviati a qualsiasi dispositivo, in una vasta gamma di formati. Questo rende l&#39;intero processo molto più flessibile, e significa anche che non è necessario preoccuparsi del layout e della formattazione.
* [!NOTE]
* Per ulteriori informazioni sui dettagli tecnici di Headless CMS, consulta Informazioni sullo sviluppo headless di CMS.
* Adobe Experience Manager as a Cloud Service

Allora cosa è AEM?

![Innanzitutto, AEM è un sistema di gestione dei contenuti con un&#39;ampia gamma di funzioni personalizzabili per soddisfare le tue esigenze.](/help/journey-headless/developer/assets/adding-channel.png)

Questo significa che può essere utilizzato come:

## CMS headless {#the-head}

Per i contenuti headless, è possibile creare come **Frammenti di contenuto**.
Si tratta di elementi autonomi di contenuto a cui è possibile accedere direttamente da una serie di applicazioni, in quanto dispongono di una struttura predefinita basata su **Modelli per frammenti di contenuto**.
Ciò significa che i contenuti possono raggiungere una vasta gamma di dispositivi, in una vasta gamma di formati e con un&#39;ampia gamma di funzionalità.
Inoltre, questi frammenti possono essere utilizzati anche per la creazione di pagine web AEM, se lo desideri.

CMS &quot;tradizionale&quot;********

![Il contenuto viene creato per le pagine web utilizzando una serie di componenti che definiscono come verrà eseguito il rendering del contenuto sul sito web. Anche qui AEM è estremamente flessibile in quanto il team di progetto può sviluppare componenti personalizzati.](/help/journey-headless/developer/assets/headless-cms.png)

Modellazione dei contenuti

Quindi la modellazione dei contenuti (nota anche come modellazione dei dati) è un altro termine tecnico - perché dovrebbe interessarti in qualità di autore?

## Affinché le applicazioni headless possano accedere ai contenuti e utilizzarli, il contenuto deve avere una struttura predefinita. Sarebbe possibile avere i contenuti come forma libera, ma renderebbe la vita *molto* complicato per le applicazioni. {#content-modeling}

In sostanza, il processo di definizione della struttura del contenuto da rispettare prevede la progettazione di un modello, denominato modellazione dei dati.

Per AEM il ruolo Architetto contenuto (spesso una persona diversa) eseguirà la modellazione dei dati per progettare un intervallo di **Modelli per frammenti di contenuto** - da utilizzare come base per i contenuti utilizzando **Frammenti di contenuto**.

[!NOTE]******

### Per ulteriori informazioni sulla modellazione dei dati, consulta il Percorso AEM architetto di contenuti headless . {#access-content}

Novità

Ora che hai imparato i concetti e la terminologia, il passo successivo è [Scopri le nozioni di base sulla creazione di frammenti di contenuto](basics.md). Viene introdotta la gestione di base delle AEM e la creazione di frammenti di contenuto.

Risorse aggiuntive**

AEM Percorso di sviluppatori headless

## Scopri lo sviluppo di CMS Headless {#whats-next}

Scopri come modellare il contenuto[](basics.md)

## Percorso Architect di contenuti AEM headless {#additional-resources}

* AEM Percorso di traduzione dei contenuti headless
   * [Learn About CMS Headless Development](/help/journey-headless/developer/learn-about.md)
   * [Learn how to Model Your Content](/help/journey-headless/developer/model-your-content.md)
