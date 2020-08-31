---
title: Sviluppo di SPA per AEM
description: Questo articolo presenta domande importanti da tenere in considerazione quando uno sviluppatore front-end si impegna a sviluppare una SPA per AEM e fornisce una panoramica dell'architettura di AEM rispetto alle SPA da tenere presente quando si implementa una SPA sviluppata su AEM.
translation-type: tm+mt
source-git-commit: d0685af8b05d5491debf7bad99b5c8f111808f26
workflow-type: tm+mt
source-wordcount: '2088'
ht-degree: 0%

---


# Sviluppo di SPA per AEM {#developing-spas-for-aem}

Le applicazioni SPA (Single Page Applications) possono offrire esperienze coinvolgenti agli utenti di siti Web. Gli sviluppatori desiderano essere in grado di creare siti utilizzando i framework SPA e gli autori desiderano modificare i contenuti all&#39;interno AEM per un sito creato utilizzando tali framework.

Questo articolo presenta domande importanti da tenere in considerazione quando uno sviluppatore front-end si impegna a sviluppare una SPA per AEM e fornisce una panoramica dell&#39;architettura di AEM per quanto riguarda l&#39;implementazione di SPA su AEM.

## Principi di sviluppo SPA per AEM {#spa-development-principles-for-aem}

Lo sviluppo di applicazioni a pagina singola in AEM presuppone che lo sviluppatore front-end rispetti le best practice standard per la creazione di un&#39;app SPA. Se uno sviluppatore front-end segue queste best practice generali e pochi principi AEM specifici, l&#39;SPA funzionerà con le funzioni di creazione dei [AEM e di creazione dei contenuti](introduction.md#content-editing-experience-with-spa).

