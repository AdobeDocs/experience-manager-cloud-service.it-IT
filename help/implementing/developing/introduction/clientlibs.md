---
title: Utilizzo di librerie lato client su AEM come Cloud Service
description: AEM fornisce Cartelle libreria lato client che consentono di memorizzare il codice lato client (clientlibs) nell'archivio, organizzarlo in categorie e definire quando e come ciascuna categoria di codice deve essere distribuita al client
translation-type: tm+mt
source-git-commit: d4c031e17c0c83e44b687474502252c89ed37922
workflow-type: tm+mt
source-wordcount: '2571'
ht-degree: 1%

---


# Utilizzo di librerie lato client su AEM come Cloud Service {#using-client-side-libraries}

Le esperienze digitali dipendono in larga misura dall&#39;elaborazione sul lato client basata su codice JavaScript e CSS complessi. AEM Client-Side Libraries (clientlibs) consentono di organizzare e archiviare centralmente queste librerie lato client all&#39;interno dell&#39;archivio. Unita al processo di [build front-end nell&#39;archetipo AEM progetto, ](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/archetype/uifrontend.html) la gestione del codice front-end per il progetto AEM diventa semplice.

I vantaggi dell&#39;uso di clientlibes in AEM includono:

* Il codice lato client viene memorizzato nell&#39;archivio come tutti gli altri codici e contenuti dell&#39;applicazione
* Clientlibs in AEM può aggregare tutti i CSS e JS in un unico file
* Esposizione di clientlibs tramite un percorso accessibile tramite [dispatcher](/help/implementing/dispatcher/disp-overview.md)
* Consente la riscrittura dei percorsi per i file o le immagini di riferimento

Clientlibs è la soluzione integrata per la distribuzione di CSS e Javascript da AEM.

>[!TIP]
>
>Gli sviluppatori front-end che creano file CSS e Javascript per AEM progetti devono anche familiarizzare con il [AEM Project Archetype e con il suo processo automatizzato di build front-end.](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/uifrontend.html)

## Che cosa sono le librerie lato client {#what-are-clientlibs}

I siti richiedono l&#39;elaborazione di JavaScript e CSS e di risorse statiche come icone e font Web sul lato client. Una clientlib è AEM meccanismo di riferimento (se necessario per categoria) e di gestione di tali risorse.

AEM raccoglie i file CSS e Javascript del sito in un singolo file, in una posizione centrale, per garantire che solo una copia di qualsiasi risorsa sia inclusa nell&#39;output HTML. Questo ottimizza l&#39;efficienza della distribuzione e consente di mantenere le risorse a livello centrale nell&#39;archivio tramite proxy, garantendo la sicurezza dell&#39;accesso.

## Sviluppo front-end per AEM come Cloud Service {#fed-for-aemaacs}

