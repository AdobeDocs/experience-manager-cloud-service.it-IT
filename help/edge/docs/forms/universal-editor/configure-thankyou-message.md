---
title: Come configurare una pagina di reindirizzamento o un messaggio di ringraziamento
description: Scopri come gli utenti possono visualizzare un messaggio di ringraziamento o essere reindirizzati a una pagina web che gli autori dei moduli possono configurare durante la creazione del modulo.
feature: Adaptive Forms, Edge Delivery Services
role: User
level: Intermediate
exl-id: cacd7b0a-aad0-4b5d-a6a0-e4bac4cb196d
source-git-commit: fd3c53cf5a6d1c097a5ea114a831ff626ae7ad7e
workflow-type: ht
source-wordcount: '1139'
ht-degree: 100%

---

# Configurare i messaggi di ringraziamento e gli URL di reindirizzamento

Le esperienze successive all’invio influiscono in modo significativo sulla soddisfazione degli utenti e sui tassi di completamento dei moduli. L’editor universale di Adobe offre opzioni complete per la configurazione di ciò che gli utenti visualizzano dopo l’invio dei moduli, sia tramite messaggi di ringraziamento personalizzati che tramite reindirizzamenti strategici a pagine specifiche.

Questo articolo fornisce indicazioni dettagliate sull’implementazione dei messaggi di ringraziamento e degli URL di reindirizzamento, incluse considerazioni tecniche, best practice e linee guida sull’esperienza utente per massimizzare l’efficacia dell’invio dei moduli.

## Prerequisiti

Prima di configurare le esperienze successive all’invio, assicurati di disporre di:

**Configurazione tecnica:**

- Accesso all’editor universale con le autorizzazioni appropriate
- Modulo adattivo esistente creato nell’editor universale
- Informazioni sui requisiti degli URL di reindirizzamento dell’organizzazione

**Considerazioni sulla pianificazione:**

- **Strategia relativa ai messaggi**: definisci il tono, la lunghezza e le informazioni specifiche da includere nei messaggi di ringraziamento
- **Strategia relariva al reindirizzamento**: identifica le pagine di destinazione e assicurati che siano ottimizzate per le esperienze di completamento post-modulo
- **Integrazione dell’analisi**: pianifica come tenere traccia delle interazioni dell’utente con i messaggi di ringraziamento o le destinazioni di reindirizzamento

## Configurare i messaggi di ringraziamento

I messaggi di ringraziamento consentono di confermare immediatamente l’invio corretto del modulo e possono includere contenuto personalizzato, passaggi successivi o informazioni rilevanti relative all’invio da parte dell’utente.

### Quando utilizzare i messaggi di ringraziamento

I messaggi di ringraziamento funzionano al meglio quando:

- **Riconoscimento semplice**: gli utenti devono essere confermati senza ulteriori requisiti di navigazione
- **Contenuto istruttivo**: è necessario specificare i passaggi successivi o le informazioni importanti
- **Coerenza del brand**: il messaggio può essere creato per allinearsi allo stile di comunicazione dell’organizzazione
- **Esperienza a pagina singola**: gli utenti devono rimanere nella pagina corrente per la continuità del flusso di lavoro

### Passaggi di implementazione

**1. Accedere alle proprietà del modulo**

Apri il modulo adattivo nell’editor universale e fai clic sull’icona **Modifica proprietà modulo** nella barra degli strumenti. Verrà visualizzata la finestra di dialogo completa delle proprietà del modulo.

![Icona proprietà modulo](/help/forms/assets/ue-form-properties-icon.png)

**2. Passare alla configurazione del ringraziamento**

Nella finestra di dialogo Proprietà modulo, seleziona la scheda **Ringraziamento** per accedere alle opzioni di configurazione successive all’invio.

![Proprietà del modulo dell’editor universale](/help/forms/assets/ue-form-properties.png)

**3. Configurare la visualizzazione del messaggio**

Seleziona **Mostra messaggio** dalle opzioni disponibili.