* **[Portabilità](#portability)** - Come per qualsiasi componente, i componenti devono essere costruiti per essere il più possibile portatili. La SPA deve essere realizzata con componenti portabili e riutilizzabili.
* **[AEM struttura](#aem-drives-site-structure)** del sito - Lo sviluppatore front-end crea componenti e possiede la propria struttura interna, ma si basa su AEM per definire la struttura del contenuto del sito.
* **[Rendering](#dynamic-rendering)** dinamico - Il rendering deve essere dinamico.
* **[Routing](#dynamic-routing)** dinamico - L&#39;SPA è responsabile dell&#39;instradamento e AEM lo ascolta e recupera in base ad esso. Anche l&#39;indirizzamento deve essere dinamico.

Se tenete presenti questi principi nello sviluppo dell&#39;SPA, sarà quanto più flessibile e affidabile possibile, consentendo al contempo tutte le funzionalità di authoring AEM supportate.

Se non è necessario supportare AEM funzioni di authoring, potrebbe essere necessario considerare un diverso modello [di progettazione](#spa-design-models)SPA.

### Portabilità {#portability}

Come per lo sviluppo di qualsiasi componente, i componenti devono essere progettati in modo da massimizzarne la portabilità. Eventuali schemi che contrastino con la portabilità o riutilizzabilità dei componenti dovrebbero essere evitati per garantire compatibilità, flessibilità e manutenibilità in futuro.

La SPA risultante deve essere realizzata con componenti altamente portatili e riutilizzabili.

### AEM struttura del sito {#aem-drives-site-structure}

Lo sviluppatore front-end deve considerare se stesso come responsabile della creazione di una libreria di componenti SPA utilizzati per creare l&#39;app. Lo sviluppatore front-end ha il controllo completo della struttura interna dei componenti. [Tuttavia AEM possiede sempre la struttura del sito.](editor-overview.md)

Questo significa che lo sviluppatore front-end può aggiungere il contenuto del cliente prima o dopo il punto di ingresso dei componenti e può anche effettuare chiamate di terze parti all’interno del componente. Tuttavia, lo sviluppatore front-end non ha il controllo completo del modo in cui i componenti vengono nidificati, ad esempio.

### Rendering dinamico {#dynamic-rendering}

L&#39;area SPA deve basarsi solo sul rendering dinamico dei contenuti. Questa è l&#39;aspettativa predefinita in cui AEM recupera e visualizza tutti gli elementi secondari della struttura del contenuto.

Qualsiasi rendering esplicito che punti a contenuto specifico viene considerato come rendering statico e, anche se supportato, non sarà compatibile con AEM funzioni di authoring dei contenuti. Ciò va anche contro il principio di [portabilità](#portability).

### Routing dinamico {#dynamic-routing}

Come per il rendering, anche tutti i routing devono essere dinamici. In AEM, [l&#39;SPA deve sempre possedere l&#39;indirizzamento](routing.md) e AEM ascoltare e recuperare il contenuto in base ad esso.

Qualsiasi routing statico funziona in base al [principio di portabilità](#portability) e limita l’autore in quanto non è compatibile con le funzioni di authoring dei contenuti di AEM. Ad esempio, con l&#39;indirizzamento statico, se l&#39;autore del contenuto desidera modificare una route o una pagina, deve chiedere allo sviluppatore front-end di farlo.

## AEM Project Archetype {#aem-project-archetype}

Qualsiasi progetto AEM dovrebbe sfruttare il [AEM Project Archetype](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/archetype/overview.html), che supporta i progetti SPA utilizzando React o Angular e sfrutta l’SDK SPA.

## Modelli di progettazione SPA {#spa-design-models}

Se [vengono seguiti i principi dello sviluppo di SPA in AEM](#spa-development-principles-for-aem) , l&#39;SPA funzionerà con tutte le funzioni AEM di authoring dei contenuti supportate.

Ci possono essere tuttavia dei casi in cui ciò non è del tutto necessario. La tabella seguente fornisce una panoramica dei vari modelli di progettazione, dei relativi vantaggi e dei relativi svantaggi.

<table>
 <tbody>
  <tr>
   <th><strong>Modello di progettazione<br /> </strong></th>
   <th><strong>Vantaggi</strong></th>
   <th><strong>Svantaggi</strong></th>
  </tr>
  <tr>
   <td>AEM viene utilizzato come CMS headless senza utilizzare il framework SDK <a href="https://docs.adobe.com/content/help/en/experience-manager-65/developing/headless/spas/spa-reference-materials.html">SPA Editor.</a></td>
   <td>Lo sviluppatore front-end ha il controllo completo sull'app.</td>
   <td><p>Gli autori dei contenuti non possono sfruttare AEM'esperienza di authoring dei contenuti.</p> <p>Il codice non è né portatile né riutilizzabile se contiene riferimenti statici o routing.</p> <p>Non consente l'utilizzo dell'editor modelli, pertanto lo sviluppatore front-end deve mantenere i modelli modificabili tramite JCR.</p> </td>
  </tr>
  <tr>
   <td>Lo sviluppatore front-end utilizza il framework SPA Editor SDK, ma apre solo alcune aree all’autore del contenuto.</td>
   <td>Lo sviluppatore mantiene il controllo sull'app abilitando solo l'authoring nelle aree limitate dell'app.</td>
   <td><p>Gli autori dei contenuti sono limitati a una serie limitata di esperienze di authoring AEM contenuto.</p> <p>Il codice non può essere portatile né riutilizzabile se contiene riferimenti statici o routing.</p> <p>Non consente l'utilizzo dell'editor modelli, pertanto lo sviluppatore front-end deve mantenere i modelli modificabili tramite JCR.</p> </td>
  </tr>
  <tr>
   <td>Il progetto sfrutta appieno l’SDK dell’editor SPA e i componenti frontend sono sviluppati come libreria e la struttura del contenuto dell’app è delegata a AEM.</td>
   <td><p>L'app è riutilizzabile e portatile.</p> <p>L'autore del contenuto può modificare l'app utilizzando AEM'esperienza di creazione del contenuto.<br /> </p> <p>L'SPA è compatibile con l'editor modelli.</p> </td>
   <td><p>Lo sviluppatore non ha il controllo della struttura dell'app e della parte di contenuto delegata a AEM.</p> <p>Lo sviluppatore può comunque riservare aree dell'app per il contenuto che non deve essere creato utilizzando AEM.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Anche se tutti i modelli sono supportati in AEM, solo implementando il terzo (e quindi seguendo i principi di sviluppo [SPA consigliati in AEM](#spa-development-principles-for-aem)) gli autori dei contenuti potranno interagire con e modificare il contenuto dell&#39;SPA in AEM come sono abituati.

## Migrazione di SPA esistenti a AEM {#migrating-existing-spas-to-aem}

In genere, se l&#39;SPA segue i principi di sviluppo dell&#39; [SPA per AEM](#spa-development-principles-for-aem), l&#39;SPA lavorerà in AEM e sarà modificabile utilizzando AEM SPA Editor.

Seguite questi passaggi per rendere l&#39;SPA esistente pronto a funzionare con AEM.

1. **I componenti JS sono modulari.** - Renderli in grado di essere sottoposti a rendering in qualsiasi ordine, posizione e dimensione.
1. **Utilizza i contenitori forniti dal nostro SDK per inserire i componenti sullo schermo.** - AEM fornisce un componente per il sistema di paragrafi e pagine da usare.
1. **Create un componente AEM per ciascun componente JS.** - I componenti AEM definiscono la finestra di dialogo e l&#39;output JSON.

## Istruzioni per gli sviluppatori front-end {#instructions-for-front-end-developers}

Il compito principale di coinvolgere uno sviluppatore front-end nella creazione di un&#39;app per AEM è quello di concordare i componenti e i relativi modelli JSON.

Di seguito viene illustrato i passi che uno sviluppatore front-end deve seguire nello sviluppo di un&#39;app per AEM.

1. **Concordare sui componenti e il relativo modello JSON**

   Gli sviluppatori front-end e gli sviluppatori AEM back-end devono concordare su quali componenti sono necessari e un modello, per cui esiste una corrispondenza uno-a-uno tra i componenti SPA e i componenti back-end.

   AEM componenti sono ancora necessari principalmente per fornire finestre di dialogo di modifica ed esportare il modello di componente.

1. **In React components, accedere al modello tramite`this.props.cqModel`**

   Una volta che i componenti sono concordati e il modello JSON è in atto, lo sviluppatore front-end è libero di sviluppare l&#39;SPA e può semplicemente accedere al modello JSON tramite `this.props.cqModel`.

1. **Implementare il metodo del`render()`componente**

   Lo sviluppatore front-end implementa il `render()` metodo nel modo desiderato e può utilizzare i campi della `cqModel` proprietà. Questo produce il DOM e i frammenti HTML che verranno inseriti nella pagina. Questo è il modo standard per creare un&#39;app in React.

1. **Mappa il componente sul tipo di risorsa AEM tramite`MapTo()`**

   La mappatura memorizza le classi di componenti e viene utilizzata internamente dal `Container` componente fornito per recuperare e creare in modo dinamico le istanze dei componenti in base al tipo di risorsa specificato.

   Questo serve come &quot;colla&quot; tra front-end e back-end in modo che l&#39;editor sappia quali componenti corrispondono.

   Gli esempi `Page` e `ResponsiveGrid` sono buoni di classi che estendono la base `Container`.

1. **Definite il componente come`EditConfig`parametro in`MapTo()`**

   Questo parametro è necessario per indicare all’editor in che modo il componente deve essere nominato fino a quando non viene ancora eseguito il rendering o non ha contenuto da riprodurre.

1. **Estende la`Container`classe fornita per pagine e contenitori**

   Le pagine e i sistemi paragrafo devono estendere questa classe in modo che la delega ai componenti interni funzioni come previsto.

1. **Implementate una soluzione di routing che utilizza l’`History`API HTML5.**

   Quando `ModelRouter` è abilitata, la chiamata delle funzioni `pushState` e `replaceState` attiverà una richiesta `PageModelManager` per recuperare un frammento mancante del modello.

   La versione corrente dell&#39; `ModelRouter` unico supporto per l&#39;uso di URL che puntano al percorso effettivo delle risorse dei punti di ingresso del modello Sling. Non supporta l’uso di URL personalizzati o alias.

   È `ModelRouter` possibile disabilitare o configurare in modo da ignorare un elenco di espressioni regolari.

## AEM-Agnostico {#aem-agnostic}

Questi blocchi di codice illustrano come i componenti React e Angular non necessitano di elementi specifici per  Adobe o AEM.

* Tutto ciò che si trova all&#39;interno del componente JavaScript è AEMagnostico.
* Ciò che è specifico di AEM è che il componente JS deve essere mappato a un componente AEM con l’helper MapTo.

![Approccio Agnostico AEM](assets/aem-agnostic.png)

L&#39; `MapTo` aiutante è la &quot;colla&quot; che permette di combinare i componenti back-end e front-end:

* Indica al contenitore JS (o al sistema di paragrafi JS) quale componente JS è responsabile per il rendering di ciascuno dei componenti presenti nel JSON.
* Aggiunge all’HTML un attributo di dati HTML di cui il componente JS esegue il rendering, in modo che l’editor SPA sappia quale finestra di dialogo visualizzare all’autore quando modifica il componente.

Per ulteriori informazioni sull’utilizzo `MapTo` e la creazione di app per AEM in generale, consulta la Guida introduttiva per il framework scelto.

* [Guida introduttiva alle app SPA in AEM Utilizzo di React](getting-started-react.md)
* [Guida introduttiva alle app SPA in AEM Utilizzo di Angular](getting-started-angular.md)

## Architettura AEM e SPA {#aem-architecture-and-spas}

L’architettura generale di AEM, inclusi gli ambienti di sviluppo, creazione e pubblicazione, non cambia quando si utilizzano gli ZPS. Tuttavia, è utile comprendere in che modo lo sviluppo SPA si inserisce in questa architettura.

![Architettura AEM e SPA](assets/aem-architecture.png)

* **Ambiente di generazione**

   Qui si trova l&#39;origine dell&#39;applicazione SPA e l&#39;origine del componente.

   * Il generatore clientlib NPM crea una libreria client dal progetto SPA.
   * Tale libreria verrà scattata da Maven e distribuita dal plug-in Maven Build insieme al componente in AEM Author.

* **AEM Author**

   Il contenuto viene creato sull’autore AEM, inclusi gli SPA di authoring.

   Quando si modifica un&#39;app SPA utilizzando l&#39;editor SPA nell&#39;ambiente di authoring:

   1. SPA richiede l’HTML esterno.
   1. Il CSS viene caricato.
   1. Viene caricato il codice JavaScript dell’applicazione SPA.
   1. Quando l&#39;applicazione SPA viene eseguita, viene richiesto l&#39;JSON, che consente all&#39;app di creare il DOM della pagina, inclusi gli `cq-data` attributi.
   1. Questi `cq-data` attributi consentono all’editor di caricare informazioni aggiuntive sulla pagina, in modo da sapere quali configurazioni di modifica sono disponibili per i componenti.

* **AEM Publish**

   Qui vengono pubblicati per l’uso pubblico i contenuti creati e le librerie compilate, inclusi gli artefatti dell’applicazione SPA, i clientlibs e i componenti.

* **Dispatcher/CDN**

   Il dispatcher funge da livello di caching dei AEM per i visitatori del sito.
   * Le richieste vengono elaborate in modo simile a come si trovano in AEM Author, ma non vi sono richieste di informazioni sulla pagina, poiché ciò è necessario solo per l&#39;editor.
   * Javascript, CSS, JSON e HTML sono memorizzati nella cache, ottimizzando la pagina per una distribuzione rapida.

>[!NOTE]
>
>All&#39;interno AEM non è necessario eseguire meccanismi di creazione Javascript o eseguire lo stesso Javascript. AEM ospita solo gli artifact compilati dall&#39;applicazione SPA.

## Passaggi successivi {#next-steps}

* [La Guida introduttiva alle app SPA in AEM con React](getting-started-react.md) mostra come è stata creata una piattaforma SPA di base per lavorare con l&#39;editor SPA in AEM utilizzando React.
* [Guida introduttiva alle app SPA in AEM con Angular](getting-started-angular.md) mostra come è stata creata una piattaforma SPA di base per lavorare con l&#39;editor SPA in AEM con Angular.
* [SPA Editor Overview](editor-overview.md) approfondisce il modello di comunicazione tra AEM e SPA.
* [WKND SPA Project](wknd-tutorial.md) è un&#39;esercitazione passo-passo che implementa un semplice progetto SPA in AEM.
* [La mappatura da modello dinamico a componente per gli SPA](model-to-component-mapping.md) spiega il modello dinamico alla mappatura dei componenti e come funziona all&#39;interno degli SPA in AEM.
* [SPA Blueprint](blueprint.md) offre informazioni approfondite sul funzionamento di SPA SDK per AEM nel caso in cui desideri implementare SPA in AEM per un framework diverso da React o Angular o desideri semplicemente una comprensione più approfondita.
