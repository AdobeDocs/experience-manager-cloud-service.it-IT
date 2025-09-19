---
title: Campi avanzati migliorati LLM in Forms Experience Builder
description: Scopri come creare campi modulo intelligenti con opzioni precompilate utilizzando la knowledge base di intelligenza artificiale per dati geografici, classificazioni aziendali e standard di settore.
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: de524aeddd5f53cbd713ff0523222966752ebbc0
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 0%

---


# Campi avanzati migliorati LLM in Forms Experience Builder {#llm-enhanced-smart-fields}

Forms Experience Builder sfrutta la potenza dei modelli di linguaggio di grandi dimensioni (LLM, Large Language Models) per creare campi di modulo intelligenti con opzioni precompilate basate su basi di conoscenza complete. Questa funzionalità elimina la necessità di ricercare e inserire manualmente set di dati estesi, migliorando notevolmente l&#39;efficienza e l&#39;accuratezza nella creazione dei moduli.

## Cosa sono i campi avanzati migliorati di LLM? {#what-are-llm-smart-fields}

I campi avanzati migliorati di LLM sono campi modulo che si compilano automaticamente con dati completi e precisi utilizzando la knowledge base incorporata dell’intelligenza artificiale. Invece di creare manualmente elenchi a discesa o set di opzioni, puoi richiedere campi che richiedono set di dati estesi e l’intelligenza artificiale genererà automaticamente le opzioni appropriate.

**Vantaggi principali:**

* **Set di dati completi** - Accesso a informazioni complete e aggiornate su più domini
* **Popolazione automatica** - Non è necessario eseguire ricerche e inserire dati manualmente
* **Formati standardizzati** - Utilizza codici standard, classificazioni e convenzioni di denominazione
* **Opzioni in base al contesto** - I campi possono essere adattati in base ad altre selezioni di moduli
* **Risparmio di tempo** - Riduce il tempo di creazione del modulo da ore a minuti

## Quando utilizzare i campi avanzati migliorati di LLM {#when-to-use-smart-fields}

Utilizza i campi avanzati migliorati con LLM quando hai bisogno di:

* **Set di dati completi** - Campi che richiedono informazioni estese e standardizzate
* **Standard di settore** - Classificazioni, codici o dati normativi
* **Informazioni geografiche** - Sedi, aree geografiche o divisioni amministrative
* **Dati professionali** - Titoli di lavoro, certificazioni o classificazioni di settore
* **Standard tecnici** - Formati di file, protocolli o specifiche di sistema

## Campi geografici e di ubicazione {#geographic-location-fields}

Creazione di campi basati sulla posizione con dati geografici e informazioni amministrative complete.

### Aeroporti e trasporti

**Aeroporti internazionali con codice IATA:**

    Aggiungi un elenco a discesa per gli aeroporti di partenza con tutti i principali aeroporti internazionali
    Aggiungi il campo dell&#39;aeroporto di arrivo con i codici IATA e i nomi completi
    Crea un campo per l&#39;aeroporto più vicino alla posizione dell&#39;utente
    Aggiungi una selezione di stazioni ferroviarie per le città europee

**Esempi di prompt:**

* &quot;Aggiungere un campo aeroporto di partenza con tutti i principali aeroporti del mondo, inclusi i codici IATA e i nomi delle città&quot;
* &quot;Creare un menu a discesa dell’aeroporto di arrivo con aeroporti internazionali organizzati per continente&quot;
* &quot;Includere una selezione di stazioni ferroviarie per le principali città europee con codici di stazione&quot;

### Aree amministrative

**Paesi, stati e province:**

    Aggiungi un elenco completo degli stati degli Stati Uniti con le abbreviazioni
    Crea un elenco a discesa di un paese con codici ISO e nomi completi
    Aggiungi un campo per le principali città del mondo con fusi orari
    Includi un elenco a discesa di province e territori canadesi
    Aggiungi un campo per le contee e le aree postali del Regno Unito

**Esempi di prompt:**

* &quot;Creare un campo di selezione paese con codici paese ISO e nomi completi&quot;
* &quot;Aggiungi un menu a discesa di stato USA con abbreviazioni di stato e nomi completi&quot;
* &quot;Includi un campo provincia canadese con territori e codici postali&quot;
* &quot;Creare un campo città del mondo con le principali aree metropolitane e fusi orari&quot;

## Dati aziendali e di settore {#business-industry-data}

Utilizzo di classificazioni aziendali complete e dati professionali per i moduli aziendali.

### Classificazioni società

**Tipi di entità di settore e business:**

    Aggiungi un campo per la classificazione del settore con codici NAICS
    Crea un elenco a discesa dei tipi di entità business (LLC, Corporation, Partnership, ecc.)
    Aggiungi un campo per le categorie di dimensione società (avvio, PMI, impresa)
    Includi selezione reparto per organizzazioni di grandi dimensioni
    Aggiungi un campo per i tipi di servizi professionali

