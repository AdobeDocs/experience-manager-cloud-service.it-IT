---
title: Guida alla richiesta di informazioni per l’agente di modernizzazione esperienza
description: Questa guida fornisce suggerimenti per una richiesta efficace dell’agente di modernizzazione esperienza e descrive le sue funzioni.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: e2a9c55644c0d9542f6a299f0df30a3dfd4a55de
workflow-type: tm+mt
source-wordcount: '2696'
ht-degree: 0%

---


# Guida alla richiesta di informazioni per l’agente di modernizzazione esperienza {#prompting-guide}

L’agente di modernizzazione esperienza seleziona automaticamente l’abilità appropriata in base alle richieste in linguaggio naturale. Questa guida fornisce suggerimenti per una richiesta efficace e descrive le funzioni da svolgere.

## Suggerimenti generali {#general-tips}

### Alcune abilità dipendono dai risultati ottenuti da altre competenze. {#dependency}

* Poiché l’importazione in blocco richiede l’infrastruttura di importazione creata dalla migrazione delle pagine, esegui la migrazione di almeno una pagina prima di eseguire l’importazione in blocco.
* Poiché il CSS del blocco fa riferimento ai token di progettazione globali, completa la progettazione a livello di sito prima di formattare i singoli blocchi.

### L’intelligenza artificiale segue flussi di lavoro strutturati e porrà domande chiarificatrici quando avrà bisogno di ulteriori informazioni. {#workflows}

* Fidati del processo e rispondi a queste domande qualificanti man mano che vengono sollevate.
* Non cercare di caricare in primo piano tutti i requisiti nel prompt iniziale.

### Crea file markdown nel progetto per documentare regole, linee guida, decisioni di progettazione o vincoli specifici del progetto. {#markdown-files}

* Questi file markdown (ad esempio, ISTRUZIONI.md, CONTESTO.md) possono includere convenzioni di denominazione dei file, regole di mappatura dei contenuti o linee guida per il brand.
* Quando inizi una nuova conversazione, chiedi all&#39;agente di &quot;riscaldarsi leggendo la documentazione del progetto&quot; in modo da caricare il contesto prima di procedere con le attività.

### La finestra di contesto dell&#39;agente non è infinita. {#limited-window}

* Nel corso di lunghe conversazioni, le istruzioni precedenti possono essere compattate o dimenticate.
* Se l’agente sembra aver perso contesto, ricordagli i punti chiave oppure cancella la chat e ricomincia da capo con un prompt di riscaldamento per leggere la documentazione del progetto.

### Utilizza il prompt iterativo per perfezionare i risultati. {#iterate}

* Se qualcosa non sembra giusto (ad es., colore di sfondo errato su un blocco), chiedi all&#39;agente di risolvere il problema specifico invece di ricominciare da capo.

## Abilità per la creazione di siti e la migrazione {#site-migration}

L’agente di modernizzazione sito offre molte competenze per la creazione di nuovi siti Edge Delivery Services e la migrazione di siti web esistenti. Qualsiasi nuovo sito o progetto di migrazione di Edge Delivery Sites deve sfruttare queste competenze.

### Migrare un sito o una pagina ad AEM {#migrate-a-site}

Utilizza questo prompt per eseguire la migrazione del contenuto da un sito Web esistente a Edge Delivery Services.

#### Esempio di prompt {#example-migrate}

* &quot;Esegui migrazione pagina: `https://example.com/about`
* &quot;Eseguire la migrazione di queste pagine: URL1, URL2, URL3&quot;

#### Cosa sapere {#wtk-migrate}

* La migrazione segue un flusso di lavoro in sette passaggi:
   1. L&#39;agente esegue il scraping della pagina di origine.
   1. Identifica la struttura della sezione.
   1. Esegue analisi di authoring.
   1. Il contenuto viene mappato per bloccare le varianti.
   1. Genera markdown.
   1. Crea infrastrutture di importazione.
   1. Visualizza l’anteprima del risultato.
