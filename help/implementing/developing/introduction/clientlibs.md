---
title: Utilizzo di librerie lato client su AEM as a Cloud Service
description: AEM fornisce cartelle di librerie lato client, che consentono di memorizzare il codice lato client (clientlibs) nell’archivio, organizzarlo in categorie e definire quando e come ogni categoria di codice deve essere trasmessa al client
exl-id: 370db625-09bf-43fb-919d-4699edaac7c8
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '2562'
ht-degree: 1%

---


# Utilizzo di librerie lato client su AEM as a Cloud Service {#using-client-side-libraries}

Le esperienze digitali si basano fortemente sull’elaborazione lato client guidata da codice JavaScript e CSS complesso. Le librerie lato client (clientlibs) dell’AEM consentono di organizzare e archiviare centralmente queste librerie lato client all’interno dell’archivio. Abbinato al [processo di sviluppo front-end nell’archetipo del progetto AEM,](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) la gestione del codice front-end per il progetto AEM diventa semplice.

I vantaggi dell’utilizzo di clientlibs in AEM includono:

* Il codice lato client viene memorizzato nell&#39;archivio come tutti gli altri codici e contenuti dell&#39;applicazione
* Clientlibs in AEM può aggregare tutti i file CSS e JS in un unico file
* Esporre clientlibs tramite un percorso accessibile tramite [dispatcher](/help/implementing/dispatcher/disp-overview.md)
* Consente la riscrittura dei percorsi per i file o le immagini di riferimento

Clientlibs è la soluzione integrata per la distribuzione di CSS e JavaScript dall’AEM.

>[!TIP]
>
>Anche gli sviluppatori front-end che creano CSS e JavaScript per progetti AEM devono familiarizzare con [AEM Project Archetype e il suo processo di sviluppo front-end automatizzato.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)

## Cosa sono le librerie lato client {#what-are-clientlibs}

I siti richiedono risorse JavaScript e CSS nonché risorse statiche come icone e font web da elaborare lato client. Una clientlib è un meccanismo AEM da utilizzare come riferimento (per categoria, se necessario) e al servizio di tali risorse.

AEM raccoglie i file CSS e JavaScript del sito in un singolo file, in una posizione centrale, per garantire che nell’output HTML venga inclusa una sola copia di qualsiasi risorsa. In questo modo si ottimizza l&#39;efficienza della distribuzione e si consente la gestione centralizzata di tali risorse nell&#39;archivio tramite proxy, mantenendo l&#39;accesso sicuro.

## Sviluppo front-end per AEM as a Cloud Service {#fed-for-aemaacs}

Tutte le risorse JavaScript, CSS e altre risorse front-end devono essere gestite nel [Modulo ui.frontend dell’Archetipo di progetto AEM.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) La flessibilità dell’archetipo consente di utilizzare i moderni strumenti web a tua scelta per creare e gestire tali risorse.

L’archetipo può quindi compilare le risorse in singoli file CSS e JS, incorporandoli automaticamente in un `cq:clientLibraryFolder` nell’archivio.

## Struttura delle cartelle della libreria lato client {#clientlib-folders}

