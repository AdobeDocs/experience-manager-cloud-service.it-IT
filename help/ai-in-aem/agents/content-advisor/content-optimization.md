---
title: Processo di ottimizzazione dei contenuti
description: Scopri come utilizzare il processo di ottimizzazione dei contenuti per trasformare il modo in cui gli utenti perfezionano e adattano le risorse applicando istruzioni in linguaggio naturale per creare varianti pronte per il canale.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: 896fc25b-7f60-47b8-9264-2ef6b85d954c
source-git-commit: a31cd8ea0ae02a51efb748097c195d68dc8b554d
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---


# Processo di ottimizzazione dei contenuti {#content-optimization-job}

Come parte dell&#39;[agente Content Advisor di AEM](/help/ai-in-aem/agents/content-advisor/overview.md), il processo di ottimizzazione dei contenuti trasforma il modo in cui gli utenti perfezionano e adattano le risorse applicando le istruzioni in linguaggio naturale per creare varianti compatibili con i canali. Sia che si tratti della generazione di nuove copie trasformate, della regolazione delle proprietà visive, della modifica degli sfondi o della preparazione delle risorse per canali digitali specifici, il processo interpreta le intenzioni degli utenti ed esegue automaticamente attività di modifica complesse. Funziona perfettamente con [il processo di individuazione dei contenuti](/help/ai-in-aem/agents/content-advisor/discovery.md), recuperando le risorse trovate e producendo varianti ottimizzate utilizzando [Dynamic Media di base con funzionalità OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) che soddisfano i requisiti di brand, canale e campagna senza dover eseguire manualmente le attività di progettazione.

Alcuni dei vantaggi principali del processo di ottimizzazione dei contenuti includono:

* **Trasformazione delle risorse senza problemi**: converte semplici prompt conversazionali in operazioni di immagine precise, quali ridimensionamento, nitidezza, mirroring o ricolorazione, eliminando la necessità di strumenti di modifica specializzati.

* **Output ottimizzati per il canale**: produce rapidamente rendering personalizzati per piattaforme specifiche come Instagram Stories, banner Web o altri punti di contatto di marketing, garantendo risorse pronte per l&#39;uso immediato.

* **Miglioramento di Creative su scala**: applica regolazioni visive e miglioramenti, ad esempio modifiche di sfondo o sovrapposizioni grafiche, per supportare flussi di lavoro creativi di grandi volumi senza rallentare il lavoro dei team.

* **[Collaborazione perfetta con il processo di individuazione dei contenuti](/help/ai-in-aem/agents/content-advisor/discovery.md)**: si basa sulle risorse identificate dal processo di individuazione dei contenuti, consentendo il recupero e l&#39;ottimizzazione end-to-end delle risorse tramite conversazione naturale.

