---
title: Guida introduttiva di Forms Experience Builder
description: Scopri come utilizzare Forms Experience Builder per creare e gestire moduli con divulgazione progressiva per tutti i tipi di utenti
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: 9996bc602ae6169dd1aade622d5dbc5b1addeb54
workflow-type: tm+mt
source-wordcount: '1737'
ht-degree: 15%

---


# Guida introduttiva di Forms Experience Builder

>[!NOTE]
>
> La funzionalità Forms Experience Builder è disponibile nel **programma per utenti precoci**. Se sei interessato, invia una breve e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com` per richiedere l&#39;accesso alla funzionalità.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa documentazione è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. Funzionalità, comandi ed esempi potrebbero cambiare man mano che Forms Experience Builder continua ad evolversi durante il programma per i primi utenti.

Questa guida completa ti aiuta a iniziare a creare e gestire i moduli utilizzando la tecnologia di intelligenza artificiale per conversazioni. Sia che si tratti di un principiante che desidera creare il primo modulo o di un utente avanzato che desidera sfruttare funzionalità sofisticate, è possibile trovare informazioni dettagliate ed esempi pratici per guidare il percorso attraverso le funzionalità di Forms Experience Builder.

## Prerequisiti e configurazione

### &#x200B;1. Richiedi accesso

Se non hai accesso a Forms Experience Builder:

1. **Richiedi accesso**: invia un&#39;e-mail a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) dall&#39;e-mail aziendale
2. **Includi informazioni**: nome organizzazione e dettagli progetto
3. **Attendi approvazione**: Adobe rivedrà e fornirà istruzioni di onboarding

### &#x200B;2. Verificare che Forms sia abilitato

Prima di utilizzare Forms Experience Builder, assicurati che [AEM Forms sia abilitato per il tuo ambiente](/help/forms/setup-forms-cloud-service.md).


### &#x200B;3. Configurare l’ambiente


* **Per Edge Delivery Services (EDS):**

   * [Ambiente di configurazione per Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
   * [Creare un nuovo modulo utilizzando il modello Forms di Edge Delivery](/help/edge/docs/forms/universal-editor/create-forms.md)

* **Per moduli basati su Componenti core:**

   * Nell’istanza di Adobe Experience Manager, accedi a Forms > Forms e documenti
   * [Creare una nuova pagina utilizzando il modello Componenti core](/help/forms/creating-adaptive-form-core-components.md)

## Inizio rapido

### Accedere a Forms Experience Builder

**Editor universale**

* Aprire la pagina EDS in Universal Editor
* Cerca l’icona Forms Experience Builder nel pannello a sinistra
* Fare clic per aprire l&#39;interfaccia di conversazione

**Editor dei moduli adattivi**

* Passa a: AEM > Forms > Forms e documenti
* Creare o aprire un modulo basato su Componenti core per la modifica
* Fai clic sull’icona di Forms Experience Builder nella barra degli strumenti dell’editor

### Il primo modulo

Prova questa semplice conversazione per iniziare:

```
👤 You: "Create a simple contact form"
🤖 AI: "I'll create a contact form with name, email, and message fields for you."

