---
title: Forms Experience Builder - Guida alla risoluzione dei problemi
description: Guida completa alla risoluzione dei problemi per Forms Experience Builder in cui sono illustrati problemi comuni, soluzioni e tecniche di debug per la creazione e la gestione dei moduli.
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: 6a7810fd-2860-410b-867d-8d29afd5297d
source-git-commit: fe34b44d02c308e7d18a08dd05f21abc67bd0cb2
workflow-type: tm+mt
source-wordcount: '2282'
ht-degree: 100%

---


# Forms Experience Builder - Guida alla risoluzione dei problemi

>[!NOTE]
>
> Forms Experience Builder è disponibile nell’ambito del programma per i primi utilizzatori. Per richiedere l’accesso, invia un’e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com`.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa guida alla risoluzione dei problemi è attualmente in fase di test rispetto al prodotto, pertanto è soggetta ad aggiornamenti e revisioni. Problemi, soluzioni e tecniche di debug possono cambiare in base all’evoluzione di Forms Experience Builder durante il programma per primi utilizzatori.

Questa guida completa alla risoluzione dei problemi consente di identificare, diagnosticare e risolvere i problemi più comuni durante l’utilizzo di Forms Experience Builder. La guida è organizzata per categorie di problemi con correzioni rapide e soluzioni dettagliate.

## Riferimento rapido - Problemi comuni

| Problema | Correzione rapida |
|-------|-----------|
| **L’interfaccia non si carica** | Aggiorna il browser, controlla la connessione Internet e verifica le autorizzazioni di accesso anticipato |
| **Comandi non funzionanti** | Prova `/help` o usa il linguaggio naturale invece dei comandi slash |
| **@fieldName non riconosciuto** | Controlla l’ortografia, assicurati che il campo esista e verifica la sintassi del nome del campo |
| **Impossibile caricare il file** | Usa un file PDF/JPG/PNG con dimensioni inferiori a 10 MB e verifica la compatibilità del formato di file |
| **Aspetto del modulo sbagliato** | Sii più specifico: &quot;Rendilo semplice e intuitivo&quot; invece di &quot;Correggi il layout&quot; |
| **Integrazione non riuscita** | Verifica le credenziali e le autorizzazioni API e controlla la disponibilità dell’endpoint |
| **Il modulo non viene inviato** | Verifica la configurazione e le regole di convalida dell’azione di invio |
| **Errori di convalida non visualizzati** | Verifica le impostazioni di convalida del campo e il posizionamento del messaggio di errore |
| **Problemi di layout dei dispositivi mobili** | Rivedi le impostazioni di design responsive e del dimensionamento dei campi |
| **Campi non visualizzati** | Verifica la logica condizionale e le regole di visibilità |
| **Errori durante l’importazione** | Verifica la compatibilità del formato del file e i limiti di dimensione |
| **Problemi relativi alle prestazioni** | Ottimizza il conteggio dei campi e rimuovi le convalide non necessarie |
| **Problemi di accessibilità** | Rivedi le etichette dei campi, gli attributi ARIA e l’ordine delle schede |

**Hai ancora bisogno di aiuto?** Digita `/help` seguito da una domanda specifica o contatta l’amministratore di sistema per richiedere assistenza tecnica.

## Problemi di accesso e autenticazione

### Impossibile accedere a Forms Experience Builder

**Sintomi:**

- Interfaccia di Forms Experience Builder non visibile
- &quot;Accesso negato&quot; o messaggi di errore simili
- Icona di Forms Experience Builder non presente nell’editor

**Soluzioni:**

1. **Verifica l’iscrizione al programma di accesso anticipato**
   - Conferma di avere ricevuto l’approvazione per partecipare al programma di adozione anticipata.
   - Verifica che la richiesta sia stata inviata dal tuo indirizzo e-mail ufficiale di lavoro.
   - Se l’accesso risulta ancora in sospeso, contatta `aem-forms-ea@adobe.com`.

2. **Verifica la configurazione dell’ambiente**
   - Verifica che AEM Forms sia abilitato per il tuo ambiente.
   - Assicurati di utilizzare un browser supportato (Chrome, Firefox, Safari, Edge).
   - Cancella la cache del browser e i cookie
   - Disattiva eventuali estensioni del browser che potrebbero interferire

3. **Verifica le autorizzazioni utente**
   - Conferma di disporre dei ruoli utente e delle autorizzazioni appropriati.
   - Rivolgiti all’amministratore di sistema per informazioni sui diritti di accesso.
   - Verifica di aver effettuato l’accesso con l’account corretto.

### Problemi di caricamento dell’interfaccia

**Sintomi**

- Interfaccia vuota o parzialmente caricata
- Indicatori di caricamento che continuano a ruotare
- Errori JavaScript nella console del browser

**Soluzioni:**

1. **Risoluzione dei problemi del browser**
   - Aggiorna la pagina (Ctrl+F5 o Comando+Maiusc+R).
   - Prova con un altro browser o in modalità incognito/privata.
   - Controlla se è disponibile un aggiornamento del browser e, se disponibile, installalo.
   - Disabilita temporaneamente ad blocker ed estensioni di privacy.

2. **Connettività di rete**
   - Verifica che la connessione Internet sia stabile.
   - Controlla se il firewall aziendale blocca i domini richiesti.
   - Se possibile, prova con una connessione di rete diversa.
   - Per problemi di configurazione della rete, contatta il supporto IT.

3. **Problemi relativi a cache e archiviazione**
   - Cancella la cache del browser e l’archiviazione locale.
   - Ripristina le impostazioni predefinite del browser.
   - Controlla lo spazio disponibile sul dispositivo.
   - Prova ad accedere da un altro dispositivo.

## Problemi di comandi e interazione

### Comandi con barra non funzionanti

**Sintomi**

- `/create-form` o altri comandi con barra non riconosciuti
- Non vengono visualizzati i suggerimenti di completamento automatico
- I comandi generano messaggi di errore

**Soluzioni:**

1. **Verifica la sintassi del comando**
   - Verifica che il formato del comando sia corretto: `/command-name description`
   - Verifica la presenza di errori di battitura nei nomi dei comandi.
   - Utilizza il linguaggio naturale come alternativa: &quot;Crea un modulo di contatto&quot;
   - Prova `/help` per verificare se il comando è disponibile.

2. **Comandi specifici per il contesto**
   - Verifica di essere nel contesto dell’editor corretto (editor universale o editor di moduli adattivi).
   - Alcuni comandi funzionano solo in ambienti specifici.
   - Consulta la documentazione di riferimento dei comandi per verificare i requisiti di contesto.

3. **Approcci alternativi**
   - Utilizza il linguaggio naturale invece dei comandi slash
   - Suddividi i comandi complessi in richieste più semplici e di dimensioni ridotte
   - Prova a creare i moduli passo dopo passo invece di eseguire un unico comando complesso

### Riferimenti ai campi non funzionanti

**Sintomi:**

- Riferimenti `@fieldName` non riconosciuti
- Messaggi di errore relativi a campi sconosciuti
- Le modifiche apportate ai campi non si applicano correttamente

**Soluzioni:**

1. **Verifica del nome del campo**
   - Controlla l’ortografia esatta dei nomi dei campi (distinzione maiuscole/minuscole)
   - Assicurati che il campo sia presente prima di farvi riferimento
   - Utilizza il nome preciso del campo come creato, non l’etichetta visualizzata
   - Verifica le convenzioni di denominazione dei campi (camelCase, snake_case, ecc.)

2. **Sintassi di riferimento ai campi**
   - Usa la sintassi `@fieldName` corretta senza spazi
   - Evita caratteri speciali nei riferimenti ai campi
   - Verifica l’eventuale presenza di caratteri invisibili o problemi di formattazione
   - Prova a ricreare manualmente il riferimento al campo

3. **Debug dei riferimenti ai campi**
   - Elenca prima tutti i campi esistenti: &quot;Mostra tutti i campi dei moduli correnti&quot;
   - Crea campi prima di farvi riferimento nelle regole
   - Utilizza nomi di campo semplici senza caratteri complessi
   - Prova i riferimenti ai campi uno alla volta

## Problemi relativi alla creazione e alla progettazione dei moduli

### Il modulo non viene creato come previsto

**Sintomi:**

- Il modulo generato non presenta i campi richiesti
- Layout o tipi di campo non corretti
- La struttura del modulo non corrisponde alla descrizione

**Soluzioni:**

1. **Migliora la specificità del prompt**
   - Descrivi i moduli in modo più dettagliato
   - Specifica i tipi di campo e i requisiti di convalida esatti
   - Includi preferenze di layout e requisiti di user experience
   - Suddividi i moduli complessi in richieste incrementali e di dimensioni ridotte

2. **Approccio allo sviluppo iterativo**
   - Inizia con la struttura di base del modulo
   - Aggiungi campi e funzionalità in modo incrementale
   - Verifica ogni aggiunta prima di procedere
   - Ottimizza la conversazione anziché una singola richiesta complessa

3. **Esempio di prompt migliori**

   Invece di:

       Crea un modulo per i clienti
   
   Utilizza:

       Crea un modulo di contatto con il cliente con:
       - Nome completo (campo di testo obbligatorio)
       - Indirizzo e-mail (obbligatorio con la convalida)
       - Numero di telefono (facoltativo, formattato)
       - Messaggio (area di testo richiesta, massimo 500 caratteri)
       - Invio alla notifica e-mail
   
### Problemi di layout e applicazione dello stile

**Sintomi:**

- Il modulo appare tagliato sui dispositivi mobili
- Spaziatura o allineamento non coerente
- Campi non visualizzati correttamente
- Gerarchia visiva insufficiente

**Soluzioni:**

1. **Reattività sui dispositivi mobili**
   - Richiedere ottimizzazioni specifiche per dispositivi mobili: “Rendi questo modulo adatto ai dispositivi mobili”
   - Specifica i requisiti di progettazione dinamica
   - Esegui test su dispositivi mobili effettivi
   - Utilizzare layout a colonna singola per dispositivi mobili

2. **Miglioramenti del layout**
   - Specificare i requisiti di layout: “Disponi i campi indirizzo in due colonne”
   - Richiedere uno stile specifico: “Utilizza colori professionali e composizione tipografica pulita”
   - Specificare le esigenze di spaziatura e allineamento
   - Richiedere conformità all’accessibilità

3. **Coerenza del brand**
   - Preparare le linee guida per il brand prima della creazione del modulo
   - Includere codici colore e font specifici nelle richieste
   - Utilizzare uno stile coerente in tutti i moduli
   - Creare modelli di brand da riutilizzare

### Problemi di logica condizionale

**Sintomi:**

- Le regole non vengono attivate come previsto
- Campi visualizzati/nascosti in modo errato
- Logica di convalida non funzionante
- Errore nelle regole di business complesse

**Soluzioni:**

1. **Semplificazione delle regole**
   - Suddividere regole complesse in condizioni più semplici e più piccole
   - Testare ogni regola singolarmente prima di combinarla
   - Utilizzare condizioni chiare e specifiche: “Mostra @spouseInfo quando @maritalStatus è uguale a “Sposato””
   - Evitare inizialmente la logica nidificata o eccessivamente complessa

2. **Debug e test delle regole**
   - Testare tutti i possibili percorsi e scenari utente
   - Verificare i nomi e i valori dei campi nelle condizioni
   - Verificare la differenziazione tra maiuscole e minuscole nelle condizioni della regola
   - Utilizzare la modalità di debug per tracciare l’esecuzione della regola

3. **Implementazione della logica di business**
   - Documentare chiaramente i requisiti aziendali prima dell’implementazione
   - Implementare le regole in modo incrementale e testare ogni passaggio
   - Fornire un feedback chiaro all’utente quando vengono attivate le regole
   - Gestire casi limite e scenari di eccezione

## Problemi relativi alla conversione e all’importazione dei file

### Errori di importazione PDF

**Sintomi:**

- I file PDF non vengono caricati né elaborati
- Campi o contenuto mancanti nei moduli convertiti
- Messaggi di errore durante la conversione PDF
- Riconoscimento dei campi non corretto da PDF

**Soluzioni:**

1. **Formato e dimensioni del file**
   - Assicurarsi che i file PDF siano inferiori a 10 MB
   - Utilizza PDF di alta qualità basati su testo (immagini non scansionate)
   - Verifica che il file PDF non sia crittografato o protetto da password
   - Prova a convertire il file PDF in formato immagine se non è possibile estrarre il testo

2. **Ottimizzazione della qualità dei file PDF**
   - Utilizza i file PDF con campi modulo chiari e ben definiti
   - Garantisci un buon contrasto e testo leggibile
   - Evita layout complessi o elementi sovrapposti
   - Fornisci contesto aggiuntivo nella richiesta di conversione

3. **Miglioramento della conversione**
   - Descrivi in modo dettagliato la struttura del modulo prevista
   - Specifica i tipi di campo e i requisiti di convalida
   - Richiedi miglioramenti specifici: &quot;Aggiungere capacità di risposta e convalida per dispositivi mobili&quot;
   - Rivedi e perfeziona manualmente i moduli convertiti

### Problemi di conversione di immagini e schermate

**Sintomi:**

- Riconoscimento dei campi non sufficiente dalle immagini
- Layout o tipi di campo non corretti
- Elementi del modulo mancanti
- Timeout o errori di conversione

**Soluzioni:**

1. **Requisiti di qualità delle immagini**
   - Usa immagini ad alta risoluzione (minimo 300 DPI)
   - Assicura una buona illuminazione e un buon contrasto
   - Evita ombre, bagliori o distorsioni
   - Ritaglia le immagini per concentrarti solo sul contenuto del modulo

2. **Formati immagine ottimali**
   - Utilizza i formati PNG o JPG per ottenere risultati ottimali
   - Evita GIF o immagini compresse di bassa qualità
   - Assicurati che il testo sia chiaramente leggibile nell’immagine
   - Se necessario, prova a orientare l’immagine in modo diverso

3. **Indicazioni per la conversione**
   - Fornisci descrizioni dettagliate della struttura del modulo
   - Specifica in modo esplicito i tipi di campo e i requisiti
   - Richiedi miglioramenti specifici durante la conversione
   - Preparati ad apportare delle modifiche manuali dopo la conversione

## Problemi di integrazione e invio

### Errori di invio del modulo

**Sintomi:**

- Invio dei moduli non riuscito
- Messaggi di errore durante l’invio
- I dati non raggiungono le destinazioni previste
- Errori di timeout durante l’invio

**Soluzioni:**

1. **Configurazione delle azioni di invio**
   - Verifica che l’azione di invio sia configurata correttamente
   - Verifica gli endpoint API e credenziali di autenticazione
   - Effettua un test con l’invio di un’e-mail semplice
   - Convalida i requisiti del formato dati

2. **Rete e connettività**
   - Verifica la connessione a Internet e la stabilità della rete
   - Verifica che le impostazioni del firewall consentano l&#39;invio di moduli.
   - Esegui test da altre connessioni di rete.
   - Verifica la presenza di proxy aziendali o restrizioni di sicurezza.

3. **Problemi di convalida dei dati**
   - Assicurati che tutti i campi obbligatori siano completati.
   - Verifica che i formati dei dati corrispondano ai requisiti API.
   - Verifica che non vi siano caratteri speciali o problemi di codifica.
   - Esegui prima un test con un set di dati minimo.

### Problemi di integrazione API

**Sintomi**

- Gli endpoint REST API non rispondono
- Errori di autenticazione
- Formato dati non corrispondente
- Timeout o errori di integrazione

**Soluzioni:**

1. **Verifica della configurazione API**
   - Verifica che gli URL degli endpoint API siano corretti e accessibili.
   - Verifica le credenziali e le autorizzazioni di autenticazione.
   - Esegui un test degli endpoint API in modo indipendente con strumenti come Postman.
   - Verifica che l’API accetti il formato dati corretto (JSON, XML, ecc.).

2. **Problemi di mappatura dei dati**
   - Assicurati che i nomi dei campi modulo corrispondano ai requisiti dei parametri API.
   - Verifica che tutti i campi obbligatori siano presenti.
   - Verifica la compatibilità del tipo di dati (stringhe, numeri, date).
   - Esegui test con dati di esempio per identificare eventuali problemi di mappatura.

3. **Gestione e debug degli errori**
   - Abilita la registrazione dettagliata degli errori per le chiamate API.
   - Controlla i messaggi di errore e i codici di risposta API.
   - Implementa la logica per nuovi tentativi in caso di errori temporanei.
   - Fornisci opzioni di fallback per gli utenti quando l’API non riesce.

### Risoluzione dei problemi di integrazione

**Sintomi**

- E-mail di conferma non inviate
- E-mail in cartelle di posta indesiderata
- E-mail con formattazione errata
- E-mail prive di dati modulo

**Soluzioni:**

1. **Configurazione delle e-mail**
   - Verifica che gli indirizzi e-mail siano formattati correttamente.
   - Verifica le impostazioni SMTP e l’autenticazione
   - Esegui un test con indirizzi e-mail semplici.
   - Verifica le autorizzazioni e le quote del server e-mail.

2. **Ottimizzazione della consegna e-mail**
   - Assicurati che le intestazioni e-mail e le informazioni sul mittente siano corrette.
   - Evita di inserire nell’oggetto parole che potrebbero attivare regole anti-spam
   - Includi meccanismi corretti per l’annullamento dell’iscrizione.
   - Esegui un test della consegna e-mail verso altri provider.

3. **Contenuti e formattazione**
   - Verifica che i dati del modulo siano formattati correttamente nelle e-mail.
   - Verifica che non vi siano caratteri speciali o problemi di codifica.
   - Testa modelli di e-mail con varie combinazioni di dati
   - Assicurati che il contenuto delle e-mail sia accessibile e leggibile

## Problemi relativi a prestazioni e caricamento

### Caricamento lento del modulo

**Sintomi:**

- Il caricamento iniziale di dei moduli richiede molto tempo
- Interazioni utente lente
- Timeout durante le operazioni nel modulo
- Prestazioni scadenti sui dispositivi mobili

**Soluzioni:**

1. **Ottimizzazione del modulo**
   - Riduci il numero di campi e la complessità
   - Implementa il caricamento lento per le sezioni non critiche
   - Ottimizza immagini e risorse per la distribuzione sul web
   - Rimuovi le regole di convalida o la logica non necessarie

2. **Ottimizzazione di browser e dispositivi**
   - Cancella la cache del browser e i file temporanei
   - Chiudi le applicazioni e le schede del browser non necessarie
   - Controlla l’archiviazione e la memoria del dispositivo disponibili
   - Prova browser diversi per il confronto delle prestazioni

3. **Ottimizzazione della rete**
   - Esegui il test con diverse connessioni di rete
   - Verifica la presenza di congestione di rete o di limitazioni della larghezza di banda
   - Se possibile, utilizza la connessione cablata anziché il WiFi
   - Contatta il supporto IT per problemi relativi alle prestazioni della rete

### Problemi relativi alle prestazioni di convalida

**Sintomi:**

- Risposte di convalida lente
- Visualizzazione ritardata dei messaggi di errore
- Blocco del modulo durante la convalida
- Errori di timeout durante la convalida del campo

**Soluzioni:**

1. **Ottimizzazione della convalida**
   - Riduci la frequenza di convalida in tempo reale
   - Implementa il debouncing per le chiamate di convalida
   - Semplifica le regole di convalida complesse
   - Se possibile, utilizza la convalida lato client

2. **Semplificazione delle regole**
   - Suddividi la convalida complessa in regole più semplici
   - Rimuovi le convalide tra campi non necessarie
   - Ottimizza la logica condizionale per le prestazioni
   - Memorizza nella cache i risultati della convalida, se possibile

3. **Miglioramenti della user experience**
   - Fornisci feedback immediati per assicurare convalide semplici
   - Utilizza la convalida progressiva invece del tempo reale per le regole complesse
   - Mostra gli indicatori di caricamento durante i processi di convalida
   - Consenti agli utenti di continuare a lavorare in background durante i processi di convalida

## Risoluzione dei problemi avanzata

### Modalità di debug e diagnostica

**Abilita le informazioni di debug**

Utilizza questi prompt per ottenere informazioni più dettagliate sui problemi relativi ai moduli:

    Abilita la modalità di debug per identificare i problemi relativi all’invio dei moduli e alla convalida dei campi
    
    Analizza gli errori dei moduli: controlla le regole di convalida, le risposte API e i pattern di input dell’utente
    
    Mostra informazioni dettagliate sulla struttura del modulo e sulla configurazione dei campi

### Tecniche di analisi degli errori

**Approccio al debug sistematico**

1. **Isola il problema**
   - Esegui test con configurazione minima del modulo
   - Rimuovi temporaneamente le funzionalità complesse
   - Esegui test separati dei singoli componenti
   - Utilizza il processo di eliminazione per identificare la causa principale

2. **Raccogli informazioni di diagnostica**
   - Verifica la presenza di errori JavaScript nella console del browser
   - Rivedi le richieste e le risposte della rete
   - Documenta i passaggi specifici per la riproduzione del problema
   - Raccogli screenshot e messaggi di errore

3. **Esegui test delle variabili di ambiente**
   - Utilizza browser e dispositivi diversi
   - Esegui test con account utente e autorizzazioni diversi
   - Verifica in diversi ambienti di rete
   - Esegui il confronto con moduli di lavoro o configurazioni

### Analisi e monitoraggio dei registri

**Debug della console del browser**

1. Apri gli strumenti per sviluppatori di browser (F12)
2. Verifica la presenza di errori JavaScript nella scheda Console
3. Verifica la presenza di richieste non riuscite nella scheda Rete
4. Controlla la scheda Prestazioni per la presenza di operazioni lente

**Pattern di errori comuni**

- **Errori CORS**: problemi di richieste tra origini diverse con integrazioni API
- **Errori di autenticazione**: credenziali non valide o token scaduti
- **Errori di convalida**: conflitti della regola di convalida dei campi o errori di sintassi
- **Timeout della rete**: connessioni di rete lente o inaffidabili

## Ottenere ulteriore assistenza

### Risorse self-service

**Sistema di assistenza incorporato**

- Utilizza il comando `/help` seguito da domande specifiche
- Accedi alla guida contestuale nell’interfaccia di Forms Experience Builder
- Rivedi attentamente i messaggi di errore per ottenere indicazioni specifiche
- Consulta la [Guida introduttiva di Forms Experience Builder](forms-ai-assistant-getting-started.md)

**Risorse della documentazione**

- [Libreria di prompt di Forms Experience Builder](ai-assistant-prompt-library.md)
- [Best practice per Forms Experience Builder](aem-forms-ai-assistant-best-practices.md)
- [Documentazione di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=it)

### Escalation e supporto

**Quando contattare il supporto**

- I problemi persistono dopo aver provato le soluzioni documentate
- Problemi a livello di sistema che interessano più utenti
- Problemi di sicurezza o integrità dei dati
- Problemi di integrazione che richiedono la configurazione a livello di sistema

**Informazioni da fornire**

- Descrizione dettagliata del problema e passaggi da riprodurre
- Schermate o registrazioni dello schermo relative al problema
- Informazioni su browser e sistema
- Messaggi di errore e registri della console
- Dettagli di configurazione e integrazione dei moduli

**Metodi di contatto**

- Amministratore di sistema: per problemi di ambiente e accesso
- Assistenza tecnica: per problemi di integrazione e configurazione complessi
- Programma di accesso anticipato: `aem-forms-ea@adobe.com` per problemi relativi al programma

### Community e condivisione delle conoscenze

**Best practice per la risoluzione di problemi**

- Documenta le soluzioni per farvi riferimento in futuro.
- Condividi con i membri del team gli approcci che hanno consentito di risolvere problemi.
- Contribuisci alla knowledge base della tua organizzazione.
- Partecipa a community di utenti e forum.

**Miglioramento continuo**

- Rivedi periodicamente i problemi e le soluzioni più comuni.
- Aggiorna le procedure di risoluzione dei problemi in base ai nuovi risultati.
- Organizza sessioni di formazione e condivisione delle conoscenze.
- Fornisci feedback al team del prodotto a scopo di miglioramento delle funzioni.

Questa guida alla risoluzione dei problemi viene continuamente aggiornata in base al feedback ricevuto dagli utenti e alle nuove funzionalità di Forms Experience Builder. Per informazioni sempre aggiornate e risorse aggiuntive, consulta la [documentazione di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=it).
