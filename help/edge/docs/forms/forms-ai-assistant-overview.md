---
title: Forms Experience Builder
description: Creare moduli potenti più rapidamente utilizzando i frammenti di modulo
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: 9996bc602ae6169dd1aade622d5dbc5b1addeb54
workflow-type: tm+mt
source-wordcount: '1113'
ht-degree: 2%

---


# Introduzione a Forms Experience Builder

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa documentazione è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. Funzionalità, comandi ed esempi potrebbero cambiare man mano che Forms Experience Builder continua ad evolversi durante il programma per i primi utenti.

Forms Experience Builder porta la potenza dell&#39;intelligenza artificiale a Adobe Experience Manager (AEM) Forms. Questa soluzione innovativa trasforma il modo in cui le organizzazioni creano, gestiscono e ottimizzano i propri moduli digitali attraverso interazioni nel linguaggio naturale e automazione intelligente.

Basato sulle moderne tecnologie web e su servizi di intelligenza artificiale avanzati, Forms Experience Builder consente agli utenti tecnici e non di creare moduli sofisticati di livello professionale tramite interfacce conversazionali. Forms Experience Builder semplifica l&#39;intero processo di creazione dei moduli, sia che si tratti di un analista aziendale che necessita di un semplice modulo di registrazione o di uno sviluppatore che crea flussi di lavoro complessi in più passaggi.

## Interfaccia conversazionale

Forms Experience Builder offre un’interfaccia intuitiva basata su chat che rende la creazione di moduli semplice come una conversazione:

```
┌─────────────────────────────────────────────────────────┐
│ Forms Experience Builder                               │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  👤 User: Create a customer feedback form              │
│                                                         │
│  🤖 AI: I'll help you create a feedback form. What    │
│       type of feedback do you want to collect?         │
│                                                         │
│  👤 User: Product reviews with ratings and comments    │
│                                                         │
│  🤖 AI: Perfect! I've created a feedback form with:   │
│       * Product rating (1-5 stars)                     │
│       * Comment field                                   │
│       * Customer email (optional)                       │
│       * Submit to email notification                    │
│                                                         │
│  👤 User: Add a field for product category             │
│                                                         │
│  🤖 AI: Added a dropdown field with common categories  │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

## Funzionalità di base

### Creazione di moduli basati su intelligenza artificiale

**Generazione modulo lingua naturale**

Crea moduli completi da zero utilizzando descrizioni in inglese semplice. È sufficiente descrivere i requisiti, ad esempio &quot;Creare un modulo di feedback del cliente con scale di valutazione e campi di commento&quot; e Forms Experience Builder genera la struttura del modulo, i tipi di campo e le regole di convalida appropriati.

**Dynamic Field Management**

Aggiungi, modifica o rimuovi campi modulo tramite comandi di conversazione. L’intelligenza artificiale comprende il contesto e può suggerire in modo intelligente tipi di campi, regole di convalida e miglioramenti all’interfaccia utente in base alle tue esigenze.

**Ottimizzazione layout**

Aggiorna i layout e le configurazioni dei moduli tramite il linguaggio naturale. Richiedi modifiche quali &quot;Rendi il modulo più facile da usare&quot; o &quot;Riorganizza i campi in un flusso logico&quot; e Forms Experience Builder applica le regolazioni di stile e layout appropriate.

### Importazione e conversione intelligenti

**Conversione da PDF a modulo**

Trasformare i documenti PDF statici in moduli interattivi e dinamici. Caricare qualsiasi documento PDF e Forms Experience Builder analizza la struttura per creare un modulo digitale corrispondente con i tipi di campo e la convalida appropriati.

**URL per conversione modulo**

Converti moduli web o pagine esistenti in AEM Forms. È sufficiente fornire un URL; Forms Experience Builder estrae gli elementi modulo e li ricrea come AEM Forms nativo con funzionalità avanzate.

**Supporto di file multiformato**

Gestisci vari tipi di file per la creazione di moduli, tra cui PDF, immagini, schermate e modelli di modulo esistenti. Forms Experience Builder è in grado di elaborare e convertire questi elementi in AEM Forms funzionali.

### Logica avanzata dei moduli e integrazione

**Generazione intelligente di regole**

Creazione di regole complesse di convalida dei moduli e di logica di business attraverso il linguaggio naturale. Forms Experience Builder può generare una logica condizionale sofisticata, dipendenze dei campi e regole di convalida che in genere richiedono una conoscenza approfondita della codifica.

**Configurazione completa azione di invio**

Configura l’invio dei moduli da integrare con i sistemi aziendali esistenti:

- **Integrazione e-mail**: configurare notifiche e conferme e-mail automatiche
- **Endpoint REST API**: connessione ad applicazioni e servizi personalizzati
- **Archiviazione cloud**: integrazione con Azure Blob Storage, SharePoint e OneDrive
- **Automazione dei flussi di lavoro**: connessione a Power Automate e Workfront Fusion
- **Piattaforme di marketing**: integrazione diretta con Marketo per la gestione dei lead
- **Flussi di lavoro di AEM**: sfrutta le funzionalità del flusso di lavoro di AEM esistenti

**Analisi delle prestazioni**

Analizza le prestazioni di conversione dei moduli e i modelli di coinvolgimento degli utenti. Forms Experience Builder fornisce informazioni approfondite sull’efficacia dei moduli e suggerisce ottimizzazioni per migliorare i tassi di completamento e l’esperienza utente.

## Come funziona

Forms Experience Builder adotta un approccio semplice e conversazionale:

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│  1. Describe    │───▶│  2. AI Creates  │───▶│  3. Refine &    │
│  Your Form      │    │  Initial Form   │    │  Configure      │
│  Requirements   │    │                 │    │                 │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         │                       │                       │
         ▼                       ▼                       ▼
┌─────────────────────────────────────────────────────────────────┐
│  "Create a loan application form"  →  Form with relevant        │
│  "Add conditional logic"           →  fields and basic          │
│  "Connect to CRM system"           →  validation rules          │
└─────────────────────────────────────────────────────────────────┘
```

