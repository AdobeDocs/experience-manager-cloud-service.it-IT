---
title: Agente di individuazione contenuto
description: Scopri come utilizzare l’agente di individuazione contenuti per fornire contenuti AEM pertinenti on-demand attraverso prompt conversazionali naturali per un’esperienza di individuazione semplice e senza clic.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Developer
exl-id: 676300cd-b799-4c53-a58e-043e58a2cbc5
source-git-commit: 81f85045212ca6fd92f2b665aeceaa0d4b92318c
workflow-type: tm+mt
source-wordcount: '2073'
ht-degree: 0%

---


# Agente di individuazione contenuto {#discovery-agent}

Come parte dell&#39;[agente di Content Advisor](/help/ai-in-aem/agents/content-advisor/overview.md) di AEM, l&#39;agente di individuazione dei contenuti distribuisce i contenuti AEM su richiesta tramite messaggi di richiesta espliciti per un&#39;esperienza di individuazione semplificata e senza clic. Esegue ricerche in modo intelligente in Assets, frammenti di contenuto, pagine AEM Sites e Forms adattivo per fornire materiali rilevanti come immagini, video, documenti PDF, articoli e modelli di moduli. Con il linguaggio naturale, puoi cercare contenuti senza creare query complesse o applicare filtri nell’interfaccia di AEM Assets. In base al prompt, l’agente restituisce i risultati curati, insieme ai metadati delle risorse e agli URL di consegna, pronti per essere incorporati in altre applicazioni.

Alcuni dei vantaggi principali dell&#39;agente di individuazione dei contenuti includono:

* **Individuazione unificata dei contenuti**: consente di accedere a tutti i tipi di contenuti AEM, ad esempio immagini, video, documenti PDF, articoli, pagine e moduli, da un&#39;unica interfaccia di conversazione.

* **Pianificazione più rapida delle campagne**: raccogli rapidamente elementi visivi e moduli per le campagne di marketing su canali e-mail, web e social.

* **Produttività migliorata**: riduzione del tempo impiegato per la navigazione negli archivi o per filtrare i metadati tramite la ricerca automatizzata basata su intento.

* **Utilizzo coerente dei contenuti**: assicura il riutilizzo delle risorse e dei frammenti approvati, mantenendo la coerenza del brand tra i canali.

