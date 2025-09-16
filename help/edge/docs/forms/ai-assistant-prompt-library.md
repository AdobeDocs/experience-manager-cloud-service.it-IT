---
title: 'Forms Experience Builder: libreria di prompt'
description: Raccolta di pattern di prompt ed esempi dimostrati per la creazione di moduli con assistenza IA nell’interfaccia utente per la gestione dei moduli, nell’editor dei moduli adattivi e nell’editor universale.
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: c8f64082-a23f-4919-ad66-042faad77d31
source-git-commit: fe34b44d02c308e7d18a08dd05f21abc67bd0cb2
workflow-type: tm+mt
source-wordcount: '2193'
ht-degree: 39%

---


# Forms Experience Builder: libreria di prompt

Raccolta di esempi e pattern di prompt riutilizzabili ottimizzati per Forms Experience Builder. Questa libreria semplificata si concentra sui due metodi di creazione principali, ovvero la creazione da zero e l’importazione e la conversione, con supporto migliorato per i campi avanzati basati su LLM e la coerenza del brand.

>[!NOTE]
>
> Forms Experience Builder è disponibile nell’ambito del programma per i primi utilizzatori. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa libreria di prompt è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. I prompt, gli esempi e le best practice possono cambiare man mano che Forms Experience Builder continua a evolversi durante il programma per primi utilizzatori.

## Utilizzo di questa libreria di prompt

