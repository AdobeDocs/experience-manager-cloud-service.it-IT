---
title: Forms Experience Builder - Best practice
description: Best practice complete per la creazione di moduli efficaci con Forms Experience Builder, che includono progettazione, esperienza utente, prestazioni e coerenza del brand.
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: fe34b44d02c308e7d18a08dd05f21abc67bd0cb2
workflow-type: tm+mt
source-wordcount: '2072'
ht-degree: 100%

---


# Forms Experience Builder - Best practice

>[!NOTE]
>
> Forms Experience Builder è disponibile nell’ambito del programma per i primi utilizzatori. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa guida alle best practice è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. Le best practice, i consigli e gli esempi possono cambiare man mano che Forms Experience Builder continua a evolversi durante il programma per primi utilizzatori.

Questa guida completa fornisce best practice collaudate per la creazione di moduli efficaci e intuitivi tramite Forms Experience Builder. Queste pratiche derivano da implementazioni di successo e feedback degli utenti in vari settori e casi d’uso.

## Best practice per la progettazione dei moduli

### Semplifica

**Inizia con campi essenziali**

- Inizia con le sole informazioni più necessarie per ridurre il sovraccarico degli utenti
- Aggiungi gradualmente la complessità in base alle esigenze degli utenti e ai requisiti aziendali
- Evita di chiedere informazioni di cui non hai bisogno o che non usi realmente
- Considera il tempo e il carico cognitivo dell’utente durante la progettazione dei moduli

**Usa etichette chiare e descrittive**

- Rendi immediatamente visibili gli scopi del campo con etichette descrittive
- Evita il gergo tecnico o la terminologia interna che gli utenti non comprenderebbero
- Utilizza convenzioni di etichettatura coerenti in tutti i moduli
- Fornisci il contesto quando i requisiti del campo potrebbero non essere evidenti

**Fornisci indicazioni utili**

- Includi testo di istruzioni per campi complessi con esempi e requisiti di formattazione
- Utilizza il testo segnaposto per visualizzare i formati di input previsti
- Fornisci istruzioni chiare per il caricamento dei file, inclusi i formati accettati e i limiti di dimensione
- Guida gli utenti attraverso processi a più passaggi con indicatori di avanzamento

**Esegui il test completo**

- Convalida tutti i percorsi utente e gli scenari prima della distribuzione
- Testa i moduli con utenti reali del pubblico di destinazione
- Verifica che tutta la logica condizionale funzioni come previsto
- Assicurati che la gestione degli errori fornisca feedback chiari e fruibili

### Divulgazione progressiva

**Mostra campi rilevanti in base al contesto**

- Visualizza campi aggiuntivi solo quando sono rilevanti per le selezioni dell’utente
- Utilizza la logica condizionale per ridurre il carico cognitivo e la lunghezza del modulo
- Raggruppa i campi correlati in sezioni logiche
- Nascondi opzioni avanzate finché gli utenti non indicano di averne bisogno

**Esempio di implementazione:**

    Crea una regola che mostri il pannello @spouseInformation solo quando @maritalStatus è uguale a “Sposato”

**Cancella la navigazione e l’avanzamento**

- Guida gli utenti a comprendere la posizione in cui si trovano nei moduli a più passaggi
- Fornisci una navigazione chiara tra le sezioni del modulo
- Mostra indicatori di avanzamento per moduli più lunghi
- Consenti agli utenti di salvare l’avanzamento e ritornarvi in un secondo momento

## Best practice per l’esperienza utente

### Progettazione mobile-first

**Ottimizzazione del layout dinamico**

- Progetta moduli con utenti di dispositivi mobili come considerazione principale
- Utilizza layout a colonna singola per dispositivi mobili
- Assicurati che le dimensioni delle destinazioni di contatto siano appropriate (minimo 44 pixel)
- Testa i moduli su dispositivi di varie dimensioni e orientamenti

**Interazioni adatte al touch**

