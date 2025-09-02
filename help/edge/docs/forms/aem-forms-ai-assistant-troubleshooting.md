---
title: Forms Experience Builder - Guida alla risoluzione dei problemi
description: Guida completa alla risoluzione dei problemi per Forms Experience Builder, che tratta problemi comuni, soluzioni e tecniche di debug per la creazione e la gestione dei moduli.
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: 6a7810fd-2860-410b-867d-8d29afd5297d
source-git-commit: fe34b44d02c308e7d18a08dd05f21abc67bd0cb2
workflow-type: tm+mt
source-wordcount: '2282'
ht-degree: 1%

---


# Forms Experience Builder - Guida alla risoluzione dei problemi

>[!NOTE]
>
> Forms Experience Builder è disponibile nell&#39;ambito del programma per gli utenti meno esperti. Invia un&#39;e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com` per richiedere l&#39;accesso.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa guida alla risoluzione dei problemi è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. Problemi, soluzioni e tecniche di debug possono cambiare in base all’evoluzione di Forms Experience Builder durante il programma di adozione anticipata.

Questa guida completa alla risoluzione dei problemi consente di identificare, diagnosticare e risolvere i problemi più comuni quando si lavora con Forms Experience Builder. La guida è organizzata per categorie di problemi con correzioni rapide e soluzioni dettagliate.

## Riferimento rapido - Problemi comuni

| Problema | Correzione rapida |
|-------|-----------|
| **Impossibile caricare l&#39;interfaccia** | Aggiorna il browser, controlla la connessione Internet, verifica le autorizzazioni di accesso anticipato |
| **Comandi non funzionanti** | Prova `/help` o usa il linguaggio naturale invece dei comandi barra |
| **@fieldName non riconosciuto** | Controlla l&#39;ortografia, verifica che il campo esista, verifica la sintassi del nome campo |
| **Impossibile caricare il file** | Usa PDF/JPG/PNG inferiore a 10 MB, verifica la compatibilità del formato file |
| **Il modulo ha un aspetto errato** | Sii più specifico: &quot;Rendi mobile-friendly&quot; invece di &quot;fix layout&quot; |
| **Integrazione non riuscita** | Verifica credenziali e autorizzazioni API, verifica la disponibilità dell’endpoint |
| **Modulo non inviato** | Verifica la configurazione e le regole di convalida dell’azione di invio |
| **Errori di convalida non visualizzati** | Verificare le impostazioni di convalida del campo e il posizionamento del messaggio di errore |
| **Problemi di layout dispositivi mobili** | Verifica delle impostazioni di progettazione reattiva e del dimensionamento dei campi |
| **Campi non visualizzati** | Verificare la logica condizionale e le regole di visibilità |
| **Errori di importazione** | Verifica della compatibilità del formato del file e dei limiti di dimensione |
| **Problemi di prestazioni** | Ottimizza il conteggio dei campi e rimuovi le convalide non necessarie |
| **Problemi di accessibilità** | Etichette dei campi di revisione, attributi ARIA e ordine di tabulazione |

**Hai ancora bisogno di aiuto?** Digitare `/help` seguito da una domanda specifica o contattare l&#39;amministratore di sistema per assistenza tecnica.

## Problemi di accesso e autenticazione

### Impossibile accedere a Forms Experience Builder

**Sintomi:**

- Interfaccia di Forms Experience Builder non visibile
- &quot;Accesso negato&quot; o messaggi di errore simili
- Icona Forms Experience Builder mancante nell’editor

**Soluzioni:**

1. **Verifica iscrizione programma di accesso anticipato**
   - Conferma di essere stato approvato per il programma di adozione anticipata
   - Verifica che la richiesta sia stata inviata dall’e-mail ufficiale di lavoro
   - Contattare `aem-forms-ea@adobe.com` se l&#39;accesso è ancora in sospeso

2. **Verifica configurazione ambiente**
   - Verifica che AEM Forms sia abilitato per il tuo ambiente
   - Assicurati di utilizzare un browser supportato (Chrome, Firefox, Safari, Edge)
   - Cancella cache del browser e cookie
   - Disattiva le estensioni del browser che potrebbero interferire

