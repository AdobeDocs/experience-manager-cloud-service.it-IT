---
title: Fondamenti tecnici AEM
description: Panoramica delle basi tecniche di AEM, compreso il modo in cui AEM è strutturata e le tecnologie fondamentali come JCR, Sling e OSGi.
exl-id: ab6e7fe9-a25d-4351-a005-f4466cc0f40e
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2129'
ht-degree: 1%

---

# Fondamenti tecnici AEM {#aem-technical-foundations}

AEM è una piattaforma solida basata su tecnologie collaudate, scalabili e flessibili. Questo documento offre una panoramica dettagliata delle varie parti che compongono AEM ed è concepito come un’appendice tecnica per uno sviluppatore AEM full-stack. Non è concepito come guida introduttiva. Se hai poca esperienza con lo sviluppo AEM, consulta [Guida introduttiva allo sviluppo per AEM Sites - Esercitazione WKND](develop-wknd-tutorial.md) come primo passaggio.

>[!TIP]
>
>Prima di immergerti nelle tecnologie di base di AEM, Adobe consiglia di completare l&#39;[esercitazione Guida introduttiva allo sviluppo per AEM Sites - WKND](develop-wknd-tutorial.md).

## Nozioni di base {#fundamentals}

In quanto sistema moderno di gestione dei contenuti, AEM si basa sulle tecnologie web standard:

* Ciclo richiesta-risposta (XMLHttpRequest / XMLHttpResponse)
* HTML
* CSS
* JavaScript

I livelli dell’archivio dei contenuti e della logica di business sottostanti sono basati sulle tecnologie Java™:

* JCR
* Sling
* OSGi

## Archivio dei contenuti Java™ {#java-content-repository}

Lo standard Java™ Content Repository (JCR), [JSR 283](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html), specifica un modo indipendente dal fornitore e dall&#39;implementazione per accedere al contenuto in modo bidirezionale su un livello granulare all&#39;interno di un repository dei contenuti. Il lead della specifica è detenuto da Adobe Research (Switzerland) AG.

Il pacchetto [JCR API 2.0](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html), `javax.jcr.*`, viene utilizzato per l&#39;accesso diretto e la manipolazione del contenuto dell&#39;archivio.

AEM è basato su JCR.

## Apache Jackrabbit Oak {#jackrabbit-oak}

[Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/) è un&#39;implementazione di un archivio di contenuti gerarchici scalabile e ad alte prestazioni da utilizzare come base per siti Web moderni e altre applicazioni di contenuti complesse, conformi allo standard JCR.

Jackrabbit Oak (noto anche semplicemente come Oak) è l’implementazione dello standard JCR su cui viene creato AEM.

## Elaborazione richiesta Sling {#sling-request-processing}

