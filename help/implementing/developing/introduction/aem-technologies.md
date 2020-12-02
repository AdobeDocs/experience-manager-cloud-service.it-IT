---
title: AEM Fondamenti Tecnici
description: Una panoramica delle fondamenta tecniche di AEM che include la struttura delle AEM e tecnologie fondamentali come JCR, Sling e OSGi.
translation-type: tm+mt
source-git-commit: 750fded1564de2b11f6c104cc70befc4453405b4
workflow-type: tm+mt
source-wordcount: '2187'
ht-degree: 0%

---


# AEM Fondamenti tecnici {#aem-technical-foundations}

AEM è una piattaforma solida basata su tecnologie collaudate, scalabili e flessibili. Questo documento fornisce una panoramica dettagliata delle varie parti che compongono AEM ed è inteso come appendice tecnica per uno sviluppatore di AEM a pieno stack. Non si tratta di una guida introduttiva. Se non avete esperienza AEM sviluppo, come primo passo, consultate la [Guida introduttiva allo sviluppo  AEM Sites - Esercitazione WKND](develop-wknd-tutorial.md).

>[!TIP]
>
>Prima di immergersi nelle tecnologie di base di AEM,  Adobe consiglia di completare la [Guida introduttiva allo sviluppo  AEM Sites - Esercitazione WKND.](develop-wknd-tutorial.md)

## Nozioni di base {#fundamentals}

Come moderno sistema di gestione dei contenuti, AEM si basa sulle tecnologie Web standard:

* Ciclo request-response (XMLHttpRequest/XMLHttpResponse)
* HTML
* CSS
* JavaScript

L&#39;archivio dei contenuti sottostante e i livelli di business logic sono basati sulle tecnologie Java:

* JCR
* Sling
* OSGi

## Repository di contenuti Java {#java-content-repository}

Lo standard JCR (Java Content Repository), [JSR 283](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/index.html), specifica un modo indipendente dal fornitore e indipendente dall&#39;implementazione per accedere ai contenuti in modo bidirezionale su un livello granulare all&#39;interno di un repository di contenuti. Il lead è detenuto da  Adobe Research (Svizzera) AG.

Il pacchetto [JCR API 2.0](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/index.html), `javax.jcr.*` viene utilizzato per l&#39;accesso diretto e la manipolazione del contenuto del repository.

AEM è basato su un JCR.

## Apache Jackrabbit Oak {#jackrabbit-oak}