3. **Verifica autorizzazioni utente**
   - Conferma di disporre dei ruoli utente e delle autorizzazioni appropriati
   - Rivolgiti all’amministratore di sistema per informazioni sui diritti di accesso
   - Verifica di aver effettuato l’accesso con l’account corretto

### Problemi di caricamento dell’interfaccia

**Sintomi:**

- Interfaccia vuota o parzialmente caricata
- Spinning degli indicatori di caricamento non completati
- Errori JavaScript nella console del browser

**Soluzioni:**

1. **Risoluzione dei problemi del browser**
   - Aggiorna la pagina (Ctrl+F5 o Comando+Maiusc+R)
   - Prova con un browser diverso o in modalità incognito/privata
   - Controlla la disponibilità di aggiornamenti del browser e installalo se disponibile
   - Disattiva temporaneamente ad blocker e estensioni della privacy

2. **Connettività di rete**
   - Verifica connessione Internet stabile
   - Controlla se il firewall aziendale sta bloccando i domini richiesti
   - Se possibile, prova con una connessione di rete diversa
   - Contattare il supporto IT per problemi di configurazione della rete

3. **Problemi relativi a cache e archiviazione**
   - Cancella cache del browser e archiviazione locale
   - Ripristina impostazioni predefinite browser
   - Controllare lo spazio disponibile sul dispositivo
   - Prova ad accedere da un altro dispositivo

## Problemi di comando e interazione

### Comandi barra non funzionanti

**Sintomi:**

- `/create-form` o altri comandi barra non riconosciuti
- Nessun suggerimento di completamento automatico visualizzato
- I comandi generano messaggi di errore

**Soluzioni:**

1. **Verifica della sintassi del comando**
   - Verificare che il formato del comando sia corretto: `/command-name description`
   - Verificare la presenza di errori di battitura nei nomi dei comandi
   - Utilizza il linguaggio naturale come alternativa: &quot;Crea un modulo di contatto&quot;
   - Prova `/help` a verificare la disponibilità del comando

2. **Comandi specifici del contesto**
   - Verifica di essere nel contesto dell’editor corretto (Universal Editor vs Adaptive Forms Editor)
   - Alcuni comandi funzionano solo in ambienti specifici
   - Controlla il riferimento del comando per i requisiti di contesto

3. **Approcci alternativi**
   - Utilizza il linguaggio naturale invece dei comandi barra
   - Suddividere comandi complessi in richieste più semplici e di dimensioni ridotte
   - Prova a creare moduli in modo dettagliato invece di eseguire un singolo comando complesso

### Riferimenti campo non funzionanti

**Sintomi:**

- `@fieldName` riferimenti non riconosciuti
- Messaggi di errore su campi sconosciuti
- Modifiche dei campi non applicate correttamente

**Soluzioni:**

1. **Verifica nome campo**
   - Controllare l&#39;ortografia esatta dei nomi di campo (distinzione maiuscole/minuscole)
   - Assicurati che il campo esista prima di farvi riferimento
   - Utilizza il nome esatto del campo come creato, non l’etichetta visualizzata
   - Verifica le convenzioni di denominazione dei campi (camelCase, snake_case, ecc.)

2. **Sintassi di riferimento campo**
   - Usa la sintassi `@fieldName` corretta senza spazi
   - Evita caratteri speciali nei riferimenti di campo
   - Verifica la presenza di caratteri invisibili o problemi di formattazione
   - Provare a ricreare manualmente il riferimento campo

3. **Riferimenti campo debug**
   - Elenca prima tutti i campi esistenti: &quot;Mostra tutti i campi modulo correnti&quot;
   - Crea campi prima di farvi riferimento nelle regole
   - Utilizzare nomi di campo semplici senza caratteri complessi
   - Riferimenti di campo di prova uno alla volta

## Problemi relativi alla creazione e alla progettazione dei moduli

### Creazione modulo non prevista

**Sintomi:**

