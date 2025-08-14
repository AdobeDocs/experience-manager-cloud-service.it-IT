---
title: Come configurare una pagina di reindirizzamento o un messaggio di ringraziamento
description: Scopri come gli utenti possono visualizzare un messaggio di ringraziamento o essere reindirizzati a una pagina web che gli autori dei moduli possono configurare durante la creazione del modulo.
feature: Adaptive Forms, Edge Delivery Services
role: User
level: Intermediate
source-git-commit: 07160248d5b5817d155a118475878ce04a687a32
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 0%

---


# Configurare i messaggi di ringraziamento e gli URL di reindirizzamento

Le esperienze successive all’invio influiscono in modo significativo sulla soddisfazione degli utenti e sui tassi di completamento dei moduli. L’Editor universale di Adobe offre opzioni complete per la configurazione di ciò che gli utenti visualizzano dopo l’invio dei moduli, sia tramite messaggi di ringraziamento personalizzati che tramite reindirizzamenti strategici a pagine specifiche.

Questo articolo fornisce indicazioni dettagliate sull’implementazione dei messaggi di ringraziamento e degli URL di reindirizzamento, incluse considerazioni tecniche, best practice e linee guida sull’esperienza utente per massimizzare l’efficacia dell’invio dei moduli.

## Prerequisiti

Prima di configurare le esperienze di post-invio, assicurati di disporre di:

**Configurazione tecnica:**

- Accesso a Universal Editor con le autorizzazioni appropriate
- Modulo adattivo esistente creato nell’editor universale
- Informazioni sui requisiti URL di reindirizzamento della tua organizzazione

**Considerazioni sulla pianificazione:**

- **Strategia messaggi**: definisci il tono, la lunghezza e le informazioni specifiche da includere nei messaggi di ringraziamento
- **Strategia di reindirizzamento**: identifica le pagine di destinazione e assicurati che siano ottimizzate per le esperienze di completamento post-modulo
- **Integrazione di Analytics**: pianifica come tenere traccia delle interazioni utente con messaggi di ringraziamento o destinazioni di reindirizzamento

## Configurare i messaggi di ringraziamento

I messaggi di ringraziamento consentono di confermare immediatamente l’invio corretto del modulo e possono includere contenuto personalizzato, passaggi successivi o informazioni importanti relative all’invio dell’utente.

### Quando utilizzare i messaggi di ringraziamento

I messaggi di ringraziamento funzionano al meglio quando:

- **Riconoscimento semplice**: gli utenti devono essere confermati senza ulteriori requisiti di navigazione
- **Contenuto istruttivo**: è necessario specificare i passaggi successivi o le informazioni importanti
- **Coerenza del marchio**: il messaggio può essere creato per allinearsi allo stile di comunicazione della tua organizzazione
- **Esperienza a pagina singola**: gli utenti devono rimanere nella pagina corrente per la continuità del flusso di lavoro

### Passaggi di implementazione

**1. Accedi alle proprietà del modulo**

Apri il modulo adattivo in Universal Editor e fai clic sull&#39;icona **Modifica proprietà modulo** nella barra degli strumenti. Verrà visualizzata la finestra di dialogo completa delle proprietà del modulo.

**2. Passa alla configurazione di ringraziamento**

Nella finestra di dialogo Proprietà modulo, seleziona la scheda **Grazie** per accedere alle opzioni di configurazione successive all’invio.

**3. Configura visualizzazione messaggio**

Selezionare **Mostra messaggio** dalle opzioni disponibili. In questo modo viene attivato l’editor del contenuto dei messaggi con funzionalità Rich Text.

**4. Crea il contenuto del messaggio**

Nel campo **Contenuto messaggio**, crea il messaggio di ringraziamento utilizzando l&#39;editor Rich Text. L’editor supporta:

- **Formattazione testo**: grassetto, corsivo, sottolineato e colore
- **Elenchi**: elenchi puntati e numerati per organizzare le informazioni
- **Collegamenti**: collegamenti diretti alle risorse rilevanti o ai passaggi successivi
- **Modifica a tutto schermo**: fai clic sull&#39;icona di espansione per ingrandire l&#39;area di lavoro di modifica