* L’agente analizza le pagine utilizzando una gerarchia a due livelli:
   * Per prima cosa identifica i limiti della sezione (modifiche di sfondo, spostamenti di spaziatura)
   * Quindi identifica le sequenze di contenuto all’interno di ogni sezione.
* L&#39;analisi di authoring segue il modello di [David.](https://www.aem.live/docs/davidsmodel)
   * per ogni sequenza di contenuto, controlla innanzitutto &quot;Può un autore crearlo digitando normalmente?&quot;
   * Il contenuto predefinito (intestazioni, paragrafi, elenchi e immagini in linea) è da preferire rispetto ai blocchi.
* L’agente tenta di riutilizzare i blocchi esistenti dalla libreria di blocchi dell’archivio prima di crearne di nuovi.
   * Quando il contenuto non può essere mappato su un blocco esistente, crea nuove varianti di blocco.
   * Puoi richiedere modifiche, richiedere nuove varianti o regolare le mappature in modo interattivo.
* Le varianti di blocco vengono tracciate con i metadati.
   * Durante la migrazione di più pagine, l’agente carica prima le varianti personalizzate esistenti e le riutilizza quando lo stile corrisponde a (soglia di somiglianza del 70% in base a scopo, colori, composizione tipografica, spaziatura, layout).
* Intestazione, navigazione e piè di pagina sono esclusi dalla migrazione delle pagine. Questi sono gestiti da abilità dedicate.
* Ogni migrazione crea un’infrastruttura di importazione (modelli di pagina, parser di blocchi, trasformatori) per le future importazioni in blocco.

### Importazione in blocco {#bulk-import}