AEM è stato creato utilizzando [Sling](https://sling.apache.org/index.html), un framework di applicazioni Web basato sui principi REST che consente di sviluppare facilmente applicazioni orientate ai contenuti. Sling utilizza un archivio JCR, come Apache Jackrabbit Oak, come archivio dati. Sling ha contribuito alla Apache Software Foundation; ulteriori informazioni sono disponibili su Apache.

### Introduzione a Sling {#introduction-to-sling}

Utilizzando Sling, il tipo di contenuto di cui eseguire il rendering non è la prima considerazione di elaborazione. Al contrario, la considerazione principale è se l’URL si risolve in un oggetto di contenuto per il quale è possibile trovare uno script per eseguire il rendering. Questo processo fornisce un supporto eccellente agli autori di contenuti web per creare pagine facilmente personalizzate in base alle loro esigenze.

I vantaggi di questa flessibilità sono evidenti nelle applicazioni con un’ampia gamma di elementi di contenuto diversi o quando servono pagine facilmente personalizzabili. In particolare, quando si implementa un sistema di gestione dei contenuti web come AEM.

Consulta [Scopri Sling in 15 minuti](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) per i primi passaggi per lo sviluppo con Sling.

Il diagramma seguente spiega la risoluzione dello script Sling. Mostra come passare dalla richiesta HTTP al nodo di contenuto, dal nodo di contenuto al tipo di risorsa, dal tipo di risorsa allo script e quali variabili di script sono disponibili.

![Informazioni sulla risoluzione dello script Apache Sling](assets/sling-cheatsheet-01.png)

Nel diagramma seguente vengono illustrati i parametri di richiesta nascosti ma potenti che è possibile utilizzare con `SlingPostServlet`, il gestore predefinito per tutte le richieste POST. Il gestore offre opzioni infinite per la creazione, la modifica, l’eliminazione, la copia e lo spostamento di nodi nell’archivio.

![Utilizzo di SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling è incentrato sui contenuti {#sling-is-content-centric}

Sling è *incentrato sul contenuto*. Ciò significa che l’elaborazione si concentra sul contenuto, in quanto ogni richiesta (HTTP) è mappata sul contenuto sotto forma di risorsa JCR (un nodo dell’archivio):

* La prima destinazione è la risorsa (nodo JCR) contenente il contenuto
* In secondo luogo, la rappresentazione, o script, si trova dalle proprietà della risorsa con alcune parti della richiesta (ad esempio, selettori e/o estensione)

### Sling RESTful {#restful-sling}

Grazie alla sua filosofia incentrata sui contenuti, Sling implementa un server orientato a REST e quindi presenta un nuovo concetto nei framework delle applicazioni web. I vantaggi sono i seguenti:

* RESTful, non solo sulla superficie; le risorse e le rappresentazioni sono modellate correttamente all&#39;interno del server
* Rimuove uno o più modelli di dati
   * Altri framework di gestione dei contenuti potrebbero richiedere struttura URL, oggetti aziendali e schema di database per accedere a una risorsa.
   * L’utilizzo di Sling lo riduce a: URL = risorsa = struttura JCR

### Scomposizione URL {#url-decomposition}

In Sling, l’elaborazione è guidata dall’URL della richiesta dell’utente. Definisce il contenuto da visualizzare mediante gli script appropriati e le informazioni vengono estratte dall’URL.

Analisi del seguente URL:

```text
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

È possibile suddividerlo nelle sue parti composite:

| protocollo | host |  | percorso contenuto | selettori | estensione |  | suffisso |  | parametri |
|---|---|---|---|---|---|---|---|---|---|
| `https://` | `myhost` | `/` | `tools/spy` | `.printable.a4.` | `html` | `/` | `a/b` | `?` | `x=12` |

* **protocollo** - HTTPS
* **host** - Dominio del sito
* **percorso contenuto** - Percorso che specifica il contenuto da riprodurre e viene utilizzato con l&#39;estensione. In questo esempio, si traduce in `tools/spy.html`
* **selettori** - Utilizzati per metodi alternativi di rendering del contenuto; in questo esempio una versione di formato A4 compatibile con la stampante
* **estensione** - Formato contenuto; specifica anche lo script da utilizzare per il rendering
* **suffix** - Può essere utilizzato per specificare informazioni aggiuntive
* **parametri** - Qualsiasi parametro richiesto per il contenuto dinamico

#### Da URL a contenuto e script {#from-url-to-content-and-scripts}

Utilizzo dei principi di decomposizione degli URL:

* La mappatura utilizza il percorso del contenuto estratto dalla richiesta per individuare la risorsa.
* Quando si trova la risorsa appropriata, il tipo di risorsa sling viene estratto e utilizzato per individuare lo script da utilizzare per il rendering del contenuto.

La figura riportata di seguito illustra il meccanismo utilizzato, descritto più dettagliatamente nelle sezioni seguenti.

![Meccanismo di mappatura URL](assets/url-mapping.png)

Con Sling, puoi specificare quale script esegue il rendering di una determinata entità (impostando la proprietà `sling:resourceType` nel nodo JCR). Questo meccanismo offre maggiore libertà rispetto a uno in cui lo script accede alle entità di dati (come farebbe un’istruzione SQL in uno script PHP) in quanto una risorsa può avere diverse rappresentazioni.

#### Mappatura delle richieste alle risorse {#mapping-requests-to-resources}

La richiesta è suddivisa ed è possibile estrarre le informazioni necessarie. Nell’archivio viene eseguita la ricerca della risorsa richiesta (nodo del contenuto):

* First Sling controlla se un nodo esiste nel percorso specificato nella richiesta, ad esempio `../content/corporate/jobs/developer.html`
* Se non viene trovato alcun nodo, l&#39;estensione verrà eliminata e la ricerca verrà ripetuta, ad esempio `../content/corporate/jobs/developer`
* Se non viene trovato alcun nodo, Sling restituisce il codice http 404 (Not Found).

Sling consente anche di utilizzare come risorse elementi diversi dai nodi JCR, ma questa funzionalità è avanzata.

### Individuazione dello script {#locating-the-script}

Quando si trova la risorsa appropriata (nodo di contenuto), viene estratto il tipo di risorsa **sling**. Questo percorso individua lo script da utilizzare per il rendering del contenuto.

Il percorso specificato da `sling:resourceType` può essere:

* Assoluto
* Relativo a un parametro di configurazione

>[!TIP]
>
>I percorsi relativi sono consigliati da Adobe in quanto aumentano la portabilità.

Tutti gli script Sling sono archiviati in sottocartelle di `/apps` (mutable, user scripts) o `/libs` (immutable, system scripts), in cui viene eseguita la ricerca in questo ordine.

Altri punti da notare sono:

* Quando il metodo (GET, POST) è obbligatorio, viene specificato in maiuscolo in base alla specifica HTTP, ad esempio, `jobs.POST.esp`
* Sono supportati vari motori di script, ma gli script comuni e consigliati sono HTL e JavaScript.

L&#39;elenco dei motori di script supportati dall&#39;istanza di AEM specificata è elencato nella console di gestione Felix ( `http://<host>:<port>/system/console/slingscripting`).

Utilizzando l&#39;esempio precedente, se `sling:resourceType` è `hr/jobs` per:

* Richieste e URL di GET/HEAD che terminano con `.html` (tipi di richiesta predefiniti, formato predefinito)
   * Lo script è `/apps/hr/jobs/jobs.esp`; l&#39;ultima sezione di `sling:resourceType` costituisce il nome del file.
* Richieste POST (tutti i tipi di richiesta eccetto GET/HEAD, il nome del metodo deve essere in maiuscolo)
   * POST viene utilizzato nel nome dello script.
   * Lo script è `/apps/hr/jobs/jobs.POST.esp`.
* URL in altri formati, che non terminano con `.html`
   * Ad esempio `../content/corporate/jobs/developer.pdf`
   * Lo script è `/apps/hr/jobs/jobs.pdf.esp`. Il suffisso viene aggiunto al nome dello script.
* URL con selettori
   * I selettori possono essere utilizzati per visualizzare lo stesso contenuto in un formato alternativo. Ad esempio, una versione compatibile con la stampante, un feed rss o un riepilogo.
   * Se si considera una versione adatta alla stampante in cui il selettore potrebbe essere `print`, come in `../content/corporate/jobs/developer.print.html`
   * Lo script è `/apps/hr/jobs/jobs.print.esp`. Il selettore viene aggiunto al nome dello script.
* In caso negativo, viene definito `sling:resourceType`:
   * Il percorso del contenuto viene utilizzato per cercare uno script appropriato (se il `ResourceTypeProvider` basato sul percorso è attivo).
   * Ad esempio, lo script per `../content/corporate/jobs/developer.html` genererebbe una ricerca in `/apps/content/corporate/jobs/`.
   * Viene utilizzato il tipo di nodo principale.
* Se non viene trovato alcuno script, viene utilizzato lo script predefinito.
   * Il rendering predefinito è supportato come testo normale (`.txt`), HTML (`.html`) e JSON (`.json`), che elencano tutte le proprietà del nodo (formattate in modo appropriato). Il rendering predefinito per l&#39;estensione `.res`, o per le richieste senza estensione di richiesta, consiste nello spool della risorsa (ove possibile).
* Per la gestione degli errori http (codici 403 o 404), Sling cerca uno script in:
   * Percorso `/apps/sling/servlet/errorhandler` per gli script personalizzati
   * Oppure il percorso dello script standard `/libs/sling/servlet/errorhandler/404.jsp`

Se per una determinata richiesta sono applicabili più script, viene selezionato lo script con la corrispondenza migliore. Più specifica è una corrispondenza, migliore sarà; in altre parole, più il selettore corrisponderà, indipendentemente da qualsiasi estensione di richiesta o corrispondenza del nome del metodo.

Ad esempio, considera una richiesta di accesso alla risorsa

* `/content/corporate/jobs/developer.print.a4.html`

Di tipo

* `sling:resourceType="hr/jobs"`

Supponendo di avere il seguente elenco di script nella posizione corretta:

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

Quindi l&#39;ordine di preferenza sarebbe (8) - (7) - (6) - (5) - (4) - (3) - (2) - (1).

Oltre ai tipi di risorsa (definiti principalmente dalla proprietà `sling:resourceType`), è presente anche il super tipo di risorsa. Tipo indicato dalla proprietà `sling:resourceSuperType`. Questi super tipi vengono considerati anche quando si tenta di trovare uno script. Il vantaggio dei super-tipi di risorse è che possono formare una gerarchia di risorse in cui il tipo di risorsa predefinito `sling/servlet/default` (utilizzato dai servlet predefiniti) è effettivamente la radice.

Il super tipo di risorsa di una risorsa può essere definito in due modi:

* dalla proprietà `sling:resourceSuperType` della risorsa.
* dalla proprietà `sling:resourceSuperType` del nodo a cui punta `sling:resourceType`.

Ad esempio:

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

Gerarchia dei tipi di:

* `/x`
   * È `[ c, b, a, <default>]`
* Mentre per `/y`
   * La gerarchia è `[ c, a, <default>]`

Il motivo è che `/y` ha la proprietà `sling:resourceSuperType`, mentre `/x` no e pertanto il suo supertipo viene preso dal suo tipo di risorsa.

#### Gli script Sling non possono essere chiamati direttamente {#sling-scripts-cannot-be-called-directly}

All’interno di Sling, gli script non possono essere chiamati direttamente perché violerebbero il concetto rigoroso di server REST; è possibile combinare risorse e rappresentazioni.

Se chiami direttamente la rappresentazione (lo script), nascondi la risorsa all’interno dello script, pertanto il framework (Sling) non ne è più a conoscenza. In questo modo si perdono alcune funzionalità:

* Gestione automatica di metodi http diversi da GET, tra cui:
   * POST, PUT, DELETE gestito con un’implementazione sling predefinita
   * Lo script `POST.jsp` nel percorso `sling:resourceType`
* L&#39;architettura del codice non è più pulita né strutturata in modo chiaro come dovrebbe essere; di primaria importanza per lo sviluppo su larga scala

### API Sling {#sling-api}

Utilizza il pacchetto API Sling, `org.apache.sling.*`, e le librerie tag.

### Riferimento a elementi esistenti tramite sling:include {#referencing-existing-elements-using-sling-include}

Un&#39;ultima considerazione è la necessità di fare riferimento agli elementi esistenti all&#39;interno degli script.

Gli script più complessi (aggregazione di script) accedono a più risorse (ad esempio, navigazione, barra laterale, piè di pagina, elementi di un elenco), includendo la *risorsa*.

In questo caso, è possibile utilizzare il comando `sling:include("/<path>/<resource>")`. Include effettivamente la definizione della risorsa di riferimento.

## OSGi {#osgi}

OSGi (Open Services Gateway Initiative) definisce un&#39;architettura per lo sviluppo e la distribuzione di librerie e applicazioni modulari (nota anche come Dynamic Module System per Java™). I contenitori OSGi ti consentono di suddividere l’applicazione in singoli moduli (file jar con metadati aggiuntivi e denominati bundle nella terminologia OSGi) e di gestire le dipendenze incrociate tra di essi con:

* Servizi implementati nel contenitore
* Un contratto tra il contenitore e l’applicazione

Questi servizi e contratti forniscono un’architettura che consente ai singoli elementi di scoprirsi dinamicamente a vicenda per collaborare.

Un framework OSGi offre quindi operazioni dinamiche di caricamento/scaricamento, configurazione e controllo di questi bundle, senza richiedere riavvii.

>[!NOTE]
>
>Per informazioni complete sulla tecnologia OSGi, visita il [sito Web OSGi](https://www.osgi.org).
>
>In particolare, la pagina Istruzione di base contiene una raccolta di presentazioni e tutorial.

Questa architettura consente di estendere Sling con moduli specifici per le applicazioni. Sling, e quindi AEM, utilizza l&#39;implementazione [Apache Felix](https://felix.apache.org/documentation/index.html) di OSGi. Sono entrambe raccolte di bundle OSGi in esecuzione all’interno di un framework OSGi.

Questa funzionalità consente di eseguire le azioni seguenti su uno qualsiasi dei pacchetti all’interno dell’installazione:

* Installa
* Inizia
* Interrompi
* Aggiornare
* Disinstalla
* Vedi lo stato più recente
* Accedi a informazioni più dettagliate su bundle specifici, ad esempio nome simbolico, versione e posizione

Per ulteriori informazioni, vedere [Configurazione di OSGi per AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md).

## Struttura all’interno del repository {#structure-within-the-repository}

L’elenco seguente offre una panoramica della struttura visualizzata all’interno dell’archivio.

* `/apps` - Relativo all&#39;applicazione; include definizioni di componenti specifiche del sito Web. I componenti sviluppati possono essere basati sui componenti predefiniti disponibili in `/libs/core/wcm/components`.
* `/content` - Contenuto creato per il sito Web.
* `/etc`
* `/home` - Informazioni utente e gruppo.
* `/libs` - Librerie e definizioni che appartengono al nucleo di AEM. Le sottocartelle in `/libs` rappresentano le funzionalità predefinite di AEM. Impossibile modificare il contenuto in `/libs`. Le funzionalità specifiche del sito Web devono essere effettuate in `/apps`.
* `/tmp` - Area di lavoro temporanea.
* `/var` - File che vengono modificati e aggiornati dal sistema, ad esempio registri di controllo, statistiche e gestione degli eventi.

>[!CAUTION]
>
>Le modifiche a questa struttura, o ai file al suo interno, devono essere effettuate con cautela. Assicurati di comprendere appieno le implicazioni di eventuali modifiche apportate.
>
>Non modificare nulla nel percorso `/libs`. Per la configurazione e altre modifiche, copiare l&#39;elemento da `/libs` a `/apps` e apportare eventuali modifiche entro `/apps`.
