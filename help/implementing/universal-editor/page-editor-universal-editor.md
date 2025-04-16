---
title: Editor Pagina e Editor universale
description: L'editor Pagina rimane supportato da Adobe Systems, ma l'editor universale offre possibilità interessanti ai tuoi nuovi progetti.
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 9fdc24600c9dd4ebf6a3d12462eb9bd387815360
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 3%

---


# Editor Pagina e Editor universale {#page-editor-universal-editor}

L&#39;editor Pagina rimane supportato da Adobe Systems, ma l&#39;editor universale offre possibilità interessanti ai tuoi nuovi progetti.

## Informazioni di base {#background}

Adobe Systems introdotto Universal [Editor](/help/implementing/universal-editor/introduction.md) nel 2024 come editor semplificato che abbraccia un moderno approccio di sviluppo basato su JavaScript. L&#39;Universal Editor è la visione di Adobe Systems per un&#39;esperienza visiva authoring dei contenuti senza soluzione di continuità ed estensibile.

Riconoscendo il ricco set di funzionalità di Pagina [Editor](/help/sites-cloud/authoring/page-editor/introduction.md) e gli innumerevoli progetti che vi hanno investito nel corso della lunga storia di AEM, Adobe Systems continua a supportare pienamente l&#39;Pagina Editor, anche se l&#39;innovazione sarà focalizzata sull&#39;Universal Editor.

## Consiglio {#recommendation}

