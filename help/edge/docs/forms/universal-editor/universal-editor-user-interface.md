---
title: Navigare nell’interfaccia dell’editor universale per AEM Forms
description: Padroneggia l’interfaccia dell’editor universale per creare moduli AEM con Edge Delivery Services. Scopri gli strumenti essenziali, le scelte rapide da tastiera e i flussi di lavoro per creare moduli in modo efficiente con questa guida completa all’interfaccia.
keywords: editor universale, moduli AEM, edge delivery services, guida all’interfaccia, authoring di moduli, editor WYSIWYG, strumenti per la crezione di moduli, navigazione nell’interfaccia utente
feature: Edge Delivery Services
role: User, Developer, Admin
level: Beginner
exl-id: 90321e81-bb55-48b2-b329-4944bf926309
source-git-commit: 07160248d5b5817d155a118475878ce04a687a32
workflow-type: tm+mt
source-wordcount: '2355'
ht-degree: 97%

---


# Navigare nell’interfaccia dell’editor universale per AEM Forms

L’[editor universale](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) fornisce un’interfaccia visiva per la creazione di moduli AEM con Edge Delivery Services. Offre un&#39;esperienza di **What You See Is What You Get (WYSIWYG)** che mostra esattamente come i moduli appariranno agli utenti.

![Panoramica sull’interfaccia dell’editor universale](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface.png)

Questa guida ti aiuta a comprendere l’interfaccia per creare moduli in modo efficiente. Se non hai mai sperimentato la creazione di moduli o anche se hai esperienza nello sviluppo, questa guida ti aiuterà a:

**Scoprire le abilità essenziali:**

- Navigare nell’interfaccia in modo sicuro ed efficiente
- Utilizzare gli strumenti appropriati per le attività comuni di creazione dei moduli
- Sfruttare le scelte rapide da tastiera per aumentare la produttività
- Risolvere i problemi comuni dell’interfaccia

**Conoscere a fondo i principali flussi di lavoro:**

- Configurare l’area di lavoro per una produttività ottimale
- Creare moduli dal concetto alla pubblicazione
- Eseguire test e visualizzare l’anteprima dei moduli tra dispositivi
- Collaborare con i membri del team nei progetti modulo



## Guida introduttiva rapida