**Esempi di prompt:**

* &quot;Crea un campo di settore completo utilizzando la classificazione NAICS standard con sottocategorie tecnologiche&quot;
* &quot;Aggiungere un elenco a discesa di tipo entità business con strutture legali e descrizioni&quot;
* &quot;Includi un campo dimensione società con intervalli di conteggio dipendenti e scaglioni di ricavi&quot;

### Classificazioni professionali

**Qualifiche e certificazioni:**

    Aggiungi un campo per i titoli di lavoro con ruoli di settore comuni
    Crea un elenco a discesa di certificazioni professionali per campo
    Includi livelli di formazione con tipi di laurea
    Aggiungi un campo per anni di intervalli di esperienza
    Crea una selezione per linguaggi e framework di programmazione

**Esempi di prompt:**

* &quot;Includi un elenco a discesa di certificazione professionale che si adatta in base al campo del processo selezionato&quot;
* &quot;Creare un campo di qualifica professionale con ruoli comuni in tecnologia, sanità e finanza&quot;
* &quot;Aggiungere un campo di livello di istruzione con tipi di laurea e specializzazioni&quot;

## Standard e dati normativi {#standards-regulatory-data}

Accedi a codici standardizzati, classificazioni e informazioni sulle normative per i moduli incentrati sulla conformità.

### Finanziario e legale

**Informazioni su valuta, imposta e pagamento:**

    Aggiungi un campo per i codici valuta con simboli e tassi di cambio
    Crea un elenco a discesa di tipi di ID imposta per paese
    Includi un campo per i tipi di documenti legali
    Aggiungi opzioni metodo di pagamento con caratteristiche di sicurezza
    Crea una selezione per gli istituti bancari per paese

**Esempi di prompt:**

* &quot;Crea un campo di selezione valuta con codici ISO, simboli e tassi di cambio principali&quot;
* &quot;Aggiungere un campo di tipo ID imposta con formati di identificazione fiscale specifici per il paese&quot;
* &quot;Includi un elenco a discesa del metodo di pagamento con funzioni di sicurezza e tempi di elaborazione&quot;

### Norme tecniche

**Formati e protocolli di file:**

    Aggiungi un elenco a discesa dei tipi di formato file con estensioni
    Includi opzioni del protocollo di rete
    Aggiungi un campo per i tipi di database e le versioni
    Crea una selezione per i metodi di autenticazione API

**Esempi di prompt:**

* &quot;Creare un elenco a discesa del formato di file con estensioni e tipi MIME comuni&quot;
* &quot;Aggiungere un campo di selezione del database con versioni e confronti di funzionalità&quot;
* &quot;Includi un campo del metodo di autenticazione API con livelli di sicurezza&quot;

## Settore sanitario e medico {#healthcare-medical-fields}

Dati medici e sanitari specializzati per moduli specifici del settore.

### Classificazioni mediche

**Dati medici e speciali:**

    Aggiungi un campo per le specializzazioni mediche
    Crea un elenco a discesa di farmaci comuni con nomi generici
    Includi un campo per i tipi di provider di assicurazioni
    Aggiungi una selezione per le relazioni di contatto di emergenza medica
    Crea un campo per le restrizioni alimentari e le allergie

**Esempi di prompt:**

* &quot;Crea un campo di specializzazione medica con specializzazioni secondarie e certificazioni del consiglio di amministrazione&quot;
* &quot;Aggiungere un campo di farmaci con nomi generici, nomi di marchi e moduli di dosaggio&quot;
* &quot;Includere un campo provider di assicurazioni con i principali vettori e i tipi di piano&quot;

## Informazioni sul tempo e sul calendario {#time-calendar-intelligence}

Campi di data e ora avanzati con informazioni sul contesto aziendale e sulla pianificazione.

### Campi data e ora

**Orario operativo e pianificazione:**

    Aggiungi un campo per gli orari lavorativi con gestione del fuso orario
    Crea un elenco a discesa delle festività per paese
    Includi opzioni stagionali con intervalli di date
    Aggiungi un campo per la prenotazione di una sala conferenze con disponibilità
    Crea una selezione per i modelli di riunione ricorrenti

**Esempi di prompt:**

* &quot;Crea un campo orario di lavoro con fusi orari ed eccezioni per le festività&quot;
* &quot;Aggiungere una selezione di festività nazionali&quot;
* &quot;Includi un campo pattern riunione ricorrente con opzioni di frequenza&quot;

## Categorie di prodotti e servizi {#product-service-categories}

Campi orientati al commercio elettronico e ai servizi con categorizzazione completa.

### Classificazioni di e-commerce

