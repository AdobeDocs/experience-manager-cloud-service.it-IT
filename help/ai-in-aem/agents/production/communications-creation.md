---
title: Abilità nella creazione di comunicazioni
description: Scopri l’abilità di creazione di comunicazioni dell’agente di produzione Experience e come utilizzare il linguaggio naturale per creare comunicazioni interattive.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: aa8369979c99535f0fd77e6a51af10cc17afd971
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---


# Abilità nella creazione di comunicazioni {#ic-creation-skill}

>[!NOTE]
>
> L&#39;abilità di creazione delle comunicazioni è attualmente in formato alfa. Se desideri partecipare, invia una richiesta dal tuo indirizzo e-mail ufficiale a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com).

Le comunicazioni interattive sono documenti personalizzati, basati su dati, progettati per la corrispondenza aziendale, ad esempio estratti conto, documenti relativi alle politiche, fatture, kit di benvenuto e avvisi sui benefit. A differenza dei moduli che raccolgono input dagli utenti, le comunicazioni interattive generano documenti di output con contenuto dinamico specifico per il destinatario.

L’abilità di creazione delle comunicazioni è una funzionalità dell’agente di produzione dell’esperienza progettata per sviluppare comunicazioni interattive utilizzando prompt del linguaggio naturale. Questa abilità genera automaticamente una corrispondenza personalizzata basata su dati per la stampa (in formato PDF). L’abilità viene evidenziata tramite l’Assistente IA.

Alcuni dei vantaggi chiave dell’abilità di creazione di comunicazioni includono:

* **Sviluppo delle comunicazioni accelerato**: creazione rapida di comunicazioni utilizzando semplici comandi del linguaggio naturale, eliminando la necessità di imparare le interfacce di prodotto tradizionali.
* **Corrispondenza coerente e nel marchio**: crea comunicazioni che seguono il branding, i modelli e le linee guida di stile della tua organizzazione utilizzando modelli e stili approvati.
* **Abbassare la barriera tecnica**: consente agli utenti aziendali di creare facilmente comunicazioni senza dover disporre di competenze tecniche avanzate o di prodotto approfondite.

## Funzionalità {#capabilities}

<!-- * **Create personalized communications with plain text prompt**: You can create communication documents for print (in PDF format) by submitting your requirements in plain language. The agent automatically generates appropriate document structures, layouts, and data bindings based on your natural language description. -->

* **Crea da modelli**: puoi utilizzare modelli organizzativi approvati per garantire la coerenza del brand e gli standard di conformità. L’agente sfrutta i modelli e le linee guida di stile esistenti per creare corrispondenza all’interno del brand che soddisfa i requisiti normativi.

* **Importa e converti immagini e documenti esistenti in comunicazioni interattive**: puoi importare e trasformare documenti esistenti in comunicazioni interattive. L’agente analizza il contenuto caricato per rilevare i campi, mantenere i layout e creare corrispondenza basata sui dati con funzionalità di contenuto dinamico. I formati supportati includono PDF, immagini (JPG, PNG) e modelli disegnati a mano.


## Prompt di esempio {#sample-prompts}

* *Crea una comunicazione per un rendiconto del prestito utilizzando il modello all&#39;indirizzo https://[aem-author-url]/path/to/pdf/file*
* *Crea una comunicazione da PDF in https://[aem-author-url]/path/to/pdf/file*
* *Crea una comunicazione dal file di immagine all&#39;indirizzo https://[aem-author-url]/path/to/image/file*
* Crea una lettera utilizzando il file PDF all&#39;indirizzo https://[aem-author-url]/path/to/pdf/file


## Ottimizzare la comunicazione {#refine-with-ic-editor}


Dopo aver creato la struttura di comunicazione iniziale mediante l&#39;Assistente AI, è possibile utilizzare l&#39;Editor di comunicazioni interattive per perfezionare e migliorare il documento. Nell&#39;editor di comunicazioni interattive è possibile fornire prompt in linguaggio naturale per:

