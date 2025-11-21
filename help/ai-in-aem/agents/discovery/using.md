---
title: Panoramica di Discovery Agent
description: Scopri come utilizzare Discovery Agent per distribuire contenuti AEM rilevanti on-demand attraverso messaggi di richiesta conversazionali per un’esperienza di rilevamento semplificata e senza clic.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 25ca9a85b3d3e9917ae144cd906dae7736adb2f0
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 1%

---


# Discovery Agent {#discovery-agent}

Discovery Agent fornisce contenuti AEM on-demand attraverso semplici richieste di conversazione per un&#39;esperienza di rilevamento semplice e senza clic. Esegue una ricerca intelligente tra Assets, Frammenti di contenuto e Forms adattivo per fornire materiali rilevanti come immagini, video, documenti PDF, articoli e modelli di modulo. Con il linguaggio naturale, puoi cercare contenuti senza creare query complesse o applicare filtri nell’interfaccia di AEM Assets. In base al prompt, l’agente restituisce i risultati curati, insieme ai metadati delle risorse e agli URL di consegna, pronti per essere incorporati in altre applicazioni.

Alcuni dei vantaggi principali di Discovery Agent includono:

* **Individuazione unificata dei contenuti**: consente di accedere a tutti i tipi di contenuti AEM, ad esempio immagini, video, documenti PDF, articoli e moduli, da un&#39;unica interfaccia di conversazione.

* **Pianificazione più rapida delle campagne**: raccogli rapidamente elementi visivi e moduli per le campagne di marketing su canali e-mail, web e social.

* **Produttività migliorata**: riduzione del tempo impiegato per la navigazione negli archivi o per filtrare i metadati tramite la ricerca automatizzata basata su intento.

* **Utilizzo coerente dei contenuti**: assicura il riutilizzo delle risorse e dei frammenti approvati, mantenendo la coerenza del brand tra i canali.

