---
title: Assistente IA per AEM Forms (Forms Experience Builder)
description: Creare moduli potenti più rapidamente utilizzando i frammenti di modulo
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: fe34b44d02c308e7d18a08dd05f21abc67bd0cb2
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 97%

---


# Guida introduttiva all’Assistente AI per AEM Forms (Forms Experience Builder)

>[!NOTE]
>
>
> La funzionalità dell’Assistente IA per AEM Forms (Forms Experience Builder) è disponibile nel **programma per primi utilizzatori**. Se sei interessato, invia un&#39;e-mail rapida dal tuo indirizzo di lavoro a mailto:aem-forms-ea@adobe.com per richiedere l&#39;accesso alla funzionalità.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa documentazione è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. Funzionalità, comandi ed esempi possono cambiare man mano che l’Assistente IA per AEM Forms continua a evolversi durante il programma per primi utilizzatori.

L’Assistente IA per AEM Forms trasforma il modo in cui si creano i moduli: basta semplicemente descrivere ciò di cui hai bisogno in linguaggio naturale e vedrai i moduli prendere vita. Disponibile nell’interfaccia utente per la gestione dei moduli, nell’editor dei moduli adattivi e nell’editor universale, comprende le tue intenzioni e crea esattamente ciò che stai cercando.

## Guida introduttiva: basta parlarci

Interagire con l’Assistente IA è come parlare con un collega esperto. Invece di imparare a usare menu e impostazioni complessi, descrivi semplicemente ciò che desideri creare.

### Inizio rapido

Inizia subito guardando il nostro video introduttivo:

>[!VIDEO](https://video.tv.adobe.com/v/3463164/)

### Accesso all’Assistente IA

Puoi accedere all’Assistente IA da tre diverse posizioni in AEM Forms:

1. **Interfaccia utente per la gestione dei moduli**
   - Passa a: Adobe Experience Manager > Moduli > Moduli e documenti
   - Cerca l’icona dell’Assistente IA sul lato sinistro dell’interfaccia
   - Fai clic sull’icona per aprire il pannello dell’Assistente IA

   ![Icona Assistente IA*](/help/edge/docs/forms/assets/forms-manager.gif){width="50%"}

2. **Editor dei moduli adattivi**
   - Passa a: Adobe Experience Manager > Moduli > Moduli e documenti
   - Seleziona e apri un modulo per la modifica
   - Fai clic sull’icona dell’Assistente IA nell’interfaccia dell’editor

   ![Icona Assistente IA*](/help/edge/docs/forms/assets/adaptive-forms-editor.gif){width="75%"}

3. **Editor universale**

   - Passa a: Adobe Experience Manager > Moduli > Moduli e documenti
   - Cerca l’icona dell’Assistente IA sul lato sinistro dell’interfaccia
   - Fai clic sull’icona dell’Assistente IA nell’interfaccia dell’editor

### Come iniziare: conversazioni semplici

Il modo migliore per iniziare ad usare l’Assistente IA è tramite il linguaggio naturale. Ecco come:

**Descrivi semplicemente ciò di cui hai bisogno:**

- “Crea un modulo di contatto per il mio sito web”
- “Ho bisogno di un modulo di feedback dei clienti con le scale di valutazione”
- “Crea un modulo di registrazione per il mio prossimo evento”
- “Fai un semplice sondaggio sulla soddisfazione del prodotto”

**Aggiungi dettagli man mano che procedi:**

- “Crea un modulo di contatto con i campi nome, e-mail, telefono e messaggio”
- “Ho bisogno di un modulo di registrazione in più passaggi per una conferenza”
- “Crea un modulo di feedback dei clienti con valutazioni a 5 stelle e sezioni di commenti”

**Riferimento ai campi esistenti:**

- “Rendi obbligatorio il campo dell’e-mail” (per @e-mail)
- “Aggiungi convalida al campo del numero di telefono” (per @phoneNumber)

- “Mostra le informazioni sul coniuge solo se è selezionata l’opzione sposato” (per @spouseInfo e @maritalStaus)

### Ulteriori azioni disponibili

Oltre al linguaggio naturale, l’Assistente IA offre ulteriori modi per interagire:

- **Carica file**: allega immagini, PDF o progettazioni Figma per mostrare all’IA ciò che stai immaginando
- **Usa comandi rapidi**: digita `/` per visualizzare le scelte rapide disponibili per le azioni comuni
- **Riferimento a campi specifici**: utilizza `@fieldName` per modificare campi modulo esistenti (ad esempio `@firstName`, `@emailAddress`)

## Cosa puoi creare: esempi efficaci

Di seguito sono riportati esempi reali di ciò che è possibile realizzare con un linguaggio semplice e naturale:

### Avviare un nuovo modulo

**Approccio semplice:**

```
"Create a contact form"
```

**Approccio più dettagliato:**

```
"Create a professional contact form for a law firm with fields for name, email, phone, case type, and message. Make it mobile-friendly."
```

**Con riferimento alla progettazione:**

```
"Create a contact form based on the attached design mockup. Include all the fields shown in the layout."
```

### Aggiunta di elementi modulo

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

**Modifiche del layout:**

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

Carica i file per aiutare l’IA a comprendere esattamente ciò che stai cercando:

### Tipi di file supportati

| Tipo file | Ideale per | Esempio d’uso |
|-----------|----------|-------------|
| **Immagini** (PNG, JPG, GIF) | Layout dei moduli, modelli dell’interfaccia utente, scansioni dei moduli cartacei | “Crea un modulo corrispondente a questo layout” |
| **File PDF** | Moduli esistenti da convertire, specifiche | “Converti questo modulo PDF in formato digitale” |
| **File Figma** | Prototipi di progettazione, linee guida per il marchio | “Crea questo modulo dalla mia progettazione Figma” |
| **File di progettazione** | Riferimenti visivi, guide allo stile | “Crea una corrispondenza di stile in questa progettazione” |

### Come utilizzare gli allegati

1. **Fai clic sull’icona dell’allegato** nell’interfaccia dell’Assistente IA
2. **Seleziona il file** dal tuo dispositivo
3. **Descrivi cosa desideri** facendo riferimento al file allegato:
   - “Crea un modulo basato su questo PDF allegato”
   - “Crea un modulo di contatto corrispondente al layout in questa immagine”
   - “Convertire questo modulo cartaceo in una versione digitale”

### Best practice con allegati

- **Utilizza immagini chiare e di alta qualità** per un’analisi IA migliore
- **Concentrati su un concetto per allegato** (layout, stile, ecc.)
- **Descrivi cosa desideri** insieme all’allegato
- **Mantieni i file sotto i 10 MB** per un’elaborazione ottimale

## Suggerimenti per ottenere risultati ottimali

### Inizia in modo semplice, poi costruisci

- Inizia con le richieste di base: “Crea un modulo di contatto”
- Aggiungi gradualmente i dettagli: “Aggiungi convalida al campo dell’e-mail”
- Testa e perfeziona: “Rendi opzionale il campo del telefono”

### Fornisci dettagli quando necessario

- Invece di: “Rendilo bello”
- Prova: “Usa colori professionali e una tipografia pulita”

### Utilizza un linguaggio naturale

- Invece di: “Aggiungi un componente di input di testo”
- Prova: “Aggiungi un campo per il nome”

### Riferimento agli elementi esistenti

- Usa `@fieldName` per i campi esistenti: “Rendi @email obbligatorio”
- Fornisci dettagli per i nomi dei campi: “Aggiorna il campo @phoneNumber”

### Suddividere le richieste complesse

- Invece di una grande richiesta, prova con più richieste più piccole
- Creare il modulo passo dopo passo
- Verificare ogni modifica prima di passare a quella successiva

## Assistenza e formazione sul prodotto

L’Assistente IA può anche insegnarti le funzioni di AEM Forms:

### Fai domande come:

- “Come si crea un modulo con più passaggi?”
- “Qual è la differenza tra pannelli e sezioni?”
- “Come si configurano le notifiche e-mail?”
- “Quali sono le best practice per i moduli compatibili con i dispositivi mobili?”
- “Come si applicano i temi ai moduli?”

### Ottieni assistenza per:

- Concetti e terminologia di AEM Forms
- Istruzioni passo dopo passo per le funzioni complesse
- Best practice e consigli
- Risoluzione dei problemi comuni

## Rferimento per le funzioni avanzate

Per gli utenti che desiderano esplorare le funzionalità avanzate:

### Comandi rapidi

Digita `/` per visualizzare le scelte rapide disponibili:

| Comando | Scopo | Esempio |
|---------|---------|---------|
| `/create-form` | Avviare un nuovo modulo | `/create-form customer survey` |
| `/add-form` | Aggiungere un modulo nell’editor universale | `/add-form contact form` |
| `/update-layout` | Modificare la struttura del modulo | `/update-layout wizard with 3 steps` |
| `/update-field` | Modificare le proprietà del campo | `/update-field @email to be required` |
| `/create-rule` | Aggiungere un comportamento dinamico | `/create-rule show @spouse if married` |
| `/create-panel` | Aggiungere contenitori di campi | `/create-panel Personal Information` |
| `/configure-submit` | Configurare l’invio di un modulo | `/configure-submit to email support` |
| `/help` | Ottenere assistenza | `/help multi-step forms` |

### Sintassi di riferimento del campo

Utilizza `@fieldName` per fare riferimento ai campi esistenti:

- `@firstName` - Campo nome
- `@email` - Campo e-mail
- `@phoneNumber` - Campo numero di telefono
- `@dateOfBirth` - Campo data di nascita

### Tipi componente

Utilizza questi termini per ottenere risultati ottimali:

- `text input` - Campo di testo su riga singola
- `text area` - Campo di testo su più righe
- `dropdown` - Seleziona elenco
- `checkbox` - Casella di controllo singola
- `checkbox group` - Più caselle di controllo
- `radio group` - Gruppo pulsanti di scelta
- `date picker` - Selezione data
- `file upload` - Allegato file
- `panel` - Contenitore per il raggruppamento dei campi

## Risoluzione dei problemi

### Problemi comuni e soluzioni

**Assistente IA non risponde:**

- Verifica la connessione Internet
- Assicurati di essere in un ambiente supportato
- Chiudi e riapri il pannello dell’Assistente IA

**Risultati imprevisti:**

- Prova a riformulare la richiesta in modo più specifico
- Suddividi le richieste complesse in passaggi più piccoli
- Utilizza la terminologia standard di AEM Forms

**Riferimenti al campo non funzionanti:**

- Verifica che i nomi dei campi siano scritti esattamente come appaiono
- Usa la sintassi `@fieldName` per i campi esistenti
- Assicurati che il campo esista prima di farvi riferimento

**Problemi relativi all’importazione della progettazione:**

- Verifica che i file siano chiari e ben strutturati
- Utilizza i formati supportati (PDF, PNG, JPG, Figma)
- Assicurati che la dimensione del file sia inferiore a 10 MB

## Feedback e supporto

Aiutaci a migliorare l’Assistente IA:

- **Fornisci feedback**: utilizza il pulsante Feedback nell’interfaccia dell’Assistente IA
- **Segnala problemi**: contatta il supporto Adobe tramite i canali ufficiali
- **Condividi esperienze**: il tuo input rende l’assistente migliore per tutti

## Risorse correlate

[Assistente IA di AEM Forms - Libreria dei prompt](/help/edge/docs/forms/ai-assistant-prompt-library.md)
