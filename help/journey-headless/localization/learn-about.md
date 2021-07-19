---
title: Scopri i contenuti headless e come localizzare in AEM
description: Scopri concetti headless, come si mappano a AEM e la teoria della localizzazione AEM.
source-git-commit: 22ca7c01bfddb407c119de7d9a4d105941772664
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 0%

---

# Scopri i contenuti headless e come localizzare in AEM {#learn-about}

Scopri concetti headless, come si mappano a AEM e la teoria della localizzazione AEM.

## Obiettivo {#objective}

Questo documento ti aiuta a comprendere la distribuzione headless dei contenuti, come AEM supporta la funzione headless e come localizzare tali contenuti. Dopo la lettura è necessario:

* Comprendi i concetti di base sulla distribuzione di contenuti headless.
* Verificare come AEM supporta la localizzazione e l&#39;headless.

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

La complessità delle dipendenze all’interno dello stack diventa rapidamente evidente, in quanto altri elementi dello stack devono essere regolati per adattarsi alle modifiche.

## Testa senza testa {#the-head}

La testa di qualsiasi sistema è generalmente il renderer di output di quel sistema, tipicamente sotto forma di un&#39;interfaccia grafica o di un&#39;altra uscita grafica.

Quando parliamo di un CMS headless, il CMS gestisce i contenuti e continua a consegnarli ai consumatori. Tuttavia, consegnando solo il **contenuto** in modo standardizzato, un CMS headless omette il rendering finale dell&#39;output, lasciando al servizio che consuma la **presentazione** dei contenuti.

![CMS headless](/help/journey-headless/developer/assets/headless-cms.png)

I servizi che consumano, siano essi esperienze AR, un webshop, esperienze mobili, app web progressive (PWA), ecc, prendono i contenuti dal CMS headless e forniscono il loro rendering. Si prendono cura di fornire le proprie teste per i contenuti.

Omettendo la testa si semplifica il CMS rimuovendo la complessità. In questo modo si sposta anche la responsabilità di rendere i contenuti ai servizi che ne hanno effettivamente bisogno e che sono spesso più adatti a tale rendering.

## Localizzazione dei contenuti headless in AEM {#localizing-in-aem}

Oltre ad offrire strumenti affidabili per la creazione, la gestione e la distribuzione di pagine web tradizionali in modalità impilata, AEM offre anche la possibilità di creare selezioni di contenuti indipendenti e di distribuirle senza testa.

La potenza di AEM consente di distribuire contenuti headless, full-stack o contemporaneamente in entrambi i modelli. Per gli specialisti di localizzazione, lo stesso set di strumenti di localizzazione può essere applicato a entrambi i tipi di contenuti, offrendo un approccio unificato per la traduzione dei contenuti.

## Novità {#what-is-next}

Grazie per aver iniziato sul vostro percorso di localizzazione senza testa AEM! Dopo aver letto questo documento, è necessario:

* Comprendi i concetti di base sulla distribuzione di contenuti headless.
* Verificare come AEM supporta la localizzazione e l&#39;headless.

Sviluppa questa conoscenza e continua il tuo percorso di localizzazione senza testa AEM esaminando il documento [Inizia con AEM localizzazione senza testa](getting-started.md) dove avrai una panoramica di come AEM gestire i contenuti headless e conoscere i suoi strumenti di localizzazione.

## Risorse aggiuntive {#additional-resources}

Mentre si consiglia di passare alla parte successiva del percorso di localizzazione headless esaminando il documento [Guida introduttiva alla localizzazione headless AEM,](getting-started.md) sono riportate di seguito alcune risorse aggiuntive facoltative che consentono di approfondire alcuni concetti menzionati in questo documento, ma non è necessario che continuino sul percorso headless.

* [MSM e traduzione](/help/sites-cloud/administering/msm-and-translation.md)  - I dettagli di AEM Multi-Site Manager e come funziona con i suoi strumenti di traduzione