- Campi richiesti mancanti nel modulo generato
- Layout o tipi di campo non corretti
- La struttura del modulo non corrisponde alla descrizione

**Soluzioni:**

1. **Migliora la specificità del prompt**
   - Descrivere in modo più dettagliato i moduli
   - Specificare i tipi di campo esatti e i requisiti di convalida
   - Includi preferenze di layout e requisiti di esperienza utente
   - Suddividere moduli complessi in richieste incrementali di dimensioni inferiori

2. **Approccio di sviluppo iterativo**
   - Inizia con la struttura di base del modulo
   - Aggiungere campi e funzionalità in modo incrementale
   - Verificare ogni aggiunta prima di procedere
   - Ottimizzare la conversazione anziché una singola richiesta complessa

3. **Esempio di prompt migliorati**

   Invece di:

       Crea un modulo per i clienti
   
   Usa:

       Crea un modulo contatto cliente con:
       - Nome completo (campo di testo obbligatorio)
       - Indirizzo e-mail (obbligatorio con convalida)
       - Numero di telefono (facoltativo, formattato)
       - Messaggio (area di testo richiesta, massimo 500 caratteri)
       - Invia a notifica e-mail
   
### Problemi di layout e stile

**Sintomi:**

- Il modulo appare danneggiato su dispositivi mobili
- Spaziatura o allineamento non coerenti
- Campi non visualizzati correttamente
- Gerarchia visiva insufficiente

**Soluzioni:**

1. **Velocità di risposta mobile**
   - Richiedi ottimizzazioni specifiche per dispositivi mobili: &quot;Rendi questo modulo compatibile con i dispositivi mobili&quot;
   - Specificare i requisiti di progettazione reattiva
   - Test su dispositivi mobili effettivi
   - Utilizzare layout a colonna singola per dispositivi mobili

2. **Miglioramenti layout**
   - Specifica i requisiti di layout: &quot;Disponi i campi indirizzo in due colonne&quot;
   - Richiedi uno stile specifico: &quot;Usa colori professionali e tipografia pulita&quot;
   - Specificare le esigenze di spaziatura e allineamento
   - Richiedi conformità accessibilità

3. **Coerenza marchio**
   - Preparare le linee guida per il brand prima della creazione del modulo
   - Includere codici colore e font specifici nelle richieste
   - Utilizza uno stile coerente in tutti i moduli
   - Creare modelli di marchio da riutilizzare

### Problemi di logica condizionale

**Sintomi:**

- Le regole non vengono attivate come previsto
- Campi visualizzati/nascosti in modo errato
- Logica di convalida non funzionante
- Errore di regole business complesse

**Soluzioni:**

1. **Semplificazione regole**
   - Suddividere regole complesse in condizioni più semplici e più piccole
   - Testare ogni regola singolarmente prima di combinarla
   - Utilizza condizioni chiare e specifiche: &quot;Mostra @spouseInfo quando @maritalStatus è uguale a &quot;Sposato&quot;&quot;
   - Evita logica nidificata o eccessivamente complessa inizialmente

2. **Test e debug delle regole**
   - Test di tutti i possibili percorsi e scenari utente
   - Verificare i nomi e i valori dei campi nelle condizioni
   - Verifica la sensibilità alle maiuscole/minuscole nelle condizioni della regola
   - Utilizza la modalità di debug per tracciare l’esecuzione della regola

3. **Implementazione della logica di business**
   - Documentare chiaramente i requisiti aziendali prima dell&#39;implementazione
   - Implementa le regole in modo incrementale e testa ogni passaggio
   - Fornire un feedback chiaro agli utenti quando vengono attivate le regole
   - Gestire casi edge e scenari di eccezione

## Problemi relativi all’importazione e alla conversione dei file

### Errori di importazione PDF

**Sintomi:**

- I file PDF non vengono caricati né elaborati
- Campi o contenuto mancanti nei moduli convertiti
- Messaggi di errore durante la conversione PDF
- Riconoscimento dei campi non corretto da PDF

**Soluzioni:**

