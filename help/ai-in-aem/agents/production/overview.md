---
title: Panoramica di Experience Production Agent
description: Scopri in che modo l’agente di produzione Experience in AEM consente di accelerare la creazione dei contenuti e di orchestrare automaticamente le modifiche.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 8cd524891df550913a734a9355c1012dc11adf5b
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 3%

---


# Panoramica di Experience Production Agent {#experience-production-agent}

Experience Production Agent automatizza le attività più impegnative e con volumi elevati. Team autonomi e processi manuali di settimane in flussi di lavoro rapidi e assistiti dall’intelligenza artificiale che mantengono ogni esperienza aggiornata e coerente, aiutando l’azienda a raggiungere i propri obiettivi.

## Jobs {#jobs}

L&#39;agente fornisce i seguenti processi:

* [Aggiornamento contenuti](#content-update)
* [Creazione modulo](#form-creation)
* [Creazione di comunicazioni](#communications-creation)
* [Migrazione del sito](#site-migration)

>[!IMPORTANT]
>
>Le risposte generate dall’intelligenza artificiale possono essere imprecise o fuorvianti. Controlla nuovamente le correzioni e le risposte suggerite.
>
>Consulta anche [Linee guida per l&#39;utente di Adobe Experience Cloud Generative AI](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html).

### Aggiornamento contenuti {#content-update}

[Aggiornamento contenuto](/help/ai-in-aem/agents/production/content-update.md) aggiorna facilmente i contenuti esistenti in CMS, inclusi frammenti di contenuto, pagine, moduli e risorse. L’agente può eseguire azioni quali l’aggiornamento, la rimozione, la sostituzione o l’aggiunta di elementi di contenuto per mantenere le esperienze accurate e correnti. Gli input possono essere descrizioni in linguaggio naturale e, se utilizzati con Jira PDF e screenshot, possono fornire anche input.

### Creazione modulo {#form-creation}

L&#39;abilità [Creazione moduli](/help/ai-in-aem/agents/production/form-creation.md) consente agli utenti di creare moduli adattivi tramite prompt in linguaggio naturale senza dipendere dai team di sviluppo o IT. Questa funzionalità accelera lo sviluppo dei moduli mantenendo al contempo la coerenza del marchio e consentendo agli utenti aziendali di creare moduli senza una profonda conoscenza tecnica dei prodotti.

### Creazione di comunicazioni {#communications-creation}

L&#39;abilità [Creazione di comunicazioni](/help/ai-in-aem/agents/production/communications-creation.md) consente agli utenti aziendali di produrre corrispondenza personalizzata e basata su dati su larga scala. Dagli estratti conto e dai documenti delle policy alle fatture e ai kit di benvenuto, l&#39;agente trasforma i requisiti di linguaggio naturale in comunicazioni professionali.

>[!NOTE]
>
> L&#39;abilità di creazione delle comunicazioni è attualmente in formato alfa. Se desideri partecipare, invia una richiesta dal tuo indirizzo e-mail ufficiale a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com).

### Migrazione del sito {#site-migration}

[Migrazione siti](/help/ai-in-aem/agents/production/site-migration.md) esegue la migrazione diretta di siti non AEM in ambienti AEM (Experience Delivery Services), garantendo che siano performanti, conformi e pronti per gli agenti. L&#39;agente semplifica la configurazione e la trasformazione, riducendo l&#39;impegno manuale e il time-to-value.

L’agente deve essere in grado di lavorare con altre competenze dell’agente, ad esempio:

## Uso con altri agenti {#use-with-other-agents}

* Ottenere risorse di origine da Experience Advisory Agent

## Attivazione {#activation}

Per attivare e accedere a Experience Production Agent è necessario contattare Adobe. Per iniziare, contatta:

* `experience-production-agent@adobe.com`
* oppure rivolgiti al team del tuo account

Per velocizzare il processo, è utile fornire le seguenti informazioni:

* Per AEM as a Cloud Service
   * Devi fornire:
      * ID organizzazione
      * `product_id`
      * `profile_id`

   * Per trovare questi valori, segui la procedura riportata di seguito.
      * L&#39;amministratore deve visitare <https://adminconsole.adobe.com/>
      * Seleziona **Adobe Experience Manager as a Cloud Service**
      * Seleziona l’istanza di AEM appropriata
      * Seleziona il profilo che consente le operazioni di lettura e scrittura per il contenuto in questione
      * Acquisisci l’URL del browser
      * Estrarre `product_id` e `profile_id` dall&#39;URL.
Ad esempio <https://adminconsole.adobe.com/products/profiles/users>

* Authoring di documenti Edge Delivery
   * Fornisci al tuo team Adobe le seguenti informazioni:
      * Domini rilevanti
      * Informazioni pertinenti su Github:
         * Organizzazione
         * Repo
         * Ramo
