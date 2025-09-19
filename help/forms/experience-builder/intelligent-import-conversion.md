---
title: Importazione e conversione intelligenti
description: Scopri come trasformare documenti, PDF e immagini esistenti in moduli digitali interattivi utilizzando le funzionalità intelligenti di importazione e conversione di Forms Experience Builder.
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: de524aeddd5f53cbd713ff0523222966752ebbc0
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 0%

---


# Importazione e conversione intelligenti

>[!NOTE]
>
> Forms Experience Builder è disponibile in un programma di accesso anticipato. Prima di iniziare, assicurati di aver richiesto e ottenuto l’accesso.

La funzione intelligente di importazione e conversione di Forms Experience Builder consente di trasformare documenti, PDF e immagini esistenti in moduli digitali interattivi moderni tramite l’analisi e la conversione basate sull’intelligenza artificiale.

## Formati di origine supportati

### Documenti PDF

**PDF AcroForm:**

- PDF forms interattivo con campi modulo
- PDF statici con layout simili a moduli
- Documenti multipagina con contenuti strutturati

**PDF basati su XFA:**

- Moduli XFA (XML Forms Architecture) legacy
- Moduli aziendali complessi con layout avanzati
- Moduli governativi ed aziendali

**PDF statici:**

- Documenti e moduli digitalizzati
- Moduli pronti per la stampa senza elementi interattivi
- Documenti con strutture simili a moduli

### File immagine

**Formati supportati:**

- PNG, JPG, JPEG, GIF
- Scansioni ad alta risoluzione di moduli cartacei
- Schermate di moduli digitali
- sketch e wireframe disegnati a mano

**Requisiti di qualità immagine:**

- Minimo 300 DPI per il riconoscimento del testo
- Testo ed elementi modulo chiari e leggibili
- Buon contrasto tra testo e sfondo
- Orientamento corretto (non ruotato)

### Progettare i file

**Progettazioni Figma:**

- Modelli di moduli e prototipi
- File di progettazione UI/UX
- Layout dei moduli basati su componenti

**Altri formati di progettazione:**

- File Adobe XD
- Disegni di sketch
- Documenti wireframe

## Importare e convertire

### Passaggio 1: accedere alla funzione di importazione

1. Apri Forms Experience Builder
2. Fai clic sull’icona dell’allegato nell’interfaccia di
3. Seleziona l’opzione &quot;Importa e converti&quot;
4. Scegli il file di origine

### Passaggio 2: Caricare il documento

**Per i file PDF:**

1. Seleziona il documento PDF
2. Attendi che l’intelligenza artificiale analizzi la struttura
3. Esamina gli elementi modulo rilevati
4. Conferma le impostazioni di conversione

**Per i file di immagine:**

1. Carica l’immagine (PNG, JPG, ecc.)
2. L’intelligenza artificiale analizzerà il layout e il testo
3. Esamina i campi modulo rilevati
4. Se necessario, apporta le modifiche necessarie

**Per i file di progettazione:**

1. Carica il file di progettazione
2. L’intelligenza artificiale estrarrà i componenti del modulo
3. Esaminare gli elementi convertiti
4. Personalizzare la struttura del modulo

### Passaggio 3: rivedere e personalizzare

Dopo la conversione iniziale:

1. **Controlla i campi rilevati**: verifica che tutti gli elementi del modulo siano identificati correttamente
2. **Regola tipi di campo**: modifica tipi di campo (testo, elenco a discesa, casella di controllo e così via)
3. **Aggiungi convalida**: imposta le regole di convalida del campo
4. **Personalizza stile**: applica temi e branding
5. **Funzionalità di test**: verifica del comportamento e della logica del modulo

## Esempi di conversione

### Conversione modulo PDF

**Modulo PDF originale:**

- Modulo di contatto statico con nome, e-mail, campi telefono
- Sezione Informazioni aziendali
- Area Commenti

**Modulo adattivo convertito:**

- Campi di testo interattivo con convalida
- Elenco a discesa per dimensione società
- Area di testo su più righe per i commenti
- Pulsante Invia con integrazione e-mail

### Conversione da immagine a modulo

**Immagine originale:**

- Foto di un modulo di registrazione cartaceo
- Modulo scritto a mano con caselle di controllo
- Più sezioni per informazioni diverse

**Modulo adattivo convertito:**

