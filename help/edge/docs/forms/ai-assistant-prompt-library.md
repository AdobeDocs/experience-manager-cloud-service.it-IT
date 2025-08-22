---
title: Forms Experience Builder - Libreria di richieste
description: Raccolta di pattern di prompt ed esempi dimostrati per la creazione di moduli con assistenza IA nell’interfaccia utente per la gestione dei moduli, nell’editor dei moduli adattivi e nell’editor universale.
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: c8f64082-a23f-4919-ad66-042faad77d31
source-git-commit: 9996bc602ae6169dd1aade622d5dbc5b1addeb54
workflow-type: tm+mt
source-wordcount: '1338'
ht-degree: 28%

---


# Forms Experience Builder - Libreria di richieste

Raccolta di modelli ed esempi di prompt riutilizzabili ottimizzati per Forms Experience Builder. Questa libreria semplificata si concentra sui due metodi di creazione di base: Crea da zero e Importa e converti, con supporto migliorato per campi avanzati basati su LLM e coerenza del brand.

>[!NOTE]
>
> Forms Experience Builder è disponibile nell&#39;ambito del programma per gli utenti meno esperti. Invia un&#39;e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com` per richiedere l&#39;accesso.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa libreria di prompt è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. I prompt, gli esempi e le best practice possono cambiare man mano che Forms Experience Builder continua a evolversi durante il programma per i primi utenti.

## Utilizzo di questa libreria di richieste

