---
title: Assistente IA di AEM Forms - Libreria dei prompt
description: Raccolta di pattern di prompt ed esempi dimostrati per la creazione di moduli con assistenza IA nell’interfaccia utente per la gestione dei moduli, nell’editor dei moduli adattivi e nell’editor universale.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: 333d42e0-625f-432e-a61b-5d49bf08765a
source-git-commit: abcd5be06b0bf24ebe8737827fb4abdbf148b1b0
workflow-type: ht
source-wordcount: '1613'
ht-degree: 100%

---

# Assistente IA di AEM Forms - Libreria dei prompt

Raccolta di pattern ed esempi di prompt riutilizzabili per scenari comuni di creazione di moduli. Considerali come modelli che puoi adattare alle tue esigenze specifiche. Ogni sezione tratta un caso d’uso particolare con indicazioni su quando utilizzarlo ed esempi dimostrati.

>[!NOTE]
>
> L’Assistente IA per AEM Forms è disponibile nel programma per primi utilizzatori. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a mailto:aem-forms-ea@adobe.com.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa libreria di prompt è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. I prompt, gli esempi e le best practice possono cambiare man mano che l’Assistente IA per AEM Forms continua a evolversi durante il programma per primi utilizzatori.

## Best practice per risultati ottimali

Per ottenere il massimo dall’Assistente IA, tieni presente i seguenti consigli:

### Inizia in modo semplice, crea gradualmente

Inizia con comandi specifici più piccoli (ad esempio, “Aggiungi un input di testo per ‘Nome’”) invece di richieste complesse in più passaggi fin da subito. Questo approccio contribuisce a garantire precisione e semplifica la risoluzione dei problemi se qualcosa non funziona come previsto.

**Esempio di inizio semplice:**

```
Add a text input field for "First Name" with placeholder "Enter your first name"
```

**Quindi costruisci in modo graduale:**

```
Make @firstName mandatory and add validation message "First name is mandatory"
```

### Utilizzare la terminologia di AEM Forms

Utilizza termini come “pannello”, “campo di input di testo”, “gruppo di caselle di controllo”, “azione di invio”, “regola” ecc. per una comprensione migliore da parte dell’assistente. Ciò assicura che l’IA interpreti correttamente le richieste nel contesto di AEM Forms.

**Termini preferiti:**

- “campo di input di testo” invece di “casella di testo”
- “gruppo di caselle di controllo” invece di “caselle di controllo”
- “menu a discesa” invece di “seleziona elenco”
- “pannello” invece di “sezione” o “contenitore”
- “invia azione” invece di “invio modulo”
- “regola” invece di “logica” o “condizione”

### Riferimento ai campi in modo chiaro

Durante la configurazione dei campi esistenti, utilizza la notazione @fieldName (ad esempio, “Rendi @firstName obbligatorio”). Questo aiuta l’IA a identificare esattamente a quale campo stai facendo riferimento, soprattutto nei moduli complessi con molti campi.

**Esempi:**

- `Make @email mandatory with real-time validation`
- `Show @spouseInfo panel when @maritalStatus equals "Married"`
- `Set @country default value to "United States"`

### Rivedere sempre i piani

Prima di fare clic su “Applica”, rivedi sempre attentamente i piani per le modifiche proposte dall’assistente nell’editor universale. L’IA ti mostrerà cosa intende fare; prenditi un momento per verificare che corrisponda alle tue aspettative.

### Convalidare manualmente

Dopo che l’assistente apporta le modifiche, visualizza sempre in anteprima e testa il modulo per assicurarti che funzioni e appaia come previsto. L’IA è uno strumento potente, ma la convalida finale è fondamentale per garantire la qualità.

**Elenco di controllo della convalida:**

- Testare la funzionalità del modulo in modalità anteprima
- Verificare che la logica condizionale funzioni correttamente
- Controllare la reattività dei dispositivi mobili
- Invio di un modulo di test
- Convalidare le funzioni di accessibilità

### Iterare e perfezionare