1. **Formato e dimensioni file**
   - Assicurati che i file PDF siano inferiori a 10 MB
   - Utilizza PDF di alta qualità basati su testo (immagini non acquisite)
   - Verificare che PDF non sia crittografato o protetto da password
   - Prova a convertire PDF in formato immagine se l’estrazione del testo non riesce

2. **Ottimizzazione qualità PDF**
   - Utilizzare i PDF con campi modulo chiari e ben definiti
   - Garantire un buon contrasto e testo leggibile
   - Evitare layout complessi o elementi sovrapposti
   - Fornisci contesto aggiuntivo nella richiesta di conversione

3. **Miglioramento conversione**
   - Descrizione dettagliata della struttura di modulo prevista
   - Specificare i tipi di campo e i requisiti di convalida
   - Miglioramenti specifici per le richieste: &quot;Aggiungere capacità di risposta e convalida per dispositivi mobili&quot;
   - Revisione e perfezionamento manuale dei moduli convertiti

### Problemi di conversione di immagini e schermate

**Sintomi:**

- Riconoscimento campo insufficiente dalle immagini
- Layout o tipi di campo non corretti
- Elementi modulo mancanti
- Errori o timeout di conversione

**Soluzioni:**

1. **Requisiti di qualità delle immagini**
   - Usare immagini ad alta risoluzione (minimo 300 DPI)
   - Assicurare una buona illuminazione e un buon contrasto
   - Evitare ombre, abbagliamenti o distorsioni
   - Ritaglia le immagini per concentrarti solo sul contenuto del modulo

2. **Formati immagine ottimali**
   - Utilizzare i formati PNG o JPG per ottenere risultati ottimali
   - Evita GIF o immagini compresse di bassa qualità
   - Assicurati che il testo sia chiaramente leggibile nell’immagine
   - Se necessario, prova con orientamenti immagine diversi

3. **Guida alla conversione**
   - Fornire descrizioni dettagliate della struttura del modulo
   - Specificare in modo esplicito i tipi di campo e i requisiti
   - Richiedi miglioramenti specifici durante la conversione
   - Prepararsi a eseguire regolazioni manuali dopo la conversione

## Problemi di integrazione e invio

### Errori di invio modulo

**Sintomi:**

- Invio di Forms non riuscito
- Messaggi di errore durante l’invio
- I dati non raggiungono le destinazioni previste
- Errori di timeout durante l’invio

**Soluzioni:**

1. **Configurazione azione invio**
   - Verifica che l’azione di invio sia configurata correttamente
   - Verifica endpoint API e credenziali di autenticazione
   - Test con invio di e-mail semplice
   - Convalidare i requisiti del formato dati

2. **Rete e connettività**
   - Verificare la connettività Internet e la stabilità della rete
   - Verificare che le impostazioni del firewall consentano l&#39;invio di moduli
   - Test da diverse connessioni di rete
   - Verifica la presenza di proxy aziendali o restrizioni di sicurezza

3. **Problemi di convalida dei dati**
   - Assicurati che tutti i campi obbligatori siano completati
   - Verificare che i formati dei dati corrispondano ai requisiti API
   - Verifica la presenza di caratteri speciali o problemi di codifica
   - Esegui prima il test con set di dati minimo

### Problemi di integrazione API

**Sintomi:**

- Gli endpoint REST API non rispondono
- Errori di autenticazione
- Mancata corrispondenza formato dati
- Timeout o errori di integrazione

**Soluzioni:**

1. **Verifica configurazione API**
   - Verificare che gli URL degli endpoint API siano corretti e accessibili
   - Verifica credenziali e autorizzazioni di autenticazione
   - Test degli endpoint API in modo indipendente utilizzando strumenti come Postman
   - Verifica che l’API accetti il formato dati corretto (JSON, XML, ecc.)

2. **Problemi di mappatura dei dati**
   - Assicurati che i nomi dei campi modulo corrispondano ai requisiti dei parametri API
   - Verifica la presenza di campi obbligatori che potrebbero essere mancanti
   - Verificare la compatibilità del tipo di dati (stringhe, numeri, date)
   - Test con dati di esempio per identificare i problemi di mappatura

