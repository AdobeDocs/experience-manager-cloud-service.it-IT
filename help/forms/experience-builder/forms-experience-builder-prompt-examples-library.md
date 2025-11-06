---
title: 'Forms Experience Builder: libreria di prompt'
description: Raccolta di pattern di prompt ed esempi dimostrati per la creazione di moduli con assistenza IA nell’interfaccia utente per la gestione dei moduli, nell’editor dei moduli adattivi e nell’editor universale.
hide: true
index: false
hidefromtoc: true
role: Admin, Developer
exl-id: 48eb137c-fe12-4e4f-b845-3321ca8b6075
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2193'
ht-degree: 99%

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

Questa libreria fornisce modelli di prompt riutilizzabili per scenari comuni di creazione di moduli. Per best practice complete, consulta la [Guida introduttiva di Forms Experience Builder](/help/forms/experience-builder/forms-experience-builder-getting-started.md).

### Suggerimenti rapidi per questa libreria

- **Inizia con gli esempi**: utilizza i prompt forniti come modelli e adattali alle tue esigenze
- **Due metodi di creazione**: scegli Crea da zero o Importa e converti.
- **Specificità**: aggiungi dettagli personali agli esempi generici
- **Verifica approfonditamente**: convalida sempre i risultati nel tuo ambiente specifico

### Modelli e stili del brand

**Prepara in anticipo le risorse del brand per la creazione di moduli coerenti:**

- **Modelli di brand**: crea modelli di modulo standardizzati con i colori, i font e i pattern di layout della tua organizzazione
- **Linee guida per gli stili**: definisci stili di campo coerenti, progettazioni di pulsanti e standard di spaziatura che Forms Experience Builder può applicare
- **Libreria componenti**: collabora con il team di sviluppo per preparare componenti modulo riutilizzabili che corrispondano alla tua identità del brand
- **Risorse visive**: prepara logo, icone ed elementi dello sfondo per l’integrazione dei moduli


## Esempi di sviluppo incrementale

Questi esempi mostrano come creare moduli passo dopo passo, iniziando in modo semplice e aggiungendo complessità gradualmente:

### Esempio 1: creazione incrementale di un modulo di contatto

**Passaggio 1 - Inizia in modo semplice:**

    Crea un modulo di contatto base con i campi nome, e-mail e messaggio

**Passaggio 2 - Aggiungere la convalida:**

    Rendi obbligatori i campi @name e @email con la convalida appropriata

**Passaggio 3 - Migliorare l’esperienza utente:**

    Aggiungi testo segnaposto: @name “Nome e cognome”, @email “your.email@company.com”, @message “Come possiamo essere di aiuto”

**Passaggio 4 - Aggiungere funzionalità avanzate:**

    Aggiungi un tipo di richiesta a discesa con opzioni: “Domanda generale”, “Richiesta di supporto”, “Richiesta di informazioni sulle vendite”, “Partnership”

**Passaggio 5 - Implementare logica condizionale:**

    /create-rule mostra @urgencyLevel menu a discesa (Basso, Medio, Alto) solo quando @inquiryType è uguale a “Richiesta di supporto”

### Esempio 2: creazione incrementale di un modulo di registrazione

**Passaggio 1 - Struttura di base:**

    Crea un modulo di registrazione utente con il pannello informazioni personali

**Passaggio 2 - Aggiungere campi obbligatori:**

    Aggiungi campi per @firstName, @lastName, @email, @phoneNumber con convalida appropriata

**Passaggio 3 - Aggiungere la logica di business:**

    Crea una regola: se @age è inferiore a 18, mostra sezione informazioni genitore/tutore

**Passaggio 4 - Migliorare con le preferenze:**

    Aggiungi un pannello preferenze con @newsletterSubscription, @marketingConsent, @termsAccepted

**Passaggio 5 - Aggiungere un caricamento file:**

    Includi un campo di caricamento file per @profilePicture con limite di dimensione di 5 MB

## Creazione e gestione moduli

**Quando utilizzare:** quando è necessario creare nuovi moduli o modificare quelli esistenti.

