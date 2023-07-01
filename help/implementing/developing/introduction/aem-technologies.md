---
title: Fondamenti tecnici AEM
description: Una panoramica delle basi tecniche dell’AEM, compreso il modo in cui l’AEM è strutturato e le tecnologie fondamentali come JCR, Sling e OSGi.
exl-id: ab6e7fe9-a25d-4351-a005-f4466cc0f40e
source-git-commit: a01583483fa89f89b60277c2ce4e1c440590e96c
workflow-type: tm+mt
source-wordcount: '2144'
ht-degree: 1%

---

# Fondamenti tecnici AEM {#aem-technical-foundations}

AEM è una piattaforma solida basata su tecnologie collaudate, scalabili e flessibili. Questo documento offre una panoramica dettagliata delle varie parti che compongono l&#39;AEM ed è concepito come un&#39;appendice tecnica per uno sviluppatore AEM full stack. Non è concepito come guida introduttiva. Se non ha ancora sviluppato l’AEM, consulti [Guida introduttiva allo sviluppo per AEM Sites - Tutorial WKND](develop-wknd-tutorial.md) come primo passo.

>[!TIP]
>
>Prima di immergerti nelle tecnologie di base dell’AEM, Adobe consiglia di completare [Guida introduttiva allo sviluppo per AEM Sites: esercitazione WKND.](develop-wknd-tutorial.md)

## Nozioni di base {#fundamentals}

In quanto sistema moderno di gestione dei contenuti, l’AEM si basa sulle tecnologie web standard:

* Ciclo richiesta-risposta (XMLHttpRequest / XMLHttpResponse)
* HTML
* CSS
* JavaScript

I livelli dell’archivio dei contenuti e della logica di business sottostanti sono basati sulle tecnologie Java™:

* JCR
* Sling
* OSGi

## Archivio dei contenuti Java™ {#java-content-repository}

Lo standard Java™ Content Repository (JCR), [JSR 283](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html)specifica un modo indipendente dal fornitore e indipendente dall’implementazione per accedere al contenuto in modo bidirezionale a livello granulare all’interno di un archivio di contenuti. Il lead della specifica è detenuto da Adobe Research (Switzerland) AG.

Il [API JCR 2.0](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) imballaggio, `javax.jcr.*` viene utilizzato per l’accesso diretto e la manipolazione del contenuto dell’archivio.

L’AEM si basa su un JCR.

## Apache Jackrabbit Oak {#jackrabbit-oak}

[Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/) è un’implementazione di un archivio di contenuti gerarchico scalabile e ad alte prestazioni da utilizzare come base per siti web moderni e altre applicazioni di contenuti complesse, conforme allo standard JCR.

Jackrabbit Oak (noto anche semplicemente come Oak), è l&#39;implementazione dello standard JCR su cui si basa l&#39;AEM.

## Elaborazione richiesta Sling {#sling-request-processing}