Tutte le risorse front-end JavaScript, CSS e altre devono essere mantenute nel modulo [ui.frontend dell&#39;archivio AEM progetto.](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/uifrontend.html) La flessibilità di questo archetipo consente di utilizzare i moderni strumenti Web a scelta per creare e gestire queste risorse.

L&#39;archetype può quindi compilare le risorse in singoli file CSS e JS, incorporandoli automaticamente in un `cq:clientLibraryFolder` nella directory archivio.

## Struttura cartella libreria lato client {#clientlib-folders}

Una cartella libreria lato client è un nodo di repository di tipo `cq:ClientLibraryFolder`. La sua definizione in [notazione CND](https://jackrabbit.apache.org/node-type-notation.html) è

```text
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

* `cq:ClientLibraryFolder` i nodi possono essere posizionati ovunque all&#39;interno della  `/apps` sottostruttura dell&#39;archivio.
* Utilizzare la proprietà `categories` del nodo per identificare le categorie di libreria alle quali appartiene.

Ogni file `cq:ClientLibraryFolder` viene popolato con un set di file JS e/o CSS, insieme ad alcuni file di supporto (vedere di seguito). Le proprietà importanti di `cq:ClientLibraryFolder` sono configurate come segue:

* `allowProxy`: Poiché tutti i clientlibs devono essere memorizzati in  `apps`, questa proprietà consente l&#39;accesso a clientlibraries tramite servlet proxy. Vedere [Individuazione di una cartella della libreria client e Utilizzo del servlet delle librerie client proxy](#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) di seguito.
* `categories`: Identifica le categorie in cui il set di file JS e/o CSS entro questo  `cq:ClientLibraryFolder` autunno. La proprietà `categories`, con un valore multiplo, consente a una cartella di libreria di appartenere a più categorie (vedere di seguito per informazioni su come potrebbe essere utile).

Se la cartella della libreria client contiene uno o più file sorgente che, in fase di esecuzione, vengono uniti in un singolo file JS e/o CSS. Il nome del file generato è il nome del nodo con l&#39;estensione del nome di file `.js` o `.css`. Ad esempio, il nodo della libreria denominato `cq.jquery` restituisce il file generato denominato `cq.jquery.js` o `cq.jquery.css`.

Le cartelle della libreria client contengono i seguenti elementi:

* I file sorgente JS e/o CSS
* Risorse statiche che supportano stili CSS, ad esempio icone, font Web ecc.
* Un file `js.txt` e/o un file `css.txt` che identifica i file sorgente da unire nei file JS e/o CSS generati

![Architettura Clientlib](assets/clientlib-architecture.drawio.png)

## Creazione di cartelle libreria lato client {#creating-clientlib-folders}

Le librerie client devono trovarsi in `/apps`. Ciò consente di isolare meglio il codice dal contenuto e dalla configurazione.

Per rendere accessibili le librerie client in `/apps`, viene utilizzato un servlet proxy. Gli ACL sono ancora applicati alla cartella della libreria client, ma il servlet consente la lettura del contenuto tramite `/etc.clientlibs/` se la proprietà `allowProxy` è impostata su `true`.

1. Aprite il CRXDE Lite in un browser Web (`https://<host>:<port>/crx/de`).
1. Selezionare la cartella `/apps` e fare clic su **Crea > Crea nodo**.
1. Immettete un nome per la cartella della libreria e nell&#39;elenco **Tipo** selezionate `cq:ClientLibraryFolder`. Fare clic su **OK**, quindi fare clic su **Salva tutto**.
1. Per specificare la categoria o le categorie a cui appartiene la libreria, selezionare il nodo `cq:ClientLibraryFolder`, aggiungere la seguente proprietà, quindi fare clic su **Salva tutto**:
   * Nome: `categories`
   * Tipo: Stringa
   * Valore: Nome categoria
   * Multi: Selezionato
1. Affinché le librerie client siano accessibili tramite proxy in `/etc.clientlibs`, selezionare il nodo `cq:ClientLibraryFolder`, aggiungere la seguente proprietà, quindi fare clic su **Salva tutto**:
   * Nome: `allowProxy`
   * Tipo: booleano
   * Valore: `true`
1. Per gestire le risorse statiche, create una sottocartella denominata `resources` sotto la cartella della libreria client.
   * Se archiviate risorse statiche nella cartella `resources`, non è possibile fare riferimento a tali risorse in un&#39;istanza pubblicata.
1. Aggiungete i file sorgente alla cartella della libreria.
   * Questo è in genere fatto dal processo di compilazione front-end del [AEM Project Archetype.](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/uifrontend.html)
   * Se necessario, potete organizzare i file sorgente in sottocartelle.
1. Selezionate la cartella della libreria client e fate clic su **Crea > Crea file**.
1. Nella casella Nome file digitare uno dei seguenti nomi di file e fare clic su OK:
   * **`js.txt`:** Utilizzate questo nome file per generare un file JavaScript.
   * **`css.txt`:** Utilizzate questo nome file per generare un foglio di stile a cascata.
1. Aprite il file e digitate il testo seguente per identificare la radice del percorso dei file sorgente:
   * `#base=*[root]*`
   * Sostituire `[root]` con il percorso della cartella che contiene i file sorgente, relativo al file TXT. Ad esempio, usate il testo seguente quando i file sorgente si trovano nella stessa cartella del file TXT:
      * `#base=.`
   * Il codice seguente imposta la radice come cartella denominata mobile sotto il nodo `cq:ClientLibraryFolder`:
      * `#base=mobile`
1. Sulle righe sottostanti `#base=[root]`, digitare i percorsi dei file di origine relativi alla radice. Posizionare ciascun nome file su una riga separata.
1. Fare clic su **Salva tutto**.

## Server delle librerie lato client {#serving-clientlibs}

Una volta che la cartella della libreria client è [configurata come necessario,](#creating-clientlib-folders) i client possono essere richiesti tramite proxy. Ad esempio:

* Hai una clientlib in `/apps/myproject/clientlibs/foo`
* L&#39;immagine è statica in `/apps/myprojects/clientlibs/foo/resources/icon.png`

La proprietà `allowProxy` consente di richiedere:

* clientlib tramite j`/etc.clientlibs/myprojects/clientlibs/foo.js`
* Immagine statica tramite `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

### Caricamento delle librerie client tramite HTL {#loading-via-htl}

Una volta che i client sono stati memorizzati e gestiti correttamente nella cartella della libreria client, possono accedervi tramite HTL.

Le librerie client vengono caricate tramite un modello helper fornito da AEM, accessibile tramite `data-sly-use`. I modelli helper sono disponibili in questo file, che può essere chiamato tramite `data-sly-call`.

Ogni modello di supporto prevede un&#39;opzione `categories` per fare riferimento alle librerie client desiderate. Tale opzione può essere una matrice di valori stringa o una stringa contenente un elenco di valori separati da virgola.

[Per ulteriori informazioni sul caricamento di clientlibs tramite HTL, consultate la ](https://docs.adobe.com/content/help/en/experience-manager-htl/using/getting-started/getting-started.html#loading-client-libraries) documentazione HTL.

<!--
### Setting Cache Timestamps {#setting-cache-timestamps}

This is possible. Still need detail.
-->

## Librerie client su Autore e pubblicazione {#clientlibs-author-publish}

La maggior parte dei clientlibs sarà necessaria nell’istanza di pubblicazione AEM. In altre parole, lo scopo della maggior parte dei clienti è quello di produrre l&#39;esperienza dell&#39;utente finale del contenuto. Per i client sulle istanze di pubblicazione, [strumenti di compilazione front-end](#fed-for-aemaacs) possono essere utilizzati e distribuiti tramite [cartelle della libreria client come descritto sopra.](#creating-clientlib-folders)

Tuttavia, in alcuni casi potrebbe essere necessario personalizzare l’esperienza di authoring con le librerie client. Ad esempio, la personalizzazione di una finestra di dialogo potrebbe richiedere la distribuzione di piccoli bit di CSS o JS nell’istanza di authoring AEM.

### Gestione delle librerie client sull&#39;autore {#clientlibs-on-author}

Se è necessario utilizzare le librerie client per l&#39;authoring, è possibile creare le librerie client in `/apps` utilizzando gli stessi metodi utilizzati per la pubblicazione, ma scriverle direttamente in `/apps/.../clientlibs/foo` invece di creare un intero progetto per gestirlo.

Potete quindi eseguire il &quot;collegamento&quot; al JS di authoring aggiungendo le librerie client a una categoria di libreria client out-of-the-box.

## Strumenti di debug {#debugging-tools}

AEM fornisce diversi strumenti per il debug e il test delle cartelle della libreria client.

### Scopri librerie client {#discover-client-libraries}

Il componente `/libs/cq/granite/components/dumplibs/dumplibs` genera una pagina di informazioni su tutte le cartelle della libreria client nel sistema. Il nodo `/libs/granite/ui/content/dumplibs` ha il componente come tipo di risorsa. Per aprire la pagina, usate il seguente URL (modificando l’host e la porta come richiesto):

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

Le informazioni includono il percorso e il tipo della libreria (CSS o JS) e i valori degli attributi della libreria, come categorie e dipendenze. Le tabelle successive della pagina mostrano le librerie in ogni categoria e canale.

### Vedere Uscita generata {#see-generated-output}

Il componente `dumplibs` include un selettore di test che visualizza il codice sorgente generato per i tag `ui:includeClientLib`. La pagina include il codice per diverse combinazioni di attributi js, css e a tema.

1. Per aprire la pagina Test Output, utilizzare uno dei metodi seguenti:
   * Dalla pagina `dumplibs.html`, fare clic sul collegamento nel testo **Fare clic qui per il test dell&#39;output**.
   * Aprite il seguente URL nel browser Web (utilizzate un host e una porta diversi come richiesto):
      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`
   * La pagina predefinita mostra l&#39;output per i tag senza valore per l&#39;attributo category.
1. Per visualizzare l&#39;output di una categoria, digitare il valore della proprietà `categories` della libreria client e fare clic su **Invia query**.

## Funzionalità aggiuntive della cartella libreria client {#additional-features}

Esistono diverse altre funzionalità supportate dalle cartelle della libreria client in AEM. Tuttavia, non sono necessari in AEM come Cloud Service e come tale il loro uso è scoraggiato. Sono elencati qui per completezza.

>[!WARNING]
>
>Queste funzioni aggiuntive delle cartelle della libreria client non sono necessarie in AEM come Cloud Service e pertanto il loro utilizzo non è consigliato. Sono elencati qui per completezza.

###  Adobe Granite HTML LIbrary Manager {#html-library-manager}

È possibile controllare altre impostazioni della libreria client tramite il pannello **Adobe Granite HTML Library Manager** della console di sistema all&#39;indirizzo `https://<host>:<port>/system/console/configMgr`.

### Proprietà cartella aggiuntive {#additional-folder-properties}

Ulteriori proprietà delle cartelle includono l&#39;autorizzazione del controllo di dipendenze e incorporamenti, ma in genere non sono più necessarie e il loro utilizzo non è più consigliato:

* `dependencies`: Si tratta di un elenco di altre categorie di libreria client da cui dipende la cartella libreria. Ad esempio, a due nodi `cq:ClientLibraryFolder` `F` e `G`, se un file in `F` richiede un altro file in `G` per funzionare correttamente, almeno uno dei `categories` di `G` deve essere compreso tra `dependencies` di `F`.
* `embed`: Utilizzato per incorporare il codice da altre librerie. Se il nodo `F` incorpora i nodi `G` e `H`, l&#39;HTML risultante sarà una concatenazione di contenuto dai nodi `G` e `H`.

### Collegamento a dipendenze {#linking-to-dependencies}

Quando il codice nella cartella della libreria client fa riferimento ad altre librerie, identificate le altre librerie come dipendenze. Il tag `ui:includeClientLib` che fa riferimento alla cartella della libreria client causa l&#39;inclusione nel codice HTML di un collegamento al file libreria generato e alle dipendenze.

Le dipendenze devono essere un&#39;altra `cq:ClientLibraryFolder`. Per identificare le dipendenze, aggiungi una proprietà al nodo `cq:ClientLibraryFolder` con i seguenti attributi:

* **Nome:** dipendenze
* **Tipo:** Stringa[]
* **Valori:** il valore della proprietà category del nodo cq:ClientLibraryFolder da cui dipende la cartella libreria corrente.

Ad esempio, la `/etc/clientlibs/myclientlibs/publicmain` ha una dipendenza dalla libreria `cq.jquery`. La pagina che fa riferimento alla libreria client principale genera codice HTML che include il seguente codice:

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### Incorporazione del codice da altre librerie {#embedding-code-from-other-libraries}

Potete incorporare il codice da una libreria client a un&#39;altra libreria client. In fase di esecuzione, i file JS e CSS generati dalla libreria di incorporamento includono il codice della libreria incorporata.

L&#39;incorporazione del codice è utile per fornire l&#39;accesso alle librerie memorizzate nelle aree protette dell&#39;archivio.

#### Cartelle libreria client specifiche per l&#39;app {#app-specific-client-library-folders}

È consigliabile mantenere tutti i file relativi alle applicazioni nella cartella dell&#39;applicazione al di sotto di `/app`. È inoltre consigliabile negare l&#39;accesso ai visitatori del sito Web nella cartella `/app`. Per soddisfare entrambe le procedure ottimali, create una cartella della libreria client sotto la cartella `/etc` che incorpora la libreria client che si trova sotto `/app`.

Utilizzare la proprietà category per identificare la cartella della libreria client da incorporare. Per incorporare la libreria, aggiungere una proprietà al nodo `cq:ClientLibraryFolder` in cui incorporare, utilizzando i seguenti attributi di proprietà:

* **Nome:** embed
* **Tipo:** Stringa[]
* **Valore:** il valore della proprietà category del  `cq:ClientLibraryFolder` nodo da incorporare.

#### Utilizzo dell&#39;incorporazione per ridurre al minimo le richieste {#using-embedding-to-minimize-requests}

In alcuni casi, l’HTML finale generato per la pagina tipica dall’istanza di pubblicazione include un numero relativamente elevato di elementi `<script>`.

In tali casi, può essere utile combinare tutti i codici libreria client richiesti in un singolo file in modo da ridurre il numero di richieste di andata e ritorno al caricamento della pagina. A questo scopo, è possibile `embed` inserire le librerie necessarie nella libreria client specifica per l&#39;app utilizzando la proprietà embed del nodo `cq:ClientLibraryFolder`.

#### Percorsi nei file CSS {#paths-in-css-files}

Quando incorporate file CSS, il codice CSS generato utilizza percorsi verso risorse relative alla libreria di incorporamento. Ad esempio, la libreria accessibile al pubblico `/etc/client/libraries/myclientlibs/publicmain` incorpora la libreria client `/apps/myapp/clientlib`:

Il file `main.css` contiene lo stile seguente:

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

#### Vedere File incorporati in Output HTML {#see-embedded-files}

Per tracciare l&#39;origine del codice incorporato o per assicurarsi che le librerie client incorporate producano i risultati previsti, è possibile visualizzare i nomi dei file che vengono incorporati in fase di esecuzione. Per visualizzare i nomi dei file, aggiungete il parametro `debugClientLibs=true` all&#39;URL della pagina Web. La libreria generata contiene istruzioni `@import` invece del codice incorporato.

Nell&#39;esempio della sezione precedente [Incorporamento del codice da altre librerie](#embedding-code-from-other-libraries), la cartella della libreria client `/etc/client/libraries/myclientlibs/publicmain` incorpora la cartella della libreria client `/apps/myapp/clientlib`. L&#39;aggiunta del parametro alla pagina Web genera il seguente collegamento nel codice sorgente della pagina Web:

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

Aprendo il file `publicmain.css` viene visualizzato il seguente codice:

```javascript
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. Nella casella dell’indirizzo del browser Web, aggiungete il testo seguente all’URL del codice HTML:
   * `?debugClientLibs=true`
1. Quando la pagina viene caricata, visualizzate l’origine della pagina.
1. Fare clic sul collegamento fornito come href per l&#39;elemento di collegamento per aprire il file e visualizzare il codice sorgente.

### Utilizzo dei preprocessori {#using-preprocessors}

AEM è possibile collegare preprocessori e navi con supporto per [YUI Compressor](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) per CSS e JavaScript e [Google Closure Compiler (GCC)](https://developers.google.com/closure/compiler/) per JavaScript con YUI impostato AEM preprocessore predefinito.

I preprocessori collegabili consentono un utilizzo flessibile, tra cui:

* Definizione di ScriptProcessors in grado di elaborare origini di script
* I processori sono configurabili con opzioni
* I processori possono essere utilizzati per la minificazione, ma anche per i casi non minati
* clientlib può definire quale processore utilizzare

>[!NOTE]
>
>Per impostazione predefinita, AEM utilizza il compressore YUI. Per un elenco dei problemi noti, consultate la [documentazione GitHub del compressore YUI](https://github.com/yui/yuicompressor/issues). Il passaggio al compressore GCC per determinati clientlibs può risolvere alcuni problemi rilevati durante l’utilizzo di YUI.

>[!CAUTION]
>
>Non inserite una libreria ridotta in una libreria client. Fornite invece la libreria non elaborata e, se è necessaria la minificazione, utilizzate le opzioni dei preprocessori.

#### Utilizzo {#usage}

Potete scegliere di configurare la configurazione dei preprocessori per clientlibrary o per tutta la struttura del sistema.

* Aggiungere le proprietà multivalore `cssProcessor` e `jsProcessor` nel nodo clientlibrary
* Oppure definire la configurazione predefinita del sistema tramite la configurazione **HTML Library Manager** OSGi

Una configurazione preprocessore sul nodo clientlib ha la precedenza rispetto alla configurazione OSGI.

#### Formato ed esempi {#format-and-examples}

##### Formato {#format}

```javascript
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

##### Compressore YUI per la riduzione CSS e GCC per JS {#yui-compressor-for-css-minification-and-gcc-for-js}

```javascript
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

##### Typescript to Preprocess (Prepara da preelaborare) e poi GCC to Minify and Obfuscate {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

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

Per ulteriori dettagli sulle opzioni GCC, consultare la [documentazione GCC](https://developers.google.com/closure/compiler/docs/compilation_levels).

#### Imposta minificatore predefinito di sistema {#set-system-default-minifier}

YUI è impostato come minificatore predefinito in AEM. Per modificare questa impostazione in GCC, attenetevi alla procedura seguente.

1. Vai a Gestione configurazione Apache Felix all&#39;indirizzo (`http://<host>:<portY/system/console/configMgr`)
1. Trovare e modificare il **Adobe Granite HTML Library Manager**.
1. Abilitare l&#39;opzione **Minify** (se non è già abilitata).
1. Impostare il valore **Configurazione predefinita processore JS** su `min:gcc`.
   * Le opzioni possono essere passate se separate da un punto e virgola, ad esempio `min:gcc;obfuscate=true`.
1. Fare clic su **Salva** per salvare le modifiche.
