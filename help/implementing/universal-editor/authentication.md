---
title: Autenticazione dell’editor universale
description: Scopri come l’editor universale effettua l’autenticazione.
source-git-commit: 0e66c379e10d275610d85a699da272dc0c32a9a8
workflow-type: ht
source-wordcount: '326'
ht-degree: 100%

---


# Autenticazione dell’editor universale {#authentication}

Scopri come l’editor universale effettua l’autenticazione.

## Opzioni {#options}

L’editor universale utilizza l’autenticazione Identity Management System (IMS) di Adobe, fornita tramite la shell unificata.

Tutte le applicazioni/pagine remote necessitano dell’autenticazione dei sistemi back-end richiesti. Il servizio editor universale richiede questa autenticazione ai sistemi di back-end per eseguire operazioni CRUD in quanto si tratta di un servizio indipendente.

## Flusso standard {#standard-flow}

Questa è la soluzione per AEM as a Cloud Service e AMS che usano IMS per servirsi dell’editor universale.

Per utilizzare l’editor universale, l’utente deve essere connesso alla shell unificata che esegue l’autenticazione tramite IMS. Il token IMS fornito viene memorizzato nell’archivio delle sessioni degli utenti.

Ogni volta che un utente esegue un’operazione CRUD, viene inviata una chiamata al servizio editor universale con il token di connessione IMS nell’intestazione HTTP. Il servizio editor universale utilizza quindi il token di connessione per autenticare la richiesta al sistema di back-end di AEM per eseguire operazioni a nome dell’utente.

![Flusso di autenticazione standard](assets/standard-flow.png)

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni sull’editor universale, consulta questi documenti.

* [Introduzione all’editor universale](introduction.md): scopri come l’editor universale consente di modificare qualsiasi aspetto di qualsiasi contenuto in qualsiasi implementazione per offrire esperienze eccezionali, velocizzare i contenuti e fornire un’esperienza di sviluppo all’avanguardia.
* [Authoring dei contenuti con l’editor universale](authoring.md): scopri quanto è semplice e intuitivo per gli autori di contenuti creare contenuti utilizzando l’editor universale.
* [Pubblicazione di contenuti con l’editor universale](publishing.md): scopri in che modo l’editor visivo universale pubblica i contenuti e come le tue app possono gestire i contenuti pubblicati.
* [Guida introduttiva all’editor universale in AEM](getting-started.md): scopri come accedere all’editor universale e come iniziare a instrumentare la tua prima app AEM da utilizzare.
* [Architettura dell’editor universale](architecture.md): scopri l’architettura dell’editor universale e il flusso di dati tra i suoi servizi e livelli.
* [Attributi e tipi](attributes-types.md): scopri gli attributi e i tipi di dati richiesti dall’editor universale.