Se il primo prompt non restituisce il risultato esatto, prova a riformulare o suddividere la richiesta in passaggi più piccoli. L’IA apprende dal contesto, quindi fornire dettagli più specifici spesso migliora i risultati.

**Esempio di iterazione:**

1. Primo tentativo: “Rendi il modulo adatto ai dispositivi mobili”
2. Perfezionato: “Ottimizza il layout del modulo per schermi di dispositivi mobili sotto i 768px con layout a colonna singola e target touch più grandi”

### Fornire feedback

Utilizza il meccanismo di feedback incorporato per aiutare l’assistente ad apprendere e migliorare. Il tuo feedback aiuta a migliorare l’IA per tutti.


## Esempi di sviluppo incrementale

Questi esempi mostrano come creare moduli passo dopo passo, iniziando in modo semplice e aggiungendo complessità gradualmente:

### Esempio 1: creazione incrementale di un modulo di contatto

**Passaggio 1 - Inizia in modo semplice:**

```
Create a basic contact form with name, email, and message fields
```

**Passaggio 2 - Aggiungi convalida:**

```
Make @name and @email mandatory fields with appropriate validation
```

**Passaggio 3 - Migliora l’esperienza utente:**

```
Add placeholder text: @name "Your full name", @email "your.email@company.com", @message "Tell us how we can help"
```

**Passaggio 4 - Aggiungi funzionalità avanzate:**

```
Add a dropdown @inquiryType with options: "General Question", "Support Request", "Sales Inquiry", "Partnership"
```

**Passaggio 5 - Implementa logica condizionale:**

```
Show @urgencyLevel dropdown (Low, Medium, High) only when @inquiryType equals "Support Request"
```

### Esempio 2: creazione incrementale di un modulo di registrazione

**Passaggio 1 - Struttura di base:**

```
Create a user registration form with personal information panel
```

**Passaggio 2 - Aggiungi campi principali:**

```
Add text input fields: @firstName, @lastName, @email, @phone to the personal information panel
```

**Passaggio 3 - Aggiungi convalida:**

```
Make @firstName, @lastName, and @email mandatory with real-time validation
```

**Passaggio 4 - Aggiungi informazioni account:**

```
Create a new panel "Account Information" with @username and @password fields
```

**Passaggio 5 - Migliora sicurezza:**

```
Add password confirmation field @confirmPassword with validation to match @password
```

**Passaggio 6 - Aggiungi preferenze:**

```
Create "Preferences" panel with @newsletter checkbox and @communicationMethod radio group (Email, SMS, Phone)
```

Questo approccio incrementale consente di:

- Rilevare i problemi prima che si verifichino
- Testare accuratamente ogni funzione
- Effettuare modifiche in base al feedback degli utenti
- Mantenere un maggiore controllo sul processo di sviluppo

## Avvio di nuovi moduli

**Quando utilizzarlo:** all’inizio di qualsiasi progetto di modulo. Questo prompt consente all’IA di comprendere i requisiti e creare la struttura di base.

**Come utilizzarlo:** inizia con la struttura di base e i requisiti principali. Specifica il tipo di modulo, il pubblico di destinazione e lo scopo principale. Aggiungi complessità nei prompt successivi.

**Prompt di esempio - Inizio semplice:**

```
Create a **customer onboarding form** for new bank account applications with:

**Purpose:** Collect personal information for account setup
**Target Users:** New customers applying for checking/savings accounts
**Basic Structure:** Single panel with essential fields
**Core Fields:** Name, email, phone, account type selection

Start with a simple layout that we can enhance step by step.
```

**Quindi crea in modo incrementale:**

```
Add an address panel to @customerOnboardingForm with street address, city, state, and zip code fields
```

```
Add employment information panel with @employer, @jobTitle, and @annualIncome fields
```

```
Add file upload field @identityDocuments for identity verification (Accept: .pdf,.jpg,.png)
```

**Prompt alternativi di inizio semplice:**

```
Create a basic **event registration form** with name, email, and event selection fields
```

```
Build a simple **contact form** with name, email, and message fields
```

```
Design a basic **feedback survey** with rating scale and comments field
```