👤 You: "Make the email field required"
🤖 AI: "Updated the email field to be required with validation."
```

### Comandi essenziali

| Simbolo | Scopo | Guida all’uso |
|--------|---------|------------|
| `/` | Azioni rapide e collegamenti | Digitare `/create` per la creazione del modulo, `/help` per assistenza |
| `@` | Fai riferimento a campi modulo esistenti | Digitare `@fieldName` per modificare campi specifici (ad esempio, `@email`) |
| Testo normale | Conversazione naturale | Descrivi cosa desideri: &quot;Aggiungi un campo numero di telefono obbligatorio&quot; |

### Suggerimenti per il successo

* **Specificare**: &quot;Aggiungere un campo e-mail obbligatorio con convalida&quot; funziona meglio di &quot;aggiungere e-mail&quot;
* **Riferimento a campi esistenti**: utilizzare `@fieldName` per modificare i moduli
* **Chiedi aiuto**: digita `/help` seguito dalla domanda
* **Iterazione**: apporta una modifica alla volta per ottenere risultati ottimali


## Metodi per iniziare a creare un modulo

### &#x200B;1. Inizia con i prompt del linguaggio naturale

Descrivi i requisiti del modulo nel linguaggio naturale e Forms Experience Builder genera la struttura completa del modulo:

**Esempi:**

* &quot;Crea un modulo di richiesta di prestito con informazioni personali, dettagli finanziari e caricamenti di documenti&quot;
* &quot;Creare un modulo di feedback dei clienti con valutazioni, commenti e categorie di prodotti&quot;
* &quot;Ho bisogno di un modulo di registrazione in più passaggi per una conferenza con elaborazione dei pagamenti&quot;

### &#x200B;2. Importare e convertire

Trasforma i moduli e i documenti esistenti in esperienze moderne e interattive:

**Origini supportate:**

* **PDF forms**: carica PDF statici per convertirli in moduli digitali interattivi con convalide.
* **Schermate o immagini**: carica foto dei moduli cartacei per generare versioni digitali funzionali
* **HTML Forms**: importa e converti i moduli Web di base in AEM Forms avanzato con funzionalità avanzate
* **XFA Forms**: convertire i moduli basati su XFA legacy in moduli reattivi moderni
* **URL**: converti i moduli web esistenti in AEM Forms nativi con interfaccia utente migliorata

**Come importare:**

1. Fai clic sull’icona dell’allegato nell’interfaccia di Forms Experience Builder
2. Carica il file (PDF, immagine, progettazione Figma, ecc.)
3. Descrivi le tue esigenze:
   * &quot;Converti questo modulo PDF in una versione digitale&quot;
   * &quot;Crea un modulo che corrisponda a questo layout di schermata&quot;
   * “Crea questo modulo dalla mia progettazione Figma”

**Tipi di file supportati:**

* **Immagini** (PNG, JPG, GIF): layout di moduli, modelli di interfaccia utente, moduli digitalizzati
* **File PDF**: moduli, specifiche e documenti esistenti
* **File Figma**: prototipi di progettazione, linee guida del brand
* **File di progettazione**: riferimenti visivi, guide di stile

### Interazioni chiave

#### Aggiunta di elementi modulo

**Aggiunte di base:**

```
👤 You: "Add a section for personal information"
🤖 AI: "Added a personal information panel with standard fields"

👤 You: "Include a file upload for resume"
🤖 AI: "Added a secure file upload component for documents"

👤 You: "Add a dropdown for country selection"
🤖 AI: "Added a country dropdown with common options"
```

**Specifiche dettagliate:**

```
👤 You: "Add a personal information panel with fields for full name, date of birth, phone number, and email address"
🤖 AI: "Created a personal information panel with all requested fields and appropriate validation"

👤 You: "Include a secure file upload component for documents, limited to PDF files under 5MB"
🤖 AI: "Added a file upload field with PDF restriction and 5MB size limit"

👤 You: "Add a country dropdown with options for USA, Canada, UK, and Germany"
🤖 AI: "Added a country dropdown with the specified options"
```

#### Creazione di un comportamento dinamico

**Logica semplice:**

```
👤 You: "Show additional fields when 'Other' is selected"
🤖 AI: "Created a conditional rule that shows additional fields when 'Other' is chosen"

👤 You: "Make the email field required"
🤖 AI: "Updated the email field to be required with validation"

👤 You: "Calculate the total automatically"
🤖 AI: "Added calculation logic to automatically compute totals"
```

**Regole di business complesse:**

```
👤 You: "Show the spouse information fields only when marital status is set to 'Married'"
🤖 AI: "Created a conditional rule that displays spouse fields based on marital status"

👤 You: "Calculate the total cost by multiplying quantity and price, then add 10% tax"
🤖 AI: "Added calculation logic with quantity, price, and tax computation"

👤 You: "Enable the submit button only when all required fields are completed and terms are accepted"
🤖 AI: "Created validation logic that enables submission only when all conditions are met"
```

#### Layout e progettazione dei moduli

**Modifiche del layout:**

```
👤 You: "Make this a multi-step form"
🤖 AI: "Converted the form to a progressive layout with navigation"

👤 You: "Organize fields in two columns"
🤖 AI: "Updated the layout to display fields in a two-column arrangement"

👤 You: "Convert to an accordion layout"
🤖 AI: "Transformed the form to use accordion-style sections"
```

**Miglioramenti alla progettazione:**

```
👤 You: "Create a wizard-style form with 3 steps: personal info, preferences, and review"
🤖 AI: "Created a wizard form with three distinct steps and navigation"