>[!IMPORTANT]
>
>Le risposte generate dall’intelligenza artificiale possono essere imprecise o fuorvianti. Controlla nuovamente le correzioni e le risposte suggerite.
>
>Consulta anche [Linee guida per l&#39;utente di Adobe Experience Cloud Generative AI](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html).

## Competenze {#skills-discovery-agent}

Discovery Agent fornisce le seguenti competenze:

* **Individuazione contenuti in linguaggio naturale**\
  Discovery Agent consente agli utenti di trovare risorse rilevanti, frammenti di contenuto e moduli adattivi all’interno di Adobe Experience Manager (AEM) utilizzando semplici prompt del linguaggio naturale, senza richiedere query di ricerca complesse.

* **Individuazione risorse basata su tag**

  Discovery Agent utilizza i prompt del linguaggio naturale per trovare le risorse associate a tag specifici nell’archivio AEM, consentendo agli utenti di accedere rapidamente ai contenuti organizzati o non organizzati in base alla tassonomia dell’organizzazione.

* **Individuazione contenuto basato su cartelle:**\
  Discovery Agent può identificare le risorse interpretando i prompt del linguaggio naturale che fanno riferimento ai nomi delle cartelle in AEM. Gli utenti possono semplicemente menzionare la cartella nel prompt, senza navigare manualmente nell’archivio, riducendo in modo significativo il numero di clic necessari per individuare il contenuto corretto.

## Persone {#personas-discovery-agent}

### Manager campagne {#campaign-managers}

Discovery Agent consente ai responsabili di Campaign di identificare e riutilizzare rapidamente i contenuti affidabili e ad alte prestazioni per la creazione.

### Responsabili marketing per canale {#channel-marketers}

Discovery Agent consente agli addetti al marketing dei canali di trovare in modo efficiente le risorse rilevanti per creare esperienze coese e multicanale.

### Librerie DAM {#dam-librarians}

Le librerie DAM possono contrassegnare le risorse a cui mancano gli standard di metadati impostati dall’organizzazione, supportando una governance coerente e garantendo che le risorse rimangano complete e pronte per l’uso su tutti i canali.

### Agenzie e partner {#agencies-partners}

Agenzie e partner possono trovare facilmente all’interno di Content Hub le risorse approvate dal marchio e riutilizzarle per accelerare il lavoro creativo mantenendo l’allineamento con gli standard del marchio.

## Come accedere a Discovery Agent? {#access-discovery-agent}

Puoi accedere ad AEM Business Agent tramite l’Assistente AI. Accedi a experience.adobe.com e inizia a interagire con l’Assistente AI specificando il prompt in linguaggio naturale utilizzando la casella di ricerca:

![Agente individuazione accesso](/help/ai-in-aem/agents/discovery/assets/access-discovery-agent.png)

Per informazioni sull’endpoint MCP per accedere a Discovery Agent, contatta il supporto Adobe.

## Casi d’uso comuni e prompt di esempio {#use-cases-prompts}

### Risorse {#discovery-agent-use-cases-assets}

**Individuazione risorse basata su tag**

Discovery Agent utilizza i prompt del linguaggio naturale per trovare le risorse associate a tag specifici nell’archivio AEM, consentendo agli utenti di accedere rapidamente ai contenuti organizzati in base alla tassonomia della propria organizzazione.

Esempio di prompt:

Mostra le immagini con tag `office` nella cartella `WKND`.

**Individuazione contenuto basato su cartelle:**\
Discovery Agent può identificare le risorse interpretando i prompt del linguaggio naturale che fanno riferimento ai nomi delle cartelle in AEM. Gli utenti possono semplicemente menzionare la cartella nel prompt, senza navigare manualmente nell’archivio, riducendo in modo significativo il numero di clic necessari per individuare il contenuto corretto.

Prompt di esempio:

* La cartella `WKND` contiene svg?
* Mostra le risorse modificate dopo `Nov 1 2025` nella cartella `WKND`.
* Elencare `lifestyle` immagini nella cartella `WKND`.

**Individuazione risorse basata su risoluzione e formato**

Discovery Agent è in grado di identificare le risorse che soddisfano specifici requisiti di qualità, ad esempio il formato di file o la risoluzione minima, consentendo agli utenti di individuare rapidamente gli elementi visivi dei prodotti pronti per la distribuzione di alta qualità e il riutilizzo tra i canali.

Esempio di prompt:

Trova il pacchetto del prodotto PNG immagini di larghezza di almeno 2000 px.

**Individuazione contenuto basata su orientamento**

Discovery Agent può filtrare le risorse riconoscendo l&#39;attributo visivo, ad esempio la presenza di persone e l&#39;orientamento di un&#39;immagine. Questo consente agli utenti di limitare rapidamente il contenuto agli elementi visivi più rilevanti senza applicare manualmente più filtri in AEM.

Esempio di prompt:

Mostra le risorse con la persona nell’orientamento orizzontale.

### Frammenti di contenuto {#discovery-agent-use-cases-content-fragments}

Discovery Agent consente agli utenti di individuare rapidamente i frammenti di contenuto appropriati interpretando i riferimenti in linguaggio naturale ai nomi delle campagne, ai marchi di prodotto, allo stato della pubblicazione e alle attività di creazione recenti. Consente ai team di creare frammenti pronti per la campagna e visualizzare contenuti specifici per il brand, il tutto senza sfogliare manualmente le cartelle o applicare più filtri in AEM.

Prompt di esempio:

* Mostra frammenti di contenuto per la creazione di una campagna di offerte WKND.

* Mostra il frammento di contenuto per la bevanda americana.

* Mostra tutti i frammenti di contenuto pubblicati per le bevande WKND.

* Elenca tutti i frammenti di contenuto creati nelle ultime 2 settimane.

### Forms {#discovery-agent-use-cases-forms}

Discovery Agent consente di trovare rapidamente i moduli adattivi utilizzando i prompt del linguaggio naturale. Esegue la ricerca tra il contenuto del modulo e i metadati per trovare le corrispondenze in base alle parole chiave delle richieste. Ciò significa che è possibile individuare correttamente i moduli rilevanti anche se i termini di ricerca non sono nel titolo o nella descrizione del modulo.

Prompt di esempio:

* Mostrami tutti i moduli di richiesta di prestito.
* Trova i moduli da applicare per un processo.
* Trova i moduli per i contatti.
* Sto cercando i moduli di onboarding dei dipendenti.
* Mostrami i moduli di richiesta della carta di credito.

Nota: l&#39;individuazione dei moduli supporta attualmente solo Edge Delivery Services Form e la ricerca basata su tag non è al momento disponibile per i moduli.

## Risultati di ricerca {#discovery-agent-search-results}

### Risorse {#discovery-agent-search-results-assets}

Discovery Agent restituisce i primi risultati per ogni query, ordinati in base alla rilevanza per garantire che le corrispondenze esatte vengano visualizzate per prime. L’agente combina query basate su metadati con ricerche semantiche per assemblare un set mirato di corrispondenze probabili, quindi utilizza un LLM per classificarle in base alle intenzioni dell’utente. Questo approccio misto offre risultati precisi e in base al contesto, senza dipendere interamente da una corrispondenza diretta delle parole chiave.

Ogni risultato include il nome della risorsa e i metadati chiave della risorsa, ad esempio il percorso della risorsa, il creatore, la data di creazione, il titolo, la descrizione, il formato, l&#39;ultimo modificatore, la data dell&#39;ultima modifica, la dimensione del file, le dimensioni, l&#39;[URL Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) e i tag associati. Se una risorsa è in stato approvato, i risultati includono anche [Dynamic Media con URL OpenAPI](/help/assets/dynamic-media-open-apis-overview.md).

Puoi fare clic sul percorso della risorsa per passare facilmente alla posizione della risorsa in AEM.

![Cerca risorse tramite Discovery Agent](/help/ai-in-aem/agents/discovery/assets/search-results-discovery-agent.png)

Puoi utilizzare questi dettagli per valutare rapidamente se una risorsa soddisfa i requisiti senza passare a ciascuna risorsa per visualizzarne i dettagli.

>[!NOTE]
>
>Il campo [URL elemento multimediale dinamico](/help/assets/dynamic-media/dynamic-media.md) viene visualizzato nei risultati di ricerca solo se la risorsa è pubblicata e si dispone di una licenza elemento multimediale dinamico valida. Analogamente, il campo [Dynamic Media con URL OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) viene visualizzato solo se si dispone di una licenza Dynamic Media valida e Dynamic Media con OpenAPI è abilitato per l&#39;istanza AEM as a Cloud Service.

### Frammenti di contenuto {#discovery-agent-search-results-content-fragments}

Discovery Agent fornisce funzionalità di ricerca full-text per i frammenti di contenuto, restituendo i primi risultati che meglio corrispondono al prompt specificato. Ogni risultato include il nome del frammento di contenuto e i campi di metadati chiave, ad esempio il percorso del frammento di contenuto, il creatore, la data di creazione, le varianti, l’ultimo modificatore e i campi data dell’ultima modifica.

![Cerca frammenti di contenuto tramite Discovery Agent](/help/ai-in-aem/agents/discovery/assets/search-content-fragments-discovery-agent.png)

Puoi fare clic sul percorso del frammento di contenuto per passare facilmente alla posizione del frammento di contenuto all’interno di AEM.

## Best practice per la richiesta di informazioni {#prompting-best-practices-discovery-agent}

Specifica dettagli concisi nei prompt del linguaggio naturale in modo che l&#39;agente possa restituire risultati accurati e pertinenti. Più si descrive chiaramente ciò che si sta cercando, meglio l&#39;agente può perfezionare e restringere l&#39;output. Ad esempio:

* Definisci i metadati delle risorse come tag, nomi delle cartelle, date di creazione, stato di pubblicazione e nomi degli autori nelle richieste di filtraggio delle risorse.

* Utilizza i metadati specifici della tua organizzazione, come categorie (scarpe da corsa, elettronica), stagioni (autunno, primavera), eventi (Black Friday, lancio del prodotto) e canali (Web, e-mail, stampa) per filtrare ulteriormente i contenuti.

