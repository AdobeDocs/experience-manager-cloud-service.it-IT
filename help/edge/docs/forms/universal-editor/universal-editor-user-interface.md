---
title: Navigare nell’interfaccia dell’editor universale per AEM Forms
description: Padroneggia l’interfaccia di Universal Editor per creare AEM Forms con Edge Delivery Services. Scopri gli strumenti essenziali, le scelte rapide e i flussi di lavoro per creare moduli in modo efficiente con questa guida completa all’interfaccia.
keywords: editor universale, AEM forms, servizi di consegna edge, guida all’interfaccia, authoring di moduli, editor WYSIWYG, strumenti per la generazione di moduli, navigazione nell’interfaccia utente
feature: Edge Delivery Services
role: User, Developer, Admin
level: Beginner
exl-id: 90321e81-bb55-48b2-b329-4944bf926309
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: tm+mt
source-wordcount: '2358'
ht-degree: 4%

---


# Navigare nell’interfaccia dell’editor universale per AEM Forms

[Universal Editor](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) fornisce un&#39;interfaccia visiva per la creazione di AEM Forms con Edge Delivery Services. Questa guida ti aiuta a comprendere l’interfaccia per creare moduli in modo efficiente.

![Panoramica dell&#39;interfaccia dell&#39;editor universale](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface.png)

## Panoramica

L&#39;editor universale offre un&#39;esperienza di **What You See Is What You Get (WYSIWYG)** che visualizza esattamente l&#39;aspetto dei moduli per gli utenti. Che tu sia un nuovo utente nella creazione di moduli o uno sviluppatore esperto, questa guida ti aiuterà a:

**Scopri le abilità essenziali:**

- Navigare nell’interfaccia in modo sicuro ed efficiente
- Utilizzare gli strumenti appropriati per le attività comuni di creazione dei moduli
- Sfruttare le scelte rapide da tastiera per aumentare la produttività
- Risolvere i problemi comuni dell’interfaccia

**Flussi di lavoro chiave master:**

- Configurate l&#39;area di lavoro per una produttività ottimale
- Creare moduli dal concetto alla pubblicazione
- Test e anteprima dei moduli tra dispositivi
- Collaborazione con i membri del team nei progetti modulo

## Guida introduttiva

**Utenti nuovi:** Inizia con [Strumenti essenziali](#essential-tools-for-form-building) per scoprire le funzionalità principali che userai più spesso.

**Utenti esperti:** passa a [Funzionalità avanzate](#advanced-features-and-integrations) per strumenti e integrazioni speciali.

**Riferimento rapido:** Utilizzare le sezioni [Panoramica dell&#39;interfaccia](#interface-overview) e [Scelte rapide da tastiera](#keyboard-shortcuts) per eseguire ricerche rapide.

>[!NOTE]
>
> Sei nuovo all’authoring di moduli? Per istruzioni dettagliate sulla creazione di moduli, consulta [Guida introduttiva a Edge Delivery Services per AEM Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md).

## Panoramica dell’interfaccia

L&#39;interfaccia di Universal Editor è strutturata in quattro aree principali, ognuna delle quali è progettata per attività specifiche:

![Layout interfaccia editor universale](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface1.png)

| **Area** | **Scopo** | **Uso primario** |
|----------|-------------|----------------|
| **[A: intestazione di Experience Cloud](#experience-cloud-header)** | Navigazione e gestione account | Passare da uno strumento Adobe all’altro, accedere alla guida e gestire le notifiche |
| **[B: barra degli strumenti dell’editor universale](#universal-editor-toolbar)** | Modifica e pubblicazione di moduli | Creare, modificare, visualizzare in anteprima e pubblicare moduli |
| **[C: pannello Proprietà](#properties-panel)** | Configurazione del componente | Configurare i campi modulo, gestire la struttura del contenuto e accedere alle funzioni avanzate |
| **[D: area di lavoro editor](#editor-canvas)** | Creazione di moduli visivi | Aggiungi componenti, disponi il layout, vedi anteprima in tempo reale |

**Flusso interfaccia:** La maggior parte degli utenti lavora principalmente nell&#39;**Area di lavoro editor** (D) e nel **Pannello proprietà** (C), utilizzando la **Barra degli strumenti** (B) per azioni quali anteprima e pubblicazione.

## Strumenti essenziali per la creazione di moduli

Inizia qui se hai poca esperienza con Universal Editor. Questi sono gli strumenti di base che verranno utilizzati per la maggior parte delle attività di creazione moduli:

### **1. Area di lavoro dell&#39;editor - Workspace principale**

Nell&#39;area di lavoro **Editor** è possibile creare i moduli visivamente. Viene visualizzato esattamente l&#39;aspetto del modulo per gli utenti.

![Area di lavoro editor](/help/edge/docs/forms/universal-editor/assets/ue-editor.png)

**Azioni chiave:**

- **Aggiungi componenti** facendo clic sul pulsante **Aggiungi** nel pannello Proprietà
- **Selezionare gli elementi** facendo clic direttamente su di essi nell&#39;area di lavoro
- **Visualizza modifiche in tempo reale** durante la configurazione dei componenti
- **Interazioni test** in modalità Anteprima

### **2. Pannello Proprietà - Configurazione Dei Componenti**

Nel **pannello Proprietà** (lato destro) è possibile personalizzare i componenti selezionati e gestire la struttura del modulo.

![Pannello Proprietà](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png)

**Caratteristiche essenziali:**

- **Modalità proprietà** (`d` collegamento) - Configura le impostazioni del componente selezionato
- **Struttura contenuto** (`f` collegamento) - Naviga nella struttura del modulo
- **Aggiungi componenti** (collegamento `a`) - Inserisci nuovi campi modulo
- **Azioni componente** - Duplica o elimina gli elementi selezionati

### **3. Nozioni di base sulla barra degli strumenti - Anteprima e pubblicazione**

La **Barra degli strumenti dell&#39;editor universale** fornisce azioni chiave per testare e pubblicare i moduli.

![Barra degli strumenti dell’editor universale](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

**Strumenti da conoscere:**

- **Modalità anteprima** (`p` collegamento) - Verifica il modulo così come verrà visualizzato dagli utenti
- **Modalità reattiva** - Controlla l&#39;aspetto del modulo sui dispositivi mobili
- **Apri pagina** (collegamento `o`) - Visualizza modulo in una nuova scheda
- **Pubblica** - Rendi il modulo attivo per gli utenti

### **4. Flusso di lavoro di avvio rapido**

**Per il primo modulo:**

1. **Inizia la compilazione** - Aggiungi componenti utilizzando il pulsante **Aggiungi** (`a`)
2. **Configura campi** - Seleziona i componenti e utilizza **Modalità proprietà** (`d`)
3. **Verifica il modulo** - Utilizza la **modalità anteprima** (`p`) per interagire con il modulo
4. **Controlla la visualizzazione per dispositivi mobili** - Passa alla **modalità reattiva** per i test mobili
5. **Pubblica** - Fai clic su **Pubblica** quando è pronto

**Checkpoint di convalida:**

- È possibile aggiungere e configurare campi modulo?
- La modalità Anteprima funziona correttamente?
- Tutti i campi obbligatori sono impostati correttamente?
- Il modulo viene visualizzato correttamente sui dispositivi mobili?

## Intestazione di Experience Cloud

L&#39;**Intestazione Experience Cloud** fornisce gli strumenti di navigazione e gestione account. La maggior parte dei creatori di moduli lo utilizza occasionalmente per passare da uno strumento Adobe all’altro o per accedere all’Aiuto.

![Intestazione Experience Cloud](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager-header.png)

**Elementi chiave:**

| **Elemento** | **Scopo** | **Quando utilizzare** |
|-------------|-------------|----------------|
| **Adobe Experience Cloud** | Passare ad altri strumenti di Adobe | Passaggio tra Sites, Assets, Forms |
| **Organizzazione** | Passare da un’organizzazione all’altra | Scenari di accesso per più organizzazioni |
| **Guida** | Accedere alla documentazione e al supporto tecnico | Quando hai bisogno di assistenza o desideri inviare un feedback |
| **Notifiche** | Visualizza le attività e gli avvisi assegnati | Verifica dello stato del flusso di lavoro |
| **Soluzioni** | Accesso rapido ad altre soluzioni Adobe | Passare da un prodotto Adobe a un altro |
| **Profilo utente** | Impostazioni account e disconnessione | Gestione dell’account o cambio di utente |

**Usi più comuni:**

- **Visualizzazione della Guida** - Fare clic sull&#39;icona della Guida per accedere alla documentazione e al supporto tecnico
- **Cambio di organizzazioni** - Utilizza il menu a discesa Organizzazione se disponi di accesso per più organizzazioni

## Barra degli strumenti dell’editor universale

La **Barra degli strumenti dell&#39;editor universale** contiene gli strumenti principali di modifica e pubblicazione dei moduli. Queste sono organizzate in base alla frequenza di utilizzo e al flusso di lavoro tipico.

![Barra degli strumenti dell’editor universale](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

### **Strumenti flusso di lavoro giornalieri**

**Questi strumenti vengono utilizzati nella maggior parte delle sessioni di creazione moduli:**

#### **Modalità anteprima** (`p` collegamento)

**Scopo:** verifica il modulo esattamente come verrà visualizzato dagli utenti\
**Quando utilizzare:** Prima della pubblicazione, dopo aver apportato modifiche, per testare la funzionalità del modulo

![Modalità Anteprima](/help/edge/docs/forms/universal-editor/assets/ue-preview.png)

**Best practice:** visualizza l&#39;anteprima dopo ogni modifica importante per rilevare i problemi in anticipo.

#### **Modalità reattiva**

**Scopo:** verifica la visualizzazione del modulo sui dispositivi mobili\
**Quando utilizzare:** Dopo aver generato il modulo, prima della pubblicazione

![Modalità reattiva](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png)

**Best practice:** verifica sempre la visualizzazione per dispositivi mobili. Molti utenti accederanno ai moduli sul telefono.

#### **Apri pagina** (`o` collegamento)

**Scopo:** Visualizza il modulo in una nuova scheda senza l&#39;interfaccia dell&#39;editor\
**Quando utilizzare:** Per test a schermo intero, condivisione con le parti interessate per la revisione

![Apri pagina](/help/edge/docs/forms/universal-editor/assets/ue-openpage.png)

#### **Pubblica**

**Scopo:** Rendere il modulo attivo e accessibile agli utenti\
**Quando utilizzare:** Dopo un test approfondito in modalità Anteprima e Reattiva

![Pubblica](/help/edge/docs/forms/universal-editor/assets/ue-publish.png)

**Elenco di controllo convalida prima della pubblicazione:**

- Modulo testato in modalità Anteprima
- Velocità di risposta mobile verificata
- Tutti i campi obbligatori configurati
- Azioni di invio che funzionano correttamente

### **Strumenti di navigazione**

#### **Pulsante Home**

**Scopo:** Tornare alla pagina iniziale dell&#39;editor universale\
**Quando utilizzare:** Avvio del lavoro in un modulo diverso

![Pulsante Home](/help/edge/docs/forms/universal-editor/assets/ue-home.png)

#### **Barra località** (`l` collegamento)

**Scopo:** Passare direttamente a qualsiasi modulo tramite URL\
**Quando utilizzare:** Passaggio rapido tra moduli specifici

![Barra della posizione](/help/edge/docs/forms/universal-editor/assets/ue-locationbar.png)

### **Strumenti di configurazione avanzati**

**Questi strumenti vengono utilizzati per scenari specifici o impostazioni avanzate:**

#### **Proprietà modulo AEM**

**Scopo:** configurare le impostazioni a livello di modulo come Modello dati modulo (FDM) e le date di pubblicazione\
**Quando utilizzare:** Configurazione delle integrazioni di dati, pianificazione della pubblicazione

![Proprietà modulo](/help/edge/docs/forms/universal-editor/assets/ue-formproperties.png)

![Creazione guidata proprietà modulo](/help/edge/docs/forms/universal-editor/assets/form-properties-ue.png)

Il pannello Proprietà modulo include le sezioni seguenti:

- **Invio**: definisci cosa accade dopo che un utente invia il modulo. È possibile scegliere tra più azioni di invio, ad esempio l’invio di dati tramite e-mail, l’invio a SharePoint, l’utilizzo di un modello dati modulo o l’integrazione con servizi come Adobe Experience Platform o Microsoft Power Automate. Per un elenco completo delle azioni di invio supportate, fare riferimento all&#39;articolo [Azione di invio](/help/edge/docs/forms/universal-editor/submit-action.md).

- **Precompilazione**: configura il popolamento automatico dei campi modulo prima che l&#39;utente interagisca con il modulo. Puoi connetterti a origini dati, ad esempio un Modello dati modulo (FDM), oppure utilizzare parametri URL per precompilare i campi, migliorando l’esperienza utente e riducendo l’input manuale. Per ulteriori informazioni, consulta l&#39;articolo [Servizio di precompilazione](/help/edge/docs/forms/universal-editor/prefill-form.md).

- **Grazie**: personalizza i contenuti visualizzati dagli utenti dopo l&#39;invio del modulo. Puoi visualizzare un messaggio di conferma o reindirizzarli a un’altra pagina web, garantendo un’esperienza di completamento fluida e professionale. Per informazioni su come configurare un messaggio di ringraziamento per i moduli, vedere l&#39;articolo [Configura messaggio di ringraziamento](/help/edge/docs/forms/universal-editor/configure-thankyou-message.md).

#### **Editor regole** (accesso anticipato)

**Scopo:** Aggiungere comportamenti dinamici, convalide e logica condizionale\
**Quando utilizzare:** Creazione di moduli interattivi con logica di business complessa

![Editor di regole](/help/edge/docs/forms/universal-editor/assets/ue-ruleeditor.png)

>[!IMPORTANT]
>
> **Funzione di accesso anticipato:** L&#39;editor di regole richiede un accesso speciale. Contattare [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) per abilitare questa funzionalità.
>
> **Ulteriori informazioni:** Per istruzioni dettagliate, consulta la [Guida dell&#39;editor di regole](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md).

#### **Impostazioni intestazione di autenticazione**

**Scopo:** impostare intestazioni di autenticazione personalizzate per i test di sviluppo\
**Quando utilizzare:** Sviluppo locale con moduli richiesti per l&#39;autenticazione

![Intestazioni di autenticazione](/help/edge/docs/forms/universal-editor/assets/ue-authenticationheader.png)

#### **Opzioni aggiuntive** (Menu con puntini di sospensione)

**Finalità:** Accedi ad azioni meno comuni, ad esempio l&#39;annullamento della pubblicazione\
**Quando utilizzare:** Disconnessione dei moduli, accesso alle opzioni avanzate

![Opzioni aggiuntive](/help/edge/docs/forms/universal-editor/assets/ue-ellipsis.png)

## Pannello Proprietà

Il **pannello Proprietà** (lato destro) è il centro di controllo per la creazione e la configurazione dei moduli. Cambia in base a ciò che selezioni e fornisce strumenti diversi per le diverse attività.

![Pannello Proprietà](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png)

### **Strumenti core per la generazione di moduli**

**Questi strumenti sono essenziali per la creazione e l&#39;organizzazione dei moduli:**

#### **Aggiungi componenti** (`a` collegamento)

**Scopo:** inserire nuovi campi ed elementi del modulo\
**Funzionamento:** mostra i componenti disponibili per il contenitore selezionato

![Aggiungi componenti](/help/edge/docs/forms/universal-editor/assets/ue-add.png)

**Componenti comuni:**

- Input di testo, e-mail, campi telefono
- Menu a discesa, pulsanti di scelta, caselle di controllo
- Caricamento di file, selezione data
- Pannelli e sezioni per l’organizzazione

#### **Modalità proprietà** (`d` collegamento)

**Scopo:** configurare le impostazioni per i componenti selezionati\
**Quando utilizzare:** Dopo aver aggiunto un componente per personalizzarne il comportamento

![Modalità proprietà](/help/edge/docs/forms/universal-editor/assets/ue-properties.png)

**Impostazioni chiave:**

- Etichette di campo e testo segnaposto
- Regole di convalida (obbligatorio, formato, lunghezza)
- Valori predefiniti e testo della guida
- Regole di visibilità condizionale

#### **Struttura contenuto** (`f` collegamento)

**Scopo:** Navigare e organizzare la struttura del modulo\
**Quando utilizzare:** moduli complessi con più sezioni, ricerca di componenti specifici

![Struttura contenuto](/help/edge/docs/forms/universal-editor/assets/ue-contenttree.png)

**Vantaggi:**

- Navigazione rapida a qualsiasi componente
- Gerarchia dei moduli visivi
- Riordinamento semplice degli elementi

#### **Azioni componente**

**Scopo:** gestire i componenti esistenti\
**Azioni disponibili:**

- **Duplica** - Copia rapidamente i componenti ![Duplica](/help/edge/docs/forms/universal-editor/assets/ue-duplicate.png)
- **Elimina** - Rimuovi componenti (nessuna richiesta di conferma) ![Elimina](/help/edge/docs/forms/universal-editor/assets/ue-delete.png)

### **Funzioni e integrazioni avanzate**

**Questi strumenti abilitano funzionalità avanzate per moduli:**

+++Integrazione dei dati

#### **Origine dati**

**Scopo:** connettere i moduli ai sistemi di dati back-end\
**Quando utilizzare:** Forms che devono leggere/scrivere su database o servizi esterni

![Origine dati](/help/edge/docs/forms/universal-editor/assets/ue-datasource.png)

**Funzionalità:**

- Configurazione modello dati modulo (FDM)
- Popolazione dati dinamici
- Invio a sistemi esterni

+++

+++Strumenti basati sull’intelligenza artificiale

#### **Generare varianti**

**Scopo:** utilizzare l&#39;intelligenza artificiale per creare diverse versioni del contenuto del modulo\
**Quando utilizzare:** Sperimentazione con testo, layout o approcci diversi

    .[Genera varianti](/help/edge/docs/forms/universal-editor/assets/ue-variations.png)

**Ulteriori informazioni:** [Genera guida varianti](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/generative-ai/generate-variations)

#### **Bozze di contenuto**

**Scopo:** Creare e salvare le versioni preliminari del testo\
**Quando utilizzare:** Iterazione nella copia del modulo, salvataggio di opzioni di testo alternative

![Bozze di contenuto](/help/edge/docs/forms/universal-editor/assets/ue-contentdraft.png)

+++

+++Test e ottimizzazione

#### **Test A/B**

**Scopo:** Confronta le varianti di modulo per ottimizzare le prestazioni\
**Quando utilizzare:** Ottimizzazione dei tassi di conversione, test di diverse progettazioni

![Test A/B](/help/edge/docs/forms/universal-editor/assets/ue-abtesting.png)

#### **Sperimentazione**

**Scopo:** eseguire test controllati sulle progettazioni dei moduli\
**Quando utilizzare:** Ottimizzazione dei moduli basati su dati, test dell&#39;esperienza utente

    .[Sperimentazione](/help/edge/docs/forms/universal-editor/assets/ue-experimentation.png)

+++

+++Strumenti Collaboration

#### **Gestione attività**

**Scopo:** organizzare il flusso di lavoro del team per i progetti modulo\
**Quando utilizzare:** Sviluppo di moduli per più persone, tracciamento dei progetti

![Gestione attività](/help/edge/docs/forms/universal-editor/assets/ue-taskmanagement.png)

#### **Personalizzazione**

**Scopo:** Connettiti con Adobe Experience Platform per esperienze personalizzate\
**Quando utilizzare:** Creazione di moduli personalizzati basati su dati utente

    .[Personalization](/help/edge/docs/forms/universal-editor/assets/ue-personalizaton.png)

+++

## Editor Canvas

L&#39;**Area di lavoro editor** è l&#39;area di lavoro principale in cui si creano visivamente i moduli. Visualizza esattamente l&#39;aspetto del modulo per gli utenti e fornisce feedback in tempo reale durante l&#39;esecuzione delle modifiche.

![Area di lavoro editor](/help/edge/docs/forms/universal-editor/assets/ue-editor.png)

**Caratteristiche principali:**

- **Modifica WYSIWYG** - Visualizza le modifiche immediatamente dopo averle apportate
- **Interazione diretta** - Fai clic su un componente per selezionarlo e modificarlo
- **Anteprima in tempo reale** - Passa alla modalità Anteprima per testare la funzionalità
- **Visualizzazione reattiva** - Attiva/disattiva le visualizzazioni del dispositivo per verificare la compatibilità mobile

**Best practice:**

- **Inizia con la struttura** - Aggiungi sezioni principali prima dei componenti dettagliati
- **Test frequente** - Utilizza regolarmente la modalità Anteprima per rilevare i problemi in anticipo
- **Pensa a mobile-first** - Controlla la modalità reattiva durante il processo di progettazione

## Scelte rapide da tastiera

Utilizza queste scelte rapide per creare moduli in modo più rapido ed efficiente:

| **Collegamento** | **Azione** | **Quando utilizzare** |
|--------------|------------|----------------|
| `a` | Apri elenco componenti | Aggiunta di nuovi campi modulo |
| `d` | Apri proprietà componente | Configurazione degli elementi selezionati |
| `f` | Attiva/disattiva struttura contenuto | Esplorazione di moduli complessi |
| `p` | Attiva/disattiva modalità anteprima | Verifica della funzionalità del modulo |
| `o` | Apri modulo in una nuova scheda | Test a schermo intero |
| `l` | Barra di posizione dello stato attivo | Passaggio a diversi moduli |

**Suggerimento pro:** Utilizza queste scelte rapide in combinazione. Ad esempio, seleziona un componente, premi `d` per configurarlo, quindi `p` per verificare le modifiche.

## Flussi di lavoro comuni

### **Creazione del primo modulo**

1. **Aggiungi struttura** - Utilizza `a` per aggiungere un pannello per le sezioni del modulo
2. **Aggiungi campi** - Inserisci input testo, e-mail e altri componenti
3. **Configura proprietà** - Seleziona ogni campo e premi `d` per impostare le etichette e la convalida
4. **Funzionalità di test** - Premere `p` per visualizzare l&#39;anteprima e verificare il modulo
5. **Controlla visualizzazione mobile** - Utilizza la modalità reattiva per verificare la visualizzazione mobile
6. **Pubblica** - Fai clic su Pubblica per andare &quot;live&quot;

### **Modifica di Forms esistenti**

1. **Naviga nella struttura** - Utilizza la struttura contenuto (`f`) per trovare rapidamente i componenti
2. **Seleziona e modifica** - Fai clic direttamente sui componenti o utilizza la struttura contenuto
3. **Modifiche test** - Anteprima (`p`) dopo ogni modifica significativa
4. **Convalida flusso di lavoro** - Verifica il flusso di modulo completo prima della ripubblicazione

### **Collaborazione con i team**

1. **Gestione attività** - Assegna sezioni di modulo specifiche ai membri del team
2. **Condividi per revisione** - Utilizza Apri pagina (`o`) per condividere anteprime pulite
3. **Test congiunto** - Utilizza la modalità Anteprima per le sessioni di test collaborativo
4. **Tracciamento avanzamento** - Controlla notifiche per aggiornamenti attività

## Risoluzione dei problemi comuni

### **Problemi di interfaccia**

+++Impossibile caricare gli elementi dell&#39;interfaccia

**Problema:** i pulsanti della barra degli strumenti, il pannello delle proprietà o altri elementi dell&#39;interfaccia non vengono visualizzati

**Soluzioni:**

- **Aggiorna la pagina** - Un semplice aggiornamento del browser spesso risolve i problemi di caricamento
- **Verifica compatibilità browser** - Utilizza Chrome, Firefox o Safari
- **Cancella cache del browser** - Rimuovi i file memorizzati nella cache che potrebbero non essere aggiornati
- **Verifica autorizzazioni** - Assicurati di disporre dell&#39;accesso corretto per la modifica dei moduli

+++

+++I Componenti Non Rispondono

**Problema:** impossibile selezionare i componenti o il pannello Proprietà non viene aggiornato

**Soluzioni:**

- **Fai clic direttamente sui componenti** - Evita di fare clic su aree vuote
- **Utilizza struttura contenuto** - Premi `f` e seleziona i componenti dalla struttura
- **Verifica la presenza di elementi sovrapposti** - Alcuni componenti potrebbero bloccarne altri
- **Ricarica il modulo**. Utilizzare la barra della posizione (`l`) per ricaricare il modulo corrente

+++

+++Problemi relativi alla modalità Anteprima

**Problema:** la modalità Anteprima non funziona correttamente o mostra errori

**Soluzioni:**

- **Verifica convalida modulo** - Verifica che tutti i campi obbligatori siano configurati correttamente
- **Verifica prima in modalità di modifica** - Verifica del funzionamento dei componenti prima dell&#39;anteprima
- **Cancella cache del browser** - Gli script memorizzati nella cache potrebbero interferire con l&#39;anteprima
- **Verifica la configurazione del componente** - Controlla le impostazioni della modalità delle proprietà per individuare eventuali errori

+++

## Procedure consigliate per la creazione efficiente di moduli

### **Suggerimenti organizzazione**

- **Usa nomi descrittivi** - Etichetta chiaramente i componenti in modalità Proprietà
- **Campi correlati al gruppo** - Utilizza i pannelli per organizzare in modo logico le sezioni del modulo
- **Pianifica prima della compilazione** - Crea uno schizzo della struttura del modulo prima dell&#39;inizio
- **Semplifica** - Evita di sopraffare gli utenti con troppi campi

### **Esperienza utente**

- **Test frequente** - Utilizza la modalità Anteprima dopo ogni modifica importante
- **Pensa come utenti** - Considera l&#39;esperienza completa di compilazione dei moduli
- **Fornisci etichette chiare** - Rendi evidenti gli scopi del campo agli utenti
- **Aggiungi testo utile** - Utilizza testo della Guida per campi complessi

### **Ottimizzazione delle prestazioni**

- **Riduci a icona i componenti** - Utilizza solo i campi modulo necessari
- **Ottimizza immagini** - Comprimi tutte le immagini utilizzate nei moduli
- **Test su dispositivi mobili** - Garantire buone prestazioni su connessioni mobili più lente
- **Convalida anticipata** - Imposta la convalida corretta per evitare errori di invio

## Passaggi successivi

Ora che conosci l’interfaccia di Universal Editor:

1. **Esercitarsi con un modulo semplice** - Iniziare con i campi di base per iniziare
2. **Esplora le funzionalità avanzate** - Prova gli strumenti e le integrazioni basati sull&#39;intelligenza artificiale quando saranno pronti
3. **Scopri come creare i moduli**. Consulta la [Guida introduttiva](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
4. **Editor regole master** - Aggiungi comportamenti dinamici con la [Guida dell&#39;editor regole](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md)

**Ricorda:** L&#39;editor universale è progettato per rendere intuitivo lo sviluppo di moduli. Inizia con le funzionalità essenziali ed esplora gradualmente le funzioni avanzate man mano che le tue esigenze aumentano.
