---
title: percorso di architetti di contenuti headless AEM
description: Introduzione alle funzioni avanzate, flessibili e headless di Adobe Experience Manager as a Cloud Service e modello dei contenuti per il progetto.
index: false
hide: true
hidefromtoc: true
source-git-commit: 41ad9e8ee77ae4494d28026b5ad9da45c06eaeaf
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 0%

---


# Modellazione dei contenuti per headless con AEM - Introduzione {#architect-headless-introduction}

In questa parte del Percorso [AEM architetto di contenuti headless](overview.md), puoi imparare i concetti e la terminologia di base necessari per comprendere la modellazione dei contenuti per la distribuzione di contenuti headless con Adobe Experience Manager (AEM) come Cloud Service.

Questo documento ti aiuta a comprendere la distribuzione headless dei contenuti, come AEM supporta gli headless e come viene modellato il contenuto per gli headless. Dopo la lettura è necessario:

* Comprendi i concetti di base sulla distribuzione di contenuti headless.
* Verificare come AEM supporta la modellazione headless e content.

## Obiettivo {#objective}

* **Pubblico**: Principiante
* **Obiettivo**: Introduce i concetti e la terminologia relativi alla modellazione dei contenuti headless.

## Distribuzione completa dei contenuti {#full-stack}

Sin dall&#39;introduzione dei sistemi di gestione dei contenuti (CMS), facili da usare e su larga scala, le aziende li hanno sfruttati come posizione centrale per gestire messaggi, branding e comunicazioni. Utilizzando il CMS come punto centrale per l&#39;amministrazione delle esperienze, è possibile migliorare l&#39;efficienza eliminando la necessità di duplicare attività in sistemi diversi.

![Il classico CMS full-stack](/help/journey-headless/developer/assets/full-stack.png)

In un CMS completo, tutte le funzionalità per la manipolazione dei contenuti si trovano nel CMS. Le caratteristiche del sistema compongono diversi componenti dello stack CMS. La soluzione completa offre molti vantaggi.

* C&#39;è un sistema da mantenere.
* I contenuti vengono gestiti a livello centrale.
* Tutti i servizi del sistema sono integrati.
* L’authoring dei contenuti è semplice.

Quindi, se è necessario aggiungere un nuovo canale o supportare nuovi tipi di esperienze, è possibile inserire uno (o più) nuovi componenti nello stack e c&#39;è una sola posizione per apportare modifiche.

![Aggiunta di un nuovo canale alla pila](/help/journey-headless/developer/assets/adding-channel.png)

Tuttavia, la complessità delle dipendenze all’interno dello stack diventa rapidamente evidente, poiché altri elementi nello stack devono essere regolati per adattarsi alle modifiche.

## Testa senza testa {#the-head}

La testa di qualsiasi sistema è generalmente il renderer di output di quel sistema, tipicamente sotto forma di un&#39;interfaccia grafica o di un&#39;altra uscita grafica.

Quando parliamo di un CMS headless, il CMS gestisce i contenuti e continua a consegnarli ai consumatori. Tuttavia, consegnando solo il **contenuto** in modo standardizzato, un CMS headless omette il rendering finale dell&#39;output, lasciando al servizio che consuma la **presentazione** dei contenuti.

![CMS headless](/help/journey-headless/developer/assets/headless-cms.png)

I servizi che consumano, siano essi esperienze AR, un webshop, esperienze mobili, app web progressive (PWA), ecc, prendono i contenuti dal CMS headless e forniscono il loro rendering. Si prendono cura di fornire le proprie teste per i contenuti.

Omettendo la testa si semplifica il CMS rimuovendo la complessità. In questo modo si sposta anche la responsabilità di rendere i contenuti ai servizi che ne hanno effettivamente bisogno e che sono spesso più adatti a tale rendering.

## Modellazione dei contenuti {#content-modeling}

La modellazione dei contenuti (nota anche come modellazione dei dati) è una vostra specialità, quindi cosa deve essere considerato durante la modellazione per senza testa?

Affinché le applicazioni headless possano accedere ai contenuti e utilizzarli, il contenuto deve avere una struttura predefinita. Sarebbe possibile avere i contenuti come forma libera, ma renderebbe la vita *molto* complicata per le applicazioni.

In qualità di architetto di contenuti, AEM eseguire la modellazione dei contenuti per progettare una gamma di **Modelli di frammenti di contenuto**. Definiscono la struttura utilizzata dagli autori dei contenuti per creare i **Frammenti di contenuto** che contengono il contenuto.

### Accesso al contenuto {#access-content}

Questo è più un dettaglio di sviluppo - ma potrebbe interessarvi, solo per completare la storia.

Dopo aver creato i modelli di frammento di contenuto e dopo che gli autori li hanno utilizzati per generare il contenuto, le applicazioni headless dovranno accedere a tale contenuto.

Adobe Experience Manager (AEM) come Cloud Service, può accedere in modo selettivo ai frammenti di contenuto utilizzando l’API GraphQL di AEM, per restituire solo il contenuto necessario. Utilizzando l’API, uno sviluppatore può formulare query per la selezione di contenuti specifici.Questo processo di selezione si basa sui *modelli di frammenti di contenuto*.

Questo significa che il progetto può realizzare una distribuzione headless di contenuti strutturati da utilizzare nelle applicazioni.

## Novità {#whats-next}

Dopo aver appreso i concetti e la terminologia, il passaggio successivo è [Scopri le basi della modellazione con Modelli di frammenti di contenuto](basics.md).

## Risorse aggiuntive {#additional-resources}

* AEM Percorso di sviluppatori headless
   * [Scopri lo sviluppo di CMS Headless](/help/journey-headless/developer/learn-about.md)
   * [Scopri come modellare il contenuto](/help/journey-headless/developer/model-your-content.md)
