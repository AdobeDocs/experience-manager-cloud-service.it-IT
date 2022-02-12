---
title: Introduzione a AEM senza testa
description: Risorse di supporto autonomo e collegamenti alla documentazione di Adobe Experience Manager (AEM) Headless. Scopri come le funzioni come Modelli di contenuto, Frammenti di contenuto e API GraphQL vengono utilizzate per sviluppare esperienze headless con AEM.
landing-page-description: Scopri come utilizzare e amministrare Experience Manager Headless as a Cloud Service.
exl-id: 24300499-ae9c-49d0-aa25-f51e14d9cf79
source-git-commit: c5d67e0ece40cdf7a9009436ec90305fe81425a2
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 2%

---


# Introduzione ad Adobe Experience Manager Headless  {#introduction-aem-headless}

Scopri come le funzioni di Adobe Experience Manager (AEM) come Modelli di contenuto, Frammenti di contenuto e un’API GraphQL vengono utilizzate per sviluppare esperienze headless su scala.

## Panoramica {#overview}

AEM Headless è una soluzione CMS di Experience Manager che consente di utilizzare contenuti strutturati (frammenti di contenuto) in AEM da qualsiasi app tramite HTTP tramite GraphQL. Le implementazioni headless consentono la distribuzione di esperienze su piattaforme e canali su larga scala.

L’implementazione headless dimentica la gestione di pagine e componenti come avviene nelle soluzioni complete stack e ibride e si concentra sulla creazione di frammenti di contenuto riutilizzabili e neutri per i canali e sulla loro distribuzione cross-channel. Si tratta di un modello di sviluppo moderno e dinamico per l’implementazione di esperienze web.

![Modelli di implementazione AEM](assets/aem-implementation-models.png)

## Caratteristiche di AEM senza testa {#aem-headless-features}

AEM as a Cloud Service è uno strumento flessibile per il modello di implementazione headless, che offre tre potenti caratteristiche:

1. **Modelli di contenuto**
   * I modelli di contenuto sono una rappresentazione strutturata del contenuto.
   * I modelli di contenuto sono definiti dagli architetti di informazioni nell’editor AEM modello di frammento di contenuto .
   * I modelli di contenuto fungono da base per i frammenti di contenuto.
1. **Frammenti di contenuto**
   * I frammenti di contenuto vengono creati in base a un modello di contenuto.
   * Creati dagli autori di contenuti tramite l’editor Frammento di contenuto AEM.
   * I frammenti di contenuto sono memorizzati in AEM Assets e gestiti nell’interfaccia utente di amministrazione delle risorse.
1. **API di contenuto per la consegna**
   * L’API GraphQL di AEM supporta la distribuzione di frammenti di contenuto.
   * L’API REST di AEM Assets supporta le operazioni CRUD relative ai frammenti di contenuto.
   * La consegna diretta dei contenuti è possibile anche con [Esportazione JSON del componente core Frammento di contenuto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html).

## I tuoi primi passi con AEM senza testa {#first-steps}

Sono disponibili diverse risorse per iniziare a utilizzare AEM funzionalità headless. Ogni guida è personalizzata per diversi casi d’uso e tipi di pubblico.

| Risorsa | Descrizione | Tipo | Pubblico | Est Tempo |
|---|---|---|---|---|
| [Percorso per sviluppatori headless](/help/journey-headless/developer/overview.md) | **Per gli sviluppatori non esperti in AEM e headless** tecnologie, inizia qui per un&#39;introduzione completa a AEM e le sue caratteristiche headless dalla teoria dei headless attraverso il vivere con il tuo primo progetto headless. | Guida | Sviluppatori **nuovo a AEM e senza testa** | 1 ora |
| [Configurazione headless](/help/headless/setup/introduction.md) | **Per utenti AEM esperti** per un breve riepilogo delle funzioni principali AEM headless, consulta questa panoramica rapida. | Configurazione di riferimento | Sviluppatori e amministratori **con esperienza AEM** | 20 minuti |
| [Tutorial pratico headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) | **Se preferisci un approccio pratico e hai familiarità con AEM**, questa esercitazione si basa direttamente sull’implementazione di una semplice app headless. | Esercitazione | Sviluppatori | 2 ore |
| [Percorso architetto headless](/help/journey-headless/architect/overview.md) | **Per architetti nuovi a AEM e senza testa** Le tecnologie sono disponibili qui per un’introduzione alle funzionalità avanzate, flessibili e headless di Adobe Experience Manager as a Cloud Service e a come modellare i contenuti per il progetto. | Guida | Architetti | 1 ora |
| [Percorso di authoring headless](/help/journey-headless/author/overview.md) | **Per gli utenti aziendali nuovi a AEM e headless** Le tecnologie sono disponibili qui per un’introduzione alle funzionalità avanzate, flessibili e headless di Adobe Experience Manager as a Cloud Service e a come modellare i contenuti per il progetto. | Guida | Creatori di contenuti | 1 ora |
| [Percorso di traduzione headless](/help/journey-headless/translation/overview.md) | Per quelli **interessato AEM approccio di traduzione a headless**. Scopri le tecnologie headless e come creare e aggiornare progetti di traduzione in AEM da A a Z. | Guida | Specialisti di traduzione | 1 ora |

## Confronto headful e Headless {#headful-headless}

Questa guida si concentra sul modello di implementazione headless completo di AEM. Tuttavia headful contro headless non deve essere una scelta binaria in AEM. Le funzioni headless consentono di gestire e distribuire contenuti a più punti di contatto, consentendo agli autori di contenuti di modificare applicazioni a pagina singola. Tutto in AEM.

>[!TIP]
>
>Vedere il documento [Cefalea e senza testa in AEM](/help/implementing/developing/headful-headless.md) per ulteriori informazioni.