---
title: Utilizzo delle librerie lato client su AEM as a Cloud Service
description: AEM fornisce cartelle della libreria lato client, che ti consentono di memorizzare il codice lato client (clientlibs) nell’archivio, organizzarlo in categorie e definire quando e come ogni categoria di codice deve essere trasmessa al client
exl-id: 370db625-09bf-43fb-919d-4699edaac7c8
feature: Developing
role: Admin, Architect, Developer
source-git-commit: da44719521546e81af60e4f8dd5452d83ff5e1e7
workflow-type: tm+mt
source-wordcount: '2422'
ht-degree: 1%

---


# Utilizzo delle librerie lato client su AEM as a Cloud Service {#using-client-side-libraries}

Le esperienze digitali si basano in larga misura sull’elaborazione lato client guidata da codice JavaScript e CSS complesso. Le librerie lato client di AEM (clientlibs) consentono di organizzare e archiviare centralmente queste librerie lato client all’interno dell’archivio. In combinazione con il [processo di sviluppo front-end nell&#39;archetipo del progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html?=it), la gestione del codice front-end per il progetto AEM diventa semplice.

I vantaggi dell’utilizzo di clientlibs in AEM includono:

* Il codice lato client viene memorizzato nell&#39;archivio come tutti gli altri codici e contenuti dell&#39;applicazione
* Clientlibs in AEM può aggregare tutti i file CSS e JS in un unico file
* Esporre clientlibs tramite un percorso accessibile tramite [dispatcher](/help/implementing/dispatcher/disp-overview.md)
* Consente la riscrittura dei percorsi per i file o le immagini di riferimento

Clientlibs è la soluzione integrata per la distribuzione di CSS e JavaScript da AEM.

>[!TIP]
>
>Anche gli sviluppatori front-end che creano CSS e JavaScript per progetti AEM devono acquisire familiarità con [Archetipo progetto AEM e il relativo processo di sviluppo front-end automatizzato](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html?=it).

## Cosa sono le librerie lato client {#what-are-clientlibs}

I siti richiedono l’elaborazione lato client di risorse JavaScript e CSS e statiche, come icone e font web. Una clientlib è il meccanismo di AEM per fare riferimento (se necessario per categoria) e fornire tali risorse.

AEM raccoglie i file CSS e JavaScript del sito in un unico file, in una posizione centrale, per garantire che nell’output di HTML venga inclusa una sola copia di qualsiasi risorsa. In questo modo si ottimizza l&#39;efficienza della distribuzione e si consente la gestione centralizzata di tali risorse nell&#39;archivio tramite proxy, mantenendo l&#39;accesso sicuro.

## Sviluppo front-end per AEM as a Cloud Service {#fed-for-aemaacs}

Tutte le risorse JavaScript, CSS e altre risorse front-end devono essere mantenute nel modulo [ui.frontend dell&#39;archetipo di progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html?=it). La flessibilità dell’archetipo consente di utilizzare i moderni strumenti web a tua scelta per creare e gestire tali risorse.

L&#39;archetipo può quindi compilare le risorse in singoli file CSS e JS, incorporandoli automaticamente in un `cq:clientLibraryFolder` nell&#39;archivio.

## Struttura delle cartelle della libreria lato client {#clientlib-folders}

Una cartella di libreria lato client è un nodo di repository di tipo `cq:ClientLibraryFolder`. La sua definizione nella [notazione CND](https://jackrabbit.apache.org/node-type-notation.html) è

```text
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

* I nodi `cq:ClientLibraryFolder` possono essere posizionati ovunque all&#39;interno della sottostruttura `/apps` dell&#39;archivio.
* Utilizzare la proprietà `categories` del nodo per identificare le categorie di libreria a cui appartiene.

Ogni `cq:ClientLibraryFolder` è compilato con un set di file JS e/o CSS, insieme ad alcuni file di supporto (vedi sotto). Le proprietà importanti di `cq:ClientLibraryFolder` sono configurate come segue:

* `allowProxy`: poiché tutte le clientlibs devono essere archiviate in `apps`, questa proprietà consente l&#39;accesso alle librerie client tramite il servlet proxy. Consulta la sezione [Individuazione di una cartella della libreria client e utilizzo del servlet delle librerie client proxy](#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) di seguito.
* `categories`: identifica le categorie in cui rientra il set di file JS e/o CSS in `cq:ClientLibraryFolder`. La proprietà `categories`, essendo multivalore, consente a una cartella di libreria di far parte di più di una categoria (vedere di seguito per informazioni sull&#39;utilità di questa proprietà).

Se la cartella della libreria client contiene uno o più file di origine che, in fase di esecuzione, vengono uniti in un singolo file JS e/o CSS. Il nome del file generato è il nome del nodo con estensione `.js` o `.css`. Ad esempio, il nodo della libreria denominato `cq.jquery` genera il file generato denominato `cq.jquery.js` o `cq.jquery.css`.

Le cartelle delle librerie client contengono i seguenti elementi:

* File sorgente JS e/o CSS
* Risorse statiche che supportano gli stili CSS, ad esempio icone, caratteri web e così via.
* Un file `js.txt` e/o un file `css.txt` che identificano i file di origine da unire nei file JS e/o CSS generati

![Architettura Clientlib](assets/clientlib-architecture.drawio.png)

## Creazione di cartelle di librerie lato client {#creating-clientlib-folders}

Le librerie client devono trovarsi in `/apps`. Questa regola è necessaria per isolare meglio il codice dal contenuto e dalla configurazione.

Per rendere accessibili le librerie client in `/apps`, viene utilizzato un servlet proxy. Gli ACL sono ancora applicati nella cartella della libreria client, ma il servlet consente la lettura del contenuto tramite `/etc.clientlibs/` se la proprietà `allowProxy` è impostata su `true`.

1. Aprire CRXDE Lite in un browser Web (`https://<host>:<port>/crx/de`).
1. Selezionare la cartella `/apps` e fare clic su **Crea > Crea nodo**.
1. Immettere un nome per la cartella della libreria e nell&#39;elenco **Tipo** selezionare `cq:ClientLibraryFolder`. Fare clic su **OK** e quindi su **Salva tutto**.
1. Per specificare la categoria o le categorie a cui appartiene la libreria, selezionare il nodo `cq:ClientLibraryFolder`, aggiungere la seguente proprietà e quindi fare clic su **Salva tutto**:
   * Nome: `categories`
   * Tipo: String
   * Valore: il nome della categoria
   * Multiplo: selezionato
1. Per rendere accessibili le librerie client tramite proxy in `/etc.clientlibs`, selezionare il nodo `cq:ClientLibraryFolder`, aggiungere la seguente proprietà e quindi fare clic su **Salva tutto**:
   * Nome: `allowProxy`
   * Tipo: booleano
   * Valore: `true`
1. Se è necessario gestire risorse statiche, creare una sottocartella denominata `resources` sotto la cartella della libreria client.
   * Se si archiviano risorse statiche in un punto qualsiasi diverso dalla cartella `resources`, non è possibile farvi riferimento in un&#39;istanza Publish.
1. Aggiungere i file di origine alla cartella della libreria.
   * Questa operazione viene in genere eseguita dal processo di compilazione front-end dell&#39;[Archetipo progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html?=it).
   * Se necessario, è possibile organizzare i file di origine in sottocartelle.
1. Selezionare la cartella della libreria client e fare clic su **Crea > Crea file**.
1. Nella casella Nome file digitare uno dei seguenti nomi di file e fare clic su OK:
   * **`js.txt`:** Utilizzare questo nome di file per generare un file JavaScript.
   * **`css.txt`:** Utilizzare questo nome di file per generare un foglio di stile CSS.
1. Apri il file e digita il testo seguente per identificare la directory principale del percorso dei file di origine:
   * `#base=*[root]*`
   * Sostituire `[root]` con il percorso della cartella che contiene i file di origine, relativo al file TXT. Ad esempio, utilizza il testo seguente quando i file di origine si trovano nella stessa cartella del file TXT:
      * `#base=.`
   * Il codice seguente imposta la radice come cartella denominata mobile sotto il nodo `cq:ClientLibraryFolder`:
      * `#base=mobile`
1. Nelle righe sottostanti `#base=[root]`, digitare i percorsi dei file di origine relativi alla radice. Posizionare ogni nome di file su una riga separata.
1. Fare clic su **Salva tutto**.

## Distribuzione di librerie lato client {#serving-clientlibs}

Una volta che la cartella della libreria client è [configurata come richiesta](#creating-clientlib-folders), è possibile richiedere clientlibs tramite proxy. Ad esempio:

* Hai una libreria client in `/apps/myproject/clientlibs/foo`
* È presente un&#39;immagine statica in `/apps/myprojects/clientlibs/foo/resources/icon.png`

La proprietà `allowProxy` consente di richiedere:

* clientlib tramite `/etc.clientlibs/myprojects/clientlibs/foo.js`
* Immagine statica tramite `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

### Caricamento delle librerie client tramite HTL {#loading-via-htl}

Una volta memorizzate e gestite correttamente le clientlibs nella cartella della libreria client, è possibile accedervi tramite HTL.

Le librerie client vengono caricate tramite un modello helper fornito da AEM, accessibile tramite `data-sly-use`. In questo file sono disponibili modelli di supporto che possono essere richiamati tramite `data-sly-call`.

Ogni modello helper richiede un’opzione `categories` per fare riferimento alle librerie client desiderate. Tale opzione può essere un array di valori stringa o una stringa contenente un elenco di valori separati da virgola.

[Consulta la documentazione di HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/getting-started/getting-started.html#loading-client-libraries) per ulteriori dettagli sul caricamento di clientlibs tramite HTL.

<!--
### Setting Cache Timestamps {#setting-cache-timestamps}

This is possible. Still need detail.
-->

## Confronto tra le librerie client di Author e Publish {#clientlibs-author-publish}

La maggior parte delle clientlibs è richiesta nell’istanza AEM Publish. In altre parole, lo scopo della maggior parte delle clientlibs è quello di produrre l’esperienza dell’utente finale del contenuto. Per clientlibs nelle istanze di pubblicazione, è possibile utilizzare [strumenti di compilazione front-end](#fed-for-aemaacs) e distribuirli tramite [cartelle di librerie client come descritto in precedenza](#creating-clientlib-folders).

Tuttavia, in alcuni casi le librerie client possono essere necessarie per personalizzare l’esperienza di authoring. Ad esempio, per personalizzare una finestra di dialogo potrebbe essere necessario distribuire piccoli bit di CSS o JS nell’istanza di authoring di AEM.

### Gestione delle librerie client durante l’authoring {#clientlibs-on-author}

Se è necessario utilizzare le librerie client per l&#39;authoring, è possibile creare le librerie client in `/apps` utilizzando gli stessi metodi utilizzati per la pubblicazione, ma scriverle direttamente in `/apps/.../clientlibs/foo` anziché creare un intero progetto per gestirlo.

Puoi quindi effettuare l’hook in JS per l’authoring aggiungendo le librerie client a una categoria di librerie client preconfigurata.

## Strumenti di debug {#debugging-tools}

AEM fornisce diversi strumenti per il debug e il test delle cartelle delle librerie client.

### Scopri le librerie client {#discover-client-libraries}

Il componente `/libs/cq/granite/components/dumplibs/dumplibs` genera una pagina di informazioni su tutte le cartelle delle librerie client nel sistema. Il nodo `/libs/granite/ui/content/dumplibs` ha il componente come tipo di risorsa. Per aprire la pagina, utilizza il seguente URL (modificando l’host e la porta come richiesto):

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

Le informazioni includono il percorso e il tipo della libreria (CSS o JS) e i valori degli attributi della libreria, come categorie e dipendenze. Le tabelle successive nella pagina mostrano le librerie in ogni categoria e canale.

### Vedi Output generato {#see-generated-output}

Il componente `dumplibs` include un selettore di test che visualizza il codice sorgente generato per i tag `ui:includeClientLib`. La pagina include il codice per diverse combinazioni di attributi js, css e a tema.

1. Per aprire la pagina Output test, utilizzare uno dei metodi seguenti:
   * Dalla pagina `dumplibs.html`, fai clic sul collegamento nel testo **Fai clic qui per il test dell&#39;output**.
   * Apri il seguente URL nel browser web (utilizza un host e una porta diversi, a seconda delle necessità):
      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`
   * La pagina predefinita mostra l’output per i tag senza alcun valore per l’attributo categorie.
1. Per visualizzare l&#39;output di una categoria, digitare il valore della proprietà `categories` della libreria client e fare clic su **Invia query**.

## Caratteristiche aggiuntive della cartella della libreria client {#additional-features}

Esistono diverse altre funzioni supportate dalle cartelle delle librerie client in AEM. Tuttavia, questi non sono richiesti su AEM as a Cloud Service e come tali il loro utilizzo è sconsigliato. Sono elencati qui per completezza.

>[!WARNING]
>
>Queste funzioni aggiuntive delle cartelle delle librerie client non sono necessarie in AEM as a Cloud Service e pertanto il loro utilizzo è sconsigliato. Sono elencati qui per completezza.

### Adobe Granite HTML Libreria Manager {#html-library-manager}

È possibile controllare ulteriori impostazioni della libreria client tramite il pannello **Adobe Granite HTML Library Manager** della console di sistema in `https://<host>:<port>/system/console/configMgr`).

### Proprietà cartella aggiuntive {#additional-folder-properties}

Altre proprietà della cartella includono consentono il controllo delle dipendenze e degli incorporamenti, ma in genere non sono più necessari e il loro utilizzo è sconsigliato:

* `dependencies`: questo è un elenco di altre categorie di librerie client da cui dipende la cartella della libreria. Ad esempio, dati due nodi `cq:ClientLibraryFolder` `F` e `G`, se un file in `F` richiede un altro file in `G` per funzionare correttamente, almeno uno dei `categories` di `G` deve essere tra i `dependencies` di `F`.
* `embed`: utilizzato per incorporare il codice da altre librerie. Se il nodo `F` incorpora i nodi `G` e `H`, il HTML risultante è una concatenazione di contenuto dai nodi `G` e `H`.

### Collegamento alle dipendenze {#linking-to-dependencies}

Quando il codice nella cartella della libreria client fa riferimento ad altre librerie, identifica le altre librerie come dipendenze. Il tag `ui:includeClientLib` che fa riferimento alla cartella della libreria client fa in modo che il codice HTML includa un collegamento al file di libreria generato e alle dipendenze.

Le dipendenze devono essere un altro `cq:ClientLibraryFolder`. Per identificare le dipendenze, aggiungere una proprietà al nodo `cq:ClientLibraryFolder` con i seguenti attributi:

* **Nome:** dipendenze
* **Tipo:** Stringa[]
* **Valori:** il valore della proprietà Categories del nodo cq:ClientLibraryFolder da cui dipende la cartella della libreria corrente.

`/etc/clientlibs/myclientlibs/publicmain`, ad esempio, ha una dipendenza dalla libreria `cq.jquery`. La pagina che fa riferimento alla libreria client principale genera HTML che include il seguente codice:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### Incorporazione Di Codice Da Altre Librerie {#embedding-code-from-other-libraries}

Puoi incorporare il codice da una libreria client a un’altra libreria client. In fase di esecuzione, i file JS e CSS generati della libreria di incorporamento includono il codice della libreria incorporata.

L’incorporamento del codice è utile per fornire accesso alle librerie memorizzate in aree protette dell’archivio.

#### Cartelle Libreria Client Specifiche Per L&#39;App {#app-specific-client-library-folders}

È consigliabile mantenere tutti i file relativi all&#39;applicazione nella cartella dell&#39;applicazione al di sotto di `/apps`. È inoltre consigliabile negare l&#39;accesso alla cartella `/apps` ai visitatori del sito Web. Per soddisfare entrambe le best practice, crea una cartella della libreria client sotto la cartella `/etc` che incorpora la libreria client al di sotto di `/apps`.

Utilizzare la proprietà Categories per identificare la cartella della libreria client da incorporare. Per incorporare la libreria, aggiungere una proprietà al nodo `cq:ClientLibraryFolder` che incorpora, utilizzando i seguenti attributi di proprietà:

* **Nome:** incorporato
* **Tipo:** Stringa[]
* **Valore:** il valore della proprietà Categories del nodo `cq:ClientLibraryFolder` da incorporare.

#### Utilizzo dell’incorporamento per ridurre al minimo le richieste {#using-embedding-to-minimize-requests}

In alcuni casi è possibile che il HTML finale generato per la pagina tipica dall&#39;istanza Publish includa un numero relativamente elevato di `<script>` elementi.

In questi casi, può essere utile combinare in un unico file tutto il codice libreria client richiesto, in modo da ridurre il numero di richieste avanti e indietro al caricamento della pagina. A questo scopo, puoi `embed` le librerie richieste nella libreria client specifica per l&#39;app utilizzando la proprietà embed del nodo `cq:ClientLibraryFolder`.

#### Percorsi nei file CSS {#paths-in-css-files}

Quando incorpori file CSS, il codice CSS generato utilizza i percorsi delle risorse relativi alla libreria di incorporamento. Ad esempio, la libreria `/etc/client/libraries/myclientlibs/publicmain` accessibile al pubblico incorpora la libreria client `/apps/myapp/clientlib`:

Il file `main.css` contiene il seguente stile:

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

Il file CSS generato dal nodo `publicmain` contiene il seguente stile, che utilizza l&#39;URL dell&#39;immagine originale:

```javascript
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

#### Vedere File incorporati nell&#39;output di HTML {#see-embedded-files}

Per tracciare l’origine del codice incorporato o per garantire che le librerie client incorporate producano i risultati previsti, puoi visualizzare i nomi dei file incorporati in fase di esecuzione. Per visualizzare i nomi dei file, aggiungi il parametro `debugClientLibs=true` all&#39;URL della pagina Web. La libreria generata contiene `@import` istruzioni invece del codice incorporato.

Nell&#39;esempio della precedente sezione [Incorporazione di codice da altre librerie](#embedding-code-from-other-libraries), la cartella della libreria client `/etc/client/libraries/myclientlibs/publicmain` incorpora la cartella della libreria client `/apps/myapp/clientlib`. L’aggiunta del parametro alla pagina web genera il seguente collegamento nel codice sorgente della pagina web:

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

L&#39;apertura del file `publicmain.css` rivela il seguente codice:

```javascript
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. Nella casella dell’indirizzo del browser web, aggiungi il testo seguente all’URL del HTML:
   * `?debugClientLibs=true`
1. Al caricamento della pagina, visualizza l’origine della pagina.
1. Fai clic sul collegamento fornito come href per l’elemento collegamento per aprire il file e visualizzare il codice sorgente.

### Utilizzo dei preprocessori {#using-preprocessors}

AEM consente preprocessori collegabili e viene fornito con il supporto per [Compressore YUI](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) per CSS e JavaScript e [Compilatore di chiusura Google (GCC)](https://developers.google.com/closure/compiler/) per JavaScript con YUI impostato come preprocessore predefinito di AEM.

I preprocessori collegabili consentono un utilizzo flessibile, tra cui:

* Definizione di ScriptProcessors che possono elaborare origini script
* I processori sono configurabili con opzioni
* I processori possono essere utilizzati per la minimizzazione, ma anche per i casi non minimizzati
* La libreria client può definire quale processore utilizzare

>[!NOTE]
>
>Per impostazione predefinita, AEM utilizza il Compressore GCC per minimizzare JavaScript.

>[!CAUTION]
>
>Non inserire una libreria minimizzata in una libreria client. Fornisci invece la libreria raw e, se è richiesta la minimizzazione, utilizza le opzioni dei preprocessori.

#### Utilizzo {#usage}

È possibile scegliere di configurare la configurazione dei preprocessori per libreria client o a livello di sistema.

* Aggiungere le proprietà multivalore `cssProcessor` e `jsProcessor` nel nodo clientlibrary

La definizione della configurazione predefinita del sistema tramite la configurazione OSGi **HTML Library Manager** non è supportata. Si applica solo al SDK locale e non alle esecuzioni di pipeline full stack.

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
languageOut (defaults to "ECMASCRIPT_2018" as of release 21994, was previously "ECMASCRIPT5" )
compilationLevel (defaults to "simple") (can be "whitespace", "simple", "advanced")
```

Per ulteriori dettagli sulle opzioni GCC, vedi [documentazione GCC](https://developers.google.com/closure/compiler/docs/compilation_levels).

#### Imposta minimizzatore predefinito di sistema {#set-system-default-minifier}

L&#39;impostazione del minifier predefinito del sistema non è supportata in AEM as a Cloud Service.
