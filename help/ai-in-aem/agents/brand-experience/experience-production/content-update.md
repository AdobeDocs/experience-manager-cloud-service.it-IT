---
title: Processo di aggiornamento contenuti
description: Scopri cos’è il processo di aggiornamento dei contenuti di Brand Experience Agent e cosa può fare per te.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: e2d1dae8-38de-4357-bb14-ad35acb71aee
source-git-commit: baf12e49dadc7b25f5169279a52d5712380445de
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 2%

---


# Processo di aggiornamento contenuti {#content-update}

Il processo di aggiornamento dei contenuti di [Experience Production Agent](/help/ai-in-aem/agents/brand-experience/experience-production/overview.md) automatizza la produzione dei contenuti per accelerare le attività quotidiane per Adobe Experience Manager (AEM) as a Cloud Service e Edge Delivery Services.

## Panoramica {#overview}

Il processo di aggiornamento del contenuto aggiorna il contenuto esistente, inclusi frammenti di contenuto, pagine, moduli e risorse. Il processo può eseguire azioni quali l’aggiornamento, la rimozione, la sostituzione o l’aggiunta di elementi di contenuto per mantenere le esperienze accurate e correnti. Gli input possono essere descrizioni in linguaggio naturale e, se utilizzati con Jira PDF e screenshot, possono fornire anche input.