Sebbene si stia rapidamente restringendo, rimane un divario di funzionalità tra Universal Editor e Pagina Editor ([un confronto delle funzionalità può essere trovato nella prossima sezione](#feature-comparison)).

Come regola empirico:

* **Per impostazione predefinita, i nuovi progetti** devono sfruttare l&#39;Editor universale.
* **I progetti esistenti** devono continuare a utilizzare l&#39;Editor pagina e considerare l&#39;Editor universale all&#39;avvio delle attività di Edge Delivery o headless.

**L&#39;editor scelto deve essere interamente basato sulle esigenze del singolo progetto.**

## Caratteristiche a confronto {#feature-comparison}

Poiché il gap di funzionalità tra i due editor si riduce costantemente, consultare le note sulla versione [di Universal Editor](/help/release-notes/universal-editor/current.md) per gli ultimi sviluppi.

### Distribuzione {#delivery}

|  | Editor pagina | Note | Editor universale | Note |
|---|---|---|---|---|
| [Consegna classica di AEM](/help/sites-cloud/authoring/author-publish.md) | [!BADGE Disponibile]{type=Positive} | Consigliato per l’utilizzo con i Componenti core | [!BADGE Non disponibile]{type=Negative} | Classic AEM pages typically rely on several Page Editor-specific features that are difficult to replicate as-is with the Universal Editor. |
| [Edge Delivery](/help/edge/overview.md) | [!BADGE Non disponibile]{type=Negative} |  | [!BADGE Disponibile]{type=Positive} |  |
| [Consegna headless](/help/headless/introduction.md) | [!BADGE Parzialmente disponibile]{type=Caution} | Solo con [l&#39;editor SPA,](/help/implementing/developing/hybrid/introduction.md) che era [obsoleto](/help/implementing/developing/hybrid/spa-editor-deprecation.md) a favore dell&#39;editor universale | [!BADGE Disponibile]{type=Positive} | L’editor universale consente agli sviluppatori di creare una propria app web senza imporre requisiti di framework o vincoli di implementazione specifici. |

### Persistenza {#persistence}

|  | Editor pagina | Nota | Editor universale | Note |
|---|---|---|---|---|
| Modifica dei componenti di una pagina | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} |  |
| Modifica di [frammenti di contenuto](/help/assets/content-fragments/content-fragments.md) | [!BADGE Non disponibile]{type=Negative} |  | [!BADGE Disponibile]{type=Positive} | Compreso l&#39;inserimento di frammenti nuovi o il riordinamento di frammenti |

### Funzionalità {#capabilities}

|  | Editor pagina | Nota | Editor universale | Note |
|---|---|---|---|---|
| Modelli di pagina | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} | L&#39;editor universale è indipendente dal sistema di modelli utilizzato. However, the typical implementation pattern favors developer-defined templates, as modern frontend tooling makes it much easier for developers to define and maintain template logic directly in code. |
| Modifica WYSIWYG | [!BADGE Disponibile]{type=Positive} limitato a pagine |  | [!BADGE Disponibile]{type=Positive} | Pagine di supporto e frammenti di contenuto |
| [Genera varianti](/help/generative-ai/generate-variations.md) | [!BADGE Indisponibile]{type=Negative} |  | [!BADGE Disponibile]{type=Positive} | [Disponibile come estensione](/help/implementing/universal-editor/extending.md) |
| Inserisci nuovo blocco | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} |  |
| Riordina blocco | [!BADGE Disponibile]{type=Positive} | È possibile con il drag-and-drop contestuale, ma non nel pannello laterale &quot;visualizzazione ad albero&quot; | [!BADGE Disponibile]{type=Positive} | Possibile tramite drag-and-drop nel pannello laterale &quot;vista ad albero&quot;, ma non ancora nel contesto (pianificato) |
| Taglia/Copia-Incolla blocco | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Non disponibile]{type=Negative} | Pianificato |
| Applica stili | [!BADGE Disponibile]{type=Positive} | Gli stili possono essere applicati ai componenti utilizzando [il Sistema di stili.](/help/sites-cloud/authoring/page-editor/style-system.md) | [!BADGE Disponibile]{type=Positive} | Gli stili possono essere applicati utilizzando le proprietà normali del componente (o del frammento di contenuto). Lo stesso selettore di stile non è disponibile nell’editor universale, tuttavia utilizzando un widget a selezione multipla è possibile ottenere un’interfaccia utente molto simile. |
| Applica layout | [!BADGE Disponibile]{type=Positive} | Sites must implement the [AEM Responsive Grid](/help/implementing/developing/introduction/responsive-design.md) to enable authors to resize components across three predefined breakpoints. | [!BADGE Disponibile]{type=Positive} | I layout possono essere applicati utilizzando le proprietà del componente regolare (o Frammento di contenuto), ma la griglia reattiva non è supportata. |
| Undo-Redo | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Non disponibile]{type=Negative} | Pianificato |
| Pubblica (anche in anteprima) | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} |  |
| [Avvia flusso di lavoro](/help/sites-cloud/authoring/workflows/overview.md) | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} | Disponibile come estensione |
| Commentando | [!BADGE Disponibile]{type=Positive} | Using [annotations](/help/sites-cloud/authoring/page-editor/annotations.md) | [!BADGE Non disponibile]{type=Negative} | Pianificato |
| Integrazione con Workfront | [!BADGE Non disponibile]{type=Negative} |  | [!BADGE Disponibile]{type=Positive} | Disponibile come estensione |
| [MSM e avvii](/help/sites-cloud/administering/msm-and-translation.md) | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} | Disponibile per le pagine come estensione |
| Sperimentazione e personalizzazione | [!BADGE Disponibile]{type=Positive} | Utilizzo della [modalità di destinazione](/help/sites-cloud/authoring/personalization/targeted-content.md) | [!BADGE Disponibile]{type=Positive} | Disponibile come estensione per Edge Delivery Services |
| Struttura contenuto | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} | Consente inoltre il riordinamento all&#39;interno della struttura |
| Simulazione dispositivo | [!BADGE Disponibile]{type=Positive} | [I dispositivi configurati possono essere simulati,](/help/sites-cloud/administering/responsive-layout.md) ma il utente non può immettere manualmente dimensioni dello schermo diverse da simulare. | [!BADGE Disponibile]{type=Positive} | [Qualsiasi dimensione dello schermo da simulare può essere immessa manualmente,](/help/sites-cloud/authoring/universal-editor/navigation.md#emulator) ma non è possibile configurare i punti di interruzione predefiniti. |
| [Blocco Pagina](/help/sites-cloud/authoring/sites-console/managing-pages.md) | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} | Rispetta lo stato di blocco impostato nella console Sites con estensione disponibile per bloccare/sbloccare pagine dal editor |
| [Pagina proprietà](/help/sites-cloud/authoring/sites-console/page-properties.md) | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} | Disponibile presso l&#39;amministratore del sito, con estensione per accesso anche le proprietà delle pagine del editor |
| Proprietà con più campi | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Non disponibile]{type=Negative} | Pianificato |
| [DAM remoto](/help/assets/dynamic-media-open-apis-overview.md) | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} |  |
| [Controllo delle versioni delle pagine](/help/sites-cloud/authoring/sites-console/page-versions.md) | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} |  |
| [TimeWarp](/help/sites-cloud/authoring/sites-console/page-versions.md#timewarp) e [Diff View](/help/sites-cloud/authoring/sites-console/page-diff.md) | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Non disponibile]{type=Negative} | Pianificato |
| View in admin | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} | Disponibile come estensione per le pagine |
| Visualizza stato pagina | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Non disponibile]{type=Negative} | Disponibile nella console Sites |
| Estensibilità | [!BADGE Disponibile]{type=Positive} | Come AEM sovrapposizioni | [!BADGE Disponibile]{type=Positive} | Punti di estensione chiaramente definiti utilizzando App Builder e conoscenze specifiche di AEM molto limitate |

