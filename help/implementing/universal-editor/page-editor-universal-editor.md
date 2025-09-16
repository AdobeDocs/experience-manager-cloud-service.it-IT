---
title: Editor di pagine ed editor universale
description: L’editor di pagine continua ad essere supportato da Adobe, ma l’editor universale offre nuove possibilità per i nuovi progetti.
feature: Developing
role: Admin, Architect, Developer
exl-id: 0a13fb52-623e-4aff-b254-186d8d117e4d
source-git-commit: fd52e51c336e65ae698c5102cbe00b90e7038b5e
workflow-type: tm+mt
source-wordcount: '1068'
ht-degree: 99%

---

# Editor di pagine ed editor universale {#page-editor-universal-editor}

L’editor di pagine continua ad essere supportato da Adobe, ma l’editor universale offre nuove possibilità per i nuovi progetti.

## Esperienza pregressa {#background}

Adobe ha introdotto l’[editor universale](/help/implementing/universal-editor/introduction.md) nel 2024 come editor semplificato che adotta un approccio di sviluppo moderno basato su JavaScript. L’editor universale è la visione di Adobe per un’esperienza di authoring di contenuti visivi fluida ed estensibile.

Riconoscendo la ricca serie di funzioni dell’[editor di pagine](/help/sites-cloud/authoring/page-editor/introduction.md) e gli innumerevoli progetti che vi investono nel corso della lunga storia di AEM, Adobe continua a supportare completamente l’editor di pagine, anche se l’innovazione sarà incentrata sull’editor universale.

## Consiglio {#recommendation}