>[!VIDEO](https://video.tv.adobe.com/v/3479983)

>[!IMPORTANT]
>
>Le risposte generate dall’intelligenza artificiale possono essere imprecise o fuorvianti. Controlla nuovamente le correzioni e le risposte suggerite.
>
>Consulta anche [Linee guida per l&#39;utente di Adobe Experience Cloud Generative AI.](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html)

## Competenze {#skills-discovery-agent}

L’agente di individuazione contenuti fornisce le seguenti competenze:

* **Individuazione contenuti in linguaggio naturale**

  L’agente di individuazione dei contenuti consente agli utenti di trovare risorse rilevanti, frammenti di contenuto, moduli adattivi e pagine AEM Sites all’interno di Adobe Experience Manager (AEM) utilizzando semplici prompt del linguaggio naturale, senza richiedere query di ricerca complesse.

* **Individuazione risorse basata su metadati**

  L’agente di individuazione dei contenuti utilizza i prompt in linguaggio naturale per trovare le risorse in base ai metadati disponibili in AEM. Gli utenti possono individuare le risorse utilizzando metadati quali tag, ID e-mail dell’autore o dell’editore, date di pubblicazione o modifica, tipo di risorsa MIME, tipo di risorsa, stato, proprietà dei metadati personalizzate definite nei moduli di metadati nella vista Assets o Admin e così via. Per l&#39;elenco completo, vedere [Casi d&#39;uso comuni e prompt di esempio](#use-cases-prompts).

  Puoi anche combinare più filtri di metadati in un singolo prompt per perfezionare i risultati della ricerca.

* **Individuazione contenuto basato su cartelle:**\
  L’agente di individuazione contenuti può identificare le risorse interpretando i prompt del linguaggio naturale che fanno riferimento ai nomi delle cartelle in AEM. Gli utenti possono semplicemente menzionare la cartella nel prompt, senza navigare manualmente nell’archivio, riducendo in modo significativo il numero di clic necessari per individuare il contenuto corretto.

## Persone {#personas-content-discovery}

### Manager campagne {#campaign-managers}

L’agente per l’individuazione dei contenuti consente ai manager delle campagne di identificare e riutilizzare rapidamente per la creazione contenuti affidabili e dalle prestazioni elevate.

### Responsabili marketing per canale {#channel-marketers}

L’agente di rilevamento dei contenuti consente agli addetti al marketing dei canali di trovare in modo efficiente le risorse rilevanti per creare esperienze coese e multicanale.

### Librerie DAM {#dam-librarians}

I bibliotecari DAM possono segnalare le risorse a cui mancano gli standard di metadati impostati dall’organizzazione, supportando una governance coerente e garantendo che le risorse rimangano complete e pronte per l’uso su tutti i canali.

### Agenzie e partner {#agencies-partners}

Le agenzie e i partner possono trovare facilmente all&#39;interno di Content Hub le risorse approvate dal marchio e riutilizzarle per accelerare il lavoro creativo mantenendo l&#39;allineamento con gli standard del marchio.

## Come accedere {#access}

Puoi accedere all’agente di individuazione contenuti in AEM tramite l’Assistente AI. Accedere a [`experience.adobe.com`](https://experience.adobe.com) e iniziare a interagire con l&#39;Assistente AI specificando il prompt nel linguaggio naturale utilizzando la casella di ricerca:

![Accedere all&#39;agente di individuazione contenuto](/help/ai-in-aem/agents/content-advisor/assets/access-discovery-agent.png)

Per informazioni sull’endpoint MCP per accedere all’agente di individuazione contenuti, contatta il supporto Adobe.

## Casi d’uso comuni e prompt di esempio {#use-cases-prompts}

### Risorse {#discovery-agent-use-cases-assets}

**Individuazione risorse basata su metadati**

L’agente di individuazione dei contenuti utilizza i prompt in linguaggio naturale per trovare le risorse in base ai metadati disponibili in AEM. Gli utenti possono individuare le risorse utilizzando le seguenti proprietà di metadati: Tag, Created by Email ID, Modified by Email ID, Published by Email ID, Created Date, Modified Date, Published Date, MIME type, Asset Type, Status, file format, file size, image width, image height, e più filtri di metadati in un singolo prompt.

L’agente di individuazione contenuti cerca anche le proprietà personalizzate disponibili negli schemi di metadati per la visualizzazione Amministratore e nei moduli di metadati per la visualizzazione Assets. Puoi modificare le richieste di conseguenza in base ai valori di ricerca disponibili all’interno di tali proprietà personalizzate delle risorse.

>[!NOTE]
>
>Per migliorare le prestazioni dell&#39;individuazione, indicizzare le proprietà dei metadati personalizzati pertinenti. Le proprietà indicizzate consentono all&#39;agente di recuperare più rapidamente il contenuto corrispondente quando gli utenti le includono nelle richieste.


Prompt di esempio:

* **Ricerca basata sui tag**: visualizza le immagini con tag `office` nella cartella `WKND`.
* **Ricerca basata su formato file, tipo di risorsa, stato risorsa e Pubblicato da ID e-mail**: visualizza le immagini in formato `.PNG` che sono `approved` e `published by <user email ID>`.
* **Ricerca basata su formato file, tipo di risorsa, stato risorsa e Creato da ID e-mail**: mostra video in formato `.mp4` approvati e `created by <user email ID>`.
* **Ricerca in base al formato di file, al tipo di risorsa, allo stato della risorsa e alla data di creazione**: mostra le immagini in formato `.PNG` create dopo il 1° gennaio 2025 e `published by <user email ID>`
* **Ricerca basata sul tipo MIME, Data creazione e Pubblicato da ID e-mail**: mostra `image/jpeg` creato dopo `January 1, 2025` e `published by <user email ID>`.
* **Ricerca basata sul formato di file e sulle proprietà dei metadati personalizzate**: mostra le immagini in formato `.JPEG` con `Product SKU ID = <SKU value>` (deve essere nel formato proprietà metadati = valore).

* **Cerca le risorse con metadati mancanti**: il campo Mostra risorse create negli ultimi 90 giorni con `<Name of metadata property including custom properties>` è vuoto.

* **Cerca le risorse utilizzando le dimensioni del file, la larghezza dell&#39;immagine e l&#39;altezza dell&#39;immagine**: mostra immagini di dimensioni superiori a 5 MB con una larghezza superiore a 2000 pixel e un&#39;altezza superiore a 1200 pixel.


**Individuazione contenuto basato su cartelle:**\
L’agente di individuazione dei contenuti può identificare le risorse interpretando i prompt del linguaggio naturale che fanno riferimento ai nomi delle cartelle in AEM. Gli utenti possono semplicemente menzionare la cartella nel prompt, senza navigare manualmente nell’archivio, riducendo in modo significativo il numero di clic necessari per individuare il contenuto corretto.

Prompt di esempio:

* La cartella `WKND` contiene svg?
* Mostra le risorse modificate dopo `Nov 1 2025` nella cartella `WKND`.
* Elencare `lifestyle` immagini nella cartella `WKND`.

**Ulteriori domande per abilitare l&#39;individuazione del contenuto basato su cartelle**

Quando un nome di cartella viene incluso in un prompt (senza il percorso completo della risorsa), l&#39;agente di individuazione contenuto verifica innanzitutto la presenza di una cartella corrispondente nel percorso radice `/content/dam/<folder-name>`.

Se non viene trovata una cartella corrispondente a livello di radice, l&#39;agente suggerisce percorsi di cartella alternativi in cui il nome di cartella specificato esiste nell&#39;archivio. In questo modo gli utenti possono identificare rapidamente la posizione corretta senza sfogliare manualmente la struttura delle cartelle.

Ad esempio, il percorso `/content/dam/<folder-name>` non è stato trovato. Intendevi una di queste?

* Opzione 1

* Opzione 2

**Individuazione risorse basata sul formato**

L’agente di individuazione dei contenuti è in grado di identificare le risorse che soddisfano specifici requisiti di qualità, ad esempio il formato di file, consentendo agli utenti di individuare rapidamente gli elementi visivi dei prodotti pronti per la distribuzione di alta qualità e il riutilizzo tra i canali.

Esempio di prompt:

Trova il pacchetto del prodotto PNG images.

**Individuazione contenuto basata su orientamento**

L’agente di individuazione contenuto può filtrare le risorse riconoscendo l’attributo visivo, ad esempio la presenza di persone e l’orientamento di un’immagine. Questo consente agli utenti di limitare rapidamente il contenuto agli elementi visivi più rilevanti senza applicare manualmente più filtri in AEM.

Esempio di prompt:

Mostra le risorse con la persona nell’orientamento orizzontale.

**Espansione dei risultati della ricerca**

L&#39;agente di individuazione contenuto restituisce i primi 20 risultati più rilevanti per tipo di contenuto per un prompt. Se sono disponibili altri risultati corrispondenti, gli utenti possono richiedere il set successivo immettendo un prompt di completamento come `show me more`. L’agente recupera quindi il set successivo di risultati dalla ricerca originale, consentendo agli utenti di esplorare progressivamente set di risultati più grandi senza perfezionare il prompt.

**Ricerca di risorse simili**

L&#39;agente di individuazione contenuto consente agli utenti di trovare risorse simili a un risultato specifico restituito nei risultati di ricerca. Quando l’agente visualizza i primi risultati per un prompt, puoi richiedere risorse simili facendo riferimento alla posizione di un elemento nell’elenco dei risultati. Ad esempio, un prompt come `find assets similar to the 3rd result` indica all&#39;agente di identificare e restituire altre risorse rilevanti correlate a tale elemento. In questo modo gli utenti possono individuare rapidamente i contenuti correlati senza dover creare un nuovo prompt di ricerca.

**Ordinamento dei risultati della ricerca**

L’agente di individuazione contenuti consente agli utenti di ordinare i risultati della ricerca direttamente nei prompt del linguaggio naturale. Gli utenti possono specificare i criteri di ordinamento, ad esempio la data di modifica, la data di creazione o il nome della risorsa, e scegliere l’ordine crescente o decrescente.

Prompt di esempio:

* Trova le immagini di montagna in ordine decrescente in base alla data di modifica (per prima cosa, mostra le risorse modificate più di recente).

* Mostra le immagini di montagna ordinate per nome in ordine crescente (mostra i nomi delle immagini che iniziano con la lettera A seguita da B e così via).

### Pagine AEM Sites {#content-discovery-agent-aem-sites-pages}

L’agente di individuazione dei contenuti consente agli utenti di individuare rapidamente le pagine AEM Sites rilevanti interpretando i prompt in linguaggio naturale che fanno riferimento ad argomenti della pagina, campagne o altre parole chiave contestuali. L’agente esegue una ricerca full-text in base alle parole chiave nel prompt per identificare le pagine corrispondenti nell’archivio AEM, eliminando la necessità di sfogliare manualmente la struttura Sites.

Prompt di esempio:

* Trova tutte le pagine di AEM Sites per la campagna estiva.

* Trova le pagine AEM Sites con un tema Coffee.

### Frammenti di contenuto {#discovery-agent-use-cases-content-fragments}

L’agente di individuazione dei contenuti consente agli utenti di individuare rapidamente i frammenti di contenuto corretti interpretando i riferimenti in linguaggio naturale ai nomi delle campagne, ai marchi di prodotto, allo stato della pubblicazione e alle attività di creazione recenti. Consente ai team di creare frammenti pronti per la campagna e visualizzare contenuti specifici per il brand, il tutto senza sfogliare manualmente le cartelle o applicare più filtri in AEM.

Prompt di esempio:

* Mostra frammenti di contenuto per la creazione di una campagna di offerte WKND.

* Mostra il frammento di contenuto per la bevanda americana.

* Mostra tutti i frammenti di contenuto pubblicati per le bevande WKND.

* Elenca tutti i frammenti di contenuto creati nelle ultime 2 settimane.

### Forms {#discovery-agent-use-cases-forms}

L’agente di individuazione dei contenuti consente di trovare rapidamente i moduli adattivi utilizzando i prompt in linguaggio naturale. Esegue la ricerca tra il contenuto del modulo e i metadati per trovare le corrispondenze in base alle parole chiave delle richieste. Ciò significa che è possibile individuare correttamente i moduli rilevanti anche se i termini di ricerca non sono nel titolo o nella descrizione del modulo.

Prompt di esempio:

* Mostrami tutti i moduli di richiesta di prestito.
* Trova i moduli da applicare per un agente.
* Trova i moduli per i contatti.
* Sto cercando i moduli di onboarding dei dipendenti.
* Mostrami i moduli di richiesta della carta di credito.

Nota: l&#39;individuazione dei moduli supporta attualmente solo Edge Delivery Services Form e la ricerca basata su tag non è al momento disponibile per i moduli.

## Risultati di ricerca {#discovery-agent-search-results}

### Risorse {#discovery-agent-search-results-assets}

L’agente di individuazione contenuto restituisce i primi risultati per ogni query, ordinati in base alla rilevanza per garantire che vengano visualizzate per prime le corrispondenze esatte. L’agente combina query guidate da metadati con ricerca semantica per assemblare un set mirato di corrispondenze probabili, quindi utilizza un LLM per classificarle in base alle intenzioni dell’utente. Questo approccio misto offre risultati precisi e in base al contesto, senza dipendere interamente da una corrispondenza diretta delle parole chiave.

Ogni risultato include il nome della risorsa e i metadati chiave della risorsa, ad esempio il percorso della risorsa, il creatore, la data di creazione, il titolo, la descrizione, il formato, l&#39;ultimo modificatore, la data dell&#39;ultima modifica, la dimensione del file, le dimensioni, l&#39;[URL Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) e i tag associati. Se una risorsa è in stato approvato, i risultati includono anche [Dynamic Media con URL OpenAPI](/help/assets/dynamic-media-open-apis-overview.md).

Puoi fare clic sul percorso della risorsa per passare facilmente alla posizione della risorsa in AEM.

![Cerca le risorse utilizzando l&#39;agente di individuazione contenuto](/help/ai-in-aem/agents/content-advisor/assets/search-results-discovery-agent.png)

Puoi utilizzare questi dettagli per valutare rapidamente se una risorsa soddisfa i requisiti senza passare a ciascuna risorsa per visualizzarne i dettagli.

>[!NOTE]
>
>Il campo [URL elemento multimediale dinamico](/help/assets/dynamic-media/dynamic-media.md) viene visualizzato nei risultati di ricerca solo se la risorsa è pubblicata e si dispone di una licenza elemento multimediale dinamico valida. Analogamente, il campo [Dynamic Media con URL OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) viene visualizzato solo se si dispone di una licenza Dynamic Media valida e Dynamic Media con OpenAPI è abilitato per l&#39;istanza AEM as a Cloud Service.

### Frammenti di contenuto {#discovery-agent-search-results-content-fragments}

L’agente di individuazione contenuti fornisce funzionalità di ricerca full-text per Frammenti di contenuto, restituendo i primi risultati che meglio corrispondono al prompt specificato. Ogni risultato include il nome del frammento di contenuto e i campi di metadati chiave, ad esempio il percorso del frammento di contenuto, il creatore, la data di creazione, le varianti, l’ultimo modificatore e i campi data dell’ultima modifica.

![Cerca frammenti di contenuto utilizzando l&#39;agente di individuazione contenuto](/help/ai-in-aem/agents/content-advisor/assets/search-content-fragments-discovery-agent.png)

Puoi fare clic sul percorso del frammento di contenuto per passare facilmente alla posizione del frammento di contenuto all’interno di AEM.

## Best practice per la richiesta di assistenza {#prompting-best-practices-discovery-agent}

Specifica dettagli concisi nei prompt del linguaggio naturale in modo che l&#39;agente possa restituire risultati accurati e pertinenti. Più si descrive chiaramente ciò che si sta cercando, meglio l&#39;agente può perfezionare e restringere l&#39;output. Ad esempio:

* Definisci i metadati delle risorse come tag, nomi delle cartelle, date di creazione, stato di pubblicazione e nomi degli autori nelle richieste di filtraggio delle risorse.

* Utilizza i metadati specifici della tua organizzazione, come categorie (scarpe da corsa, elettronica), stagioni (autunno, primavera), eventi (Black Friday, lancio del prodotto) e canali (Web, e-mail, stampa) per filtrare ulteriormente i contenuti.

## Limitazioni {#limitations-discovery-agent}

* L&#39;agente di individuazione contenuto supporta i prompt basati sulle dimensioni solo per i tipi di formato immagine e SVG. Ad esempio, `Find images wider than 1080px`.

* Gli amministratori di Content Hub possono accedere a Content Discovery Agent utilizzando il portale Content Hub; tuttavia, i risultati vengono recuperati solo dall&#39;istanza di authoring di AEM. Al momento gli utenti di Content Hub Limited non possono usufruire dei vantaggi dell&#39;agente di individuazione contenuti (disponibile a breve).

* Trova funzionalità simile funziona solo per le immagini con [miglioramenti Tag avanzati](/help/assets/ai-generated-metadata-assets-view.md).
