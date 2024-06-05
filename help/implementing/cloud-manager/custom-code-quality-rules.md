---
title: Regole per la qualità del codice personalizzato
description: Questa pagina descrive le regole per la qualità del codice personalizzato eseguite da Cloud Manager come parte del test di qualità del codice. Si basano sulle best practice dei team tecnici di Adobe Experience Manager.
exl-id: f40e5774-c76b-4c84-9d14-8e40ee6b775b
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '4167'
ht-degree: 87%

---

# Regole per la qualità del codice personalizzato {#custom-code-quality-rules}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_customcodequalityrules"
>title="Regole per la qualità del codice personalizzato"
>abstract="Questa pagina descrive le regole per la qualità del codice personalizzato eseguite da Cloud Manager come parte del test di qualità del codice. Si basano sulle best practice dei team tecnici di Adobe Experience Manager."

Questa pagina descrive le regole per la qualità del codice personalizzato eseguite da Cloud Manager come parte del [test di qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md). Si basano sulle best practice dei team tecnici di Experience Manager.

>[!NOTE]
>
>Le regole SonarQube complete non sono disponibili per il download a causa di informazioni proprietarie Adobe. È possibile scaricare l’elenco completo delle regole [utilizzando questo collegamento](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS.xlsx). Continua a leggere questo documento per descrizioni ed esempi delle regole.

