---
title: Editor pagina ed editor universale
description: L’Editor pagina rimane supportato da Adobe, ma l’Editor universale offre nuove possibilità per i tuoi nuovi progetti.
feature: Developing
role: Admin, Architect, Developer
exl-id: 0a13fb52-623e-4aff-b254-186d8d117e4d
source-git-commit: fd52e51c336e65ae698c5102cbe00b90e7038b5e
workflow-type: tm+mt
source-wordcount: '1068'
ht-degree: 3%

---

# Editor pagina ed editor universale {#page-editor-universal-editor}

L’Editor pagina rimane supportato da Adobe, ma l’Editor universale offre nuove possibilità per i tuoi nuovi progetti.

## Esperienza pregressa {#background}

Adobe ha introdotto [Universal Editor](/help/implementing/universal-editor/introduction.md) nel 2024 come editor semplificato che adotta un approccio di sviluppo moderno basato su JavaScript. Universal Editor è la visione di Adobe per un’esperienza di authoring di contenuti visivi fluida ed estensibile.

Riconoscendo la ricca serie di funzioni dell&#39;[Editor pagine](/help/sites-cloud/authoring/page-editor/introduction.md) e gli innumerevoli progetti che vi investono nel corso della lunga storia di AEM, Adobe continua a supportare completamente l&#39;Editor pagine, anche se l&#39;innovazione sarà incentrata sull&#39;Editor universale.

## Consiglio {#recommendation}

