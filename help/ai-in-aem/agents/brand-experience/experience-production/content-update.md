---
title: Processo di aggiornamento contenuti
description: Scopri cos’è il processo di aggiornamento dei contenuti di Brand Experience Agent e cosa può fare per te.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: e2d1dae8-38de-4357-bb14-ad35acb71aee
source-git-commit: 71e3770a7a26b8d3144717513f3ec1c997b3b435
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 2%

---


# Processo di aggiornamento contenuti {#content-update}

Il processo di aggiornamento dei contenuti di [Brand Experience Agent](/help/ai-in-aem/agents/brand-experience/overview.md) automatizza la produzione dei contenuti per accelerare le attività quotidiane per Adobe Experience Manager (AEM) as a Cloud Service e Edge Delivery Services.

## Panoramica {#overview}

Il processo di aggiornamento del contenuto aggiorna il contenuto esistente, inclusi frammenti di contenuto, pagine, moduli e risorse. Il processo può eseguire azioni quali l’aggiornamento, la rimozione, la sostituzione o l’aggiunta di elementi di contenuto per mantenere le esperienze accurate e correnti. Gli input possono essere descrizioni in linguaggio naturale e, se utilizzati con Jira PDF e screenshot, possono fornire anche input.

Il processo di aggiornamento dei contenuti trasforma i dettagli forniti, tramite linguaggio naturale o visualizzazioni, in aggiornamenti dei contenuti sulla pagina. Fornisci l’URL di una pagina da aggiornare, insieme ai dettagli su cosa è necessario aggiornare e all’abilità dell’agente che completa l’attività.

## Funzionalità {#capabilities}

Puoi accedere all’abilità di aggiornamento del contenuto da:

* [L’Assistente AI](#ai-assistant)
* [Jira](#jira)

## Assistente IA {#ai-assistant}

Puoi accedere al processo in AEM tramite l’Assistente AI.

Apri l&#39;Assistente IA da [`experience.adobe.com`,](https://experience.adobe.com) e inizia a interagire specificando il prompt nel linguaggio naturale utilizzando il campo `Ask AI Assistant anything`:

![Processo di aggiornamento contenuto](/help/ai-in-aem/agents/brand-experience/experience-production/assets/content-update-ai-assistant-example.png)

### Prompt di esempio {#sample-prompts}

Per avviare gli aggiornamenti dei contenuti è possibile inviare una vasta gamma di prompt in linguaggio naturale. È inoltre necessario specificare l&#39;URL pubblico della pagina da aggiornare. Ad esempio:

* Modificare la pagina seguente `https://www.your-url.com/sale` Aggiornare l&#39;intestazione principale hero a &quot;Black Friday Mega Sale - Fino al 70% Off&quot;, Modificare il timer di conto alla rovescia per mostrare &quot;Termina in 48 ore&quot;, Rimuovere &quot;Registrarsi per gli aggiornamenti&quot;, Cambiare tutti i pulsanti &quot;Shop Now&quot; in &quot;Afferrare l&#39;offerta&quot;&quot;

* `https://www.your-url.com/laptops/your-laptop-model` Aggiorna la copia del banner in &quot;Salva solo 300 USD oggi&quot;, aggiorna i prezzi da 1.299 USD a 999 USD, rimuovi banner opzione di finanziamento

* `https://www.your-url.com/your-sneaker` Aggiornare lo stato delle scorte da &quot;Magazzino basso&quot; a &quot;Torna in magazzino - Quantità limitate&quot;, Modificare il selettore delle dimensioni per evidenziare le dimensioni disponibili in verde, Rimuovere il badge &quot;Disponibile a breve&quot;

* `https://www.your-url.com/your-sneaker` Aggiorna le immagini del prodotto per visualizzare nuove colorway

>[!NOTE]
>
>I caricamenti di file possono essere utilizzati quando si interagisce utilizzando [Jira](#jira), ma non sono supportati con l&#39;Assistente IA.

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

Per utilizzare il processo, aggiungi un commento al ticket. Nel commento indicare il processo con il simbolo `@`, insieme al comando che deve essere eseguito; ad esempio:

* `@aemagent@adobe.com process`

Attualmente, il processo comprende i comandi:

* `process` - elabora la richiesta
* `cancel` - annulla una richiesta di elaborazione
* `retry` - rielaborazione di una richiesta
* `feedback` - Applica feedback a una generazione precedente
* `reprocess` - rielabora la richiesta originale

### Interazione del processo {#how-the-agent-interacts}

Dopo aver inviato un comando al processo, questo risponde con commenti nella Jira. I commenti descrivono nel dettaglio l’avanzamento del processo e le azioni intraprese.

Nel caso di un comando `process` per attivare gli aggiornamenti, le risposte potrebbero seguire la sequenza:

* Il commento iniziale conferma l&#39;avvio del processo.

* Una volta completata l’attività, il processo risponde con un altro commento contenente i dettagli delle azioni intraprese.
   * Gli aggiornamenti del contenuto effettuati dal processo non sono distruttivi, ovvero vengono effettuati in un’istanza di anteprima.
   * Il commento contiene collegamenti agli aggiornamenti, in modo da poter rivedere e pubblicare come necessario, o assegnare la Jira a chi sarà responsabile.

* Nell&#39;immagine seguente viene illustrato un esempio di Jira che attiva il comando `process` per il processo di aggiornamento del contenuto:

  ![Jira di esempio che utilizza il processo di aggiornamento del contenuto dell&#39;agente di produzione di Experience](assets/content-update-jira-example.png)

## Attivazione {#activation}

Per attivare e accedere al processo di creazione delle comunicazioni è necessario contattare Adobe. Per iniziare puoi:

* Contatta `experience-production-agent@adobe.com`
* Oppure rivolgiti al team del tuo account

Per velocizzare il processo, è utile fornire le seguenti informazioni:

* Per AEM as a Cloud Service, devi fornire:
   * ID organizzazione
   * `product_id`
   * `profile_id`

   * Questi valori si trovano nei seguenti passaggi:
      1. L&#39;amministratore deve visitare [`https://adminconsole.adobe.com`](https://adminconsole.adobe.com)
      1. Seleziona **Adobe Experience Manager as a Cloud Service**
      1. Seleziona l’istanza di AEM appropriata
      1. Seleziona il profilo che consente le operazioni di lettura e scrittura per il contenuto in questione
      1. Acquisisci l’URL del browser
      1. Estrarre `product_id` e `profile_id` dall&#39;URL.
Ad esempio `https://adminconsole.adobe.com/products/profiles/users`

* Authoring di documenti Edge Delivery
   * Fornisci al tuo team Adobe le seguenti informazioni:
      * Domini rilevanti
      * Informazioni pertinenti su Github:
         * Organizzazione
         * Repo
         * Ramo

## Limitazioni {#limitations}

Tieni presente le seguenti limitazioni:

* I caricamenti di file possono essere utilizzati quando si interagisce con [Jira](#jira), ma non sono supportati quando si interagisce con l&#39;Assistente di [IA.](#ai-assistant)