👤 You: "Arrange the address fields in a compact two-column layout"
🤖 AI: "Organized address fields in a compact two-column format"

👤 You: "Update the layout to match the attached wireframe"
🤖 AI: "Modified the layout to match the provided design reference"
```

### Configurazione dell’integrazione

Forms Experience Builder può configurare vari endpoint di invio per collegare i moduli a sistemi e servizi esterni:

| Tipo di integrazione | Comando di installazione | Caso d’uso |
|------------------|---------------|----------|
| **E-mail** | &quot;Invia modulo a e-mail&quot; | Notifiche e conferme per l’invio di moduli |
| **API REST** | &quot;Invia all’endpoint REST&quot; | Applicazioni personalizzate e sistemi di terze parti |
| **Archiviazione cloud** | &quot;Salva in Azure/SharePoint&quot; | Archiviazione dei documenti e gestione dei file |
| **Flusso di lavoro** | &quot;Connetti a Power Automate&quot; | Automazione e approvazione dei processi aziendali |
| **Marketing** | &quot;Integrare con Marketo&quot; | Gestione dei lead e automazione del marketing |

**Esempi di integrazione avanzata:**

```
👤 You: "Send form submissions to hr@company.com and create a case in our CRM system"
🤖 AI: "Configured email submission and CRM integration"

👤 You: "Submit data to our REST API endpoint and trigger the new customer workflow"
🤖 AI: "Set up REST API submission with workflow triggers"