L’AEM viene creato utilizzando [Sling](https://sling.apache.org/index.html): framework di applicazioni web basato sui principi REST che consente di sviluppare facilmente applicazioni orientate ai contenuti. Sling utilizza un archivio JCR, come Apache Jackrabbit Oak, come archivio dati. Sling ha contribuito alla Apache Software Foundation; ulteriori informazioni sono disponibili su Apache.

### Introduzione a Sling {#introduction-to-sling}

Utilizzando Sling, il tipo di contenuto di cui eseguire il rendering non è la prima considerazione di elaborazione. Al contrario, la considerazione principale è se l’URL si risolve in un oggetto di contenuto per il quale è possibile trovare uno script per eseguire il rendering. Questo processo fornisce un supporto eccellente agli autori di contenuti web per creare pagine facilmente personalizzate in base alle loro esigenze.

I vantaggi di questa flessibilità sono evidenti nelle applicazioni con un’ampia gamma di elementi di contenuto diversi o quando servono pagine facilmente personalizzabili. In particolare, quando si implementa un sistema di gestione dei contenuti web come AEM.

Consulta [Scopri Sling in 15 minuti](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) per i primi passaggi per lo sviluppo con Sling.

Il diagramma seguente spiega la risoluzione dello script Sling. Mostra come passare dalla richiesta HTTP al nodo di contenuto, dal nodo di contenuto al tipo di risorsa, dal tipo di risorsa allo script e quali variabili di script sono disponibili.

![Informazioni sulla risoluzione dello script Apache Sling](assets/sling-cheatsheet-01.png)

Il diagramma seguente illustra i parametri di richiesta nascosti ma potenti che è possibile utilizzare con `SlingPostServlet`, gestore predefinito per tutte le richieste POST. Il gestore offre opzioni infinite per la creazione, la modifica, l’eliminazione, la copia e lo spostamento di nodi nell’archivio.

![Utilizzo di SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling è incentrato sui contenuti {#sling-is-content-centric}

Sling è *incentrato sui contenuti*. Ciò significa che l’elaborazione si concentra sul contenuto, in quanto ogni richiesta (HTTP) è mappata sul contenuto sotto forma di risorsa JCR (un nodo dell’archivio):

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
* **percorso contenuto** : percorso che specifica il contenuto di cui eseguire il rendering e che viene utilizzato con l’estensione. In questo esempio, si traduce in `tools/spy.html`
* **selettori** : utilizzato per metodi alternativi di rendering del contenuto; in questo esempio, una versione di formato A4 compatibile con la stampante
* **estensione** - Formato del contenuto; specifica anche lo script da utilizzare per il rendering
* **suffisso** - Può essere utilizzato per specificare informazioni aggiuntive
* **parametri** - Qualsiasi parametro richiesto per il contenuto dinamico

#### Da URL a contenuto e script {#from-url-to-content-and-scripts}

Utilizzo dei principi di decomposizione degli URL:

* La mappatura utilizza il percorso del contenuto estratto dalla richiesta per individuare la risorsa.
* Quando si trova la risorsa appropriata, il tipo di risorsa sling viene estratto e utilizzato per individuare lo script da utilizzare per il rendering del contenuto.

La figura riportata di seguito illustra il meccanismo utilizzato, descritto più dettagliatamente nelle sezioni seguenti.

![Meccanismo di mappatura URL](assets/url-mapping.png)

Con Sling, puoi specificare quale script esegue il rendering di una determinata entità (impostando il `sling:resourceType` nel nodo JCR. Questo meccanismo offre maggiore libertà rispetto a uno in cui lo script accede alle entità di dati (come farebbe un’istruzione SQL in uno script PHP) in quanto una risorsa può avere diverse rappresentazioni.

#### Mappatura delle richieste alle risorse {#mapping-requests-to-resources}

La richiesta è suddivisa ed è possibile estrarre le informazioni necessarie. Nell’archivio viene eseguita la ricerca della risorsa richiesta (nodo del contenuto):

* First Sling controlla se un nodo esiste nella posizione specificata nella richiesta; ad esempio, `../content/corporate/jobs/developer.html`
* Se non viene trovato alcun nodo, l’estensione viene rilasciata e la ricerca ripetuta; ad esempio, `../content/corporate/jobs/developer`
* Se non viene trovato alcun nodo, Sling restituisce il codice http 404 (Not Found).

Sling consente anche di utilizzare come risorse elementi diversi dai nodi JCR, ma questa funzionalità è avanzata.

### Individuazione dello script {#locating-the-script}

Quando si trova la risorsa appropriata (nodo di contenuto), il **tipo di risorsa sling** viene estratto. Questo percorso individua lo script da utilizzare per il rendering del contenuto.

Percorso specificato da `sling:resourceType` può essere:

* Assoluto
* Relativo a un parametro di configurazione

>[!TIP]
>
>I percorsi relativi sono consigliati da Adobe in quanto aumentano la portabilità.

Tutti gli script Sling vengono memorizzati nelle sottocartelle di `/apps` (mutable, user scripts) o `/libs` (immutabile, script di sistema), che viene ricercato in questo ordine.

Altri punti da notare sono:

* Quando il metodo (GET, POST) è obbligatorio, viene specificato in maiuscolo, ad esempio in base alla specifica HTTP. `jobs.POST.esp`
* Sono supportati vari motori di script, ma gli script comuni e consigliati sono HTL e JavaScript.

L&#39;elenco dei motori di script supportati dall&#39;istanza di AEM specificata è elencato nella console di gestione Felix ( `http://<host>:<port>/system/console/slingscripting`).

Utilizzando l&#39;esempio precedente, se `sling:resourceType` è `hr/jobs` quindi per:

* Richieste GET/HEAD e URL che terminano con `.html` (tipi di richiesta predefiniti, formato predefinito)
   * Lo script è `/apps/hr/jobs/jobs.esp`; l&#39;ultima sezione del `sling:resourceType` forma il nome del file.
* Richieste POST (tutti i tipi di richiesta tranne GET/HEAD, il nome del metodo deve essere in maiuscolo)
   * POST viene utilizzato nel nome dello script.
   * Lo script è `/apps/hr/jobs/jobs.POST.esp`.
* URL in altri formati, che non terminano con `.html`
   * Ad esempio `../content/corporate/jobs/developer.pdf`
   * Lo script è `/apps/hr/jobs/jobs.pdf.esp`; il suffisso viene aggiunto al nome dello script.
* URL con selettori
   * I selettori possono essere utilizzati per visualizzare lo stesso contenuto in un formato alternativo. Ad esempio, una versione compatibile con la stampante, un feed rss o un riepilogo.
   * Se si considera una versione compatibile con la stampante in cui il selettore potrebbe essere `print`; come in `../content/corporate/jobs/developer.print.html`
   * Lo script è `/apps/hr/jobs/jobs.print.esp`; il selettore viene aggiunto al nome dello script.
* In caso negativo, `sling:resourceType` è definito quindi:
   * Il percorso del contenuto viene utilizzato per cercare uno script appropriato (se il `ResourceTypeProvider` è attivo).
   * Ad esempio, lo script per `../content/corporate/jobs/developer.html` genera una ricerca in `/apps/content/corporate/jobs/`.
   * Viene utilizzato il tipo di nodo principale.
* Se non viene trovato alcuno script, viene utilizzato lo script predefinito.
   * La rappresentazione predefinita è supportata come testo normale (`.txt`), HTML (`.html`), e JSON (`.json`), che elenca tutte le proprietà del nodo (formattate in modo appropriato). Rendering predefinito per l’estensione `.res`, o richieste senza estensione di richiesta, consiste nello spool della risorsa (ove possibile).
* Per la gestione degli errori http (codici 403 o 404), Sling cerca uno script in:
   * La posizione `/apps/sling/servlet/errorhandler` per script personalizzati
   * Oppure la posizione dello script standard `/libs/sling/servlet/errorhandler/404.jsp`

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

Oltre ai tipi di risorse (definiti principalmente dalla `sling:resourceType` proprietà ), esiste anche il super tipo di risorsa. Questo tipo è indicato dalla `sling:resourceSuperType` proprietà. Questi super tipi vengono considerati anche quando si tenta di trovare uno script. Il vantaggio dei super-tipi di risorse è che possono formare una gerarchia di risorse in cui il tipo di risorsa predefinito `sling/servlet/default` (utilizzato dai servlet predefiniti) è effettivamente la radice.

Il super tipo di risorsa di una risorsa può essere definito in due modi:

* da `sling:resourceSuperType` della risorsa.
* da `sling:resourceSuperType` proprietà del nodo a cui è associato `sling:resourceType` punti.

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

Il motivo è perché `/y` ha `sling:resourceSuperType` proprietà, mentre `/x` does not e pertanto il relativo supertipo viene preso dal relativo tipo di risorsa.

#### Gli script Sling non possono essere chiamati direttamente {#sling-scripts-cannot-be-called-directly}

All’interno di Sling, gli script non possono essere chiamati direttamente perché violerebbero il concetto rigoroso di server REST; è possibile combinare risorse e rappresentazioni.

Se chiami direttamente la rappresentazione (lo script), nascondi la risorsa all’interno dello script, pertanto il framework (Sling) non ne è più a conoscenza. In questo modo si perdono alcune funzionalità:

* Gestione automatica di metodi http diversi da GET, tra cui:
   * POST, PUT, DELETE gestito con un’implementazione sling predefinita
   * Il `POST.jsp` script nel tuo `sling:resourceType` posizione
* L&#39;architettura del codice non è più pulita né strutturata in modo chiaro come dovrebbe essere; di primaria importanza per lo sviluppo su larga scala

### API Sling {#sling-api}

Utilizza il pacchetto API di Sling, `org.apache.sling.*`, e le librerie di tag.

### Riferimento a elementi esistenti mediante sling:include {#referencing-existing-elements-using-sling-include}

Un&#39;ultima considerazione è la necessità di fare riferimento agli elementi esistenti all&#39;interno degli script.

Gli script più complessi (aggregazione di script) accedono a più risorse (ad esempio navigazione, barra laterale, piè di pagina, elementi di un elenco) e includono *resource*.

In questo caso, puoi utilizzare `sling:include("/<path>/<resource>")` comando. Include effettivamente la definizione della risorsa di riferimento.

## OSGi {#osgi}

OSGi (Open Services Gateway Initiative) definisce un&#39;architettura per lo sviluppo e la distribuzione di librerie e applicazioni modulari (nota anche come Dynamic Module System per Java™). I contenitori OSGi ti consentono di suddividere l’applicazione in singoli moduli (file jar con metadati aggiuntivi e denominati bundle nella terminologia OSGi) e di gestire le dipendenze incrociate tra di essi con:

* Servizi implementati nel contenitore
* Un contratto tra il contenitore e l’applicazione

Questi servizi e contratti forniscono un’architettura che consente ai singoli elementi di scoprirsi dinamicamente a vicenda per collaborare.

Un framework OSGi offre quindi operazioni dinamiche di caricamento/scaricamento, configurazione e controllo di questi bundle, senza richiedere riavvii.

>[!NOTE]
>
>Per informazioni complete sulla tecnologia OSGi, visitare il sito [Sito Web OSGi](https://www.osgi.org).
>
>In particolare, la pagina Istruzione di base contiene una raccolta di presentazioni e tutorial.

Questa architettura consente di estendere Sling con moduli specifici per le applicazioni. Sling, e quindi AEM, utilizza [Apache Felix](https://felix.apache.org/documentation/index.html) implementazione di OSGi. Sono entrambe raccolte di bundle OSGi in esecuzione all’interno di un framework OSGi.

Questa funzionalità consente di eseguire le azioni seguenti su uno qualsiasi dei pacchetti all’interno dell’installazione:

* Installa
* Avvia
* Arresta
* Aggiornare
* Disinstalla
* Vedi lo stato più recente
* Accedi a informazioni più dettagliate su bundle specifici, ad esempio nome simbolico, versione e posizione

Consulta [Configurazione di OSGi per AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md) per ulteriori informazioni.

## Struttura all’interno del repository {#structure-within-the-repository}

L’elenco seguente offre una panoramica della struttura visualizzata all’interno dell’archivio.

* `/apps` - Relativo all’applicazione; include le definizioni dei componenti specifiche del sito web. I componenti sviluppati possono essere basati sui componenti predefiniti disponibili all’indirizzo `/libs/core/wcm/components`.
* `/content` - Contenuto creato per il sito web.
* `/etc`
* `/home` - Informazioni su utenti e gruppi.
* `/libs` - le biblioteche e le definizioni che appartengono al nucleo centrale dell&#39;AEM. Le sottocartelle in `/libs` rappresenta le funzioni predefinite dell’AEM. Il contenuto in `/libs` non può essere modificato. Le funzioni specifiche del sito web devono essere effettuate in `/apps`.
* `/tmp` - Area di lavoro temporanea.
* `/var` - File che vengono modificati e aggiornati dal sistema, ad esempio registri di audit, statistiche e gestione degli eventi.

>[!CAUTION]
>
>Le modifiche a questa struttura, o ai file al suo interno, devono essere effettuate con cautela. Assicurati di comprendere appieno le implicazioni di eventuali modifiche apportate.
>
>Non modificare nulla nella `/libs` percorso. Per la configurazione e altre modifiche, copia l’elemento da `/libs` a `/apps` e apporta le modifiche necessarie entro `/apps`.