Questa libreria fornisce modelli di prompt riutilizzabili per scenari comuni di creazione di moduli. Per best practice complete, consulta la [Guida introduttiva di Forms Experience Builder](forms-ai-assistant-getting-started.md#best-practices).

### Suggerimenti rapidi per questa libreria

- **Inizia con gli esempi**: utilizza i prompt forniti come modelli e adattali alle tue esigenze
- **Due metodi di creazione**: scegli Crea da zero o Importa e converti.
- **Specificità**: aggiungi dettagli personali agli esempi generici
- **Verifica approfonditamente**: convalida sempre i risultati nel tuo ambiente specifico

### Modelli e stili del brand

**Prepara in anticipo le risorse del brand per la creazione di moduli coerenti:**

- **Modelli marchio** - Prepara modelli di modulo standardizzati con i colori, i font e i modelli di layout della tua organizzazione
- **Linee guida per gli stili** - Definisci stili di campo coerenti, progettazioni di pulsanti e standard di spaziatura che Forms Experience Builder può applicare
- **Libreria componenti** - Collabora con il team di sviluppo per preparare componenti modulo riutilizzabili che corrispondano alla tua brand identity
- **Risorse visive**: prepara logo, icone ed elementi di sfondo per l’integrazione dei moduli

<!-- **Example Brand Application Prompt:**

    Apply our financial services brand template with:
    - Corporate blue (#003366) and silver (#C0C0C0) color scheme
    - Open Sans font family for all text
    - 16px minimum font size for accessibility
    - Consistent 24px spacing between sections
    - Corporate logo in header with proper sizing
    - Professional button styling with hover effects

>[!NOTE]
>
>**Custom Components**: Check with your development team about using organization-specific components and their compatibility with Forms Experience Builder before implementing custom brand elements.

>[!NOTE]
>
> This prompt library has been updated to reflect the streamlined Forms Experience Builder capabilities. Some advanced integration and testing features shown in examples may require additional configuration.

-->


## Esempi di sviluppo incrementale

Questi esempi mostrano come creare moduli passo dopo passo, iniziando in modo semplice e aggiungendo complessità gradualmente:

### Esempio 1: creazione incrementale di un modulo di contatto

**Passaggio 1 - Inizia in modo semplice:**

    Crea un modulo di contatto di base con i campi nome, e-mail e messaggio

**Passaggio 2 - Aggiungi convalida:**

    Rendi obbligatori @name e @email i campi con la convalida appropriata

**Passaggio 3 - Migliora l’esperienza utente:**

    Aggiungi testo segnaposto: @name &quot;Nome e cognome&quot;, @email &quot;your.email@company.com&quot;, @message &quot;Come possiamo aiutarci&quot;

**Passaggio 4 - Aggiungi funzionalità avanzate:**

    Aggiungi un tipo di richiesta a discesa con le opzioni: &quot;Domanda generale&quot;, &quot;Richiesta di supporto&quot;, &quot;Richiesta di informazioni sulle vendite&quot;, &quot;Partnership&quot;

**Passaggio 5 - Implementa logica condizionale:**

    /create-rule mostra @urgencyLevel menu a discesa (Basso, Medium, Alto) solo quando @inquiryType è uguale a &quot;Richiesta di supporto&quot;

### Esempio 2: creazione incrementale di un modulo di registrazione

**Passaggio 1 - Struttura di base:**

    Crea un modulo di registrazione utente con il pannello informazioni personali

**Passaggio 2 - Aggiungi campi obbligatori:**

    Aggiungi campi per @firstName, @lastName, @email, @phoneNumber con convalida appropriata

**Passaggio 3 - Aggiungi logica di business:**

    Crea una regola: se il @age è inferiore a 18, mostra sezione informazioni padre/tutore

**Passaggio 4 - Migliora con preferenze:**

    Aggiungi un pannello preferenze con @newsletterSubscription, @marketingConsent, @termsAccepted

**Passaggio 5 - Aggiungi caricamento file:**

    Includi un campo di caricamento file per @profilePicture con limite di dimensione di 5 MB

## Creazione e gestione moduli

**Quando utilizzare:** quando è necessario creare nuovi moduli o modificare quelli esistenti.

**Come utilizzare:** scegli uno dei due approcci seguenti: Crea da zero o Importa e converti (consulta la [Guida introduttiva](forms-ai-assistant-getting-started.md#two-ways-to-create-forms)).

**Esempio di prompt - Creazione semplice del modulo:**

    Crea un modulo di feedback del cliente con:
    - Valutazione del prodotto (1-5 stelle)
    - Campo di commento per feedback dettagliato
    - E-mail del cliente (facoltativo)
    - Invia a notifica e-mail

**Esempio di prompt: creazione modulo complesso:**

    Crea un modulo di onboarding completo per i dipendenti con:
    
    **Sezione informazioni personali:**
    - Nome completo (primo, secondo e ultimo)
    - Data di nascita con convalida dell&#39;età
    - Informazioni di contatto (e-mail, telefono, indirizzo)
    - Dettagli di contatto di emergenza
    
    **Dettagli sull&#39;impiego:**
    - Selezione di posizione e reparto
    - Data di inizio con convalida del giorno lavorativo
    - Informazioni sullo stipendio con avviso di riservatezza
    - Struttura di reporting
    
    **Caricamento documento:**
    - Caricamento curriculum/CV (PDF, DOC, DOC, DOC, DOCX)
    - Documenti di verifica ID
    - Moduli fiscali e informazioni bancarie
    - Contratto di lavoro firmato
    
    **Preferenze:**
    - Selezione dei benefici con il calcolatore dei costi
    - Preferenze programmazione lavoro
    - Requisiti di formazione
    - Necessità attrezzature
    
    **Regole di convalida:**
    - Convalida formato e-mail
    - Convalida formato numero di telefono
    - Età non superiore a 18
    - Caricare tutti i documenti richiesti
    - Condizioni accettato
    
    **Invia azioni:**
    - Invia un&#39;e-mail di conferma al nuovo dipendente
    - Notifica al reparto HR
    - Crea record dipendente nel sistema HR
    - Pianifica riunione orientamento

**Prompt gestione moduli:**

    Importa il modulo di richiesta PDF e convertilo in un modulo adattivo con convalida avanzata
    
    Aggiorna il modulo di contatto esistente per includere gli handle di social media e il metodo di contatto preferito
    
    Riorganizza il modulo di registrazione in una procedura guidata in tre passaggi: informazioni personali, preferenze, conferma

## Gestione e configurazione del campo

**Quando utilizzare:** quando hai bisogno dio aggiungere, modificare o configurare campi modulo.

**Come utilizzare:** specifica i tipi di campo, i requisiti di convalida e i requisiti dell’esperienza utente.

**Esempio di prompt: aggiunta di un campo di base:**

    Aggiungi un campo di immissione testo per &quot;Nome società&quot; con segnaposto &quot;Inserisci il nome società&quot;

**Esempio di prompt: configurazione avanzata del campo:**

    Aggiungi una sezione di indirizzo completa con:
    
    **Indirizzo:**
    - Indirizzo 1 (obbligatorio, massimo 100 caratteri)
    - Indirizzo 2 (facoltativo, massimo 100 caratteri)
    - Città (obbligatorio, a discesa con le città comuni)
    - Stato/Provincia (obbligatorio, a discesa)
    - Codice postale (obbligatorio, convalida formato)
    - Paese (obbligatorio, predefinito &quot;Stati Uniti&quot;)
    
    **Regole di convalida:**
    - Il codice postale deve corrispondere alla selezione dello stato
    - Indirizzo 1 non può essere empty
    - La città deve essere valida per lo stato selezionato
    
    **Esperienza utente:**
    - Completamento automatico per i campi indirizzo
    - Cancella etichette e testo della guida
    - Campi di input descrittivi per dispositivi mobili
    - Conformità per l&#39;accessibilità

**Prompt di configurazione campo:**

    Rendi obbligatorio @email campo con convalida in tempo reale e messaggio di errore personalizzato
    
    Aggiungi un elenco a discesa per @country con opzioni per Stati Uniti, Canada, Regno Unito, Germania, Francia e &quot;Altro&quot;
    
    Configura @phoneNumber campo con formato (XXX) XXX-XXXX e convalida
    
    Aggiungi un campo di caricamento file per @resume con restrizioni PDF e DOC, massimo 5 MB

## Campi avanzati migliorati con LLM

**Quando utilizzare:** quando sono necessari campi con opzioni precompilate che sfruttano la knowledge base dell’intelligenza artificiale.

**Come utilizzare:** se ci sono campi di richiesta che richiedono set di dati completi. L’intelligenza artificiale può compilare automaticamente le opzioni utilizzando la propria conoscenza incorporata.

### Campi geografici e di posizione

**Aeroporti e trasporti:**

    Aggiungi un elenco a discesa per gli aeroporti di partenza con tutti i principali aeroporti internazionali
    Aggiungi il campo dell&#39;aeroporto di arrivo con i codici IATA e i nomi completi
    Crea un campo per l&#39;aeroporto più vicino alla posizione dell&#39;utente
    Aggiungi una selezione di stazioni ferroviarie per le città europee

**Aree amministrative:**

    Aggiungi un elenco completo degli stati degli Stati Uniti con le abbreviazioni
    Crea un elenco a discesa di un paese con codici ISO e nomi completi
    Aggiungi un campo per le principali città del mondo con fusi orari
    Includi un elenco a discesa di province e territori canadesi
    Aggiungi un campo per le contee e le aree postali del Regno Unito

### Dati aziendali e di settore

**Classificazioni aziendali:**

    Aggiungi un campo per la classificazione del settore con codici NAICS
    Crea un elenco a discesa dei tipi di entità business (LLC, Corporation, Partnership, ecc.)
    Aggiungi un campo per le categorie di dimensione società (avvio, PMI, impresa)
    Includi selezione reparto per organizzazioni di grandi dimensioni
    Aggiungi un campo per i tipi di servizi professionali

**Classificazioni professionali:**

    Aggiungi un campo per i titoli di lavoro con ruoli di settore comuni
    Crea un elenco a discesa di certificazioni professionali per campo
    Includi livelli di formazione con tipi di laurea
    Aggiungi un campo per anni di intervalli di esperienza
    Crea una selezione per linguaggi e framework di programmazione

### Standard e normative

**Aree finanziaria e legale:**

    Aggiungi un campo per i codici valuta con simboli e tassi di cambio
    Crea un elenco a discesa di tipi di ID imposta per paese
    Includi un campo per i tipi di documenti legali
    Aggiungi opzioni metodo di pagamento con caratteristiche di sicurezza
    Crea una selezione per gli istituti bancari per paese

**Standard tecnici:**

    Aggiungi un elenco a discesa dei tipi di formato file con estensioni
    Includi opzioni del protocollo di rete
    Aggiungi un campo per i tipi di database e le versioni
    Crea una selezione per i metodi di autenticazione API

### Settore sanitario e medicale

**Classificazioni mediche:**

    Aggiungi un campo per le specializzazioni mediche
    Crea un elenco a discesa di farmaci comuni con nomi generici
    Includi un campo per i tipi di provider di assicurazioni
    Aggiungi una selezione per le relazioni di contatto di emergenza medica
    Crea un campo per le restrizioni alimentari e le allergie

### Intelligence su orario e calendario

**Campi data e ora:**

    Aggiungi un campo per gli orari lavorativi con gestione del fuso orario
    Crea un elenco a discesa delle festività per paese
    Includi opzioni stagionali con intervalli di date
    Aggiungi un campo per la prenotazione di una sala conferenze con disponibilità
    Crea una selezione per i modelli di riunione ricorrenti

### Categorie di prodotti e servizi

**Classificazioni e-commerce:**

    Aggiungi un campo per le categorie di prodotto con sottocategorie
    Crea un elenco a discesa dei metodi di spedizione con le stime di consegna
    Includi un campo per le opzioni dei criteri di restituzione
    Aggiungi una selezione per i livelli di priorità del cliente
    Crea un campo per i cicli di fatturazione dell&#39;abbonamento

**Esempio di prompt per campi avanzati:**

    &quot;Aggiungere un campo aeroporto di partenza con tutti i principali aeroporti del mondo, inclusi i codici IATA e i nomi delle città&quot;
    
    &quot;Creare un campo di settore completo utilizzando la classificazione NAICS standard con sottocategorie tecnologiche&quot;
    
    &quot;Includere un elenco a discesa di certificazione professionale che si adatta in base al campo di lavoro selezionato&quot;
    
    &quot;Aggiungere un campo numero di telefono internazionale che si formatta in base al paese selezionato&quot;
    
    &quot;Creare un campo di selezione universitario con le principali istituzioni organizzate per paese e classificazione&quot;

## Creazione di regole e logica di business

**Quando utilizzare:** quando è necessario implementare logica condizionale, regole di convalida o processi aziendali.

**Come utilizzare:** per descrivere chiaramente la logica di business, specificando condizioni e azioni.

**Prompt di esempio: logica condizionale semplice:**

    Crea una regola che mostri il pannello @spouseInformation solo quando @maritalStatus è uguale a “Sposato”

**Esempio di prompt: regole aziendali complesse:**

    Implementare la convalida completa della richiesta di prestito:
    
    **Convalida del reddito:**
    - Se il @annualIncome è inferiore a 30000:
    - Visualizzare il messaggio di avviso: &quot;Il reddito potrebbe essere insufficiente per l&#39;importo del prestito richiesto&quot;
    - Richiedere ulteriore documentazione sul reddito
    - Visualizzare il messaggio: &quot;Potrebbe essere richiesta documentazione aggiuntiva&quot;
    - Se il @annualIncome è superiore a 100000:
    - Visualizzare le opzioni dei servizi premium
    - Abilitare la casella di controllo di elaborazione prioritaria
    
    **Convalida basata sull&#39;età:**
    - Se @age è inferiore a 18:
    - Visualizzare le informazioni padre caricamento della firma obbligatorio
    - Modificare il testo del pulsante Invia in &quot;Invia per revisione&quot;
    - Se @age 65 anni o più:
    - Mostra opzioni sconto senior
    - Aggiungi preferenze di accessibilità sezione
    

**Prompt specifici per regole:**

    Crea una **regola di visibilità** che mostra @spouseInformation pannello solo quando @maritalStatus è uguale a &quot;Coniugato&quot; o &quot;Collaborazione domestica&quot;
    
    Aggiungi **divulgazione progressiva** dove vengono visualizzate ulteriori domande in base alle risposte precedenti. Inizia con informazioni di base, quindi mostra i follow-up pertinenti
    
    Implementa **impostazioni predefinite avanzate** in cui @country selezione imposta automaticamente i campi correlati. Consenti sostituzione manuale

## Integrazione e invio dei dati

**Quando utilizzarlo:** quando è necessario connettere i moduli a sistemi back-end, database o servizi esterni.

**Come utilizzarlo:** inizia con la configurazione di base dell’invio, quindi aggiungi ulteriori integrazioni in modo incrementale. Specifica il tipo di integrazione, i requisiti del formato dati e le preferenze di gestione degli errori.

**Prompt di esempio - Inizia con invio di base:**

    Configura invio modulo di base per @applicationForm:
    
    **Invio primario:**
    - Invia dati modulo all&#39;endpoint REST: `/api/v1/applications`
    - Formatta dati come JSON
    - Mostra messaggio di operazione riuscita: &quot;Applicazione inviata correttamente&quot;
    - Mostra messaggio di errore se l&#39;invio non riesce: &quot;Invio non riuscito, riprova&quot;

**Aggiungi azioni secondarie in modo in modo incrementale:**

    Aggiungi notifica e-mail a @applicationForm: invia un messaggio e-mail di conferma all@emailindirizzo con numero di riferimento dell&#39;applicazione
    
    Aggiungi l&#39;integrazione CRM a @applicationForm: crea un nuovo record cliente potenziale con @firstName, @lastName, @email e imposta lo stato su &quot;Nuova applicazione&quot;

**Prompt di esempio: invio multicanale standard:**

    Configura invio modulo con più destinazioni dati:
    
    **Invio principale:**
    - Invia dati modulo all&#39;endpoint REST: `/api/v1/applications`
    - Includi intestazione autenticazione con chiave API
    - Formatta i dati come JSON con oggetti nidificati per indirizzo e impiego
    - Gestisci risposta di successo (201) mostrando il messaggio di ringraziamento
    
    **Azioni secondarie:**
    - Invia e-mail di notifica al richiedente all&#39;indirizzo @email
    - Copia i dati dell&#39;applicazione nel sistema di tracciamento
    - Attiva il flusso di lavoro per il processo di approvazione
    - Crea record nel CRM con stato nuovo Applicazione&quot;
    
    **Gestione degli errori:**
    - Se l&#39;invio primario non riesce, salvare i dati localmente e riprovare
    - Mostra messaggio di errore intuitivo: &quot;Invio temporaneamente non disponibile&quot;
    - Fornire l&#39;opzione per scaricare i dati del modulo come backup
    - Inviare un messaggio e-mail di avviso al team di amministrazione sull&#39;invio non riuscito
    
    **Flusso di successo:**
    - Reindirizzare alla pagina di conferma con il numero di riferimento dell&#39;applicazione
    - Inviare un messaggio e-mail di conferma con i passaggi successivi
    - Visualizzare la timeline di elaborazione stimata 

**Prompt specifici per integrazione:**

    Connetti il modulo al **sistema CRM** per creare nuovi lead. Mappa @firstName su FirstName, @email su Email, imposta LeadSource su &quot;Web Form&quot; e Status su &quot;New&quot;
    
    Imposta **trigger del flusso di lavoro** quando il modulo viene inviato. Passa tutti i dati del modulo e attiva il flusso di lavoro di approvazione con la notifica del manager
    
    Configura **integrazione del database** per salvare gli invii del modulo come record. Crea una nuova cartella per ogni invio con documenti caricati

<!-- ## Import & Convert Existing Forms

**When to use:** When you have existing forms, documents, or designs to transform into modern AEM forms.

**How to use:** Upload your source file and describe the conversion requirements (see [Import Guide](forms-ai-assistant-getting-started.md#2-import-and-convert)).


**Design Import Prompts:**

    Import this **design mockup** and convert it into an adaptive form. Maintain the exact visual design but add proper validation and mobile responsiveness

    Analyze this **image of a paper form** and recreate it digitally. Improve the layout for better mobile experience while keeping all mandatory fields

    Convert this **existing HTML form** to AEM adaptive form format. Preserve all functionality but add AEM-specific features like rules and themes

## Mobile Optimization & Responsiveness

**When to use:** When forms need to work seamlessly across all device types and screen sizes.

**How to use:** Start with basic mobile optimization, then enhance with advanced features. Emphasize mobile-first approach and specify breakpoint behaviors incrementally.

**Example Prompt - Start with Basic Mobile Optimization:**

    Make @contactForm mobile-friendly with:
    
    **Basic Mobile Layout:**
    - Single column layout for all form sections
    - Larger touch targets for buttons and inputs
    - Responsive design that works on phones and tablets

**Then Add Advanced Mobile Features:**

    Enhance @contactForm mobile experience with:
    - Sticky submit button at bottom of screen
    - Touch-friendly date pickers
    - Swipe gestures for multi-step navigation

**Example Prompt - Comprehensive Mobile-First Optimization:**

    Optimize this form for **mobile-first responsive design**:
    
    **Mobile Layout (320px - 768px):**
    - Single column layout for all form sections
    - Larger touch targets (minimum 44px height)
    - Simplified navigation with collapsible sections
    - Sticky submit button at bottom of screen
    - Auto-zoom disabled on input focus
    
    **Tablet Layout (768px - 1024px):**
    - Two-column layout for shorter fields (name, email)
    - Single column for complex fields (address, comments)
    - Side navigation for multi-step forms
    - Optimized for both portrait and landscape
    
    **Desktop Layout (1024px+):**
    - Multi-column layouts where appropriate
    - Horizontal form sections for related fields
    - Sidebar navigation for long forms
    - Hover states and advanced interactions

**Mobile-Specific Prompts:**

    Make this form **touch-friendly** with larger buttons and simplified navigation for mobile users

    Optimize form for **tablet users** with appropriate field sizes and navigation patterns

    Add **swipe gestures** for multi-step form navigation on mobile devices

## Accessibility & Compliance

**When to use:** When forms need to meet accessibility standards (WCAG) or compliance requirements.

**How to use:** Specify the required compliance level and any specific accessibility features needed.

**Example Prompt - Basic Accessibility:**

    Make @contactForm accessible with:
    
    **Basic Accessibility:**
    - Proper ARIA labels for all form fields
    - Keyboard navigation support
    - High contrast color scheme
    - Screen reader compatibility
    - Focus indicators for all interactive elements

**Example Prompt - Advanced Accessibility:**

    Implement comprehensive accessibility for @applicationForm:
    
    **WCAG 2.1 AA Compliance:**
    
    - Semantic HTML structure with proper headings
    - ARIA landmarks and roles for navigation
    - Color contrast ratio of at least 4.5:1
    - Keyboard-only navigation support
    - Screen reader announcements for dynamic content
    
    **Form-Specific Accessibility:**
    
    - Error messages announced to screen readers
    - Field validation with clear error descriptions
    - Progress indicators for multi-step forms
    - Skip navigation links for keyboard users
    - Alternative text for all images and icons
    
    **User Experience:**
    
    - Clear focus indicators on all interactive elements
    - Logical tab order through form fields
    - Descriptive link text and button labels
    - Help text available for complex fields
    - Timeout warnings for session expiration

**Accessibility-Specific Prompts:**

    Add **screen reader support** to this form with proper ARIA labels and announcements

    Implement **keyboard navigation** for all form interactions and navigation elements

    Ensure **color contrast** meets WCAG AA standards for all text and interactive elements  

## Performance Optimization

**When to use:** When forms need to load quickly and perform well under various conditions.

**How to use:** Specify performance requirements and optimization strategies.

**Example Prompt - Basic Performance:**

    
Optimize @contactForm for performance:

**Loading Optimization:**

- Lazy load non-critical form sections
- Minimize initial bundle size
- Optimize images and assets
- Enable caching for static resources
    

**Example Prompt - Advanced Performance:**

    
Implement comprehensive performance optimization for @applicationForm:

**Loading Performance:**

- Progressive loading of form sections
- Optimize images with WebP format
- Minimize JavaScript bundle size
- Enable gzip compression for all assets

**Runtime Performance:**

- Debounce validation calls to reduce API requests
- Optimize conditional logic execution
- Cache frequently used data
- Implement virtual scrolling for long lists

**User Experience:**

- Show loading indicators for async operations
- Provide offline capability for form data
- Auto-save form progress every 30 seconds
- Optimize form submission with retry logic

**Monitoring:**

- Track form load times and user interactions
- Monitor validation performance
- Measure submission success rates
- Alert on performance degradation
    

**Performance-Specific Prompts:**

    
Optimize form **loading speed** by implementing progressive loading and asset optimization
    

    
Add **auto-save functionality** to prevent data loss during form completion
    

    
Implement **offline support** so users can complete forms without internet connection
    

## Testing & Quality Assurance

**When to use:** When forms need comprehensive testing to ensure reliability and user satisfaction.

**How to use:** Specify testing scenarios, validation requirements, and quality metrics.

**Example Prompt - Basic Testing:**

    
Add comprehensive testing for @contactForm:

**Functional Testing:**

- Test all form field validations
- Verify submit functionality works correctly
- Test error handling and user feedback
- Validate conditional logic and rules
    

**Example Prompt - Advanced Testing:**

    
Implement comprehensive testing strategy for @applicationForm:

**Functional Testing:**

- Unit tests for all validation rules
- Integration tests for submit actions
- End-to-end testing for complete user flows
- Cross-browser compatibility testing

**User Experience Testing:**

- Usability testing with target user groups
- Accessibility testing with screen readers
- Mobile device testing on various screen sizes
- Performance testing under load conditions

**Quality Assurance:**

- Automated testing for regression prevention
- Manual testing for edge cases and scenarios
- Security testing for data protection
- Compliance testing for regulatory requirements

**Monitoring:**

- Track form completion rates and abandonment
- Monitor error rates and user feedback
- Measure performance metrics and load times
- Analyze user behavior and interaction patterns
    

**Testing-Specific Prompts:**

    
Add **automated testing** for all form validations and submit functionality
    

    
Implement **user acceptance testing** scenarios for complete form workflows
    

    
Set up **performance monitoring** to track form load times and user interactions
    
-->

## Documentazione di riferimento ai comandi

### Comandi essenziali

| Comando | Miglior caso d’uso | Esempio |
|---------|---------------|---------|
| `/create-form` | Avvio di nuovi moduli | `/create-form employee onboarding with personal info and benefits selection` |
| `/add-form` | Aggiunta di moduli alle pagine | `/add-form newsletter signup with email and preferences` |
| `/update-layout` | Modifica della struttura del modulo | `/update-layout wizard with 4 steps: info, preferences, review, confirm` |
| `/update-field` | Modifica delle proprietà del campo | `/update-field @email to be mandatory with real-time validation` |
| `/create-rule` | Aggiunta di un comportamento dinamico | `/create-rule show @spouseInfo if @maritalStatus equals "Married"` |
| `/create-panel` | Organizzazione delle sezioni del modulo | `/create-panel Employment Details with job title, company, salary fields` |
| `/add-panel` | Conversione delle progettazioni | `/add-panel from uploaded form image with field recognition` |
| `/help` | Ottenere assistenza | `/help how to implement multi-step validation?` |

### Riferimenti ai campi

Utilizza la sintassi `@fieldName` per fare riferimento a campi esistenti nei prompt:

- `@email`: campo e-mail di riferimento
- `@firstName`: campo nome di riferimento
- `@maritalStatus`: campo stato civile di riferimento

### Tipi di componente

**Componenti di input:**

- `text`, `email`, `number`, `tel`, `date`, `checkbox`, `radio`, `dropdown`, `file`, `textarea`

**Componenti contenitore:**

- `fieldset`, `panel`, `repeatable`, `wizard`

### Proprietà componente

**Proprietà universali (tutti i componenti):**

- **Tipo**: tipo di componente
- **Nome**: identificatore del campo per l’invio del modulo
- **Etichetta**: visualizza il testo per il campo
- **Descrizione**: testo di istruzioni per il campo
- **Visibile**: booleano per la visibilità iniziale
- **Obbligatorio**: booleano per i campi obbligatori

**Proprietà del campo di input:**

- **Valore**: valore predefinito/iniziale
- **Segnaposto**: testo di suggerimento per i campi di input
- **Min**: valore minimo (per numeri/date)
- **Max**: valore massimo (per numeri/date)

**Proprietà di caricamento del file:**

- **Accetta**: tipi di file (.pdf, .doc, .docx, .jpg, .png, ecc.)
- **Multipli**: booleano per la selezione di più file

**Proprietà di controllo della selezione:**

- **Opzioni**: scelte per i menu a discesa (elenco separato da virgole)
- **Selezionato**: selezione predefinita per caselle di controllo/radio

**Proprietà del contenitore:**

- **Set di campi**: raggruppamento di campi correlati
- **Ripetibile**: booleano per sezioni ripetibili

**Proprietà avanzate:**

- **Espressione visibile**: formula per la visibilità condizionale (=formula)
- **Espressione valore**: formula per valori calcolati (=formula)

### Comandi di integrazione

**Azioni di invio:**

- Notifiche e-mail
- Invii API REST
- Archiviazione cloud (Azure, SharePoint)
- Automazione del flusso di lavoro (Power Automate, Workfront Fusion)
- Piattaforme di marketing (Marketo)
- Integrazioni CRM

### Linee guida per la sintassi dei prompt

- **Riferimenti campo**: utilizza `@fieldName` per i campi esistenti
- **Comandi**: utilizza `/command` per azioni specifiche
- **Linguaggio naturale**: descrivi i requisiti in modo chiaro e specifico

### Elenco di controllo della convalida

Per informazioni complete sulle best practice e le linee guida per la convalida, consulta la [Guida introduttiva di Forms Experience Builder](forms-ai-assistant-getting-started.md#best-practices).

*Questa libreria di prompt viene continuamente aggiornata in base al feedback degli utenti e alle nuove funzionalità di Forms Experience Builder. Per le funzionalità e gli esempi più recenti, consulta la [documentazione di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=it).*