- Campi di testo digitale corrispondenti al layout
- Caselle di controllo interattive e pulsanti di scelta
- Sezioni organizzate con spaziatura adeguata
- Progettazione adattabile ai dispositivi mobili

### Conversione del file di progettazione

**Progettazione Figma originale:**

- Modello moderno dell’interfaccia utente con componenti modulo
- Stile e colori del marchio
- Layout complesso con più pannelli

**Modulo adattivo convertito:**

- Riproduzione perfetta dei pixel del design
- Elementi modulo interattivi
- Comportamento reattivo tra dispositivi
- Stile coerente con il marchio

## Funzioni di conversione avanzate

### Rilevamento intelligente dei campi

L’intelligenza artificiale rileva e converte automaticamente:

- **Campi di testo**: aree di testo a riga singola e a più righe
- **Campi di selezione**: elenchi a discesa, pulsanti di scelta, caselle di controllo
- **Campi data**: selettori data con formattazione corretta
- **Campi numerici**: input numerici con convalida
- **Caricamenti di file**: aree di caricamento di documenti e immagini

### Mantenimento layout

La conversione mantiene:

- **Struttura originale**: mantiene il layout e l&#39;organizzazione
- **Gerarchia visiva**: mantiene intestazioni e interruzioni di sezione
- **Spaziatura e allineamento**: mantiene la spaziatura corretta del modulo
- **Elementi marchio**: mantiene logo ed elementi di stile

### Convalida intelligente

Aggiunge automaticamente la convalida appropriata:

- **Campi e-mail**: convalida del formato e-mail
- **Numeri di telefono**: convalida formato numero di telefono
- **Campi obbligatori**: contrassegna i campi obbligatori come evidenti
- **Intervalli di date**: imposta vincoli di data appropriati

## Best practice per l’importazione e la conversione

### Preparazione dei documenti di origine

**Per i file PDF:**

- Assicurati che il testo sia selezionabile (non solo immagini)
- Utilizzare scansioni di alta qualità per PDF statici
- Organizzare il contenuto nelle sezioni logiche
- Includi etichette di campo non crittografate

**Per le immagini:**

- Usa immagini ad alta risoluzione (oltre 300 DPI)
- Assicurare un buon contrasto e una buona leggibilità
- Evitare le immagini ruotate o inclinate
- Includi tutti gli elementi modulo nell&#39;immagine

**Per i file di progettazione:**

- Utilizza una denominazione coerente per i componenti del modulo
- Organizzare i livelli logicamente
- Includi tutti gli elementi modulo necessari
- Esportazione di alta qualità

### Ottimizzazione post-conversione

**Revisione e test:**

- Verifica di tutti i campi modulo e convalida
- Verificare la reattività mobile
- Verifica conformità accessibilità
- Test della funzionalità di invio

**Personalizza e migliora:**

- Aggiungere regole business e regole condizionali
- Implementare una corretta gestione degli errori
- Configurare gli endpoint di invio
- Applicare lo stile e i temi del brand

## Risoluzione dei problemi di conversione

### Problemi comuni

**Rilevamento campo non valido:**

- Migliorare la qualità delle immagini o la chiarezza del testo in PDF
- Regola manualmente i tipi di campo dopo la conversione
- Usa etichette di campo più descrittive nell’origine

**Problemi di layout:**

- Regolare manualmente la spaziatura e l&#39;allineamento
- Utilizzare i principi di progettazione reattiva
- Eseguire il test su schermi di dimensioni diverse

**Elementi mancanti:**

- Aggiungi manualmente i campi mancanti
- Reimportare con una migliore qualità dell&#39;origine
- Utilizza approccio di conversione incrementale

### Ottenere aiuto

Per problemi di conversione:

- Controlla le [domande frequenti su Forms Experience Builder](forms-experience-builder-frequently-asked-questions.md)
- Rivedi la [Guida introduttiva](forms-experience-builder-getting-started.md)
- Contatta l’amministratore di sistema per assistenza tecnica

## Articoli correlati

- [Panoramica di Forms Experience Builder](product-overview.md)
- [Guida introduttiva di Forms Experience Builder](forms-experience-builder-getting-started.md)
- [Implementare e configurare Forms Experience Builder](deploy-forms-experience-builder.md)
- [Invio e integrazione di moduli](form-submission-integration.md)
- [Domande frequenti](forms-experience-builder-frequently-asked-questions.md)
