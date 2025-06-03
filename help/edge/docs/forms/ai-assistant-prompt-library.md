---
title: Assistente AI di AEM Forms - Libreria di richieste
description: Raccolta di modelli ed esempi comprovati per la creazione di moduli con assistenza AI nell’interfaccia utente di gestione di Forms, nell’editor di Forms adattivo e nell’editor universale.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: d3ade6ee9216b44b55d6808d8acffe83f1e263c9
workflow-type: tm+mt
source-wordcount: '1613'
ht-degree: 0%

---



# Assistente AI di AEM Forms - Libreria di richieste

Raccolta di modelli di prompt riutilizzabili ed esempi per scenari comuni di creazione di moduli. Considera questi modelli come modelli che puoi adattare alle tue esigenze specifiche. Ogni sezione tratta un caso d’uso particolare con istruzioni su quando utilizzarlo e esempi comprovati.

>[!NOTE]
>
> L’Assistente all’intelligenza artificiale per AEM Forms è disponibile nell’ambito del programma per l’adozione anticipata. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a mailto:aem-forms-ea@adobe.com.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifica**: questa libreria di prompt è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. I prompt, gli esempi e le best practice possono cambiare man mano che l’Assistente IA per AEM Forms continua a evolvere durante il programma di adozione anticipata.

## Best practice per risultati ottimali

Per ottenere il massimo dall’Assistente AI, tieni presenti i seguenti suggerimenti:

### Avvio semplice, creazione incrementale