Utilizzare questo prompt per importare molte pagine dello stesso modello dopo il completamento di una [migrazione iniziale a pagina singola.](#migrate-a-site)

#### Esempio di prompt {#example-prompts-bulk-import}

* &quot;Esegui l’importazione in blocco su queste pagine: URL1, URL2, URL3.&quot;
* &quot;Esegui l’importazione in blocco su tutte le pagine dei prodotti.&quot;
* &quot;Importa in blocco queste pagine di blog: URL1, URL2.&quot;

#### Cosa sapere {#wtk-bulk-import}

* L’importazione in blocco dipende dall’infrastruttura di importazione creata durante una precedente migrazione di una singola pagina.
   * Ciò include modelli di pagina (struttura di sezione), trasformatori (pulizia DOM a livello di sito) e parser (conversione da HTML a tabella specifica per blocco).
* È necessario eseguire la migrazione di almeno una pagina rappresentativa per modello prima di eseguire l’importazione in blocco.
* L’importazione in blocco riutilizza la struttura e le mappature stabilite durante la migrazione di una singola pagina.
   * Non deduce modelli da zero.
* I trasformatori operano sull&#39;intero DOM prima e dopo l&#39;analisi. I parser operano a livello di singolo blocco.
* Tutti i parser vengono convalidati prima di procedere con l&#39;importazione in blocco.
* Un modello corrisponde a una configurazione di importazione in blocco.
   * La combinazione di modelli in una singola esecuzione non è supportata.

#### Flusso di lavoro tipico {#typical-workflow}

Il flusso di lavoro consigliato è iterativo: effettua prima la convalida su un set ridotto, quindi aumenta.

1. **Eseguire prima una migrazione a pagina singola.** - Eseguire la migrazione di una pagina rappresentativa per il modello da importare in blocco.
   * In questo modo viene creata l’infrastruttura di importazione richiesta.
1. **Eseguire l&#39;importazione in blocco su un piccolo gruppo di pagine.** - Chiedi all&#39;agente di eseguire l&#39;importazione in blocco e fornisci un breve elenco di URL che seguono lo stesso modello.
1. **Rivedere e perfezionare i risultati.** - Controlla le pagine importate.
   * Se qualcosa sembra sbagliato, chiedi all&#39;agente di regolare i parser, i trasformatori o la logica di importazione.
1. **Aumenta dimensioni.** - Quando i risultati sono corretti, fornire l&#39;elenco completo degli URL.
   * L&#39;agente riutilizzerà la stessa logica di importazione ed eseguirà l&#39;importazione in blocco su scala.

### Rottamazione di pagine Web {#scraping-webpages}

Utilizza questo prompt per estrarre contenuti, metadati e immagini da un URL di origine per l’analisi o la migrazione.

#### Esempio di prompt {#example-scraping}

* &quot;Eliminare la pagina per l&#39;analisi: `https://example.com`&quot;
* &quot;Estrai contenuto da `https://example.com/product`&quot;

#### Cosa sapere {#wtk-scraping}

* Questo prompt viene in genere richiamato automaticamente come primo passaggio della migrazione delle pagine.
* I contenuti nascosti tramite CSS vengono acquisiti anche se presenti nel DOM.
* Le immagini caricate con lazy e il contenuto renderizzato lato client vengono gestiti scorrendo la pagina in Chromium headless e lasciando eseguire gli script.
* Le immagini WebP/AVIF/SVG vengono convertite in PNG per compatibilità.
* Vengono estratti i metadati, inclusi titolo, descrizione, tag Open Graph, dati strutturati JSON-LD, URL canonico.
* Le immagini nel DOM sono fisse.
   * background-image viene convertito in img.
   * Disattivazione degli elementi immagine
   * srcset è risolto in src
   * Gli URL relativi vengono convertiti in assoluti
   * I file SVG in linea vengono convertiti in file di immagine.
* Vengono generati percorsi di documenti personalizzati (lettere minuscole senza estensione `.html`).
* Vengono prodotti i seguenti output:
   * `screenshot.png`
   * `cleaned.html` (nessuno script/stili)
   * `metadata.json`
   * Cartella `images/` con copie locali
* Gli utenti possono chiedere informazioni sulle dimensioni della schermata e richiedere dimensioni specifiche del dispositivo (mobile, desktop) per l’estrazione dei contenuti.
* L’estrazione del contenuto in più punti di interruzione aumenta il tempo di elaborazione.

### Migrazione progettazione {#design-migration}

Utilizzare questo prompt per estrarre e applicare la progettazione visiva da un sito di origine a Edge Delivery Services.

#### Esempio di prompt {#example-design}

* &quot;Migra la progettazione da `https://example.com`&quot;
* &quot;Estrai token di progettazione&quot;
* &quot;Personalizzare lo stile del blocco hero&quot;

#### Cosa sapere {#wtk-design}

* La migrazione della progettazione prevede due fasi:
   1. La fase 1 (a livello di sito) estrae quanto segue in `styles/styles.css`:
      * Tavolozza dei colori globale e colori degli accenti
      * Sistema tipografico (caratteri, dimensioni, pesi)
      * Sistema di spaziatura (spaziatura, margini, spazi)
      * Sfondi sezione (chiaro, scuro, colorato)
      * Stili dei componenti di base (pulsanti, collegamenti, immagini)
      * Invia a
   1. La fase 2 esegue la migrazione dei singoli stili di blocco e crea CSS specifici per il blocco in `/blocks/{name}/{name}.css`.
* Lo stile del blocco (fase 2) richiede che il progetto a livello di sito (fase 1) sia completo per primo.
   * Il sistema di progettazione globale fornisce proprietà personalizzate CSS che bloccano il riferimento.
* Tempo stimato:
   * Fase 1: 5-10 minuti
   * Fase 2: 10-15 minuti
* Per impostazione predefinita, le richieste ambigue completano la migrazione (entrambe le fasi).

### Critica di blocco {#block-critique}

Utilizza questo prompt per convalidare e perfezionare i singoli blocchi migrati e garantire l’accuratezza visiva rispetto al sito web originale.

#### Esempio di prompt {#example-block-critique}

* &quot;Blocco eroe critico&quot;
* &quot;Convalida schede personalizzate del blocco&quot;

#### Cosa sapere {#wtk-block-critique}

* La critica di blocco confronta un blocco migrato con la sua origine originale e applica iterativamente le correzioni CSS fino a raggiungere una somiglianza visiva dell’85% o a completare tre iterazioni.
* L’abilità richiede che il blocco sia stato creato prima dalla migrazione delle pagine.
* Una critica di blocco segue un flusso di lavoro in sei passaggi:
   1. Acquisisce il blocco originale dalla pagina sorgente utilizzando un selettore XPath.
   1. Inizializza la sessione di critica.
   1. Controlla il blocco originale (schermate, stili, HTML).
   1. Controlla il blocco migrato.
   1. Confronta gli elementi e genera un punteggio di somiglianza con le correzioni CSS.
   1. Applica correzioni e riesamina fino al raggiungimento dell’obiettivo dell’85%.
* Ogni iterazione visualizza un rapporto critico completo con tutte le differenze, applica tutte le correzioni CSS (con priorità in base all’impatto visivo), verifica in anteprima, riesamina e mostra le metriche di miglioramento.
* Utilizza la critica di blocco dopo il completamento di [migrazione progettazione](#design-migration).

### Critica pagina {#page-critique}

Utilizzare questo prompt per convalidare intere pagine migrate per la fedeltà visiva a pagina intera rispetto al sito Web originale.

#### Esempio di prompt {#example-page-critique}

* &quot;Critica la pagina Informazioni su&quot;
* &quot;Convalida la pagina migrata rispetto a `https://example.com/about`&quot;

#### Cosa sapere {#wtk-page-critique}

* Il criterio di pagina esegue un confronto visivo a pagina intera tra la pagina originale e quella migrata, ripetendo l’iterazione fino a raggiungere un target di somiglianza dell’85% o fino a tre iterazioni completate.
* Una critica di pagina prevede un flusso di lavoro in cinque passaggi:
   1. Inizializza una sessione critica.
   1. Esamina tutti gli elementi della pagina originale.
   1. Esamina tutti gli elementi della pagina migrata.
   1. Confronta e genera un punteggio di somiglianza con le correzioni CSS con priorità.
   1. Applica correzioni e riesamina fino al raggiungimento dell’obiettivo dell’85%.
* Un criterio di pagina richiede come input l’URL della pagina sorgente e il percorso migrato (ad esempio,&quot;/about&quot;).
* Utilizza il criterio di pagina per convalidare la fedeltà complessiva della pagina o più blocchi simultaneamente.
* [Utilizza la critica del blocco](#block-critique) per una convalida incentrata su componenti specifici.
* Si consiglia il seguente flusso di lavoro:
   1. Migrare una pagina.
   1. Applicare una progettazione.
   1. Eseguire una critica di blocco sui blocchi chiave
   1. Esegui il criterio di pagina per la convalida completa.

### Migrazione in blocco Figma {#figma-block-migration}

Utilizza questo prompt per migrare un blocco da Figma design a Edge Delivery Services.

Per utilizzare questo prompt, è necessario impostare i dettagli di Figma in [Console di modernizzazione esperienza](/help/ai-in-aem/agents/brand-experience/modernization/console.md).

#### Esempio di prompt {#example-figma}

* &quot;Migrare il blocco `https://figma.com/design/{fileKey}?node-id={nodeId}` a Edge Delivery Services&quot;
* &quot;Migra `{blockName}` da `https://figma.com/file/{fileKey}` a Edge Delivery Services&quot;

#### Cosa sapere {#wtk-figma}

* Questa abilità consente di eseguire la migrazione di un blocco alla volta, non di pagine intere o file Figma completi.
* Per ottenere risultati ottimali:
   * Seleziona il blocco specifico di cui vuoi eseguire la migrazione in Figma e copiane il collegamento (con `node-id`) o il nome.
   * Fornisci il parametro `node-id` nell&#39;URL per eseguire il targeting del blocco esatto.
* Quando esegui questa abilità, i seguenti passaggi vengono eseguiti automaticamente nell’ambiente in hosting:
   1. **Individuazione struttura di blocco**: l&#39;agente legge il nodo Figma per comprendere livelli e componenti.
   1. **Estrazione stile globale**: l&#39;agente richiama colori, composizione tipografica e spaziatura in `styles/styles.css` come proprietà personalizzate CSS (token di progettazione).
   1. **Creazione di stili specifici del blocco**. L&#39;agente crea proprietà personalizzate CSS aggiuntive specifiche per il blocco di cui si esegue la migrazione.
   1. **Mappatura a blocchi esistenti**: l&#39;agente identifica il blocco corrispondente più vicino nella libreria di blocchi del progetto e crea una variante personalizzata.
   1. **Generazione CSS**: l&#39;agente scrive stili che fanno riferimento alle proprietà personalizzate CSS estratte, garantendo la coerenza della progettazione.
   1. **Download risorse**: l&#39;agente salva immagini e icone da Figma nell&#39;area di lavoro dell&#39;ambiente ospitato.
   1. **Generazione di contenuti Edge Delivery Services**: l&#39;agente crea il file markdown seguendo la struttura di blocchi EDS
   1. **Convalida output**: l&#39;agente visualizza in anteprima il risultato ed esegue un confronto visivo con la struttura Figma originale.
* L’abilità legge innanzitutto i metadati (passaggio 1) per comprendere la struttura, quindi estrae il contesto di progettazione dettagliato (passaggi 2-5).
   * Questo approccio graduale evita problemi con file Figma di grandi dimensioni o complessi.
* Questa abilità adotta un approccio basato sugli stili.
   * Tutti gli stili vengono estratti come proprietà personalizzate CSS (token di progettazione) prima della scrittura di qualsiasi CSS.
   * In questo modo il blocco migrato rimane coerente con il sistema di progettazione.
* Il prompt richiede l&#39;URL Figma (con `fileKey` e l&#39;opzione `node-id`) o una chiave di file Figma direttamente come input.

### Impostazione navigazione {#navigation-setup}

Utilizzare questo prompt per configurare o eseguire la migrazione della navigazione del sito.

#### Esempio di prompt {#example-navigation}

* &quot;Configura navigazione da `https://example.com`&quot;
* &quot;Correggi il menu di navigazione&quot;

#### Cosa sapere {#wtk-navigation}

* La navigazione Edge Delivery Services applica una struttura a tre sezioni (imposta da `header.js`):
   1. **Marchio** (sezione 1): Logo e collegamento di branding principale
   1. **Sezioni** (sezione 2): menu di navigazione principale con menu a discesa facoltativi
   1. **Strumenti** (sezione 3): collegamenti alle utilità (abbonamento, accesso, carrello)
* Il contenuto di navigazione si trova in `nav.md` nella directory principale.
* Le sezioni sono separate da (`---`) marcatori.
* Gli elementi in grassetto (`**Text**`) con elenchi nidificati creano elenchi a discesa.
* I collegamenti nella navigazione possono essere visualizzati come pulsanti a causa del comportamento di wrapping automatico di Document Authoring.
   * Il blocco intestazione include codice per eliminare le classi di pulsanti dai collegamenti di navigazione.

## Blocca funzionalità di sviluppo {#block-development-capabilities}

Questi prompt vengono utilizzati per la creazione e l’evoluzione dei blocchi, fornendo un valore continuo oltre la creazione o la migrazione iniziale del sito.

### Blocca sviluppo {#block-development}

Utilizzare questo prompt per creare nuovi blocchi o modificare quelli esistenti.

#### Esempio di prompt {#example-block-development}

* &quot;Crea un blocco delle testimonianze&quot;
* &quot;Aggiungi una variante di sfondo video al blocco hero&quot;

#### Cosa sapere {#wtk-block-development}

* L’agente segue Content-Driven Development (CDD), un processo obbligatorio per tutti gli sviluppi Edge Delivery Services.
   * Si occuperà di modelli di contenuto e di testare il contenuto prima di scrivere il codice.
* La filosofia di CDD è che l’autore deve venire prima delle esigenze dello sviluppatore.
   * I modelli di contenuto devono essere intuitivi per gli autori, anche se ciò significa codice di decorazione più complesso.
* La creazione del contenuto di test fornisce innanzitutto:
   * Funzionalità di test immediato
   * Collegamenti di convalida PR per i controlli PSI
   * Documentazione live per autori
   * Individuazione dei casi edge non raggiunti con l’approccio code-first
* L&#39;agente cercherà blocchi simili nella [raccolta blocchi](https://www.aem.live/developer/block-collection) e nella [parte blocchi](https://www.aem.live/developer/block-party/) prima di implementarli, per trovare modelli e codice riutilizzabile.
* Ignora CDD solo per modifiche banali apportate solo a CSS (ma identifica comunque il contenuto di test per la convalida).

### Modellazione dei contenuti {#content-modeling}

Utilizza questo prompt per progettare la struttura di tabella con cui gli autori lavorano durante la creazione di contenuto di blocchi.

#### Esempio di prompt {#example-modeling}

* &quot;Progettare un modello di contenuto per un blocco di testimonianze&quot;
* &quot;Qual è il modello di contenuto migliore per questo carosello?&quot;

#### Cosa sapere {#wtk-modeling}

* Edge Delivery Services dispone di quattro tipi di modelli canonici:
   * **Autonomo:** elementi visivi/narrativi distinti (hero, blockquote)
      * Tabella singola con contenuto blocco
   * **Raccolta:** contenuto semistrutturato ripetuto (schede, carosello)
      * Tabella con pattern di righe ripetuto
   * **Configurazione:** contenuto dinamico o basato su API in cui vengono visualizzati i controlli di configurazione (elenco blog, risultati ricerca)
      * Tabella con righe di configurazione chiave-valore.
   * **Bloccato automaticamente:** strutture complesse create dagli autori come sezioni/contenuto predefinito e trasformate (schede, incorporamenti YouTube)
* C&#39;è un limite di quattro celle per riga.
   * Raggruppa elementi correlati in celle.
* Preferisci le varianti di blocco alle celle di configurazione per le differenze di stile.
* [Segui la legge di Postel](https://en.wikipedia.org/wiki/Robustness_principle): Sii flessibile sulla struttura di input.
   * Un blocco hero deve funzionare sia che il contenuto si trovi in una cella, diviso in due celle o in righe separate.
* Questa abilità viene in genere richiamata automaticamente dallo sviluppo basato sui contenuti durante la creazione dei blocchi.

### Ricerca di blocchi di riferimento {#reference-blocks}

Utilizza questo prompt per cercare le implementazioni esistenti da utilizzare come punti di partenza.

#### Esempio di prompt {#example-reference}

* &quot;Trova blocchi simili a una tabella dei prezzi&quot;
* &quot;Quali blocchi sono disponibili per le testimonianze?&quot;
* &quot;Cerca parte del blocco per un’implementazione di schede&quot;

#### Cosa sapere {#wtk-reference}

* La [Raccolta blocchi](https://www.aem.live/developer/block-collection) è gestita da Adobe e valutata per le best practice, la modellazione dei contenuti eccellente, le prestazioni elevate e l&#39;accessibilità.
   * È limitato ai blocchi comunemente necessari. Inizia qui.
* Il [Blocca festa](https://www.aem.live/developer/block-party/) è guidato dalla community e offre una varietà più ampia, inclusi gli approcci sperimentali.
   * Include inoltre plug-in per la barra laterale, strumenti di creazione (webpack, vite, sass) e integrazioni.
   * Da utilizzare quando la raccolta Blocca non dispone di ciò che è necessario.
* Considera nomi alternativi durante la ricerca
   * FAQ = Pannello a soffietto
   * Galleria = carosello/presentazione
   * Navigazione = menu/intestazione
* Il Blocca parte restituisce solo le voci approvate/curate.

### Ricerca nella documentazione {#searching-documentation}

Utilizza questo prompt per trovare informazioni sulle funzioni di Edge Delivery Services o linee guida per l’implementazione.

#### Esempio di prompt {#example-documentation}

* &quot;Come si implementa il caricamento lento in Edge Delivery Services?&quot;
* &quot;Cerca metadati di sezione nei documenti&quot;

#### Cosa sapere {#wtk-documentation}

* Effettua ricerche specifiche nella documentazione di [aem.live](https://aem.live) (documenti e post di blog).
* Utilizza parole chiave specifiche (&quot;decorazione a blocchi&quot;,&quot;plug-in di barra laterale&quot;,&quot;metadati&quot;) invece di termini generici (&quot;aem&quot;,&quot;sito web&quot;,&quot;come creare&quot;).
* Per esempi di codice e implementazioni di riferimento, utilizza invece &quot;trova blocchi di riferimento&quot;.
* Per impostazione predefinita vengono restituiti i primi dieci risultati più rilevanti.

### Test {#testing}

Utilizza questo prompt per convalidare le modifiche al codice prima di aprire una richiesta di pull.

#### Esempio di prompt {#example-testing}

* &quot;Verifica il nuovo blocco di schede&quot;
* &quot;Esegui i test prima di aprire una PR&quot;

#### Cosa sapere {#wtk-testing}

* I test seguono una filosofia di &quot;valore rispetto ai costi&quot; in cui si creano e gestiscono test quando il loro valore supera i costi.
   * **I test Keeper** (unit test) sono per utilità pesanti per la logica, elaborazione dati, integrazioni API. Si tratta di regressioni rapide, facili da mantenere e intercettate nel codice riutilizzato.
   * **I test di eliminazione** (test del browser) sono per trasformazioni DOM e convalida visiva. Utilizza per convalidare l’implementazione, acquisire screenshot per la revisione PR e quindi eliminarlo.
* I test di eliminazione vengono eseguiti in `test/tmp/` e il contenuto dei test in `drafts/tmp/` (entrambi ignorati).
* Prima di aprire una PR, accertati di:
   * Test esistenti superati
   * Gli unit test vengono scritti per la nuova logica
   * Convalida del browser completata
   * Tutte le varianti vengono testate
   * Il comportamento reattivo è verificato
   * Passate di colorazione

### Debugging {#debugging}

Utilizza questo prompt per risolvere i problemi relativi a blocchi, immagini, CSS o anteprima.

#### Esempio di prompt {#example-debugging}

* &quot;Debug del motivo per cui le immagini vengono visualizzate come circa:error&quot;
* &quot;Correggi il blocco hero senza rendering&quot;
* &quot;Perché le modifiche non vengono visualizzate in anteprima?&quot;

#### Cosa sapere {#wtk-debugging}

* I problemi comuni presentano pattern noti:
   * **Immagini che mostrano &quot;about:error&quot;**: chiamata `createOptimizedPicture` generalmente mancante nel blocco JS o chiamata prima della ristrutturazione DOM
   * **Blocchi senza rendering**: controlla il formato del nome del blocco in markdown e verifica che il blocco contenga `.js` e `.css` file in `blocks/`.
   * **Impossibile caricare il file CSS**: controllare i percorsi dei file, verificare che il file CSS esista e controllare la scheda Rete nel browser.
   * **Modifiche non visualizzate**: la sincronizzazione del codice richiede 3-5 secondi. Prova ad aggiornare (Ctrl+Maiusc+R).
* L&#39;agente controlla sistematicamente ogni livello:
   1. File Source
   1. Output di rendering
   1. Codice di blocco
   1. Console del browser
* L&#39;agente è in grado di controllare le anteprime locali alle `http://localhost:3000`.
