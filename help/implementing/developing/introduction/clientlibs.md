---
title: Utilizzo di librerie lato client su AEM come Cloud Service
description: AEM fornisce Cartelle libreria lato client, che ti consentono di memorizzare il codice lato client (clientlibs) nell’archivio, organizzarlo in categorie e definire quando e come ogni categoria di codice deve essere distribuita al client
exl-id: 370db625-09bf-43fb-919d-4699edaac7c8
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '2561'
ht-degree: 0%

---

# Utilizzo di librerie lato client su AEM come Cloud Service {#using-client-side-libraries}

Le esperienze digitali si basano fortemente sull’elaborazione lato client basata su codice JavaScript e CSS complessi. AEM librerie lato client (clientlibs) consentono di organizzare e archiviare centralmente queste librerie lato client all’interno dell’archivio. Insieme al processo di creazione front-end [nell&#39;archetipo di progetto AEM, la gestione del codice front-end per il progetto AEM diventa semplice.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)

I vantaggi dell&#39;utilizzo di clientlibs in AEM includono:

* Il codice lato client viene memorizzato nell&#39;archivio come tutti gli altri codici e contenuti dell&#39;applicazione
* Le clientlibs in AEM possono aggregare tutti i CSS e JS in un unico file
* Esporre clientlib tramite un percorso accessibile tramite il [dispatcher](/help/implementing/dispatcher/disp-overview.md)
* Consente la riscrittura dei percorsi dei file o delle immagini di riferimento

Clientlibs è la soluzione incorporata per la distribuzione di CSS e Javascript da AEM.

>[!TIP]
>
>Anche gli sviluppatori front-end che creano CSS e JavaScript per progetti AEM devono acquisire familiarità con [AEM Project Archetype e il relativo processo di creazione front-end automatizzato.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)

## Cosa sono le librerie lato client {#what-are-clientlibs}

I siti richiedono JavaScript e CSS, nonché risorse statiche come icone e font web da elaborare lato client. Una clientlib è AEM meccanismo di riferimento (se necessario per categoria) e di distribuzione di tali risorse.

AEM raccoglie i CSS e JavaScript del sito in un singolo file, in una posizione centrale, per garantire che nell’output HTML sia inclusa una sola copia di qualsiasi risorsa. Questo ottimizza l&#39;efficienza della distribuzione e consente di mantenere tali risorse a livello centrale nell&#39;archivio tramite proxy, mantenendo l&#39;accesso sicuro.

## Sviluppo front-end per AEM come Cloud Service {#fed-for-aemaacs}

Tutti i file JavaScript, CSS e altre risorse front-end devono essere mantenuti nel modulo [ui.frontend dell’Archetipo di progetto AEM.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) La flessibilità dell’archetipo ti consente di utilizzare i tuoi moderni strumenti web di scelta per creare e gestire queste risorse.

L’archetipo può quindi compilare le risorse in file CSS e JS singoli, incorporandole automaticamente in un `cq:clientLibraryFolder` nell’archivio.

## Struttura delle cartelle lato client {#clientlib-folders}

Una cartella di libreria lato client è un nodo di archivio di tipo `cq:ClientLibraryFolder`. La sua definizione in [notazione CND](https://jackrabbit.apache.org/node-type-notation.html) è

```text
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

* `cq:ClientLibraryFolder` i nodi possono essere posizionati in qualsiasi punto all’interno della  `/apps` sottostruttura dell’archivio.
* Utilizza la proprietà `categories` del nodo per identificare le categorie della libreria a cui appartiene.

Ogni `cq:ClientLibraryFolder` viene popolato con un set di file JS e/o CSS, insieme ad alcuni file di supporto (vedi di seguito). Le proprietà importanti di `cq:ClientLibraryFolder` sono configurate come segue:

* `allowProxy`: Poiché tutte le clientlibs devono essere memorizzate in  `apps`, questa proprietà consente l&#39;accesso alle clientlibrerie tramite il servlet proxy. Consultare [Individuazione di una cartella della libreria client e Utilizzo del servlet delle librerie client proxy](#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) di seguito.
* `categories`: Identifica le categorie in cui il set di file JS e/o CSS entro questo  `cq:ClientLibraryFolder` autunno. La proprietà `categories`, con più valori, consente a una cartella di libreria di far parte di più di una categoria (consulta di seguito per informazioni su come ciò possa essere utile).

Se la cartella della libreria client contiene uno o più file di origine che, in fase di runtime, vengono uniti in un singolo file JS e/o CSS. Il nome del file generato è il nome del nodo con l&#39;estensione del nome file `.js` o `.css`. Ad esempio, il nodo della libreria denominato `cq.jquery` restituisce il file generato denominato `cq.jquery.js` o `cq.jquery.css`.

Le cartelle della libreria client contengono i seguenti elementi:

* File sorgente JS e/o CSS
* Risorse statiche che supportano gli stili CSS, ad esempio icone, font web e così via
* Un file `js.txt` e/o un file `css.txt` che identificano i file di origine da unire nei file JS e/o CSS generati

![Architettura clientlib](assets/clientlib-architecture.drawio.png)

## Creazione di cartelle della libreria lato client {#creating-clientlib-folders}

Le librerie client devono trovarsi in `/apps`. Questo per isolare meglio il codice dal contenuto e dalla configurazione.

Affinché le librerie client sotto `/apps` siano accessibili, viene utilizzato un servlet proxy. Le ACL sono ancora applicate nella cartella della libreria client, ma il servlet consente la lettura del contenuto tramite `/etc.clientlibs/` se la proprietà `allowProxy` è impostata su `true`.

1. Apri CRXDE Lite in un browser Web (`https://<host>:<port>/crx/de`).
1. Seleziona la cartella `/apps` e fai clic su **Crea > Crea nodo**.
1. Immettere un nome per la cartella della libreria e selezionare **Tipo** nell&#39;elenco `cq:ClientLibraryFolder`. Fare clic su **OK**, quindi fare clic su **Salva tutto**.
1. Per specificare la categoria o le categorie a cui appartiene la libreria, selezionare il nodo `cq:ClientLibraryFolder`, aggiungere la seguente proprietà, quindi fare clic su **Salva tutto**:
   * Nome: `categories`
   * Tipo: Stringa
   * Valore: Nome della categoria
   * Multi: Selezionati
1. Affinché le librerie client siano accessibili tramite proxy in `/etc.clientlibs`, seleziona il nodo `cq:ClientLibraryFolder`, aggiungi la seguente proprietà, quindi fai clic su **Salva tutto**:
   * Nome: `allowProxy`
   * Tipo: booleano
   * Valore: `true`
1. Per gestire le risorse statiche, crea una sottocartella denominata `resources` sotto la cartella della libreria client.
   * Se si memorizzano risorse statiche nella cartella `resources`, non è possibile fare riferimento a tali risorse in un&#39;istanza di pubblicazione.
1. Aggiungi i file di origine alla cartella della libreria.
   * Questa operazione viene generalmente eseguita dal processo di compilazione front-end di [AEM Project Archetype.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)
   * Se necessario, è possibile organizzare i file di origine in sottocartelle.
1. Seleziona la cartella della libreria client e fai clic su **Crea > Crea file**.
1. Nella casella Nome file digitare uno dei seguenti nomi di file e fare clic su OK:
   * **`js.txt`:** Usa questo nome file per generare un file JavaScript.
   * **`css.txt`:** Usa questo nome file per generare un foglio di stile a cascata.
1. Apri il file e digita il seguente testo per identificare la radice del percorso dei file di origine:
   * `#base=*[root]*`
   * Sostituisci `[root]` con il percorso della cartella che contiene i file di origine, relativo al file TXT. Ad esempio, utilizzare il testo seguente quando i file di origine si trovano nella stessa cartella del file TXT:
      * `#base=.`
   * Il codice seguente imposta la radice come cartella denominata mobile sotto il nodo `cq:ClientLibraryFolder` :
      * `#base=mobile`
1. Sulle righe seguenti `#base=[root]`, digita i percorsi dei file di origine relativi alla radice. Posizionare ogni nome di file su una riga separata.
1. Fare clic su **Salva tutto**.

## Server delle librerie lato client {#serving-clientlibs}

Una volta che la cartella della libreria client è [configurata come necessario,](#creating-clientlib-folders) le clientlibs possono essere richieste tramite proxy. Ad esempio:

* Hai una clientlib in `/apps/myproject/clientlibs/foo`
* Hai un’immagine statica in `/apps/myprojects/clientlibs/foo/resources/icon.png`

La proprietà `allowProxy` ti consente di richiedere:

* clientlib tramite j`/etc.clientlibs/myprojects/clientlibs/foo.js`
* Immagine statica tramite `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

### Caricamento delle librerie client tramite HTL {#loading-via-htl}

Una volta archiviate e gestite correttamente le clientlibs nella cartella della libreria client, è possibile accedervi tramite HTL.

Le librerie client vengono caricate tramite un modello di supporto fornito da AEM, accessibile tramite `data-sly-use`. In questo file sono disponibili modelli helper, che possono essere richiamati tramite `data-sly-call`.

Ogni modello di supporto richiede un&#39;opzione `categories` per fare riferimento alle librerie client desiderate. Tale opzione può essere una matrice di valori stringa o una stringa contenente un elenco di valori separati da virgola.

[Per ulteriori informazioni sul caricamento di clientlibs tramite HTL, consulta la ](https://experienceleague.adobe.com/docs/experience-manager-htl/using/getting-started/getting-started.html#loading-client-libraries) documentazione HTL .

<!--
### Setting Cache Timestamps {#setting-cache-timestamps}

This is possible. Still need detail.
-->

## Librerie client in modalità Autore e pubblicazione {#clientlibs-author-publish}

La maggior parte dei clientlibs sarà necessaria sull&#39;istanza di pubblicazione AEM. In altre parole, lo scopo della maggior parte dei clientlibs è quello di produrre l&#39;esperienza dell&#39;utente finale del contenuto. Per le clientlibs sulle istanze di pubblicazione, [strumenti di compilazione front-end](#fed-for-aemaacs) possono essere utilizzati e distribuiti tramite [cartelle di libreria client come descritto sopra.](#creating-clientlib-folders)

In alcuni casi, tuttavia, le librerie client potrebbero essere necessarie per personalizzare l’esperienza di authoring. Ad esempio, per personalizzare una finestra di dialogo potrebbe essere necessario distribuire piccoli bit di CSS o JS nell’istanza di authoring AEM.

### Gestione delle librerie client sull&#39;autore {#clientlibs-on-author}

Se devi utilizzare le librerie client sull&#39;autore, puoi creare le librerie client in `/apps` utilizzando gli stessi metodi di pubblicazione, ma scriverle direttamente in `/apps/.../clientlibs/foo` invece di creare un intero progetto per gestirlo.

Puoi quindi eseguire l’&quot;hook&quot; nel JS di authoring aggiungendo le librerie client a una categoria preconfigurata della libreria client.

## Strumenti di debug {#debugging-tools}

AEM fornisce diversi strumenti per il debug e il test delle cartelle della libreria client.

### Scopri le librerie client {#discover-client-libraries}

Il componente `/libs/cq/granite/components/dumplibs/dumplibs` genera una pagina di informazioni su tutte le cartelle della libreria client sul sistema. Il nodo `/libs/granite/ui/content/dumplibs` ha il componente come tipo di risorsa. Per aprire la pagina, utilizza il seguente URL (modificando l’host e la porta come richiesto):

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

Le informazioni includono il percorso e il tipo della libreria (CSS o JS) e i valori degli attributi della libreria, ad esempio categorie e dipendenze. Le tabelle successive nella pagina mostrano le librerie in ogni categoria e canale.

### Vedere Output generato {#see-generated-output}

Il componente `dumplibs` include un selettore di test che visualizza il codice sorgente generato per i tag `ui:includeClientLib` . La pagina include il codice per diverse combinazioni di attributi js, css e a tema.

1. Utilizza uno dei metodi seguenti per aprire la pagina Test output:
   * Dalla pagina `dumplibs.html`, fai clic sul collegamento nel testo **Fai clic qui per il test dell&#39;output**.
   * Apri il seguente URL nel browser Web (utilizza un host e una porta diversi come richiesto):
      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`
   * La pagina predefinita mostra l’output per i tag senza valore per l’attributo categories.
1. Per visualizzare l&#39;output di una categoria, digitare il valore della proprietà `categories` della libreria client e fare clic su **Invia query**.

## Funzionalità aggiuntive della cartella della libreria client {#additional-features}

Sono disponibili numerose altre funzioni supportate dalle cartelle della libreria client in AEM. Tuttavia, tali requisiti non sono richiesti in AEM come Cloud Service e come tale il loro uso è scoraggiato. Sono elencati qui per completezza.

>[!WARNING]
>
>Queste funzionalità aggiuntive delle cartelle della libreria client non sono necessarie in AEM come Cloud Service e pertanto il loro utilizzo è scoraggiato. Sono elencati qui per completezza.

### Adobe Granite HTML Library Manager {#html-library-manager}

È possibile controllare altre impostazioni della libreria client tramite il pannello **Adobe Granite HTML Library Manager** della console di sistema all&#39;indirizzo `https://<host>:<port>/system/console/configMgr`).

### Proprietà cartella aggiuntive {#additional-folder-properties}

Ulteriori proprietà della cartella includono consentire il controllo di dipendenze e incorporamenti, ma in genere non sono più necessarie e il loro utilizzo non è consigliato:

* `dependencies`: Elenco di altre categorie della libreria client da cui dipende la cartella della libreria. Ad esempio, se due `cq:ClientLibraryFolder` nodi `F` e `G` richiedono un altro file in `F` per funzionare correttamente, almeno uno dei `categories` di `G` deve essere compreso tra `dependencies` di `F`.`G`
* `embed`: Utilizzato per incorporare il codice da altre librerie. Se il nodo `F` incorpora i nodi `G` e `H`, l’HTML risultante sarà una concatenazione di contenuto dai nodi `G` e `H`.

### Collegamento a dipendenze {#linking-to-dependencies}

Quando il codice nella cartella della libreria client fa riferimento ad altre librerie, identifica le altre librerie come dipendenze. Il tag `ui:includeClientLib` che fa riferimento alla cartella della libreria client fa sì che il codice HTML includa un collegamento al file della libreria generato e alle dipendenze.

Le dipendenze devono essere un&#39;altra `cq:ClientLibraryFolder`. Per identificare le dipendenze, aggiungi una proprietà al nodo `cq:ClientLibraryFolder` con i seguenti attributi:

* **Nome:** dipendenze
* **Tipo:** String[]
* **Valori:** il valore della proprietà categories del nodo cq:ClientLibraryFolder da cui dipende la cartella libreria corrente.

Ad esempio, la `/etc/clientlibs/myclientlibs/publicmain` ha una dipendenza dalla libreria `cq.jquery`. La pagina che fa riferimento alla libreria client principale genera codice HTML che include il seguente codice:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### Incorporazione di codice da altre librerie {#embedding-code-from-other-libraries}

Puoi incorporare il codice da una libreria client in un&#39;altra libreria client. In fase di runtime, i file JS e CSS generati dalla libreria di incorporamento includono il codice della libreria incorporata.

L&#39;incorporamento del codice è utile per fornire l&#39;accesso alle librerie memorizzate nelle aree protette dell&#39;archivio.

#### Cartelle della libreria client specifiche per l’app {#app-specific-client-library-folders}

È consigliabile mantenere tutti i file relativi all’applicazione nella cartella dell’applicazione sotto `/app`. È inoltre consigliabile negare l’accesso alla cartella `/app` ai visitatori del sito web. Per soddisfare entrambe le best practice, crea una cartella della libreria client sotto la cartella `/etc` che incorpora la libreria client sottostante `/app`.

Utilizzare la proprietà categories per identificare la cartella della libreria client da incorporare. Per incorporare la libreria, aggiungi una proprietà al nodo di incorporamento `cq:ClientLibraryFolder` utilizzando i seguenti attributi di proprietà:

* **Nome:** incorporato
* **Tipo:** String[]
* **Valore:** il valore della proprietà categories del  `cq:ClientLibraryFolder` nodo da incorporare.

#### Utilizzo dell’incorporamento per ridurre al minimo le richieste {#using-embedding-to-minimize-requests}

In alcuni casi, potresti riscontrare che l’HTML finale generato per la pagina tipica dall’istanza di pubblicazione include un numero relativamente elevato di elementi `<script>`.

In questi casi, può essere utile combinare tutto il codice della libreria client richiesto in a un singolo file in modo che il numero di richieste avanti e indietro al caricamento della pagina venga ridotto. A questo scopo, puoi `embed` inserire le librerie richieste nella libreria client specifica dell’app utilizzando la proprietà embed del nodo `cq:ClientLibraryFolder` .

#### Percorsi nei file CSS {#paths-in-css-files}

Quando incorpori file CSS, il codice CSS generato utilizza percorsi verso risorse relative alla libreria di incorporamento. Ad esempio, la libreria accessibile al pubblico `/etc/client/libraries/myclientlibs/publicmain` incorpora la libreria client `/apps/myapp/clientlib`:

Il file `main.css` contiene il seguente stile:

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

Il file CSS generato dal nodo `publicmain` contiene il seguente stile, utilizzando l&#39;URL dell&#39;immagine originale:

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

#### Vedere File incorporati nell&#39;output HTML {#see-embedded-files}

Per tracciare l&#39;origine del codice incorporato o per garantire che le librerie client incorporate producano i risultati previsti, puoi vedere i nomi dei file che vengono incorporati in fase di esecuzione. Per visualizzare i nomi dei file, aggiungi il parametro `debugClientLibs=true` all’URL della pagina web. La libreria generata contiene istruzioni `@import` invece del codice incorporato.

Nell&#39;esempio della precedente sezione [Incorporamento di codice da altre librerie](#embedding-code-from-other-libraries), la cartella della libreria client `/etc/client/libraries/myclientlibs/publicmain` incorpora la cartella della libreria client `/apps/myapp/clientlib`. L&#39;aggiunta del parametro alla pagina web produce il seguente collegamento nel codice sorgente della pagina web:

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

Quando si apre il file `publicmain.css` viene visualizzato il seguente codice:

```javascript
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. Nella casella dell’indirizzo del browser web, aggiungi il seguente testo all’URL del codice HTML:
   * `?debugClientLibs=true`
1. Quando la pagina viene caricata, visualizza l&#39;origine della pagina.
1. Fare clic sul collegamento fornito come href per l&#39;elemento di collegamento per aprire il file e visualizzare il codice sorgente.

### Utilizzo dei preprocessori {#using-preprocessors}

AEM consente preprocessori inseribili e viene fornito il supporto per [YUI Compressor](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) per CSS e JavaScript e [Google Closure Compiler (GCC)](https://developers.google.com/closure/compiler/) per JavaScript con YUI impostato come preprocessore predefinito AEM.

I preprocessori inseribili consentono un utilizzo flessibile, tra cui:

* Definizione di ScriptProcessors in grado di elaborare origini script
* I processori sono configurabili con le opzioni
* I processori possono essere utilizzati per la minimizzazione, ma anche per i casi non minimizzati
* clientlib può definire quale processore utilizzare

>[!NOTE]
>
>Per impostazione predefinita, AEM utilizza il compressore YUI. Per un elenco dei problemi noti, consulta la [documentazione GitHub del compressore YUI](https://github.com/yui/yuicompressor/issues) . Il passaggio al compressore GCC per particolari clientlibs può risolvere alcuni problemi osservati quando si utilizza YUI.

>[!CAUTION]
>
>Non inserire una libreria minimizzata in una libreria client. Fornisci invece la libreria non elaborata e, se è necessaria la minimizzazione, utilizza le opzioni dei preprocessori.

#### Utilizzo {#usage}

Puoi scegliere di configurare la configurazione dei preprocessori per clientlibrary o a livello di sistema.

* Aggiungi le proprietà multivalore `cssProcessor` e `jsProcessor` sul nodo clientlibrary
* Oppure definisci la configurazione predefinita del sistema tramite la configurazione **HTML Library Manager** OSGi

Una configurazione preprocessore sul nodo clientlib ha la precedenza sulla configurazione OSGI.

#### Formato ed esempi {#format-and-examples}

##### Formato {#format}

```javascript
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

##### Compressore YUI per la minimizzazione CSS e GCC per JS {#yui-compressor-for-css-minification-and-gcc-for-js}

```javascript
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

##### Script per la preelaborazione e quindi GCC per minimizzare e offuscare {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

```javascript
jsProcessor: [
   "default:typescript",
   "min:typescript",
   "min:gcc;obfuscate=true"
]
```

##### Opzioni GCC aggiuntive {#additional-gcc-options}

```javascript
failOnWarning (defaults to "false")
languageIn (defaults to "ECMASCRIPT5")
languageOut (defaults to "ECMASCRIPT5")
compilationLevel (defaults to "simple") (can be "whitespace", "simple", "advanced")
```

Per ulteriori dettagli sulle opzioni GCC, consulta la [documentazione GCC](https://developers.google.com/closure/compiler/docs/compilation_levels).

#### Imposta il minatore predefinito di sistema {#set-system-default-minifier}

YUI è impostato come minificatore predefinito in AEM. Per modificare questo valore in GCC, segui questi passaggi.

1. Vai a Apache Felix Config Manager in (`http://<host>:<portY/system/console/configMgr`)
1. Trova e modifica il **Adobe Granite HTML Library Manager**.
1. Abilita l&#39;opzione **Minify** (se non è già abilitata).
1. Imposta il valore **Configurazione predefinita processore JS** su `min:gcc`.
   * Le opzioni possono essere passate se separate da un punto e virgola, ad esempio `min:gcc;obfuscate=true`.
1. Fai clic su **Salva** per salvare le modifiche.
