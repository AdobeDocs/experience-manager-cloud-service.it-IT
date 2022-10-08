---
title: Fondamenti tecnici AEM
description: Una panoramica delle fondamenta tecniche di AEM, tra cui il modo in cui AEM è strutturato e tecnologie fondamentali come JCR, Sling e OSGi.
exl-id: ab6e7fe9-a25d-4351-a005-f4466cc0f40e
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '2191'
ht-degree: 1%

---

# Fondamenti tecnici AEM {#aem-technical-foundations}

AEM è una piattaforma solida basata su tecnologie collaudate, scalabili e flessibili. Questo documento fornisce una panoramica dettagliata delle varie parti che compongono AEM ed è inteso come appendice tecnica per uno sviluppatore AEM pieno stack. Non è inteso come guida introduttiva. Se hai poca esperienza nello sviluppo AEM, consulta la [Guida introduttiva allo sviluppo per AEM Sites - Tutorial WKND](develop-wknd-tutorial.md) come primo passo.

>[!TIP]
>
>Prima di immergersi nelle tecnologie di base di AEM, Adobe consiglia di completare la [Guida introduttiva allo sviluppo per AEM Sites - Tutorial WKND.](develop-wknd-tutorial.md)

## Nozioni fondamentali {#fundamentals}

In qualità di moderno sistema di gestione dei contenuti, AEM si basa sulle tecnologie web standard:

* Ciclo request-response (XMLHttpRequest / XMLHttpResponse)
* HTML
* CSS
* JavaScript

L’archivio dei contenuti sottostante e i livelli di logica di business sono costruiti intorno alle tecnologie Java:

* JCR
* Sling
* OSGi

## Archivio dei contenuti Java {#java-content-repository}

Lo standard Java Content Repository (JCR), [JSR 283](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/index.html), specifica un modo indipendente dal fornitore e indipendente dall’implementazione per accedere al contenuto in modo bidirezionale a un livello granulare all’interno di un archivio di contenuti. Il lead di specificazione è detenuto da Adobe Research (Switzerland) AG.

