---
title: Agente di ottimizzazione del contenuto
description: Scopri come utilizzare l’agente di ottimizzazione dei contenuti per trasformare il modo in cui gli utenti perfezionano e adattano le risorse applicando istruzioni in linguaggio naturale per creare varianti pronte per il canale.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 3f44e74488fc73c406fefb6decc41782859d029b
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---


# Agente di ottimizzazione del contenuto {#content-optimization-agent}

L’agente di ottimizzazione dei contenuti trasforma il modo in cui gli utenti perfezionano e adattano le risorse applicando istruzioni in linguaggio naturale per creare varianti pronte per il canale. Sia che si tratti della generazione di nuove copie trasformate, della regolazione delle proprietà visive, della modifica degli sfondi o della preparazione delle risorse per canali digitali specifici, l’agente interpreta le intenzioni dell’utente ed esegue automaticamente attività di modifica complesse. Funziona perfettamente con Discovery Agent, raccogliendo le risorse trovate e producendo varianti ottimizzate utilizzando i [Dynamic Media di base con funzionalità OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) che soddisfano i requisiti di brand, canale e campagna senza alcuna attività di progettazione manuale.

Alcuni dei vantaggi chiave dell’ottimizzazione dei contenuti includono:

* **Trasformazione delle risorse senza problemi**: converte semplici prompt conversazionali in operazioni di immagine precise, quali ridimensionamento, nitidezza, mirroring o ricolorazione, eliminando la necessità di strumenti di modifica specializzati.

* **Output ottimizzati per il canale**: produce rapidamente rendering personalizzati per piattaforme specifiche come Instagram Stories, banner Web o altri punti di contatto di marketing, garantendo risorse pronte per l&#39;uso immediato.

* **Miglioramento di Creative su scala**: applica regolazioni visive e miglioramenti, ad esempio modifiche di sfondo o sovrapposizioni grafiche, per supportare flussi di lavoro creativi di grandi volumi senza rallentare il lavoro dei team.

* **[Collaborazione perfetta con Discovery Agent](/help/ai-in-aem/agents/discovery/overview.md)**: si basa sulle risorse identificate da Discovery Agent, consentendo il recupero e l&#39;ottimizzazione end-to-end delle risorse tramite conversazione naturale.

