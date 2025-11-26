---
title: Abilità nella creazione di moduli
description: Scopri le competenze di Experience Production Agent nella creazione di moduli e come utilizzare il linguaggio naturale per creare moduli da zero.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: aa8369979c99535f0fd77e6a51af10cc17afd971
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 0%

---


# Abilità per la creazione di moduli {#form-creation-skill}

L’abilità di creazione dei moduli è una funzionalità di Experience Production Agent progettata per sviluppare moduli utilizzando prompt del linguaggio naturale. Questa abilità genera automaticamente la struttura del modulo e i tipi di campo appropriati. L’abilità viene evidenziata tramite l’Assistente IA.

Alcuni dei vantaggi chiave dell’abilità di creazione dei moduli includono:

* **Sviluppo moduli accelerato**: creazione rapida di moduli tramite
semplici comandi per il linguaggio naturale, eliminando la necessità di imparare le interfacce di prodotto tradizionali.
* **Esperienze coerenti e nel marchio**: crea moduli che seguono il branding, i modelli e le linee guida di stile della tua organizzazione utilizzando modelli e stili approvati.
* **Abbassare la barriera tecnica**: consente agli utenti aziendali di creare moduli facilmente, senza necessità di competenze tecniche avanzate o approfondite sui prodotti.

## Funzionalità {#capabilitiess}

* **Crea un nuovo modulo con prompt di testo normale**: è possibile creare un modulo inviando i requisiti in linguaggio normale. L’agente genera automaticamente la struttura del modulo, i tipi di campo e le esperienze sul marchio appropriati in base alla descrizione del linguaggio naturale e al modello specificato. Questa funzionalità accelera la creazione dei moduli, garantendo al contempo il mantenimento degli standard di marchio e conformità.

* **Importare un documento PDF e convertirlo in un modulo**: è possibile importare e trasformare documenti PDF esistenti in moduli. L’agente analizza i contenuti caricati per rilevare i tipi di campo, mantenere i layout e migliorare i moduli con una logica di progettazione e convalida reattiva, garantendo al contempo il mantenimento degli standard di marchio e conformità.

  Quando si utilizza una delle funzionalità precedenti, viene richiesto di scegliere il tipo di modulo da creare, specificare un modello di moduli adattivi basato su Componenti core o un modello di moduli adattivi basato su Edge Delivery Services e indicare il percorso preferito per il salvataggio del modulo. Se stai creando un modulo basato su Edge Delivery Services, puoi anche specificare l’URL GitHub dell’archivio.


### Prompt di esempio {#sample-prompts}

* *Crea un modulo per la raccolta di commenti e suggerimenti con campi per nome, e-mail e messaggio*
* *Crea un modulo di feedback del cliente con valutazione del prodotto (1-5 stelle), campo commento e e-mail opzionale*
* *Crea un modulo per i contatti con i campi Nome, E-mail, Oggetto e Messaggio*
* *Crea un modulo di registrazione con informazioni personali, preferenze dell&#39;account e accettazione dei termini*
* *Crea un modulo di richiesta della carta di credito importando il file PDF disponibile all&#39;indirizzo &#39;https://[aem-author-url]/path/to/pdf/file*
* *Crea un modulo di feedback utilizzando la boilerplate in &#39;<https://github.com/wkndforms/wesecure>&#39;*

## Ridefinisci il modulo {#refine-with-forms-experience-builder}

Dopo aver creato la struttura del modulo iniziale tramite l’Assistente di intelligenza artificiale, puoi utilizzare Forms Experience Builder per:

* **Aggiorna moduli**: aggiungi o modifica campi, regola i tipi di campo e aggiorna lo stile in base alle esigenze tramite l&#39;editor visivo.

* **Aggiorna layout**: ridisponi sezioni, gruppi o campi, regola la spaziatura e modifica la gerarchia visiva per migliorare l&#39;usabilità e garantire che il modulo sia chiaro e intuitivo per il pubblico.

* **Aggiungi regola business**: crea logica condizionale, mostra/nascondi regole, dipendenze campo e definisci regole di convalida.

* **Configura invio**: configura dove vengono inviati i dati del modulo, inclusa la configurazione delle notifiche e-mail, le integrazioni con i flussi di lavoro o le connessioni a sistemi esterni.

Per ulteriori informazioni, consulta la [documentazione di Forms Experience Builder](/help/forms/experience-builder/product-overview.md).


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

<!-- 
#### Import and convert {#import-and-convert}

Transform existing documents into interactive digital forms. The agent analyzes uploaded content to detect field types, preserve layouts, and enhance forms with responsive design and validation logic. Supported formats include Acroforms, XFA PDFs, flat PDFs, images (JPG, PNG), and hand-drawn form photographs.

>[!VIDEO](https://video.tv.adobe.com/v/3474042)

**Prompt examples:**

* *Convert the attached PDF file to an adaptive form*
* *Transform this scanned form image into an interactive digital form*
* *Import the employee onboarding PDF and create an editable form*
* *Convert this paper form photograph into a digital form with validation*
-->

<!-- 
### Embed an existing form to a sites page {#embed-existing-form}

The form creation skill enables seamless integration of existing forms into any sites page through natural language commands. Rather than manually locating, copying, and embedding form components, users can simply specify which form to add and where to place it. The agent handles the technical implementation, ensuring proper rendering and functionality.

>[!VIDEO](https://video.tv.adobe.com/v/PLACEHOLDER)

**Prompt examples:**

* *Embed the contact form to the homepage*
* *Add the existing customer feedback form to the support page*
* *Insert the newsletter signup form into the footer section*
* *Place the registration form on /content/site/signup*
* *Add form "contact-us-2024" to the current page*
-->

<!-- 
### Build and add a form to an existing sites page {#build-and-add-form}

The form creation skill combines form creation and site integration in a single conversational workflow. Users can describe the form they need and specify where to add it, and the agent creates the form and embeds it into the specified page automatically. This eliminates the traditional multi-step process of creating a form separately and then manually adding it to a page.

>[!VIDEO](https://video.tv.adobe.com/v/PLACEHOLDER)

**Prompt examples:**

* *Create a newsletter signup form with email field and add it to the footer*
* *Build a quick contact form with name, email, and message, then add it to /content/about-us*
* *Add a feedback form with rating stars and comment field to this page*
* *Create a simple survey form with 5 questions and embed it on the customer portal homepage*
* *Build an event registration form with name, email, and date selection, then add it to /content/events/conference-2025*
-->