**Come utilizzare:** Scegliere uno dei due approcci seguenti: Crea da zero o Importa e converti (vedere [Guida introduttiva](/help/forms/experience-builder/forms-experience-builder-getting-started.md).

**Esempio di prompt - Creazione semplice del modulo:**

    Crea un modulo di feedback dei clienti con:
    - Valutazione del prodotto (1-5 stelle)
    - Campo di commento per feedback dettagliato
    - E-mail del cliente (facoltativo)
    - Invia a notifica e-mail

**Esempio di prompt - Creazione di un modulo complesso:**

    Crea un modulo di onboarding completo per i dipendenti con:
    
    **Sezione informazioni personali:**
    - Nome completo (nome, secondo nome e cognome)
    - Data di nascita con convalida dell’età
    - Informazioni di contatto (e-mail, telefono, indirizzo)
    - Dettagli di contatto di emergenza
    
    **Dettagli sull’impiego:**
    - Selezione di posizione e reparto
    - Data di inizio con convalida del giorno lavorativo
    - Informazioni sullo stipendio con avviso di riservatezza
    - Struttura di reporting
    
    **Caricamento documento:**
    - Caricamento curriculum/CV (PDF, DOC, DOCX)
    - Documenti di verifica ID
    - Moduli fiscali e informazioni bancarie
    - Contratto di lavoro firmato
    
    **Preferenze:**
    - Selezione dei benefici con il calcolatore dei costi
    - Preferenze pianificazione lavoro
    - Requisiti di formazione
    - Necessità attrezzature
    
    **Regole di convalida:**
    - Convalida formato e-mail
    - Convalida formato numero di telefono
    - Età non superiore a 18
    - Tutti i documenti richiesti devono essere caricati
    - Termini e condizioni devono essere accettati
    
    **Invia azioni:**
    - Invia un’e-mail di conferma al nuovo dipendente
    - Notifica al reparto Risorse umane
    - Crea record dipendente nel sistema Risorse umane
    - Pianifica riunione orientamento

**Prompt gestione moduli:**

    Importa il modulo di richiesta PDF e convertilo in un modulo adattivo con convalida avanzata
    
    Aggiorna il modulo di contatto esistente per includere le maniglie dei social media e il metodo di contatto preferito
    
    Riorganizza il modulo di registrazione in una procedura guidata in tre passaggi: informazioni personali, preferenze, conferma

## Gestione e configurazione del campo

**Quando utilizzare:** quando hai bisogno dio aggiungere, modificare o configurare campi modulo.

**Come utilizzare:** specifica i tipi di campo, i requisiti di convalida e i requisiti dell’esperienza utente.

**Esempio di prompt: aggiunta di un campo di base:**

    Aggiungi un campo di immissione testo per “Nome società” con segnaposto “Inserisci il nome società”

**Esempio di prompt - Configurazione avanzata del campo:**

    Aggiungi una sezione di indirizzo completa con:
    
    **Indirizzo:**
    - Indirizzo 1 (obbligatorio, massimo 100 caratteri)
    - Indirizzo 2 (facoltativo, massimo 100 caratteri)
    - Città (obbligatorio, a discesa con le città comuni)
    - Stato/Provincia (obbligatorio, a discesa)
    - Codice postale (obbligatorio, convalida formato)
    - Paese (obbligatorio, predefinito “Stati Uniti”)
    
    **Regole di convalida:**
    - Il codice postale deve corrispondere alla selezione dello stato
    - Indirizzo 1 non può essere vuoto
    - La città deve essere valida per lo stato selezionato
    
    **Esperienza utente:**
    - Completamento automatico per i campi indirizzo
    - Etichette e testo della guida chiari
    - Campi di input descrittivi ottimizzati per i dispositivi mobili
    - Conformità per dell’accessibilità

**Prompt di configurazione campo:**

    Rendi obbligatorio il campo @email con convalida in tempo reale e messaggio di errore personalizzato
    
    Aggiungi un elenco a discesa per @country con opzioni per Stati Uniti, Canada, Regno Unito, Germania, Francia e “Altro”
    
    Configura il campo @phoneNumber con il formato (XXX) XXX-XXXX e convalida
    
    Aggiungi un campo di caricamento file per @resume con restrizioni PDF e DOC, massimo 5 MB

## Campi avanzati migliorati con LLM

**Quando utilizzare:** quando sono necessari campi con opzioni precompilate che sfruttano la knowledge base dell’intelligenza artificiale.

**Come utilizzare:** se ci sono campi di richiesta che richiedono set di dati completi. L’intelligenza artificiale può compilare automaticamente le opzioni utilizzando la propria conoscenza incorporata.

### Campi geografici e di posizione

**Aeroporti e trasporti:**

    Aggiungi un elenco a discesa per gli aeroporti di partenza con tutti i principali aeroporti internazionali
    Aggiungi il campo dell’aeroporto di arrivo con i codici IATA e i nomi completi
    Crea un campo per l’aeroporto più vicino alla posizione dell’utente
    Aggiungi una selezione di stazioni ferroviarie per le città europee

**Aree geografiche amministrative:**

    Aggiungi un elenco completo degli stati degli Stati Uniti con le abbreviazioni
    Crea un elenco a discesa di un Paese con codici ISO e nomi completi
    Aggiungi un campo per le principali città del mondo con fusi orari
    Includi un elenco a discesa di province e territori canadesi
    Aggiungi un campo per le contee e le aree postali del Regno Unito

### Dati aziendali e di settore

**Classificazioni aziendali:**

    Aggiungi un campo per la classificazione del settore con codici NAICS
    Crea un elenco a discesa dei tipi di entità aziendale (S.r.l,, S.p.A., S.n.c, ecc.)
    Aggiungi un campo per le categorie di dimensione società (startup, PMI, impresa)
    Includi selezione reparto per organizzazioni di grandi dimensioni
    Aggiungi un campo per i tipi di servizi professionali

**Classificazioni professionali:**

    Aggiungi un campo per le mansioni con ruoli di settore comuni
    Crea un elenco a discesa di certificazioni professionali per campo
    Includi livelli di formazione con tipi di laurea
    Aggiungi un campo per gli intervalli degli anni di esperienza
    Crea una selezione per linguaggi di programmazione e framework

### Standard e normative

**Aree finanziaria e legale:**

    Aggiungi un campo per i codici valuta con simboli e tassi di cambio
    Crea un elenco a discesa di tipi di codice fiscale per Paese
    Includi un campo per i tipi di documenti legali
    Aggiungi opzioni metodo di pagamento con funzioni di sicurezza
    Crea una selezione di istituti bancari per Paese

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

    Aggiungi un campo per gli orari d’ufficio con gestione del fuso orario
    Crea un elenco a discesa delle festività per Paese
    Includi opzioni stagionali con intervalli di date
    Aggiungi un campo per la prenotazione di una sala conferenze con disponibilità
    Crea una selezione per i modelli di riunione ricorrenti

### Categorie di prodotti e servizi

**Classificazioni e-commerce:**

    Aggiungi un campo per le categorie di prodotto con sottocategorie
    Crea un elenco a discesa dei metodi di spedizione con le stime di consegna
    Includi un campo per le opzioni dei criteri di restituzione
    Aggiungi una selezione per i livelli di priorità dei clienti
    Crea un campo per i cicli di fatturazione dell’abbonamento

**Esempio di prompt per campi avanzati:**

    “Aggiungi un campo aeroporto di partenza con tutti i principali aeroporti del mondo, inclusi i codici IATA e i nomi delle città”
    
    &quot;Crea un campo di settore completo utilizzando la classificazione NAICS standard con sottocategorie tecnologiche”
    
    “Includi un elenco a discesa di certificazione professionale che si adatta in base al campo di lavoro selezionato”
    
    “Aggiungi un campo numero di telefono internazionale che si formatta in base al Paese selezionato”
    
    “Crea un campo di selezione universitario con le principali istituzioni organizzate per Paese e classificazione”

## Creazione di regole e logica di business

**Quando utilizzare:** quando è necessario implementare logica condizionale, regole di convalida o processi aziendali.

**Come utilizzare:** per descrivere chiaramente la logica di business, specificando condizioni e azioni.

**Prompt di esempio: logica condizionale semplice:**

    Crea una regola che mostri il pannello @spouseInformation solo quando @maritalStatus è uguale a “Sposato”

**Esempio di prompt- Regole aziendali complesse:**

    Implementa la convalida completa della richiesta di prestito:
    
    **Convalida del reddito:**
    - Se @annualIncome è inferiore a 30000:
    - Mostra il messaggio di avviso: “Il reddito potrebbe essere insufficiente per l’importo del prestito richiesto”
    - Richiedi ulteriore documentazione sul reddito
    - Mostra il messaggio: “Potrebbe essere richiesta documentazione aggiuntiva”
    - Se @annualIncome è superiore a 100000:
    - Mostra le opzioni dei servizi premium
    - Abilita la casella di controllo di elaborazione prioritaria
    
    **Convalida basata sull’età:**
    - Se @age è inferiore a 18:
    - Mostra la sezione di informazioni genitore/tutore
    - Rendi obbligatorio il caricamento della firma del genitore
    - Modifica il testo del pulsante Invia in “Invia per revisione”
    - Se @age 65 anni o più:
    - Mostra opzioni sconto senior
    - Aggiungi sezione di preferenze di accessibilità

**Prompt specifici per regole:**

    Crea una **regola di visibilità** che mostra il pannello @spouseInformation solo quando @maritalStatus è uguale a “Coniugato” o “Convivenza”
    
    Aggiungi **divulgazione progressiva** dove vengono mostrate ulteriori domande in base alle risposte precedenti. Inizia con informazioni di base, quindi mostra i follow-up pertinenti
    
    Implementa **impostazioni predefinite avanzate** dove la selezione @country imposta automaticamente i campi correlati. Consenti sostituzione manuale

## Integrazione e invio dei dati

**Quando utilizzarlo:** quando è necessario connettere i moduli a sistemi back-end, database o servizi esterni.

**Come utilizzarlo:** inizia con la configurazione di base dell’invio, quindi aggiungi ulteriori integrazioni in modo incrementale. Specifica il tipo di integrazione, i requisiti del formato dati e le preferenze di gestione degli errori.

**Prompt di esempio - Inizia con invio di base:**

    Configura invio modulo di base per @applicationForm:
    
    **Invio primario:**
    - Invia dati modulo all’endpoint REST: `/api/v1/applications`
    - Formatta dati come JSON
    - Mostra messaggio di operazione riuscita: “Richiesta inviata correttamente”
    - Mostra messaggio di errore se l’invio non riesce: “Invio non riuscito, riprova”

**Aggiungi azioni secondarie in modo in modo incrementale:**

    Aggiungi notifica e-mail ad @applicationForm: invia un messaggio e-mail di conferma all’indirizzo @email con numero di riferimento della richiesta
    
    Aggiungi l’integrazione CRM ad @applicationForm: crea un nuovo record lead potenziale con @firstName, @lastName, @email e imposta lo stato su “Nuova richiesta”

**Prompt di esempio- Invio multicanale standard:**

    Configura l’invio del modulo con più destinazioni dati:
    
    **Invio principale:**
    - Invia dati modulo all’endpoint REST: `/api/v1/applications`
    - Includi intestazione autenticazione con chiave API
    - Formatta i dati come JSON con oggetti nidificati per indirizzo e impiego
    - Gestisci risposta di completamento (201) mostrando il messaggio di ringraziamento
    
    **Azioni secondarie:**
    - Invia e-mail di notifica al richiedente all’indirizzo @email
    - Copia i dati della richiesta nel sistema di tracciamento
    - Attiva il flusso di lavoro per il processo di approvazione
    - Crea record nel CRM con stato lead “Nuova richiesta”
    
    **Gestione degli errori:**
    - Se l’invio primario non riesce, salvare i dati in locale e riprova
    - Mostra messaggio di errore descrittivo: “Invio temporaneamente non disponibile”
    - Fornisci l’opzione per scaricare i dati del modulo come backup
    - Invia un messaggio e-mail di avviso al team di amministrazione sull’invio non riuscito
    
    **Flusso di completamento:**
    - Reindirizza alla pagina di conferma con il numero di riferimento della richiesta
    - Invia un messaggio e-mail di conferma con i passaggi successivi
    - Visualizza la timeline di elaborazione stimata

**Prompt specifici per integrazione:**

    Connetti questo modulo al **sistema CRM** per creare nuovi lead. Mappa @firstName su FirstName, @email su Email, imposta LeadSource su “Modulo web” e Status su “Nuovo”
    
    Imposta **trigger del flusso di lavoro** quando il modulo viene inviato. Trasmetti tutti i dati del modulo e attiva il flusso di lavoro di approvazione con la notifica del manager
    
    Configura **integrazione del database** per salvare gli invii del modulo come record. Crea una nuova cartella per ogni invio con documenti caricati



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

Per informazioni complete sulle best practice e le linee guida per la convalida, consulta la [Guida introduttiva di Forms Experience Builder](/help/forms/experience-builder/forms-experience-builder-getting-started.md).

*Questa libreria di prompt viene continuamente aggiornata in base al feedback degli utenti e alle nuove funzionalità di Forms Experience Builder. Per le funzionalità e gli esempi più recenti, consulta la [documentazione di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=it).*