**Dati prodotti e servizi:**

    Aggiungi un campo per le categorie di prodotto con sottocategorie
    Crea un elenco a discesa dei metodi di spedizione con le stime di consegna
    Includi un campo per le opzioni dei criteri di restituzione
    Aggiungi una selezione per i livelli di priorità del cliente
    Crea un campo per i cicli di fatturazione dell&#39;abbonamento

**Esempi di prompt:**

* &quot;Creare un campo categoria di prodotto con sottocategorie e modelli di SKU per l’e-commerce&quot;
* &quot;Aggiungi un elenco a discesa del metodo di spedizione con i tempi di consegna e le stime dei costi&quot;
* &quot;Includi un campo del ciclo di fatturazione dell’abbonamento con frequenze di pagamento&quot;

## Best practice per i campi avanzati migliorati con LLM {#best-practices-smart-fields}

### Sii specifico nelle tue richieste

**Esempi validi:**

* &quot;Aggiungi un elenco a discesa del paese con codici ISO, nomi completi e informazioni sulla valuta&quot;
* &quot;Crea un campo di specializzazione medica con certificazioni e sottospecializzazioni del consiglio di amministrazione&quot;
* &quot;Includi un campo del linguaggio di programmazione con framework e livelli di abilità&quot;

**Evita richieste vaghe:**

* &quot;Aggiungere un campo paese&quot;
* &quot;Menu a discesa Crea un ruolo&quot;
* &quot;Includi un campo categoria prodotto&quot;

### Combina con logica condizionale

I campi avanzati funzionano in modo eccezionale con le regole condizionali:

    Crea un campo di certificazione professionale che mostra le opzioni rilevanti in base al settore selezionato
    Aggiungi un campo città che filtra in base al paese selezionato
    Includi un campo università che si adatta in base al campo di studio scelto

### Convalidare e personalizzare

Mentre i campi ottimizzati per LLM forniscono dati completi, è sempre possibile:

* **Controlla le opzioni generate** per la precisione e la rilevanza
* **Aggiungi opzioni personalizzate** specifiche per la tua organizzazione
* **Rimuovi opzioni irrilevanti** per semplificare l&#39;esperienza utente
* **Verifica con utenti reali** per assicurarne l&#39;usabilità

## Tecniche avanzate per campi avanzati {#advanced-smart-field-techniques}

### Campi contestuali

Crea campi che si adattano in base ad altre selezioni di moduli:

    Aggiungi un campo di selezione per università con istituzioni principali organizzate per paese e classificazione
    Crea un elenco a discesa di certificazione professionale che mostra le opzioni rilevanti in base alla qualifica
    Includi un campo città che filtra in base al paese e all&#39;area geografica selezionati

### Classificazioni a più livelli

Creare strutture di dati gerarchiche:

    Crea un campo categoria prodotto con categorie principali, sottocategorie e tipi di prodotto
    Aggiungi un campo geografico con i livelli di paese, stato/provincia e città
    Includi un campo valutazione abilità con categorie, sottocategorie e livelli di esperienza

### Integrazione con dati esterni

Combina la conoscenza di LLM con i dati della tua organizzazione:

    Aggiungi un campo reparto che includa sia i reparti aziendali standard che le divisioni specifiche della tua organizzazione
    Crea un campo prodotto che combini le categorie standard del settore con il catalogo prodotti
    Includi un campo località che unisca i dati geografici con le sedi dell&#39;ufficio

## Risoluzione dei problemi dei campi avanzati {#troubleshooting-smart-fields}

### Problemi e soluzioni comuni

**Problema: troppe opzioni generate**

* **Soluzione**: specifica di più nella richiesta o aggiungi criteri di filtro
* **Esempio**: anziché &quot;tutti i paesi&quot;, richiedi &quot;paesi partner commerciali principali&quot;

**Problema: opzioni specifiche mancanti**

* **Soluzione**: aggiungi opzioni personalizzate o perfeziona la richiesta
* **Esempio**: &quot;Includi i paesi principali più [i tuoi paesi specifici]&quot;

**Problema: informazioni obsolete**

* **Soluzione**: richiedere i dati correnti o specificare intervalli di date
* **Esempio**: &quot;Aggiungere festività correnti per il 2024&quot;

### Ottimizzazione delle prestazioni

* **Opzioni limite**: utilizza i filtri per ridurre il numero di opzioni generate
* **Divulgazione progressiva**: mostra prima le opzioni di base, quindi consenti l&#39;espansione
* **Memorizzazione in cache**: è consigliabile memorizzare nella cache i dati dei campi avanzati utilizzati di frequente

## Articoli correlati

* [Guida introduttiva di Forms Experience Builder](forms-experience-builder-getting-started.md)
* [Creazione di moduli basati sull’intelligenza artificiale](forms-experience-builder-prompt-examples-library.md)
* [Creazione di regole e logica di business](forms-experience-builder-prompt-examples-library.md#rule-creation--business-logic)
* [Invio e integrazione di moduli](form-submission-integration.md)