La [API JCR 2.0](https://www.adobe.io/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) pacchetto, `javax.jcr.*` viene utilizzato per l’accesso diretto e la manipolazione del contenuto dell’archivio.

AEM è basato su un JCR.

## Apache Jackrabbit Oak {#jackrabbit-oak}

[Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/) è un’implementazione di un archivio di contenuti gerarchici scalabile e ad alte prestazioni da utilizzare come base dei siti web moderni di livello mondiale e di altre applicazioni di contenuti esigenti, in conformità allo standard JCR.

Jackrabbit Oak (detto anche semplicemente come Oak), è l&#39;implementazione dello standard JCR su cui viene costruito AEM.

## Elaborazione delle richieste Sling {#sling-request-processing}

AEM viene generato utilizzando [Sling](https://sling.apache.org/site/index.html), un framework di applicazione web basato su principi REST che fornisce un facile sviluppo di applicazioni orientate ai contenuti. Sling utilizza un archivio JCR, come Apache Jackrabbit Oak, come archivio dati. Sling è stato contribuito a Apache Software Foundation - ulteriori informazioni sono disponibili su Apache.

### Introduzione a Sling {#introduction-to-sling}

Utilizzando Sling, il tipo di contenuto di cui eseguire il rendering non è il primo aspetto di elaborazione. La considerazione principale è se l’URL viene risolto in un oggetto di contenuto per il quale è quindi possibile trovare uno script per eseguire il rendering. Questo offre un supporto eccellente agli autori di contenuti web per creare pagine facilmente personalizzate in base alle loro esigenze.

I vantaggi di questa flessibilità sono evidenti nelle applicazioni con una vasta gamma di elementi di contenuto diversi, o quando è necessario personalizzare pagine facilmente. In particolare, quando si implementa un sistema di gestione dei contenuti web come AEM.

Vedi [Scopri Sling in 15 minuti](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) per i primi passi per lo sviluppo con Sling.

Il diagramma seguente spiega la risoluzione dello script Sling: mostra come passare dalla richiesta HTTP al nodo del contenuto, dal nodo del contenuto al tipo di risorsa, dal tipo di risorsa allo script e quali variabili di script sono disponibili.

![Comprensione della risoluzione degli script Apache Sling](assets/sling-cheatsheet-01.png)

Il diagramma seguente illustra tutti i parametri di richiesta nascosti ma potenti che è possibile utilizzare per gestire `SlingPostServlet`, il gestore predefinito per tutte le richieste POST che offre infinite opzioni per creare, modificare, eliminare, copiare e spostare i nodi nell’archivio.

![Utilizzo di SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling è incentrato sul contenuto {#sling-is-content-centric}

Sling è *incentrato sul contenuto*. Ciò significa che l’elaborazione è incentrata sul contenuto, in quanto ogni richiesta (HTTP) viene mappata sul contenuto sotto forma di una risorsa JCR (un nodo di archivio):

* Il primo target è la risorsa (nodo JCR) che contiene il contenuto
* In secondo luogo, la rappresentazione, o script, si trova dalle proprietà della risorsa in combinazione con alcune parti della richiesta (ad esempio, selettori e/o estensione)

### Sling RESTful {#restful-sling}

Grazie alla sua filosofia incentrata sui contenuti, Sling implementa un server orientato al REST e quindi presenta un nuovo concetto nei framework delle applicazioni web. I vantaggi sono:

* Molto RESTful, non solo sulla superficie; le risorse e le rappresentazioni vengono modellate correttamente all’interno del server
* Rimuove uno o più modelli di dati
   * Altri framework di gestione dei contenuti potrebbero richiedere struttura URL, oggetti aziendali, schema DB per accedere a una risorsa.
   * Utilizzando Sling, questo viene ridotto a: URL = resource = JCR structure

### Decomposizione URL {#url-decomposition}

In Sling, l&#39;elaborazione è guidata dall&#39;URL della richiesta dell&#39;utente. Definisce il contenuto da visualizzare dagli script appropriati. A questo scopo, le informazioni vengono estratte dall’URL.

Se analizziamo il seguente URL:

```text
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

Possiamo suddividerlo nelle sue parti composite:

| protocollo | host |  | percorso del contenuto | selettori | estensione |  | suffisso |  | param(i) |
|---|---|---|---|---|---|---|---|---|---|
| `https://` | `myhost` | `/` | `tools/spy` | `.printable.a4.` | `html` | `/` | `a/b` | `?` | `x=12` |

* **protocollo** - HTTPS
* **host** - Dominio del sito
* **percorso del contenuto** - Percorso che specifica il contenuto di cui eseguire il rendering e che viene utilizzato in combinazione con l&#39;estensione; in questo esempio si traducono in `tools/spy.html`
* **selettori** - Utilizzato per metodi alternativi di rendering del contenuto; in questo esempio una versione compatibile con la stampante in formato A4
* **estensione** - Formato del contenuto; specifica anche lo script da utilizzare per il rendering
* **suffisso** - Può essere utilizzato per specificare informazioni aggiuntive
* **param(i)** - Qualsiasi parametro richiesto per il contenuto dinamico

#### Da URL a contenuto e script {#from-url-to-content-and-scripts}

Utilizzando i principi di decomposizione URL:

* La mappatura utilizza il percorso del contenuto estratto dalla richiesta per individuare la risorsa.
* Quando si trova la risorsa appropriata, viene estratto il tipo di risorsa sling e utilizzato per individuare lo script da utilizzare per il rendering del contenuto.

La figura seguente illustra il meccanismo utilizzato, che sarà discusso più dettagliatamente nelle sezioni seguenti.

![Meccanismo di mappatura URL](assets/url-mapping.png)

Con Sling, è possibile specificare quale script esegue il rendering di una determinata entità (impostando il `sling:resourceType` nel nodo JCR). Questo meccanismo offre più libertà di una in cui lo script accede alle entità dati (come farebbe un&#39;istruzione SQL in uno script PHP) in quanto una risorsa può avere diverse rappresentazioni.

#### Mappatura delle richieste alle risorse {#mapping-requests-to-resources}

La richiesta è suddivisa ed estrae le informazioni necessarie. Nell’archivio viene eseguita la ricerca della risorsa richiesta (nodo di contenuto):

* Il primo Sling controlla se un nodo esiste nella posizione specificata nella richiesta; ad esempio, `../content/corporate/jobs/developer.html`
* Se non viene trovato alcun nodo, l&#39;estensione viene eliminata e la ricerca viene ripetuta; ad esempio, `../content/corporate/jobs/developer`
* Se non viene trovato alcun nodo, Sling restituirà il codice http 404 (Non trovato).

Sling consente anche di usare risorse diverse dai nodi JCR, ma questa è una funzione avanzata.

### Individuazione dello script {#locating-the-script}

Quando si trova la risorsa appropriata (nodo di contenuto), la **tipo di risorsa sling** viene estratto. Si tratta di un percorso che individua lo script da utilizzare per il rendering del contenuto.

Il percorso specificato dal `sling:resourceType` può essere:

* Assoluto
* Relativo a un parametro di configurazione

>[!TIP]
>
>I percorsi relativi sono consigliati per Adobe in quanto aumentano la portabilità.

Tutti gli script Sling sono memorizzati in sottocartelle di `/apps` (modificabili, script utente) o `/libs` (immutabili, script di sistema), che verranno ricercati in questo ordine.

Alcuni altri punti da sottolineare sono:

* Quando il metodo (GET, POST) è obbligatorio, viene specificato in maiuscolo come in base alle specifiche HTTP, ad esempio: `jobs.POST.esp`
* Sono supportati diversi motori di script, ma gli script comuni consigliati sono HTL e JavaScript.

L&#39;elenco dei motori di script supportati dalla data istanza di AEM è elencato nella console di gestione Felix ( `http://<host>:<port>/system/console/slingscripting`).

Utilizzando l&#39;esempio precedente, se il `sling:resourceType` è `hr/jobs` quindi per:

* Richieste e URL GET/HEAD che terminano con `.html` (tipi di richiesta predefiniti, formato predefinito)
   * Lo script sarà `/apps/hr/jobs/jobs.esp`; l&#39;ultima sezione del `sling:resourceType` forma il nome del file.
* Richieste POST (tutti i tipi di richiesta ad eccezione di GET/HEAD, il nome del metodo deve essere maiuscolo)
   * POST verrà utilizzato nel nome dello script.
   * Lo script sarà `/apps/hr/jobs/jobs.POST.esp`.
* URL in altri formati, senza fine con `.html`
   * Esempio `../content/corporate/jobs/developer.pdf`
   * Lo script sarà `/apps/hr/jobs/jobs.pdf.esp`; il suffisso viene aggiunto al nome dello script.
* URL con selettori
   * I selettori possono essere utilizzati per visualizzare lo stesso contenuto in un formato alternativo. Ad esempio, una versione compatibile con la stampante, un feed rss o un riepilogo.
   * Se si considera una versione adatta alla stampante, il selettore potrebbe essere `print`; come in `../content/corporate/jobs/developer.print.html`
   * Lo script sarà `/apps/hr/jobs/jobs.print.esp`; il selettore viene aggiunto al nome dello script.
* Se no `sling:resourceType` è stato definito in seguito:
   * Il percorso del contenuto verrà utilizzato per cercare uno script appropriato (se basato sul percorso `ResourceTypeProvider` è attivo).
   * Ad esempio, lo script per `../content/corporate/jobs/developer.html` genererebbe una ricerca in `/apps/content/corporate/jobs/`.
   * Verrà utilizzato il tipo di nodo principale.
* Se non viene trovato alcuno script, verrà utilizzato lo script predefinito.
   * Il rendering predefinito è attualmente supportato come testo normale (`.txt`), HTML (`.html`) e JSON (`.json`), che elenca tutte le proprietà del nodo (formattate in modo appropriato). Rendering predefinito dell&#39;estensione `.res`, o richieste senza estensione di richiesta, per spool la risorsa (dove possibile).
* Per la gestione degli errori http (codici 403 o 404) Sling cerca uno script in:
   * La posizione `/apps/sling/servlet/errorhandler` per script personalizzati
   * Oppure la posizione dello script standard `/libs/sling/servlet/errorhandler/404.jsp`

Se per una determinata richiesta sono validi più script, viene selezionato lo script con la migliore corrispondenza. Più una partita è specifica, meglio è. in altre parole, più il selettore corrisponde meglio, indipendentemente da eventuali estensioni di richiesta o dalla corrispondenza del nome del metodo.

Ad esempio, considera una richiesta per accedere alla risorsa

* `/content/corporate/jobs/developer.print.a4.html`

di tipo

* `sling:resourceType="hr/jobs"`

Presupponendo che il seguente elenco di script sia nella posizione corretta:

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

Quindi l&#39;ordine di preferenza sarebbe (8) - (7) - (6) - (5) - (4) - (3) - (2) - (1).

Oltre ai tipi di risorse (definiti principalmente da `sling:resourceType` (proprietà) esiste anche il super tipo di risorsa. Questo è generalmente indicato dal `sling:resourceSuperType` proprietà. Questi super tipi vengono considerati anche quando si cerca di trovare uno script. I super tipi di risorse consentono di creare una gerarchia di risorse in cui il tipo di risorsa predefinito `sling/servlet/default` (utilizzato dai servlet predefiniti) è effettivamente la radice.

Il super tipo di risorsa può essere definito in due modi:

* dal `sling:resourceSuperType` della risorsa.
* dal `sling:resourceSuperType` proprietà del nodo a cui `sling:resourceType` punti.

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
   * Is `[ c, b, a, <default>]`
* Mentre per `/y`
   * La gerarchia è `[ c, a, <default>]`

Questo perché `/y` ha `sling:resourceSuperType` proprietà considerando `/x` non e quindi il relativo supertipo viene prelevato dal relativo tipo di risorsa.

#### Gli Script Sling Non Possono Essere Chiamati Direttamente {#sling-scripts-cannot-be-called-directly}

All’interno di Sling, gli script non possono essere chiamati direttamente in quanto ciò violerebbe il concetto rigoroso di server REST; puoi combinare risorse e rappresentazioni.

Se chiami direttamente la rappresentazione (lo script), nascondi la risorsa all’interno dello script, in modo che il framework (Sling) non ne sia più a conoscenza. Così si perdono alcune caratteristiche:

* Gestione automatica dei metodi http diversi da GET, compresi:
   * POST, PUT, DELETE che vengono gestiti con un’implementazione predefinita sling
   * La `POST.jsp` script nel `sling:resourceType` posizione
* L&#39;architettura del codice non è più pulita né strutturata come dovrebbe; di importanza primaria per lo sviluppo su larga scala

### API Sling {#sling-api}

Questo utilizza il pacchetto API Sling, `org.apache.sling.*`e le librerie di tag.

### Riferimento a elementi esistenti utilizzando sling:include {#referencing-existing-elements-using-sling-include}

Una considerazione finale è la necessità di fare riferimento agli elementi esistenti all&#39;interno degli script.

Gli script più complessi (aggregazione degli script) potrebbero dover accedere a più risorse (ad esempio navigazione, barra laterale, piè di pagina, elementi di un elenco) e farlo includendo *risorsa*.

A questo scopo, puoi utilizzare la `sling:include("/<path>/<resource>")` comando. Ciò includerà in modo efficace la definizione della risorsa a cui si fa riferimento.

## OSGi {#osgi}

OSGi (Open Services Gateway Initiative) definisce un&#39;architettura per lo sviluppo e la distribuzione di applicazioni e librerie modulari (nota anche come Dynamic Module System for Java). I contenitori OSGi ti consentono di suddividere l’applicazione in singoli moduli (sono file jar con metadati aggiuntivi e chiamati bundle nella terminologia OSGi) e di gestire le dipendenze trasversali tra di loro con:

* Servizi implementati all’interno del contenitore
* Un contratto tra il contenitore e l’applicazione

Questi servizi e contratti offrono un&#39;architettura che consente ai singoli elementi di scoprirsi l&#39;un l&#39;altro in modo dinamico per la collaborazione.

Un framework OSGi ti offre quindi il caricamento/scaricamento dinamico, la configurazione e il controllo di questi bundle, senza dover riavviare.

>[!NOTE]
>
>Informazioni complete sulla tecnologia OSGi sono disponibili all&#39;indirizzo [Sito web OSGi](https://www.osgi.org).
>
>In particolare, la pagina Basic Education contiene una raccolta di presentazioni ed esercitazioni.

Questa architettura consente di estendere Sling con moduli specifici per le applicazioni. Sling, e quindi AEM, utilizza il [Apache Felix](https://felix.apache.org/) implementazione di OSGi. Sono entrambe raccolte di bundle OSGi in esecuzione all&#39;interno di un framework OSGi.

Questo consente di eseguire le seguenti azioni su uno qualsiasi dei pacchetti all’interno dell’installazione:

* Installare la versione
* Avvia
* Arresta
* Aggiorna
* Disinstalla
* Vedi lo stato corrente
* Accedi a informazioni più dettagliate (ad esempio, nome simbolico, versione, posizione, ecc.) sui bundle specifici

Vedi [Configurazione di OSGi per AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md) per ulteriori informazioni.

## Struttura all’interno dell’archivio {#structure-within-the-repository}

L’elenco seguente fornisce una panoramica della struttura che verrà visualizzata all’interno dell’archivio.

* `/apps` - Applicazione correlata; include definizioni di componenti specifiche del sito web. I componenti sviluppati possono essere basati sui componenti predefiniti disponibili in `/libs/core/wcm/components`.
* `/content` - Contenuto creato per il sito web.
* `/etc`
* `/home` - Informazioni utente e gruppo.
* `/libs` - Librerie e definizioni che appartengono al nucleo di AEM. Le sottocartelle in `/libs` rappresentano le funzionalità predefinite AEM. Contenuto `/libs` non possono essere modificate. Le funzionalità specifiche del tuo sito web devono essere create in `/apps`.
* `/tmp` - Area di lavoro temporanea.
* `/var` - i file che cambiano e vengono aggiornati dal sistema; come i registri di controllo, le statistiche, la gestione degli eventi.

>[!CAUTION]
>
>Le modifiche a questa struttura, o ai relativi file, devono essere effettuate con attenzione. Assicurati di comprendere appieno le implicazioni di eventuali modifiche apportate.
>
>Non devi cambiare nulla nel `/libs` percorso. Per la configurazione e altre modifiche, copia l’elemento da `/libs` a `/apps` e apporta eventuali modifiche all&#39;interno di `/apps`.