## Struttura e layout del modulo

**Quando utilizzarlo:** quando è necessario organizzare moduli complessi o migliorare l’esperienza utente tramite una migliore progettazione del layout.

**Come utilizzarlo:** concentrati sul percorso dell’utente e sul raggruppamento logico delle informazioni. Specifica le preferenze di layout e i modelli di navigazione.

**Prompt di esempio - Struttura di modulo con più passaggi:**

```
Convert this single-page form into a **3-step wizard** with:

**Step 1: Personal Information**
- Name, email, phone, address fields
- Progress indicator showing "Step 1 of 3"
- "Next" button (validate mandatory fields before proceeding)

**Step 2: Preferences & Requirements** 
- Service selection (checkbox group)
- Budget range (dropdown)
- Timeline preferences (radio group)
- Special requirements (text input field)

**Step 3: Review & Submit**
- Summary of all entered information
- Edit links to go back to specific steps
- Terms and conditions checkbox
- Submit button with confirmation

Include "Previous" and "Next" buttons, allow users to jump between completed steps, save progress automatically.
```

**Prompt di ottimizzazione del layout:**

```
Reorganize this form using a **wizard layout** for desktop and single column for mobile. 
```

```
Convert this long form into an **accordion layout** where users can expand/collapse sections.
```

```
Create a **vertical tabbed interface** for this form with tabs for: Basic Info, Contact Details, Preferences, and Review.
```

## Gestione e convalida del campo

**Quando utilizzarlo:** quando è necessario aggiungere, modificare o migliorare i campi modulo con regole e comportamenti di convalida specifici.

**Come utilizzarlo:** specifica i tipi di campo, i requisiti di convalida e le aspettative dell’esperienza utente. Fai riferimento ai campi esistenti utilizzando la sintassi @fieldName.


**Prompt di esempio - Miglioramento del campo:**

```
Enhance the form fields with these specific requirements:

**Email Field (@email):**
- Make mandatory with real-time validation
- Show green checkmark when valid format entered
- Display helpful error message: "Please enter a valid email address"
- Add placeholder: "your.email@company.com"

**Phone Number (@phone):**
- Type: tel for mobile optimization
- Make mandatory for business customers, optional for personal
- Add placeholder: "Enter your phone number"

**Date of Birth (@dateOfBirth):**
- Type: date with date picker
- Validate age is 18+ for account opening
- Show error if under 18: "Must be 18 or older to open account"

**File Upload (@documents):**
- Accept: .pdf,.doc,.docx
- Multiple: true for multiple document upload
- Show upload progress and file names after upload
```

**Prompt specifici per i campi:**

```
Add a **file upload field** for resume with these specs: Accept only PDF/DOC/DOCX files, allow multiple files, show upload progress, display file names after upload.
```

```
Create a **dropdown field** for country selection with all countries listed. Set default value based on user's location if available.
```

```
Build a **repeatable panel** for work experience where users can add/remove multiple jobs. Each entry needs: company, title, start date, end date, description.
```

## Logica e regole condizionali

**Quando utilizzarlo:** quando è necessario un comportamento dinamico del modulo basato su input utente o regole di business.

**Come utilizzarlo:** definisci chiaramente le condizioni e le azioni risultanti. Utilizza riferimenti di campo specifici e operatori logici.

**Prompt di esempio - Logica condizionale complessa:**

```
Implement these conditional rules for the application form:

**Business vs Personal Account Logic:**
- If @accountType equals "Business", show:
  - Business name field (mandatory)
  - Tax ID field (mandatory)
  - Business address section
  - Number of employees dropdown
- If @accountType equals "Personal", hide all business fields

**Income-Based Requirements:**
- If @annualIncome is less than 25000:
  - Show additional verification section
  - Make co-signer information mandatory
  - Display message: "Additional documentation may be required"
- If @annualIncome is greater than 100000:
  - Show premium services options
  - Enable priority processing checkbox

**Age-Based Validation:**
- If @age is under 18:
  - Show parent/guardian information section
  - Make parent signature upload mandatory
  - Change submit button text to "Submit for Review"
- If @age is 65 or older:
  - Show senior discount options
  - Add accessibility preferences section
```