Una cartella di libreria lato client è un nodo di archivio di tipo `cq:ClientLibraryFolder`. La sua definizione in [Notazione CND](https://jackrabbit.apache.org/node-type-notation.html) è

```text
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

* `cq:ClientLibraryFolder` I nodi possono essere posizionati ovunque all&#39;interno del `/apps` sottostruttura dell’archivio.
* Utilizza il `categories` del nodo per identificare le categorie di libreria a cui appartiene.

Ogni `cq:ClientLibraryFolder` viene compilato con un set di file JS e/o CSS, insieme ad alcuni file di supporto (vedi di seguito). Proprietà importanti del `cq:ClientLibraryFolder` sono configurate come segue:

* `allowProxy`: poiché tutte le clientlibs devono essere memorizzate in `apps`, questa proprietà consente l’accesso alle librerie client tramite il servlet proxy. Consulta la sezione [Individuazione di una cartella di librerie client e utilizzo del servlet delle librerie client proxy](#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) di seguito.
* `categories`: identifica le categorie in cui il set di file JS e/o CSS all’interno di questo `cq:ClientLibraryFolder` caduta. Il `categories` Poiché questa proprietà ha più valori, una cartella libreria può far parte di più categorie (vedi di seguito per informazioni su come può essere utile).

Se la cartella della libreria client contiene uno o più file di origine che, in fase di esecuzione, vengono uniti in un singolo file JS e/o CSS. Il nome del file generato è il nome del nodo con `.js` o `.css` estensione del nome file. Ad esempio, il nodo della libreria denominato `cq.jquery` restituisce il file generato denominato `cq.jquery.js` o `cq.jquery.css`.

Le cartelle delle librerie client contengono i seguenti elementi:

* File sorgente JS e/o CSS
* Risorse statiche che supportano gli stili CSS, ad esempio icone, font web e così via.
* Uno `js.txt` file e/o uno `css.txt` file che identifica i file sorgente da unire nei file JS e/o CSS generati

![Architettura Clientlib](assets/clientlib-architecture.drawio.png)

## Creazione di cartelle di librerie lato client {#creating-clientlib-folders}

Le librerie client devono trovarsi in `/apps`. Questa regola è necessaria per isolare meglio il codice dal contenuto e dalla configurazione.

Per le librerie client in `/apps` per essere accessibile, viene utilizzato un servlet proxy. Gli ACL vengono ancora applicati nella cartella della libreria client, ma il servlet consente la lettura del contenuto tramite `/etc.clientlibs/` se `allowProxy` proprietà impostata su `true`.

1. Apri CRXDE Lite in un browser Web (`https://<host>:<port>/crx/de`).
1. Seleziona la `/apps` cartella e fai clic su **Crea > Crea nodo**.
1. Immetti un nome per la cartella della libreria e nella **Tipo** selezione elenco `cq:ClientLibraryFolder`. Clic **OK** e quindi fare clic su **Salva tutto**.
1. Per specificare la categoria o le categorie a cui appartiene la libreria, seleziona la `cq:ClientLibraryFolder` , aggiungere la seguente proprietà e quindi fare clic su **Salva tutto**:
   * Nome: `categories`
   * Tipo: String
   * Valore: il nome della categoria
   * Multiplo: selezionato
1. Affinché le librerie client siano accessibili tramite proxy in `/etc.clientlibs`, seleziona la `cq:ClientLibraryFolder` , aggiungere la seguente proprietà e quindi fare clic su **Salva tutto**:
   * Nome: `allowProxy`
   * Tipo: booleano
   * Valore: `true`
1. Per gestire le risorse statiche, crea una sottocartella denominata `resources` nella cartella della libreria client.
   * Se archivi risorse statiche in un punto diverso da quello della cartella `resources`, non è possibile farvi riferimento in un’istanza di pubblicazione.
1. Aggiungere i file di origine alla cartella della libreria.
   * Questa operazione viene in genere eseguita dal processo di sviluppo front-end del [Archetipo progetto AEM.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html)
   * Se necessario, è possibile organizzare i file di origine in sottocartelle.
1. Seleziona la cartella della libreria client e fai clic su **Crea > Crea file**.
1. Nella casella Nome file digitare uno dei seguenti nomi di file e fare clic su OK:
   * **`js.txt`:** Utilizza questo nome di file per generare un file JavaScript.
   * **`css.txt`:** Utilizzate questo nome di file per generare un foglio di stile CSS.
1. Apri il file e digita il testo seguente per identificare la directory principale del percorso dei file di origine:
   * `#base=*[root]*`
   * Sostituisci `[root]` con il percorso della cartella che contiene i file di origine, relativo al file TXT. Ad esempio, utilizza il testo seguente quando i file di origine si trovano nella stessa cartella del file TXT:
      * `#base=.`
   * Il codice seguente imposta la radice come cartella denominata mobile sotto il `cq:ClientLibraryFolder` nodo:
      * `#base=mobile`
1. Sulle righe sottostanti `#base=[root]`, digitare i percorsi dei file di origine relativi alla directory principale. Posizionare ogni nome di file su una riga separata.
1. Clic **Salva tutto**.

## Distribuzione di librerie lato client {#serving-clientlibs}

Quando la cartella della libreria client è [configurate come richiesto,](#creating-clientlib-folders) le clientlibs possono essere richieste tramite proxy. Ad esempio:

* Hai una libreria client in `/apps/myproject/clientlibs/foo`
* Hai un’immagine statica in `/apps/myprojects/clientlibs/foo/resources/icon.png`

Il `allowProxy` La proprietà ti consente di richiedere:

* La libreria client tramite `/etc.clientlibs/myprojects/clientlibs/foo.js`
* L’immagine statica tramite `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

### Caricamento delle librerie client tramite HTL {#loading-via-htl}

Una volta memorizzate e gestite correttamente le clientlibs nella cartella della libreria client, è possibile accedervi tramite HTL.

Le librerie client vengono caricate tramite un modello helper fornito da AEM, a cui è possibile accedere tramite `data-sly-use`. In questo file sono disponibili modelli di supporto che possono essere richiamati tramite `data-sly-call`.

Ogni modello helper richiede un’opzione `categories` per fare riferimento alle librerie client desiderate. Tale opzione può essere una matrice di valori stringa o una stringa contenente un elenco di valori separati da virgola.

[Consulta la documentazione di HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/getting-started/getting-started.html#loading-client-libraries) per ulteriori dettagli sul caricamento di clientlibs tramite HTL.

<!--
### Setting Cache Timestamps {#setting-cache-timestamps}

This is possible. Still need detail.
-->

## Confronto tra le librerie client di Author e Publish {#clientlibs-author-publish}

La maggior parte delle clientlibs è richiesta nell’istanza di pubblicazione dell’AEM. In altre parole, lo scopo della maggior parte delle clientlibs è quello di produrre l’esperienza dell’utente finale del contenuto. Per clientlibs sulle istanze di pubblicazione, [strumenti di sviluppo front-end](#fed-for-aemaacs) utilizzabile e implementabile tramite [cartelle della libreria client come descritto in precedenza.](#creating-clientlib-folders)

Tuttavia, in alcuni casi le librerie client possono essere necessarie per personalizzare l’esperienza di authoring. Ad esempio, per personalizzare una finestra di dialogo potrebbe essere necessario distribuire piccoli bit di CSS o JS nell’istanza di authoring dell’AEM.

### Gestione delle librerie client durante l’authoring {#clientlibs-on-author}

Se devi utilizzare le librerie client durante l’authoring, puoi creare le librerie client in `/apps` utilizzando gli stessi metodi utilizzati per la pubblicazione, ma scrivila direttamente in `/apps/.../clientlibs/foo` invece di creare un intero progetto per gestirlo.

Puoi quindi effettuare l’hook in JS per l’authoring aggiungendo le librerie client a una categoria di librerie client preconfigurata.

## Strumenti di debug {#debugging-tools}

AEM fornisce diversi strumenti per il debug e il test delle cartelle delle librerie client.

### Scopri le librerie client {#discover-client-libraries}

Il `/libs/cq/granite/components/dumplibs/dumplibs` il componente genera una pagina di informazioni su tutte le cartelle delle librerie client sul sistema. Il `/libs/granite/ui/content/dumplibs` Il componente del nodo è un tipo di risorsa. Per aprire la pagina, utilizza il seguente URL (modificando l’host e la porta come richiesto):

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

Le informazioni includono il percorso e il tipo della libreria (CSS o JS) e i valori degli attributi della libreria, come categorie e dipendenze. Le tabelle successive nella pagina mostrano le librerie in ogni categoria e canale.

### Vedi Output generato {#see-generated-output}

Il `dumplibs` il componente include un selettore di test che visualizza il codice sorgente generato per `ui:includeClientLib` tag. La pagina include il codice per diverse combinazioni di attributi js, css e a tema.

1. Per aprire la pagina Output test, utilizzare uno dei metodi seguenti:
   * Dalla sezione `dumplibs.html` , fare clic sul collegamento nella **Fai clic qui per il test di output** testo.
   * Apri il seguente URL nel browser web (utilizza un host e una porta diversi, a seconda delle necessità):
      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`
   * La pagina predefinita mostra l’output per i tag senza alcun valore per l’attributo categorie.
1. Per visualizzare l’output di una categoria, digita il valore della proprietà `categories` e fai clic su **Invia query**.

## Caratteristiche aggiuntive della cartella della libreria client {#additional-features}

Esistono diverse altre funzioni supportate dalle cartelle delle librerie client in AEM. Tuttavia, questi non sono richiesti per AEM as a Cloud Service e come tale il loro uso è sconsigliato. Sono elencati qui per completezza.

>[!WARNING]
>
>Queste funzioni aggiuntive delle cartelle delle librerie client non sono necessarie per le AEM as a Cloud Service e pertanto il loro utilizzo è sconsigliato. Sono elencati qui per completezza.

### Adobe Granite HTML Libreria Manager {#html-library-manager}

È possibile controllare ulteriori impostazioni della libreria client tramite **Adobe Granite HTML Library Manager** della console del sistema in `https://<host>:<port>/system/console/configMgr`).

### Proprietà cartella aggiuntive {#additional-folder-properties}

Altre proprietà della cartella includono consentono il controllo delle dipendenze e degli incorporamenti, ma in genere non sono più necessari e il loro utilizzo è sconsigliato:

* `dependencies`: questo è un elenco di altre categorie di librerie client da cui dipende la cartella della libreria. Ad esempio, dato due `cq:ClientLibraryFolder` nodi `F` e `G`, se un file in `F` richiede un altro file in `G` per funzionare correttamente, almeno uno dei `categories` di `G` deve essere tra i `dependencies` di `F`.
* `embed`: utilizzato per incorporare il codice da altre librerie. Se nodo `F` incorpora nodi `G` e `H`, il HTML risultante è una concatenazione di contenuto dai nodi `G` e `H`.

### Collegamento alle dipendenze {#linking-to-dependencies}

Quando il codice nella cartella della libreria client fa riferimento ad altre librerie, identifica le altre librerie come dipendenze. Il `ui:includeClientLib` Se si utilizza un tag che fa riferimento alla cartella della libreria client, nel codice HTML verrà incluso un collegamento al file di libreria generato e alle dipendenze.

Le dipendenze devono essere un&#39;altra `cq:ClientLibraryFolder`. Per identificare le dipendenze, aggiungi una proprietà alla `cq:ClientLibraryFolder` con i seguenti attributi:

* **Nome:** dipendenze
* **Tipo:** Stringa[]
* **Valori:** Valore della proprietà Categories del nodo cq:ClientLibraryFolder da cui dipende la cartella della libreria corrente.

Ad esempio, il `/etc/clientlibs/myclientlibs/publicmain` ha una dipendenza da `cq.jquery` libreria. La pagina che fa riferimento alla libreria client principale genera HTML che include il seguente codice:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### Incorporazione Di Codice Da Altre Librerie {#embedding-code-from-other-libraries}

Puoi incorporare il codice da una libreria client a un’altra libreria client. In fase di esecuzione, i file JS e CSS generati della libreria di incorporamento includono il codice della libreria incorporata.

L’incorporamento del codice è utile per fornire accesso alle librerie memorizzate in aree protette dell’archivio.

#### Cartelle Libreria Client Specifiche Per L&#39;App {#app-specific-client-library-folders}

È consigliabile conservare tutti i file relativi all&#39;applicazione nella cartella dell&#39;applicazione sottostante `/apps`. È inoltre consigliabile negare l’accesso ai visitatori del sito web `/apps` cartella. Per soddisfare entrambe le best practice, crea una cartella della libreria client sotto al `/etc` cartella che incorpora la libreria client sottostante `/apps`.

Utilizzare la proprietà Categories per identificare la cartella della libreria client da incorporare. Per incorporare la libreria, aggiungi una proprietà all’incorporamento `cq:ClientLibraryFolder` utilizzando i seguenti attributi di proprietà:

* **Nome:** incorporare
* **Tipo:** Stringa[]
* **Valore:** Il valore della proprietà Categories della proprietà `cq:ClientLibraryFolder` nodo da incorporare.

#### Utilizzo dell’incorporamento per ridurre al minimo le richieste {#using-embedding-to-minimize-requests}

In alcuni casi è possibile che il HTML finale generato per la pagina tipica dall’istanza Publish includa un numero relativamente elevato di `<script>` elementi.

In questi casi, può essere utile combinare in un unico file tutto il codice libreria client richiesto, in modo da ridurre il numero di richieste avanti e indietro al caricamento della pagina. A tale scopo è possibile: `embed` le librerie richieste nella libreria client specifica per l’app utilizzando la proprietà embed di `cq:ClientLibraryFolder` nodo.

#### Percorsi nei file CSS {#paths-in-css-files}

Quando incorpori file CSS, il codice CSS generato utilizza i percorsi delle risorse relativi alla libreria di incorporamento. Ad esempio, la libreria accessibile al pubblico `/etc/client/libraries/myclientlibs/publicmain` incorpora il `/apps/myapp/clientlib` libreria client:

Il `main.css` Il file contiene il seguente stile:

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

Il file CSS che `publicmain` Il nodo genera contiene il seguente stile, utilizzando l’URL dell’immagine originale:

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

#### Vedi File incorporati nell’output di HTML {#see-embedded-files}

Per tracciare l’origine del codice incorporato o per garantire che le librerie client incorporate producano i risultati previsti, puoi visualizzare i nomi dei file incorporati in fase di esecuzione. Per visualizzare i nomi dei file, aggiungi `debugClientLibs=true` all’URL della pagina web. La libreria generata contiene `@import` al posto del codice incorporato.

Nell’esempio del precedente [Incorporazione Di Codice Da Altre Librerie](#embedding-code-from-other-libraries) sezione, il `/etc/client/libraries/myclientlibs/publicmain` la cartella della libreria client incorpora `/apps/myapp/clientlib` cartella della libreria client. L’aggiunta del parametro alla pagina web genera il seguente collegamento nel codice sorgente della pagina web:

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

Apertura di `publicmain.css` Il file mostra il seguente codice:

```javascript
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. Nella casella dell’indirizzo del browser web, aggiungi il testo seguente all’URL del tuo HTML:
   * `?debugClientLibs=true`
1. Al caricamento della pagina, visualizza l’origine della pagina.
1. Fai clic sul collegamento fornito come href per l’elemento collegamento per aprire il file e visualizzare il codice sorgente.

### Utilizzo dei preprocessori {#using-preprocessors}

L&#39;AEM consente preprocessori collegabili e viene fornito con supporto per [Compressore YUI](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) per CSS e JavaScript e [Compilatore di chiusura Google (GCC)](https://developers.google.com/closure/compiler/) per JavaScript con YUI impostato come preprocessore predefinito per AEM.

I preprocessori collegabili consentono un utilizzo flessibile, tra cui:

* Definizione di ScriptProcessors che possono elaborare origini script
* I processori sono configurabili con opzioni
* I processori possono essere utilizzati per la minimizzazione, ma anche per i casi non minimizzati
* La libreria client può definire quale processore utilizzare

>[!NOTE]
>
>Per impostazione predefinita, l’AEM utilizza il compressore YUI. Consulta la [Documentazione di GitHub per il compressore YUI](https://github.com/yui/yuicompressor/issues) per un elenco dei problemi noti. Il passaggio al compressore GCC per particolari clientlibs può risolvere alcuni problemi osservati durante l’utilizzo di YUI.

>[!CAUTION]
>
>Non inserire una libreria minimizzata in una libreria client. Fornisci invece la libreria raw e, se è richiesta la minimizzazione, utilizza le opzioni dei preprocessori.

#### Utilizzo {#usage}

È possibile scegliere di configurare la configurazione dei preprocessori per libreria client o a livello di sistema.

* Aggiungere le proprietà multivalore `cssProcessor` e `jsProcessor` sul nodo clientlibrary
* Oppure definisci la configurazione predefinita del sistema tramite **Gestione librerie HTML** Configurazione OSGi

Una configurazione del preprocessore sul nodo clientlib ha la precedenza sulla configurazione OSGI.

#### Formato ed esempi {#format-and-examples}

##### Formato {#format}

```javascript
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

##### Compressore YUI per minimizzazione CSS e GCC per JS {#yui-compressor-for-css-minification-and-gcc-for-js}

```javascript
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

##### Script da pre-elaborare e poi GCC da minimizzare e oscurare {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

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

Per maggiori dettagli sulle opzioni GCC, vedi [Documentazione GCC](https://developers.google.com/closure/compiler/docs/compilation_levels).

#### Imposta minimizzatore predefinito di sistema {#set-system-default-minifier}

YUI è impostato come minimizzatore predefinito in AEM. Per cambiare in GCC, segui la procedura riportata di seguito.

1. Vai a Apache Felix Config Manager all’indirizzo (`http://<host>:<portY/system/console/configMgr`)
1. Trova e modifica il **Adobe Granite HTML Library Manager**.
1. Abilita **Minimizza** (se non già abilitata).
1. Imposta il valore **Configurazioni predefinite processore JS** a `min:gcc`.
   * Le opzioni possono essere trasmesse se separate ad esempio da un punto e virgola, `min:gcc;obfuscate=true`.
1. Clic **Salva** per salvare le modifiche.
