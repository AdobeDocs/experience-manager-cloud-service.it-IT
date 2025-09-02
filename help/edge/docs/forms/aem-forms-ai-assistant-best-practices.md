---
title: Forms Experience Builder - Procedure consigliate
description: Best practice complete per la creazione di moduli efficaci con Forms Experience Builder, che includono progettazione, esperienza utente, prestazioni e coerenza del marchio.
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: fe34b44d02c308e7d18a08dd05f21abc67bd0cb2
workflow-type: tm+mt
source-wordcount: '2072'
ht-degree: 0%

---


# Forms Experience Builder - Procedure consigliate

>[!NOTE]
>
> Forms Experience Builder è disponibile nell&#39;ambito del programma per gli utenti meno esperti. Invia un&#39;e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com` per richiedere l&#39;accesso.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifica**: questa guida alle best practice è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. Le best practice, i consigli e gli esempi possono cambiare man mano che Forms Experience Builder continua a evolvere durante il primo programma di adozione.

Questa guida completa fornisce best practice collaudate per la creazione di moduli efficaci e intuitivi tramite Forms Experience Builder. Queste pratiche derivano da implementazioni di successo e feedback degli utenti in vari settori e casi d’uso.

## Best practice per la progettazione dei moduli

### Semplifica

**Inizia con campi essenziali**

- Inizia con solo le informazioni più necessarie per ridurre il sovraccarico degli utenti
- Aggiunta graduale della complessità in base alle esigenze degli utenti e ai requisiti aziendali
- Evita di chiedere informazioni che non usi realmente
- Considera il tempo e il carico cognitivo dell’utente durante la progettazione dei moduli

**Usa etichette chiare e descrittive**

- Rendi immediatamente visibili gli scopi del campo con etichette descrittive
- Evita il gergo tecnico o la terminologia interna che gli utenti non comprenderanno
- Utilizzare convenzioni di etichettatura coerenti in tutti i moduli
- Fornisci contesto quando i requisiti del campo potrebbero non essere evidenti

**Fornisci indicazioni utili**

- Includi testo della guida per campi complessi con esempi e requisiti di formattazione
- Utilizza il testo segnaposto per visualizzare i formati di input previsti
- Fornisci istruzioni chiare per il caricamento dei file, inclusi i formati accettati e i limiti di dimensione
- Guida gli utenti attraverso processi in più fasi con indicatori di avanzamento

**Verifica approfondita**

- Convalida tutti i percorsi utente e gli scenari prima della distribuzione
- Test dei moduli con utenti reali del pubblico di destinazione
- Verifica che tutta la logica condizionale funzioni come previsto
- Assicurati che la gestione degli errori fornisca feedback chiari e fruibili

### Divulgazione progressiva

**Mostra campi rilevanti in base al contesto**

- Visualizza campi aggiuntivi solo quando sono rilevanti per le selezioni dell&#39;utente
- Utilizza la logica condizionale per ridurre il carico cognitivo e la lunghezza del modulo
- Raggruppare i campi correlati in sezioni logiche
- Nascondi opzioni avanzate finché gli utenti non ne indicano la necessità

**Implementazione di esempio:**

    Crea una regola che mostri @spouseInformation pannello solo quando @maritalStatus è uguale a &quot;Sposato&quot;

**Cancella navigazione e avanzamento**

- Aiutare gli utenti a capire la posizione in cui si trovano nei moduli in più passaggi
- Fornire una navigazione chiara tra le sezioni del modulo
- Mostra indicatori di avanzamento per moduli più lunghi
- Consenti agli utenti di salvare l&#39;avanzamento e tornare in un secondo momento

## Best practice per l’esperienza utente

### Design primo dispositivo mobile

**Ottimizzazione layout reattivo**

- Progettare moduli con utenti mobili come considerazione principale
- Utilizzare layout a colonna singola per dispositivi mobili
- Assicurati che le dimensioni delle destinazioni di contatto siano appropriate (minimo 44 px)
- Test dei moduli su dispositivi di varie dimensioni e orientamenti

**Interazioni Touch-Friendly**