Inizia con comandi specifici più piccoli (ad esempio, &quot;Aggiungi un input di testo per &#39;Nome&#39;&quot;) invece di richieste complesse in più passaggi inizialmente. Questo approccio garantisce precisione e semplifica la risoluzione dei problemi se qualcosa non funziona come previsto.

**Esempio di avvio semplice:**

```
Add a text input field for "First Name" with placeholder "Enter your first name"
```

**Quindi Generare In Modo Incrementale:**

```
Make @firstName mandatory and add validation message "First name is mandatory"
```

### Utilizzare la terminologia di AEM Forms

Utilizza termini come &quot;pannello&quot;, &quot;campo di immissione testo&quot;, &quot;gruppo di caselle di controllo&quot;, &quot;azione di invio&quot;, &quot;regola&quot; ecc. per una migliore comprensione da parte dell’assistente. In questo modo l’intelligenza artificiale interpreta correttamente le richieste nel contesto di AEM Forms.

**Termini preferiti:**

- &quot;campo di immissione testo&quot; invece di &quot;casella di testo&quot;
- &quot;gruppo di caselle di controllo&quot; invece di &quot;caselle di controllo&quot;
- &quot;menu a discesa&quot; invece di &quot;seleziona elenco&quot;
- &quot;pannello&quot; invece di &quot;sezione&quot; o &quot;contenitore&quot;
- &quot;invia azione&quot; invece di &quot;invio modulo&quot;
- &quot;rule&quot; invece di &quot;logic&quot; o &quot;condition&quot;

### Campi di riferimento chiari

Durante la configurazione dei campi esistenti, utilizza la notazione @fieldName (ad esempio, &quot;Rendi @firstName obbligatorio&quot;). Questo aiuta l’intelligenza artificiale a identificare esattamente a quale campo stai facendo riferimento, soprattutto nelle forme complesse con molti campi.

**Esempi:**

- `Make @email mandatory with real-time validation`
- `Show @spouseInfo panel when @maritalStatus equals "Married"`
- `Set @country default value to "United States"`

### Rivedi sempre i piani

Prima di fare clic su Applica, esaminare sempre attentamente i piani per le modifiche proposte dall&#39;assistente nell&#39;Editor universale. L’intelligenza artificiale ti mostrerà cosa intende fare; impiega un attimo a verificare che corrisponda alle tue aspettative.

### Convalida manuale

Dopo che l&#39;assistente apporta le modifiche, visualizzare sempre in anteprima e verificare il funzionamento e l&#39;aspetto del modulo. L’intelligenza artificiale è uno strumento potente, ma la convalida finale è fondamentale per garantire la qualità.

**Elenco di controllo convalida:**

- Verifica della funzionalità del modulo in modalità anteprima
- Verificare che la logica condizionale funzioni correttamente
- Verifica la reattività mobile
- Invio modulo di prova
- Convalidare le funzioni di accessibilità

### Iterare e perfezionare

Se il primo prompt non restituisce il risultato esatto, prova a riformulare o suddividere la richiesta in passaggi più piccoli. L’intelligenza artificiale apprende dal contesto, quindi fornire dettagli più specifici spesso migliora i risultati.

**Esempio iterazione:**

1. Primo tentativo: &quot;Rendi il modulo compatibile con i dispositivi mobili&quot;
2. Perfezionato: &quot;Ottimizza il layout del modulo per schermi mobili sotto i 768 px con layout a colonna singola e target touch più grandi&quot;

### Invia feedback

Utilizza il meccanismo di feedback integrato per aiutare l’assistente ad apprendere e migliorare. Il tuo feedback aiuta a migliorare l’intelligenza artificiale per tutti.


## Esempi di sviluppo incrementale

Questi esempi mostrano come creare moduli passo dopo passo, partendo da semplici e aggiungendo gradualmente complessità:

### Esempio 1: creazione incrementale di un modulo contatto

**Passaggio 1 - Inizio semplice:**

```
Create a basic contact form with name, email, and message fields
```

**Passaggio 2 - Aggiungi convalida:**

```
Make @name and @email mandatory fields with appropriate validation
```

**Passaggio 3 - Migliorare l&#39;esperienza utente:**

```
Add placeholder text: @name "Your full name", @email "your.email@company.com", @message "Tell us how we can help"
```

**Passaggio 4 - Aggiunta di funzionalità avanzate:**

```
Add a dropdown @inquiryType with options: "General Question", "Support Request", "Sales Inquiry", "Partnership"
```

**Passaggio 5 - Implementazione logica condizionale:**

```
Show @urgencyLevel dropdown (Low, Medium, High) only when @inquiryType equals "Support Request"
```

### Esempio 2: creazione di un modulo di registrazione in modo incrementale

**Passaggio 1 - Struttura di base:**

```
Create a user registration form with personal information panel
```

**Passaggio 2 - Aggiungi campi di base:**

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

**Passaggio 5 - Miglioramento della sicurezza:**

```
Add password confirmation field @confirmPassword with validation to match @password
```

**Passaggio 6 - Aggiungi preferenze:**

```
Create "Preferences" panel with @newsletter checkbox and @communicationMethod radio group (Email, SMS, Phone)
```

Questo approccio incrementale consente di:

- Rileva i problemi prima che si verifichino
- Testare accuratamente ogni funzione
- Effettua regolazioni in base al feedback degli utenti
- Mantenere un maggiore controllo sul processo di sviluppo

## Avvio di un nuovo Forms

**Quando utilizzare:** All&#39;inizio di qualsiasi progetto modulo. Questo prompt consente all’intelligenza artificiale di comprendere le tue esigenze e creare la struttura di base.

**Come utilizzare:** Inizia con la struttura di base e i requisiti di base. Specifica il tipo di modulo, il pubblico di destinazione e lo scopo principale. Aggiungete complessità ai prompt successivi.

**Esempio di prompt - Avvio semplice:**

```
Create a **customer onboarding form** for new bank account applications with:

**Purpose:** Collect personal information for account setup
**Target Users:** New customers applying for checking/savings accounts
**Basic Structure:** Single panel with essential fields
**Core Fields:** Name, email, phone, account type selection

Start with a simple layout that we can enhance step by step.
```

**Quindi Generare In Modo Incrementale:**

```
Add an address panel to @customerOnboardingForm with street address, city, state, and zip code fields
```

```
Add employment information panel with @employer, @jobTitle, and @annualIncome fields
```

```
Add file upload field @identityDocuments for identity verification (Accept: .pdf,.jpg,.png)
```

**Richieste di avvio semplici alternative:**

```
Create a basic **event registration form** with name, email, and event selection fields
```

```
Build a simple **contact form** with name, email, and message fields
```

```
Design a basic **feedback survey** with rating scale and comments field
```

## Struttura e layout modulo

**Quando utilizzare:** quando è necessario organizzare moduli complessi o migliorare l&#39;esperienza utente tramite una migliore progettazione del layout.

**Come utilizzare:** Concentrarsi sul percorso di utenti e sul raggruppamento logico delle informazioni. Specifica le preferenze di layout e i pattern di navigazione.

**Esempio di richiesta - Struttura di modulo con più passaggi:**

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

**Prompt di ottimizzazione layout:**

```
Reorganize this form using a **wizard layout** for desktop and single column for mobile. 
```

```
Convert this long form into an **accordion layout** where users can expand/collapse sections.
```

```
Create a **vertical tabbed interface** for this form with tabs for: Basic Info, Contact Details, Preferences, and Review.
```

## Gestione e convalida dei campi

**Quando utilizzare:** Quando è necessario aggiungere, modificare o migliorare i campi modulo con regole e comportamenti di convalida specifici.

**Come utilizzare:** Specifica i tipi di campo, i requisiti di convalida e le aspettative di esperienza utente. Fai riferimento ai campi esistenti utilizzando la sintassi @fieldName.

**Esempio di richiesta - Miglioramento del campo:**

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

**Prompt Specifici Del Campo:**

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

**Quando utilizzare:** Quando è necessario un comportamento di modulo dinamico basato su input utente o regole business.

**Come utilizzare:** Definisci chiaramente le condizioni e le azioni risultanti. Utilizza riferimenti di campo specifici e operatori logici.

**Esempio di richiesta - Logica condizionale complessa:**

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

**Prompt Specifici Della Regola:**

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

**Quando utilizzare:** Quando è necessario connettere i moduli a sistemi back-end, database o servizi esterni.

**Come utilizzare:** Inizia con la configurazione di base dell&#39;invio, quindi aggiungi ulteriori integrazioni in modo incrementale. Specifica il tipo di integrazione, i requisiti del formato dati e le preferenze di gestione degli errori.

**Prompt di esempio - Inizia con invio di base:**

```
Configure basic form submission for @applicationForm:

**Primary Submission:**
- Send form data to REST endpoint: `/api/v1/applications`
- Format data as JSON
- Show success message: "Application submitted successfully"
- Show error message if submission fails: "Submission failed, please try again"
```

**Aggiungi Azioni Secondarie In Modo Incrementale:**

```
Add email notification to @applicationForm: Send confirmation email to @email address with application reference number
```

```
Add CRM integration to @applicationForm: Create new lead record with @firstName, @lastName, @email, and set Status to "New Application"
```

**Esempio di richiesta - Invio multicanale avanzato:**

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

**Prompt Specifici Dell&#39;Integrazione:**

```
Connect this form to **CRM system** to create new leads. Map @firstName to FirstName, @email to Email, set LeadSource to "Web Form", and Status to "New".
```

```
Set up **workflow trigger** when form is submitted. Pass all form data and trigger approval workflow with manager notification.
```

```
Configure **database integration** to save form submissions as records. Create new folder for each submission with uploaded documents.
```

## Importazione progettazione e conversione

**Quando utilizzare:** Se sono presenti progettazioni di moduli esistenti (PDF, Figma, immagini) che devono essere convertite in moduli AEM funzionali.

**Come utilizzare:** Fornire un contesto chiaro sulla progettazione di origine e specificare eventuali modifiche o miglioramenti necessari.

**Esempio di richiesta - Conversione PDF Form:**

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

**Richieste di importazione progettazione:**

```
Import this **design mockup** and convert it into an adaptive form. Maintain the exact visual design but add proper validation and mobile responsiveness.
```

```
Analyze this **image of a paper form** and recreate it digitally. Improve the layout for better mobile experience while keeping all mandatory fields.
```

```
Convert this **existing HTML form** to AEM adaptive form format. Preserve all functionality but add AEM-specific features like rules and themes.
```

## Ottimizzazione mobile e reattività

**Quando utilizzare:** Quando i moduli devono funzionare senza problemi su tutti i tipi di dispositivi e le dimensioni dello schermo.

**Come utilizzare:** Inizia con l&#39;ottimizzazione mobile di base, quindi migliora con le funzionalità avanzate. Enfatizza l’approccio mobile-first e specifica i comportamenti dei punti di interruzione in modo incrementale.

**Esempio di richiesta - Inizia con ottimizzazione mobile di base:**

```
Make @contactForm mobile-friendly with:

**Basic Mobile Layout:**
- Single column layout for all form sections
- Larger touch targets for buttons and inputs
- Responsive design that works on phones and tablets
```

**Aggiungi funzionalità mobili avanzate:**

```
Enhance @contactForm mobile experience with:
- Sticky submit button at bottom of screen
- Touch-friendly date pickers
- Swipe gestures for multi-step navigation
```

**Esempio di richiesta - Ottimizzazione completa di Mobile-First:**

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

**Richieste semplici specifiche per dispositivi mobili:**

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

**Quando utilizzare:** Quando i moduli devono soddisfare gli standard di accessibilità (WCAG 2.1 AA) o i requisiti di conformità.

**Come utilizzare:** Specificare i requisiti di accessibilità e gli standard di conformità che devono essere soddisfatti.

**Esempio di richiesta - Implementazione accessibilità:**

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

**Richieste specifiche di conformità:**

```
Ensure this **healthcare form meets HIPAA requirements** with proper data encryption, audit logging, and privacy controls.
```

```
Make this **financial form PCI DSS compliant** with secure payment field handling and data protection measures.
```

```
Create a **government form meeting Section 508 standards** with full accessibility and plain language requirements.
```

## Test e qualità Assurance

**Quando utilizzare:** Quando è necessario convalidare la funzionalità del modulo, l&#39;esperienza utente e le prestazioni tecniche.

**Come utilizzare:** Specificare scenari di test, casi limite e criteri di qualità da verificare.

**Esempio di richiesta - Test modulo completo:**

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

**Prompt Specifici Per Il Test:**

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

**Quando utilizzare:** Quando sono necessarie funzionalità di moduli sofisticati come l&#39;assistenza AI, flussi di lavoro avanzati o integrazioni complesse.

**Come utilizzare:** Definisci chiaramente le funzionalità avanzate e i requisiti di integrazione.

**Esempio di richiesta - Modulo avanzato dall&#39;intelligenza artificiale:**

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

**Quando utilizzare:** Quando i moduli presentano problemi di prestazioni, di esperienza utente o tecnici.

**Come utilizzare:** Descrivere chiaramente il problema specifico e il risultato desiderato.

**Esempio di prompt - Ottimizzazione delle prestazioni:**

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

**Prompt per la risoluzione dei problemi:**

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

### Interfaccia utente di gestione Forms

**Quando utilizzare:** per attività di gestione e creazione di moduli di alto livello.

```
In Forms Management UI, create a new **customer survey template** that can be reused across different departments. Include standard branding, common field types, and configurable sections.
```

### Editor Forms adattivo

**Quando utilizzare:** Per la configurazione dettagliata del modulo e la creazione di regole complesse.

```
In the Adaptive Forms Editor, configure **advanced business rules** for this loan application: calculate debt-to-income ratio, determine eligibility, and show appropriate next steps.
```

### Editor universale

**Quando utilizzare:** Per Edge Delivery Services Form con modifica visiva.

```
In Universal Editor, create a **responsive contact form** for the company website. Ensure it matches the site design and integrates with the existing content management workflow.
```

## Guida rapida alla guida di riferimento dei comandi

| Comando | Caso d’uso migliore | Esempio |
|---------|---------------|---------|
| `/create-form` | Avvio di nuovi moduli | `/create-form employee onboarding with personal info and benefits selection` |
| `/add-form` | Aggiunta di moduli alle pagine | `/add-form newsletter signup with email and preferences` |
| `/update-layout` | Modifica della struttura del modulo | `/update-layout wizard with 4 steps: info, preferences, review, confirm` |
| `/update-field` | Modifica delle proprietà dei campi | `/update-field @email to be mandatory with real-time validation` |
| `/create-rule` | Aggiunta di un comportamento dinamico | `/create-rule show @spouseInfo if @maritalStatus equals "Married"` |
| `/create-panel` | Organizzazione delle sezioni del modulo | `/create-panel Employment Details with job title, company, salary fields` |
| `/add-panel` | Conversione di progetti | `/add-panel from uploaded form image with field recognition` |
| `/configure-submit` | Impostazione della gestione dei dati | `/configure-submit to CRM and send confirmation email` |
| `/help` | Ottenere assistenza | `/help how to implement multi-step validation?` |

## Riferimento alle proprietà dei componenti supportati

### Proprietà universali (tutti i componenti)

- **Tipo**: tipo di componente (testo, e-mail, numero, telefono, data, casella di controllo, radio, elenco a discesa, file, ecc.)
- **Nome**: identificatore del campo per l&#39;invio del modulo
- **Etichetta**: visualizza il testo per il campo
- **Descrizione**: testo della Guida per il campo
- **Visibile**: booleano per la visibilità iniziale
- **Obbligatorio**: booleano per i campi obbligatori

### Proprietà campo di input

- **Valore**: valore predefinito/iniziale
- **Segnaposto**: testo suggerimento per i campi di input
- **Min**: valore minimo (per numeri/date)
- **Max**: valore massimo (per numeri/date)

### Proprietà caricamento file

- **Accetta**: tipi di file (.pdf, .doc, .docx, .jpg, .png, ecc.)
- **Multipli**: booleano per la selezione di più file

### Proprietà controllo selezione

- **Opzioni**: scelte per i menu a discesa (elenco separato da virgole)
- **Selezionato**: selezione predefinita per caselle di controllo/radio

### Proprietà contenitore

- **Set di campi**: raggruppamento campi correlati
- **Ripetibile**: booleano per sezioni ripetibili

### Proprietà avanzate

- **Espressione visibile**: formula per la visibilità condizionale (=formula)
- **Espressione valore**: formula per valori calcolati (=formula)

## Riepilogo delle best practice

### Linee guida tecniche

- **Utilizza solo le proprietà supportate** dalla specifica ufficiale del componente AEM Forms
- **Seguire la sintassi corretta** per i riferimenti di campo (@fieldName) e le espressioni (=formula)
- **Esegui il test in modo incrementale** dopo ogni modifica per rilevare i problemi in anticipo
- **Pianifica l&#39;accessibilità** fin dall&#39;inizio, non come ulteriore considerazione
- **Considera gli utenti mobili** in ogni decisione di progettazione
- **Documenta regole complesse** per manutenzione futura e collaborazione tra team

### Approccio strategico

- **Inizia con le esigenze dell&#39;utente** - Concentrati su ciò che gli utenti devono eseguire, non solo sulle caratteristiche tecniche
- **Progettazione per il completamento** - Riduci al minimo l&#39;attrito e il carico cognitivo nella progettazione del modulo
- **Pianifica il flusso di dati** in anticipo. Valuta come verranno elaborati, memorizzati e utilizzati i dati
- **Generazione per la scala** - Progetta moduli in grado di gestire la crescita prevista del volume utente e dei dati
- **Implementa miglioramento progressivo** - Assicurati che le funzionalità di base funzionino, quindi aggiungi funzionalità avanzate

### Insidie comuni da evitare

- **Richieste iniziali eccessivamente complesse** - Suddividi le attività di grandi dimensioni in passaggi più piccoli e gestibili
- **Utilizzo di proprietà non supportate** non incluse nelle specifiche AEM Forms
- **Esperienza mobile ignorata** fino alla fine del processo di sviluppo
- **I test utente** verranno ignorati con scenari reali e casi limite
- **Presupponendo che AI comprenda il contesto** senza fornire istruzioni chiare e specifiche
- **Dimenticanza dei requisiti di accessibilità** e conformità
- **Impossibile convalidare le modifiche** prima di passare al passaggio successivo

### Approccio Assurance di qualità

1. **Anteprima frequente** - Controlla il tuo lavoro in modalità anteprima dopo ogni modifica significativa
2. **Test dei casi limite** - Prova input insoliti, testo lungo, caratteri speciali
3. **Convalida su più dispositivi** - Test su dispositivi mobili, tablet e desktop
4. **Verifica accessibilità** - Verifica della compatibilità della navigazione da tastiera e dell&#39;utilità di lettura dello schermo
5. **Test delle prestazioni** - Assicurarsi che i moduli vengano caricati rapidamente e che rispondano senza problemi
6. **Test di accettazione utente** - Chiedi a utenti reali di testare il modulo prima della distribuzione


*Questa libreria di prompt viene continuamente aggiornata in base al feedback degli utenti e alle nuove funzionalità dell&#39;Assistente di intelligenza artificiale. Per le funzionalità e gli esempi più recenti, consulta la [documentazione di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=it).*
