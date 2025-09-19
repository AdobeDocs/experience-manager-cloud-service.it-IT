---
title: Guida introduttiva di Forms Experience Builder
description: Scopri le nozioni di base sulla creazione del primo modulo basato sull’intelligenza artificiale con Forms Experience Builder. Tutorial dettagliato con esempi e best practice.
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: de524aeddd5f53cbd713ff0523222966752ebbc0
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 0%

---


# Guida introduttiva di Forms Experience Builder {#getting-started-forms-experience-builder}

Forms Experience Builder rivoluziona la creazione di moduli sfruttando l’intelligenza artificiale per trasformare le descrizioni del linguaggio naturale in moduli digitali completamente funzionali. Questa guida ti aiuterà a creare il primo modulo e a comprendere i concetti di base che rendono potente Forms Experience Builder.

## Cos’è Forms Experience Builder? {#what-is-forms-experience-builder}

Forms Experience Builder è uno strumento per la creazione di moduli basato sull’intelligenza artificiale che consente di creare moduli digitali sofisticati utilizzando un linguaggio di conversazione. Invece delle tradizionali interfacce di trascinamento o della codifica complessa, puoi semplicemente descrivere ciò che desideri e l’intelligenza artificiale crea il modulo per te.

**Funzionalità chiave:**

* **Creazione di moduli in linguaggio naturale** - Descrivi i requisiti del modulo in inglese semplice

* **Importazione e conversione intelligenti** - Trasforma i documenti esistenti in moduli interattivi

* **Generazione campi avanzati** - Campi basati su IA con opzioni precompilate

* **Automazione della logica di business** - Creazione di regole condizionali e convalida tramite conversazione

* **Integrazione di sistema** - Connessione dei moduli ai flussi di lavoro aziendali esistenti

## Prerequisiti {#prerequisites-getting-started}

Prima di iniziare, assicurati di avere:

* **Accesso a Forms Experience Builder** - Disponibile tramite il programma di accesso anticipato
* **AEM Forms as a Cloud Service** - Ambiente di authoring di produzione con componenti core di Forms adattivi
* **Nozioni di base** - Familiarità con i concetti dei moduli e i requisiti aziendali

Per i requisiti tecnici dettagliati relativi all&#39;installazione e alla configurazione dell&#39;ambiente, vedere [Distribuire e configurare Forms Experience Builder](deploy-forms-experience-builder.md).

## Modalità di creazione dei moduli {#two-ways-to-create-forms}

Dopo aver utilizzato la procedura guidata di Forms per selezionare un modello [Componenti core](/help/forms/creating-adaptive-form-core-components.md) o un modello [Edge Delivery Services](/help/edge/docs/forms/universal-editor/create-forms.md), un tema e altre opzioni, Forms Experience Builder offre due approcci principali per la creazione di moduli:

### &#x200B;1. Creare da zero {#create-from-scratch}

Crea moduli utilizzando descrizioni in linguaggio naturale delle tue esigenze.

**Quando utilizzare:**

* Creazione di nuovi moduli dai requisiti

* Creazione di moduli per nuovi processi aziendali

* Se si dispone di specifiche chiare ma non di documenti esistenti

**Esempio:**

    Crea un modulo di feedback del cliente con:
    - Valutazione del prodotto (1-5 stelle)
    - Campo di commento per feedback dettagliato
    - E-mail del cliente (facoltativo)
    - Invia a notifica e-mail