- Implementa pulsanti più grandi e campi di input per le interfacce touch
- Utilizza tipi di input appropriati per attivare le tastiere per i dispositivi mobili corrette
- Evita interazioni dipendenti dal passaggio del mouse che non funzionano sui dispositivi touch
- Fornisci un feedback visivo chiaro per le interazioni degli utenti

### Conformità dell’accessibilità

**Linee guida WCAG 2.1**

- Segui le linee guida per l’accessibilità dei contenuti web per assicurare una progettazione inclusiva
- Verifica che i rapporti di contrasto dei colori siano corretti (minimo 4,5:1 per il testo normale)
- Fornisci un testo alternativo per tutte le immagini e le icone
- Implementa una corretta struttura del titolo e un HTML semantico

**Navigazione tramite tastiera**

- Assicurati che tutti gli elementi del modulo siano accessibili con la navigazione tramite tastiera
- Fornisci indicatori di focus chiari per tutti gli elementi interattivi
- Implementa l’ordine logico delle schede tramite i campi del modulo
- Includi collegamenti di spostamento nella navigazione per i moduli complessi

**Supporto dell’utilità per la lettura dello schermo**

- Utilizza le etichette ARIA e le descrizioni corrette per i campi del modulo
- Fornisci messaggi di errore chiari che vengono annunciati alle utilità per la lettura della schermo
- Assicurati che le modifiche ai contenuti dinamici vengano annunciate correttamente
- Esegui test dei moduli con il software dell’utilità per la lettura dello schermo

### Ottimizzazione delle prestazioni

**Velocità di caricamento**

- Ottimizza i tempi di caricamento dei moduli riducendo al minimo le dimensioni iniziali del bundle
- Implementa il caricamento lento per le sezioni di moduli non critici
- Ottimizza immagini e risorse per la distribuzione sul web
- Abilita strategie di memorizzazione in cache appropriate per le risorse statiche

**Prestazioni di runtime**

- Utilizza tempi di convalida appropriati per bilanciare la user experience e le prestazioni
- Implementa il debouncing per la convalida in tempo reale per ridurre le richieste dei server
- Memorizza nella cache i dati a cui accedi di frequente e i risultati della convalida
- Ottimizza l’esecuzione della logica condizionale per i moduli complessi

**Salvataggio automatico e protezione dei dati**

- Implementa il salvataggio automatico dell’avanzamento del modulo per evitare la perdita di dati
- Dove possibile, fornisci funzionalità offline per assicurare il completamento del modulo
- Includi la logica per nuovi tentativi per gli invii non riusciti
- Offri opzioni di esportazione dei dati come backup per gli utenti

## Best practice per la brand consistency

### Prepara in anticipo la brand consistency

**Crea modelli di brand**

- Sviluppa modelli di moduli standardizzati con l’identità visiva dell’organizzazione
- Includi schemi di colori, composizione tipografica e pattern di layout coerenti
- Prepara componenti riutilizzabili che corrispondano alle linee guida del tuo brand
- Documenta gli standard di stile per un’implementazione coerente tra i team

**Definisci linee guida per gli stili**

- Definisci stili per i campi, progettazioni di pulsanti e standard di spaziatura coerenti
- Crea una guida di stile che includa codici colore, specifiche dei font e regole di layout
- Definisci pattern di interazione e linee guida per le animazioni
- Prepara messaggi di errore e testi di aiuto specifici per il brand

**Creare la libreria dei componenti**

- Crea componenti modulo riutilizzabili che corrispondono all’identità del brand
- Sviluppa modelli di navigazione ed elementi dell’interfaccia utente coerenti
- Prepara icone con brand, logo e risorse visive per l’integrazione dei moduli
- Definisci modelli per i tipi di modulo comuni (contatto, registrazione, feedback)

### Strategie di implementazione del brand

**Prompt di stile per coerenza**