**Prompt specifici per regole:**

```
Create a **visibility rule** that shows @spouseInformation panel only when @maritalStatus equals "Married" or "Domestic Partnership".
```

```
Add **progressive disclosure** where additional questions appear based on previous answers. Start with basic info, then show relevant follow-ups.
```

```
Implement **smart defaults** where @country selection auto-sets related fields. Allow manual override.
```

## Integrazione e invio dei dati

**Quando utilizzarlo:** quando è necessario connettere i moduli a sistemi back-end, database o servizi esterni.

**Come utilizzarlo:** inizia con la configurazione di base dell’invio, quindi aggiungi ulteriori integrazioni in modo incrementale. Specifica il tipo di integrazione, i requisiti del formato dati e le preferenze di gestione degli errori.

**Prompt di esempio - Inizia con invio di base:**

```
Configure basic form submission for @applicationForm:

**Primary Submission:**
- Send form data to REST endpoint: `/api/v1/applications`
- Format data as JSON
- Show success message: "Application submitted successfully"
- Show error message if submission fails: "Submission failed, please try again"
```

**Aggiungi azioni secondarie in modo in modo incrementale:**

```
Add email notification to @applicationForm: Send confirmation email to @email address with application reference number
```

```
Add CRM integration to @applicationForm: Create new lead record with @firstName, @lastName, @email, and set Status to "New Application"
```

**Prompt di esempio - Invio multicanale avanzato:**

```
Configure form submission with multiple data destinations:

**Primary Submission:**
- Send form data to REST endpoint: `/api/v1/applications`
- Include authentication header with API key
- Format data as JSON with nested objects for address and employment
- Handle success response (201) by showing thank you message

**Secondary Actions:**
- Send notification email to applicant at @email address
- Copy application data to tracking system
- Trigger workflow for approval process
- Create record in CRM with lead status "New Application"

**Error Handling:**
- If primary submission fails, save data locally and retry
- Show user-friendly error message: "Submission temporarily unavailable"
- Provide option to download form data as backup
- Send alert email to admin team about failed submission

**Success Flow:**
- Redirect to confirmation page with application reference number
- Send confirmation email with next steps
- Display estimated processing timeline
```

**Prompt specifici per integrazione:**

```
Connect this form to **CRM system** to create new leads. Map @firstName to FirstName, @email to Email, set LeadSource to "Web Form", and Status to "New".
```

```
Set up **workflow trigger** when form is submitted. Pass all form data and trigger approval workflow with manager notification.
```

```
Configure **database integration** to save form submissions as records. Create new folder for each submission with uploaded documents.
```

## Importazione e conversione della progettazione

**Quando utilizzarlo:** quando disponi di progettazioni di moduli esistenti (PDF, Figma, immagini) che devono essere convertite in moduli AEM funzionali.

**Come utilizzarlo:** fornisci un contesto chiaro sulla progettazione di origine e specifica eventuali modifiche o miglioramenti necessari.

**Prompt di esempio - Conversione modulo PDF:**

```
Convert this uploaded **PDF application form** into a functional AEM adaptive form:

**Source Analysis:**
- Analyze the PDF layout and identify all form fields
- Preserve the visual hierarchy and grouping
- Maintain the professional appearance and branding

**Field Mapping:**
- Convert PDF text fields to adaptive form text inputs
- Transform checkboxes to checkbox components
- Convert dropdown lists to AEM dropdown components
- Map signature areas to digital signature fields

**Enhancements:**
- Add real-time validation that wasn't possible in PDF
- Implement conditional logic for dependent fields
- Make the form responsive for mobile devices
- Add progress saving capability
- Include accessibility improvements (ARIA labels, keyboard navigation)

**Styling:**
- Match the original color scheme and fonts
- Maintain professional business appearance
- Ensure consistent spacing and alignment
- Add subtle animations for better user experience

Preserve all original field labels and help text, but improve the user experience with modern form interactions.
```