### Considerazioni tecniche

**Comportamento visualizzazione messaggio:**

- I messaggi vengono visualizzati in una sovrapposizione modale immediatamente dopo l’invio del modulo
- Il contenuto supporta la formattazione HTML e mantiene la progettazione reattiva
- I messaggi possono essere chiusi dagli utenti o configurati con timer di chiusura automatica

**Linee guida per il contenuto:**

- Mantenere i messaggi concisi fornendo le informazioni necessarie
- Includi i passaggi successivi non crittografati, se appropriato
- Valuta se includere numeri di riferimento o dettagli di conferma
- Assicurati una formattazione semplice e intuitiva

### Esempio di implementazione

    Grazie per aver inviato la richiesta.
    
    La richiesta è stata ricevuta e le è stato assegnato il numero di riferimento #REF-2024-001234.
    
    **Cosa succede dopo:**
    - Riceverai un&#39;e-mail di conferma entro 15 minuti
    - Il nostro team rivedrà l&#39;invio entro 2 giorni lavorativi
    - Ti contatteremo direttamente se sono necessarie ulteriori informazioni
    
    **Per assistenza?** Contatta il nostro team di supporto all&#39;indirizzo support@example.com

## Configurare gli URL di reindirizzamento

Gli URL di reindirizzamento indirizzano automaticamente gli utenti a pagine specifiche dopo l’invio del modulo, consentendo un’integrazione perfetta con i flussi di lavoro esistenti o indirizzando gli utenti a contenuti rilevanti.

### Quando utilizzare gli URL di reindirizzamento

Gli URL di reindirizzamento sono ottimali per:

- **Integrazione del flusso di lavoro**: indirizzamento degli utenti a dashboard, pagine account o passaggi successivi in un processo
- **Consegna dei contenuti**: presentazione di prodotti, servizi o informazioni rilevanti in base alle risposte ai moduli
- **Tracciamento di Analytics**: reindirizzamento a pagine con implementazioni di tracciamento specifiche
- **Processi con più passaggi**: spostamento degli utenti alla fase successiva di flussi di lavoro complessi

### Passaggi di implementazione

**1. Accedi alle proprietà del modulo**

Apri il modulo adattivo in Universal Editor e fai clic sull&#39;icona **Modifica proprietà modulo** per aprire la finestra di dialogo per la configurazione del modulo.

**2. Passa alla configurazione di ringraziamento**

Seleziona la scheda **Grazie** nella finestra di dialogo Proprietà modulo per accedere alle opzioni di configurazione di reindirizzamento.

**3. Abilita funzionalità di reindirizzamento**

Scegli **Reindirizza all&#39;URL** tra le opzioni disponibili per il post-invio.

**4. Configura URL di destinazione**

Immetti l’URL di destinazione nel campo fornito. Il sistema supporta più formati URL per un’implementazione flessibile.

### Opzioni di configurazione URL

**URL assoluti**

Indirizzi web completi, inclusi protocollo e dominio:

    https://www.example.com/thank-you
    https://dashboard.example.com/user/profile

**Percorsi relativi**

Percorsi relativi al dominio corrente:

    /grazie
    /dashboard/profilo-utente
    ../confirmation-page.html

**Riferimenti pagina AEM Sites**

Riferimenti ad altre pagine all’interno dell’implementazione AEM Sites:

    /content/mysite/en/thank-you
    /content/mysite/en/next-steps

### Considerazioni tecniche

**Comportamento di reindirizzamento:**

- I reindirizzamenti si verificano immediatamente dopo l’invio corretto del modulo
- La cronologia del browser include il reindirizzamento per la corretta funzionalità del pulsante Indietro
- La tempistica di reindirizzamento può essere configurata con ritardi opzionali

**Convalida URL:**

- Il sistema convalida il formato URL prima di consentire la configurazione
- Gli URL relativi vengono risolti rispetto al dominio corrente
- Se necessario, gli URL esterni richiedono una configurazione CORS corretta