>[!VIDEO](https://video.tv.adobe.com/v/3473104)



### &#x200B;2. Importare e convertire {#import-and-convert}

Trasformare i documenti esistenti in moduli digitali interattivi.

Prima di utilizzare questa opzione, carica il file PDF o un’immagine del modulo. PDF può essere un modulo AcroForm o un modulo PDF basato su XFA. Per [altri tipi di PDF forms](https://experienceleague.adobe.com/en/docs/experience-manager-learn/forms/document-services/pdf-forms-and-documents), utilizzare l&#39;opzione [Prepara modulo](https://helpx.adobe.com/in/acrobat/using/creating-distributing-pdf-forms.html) in Adobe Acrobat per convertirli in un AcroForm

**Quando utilizzare:**

* Conversione di PDF forms esistente

* Modernizzazione dei processi basati su carta

* Quando si dispone di schemi di modulo esistenti per migliorare

**Esempio:**

    /create-form converte il file PDF allegato in un modulo adattivo

>[!VIDEO](https://video.tv.adobe.com/v/3474042)


## Il primo modulo: tutorial dettagliato {#first-form-tutorial}

Creiamo un semplice modulo di contatto per comprendere il flusso di lavoro di base.

### Passaggio 1: iniziare con una semplice descrizione {#step-1-simple-description}

Inizia con una descrizione di base del modulo:

    Crea un modulo di contatto di base con i campi nome, e-mail e messaggio

In questo modo viene creato un modulo con tre campi essenziali.

![Modulo con tre campi essenziali, creato utilizzando il prompt del linguaggio naturale](/help/forms/assets/forms-experience-builder-contact-us-form.png)

### Passaggio 2: aggiungere convalida e requisiti {#step-2-add-validation}

Migliora il modulo con le regole di convalida:

    Rendi obbligatori @name e @email i campi con la convalida appropriata

Il simbolo `@` fa riferimento a campi specifici per le modifiche mirate.

![Aggiunta della convalida nel generatore di esperienze modulo tramite il prompt del linguaggio naturale](/help/forms/assets/forms-experience-builder-contact-us-form-add-validation.png)


### Passaggio 3: migliorare l’esperienza utente {#step-3-improve-ux}

Aggiungi testo e indicazioni utili per i segnaposto:

    Aggiungi testo segnaposto: @name &quot;Nome e cognome&quot;, @email &quot;your.email@company.com&quot;, @message &quot;Come possiamo aiutarci&quot;

![È stata aggiunta la convalida tramite i prompt del linguaggio naturale nel generatore di esperienze di Forms](/help/forms/assets/forms-experience-builder-contact-us-form-add-placeholder.png)

### Passaggio 4: aggiungere funzioni avanzate {#step-4-advanced-features}

Includi funzionalità aggiuntive:

    Aggiungi due elenchi a discesa
    
    - tipo di richiesta con opzioni: &quot;Domanda generale&quot;, &quot;Richiesta di supporto&quot;, &quot;Interrogazione vendite&quot;, &quot;Partnership&quot;
    
    - livello di urgenza con opzioni (Basso, Medium, Alto)


![È stato aggiunto un elenco a discesa utilizzando i prompt del linguaggio naturale in Forms Experience Builder](/help/forms/assets/forms-experience-builder-contact-us-form-add-dropdown.png)


### Passaggio 5: implementare la logica condizionale {#step-5-conditional-logic}

Crea un comportamento intelligente in base al contesto aggiungendo regole quali:

    Nascondi il menu a discesa @urgencyLevel al caricamento del modulo
    Mostra @urgencyLevel menu a discesa (Basso, Medium, Alto) solo quando @inquiryType è uguale a &quot;Richiesta di supporto&quot;

Si tratta di due regole separate: una nasconde il menu a discesa del livello di urgenza quando il modulo viene caricato e l’altra lo mostra solo quando il tipo di richiesta è &quot;Richiesta di supporto&quot;. È necessario creare ogni regola con un prompt separato. È possibile creare una sola regola alla volta.

## Comprensione dell’approccio alla conversazione AI {#ai-conversation-approach}

Forms Experience Builder utilizza un&#39;interfaccia di conversazione in cui è possibile:

### Campi di riferimento con simboli @ {#reference-fields}

Utilizza `@fieldName` per fare riferimento a campi specifici:

    Imposta @email campo obbligatorio
    Aggiungi convalida a @phoneNumber per il formato Stati Uniti
    Modifica @submitButton testo in &quot;Invia messaggio&quot;

>[!VIDEO](https://video.tv.adobe.com/v/3474043)


### Utilizzare i comandi del linguaggio naturale {#natural-language-commands}

Descrivi cosa vuoi in inglese semplice:

    - Aggiungi una sezione per le informazioni sulla società
    - Crea un menu a discesa per la selezione del reparto
    - Includi un caricamento di file per la ripresa
    - Configura le notifiche e-mail quando il modulo viene inviato

### Generazione incrementale {#build-incrementally}

Inizia con semplicità e aggiungi gradualmente complessità:

1. **Struttura di base** - Crea prima i campi essenziali
2. **Aggiungi convalida** - Implementa i campi obbligatori e convalida del formato
3. **Migliora UX** - Aggiungi segnaposto, testo guida e stile
4. **Implementare la logica** - Aggiungere regole condizionali e logica di business
5. **Configura invio** - Configura elaborazione modulo e notifiche


## Modelli di modulo comuni {#common-form-patterns}

### Moduli di contatto e di feedback {#contact-feedback-forms}

**Modulo di contatto di base:**

    Crea un modulo di contatto con:
    - Nome (obbligatorio)
    - E-mail (obbligatorio, convalidato)
    - Menu a discesa Oggetto (Generale, Supporto, Vendite, Partnership)
    - Messaggio (obbligatorio, su più righe)
    - Pulsante Invia

**Modulo feedback cliente:**

    Crea un modulo di feedback del cliente con:
    - Valutazione del prodotto (1-5 stelle)
    - Campo di commento per feedback dettagliato
    - E-mail del cliente (facoltativo)
    - Invia a notifica e-mail

### Moduli di registrazione e onboarding {#registration-onboarding-forms}

**Registrazione utente:**

    Crea un modulo di registrazione utente con:
    - Informazioni personali (nome, e-mail, telefono)
    - Preferenze account (newsletter, notifiche)
    - Accettazione termini e condizioni
    - Creazione password con convalida di forza

**Onboarding dei dipendenti:**

    Crea un modulo per l&#39;onboarding dei dipendenti con:
    - Dati personali e informazioni di contatto
    - Informazioni sull&#39;impiego e data di inizio
    - Caricamenti di documenti (curriculum, ID, moduli fiscali)
    - Selezione di benefit e preferenze

### Moduli di indagine e valutazione {#survey-assessment-forms}

**Sondaggio sulla soddisfazione dei clienti:**

    Crea un sondaggio sulla soddisfazione dei clienti con:
    - Valutazione complessiva (scala da 1 a 10)
    - Valutazione delle categorie (prodotto, servizio, supporto)
    - Sezioni di feedback aperte
    - Informazioni demografiche (facoltative)

**Valutazione delle abilità:**

    Crea un modulo di valutazione delle abilità con:
    - Categorie di abilità con livelli di esperienza
    - Durata dell&#39;esperienza per ogni abilità
    - Informazioni sulla certificazione e sulla formazione
    - Autovalutazione e obiettivi

## Test e convalida {#testing-validation}

### Verifica sempre i moduli {#always-test-forms}

Prima di distribuire un modulo:

1. **Verifica tutti i campi** - Verifica che la convalida funzioni correttamente

2. **Verifica logica condizionale**. Verificare che le regole vengano attivate correttamente

3. **Invio test** - Conferma che i dati siano elaborati correttamente

4. **Convalida su dispositivi diversi** - Garantire la compatibilità mobile

5. **Rivedi con le parti interessate** - Ottieni feedback dagli utenti finali

### Modelli di convalida comuni {#validation-patterns}

**Convalida e-mail:**

    Aggiungi la convalida del formato e-mail @email campo

**Convalida numero di telefono:**

    Aggiungi convalida formato numero di telefono USA a @phoneNumber

**Convalida età:**

    Aggiungi convalida età: deve essere di almeno 18 anni per @dateOfBirth

**Convalida caricamento file:**

    Convalida del tipo di file aggiunto: sono consentiti solo PDF, DOC e DOCX per @resume
    Aggiungi limite dimensione file: massimo 5 MB per @resume

## Passaggi successivi {#next-steps}

Ora che conosci le nozioni di base, scopri questi argomenti avanzati:

* **[Campi avanzati migliorati LLM](forms-experience-builder-llm-smart-fields.md)** - Crea campi con opzioni precompilate utilizzando la conoscenza IA
* **[Creazione di moduli basati su IA](forms-experience-builder-prompt-examples-library.md)** - Modelli ed esempi di prompt avanzati
* **[Importazione e conversione intelligenti](intelligent-import-conversion.md)** - Trasforma i documenti esistenti in moduli
* **[Invio e integrazione dei moduli](form-submission-integration.md)** - Connettere i moduli ai sistemi aziendali


## Articoli correlati

* [Panoramica di Forms Experience Builder](product-overview.md)
* [Campi avanzati migliorati LLM](forms-experience-builder-llm-smart-fields.md)
* [Creazione di moduli basati sull’intelligenza artificiale](forms-experience-builder-prompt-examples-library.md)
* [Importazione e conversione intelligenti](intelligent-import-conversion.md)
* [Invio e integrazione di moduli](form-submission-integration.md)
* [Domande frequenti](forms-experience-builder-frequently-asked-questions.md)
