---
title: Regole per la qualità del codice personalizzato
description: Questa pagina descrive le regole per la qualità del codice personalizzato eseguite da Cloud Manager come parte del test di qualità del codice. Si basano sulle best practice di Adobe Experience Manager Engineering.
exl-id: f40e5774-c76b-4c84-9d14-8e40ee6b775b
source-git-commit: 2935338b847f7e852dfd31c93a61e737e8a3ec80
workflow-type: tm+mt
source-wordcount: '3485'
ht-degree: 44%

---

# Regole per la qualità del codice personalizzato {#custom-code-quality-rules}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_customcodequalityrules"
>title="Regole per la qualità del codice personalizzato"
>abstract="Questa pagina descrive le regole per la qualità del codice personalizzato eseguite da Cloud Manager come parte del test di qualità del codice. Si basano sulle best practice di Adobe Experience Manager Engineering."

Questa pagina descrive le regole per la qualità del codice personalizzato eseguite da Cloud Manager come parte del [test di qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md). Si basano sulle best practice di Experience Manager Engineering.

>[!NOTE]
>
>Gli esempi di codice qui forniti sono esclusivamente a scopo illustrativo. Per informazioni sui concetti e le regole di qualità di SonarQube, consulta la [Documentazione sui concetti](https://docs.sonarqube.org/latest/) di SonarQube.

## Regole SonarQube {#sonarqube-rules}

Nella sezione seguente sono descritte le regole di SonarQube eseguite da Cloud Manager.

### Non utilizzare funzioni potenzialmente pericolose {#do-not-use-potentially-dangerous-functions}

* **Chiave**: CQRules:CWE-676
* **Tipo**: vulnerabilità
* **Gravità**: importante
* **Da**: versione 2018.4.0

I metodi `Thread.stop()` e `Thread.interrupt()` può produrre problemi difficili da riprodurre e, a volte, vulnerabilità di sicurezza. Il loro utilizzo deve essere controllato e convalidato. In generale, il passaggio di messaggi è un modo più sicuro per raggiungere obiettivi simili.

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

### Le richieste HTTP devono sempre avere un socket e un timeout di connessione {#http-requests-should-always-have-socket-and-connect-timeouts}

* **Chiave**: CQRules:ConnectionTimeoutMechanism
* **Tipo**: bug
* **Gravità**: critico
* **Da**: versione 2018.6.0

Durante l’esecuzione di richieste HTTP dall’interno di un’applicazione Experience Manager, è fondamentale assicurarsi che siano configurati timeout appropriati al fine di evitare un consumo di thread non necessario. Sfortunatamente, il comportamento predefinito di entrambi i client HTTP predefiniti di Java™ (`java.net.HttpUrlConnection`) e il client Apache HTTP Components comunemente utilizzato non subisce mai timeout, pertanto i timeout devono essere impostati in modo esplicito. Inoltre, come best practice, i timeout non devono superare i 60 secondi.

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

public void orDoThis() {
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

### Chiudi sempre gli oggetti ResourceResolver {#resourceresolver-objects-should-always-be-closed}

* **Chiave**: CQRules:CQBP-72
* **Tipo**: code smell
* **Gravità**: importante
* **Da**: versione 2018.4.0

Gli oggetti `ResourceResolver` ottenuti da `ResourceResolverFactory` consumano risorse di sistema. Sebbene esistano misure per recuperare tali risorse quando un oggetto `ResourceResolver` non è più in uso, è più efficiente chiudere in modo esplicito qualsiasi oggetto `ResourceResolver` aperto con una chiamata al metodo `close()`.

Un equivoco relativamente comune è che `ResourceResolver` gli oggetti creati utilizzando una sessione JCR esistente non devono essere chiusi in modo esplicito o in questo modo viene chiusa la sessione JCR sottostante. Questo non succede. Indipendentemente da come si apre un oggetto `ResourceResolver`, quando non viene più utilizzato deve essere chiuso. Poiché `ResourceResolver` implementa l’interfaccia `Closeable`, è possibile utilizzare anche la sintassi `try-with-resources` anziché richiamare esplicitamente `close()`.

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

### Non utilizzare i percorsi dei servlet Sling per registrare i servlet {#do-not-use-sling-servlet-paths-to-register-servlets}

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

### Le eccezioni catturate devono essere registrate o lanciate, non entrambe {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

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

### Evitare le istruzioni di registro immediatamente seguite da un&#39;istruzione di tipo &quot;drill&quot; {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

* **Chiave**: CQRules:CQBP-44---ConsecutivelyLogAndThrow
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2018.4.0

Un altro modello comune da evitare è registrare un messaggio e generare immediatamente un’eccezione. Questa pratica indica in genere che il messaggio di eccezione viene duplicato nei file di registro.

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

### Evita la registrazione a INFO quando gestisci richieste GET o HEAD {#avoid-logging-at-info-when-handling-get-or-head-requests}

* **Chiave**: CQRules:CQBP-44---LogInfoInGetOrHeadRequests
* **Tipo**: code smell
* **Gravità**: minore

In generale, il livello di log INFO deve essere utilizzato per delimitare azioni importanti e, per impostazione predefinita, l&#39;Experience Manager è configurato per il log al livello INFO o superiore. I metodi GET e HEAD devono essere sempre di sola lettura e non costituiscono pertanto azioni importanti. È probabile che la registrazione a livello INFO in risposta alle richieste di GET o HEAD generi un rumore di registro significativo, rendendo più difficile l’identificazione di informazioni utili nei file di registro. Per la gestione delle richieste GET o HEAD, la registrazione deve essere ai livelli WARN o ERROR in caso di errori oppure ai livelli DEBUG o TRACE in caso siano necessarie informazioni più dettagliate sulla risoluzione dei problemi.

>[!NOTE]
>
>Questo non si applica a `access.log`Registrazione di tipo -type per ogni richiesta.

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

Come best practice, i messaggi del registro devono fornire informazioni contestuali sulla posizione in cui è stata generata un’eccezione nell’applicazione. Anche se il contesto può essere determinato utilizzando le tracce dello stack, in generale il messaggio di log sarà più facile da leggere e comprendere. Di conseguenza, quando si registra un’eccezione, è sconsigliato utilizzare il messaggio dell’eccezione come messaggio del registro. Il messaggio di eccezione contiene ciò che è andato storto, mentre il messaggio di log deve essere utilizzato per comunicare al lettore di log cosa stava facendo l&#39;applicazione quando si è verificata l&#39;eccezione. Il messaggio di eccezione è ancora registrato. Specificando il tuo messaggio, i registri sono più facili da comprendere.

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

### L&#39;accesso ai blocchi di blocco deve essere a livello di WARN o ERROR {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

* **Chiave**: CQRules:CQBP-44---WrongLogLevelInCatchBlock
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2018.4.0

Come suggerisce il nome, le eccezioni Java™ devono sempre essere utilizzate in circostanze eccezionali. Di conseguenza, quando viene rilevata un’eccezione, è importante assicurarsi che i messaggi del registro vengano registrati al livello appropriato, WARN o ERROR. In questo modo i messaggi verranno visualizzati correttamente nei registri.

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

### Non stampare le tracce di stack nella console {#do-not-print-stack-traces-to-the-console}

* **Chiave**: CQRules:CQBP-44---ExceptionPrintStackTrace
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2018.4.0

Come già menzionato, il contesto è fondamentale per comprendere i messaggi del registro. Utilizzo `Exception.printStackTrace()` fa sì che solo la traccia dello stack venga trasmessa al flusso di errore standard, perdendo tutto il contesto. Inoltre, in un&#39;applicazione multi-thread come l&#39;Experience Manager, se vengono stampate più eccezioni utilizzando questo metodo in parallelo, le loro tracce di stack possono sovrapporsi, il che crea una confusione significativa. Le eccezioni devono essere registrate unicamente tramite il framework di registrazione.

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

L’accesso all’Experience Manager deve sempre essere effettuato tramite il framework di registrazione (SLF4J). L’output diretto nei flussi di errore standard o standard perde le informazioni strutturali e contestuali fornite dal framework di registrazione. A volte può causare problemi di prestazioni.

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

### Evitare percorsi /apps e /libs codificati {#avoid-hardcoded-apps-and-libs-paths}

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

### Non utilizzare lo schedulatore Sling {#sonarqube-sling-scheduler}

* **Chiave**: CQRules:AMSCORE-554
* **Tipo**: code smell/compatibilità con Cloud Service
* **Gravità**: minore
* **Da**: versione 2020.5.0

Non utilizzare lo strumento di pianificazione Sling per le attività che richiedono un’esecuzione garantita. I processi pianificati Sling garantiscono l’esecuzione e sono più adatti per gli ambienti cluster e per quelli non cluster.

Fai riferimento a [Eventi Sling Apache e gestione dei processi](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html) per ulteriori informazioni sulla gestione dei processi Sling in ambienti cluster.

### Non utilizzare API obsolete di Experience Manager {#sonarqube-aem-deprecated}

* **Chiave**: AMSCORE-553
* **Tipo**: code smell/compatibilità con Cloud Service
* **Gravità**: minore
* **Da**: versione 2020.5.0

La superficie API di Experience Manager è soggetta a revisioni costanti per identificare le API per le quali l’utilizzo è scoraggiato e quindi considerato obsoleto.

Spesso queste API sono obsolete con Java™ standard `@Deprecated` l&#39;annotazione e, in quanto tale, quali identificati `squid:CallToDeprecatedMethod`.

Tuttavia, in alcuni casi un’API è obsoleta nel contesto di un Experience Manager ma potrebbe non essere deprecata in altri contesti. Questa regola identifica questa seconda classe.


## Regole di contenuto OakPAL {#oakpal-rules}

Nella sezione seguente sono descritti i controlli OakPAL eseguiti da Cloud Manager.

>[!NOTE]
>
>OakPAL è un framework che convalida i pacchetti di contenuti con un archivio Oak autonomo. È stato sviluppato da un partner Experience Manager e vincitore del 2019 Experience Manager Rockstar Nord America Award.

### Le API del prodotto annotate con @ProviderType non devono essere implementate o estese dai clienti {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

* **Chiave**: CQBP-84
* **Tipo**: bug
* **Gravità**: critico
* **Da**: versione 2018.7.0

L&#39;API Experience Manager contiene interfacce e classi Java™ che devono essere utilizzate solo con codice personalizzato, ma non implementate. Ad esempio, l’interfaccia `com.day.cq.wcm.api.Page` devono essere attuate solo a titolo di Experience Manager.

Quando a queste interfacce vengono aggiunti nuovi metodi, tali metodi aggiuntivi non influiscono sul codice esistente che utilizza queste interfacce. Di conseguenza, l’aggiunta di nuovi metodi a queste interfacce è considerata retrocompatibile. Tuttavia, se il codice personalizzato implementa una di queste interfacce, genera per il cliente un rischio di retrocompatibilità con le versioni precedenti.

Le interfacce e le classi, come implementato dall’Experience Manager, vengono annotate con `org.osgi.annotation.versioning.ProviderType` o a volte un’annotazione legacy simile `aQute.bnd.annotation.ProviderType`. Questa regola identifica i casi in cui tale interfaccia viene implementata o in cui una classe viene estesa dal codice personalizzato.

#### Codice non conforme {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### Gli indici Lucene personalizzati Oak devono avere una configurazione Tika {#oakpal-indextikanode}

* **Chiave**: IndexTikaNode
* **Tipo**: bug
* **Gravità**: bloccante
* **Da**: 2021.8.0

Gli indici Oak di Experience Manager predefiniti multipli includono una configurazione Tika e le personalizzazioni di questi indici devono includere una configurazione Tika. Questa regola controlla le personalizzazioni degli indici `damAssetLucene`, `lucene` e `graphqlConfig` e genera un problema se il nodo `tika` risulta mancante o se nel nodo `tika` manca un nodo secondario denominato `config.xml`.

Per ulteriori informazioni sulla personalizzazione delle definizioni dell’indice, consulta [Indicizzazione della documentazione](/help/operations/indexing.md#preparing-the-new-index-definition).

#### Codice non conforme {#non-compliant-code-indextikanode}

```text
+ oak:index
    + damAssetLucene-1-custom
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
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
      - reindex: false
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

Gli indici Oak di tipo `lucene` devono essere sempre asincroni. In caso contrario, potrebbe verificarsi un’instabilità del sistema. Ulteriori informazioni sulla struttura degli indici Lucene sono disponibili nella sezione [Documentazione Oak.](https://jackrabbit.apache.org/oak/docs/query/lucene.html#index-definition)

#### Codice non conforme {#non-compliant-code-indexasync}

```text
+ oak:index
    + damAssetLucene-1-custom
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - type: lucene
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
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
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### Gli indici Oak personalizzati DAM Asset Lucene sono strutturati correttamente  {#oakpal-damAssetLucene-sanity-check}

* **Chiave**: IndexDamAssetLucene
* **Tipo**: bug
* **Gravità**: bloccante
* **Da**: 2021.6.0

Affinché la ricerca delle risorse funzioni correttamente in Experience Manager Assets, le personalizzazioni del `damAssetLucene` L&#39;indice Oak deve seguire una serie di linee guida specifiche di questo indice. Questa regola controlla che la definizione dell’indice presenti una proprietà con valori multipli denominata `tags` e contenente il valore `visualSimilaritySearch`.

#### Codice non conforme {#non-compliant-code-damAssetLucene}

```text
+ oak:index
    + damAssetLucene-1-custom
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
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
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### I pacchetti cliente non devono creare o modificare nodi sotto /libs {#oakpal-customer-package}

* **Chiave**: BannedPath
* **Tipo**: bug
* **Gravità**: critico
* **Da**: versione 2019.6.0

È stata una best practice consolidata che `/libs` la struttura del contenuto nell’archivio dei contenuti di Experience Manager deve essere considerata di sola lettura dai clienti. Modificare nodi e proprietà in `/libs` crea rischi significativi per gli aggiornamenti principali e secondari. Modifiche a `/libs` deve essere fatto per Adobe attraverso canali ufficiali.

### I pacchetti non devono contenere configurazioni OSGi duplicate {#oakpal-package-osgi}

* **Chiave**: DuplicateOsgiConfigurations
* **Tipo**: bug
* **Gravità**: importante
* **Da**: versione 2019.6.0

Un problema comune che si verifica in progetti complessi è che lo stesso componente OSGi viene configurato più volte. Questo problema crea un&#39;ambiguità riguardo alla configurazione applicabile. Questa regola è consapevole del fatto che identifica solo i problemi in cui lo stesso componente viene configurato più volte nella stessa modalità di esecuzione o nella stessa combinazione di modalità di esecuzione.

>[!NOTE]
>
>Questa regola genera problemi in cui la stessa configurazione, nello stesso percorso, è definita in più pacchetti, compresi i casi in cui lo stesso pacchetto viene duplicato nell&#39;elenco complessivo dei pacchetti generati.
>
>Ad esempio, se la build produce pacchetti denominati `com.myco:com.myco.ui.apps` e `com.myco:com.myco.all` dove `com.myco:com.myco.all` incorporamenti `com.myco:com.myco.ui.apps`, quindi tutte le configurazioni in `com.myco:com.myco.ui.apps` sono segnalati come duplicati.
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

Un problema comune è l’utilizzo di nodi denominati `config` nelle finestre di dialogo dei componenti o quando si specifica la configurazione dell’editor Rich Text per la modifica in linea. Per risolvere questo problema, il nodo che ha commesso l’errore deve essere rinominato in un nome conforme. Per la configurazione dell’editor Rich Text, utilizza `configPath` sulla proprietà `cq:inplaceEditing` per specificare la nuova posizione.

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

### La modalità di authoring predefinita non deve essere un’interfaccia classica {#oakpal-default-authoring}

* **Chiave**: ClassicUIAuthoringMode
* **Tipo**: code smell/compatibilità con Cloud Service
* **Gravità**: minore
* **Da**: versione 2020.5.0

Configurazione OSGi `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` definisce la modalità di authoring predefinita all’interno di Experience Manager. Perché [l’interfaccia classica è stata rimossa a partire dall’Experience Manager 6.4](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/deprecated-removed-features.html?lang=it), viene ora sollevato un problema quando la modalità di authoring predefinita è configurata nell’interfaccia classica.

### I componenti con finestre di dialogo devono avere finestre di dialogo dell’interfaccia touch {#oakpal-components-dialogs}

* **Chiave**: ComponentWithOnlyClassicUIDialog
* **Tipo**: code smell/compatibilità con Cloud Service
* **Gravità**: minore
* **Da**: versione 2020.5.0

Ad Experience Manager, i componenti che dispongono di una finestra di dialogo Interfaccia classica devono sempre avere una finestra di dialogo corrispondente. Entrambi offrono un’esperienza di authoring ottimale e devono essere compatibili con il modello di distribuzione del Cloud Service, dove l’interfaccia classica non è supportata. Questa regola verifica i seguenti scenari:

* Un componente con una finestra di dialogo dell’interfaccia classica (ovvero un nodo figlio `dialog`) deve avere una finestra di dialogo corrispondente dell’interfaccia Touch (ovvero un nodo figlio `cq:dialog`).
* Un componente con una finestra di dialogo di progettazione Interfaccia classica (ossia un nodo `design_dialog`) deve avere una finestra di dialogo di progettazione Interfaccia Touch corrispondente (ossia un nodo figlio `cq:design_dialog`).
* Un componente con una finestra di dialogo Interfaccia classica e una finestra di dialogo di progettazione Interfaccia classica deve avere una finestra di dialogo Interfaccia Touch corrispondente così come una finestra di dialogo di progettazione Interfaccia Touch corrispondente.

La documentazione sugli strumenti di modernizzazione Experience Manager fornisce documentazione e strumenti per la conversione dei componenti dall’interfaccia classica all’interfaccia utente touch. Fai riferimento a [la documentazione relativa agli strumenti di modernizzazione Experience Manager](https://opensource.adobe.com/aem-modernize-tools/) per ulteriori dettagli.

### I pacchetti non devono mescolare contenuti mutabili e immutabili {#oakpal-packages-immutable}

* **Chiave**: ImmutableMutableMixedPackage
* **Tipo**: code smell/compatibilità con Cloud Service
* **Gravità**: minore
* **Da**: versione 2020.5.0

Per essere compatibile con il modello di distribuzione del Cloud Service, i singoli pacchetti di contenuto devono contenere contenuto per le aree immutabili dell’archivio (`/apps` e `/libs`), o l&#39;area mutabile (tutto ciò che non si trova in `/apps` o `/libs`), ma non entrambe. Ad esempio, un pacchetto che include entrambi `/apps/myco/components/text` e `/etc/clientlibs/myco` non è compatibile con il Cloud Service e causa la segnalazione di un problema.

>[!NOTE]
>
>La regola [I pacchetti cliente non devono creare o modificare nodi in /libs](#oakpal-customer-package) si applica sempre.

Fai riferimento a [Experience Manager struttura del progetto](/help/implementing/developing/introduction/aem-project-content-package-structure.md) per ulteriori dettagli.

### Non utilizzare agenti di replica inversa {#oakpal-reverse-replication}

* **Chiave**: ReverseReplication
* **Tipo**: code smell/compatibilità con Cloud Service
* **Gravità**: minore
* **Da**: versione 2020.5.0

Il supporto per la replica inversa non è disponibile nelle distribuzioni di Cloud Service, come descritto come parte di Experience Manager as a Cloud Service [note sulla versione.](/help/release-notes/aem-cloud-changes.md#replication-agents)

Se utilizzi la replica inversa, contatta Adobe per scoprire le soluzioni alternative.

### Le risorse contenute nelle librerie client abilitate per i proxy devono trovarsi in una cartella denominata risorse {#oakpal-resources-proxy}

* **Chiave**: ClientlibProxyResource
* **Tipo**: bug
* **Gravità**: minore
* **Da**: versione 2021.2.0

Ad Experience Manager, le librerie client possono contenere risorse statiche come immagini e font. Come descritto nel documento [Utilizzo dei preprocessori,](/help/implementing/developing/introduction/clientlibs.md#using-preprocessors) quando si usano le librerie client abilitate al proxy le risorse statiche devono essere contenute in una cartella secondaria denominata `resources` affinché sia possibile farvi riferimento nelle istanze pubbliche.

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

### Utilizzo dei processi del flusso di lavoro Cloud Service incompatibili {#oakpal-usage-cloud-service}

* **Chiave**: CloudServiceIncompatibleWorkflowProcess
* **Tipo**: bug
* **Gravità**: importante
* **Da**: versione 2021.2.0

Con il passaggio ai microservizi per le risorse per l’elaborazione delle risorse su Experience Manager as a Cloud Service, diversi processi di flusso di lavoro utilizzati nelle versioni di Experience Manager on-premise e AMS sono diventati non supportati o non necessari.

Lo strumento di migrazione nel [Experience Manager archivio GitHub risorse as a Cloud Service](https://github.com/adobe/aem-cloud-migration) può essere utilizzato per aggiornare i modelli di flusso di lavoro durante la migrazione ad Experience Manager as a Cloud Service.

### L’utilizzo di modelli statici è scoraggiato a favore di modelli modificabili {#oakpal-static-template}

* **Chiave**: StaticTemplateUsage
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2021.2.0

Sebbene l’utilizzo di modelli statici sia storicamente comune nei progetti di Experience Manager, Adobe consiglia di utilizzare modelli modificabili in quanto forniscono la flessibilità e supportano funzionalità aggiuntive non presenti nei modelli statici. Per ulteriori informazioni, consulta il documento [Modelli pagina.](/help/implementing/developing/components/templates.md)

La migrazione da modelli statici a modificabili può essere in gran parte automatizzata utilizzando [Strumenti di modernizzazione Experience Manager.](https://opensource.adobe.com/aem-modernize-tools/)

### L’utilizzo dei componenti di base legacy è scoraggiato {#oakpal-usage-legacy}

* **Chiave**: LegacyFoundationComponentUsage
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2021.2.0

I componenti di base legacy (ovvero i componenti in `/libs/foundation`) [obsoleto per diverse versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/deprecated-removed-features.html?lang=it) a favore dei componenti core. L’utilizzo dei componenti Foundation come base per i componenti personalizzati (tramite sovrapposizione o ereditarietà) viene scoraggiato; si consiglia di optare per la conversione nei corrispondenti componenti core.

Questa conversione può essere facilitata dal [Strumenti di modernizzazione Experience Manager.](https://opensource.adobe.com/aem-modernize-tools/)

### Utilizza solo i nomi e l&#39;ordine delle modalità di esecuzione supportati {#oakpal-supported-runmodes}

* **Chiave**: SupportedRunmode
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2021.2.0

L&#39;Experience Manager as a Cloud Service applica un criterio di denominazione rigoroso per i nomi delle modalità di esecuzione e un ordine rigoroso per tali modalità di esecuzione. L&#39;elenco delle modalità di esecuzione supportate si trova nel documento [Distribuzione ad Experience Manager as a Cloud Service](/help/implementing/deploying/overview.md#runmodes) e qualsiasi deviazione da questo problema è identificato come un problema.

### I nodi di definizione dell&#39;indice di ricerca personalizzato devono essere figli diretti di /oak:index {#oakpal-custom-search}

* **Chiave**: OakIndexLocation
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2021.2.0

L&#39;Experience Manager as a Cloud Service richiede le definizioni dell&#39;indice di ricerca personalizzato (ovvero nodi di tipo `oak:QueryIndexDefinition`) devono essere nodi figlio diretti di `/oak:index`. Gli indici in altre posizioni devono essere spostati per essere compatibili con l’Experience Manager as a Cloud Service. Ulteriori informazioni sugli indici di ricerca sono disponibili nel documento [Ricerca e indicizzazione dei contenuti.](/help/operations/indexing.md)

### I nodi di definizione dell&#39;indice di ricerca personalizzato devono avere una compatVersion di 2 {#oakpal-custom-search-compatVersion}

* **Chiave**: IndexCompatVersion
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2021.2.0

L&#39;Experience Manager as a Cloud Service richiede le definizioni dell&#39;indice di ricerca personalizzato (ad esempio i nodi di tipo `oak:QueryIndexDefinition`) deve avere `compatVersion` proprietà impostata su `2`. Qualsiasi altro valore non è supportato dall&#39;Experience Manager as a Cloud Service. Per ulteriori informazioni sugli indici di ricerca, consulta [Ricerca e indicizzazione dei contenuti.](/help/operations/indexing.md)

### I nodi discendenti dei nodi di definizione dell&#39;indice di ricerca personalizzato devono essere di tipo nt:unstructured {#oakpal-descendent-nodes}

* **Chiave**: IndexDescendantNodeType
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2021.2.0

Difficile risolvere i problemi possono verificarsi quando un nodo di definizione dell&#39;indice di ricerca personalizzato ha nodi figlio non ordinati. Per evitare questa situazione, si raccomanda che tutti i nodi discendenti di un `oak:QueryIndexDefinition` nodo essere di tipo `nt:unstructured`.

### I nodi di definizione dell&#39;indice di ricerca personalizzato devono contenere un nodo figlio denominato indexRules con figli {#oakpal-custom-search-index}

* **Chiave**: IndexRulesNode
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2021.2.0

Un nodo di definizione dell’indice di ricerca personalizzato definito correttamente deve contenere un nodo secondario denominato `indexRules` che, a sua volta, deve avere almeno un elemento secondario. Per ulteriori informazioni consulta la sezione [Documentazione di Oak.](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

### I nodi di definizione dell&#39;indice di ricerca personalizzati devono seguire le convenzioni di denominazione {#oakpal-custom-search-definitions}

* **Chiave**: IndexName
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2021.2.0

L&#39;Experience Manager as a Cloud Service richiede le definizioni dell&#39;indice di ricerca personalizzato (ovvero, nodi di tipo `oak:QueryIndexDefinition`) deve essere denominato seguendo un pattern specifico descritto nel documento [Ricerca e indicizzazione dei contenuti.](/help/operations/indexing.md)

### I nodi di definizione dell&#39;indice di ricerca personalizzato devono utilizzare il tipo di indice Lucene  {#oakpal-index-type-lucene}

* **Chiave**: IndexType
* **Tipo**: bug
* **Gravità**: bloccante
* **Da**: versione 2021.2.0 (tipo e gravità modificati nella versione 2021.8.0)

L&#39;Experience Manager as a Cloud Service richiede le definizioni dell&#39;indice di ricerca personalizzato (ovvero nodi di tipo `oak:QueryIndexDefinition`) hanno `type` con il valore impostato su `lucene`. L&#39;indicizzazione utilizzando tipi di indice legacy deve essere aggiornata prima della migrazione ad Experience Manager as a Cloud Service. Vedi [Ricerca e indicizzazione dei contenuti](/help/operations/indexing.md#how-to-use) per ulteriori informazioni.

### I nodi di definizione dell&#39;indice di ricerca personalizzato non devono contenere una proprietà denominata seed {#oakpal-property-name-seed}

* **Chiave**: IndexSeedProperty
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2021.2.0

L&#39;Experience Manager as a Cloud Service vieta le definizioni degli indici di ricerca personalizzati (ovvero, i nodi di tipo `oak:QueryIndexDefinition`) da contenente una proprietà denominata `seed`. L&#39;indicizzazione utilizzando questa proprietà deve essere aggiornata prima della migrazione ad Experience Manager as a Cloud Service. Per ulteriori informazioni, consulta il documento [Ricerca e indicizzazione dei contenuti](/help/operations/indexing.md#how-to-use).

### I nodi di definizione dell&#39;indice di ricerca personalizzato non devono contenere una proprietà denominata reindex {#oakpal-reindex-property}

* **Chiave**: IndexReindexProperty
* **Tipo**: code smell
* **Gravità**: minore
* **Da**: versione 2021.2.0

L&#39;Experience Manager as a Cloud Service vieta le definizioni degli indici di ricerca personalizzati (ovvero, i nodi di tipo `oak:QueryIndexDefinition`) da contenente una proprietà denominata `reindex`. L&#39;indicizzazione utilizzando questa proprietà deve essere aggiornata prima della migrazione ad Experience Manager as a Cloud Service. Per ulteriori informazioni, consulta il documento [Ricerca e indicizzazione dei contenuti](/help/operations/indexing.md#how-to-use).