>[!IMPORTANT]
>
>Le risposte generate dall’intelligenza artificiale possono essere imprecise o fuorvianti. Controlla nuovamente le correzioni e le risposte suggerite.
>
>Consulta anche [Linee guida per l&#39;utente di Adobe Experience Cloud Generative AI](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html).

## Prerequisiti {#prerequisites-content-optimization-agent}

Per generare varianti o ottimizzazioni per le risorse immagine. Devi avere:

* Una licenza Dynamic Media valida

* Dynamic Media con OpenAPI abilitato nell’ambiente AEM as a Cloud Service.

* Le risorse in [stato approvato](/help/assets/manage-organize-assets-view.md#manage-asset-status) nell&#39;ambiente AEM as a Cloud Service.


## Competenze {#skills-content-optimization-agent}

L&#39;agente di ottimizzazione dei contenuti fornisce le seguenti competenze:

* **Comprendere le intenzioni attraverso il linguaggio naturale**

  L’agente di ottimizzazione dei contenuti interpreta le intenzioni degli utenti dai prompt del linguaggio naturale, tenendo conto del contesto di canale, campagna e pubblico per determinare le azioni di ottimizzazione più rilevanti.

* **Genera varianti di contenuto dinamico**

  L’agente di ottimizzazione del contenuto crea varianti ottimizzate come URL dinamici adatti a canali e tipi di formato diversi.

* **Ottimizza il contenuto dell&#39;immagine**

  L’agente di ottimizzazione del contenuto applica miglioramenti come la conversione del formato, le regolazioni della risoluzione, il ritaglio e la nitidezza per migliorare la qualità delle immagini.

* **Ottimizzazione risorse con più varianti**

  L&#39;agente di ottimizzazione dei contenuti può generare più varianti di immagine ottimizzate dalle risorse restituite dall&#39;agente di individuazione utilizzando un unico prompt in linguaggio naturale, consentendo agli utenti di produrre copie trasformate pronte per il canale in modo rapido ed efficiente.

## Persone {#personas-content-optimization-agent}

I responsabili marketing dei canali, persona chiave per l’agente di ottimizzazione dei contenuti, possono selezionare il contenuto sorgente ad alta risoluzione adatto e richiedere formati ottimizzati personalizzati per i loro canali e segmenti di pubblico.

Gli addetti al marketing e i dipendenti delle agenzie regionali possono inoltre utilizzare l’agente di ottimizzazione dei contenuti per generare rapidamente varianti di immagini pronte per il canale che supportano una produzione dei contenuti più rapida e coerente.

## Come accedere all’agente di ottimizzazione dei contenuti? {#access-content-optimization-agent}

Puoi accedere agli agenti in AEM tramite l’Assistente AI. Accedere a experience.adobe.com e iniziare a interagire con l&#39;Assistente AI specificando il prompt nel linguaggio naturale utilizzando il campo `Ask AI Assistant anything`:

![Agente individuazione accesso](/help/ai-in-aem/agents/discovery/assets/access-discovery-agent.png)

## Casi d’uso comuni e prompt di esempio {#use-cases-prompts}

Utilizzare le richieste di ottimizzazione del contenuto ricercando le risorse corrette tramite [Discovery Agent](/help/ai-in-aem/agents/discovery/overview.md). Una volta visualizzate le immagini rilevanti, gli utenti possono generare varianti ottimizzate o specifiche per il canale per una o più risorse direttamente dai risultati della ricerca. Questo flusso di lavoro garantisce input di alta qualità e risultati di ottimizzazione sempre migliori. [Visualizza l&#39;elenco completo delle ottimizzazioni disponibili](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/).

* **Creazione rappresentazione ad alta risoluzione**

  L’agente può generare nuove rappresentazioni di una risorsa a una risoluzione e a un livello di qualità specifici, semplificando la preparazione di varianti pronte per il canale senza dover eseguire modifiche manuali.


  Esempio di prompt:

  Crea una rappresentazione `2000px` come `JPEG` con qualità `80%`.

  Cercare la risorsa corretta utilizzando l&#39;[agente di individuazione](/help/ai-in-aem/agents/discovery/overview.md), quindi utilizzare i seguenti prompt in caso di più risultati di ricerca:

  Per ottenere il terzo risultato di ricerca, creare una copia trasformata `2000px` come `JPEG` con qualità `80%`.

  OR

  Per `Asset ID`, genera una copia trasformata di 2.000 px come `JPEG` con qualità `80%`

* **Miglioramento immagine**

  L’agente può applicare miglioramenti visivi, come la nitidezza, per garantire che le risorse appaiano nitide e ben definite prima di essere utilizzate nelle campagne.

  Esempio di prompt:

  Contrasta l&#39;immagine.


* **Regolazioni colore di sfondo**

  L’agente può aggiornare o sostituire i colori di sfondo nelle risorse trasparenti, supportando combinazioni di colori specifiche per il brand o temi visivi basati su campagne.

  Esempio di prompt:

  Cambia il colore di sfondo di `PNG` in `#ff8932`.

* **Trasformazioni orientamento**

  L’agente può capovolgere o specchiare gli elementi visivi per allinearli alle esigenze di layout o alla direzione creativa, senza richiedere strumenti di modifica esterni.

  Esempio di prompt:

  Specchiate l&#39;immagine orizzontalmente.

* **Rappresentazioni ottimizzate per il canale**

  L’agente può produrre rappresentazioni personalizzate in base ai requisiti specifici della piattaforma, ad esempio Instagram Stories, garantendo che le risorse soddisfino automaticamente le linee guida relative a formato, rapporto e qualità.

  Richiesta di esempio:

  Creare una rappresentazione per una storia `Instagram`.

* **Sovrapposizioni con marchio e generazione composita**

  L’agente può applicare grafici promozionali, sovrapposizioni o badge alle risorse esistenti con un posizionamento preciso, per supportare la creazione rapida di composizioni pronte per la campagna.

  Richiesta di esempio:

  Sovrapponi l&#39;immagine con `30%` grafici di sconto sul banner promozionale, posizionandolo `100px` dal centro.

  >[!NOTE]
  >
  >Le posizioni di sovrapposizione potrebbero non essere precise.


## Risultati ottimizzazione {#content-optimization-agent-results}

Quando specifichi una richiesta di ottimizzazione, l’agente di ottimizzazione del contenuto restituisce la risorsa avanzata insieme a comode opzioni di accesso basate sul tipo di risorsa:

* **Immagini**: la risposta include un&#39;anteprima delle miniature e opzioni per aprire l&#39;URL di Dynamic Media o scaricare l&#39;immagine ottimizzata.

* **Documenti PDF**: la risposta include un&#39;anteprima delle miniature e opzioni per aprire l&#39;URL di Dynamic Media o scaricare il file ottimizzato.

* **Video**: la risposta fornisce le opzioni per aprire l&#39;URL di Dynamic Media o scaricare il video ottimizzato.

![Risultati ottimizzazione contenuto](/help/ai-in-aem/agents/content-optimization/assets/download-content-optimization.png)

Questi risultati semplificano la revisione dell’output ottimizzato e lo utilizzano immediatamente tra i canali o i flussi di lavoro a valle.


## Limitazioni {#limitations-content-optimization}

* L’agente di ottimizzazione del contenuto non supporta attualmente le risorse PNG.

* Impostazione del colore di sfondo non supportata.

<!--


## Prompting best Practices {#prompting-best-practices-content-optimization-agent}

The following are some of the prompting best practices:

* Be explicit about the enhancement you want the Content Optimization Agent to apply. Clearly state the transformation or adjustment you expect. Precise instructions help the agent produce accurate and predictable results. For example, Instead of `Make it good quality`, specify `Create a JPEG image with 90% quality`.

* Provide detailed parameters whenever possible. The more context you give, such as dimensions, format, quality, placement, or color values, the more tailored the output is.

-->