## Esempi di casi d’uso

### Modulo di richiesta di prestito

```
┌─────────────────────────────────────────────────────────┐
│ Loan Application - Multi-Step Form                    │
├─────────────────────────────────────────────────────────┤
│ Step 1: Personal Information                           │
│  🏠 Property Type: [Primary] [Investment] [Commercial] │
│  💰 Loan Amount: [$_______] (triggers different paths) │
│  📊 Income Verification: [W2] [Self-Employed] [Other]  │
│                                                         │
│ Step 2: Financial Details (conditional based on above) │
│  ↳ If Self-Employed: Show tax returns, profit/loss     │
│  ↳ If W2: Show employment history, pay stubs           │
│  ↳ Complex debt-to-income calculations                 │
│                                                         │
│ Step 3: Compliance & Review                            │
│  📋 Regulatory disclosures, digital signatures         │
│  🔍 Automated eligibility pre-screening                │
└─────────────────────────────────────────────────────────┘
```

### Modulo di richiesta di risarcimento assicurativo

```
┌─────────────────────────────────────────────────────────┐
│ Insurance Claim - Adaptive Form                        │
├─────────────────────────────────────────────────────────┤
│ 🚗 Claim Type: [Auto] [Property] [Health] [Business]   │
│                                                         │
│ ↳ Auto Selected: Shows accident details, police report │
│ ↳ Property: Shows damage assessment, repair estimates  │
│ ↳ Health: Shows medical provider network, pre-auth     │
│                                                         │
│ 📎 Dynamic Document Requirements:                       │
│   * Photos/videos of damage                            │
│   * Police reports (auto only)                         │
│   * Medical records (health only)                      │
│   * Repair estimates (property only)                   │
│                                                         │
│ 🔄 Real-time claim status updates                      │
└─────────────────────────────────────────────────────────┘
```

### Scenari di migrazione e conversione

Trasforma i moduli esistenti in potenti esperienze digitali con la conversione basata sull’intelligenza artificiale.


#### Trasformare PDF forms in Digital Forms

Trasforma PDF forms con più campi in esperienze digitali dinamiche con calcoli automatizzati e design reattivo per i dispositivi mobili.

**Vantaggi chiave:**

- Calcolo automatico delle imposte e dipendenze dei campi
- Firme digitali e integrazione di archiviazione elettronica
- Ottimizzazione del layout adattabile ai dispositivi mobili
- Riduzione del 95% degli errori di elaborazione


#### Modernizzazione dei moduli legacy basati su XFA

È possibile convertire applicazioni XFA complesse in moderne procedure guidate in più passaggi con convalida in tempo reale e conformità alle normative di accessibilità.

**Vantaggi chiave:**

- Interfaccia semplificata con procedura guidata in più passaggi
- Convalida in tempo reale con aiuto contestuale
- Integrazione del database governativo
- Conformità completa alle linee guida WCAG 2.1 per l’accessibilità