>[!NOTE]
>
>Gli esempi di codice qui forniti sono esclusivamente a scopo illustrativo. Per informazioni sui concetti e le regole di qualità di SonarQube, consulta la [Documentazione sui concetti](https://docs.sonarqube.org/latest/) di SonarQube.

## Regole di SonarQube {#sonarqube-rules}

La sezione seguente descrive le regole di SonarQube eseguite da Cloud Manager.

### Non utilizzare funzioni potenzialmente pericolose {#do-not-use-potentially-dangerous-functions}

* **Chiave**: CQRules:CWE-676
* **Tipo**: vulnerabilità
* **Gravità**: importante
* **Da**: versione 2018.4.0

I metodi `Thread.stop()` e `Thread.interrupt()` possono generare problemi difficili da riprodurre e, in alcuni casi, vulnerabilità di sicurezza. Il loro utilizzo deve essere controllato e convalidato. In generale, il passaggio di messaggi è un modo più sicuro per raggiungere obiettivi simili.

#### Codice non conforme {#non-compliant-code}

```java
public class DontDoThis implements Runnable {
  private Thread thread;
 
  public void start() {
    thread = new Thread(this);
    thread.start();
  }
 
  public void stop() {
    thread.stop();  // UNSAFE!
  }
 
  public void run() {
    while (true) {
        somethingWhichTakesAWhileToDo();
    }
  }
}
```

#### Codice conforme {#compliant-code}

```java
public class DoThis implements Runnable {
  private Thread thread;
  private boolean keepGoing = true;
 
  public void start() {
    thread = new Thread(this);
    thread.start();
  }
 
  public void stop() {
    keepGoing = false;
  }
 
  public void run() {
    while (this.keepGoing) {
        somethingWhichTakesAWhileToDo();
    }
  }
}
```

### Non utilizzare stringhe di formato che possono essere controllate esternamente {#do-not-use-format-strings-which-may-be-externally-controlled}

* **Chiave**: CQRules:CWE-134
* **Tipo**: vulnerabilità
* **Gravità**: importante
* **Da**: versione 2018.4.0

L’utilizzo di una stringa di formato da un’origine esterna (come un parametro di richiesta o contenuti generati dall’utente) può esporre un’applicazione ad attacchi DoS. In alcune circostanze una stringa di formato può essere controllata esternamente, ma ciò è consentito solo da fonti attendibili.

#### Codice non conforme {#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text"));
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### Le richieste HTTP devono sempre avere timeout del socket e connessione {#http-requests-should-always-have-socket-and-connect-timeouts}

* **Chiave**: CQRules:ConnectionTimeoutMechanism
* **Tipo**: bug
* **Gravità**: critico
* **Da**: versione 2018.6.0

Durante l’esecuzione di richieste HTTP dall’interno di un’applicazione Experience Manager, è fondamentale assicurarsi che siano configurati timeout appropriati al fine di evitare un consumo di thread inutile. Sfortunatamente, i comportamenti predefiniti di entrambi i client HTTP predefiniti di Java™ (`java.net.HttpUrlConnection`) e il client Apache HTTP Components comunemente utilizzato non si interrompe mai, peranto i timeout devono pertanto essere impostati in modo esplicito. Inoltre, come best practice, questi timeout non devono superare i 60 secondi.

#### Codice non conforme {#non-compliant-code-2}

```java
@Reference
private HttpClientBuilderFactory httpClientBuilderFactory;
 
public void dontDoThis() {
  HttpClientBuilder builder = httpClientBuilderFactory.newBuilder();
  HttpClient httpClient = builder.build();

  // do something with the client
}

public void dontDoThisEither() {
  URL url = new URL("http://www.google.com");
  URLConnection urlConnection = url.openConnection();
 
  BufferedReader in = new BufferedReader(new InputStreamReader(
    urlConnection.getInputStream()));
 
  String inputLine;
  while ((inputLine = in.readLine()) != null) {
    logger.info(inputLine);
  }
 
  in.close();
}
```

#### Codice conforme {#compliant-code-1}

```java
@Reference
private HttpClientBuilderFactory httpClientBuilderFactory;
 
public void doThis() {
  HttpClientBuilder builder = httpClientBuilderFactory.newBuilder();
  RequestConfig requestConfig = RequestConfig.custom()
    .setConnectTimeout(5000)
    .setSocketTimeout(5000)
    .build();
  builder.setDefaultRequestConfig(requestConfig);
 
  HttpClient httpClient = builder.build();
   
  // do something with the client
}

public void orDoThis () {
  URL url = new URL("http://www.google.com");
  URLConnection urlConnection = url.openConnection();
  urlConnection.setConnectTimeout(5000);
  urlConnection.setReadTimeout(5000);
 
  BufferedReader in = new BufferedReader(new InputStreamReader(
    urlConnection.getInputStream()));
 
  String inputLine;
  while ((inputLine = in.readLine()) != null) {
    logger.info(inputLine);
  }
 
  in.close();
}
```

### Chiudere sempre gli oggetti ResourceResolver {#resourceresolver-objects-should-always-be-closed}

* **Chiave**: CQRules:CQBP-72
* **Tipo**: code smell
* **Gravità**: importante
* **Da**: versione 2018.4.0

Gli oggetti `ResourceResolver` ottenuti da `ResourceResolverFactory` consumano risorse di sistema. Sebbene esistano misure per recuperare tali risorse quando un oggetto `ResourceResolver` non è più in uso, è più efficiente chiudere in modo esplicito qualsiasi oggetto `ResourceResolver` aperto con una chiamata al metodo `close()`.

Un equivoco relativamente comune è che gli oggetti `ResourceResolver` creati utilizzando una sessione JCR esistente non devono essere chiusi in modo esplicito, altrimenti la sessione JCR sottostante verrà chiusa. Questo non succede. Indipendentemente da come si apre un oggetto `ResourceResolver`, quando non viene più utilizzato deve essere chiuso. Poiché `ResourceResolver` implementa l’interfaccia `Closeable`, è possibile utilizzare anche la sintassi `try-with-resources` anziché richiamare esplicitamente `close()`.

#### Codice non conforme {#non-compliant-code-4}

```java
public void dontDoThis(Session session) throws Exception {
  ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
  // do some stuff with the resolver
}
```

#### Codice conforme {#compliant-code-2}

```java
public void doThis(Session session) throws Exception {
  ResourceResolver resolver = null;
  try {
    resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
    // do something with the resolver
  } finally {
    if (resolver != null) {
      resolver.close();
    }
  }
}

public void orDoThis(Session session) throws Exception {
  try (ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object) session))){
    // do something with the resolver
  }
}
```

### Non utilizzare i percorsi Sling Servlet per registrare i Servlet {#do-not-use-sling-servlet-paths-to-register-servlets}

* **Chiave**: CQRules:CQBP-75
* **Tipo**: code smell
* **Gravità**: importante
* **Da**: versione 2018.4.0

Come descritto nella [documentazione di Sling](https://sling.apache.org/documentation/the-sling-engine/servlets.html), si sconsiglia di associare i servlet ai percorsi. I servlet associati ai percorsi non possono utilizzare controlli dell’accesso JCR standard e, di conseguenza, richiedono un’ulteriore misura di sicurezza. Anziché utilizzare i servlet associati ai percorsi, si consiglia di creare nodi nell’archivio e di registrare i servlet in base al tipo di risorsa.

#### Codice non conforme {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### Le eccezioni rilevate devono essere registrate o generate, non entrambe {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

* **Chiave**: CQRules:CQBP-44---CatchAndEitherLogOrThrow
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2018.4.0

In generale, un’eccezione deve essere registrata una sola volta. Registrare le eccezioni più volte può causare confusione sul numero di volte che un’eccezione si è verificata. Il modello più comune che porta a questo problema è la registrazione e la generazione di un’eccezione rilevata.

#### Codice non conforme {#non-compliant-code-6}

```java
public void dontDoThis() throws Exception {
  try {
    someOperation();
  } catch (Exception e) {
    logger.error("something went wrong", e);
    throw e;
  }
}
```

#### Codice conforme {#compliant-code-3}

```java
public void doThis() {
  try {
    someOperation();
  } catch (Exception e) {
    logger.error("something went wrong", e);
  }
}

public void orDoThis() throws MyCustomException {
  try {
    someOperation();
  } catch (Exception e) {
    throw new MyCustomException(e);
  }
}
```

### Evitare le istruzioni di registro immediatamente seguite da un’istruzione di generazione {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

* **Chiave**: CQRules:CQBP-44---ConsecutivelyLogAndThrow
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2018.4.0

Un altro modello comune da evitare è registrare un messaggio e generare immediatamente un’eccezione. Questo indica in genere che il messaggio di eccezione verrà duplicato nei file di log.

#### Codice non conforme {#non-compliant-code-7}

```java
public void dontDoThis() throws Exception {
  logger.error("something went wrong");
  throw new RuntimeException("something went wrong");
}
```

#### Codice conforme {#compliant-code-4}

```java
public void doThis() throws Exception {
  throw new RuntimeException("something went wrong");
}
```

### Evita la registrazione a INFO durante la gestione delle richieste GET o HEAD {#avoid-logging-at-info-when-handling-get-or-head-requests}

* **Chiave**: CQRules:CQBP-44---LogInfoInGetOrHeadRequests
* **Tipo**: code smell
* **Gravità**: minore

In generale, il livello di registro INFO deve essere utilizzato per delimitare azioni importanti e, per impostazione predefinita, Experience Manager è configurato per registrare a livello INFO o superiore. I metodi GET e HEAD devono essere sempre di sola lettura e non costituiscono pertanto azioni importanti. È probabile che la registrazione a livello INFO in risposta alle richieste GET o HEAD generi un notevole disturbo nel registro, rendendo così più difficile identificare le informazioni utili nei file di log. La registrazione durante la gestione delle richieste GET o HEAD deve essere a livello WARN o ERROR quando si è verificato un errore o a livello DEBUG o TRACE se è utilie fornire informazioni più approfondite sulla risoluzione dei problemi.

>[!NOTE]
>
>Questo non si applica alle registrazioni del tipo `access.log` per ogni richiesta.

#### Codice non conforme {#non-compliant-code-8}

```java
public void doGet() throws Exception {
  logger.info("handling a request from the user");
}
```

#### Codice conforme {#compliant-code-5}

```java
public void doGet() throws Exception {
  logger.debug("handling a request from the user.");
}
```

### Non utilizzare Exception.getMessage() come primo parametro di un&#39;istruzione di registrazione {#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}

* **Chiave**: CQRules:CQBP-44---ExceptionGetMessageIsFirstLogParam
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2018.4.0

Come best practice, i messaggi del registro devono fornire informazioni contestuali sulla posizione in cui è stata generata un’eccezione nell’applicazione. Mentre il contesto può essere determinato anche tramite l’utilizzo di tracce dello stack, in generale il messaggio di registro sarà più facile da leggere e comprendere. Di conseguenza, quando si registra un’eccezione, non è consigliabile utilizzare il messaggio di eccezione come messaggio di registro. Il messaggio di eccezione contiene la descrizione del problema che si è verificato, mentre il messaggio di registro deve essere utilizzato per comunicare al lettore del registro cosa stava facendo l’applicazione quando si è verificata l’eccezione. Il messaggio di eccezione è comunque registrato. Specificando il messaggio, i registri saranno più facili da comprendere.

#### Codice non conforme {#non-compliant-code-9}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error(e.getMessage(), e);
  }
}
```

#### Codice conforme {#compliant-code-6}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### La registrazione dei blocchi catch deve essere a livello WARN o ERROR {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

* **Chiave**: CQRules:CQBP-44---WrongLogLevelInCatchBlock
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2018.4.0

Come suggerisce il nome, le eccezioni Java™ dovrebbero sempre essere utilizzate in circostanze eccezionali. Di conseguenza, quando viene rilevata un’eccezione, è importante assicurarsi che i messaggi del registro vengano registrati al livello appropriato, WARN o ERROR. In questo modo i messaggi verranno visualizzati correttamente nei registri.

#### Codice non conforme {#non-compliant-code-10}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.debug(e.getMessage(), e);
  }
}
```