## Adozione dell’editor universale {#adopt-ue}

Universal Editor offre numerosi vantaggi, rendendolo una soluzione ideale per nuovi progetti.

* **Visual Editing:** Like for the Page Editor, authors can edit content directly within the preview and instantly see how their changes affect the visitor experience.
* **Future-Proofing:** la roadmap di AEM dà priorità all&#39;editor universale come editor visivo. Adopting it ensures access to the latest innovations and enhancements.
* **Integrazione semplificata:** Non è necessario alcun SDK specifico per AEM per utilizzare Universal Editor, riducendo il blocco dello stack tecnologico.
* **Porta la tua app:** Universal Editor supporta qualsiasi framework o architettura Web, consentendo l&#39;adozione senza richiedere il refactoring complesso.
* **Estensibilità:** Universal Editor dispone di un solido framework di [estensione,](/help/implementing/universal-editor/extending.md) che include integrazioni con GenAI, Workfront e altro ancora.

### Migrazione all’editor universale {#migrate-ue}

Non esiste un percorso di migrazione diretta dall’Editor pagina all’Editor universale. Ciò è dovuto a differenze fondamentali nelle due tecnologie.

* L’editor universale non reintroduce funzioni quali Editor modelli, Sistema di stili o Griglia reattiva.
   * Questi casi d’uso possono ora essere gestiti in modo più efficiente con CSS e JavaScript front-end snelli in Edge Delivery Services o progetti headless.
* Poiché l’editor universale è un editor come servizio, non può consentire agli implementatori di inserire CSS o JS nelle finestre di dialogo dei componenti.
   * Questo impedisce la conversione automatica delle finestre di dialogo dei componenti dall’Editor pagina.
   * Ciò interessa molte aree delle finestre di dialogo, like widget personalizzati, convalida dei campi, regole di visualizzazione/nascondere e personalizzazioni basate su modelli.
      * Sebbene tali funzionalità siano ancora possibili, Universal Editor le risolve attraverso la configurazione, anziché JavaScript personalizzate distribuite nelle finestre di dialogo.

Mentre Universal Editor può tecnicamente consentire la modifica per le pagine AEM classiche (ad esempio costruite con i componenti core), questi siti in genere si basano su diverse funzionalità specifiche dell&#39;editor Pagina, come il sistema di stili, la griglia reattiva, i modelli modificabili e il javascript personalizzato all&#39;interno delle finestre di dialogo.

Poiché Universal Editor adotta un approccio più semplice e moderno che non supporta queste funzioni legacy, la migrazione di tali siti richiederebbe un refactoring significativo. Per questo motivo, **la migrazione dei siti Editor pagina nell&#39;Editor universale è consigliata solo per i progetti che passano a Edge Delivery Services.**