Sebbene si stia riducendo rapidamente, rimane uno spazio vuoto tra le funzionalità di Editor universale e Editor pagina ([nella sezione successiva](#feature-comparison) è disponibile un confronto delle funzionalità.

Come regola empirica:

* **Per impostazione predefinita, i nuovi progetti** devono sfruttare l&#39;Editor universale.
* **I progetti esistenti** devono continuare a utilizzare l&#39;Editor pagina e considerare l&#39;Editor universale all&#39;avvio delle attività di Edge Delivery o headless.

**L&#39;editor scelto deve essere interamente basato sulle esigenze del singolo progetto.**

## Caratteristiche a confronto {#feature-comparison}

Poiché il gap di funzionalità tra i due editor si riduce costantemente, consultare le note sulla versione [di Universal Editor](/help/release-notes/universal-editor/current.md) per gli ultimi sviluppi.

### Distribuzione {#delivery}

|  | Editor pagina | Note | Editor universale | Note |
|---|---|---|---|---|
| [Pubblica consegna](/help/sites-cloud/authoring/author-publish.md) | [!BADGE Disponibile]{type=Positive} | Consigliato per l’utilizzo con i Componenti core e i progetti AEM tradizionali | [!BADGE Non disponibile]{type=Negative} | Le pagine tradizionali di AEM in genere si basano su diverse funzioni specifiche dell’Editor pagina che sono difficili da replicare così com’è con l’Editor universale. |
| [Edge Delivery](/help/edge/overview.md) | [!BADGE Non disponibile]{type=Negative} |  | [!BADGE Disponibile]{type=Positive} |  |
| [Consegna headless](/help/headless/introduction.md) | [!BADGE Parzialmente disponibile]{type=Caution} | Solo con [l&#39;editor SPA,](/help/implementing/developing/hybrid/introduction.md) che era [obsoleto](/help/implementing/developing/hybrid/spa-editor-deprecation.md) a favore dell&#39;editor universale | [!BADGE Disponibile]{type=Positive} | L’editor universale consente agli sviluppatori di creare una propria app web senza imporre requisiti di framework o vincoli di implementazione specifici. |

### Persistenza {#persistence}

|  | Editor pagina | Note | Editor universale | Note |
|---|---|---|---|---|
| Modifica dei componenti di una pagina | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} |  |
| Modifica di [frammenti di contenuto](/help/assets/content-fragments/content-fragments.md) | [!BADGE Non disponibile]{type=Negative} |  | [!BADGE Disponibile]{type=Positive} | Inclusione dell’inserimento di nuovi frammenti e riordinamento degli stessi |

### Funzionalità {#capabilities}

|  | Editor pagina | Note | Editor universale | Note |
|---|---|---|---|---|
| Modelli di pagina | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} | L’editor universale è indipendente dal sistema di modelli utilizzato. Tuttavia, il modello di implementazione tipico favorisce i modelli definiti dagli sviluppatori, in quanto i moderni strumenti front-end consentono agli sviluppatori di definire e gestire più facilmente la logica dei modelli direttamente nel codice. |
| Modifica WYSIWYG | [!BADGE Disponibile]{type=Positive} | Limitato alle pagine | [!BADGE Disponibile]{type=Positive} | Pagine di supporto e frammenti di contenuto |
| [Generare varianti](/help/generative-ai/generate-variations.md) | [!BADGE Non disponibile]{type=Negative} |  | [!BADGE Disponibile]{type=Positive} | [Disponibile come estensione](/help/implementing/universal-editor/extending.md) |
| Inserisci nuovo blocco | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} |  |
| Riordina blocco | [!BADGE Disponibile]{type=Positive} | Possibile con trascinamento nel contesto, ma non nel pannello laterale &quot;visualizzazione struttura&quot; | [!BADGE Disponibile]{type=Positive} | È possibile trascinarlo nella vista ad albero, ma non ancora nel contesto (operazione pianificata) |
| Taglia/Copia-Incolla blocco | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Non disponibile]{type=Negative} | Pianificato |
| Applica stili | [!BADGE Disponibile]{type=Positive} | Gli stili possono essere applicati ai componenti utilizzando [il sistema di stili.](/help/sites-cloud/authoring/page-editor/style-system.md) | [!BADGE Disponibile]{type=Positive} | Gli stili possono essere applicati utilizzando le proprietà normali del componente (o del frammento di contenuto). Lo stesso selettore di stile non è disponibile nell’editor universale, tuttavia utilizzando un widget a selezione multipla è possibile ottenere un’interfaccia utente molto simile. |
| Applica layout | [!BADGE Disponibile]{type=Positive} | I siti devono implementare la [griglia reattiva di AEM](/help/implementing/developing/introduction/responsive-design.md) per consentire agli autori di ridimensionare i componenti in tre punti di interruzione predefiniti. | [!BADGE Disponibile]{type=Positive} | I layout possono essere applicati utilizzando le proprietà del componente regolare (o Frammento di contenuto), ma la griglia reattiva non è supportata. |
| Annulla-Ripristina | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} |  |
| Pubblica (anche in anteprima) | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} |  |
| [Avvia flusso di lavoro](/help/sites-cloud/authoring/workflows/overview.md) | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} | Disponibile come estensione |
| Commento | [!BADGE Disponibile]{type=Positive} | Utilizzo di [annotazioni](/help/sites-cloud/authoring/page-editor/annotations.md) | [!BADGE Non disponibile]{type=Negative} | Pianificato |
| Integrazione di Workfront | [!BADGE Non disponibile]{type=Negative} |  | [!BADGE Disponibile]{type=Positive} | Disponibile come estensione |
| [MSM e avvii](/help/sites-cloud/administering/msm-and-translation.md) | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} | Disponibile per le pagine come estensione |
| Sperimentazione e personalizzazione | [!BADGE Disponibile]{type=Positive} | Utilizzo della [modalità di destinazione](/help/sites-cloud/authoring/personalization/targeted-content.md) | [!BADGE Disponibile]{type=Positive} | Disponibile come estensione per Edge Delivery Services |
| Struttura contenuto | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} | Consente inoltre il riordinamento all&#39;interno della struttura |
| Simulazione dispositivo | [!BADGE Disponibile]{type=Positive} | [È possibile simulare i dispositivi configurati](/help/sites-cloud/administering/responsive-layout.md), ma l&#39;utente non può immettere manualmente dimensioni dello schermo diverse da simulare. | [!BADGE Disponibile]{type=Positive} | [È possibile immettere manualmente qualsiasi dimensione dello schermo da simulare](/help/sites-cloud/authoring/universal-editor/navigation.md#emulator), ma non è possibile configurare i punti di interruzione predefiniti. |
| [Blocco pagine](/help/sites-cloud/authoring/sites-console/managing-pages.md) | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} | Rispetta lo stato di blocco impostato nella console Sites con l’estensione disponibile per bloccare/sbloccare le pagine dall’editor |
| [Proprietà pagina](/help/sites-cloud/authoring/sites-console/edit-page-properties.md) | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} | Disponibile dall’amministratore del sito, con estensione per accedere anche alle proprietà delle pagine dall’editor |
| Proprietà con più campi | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Non disponibile]{type=Negative} | Pianificato |
| [DAM remoto](/help/assets/dynamic-media-open-apis-overview.md) | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} |  |
| [Controllo delle versioni delle pagine](/help/sites-cloud/authoring/sites-console/page-versions.md) | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} |  |
| [TimeWarp](/help/sites-cloud/authoring/sites-console/page-versions.md#timewarp) e [Diff View](/help/sites-cloud/authoring/sites-console/page-diff.md) | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Non disponibile]{type=Negative} | Pianificato |
| Visualizza in amministrazione | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} | Disponibile come estensione per le pagine |
| Visualizza stato pagina | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Non disponibile]{type=Negative} | Disponibile nella console Sites |
| Estensibilità | [!BADGE Disponibile]{type=Positive} | Come sovrapposizioni di AEM | [!BADGE Disponibile]{type=Positive} | Punti di estensione chiaramente definiti utilizzando App Builder e conoscenze specifiche di AEM molto limitate |