👤 You: "Email responses to the sales team and add the lead to our marketing automation platform"
🤖 AI: "Configured multi-channel submission with email and marketing automation"
```





## Operazioni avanzate per moduli


### Creazione di regole complesse

Creare regole di convalida e business sofisticate che rispondano alle interazioni degli utenti e garantiscano l&#39;integrità dei dati:

```
👤 You: "Show the address section only if the user selects 'Ship to different address'"
🤖 AI: "Created a conditional rule that shows/hides the address panel based on checkbox selection"
```

### Creazione di moduli in più passaggi

```
👤 You: "Create a progressive form with 3 steps: personal info, preferences, confirmation"
🤖 AI: "Created a progressive form with navigation between steps and validation at each stage"
```

### Tipi di campo avanzati

* Caricamento di file con restrizioni di convalida e dimensione per la gestione dei documenti
* Selettori di date con vincoli e regole aziendali per la programmazione
* Elenchi a discesa con opzioni dinamiche che cambiano in base alle selezioni effettuate dagli utenti
* Pulsanti di scelta con logica condizionale per strutture decisionali complesse


### Conversione da PDF a modulo

```
👤 You: "Convert this PDF into an interactive form"
🤖 AI: "Analyzed the PDF and created a form with appropriate field types and validation"
```

### Conversione da URL a modulo

```
👤 You: "Create a form from this website"
🤖 AI: "Extracted form elements and created a native AEM Form with enhanced functionality"
```

### Analisi delle prestazioni

```
👤 You: "Analyze this form's conversion performance"
🤖 AI: "Provided insights on form effectiveness and suggested optimizations"
```

### Personalizzazione avanzata

#### Regole di convalida personalizzate

* Dipendenze dei campi che creano un comportamento dinamico del modulo basato sugli input dell’utente
* Logica condizionale complessa che adatta l’esperienza del modulo alle esigenze dell’utente
* Messaggi di errore personalizzati che forniscono indicazioni chiare agli utenti
* Convalida tra campi che garantisce la coerenza dei dati tra più input

#### Ottimizzazione del layout

* Tempi di risposta mobili che garantiscono il funzionamento ottimale dei moduli su tutti i dispositivi
* Conformità in materia di accessibilità che rende i moduli utilizzabili da persone con disabilità
* Miglioramenti nella progettazione visiva che migliorano il coinvolgimento degli utenti e i tassi di completamento
* Miglioramenti dell’esperienza utente che riducono l’attrito e migliorano la soddisfazione

#### Flussi di lavoro di integrazione

* Processi di approvazione in più fasi che indirizzano l’invio dei moduli tramite i flussi di lavoro aziendali
* Trasformazione dei dati che converte i dati del modulo in formati richiesti da sistemi esterni
* Logica di business personalizzata che applica regole e calcoli specifici all&#39;invio di moduli
* Gestione avanzata degli errori che fornisce un ripristino agevole dai problemi di sistema

## Riferimento comando

### Comandi essenziali

| Simbolo | Scopo | Guida all’uso |
|--------|---------|------------|
| `/` | Azioni rapide e collegamenti | Digitare `/create` per la creazione del modulo, `/help` per assistenza |
| `@` | Fai riferimento a campi modulo esistenti | Digitare `@fieldName` per modificare campi specifici (ad esempio, `@email`) |
| Testo normale | Conversazione naturale | Descrivi cosa desideri: &quot;Aggiungi un campo numero di telefono obbligatorio&quot; |

### Comandi barra

| Comando | Contesto | Esempio di utilizzo |
|---------|---------|---------------|
| `/create-form` | Tutti gli ambienti | `/create-form customer survey` |
| `/add-form` | Editor universale | `/add-form contact form` |
| `/update-layout` | Editor modulo | `/update-layout wizard with 3 steps` |
| `/update-field` | Editor modulo | `/update-field @email to be required` |
| `/create-rule` | Editor modulo | `/create-rule show @spouse if married` |
| `/create-panel` | Editor modulo | `/create-panel Personal Information` |
| `/configure-submit` | Editor modulo | `/configure-submit to email support` |
| `/help` | Tutti gli ambienti | `/help multi-step forms` |

### Riferimenti campo

Utilizza `@fieldName` per fare riferimento ai campi esistenti:

* `@firstName`, `@lastName` * Campi nome
* `@email`, `@phoneNumber` * Campi di contatto
* `@address`, `@city`, `@zipCode` * Campi indirizzo
* `@dateOfBirth`, `@startDate` * Campi data

### Tipi componente

Utilizza questi termini per descrivere gli elementi del modulo:

* `text input` * Campo di testo a riga singola
* `text area` * Campo di testo su più righe
* `dropdown` * Seleziona elenco con opzioni
* `checkbox` * Casella di controllo singola
* `checkbox group` * Più caselle di controllo
* `radio group` * Gruppo di pulsanti di scelta
* `date picker` * Campo selezione data
* `file upload` * Campo allegato
* `panel` * Contenitore per il raggruppamento dei campi

### Comandi di integrazione

| Servizio | Comando linguaggio naturale | Requisiti |
|---------|--------------------------|--------------|
| E-mail | &quot;Invia invii a [e-mail]&quot; | Indirizzo e-mail valido |
| API REST | &quot;Invia all&#39;endpoint REST [URL]&quot; | Endpoint API e credenziali |
| Archiviazione Azure | &quot;Salva i file nell’archiviazione di Azure&quot; | Configurazione dell&#39;account di archiviazione |
| SharePoint | &quot;Archivia in SharePoint [sito]&quot; | Accesso al sito SharePoint |
| Power Automate | Flusso di &quot;Trigger Power Automate&quot; | Configurazione del flusso |
| Marketo | &quot;Aggiungere lead a Marketo&quot; | Credenziali API di Marketo |

### Suggerimenti

1. **Usa linguaggio naturale**: l&#39;intelligenza artificiale comprende le richieste complesse e può interpretare i requisiti dettagliati
2. **Essere specifici**: le descrizioni dettagliate producono risultati migliori e una generazione più accurata dei moduli
3. **Iterazione**: perfeziona i moduli tramite conversazione per ottenere un&#39;esperienza utente perfetta
4. **Sfrutta il contesto**: fai riferimento agli elementi del modulo esistenti per creare nuove versioni in base a quelli già disponibili
5. **Verifica approfondita**: convalida tutti gli scenari utente per garantire che i moduli funzionino come previsto

## Assistenza e formazione sul prodotto

Forms Experience Builder può anche insegnarti le funzioni di AEM Forms:

### Fai domande come:

* “Come si crea un modulo con più passaggi?”
* “Qual è la differenza tra pannelli e sezioni?”
* “Come si configurano le notifiche e-mail?”
* “Quali sono le best practice per i moduli compatibili con i dispositivi mobili?”
* “Come si applicano i temi ai moduli?”

### Ottieni assistenza per:

* Concetti e terminologia di AEM Forms
* Istruzioni passo dopo passo per le funzioni complesse
* Best practice e consigli
* Risoluzione dei problemi comuni

## Best practice

### Progettazione modulo

* **Semplifica**: inizia con campi essenziali e aggiungi complessità solo quando necessario per evitare di sovraffollare gli utenti
* **Usa etichette chiare**: le finalità dei campi sono evidenti con etichette descrittive che guidano gli utenti attraverso il modulo
* **Fornisci testo di aiuto**: guida gli utenti attraverso campi complessi con esempi e guida contestuale
* **Verifica approfondita**: convalida tutti i percorsi utente per garantire il corretto funzionamento dei moduli in tutti gli scenari

### Esperienza utente

* **Divulgazione progressiva**: mostra i campi rilevanti in base al contesto per ridurre il carico cognitivo e migliorare i tassi di completamento
* **Cancella navigazione**: aiuta gli utenti a capire dove si trovano nel modulo e quali passaggi rimangono
* **Progettazione reattiva**: assicurarsi che i moduli funzionino su tutti i dispositivi e su tutte le dimensioni dello schermo per la massima accessibilità
* **Accessibilità**: attieniti alle linee guida WCAG per rendere i moduli utilizzabili da persone con disabilità

### Prestazioni

* **Ottimizza conteggio campi**: richiedi solo le informazioni necessarie per ridurre l&#39;abbandono dei moduli e migliorare i tassi di completamento
* **Utilizza la convalida appropriata**: evita errori prima dell&#39;invio per fornire feedback e indicazioni immediati
* **Tassi di completamento dei test**: monitora e migliora l&#39;efficacia dei moduli tramite analisi e feedback degli utenti
* **Aggiornamenti regolari**: i moduli sono aggiornati in base alle esigenze aziendali e alle aspettative degli utenti per prestazioni ottimali

### Coerenza del brand

* **Crea modelli marchio**: prepara modelli di modulo con marchio con i colori, i font e lo stile della tua organizzazione prima di iniziare la creazione del modulo
* **Definisci standard di stile**: stabilisce stili di pulsante, layout di campo e linee guida di spaziatura coerenti a cui è possibile fare riferimento nei prompt
* **Utilizzare le risorse per i marchi**: prepara logo, codici colore e linee guida per i marchi per un riferimento semplice durante la creazione dei moduli
* **Libreria modelli**: crea una raccolta di modelli di modulo con marchio per i casi d&#39;uso comuni (contatto, registrazione, feedback)
* **Richieste di stile**: includere istruzioni specifiche per il marchio: &quot;Utilizza il blu società (#1234AB) per i pulsanti e il font aziendale Helvetica&quot;

### Suggerimenti per ottenere risultati ottimali

**Avvio semplice, compilazione**

* Inizia con le richieste di base: “Crea un modulo di contatto”
* Aggiungi gradualmente i dettagli: “Aggiungi convalida al campo dell’e-mail”
* Testa e perfeziona: “Rendi opzionale il campo del telefono”

**Specifica Quando Necessario**

* Invece di: “Rendilo bello”
* Prova: “Usa colori professionali e una tipografia pulita”

**Usa linguaggio naturale**

* Invece di: “Aggiungi un componente di input di testo”
* Prova: “Aggiungi un campo per il nome”

**Riferimento a elementi esistenti**

* Usa `@fieldName` per i campi esistenti: “Rendi @email obbligatorio”
* Fornisci dettagli per i nomi dei campi: “Aggiorna il campo @phoneNumber”

**Suddividere Richieste Complesse**

* Invece di una grande richiesta, prova con più richieste più piccole
* Creare il modulo passo dopo passo
* Verificare ogni modifica prima di passare a quella successiva

## Risoluzione di problemi

| Problema   | Correzione rapida |
|-------|-----------|
| **Impossibile caricare l&#39;interfaccia** | Aggiorna browser, controlla la connessione Internet |
| **Comandi non funzionanti** | Prova `/help` o usa il linguaggio naturale |
| **@fieldName non riconosciuto** | Controlla ortografia, assicurati che il campo esista |
| **Impossibile caricare il file** | Usa PDF/JPG/PNG inferiore a 10 MB |
| **Il modulo ha un aspetto errato** | Essere più specifici: &quot;Rendi mobile-friendly&quot; |
| **Integrazione non riuscita** | Verifica credenziali e autorizzazioni API |

**Hai ancora bisogno di aiuto?** Digitare `/help` seguito da una domanda specifica o contattare l&#39;amministratore di sistema.

Per ulteriore supporto, fare riferimento alla [Libreria prompt di Forms Experience Builder](ai-assistant-prompt-library.md) principale o contattare l&#39;amministratore di sistema per assistenza tecnica.