**Prompt di importazione della progettazione:**

```
Import this **design mockup** and convert it into an adaptive form. Maintain the exact visual design but add proper validation and mobile responsiveness.
```

```
Analyze this **image of a paper form** and recreate it digitally. Improve the layout for better mobile experience while keeping all mandatory fields.
```

```
Convert this **existing HTML form** to AEM adaptive form format. Preserve all functionality but add AEM-specific features like rules and themes.
```

## Ottimizzazione e reattività per dispositivi mobili

**Quando utilizzarlo:** quando i moduli devono funzionare senza problemi su tutti i tipi di dispositivi e dimensioni dello schermo.

**Come utilizzarlo:** inizia con l’ottimizzazione per dispositivi mobili di base, quindi migliora con le funzioni avanzate. Enfatizza l’approccio mobile-first e specifica i comportamenti dei punti di interruzione in modo incrementale.

**Prompt di sempio - Inizia con l’ottimizzazione per dispositivi mobili di base:**

```
Make @contactForm mobile-friendly with:

**Basic Mobile Layout:**
- Single column layout for all form sections
- Larger touch targets for buttons and inputs
- Responsive design that works on phones and tablets
```

**Aggiungi funzioni avanzate per dispositivi mobili:**

```
Enhance @contactForm mobile experience with:
- Sticky submit button at bottom of screen
- Touch-friendly date pickers
- Swipe gestures for multi-step navigation
```

**Prompt di esempio - Ottimizzazione completa mobile-first:**

```
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

**Touch Optimization:**
- Larger checkbox and radio button targets
- Swipe gestures for multi-step navigation
- Pull-to-refresh for saved drafts
- Touch-friendly date/time pickers

**Performance:**
- Lazy load non-critical form sections
- Optimize images and icons for mobile
- Minimize JavaScript for faster loading
- Progressive enhancement approach
```

**Prompt semplici specifici per dispositivi mobili:**

```
Make @checkoutForm mobile-optimized with large buttons and one-thumb navigation
```

```
Add touch-friendly controls to @surveyForm for tablet users
```

```
Enable offline functionality for @applicationForm with local data saving
```

## Accessibilità e conformità

**Quando utilizzarlo:** quando i moduli devono soddisfare gli standard di accessibilità (WCAG 2.1 AA) o i requisiti di conformità.

**Come utilizzarlo:** specifica i requisiti di accessibilità e gli standard di conformità che devono essere soddisfatti.

**Prompt di esempio - Implementazione accessibilità:**

```
Make this form **WCAG 2.1 AA compliant** with these accessibility features:

**Keyboard Navigation:**
- Logical tab order through all form elements
- Skip links to main content and form sections
- Keyboard shortcuts for common actions
- Focus indicators clearly visible on all interactive elements

**Screen Reader Support:**
- Proper ARIA labels for all form fields
- Descriptive error messages announced to screen readers
- Form section headings with proper hierarchy (h1, h2, h3)
- Progress announcements for multi-step forms

**Visual Accessibility:**
- Color contrast ratio minimum 4.5:1 for text
- Don't rely solely on color to convey information
- Text size minimum 16px for body text
- Scalable up to 200% without horizontal scrolling

**Motor Accessibility:**
- Large click targets (minimum 44x44px)
- Generous spacing between interactive elements
- No time limits or provide extension options
- Alternative input methods support

**Cognitive Accessibility:**
- Clear, simple language in all instructions
- Consistent navigation and layout patterns
- Error prevention and clear error recovery
- Help text and examples for complex fields

**Testing Requirements:**
- Test with screen readers (NVDA, JAWS, VoiceOver)
- Verify keyboard-only navigation
- Check color contrast with automated tools
- Validate HTML for semantic correctness
```

**Prompt specifici per conformità:**

```
Ensure this **healthcare form meets HIPAA requirements** with proper data encryption, audit logging, and privacy controls.
```

```
Make this **financial form PCI DSS compliant** with secure payment field handling and data protection measures.
```