#### Convertire la schermata di un modulo in un modulo digitale

È possibile trasformare qualsiasi modulo cartaceo in un’esperienza digitale. AEM Forms ottimizza automaticamente il layout e crea moduli digitali pronti per l’integrazione da uno screenshot.

**Vantaggi chiave:**

- Rilevamento intelligente del tipo di campo
- Generazione di layout reattivo ottimizzato
- Convalida migliorata oltre la carta originale
- Architettura pronta per l’integrazione

#### Importare e migliorare i moduli web esistenti

Puoi importare il modulo web esistente e aggiungere ai moduli convalida avanzata, logica condizionale e invio multicanale senza interrompere le funzionalità esistenti.

**Vantaggi chiave:**

- Logica e regole di convalida avanzate
- Comportamenti e flussi di lavoro dei campi condizionali
- Opzioni di invio multicanale
- Analisi integrata e tracciamento delle prestazioni

## Confronto tra Forms Experience Builder e sviluppo tradizionale

| Aspetto | Creazione di moduli tradizionali | Forms Experience Builder |
|--------|---------------------------|----------------------|
| **Tempo di creazione** | 2-3 giorni | 2-3 ore |
| **Conoscenze tecniche** | Obbligatorio | Non obbligatorio |
| **Regole di convalida** | Codifica manuale | Linguaggio naturale |
| **Ottimizzazione mobile** | CSS/JS manuale | Automatico |
| **Accessibilità** | Implementazione manuale | Conformità incorporata |
| **Aggiornamenti** | Modifiche al codice necessarie | Linguaggio naturale |


## Vantaggi per le organizzazioni

### Creazione di moduli democratizzati

Consentire agli utenti non tecnici di creare moduli sofisticati senza conoscenze di programmazione. Gli analisti aziendali, gli esperti in materia e i creatori di contenuti possono tradurre direttamente le loro esigenze in forme funzionali attraverso conversazioni in linguaggio naturale.

### Time-to-Value ridotto (TTV)

Accelerare notevolmente lo sviluppo dei moduli da giorni ad ore. Ciò che in precedenza richiedeva cicli di sviluppo estesi ora può essere realizzato in una singola sessione tramite IA conversazionale, consentendo un più rapido go-to-market per le iniziative digitali.

### Semplicità dell&#39;interfaccia

Elimina la curva di apprendimento con un&#39;interfaccia di conversazione intuitiva. Gli utenti possono creare moduli complessi utilizzando il linguaggio naturale invece di imparare gli strumenti tecnici per la creazione dei moduli, riducendo i tempi di formazione e aumentando l’adozione.

### Ridimensionamento degli sforzi di modernizzazione

Modernizzare in modo efficiente i portfolio di moduli legacy. Converti i moduli PDF, XFA e HTML esistenti in esperienze digitali dinamiche, preservando al contempo la logica di business e migliorando l’esperienza utente nell’intero ecosistema dei moduli.

## Guida introduttiva

Per iniziare a utilizzare Forms Experience Builder, visita la [documentazione di Forms Experience Builder](forms-ai-assistant-getting-started.md). Puoi accedere a Forms Experience Builder tramite AEM Forms Editor o Universal Editor, a seconda del flusso di lavoro preferito.

Per le organizzazioni che intendono trasformare i processi di creazione dei moduli, Forms Experience Builder offre una soluzione potente e intuitiva che combina la flessibilità dell’intelligenza artificiale conversazionale con la robustezza della gestione dei moduli di livello enterprise.

## Onboarding e accesso anticipato

Forms Experience Builder è attualmente disponibile come parte del programma di accesso anticipato (EA). Per partecipare e ottenere l&#39;accesso, eseguire la procedura seguente:

1. Assicurati di utilizzare il tuo indirizzo e-mail ufficiale di lavoro associato alla tua organizzazione.
2. Invia un&#39;e-mail a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) richiedendo l&#39;accesso a Forms Experience Builder.
3. Includi il nome della tua organizzazione ed eventuali dettagli rilevanti sul progetto nella richiesta per accelerare il processo di onboarding.

>[!NOTE]
>
> L’accesso a Forms Experience Builder è limitato ai partecipanti approvati nel programma Early Access. Adobe rivedrà la tua richiesta e fornirà ulteriori istruzioni per l’onboarding, se hai i requisiti necessari.

Per ulteriori informazioni sul programma Early Access e sulle relative funzionalità, consulta la [documentazione di AEM Forms Early Access](/help/forms/early-access-ea-features.md).