- Implementazione di pulsanti più grandi e campi di input per le interfacce touch
- Utilizza tipi di input appropriati per attivare le tastiere corrette per i dispositivi mobili
- Evitare interazioni dipendenti dal passaggio del mouse che non funzionano sui dispositivi touch
- Fornire un feedback visivo chiaro per le interazioni degli utenti

### Conformità all’accessibilità

**Linee guida WCAG 2.1**

- Segui le linee guida per l’accessibilità dei contenuti web per una progettazione inclusiva
- Verificare che i rapporti di contrasto dei colori siano corretti (minimo 4,5:1 per il testo normale)
- Fornisci testo alternativo per tutte le immagini e le icone
- Implementare una corretta struttura del titolo e un HTML semantico

**Navigazione da tastiera**

- Assicurati che tutti gli elementi del modulo siano accessibili tramite navigazione da tastiera
- Fornire indicatori di focus chiari per tutti gli elementi interattivi
- Implementare l&#39;ordine di tabulazione logico tramite i campi modulo
- Includi collegamenti di spostamento per moduli complessi

**Supporto Reader per schermo**

- Utilizza le etichette ARIA e le descrizioni corrette per i campi modulo
- Fornire messaggi di errore chiari che vengono annunciati agli assistenti vocali
- Assicurati che le modifiche ai contenuti dinamici vengano annunciate correttamente
- Test dei moduli con il software per la lettura dello schermo

### Ottimizzazione delle prestazioni

**Velocità di caricamento**

- Ottimizzazione dei tempi di caricamento dei moduli riducendo al minimo le dimensioni iniziali del bundle
- Implementare il caricamento lento per le sezioni di moduli non critici
- Ottimizzare immagini e risorse per la distribuzione web
- Abilitare strategie di caching appropriate per le risorse statiche

**Prestazioni runtime**

- Utilizza tempi di convalida appropriati per bilanciare l’esperienza utente e le prestazioni
- Implementazione del debouncing per la convalida in tempo reale per ridurre le richieste dei server
- Memorizza nella cache i dati a cui si accede di frequente e i risultati della convalida
- Ottimizzare l’esecuzione della logica condizionale per i moduli complessi

**Salvataggio automatico e protezione dei dati**

- Implementa il salvataggio automatico dell’avanzamento del modulo per evitare la perdita di dati
- Fornisci funzionalità offline, ove possibile, per il completamento del modulo
- Includi logica per nuovi tentativi per invii non riusciti
- Opzioni di esportazione dei dati dell&#39;offerta come backup per gli utenti

## Best practice per la coerenza del marchio

### Preparare Brand Assets in anticipo

**Crea modelli marchio**

- Sviluppo di modelli di modulo standardizzati con l&#39;identità visiva dell&#39;organizzazione
- Includi combinazioni di colori, composizione tipografica e motivi di layout coerenti
- Prepara componenti riutilizzabili che corrispondano alle linee guida del tuo marchio
- Documenta gli standard di stile per un’implementazione coerente tra i team

**Definisci linee guida per gli stili**

- Definizione di stili di campo, progettazioni di pulsanti e standard di spaziatura coerenti
- Creare una guida di stile che includa codici colore, specifiche dei caratteri e regole di layout
- Definire i pattern di interazione e le linee guida di animazione
- Preparare messaggi di errore e testo di aiuto specifici per il brand

**Genera libreria componenti**

- Creare componenti modulo riutilizzabili che corrispondono alla tua brand identity
- Sviluppare modelli di navigazione ed elementi dell’interfaccia utente coerenti
- Prepara icone con marchio, logo e risorse visive per l’integrazione dei moduli
- Stabilire modelli per i tipi di modulo comuni (contatto, registrazione, feedback)

### Strategie di implementazione del brand

**Richieste di stile per coerenza**