**Utenti nuovi:** inizia con [Strumenti essenziali](#essential-tools-for-form-building) per scoprire le funzionalità principali che userai più spesso.

**Utenti esperti:** passa a [Funzionalità avanzate](#advanced-features-and-integrations) per avere strumenti e integrazioni specializzati.

**Riferimento rapido:** utilizza le sezioni [Panoramica dell’interfaccia](#interface-overview) e [Scelte rapide da tastiera](#keyboard-shortcuts) per eseguire ricerche rapide.

>[!NOTE]
>
> Nessuna esperienza nell’authoring di moduli? Per istruzioni dettagliate sulla creazione di moduli, consulta [Guida introduttiva a Edge Delivery Services per AEM Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md).

## Panoramica dell’interfaccia

L’interfaccia dell’editor universale è strutturata in quattro aree principali, ognuna delle quali è progettata per attività specifiche:

![Layout interfaccia editor universale](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface1.png)

| **Area** | **Scopo** | **Uso principale** |
|----------|-------------|----------------|
| **[A: intestazione di Experience Cloud](#experience-cloud-header)** | Navigazione e gestione account | Passare da uno strumento Adobe all’altro, accedere alla guida e gestire le notifiche |
| **[B: barra degli strumenti dell’editor universale](#universal-editor-toolbar)** | Modifica e pubblicazione di moduli | Creare, modificare, visualizzare in anteprima e pubblicare moduli |
| **[C: pannello Proprietà](#properties-panel)** | Configurazione componente | Configurare i campi modulo, gestire la struttura dei contenuti e accedere alle funzioni avanzate |
| **[D: area di lavoro editor](#editor-canvas)** | Creazione di moduli visivi | Aggiungere componenti, disporre il layout, visualizzare anteprima in tempo reale |

**Flusso interfaccia:** la maggior parte degli utenti lavora principalmente nell’**area di lavoro editor** (D) e nel **pannello Proprietà** (C), utilizzando la **barra degli strumenti** (B) per azioni quali anteprima e pubblicazione.

## Strumenti essenziali per la creazione di moduli

Inizia qui se hai poca esperienza con l’editor universale. Questi sono gli strumenti di base che utilizzerai per la maggior parte delle attività di creazione moduli:

### **1. Area di lavoro dell’editor -La tua area di lavoro principale**

Nell’**area di lavoro dell’editor** puoi creare i moduli visivamente. Mostra esattamente come il modulo apparirà agli utenti.

![Area di lavoro dell’editor](/help/edge/docs/forms/universal-editor/assets/ue-editor.png)

**Azioni chiave:**

- **Aggiungere componenti** facendo clic sul pulsante **Aggiungi** nel pannello Proprietà
- **Selezionare gli elementi** facendo clic direttamente su di essi nell’area di lavoro
- **Visualizzare le modifiche in tempo reale** durante la configurazione dei componenti
- **Testare le interazioni** in modalità anteprima

### **2. Pannello Proprietà - Configurare i componenti**

Nel **pannello Proprietà** (lato destro) puoi personalizzare i componenti selezionati e gestire la struttura del modulo.

![Pannello Proprietà](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png)

**Funzioni essenziali:**

- **Modalità delle proprietà** (scelta rapida da tastiera `d`): configura le impostazioni del componente selezionato
- **Struttura del contenuto** (scelta rapida da tastiera`f`): naviga nella struttura del modulo
- **Aggiungere componenti** (scelta rapida da tastiera `a`): inserisci nuovi campi modulo
- **Azioni dei componenti**: duplica o elimina gli elementi selezionati

### **3. Nozioni di base sulla barra degli strumenti - Anteprima e pubblicazione**

La **barra degli strumenti dell’editor universale** fornisce azioni chiave per il test e la pubblicazione dei moduli.

![Barra degli strumenti dell’editor universale](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

**Strumenti fondamentali**

- **Modalità anteprima** (scelta rapida da tastiera`p`): testa il modulo così come verrà visualizzato dagli utenti
- **Modalità reattiva**: verifica l’aspetto del modulo sui dispositivi mobili
- **Apri pagina** (scelta rapida da tastiera `o`): visualizza modulo in una nuova scheda
- **Pubblica**: rendi il modulo attivo per gli utenti

### **4. Flusso di lavoro di avvio rapido**

**Per il primo modulo:**

1. **Iniziare la compilazione**: aggiungi componenti utilizzando il pulsante **Aggiungi** (`a`)
2. **Configura campi**: seleziona i componenti e utilizza le **Modalità delle proprietà** (`d`)
3. **Testa il modulo**: utilizza la **modalità anteprima** (`p`) per interagire con il modulo
4. **Verifica la visualizzazione per dispositivi mobili**: passa alla **modalità reattiva** per i test su dispositivi mobili
5. **Pubblica**: fai clic su **Pubblica** quando è pronto

**Punto di controllo per la convalida:**

- Puoi aggiungere e configurare campi modulo?
- La modalità anteprima funziona correttamente?
- Tutti i campi obbligatori sono configurati correttamente?
- Il modulo viene visualizzato correttamente sui dispositivi mobili?

## Intestazione di Experience Cloud

L’**Intestazione Experience Cloud** fornisce gli strumenti di navigazione e gestione account. La maggior parte dei creatori di moduli la utilizza occasionalmente per passare da uno Adobe all’altro o per accedere alla guida.

![Intestazione di Experience Cloud](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager-header.png)

**Elementi chiave:**

| **Elemento** | **Scopo** | **Quando utilizzare** |
|-------------|-------------|----------------|
| **Adobe Experience Cloud** | Passare ad altri strumenti di Adobe | Passaggio tra Sites, Assets, Forms |
| **Organizzazione** | Passaggio tra organizzazioni | Scenari di accesso per più organizzazioni |
| **Guida** | Accedere alla documentazione e al supporto | Quando si ha bisogno di assistenza o si desidera inviare un feedback |
| **Notifiche** | Visualizzare le attività e gli avvisi assegnati | Verificare lo stato del flusso di lavoro |
| **Soluzioni** | Accesso rapido ad altre soluzioni Adobe | Spostarsi da un prodotto Adobe a un altro |
| **Profilo utente** | Impostazioni account e disconnessione | Gestione dell’account o cambio di utente |

**Usi più comuni:**

- **Ottenere assistenza**: fai clic sull’icona della Guida per accedere alla documentazione e al supporto
- **Passaggio tra organizzazioni**: utilizzare il menu a discesa Organizzazione se si dispone dell’accesso per più organizzazioni

## Barra degli strumenti dell’editor universale

La **barra degli strumenti dell’editor universale** contiene gli strumenti principali di modifica e pubblicazione dei moduli. Questi sono organizzati in base alla frequenza di utilizzo e al flusso di lavoro tipico.

![Barra degli strumenti dell’editor universale](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

### **Strumenti flusso di lavoro giornalieri**

**Questi strumenti vengono utilizzati nella maggior parte delle sessioni di creazione moduli:**

#### **Modalità anteprima** (`p` scelta rapida)

**Scopo:** testare il modulo esattamente come verrà visualizzato dagli utenti\
**Quando utilizzare:** prima della pubblicazione, dopo aver apportato modifiche, per testare la funzionalità del modulo

![Modalità Anteprima](/help/edge/docs/forms/universal-editor/assets/ue-preview.png)

**Best practice:** visualizza l’anteprima dopo ogni modifica importante per rilevare i problemi in anticipo.

#### **Modalità reattiva**

**Scopo:** controllare la visualizzazione del modulo sui dispositivi mobili\
**Quando utilizzare:** dopo aver creato il modulo, prima della pubblicazione

![Modalità reattiva](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png)

**Best practice:** testa sempre la visualizzazione per dispositivi mobili. Molti utenti accederanno ai moduli dal proprio telefono.

#### **Aprire la pagina** (`o` scelta rapida)

**Scopo:** visualizzare il modulo in una nuova scheda senza l’interfaccia dell’editor\
**Quando utilizzare:** per test a schermo intero, condivisione con gli stakeholder per la revisione

![Apri pagina](/help/edge/docs/forms/universal-editor/assets/ue-openpage.png)

#### **Pubblica**

**Scopo:** rendere il modulo attivo e accessibile agli utenti\
**Quando utilizzare:** dopo un test approfondito in modalità Anteprima e Reattiva

![Pubblica](/help/edge/docs/forms/universal-editor/assets/ue-publish.png)

**Elenco di controllo convalida prima della pubblicazione:**

- Modulo testato in modalità Anteprima
- Reattività dispositivi mobili verificata
- Tutti i campi obbligatori configurati
- Azioni di invio correttamente funzionanti

### **Strumenti di navigazione**

#### **Pulsante Home**

**Scopo:** tornare alla pagina iniziale dell’editor universale\
**Quando utilizzare:** avvio del lavoro in un modulo diverso

![Pulsante Home](/help/edge/docs/forms/universal-editor/assets/ue-home.png)

#### **Barra di posizione** (`l` scelta rapida)

**Scopo:** passare direttamente a qualsiasi modulo tramite URL\
**Quando utilizzare:** passaggio rapido tra moduli specifici

![Barra della posizione](/help/edge/docs/forms/universal-editor/assets/ue-locationbar.png)

### **Strumenti di configurazione avanzati**

**Questi strumenti vengono utilizzati per scenari specifici o configurazioni avanzate:**

#### **Proprietà AEM Form**

**Scopo:** configurare le impostazioni a livello di modulo come Modello dati modulo (FDM) e le date di pubblicazione\
**Quando utilizzare:** configurazione delle integrazioni di dati, pianificazione della pubblicazione

![Proprietà modulo](/help/edge/docs/forms/universal-editor/assets/ue-formproperties.png)

![Procedura guidata proprietà modulo](/help/edge/docs/forms/universal-editor/assets/form-properties-ue.png)

Il pannello Proprietà modulo include le sezioni seguenti:

- **Invio**: definisci cosa accade dopo che un utente invia il modulo. È possibile scegliere tra più azioni di invio, ad esempio l’invio di dati tramite e-mail, l’invio a SharePoint, l’utilizzo di un modello dati modulo o l’integrazione con servizi come Adobe Experience Platform o Microsoft Power Automate. Per un elenco completo delle azioni di invio supportate, fai riferimento all’articolo [Azione di invio](/help/edge/docs/forms/universal-editor/submit-action.md).

- **Precompilazione**: configura il popolamento automatico dei campi modulo prima che l’utente interagisca con il modulo. Puoi connetterti a origini dati, ad esempio un Modello dati modulo (FDM), oppure utilizzare parametri URL per precompilare i campi, migliorando l’esperienza utente e riducendo l’input manuale. Per ulteriori informazioni, consulta l’articolo [Servizio di precompilazione](/help/edge/docs/forms/universal-editor/prefill-form.md).

- **Ringraziamento**: personalizza i contenuti visualizzati dagli utenti dopo l’invio del modulo. Puoi visualizzare un messaggio di conferma o reindirizzarli a un’altra pagina web, garantendo un’esperienza di completamento fluida e professionale. Per scoprire come configurare un messaggio di ringraziamento per i moduli, consulta l’articolo [Configurare un messaggio di ringraziamento](/help/edge/docs/forms/universal-editor/configure-thankyou-message.md).

#### **Editor regole** (accesso anticipato)

**Scopo:** aggiungere comportamenti dinamici, convalide e logica condizionale\
**Quando utilizzare:** creazione di moduli interattivi con logica di business complessa

![Editor di regole](/help/edge/docs/forms/universal-editor/assets/ue-ruleeditor.png)

>[!IMPORTANT]
>
> **Funzione di accesso anticipato:** l’editor di regole richiede un accesso speciale. Contatta [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) per abilitare questa funzione.
>
> **Ulteriori informazioni:** per istruzioni dettagliate, consulta la [Guida all’editor di regole](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md).

#### **Impostazioni dell’intestazione di autenticazione**

**Scopo:** impostare intestazioni di autenticazione personalizzate per i test di sviluppo\
**Quando utilizzare:** sviluppo locale con moduli richiesti per l’autenticazione

![Intestazioni di autenticazione](/help/edge/docs/forms/universal-editor/assets/ue-authenticationheader.png)

#### **Opzioni aggiuntive** (Menu con puntini di sospensione)

**Scopo:** accedere ad azioni meno comuni, ad esempio l’annullamento della pubblicazione\
**Quando utilizzare:** disconnessione dei moduli, accesso alle opzioni avanzate

![Opzioni aggiuntive](/help/edge/docs/forms/universal-editor/assets/ue-ellipsis.png)

## Pannello Proprietà

Il **pannello Proprietà** (lato destro) è il centro di controllo per la creazione e la configurazione dei moduli. Cambia in base a ciò che selezioni e fornisce strumenti diversi per attività diverse.

![Pannello Proprietà](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png)

### **Strumenti di base per la creazione di moduli**

**Questi strumenti sono essenziali per la creazione e l’organizzazione dei moduli:**

#### **Aggiungere componenti** (`a` scelta rapida)

**Scopo:** inserire nuovi campi ed elementi del modulo\
**Funzionamento:** mostra i componenti disponibili per il contenitore selezionato

![Aggiungere componenti](/help/edge/docs/forms/universal-editor/assets/ue-add.png)

**Componenti comuni:**

- Input di testo, e-mail, campi telefono
- Menu a discesa, pulsanti di scelta, caselle di controllo
- Caricamento di file, selettore data
- Pannelli e sezioni per l’organizzazione

#### **Modalità proprietà** (scelta rapida da tastiera `d`)

**Scopo:** configurare le impostazioni per i componenti selezionati\
**Quando utilizzarli:** dopo aver aggiunto un componente per personalizzarne il comportamento

![Modalità proprietà](/help/edge/docs/forms/universal-editor/assets/ue-properties.png)

**Impostazioni chiave:**

- Etichette di campo e testo segnaposto
- Regole di convalida (obbligatorio, formato, lunghezza)
- Valori predefiniti e testo di istruzioni
- Regole di visibilità condizionale

#### **Struttura contenuto** (scelta rapida da tastiera`f`)

**Scopo:** navigare e organizzare la struttura del modulo\
**Quando utilizzarle:** moduli complessi con più sezioni, ricerca di componenti specifici

![Struttura contenuto](/help/edge/docs/forms/universal-editor/assets/ue-contenttree.png)

**Vantaggi:**

- Navigazione rapida per qualsiasi componente
- Gerarchia dei moduli visivi
- Riordinamento semplice degli elementi

#### **Azioni dei componenti**

**Scopo:** gestire i componenti esistenti\
**Azioni disponibili:**

- **Duplica**: copia rapidamente i componenti ![Duplica](/help/edge/docs/forms/universal-editor/assets/ue-duplicate.png)
- **Elimina**: rimuovi i componenti (nessun prompt di conferma) ![Elimina](/help/edge/docs/forms/universal-editor/assets/ue-delete.png)

### **Funzioni e integrazioni avanzate**

**Questi strumenti abilitano funzionalità avanzate per moduli:**

+++Integrazione dei dati

#### **Origine dati**

**Scopo:** connetti i moduli ai sistemi di dati di back-end\
**Quando utilizzarla:** con moduli che devono leggere/scrivere su database o servizi esterni

![Origine dati](/help/edge/docs/forms/universal-editor/assets/ue-datasource.png)

**Funzionalità**

- Configurazione modello dati modulo (FDM)
- Compilazione dati dinamici
- Invio a sistemi esterni

+++

+++Strumenti basati sull’intelligenza artificiale

#### **Generare varianti**

**Scopo:** utilizza l’intelligenza artificiale per creare diverse versioni del contenuto del modulo\
**Quando utilizzarla:** per la sperimentazione con testo, layout o approcci diversi

    .[Generare varianti](/help/edge/docs/forms/universal-editor/assets/ue-variations.png)

**Ulteriori informazioni:** [Guida di generare varianti](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/generative-ai/generate-variations)

#### **Bozze di contenuto**

**Scopo:** creare e salvare le versioni preliminari del testo\
**Quando utilizzarle:** per iterazione nella copia del modulo, salvataggio di opzioni di testo alternative

![Bozze di contenuto](/help/edge/docs/forms/universal-editor/assets/ue-contentdraft.png)

+++

+++Test e ottimizzazione

#### **Test A/B**

**Scopo:** confronta le varianti del modulo per ottimizzare le prestazioni\
**Quando utilizzare:** ottimizzazione dei tassi di conversione, test delle diverse progettazioni

![Test A/B](/help/edge/docs/forms/universal-editor/assets/ue-abtesting.png)

#### **Sperimentazione**

**Scopo:** eseguire test controllati sulle progettazioni dei moduli\
**Quando utilizzare:** ottimizzazione dei moduli basati su dati, test dell’esperienza utente

    ![Sperimentazione](/help/edge/docs/forms/universal-editor/assets/ue-experimentation.png)

+++

+++Strumenti Collaboration

#### **Gestione attività**

**Scopo:** organizzare il flusso di lavoro del team per i progetti modulo\
**Quando utilizzare:** sviluppo di moduli per più persone, tracciamento di progetti

![Gestione attività](/help/edge/docs/forms/universal-editor/assets/ue-taskmanagement.png)

#### **Personalizzazione**

**Scopo:** connettersi ad Adobe Experience Platform per esperienze personalizzate\
**Quando utilizzare:** creazione di moduli personalizzati basati su dati utente

    ![Personalizzazione](/help/edge/docs/forms/universal-editor/assets/ue-personalizaton.png)

+++

## Area di lavoro dell’editor

L’**area di lavoro dell’editor** è l’area di lavoro principale in cui vengono creati visivamente i moduli. Mostra esattamente come il modulo apparirà agli utenti e fornisce feedback in tempo reale mentre apporti modifiche.

![Area di lavoro dell’editor](/help/edge/docs/forms/universal-editor/assets/ue-editor.png)

**Funzioni chiave:**

- **Modifica WYSIWYG**: visualizza subito le modifiche mentre le apporti
- **Interazione diretta**: fai clic su un componente per selezionarlo e modificarlo
- **Anteprima in tempo reale**: passa alla modalità anteprima per testare la funzionalità
- **Visualizzazione reattiva**: attiva/disattiva le visualizzazioni del dispositivo per verificarne la compatibilità

**Best practice**

- **Iniziare con la struttura**: aggiungi sezioni principali prima dei componenti dettagliati
- **Testare frequentemente**: utilizza regolarmente la modalità anteprima per rilevare i problemi in anticipo
- **Pensare mobile-first**: verifica la modalità reattiva durante il processo di progettazione

## Scelte rapide da tastiera

Impara ad usare queste scelte rapide per creare moduli in modo più rapido ed efficiente:

| **Scelta rapida da tastiera** | **Azione** | **Quando utilizzare** |
|--------------|------------|----------------|
| `a` | Aprire l’elenco dei componenti | Aggiungere nuovi campi modulo |
| `d` | Aprire le proprietà del componente | Configurazione degli elementi selezionati |
| `f` | Attivare/disattivare la struttura del contenuto | Navigazione in moduli complessi |
| `p` | Attivare/disattivare la modalità di anteprima | Testare la funzionalità del modulo |
| `o` | Aprire il modulo in una nuova scheda | Test a schermo intero |
| `l` | Concentrarsi sulla barra di posizione | Passaggio a diversi moduli |

**Suggerimento pro:** utilizza queste scelte rapide da tastiera in combinazione. Ad esempio, seleziona un componente, premi `d` per configurarlo, quindi `p` per testare le modifiche.

## Flussi di lavoro comuni

### **Creazione del primo modulo**

1. **Aggiungi struttura**: utilizzare `a` per aggiungere un pannello per le sezioni del modulo
2. **Aggiungi campi**: inserire input di testo, e-mail e altri componenti
3. **Configura proprietà**: selezionare ogni campo e premere `d` per impostare le etichette e la convalida
4. **Funzionalità del test**: premere `p` per visualizzare l’anteprima e testare il modulo
5. **Controlla visualizzazione su su dispositivo mobile**: utilizzare la modalità reattiva per verificare la visualizzazione su dispositivo mobile
6. **Pubblica**: fare clic su Pubblica per andare live

### **Modifica di moduli esistenti**

1. **Naviga nella struttura**: utilizzare la struttura contenuto (`f`) per trovare rapidamente i componenti
2. **Seleziona e modifica**: fare clic direttamente sui componenti o utilizzare la struttura contenuto
3. **Testa le modifiche**: visualizzare anteprima (`p`) dopo ogni modifica significativa
4. **Convalida flusso di lavoro**: testare il flusso di modulo completo prima della ripubblicazione

### **Collaborazione con i team**

1. **Gestione attività**: assegnare sezioni di modulo specifiche ai membri del gruppo
2. **Condividi per revisione**: utilizzare Apri pagina (`o`) per condividere anteprime chiare
3. **Test congiunto**: utilizzare la modalità Anteprima per le sessioni di test collaborativo
4. **Tracciamento avanzamento**: controllare le notifiche per aggiornamenti attività

## Risoluzione dei problemi comuni

### **Problemi di interfaccia**

+++Impossibile caricare gli elementi dell&#39;interfaccia

**Problema:** i pulsanti della barra degli strumenti, il pannello delle proprietà o altri elementi dell’interfaccia non vengono visualizzati

**Soluzioni:**

- **Aggiorna la pagina**: un semplice aggiornamento del browser spesso risolve i problemi di caricamento
- **Verifica compatibilità browser**: utilizzare Chrome, Firefox o Safari
- **Cancella cache del browser**: rimuovere i file memorizzati nella cache che potrebbero non essere aggiornati
- **Verifica autorizzazioni**: assicurarsi di disporre dell’accesso corretto per la modifica dei moduli

+++

+++I componenti non rispondono

**Problema:** impossibile selezionare i componenti o il pannello Proprietà non viene aggiornato

**Soluzioni:**

- **Fai clic direttamente sui componenti**: evita di fare clic su aree vuote
- **Utilizza la struttura del contenuto**: premi `f` e seleziona i componenti dalla struttura
- **Verifica la presenza di elementi sovrapposti**: alcuni componenti potrebbero bloccarne altri
- **Ricarica il modulo**: utilizza la barra di posizione (`l`) per ricaricare il modulo corrente

+++

+++Problemi relativi alla modalità Anteprima

**Problema:** la modalità anteprima non funziona correttamente o mostra errori

**Soluzioni:**

- **Verifica la convalida del modulo**: verifica che tutti i campi obbligatori siano configurati correttamente
- **Testa prima in modalità di modifica**: verifica il funzionamento dei componenti prima dell’anteprima
- **Cancella cache del browser**: gli script memorizzati nella cache potrebbero interferire con l’anteprima
- **Verifica la configurazione del componente**: rivedi le impostazioni della modalità delle proprietà per individuare eventuali errori

+++

## Best practice per la creazione efficiente dei moduli

### **Suggerimenti per l’organizzazione**

- **Utilizza nomi descrittivi**: etichetta i componenti in modo chiaro nella modalità Proprietà
- **Raggruppa campi correlati**: utilizza i pannelli per organizzare in modo logico le sezioni del modulo
- **Pianifica prima di creare**: crea uno schizzo della struttura del modulo prima di iniziare
- **Semplifica**: evita di caricare eccessivamente gli utenti con troppi campi

### **Esperienza utente**

- **Testa frequentemente**: utilizza la modalità Anteprima dopo ogni modifica importante
- **Pensa come gli utenti**: considera l’esperienza completa di compilazione dei moduli
- **Fornisci etichette chiare**: rendi evidenti gli scopi del campo agli utenti
- **Aggiungi testo utile**: utilizza il testo della Guida per campi complessi

### **Ottimizzazione delle prestazioni**

- **Riduci a icona i componenti**: utilizza solo i campi modulo necessari
- **Ottimizza immagini**: comprimi tutte le immagini utilizzate nei moduli
- **Test su dispositivi mobili**: garantisci buone prestazioni sulle connessioni mobili più lente
- **Convalida anticipata**: imposta una convalida corretta per evitare errori di invio

## Passaggi successivi

Ora che conosci l’interfaccia dell’editor universale:

1. **Esercitati con un modulo semplice**: inizia con i campi di base per imparare
2. **Esplora le funzionalità avanzate**: prova gli strumenti e le integrazioni basati sull’intelligenza artificiale appena sono pronti
3. **Scopri l’authoring dei moduli**: consulta la [Guida introduttiva](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
4. **Editor di regole master**: aggiungi comportamenti dinamici con la [Guida dell’editor regole](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md)

**Ricorda:** l’editor universale è progettato per rendere intuitiva la creazione di moduli. Inizia con le funzionalità essenziali ed esplora gradualmente quelle avanzate ogni volta che ne hai bisogno.