```
Create a **government form meeting Section 508 standards** with full accessibility and plain language requirements.
```

## Test e garanzia di qualità

**Quando utilizzarlo:** quando è necessario convalidare la funzionalità del modulo, l’esperienza utente e le prestazioni tecniche.

**Come utilizzarlo:** specifica scenari di test, casi limite e criteri di qualità da verificare.

**Prompt di esempio- Test modulo completo:**

```
Create a **comprehensive testing plan** for this application form:

**Functional Testing:**
- Test all field validations with valid and invalid data
- Verify conditional logic shows/hides fields correctly
- Test file upload with various file types and sizes
- Validate calculation fields update correctly
- Test form submission with complete and incomplete data

**User Experience Testing:**
- Test form completion time (target: under 10 minutes)
- Verify error messages are helpful and actionable
- Test progress saving and restoration
- Validate mobile touch interactions
- Check form accessibility with assistive technologies

**Edge Case Testing:**
- Test with extremely long text inputs
- Verify behavior with special characters and emojis
- Test with slow internet connections
- Validate offline functionality if applicable
- Test browser back/forward button behavior

**Performance Testing:**
- Measure form load time (target: under 3 seconds)
- Test with large file uploads
- Verify memory usage with long form sessions
- Test concurrent user submissions
- Validate database performance under load

**Security Testing:**
- Test input sanitization and XSS prevention
- Verify CSRF protection is working
- Test file upload security restrictions
- Validate data encryption in transit and at rest
- Check authentication and authorization controls

**Cross-Browser Testing:**
- Test on Chrome, Firefox, Safari, Edge
- Verify mobile browsers (iOS Safari, Chrome Mobile)
- Test on different operating systems
- Validate older browser fallbacks
- Check print functionality across browsers
```

**Prompt specifici per test:**

```
Create **automated test scripts** for this form's critical user paths: successful submission, validation errors, and conditional logic.
```

```
Design a **user acceptance testing plan** with realistic scenarios and success criteria for business stakeholders.
```

```
Set up **performance monitoring** to track form completion rates, abandonment points, and submission success rates.
```

## Funzioni e integrazioni avanzate

**Quando utilizzarlo:** quando sono necessarie funzionalità di moduli sofisticate come l’assistenza IA, flussi di lavoro avanzati o integrazioni complesse.

**Come utilizzarlo:** definisci chiaramente le funzionalità avanzate e i requisiti di integrazione.

**Prompt di esempio - Modulo migliorato dall’IA:**

```
Add **AI-powered features** to enhance this application form:

**Smart Auto-Complete:**
- Use AI to suggest company names as user types
- Auto-populate address fields from partial input
- Suggest job titles based on industry selection
- Provide intelligent form completion suggestions

**Dynamic Question Generation:**
- Generate follow-up questions based on previous answers
- Adapt form complexity to user's experience level
- Show relevant optional fields based on user profile
- Personalize form sections for different user types

**Intelligent Validation:**
- Use AI to detect potentially incorrect information
- Suggest corrections for common data entry errors
- Validate business information against public databases
- Flag suspicious or inconsistent responses

**Content Optimization:**
- A/B test different form layouts automatically
- Optimize field order based on completion patterns
- Adjust form length based on user engagement
- Personalize help text based on user behavior

**Predictive Analytics:**
- Predict likelihood of form completion
- Identify users who might need assistance
- Suggest optimal times for form completion reminders
- Analyze drop-off points and suggest improvements

**Natural Language Processing:**
- Allow voice input for text fields
- Convert speech to text for accessibility
- Analyze open-text responses for sentiment
- Extract structured data from unstructured input
```

**Prompt di integrazione avanzata:**

```
Integrate with **CRM system** to pre-populate known customer data, update records in real-time, and trigger automated follow-up sequences.
```

```
Connect to **payment gateway** for secure transaction processing with PCI compliance, fraud detection, and multiple payment methods.
```

```
Implement **blockchain verification** for document authenticity, immutable audit trails, and decentralized identity verification.
```

## Risoluzione dei problemi e ottimizzazione