Sebbene si stia riducendo rapidamente, rimane una differenza di funzionalità tra l’editor universale e l’editor di pagine ([nella sezione successiva è disponibile un confronto delle funzionalità](#feature-comparison).)

Come regola generale:

* **I nuovi progetti** dovrebbero sfruttare come impostazione predefinita l’editor universale.
* **I progetti esistenti** devono continuare a utilizzare l’editor pagina e prendere in considerazione l’editor universale all’avvio di iniziative Edge Delivery o headless.

**L’editor deve essere scelto interamente sulla base delle esigenze del singolo progetto.**

## Confronto funzioni {#feature-comparison}

Poiché il gap di funzionalità tra i due editor si riduce costantemente, consulta le [note sulla versione dell’editor universale](/help/release-notes/universal-editor/current.md) per gli ultimi sviluppi.

### Distribuzione {#delivery}

|  | Editor di pagine | Note | Editor universale | Note |
|---|---|---|---|---|
| [Pubblicazione della consegna](/help/sites-cloud/authoring/author-publish.md) | [!BADGE Disponibile]{type=Positive} | Consigliato per l’utilizzo con i Componenti core e i progetti AEM tradizionali | [!BADGE Non disponibile]{type=Negative} | Le pagine tradizionali di AEM in genere si basano su diverse funzioni specifiche dell’editor pagina, che sono difficili da replicare tali e quali con l’editor universale. |
| [Edge Delivery](/help/edge/overview.md) | [!BADGE Non disponibile]{type=Negative} |  | [!BADGE Disponibile]{type=Positive} |  |
| [Consegna headless](/help/headless/introduction.md) | [!BADGE Parzialmente disponibile]{type=Caution} | Solo con [l’editor SPA,](/help/implementing/developing/hybrid/introduction.md) dichiarato [obsoleto](/help/implementing/developing/hybrid/spa-editor-deprecation.md) a favore dell’editor universale | [!BADGE Disponibile]{type=Positive} | L’editor universale consente agli sviluppatori di creare una propria app web senza imporre requisiti di framework o vincoli di implementazione specifici. |

### Persistenza {#persistence}

|  | Editor di pagine | Note | Editor universale | Note |
|---|---|---|---|---|
| Modifica dei componenti di una pagina | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} |  |
| Modifica dei [Frammenti di contenuto](/help/assets/content-fragments/content-fragments.md) | [!BADGE Non disponibile]{type=Negative} |  | [!BADGE Disponibile]{type=Positive} | Inclusione dell’inserimento di nuovi frammenti e riordinamento degli stessi |

### Funzionalità {#capabilities}

|  | Editor di pagine | Note | Editor universale | Note |
|---|---|---|---|---|
| Modelli di pagina | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} | L’editor universale è indipendente dal sistema di modelli utilizzato. Tuttavia, il modello di implementazione tipico favorisce i modelli definiti dagli sviluppatori, in quanto i moderni strumenti front-end consentono agli sviluppatori di definire e gestire più facilmente la logica dei modelli direttamente nel codice. |
| Modifica WYSIWYG | [!BADGE Disponibile]{type=Positive} | Limitata alle pagine | [!BADGE Disponibile]{type=Positive} | Pagine di supporto e frammenti di contenuto |
| [Generare varianti](/help/generative-ai/generate-variations.md) | [!BADGE Non disponibile]{type=Negative} |  | [!BADGE Disponibile]{type=Positive} | [Disponibile come estensione](/help/implementing/universal-editor/extending.md) |
| Inserimento nuovo blocco | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} |  |
| Riordinamento blocco | [!BADGE Disponibile]{type=Positive} | Possibile con trascinamento nel contesto, ma non nel pannello laterale “visualizzazione struttura” | [!BADGE Disponibile]{type=Positive} | È possibile con trascinamento in ”visualizzazione struttura”, ma non ancora nel contesto (pianificato) |
| Taglia/Copia-Incolla blocco | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Non disponibile]{type=Negative} | Pianificato |
| Applicazione stili | [!BADGE Disponibile]{type=Positive} | Gli stili possono essere applicati ai componenti utilizzando [il sistema di stili.](/help/sites-cloud/authoring/page-editor/style-system.md) | [!BADGE Disponibile]{type=Positive} | Gli stili possono essere applicati utilizzando le proprietà normali del componente (o del frammento di contenuto). Lo stesso selettore di stile non è disponibile nell’editor universale, tuttavia utilizzando un widget a selezione multipla è possibile ottenere un’interfaccia utente molto simile. |
| Applicazione layout | [!BADGE Disponibile]{type=Positive} | I siti devono implementare la [griglia reattiva di AEM](/help/implementing/developing/introduction/responsive-design.md) per consentire agli autori di ridimensionare i componenti in tre punti di interruzione predefiniti. | [!BADGE Disponibile]{type=Positive} | I layout possono essere applicati utilizzando le proprietà del componente regolare (o frammento di contenuto), ma la griglia reattiva non è supportata. |
| Annulla-Ripristina | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} |  |
| Pubblicazione (anche in anteprima) | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} |  |
| [Avvio del flusso di lavoro](/help/sites-cloud/authoring/workflows/overview.md) | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} | Disponibile come estensione |
| Commento | [!BADGE Disponibile]{type=Positive} | Utilizzo di [annotazioni](/help/sites-cloud/authoring/page-editor/annotations.md) | [!BADGE Non disponibile]{type=Negative} | Pianificato |
| Integrazione di Workfront | [!BADGE Non disponibile]{type=Negative} |  | [!BADGE Disponibile]{type=Positive} | Disponibile come estensione |
| [MSM e lanci](/help/sites-cloud/administering/msm-and-translation.md) | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} | Disponibile per le pagine come estensione |
| Sperimentazione e personalizzazione | [!BADGE Disponibile]{type=Positive} | Utilizzo della [modalità targeting](/help/sites-cloud/authoring/personalization/targeted-content.md) | [!BADGE Disponibile]{type=Positive} | Disponibile come estensione per Edge Delivery Services |
| Struttura contenuto | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} | Consente inoltre il riordinamento all’interno della struttura |
| Simulazione dispositivo | [!BADGE Disponibile]{type=Positive} | [È possibile simulare i dispositivi configurati](/help/sites-cloud/administering/responsive-layout.md), ma l’utente non può immettere manualmente dimensioni dello schermo diverse da simulare. | [!BADGE Disponibile]{type=Positive} | [È possibile immettere manualmente qualsiasi dimensione dello schermo da simulare](/help/sites-cloud/authoring/universal-editor/navigation.md#emulator), ma non è possibile configurare i punti di interruzione predefiniti. |
| [Blocco pagina](/help/sites-cloud/authoring/sites-console/managing-pages.md) | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} | Rispetta lo stato di blocco impostato nella console Sites con l’estensione disponibile per bloccare/sbloccare le pagine dall’editor |
| [Proprietà pagina](/help/sites-cloud/authoring/sites-console/edit-page-properties.md) | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} | Disponibile dall’amministratore del sito, con estensione per accedere anche alle proprietà delle pagine dall’editor |
| Proprietà con più campi | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Non disponibile]{type=Negative} | Pianificato |
| [DAM remoto](/help/assets/dynamic-media-open-apis-overview.md) | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} |  |
| [Controllo delle versioni della pagina](/help/sites-cloud/authoring/sites-console/page-versions.md) | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} |  |
| [Timewarp](/help/sites-cloud/authoring/sites-console/page-versions.md#timewarp) e [Visualizzazione differenze](/help/sites-cloud/authoring/sites-console/page-diff.md) | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Non disponibile]{type=Negative} | Pianificato |
| Visualizzazione in Amministrazione | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Disponibile]{type=Positive} | Disponibile come estensione per le pagine |
| Visualizzare lo stato della pagina | [!BADGE Disponibile]{type=Positive} |  | [!BADGE Non disponibile]{type=Negative} | Disponibile nella console AEM Sites |
| Estensibilità | [!BADGE Disponibile]{type=Positive} | Come sovrapposizioni di AEM | [!BADGE Disponibile]{type=Positive} | Punti di estensione ben definiti utilizzando App Builder e conoscenze specifiche di AEM molto limitate |