3. **Gestione e debug degli errori**
   - Abilita registrazione dettagliata degli errori per le chiamate API
   - Controllare i codici di risposta API e i messaggi di errore
   - Implementare la logica dei nuovi tentativi per errori temporanei
   - Fornisci opzioni di fallback per gli utenti quando l’API non riesce

### Problemi di integrazione e-mail

**Sintomi:**

- E-mail di conferma non inviate
- E-mail che vanno in cartelle di posta indesiderata
- Formattazione e-mail errata
- Dati modulo mancanti nelle e-mail

**Soluzioni:**

1. **Configurazione e-mail**
   - Verificare che gli indirizzi di posta elettronica siano formattati correttamente
   - Verifica impostazioni SMTP e autenticazione
   - Test con indirizzi e-mail semplici
   - Verifica autorizzazioni e quote del server e-mail

2. **Ottimizzazione recapito e-mail**
   - Utilizza intestazioni e-mail e informazioni sul mittente corrette
   - Evita parole di attivazione spam nelle righe dell’oggetto
   - Includi meccanismi di annullamento iscrizione corretti
   - Testare la consegna e-mail a diversi provider

3. **Contenuto e formattazione**
   - Verificare che i dati del modulo siano formattati correttamente nelle e-mail
   - Verifica la presenza di caratteri speciali o problemi di codifica
   - Testare modelli e-mail con varie combinazioni di dati
   - Assicurati che il contenuto delle e-mail sia accessibile e leggibile

## Problemi relativi a prestazioni e caricamento

### Caricamento modulo lento

**Sintomi:**

- Il caricamento iniziale di Forms richiede molto tempo
- Interazioni utente lente
- Timeout durante le operazioni del modulo
- Prestazioni scadenti sui dispositivi mobili

**Soluzioni:**

1. **Ottimizzazione modulo**
   - Riduzione del numero di campi e della complessità
   - Implementare il caricamento lento per le sezioni non critiche
   - Ottimizzare immagini e risorse per la distribuzione web
   - Rimuovere le regole di convalida o la logica non necessarie

2. **Ottimizzazione di browser e dispositivi**
   - Cancella cache del browser e file temporanei
   - Chiudere le schede e le applicazioni del browser non necessarie
   - Controllare la memoria e lo storage del dispositivo disponibili
   - Prova diversi browser per il confronto delle prestazioni

3. **Ottimizzazione rete**
   - Verifica con diverse connessioni di rete
   - Verificare la presenza di congestione di rete o limitazioni della larghezza di banda
   - Se possibile, utilizzare la connessione cablata anziché WiFi
   - Contattare il supporto IT per problemi di prestazioni della rete

### Problemi relativi alle prestazioni di convalida

**Sintomi:**

- Risposte di convalida lente
- Visualizzazione messaggio di errore ritardato
- Blocco del modulo durante la convalida
- Errori di timeout durante la convalida del campo

**Soluzioni:**

1. **Ottimizzazione convalida**
   - Riduzione della frequenza di convalida in tempo reale
   - Implementazione del debug per le chiamate di convalida
   - Semplificare regole di convalida complesse
   - Se possibile, utilizza la convalida lato client

2. **Semplificazione regole**
   - Suddividere la convalida complessa in regole più piccole
   - Rimuovere le convalide tra campi non necessarie
   - Ottimizzare la logica condizionale per le prestazioni
   - Risultati della convalida della cache, se appropriato

3. **Miglioramenti esperienza utente**
   - Fornire feedback immediato per convalide semplici
   - Utilizza la convalida progressiva invece del tempo reale per le regole complesse
   - Mostra gli indicatori di caricamento durante i processi di convalida
   - Consenti agli utenti di continuare durante i processi di convalida in background

## Risoluzione avanzata dei problemi

### Modalità di debug e diagnostica

**Abilita informazioni di debug**