* **Aggiungi campi e contenuto**: aggiungi nuovi campi, blocchi di testo, immagini, grafici, tabelle e altri componenti ai documenti di comunicazione utilizzando prompt in linguaggio naturale. L’agente interpreta le istruzioni e inserisce gli elementi appropriati con la struttura e la formattazione corrette.

* **Modifica campi e contenuto**: modifica i campi e il contenuto esistenti nei documenti di comunicazione tramite comandi di conversazione. Aggiorna le proprietà dei campi, modifica il contenuto del testo, regola le associazioni di dati e perfeziona le configurazioni dei componenti.

* **Rimuovi campi e contenuto**: elimina campi, componenti o sezioni indesiderati dai documenti di comunicazione utilizzando istruzioni in linguaggio naturale. L&#39;agente rimuove gli elementi specificati mantenendo la struttura del documento e l&#39;integrità del layout.

* **Campi di stile e contenuto**: applica formattazione e stile ai campi e al contenuto tramite prompt in linguaggio naturale. Regola font, colori, allineamento, spaziatura e altre proprietà visive in base alle linee guida del tuo marchio e ai requisiti di progettazione.

### Prompt di esempio per l&#39;ottimizzazione delle comunicazioni {#sample-prompts-refining}

* *Genera una lettera di liquidazione per la richiesta di risarcimento per l&#39;assicurazione del veicolo*
* *Applica il corsivo al testo della liberatoria*
* *Modifica la dimensione del carattere del testo della liberatoria in 12*
* *Aggiorna il colore del carattere del testo della liberatoria in rosso*
* *Aggiorna il colore di sfondo delle caselle di testo di intestazione e piè di pagina al grigio chiaro*
* *Aggiungi un nuovo pannello di esclusione della responsabilità con campi di firma e conferma*
* *Rimuovi il campo del testo di conferma*
* *Aggiungere una tabella dei dettagli di pagamento con tre colonne*
* *Aggiorna l&#39;allineamento del campo del numero dei criteri al centro*
* *Modifica l&#39;interlinea della sezione termini e condizioni in 1.5*

Per ulteriori informazioni sulle funzionalità dell&#39;editor di comunicazioni interattive, vedere [Documentazione di comunicazioni interattive](/help/forms/introduction-to-interactive-communication.md).

## Attivazione {#activation}

Per abilitare Experience Production Agent per la tua organizzazione, l’attivazione deve essere avviata tramite Adobe. Inizia il processo contattando tramite:

* E-mail: `experience-production-agent@adobe.com`
* Oppure, contatta il team del tuo account Adobe.

Per un’esperienza di onboarding efficiente, prepara e fornisci i seguenti dettagli:

Per **AEM as a Cloud Service**, condividi i seguenti identificatori:

* ID organizzazione
* `product_id`
* `profile_id`

Il tuo amministratore AEM può individuarli:

1. Accesso a <https://adminconsole.adobe.com/>
1. Selezione di **Adobe Experience Manager as a Cloud Service**
1. Scelta dell’istanza di AEM appropriata nel tuo ambiente
1. Selezione di un profilo con autorizzazioni di lettura/scrittura per il contenuto pertinente
1. Copia dell’URL completo del browser da questa pagina
1. Estrazione dei valori `product_id` e `profile_id` dall&#39;URL\
   Ad esempio, un URL come `https://adminconsole.adobe.com/products/profiles/users` contiene questi parametri.

Per **Edge Delivery Document Authoring**, fornisci al tuo team Adobe:

* Domini per l’ambiente Edge Delivery Services
* Dettagli GitHub corrispondenti:
   * Organizzazione (Org)
   * Archivio (archivio)
   * Ramo

La fornitura di informazioni complete e accurate accelera il processo di attivazione e garantisce il provisioning tempestivo di Experience Production Agent.