Il processo di aggiornamento dei contenuti trasforma i dettagli forniti, tramite linguaggio naturale o visualizzazioni, in aggiornamenti dei contenuti sulla pagina. Fornisci l’URL di una pagina da aggiornare, insieme ai dettagli su cosa è necessario aggiornare e all’abilità dell’agente che completa l’attività. Se utilizzato con Adobe Experience Manager (AEM) as a Cloud Service, il processo crea un nuovo [lancio](/help/sites-cloud/authoring/launches/overview.md) che consente di rivedere gli aggiornamenti prima di applicare. Se utilizzato con la creazione di documenti, il processo crea una nuova [versione](https://experienceleague.adobe.com/en/docs/experience-manager-learn/sites/document-authoring/how-to/document-versions#).

## Funzionalità {#capabilities}

Puoi accedere all’abilità di aggiornamento del contenuto da:

* [L’Assistente AI](#ai-assistant)
* [Jira](#jira)

## Assistente IA {#ai-assistant}

Puoi accedere al processo in AEM tramite l’Assistente AI.

Apri l&#39;Assistente IA da [`experience.adobe.com`,](https://experience.adobe.com) e inizia a interagire specificando il prompt nel linguaggio naturale utilizzando il campo `Ask AI Assistant anything`:

![Processo di aggiornamento contenuto](/help/ai-in-aem/agents/brand-experience/experience-production/assets/content-update-ai-assistant-example.png)

### Configurazione dell’URL di pubblicazione {#configuring-the-publish-url}

Per utilizzare un URL di pubblicazione (con interfaccia pubblica) è necessario effettuare una configurazione una tantum:

* Prerequisiti:

   * Per effettuare la configurazione, l’utente deve disporre dei diritti di amministratore di sistema o di amministratore di prodotto.

* Configurazione:

   1. Richiama l’abilità Aggiornamento contenuto richiedendo un aggiornamento del contenuto per l’URL.
   1. L’assistente ti guiderà attraverso la configurazione, facendoti una serie di domande.
   1. Una volta completato, l’URL di pubblicazione viene configurato e può essere utilizzato.

Ad esempio:

![Abilità aggiornamento contenuti - configura URL di pubblicazione](/help/ai-in-aem/agents/brand-experience/experience-production/assets/content-update-publish-url-configuration.png)

### Prompt {#prompts}

Per avviare gli aggiornamenti dei contenuti è possibile inviare una vasta gamma di prompt in linguaggio naturale. È necessario specificare l’URL pubblico (di pubblicazione) o l’URL dell’ambiente di authoring della pagina da aggiornare. Alcuni, ma non tutti, i verbi supportati; sostituisci, aggiorna, rimuovi, modifica, revisionato, modifica, regola, elimina.

>[!NOTE]
>
>I caricamenti di file possono essere utilizzati quando si interagisce utilizzando [Jira](#jira), ma non sono supportati con l&#39;Assistente IA.

### Prompt di esempio {#sample-prompts}

I prompt di esempio includono:

* il `<your-publish-URL>` aggiornamento &quot;Il tuo caffè perfetto è tra quattro domande&quot; a &quot;Il tuo caffè, a modo tuo!&quot;
* il `<your-author-env-URL>` sostituire l&#39;immagine da &quot;holdingcup.png&quot; a &quot;stairhead.png&quot;
* il `<your-publish-URL>` cambia il pulsante &quot;Passa al quiz&quot; in una versione più coinvolgente&quot;
* il `<your-author-env-URL>` rimuovere la sezione &quot;Premi non rivendicati è un Regalo mancato!&quot;

## Jira {#jira}

L’utilizzo del processo di aggiornamento del contenuto con Jira consente di creare un ticket con istruzioni che automatizzano le modifiche.

### Creare un ticket {#create-a-ticket}

Crea un ticket Jira (di qualsiasi tipo). Nel campo **Descrizione** del ticket sono necessari due dettagli essenziali:

1. L’URL pubblico della pagina da modificare.

1. Le modifiche necessarie.

   Per descrivere le modifiche, il processo supporta la seguente gamma di formati:

   * Lingua naturale nella descrizione del biglietto
      * ad esempio &quot;Cambia il titolo da X a Y&quot;
   * PDF con annotazioni allegato
      * ad esempio, crea un PDF della pagina e aggiungi annotazioni che descrivono ciò che desideri modificare
   * Commenti in PDF allegato
      * ad esempio, crea un PDF della pagina e aggiungi commenti che descrivono ciò che desideri modificare
   * Schermata con annotazioni allegata
      * ad esempio, scegli una schermata di parte della pagina e aggiungi annotazioni che descrivono ciò che desideri modificare
   * File di Microsoft Word allegato, contenente le modifiche della lingua naturale

### Richiama il processo dal ticket {#invoke-the-job-from-your-ticket}

Per utilizzare il processo, aggiungi un commento al ticket. Nel commento indicare il processo con il simbolo `@`, insieme alle istruzioni.

Ad esempio:

* `@aemagent@adobe.com process this ticket`

### Interazione del processo {#how-the-agent-interacts}

Dopo aver inviato un comando al processo, questo risponde con commenti nella Jira. I commenti descrivono nel dettaglio l’avanzamento del processo e le azioni intraprese.

Nel caso di un comando `process` per attivare gli aggiornamenti, le risposte potrebbero seguire la sequenza:

* Il commento iniziale conferma l&#39;avvio del processo.

* Una volta completata l’attività, il processo risponde con un altro commento contenente i dettagli delle azioni intraprese.
   * Gli aggiornamenti del contenuto effettuati dal processo non sono distruttivi, ovvero vengono effettuati in un’istanza di anteprima.
   * Il commento contiene collegamenti agli aggiornamenti, in modo da poter rivedere e pubblicare come necessario, o assegnare la Jira a chi sarà responsabile.

* Nell&#39;immagine seguente viene illustrato un esempio di Jira che attiva il comando `process` per il processo di aggiornamento del contenuto:

  ![Esempio di Jira tramite il processo di aggiornamento del contenuto dell&#39;agente esperienza marchio](assets/content-update-jira-example.png)

## Attivazione {#activation}

Puoi esplorare gli agenti AEM tramite [Playground](https://www.aem.live/developer/aem-playground) oppure connetterti con il tuo CSM o TAM per discutere dell&#39;accesso tramite lo SKU agente.

## Limitazioni {#limitations}

Tieni presente le seguenti limitazioni:

* I caricamenti di file possono essere utilizzati quando si interagisce con [Jira](#jira), ma non sono supportati quando si interagisce con l&#39;Assistente di [IA.](#ai-assistant)