[Apache Jackrabbit ](https://jackrabbit.apache.org/oak/) Oakis implementa un archivio di contenuti gerarchici scalabile e ad alte prestazioni da usare come base per siti Web moderni e altre applicazioni di contenuto esigenti, in conformità con lo standard JCR.

Jackrabbit Oak (detto anche semplicemente Oak), è l&#39;implementazione dello standard JCR su cui AEM è costruito.

## Elaborazione richiesta Sling {#sling-request-processing}

AEM è realizzato utilizzando [Sling](https://sling.apache.org/site/index.html), un framework di applicazione Web basato su principi REST che fornisce un facile sviluppo di applicazioni orientate al contenuto. Sling utilizza un repository JCR, come Apache Jackrabbit Oak, come archivio dati. Sling ha contribuito alla Apache Software Foundation - ulteriori informazioni sono reperibili presso Apache.

### Introduzione a Sling {#introduction-to-sling}

Con Sling, il tipo di contenuto di cui eseguire il rendering non è il primo criterio di elaborazione. La considerazione principale è stabilire se l&#39;URL corrisponde a un oggetto contenuto per il quale è possibile trovare uno script per eseguire il rendering. Questo offre un eccellente supporto agli autori di contenuti Web per creare pagine facilmente personalizzate in base alle loro esigenze.

I vantaggi di questa flessibilità sono evidenti nelle applicazioni con un&#39;ampia gamma di elementi di contenuto diversi, o quando è necessario creare pagine che possano essere facilmente personalizzate. In particolare, quando si implementa un sistema di gestione dei contenuti Web come AEM.

Per i primi passi per lo sviluppo con Sling, vedere [Scoprire Sling in 15 minuti](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html).

Nel diagramma seguente viene illustrata la risoluzione dello script Sling: mostra come passare da una richiesta HTTP al nodo del contenuto, dal nodo del contenuto al tipo di risorsa, dal tipo di risorsa allo script e quali variabili di script sono disponibili.

![Informazioni sulla risoluzione degli script Apache Sling](assets/sling-cheatsheet-01.png)

Nel diagramma seguente sono illustrati tutti i parametri di richiesta nascosti, ma potenti, che è possibile utilizzare per gestire `SlingPostServlet`, il gestore predefinito per tutte le richieste di POST che offre infinite opzioni per creare, modificare, eliminare, copiare e spostare i nodi nell&#39;archivio.

![Utilizzo di SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling è incentrato sui contenuti {#sling-is-content-centric}

Sling è *incentrato sul contenuto*. Ciò significa che l&#39;elaborazione è incentrata sul contenuto, in quanto ogni richiesta (HTTP) viene mappata sul contenuto sotto forma di risorsa JCR (un nodo del repository):

* La prima destinazione è la risorsa (nodo JCR) che contiene il contenuto
* In secondo luogo, la rappresentazione, o script, si trova dalle proprietà della risorsa in combinazione con alcune parti della richiesta (ad esempio, selettori e/o estensione)

### RESTful Sling {#restful-sling}

Grazie alla sua filosofia incentrata sui contenuti, Sling implementa un server orientato al REST e quindi offre un nuovo concetto nei framework delle applicazioni Web. I vantaggi sono:

* Molto RESTful, non solo sulla superficie; le risorse e le rappresentazioni vengono modellate correttamente all&#39;interno del server
* Rimuove uno o più modelli di dati
   * Altri framework di gestione del contenuto potrebbero richiedere struttura URL, oggetti aziendali e schema DB per accedere a una risorsa.
   * Utilizzando Sling, questo viene ridotto a: URL = resource = JCR structure

### Decomposizione URL {#url-decomposition}

In Sling, l&#39;elaborazione è guidata dall&#39;URL della richiesta dell&#39;utente. Definisce il contenuto che deve essere visualizzato dagli script appropriati. A questo scopo, le informazioni vengono estratte dall’URL.

Se analizziamo il seguente URL:

```text
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

Possiamo suddividerlo nelle sue parti composite:

| protocol | host |  | percorso contenuto | selettori | extension |  | suffisso |  | param(s) |
|---|---|---|---|---|---|---|---|---|---|
| `https://` | `myhost` | `/` | `tools/spy` | `.printable.a4.` | `html` | `/` | `a/b` | `?` | `x=12` |

* **protocollo**  - HTTPS
* **host** - Dominio del sito
* **percorso**  del contenuto - Percorso che specifica il contenuto di cui eseguire il rendering ed è utilizzato in combinazione con l&#39;estensione; in questo esempio, essi traducono in  `tools/spy.html`
* **selettore(i)** - Utilizzato per metodi alternativi di rendering del contenuto; in questo esempio, una versione compatibile con la stampante in formato A4
* **extension** - Content format; specifica inoltre lo script da utilizzare per il rendering
* **suffisso** : può essere utilizzato per specificare informazioni aggiuntive
* **param(s)** - Tutti i parametri richiesti per il contenuto dinamico

#### Da URL a contenuto e script {#from-url-to-content-and-scripts}

Utilizzo dei principi di decomposizione URL:

* La mappatura utilizza il percorso contenuto estratto dalla richiesta per individuare la risorsa.
* Quando si trova la risorsa appropriata, il tipo di risorsa sling viene estratto e utilizzato per individuare lo script da utilizzare per il rendering del contenuto.

La figura seguente illustra il meccanismo utilizzato, che sarà discusso più dettagliatamente nelle sezioni seguenti.

![Meccanismo di mappatura URL](assets/url-mapping.png)

Con Sling, si specifica quale script esegue il rendering di una determinata entità (impostando la proprietà `sling:resourceType` nel nodo JCR). Questo meccanismo offre più libertà di uno in cui lo script accede alle entità dati (come un&#39;istruzione SQL in uno script PHP farebbe) in quanto una risorsa può avere diverse rappresentazioni.

#### Mapping delle richieste alle risorse {#mapping-requests-to-resources}

La richiesta è ripartita e vengono estratte le informazioni necessarie. Nella directory archivio viene ricercata la risorsa richiesta (nodo contenuto):

* First Sling controlla se un nodo esiste nella posizione specificata nella richiesta; ad esempio `../content/corporate/jobs/developer.html`
* Se non viene trovato alcun nodo, l&#39;estensione viene eliminata e la ricerca viene ripetuta; ad esempio `../content/corporate/jobs/developer`
* Se non viene trovato alcun nodo, Sling restituirà il codice http 404 (Non trovato).

Sling permette anche cose diverse dai nodi JCR di essere risorse, ma questa è una funzione avanzata.

### Individuazione dello script {#locating-the-script}

Quando si trova la risorsa appropriata (nodo di contenuto), viene estratto il tipo di risorsa **sling**. Si tratta di un percorso che individua lo script da utilizzare per il rendering del contenuto.

Il percorso specificato da `sling:resourceType` può essere:

* Assoluto
* Relativo a un parametro di configurazione

>[!TIP]
>
>I percorsi relativi sono consigliati  Adobe in quanto aumentano la portabilità.

Tutti gli script Sling sono memorizzati in sottocartelle di `/apps` (script utente modificabili) o `/libs` (script di sistema immutabili), che verranno cercate in questo ordine.

Alcuni altri punti da sottolineare sono:

* Quando il metodo (GET, POST) è richiesto, viene specificato in maiuscolo come in base alla specifica HTTP, ad esempio `jobs.POST.esp`
* Sono supportati diversi motori di script, ma gli script comuni consigliati sono HTL e JavaScript.

L&#39;elenco dei motori di script supportati dall&#39;istanza specifica di AEM è elencato nella console di gestione Felix ( `http://<host>:<port>/system/console/slingscripting`).

Utilizzando l&#39;esempio precedente, se `sling:resourceType` è `hr/jobs`, per:

* Richieste GET/HEAD e URL che terminano in `.html` (tipi di richiesta predefiniti, formato predefinito)
   * Lo script sarà `/apps/hr/jobs/jobs.esp`; l&#39;ultima sezione di `sling:resourceType` rappresenta il nome del file.
* Richieste POST (tutti i tipi di richiesta eccetto GET/HEAD, il nome del metodo deve essere maiuscolo)
   * POST verrà utilizzato nel nome dello script.
   * Lo script sarà `/apps/hr/jobs/jobs.POST.esp`.
* URL in altri formati, che non terminano con `.html`
   * Esempio `../content/corporate/jobs/developer.pdf`
   * Lo script sarà `/apps/hr/jobs/jobs.pdf.esp`; il suffisso viene aggiunto al nome dello script.
* URL con selettori
   * I selettori possono essere utilizzati per visualizzare lo stesso contenuto in un formato alternativo. Ad esempio, una versione semplice della stampante, un feed rss o un riepilogo.
   * Se si considera una versione compatibile con la stampante, il selettore potrebbe essere `print`; come in `../content/corporate/jobs/developer.print.html`
   * Lo script sarà `/apps/hr/jobs/jobs.print.esp`; il selettore viene aggiunto al nome dello script.
* Se non è stato definito nessun `sling:resourceType`, allora:
   * Il percorso del contenuto verrà utilizzato per cercare uno script appropriato (se è attivo il percorso `ResourceTypeProvider`).
   * Ad esempio, lo script per `../content/corporate/jobs/developer.html` genererebbe una ricerca in `/apps/content/corporate/jobs/`.
   * Verrà utilizzato il tipo di nodo principale.
* Se non viene trovato alcuno script, verrà utilizzato lo script predefinito.
   * La rappresentazione predefinita è attualmente supportata come testo normale (`.txt`), HTML (`.html`) e JSON (`.json`), che elencano tutte le proprietà del nodo (formattate in modo appropriato). La rappresentazione predefinita per l&#39;estensione `.res`, o per le richieste senza estensione di richiesta, consiste nello spool della risorsa (ove possibile).
* Per la gestione degli errori HTTP (codici 403 o 404), Sling cerca uno script all’indirizzo:
   * Posizione `/apps/sling/servlet/errorhandler` per gli script personalizzati
   * Oppure la posizione dello script standard `/libs/sling/servlet/errorhandler/404.jsp`

Se per una determinata richiesta sono richiesti più script, viene selezionato lo script con la corrispondenza migliore. Più specifica è una partita, meglio è. in altre parole, più il selettore corrisponde meglio, indipendentemente da eventuali estensioni di richiesta o dalla corrispondenza del nome del metodo.

Ad esempio, prendete in considerazione una richiesta per accedere alla risorsa

* `/content/corporate/jobs/developer.print.a4.html`

di tipo

* `sling:resourceType="hr/jobs"`

Presupponendo che sia presente il seguente elenco di script nella posizione corretta:

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

Quindi l&#39;ordine delle preferenze sarebbe (8) - (7) - (6) - (5) - (4) - (3) - (2) - (1).

Oltre ai tipi di risorse (principalmente definiti dalla proprietà `sling:resourceType`) è presente anche il super tipo di risorsa. Questo è indicato generalmente dalla proprietà `sling:resourceSuperType`. Questi super tipi vengono considerati anche quando si tenta di trovare uno script. Il vantaggio dei super tipi di risorse è che possono formare una gerarchia di risorse in cui il tipo di risorsa predefinito `sling/servlet/default` (utilizzato dai servlet predefiniti) è effettivamente il livello principale.

Il super tipo di risorsa può essere definito in due modi:

* dalla proprietà `sling:resourceSuperType` della risorsa.
* dalla proprietà `sling:resourceSuperType` del nodo a cui punta il `sling:resourceType`.

Esempio:

* `/`
   * `a`
   * `b`
      * `sling:resourceSuperType = a`
   * `c`
      * `sling:resourceSuperType = b`
   * `x`
      * `sling:resourceType = c`
   * `y`
      * `sling:resourceType = c`
      * `sling:resourceSuperType = a`

La gerarchia dei tipi di:

* `/x`
   * È `[ c, b, a, <default>]`
* while for `/y`
   * La gerarchia è `[ c, a, <default>]`

Questo perché `/y` ha la proprietà `sling:resourceSuperType`, mentre `/x` non lo è e quindi il relativo supertipo viene preso dal relativo tipo di risorsa.

#### Gli script Sling non possono essere chiamati direttamente {#sling-scripts-cannot-be-called-directly}

All&#39;interno di Sling, gli script non possono essere richiamati direttamente in quanto ciò violerebbe il concetto rigoroso di server REST; potete combinare risorse e rappresentazioni.

Se si chiama la rappresentazione (lo script) direttamente, si nasconde la risorsa all&#39;interno dello script, in modo che il framework (Sling) non ne sia più a conoscenza. Così si perdono alcune caratteristiche:

* Gestione automatica di metodi http diversi dagli GET, inclusi:
   * POST, PUT, DELETE che vengono gestiti con un&#39;implementazione standard sling
   * Lo script `POST.jsp` nella posizione `sling:resourceType`
* L&#39;architettura del codice non è più pulita né strutturata come dovrebbe; di importanza primaria per lo sviluppo su larga scala

### API Sling {#sling-api}

Vengono utilizzati il pacchetto Sling API, le `org.apache.sling.*` e le librerie di tag.

### Riferimento a elementi esistenti utilizzando sling:include {#referencing-existing-elements-using-sling-include}

Una considerazione finale è la necessità di fare riferimento agli elementi esistenti all&#39;interno degli script.

Script più complessi (aggregazione di script) potrebbero dover accedere a più risorse (ad esempio, navigazione, barra laterale, piè di pagina, elementi di un elenco) e farlo includendo la *risorsa*.

A tal fine è possibile utilizzare il comando `sling:include("/<path>/<resource>")`. Ciò includerà effettivamente la definizione della risorsa di riferimento.

## OSGi {#osgi}

OSGi (Open Services Gateway Initiative) definisce un&#39;architettura per lo sviluppo e la distribuzione di applicazioni e librerie modulari (è anche noto come Dynamic Module System for Java). I contenitori OSGi consentono di suddividere l’applicazione in singoli moduli (file JAR con ulteriori metadati e denominati bundle nella terminologia OSGi) e di gestire le interdipendenze tra di essi con:

* Servizi implementati all&#39;interno del contenitore
* Un contratto tra il contenitore e la vostra applicazione

Questi servizi e contratti forniscono un&#39;architettura che consente ai singoli elementi di scoprire l&#39;un l&#39;altro in modo dinamico per la collaborazione.

Un framework OSGi offre quindi il caricamento/scaricamento dinamico, la configurazione e il controllo di questi bundle, senza necessità di riavvio.

>[!NOTE]
>
>Per maggiori informazioni sulla tecnologia OSGi, visitare il [sito Web OSGi](https://www.osgi.org).
>
>In particolare, la pagina Basic Education contiene una serie di presentazioni ed esercitazioni.

Questa architettura consente di estendere Sling con moduli specifici dell&#39;applicazione. Sling, e quindi AEM, utilizza l&#39;implementazione [Apache Felix](https://felix.apache.org/) di OSGi. Sono entrambe raccolte di bundle OSGi in esecuzione in un framework OSGi.

Questo consente di eseguire le azioni seguenti su uno qualsiasi dei pacchetti all&#39;interno dell&#39;installazione:

* Installare la versione
* Avvia
* Arresta
* Aggiorna
* Disinstalla
* Vedere lo stato corrente
* Accesso a informazioni più dettagliate (ad esempio nome simbolico, versione, posizione, ecc.) sui bundle specifici

Per ulteriori informazioni, vedere [Configurazione di OSGi per AEM come Cloud Service](/help/implementing/deploying/configuring-osgi.md).

## Struttura all&#39;interno del repository {#structure-within-the-repository}

L&#39;elenco seguente fornisce una panoramica della struttura che verrà visualizzata all&#39;interno della directory archivio.

* `/apps` - applicazione correlata; include definizioni di componenti specifiche per il sito Web. I componenti sviluppati possono essere basati sui componenti forniti in `/libs/core/wcm/components`.
* `/content` - Contenuto creato per il sito Web.
* `/etc`
* `/home` - Informazioni utente e gruppo.
* `/libs` - Librerie e definizioni che appartengono al nucleo della AEM. Le sottocartelle di `/libs` rappresentano le AEM predefinite. È possibile che il contenuto in `/libs` non venga modificato. Le funzioni specifiche del sito Web devono essere eseguite in `/apps`.
* `/tmp` - Area di lavoro temporanea.
* `/var` - i file che cambiano e vengono aggiornati dal sistema; come registri di controllo, statistiche, gestione degli eventi.

>[!CAUTION]
>
>Le modifiche a questa struttura, o ai file al suo interno, devono essere apportate con attenzione. Assicuratevi di comprendere appieno le implicazioni delle modifiche apportate.
>
>Non è necessario modificare nulla nel percorso `/libs`. Per la configurazione e altre modifiche, copiate l&#39;elemento da `/libs` a `/apps` e apportate eventuali modifiche all&#39;interno di `/apps`.