**Quando utilizzarlo:** quando i moduli presentano problemi di prestazioni, di esperienza utente o difficoltà tecniche.

**Come utilizzarlo:** descrivi chiaramente il problema specifico e il risultato desiderato.

**Prompt di esempio- Ottimizzazione delle prestazioni:**

```
Optimize this form for **better performance and user experience**:

**Current Issues:**
- Form takes 8+ seconds to load on mobile
- Users are abandoning at the address section (60% drop-off)
- File uploads frequently fail or timeout
- Validation errors are confusing users

**Performance Improvements:**
- Implement lazy loading for non-critical form sections
- Optimize images and reduce bundle size
- Add progressive loading indicators
- Cache frequently used data (country lists, etc.)
- Minimize JavaScript execution time

**User Experience Fixes:**
- Simplify the address section with auto-complete
- Add inline validation with helpful error messages
- Implement smart defaults based on user location
- Add progress saving every 30 seconds
- Provide clear instructions for each section

**Technical Optimizations:**
- Implement chunked file uploads with resume capability
- Add client-side validation before server submission
- Optimize database queries for faster responses
- Implement proper error handling and retry logic
- Add comprehensive logging for debugging

**Monitoring & Analytics:**
- Set up form analytics to track user behavior
- Monitor completion rates by section
- Track error rates and types
- Measure performance metrics continuously
- A/B test improvements with real users
```

**Risoluzione dei problemi relativi ai prompt:**

```
**Debug this form submission error:** Users report getting "500 Internal Server Error" when submitting. Check validation logic, server endpoints, and data formatting.
```

```
**Fix mobile layout issues:** Form fields are overlapping on iPhone screens and submit button is not visible. Ensure proper responsive design.
```

```
**Resolve validation conflicts:** Some users can't submit even with valid data. Review validation rules for conflicts and edge cases.
```

## Best practice specifiche per l’ambiente

### Interfaccia utente per la gestione dei moduli

**Quando utilizzarlo:** per attività di gestione e creazione di moduli di alto livello.

```
In Forms Management UI, create a new **customer survey template** that can be reused across different departments. Include standard branding, common field types, and configurable sections.
```

### Editor di moduli adattivi

**Quando utilizzarlo:** per la configurazione dettagliata del modulo e la creazione di regole complesse.

```
In the Adaptive Forms Editor, configure **advanced business rules** for this loan application: calculate debt-to-income ratio, determine eligibility, and show appropriate next steps.
```

### Editor universale

**Quando utilizzarlo:** per moduli di Edge Delivery Services con modifica visiva.

```
In Universal Editor, create a **responsive contact form** for the company website. Ensure it matches the site design and integrates with the existing content management workflow.
```

## Guida rapida alla guida ai comandi

| Comando | Miglior caso d’uso | Esempio |
|---------|---------------|---------|
| `/create-form` | Avvio di nuovi moduli | `/create-form employee onboarding with personal info and benefits selection` |
| `/add-form` | Aggiunta di moduli alle pagine | `/add-form newsletter signup with email and preferences` |
| `/update-layout` | Modifica della struttura del modulo | `/update-layout wizard with 4 steps: info, preferences, review, confirm` |
| `/update-field` | Modifica delle proprietà del campo | `/update-field @email to be mandatory with real-time validation` |
| `/create-rule` | Aggiunta di un comportamento dinamico | `/create-rule show @spouseInfo if @maritalStatus equals "Married"` |
| `/create-panel` | Organizzazione delle sezioni del modulo | `/create-panel Employment Details with job title, company, salary fields` |
| `/add-panel` | Conversione delle progettazioni | `/add-panel from uploaded form image with field recognition` |
| `/configure-submit` | Impostazione della gestione dei dati | `/configure-submit to CRM and send confirmation email` |
| `/help` | Ottenere assistenza | `/help how to implement multi-step validation?` |

## Riferimento alle proprietà del componente supportato

### Proprietà universali (tutti i componenti)

