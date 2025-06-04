---
title: Assistente AI per AEM Forms (Forms Experience Builder)
description: Creare forme potenti più rapidamente utilizzando i frammenti di modulo
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: a8d64082-a23f-4919-ad66-042faad77d29
source-git-commit: ab071b9159f3d4db275313080d7c14a46096c4de
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 1%

---

# Assistente AI per AEM Forms (Forms Experience Builder)

>[!NOTE]
>
>
> La funzionalità Assistente IA per AEM Forms (Forms Experience Builder) è disponibile nel **programma per utenti precoci**. Se sei interessato, invia una breve e-mail dal tuo indirizzo di lavoro a mailto:aem-forms-ea@adobe.com per richiedere l’accesso alla funzionalità.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifica**: questa documentazione è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. Funzionalità, comandi ed esempi possono cambiare man mano che l’Assistente IA per AEM Forms continua a evolversi durante il programma per i primi utenti.

L’Assistente all’intelligenza artificiale per AEM Forms trasforma il modo in cui si creano i moduli, descrivendo semplicemente ciò di cui hai bisogno nel linguaggio naturale e osservando i moduli prendere vita. Disponibile nell’interfaccia utente di gestione di Forms, nell’editor di Forms adattivo e nell’editor universale, comprende le tue intenzioni e crea esattamente ciò che stai cercando.

## Guida introduttiva: basta parlarne

L’Assistente AI funziona come una conversazione con un collega esperto. Invece di imparare a usare menu e impostazioni complessi, descrivi semplicemente ciò che desideri creare.

### Guida rapida

Inizia subito a lavorare guardando il nostro video introduttivo:

>[!VIDEO](https://video.tv.adobe.com/v/3463164/)

### Accesso all’Assistente AI

È possibile accedere all’Assistente AI da tre diverse posizioni in AEM Forms:

1. **Interfaccia utente gestione Forms**
   - Passa a: Adobe Experience Manager > Forms > Forms e documenti
   - Cerca l’icona Assistente AI sul lato sinistro dell’interfaccia
   - Fai clic sull’icona per aprire il pannello Assistente AI

   ![Icona Assistente IA*](/help/edge/docs/forms/assets/forms-manager.gif){width="50%"}

2. **Editor Forms adattivo**
   - Passa a: Adobe Experience Manager > Forms > Forms e documenti
   - Seleziona e apri un modulo per la modifica
   - Fai clic sull’icona Assistente AI nell’interfaccia dell’editor

   ![Icona Assistente IA*](/help/edge/docs/forms/assets/adaptive-forms-editor.gif){width="75%"}

3. **Editor universale**

   - Passa a: Adobe Experience Manager > Forms > Forms e documenti
   - Cerca l’icona Assistente AI sul lato sinistro dell’interfaccia
   - Fai clic sull’icona Assistente AI nell’interfaccia dell’editor

### Come iniziare: conversazioni semplici

Il modo migliore per iniziare con l’Assistente AI è attraverso il linguaggio naturale. Ecco come:

**Descrivi solo ciò di cui hai bisogno:**

- &quot;Crea un modulo di contatto per il sito Web&quot;
- &quot;Ho bisogno di un modulo di feedback del cliente con le scale di valutazione&quot;
- &quot;Crea un modulo di registrazione per il mio prossimo evento&quot;
- &quot;Fai un semplice sondaggio sulla soddisfazione del prodotto&quot;

**Aggiungi dettagli man mano:**

- &quot;Crea un modulo per i contatti con i campi Nome, E-mail, Telefono e Messaggio&quot;
- &quot;Ho bisogno di un modulo di registrazione in più passaggi per una conferenza&quot;
- &quot;Crea un modulo di feedback del cliente con valutazioni a 5 stelle e sezioni di commenti&quot;

**Fai riferimento ai campi esistenti:**

- &quot;Rendi obbligatorio il campo e-mail&quot; (per @email)
- &quot;Aggiungi convalida al campo del numero di telefono&quot; (per @phoneNumber)
- &quot;Mostra le informazioni sul coniuge solo se è selezionata l&#39;opzione sposato&quot; (per @spouseInfo e @maritalStatus)

### Cosa puoi fare

Oltre al linguaggio naturale, l’Assistente per l’intelligenza artificiale offre ulteriori modi di interagire:

- **Carica file**: allega immagini, PDF o progettazioni Figma per mostrare all&#39;intelligenza artificiale ciò che stai immaginando
- **Usa comandi rapidi**: Digitare `/` per visualizzare le scelte rapide disponibili per le azioni comuni
- **Riferimento a campi specifici**: utilizzare `@fieldName` per modificare campi modulo esistenti (ad esempio `@firstName`, `@emailAddress`)

## Cosa puoi creare: esempi efficaci

Di seguito sono riportati esempi reali di ciò che è possibile realizzare con un linguaggio semplice e naturale:

### Avvio di un nuovo modulo

**Approccio semplice:**

```
"Create a contact form"
```

**Approccio più dettagliato:**

```
"Create a professional contact form for a law firm with fields for name, email, phone, case type, and message. Make it mobile-friendly."
```

**Con riferimento progettazione:**

```
"Create a contact form based on the attached design mockup. Include all the fields shown in the layout."
```

### Aggiunta di elementi del modulo

**Aggiunte di base:**

```
"Add a section for personal information"
"Include a file upload for resume"
"Add a dropdown for country selection"
```

**Specifiche dettagliate:**

```
"Add a personal information panel with fields for full name, date of birth, phone number, and email address"
"Include a secure file upload component for documents, limited to PDF files under 5MB"
"Add a country dropdown with options for USA, Canada, UK, and Germany"
```

### Creazione di un comportamento dinamico

**Logica semplice:**

```
"Show additional fields when 'Other' is selected"
"Make the email field required"
"Calculate the total automatically"
```

**Regole di business complesse:**

```
"Show the spouse information fields only when marital status is set to 'Married'"
"Calculate the total cost by multiplying quantity and price, then add 10% tax"
"Enable the submit button only when all required fields are completed and terms are accepted"
```

### Layout e progettazione dei moduli

**Modifiche layout:**

```
"Make this a multi-step form"
"Organize fields in two columns"
"Convert to an accordion layout"
```

**Miglioramenti alla progettazione:**

```
"Create a wizard-style form with 3 steps: personal info, preferences, and review"
"Arrange the address fields in a compact two-column layout"
"Update the layout to match the attached wireframe"
```

### Invio e integrazione

**Invio di base:**

```
"Send form data to our email"
"Save responses to a spreadsheet"
"Redirect to a thank you page"
```

**Integrazione avanzata:**

```
"Send form submissions to hr@company.com and create a case in our CRM system"
"Submit data to our REST API endpoint and trigger the new customer workflow"
"Email responses to the sales team and add the lead to our marketing automation platform"
```

## Utilizzo degli allegati

Carica i file per aiutare l’intelligenza artificiale a comprendere esattamente ciò che stai cercando:

### Tipi di file supportati

| Tipo file | Ideale per | Esempio di utilizzo |
|-----------|----------|-------------|
| **Immagini** (PNG, JPG, GIF) | Layout dei moduli, modelli di interfaccia utente, scansioni dei moduli cartacei | &quot;Crea un modulo corrispondente a questo layout&quot; |
| **File PDF** | Moduli esistenti da convertire, specifiche | &quot;Converti questo modulo PDF in digitale&quot; |
| **File Figma** | Prototipi di progettazione, linee guida per il marchio | &quot;Crea questo modulo dal mio design Figma&quot; |
| **File di progettazione** | Riferimenti visivi, guide di stile | &quot;Corrispondenza con lo stile di questo design&quot; |

### Come utilizzare gli allegati

1. **Fare clic sull&#39;icona dell&#39;allegato** nell&#39;interfaccia dell&#39;Assistente AI
2. **Seleziona il file** dal dispositivo
3. **Descrivi cosa vuoi** facendo riferimento al file allegato:
   - &quot;Crea un modulo basato su questo PDF allegato&quot;
   - &quot;Crea un modulo di contatto corrispondente al layout in questa immagine&quot;
   - &quot;Convertire il modulo cartaceo in una versione digitale&quot;

### Best practice con allegati

- **Utilizza immagini chiare e di alta qualità** per una migliore analisi AI
- **Concentrarsi su un concetto per allegato** (layout, stile, ecc.)
- **Descrivi cosa vuoi** insieme all&#39;allegato
- **Mantieni i file sotto i 10 MB** per un&#39;elaborazione ottimale

## Suggerimenti per ottenere risultati ottimali

### Avvio semplice, creazione

- Inizia con le richieste di base: &quot;Crea un modulo di contatto&quot;
- Aggiungi gradualmente i dettagli: &quot;Aggiungi convalida al campo e-mail&quot;
- Test e perfezionamento: &quot;Rendi opzionale il campo del telefono&quot;

### Sii Specifico Quando Necessario

- Invece di: &quot;Fai una buona impressione&quot;
- Prova: &quot;Usa colori professionali e tipografia pulita&quot;

### Usa linguaggio naturale

- Invece di: &quot;Aggiungi componente di input testo&quot;
- Prova: &quot;Aggiungi un campo per il nome&quot;

### Riferimento a elementi esistenti

- Usa `@fieldName` per i campi esistenti: &quot;Rendi @email obbligatorio&quot;
- Specifica i nomi dei campi: &quot;Aggiorna il campo @phoneNumber&quot;

### Suddividere richieste complesse

- Invece di una richiesta grande, prova con più richieste più piccole
- Creare il modulo passo dopo passo
- Verifica ogni modifica prima di passare a quella successiva

## Guida e apprendimento del prodotto

L’Assistente AI può anche insegnarti le funzioni di AEM Forms:

### Fai Domande Come:

- &quot;Come si crea un modulo con più passaggi?&quot;
- &quot;Qual è la differenza tra pannelli e sezioni?&quot;
- &quot;Come si impostano le notifiche e-mail?&quot;
- &quot;Quali sono le best practice per i moduli compatibili con i dispositivi mobili?&quot;
- &quot;Come si applicano i temi ai moduli?&quot;

### Ottieni Aiuto Per:

- Concetti e terminologia di AEM Forms
- Istruzioni dettagliate per le feature complesse
- Best practice e raccomandazioni
- Risoluzione dei problemi comuni

## Guida di riferimento per le funzioni avanzate

Per gli utenti che desiderano esplorare funzionalità avanzate:

### Comandi rapidi

Digitare `/` per visualizzare i collegamenti disponibili:

| Comando | Scopo | Esempio |
|---------|---------|---------|
| `/create-form` | Avvia un nuovo modulo | `/create-form customer survey` |
| `/add-form` | Aggiungi modulo nell’editor universale | `/add-form contact form` |
| `/update-layout` | Modificare la struttura del modulo | `/update-layout wizard with 3 steps` |
| `/update-field` | Modifica proprietà campo | `/update-field @email to be required` |
| `/create-rule` | Aggiungi comportamento dinamico | `/create-rule show @spouse if married` |
| `/create-panel` | Aggiungi contenitori campi | `/create-panel Personal Information` |
| `/configure-submit` | Configurare l’invio di un modulo | `/configure-submit to email support` |
| `/help` | Ottenere assistenza | `/help multi-step forms` |

### Sintassi di riferimento campo

Utilizza `@fieldName` per fare riferimento a campi esistenti:

- `@firstName` - Campo nome
- `@email` - Campo e-mail
- `@phoneNumber` - Campo numero di telefono
- `@dateOfBirth` - Campo data di nascita

### Tipi di componenti

Utilizza questi termini per ottenere risultati ottimali:

- `text input` - Campo di testo a riga singola
- `text area` - Campo di testo su più righe
- `dropdown` - Seleziona elenco
- `checkbox` - Casella di controllo singola
- `checkbox group` - Più caselle di controllo
- `radio group` - Gruppo di pulsanti di scelta
- `date picker` - Selezione data
- `file upload` - File allegato
- `panel` - Contenitore per il raggruppamento dei campi

## Risoluzione dei problemi

### Problemi comuni e soluzioni

**Assistente IA non risponde:**

- Verifica la connessione Internet
- Assicurarsi di essere in un ambiente supportato
- Chiudere e riaprire il pannello Assistente AI

**Risultati imprevisti:**

- Prova a riformulare la richiesta in modo più specifico
- Suddividere le richieste complesse in passaggi più piccoli
- Utilizza la terminologia standard di AEM Forms

**Riferimenti campo non funzionanti:**

- Controllare che i nomi dei campi siano scritti esattamente come appaiono
- Usa la sintassi `@fieldName` per i campi esistenti
- Assicurati che il campo esista prima di farvi riferimento

**Problemi relativi all&#39;importazione della progettazione:**

- Verificare che i file siano chiari e ben strutturati
- Utilizzare i formati supportati (PDF, PNG, JPG, Figma)
- Assicurati che la dimensione del file sia inferiore a 10 MB

## Feedback e supporto

Aiutaci a migliorare l’Assistente AI:

- **Invia feedback**: utilizza il pulsante Feedback nell&#39;interfaccia dell&#39;Assistente AI
- **Segnala problemi**: contatta il supporto Adobe tramite canali ufficiali
- **Condividi esperienze**: il tuo input ti aiuta a migliorare l&#39;assistente di tutti

## Risorse correlate

[Assistente AI di AEM Forms - Libreria di richieste](/help/edge/docs/forms/ai-assistant-prompt-library.md)