![grazie](/help/edge/docs/forms/universal-editor/assets/thankyou-ue.png)

**4. Creare il contenuto del messaggio**

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

- Mantieni i messaggi concisi fornendo le informazioni necessarie
- Includi i passaggi successivi non crittografati, se appropriato
- Valuta se includere numeri di riferimento o dettagli di conferma
- Assicura una formattazione semplice e intuitiva

### Esempio di implementazione

    Grazie per il contributo!
    
    La richiesta è stata ricevuta e ti è stato assegnato il numero di riferimento #REF-2024-001234.
    
    **Cosa succede dopo:**
    - Riceverai un&#39;e-mail di conferma entro 15 minuti
    - Il nostro team rivedrà l&#39;invio entro 2 giorni lavorativi
    - Ti contatteremo direttamente se sono necessarie ulteriori informazioni
    
    **Per assistenza** Contatta il nostro team di assistenza all&#39;indirizzo support@example.com

## Configurare gli URL di reindirizzamento

Gli URL di reindirizzamento indirizzano automaticamente gli utenti a pagine specifiche dopo l’invio del modulo, consentendo un’integrazione diretta con i flussi di lavoro esistenti o indirizzando gli utenti a contenuti rilevanti.

### Quando utilizzare gli URL di reindirizzamento

Gli URL di reindirizzamento sono ottimali per:

- **Integrazione del flusso di lavoro**: indirizzamento degli utenti a dashboard, pagine account o passaggi successivi in un processo
- **Consegna dei contenuti**: presentazione di prodotti, servizi o informazioni rilevanti in base alle risposte ai moduli
- **Tracciamento analisi**: indirizzamento a pagine con implementazioni di tracciamento specifiche
- **Processi con più passaggi**: spostamento degli utenti alla fase successiva di flussi di lavoro complessi

### Passaggi di implementazione

**1. Accedere alle proprietà del modulo**

Apri il modulo adattivo nell&#39;Editor universale e fai clic sull&#39;icona **Modifica proprietà modulo** per aprire la finestra di dialogo per la configurazione del modulo.

![Icona proprietà modulo](/help/forms/assets/ue-form-properties-icon.png)

**2. Passare alla configurazione di ringraziamento**

Seleziona la scheda **Ringraziamento** nella finestra di dialogo Proprietà modulo per accedere alle opzioni di configurazione del reindirizzamento.

![Proprietà del modulo dell’editor universale](/help/forms/assets/ue-form-properties.png)

**3. Abilitare lefunzionalità di reindirizzamento**

Scegli **Reindirizza all&#39;URL** tra le opzioni disponibili per il post-invio.

![reindirizzamento](/help/edge/docs/forms/universal-editor/assets/redirect-ue.png)

**4. Configurare l&#39;URL di destinazione**

Immetti l’URL di destinazione nel campo fornito. Il sistema supporta più formati URL per un’implementazione flessibile.

### Opzioni di configurazione URL

**URL assoluti**

Indirizzi web completi, inclusi protocollo e dominio:

    https://www.example.com/thank-you
    https://dashboard.example.com/user/profile

**Percorsi relativi**

Percorsi relativi al dominio corrente:

    /thank-you
    /dashboard/user-profile
    ../confirmation-page.html

**Riferimenti per la pagina AEM Sites**

Riferimenti ad altre pagine all’interno dell’implementazione AEM Sites:

    /content/mysite/en/thank-you
    /content/mysite/en/next-steps

### Considerazioni tecniche

**Comportamento del reindirizzamento:**

- I reindirizzamenti si verificano immediatamente dopo l’invio corretto del modulo
- La cronologia del browser include il reindirizzamento per la corretta funzionalità del pulsante Indietro
- La tempistica di reindirizzamento può essere configurata con ritardi opzionali

**Convalida URL:**

- Il sistema convalida il formato URL prima di consentire la configurazione
- Gli URL relativi vengono risolti rispetto al dominio corrente
- Se necessario, gli URL esterni richiedono una configurazione CORS corretta

## Best practice e consigli

### Linee guida per l’esperienza utente