## Adozione dell’editor universale {#adopt-ue}

Universal Editor offre numerosi vantaggi, rendendolo una soluzione ideale per nuovi progetti.

* **Modifica visiva:** Come per l&#39;Editor pagina, gli autori possono modificare il contenuto direttamente nell&#39;anteprima e vedere immediatamente come le loro modifiche influiscono sull&#39;esperienza del visitatore.
* **Future-Proofing:** la roadmap di AEM dà priorità all&#39;editor universale come editor visivo. La sua adozione garantisce l’accesso alle innovazioni e ai miglioramenti più recenti.
* **Integrazione semplificata:** Non è necessario alcun SDK specifico per AEM per utilizzare Universal Editor, riducendo il blocco dello stack tecnologico.
* **Porta la tua app:** Universal Editor supporta qualsiasi framework o architettura Web, consentendo l&#39;adozione senza richiedere il refactoring complesso.
* **Estensibilità:** Universal Editor dispone di un solido framework di [estensione,](/help/implementing/universal-editor/extending.md) che include integrazioni con GenAI, Workfront e altro ancora.

### Migrazione all’editor universale {#migrate-ue}

Non esiste un percorso di migrazione diretta dall’Editor pagina all’Editor universale. Ciò è dovuto a differenze fondamentali nelle due tecnologie.

* L’editor universale non reintroduce funzioni quali Editor modelli, Sistema di stili o Griglia reattiva.
   * Questi casi d’uso possono ora essere gestiti in modo più efficiente con CSS e JavaScript front-end snelli in Edge Delivery Services o progetti headless.
* Poiché l’editor universale è un editor come servizio, non può consentire agli implementatori di inserire CSS o JS nelle finestre di dialogo dei componenti.
   * Questo impedisce la conversione automatica delle finestre di dialogo dei componenti dall’Editor pagina.
   * Questo interessa molte aree delle finestre di dialogo, come i widget personalizzati, la convalida dei campi, le regole mostra/nascondi e le personalizzazioni basate su modelli.
      * Anche se tali funzionalità sono ancora possibili, l’Editor universale le risolve tramite la configurazione, invece di JavaScript personalizzato distribuito nelle finestre di dialogo.

Sebbene Universal Editor possa tecnicamente abilitare le pagine di modifica per i progetti AEM tradizionali (ad esempio generati con i Componenti core), questi siti in genere si basano su diverse funzioni specifiche dell’Editor pagina, come il Sistema di stili, la Griglia reattiva, i Modelli modificabili e JavaScript personalizzato all’interno delle finestre di dialogo.

Poiché Universal Editor adotta un approccio più semplice e moderno che non supporta queste funzioni legacy, la migrazione di tali siti richiederebbe un refactoring significativo. Per questo motivo, **la migrazione dei siti Editor pagina nell&#39;Editor universale è consigliata solo per i progetti che passano a Edge Delivery Services.**