Includi istruzioni specifiche per il tuo marchio nei prompt:

    Crea un modulo per i contatti professionali utilizzando:
    - Blu aziendale (#003366) per i pulsanti e le intestazioni principali
    - Famiglia di caratteri Open Sans per tutti gli elementi di testo
    - Dimensione minima dei caratteri di 16 px per la conformità in materia di accessibilità
    - Spaziatura coerente di 24 px tra le sezioni del modulo
    - Logo aziendale nell&#39;intestazione con il corretto posizionamento del marchio

**Gestione libreria modelli**

- Gestisci una raccolta di modelli di modulo con marchio per casi d’uso comuni
- Controllo della versione dei modelli di marchio per garantire la coerenza
- Fornisci una documentazione chiara per l’utilizzo e la personalizzazione dei modelli
- Revisione e aggiornamento regolari delle risorse del brand per mantenere gli standard attuali

>[!NOTE]
>
>**Componenti personalizzati**: prima di implementare elementi del brand personalizzati, rivolgiti al tuo team di sviluppo per informazioni sull&#39;utilizzo di componenti specifici dell&#39;organizzazione e sulla loro compatibilità con Forms Experience Builder.

## Best practice per contenuti e comunicazioni

### Approcci per la creazione di moduli

**Due metodi primari**

Scegli il metodo di creazione più appropriato alle tue esigenze:

1. **Crea da zero**: ideale per i nuovi moduli con requisiti specifici
2. **Importa e converti**: ideale per modernizzare moduli e documenti esistenti

**Prompt Lingua Naturale**

- Specifici e dettagliati nelle descrizioni del modulo
- Utilizza un linguaggio chiaro e orientato alle aziende piuttosto che termini tecnici
- Fornire contesto sullo scopo del modulo e sul pubblico di destinazione
- Includere i requisiti di convalida e delle regole business nei prompt iniziali

### Strategia di sviluppo incrementale

**Avvio semplice, complessità della compilazione**

- Inizia con la struttura del modulo di base e i campi essenziali
- Aggiungere regole di convalida e logica di business in modo incrementale
- Verifica ogni aggiunta prima di procedere al miglioramento successivo
- Raccogliere feedback degli utenti in ogni fase dello sviluppo

**Esempio di approccio incrementale:**

    Passaggio 1: &quot;Crea un modulo di contatto di base con campi nome, e-mail e messaggio&quot;
    Passaggio 2: &quot;Rendi @name e @email i campi obbligatori con la convalida appropriata&quot;
    Passaggio 3: &quot;Aggiungi testo segnaposto e testo della guida per le indicazioni dell&#39;utente&quot;
    Passaggio 4: &quot;Aggiungi logica condizionale in base al tipo di richiesta&quot;

### Best practice di riferimento sul campo

**Convenzioni di denominazione coerenti**

- Utilizza nomi di campo chiari e descrittivi corrispondenti al loro scopo
- Mantenere modelli di denominazione coerenti tra i moduli
- Utilizza camelCase o snake_case in modo coerente in tutte le tue forme
- Convenzioni di denominazione dei campi del documento per coerenza team

**Riferimenti campo effettivi**

- Usa la sintassi `@fieldName` per modificare i campi esistenti
- Specifica a quali campi fare riferimento nei moduli complessi
- Raggruppare le modifiche dei campi correlate in singole richieste
- Verifica i nomi dei campi prima di utilizzarli nella logica condizionale

## Best practice per l’integrazione e l’invio

### Strategia di invio multicanale

**Azioni primarie e secondarie**

- Configurare gli endpoint di invio principali per i processi aziendali principali
- Impostare azioni secondarie per notifiche, conferme e backup dei dati
- Implementare la gestione degli errori e la logica dei tentativi per gli invii non riusciti
- Fornire feedback agli utenti per tutti gli stati di invio (operazione riuscita, errore, elaborazione)

**Pianificazione integrazione**

- Iniziare con la configurazione di base dell’invio e aggiungere integrazioni in modo incrementale
- Testare ogni integrazione separatamente prima di combinare più endpoint
- Documentare i requisiti API e i metodi di autenticazione
- Pianificare la trasformazione dei dati e i requisiti di mappatura

### Gestione e recupero degli errori

**Messaggi di errore descrittivi**

- Fornire messaggi di errore chiari e actionable che aiutino gli utenti a risolvere i problemi
- Evita codici di errore tecnico o messaggi di sistema nel contenuto rivolto all’utente
- Offrire azioni alternative quando l’invio primario non riesce
- Includi informazioni di contatto per gli utenti che necessitano di ulteriore assistenza

**Protezione e ripristino dei dati**

- Implementare il salvataggio locale dei dati per il recupero dei moduli dopo gli errori
- Fornire agli utenti le opzioni per scaricare i dati del modulo come backup
- Impostare il monitoraggio e gli avvisi per gli errori di invio
- Pianificare le procedure di ripristino in caso di interruzioni o manutenzione del sistema

## Best practice per prestazioni e analisi

### Monitoraggio e ottimizzazione

**Metriche prestazioni chiave**

- Tracciare i tassi di completamento dei moduli e i punti di abbandono
- Monitorare i tempi di caricamento e i modelli di interazione dell’utente
- Misurare l’efficacia della convalida e i tassi di errore
- Analizzare il feedback degli utenti e i punteggi di soddisfazione

**Miglioramento continuo**

- Revisione regolare dell’analisi dei moduli per identificare le opportunità di ottimizzazione
- Test A/B di diverse progettazioni di moduli e flussi utente
- Raccolta e analisi dei feedback degli utenti per miglioramenti iterativi
- Analisi comparativa delle prestazioni rispetto agli standard di settore

### Qualità dei dati e convalida

**Strategie di convalida avanzate**

- Implementazione della convalida in tempo reale per un feedback immediato degli utenti
- Utilizzare la convalida progressiva per guidare gli utenti attraverso requisiti complessi
- Fornire messaggi di convalida chiari che spieghino come correggere gli errori
- Equilibrio tra rigidità della convalida e considerazioni sull’esperienza utente

**Integrità dei dati**

- Implementare la convalida tra campi diversi per garantire la coerenza dei dati
- Utilizza tipi e vincoli di input appropriati per evitare dati non validi
- Fornisci esempi di formato dati e indicazioni per campi complessi
- Audit periodico della qualità dei dati trasmessi e dell’efficacia della convalida

## Best practice per la sicurezza e la conformità

### Protezione dei dati

**Privacy per progettazione**

- Raccogliere solo i dati minimi necessari per lo scopo aziendale
- Implementare criteri appropriati di conservazione ed eliminazione dei dati
- Fornire avvisi chiari sulla privacy e meccanismi di consenso
- Garantire la conformità alle normative sulla protezione dei dati (GDPR, CCPA, ecc.)

**Implementazione della sicurezza**

- Usa la crittografia HTTPS per tutte le richieste di modulo e la trasmissione dei dati
- Implementare la corretta convalida e bonifica degli input
- Configurare il caricamento sicuro dei file con le restrizioni e la scansione antivirus appropriate
- Controlli di sicurezza periodici e valutazioni delle vulnerabilità

### Considerazioni sulla conformità

**Requisiti normativi**

- Comprendere e implementare i requisiti di conformità specifici del settore
- Documentare le misure di conformità a scopo di audit
- Revisione regolare delle modifiche normative e del loro impatto sui moduli
- Formazione del personale sui requisiti di conformità e sull&#39;implementazione

**Conformità all&#39;accessibilità**

- Seguire le linee guida WCAG 2.1 AA per l’accessibilità
- Test regolari di accessibilità con tecnologie per l’accessibilità
- Test degli utenti con utenti disabili
- Documentazione delle funzioni di accessibilità e delle misure di conformità

## Best practice per Team Collaboration

### Documentazione e condivisione delle conoscenze

**Documentazione modulo**

- Documentazione chiara relativa a scopi, requisiti e regole aziendali dei moduli
- Documenta endpoint di integrazione, flussi di dati e dipendenze
- Mantieni la cronologia delle versioni e i registri di modifica per gli aggiornamenti dei moduli
- Condividere best practice ed esperienze tra i vari team

**Formazione e adozione**

- Formazione dei membri del gruppo sulle funzionalità di Forms Experience Builder
- Stabilire linee guida per una creazione dei moduli coerente in tutta l’organizzazione
- Sessioni regolari di condivisione delle conoscenze per nuove funzioni e best practice
- Programmi di mentoring per nuovi utenti della piattaforma

### Controllo qualità

**Processi di revisione**

- Implementare processi di revisione tra pari per la progettazione e l’implementazione dei moduli
- Definizione dei protocolli di test per la funzionalità dei moduli e l’esperienza utente
- Audit regolari dei moduli esistenti per ottimizzare le opportunità
- Raccolta di feedback sia dagli utenti interni che dagli utenti finali

**Standard e linee guida**

- Sviluppare standard organizzativi per la progettazione e l&#39;implementazione di moduli
- Creare modelli e linee guida per i tipi di modulo più comuni
- Definizione dei processi di approvazione per i nuovi moduli e le modifiche principali
- Revisione e aggiornamento periodici degli standard organizzativi

## Best practice avanzate

### Campi avanzati migliorati LLM

**Utilizzo della conoscenza di IA**

- Utilizza le conoscenze integrate dell’intelligenza artificiale per opzioni di campo complete
- Richiedi campi avanzati per dati geografici, classificazioni aziendali e standard di settore
- Implementare la popolazione di campo intelligente per migliorare l’esperienza utente
- Verifica la precisione e la completezza intelligenti dei campi per i casi d’uso specifici

**Esempi di campi avanzati**

    &quot;Aggiungere un campo aeroporto di partenza con tutti i principali aeroporti del mondo, inclusi i codici IATA&quot;
    &quot;Creare un campo settore completo utilizzando la classificazione NAICS standard&quot;
    &quot;Includere un elenco a discesa di certificazione professionale che si adatta in base al campo del lavoro&quot;

### Logica modulo avanzata

**Regole aziendali complesse**

- Suddividere la logica di business complessa in componenti più piccoli e testabili
- Documentare chiaramente i requisiti delle regole aziendali prima dell&#39;implementazione
- Test approfondito dei casi edge e degli scenari di eccezione
- Fornire un feedback chiaro agli utenti per le violazioni delle regole di business

**Comportamento modulo dinamico**

- Utilizzare la divulgazione progressiva per mostrare i campi pertinenti in base al contributo dell’utente
- Implementare impostazioni predefinite intelligenti che possono essere ignorate dagli utenti
- Creare moduli adattivi che si adattano in base al comportamento e alle preferenze degli utenti
- Automatizzazione del bilanciamento con controllo degli utenti e trasparenza

## Convalida e verifica

### Strategia di test completa

**Test multilivello**

- Test di unità per singoli componenti del modulo e regole di convalida
- Test di integrazione per endpoint di invio e flussi di dati
- Test di accettazione utente con gruppi di utenti rappresentativi
- Test delle prestazioni in varie condizioni di carico

**Convalida tra piattaforme**

- Testare i moduli in diversi browser e versioni
- Convalidare l’esperienza mobile su vari dispositivi e dimensioni dello schermo
- Test di accessibilità con diverse tecnologie per l’accessibilità
- Test delle condizioni di rete per varie velocità di connessione

### Metriche di qualità

**Indicatori di successo**

- Tassi di completamento dei moduli superiori ai benchmark di settore
- Tassi di errore bassi e punteggi di soddisfazione degli utenti elevati
- Tempi di caricamento rapidi e interazioni utente dinamiche
- Integrazione efficace con i sistemi e i processi back-end

**Monitoraggio continuo**

- Revisione regolare delle metriche delle prestazioni dei moduli e del feedback degli utenti
- Identificazione e risoluzione proattiva dei problemi
- Analisi delle tendenze per l’utilizzo e l’efficacia dei moduli
- Analisi comparativa rispetto agli standard di settore e alle best practice

Per ulteriori informazioni ed esempi dettagliati, consultare la [Guida introduttiva di Forms Experience Builder](forms-ai-assistant-getting-started.md) e la [Libreria prompt di Forms Experience Builder](ai-assistant-prompt-library.md).