Includi nei prompt istruzioni specifiche per il brand:

    Crea un modulo per i contatti professionale utilizzando:
    - Blu aziendale (#003366) per i pulsanti e le intestazioni principali
    - Famiglia di font Open Sans per tutti gli elementi di testo
    - Dimensione minima dei font di 16 px per la conformità in materia di accessibilità
    - Spaziatura coerente di 24 px tra le sezioni del modulo
    - Logo aziendale nell’intestazione con il corretto posizionamento del brand

**Gestione libreria modelli**

- Gestisci una raccolta di modelli di modulo con brand per casi d’uso comuni
- Controlla la versione dei modelli di brand per garantire la coerenza
- Fornisci una documentazione chiara per l’utilizzo e la personalizzazione dei modelli
- Revisione e aggiornamento regolari delle risorse del brand per mantenere gli standard correnti

>[!NOTE]
>
>**Componenti personalizzati**: prima di implementare elementi del brand personalizzati, chiedi al team di sviluppo informazioni sull’utilizzo di componenti specifici dell’organizzazione e sulla loro compatibilità con Forms Experience Builder.

## Best practice per contenuti e comunicazioni

### Approcci per la creazione di moduli

**Due metodi principali**

Scegli il metodo di creazione più appropriato alle tue esigenze:

1. **Crea da zero**: ideale per i nuovi moduli con requisiti specifici
2. **Importa e converti**: ideale per modernizzare moduli e documenti esistenti

**Prompt in linguaggio naturale**

- Usa specificazioni e dettagli nelle descrizioni del modulo
- Utilizza un linguaggio chiaro e orientato alle aziende al posto di termini tecnici
- Fornisci un contesto sullo scopo del modulo e sul pubblico target
- Includi i requisiti di convalida e delle regole business nei prompt iniziali

### Strategie di sviluppo incrementale

**Inizia in modo semplice, poi aggiungi complessità**

- Inizia con la struttura del modulo di base e i campi essenziali
- Aggiungi regole di convalida e logica di business in modo incrementale
- Verifica ogni aggiunta prima di passare a quella successiva
- Raccogli feedback degli utenti in ogni fase dello sviluppo

**Esempio di approccio incrementale:**

    Passaggio 1: “Crea un modulo di contatto di base con campi nome, e-mail e messaggio”
    Passaggio 2: “Rendi i campi @name e @email obbligatori con la convalida appropriata”
    Passaggio 3: “Aggiungi testo segnaposto e testo di guida per dare indicazioni all’utente”
    Passaggio 4: “Aggiungi logica condizionale in base al tipo di richiesta”

### Best practice di riferimento al campo

**Convenzioni di denominazione coerenti**

- Utilizza nomi di campo chiari e descrittivi corrispondenti allo scopo
- Mantieni modelli di denominazione coerenti tra i moduli
- Utilizza camelCase o snake_case in modo coerente in tutti i moduli
- Convenzioni di denominazione dei campi del documento per coerenza con il team

**Riferimenti campo effettivi**

- Usa la sintassi `@fieldName` quando modifichi campi esistenti
- Specifica a quali campi fai riferimento nei moduli complessi
- Raggruppa le modifiche dei campi correlate in singole richieste
- Verifica i nomi dei campi prima di utilizzarli nella logica condizionale

## Best practice per l’integrazione e l’invio

### Strategia di invio multicanale

**Azioni principali e secondarie**

- Configura gli endpoint di invio principali per i processi aziendali principali
- Imposta azioni secondarie per notifiche, conferme e backup dei dati
- Implementa la gestione degli errori e la logica dei nuovi tentativi per gli invii non riusciti
- Fornisci feedback agli utenti per tutti gli stati di invio (operazione riuscita, errore, in elaborazione)

**Pianificazione dell’integrazione**

- Inizia con la configurazione di base dell’invio e aggiungi integrazioni in modo incrementale
- Testa ogni integrazione separatamente prima di combinare più endpoint
- Documenta i requisiti API e i metodi di autenticazione
- Pianifica la trasformazione dei dati e i requisiti di mappatura

### Gestione e recupero degli errori

**Messaggi di errore intuitivi**

- Fornisci messaggi di errore chiari e attuabili che aiutino gli utenti a risolvere i problemi
- Evita codici di errore tecnici o messaggi di sistema nel contenuto rivolto all’utente
- Offri azioni alternative quando l’invio principale non riesce
- Includi informazioni di contatto per gli utenti che necessitano di ulteriore assistenza

**Protezione dei dati e ripristino**

- Implementa il salvataggio in locale dei dati per il ripristino dei moduli in seguito a errori
- Fornisci agli utenti le opzioni per scaricare i dati del modulo come backup
- Imposta il monitoraggio e gli avvisi per gli errori di invio
- Pianifica le procedure di ripristino in caso di interruzioni o manutenzione del sistema

## Best practice per prestazioni e analisi

### Monitoraggio e ottimizzazione

**Metriche prestazioni chiave**

- Traccia i tassi di completamento dei moduli e i punti di abbandono
- Monitora i tempi di caricamento e i modelli di interazione dell’utente
- Misura l’efficacia della convalida e i tassi di errore
- Analizza il feedback degli utenti e i punteggi di soddisfazione

**Miglioramento continuo**

- Revisione regolare dell’analisi dei moduli per identificare le opportunità di ottimizzazione
- Test A/B di diverse progettazioni di moduli e flussi utente
- Raccolta e analisi dei feedback degli utenti per miglioramenti iterativi
- Analisi comparativa delle prestazioni rispetto agli standard di settore

### Qualità dei dati e convalida

**Strategie di convalida avanzate**

- Implementazione della convalida in tempo reale per un feedback immediato degli utenti
- Utilizza la convalida progressiva per guidare gli utenti attraverso requisiti complessi
- Fornisci messaggi di convalida chiari che spieghino come correggere gli errori
- Trova un equilibrio tra rigidità della convalida e considerazioni sull’esperienza utente

**Integrità dei dati**

- Implementa la convalida tra campi diversi per garantire la coerenza dei dati
- Utilizza tipi e vincoli di input appropriati per evitare dati non validi
- Fornisci esempi di formato dati e indicazioni per campi complessi
- Audit periodico della qualità dei dati trasmessi e dell’efficacia della convalida

## Best practice per la sicurezza e la conformità

### Protezione dei dati

**Privacy per progettazione**

- Raccogli solo i dati minimi necessari per lo scopo aziendale
- Implementa criteri appropriati di conservazione ed eliminazione dei dati
- Fornisci avvisi chiari sulla privacy e meccanismi di consenso
- Garantisci la conformità alle normative sulla protezione dei dati (GDPR, CCPA, ecc.)

**Implementazione della sicurezza**

- Utilizza la crittografia HTTPS per tutti gli invii di moduli e la trasmissione di dati
- Implementa la corretta bonifica e convalida dell’input
- Configura il caricamento sicuro dei file con le restrizioni appropriate e la scansione antivirus
- Controlli di sicurezza regolari e valutazioni delle vulnerabilità

### Considerazioni sulla conformità

**Requisiti normativi**

- Comprendi e implementa i requisiti di conformità specifici del settore
- Documenta le misure di conformità a scopo di controllo
- Revisione regolare delle modifiche normative e del loro impatto sui moduli
- Formazione del personale sull’implementazione e sui requisiti di conformità

**Conformità all’accessibilità**

- Segui le linee guida WCAG 2.1 AA per l’accessibilità
- Test di accessibilità regolari con tecnologie per l’accessibilità
- Test degli utenti con persone affette da disabilità
- Documentazione delle funzioni di accessibilità e delle misure di conformità

## Best practice per la collaborazione tra team

### Documentazione e condivisione delle conoscenze

**Documentazione del modulo**

- Mantieni chiara la documentazione relativa a scopi, requisiti e regole aziendali dei moduli
- Documenta endpoint di integrazione, flussi di dati e dipendenze
- Mantieni la cronologia delle versioni e i registri di modifica per gli aggiornamenti dei moduli
- Condividi best practice e insegnamenti appresi tra i team

**Formazione e adozione**

- Fornisci formazione ai membri del gruppo sulle funzionalità di Forms Experience Builder
- Stabilisci linee guida per una creazione dei moduli coerente in tutta l’organizzazione
- Sessioni regolari di condivisione delle conoscenze per nuove funzioni e best practice
- Programmi di mentorato per nuovi utenti della piattaforma

### Garanzia di qualità

**Processi di revisione**

- Implementa processi di revisione tra pari per la progettazione e l’implementazione dei moduli
- Stabilisci protocolli di test per la funzionalità dei moduli e l’esperienza utente
- Controlli regolari dei moduli esistenti per ottimizzare le opportunità
- Raccolta di feedback sia dagli utenti interni che dagli utenti finali

**Standard e linee guida**

- Sviluppa standard organizzativi per la progettazione e l’implementazione dei moduli
- Crea modelli e linee guida per i tipi di modulo comuni
- Stabilisci processi di approvazione per i nuovi moduli e le modifiche principali
- Revisione e aggiornamento regolari degli standard organizzativi

## Best practice avanzate

### Campi avanzati migliorati con LLM

**Sfruttare la conoscenza IA**

- Utilizza le conoscenze incorporate dell’intelligenza artificiale per opzioni di campo complete
- Richiedi campi avanzati per dati geografici, classificazioni aziendali e standard di settore
- Implementa la popolazione di campo intelligente per migliorare l’esperienza utente
- Testa la precisione e la completezza dei campi avanzati per i casi d’uso specifici

**Esempi di campi avanzati**

    “Aggiungi un campo aeroporto di partenza con tutti i principali aeroporti del mondo, inclusi i codici IATA”
    “Crea un campo settore completo utilizzando la classificazione NAICS standard”
    “Includi un elenco a discesa di certificazione professionale che si adatta in base al campo del lavoro”

### Logica modulo avanzata

**Regole di business complesse**

- Suddividi la logica di business complessa in componenti più piccoli e testabili
- Documenta chiaramente i requisiti delle regole aziendali prima dell’implementazione
- segui un test approfondito dei casi edge e degli scenari di eccezione
- Fornisci un feedback chiaro agli utenti per le violazioni delle regole di business

**Comportamento del modulo dinamico**

- Utilizza la divulgazione progressiva per mostrare i campi pertinenti in base al contributo dell’utente
- Implementa impostazioni predefinite intelligenti che possono essere sovrascritte dagli utenti
- Crea moduli adattivi che si modificano in base al comportamento e alle preferenze degli utenti
- Trova un equilibrio di automatizzazione tra controllo degli utenti e trasparenza

## Convalida e verifica

### Strategia di test completa

**Test a diversi livelli**

- Test unitario per singoli componenti del modulo e regole di convalida
- Test di integrazione per endpoint di invio e flussi di dati
- Test di accettazione utente con gruppi di utenti rappresentativi
- Test delle prestazioni in varie condizioni di carico

**Convalida tra piattaforme**

- Testa i moduli in diversi browser e versioni
- Convalida l’esperienza mobile su vari dispositivi e dimensioni dello schermo
- Testa l’accessibilità con diverse tecnologie per l’accessibilità
- Test delle condizioni di rete per varie velocità di connessione

### Metriche di qualità

**Indicatori di successo**

- Tassi di completamento dei moduli superiori ai benchmark di settore
- Tassi di errore bassi e punteggi di soddisfazione degli utenti elevati
- Tempi di caricamento rapidi e interazioni utente dinamiche
- Integrazione efficace con i sistemi e i processi di back-end

**Monitoraggio continuo**

- Revisione regolare delle metriche delle prestazioni dei moduli e del feedback degli utenti
- Identificazione e risoluzione proattiva dei problemi
- Analisi delle tendenze per l’utilizzo e l’efficacia dei moduli
- Analisi comparativa rispetto agli standard di settore e alle best practice

Per ulteriori informazioni ed esempi dettagliati, consulta la [Guida introduttiva di Forms Experience Builder](forms-ai-assistant-getting-started.md) e la [Libreria di prompt di Forms Experience Builder](ai-assistant-prompt-library.md).
