---
title: Guida introduttiva di Forms Experience Builder
description: Scopri come utilizzare Forms Experience Builder per creare e gestire moduli con divulgazione progressiva per tutti i tipi di utenti
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: fe34b44d02c308e7d18a08dd05f21abc67bd0cb2
workflow-type: tm+mt
source-wordcount: '2013'
ht-degree: 6%

---


# Guida introduttiva di Forms Experience Builder

>[!NOTE]
>
> La funzionalità Forms Experience Builder è disponibile nel **programma di accesso anticipato**. Se sei interessato, invia una breve e-mail dal tuo indirizzo di lavoro a `aem-forms-ea@adobe.com` per richiedere l&#39;accesso alla funzionalità.

>[!IMPORTANT]
>
> **Documentazione soggetta a modifiche**: questa documentazione è attualmente in fase di test rispetto al prodotto ed è soggetta ad aggiornamenti e revisioni. Funzionalità, comandi ed esempi potrebbero cambiare man mano che Forms Experience Builder continua ad evolversi durante il programma Early Access.

Questa guida completa ti aiuta a iniziare a creare e gestire i moduli utilizzando la tecnologia di intelligenza artificiale per conversazioni. Sia che si tratti di un principiante che desidera creare il primo modulo o di un utente avanzato che desidera sfruttare funzionalità sofisticate, è possibile trovare informazioni dettagliate ed esempi pratici per guidare il percorso attraverso le funzionalità di Forms Experience Builder.

## Prerequisiti e configurazione

### &#x200B;1. Richiedi accesso

Forms Experience Builder è attualmente disponibile come parte del programma di accesso anticipato (EA). Per partecipare e ottenere l&#39;accesso, è necessario disporre delle seguenti informazioni:

**Informazioni richieste**

- **ID organizzazione IMS**: identificatore organizzazione Adobe
- **ID programma**: identificatore del programma specifico in Adobe Experience Cloud
- **Dettagli progetto**: Timeline, ambito e casi d&#39;uso previsti
- **E-mail ufficiale di lavoro**: associata all&#39;account Adobe della tua organizzazione

**Come ottenere l&#39;ID organizzazione IMS e l&#39;ID programma**

Per i passaggi dettagliati per individuare l’ID organizzazione IMS e l’ID programma, consulta:

- [Guida alla configurazione dell&#39;organizzazione Adobe Experience Cloud](/help/onboarding/cloud-manager-introduction.md)
- [Gestione di programmi e ambienti](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

**Richiedi accesso**

1. Raccogli l’ID organizzazione IMS e l’ID programma utilizzando le guide precedenti
2. Invia un&#39;e-mail a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) richiedendo l&#39;accesso
3. Includi nella richiesta:
   - Nome organizzazione e ID organizzazione IMS
   - ID programma
   - Timeline e ambito del progetto
   - Casi d’uso previsti e obiettivi aziendali

>[!IMPORTANT]
>
> **Programma di disponibilità limitata**: l&#39;accesso a Forms Experience Builder è soggetto all&#39;approvazione delle parti interessate interne. Adobe esaminerà la tua richiesta in base alla capacità del programma e all’allineamento con i criteri di accesso in anteprima. L&#39;approvazione non è garantita e dipende dalla disponibilità del programma corrente.

### &#x200B;2. Verificare che Forms sia abilitato

Prima di utilizzare Forms Experience Builder, assicurati che [AEM Forms sia abilitato per il tuo ambiente](/help/forms/setup-forms-cloud-service.md).


### &#x200B;3. Configurare l’ambiente


- **Per Edge Delivery Services (EDS):**

   - [Ambiente di configurazione per Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
   - [Creare un nuovo modulo utilizzando il modello Forms di Edge Delivery](/help/edge/docs/forms/universal-editor/create-forms.md)

- **Per moduli basati su Componenti core:**

   - Nell’istanza di Adobe Experience Manager, accedi a Forms > Forms e documenti
   - [Creare una nuova pagina utilizzando il modello Componenti core](/help/forms/creating-adaptive-form-core-components.md)


## Inizio rapido

### Accedere a Forms Experience Builder

Forms Experience Builder è disponibile nell’interfaccia utente di gestione Forms, nell’editor universale e nell’editor di Forms adattivo. Per accedere al modulo è possibile utilizzare uno dei seguenti metodi:

**Interfaccia utente di gestione Forms (per i componenti core)**

1. **Passa a Forms**: vai a AEM > Forms > Forms e documenti
1. Fai clic sull’icona di Forms Experience Builder nella barra degli strumenti. Si trova in alto a sinistra nell’interfaccia utente.
   ![Icona Assistente IA*](/help/edge/docs/forms/assets/forms-manager.gif){width="50%"}
1. Inizia la creazione del modulo di conversazione


**Editor Forms adattivo (per componenti core)**

1. Passa a AEM > Forms > Forms e documenti
2. [Creare un nuovo modulo utilizzando il modello Componenti core](/help/forms/creating-adaptive-form-core-components.md)
3. Apri il modulo per la modifica
4. Fai clic sull’icona di Forms Experience Builder nella barra degli strumenti dell’editor
   ![Icona Assistente IA*](/help/edge/docs/forms/assets/adaptive-forms-editor.gif){width="75%"}

5. Inizia la creazione del modulo di conversazione


**Editor universale (per Edge Delivery Services Forms)**

1. Segui la [guida all&#39;installazione di Edge Delivery Services](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md) per creare la tua pagina EDS
1. Passare alla pagina EDS in Universal Editor
1. Cerca l’icona Forms Experience Builder nel pannello a destra
1. Fare clic per aprire l&#39;interfaccia di conversazione



### Il primo modulo

| Esempio di conversazione |   |
|--------------------------------------------------------------------------------------------------------------------------------------------|---|
| **Prova questa conversazione per creare un modulo di contatto completo (basato sulla demo del Summit):**<br><br>**Tu:** &quot;Crea un modulo di contatto per acquisire informazioni personali tra cui nome completo, indirizzo e-mail, numero di telefono, nome della società, titolo del processo e un campo del messaggio per le richieste&quot;<br><br>**AI:** Seleziona un modello<br>    Un elenco a discesa per selezionare un modello <br><br>**AI:** Seleziona un tema<br>    Un elenco a discesa per selezionare un tema <br><br>**AI:** Crea modulo | ![Primo modulo](/help/edge/docs/forms/assets/create-form.png) |
| <br>**AI:** Apri modulo creato | </br> Il modulo viene creato e aperto nell&#39;editor |


### Comandi essenziali

| Simbolo | Scopo | Esempio di utilizzo |
|--------|---------|---------------|
| `/` | Azioni rapide e collegamenti | `/create-form contact form`, `/help validation rules`, `/update-layout wizard` |
| `@` | Fai riferimento a campi modulo esistenti | `@email`, `@firstName`, `Make @phoneNumber required` |
| Testo normale | Conversazione naturale | &quot;Aggiungi un campo numero di telefono richiesto&quot;, &quot;Crea convalida per e-mail&quot; |

**Esempi di comandi specifici:**

- `/create-form customer survey` - Crea un nuovo modulo di sondaggio cliente
- `/add-field @email validation` - Aggiunge la convalida al campo e-mail esistente
- `/create-rule show @spouse if @maritalStatus equals married` - Crea logica condizionale
- `/configure-submit to email support@company.com` - Configura l&#39;invio di e-mail
- `/help multi-step forms` - Ottiene informazioni sulla creazione di moduli con più passaggi

### Suggerimenti per il successo

- **Specificare**: &quot;Aggiungere un campo e-mail obbligatorio con convalida&quot; funziona meglio di &quot;aggiungere e-mail&quot;
- **Riferimento a campi esistenti**: utilizzare `@fieldName` per modificare i moduli
- **Chiedi aiuto**: digita `/help` seguito dalla domanda
- **Iterazione**: apporta una modifica alla volta per ottenere risultati ottimali


## Metodi per iniziare a creare un modulo

### &#x200B;1. Inizia con i prompt del linguaggio naturale

Descrivi i requisiti del modulo nel linguaggio naturale e Forms Experience Builder genera la struttura completa del modulo:

**Esempi:**

- &quot;Crea un modulo di richiesta di prestito con informazioni personali, dettagli finanziari e caricamenti di documenti&quot;
- &quot;Creare un modulo di feedback dei clienti con valutazioni, commenti e categorie di prodotti&quot;
- &quot;Ho bisogno di un modulo di registrazione in più passaggi per una conferenza con elaborazione dei pagamenti&quot;

### &#x200B;2. Importare e convertire

Trasforma i moduli e i documenti esistenti in esperienze moderne e interattive:

**Origini supportate:**

- **PDF forms**: carica PDF statici per convertirli in moduli digitali interattivi con convalide.
- **Schermate o immagini**: carica foto dei moduli cartacei per generare versioni digitali funzionali
- **XFA Forms**: convertire i moduli basati su XFA legacy in moduli reattivi moderni

**Come importare:**

1. Fai clic sull’icona dell’allegato nell’interfaccia di Forms Experience Builder
2. Carica il file (PDF, immagine, progettazione Figma, ecc.)
3. Descrivi le tue esigenze:
   - &quot;Converti questo modulo PDF in una versione digitale&quot;
   - &quot;Crea un modulo che corrisponda a questo layout di schermata&quot;
   - “Crea questo modulo dalla mia progettazione Figma”

**Tipi di file supportati:**

- **Immagini** (PNG, JPG, GIF): layout di moduli, modelli di interfaccia utente, moduli digitalizzati, schizzi disegnati a mano
- **File PDF**: moduli, specifiche, documenti, Acroform, moduli XFA esistenti
- **Schermate**: schermate di app desktop/mobili, foto in formato cartaceo, schizzi su lavagna
- **Schizzi disegnati a mano**: schizzi di tovagliolo, wireframe, disegni concettuali (fotografati)

### Interazioni chiave

#### Aggiunta di elementi modulo

**Aggiunte di base:**

    👤 Sei: &quot;Aggiungi una sezione per informazioni personali&quot;
    👤 Sei: &quot;Includi un caricamento di file per la ripresa&quot;
    👤 Sei: &quot;Aggiungi un menu a discesa per la selezione del paese&quot;

**Specifiche dettagliate:**

    👤 You: &quot;Aggiungi un pannello di informazioni personali con campi per nome completo, data di nascita, numero di telefono e indirizzo e-mail&quot;
    👤 You: &quot;Includi un componente di caricamento file sicuro per i documenti, limitato ai file PDF sotto 5 MB&quot;
    👤 You: &quot;Aggiungi un elenco a discesa paese con opzioni per USA, Canada, Regno Unito e Germania&quot;

#### Creazione di un comportamento dinamico

**Logica semplice:**

    👤 You: &quot;Show additional fields when &#39;Other&#39; is selected&quot;
    🤖 AI: &quot;Creata una regola condizionale che mostra campi aggiuntivi quando si sceglie &#39;Other&#39;&quot;
    
    👤 You: &quot;Rendi obbligatorio il campo e-mail&quot;
    🤖 AI: &quot;Aggiornato il campo e-mail affinché sia obbligatorio con la convalida&quot;
    
    👤 You: &quot;Calcola il totale automaticamente&quot;
    🤖 AI: &quot;Aggiunta della logica di calcolo per calcolare automaticamente i totali&quot;

**Regole di business complesse:**

    👤 Sei: &quot;Mostra i campi di informazioni sul coniuge solo quando lo stato civile è impostato su &#39;Coniugato&#39;&quot;
    🤖 AI: &quot;Creata una regola condizionale che visualizza i campi del coniuge in base allo stato civile&quot;
    
    👤 Tu: &quot;Calcola il costo totale moltiplicando la quantità e il prezzo, quindi aggiungi il 10% di imposta&quot;
    🤖 AI: &quot;Aggiunta della logica di calcolo con la quantità, il prezzo e il calcolo delle imposte&quot;
    
    👤 Tu: &quot;Abilita il pulsante Invia solo quando tutti i campi obbligatori sono completati e i termini sono accettati&quot;
    🤖 AI: &quot;Creazione della logica di convalida che abilita l&#39;invio solo quando tutte le condizioni sono soddisfatte&quot;

#### Layout e progettazione dei moduli

**Modifiche del layout:**

    👤 Sei: &quot;Rendi questo un modulo con più passaggi&quot;
    🤖 AI: &quot;Ha convertito il modulo in un layout progressivo con navigazione&quot;
    
    👤 Tu: &quot;Organizza i campi in due colonne&quot;
    🤖 AI: &quot;Ha aggiornato il layout per visualizzare i campi in una disposizione a due colonne&quot;
    
    👤 Tu: &quot;Converti in un layout a soffietto&quot;
    🤖 AI: &quot;Ha trasformato il modulo per utilizzare le sezioni in stile soffietto&quot;

**Miglioramenti alla progettazione:**

    👤 Sei: &quot;Crea un modulo stile procedura guidata con 3 passaggi: informazioni personali, preferenze e revisione&quot;
    🤖 AI: &quot;Crea un modulo procedura guidata con tre passaggi distinti e navigazione&quot;
    
    👤 Tu: &quot;Disponi i campi indirizzo in un layout compatto a due colonne&quot;
    🤖 AI: &quot;Organizza i campi indirizzo in un formato compatto a due colonne&quot;
    
    👤 Tu: &quot;Aggiorna il layout in modo che corrisponda al wireframe allegato&quot;
    🤖 AI: &quot;Modificato il layout in modo che corrisponda al riferimento progettazione fornito&quot;

### Invia configurazione

Forms Experience Builder può configurare vari endpoint di invio per collegare i moduli a sistemi e servizi esterni:

| Invia tipo di azione | Comando di installazione | Caso d’uso |
|------------------|---------------|----------|
| **E-mail** | &quot;Invia modulo a e-mail&quot; | Notifiche e conferme per l’invio di moduli |
| **API REST** | &quot;Invia all’endpoint REST&quot; | Applicazioni personalizzate e sistemi di terze parti |
| **Archiviazione cloud** | &quot;Salva in Azure/SharePoint&quot; | Archiviazione dei documenti e gestione dei file |
| **Flusso di lavoro** | &quot;Connetti a Power Automate&quot; | Automazione e approvazione dei processi aziendali |
| **Marketing** | &quot;Integrare con Marketo&quot; | Gestione dei lead e automazione del marketing |

**Esempi di configurazione invio avanzata:**

    👤 Tu: &quot;Invia invii di moduli a hr@company.com e crea un caso nel nostro sistema di gestione delle relazioni con i clienti&quot;
    🤖 AI: &quot;Invio di e-mail configurato e azione di invio CRM&quot;
    
    👤 Tu: &quot;Invia dati all&#39;endpoint REST API e attiva il nuovo flusso di lavoro del cliente&quot;
    🤖 AI: &quot;Configura l&#39;invio REST API con i trigger del flusso di lavoro&quot;
    
    👤 Tu: &quot;Invia risposte e-mail al team di vendita e aggiungi il lead alla nostra piattaforma di automazione marketing&quot;
    🤖 AI: &quot;Invio multicanale configurato con automazione e-mail e marketing&quot;





## Operazioni avanzate per moduli


### Creazione di regole complesse

Creare regole di convalida e business sofisticate che rispondano alle interazioni degli utenti e garantiscano l&#39;integrità dei dati:

    👤 Sei: &quot;Mostra la sezione dell&#39;indirizzo solo se l&#39;utente seleziona &#39;Spedisci a indirizzo diverso&#39;&quot;
    🤖 AI: &quot;Creata una regola condizionale che mostra/nasconde il pannello dell&#39;indirizzo in base alla selezione della casella di controllo&quot;

### Creazione di moduli in più passaggi

    👤 You: &quot;Crea un modulo progressivo con 3 passaggi: informazioni personali, preferenze, conferma&quot;
    🤖 AI: &quot;Crea un modulo progressivo con navigazione tra passaggi e convalida in ogni fase&quot;

### Tipi di campo avanzati

- Caricamento di file con restrizioni di convalida e dimensione per la gestione dei documenti
- Selettori di date con vincoli e regole aziendali per la programmazione
- Elenchi a discesa con opzioni dinamiche che cambiano in base alle selezioni effettuate dagli utenti
- Pulsanti di scelta con logica condizionale per strutture decisionali complesse


### Conversione da PDF a modulo

    👤 Sei: &quot;Converti questo PDF in un modulo interattivo&quot;
    🤖 AI: &quot;Ha analizzato PDF e creato un modulo con i tipi di campo e la convalida appropriati&quot;





## Assistenza e formazione sul prodotto

Forms Experience Builder può anche insegnarti le funzioni di AEM Forms:

### Fai domande come:

- “Come si crea un modulo con più passaggi?”
- “Qual è la differenza tra pannelli e sezioni?”
- “Come si configurano le notifiche e-mail?”
- “Quali sono le best practice per i moduli compatibili con i dispositivi mobili?”
- “Come si applicano i temi ai moduli?”

### Ottieni assistenza per:

- Concetti e terminologia di AEM Forms
- Istruzioni passo dopo passo per le funzioni complesse
- Best practice e consigli
- Risoluzione dei problemi comuni

## Best practice

### Progettazione modulo

- **Semplifica**: inizia con campi essenziali e aggiungi complessità solo quando necessario per evitare di sovraffollare gli utenti
- **Usa etichette chiare**: le finalità dei campi sono evidenti con etichette descrittive che guidano gli utenti attraverso il modulo
- **Fornisci testo di aiuto**: guida gli utenti attraverso campi complessi con esempi e guida contestuale
- **Verifica approfondita**: convalida tutti i percorsi utente per garantire il corretto funzionamento dei moduli in tutti gli scenari

### Esperienza utente

- **Divulgazione progressiva**: mostra i campi rilevanti in base al contesto per ridurre il carico cognitivo e migliorare i tassi di completamento
- **Cancella navigazione**: aiuta gli utenti a capire dove si trovano nel modulo e quali passaggi rimangono
- **Progettazione reattiva**: assicurarsi che i moduli funzionino su tutti i dispositivi e su tutte le dimensioni dello schermo per la massima accessibilità
- **Accessibilità**: attieniti alle linee guida WCAG per rendere i moduli utilizzabili da persone con disabilità

### Prestazioni

- **Ottimizza conteggio campi**: richiedi solo le informazioni necessarie per ridurre l&#39;abbandono dei moduli e migliorare i tassi di completamento
- **Utilizza la convalida appropriata**: evita errori prima dell&#39;invio per fornire feedback e indicazioni immediati
- **Tassi di completamento dei test**: monitora e migliora l&#39;efficacia dei moduli tramite analisi e feedback degli utenti
- **Aggiornamenti regolari**: i moduli sono aggiornati in base alle esigenze aziendali e alle aspettative degli utenti per prestazioni ottimali

### Coerenza del brand

- **Crea modelli marchio**: prepara modelli di modulo con marchio con i colori, i font e lo stile della tua organizzazione prima di iniziare la creazione del modulo
- **Definisci standard di stile**: stabilisce stili di pulsante, layout di campo e linee guida di spaziatura coerenti a cui è possibile fare riferimento nei prompt
- **Utilizzare le risorse per i marchi**: prepara logo, codici colore e linee guida per i marchi per un riferimento semplice durante la creazione dei moduli
- **Libreria modelli**: crea una raccolta di modelli di modulo con marchio per i casi d&#39;uso comuni (contatto, registrazione, feedback)
- **Richieste di stile**: includere istruzioni specifiche per il marchio: &quot;Utilizza il blu società (#1234AB) per i pulsanti e il font aziendale Helvetica&quot;



## Risoluzione di problemi

| Problema | Correzione rapida |
|-------|-----------|
| **Impossibile caricare l&#39;interfaccia** | Aggiorna browser, controlla la connessione Internet |
| **Comandi non funzionanti** | Prova `/help` o usa il linguaggio naturale |
| **@fieldName non riconosciuto** | Controlla ortografia, assicurati che il campo esista |
| **Impossibile caricare il file** | Usa PDF/JPG/PNG inferiore a 10 MB |
| **Il modulo ha un aspetto errato** | Essere più specifici: &quot;Rendi mobile-friendly&quot; |
| **Impossibile inviare la configurazione** | Verifica credenziali e autorizzazioni API |

**Hai ancora bisogno di aiuto?** Digitare `/help` seguito da una domanda specifica o contattare l&#39;amministratore di sistema.

Per ulteriore supporto, fare riferimento alla [Libreria prompt di Forms Experience Builder](ai-assistant-prompt-library.md) principale o contattare l&#39;amministratore di sistema per assistenza tecnica.
