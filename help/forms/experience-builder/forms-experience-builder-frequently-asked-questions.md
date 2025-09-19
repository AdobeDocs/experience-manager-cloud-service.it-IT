---
title: Forms Experience Builder - Domande frequenti
description: Risposte alle domande comuni su Forms Experience Builder, incluse configurazione, utilizzo, risoluzione dei problemi e best practice.
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: de524aeddd5f53cbd713ff0523222966752ebbc0
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 1%

---


# Forms Experience Builder - Domande frequenti

>[!NOTE]
>
> Forms Experience Builder è disponibile in un programma di accesso anticipato. Prima di iniziare, assicurati di aver richiesto e ottenuto l’accesso.

Queste domande frequenti riguardano le domande più comuni su Forms Experience Builder, dalla configurazione di base alle funzioni avanzate e alla risoluzione dei problemi.

## Domande generali

### Cos’è Forms Experience Builder?

Forms Experience Builder è uno strumento per la creazione di moduli basato sull’intelligenza artificiale che consente di creare moduli digitali sofisticati utilizzando un linguaggio di conversazione. Invece delle tradizionali interfacce di trascinamento o della codifica complessa, puoi semplicemente descrivere ciò che desideri e l’intelligenza artificiale crea il modulo per te.

### Chi può utilizzare Forms Experience Builder?

Forms Experience Builder è progettato per:

- **Creatori di moduli** che desiderano creare moduli in modo rapido ed efficiente
- **Utenti aziendali** che devono creare moduli senza competenze tecniche
- **Sviluppatori** che desiderano sfruttare l&#39;intelligenza artificiale per la creazione rapida di prototipi di moduli
- **Amministratori** che devono configurare e gestire i flussi di lavoro per la creazione di moduli

### Forms Experience Builder è disponibile per tutti i clienti AEM Forms?

Forms Experience Builder è attualmente disponibile tramite un programma di accesso anticipato. Contatta il tuo rappresentante Adobe per richiedere l’accesso e scopri cosa significa la disponibilità per la tua organizzazione.

## Configurazione e configurazione

### Quali sono i prerequisiti per utilizzare Forms Experience Builder?

Prima di utilizzare Forms Experience Builder, assicurati di disporre di:

- Accesso a Forms Experience Builder tramite il programma di accesso anticipato
- AEM Forms as a Cloud Service con componenti core Forms adattivi
- Nozioni di base sui concetti di forma e sui requisiti aziendali

Per i requisiti tecnici di configurazione dettagliati, vedere [Distribuire e configurare Forms Experience Builder](deploy-forms-experience-builder.md).

### Come si abilita Forms Experience Builder nel proprio ambiente?

La configurazione di Forms Experience Builder dipende dall’implementazione di AEM Forms:

**Per Edge Delivery Services:**

- Prepara il progetto per Edge Delivery Services Forms
- Abilitare Forms Experience Builder nell’editor universale

**Per moduli basati su Componenti core:**

- Assicurati che i componenti core adattivi di Forms siano abilitati
- Configurare Forms Experience Builder nell’editor di Forms adattivo

### Posso utilizzare Forms Experience Builder con i moduli esistenti?

Sì, Forms Experience Builder può funzionare con i moduli esistenti in diversi modi:

- Importa e converti PDF forms esistente
- Migliorare i moduli adattivi esistenti con funzioni basate sull’intelligenza artificiale
- Aggiungere campi intelligenti alle strutture del modulo correnti

## Creazione di moduli

### Come creare il primo modulo?

Inizia con una semplice descrizione di ciò che desideri:

    Crea un modulo contatto con campi nome, e-mail e messaggio

L’intelligenza artificiale genera la struttura di modulo di base, che puoi quindi migliorare con funzioni aggiuntive, convalida e stile.

### Quali tipi di moduli è possibile creare?

Forms Experience Builder supporta vari tipi di moduli:

- Moduli di contatto e di feedback
- Moduli di registrazione e onboarding
- Moduli di indagine e valutazione
- Moduli in più passaggi con logica condizionale
- Forms con caricamenti di file e convalida complessa

### Posso creare moduli con più passaggi?

Sì, è possibile creare moduli con più passaggi utilizzando il linguaggio naturale:

    Crea un modulo progressivo con 3 passaggi: informazioni personali, preferenze, conferma

L’intelligenza artificiale imposterà automaticamente la struttura del modulo con navigazione tra i passaggi.

### Come si aggiunge la convalida ai campi modulo?

Aggiungi convalida utilizzando i comandi del linguaggio naturale:

    @email un campo obbligatorio con convalida del formato e-mail
    Aggiungi la convalida del formato del numero di telefono USA a @phoneNumber
    Imposta la convalida della validità: deve essere superiore o uguale a 18 anni per @dateOfBirth

## Funzioni avanzate

### Cosa sono i campi avanzati migliorati di LLM?

I campi avanzati migliorati con LLM sono campi modulo intelligenti precompilati con opzioni rilevanti provenienti dalle knowledge base di IA. Ad esempio:

- Menu a discesa dei paesi con tutti i paesi del mondo
- Classificazioni di settore con codici standard
- Dati geografici con stati, città e codici postali

### Come si importano i documenti esistenti nei moduli?

È possibile importare vari tipi di documenti:

- **PDF forms**: carica PDF statici o interattivi
- **Immagini**: carica foto di moduli cartacei o schermate
- **File di progettazione**: importare schemi Figma o altri formati di progettazione

Utilizza l’icona dell’allegato in Forms Experience Builder per caricare il documento e descrivere i requisiti di conversione.

### È possibile integrare i moduli con sistemi esterni?

Sì, Forms Experience Builder supporta diverse opzioni di integrazione:

- Invii e-mail con modelli personalizzati
- Integrazione REST API con servizi esterni
- Integrazione dell’archiviazione cloud (Azure, AWS, Google Cloud)
- Integrazione del flusso di lavoro (Power Automate, flusso di lavoro AEM)

## Risoluzione di problemi

### L&#39;intelligenza artificiale non capisce la mia richiesta. Cosa devo fare?

Prova questi approcci:

- Sii più specifico nella tua descrizione
- Suddividi le richieste complesse in passaggi più piccoli
- Usa riferimenti campo (@fieldName) per le modifiche mirate
- Fornisci esempi chiari di ciò che desideri

### La convalida del modulo non funziona. Come lo riparo?

Controlla questi problemi comuni:

- Verificare che i nomi dei campi corrispondano esattamente (distinzione maiuscole/minuscole)
- Verificare che la sintassi di convalida sia corretta
- Verificare singolarmente le regole di convalida
- Esaminare i messaggi di errore per problemi specifici

### La logica condizionale non si attiva correttamente. Cosa c&#39;è che non va?

Risolvere i problemi relativi alla logica condizionale in base a:

- Assicurarsi che i nomi dei campi siano referenziati correttamente
- Verifica della sintassi e delle condizioni della regola
- Test con diverse combinazioni di input
- Verifica della corrispondenza dei tipi di campo con i requisiti della regola

### Impossibile caricare l&#39;interfaccia. Cosa devo fare?

Prova le soluzioni seguenti:

- Aggiorna il browser e cancella la cache
- Verifica la connessione Internet
- Verifica di disporre delle autorizzazioni di accesso appropriate
- Se i problemi persistono, contatta l’amministratore di sistema

## Best practice

### Come si creano moduli migliori con Forms Experience Builder?

Segui queste best practice:

- **Specificare**: fornire descrizioni dettagliate di ciò che si desidera
- **Inizia semplice**: inizia con la struttura di base e aggiungi gradualmente complessità
- **Verifica completa**: convalida tutte le funzionalità del modulo prima della distribuzione
- **Usa sviluppo incrementale**: compilare i moduli passo dopo passo

### Cosa evitare durante la creazione di moduli?

Evita questi errori comuni:

- Troppo vago nelle descrizioni
- Tentativo di creare tutto contemporaneamente
- Test e convalida ignorati
- Non considerare la reattività mobile

### Come è possibile garantire l&#39;accesso ai moduli?

Forms Experience Builder include funzioni di accessibilità:

- Controllo automatico di conformità WCAG
- Compatibilità con gli assistenti vocali
- Supporto per la navigazione tramite tastiera
- Opzioni modalità di contrasto elevato

## Integrazione e distribuzione

### Come si distribuiscono i moduli creati con Forms Experience Builder?

I Forms creati con Forms Experience Builder seguono i processi di implementazione standard di AEM Forms:

- Pubblicare moduli tramite l’ambiente di authoring AEM
- Configurare gli endpoint per l’invio di moduli
- Impostare i flussi di lavoro di elaborazione dei moduli
- Moduli di prova nell’ambiente di produzione

### Posso personalizzare le risposte e il comportamento di IA?

Sì, puoi configurare vari aspetti:

- Stile di risposta (conciso, dettagliato, bilanciato)
- Preferenze linguistiche e terminologia
- Opzioni di personalizzazione dell&#39;interfaccia
- Impostazioni di accessibilità

### Come è possibile ottenere assistenza con Forms Experience Builder?

Per ulteriore supporto:

- Controlla la [Guida introduttiva](forms-experience-builder-getting-started.md)
- Rivedi la [Guida alla distribuzione e alla configurazione](deploy-forms-experience-builder.md)
- Contattare l&#39;amministratore di sistema
- Contatta il supporto Adobe per problemi tecnici

## Articoli correlati

- [Panoramica di Forms Experience Builder](product-overview.md)
- [Guida introduttiva di Forms Experience Builder](forms-experience-builder-getting-started.md)
- [Implementare e configurare Forms Experience Builder](deploy-forms-experience-builder.md)
- [Campi avanzati migliorati LLM](forms-experience-builder-llm-smart-fields.md)
- [Importazione e conversione intelligenti](intelligent-import-conversion.md)
- [Invio e integrazione di moduli](form-submission-integration.md)