**Ottimizzazione dei messaggi:**

- **Prima la chiarezza**: assicurati che gli utenti comprendano immediatamente che l’invio è stato eseguito correttamente
- **Valore aggiunto**: fornisci informazioni utili per gli utenti nei passaggi successivi
- **Branding coerente**: mantieni la voce e lo stile visivo della tua organizzazione
- **Considerazioni per i dispositivi mobili**: verifica i messaggi su schermi di varie dimensioni

**Ottimizzazione reindirizzamento**

- **Ottimizzazione delle pagine**: assicurati che le destinazioni di reindirizzamento siano ottimizzate per chi ha compilato il modulo
- **Caricamento delle prestazioni**: verifica il caricamento rapido delle pagine di reindirizzamento per mantenere l&#39;esperienza utente
- **Rilevanza dei contenuti**: assicurati che il contenuto del reindirizzamento sia pertinente al contesto del modulo

### Considerazioni sulla sicurezza

**Convalida URL:**

- Implementare la convalida corretta per gli URL di reindirizzamento per evitare reindirizzamenti dannosi
- Prendere in considerazione gli approcci basati su whitelist per i domini di reindirizzamento consentiti
- Monitorare i pattern di reindirizzamento per attività insolite

**Sicurezza dei contenuti:**

- Pulire il contenuto del messaggio di ringraziamento per evitare l’iniezione di script
- Implementare criteri di sicurezza dei contenuti appropriati per i contenuti in formattati
- Eseguire revisioni periodiche della sicurezza delle destinazioni di reindirizzamento

### Analisi e tracciamento

**Considerazioni sull’implementazione:**

- **Tracciamento obiettivo**: imposta gli obiettivi di analisi sia per le visualizzazioni dei messaggi di ringraziamento che per i completamenti del reindirizzamento
- **Mappatura percorso utenti**: tieni traccia di come gli utenti interagiscono con le esperienze post-invio
- **Ottimizzazione della conversione**: test A/B di diversi messaggi di ringraziamento e destinazioni di reindirizzamento

**Strategie di misurazione:**

- Monitorare il tempo trascorso sui messaggi di ringraziamento prima della rimozione
- Tracciare le percentuali di click-through per i collegamenti nei messaggi di ringraziamento
- Analizzare il comportamento degli utenti sulle pagine di destinazione di reindirizzamento

## Punto di controllo per la convalida

Dopo aver configurato l’esperienza post-invio:

**Verifica la configurazione:**

- Le proprietà del modulo mostrano correttamente l’opzione di ringraziamento selezionata
- Il contenuto del messaggio viene visualizzato correttamente in modalità anteprima
- Gli URL di reindirizzamento sono formattati correttamente e sono accessibili
- Tutti i collegamenti all’interno dei messaggi funzionano correttamente

**Test dell’esperienza utente:**

- Inviare i moduli di test per verificare la corretta visualizzazione del messaggio di ringraziamento
- Testare la funzionalità di reindirizzamento tra browser diversi
- Verificare la reattività mobile dei messaggi di ringraziamento
- Confermare il caricamento corretto delle destinazioni di reindirizzamento

**Configurazione dell’analisi:**

- Tracciamento dei codici correttamente implementati per i messaggi di ringraziamento
- Tracciamento della destinazione di reindirizzamento configurato
- Eventi di completamento degli obiettivi attivati correttamente

## Passaggi successivi

Dopo aver configurato correttamente l’esperienza post-invio:

- **Monitora le prestazioni**: rivedi le analisi per comprendere il coinvolgimento utenti con messaggi di ringraziamento o pagine di reindirizzamento
- **Itera e migliora**: utilizza il feedback degli utenti e le informazioni sui dati per perfezionare la tua strategia post-invio
- **Implementazione scalabile**: applica pattern di successo ad altri moduli dell’organizzazione

**Documentazione correlata:**

- [Guida alla configurazione per l’invio di moduli](submit-action.md)
- [Best practice per l’esperienza utente](responsive-layout.md)
