---
title: Modellazione dei contenuti per AEM come CMS headless - Introduzione
description: Introduzione all’utilizzo delle funzioni di Adobe Experience Manager as a Cloud Service come CMS headless per la modellazione dei contenuti del tuo progetto.
exl-id: 62061d73-6fdb-440b-a7dd-b0d530d49186
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 92%

---

# Modellazione dei contenuti per AEM come CMS headless - Introduzione {#architect-headless-introduction}

In questa parte del [Percorso Architect di contenuti AEM headless](overview.md), puoi imparare i concetti e la terminologia (di base) necessari per comprendere la modellazione dei contenuti quando utilizzi Adobe Experience Manager (AEM) as a Cloud Service come CMS headless.

Questo documento ti aiuta a comprendere cos’è la distribuzione headless dei contenuti, come è supportata da AEM e come vengono modellati i contenuti per questo tipo di distribuzione. Dopo la lettura dovresti:

* Comprendere i concetti di base sulla distribuzione headless dei contenuti.
* Comprendere come AEM supporta l’headless e la modellazione dei contenuti.

## Obiettivo {#objective}

* **Pubblico**: principiante
* **Obiettivo**: introdurre i concetti e la terminologia relativi alla modellazione dei contenuti headless.

## Distribuzione contenuti full-stack {#full-stack}

Fin dall&#39;introduzione dei sistemi CMS (Content Management System) su larga scala e facili da utilizzare, le aziende hanno utilizzato questi sistemi come posizione centrale per gestire messaggi, branding e comunicazioni. Utilizzando il CMS come punto centrale per l’amministrazione delle esperienze, è possibile migliorare l’efficienza eliminando la necessità di duplicare attività in sistemi diversi.

![CMS full-stack classico](/help/journey-headless/developer/assets/full-stack.png)

In un CMS full-stack, tutte le funzionalità per la manipolazione dei contenuti si trovano nel CMS. Le funzionalità del sistema sono articolate nei diversi componenti dello stack CMS. La soluzione full-stack offre molti vantaggi.

* Occorre gestire un solo sistema.
* I contenuti vengono gestiti a livello centrale.
* Tutti i servizi del sistema sono integrati.
* L’authoring dei contenuti è semplice.

Quindi, se è necessario aggiungere un nuovo canale o supportare nuovi tipi di esperienze, è possibile inserire uno (o più) componenti nuovi nello stack e c’è una sola posizione per apportare modifiche.

![Aggiunta di un nuovo canale nello stack](/help/journey-headless/developer/assets/adding-channel.png)

Tuttavia, la complessità delle dipendenze all’interno dello stack diventa subito evidente, poiché altri elementi nello stack devono essere regolati per adattarsi alle modifiche.

## La “testa” in headless {#the-head}

La “testa” di qualsiasi sistema è generalmente il renderer di output di quel sistema, tipicamente un&#39;interfaccia utente grafica o un altro tipo di output grafico.

Quando parliamo di un CMS headless, il CMS gestisce i contenuti e continua a consegnarli ai consumatori. Tuttavia, consegnando solo il **contenuto** in modo standardizzato, un CMS headless omette il rendering finale dell’output, lasciando la **presentazione** del contenuto al servizio utilizzato.

![CMS headless](/help/journey-headless/developer/assets/headless-cms.png)

I servizi utilizzati, siano essi esperienze AR, un webshop, esperienze mobili, app web progressive (PWA), ecc., prendono i contenuti dal CMS headless e forniscono il loro rendering. Si occupano di fornire le teste per i tuoi contenuti.

Omettendo la “testa” si semplifica il CMS rimuovendo la complessità. In questo modo si sposta anche la responsabilità di eseguire il rendering dei contenuti ai servizi che ne hanno effettivamente bisogno e che sono spesso più adatti a tale rendering.

## Modellazione dei contenuti {#content-modeling}

La modellazione dei contenuti (nota anche come modellazione dei dati) è la tua specialità, quindi cosa deve essere preso in considerazione durante la modellazione per headless?

Affinché le applicazioni headless possano accedere ai contenuti e utilizzarli, il contenuto deve avere una struttura predefinita. I contenuti potrebbero anche non essere strutturati, ma per le applicazioni sarebbe *molto* più complesso accedere ad essi.

Con AEM potrai, in qualità di architetto di contenuti, eseguire la modellazione dei contenuti per progettare una serie di **Modelli per frammenti di contenuto**. Definiscono la struttura utilizzata dagli autori dei contenuti quando creano i **Frammenti di contenuto** che racchiudono il contenuto.

### Accesso al contenuto {#access-content}

Questo è più di un dettaglio di sviluppo, ma potrebbe interessarti anche solo per avere un quadro completo.

Dopo aver creato i modelli per frammenti di contenuto e averli utilizzati dagli autori per generare il contenuto, le applicazioni headless dovranno accedere a tale contenuto.

Adobe Experience Manager (AEM) as a Cloud Service può accedere in modo selettivo ai frammenti di contenuto utilizzando l’API GraphQL di AEM, per restituire solo il contenuto necessario. Utilizzando l’API, uno sviluppatore può formulare query per la selezione di contenuti specifici. Questo processo di selezione si basa sui *tuoi* Modelli per frammenti di contenuto.

Questo significa che il progetto può realizzare una distribuzione headless di contenuti strutturati da utilizzare nelle applicazioni.

## Passaggio successivo {#whats-next}

Ora che hai imparato i concetti e la terminologia, il passo successivo è [Scoprire le nozioni di base sulla modellazione con i modelli per frammenti di contenuto](basics.md).

## Risorse aggiuntive {#additional-resources}

* Percorso per sviluppatori headless di AEM
   * [Scopri di più sullo sviluppo di CMS headless](/help/journey-headless/developer/learn-about.md)
   * [Scopri come modellare il contenuto](/help/journey-headless/developer/model-your-content.md)
