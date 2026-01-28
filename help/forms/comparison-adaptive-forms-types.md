---
title: Componenti core Forms adattivi vs Edge Delivery Services Forms vs Componenti Foundation
description: 'Confronto tecnico degli approcci di authoring di AEM Forms: componenti core, Edge Delivery Services Forms e componenti di base. Architettura, rendering, funzioni e casi d’uso.'
keywords: confronto di moduli adattivi, componenti core, componenti di base, moduli per servizi di consegna edge, confronto di AEM forms, confronto di form builder
role: Architect, Developer, Admin
level: Intermediate
feature: Adaptive Forms, Core Components, Edge Delivery Services
exl-id: adaptive-forms-comparison
source-git-commit: 37799555babb15809409ec5cda8a1c46ceff24f2
workflow-type: tm+mt
source-wordcount: '1953'
ht-degree: 8%

---


# Forms adattivo: componenti core vs Edge Delivery Services Forms vs componenti di base

Adobe Experience Manager (AEM) Forms fornisce tre approcci distinti per la creazione di esperienze di acquisizione dati: Forms adattivo basato su componenti core, Edge Delivery Services Forms e Forms adattivo basato su componenti di base. Ogni approccio ha un’architettura, un modello di rendering e un caso di utilizzo di destinazione diversi. Questo articolo fornisce un confronto tecnico per consentire ad architetti, sviluppatori e clienti AEM di selezionare l’approccio appropriato per le proprie esigenze.

## Panoramica

Tutti e tre i tipi di modulo hanno lo scopo di acquisire i dati utente e di integrarli con i sistemi back-end. Tuttavia, differiscono nell’architettura sottostante, dove vengono riprodotti i moduli, come vengono distribuiti e quali funzionalità supportano.

| Approccio | Stato | Caso d’uso principale |
|----------|--------|------------------|
| **Componenti core** | Consigliato per i nuovi moduli | Moduli moderni e scalabili che richiedono l’authoring AEM con opzioni di pubblicazione flessibili |
| **Edge Delivery Services Forms** | Consigliato per siti con prestazioni critiche | Moduli ad alte prestazioni forniti dalla rete Edge con installazione rapida |
| **Componenti di base** | Modalità di manutenzione | Moduli esistenti che richiedono il supporto di funzioni legacy |

## Forms adattivo basato su componenti core

### Definizione

I componenti core Forms adattivi sono un set di 30 componenti open-source conformi a BEM basati sui componenti core WCM di Adobe Experience Manager. Rappresentano l’approccio consigliato da Adobe per la creazione di un nuovo Forms adattivo, che fornisce architettura moderna, prestazioni migliorate e generazione automatica di moduli headless.

### Architettura

I Componenti core utilizzano un’architettura di componenti standardizzata e modulare:

- **Component Foundation**: basato su componenti core WCM AEM
- **Metodologia di stile**: convenzioni CSS BEM (Block Element Modifier)
- **Archiviazione dei contenuti**: archivio JCR con nodi di contenuto strutturato
- **Rendering**: rendering lato server in AEM con rendering headless lato client facoltativo
- **Source**: open-source (disponibile in [GitHub](https://github.com/adobe/aem-core-forms-components))

### Modello di rendering

I Componenti core supportano più modelli di rendering:

1. **Server-Side Rendering (SSR)**: rendering Forms sul server AEM e consegna il HTML completo al browser
2. **Rendering headless**: Forms espone le rappresentazioni JSON tramite API per il rendering lato client in React, Angular o altri framework
3. **Rendering ibrido**: combinazione di rendering server e client per prestazioni ottimali

### Opzioni di pubblicazione

- Istanze di AEM Publish
- Edge Delivery Services (se configurato)
- API headless per applicazioni front-end personalizzate

### Funzioni principali

| Categoria | Funzionalità |
|----------|-------------|
| **Componenti** | 30 componenti standardizzati tra cui Casella di testo, Casella numerica, Selezione data, Elenco a discesa, Gruppo di caselle di controllo, Pulsante di opzione, File allegato, Procedura guidata, Pannello a soffietto, Schede orizzontali/verticali |
| **Modelli modulo** | Schema JSON (v4 e 2020-12), modello dati modulo (FDM), modelli XDP/XFA (limitato) |
| **Motore regole** | Editor di regole visive con logica condizionale, convalida, chiamata di servizio, funzioni personalizzate |
| **Azioni di invio** | Endpoint REST, e-mail, flusso di lavoro AEM, SharePoint, OneDrive, archiviazione BLOB di Azure, Power Automate, Workfront Fusion, modello dati modulo |
| **Precompilazione** | Servizio di preriempimento modello dati modulo, servizi di preriempimento personalizzati |
| **CAPTCHA** | reCAPTCHA, hCaptcha, Turnstile |
| **Documento record** | Generazione di PDF con modelli personalizzati o OOTB |
| **Accessibilità** | Conformità WCAG, etichette ARIA, navigazione da tastiera, supporto per utilità di lettura dello schermo |
| **Localizzazione** | Supporto multilingue tramite flusso di lavoro di traduzione AEM |
| **Controllo delle versioni** | Controllo delle versioni dei contenuti ereditato da AEM Sites |

### Prerequisiti

- **AEM Forms as a Cloud Service**: componenti core abilitati per impostazione predefinita
- **AEM 6.5 Forms**: richiede l&#39;abilitazione tramite Archetipo AEM
- **Autorizzazioni utente**: l&#39;utente deve appartenere al gruppo `forms-users`
- **Modello**: modello modulo adattivo (componente core) richiesto
- **Tema**: tema canvas (OOTB) o tema personalizzato

### Limitazioni

- **Vincoli dello schema JSON**: tipo nullo, tipi di unione (qualsiasi), costrutti OneOf/AnyOf/NOT non supportati
- **Distanze tra i componenti**: blocco Adobe Sign, firma scarabocchio, grafico, scelta immagine non disponibile (disponibile nei componenti di base)
- **Funzioni personalizzate**: funzioni del generatore, async/await, metodi di classe non supportati
- **Firme digitali**: non disponibile in modalità nativa (a differenza dei componenti di base)

### Applicazione consigliata

**Consigliato per:**

- Nuovi progetti di sviluppo moduli
- Organizzazioni che richiedono un&#39;architettura moderna e gestibile
- Progetti che richiedono una pubblicazione flessibile (AEM + Edge Delivery + Headless)
- Applicazioni front-end personalizzate (React, Angular) tramite API headless
- Progetti che danno priorità a prestazioni e accessibilità
- Requisiti di consegna omni-channel (web, dispositivi mobili, chioschi)

**Non consigliato per:**

- Forms che richiede l’integrazione con Adobe Sign (utilizza i componenti di base)
- Moduli semplici in cui le prestazioni di Edge Delivery Services sono fondamentali
- Moduli basati su componenti di base esistenti (mantieni in Foundation a meno che non esegua la migrazione)

## Moduli di Edge Delivery Services

### Definizione

Edge Delivery Services (EDS) Forms è un set di servizi componibili per la creazione e la distribuzione di moduli tramite Adobe Experience Manager Edge Delivery Services. Consentono uno sviluppo rapido dei moduli con prestazioni eccezionali grazie alla distribuzione basata su Edge, al rendering lato client e a più metodi di authoring.

### Architettura

EDS Forms utilizza un&#39;architettura edge-first scollegata:

- **Origini contenuto**: Microsoft SharePoint, Google Drive (basato su documenti) o Universal Editor (WYSIWYG)
- **Archivio codici**: GitHub
- **Consegna contenuti**: Edge Delivery Services CDN
- **Rendering**: rendering lato client con Vanilla JavaScript
- **Blocco modulo**: il blocco Forms adattivo elabora le definizioni dei moduli e genera HTML

### Modello di rendering

EDS Forms utilizza esclusivamente il rendering lato client:

1. Definizione del modulo memorizzata come JSON (convertita da un foglio di calcolo o creata in Universal Editor)
2. JSON recuperato dal perimetro: `https://<branch>--<repo>--<owner>.aem.live/<form>.json`
3. Processi JSON per JavaScript a blocchi di Forms adattivi
4. Struttura HTML generata dinamicamente nel browser
5. CSS applicato per lo stile

**Pattern struttura HTML:**

```html
<div class="{Type}-wrapper field-{Name} field-wrapper" data-required="{Required}">
   <label for="{FieldId}" class="field-label">Label</label>
   <input type="{Type}" id="{FieldId}" name="{Name}">
   <div class="field-description" id="{FieldId}-description">Help text</div>
</div>
```

### Metodi di authoring

EDS Forms supporta due approcci di authoring:

#### Editor universale (WYSIWYG)

- Interfaccia visiva di trascinamento della selezione
- Anteprima in tempo reale con simulazione del dispositivo
- Editor di regole avanzate per la logica condizionale
- Integrazione del modello dati del modulo (FDM)
- Integrazione dei flussi di lavoro AEM
- Supporto di componenti personalizzati
- Creazione basata su modello

#### Authoring basato su documenti

- Creazione di fogli Microsoft Excel o Google
- Definizione di modulo basato su foglio di calcolo
- Pubblicazione immediata (le modifiche vengono applicate immediatamente)
- Adatto per moduli di complessità semplici o moderati

### Opzioni di invio

**Servizio invio Forms:**

- Invia a fogli Google
- Invia a Microsoft Excel (OneDrive/SharePoint)
- Notifiche e-mail

**Azioni di invio pubblicazione AEM:**

- Endpoint REST
- Servizi di posta AEM
- Modello dati modulo
- Flusso di lavoro AEM
- SharePoint/OneDrive
- Archiviazione BLOB di Azure
- Microsoft Power Automate
- Adobe Workfront Fusion
- Adobe Marketo Engage

### Funzioni principali

| Categoria | Funzionalità |
|----------|-------------|
| **Componenti** | Tutti i tipi di input HTML5, gruppi di caselle di controllo, gruppi pulsanti di scelta, elenco a discesa, pannelli, sezioni ripetibili, file allegati, pannello a soffietto, procedura guidata, modale |
| **Convalida** | Convalida a livello di campo (obbligatoria, min/max, pattern), messaggi di convalida personalizzati |
| **Regole** | Visibilità condizionale, espressioni di valore, regole guidate da eventi |
| **Integrazioni** | Adobe Sign, Salesforce, Microsoft Dynamics, test A/B |
| **Sicurezza** | configurazione reCAPTCHA Enterprise, hCaptcha, CORS |
| **Analytics** | Adobe Experience Platform Web SDK, visualizzazioni dei moduli e monitoraggio dell’invio |

### Prerequisiti

**Per l&#39;authoring basato su documenti:**

- Account GitHub
- Account Google Drive o Microsoft SharePoint
- Nodo/npm per sviluppo locale
- Progetto AEM con blocco Forms adattivo configurato
- Condividi cartella con `forms@adobe.com` (modifica autorizzazioni)

**Per l&#39;editor universale:**

- Istanza AEM Forms as a Cloud Service
- Progetto Edge Delivery Services configurato
- Autorizzazioni richieste per le destinazioni di destinazione

**Per Invio Pubblicazione AEM:**

- URL dell’istanza di AEM Cloud Service configurato
- Configurazione filtro referrer OSGi
- Configurazione CORS per i domini del sito Edge Delivery

### Limitazioni

**Authoring basato su documenti:**

- Denominazione del foglio limitata a `helix-default` e `shared-aem`
- Ideale per moduli a bassa complessità
- Funzionalità con regole limitate
- Nessun flusso di lavoro AEM (senza l’invio della pubblicazione AEM)
- Nessuna integrazione del modello dati modulo

**Editor universale:**

- Importazioni statiche/dinamiche non supportate nelle funzioni personalizzate
- I frammenti di modulo possono essere modificati solo in modo autonomo
- Funzionalità di incorporamento di moduli in sviluppo

**Generale:**

- I fogli `shared-aem` non devono contenere dati PII (accessibili pubblicamente)
- Richiede la configurazione CORS per gli invii tra origini
- Filtro referente OSGi richiesto per gli invii di AEM Publish

### Applicazione consigliata

**Consigliato per:**

- Siti Web critici per le prestazioni che richiedono punteggi Lighthouse elevati
- Siti che utilizzano già Edge Delivery Services
- Sviluppo e distribuzione rapidi dei moduli
- Acquisizione dei dati con complessità da semplice a moderata
- Team che preferiscono l’authoring basato su fogli di calcolo (basato su documenti)
- Progetti che richiedono tempi di realizzazione rapidi

**Non consigliato per:**

- Forms che richiede un&#39;elaborazione estesa lato server
- Integrazione profonda con sistemi legacy privi di API REST
- Requisiti del modulo offline
- Organizzazioni che richiedono framework JavaScript specifici (React, Angular) con controllo completo

## Forms adattivo basato su componenti di base

### Definizione

I componenti di base rappresentano il classico approccio di authoring di AEM Forms. Sono i componenti Forms adattivi originali disponibili in AEM Forms da molti anni. Anche se ancora supportati, Adobe consiglia i Componenti di base principalmente per mantenere i moduli esistenti anziché crearne di nuovi.

### Architettura

I componenti di base utilizzano l’architettura AEM tradizionale:

- **Modello di contenuto**: componente WCM `cq:Page` con struttura di contenuto JCR
- **Struttura principale**: `guideContainer` (radice) → `rootPanel` → `items` (campi modulo)
- **Rendering**: rendering lato server con JavaScript lato client
- **Espressioni SOM**: modello a oggetti script per il riferimento a oggetti modulo

### Modello di rendering

I componenti Foundation utilizzano il rendering lato server:

1. Contenuto del modulo memorizzato nell’archivio JCR
2. Il server AEM elabora la struttura del modulo
3. HTML completo sottoposto a rendering e inviato al browser
4. JavaScript lato client gestisce l’interattività e la convalida

### Funzioni principali

| Categoria | Funzionalità |
|----------|-------------|
| **Componenti** | Oltre 40 componenti, inclusi tutti gli equivalenti dei Componenti core, più: Adobe Sign Block, Chart, Scribble Signature, Image Choice, Summary Step, File Attachment Listing |
| **Modelli modulo** | Modello dati modulo (FDM), modelli XDP/XFA, Schema XML (XSD), Schema JSON |
| **Motore regole** | Editor visivo + editor di codice (per il gruppo forms-power-users) |
| **Firme digitali** | Integrazione di Adobe Sign, firma scarabocchio |
| **Azioni di invio** | Più azioni OOTB simili ai componenti core |

### Componenti esclusivi di Foundation

I seguenti componenti sono **solo disponibili** in Foundation Components:

- Blocco Adobe Sign
- Grafico
- Elenco allegato file
- Segnaposto Nota a piè di pagina
- Scelta immagine
- Firma a mano
- Passaggio di riepilogo
- Captcha Turnstile

### Prerequisiti

- AEM Forms as a Cloud Service o AEM 6.5 Forms
- Modello per moduli adattivi (Foundation)
- Utente nel gruppo `forms-users`

### Limitazioni

- **Pubblicazione**: solo AEM (nessuna API Edge Delivery Services o headless)
- **Prestazioni**: prestazioni standard (non ottimizzate per i punteggi di Lighthouse)
- **Architettura**: architettura legacy senza conformità BEM
- **Apri Source**: non open-source
- **Sviluppo futuro**: modalità manutenzione; nuove funzioni aggiunte principalmente ai componenti core

### Applicazione consigliata

**Consigliato per:**

- Manutenzione dei moduli basati su Foundation esistenti
- Forms che richiede l’integrazione con Adobe Sign o Scribble Signature
- Flussi di lavoro che dipendono dalle funzioni di base stabilite
- Progetti con requisiti di pubblicazione solo per AEM
- Forms che richiede componenti esclusivi di Foundation (grafico, scelta immagine)

**Non consigliato per:**

- Sviluppo di nuovi moduli (utilizzando i Componenti core)
- Progetti che richiedono la pubblicazione Edge Delivery Services
- API per moduli headless
- Implementazioni critiche per le prestazioni
- Progetti con priorità per un&#39;architettura a prova di futuro

## Tabella di confronto

| Parametro | Componenti core | Moduli di Edge Delivery Services | Componenti di base |
|-----------|-----------------|-----------------------------|-----------------------|
| **Stato** | Consigliato per i nuovi moduli | Consigliato per siti ad alte prestazioni | Modalità di manutenzione |
| **Architettura** | Modulare, compatibile con BEM | Edge-first, disaccoppiato | WCM tradizionale |
| **Rendering** | Lato server + Headless | Solo lato client | Lato server |
| **Pubblicazione** | AEM + Edge Delivery + API headless | Solo Edge Delivery Services | Solo AEM |
| **Authoring** | Editor Moduli AEM | Editor universale o fogli di calcolo | Editor Moduli AEM |
| **Prestazioni** | Buono (migliorato rispetto a Foundation) | Eccellente (punteggi elevati in Lighthouse) | Standard |
| **Numero componenti** | 30 | 20+ (tutti i tipi di ingresso HTML5) | 40+ |
| **Apri Source** | Sì (GitHub) | Sì | No |
| **Modello dati modulo** | ✅ | ✅ (solo editor universale) | ✅ |
| **Schema JSON** | ✅ | Limitata | ✅ |
| **Supporto XDP/XFA** | Limitata | ❌ | ✅ |
| **Schema XML** | ❌ | ❌ | ✅ |
| **Motore regole** | Editor visivo avanzato | Avanzato (Editor Universale) / Limitato (Basato Su Documenti) | Editor visivo e di codice avanzato |
| **Firme digitali** | ❌ | ❌ | ✅ |
| **Adobe Sign** | ❌ | Tramite integrazione | ✅ (blocco nativo) |
| **Documento record** | ✅ | ✅ | ✅ |
| **Opzioni CAPTCHA** | reCAPTCHA, hCaptcha | reCAPTCHA Enterprise, hCaptcha | reCAPTCHA, hCaptcha, Turnstile |
| **Flusso di lavoro AEM** | ✅ | ✅ (tramite pubblicazione AEM) | ✅ |
| **API headless** | ✅ (automatico) | ❌ | ❌ |
| **Accessibilità** | Conformità alle linee guida WCAG | Conformità alle linee guida WCAG | Base |
| **Velocità di distribuzione** | Basato su pipeline | Istantanea (esecuzione in tempo reale) | Basato su pipeline |
| **Definizione dello stile** | CSS BEM, temi | CSS, temi a livello di progetto | CSS, temi |
| **Controllo delle versioni** | ✅ (ereditato da Sites) | Basato su Git | ✅ |
| **Localizzazione** | Flusso di lavoro di traduzione AEM | Flusso di lavoro manuale/AEM Sites | Flusso di lavoro di traduzione AEM |

## Matrice di decisione

| Requisito | Approccio consigliato |
|-------------|---------------------|
| Sviluppo di nuovi moduli | Componenti core |
| Manutenzione dei moduli esistenti | Componenti di base (fino alla migrazione) |
| Prestazioni critiche (punteggi elevati di Lighthouse) | Moduli di Edge Delivery Services |
| Distribuzione headless/omnicanale | Componenti core |
| Integrazione con Adobe Sign | Componenti di base |
| Authoring basato su foglio di calcolo | Edge Delivery Services (basato su documenti) |
| Authoring Visual WYSIWYG con distribuzione Edge | Edge Delivery Services (Editor universale) |
| Integrazioni aziendali complesse | Componenti core o componenti di base |
| Prototipazione rapida | Edge Delivery Services (basato su documenti) |
| Supporto per modelli XFA/XDP | Componenti di base |
| React personalizzato/Angular front-end | Componenti core (API headless) |

## Considerazioni sulla migrazione

### Componenti di base in Componenti core

- **Strumento**: Strumenti di modernizzazione AEM (Utilità di conversione Forms)
- **Impegno**: da moderato a elevato a seconda della complessità del modulo
- **Considerazioni**:
   - Le regole richiedono la ricreazione manuale
   - I componenti esclusivi di Foundation (blocco Adobe Sign, firma scarabocchio, grafico) vengono eliminati durante la migrazione
   - Impostazioni di traduzione non riportate
   - Le funzioni personalizzate richiedono la riscrittura

### Tradizionale per Edge Delivery Services

- **Approccio**: ricompilare i moduli utilizzando l&#39;editor universale o l&#39;authoring basato su documenti
- **Impegno**: massimo per moduli complessi, minimo per moduli semplici
- **Vantaggi**: miglioramento significativo delle prestazioni, esperienza di sviluppo moderna

## Lacune e ambiguità nella documentazione

Le seguenti aree hanno una documentazione incompleta o ambigua:

1. **Supporto XDP/XFA dei Componenti core**: la documentazione indica un supporto &quot;limitato&quot;, ma non specifica limitazioni esatte
2. **Incorporamento di Edge Delivery Services Form**: contrassegnato come &quot;In arrivo&quot; nella documentazione; stato corrente non chiaro
3. **Componenti Foundation futuri**: nessuna sequenza temporale di deprecazione esplicita; descritta come &quot;modalità di manutenzione&quot;
4. **Copertura API headless**: non è documentata l&#39;esatta parità di funzionalità tra moduli con rendering del server e moduli headless
5. **Benchmark delle prestazioni**: confronti di punteggi Lighthouse specifici tra approcci non specificati

## Risorse correlate

- [Creare un modulo adattivo (componenti core)](/help/forms/creating-adaptive-form-core-components.md)
- [Creare un modulo adattivo (componenti di base)](/help/forms/creating-adaptive-form.md)
- [Panoramica di Edge Delivery Services Forms](/help/edge/docs/forms/overview.md)
- [Guida introduttiva dell’Editor Universale](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
- [Tutorial sull’authoring basato su documenti](/help/edge/docs/forms/tutorial.md)
- [Utilità di migrazione](/help/forms/migration-utility-tool-for-af-core-components.md)
- [Componenti core AEM Forms su GitHub](https://github.com/adobe/aem-core-forms-components)
