---
title: Abilità nella creazione di moduli
description: Scopri le competenze di Experience Production Agent nella creazione di moduli e come utilizzare il linguaggio naturale per creare moduli da zero.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: d5b7a8343551c5880b40c692266f33a1864f9d2b
workflow-type: tm+mt
source-wordcount: '469'
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

* **Crea un nuovo modulo con prompt di testo normale**: puoi creare esperienze di modulo sul marchio inviando i requisiti in un linguaggio semplice.

* **Importare un&#39;immagine PDF o un&#39;immagine e convertirla in un modulo**: è possibile importare e trasformare in moduli documenti PDF o immagini esistenti. L’agente analizza il contenuto caricato per rilevare i tipi di campo, mantenere i layout e migliorare i moduli con una progettazione reattiva e una logica di convalida. I formati supportati includono Acroforms, PDF XFA, flat PDF, immagini (JPG, PNG) e fotografie di moduli disegnati a mano.

  Quando si utilizza una delle funzionalità precedenti, viene richiesto di scegliere il tipo di modulo da creare, specificare un modello di moduli adattivi basato su Componenti core o un modello di moduli adattivi basato su Edge Delivery Services e indicare il percorso preferito per il salvataggio del modulo. Se stai creando un modulo basato su Edge Delivery Services, puoi anche specificare l’URL GitHub dell’archivio.


### Prompt di esempio {#sample-prompts}

* *Crea un modulo per la raccolta di commenti e suggerimenti con campi per nome, e-mail e messaggio*
* *Crea un modulo di feedback del cliente con valutazione del prodotto (1-5 stelle), campo commento e e-mail opzionale*
* *Crea un modulo per i contatti con i campi Nome, E-mail, Oggetto e Messaggio*
* *Crea un modulo di registrazione con informazioni personali, preferenze dell&#39;account e accettazione dei termini*
* *Crea un modulo di richiesta della carta di credito importando il file PDF disponibile all&#39;indirizzo &#39;https://[aem-author-url]/path/to/pdf/file*
* *Crea un modulo di feedback utilizzando la boilerplate in &#39;<https://github.com/wkndforms/wesecure>&#39;*

## Passaggi successivi {#refine-with-forms-experience-builder}

Dopo aver creato la struttura del modulo iniziale tramite l’Assistente per l’intelligenza artificiale, puoi utilizzare l’estensione per la creazione di Forms per:

* **Aggiorna moduli**: aggiungi o modifica campi, regola i tipi di campo e aggiorna lo stile in base alle esigenze tramite l&#39;editor visivo.

* **Aggiorna layout**: ridisponi sezioni, gruppi o campi, regola la spaziatura e modifica la gerarchia visiva per migliorare l&#39;usabilità e garantire che il modulo sia chiaro e intuitivo per il pubblico.

* **Aggiungi regola business**: crea logica condizionale, mostra/nascondi regole, dipendenze campo e definisci regole di convalida.

* **Configura invio**: configura dove vengono inviati i dati del modulo, inclusa la configurazione delle notifiche e-mail, le integrazioni con i flussi di lavoro o le connessioni a sistemi esterni.

Per ulteriori informazioni, consulta la [documentazione di Forms Experience Builder](/help/forms/experience-builder/product-overview.md).

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
