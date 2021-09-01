---
title: Sviluppo headless per AEM Sites as a Cloud Service
description: Scopri come AEM potenti funzionalità headless del Cloud Service come Modelli di contenuto, Frammenti di contenuto e API GraphQL collaborano per consentire di gestire le esperienze a livello centrale e distribuirle tra i vari canali.
exl-id: 24300499-ae9c-49d0-aa25-f51e14d9cf79
source-git-commit: 387e75faeccb0671a32a54ff0c12f05219844311
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 1%

---


# Sviluppo headless per AEM Sites as a Cloud Service {#headless-development}

Scopri come AEM potenti funzionalità headless del Cloud Service come Modelli di contenuto, Frammenti di contenuto e API GraphQL collaborano per consentire di gestire le esperienze a livello centrale e distribuirle tra i vari canali.

## Panoramica {#overview}

L’implementazione headless sta diventando sempre più importante per la distribuzione di esperienze al pubblico, ovunque si trovi e indipendentemente dal canale utilizzato.

L’implementazione headless dimentica la gestione di pagine e componenti come avviene nelle soluzioni complete stack e ibride e si concentra sulla creazione di frammenti di contenuto riutilizzabili e neutri per i canali e sulla loro distribuzione cross-channel. Si tratta di un modello di sviluppo moderno e dinamico per l’implementazione di esperienze web.

![Modelli di implementazione AEM](assets/aem-implementation-models.png)

## Confronto headful e Headless {#headful-headless}

Questo documento si concentra sul modello di implementazione senza testa di AEM completo. Tuttavia headful contro headless non deve essere una scelta binaria in AEM. Le funzioni headless consentono di gestire e distribuire i contenuti a diversi endpoint, consentendo agli autori di contenuti di modificare applicazioni a pagina singola. Tutto in AEM.

>[!TIP]
>
>Per ulteriori informazioni, consulta il documento [Headful and Headless in AEM](/help/implementing/developing/headful-headless.md) .

## AEM come Cloud Service e senza testa {#aem-headless}

AEM come Cloud Service è uno strumento flessibile per il modello di implementazione headless offrendo tre potenti servizi:

1. Modelli di contenuto
   * I modelli di contenuto sono una rappresentazione strutturata del contenuto.
   * Questi sono definiti dagli architetti delle informazioni nell’editor AEM modello di frammento di contenuto .
   * I modelli di contenuto fungono da base per i frammenti di contenuto.
1. Frammenti di contenuto
   * I frammenti di contenuto sono istanze di modelli di contenuto.
   * Vengono create dagli autori di contenuti tramite l’editor Frammento di contenuto AEM.
   * Vengono memorizzati in AEM Assets e gestiti nell’interfaccia utente di amministrazione delle risorse.
1. API di contenuto per la consegna
   * L’API GraphQL di AEM supporta la distribuzione di frammenti di contenuto.
   * L’API REST di AEM Assets supporta le operazioni CRUD relative ai frammenti di contenuto.
   * La consegna diretta del contenuto è possibile anche con l&#39;esportazione JSON del componente core [Frammento di contenuto .](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)

## I tuoi primi passi con AEM senza testa {#first-steps}

Sono disponibili numerose risorse per iniziare a utilizzare AEM funzionalità headless. Sono destinati a diversi casi d’uso, ma tutti offrono una panoramica solida delle AEM funzioni headless.

| Risorsa | Descrizione | Tipo | Pubblico | Est Tempo |
|---|---|---|---|---|
| [Percorso per sviluppatori headless](/help/journey-headless/developer/overview.md) | **Per gli utenti nuovi a AEM e** headlesstechnology, inizia qui per un&#39;introduzione completa a AEM e le sue caratteristiche headless dalla teoria dei headless attraverso il vivere con il tuo primo progetto headless. | Guida | Sviluppatori **nuovi AEM e headless** | 1 ora |
| [Guida introduttiva a Headless](/help/implementing/developing/headless/getting-started/introduction.md) | **Per** gli AEM esperti che necessitano di un breve riepilogo delle funzioni principali AEM headless, consulta questa panoramica di avvio rapido. | Guida introduttiva | Sviluppatori, amministratori **con AEM esperienza** | 20 minuti |
| [Guida introduttiva a AEM tutorial pratico headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) | **Se preferisci un approccio pratico e conosci AEM**, questa esercitazione si divide direttamente in creazione di un semplice progetto headless. | Esercitazione | Sviluppatori | 2 ore |