>[!IMPORTANT]
>
>Le risposte generate dall’intelligenza artificiale possono essere imprecise o fuorvianti. Controlla nuovamente le correzioni e le risposte suggerite.
>
>Consulta anche [Linee guida per l&#39;utente di Adobe Experience Cloud Generative AI.](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)

>[!VIDEO](https://video.tv.adobe.com/v/3480078)

## Prerequisiti {#prerequisites-content-optimization-job}

Per generare varianti o ottimizzazioni per le risorse immagine. Devi avere:

* Una licenza Dynamic Media valida

* Dynamic Media con OpenAPI abilitato nell’ambiente AEM as a Cloud Service.

* Le risorse in [stato approvato](/help/assets/manage-organize-assets-view.md#manage-asset-status) nell&#39;ambiente AEM as a Cloud Service.

## Competenze {#skills-content-optimization-job}

Il processo di ottimizzazione dei contenuti fornisce le seguenti competenze:

* **Comprendere le intenzioni attraverso il linguaggio naturale**

  Il processo di ottimizzazione dei contenuti interpreta le intenzioni degli utenti dai prompt del linguaggio naturale, tenendo conto del contesto di canale, campagna e pubblico per determinare le azioni di ottimizzazione più rilevanti.

* **Genera varianti di contenuto dinamico**

  Il processo di ottimizzazione dei contenuti crea varianti ottimizzate come URL dinamici adatti a canali e tipi di formato diversi.

* **Ottimizza il contenuto dell&#39;immagine**

  Il processo di ottimizzazione dei contenuti applica miglioramenti come la conversione del formato, le regolazioni della risoluzione, il ritaglio e la nitidezza per migliorare la qualità delle immagini.

* **Ottimizzazione risorse con più varianti**

  Il processo di ottimizzazione dei contenuti può generare più varianti di immagini ottimizzate dalle risorse restituite dal processo di individuazione dei contenuti utilizzando un unico prompt in linguaggio naturale, consentendo agli utenti di produrre rappresentazioni pronte per il canale in modo rapido ed efficiente.

## Persone {#personas-content-optimization-job}

Gli esperti di marketing dei canali, persona chiave per il processo di ottimizzazione dei contenuti, possono selezionare il contenuto sorgente ad alta risoluzione adatto e richiedere formati ottimizzati personalizzati per i loro canali e segmenti di pubblico.

Gli addetti al marketing e gli impiegati delle agenzie locali possono inoltre utilizzare il processo di ottimizzazione dei contenuti per generare rapidamente varianti di immagini adatte al canale per supportare una produzione dei contenuti più rapida e coerente.

## Come accedere {#access-content-optimization-job}

Puoi accedere al processo di ottimizzazione dei contenuti in AEM tramite l’Assistente AI. Accedere a [`experience.adobe.com`](https://experience.adobe.com) e iniziare a interagire con l&#39;Assistente IA specificando il prompt nel linguaggio naturale utilizzando il campo `Ask AI Assistant anything`:

![Processo di ottimizzazione del contenuto di Access](/help/ai-in-aem/agents/content-advisor/assets/access-discovery-agent.png)

## Casi d’uso comuni e prompt di esempio {#use-cases-prompts}

Utilizza il processo di ottimizzazione del contenuto cercando le risorse corrette tramite il processo di individuazione del contenuto [.](/help/ai-in-aem/agents/content-advisor/discovery.md) Una volta visualizzate le immagini rilevanti, gli utenti possono generare varianti ottimizzate o specifiche per il canale per una o più risorse direttamente dai risultati della ricerca. Questo flusso di lavoro garantisce input di alta qualità e risultati di ottimizzazione sempre migliori. [Per ulteriori informazioni, vedere l&#39;elenco completo delle ottimizzazioni disponibili](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/assets/delivery/).

* **Creazione rappresentazione ad alta risoluzione**

  Il processo può generare nuove rappresentazioni di una risorsa a una risoluzione e a un livello di qualità specifici, semplificando la preparazione di varianti pronte per il canale senza modifiche manuali.


  Esempio di prompt:

  Crea una rappresentazione `2000px` come `JPEG` con qualità `80%`.

  Cerca la risorsa corretta utilizzando il [processo di individuazione contenuto](/help/ai-in-aem/agents/content-advisor/discovery.md), quindi utilizza i seguenti prompt in caso di più risultati di ricerca:

  Per ottenere il terzo risultato di ricerca, creare una copia trasformata `2000px` come `JPEG` con qualità `80%`.

  OR

  Per `Asset ID`, genera una copia trasformata di 2.000 px come `JPEG` con qualità `80%`

* **Miglioramento immagine**

  Il lavoro può applicare miglioramenti visivi, come la nitidezza, per garantire che le risorse appaiano nitide e ben definite prima di essere utilizzate nelle campagne.

  Esempio di prompt:

  Contrasta l&#39;immagine.


* **Regolazioni colore di sfondo**

  Il processo può aggiornare o sostituire i colori di sfondo nelle risorse trasparenti, supportando combinazioni di colori specifiche per il brand o temi visivi basati su campagne.

  Esempio di prompt:

  Cambia il colore di sfondo di `PNG` in `#ff8932`.

* **Trasformazioni orientamento**

  Il processo può riflettere o capovolgere gli elementi visivi per allinearli alle esigenze di layout o alla direzione creativa, senza richiedere strumenti di modifica esterni.

  Esempio di prompt:

  Specchiate l&#39;immagine orizzontalmente.

* **Rappresentazioni ottimizzate per il canale**

  Il processo può produrre rappresentazioni personalizzate in base ai requisiti specifici della piattaforma, come ad esempio Instagram Stories, garantendo che le risorse soddisfino automaticamente le linee guida relative a formato, rapporto e qualità.

  Richiesta di esempio:

  Creare una rappresentazione per una storia `Instagram`.

* **Sovrapposizioni con marchio e generazione composita**

  Il lavoro può applicare grafici promozionali, sovrapposizioni o badge alle risorse esistenti con un posizionamento preciso, supportando la creazione rapida di composizioni pronte per la campagna.

  Richiesta di esempio:

  Sovrapponi l&#39;immagine con `30%` grafici di sconto sul banner promozionale, posizionandolo `100px` dal centro.

  >[!NOTE]
  >
  >Le posizioni di sovrapposizione potrebbero non essere precise.


## Risultati ottimizzazione {#content-optimization-job-results}

Quando specifichi una richiesta di ottimizzazione, il processo di ottimizzazione del contenuto restituisce la risorsa avanzata insieme a comode opzioni di accesso basate sul tipo di risorsa:

* **Immagini**: la risposta include un&#39;anteprima delle miniature e opzioni per aprire l&#39;URL di Dynamic Media o scaricare l&#39;immagine ottimizzata.

* **Documenti PDF**: la risposta include un&#39;anteprima delle miniature e opzioni per aprire l&#39;URL di Dynamic Media o scaricare il file ottimizzato.

* **Video**: la risposta fornisce le opzioni per aprire l&#39;URL di Dynamic Media o scaricare il video ottimizzato.

![Risultati ottimizzazione contenuto](/help/ai-in-aem/agents/content-advisor/assets/download-content-optimization.png)

Questi risultati semplificano la revisione dell’output ottimizzato e lo utilizzano immediatamente tra i canali o i flussi di lavoro a valle.


## Limitazioni {#limitations-content-optimization}

* Impostazione del colore di sfondo non supportata.

<!--


## Prompting best Practices {#prompting-best-practices-content-optimization-job}

The following are some prompting best practices:

* Be explicit about the enhancement you want the content optimization job to apply. Clearly state the transformation or adjustment you expect. Precise instructions help the agent produce accurate and predictable results. For example, Instead of `Make it good quality`, specify `Create a JPEG image with 90% quality`.

* Provide detailed parameters whenever possible. The more context you give, such as dimensions, format, quality, placement, or color values, the more tailored the output is.

-->