Questa libreria fornisce modelli di prompt riutilizzabili per scenari comuni di creazione di moduli. Per informazioni complete sulle best practice, consulta la [Guida introduttiva di Forms Experience Builder](forms-ai-assistant-getting-started.md#best-practices).

### Suggerimenti rapidi per questa libreria

- **Inizia con esempi**: utilizza i prompt forniti come modelli e adattali alle tue esigenze
- **Due metodi di creazione** - Scegliere Crea da zero o Importa e converti.
- **Specifici** - Aggiungi i tuoi dettagli agli esempi generici
- **Verifica approfondita** - Convalida sempre i risultati nel tuo ambiente specifico

### Modelli e stili del marchio

**Prepara in anticipo le risorse del brand per la creazione di moduli coerenti:**

- **Modelli marchio** - Crea modelli di modulo standardizzati con i colori, i font e i pattern di layout della tua organizzazione
- **Linee guida per gli stili** - Definizione di stili di campo coerenti, progettazioni di pulsanti e standard di spaziatura
- **Libreria componenti** - Crea componenti modulo riutilizzabili che corrispondono alla tua brand identity
- **Visual Assets** - Prepara logo, icone ed elementi di sfondo per l&#39;integrazione dei moduli

**Esempio di richiesta del modello di marchio:**

```
Create a brand template for financial services forms with:
- Corporate blue (#003366) and silver (#C0C0C0) color scheme
- Open Sans font family for all text
- 16px minimum font size for accessibility
- Consistent 24px spacing between sections
- Corporate logo in header with proper sizing
- Professional button styling with hover effects
```

>[!NOTE]
>
>**Componenti personalizzati**: prima di implementare elementi del marchio personalizzati, rivolgiti al tuo team di sviluppo per informazioni sull&#39;utilizzo di componenti specifici dell&#39;organizzazione e sulla loro compatibilità con Forms Experience Builder.

>[!NOTE]
>
> Questa libreria di prompt è stata aggiornata per riflettere le funzionalità semplificate di Forms Experience Builder. Alcune funzionalità di integrazione e test avanzate mostrate negli esempi potrebbero richiedere una configurazione aggiuntiva.



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

**Passaggio 2 - Aggiungi campi obbligatori:**

```
Add fields for @firstName, @lastName, @email, @phoneNumber with appropriate validation
```

**Passaggio 3 - Aggiungi logica di business:**

```
Create a rule: if @age is under 18, show parent/guardian information section
```

**Passaggio 4 - Migliora con preferenze:**

```
Add a preferences panel with @newsletterSubscription, @marketingConsent, @termsAccepted
```

**Passaggio 5 - Aggiungi caricamento file:**

```
Include a file upload field for @profilePicture with size limit of 5MB
```

## Creazione e gestione moduli

**Quando utilizzare:** Quando è necessario creare nuovi moduli o modificare quelli esistenti.

**Come utilizzare:** Scegliere uno dei due approcci seguenti: Crea da zero o Importa e converti (vedere [Guida introduttiva](forms-ai-assistant-getting-started.md#two-ways-to-create-forms)).

**Esempio di richiesta - Creazione modulo semplice:**

```
Create a customer feedback form with:
- Product rating (1-5 stars)
- Comment field for detailed feedback
- Customer email (optional)
- Submit to email notification
```

**Esempio di richiesta - Creazione modulo complessa:**

```
Create a comprehensive employee onboarding form with:

**Personal Information Section:**
- Full name (first, middle, last)
- Date of birth with age validation
- Contact information (email, phone, address)
- Emergency contact details

**Employment Details:**
- Position and department selection
- Start date with business day validation
- Salary information with confidentiality notice
- Reporting structure

**Document Upload:**
- Resume/CV upload (PDF, DOC, DOCX)
- ID verification documents
- Tax forms and banking information
- Signed employment agreement

**Preferences:**
- Benefits selection with cost calculator
- Work schedule preferences
- Training requirements
- Equipment needs

**Validation Rules:**
- Email format validation
- Phone number format validation
- Age must be 18 or older
- All required documents must be uploaded
- Terms and conditions must be accepted

**Submit Actions:**
- Send confirmation email to new employee
- Notify HR department
- Create employee record in HR system
- Schedule orientation meeting
```

**Prompt gestione moduli:**

```
Import this PDF application form and convert it to an adaptive form with enhanced validation
```

```
Update the existing contact form to include social media handles and preferred contact method
```

```
Reorganize the registration form into a 3-step wizard: personal info, preferences, confirmation
```

## Gestione e configurazione del campo

**Quando utilizzare:** Quando è necessario aggiungere, modificare o configurare campi modulo.

**Come utilizzare:** Specifica i tipi di campo, le regole di convalida e i requisiti di esperienza utente.

**Esempio di richiesta - Aggiunta di un campo di base:**

```
Add a text input field for "Company Name" with placeholder "Enter your company name"
```

**Esempio di richiesta - Configurazione avanzata del campo:**

```
Add a comprehensive address section with:

**Street Address:**
- Address line 1 (required, max 100 characters)
- Address line 2 (optional, max 100 characters)
- City (required, dropdown with common cities)
- State/Province (required, dropdown)
- Postal code (required, format validation)
- Country (required, default to "United States")

**Validation Rules:**
- Postal code must match state selection
- Address line 1 cannot be empty
- City must be a valid city for selected state

**User Experience:**
- Auto-complete for address fields
- Clear labels and help text
- Mobile-friendly input fields
- Accessibility compliance
```

**Richieste configurazione campo:**

```
Make @email field required with real-time validation and custom error message
```

```
Add a dropdown for @country with options for USA, Canada, UK, Germany, France, and "Other"
```

```
Configure @phoneNumber field with format (XXX) XXX-XXXX and validation
```

```
Add a file upload field for @resume with PDF and DOC restrictions, max 5MB
```

## Campi avanzati migliorati LLM

**Quando utilizzare:** Quando sono necessari campi con opzioni precompilate che sfruttano la knowledge base dell&#39;intelligenza artificiale.

**Come utilizzare:** Campi di richiesta che richiedono set di dati completi - L&#39;intelligenza artificiale può compilare automaticamente le opzioni utilizzando la conoscenza incorporata.

### Campi geografici e di ubicazione

**Aeroporti e trasporti:**

```
Add a dropdown for departure airports with all major international airports
Add arrival airport field with IATA codes and full names
Create a field for nearest airport to user location
Add a selection of train stations for European cities
```

**Aree amministrative:**

```
Add a complete list of US states with abbreviations
Create a country dropdown with ISO codes and full names
Add a field for major world cities with time zones
Include a dropdown of Canadian provinces and territories
Add a field for UK counties and postal areas
```

### Dati aziendali e di settore

**Classificazioni società:**

```
Add a field for industry classification with NAICS codes
Create a dropdown of business entity types (LLC, Corporation, Partnership, etc.)
Add a field for company size categories (startup, SME, enterprise)
Include department selection for large organizations
Add a field for professional service types
```

**Classificazioni professionali:**

```
Add a field for job titles with common industry roles
Create a dropdown of professional certifications by field
Include education levels with degree types
Add a field for years of experience ranges
Create a selection for programming languages and frameworks
```

### Norme e normative

**Finanziario e legale:**

```
Add a field for currency codes with symbols and exchange rates
Create a dropdown of tax ID types by country
Include a field for legal document types
Add payment method options with security features
Create a selection for banking institutions by country
```

**Standard tecnici:**

```
Add a dropdown of file format types with extensions
Include network protocol options
Add a field for database types and versions
Create a selection for API authentication methods
```

### Settore sanitario e medicale

**Classificazioni mediche:**

```
Add a field for medical specialties
Create a dropdown of common medications with generic names
Include a field for insurance provider types
Add a selection for medical emergency contact relationships
Create a field for dietary restrictions and allergies
```

### Informazioni su ora e calendario

**Campi data e ora:**

```
Add a field for business hours with time zone handling
Create a dropdown of public holidays by country
Include seasonal options with date ranges
Add a field for conference room booking with availability
Create a selection for recurring meeting patterns
```

### Categorie di prodotti e servizi

**Classificazioni e-commerce:**

```
Add a field for product categories with subcategories
Create a dropdown of shipping methods with delivery estimates
Include a field for return policy options
Add a selection for customer priority levels
Create a field for subscription billing cycles
```

**Esempio di prompt per campi avanzati:**

```
"Add a departure airport field with all major airports worldwide including IATA codes and city names"
```

```
"Create a comprehensive industry field using standard NAICS classification with technology subcategories"
```

```
"Include a professional certification dropdown that adapts based on the selected job field"
```

```
"Add an international phone number field that formats based on the selected country"
```

```
"Create a university selection field with major institutions organized by country and ranking"
```

## Creazione di regole e logica di business

**Quando utilizzare:** Quando è necessario implementare logica condizionale, regole di convalida o processi aziendali.

**Come utilizzare:** Descrivere chiaramente la logica di business, specificando condizioni e azioni.

**Esempio di richiesta - Logica condizionale semplice:**

```
Create a rule that shows @spouseInformation panel only when @maritalStatus equals "Married"
```

**Esempio di richiesta - Regole aziendali complesse:**

```
Implement comprehensive loan application validation:

**Income Validation:**
- If @annualIncome is less than 30000:
  - Show warning message: "Income may be insufficient for requested loan amount"
  - Require additional income documentation
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
Create a **visibility rule** that shows @spouseInformation panel only when @maritalStatus equals "Married" or "Domestic Partnership"
```

```
Add **progressive disclosure** where additional questions appear based on previous answers. Start with basic info, then show relevant follow-ups
```

```
Implement **smart defaults** where @country selection auto-sets related fields. Allow manual override
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

**Esempio di richiesta - Invio multicanale standard:**

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
Connect this form to **CRM system** to create new leads. Map @firstName to FirstName, @email to Email, set LeadSource to "Web Form", and Status to "New"
```

```
Set up **workflow trigger** when form is submitted. Pass all form data and trigger approval workflow with manager notification
```

```
Configure **database integration** to save form submissions as records. Create new folder for each submission with uploaded documents
```

## Importa e converti Forms esistente

**Quando utilizzare:** Quando si dispone di moduli, documenti o progettazioni esistenti da trasformare in moduli AEM moderni.

**Come utilizzare:** Caricare il file di origine e descrivere i requisiti di conversione (vedere [Guida all&#39;importazione](forms-ai-assistant-getting-started.md#2-import-and-convert)).

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

Preserve all original field labels and help text, but improve the user experience with modern form interactions
```

**Prompt di importazione della progettazione:**

```
Import this **design mockup** and convert it into an adaptive form. Maintain the exact visual design but add proper validation and mobile responsiveness
```

```
Analyze this **image of a paper form** and recreate it digitally. Improve the layout for better mobile experience while keeping all mandatory fields
```

```
Convert this **existing HTML form** to AEM adaptive form format. Preserve all functionality but add AEM-specific features like rules and themes
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
```

**Richieste specifiche per dispositivi mobili:**

```
Make this form **touch-friendly** with larger buttons and simplified navigation for mobile users
```

```
Optimize form for **tablet users** with appropriate field sizes and navigation patterns
```

```
Add **swipe gestures** for multi-step form navigation on mobile devices
```

## Accessibilità e conformità

**Quando utilizzare:** Quando i moduli devono soddisfare gli standard di accessibilità (WCAG) o i requisiti di conformità.

**Come utilizzare:** Specificare il livello di conformità richiesto ed eventuali caratteristiche di accessibilità specifiche necessarie.

**Esempio di richiesta - Accesso facilitato di base:**

```
Make @contactForm accessible with:

**Basic Accessibility:**
- Proper ARIA labels for all form fields
- Keyboard navigation support
- High contrast color scheme
- Screen reader compatibility
- Focus indicators for all interactive elements
```

**Esempio di richiesta - Accesso facilitato avanzato:**

```
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
```

**Prompt Specifici Per L&#39;Accessibilità:**

```
Add **screen reader support** to this form with proper ARIA labels and announcements
```

```
Implement **keyboard navigation** for all form interactions and navigation elements
```

```
Ensure **color contrast** meets WCAG AA standards for all text and interactive elements
```

## Ottimizzazione delle prestazioni

**Quando utilizzare:** Quando i moduli devono essere caricati rapidamente e funzionano correttamente in varie condizioni.

**Come utilizzare:** Specificare i requisiti delle prestazioni e le strategie di ottimizzazione.

**Esempio di richiesta - Prestazioni di base:**

```
Optimize @contactForm for performance:

**Loading Optimization:**
- Lazy load non-critical form sections
- Minimize initial bundle size
- Optimize images and assets
- Enable caching for static resources
```

**Esempio di richiesta - Prestazioni avanzate:**

```
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
```

**Prompt Specifici Delle Prestazioni:**

```
Optimize form **loading speed** by implementing progressive loading and asset optimization
```

```
Add **auto-save functionality** to prevent data loss during form completion
```

```
Implement **offline support** so users can complete forms without internet connection
```

## Test e garanzia di qualità

**Quando utilizzare:** Quando i moduli richiedono test completi per garantire affidabilità e soddisfazione degli utenti.

**Come utilizzare:** Specificare scenari di test, requisiti di convalida e metriche di qualità.

**Esempio di richiesta - Test di base:**

```
Add comprehensive testing for @contactForm:

**Functional Testing:**
- Test all form field validations
- Verify submit functionality works correctly
- Test error handling and user feedback
- Validate conditional logic and rules
```

**Esempio di richiesta - Test avanzati:**

```
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
```

**Prompt specifici per test:**

```
Add **automated testing** for all form validations and submit functionality
```

```
Implement **user acceptance testing** scenarios for complete form workflows
```

```
Set up **performance monitoring** to track form load times and user interactions
```

## Risoluzione di problemi

Soluzioni rapide per i problemi più comuni di Forms Experience Builder:

| Problema   | Correzione rapida |
|-------|-----------|
| Invio del modulo non eseguito | Verifica la configurazione e le regole di convalida dell’azione di invio |
| Errori di convalida non visualizzati | Verificare le impostazioni di convalida del campo e il posizionamento del messaggio di errore |
| Problemi di layout mobile | Verifica delle impostazioni di progettazione reattiva e del dimensionamento dei campi |
| Campi non visualizzati | Verificare la logica condizionale e le regole di visibilità |
| Errori di importazione | Verifica della compatibilità del formato del file e dei limiti di dimensione |
| Errori di integrazione | Convalida endpoint API e credenziali di autenticazione |
| Problemi relativi alle prestazioni | Ottimizza il conteggio dei campi e rimuovi le convalide non necessarie |
| Problemi di accessibilità | Etichette dei campi di revisione, attributi ARIA e ordine di tabulazione |

**Richiesta modalità debug:**

```
Enable debug mode to identify issues with form submission and field validation
```

**Prompt analisi errori:**

```
Analyze form errors: check validation rules, API responses, and user input patterns
```

## Analisi e approfondimenti avanzati

**Quando utilizzare:** Quando è necessario comprendere le prestazioni del modulo e il comportamento dell&#39;utente.

**Come utilizzare:** Specificare i requisiti di analisi e le informazioni necessarie.

**Esempio di richiesta - Analisi di base:**

```
Add analytics to @contactForm:

**Basic Metrics:**
- Form completion rates
- Field abandonment rates
- Submit success/failure rates
- User session duration
```

**Esempio di richiesta - Analisi avanzata:**

```
Implement comprehensive analytics for @applicationForm:

**User Behavior Analytics:**
- Track field completion rates and abandonment
- Monitor user session duration and patterns
- Analyze form navigation and user flow
- Identify bottlenecks and friction points

**Performance Analytics:**
- Measure form load times and performance
- Track API response times and failures
- Monitor validation rule effectiveness
- Analyze submission success rates

**Business Intelligence:**
- Generate reports on form effectiveness
- Track conversion rates and ROI
- Monitor user satisfaction and feedback
- Identify opportunities for optimization

**Predictive Analytics:**
- Predict form completion likelihood
- Identify users likely to abandon
- Recommend form improvements
- Optimize user experience based on data
```

**Richieste specifiche per Analytics:**

```
Add **conversion tracking** to measure form completion rates and user behavior
```

```
Implement **A/B testing** to compare different form designs and optimize performance
```

```
Create **analytics dashboard** to monitor form performance and user insights
```

## Sicurezza e protezione dei dati

**Quando utilizzare:** Quando i moduli gestiscono dati sensibili e richiedono misure di sicurezza.

**Come utilizzare:** Specificare i requisiti di sicurezza e le misure di protezione dei dati.

**Esempio di richiesta - Protezione di base:**

```
Add security measures to @contactForm:

**Basic Security:**
- HTTPS encryption for all data transmission
- Input validation and sanitization
- CSRF protection for form submissions
- Secure session management
```

**Esempio di richiesta - Protezione avanzata:**

```
Implement comprehensive security for @applicationForm:

**Data Protection:**
- End-to-end encryption for sensitive data
- PII data masking and anonymization
- Secure file upload with virus scanning
- Data retention and deletion policies

**Access Control:**
- Role-based access control for form data
- Multi-factor authentication for admin access
- Audit logging for all data access
- Secure API authentication and authorization

**Compliance:**
- GDPR compliance for data handling
- HIPAA compliance for health information
- PCI DSS compliance for payment data
- SOC 2 compliance for data security

**Monitoring:**
- Real-time security monitoring and alerts
- Intrusion detection and prevention
- Data breach notification systems
- Regular security audits and assessments
```

**Prompt Specifici Per La Sicurezza:**

```
Implement **data encryption** for sensitive form submissions and user information
```

```
Add **access control** to restrict form data access based on user roles and permissions
```

```
Set up **security monitoring** to detect and prevent unauthorized access to form data
```

## Riferimento comando

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
| `/configure-submit` | Impostazione della gestione dei dati | `/configure-submit to CRM and send confirmation email` |
| `/help` | Ottenere assistenza | `/help how to implement multi-step validation?` |

### Riferimenti campo

Utilizza la sintassi `@fieldName` per fare riferimento a campi esistenti nei prompt:

- `@email` - Campo e-mail di riferimento
- `@firstName` - Campo nome di riferimento
- `@maritalStatus` - Campo Stato civile di riferimento

### Tipi componente

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

**Proprietà campo di input:**

- **Valore**: valore predefinito/iniziale
- **Segnaposto**: testo di suggerimento per i campi di input
- **Min**: valore minimo (per numeri/date)
- **Max**: valore massimo (per numeri/date)

**Proprietà caricamento file:**

- **Accetta**: tipi di file (.pdf, .doc, .docx, .jpg, .png, ecc.)
- **Multipli**: booleano per la selezione di più file

**Proprietà controllo selezione:**

- **Opzioni**: scelte per i menu a discesa (elenco separato da virgole)
- **Selezionato**: selezione predefinita per caselle di controllo/radio

**Proprietà contenitore:**

- **Set di campi**: raggruppamento di campi correlati
- **Ripetibile**: booleano per sezioni ripetibili

**Proprietà avanzate:**

- **Espressione visibile**: formula per la visibilità condizionale (=formula)
- **Espressione valore**: formula per valori calcolati (=formula)

### Comandi di integrazione

**Azioni invio:**

- Notifiche e-mail
- Invii API REST
- Archiviazione cloud (Azure, SharePoint)
- Automazione dei flussi di lavoro (Power Automate, Workfront Fusion)
- Piattaforme di marketing (Marketo)
- Integrazioni CRM

### Linee guida per la sintassi Prompt

- **Riferimenti campo**: utilizzare `@fieldName` per i campi esistenti
- **Comandi**: utilizzare `/command` per azioni specifiche
- **Linguaggio naturale**: descrive i requisiti in modo chiaro e specifico

### Elenco di controllo convalida

Per informazioni complete sulle best practice e le linee guida per la convalida, consulta la [Guida introduttiva di Forms Experience Builder](forms-ai-assistant-getting-started.md#best-practices).

*Questa libreria di prompt viene continuamente aggiornata in base al feedback degli utenti e alle nuove funzionalità di Forms Experience Builder. Per le funzionalità e gli esempi più recenti, controlla la [documentazione di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=it).*
