---
title: Assistente AI per AEM Forms (Forms Experience Builder)
description: Creare forme potenti più rapidamente utilizzando i frammenti di modulo
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: 67416999d068af6350748d610e7c1c7b1d991bc4
workflow-type: tm+mt
source-wordcount: '1657'
ht-degree: 2%

---

# Assistente AI per AEM Forms (Forms Experience Builder)

>[!NOTE]
>
>
> La funzionalità Assistente all’intelligenza artificiale per AEM Forms (Forms Experience Builder) è disponibile nel programma per l’adozione anticipata. Se sei interessato, invia una breve e-mail dal tuo indirizzo di lavoro a mailto:aem-forms-ea@adobe.com per richiedere l’accesso alla funzionalità.


L’Assistente all’intelligenza artificiale per AEM Forms (Forms Experience Builder) migliora l’esperienza di authoring semplificando le attività comuni di creazione dei moduli tramite messaggi in linguaggio naturale. Disponibile in Forms Manager, nell’editor di Forms adattivo e nell’editor universale, consente di creare in modo più intelligente e veloce supportando sia le azioni di creazione che quelle di configurazione. Questa guida ti aiuterà a iniziare e a sfruttare al massimo le sue funzionalità.

## Guida introduttiva

Prima di immergerti in profondità, descriviamo le nozioni di base sull’accesso e l’interazione con l’Assistente AI.

### Accesso all’Assistente AI

È possibile accedere all’Assistente AI da tre diverse posizioni in AEM Forms:

1. **Forms Manager**
   - Passa a: Adobe Experience Manager > Forms > Forms e documenti
   - Cerca l’icona Assistente AI sul lato sinistro dell’interfaccia
   - Fai clic sull’icona per aprire il pannello Assistente AI

   ![Icona Assistente IA*](/help/edge/docs/forms/assets/forms-manager.gif)

2. **Editor Forms adattivo**
   - Passa a: Adobe Experience Manager > Forms > Forms e documenti
   - Seleziona e apri un modulo per la modifica
   - Fai clic sull’icona Assistente AI nell’interfaccia dell’editor

   ![Icona Assistente IA*](/help/edge/docs/forms/assets/adaptive-forms-editor.gif)

3. **Editor universale**

   - Passa a: Adobe Experience Manager > Forms > Forms e documenti
   - Cerca l’icona Assistente AI sul lato sinistro dell’interfaccia
   - Fai clic sull’icona Assistente AI nell’interfaccia dell’editor

L’Assistente AI adatta le sue funzionalità in base alla posizione e all’attività correnti, fornendo assistenza pertinente per ciascun contesto.

### Come interagire:

- È sufficiente digitare la richiesta nel linguaggio naturale.
- Utilizzare `/` per visualizzare un elenco dei comandi o delle azioni rapide disponibili.
- Fare riferimento a campi modulo specifici utilizzando `@fieldName` (ad esempio, `@firstName`, `@emailAddress`) quando si desidera che l&#39;assistente configuri o aggiorni quel particolare campo.


### Guida rapida

Inizia subito a lavorare guardando il nostro video introduttivo:

>[!VIDEO](https://video.tv.adobe.com/v/3463164/)


Questo video illustra il lancio dell’assistente in tutti gli ambienti, le interazioni di base e una panoramica delle sue funzionalità.

## Riferimento comando Assistente IA

| Comando | Descrizione | Scopo | Contesto di utilizzo | Esempi | Funzioni principali |
|---------|-------------|---------|---------------|----------|--------------|
| /create-form | Avviare un nuovo modulo in Forms Manager o Forms Editor | Avvia la creazione di un modulo completamente nuovo da zero | Forms Manager, editor Forms adattivo | /create-form sondaggio del feedback dei clienti | Fornisce opzioni per la struttura dei moduli e crea il modulo |
| /add-form | Aggiungere un nuovo modulo nell’editor universale | Aggiunge un nuovo blocco modulo o componente in Universal Editor. | Editor universale per Edge Delivery Services | Modulo di contatto /add-form con nome e indirizzo e-mail | Inserisce blocchi di modulo, funziona con la modifica basata su blocchi |
| /update-layout | Cambia il layout del modulo in Pannello a soffietto, Schede, Procedura guidata o Progettazione reattiva a pagina singola | Modifica il layout strutturale generale e il modello di navigazione | Tutti gli ambienti di modifica | procedura guidata /update-layout con 3 passaggi | Pannello a soffietto, schede, procedura guidata, opzioni reattive a pagina singola |
| /update-field | Modificare le proprietà e la configurazione dei campi modulo esistenti | Modifica gli attributi dei campi come etichette, convalida, formattazione e comportamento | Tutti gli ambienti di modifica | /update-field @email necessario per la convalida | Etichette, regole di convalida, tipi di campo, valori predefiniti, visibilità |
| /create-rule | Creare un comportamento dinamico e una logica condizionale per i moduli | Implementa logica di business, calcoli e interazioni condizionali | Tutti gli ambienti di modifica | /create-rule mostra @spouseName se @maritalStatus è uguale a &quot;Sposato&quot; | Visibilità condizionale, calcoli, convalida, impostazione valore |
| /create-panel | Crea un nuovo pannello (contenitore per raggruppare i campi correlati) | Aggiunge contenitori strutturali per organizzare i campi modulo in modo logico | Tutti gli ambienti di modifica | /create-panel Informazioni personali con nome, e-mail, telefono | Raggruppamento di campi, titoli, opzioni di layout, sezioni comprimibili |
| /add-panel | Conversione di un’immagine in un pannello modulo in Universal Editor | Utilizza l’intelligenza artificiale per analizzare le immagini caricate e convertirle in pannelli di moduli strutturati | Editor universale | /add-panel da immagine modulo caricata | Riconoscimento delle immagini, conversione da visivo a funzionale, mantenimento del layout |
| /configure-submit | Configurare le azioni di invio dei moduli e la gestione dei dati | Definisce cosa accade quando gli utenti inviano il modulo completato | Tutti gli ambienti di modifica | /configure-submit per inviare e-mail a `support@company.com` | E-mail, API REST, flussi di lavoro, fogli di calcolo, database, Power Automate |
| /help | Accedere all’assistenza e alla documentazione nell’Assistente AI | Fornisce aiuto contestuale, indicazioni e risposte su AEM Forms | Tutti gli ambienti di modifica | /help come si creano i moduli con più passaggi? | Spiegazioni delle funzioni, guide, best practice e risoluzione dei problemi |

### Categorie di comandi

| Categoria | Comandi | Casi d’uso principali |
|----------|----------|-------------------|
| Creazione modulo | /create-form, /add-form | Avvio di nuovi moduli, aggiunta di blocchi di moduli |
| Struttura e layout | /update-layout, /create-panel, /add-panel | Organizzazione della struttura del modulo, progettazione visiva |
| Gestione dei campi | /update-field | Configurazione di singoli elementi del modulo |
| Logica e regole | /create-rule | Aggiunta di comportamento dinamico e convalida |
| Invio | /configure-submit | Impostazione della gestione dei dati e dei flussi di lavoro |
| Supporto | /help | Ottenere assistenza e documentazione |

### Linee guida per la sintassi

| Elemento | Formato | Esempio | Note |
|---------|--------|---------|-------|
| Comandi | /nome-comando | /create-form | Inizia sempre con una barra |
| Riferimenti campo | @fieldName | @email, @firstName | Usa il simbolo @ per i campi esistenti |
| Linguaggio naturale | Comando + descrizione | /create-rule mostra campo se condizione | Combinare comandi con testo descrittivo |
| Azioni multiple | Comandi separati | /create-panel, quindi /update-layout | Applica un comando alla volta |


### Caratteristiche specifiche dell&#39;ambiente

| Ambiente | Comandi disponibili | Funzioni speciali |
|-------------|-------------------|------------------|
| Forms Manager | /create-form, /help | Creazione e gestione a livello di modulo |
| Editor Forms adattivo ed editor universale | Tutti i comandi | Set completo di funzioni, configurazione dettagliata |



### Sintassi dei riferimenti ai campi (elementi contestuali)

Utilizza `@fieldName` per fare riferimento a campi esistenti:

- `@firstName` - Campo nome
- `@email` - Campo e-mail
- `@phoneNumber` - Campo numero di telefono
- `@dateOfBirth` - Campo data di nascita

### Tipi di componenti

Questo elenco descrive i tipi di componenti più comuni. L’intelligenza artificiale può riconoscere varianti o tipi più specializzati, ma l’utilizzo di questi termini precisi produce i risultati migliori:

- `text input` - Campo di testo a riga singola
- `text area` - Campo di testo su più righe
- `dropdown` - Seleziona elenco
- `checkbox` - Casella di controllo singola
- `checkbox group` - Più caselle di controllo
- `radio group` - Gruppo di pulsanti di scelta
- `date picker` - Selezione data
- `file upload` - File allegato
- `panel` - Contenitore per il raggruppamento dei campi


## Funzionalità di base ed esempi di prompt estesi

L’Assistente AI è in grado di comprendere un’ampia gamma di comandi. Ecco alcuni esempi per illustrarne il potere. Ricorda di utilizzare termini precisi per componenti come &quot;pannello&quot;, &quot;immissione testo&quot;, &quot;casella di controllo&quot;, ecc.

| Categoria funzionalità | Descrizione | Esempio di prompt |
| ------------------------- | --------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Creazione modulo** | Iniziare un nuovo modulo da zero o in base a una descrizione. | `Create a new form titled 'Employee Onboarding'.` <br> `Generate a customer feedback form with fields for name, email, rating (1-5 stars), and comments.` <br> `Start a simple contact form with name, email, and message fields.` <br> `Design a multi-page registration form for an event.` |
| **Importa progettazione** | Converti una progettazione esistente (immagine, Figma, PDF) in un AEM Form. | `Import the form design from this uploaded PDF file.` <br> `Convert the uploaded Figma design into an adaptive form, focusing on the 'User Profile' frame.` <br> `Use this JPEG image of our old paper form to create a new digital version.` <br> `Create a form based on the layout of the attached PNG.` |
| **Aggiunta di componenti e pannelli** | Aggiungi vari campi modulo e contenitori strutturali (pannelli). | `Add a text input field for 'First Name'.` <br> `Add a 'Personal Details' panel with fields for full name, date of birth, and phone number.` <br> `Insert a checkbox group for 'Interests' with options: Technology, Sports, Music.` <br> `Add a file upload component for 'Resume'.` <br> `Create a repeatable panel named 'WorkExperience' with fields for company, title, and dates.` |
| **Regolazioni layout** | Modificare la struttura e l&#39;aspetto del layout del modulo. | `Change the 'Personal Details' panel to a two-column layout.` <br> `Set the overall form layout to a wizard (multi-step) navigation.` <br> `Make the header section span the full width of the form.` <br> `Adjust the spacing between fields in the 'Address' panel to be compact.` <br> `Align all field labels to the left.` |
| **Creazione regola e logica** | Implementare comportamento dinamico, calcoli e visibilità condizionale. | `Make the 'Spouse Name' field visible only if 'Marital Status' is selected as 'Married'.` <br> `Calculate the 'Total Amount' by multiplying @quantity and @price.` <br> `Enable the submit button only when the @termsAndConditions checkbox is checked.` <br> `Set the value of @countryCode to '+1' if @country is 'United States'.` <br> `If @age is less than 18, show a message 'Must be 18 or older'.` |
| **Aggiornamento proprietà campo** | Modifica gli attributi di campi modulo specifici come etichette, segnaposto e così via. | `Change the label of @email to 'Primary Email Address'.` <br> `Set the @comment field to be a multi-line text area.` <br> `Make the @phoneNumber field mandatory.` <br> `Add placeholder text 'Enter your ZIP code' to the @zipCode field.` <br> `Change the @country field to a dropdown and populate it with: USA, Canada, UK, Germany.` <br> `Update the help description for @password to 'Must include an uppercase letter, a number, and be at least 8 characters long.'` <br> `Set the maximum length of the @username field to 15 characters.` <br> `Configure the @dateOfBirth field to use a date picker.` |
| **Azioni di invio** | Definire cosa accade quando un utente invia il modulo. | `Configure the form to submit data to the REST endpoint /api/v2/application-submit.` <br> `Set up an email submission to hr@example.com and sales@example.com on successful submission.` <br> `Trigger an AEM workflow named 'NewLeadProcessing' when this form is submitted.` <br> `On submit, redirect the user to a thank you page at /content/thankyou.html.` |
| **Tema** | Applica i temi AEM Forms esistenti per applicare uno stile al modulo. | `Apply the 'Modern Business' theme to this form.` <br> `Switch to the 'Accessible Dark' theme.` <br> `Revert to the default canvas theme.` |
| **Navigazione e struttura** | Aggiungere elementi di spostamento o riorganizzare parti del modulo. | `Add a 'Next' button to the current panel and a 'Previous' button to the next panel.` <br> `Create a Table of Contents based on the form's panels.` <br> `Move the 'Address' panel to be before the 'Contact Information' panel.` |
| **Convalida** | Impostare regole di convalida specifiche per i campi. | `Set a regex pattern for the @employeeID field to be 'EMP\d{5}'.` <br> `Ensure the @age field only accepts numeric values between 18 and 99.` <br> `Validate the @email field to ensure it is a valid email format.` |
| **Piano di revisione** (editor universale) | Visualizza l&#39;anteprima delle modifiche proposte dall&#39;assistente prima dell&#39;esecuzione. | `Add a contact form with fields for name, email, subject, and message.` (l&#39;assistente mostrerà un piano di componenti e proprietà che creerà, quindi fai clic su &quot;Applica&quot;). |

## Best practice per risultati ottimali

Per ottenere il massimo dall’Assistente AI, tieni presenti i seguenti suggerimenti:

- **Inizio semplice, compilazione incrementale:** Iniziare con comandi specifici più piccoli (ad esempio, &quot;Aggiungere un input di testo per &#39;Nome&#39;&quot;) anziché richiedere più passaggi troppo complessi.
- **Utilizza la terminologia di AEM Forms:** Utilizza termini come &quot;pannello&quot;, &quot;campo di immissione testo&quot;, &quot;gruppo di caselle di controllo&quot;, &quot;azione di invio&quot;, &quot;regola&quot; ecc. per una migliore comprensione da parte dell&#39;assistente.
- **Riferimento chiaro ai campi:** Durante la configurazione dei campi esistenti, utilizzare la notazione `@fieldName` (ad esempio, `Make @firstName mandatory`).
- **Rivedi piani** Rivedi sempre i piani con attenzione per le modifiche proposte dall&#39;assistente nell&#39;editor universale prima di fare clic su &quot;Applica&quot;.
- **Convalida manuale:** Dopo che l&#39;assistente ha apportato le modifiche, visualizzare sempre l&#39;anteprima e verificare che il modulo si comporti e abbia l&#39;aspetto previsto. L’intelligenza artificiale è uno strumento potente, ma la convalida finale è fondamentale.
- **Itera e perfeziona:** Se il primo prompt non restituisce il risultato esatto, provare a riformulare o suddividere la richiesta in passaggi più piccoli.
- **Invia feedback:** Utilizza il meccanismo di feedback integrato per aiutare l&#39;assistente ad apprendere e migliorare (consulta la sezione &quot;Feedback e supporto&quot;).

## Guida del prodotto con l’Assistente AI

L’Assistente AI per AEM Forms non è solo per la creazione, ma può anche aiutarti a imparare, comprendere e utilizzare le varie funzioni di AEM Forms.

### Argomenti della Guida supportati

Puoi porre all’assistente domande come:

- &quot;Come si crea un nuovo modulo adattivo da zero?&quot;
- &quot;Che cos’è un pannello in Adaptive Forms e come viene utilizzato?&quot;
- &quot;Spiegare come applicare un tema a un modulo.&quot;
- &quot;Quali tipi di layout sono supportati per moduli e pannelli?&quot;
- &quot;Come posso configurare diverse azioni di invio, ad esempio l’invio di un’e-mail?&quot;
- &quot;Potete guidarmi nell&#39;utilizzo di un progetto Figma per creare un modulo?&quot;
- &quot;Qual è il modo migliore per creare un modulo con più passaggi?&quot;

### Come richiedere assistenza:

1. Apri l’Assistente AI in Forms Manager o nell’Editor di Forms adattivo.
2. Digita la domanda nel linguaggio naturale (ad esempio, &quot;Come posso aggiungere un pannello ripetibile?&quot;).
3. L’assistente risponderà con:
   - Istruzioni dettagliate.
   - Spiegazioni dei concetti di AEM Forms.
   - Se applicabile, collegamenti alla documentazione pertinente di Adobe Experience League.

### Suggerimenti per ottenere una guida migliore:

- **Specifica:** Fai una domanda chiara alla volta.
- **Usa parole chiave:** Includi parole chiave rilevanti per le funzioni o gli elementi dell&#39;interfaccia utente di AEM Forms (ad esempio, &quot;editor di moduli adattivi&quot;, &quot;editor di regole&quot;, &quot;tema&quot;).
- **Riformula se necessario:** Se l&#39;assistente non comprende o non fornisce le informazioni desiderate, provare a semplificare la domanda o utilizzare termini diversi.


## Risoluzione dei problemi comuni

- **L&#39;Assistente Non Risponde:**
   - Assicurati di lavorare attivamente in un ambiente supportato (Forms Manager, Adaptive Forms Editor o Universal Editor).
   - Controlla la tua connessione Internet.
   - Provare a chiudere e riaprire il pannello Assistente AI.

- **Risposte imprecise o impreviste:**
   - Riformula la richiesta in modo che sia più specifica o più semplice.
   - Suddividere una richiesta complessa in singoli comandi più piccoli.
   - Assicurati di utilizzare la terminologia standard di AEM Forms.

- **Problemi relativi all&#39;importazione della progettazione (PDF/Figma/Image):**
   - Verificare che il file di progettazione sia chiaro, ben strutturato e leggibile.
   - Assicurati che il formato del file sia supportato (PDF, collegamento Figma, tipi di immagini comuni come PNG, JPG).
   - Per Figma, assicurati che il frame di destinazione sia chiaramente definito e accessibile.

- **Campo `@fieldName` Non Riconosciuto:**
   - Controllare il nome esatto del campo nel modulo. I nomi dei campi fanno distinzione tra maiuscole e minuscole e devono corrispondere con precisione.
   - Assicurati che il campo esista già se stai tentando di modificarlo.


## Feedback e supporto

Il tuo contributo è prezioso per il continuo miglioramento dell’Assistente AI.

- **Fornisci feedback:** Utilizza il comando o il pulsante **&quot;Fornisci feedback&quot; integrato** nell&#39;interfaccia dell&#39;Assistente AI per condividere esperienze, segnalare problemi o suggerire miglioramenti. Ad esempio, è possibile digitare `/feedback` o cercare un&#39;icona di feedback.
- **Supporto ufficiale:** Per problemi critici o ulteriore assistenza, contatta i canali ufficiali di supporto Adobe o i contatti per il supporto designati della tua organizzazione.


## Contenuto correlato

[Assistente AI di AEM Forms - Libreria di richieste](/help/edge/docs/forms/ai-assistant-prompt-library.md)