#### Codice conforme {#compliant-code-7}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Non stampare le tracce dello stack sulla console {#do-not-print-stack-traces-to-the-console}

* **Chiave**: CQRules:CQBP-44---ExceptionPrintStackTrace
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2018.4.0

Come già menzionato, il contesto è fondamentale per comprendere i messaggi del registro. L’utilizzo di `Exception.printStackTrace()` fa sì che solo la traccia dello stack venga trasmessa al flusso di errore standard, perdendo così tutto il contesto. Inoltre, in un’applicazione multi-thread come Experience Manager, se vengono stampate più eccezioni utilizzando questo metodo in parallelo, le rispettive tracce dello stack possono sovrapporsi e creare confusione. Le eccezioni devono essere registrate solo tramite il framework di registrazione.

#### Codice non conforme {#non-compliant-code-11}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    e.printStackTrace();
  }
}
```

#### Codice conforme {#compliant-code-8}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Non trasmettere a output standard o errore standard {#do-not-output-to-standard-output-or-standard-error}

* **Chiave**: CQRules:CQBP-44—LogLevelConsolePrinters
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2018.4.0

La registrazione ad Experience Manager deve sempre essere effettuata tramite il framework di registrazione (SLF4J). L’output diretto nei flussi di output standard o errore standard perde le informazioni strutturali e contestuali fornite dal framework di registrazione. A volte può causare problemi di prestazioni.

#### Codice non conforme {#non-compliant-code-12}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    System.err.println("Unable to do something");
  }
}
```

#### Codice conforme {#compliant-code-9}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Evitare percorsi /apps e /libs hardcoded {#avoid-hardcoded-apps-and-libs-paths}

* **Chiave**: CQRules:CQBP-71
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2018.4.0

In generale, i percorsi che iniziano con `/libs` e `/apps` non devono essere hardcoded, in quanto i percorsi a cui fanno riferimento sono comunemente archiviati come percorsi relativi al percorso di ricerca di Sling, impostato su `/libs,/apps` per impostazione predefinita. L’utilizzo del percorso assoluto può introdurre difetti di lieve entità che emergeranno solo in un momento successivo del ciclo di vita del progetto.

#### Codice non conforme {#non-compliant-code-13}

```java
public boolean dontDoThis(Resource resource) {
  return resource.isResourceType("/libs/foundation/components/text");
}
```

#### Codice conforme {#compliant-code-10}

```java
public void doThis(Resource resource) {
  return resource.isResourceType("foundation/components/text");
}
```

### Non utilizzare lo Sling Scheduler {#sonarqube-sling-scheduler}

* **Chiave**: CQRules:AMSCORE-554
* **Tipo**: code smell/compatibilità con Cloud Service
* **Gravità**: minore
* **Da**: versione 2020.5.0

Non utilizzare lo Sling Scheduler per le attività che richiedono un’esecuzione garantita. I processi pianificati Sling garantiscono l’esecuzione e sono più adatti per gli ambienti cluster che per quelli non cluster.

Per ulteriori informazioni sulla gestione dei processi Sling in ambienti cluster, consulta [Evento Sling di Apache e Gestione dei processi](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html).

### Non utilizzare API obsolete di Experience Manager {#sonarqube-aem-deprecated}

* **Chiave**: AMSCORE-553
* **Tipo**: code smell/compatibilità con Cloud Service
* **Gravità**: minore
* **Da**: versione 2020.5.0

La superficie dell’API di Experience Manager è soggetta a revisione costante per identificare le API di cui si sconsiglia l’utilizzo e pertanto considerate obsolete.

In molti casi, queste API vengono indicate come obsolete con l’annotazione Java™ standard `@Deprecated` e, in quanto tali, identificate con `squid:CallToDeprecatedMethod`.

Tuttavia, in alcuni casi un’API può essere obsoleta nel contesto di Experience Manager ma non obsoleta in altri contesti. Questa regola identifica questa seconda classe.

### Non utilizzare @Inject’annotazione con @Optional nei modelli Sling {#sonarqube-slingmodels-inject-optional}

* **Chiave**: InjectAnnotationWithOptionalInjectionCheck
* **Tipo**: qualità del software
* **Gravità**: minore
* **Da**: versione 2023.11