- **Tipo**: tipo di componente (testo, e-mail, numero, telefono, data, casella di controllo, radio, menu a discesa, file, ecc.)
- **Nome**: identificatore del campo per l’invio del modulo
- **Etichetta**: visualizza il testo per il campo
- **Descrizione**: testo di istruzioni per il campo
- **Visibile**: booleano per la visibilità iniziale
- **Obbligatorio**: booleano per i campi obbligatori

### Proprietà del campo di input

- **Valore**: valore predefinito/iniziale
- **Segnaposto**: testo di suggerimento per i campi di input
- **Min**: valore minimo (per numeri/date)
- **Max**: valore massimo (per numeri/date)

### Proprietà di caricamento del file

- **Accetta**: tipi di file (.pdf, .doc, .docx, .jpg, .png, ecc.)
- **Multipli**: booleano per la selezione di più file

### Proprietà di controllo della selezione

- **Opzioni**: scelte per i menu a discesa (elenco separato da virgole)
- **Selezionato**: selezione predefinita per caselle di controllo/radio

### Proprietà del contenitore

- **Set di campi**: raggruppamento di campi correlati
- **Ripetibile**: booleano per sezioni ripetibili

### Proprietà avanzate

- **Espressione visibile**: formula per la visibilità condizionale (=formula)
- **Espressione valore**: formula per valori calcolati (=formula)

## Riepilogo delle best practice

### Linee guida tecniche

- **Utilizza solo le proprietà supportate** dalla specifica ufficiale del componente AEM Forms
- **Segui la sintassi corretta** per i riferimenti al campo (@fieldName e le espressioni (=formula)
- **Esegui il test in modo incrementale** dopo ogni modifica per rilevare i problemi in anticipo
- **Pianifica l’accessibilità** fin dall’inizio e non in un secondo momento
- **Considera gli utenti dei dispositivi mobili** in ogni decisione relativa alla progettazione
- **Documenta regole complesse** per la manutenzione futura e la collaborazione tra team

### Approccio strategico

- **Inizia con le esigenze dell’utente** - Concentrati su ciò che gli utenti devono eseguire, non solo sulle funzioni tecniche
- **Progettazione per il completamento**: riduci al minimo l’attrito e il carico cognitivo nella progettazione del modulo
- **Pianifica il flusso di dati** in anticipo: valuta come verranno elaborati, memorizzati e utilizzati i dati
- **Creazione per scala**: progetta moduli in grado di gestire la crescita prevista del volume degli utenti e dei dati
- **Implementa un miglioramento progressivo**: assicurati che le funzionalità di base funzionino, quindi aggiungi le funzioni avanzate

### Insidie comuni da evitare

- **Richieste iniziali eccessivamente complesse**: suddividi le attività di grandi dimensioni in passaggi più piccoli e gestibili
- **Utilizzo di proprietà non supportate** non incluse nelle specifiche AEM Forms
- **Ignorare l’esperienza dei dispositivi mobili** fino alla fine del processo di sviluppo
- **Saltare i test con gli utenti** in scenari reali e casi limite
- **Presumere che l’IA comprenda il contesto** senza fornire istruzioni chiare e specifiche
- **Dimenticare i requisiti di accessibilità** e conformità
- **Non convalidare le modifiche** prima di passare alla fase successiva

### Approccio garanzia di qualità

1. **Anteprima frequente**: controlla il tuo lavoro in modalità di anteprima dopo ogni modifica significativa
2. **Test dei casi limite**: prova input insoliti, testo lungo, caratteri speciali
3. **Convalida su più dispositivi**: testa su dispositivi mobili, tablet e desktop
4. **Verifica accessibilità**: verifica la navigazione tramite tastiera e la compatibilità di lettura dello schermo
5. **Test delle prestazioni**: assicurati che i moduli vengano caricati rapidamente e che rispondano senza problemi
6. **Test di accettazione utente**: fai testare il modulo da utenti reali prima della distribuzione


*Questa libreria di prompt viene continuamente aggiornata in base al feedback degli utenti e alle nuove funzionalità dell’Assistente IA. Per le funzionalità e gli esempi più recenti, controlla la [documentazione di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=it).*