## Best practice e raccomandazioni

### Linee guida sull’esperienza utente

**Ottimizzazione messaggi:**

- **Chiarezza**: assicurati che gli utenti comprendano immediatamente che l&#39;invio è stato eseguito correttamente
- **Valore aggiunto**: fornisci informazioni utili per gli utenti nei passaggi successivi
- **Branding coerente**: mantieni la voce e lo stile visivo della tua organizzazione
- **Considerazione mobile**: verifica i messaggi su schermi di varie dimensioni

**Ottimizzazione reindirizzamento:**

- **Ottimizzazione pagina**: assicurati che le destinazioni di reindirizzamento siano ottimizzate per i visitatori che accedono al modulo
- **Caricamento delle prestazioni**: verifica il caricamento rapido delle pagine di reindirizzamento per mantenere l&#39;esperienza utente
- **Rilevanza del contenuto**: assicurati che il contenuto del reindirizzamento sia pertinente al contesto del modulo

### Considerazioni sulla sicurezza

**Convalida URL:**

- Implementa la convalida corretta per gli URL di reindirizzamento per evitare reindirizzamenti dannosi
- Considerare gli approcci basati su whitelist per i domini di reindirizzamento consentiti
- Monitorare i pattern di reindirizzamento per attività insolite

**Sicurezza dei contenuti:**

- Pulire il contenuto del messaggio di ringraziamento per evitare l’iniezione di script
- Implementare criteri di sicurezza dei contenuti appropriati per i contenuti in formato Rich Text
- Revisioni periodiche della sicurezza delle destinazioni di reindirizzamento

### Analisi e tracciamento

**Considerazioni sull&#39;implementazione:**

- **Tracciamento obiettivo**: imposta gli obiettivi di analisi sia per le visualizzazioni dei messaggi di ringraziamento che per i completamenti del reindirizzamento
- **Mappatura percorso utenti**: tieni traccia di come gli utenti interagiscono con le esperienze post-invio
- **Ottimizzazione della conversione**: test A/B di diversi messaggi di ringraziamento e destinazioni di reindirizzamento

**Strategie di misurazione:**

- Monitora il tempo trascorso sui messaggi di ringraziamento prima della rimozione
- Tracciare le percentuali di click-through per i collegamenti nei messaggi di ringraziamento
- Analizzare il comportamento degli utenti sulle pagine di destinazione di reindirizzamento

## Checkpoint di convalida

Dopo aver configurato l’esperienza post-invio:

**Verifica configurazione:**

- Le proprietà del modulo mostrano correttamente l’opzione di ringraziamento selezionata
- Il contenuto del messaggio viene visualizzato correttamente in modalità anteprima
- Gli URL di reindirizzamento sono formattati correttamente e sono accessibili
- Tutti i collegamenti all’interno dei messaggi funzionano correttamente

**Test dell&#39;esperienza utente:**

- Invia i moduli di test per verificare la corretta visualizzazione del messaggio di ringraziamento
- Test della funzionalità di reindirizzamento tra browser diversi
- Verifica la reattività mobile dei messaggi di ringraziamento
- Conferma il caricamento corretto delle destinazioni di reindirizzamento

**Configurazione di Analytics:**

- Codici di tracciamento correttamente implementati per i messaggi di ringraziamento
- Tracciamento della destinazione di reindirizzamento configurato
- Eventi di completamento degli obiettivi attivati correttamente

## Passaggi successivi

Dopo aver configurato correttamente l’esperienza post-invio:

- **Monitoraggio delle prestazioni**: rivedi le analisi per comprendere il coinvolgimento degli utenti con messaggi di ringraziamento o pagine di reindirizzamento
- **Itera e migliora**: utilizza il feedback degli utenti e le informazioni sui dati per perfezionare la tua strategia post-invio
- **Implementazione scalabile**: applica pattern di successo ad altri moduli dell&#39;organizzazione

**Documentazione correlata:**

- [Guida alla configurazione per l’invio di moduli](submit-action.md)
- [Best practice per l’esperienza utente](responsive-layout.md)