Il progetto Apache Sling scoraggia l’utilizzo del `@Inject` nel contesto di modelli Sling, in quanto può causare prestazioni non ottimali se combinata con `DefaultInjectionStrategy.OPTIONAL` a livello di campo o di classe. Invece iniezioni più specifiche (come `@ValueMapValue` o `@OsgiInjector` annotazioni).

Controlla la [Documentazione di Apache Sling](https://sling.apache.org/documentation/bundles/models.html#discouraged-annotations-1) per ulteriori informazioni sulle annotazioni consigliate e sul motivo per cui questo consiglio è stato creato, consulta la sezione.


### Riutilizzare le istanze di un client HTTPC {#sonarqube-reuse-httpclient}

* **Chiave**: AEMSRE-870
* **Tipo**: qualità del software
* **Gravità**: minore
* **Da**: versione 2023.11

Le applicazioni AEM spesso si rivolgono ad altre applicazioni utilizzando il protocollo HTTP e Apache HttpClient è una libreria spesso utilizzata a questo scopo. Tuttavia, la creazione di un oggetto HttpClient comporta un certo sovraccarico, pertanto tali oggetti devono essere riutilizzati il più possibile.

Questa regola controlla che tale oggetto HttpClient non sia privato all&#39;interno di un metodo, ma globale a livello di classe, in modo da poterlo riutilizzare. In questo caso, il campo httpClient deve essere impostato nel costruttore della classe o nel `activate()` (se questa classe è un componente/servizio OSGi).

Controlla la [Guida all’ottimizzazione](https://hc.apache.org/httpclient-legacy/performance.html) di HttpClient per alcune best practice relative all’utilizzo di HttpClient.

#### Codice non conforme {#non-compliant-code-14}

```java
public void doHttpCall() {
  HttpClient httpclient = HttpClients.createDefault();
  // do something with the httpclient
}
```

#### Codice conforme {#compliant-code-11}

```java
public class myClass {

  HttpClient httpclient;

  public void doHttpCall() {
    // do something with the httpclient
  }

}
```

## Regole per i contenuti OakPAL {#oakpal-rules}

Nella sezione seguente sono descritti i controlli OakPAL eseguiti da Cloud Manager.

>[!NOTE]
>
>OakPAL è un framework che convalida i pacchetti di contenuti con un archivio Oak autonomo. È stato sviluppato da un partner Experience Manager e vincitore del premio Experience Manager Rockstar North America 2019.

### Le API di prodotto con notazione @ProviderType non devono essere implementate o estese dai clienti {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

* **Chiave**: CQBP-84
* **Tipo**: bug
* **Gravità**: critico
* **Da**: versione 2018.7.0

L’API di Experience Manager contiene interfacce e classi Java™ che devono essere utilizzate solo con il codice personalizzato, ma che non devono essere implementate. Ad esempio, l’interfaccia `com.day.cq.wcm.api.Page` deve essere attuata solo da Experience Manager.

Quando a queste interfacce vengono aggiunti nuovi metodi, tali metodi aggiuntivi non influiscono sul codice esistente che utilizza queste interfacce. Di conseguenza, l’aggiunta di nuovi metodi a queste interfacce è considerata retrocompatibile. Tuttavia, se il codice personalizzato implementa una di queste interfacce, genera per il cliente un rischio di retrocompatibilità con le versioni precedenti.

Le interfacce e le classi, come implementate da Experience Manager, includono un’annotazione `org.osgi.annotation.versioning.ProviderType` o a volte un’annotazione `aQute.bnd.annotation.ProviderType` legacy simile. Questa regola identifica i casi in cui tale interfaccia viene implementata o in cui una classe viene estesa dal codice personalizzato.

#### Codice non conforme {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### Gli indici Oak Lucene personalizzati devono avere una configurazione Tika {#oakpal-indextikanode}

* **Chiave**: IndexTikaNode
* **Tipo**: bug
* **Gravità**: bloccante
* **Da**: 2021.8.0

Più indici Oak predefiniti in Experience Manager includono una configurazione Tika. Le personalizzazioni di questi indici devono includere una configurazione Tika. Questa regola controlla le personalizzazioni degli indici `damAssetLucene`, `lucene` e `graphqlConfig` e genera un problema se il nodo `tika` risulta mancante o se nel nodo `tika` manca un nodo secondario denominato `config.xml`.

Per ulteriori informazioni sulla personalizzazione delle definizioni dell’indice, consulta [Indicizzazione della documentazione](/help/operations/indexing.md#preparing-the-new-index-definition).

#### Codice non conforme {#non-compliant-code-indextikanode}

```text
+ oak:index
    + damAssetLucene-1-custom
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - tags: [visualSimilaritySearch]
      - type: lucene
```

#### Codice conforme {#compliant-code-indextikanode}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### Gli indici Oak Lucene personalizzati non devono essere sincroni {#oakpal-indexasync}

* **Chiave**: IndexAsyncProperty
* **Tipo**: bug
* **Gravità**: bloccante
* **Da**: 2021.8.0

Gli indici Oak di tipo `lucene` devono essere sempre asincroni. In caso contrario, potrebbe verificarsi un’instabilità del sistema. Per ulteriori informazioni sulla struttura degli indici di tipo Lucene, consulta la [documentazione di Oak.](https://jackrabbit.apache.org/oak/docs/query/lucene.html#index-definition)

#### Codice non conforme {#non-compliant-code-indexasync}

```text
+ oak:index
    + damAssetLucene-1-custom
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - type: lucene
      - tags: [visualSimilaritySearch]
      + tika
        + config.xml
```

#### Codice conforme {#compliant-code-indexasync}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### Gli indici Oak DAM Asset Lucene personalizzati sono strutturati correttamente  {#oakpal-damAssetLucene-sanity-check}

* **Chiave**: IndexDamAssetLucene
* **Tipo**: bug
* **Gravità**: bloccante
* **Da**: 2021.6.0

Affinché la ricerca delle risorse in Experience Manager Assets funzioni correttamente, le personalizzazioni dell’indice Oak `damAssetLucene` devono seguire una serie di linee guida specifiche di questo indice. Questa regola controlla che la definizione dell’indice presenti una proprietà con valori multipli denominata `tags` e contenente il valore `visualSimilaritySearch`.

#### Codice non conforme {#non-compliant-code-damAssetLucene}

```text
+ oak:index
    + damAssetLucene-1-custom
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - type: lucene
      + tika
        + config.xml
```

#### Codice conforme {#compliant-code-damAssetLucene}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### I pacchetti cliente non devono creare o modificare nodi in /libs {#oakpal-customer-package}

* **Chiave**: BannedPath
* **Tipo**: bug
* **Gravità**: critico
* **Da**: versione 2019.6.0

È una best practice consolidata da tempo che la struttura del contenuto `/libs` nell’archivio dei contenuti Experience Manager debba essere considerata di sola lettura per i clienti. Modificare nodi e proprietà in `/libs` crea rischi significativi per gli aggiornamenti principali e secondari. Le modifiche a `/libs` devono essere fatte da Adobe attraverso canali ufficiali.

### I pacchetti non devono contenere duplicati delle configurazioni OSGi {#oakpal-package-osgi}

* **Chiave**: DuplicateOsgiConfigurations
* **Tipo**: bug
* **Gravità**: importante
* **Da**: versione 2019.6.0

Un problema comune che si verifica in progetti complessi è che lo stesso componente OSGi viene configurato più volte. Questo crea un’ambiguità in merito alla configurazione da applicare. Questa regola è “sensibile alla modalità di esecuzione”, in quanto individua solo i problemi in cui lo stesso componente è configurato più volte nella stessa modalità di esecuzione o nella stessa combinazione di modalità di esecuzione.

>[!NOTE]
>
>Questa regola genera problemi in cui la stessa configurazione, nello stesso percorso, è definita in più pacchetti, compresi i casi in cui lo stesso pacchetto viene duplicato nell’elenco complessivo dei pacchetti generati.
>
>Ad esempio, se la build produce pacchetti denominati `com.myco:com.myco.ui.apps` e `com.myco:com.myco.all` dove `com.myco:com.myco.all` incorpora `com.myco:com.myco.ui.apps`, tutte le configurazioni all’interno di `com.myco:com.myco.ui.apps` vengono segnalate come duplicati.
>
>Questo è generalmente un caso in cui non si seguono le [Linee guida per la struttura dei pacchetti di contenuti](/help/implementing/developing/introduction/aem-project-content-package-structure.md). In questo esempio specifico, nel pacchetto `com.myco:com.myco.ui.apps` risulta mancante la proprietà `<cloudManagerTarget>none</cloudManagerTarget>`.

#### Codice non conforme {#non-compliant-code-osgi}

```text
+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### Codice conforme {#compliant-code-osgi}

```text
+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### Le cartelle di configurazione e installazione devono contenere solo nodi OSGi {#oakpal-config-install}

* **Chiave**: ConfigAndInstallShouldOnlyContainOsgiNodes
* **Tipo**: bug
* **Gravità**: importante
* **Da**: versione 2019.6.0

Per motivi di sicurezza, i percorsi contenenti `/config/` e `/install/` sono leggibili solo dagli utenti amministratori in Experience Manager e devono essere utilizzati solo per la configurazione OSGi e i bundle OSGi. Posizionare altri tipi di contenuto in percorsi che contengono questi segmenti determina un comportamento dell’applicazione che comporta un cambio accidentale tra utenti amministratori e non amministratori.

Un problema comune è l’utilizzo di nodi denominati `config` nelle finestre di dialogo dei componenti o quando si specifica la configurazione dell’editor Rich Text per la modifica in linea. Per risolvere questo problema, il nodo che causa la violazione deve essere rinominato con un nome conforme. Per la configurazione del rich text editor, specifica la nuova posizione con la proprietà `configPath` nel nodo `cq:inplaceEditing`.

#### Codice non conforme {#non-compliant-code-config-install}

```text
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    + config [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

#### Codice conforme {#compliant-code-config-install}

```text
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    ./configPath = inplaceEditingConfig (String)
    + inplaceEditingConfig [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

### I pacchetti non devono sovrapporsi {#oakpal-no-overlap}

* **Chiave**: PackageOverlaps
* **Tipo**: bug
* **Gravità**: importante
* **Da**: versione 2019.6.0

Similmente alla [regola I pacchetti non devono contenere duplicati delle configurazioni OSGi,](#oakpal-package-osgi) si tratta di un problema comune nei progetti complessi in cui lo stesso percorso del nodo viene scritto da più pacchetti di contenuti separati. Con i pacchetti di contenuti è possibile utilizzare le dipendenze per garantire un risultato coerente. È preferibile evitare del tutto le sovrapposizioni.

### La modalità di authoring predefinita non deve corrispondere all’interfaccia utente classica {#oakpal-default-authoring}

* **Chiave**: ClassicUIAuthoringMode
* **Tipo**: code smell/compatibilità con Cloud Service
* **Gravità**: minore
* **Da**: versione 2020.5.0

La configurazione OSGi `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` definisce la modalità di authoring predefinita in Experience Manager. Poiché l’interfaccia classica è diventata obsoleta a partire dalla versione 6.4 di Experience Manager, ora viene segnalato un problema se la modalità di authoring predefinita è configurata sull’interfaccia utente classica.

### I componenti con finestre di dialogo devono avere finestre di dialogo dell’interfaccia utente touch {#oakpal-components-dialogs}

* **Chiave**: ComponentWithOnlyClassicUIDialog
* **Tipo**: code smell/compatibilità con Cloud Service
* **Gravità**: minore
* **Da**: versione 2020.5.0

I componenti Experience Manager che dispongono di una finestra di dialogo di interfaccia classica devono sempre avere una finestra di dialogo di interfaccia utente Touch. Entrambi offrono un’esperienza di authoring ottimale e devono essere compatibili con il modello di distribuzione del Cloud Service, dove l’interfaccia utente classica non è supportata. Questa regola verifica i seguenti scenari:

* Un componente con una finestra di dialogo dell’interfaccia classica (ovvero un nodo figlio `dialog`) deve avere una finestra di dialogo corrispondente dell’interfaccia Touch (ovvero un nodo figlio `cq:dialog`).
* Un componente che ha una finestra di dialogo di progettazione per l’interfaccia utente classica (ad es. un nodo `design_dialog`) deve avere anche una finestra di dialogo di progettazione corrispondente per l’interfaccia utente touch (cioè un nodo `cq:design_dialog` secondario).
* Un componente con una finestra di dialogo Interfaccia classica e una finestra di dialogo di progettazione Interfaccia classica deve avere una finestra di dialogo Interfaccia Touch corrispondente così come una finestra di dialogo di progettazione Interfaccia Touch corrispondente.

La documentazione sugli strumenti di modernizzazione di Experience Manager fornisce informazioni e strumenti per la conversione dei componenti dall’interfaccia utente classica all’interfaccia Touch. Per ulteriori informazioni, consulta la [documentazione degli strumenti di modernizzazione di Experience Manager](https://opensource.adobe.com/aem-modernize-tools/).

### I pacchetti non devono contenere un mix di contenuti mutabili e immutabili {#oakpal-packages-immutable}

* **Chiave**: ImmutableMutableMixedPackage
* **Tipo**: code smell/compatibilità con Cloud Service
* **Gravità**: minore
* **Da**: versione 2020.5.0

Per la compatibilità con il modello di distribuzione di Cloud Service, i singoli pacchetti di contenuti devono contenere contenuti per aree non modificabili dell’archivio (`/apps` e `/libs`) o per l’area modificabile (ovvero tutto ciò che non si trova in `/apps` o `/libs`), ma non per entrambi i tipi. Ad esempio, un pacchetto che include sia `/apps/myco/components/text` che `/etc/clientlibs/myco` non è compatibile con Cloud Service e genera un problema da segnalare.

>[!NOTE]
>
>La regola [I pacchetti cliente non devono creare o modificare nodi in /libs](#oakpal-customer-package) si applica sempre.

Per ulteriori informazioni, consulta [Struttura dei progetti Experience Manager](/help/implementing/developing/introduction/aem-project-content-package-structure.md).

### Non utilizzare agenti di replica inversa {#oakpal-reverse-replication}

* **Chiave**: ReverseReplication
* **Tipo**: code smell/compatibilità con Cloud Service
* **Gravità**: minore
* **Da**: versione 2020.5.0

Il supporto per la replica inversa non è disponibile nelle distribuzioni di Cloud Service, come descritto nelle [note sulla versione](/help/release-notes/aem-cloud-changes.md#replication-agents) di Experience Manager as a Cloud Service.

Se utilizzi la replica inversa, contatta Adobe per scoprire le soluzioni alternative.

### Le risorse da librerie client abilitate per i proxy devono essere in una cartella denominata risorse {#oakpal-resources-proxy}

* **Chiave**: ClientlibProxyResource
* **Tipo**: bug
* **Gravità**: minore
* **Da**: versione 2021.2.0

Le librerie client Experience Manager possono contenere risorse statiche come immagini e font. Come descritto nel documento [Utilizzo dei preprocessori,](/help/implementing/developing/introduction/clientlibs.md#using-preprocessors) quando si usano le librerie client abilitate al proxy le risorse statiche devono essere contenute in una cartella secondaria denominata `resources` affinché sia possibile farvi riferimento nelle istanze pubbliche.

#### Codice non conforme {#non-compliant-proxy-enabled}

```text
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + images
        + myimage.jpg
```

#### Codice conforme {#compliant-proxy-enabled}

```tet
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + resources
        + myimage.jpg
```

### Utilizzo di processi di flusso di lavoro non compatibili con Cloud Service {#oakpal-usage-cloud-service}

* **Chiave**: CloudServiceIncompatibleWorkflowProcess
* **Tipo**: bug
* **Gravità**: importante
* **Da**: versione 2021.2.0

Con il passaggio ai microservizi delle risorse per l’elaborazione delle risorse su Experience Manager as a Cloud Service, diversi processi di flusso di lavoro utilizzati nelle versioni on-premise e AMS di Experience Manager non sono più supportati o necessari.

Lo strumento di migrazione nell’[archivio GitHub di Assets Experience Manager as a Cloud Service](https://github.com/adobe/aem-cloud-migration) può essere usato per aggiornare i modelli del flusso di lavoro durante la migrazione a Experience Manager as a Cloud Service.

### È preferibile utilizzare modelli modificabili rispetto ai modelli statici {#oakpal-static-template}

* **Chiave**: StaticTemplateUsage
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2021.2.0

Sebbene l’utilizzo di modelli statici sia storicamente comune nei progetti di Experience Manager, Adobe consiglia di utilizzare modelli modificabili in quanto forniscono la massima flessibilità e supportano funzionalità aggiuntive non presenti nei modelli statici. Per ulteriori informazioni, consulta il documento [Modelli pagina](/help/implementing/developing/components/templates.md).

La migrazione da modelli statici a modificabili può essere in gran parte automatizzata con gli [strumenti di modernizzazione di Experience Manager.](https://opensource.adobe.com/aem-modernize-tools/)

### L’utilizzo dei componenti di base precedenti è sconsigliato {#oakpal-usage-legacy}

* **Chiave**: LegacyFoundationComponentUsage
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2021.2.0

I componenti Foundation legacy (ovvero i componenti in `/libs/foundation`) sono ora obsoleti per diverse versioni di Experience Manager, in favore dei componenti core. L’utilizzo dei componenti Foundation come base per i componenti personalizzati (tramite sovrapposizione o ereditarietà) viene scoraggiato; si consiglia di optare per la conversione nei corrispondenti componenti core.

Tale conversione può essere agevolata dall’uso degli [strumenti di modernizzazione di Experience Manager.](https://opensource.adobe.com/aem-modernize-tools/)

### Utilizza solo i nomi e l’ordine delle modalità di esecuzione supportati {#oakpal-supported-runmodes}

* **Chiave**: SupportedRunmode
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2021.2.0

Experience Manager as a Cloud Service applica un criterio di denominazione rigoroso per i nomi delle modalità di esecuzione e un ordine rigoroso per tali modalità di esecuzione. L’elenco delle modalità di esecuzione supportate è disponibile nel documento [Distribuzione in Experience Manager as a Cloud Service](/help/implementing/deploying/overview.md#runmodes) e qualsiasi deviazione da queste sarà identificata come un problema.

### I nodi di definizione dell’indice di ricerca personalizzato devono essere nodi secondari diretti di /oak:index {#oakpal-custom-search}

* **Chiave**: OakIndexLocation
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2021.2.0

Experience Manager as a Cloud Service richiede che le definizioni dell’indice di ricerca personalizzato (ovvero i nodi di tipo `oak:QueryIndexDefinition`) siano nodi secondari diretti di `/oak:index`. Per la compatibilità con Experience Manager as a Cloud Service è necessario spostare gli indici in altre posizioni. Ulteriori informazioni sugli indici di ricerca sono disponibili nel documento [Ricerca e indicizzazione dei contenuti](/help/operations/indexing.md).

### I nodi di definizione dell’indice di ricerca personalizzato devono avere una compatVersion di 2 {#oakpal-custom-search-compatVersion}

* **Chiave**: IndexCompatVersion
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2021.2.0

Experience Manager as a Cloud Service richiede che nelle definizioni dell’indice di ricerca personalizzato (ovvero i nodi di tipo `oak:QueryIndexDefinition`) la proprietà `compatVersion` sia impostata su `2`. Qualsiasi altro valore non è supportato da Experience Manager as a Cloud Service. Per ulteriori informazioni sugli indici di ricerca, consulta [Ricerca e indicizzazione dei contenuti](/help/operations/indexing.md).

### I nodi discendenti dei nodi di definizione dell’indice di ricerca personalizzato devono essere di tipo nt:unstructured {#oakpal-descendent-nodes}

* **Chiave**: IndexDescendantNodeType
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2021.2.0

È possibile che si verifichino problemi difficili da risolvere quando un nodo di definizione dell’indice di ricerca personalizzato ha nodi secondari non ordinati. Per evitare questa situazione, è consigliabile che tutti i nodi discendenti di un nodo `oak:QueryIndexDefinition` siano di tipo `nt:unstructured`.

### I nodi di definizione dell’indice di ricerca personalizzato devono contenere un nodo secondario denominato indexRules con elementi secondari {#oakpal-custom-search-index}

* **Chiave**: IndexRulesNode
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2021.2.0

Un nodo di definizione dell’indice di ricerca personalizzato definito correttamente deve contenere un nodo secondario denominato `indexRules` che, a sua volta, deve avere almeno un elemento secondario. Per ulteriori informazioni consulta la sezione [Documentazione di Oak.](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

### I nodi di definizione dell’indice di ricerca personalizzato devono rispettare le convenzioni di denominazione {#oakpal-custom-search-definitions}

* **Chiave**: IndexName
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2021.2.0

Experience Manager as a Cloud Service richiede che la denominazione delle definizioni dell’indice di ricerca personalizzato (ossia i nodi di tipo `oak:QueryIndexDefinition`) rispetti un modello specifico descritto nel documento [Ricerca e indicizzazione dei contenuti](/help/operations/indexing.md).

### I nodi di definizione dell’indice di ricerca personalizzato devono utilizzare il tipo di indice Lucene  {#oakpal-index-type-lucene}

* **Chiave**: IndexType
* **Tipo**: bug
* **Gravità**: bloccante
* **Da**: versione 2021.2.0 (tipo e gravità modificati nella versione 2021.8.0)

Experience Manager as a Cloud Service richiede che le definizioni dell’indice di ricerca personalizzato (ovvero i nodi di tipo `oak:QueryIndexDefinition`) presentino una proprietà `type` con valore impostato su `lucene`. Prima della migrazione a Experience Manager as a Cloud Service è necessario aggiornare l’indicizzazione che utilizza i tipi di indice legacy. Per ulteriori informazioni, consulta il documento [Ricerca e indicizzazione dei contenuti](/help/operations/indexing.md#how-to-use).

### I nodi di definizione dell’indice di ricerca personalizzato non devono contenere una proprietà denominata seed {#oakpal-property-name-seed}

* **Chiave**: IndexSeedProperty
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2021.2.0

Experience Manager as a Cloud Service non consente che le definizioni dell’indice di ricerca personalizzato (ovvero i nodi di tipo `oak:QueryIndexDefinition`) contengano una proprietà denominata `seed`. Prima della migrazione a Experience Manager as a Cloud Service è necessario aggiornare l’indicizzazione che utilizza questa proprietà. Per ulteriori informazioni, consulta il documento [Ricerca e indicizzazione dei contenuti](/help/operations/indexing.md#how-to-use).

### I nodi di definizione dell’indice di ricerca personalizzato non devono contenere una proprietà denominata reindex {#oakpal-reindex-property}

* **Chiave**: IndexReindexProperty
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2021.2.0

Experience Manager as a Cloud Service non consente che le definizioni dell’indice di ricerca personalizzato (ovvero i nodi di tipo `oak:QueryIndexDefinition`) contengano una proprietà denominata `reindex`. L’indicizzazione con questa proprietà deve essere aggiornata prima della migrazione ad Experience Manager as a Cloud Service. Per ulteriori informazioni, consulta il documento [Ricerca e indicizzazione dei contenuti](/help/operations/indexing.md#how-to-use).

### I nodi Lucene delle risorse DAM personalizzati non devono specificare &quot;queryPaths&quot; {#oakpal-damAssetLucene-queryPaths}

* **Chiave**: IndexDamAssetLucene
* **Tipo**: bug
* **Gravità**: bloccante
* **Da**: versione 2022.1.0

#### Codice non conforme {#non-compliant-code-damAssetLucene-queryPaths}

```text
+ oak:index
    + damAssetLucene-1-custom-1
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: [/content/dam]
      - queryPaths: [/content/dam]
      - type: lucene
      + tika
        + config.xml
```

#### Codice conforme {#compliant-code-damAssetLucene-queryPaths}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: [/content/dam]
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### Se la definizione dell&#39;indice di ricerca personalizzato contiene compatVersion, deve essere impostata su 2 {#oakpal-compatVersion}

* **Chiave**: IndexCompatVersion
* **Tipo**: code smell
* **Gravità**: importante
* **Da**: versione 2022.1.0


### Il nodo indice che specifica &#39;includedPaths&#39; deve inoltre specificare &#39;queryPaths&#39; con gli stessi valori {#oakpal-included-paths-without-query-paths}

* **Chiave**: IndexIncludedPathsWithoutQueryPaths
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2023.1.0

Per gli indici personalizzati, entrambi `includedPaths` e `queryPaths` deve essere configurato con valori identici. Se ne viene specificata una, l&#39;altra deve corrispondere. Tuttavia, esiste un caso speciale per gli indici di `damAssetLucene`, incluse le versioni personalizzate. Per questi, devi fornire solo `includedPaths`.

### Il nodo di indice che specifica nodeScopeIndex sul tipo di nodo generico deve inoltre specificare includedPaths e queryPaths {#oakpal-full-text-on-generic-node-type}

* **Chiave**: IndexFulltextOnGenericType
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2023.1.0

Quando si imposta `nodeScopeIndex` su un tipo di nodo &quot;generico&quot; come `nt:unstructured` o `nt:base`, è inoltre necessario specificare `includedPaths` e `queryPaths` proprietà.
`nt:base` può essere considerato &quot;generico&quot;, in quanto tutti i tipi di nodo ereditano da esso. Quindi, impostazione di un `nodeScopeIndex` il `nt:base` lo farà indicizzare tutti i nodi nell’archivio. Analogamente, `nt:unstructured` è anche considerato &quot;generico&quot; in quanto esistono molti nodi negli archivi che sono di questo tipo.

#### Codice non conforme {#non-compliant-code-full-text-on-generic-node-type}

```text
+ oak:index/acme.someIndex-custom-1
  - async: [async, nrt]
  - evaluatePathRestrictions: true
  - tags: [visualSimilaritySearch]
  - type: lucene
    + indexRules
      - jcr:primaryType: nt:unstructured
      + nt:base
        - jcr:primaryType: nt:unstructured
        + properties
          + acme.someIndex-custom-1
            - nodeScopeIndex: true
```

#### Codice conforme {#compliant-code-full-text-on-generic-node-type}

```text
+ oak:index/acme.someIndex-custom-1
  - async: [async, nrt]
  - evaluatePathRestrictions: true
  - tags: [visualSimilaritySearch]
  - type: lucene
  - includedPaths: ["/content/dam/"] 
  - queryPaths: ["/content/dam/"]
    + indexRules
      - jcr:primaryType: nt:unstructured
      + nt:base
        - jcr:primaryType: nt:unstructured
        + properties
          + acme.someIndex-custom-1
            - nodeScopeIndex: true
```

### La proprietà queryLimitReads del motore di query non deve essere sostituita {#oakpal-query-limit-reads}

* **Chiave**: OverrideOfQueryLimitReads
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2023.1.0

Se si ignora il valore predefinito, le letture delle pagine possono risultare molto lente, in particolare quando viene aggiunto più contenuto.

### Più versioni attive dello stesso indice {#oakpal-multiple-active-versions}

* **Chiave**: IndexDetectMultipleActiveVersionsOfSameIndex
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2023.1.0

#### Codice non conforme {#non-compliant-code-multiple-active-versions}

```text
+ oak:index
  + damAssetLucene-1-custom-1
    ...
  + damAssetLucene-1-custom-2
    ...
  + damAssetLucene-1-custom-3
    ...
```

#### Codice conforme {#compliant-code-multiple-active-versions}

```text
+ damAssetLucene-1-custom-3
    ...
```


### Il nome delle definizioni di indice completamente personalizzate deve essere conforme alle linee guida ufficiali {#oakpal-fully-custom-index-name}

* **Chiave**: IndexValidFullyCustomName
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2023.1.0

Il modello previsto per i nomi di indice completamente personalizzati è: `[prefix].[indexName]-custom-[version]`. Ulteriori informazioni sono disponibili nel documento [Ricerca e indicizzazione dei contenuti](/help/operations/indexing.md).


### Stessa proprietà con valori analizzati diversi nella stessa definizione di indice {#oakpal-same-property-different-analyzed-values}

#### Codice non conforme {#non-compliant-code-same-property-different-analyzed-values}

```text
+ indexRules
  + dam:Asset
    + properties
      + status
        - name: status
        - analyzed: true
  + dam:cfVariationNode
    + properties
      + status
        - name: status
```

#### Codice conforme {#compliant-code-same-property-different-analyzed-values}

Esempio:

```text
+ indexRules
  + dam:Asset
    + properties
      + status
        - name: status
        - analyzed: true
  + dam:cfVariationNode
    + properties
      + status
        - name: status
        - analyzed: true
```

Esempio:

```text
+ indexRules
  + dam:Asset
    + properties
      + status
        - name: status
  + dam:cfVariationNode
    + properties
      + status
        - name: status
        - analyzed: true
```

Se la proprietà analizzata non è stata impostata in modo esplicito, il valore predefinito sarà falso.

### Proprietà Tags

* **Chiave**: IndexHasValidTagsProperty
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2023.1.0

Per indici specifici, assicurati di mantenere la proprietà tags e i relativi valori correnti. Anche se è possibile aggiungere nuovi valori alla proprietà tags, l’eliminazione di eventuali valori esistenti (o del tutto la proprietà ) può causare risultati imprevisti.