Utilizzare queste istruzioni per ottenere informazioni più dettagliate sui problemi relativi ai moduli:

    Abilita la modalità di debug per identificare i problemi relativi all&#39;invio dei moduli e alla convalida dei campi
    
    Analizza gli errori dei moduli: controlla le regole di convalida, le risposte API e i pattern di input dell&#39;utente
    
    Mostra informazioni dettagliate sulla struttura del modulo e sulla configurazione dei campi

### Tecniche di analisi degli errori

**Approccio al debug sistematico**

1. **Isolare il problema**
   - Test con configurazione minima del modulo
   - Rimuovere temporaneamente le feature complesse
   - Test separato dei singoli componenti
   - Utilizza il processo di eliminazione per identificare la causa principale

2. **Raccogli informazioni di diagnostica**
   - Verifica la presenza di errori JavaScript nella console del browser
   - Rivedere richieste e risposte di rete
   - Documenta i passaggi esatti per riprodurre il problema
   - Raccogliere screenshot e messaggi di errore

3. **Variabili di ambiente di prova**
   - Prova browser e dispositivi diversi
   - Eseguire test con account utente e autorizzazioni diversi
   - Verifica in diversi ambienti di rete
   - Confronta con moduli di lavoro o configurazioni

### Analisi e monitoraggio dei registri

**Debug della console del browser**

1. Apri strumenti per sviluppatori browser (F12)
2. Controlla la scheda della console per individuare eventuali errori JavaScript
3. Controlla la scheda Rete per le richieste non riuscite
4. Scheda Monitora prestazioni per operazioni lente

**Modelli di errore comuni**

- **Errori CORS**: problemi di richieste tra origini diverse con integrazioni API
- **Errori di autenticazione**: credenziali non valide o token scaduti
- **Errori di convalida**: conflitti della regola di convalida del campo o errori di sintassi
- **Timeout rete**: connessioni di rete lente o inaffidabili

## Ottenere ulteriore assistenza.

### Risorse self-service

**Sistema di assistenza predefinito**

- Usa il comando `/help` seguito da domande specifiche
- Accedere all’aiuto contestuale nell’interfaccia di Forms Experience Builder
- Rivedi attentamente i messaggi di errore per indicazioni specifiche
- Consulta la [Guida introduttiva di Forms Experience Builder](forms-ai-assistant-getting-started.md)

**Risorse di documentazione**

- [Prompt Library di Forms Experience Builder](ai-assistant-prompt-library.md)
- [Best practice per Forms Experience Builder](aem-forms-ai-assistant-best-practices.md)
- [Documentazione di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=it)

### Escalation e supporto

**Quando contattare il supporto tecnico**

- I problemi persistono dopo aver provato le soluzioni documentate
- Problemi a livello di sistema che interessano più utenti
- Problemi di sicurezza o integrità dei dati
- Problemi di integrazione che richiedono la configurazione a livello di sistema

**Informazioni da fornire**

- Descrizione dettagliata del problema e passaggi da riprodurre
- Schermate o registrazioni del problema
- Informazioni su browser e sistema
- Messaggi di errore e registri della console
- Dettagli di configurazione e integrazione del modulo

**Metodi di contatto**

- Amministratore di sistema: per problemi di ambiente e accesso
- Supporto tecnico: per problemi di integrazione e configurazione complessi
- Programma di accesso in anteprima: `aem-forms-ea@adobe.com` per problemi specifici del programma

### Community e condivisione delle conoscenze

**Procedure consigliate per la risoluzione dei problemi**

- Soluzioni documentali per riferimenti futuri
- Condividere con i membri del team gli approcci per la risoluzione dei problemi
- Contribuire alla knowledge base organizzativa
- Partecipare a community di utenti e forum

**Miglioramento continuo**

- Esame periodico dei problemi e delle soluzioni comuni
- Aggiornare le procedure di risoluzione dei problemi in base ai nuovi risultati
- Sessioni di formazione e condivisione delle conoscenze
- Feedback al team di prodotto per miglioramenti delle funzioni

Questa guida alla risoluzione dei problemi viene continuamente aggiornata in base al feedback degli utenti e alle nuove funzionalità di Forms Experience Builder. Per informazioni aggiornate e risorse aggiuntive, consulta la [documentazione di AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=it).
