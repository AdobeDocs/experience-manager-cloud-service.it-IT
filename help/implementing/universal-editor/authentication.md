---
title: Autenticazione dell’editor universale
description: Scopri come l’editor universale si autentica.
source-git-commit: 0e66c379e10d275610d85a699da272dc0c32a9a8
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# Autenticazione dell’editor universale {#authentication}

Scopri come l’editor universale si autentica.

## Opzioni {#options}

L’editor universale utilizza l’autenticazione Identity Management System (IMS) di Adobe, fornita tramite la shell unificata.

Tutte le applicazioni/pagine remote sono responsabili dell&#39;autenticazione ai sistemi back-end richiesti. Il servizio Universal Editor richiede questa autenticazione ai sistemi di back-end per eseguire operazioni CRUD in quanto si tratta di un servizio indipendente.

## Flusso standard {#standard-flow}

Questa è la soluzione per AEM e AMS che utilizzano IMS per utilizzare l’editor universale.

Per utilizzare l’editor universale, l’utente deve essere connesso alla shell unificata che si autentica su IMS. Il token IMS fornito viene memorizzato nell’archivio delle sessioni degli utenti.

Ogni volta che un utente esegue un’operazione CRUD, viene inviata una chiamata al servizio Universal Editor con il token portatore IMS nell’intestazione HTTP. Il servizio Universal Editor utilizza quindi il token portatore per autenticare la richiesta rispetto al sistema di back-end AEM per eseguire operazioni a nome dell’utente.

![Flusso di autenticazione standard](assets/standard-flow.png)

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni sull’editor universale, consulta questi documenti.

* [Introduzione all’editor universale](introduction.md) - Scopri come l’editor universale consente di modificare qualsiasi aspetto di qualsiasi contenuto in qualsiasi implementazione per fornire esperienze eccezionali, velocizzare i contenuti e fornire un’esperienza di sviluppo all’avanguardia.
* [Creazione di contenuti con l’editor universale](authoring.md) - Scopri quanto è semplice e intuitivo per gli autori di contenuti creare contenuti utilizzando l’Editor universale.
* [Pubblicazione di contenuti con l’editor universale](publishing.md) - Scopri in che modo Universal Visual Editor pubblica i contenuti e come le tue app possono gestire i contenuti pubblicati.
* [Guida introduttiva all’Editor universale in AEM](getting-started.md) - Scopri come accedere all’editor universale e come iniziare a strumentalizzare la tua prima app AEM per utilizzarla.
* [Architettura dell’editor universale](architecture.md) - Scopri l’architettura dell’Editor universale e il flusso di dati tra i suoi servizi e livelli.
* [Attributi e tipi](attributes-types.md) - Scopri gli attributi e i tipi di dati richiesti dall’Editor universale.
