---
title: Abilità di aggiornamento contenuti
description: Scopri cos’è l’abilità di aggiornamento dei contenuti dell’agente di produzione di Experience e cosa può fare per te.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 8cd524891df550913a734a9355c1012dc11adf5b
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 1%

---


# Abilità di aggiornamento contenuti {#content-update}

L’abilità di aggiornamento dei contenuti di Experience Production Agent automatizza la produzione dei contenuti per accelerare le attività quotidiane per Adobe Experience Manager (AEM) as a Cloud Service e Edge Delivery Services.

L’abilità di aggiornamento del contenuto aggiorna i contenuti esistenti in CMS, inclusi frammenti di contenuto, pagine, moduli e risorse. L’agente può eseguire azioni quali l’aggiornamento, la rimozione, la sostituzione o l’aggiunta di elementi di contenuto per mantenere le esperienze accurate e correnti. Gli input possono essere descrizioni in linguaggio naturale e, se utilizzati con Jira PDF e screenshot, possono fornire anche input.

## Panoramica {#overview}

L’abilità di aggiornamento dei contenuti trasforma i dettagli forniti, tramite linguaggio naturale o visualizzazioni, in aggiornamenti dei contenuti sulla pagina. Fornisci l’URL di una pagina da aggiornare, insieme ai dettagli su cosa è necessario aggiornare e all’abilità dell’agente che completa l’attività.

## Funzionalità {#capabilities}

Puoi accedere all’abilità di aggiornamento del contenuto da:

* [Assistente IA](#ai-assistant)

* [Jira](#jira)

## Assistente IA {#ai-assistant}

Puoi accedere ad AEM Business Agent tramite l’Assistente AI.

Aprire l&#39;Assistente AI da experience.adobe.com, quindi iniziare a interagire specificando il prompt nel linguaggio naturale utilizzando il campo `Ask AI Assistant anything`:

![Agente individuazione accesso](/help/ai-in-aem/agents/production/assets/content-update-ai-assistant-example.png)

### Prompt di esempio {#sample-prompts}

Per avviare gli aggiornamenti dei contenuti è possibile inviare una vasta gamma di prompt in linguaggio naturale. È inoltre necessario specificare l&#39;URL pubblico della pagina da aggiornare. Ad esempio:

* Modificare la pagina seguente https://www.your-url.com/sale Aggiornare l&#39;intestazione principale hero a &quot;Black Friday Mega Sale - Fino al 70% Off&quot;, Cambiare il timer conto alla rovescia per mostrare &quot;Termina in 48 ore&quot;, Rimuovere &quot;Registrarsi per gli aggiornamenti&quot;, Cambiare tutti i pulsanti &quot;Shop Now&quot; a &quot;Grab the Deal&quot;&quot;

* https://www.your-url.com/laptops/your-laptop-model Aggiorna la copia del banner in "Salva solo 300 USD oggi", aggiorna i prezzi da 1.299 USD a 999 USD, Rimuovi il banner dell'opzione di finanziamento

* https://www.your-url.com/your-sneaker Aggiornare lo stato delle scorte da "Magazzino basso" a "Torna a magazzino - Quantità limitate", Modificare il selettore delle dimensioni per evidenziare le dimensioni disponibili in verde, Rimuovere il badge "In arrivo"

* https://www.your-url.com/your-sneaker Aggiorna le immagini del prodotto per visualizzare nuove colorway

>[!NOTE]
>
>I caricamenti di file possono essere utilizzati quando si interagisce utilizzando [Jira](#jira), ma non sono supportati con l&#39;Assistente IA.

## Jira {#jira}

L’utilizzo dell’abilità di aggiornamento del contenuto con Jira consente di creare un ticket con istruzioni che automatizzano le modifiche.

### Creare un ticket {#create-a-ticket}

Crea un ticket Jira (di qualsiasi tipo).

Nel campo **Descrizione** del ticket sono necessari due dettagli essenziali:

1. L’URL pubblico della pagina da modificare.

1. Le modifiche necessarie.

   Al momento l’abilità supporta la seguente gamma di formati per descrivere le modifiche:

   * Lingua naturale nella descrizione del biglietto
      * ad esempio &quot;Cambia il titolo da X a Y&quot;
   * PDF con annotazioni allegato
      * ad esempio, crea un PDF della pagina e aggiungi annotazioni che descrivono ciò che desideri modificare
   * Commenti in PDF allegato
      * ad esempio, crea un PDF della pagina e aggiungi commenti che descrivono ciò che desideri modificare
   * Schermata con annotazioni allegata
      * ad esempio, scegli una schermata di parte della pagina e aggiungi annotazioni che descrivono ciò che desideri modificare
   * File di Microsoft Word allegato, contenente le modifiche della lingua naturale

### Richiama l&#39;agente dal tuo ticket {#invoke-the-agent-from-your-ticket}

Per utilizzare l’agente, aggiungi un commento al ticket. Nel commento indicare l&#39;agente con il simbolo `@`, insieme al comando che deve eseguire; ad esempio:

* `@aemagent@adobe.com process`

Attualmente, l’agente comprende i comandi:

* `process` - elabora la richiesta
* `cancel` - annulla una richiesta di elaborazione
* `retry` - rielaborazione di una richiesta
* `feedback` - Applica feedback a una generazione precedente
* `reprocess` - rielabora la richiesta originale

### Interazione dell&#39;agente {#how-the-agent-interacts}

Dopo aver inviato un comando all&#39;agente, quest&#39;ultimo risponde con commenti nella Jira. I commenti descrivono nel dettaglio l&#39;avanzamento dell&#39;agente e le azioni intraprese.

Nel caso di un comando `process` per attivare gli aggiornamenti, le risposte potrebbero seguire la sequenza:

* Il commento iniziale conferma che l&#39;agente è stato avviato.

* Una volta completata l’attività. l’agente risponde con un altro commento contenente i dettagli delle azioni intraprese.
   * Gli aggiornamenti del contenuto effettuati dall’agente non sono distruttivi, ovvero vengono eseguiti in un’istanza di anteprima.
   * Il commento contiene collegamenti agli aggiornamenti, in modo da poter rivedere e pubblicare come necessario, o assegnare la Jira a chi sarà responsabile.

* Nell&#39;immagine seguente viene illustrato un esempio di Jira che attiva il comando `process` per l&#39;abilità di aggiornamento del contenuto:

  ![Esempio di Jira utilizzando l&#39;abilità di aggiornamento del contenuto dell&#39;agente Experience Production](assets/content-update-jira-example.png)

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

## Limitazioni {#limitations}

Attualmente il Content Updater presenta le seguenti limitazioni:

* I caricamenti di file possono essere utilizzati durante l&#39;interazione con [Jira](#jira), ma non sono supportati durante l&#39;interazione con [Assistente AI](#ai-assistant).