## Iniziare a utilizzare l’editor universale {#adopt-ue}

L’editor universale offre numerosi vantaggi, pertanto è una soluzione ideale per nuovi progetti.

* **Modifica visiva:** come per l’editor di pagine, gli autori possono modificare il contenuto direttamente nell’anteprima e visualizzare immediatamente come le modifiche influiscono sull’esperienza del visitatore.
* **Future-Proofing:** la roadmap di AEM dà priorità all&#39;editor universale come editor visivo. Il suo utilizzo garantisce l’accesso alle innovazioni e ai miglioramenti più recenti.
* **Integrazione semplificata:** non è necessario alcun SDK specifico per AEM per utilizzare l’editor universale, così si riduce il blocco dello stack tecnologico.
* **Porta la tua app:** l’editor universale supporta qualsiasi framework o architettura web, consentendo l’utilizzo senza richiedere un refactoring complesso.
* **Estensibilità:** l’editor universale dispone di un solido [framework di estensione](/help/implementing/universal-editor/extending.md), che include integrazioni con GenAI, Workfront e altro ancora.

### Eseguire la migrazione all’editor universale {#migrate-ue}

Non esiste un percorso di migrazione diretta dall’editor pagina all’editor universale. Ciò è dovuto a differenze fondamentali nelle due tecnologie.

* L’editor universale non reintroduce funzioni quali Editor modelli, Sistema di stili o Griglia reattiva.
   * Questi casi d’uso possono ora essere gestiti in modo più efficiente con CSS e JavaScript front-end snelli in Edge Delivery Services o progetti headless.
* Poiché è un editor-as-a-service, l’editor universale non può consentire agli implementatori di inserire CSS o JS nelle finestre di dialogo dei componenti.
   * In tal modo si impedisce la conversione automatica delle finestre di dialogo dei componenti dall’editor pagina.
   * Questo interessa molte aree delle finestre di dialogo, come i widget personalizzati, la convalida dei campi, le regole mostra/nascondi e le personalizzazioni basate su modelli.
      * Anche se tali funzionalità sono ancora possibili, l’editor universale le risolve tramite la configurazione, al posto di JavaScript personalizzato distribuito nelle finestre di dialogo.

Sebbene l’editor universale possa tecnicamente abilitare le pagine di modifica per i progetti AEM tradizionali (ad esempio, generati con i componenti core), questi siti in genere si basano su diverse funzioni specifiche dell’editor pagina, come il Sistema di stili, la Griglia reattiva, i Modelli modificabili e JavaScript personalizzato all’interno delle finestre di dialogo.

Poiché l’editor universale adotta un approccio più semplice e moderno che non supporta le funzioni precedenti, la migrazione di tali siti richiederebbe un refactoring significativo. Per questo motivo, **la migrazione dei siti di editor pagina nell’editor universale è consigliata solo per i progetti che passano a Edge Delivery Services.**
