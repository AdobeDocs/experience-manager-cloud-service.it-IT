---
title: Regole di qualità del codice personalizzato - Servizi cloud
description: Regole di qualità del codice personalizzato - Servizi cloud
translation-type: tm+mt
source-git-commit: 4b79f7dd3a55e140869985faa644f7da1f62846c
workflow-type: tm+mt
source-wordcount: '2254'
ht-degree: 5%

---


# Regole per la qualità del codice personalizzato {#custom-code-quality-rules}


Questa pagina descrive le regole di qualità del codice personalizzate eseguite da Cloud Manager create in base alle best practice di AEM Engineering.

>[!NOTE]
>
>Gli esempi di codice forniti qui sono solo a scopo illustrativo.

## Regole SonarQube {#sonarqube-rules}

Nella sezione seguente vengono evidenziate le regole SonarQube:

### Non utilizzare funzioni potenzialmente pericolose {#do-not-use-potentially-dangerous-functions}

**Chiave**: CQRules:CWE-676

**Tipo**: Vulnerabilità

**Gravità**: Maggiore

**Dal** momento: Versione 2018.4.0

I metodi ***Thread.stop()*** e ***Thread.interrupt()*** possono generare problemi difficili da riprodurre e, in alcuni casi, vulnerabilità di sicurezza. Il loro utilizzo deve essere controllato e convalidato. In generale, il passaggio di messaggi è un modo più sicuro per raggiungere obiettivi simili.

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

**Chiave**: CQRules:CWE-134

**Tipo**: Vulnerabilità

**Gravità**: Maggiore

**Dal** momento: Versione 2018.4.0

L&#39;utilizzo di una stringa di formato da un&#39;origine esterna (ad esempio un parametro di richiesta o contenuto generato dall&#39;utente) può determinare l&#39;esposizione di un&#39;applicazione agli attacchi di negazione del servizio. In alcune circostanze una stringa di formato può essere controllata esternamente, ma è consentita solo da fonti attendibili.

#### Codice non conforme {#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text");
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### Le richieste HTTP devono sempre avere socket e timeout di connessione {#http-requests-should-always-have-socket-and-connect-timeouts}

**Chiave**: CQRules:ConnectionTimeoutMechanism

**Tipo**: Bug

**Gravità**: Critico

**Dal** momento: Versione 2018.6.0

Durante l&#39;esecuzione di richieste HTTP dall&#39;interno di un&#39;applicazione AEM, è fondamentale assicurarsi che i timeout corretti siano configurati in modo da evitare inutili usi di thread. Purtroppo, il comportamento predefinito sia del client HTTP predefinito Java (java.net.HttpUrlConnection) che del client Apache HTTP Components comunemente utilizzato non ha mai un timeout, pertanto i timeout devono essere impostati in modo esplicito. Inoltre, come procedura ottimale, questi timeout non devono superare i 60 secondi.

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

### Le API prodotto annotate con @ProviderType non devono essere implementate o estese dai clienti {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

**Chiave**: Dipendenze CQBP-84, CQBP-84

**Tipo**: Bug

**Gravità**: Critico

**Dal** momento: Versione 2018.7.0

L’API AEM contiene interfacce e classi Java che devono essere utilizzate solo con il codice personalizzato, ma che non devono essere implementate. Ad esempio, l’interfaccia *com.day.cq.wcm.api.Page* è progettata per essere implementata ***solo da AEM***.

Quando a queste interfacce vengono aggiunti nuovi metodi, essi non influiscono sul codice esistente che utilizza tali interfacce e, di conseguenza, l’aggiunta di nuovi metodi ad esse è considerata retrocompatibile. Tuttavia, se il codice personalizzato ***implementa*** una di queste interfacce, crea al cliente un rischio di retrocompatibilità con le versioni precedenti.

Le interfacce (e le classi) che devono essere implementate solo da AEM vengono annotate con *org.osgi.annotation.versioning.ProviderType* (o, in alcuni casi, con un&#39;annotazione precedente simile, *aQuute.bnd.annotation.ProviderType*). Questa regola identifica i casi in cui tale interfaccia viene implementata (o una classe viene estesa) dal codice personalizzato.

#### Codice non conforme {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### Gli oggetti ResourceResolver devono essere sempre chiusi {#resourceresolver-objects-should-always-be-closed}

**Chiave**: CQRules:CQBP-72

**Tipo**: Odore di codice

**Gravità**: Maggiore

**Dal** momento: Versione 2018.4.0

Gli oggetti ResourceResolver ottenuti da ResourceResolverFactory utilizzano le risorse di sistema. Sebbene siano in atto misure per recuperare tali risorse quando un oggetto ResourceResolver non è più in uso, è più efficiente chiudere esplicitamente qualsiasi oggetto ResourceResolver aperto chiamando il metodo close().

Un&#39;errata concezione relativamente comune è che gli oggetti ResourceResolver creati utilizzando una sessione JCR esistente non dovrebbero essere chiusi in modo esplicito, altrimenti la sessione JCR sottostante verrà chiusa. Questo non è il caso - indipendentemente dalla modalità di apertura di ResourceResolver, deve essere chiuso quando non viene più utilizzato. Poiché ResourceResolver implementa l&#39;interfaccia Closeable, è anche possibile utilizzare la sintassi try-with-resources invece di richiamare esplicitamente close().

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

### Non utilizzare i percorsi servlet Sling per registrare i servlet {#do-not-use-sling-servlet-paths-to-register-servlets}

**Chiave**: CQRules:CQBP-75

**Tipo**: Odore di codice

**Gravità**: Maggiore

**Dal** momento: Versione 2018.4.0

Come descritto nella documentazione [](http://sling.apache.org/documentation/the-sling-engine/servlets.html)Sling, i servlet di binding per percorsi sono scoraggiati. I servlet vincolati al percorso non possono utilizzare controlli di accesso JCR standard e, di conseguenza, richiedono un ulteriore rigore di sicurezza. Anziché utilizzare i servlet associati al percorso, si consiglia di creare nodi nel repository e registrare i servlet in base al tipo di risorsa.

#### Codice non conforme {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### Le eccezioni rilevate devono essere registrate o generate, ma non entrambe {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

**Chiave**: CQRules:CQBP-44—CatchAndLogOrThrow

**Tipo**: Odore di codice

**Gravità**: Minore

**Dal** momento: Versione 2018.4.0

In generale, un&#39;eccezione deve essere registrata esattamente una volta. Le eccezioni di registrazione più volte possono creare confusione in quanto non è chiaro quante volte si è verificata un&#39;eccezione. Il modello più comune che porta a questo è il taglio e la generazione di un&#39;eccezione colta.

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

### Evitare di avere un&#39;istruzione di registro immediatamente seguita da un&#39;istruzione di rilascio {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

**Chiave**: CQRules:CQBP-44—ConsecutivamenteLogAndThrow

**Tipo**: Odore di codice

**Gravità**: Minore

**Dal** momento: Versione 2018.4.0

Un altro pattern comune da evitare è quello di registrare un messaggio e di generare immediatamente un&#39;eccezione. Questo indica in genere che il messaggio di eccezione viene duplicato nei file di registro.

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

### Evitate di effettuare l&#39;accesso a INFO quando gestite le richieste GET o HEAD {#avoid-logging-at-info-when-handling-get-or-head-requests}

**Chiave**: CQRules:CQBP-44—LogInfoInGetOrHeadRequests

**Tipo**: Odore di codice

**Gravità**: Minore

In generale, il livello di registro INFO deve essere utilizzato per delimitare le azioni importanti e, per impostazione predefinita, AEM è configurato per il login al livello INFO o superiore. I metodi GET e HEAD dovrebbero essere sempre operazioni di sola lettura e quindi non costituiscono azioni importanti. La registrazione a livello INFO in risposta a richieste GET o HEAD potrebbe creare un disturbo significativo del registro, rendendo più difficile l&#39;identificazione di informazioni utili nei file di registro. La registrazione durante la gestione delle richieste GET o HEAD deve essere a livello di AVVISO o ERRORE quando qualcosa è andato storto o a livello di DEBUG o TRACE, se utili informazioni più approfondite sulla risoluzione dei problemi.

>[!CAUTION]
>
>Ciò non si applica alla registrazione di access.log per ogni richiesta.

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

**Chiave**: CQRules:CQBP-44—ExceptionGetMessageIsFirstLogParam

**Tipo**: Odore di codice

**Gravità**: Minore

**Dal** momento: Versione 2018.4.0

Come procedura ottimale, i messaggi di registro dovrebbero fornire informazioni contestuali sulla posizione in cui si è verificata un&#39;eccezione nell&#39;applicazione. Anche se il contesto può essere determinato anche tramite l&#39;uso di tracce dello stack, in generale il messaggio di registro sarà più semplice da leggere e comprendere. Di conseguenza, durante la registrazione di un&#39;eccezione, è una procedura non corretta utilizzare il messaggio dell&#39;eccezione come messaggio di registro. Il messaggio di eccezione conterrà ciò che è andato storto, mentre il messaggio di registro dovrebbe essere utilizzato per comunicare al lettore di log cosa stava facendo l&#39;applicazione quando si è verificata l&#39;eccezione. Il messaggio di eccezione verrà comunque registrato; specificando il proprio messaggio, i registri saranno più facili da comprendere.

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

### L&#39;accesso ai blocchi catch deve essere a livello AVVISO o ERRORE {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

**Chiave**: CQRules:CQBP-44—WrongLogLevelInCatchBlock

**Tipo**: Odore di codice

**Gravità**: Minore

**Dal** momento: Versione 2018.4.0

Come suggerisce il nome, le eccezioni Java devono sempre essere utilizzate in circostanze *eccezionali* . Di conseguenza, quando viene rilevata un&#39;eccezione, è importante assicurarsi che i messaggi di registro siano registrati al livello appropriato, ovvero AVVERTENZA o ERRORE. In questo modo i messaggi verranno visualizzati correttamente nei registri.

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

### Non stampare le tracce dello stack nella console {#do-not-print-stack-traces-to-the-console}

**Chiave**: CQRules:CQBP-44—ExceptionPrintStackTrace

**Tipo**: Odore di codice

**Gravità**: Minore

**Dal** momento: Versione 2018.4.0

Come già detto, il contesto è fondamentale per comprendere i messaggi di registro. Se si utilizza Exception.printStackTrace(), **solo** la traccia dello stack viene restituita al flusso di errore standard, perdendo così tutto il contesto. Inoltre, in un’applicazione multi-thread come AEM, se vengono stampate più eccezioni utilizzando questo metodo in parallelo, le tracce dello stack possono sovrapporsi e creare confusione significativa. Le eccezioni devono essere registrate solo tramite il framework di registrazione.

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

### Non trasmettere l&#39;output a Standard Output o Standard Error {#do-not-output-to-standard-output-or-standard-error}

**Chiave**: CQRules:CQBP-44—LogLevelConsolePrinters

**Tipo**: Odore di codice

**Gravità**: Minore

**Dal** momento: Versione 2018.4.0

L’accesso in AEM deve essere sempre effettuato tramite il framework di registrazione (SLF4J). L&#39;output diretto ai flussi di output standard o di errore standard perde le informazioni strutturali e contestuali fornite dal framework di registrazione e può, in alcuni casi, causare problemi di prestazioni.

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

**Chiave**: CQRules:CQBP-71

**Tipo**: Odore di codice

**Gravità**: Minore

**Dal** momento: Versione 2018.4.0

In generale, i percorsi che iniziano con /libs e /apps non devono essere hardcoded in quanto i percorsi a cui fanno riferimento sono generalmente memorizzati come percorsi relativi al percorso di ricerca Sling (che per impostazione predefinita è impostato su /libs,/apps). L’utilizzo del percorso assoluto potrebbe introdurre lievi difetti che verrebbero visualizzati solo successivamente nel ciclo di vita del progetto.

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

### Il Programma Sling Non Deve Essere Utilizzato {#sonarqube-sling-scheduler}

**Chiave**: CQRules:AMSCORE-554

**Tipo**: Odore di codice

**Gravità**: Minore

**Dal** momento: Versione 2020.5.0

Sling Scheduler non deve essere utilizzato per le attività che richiedono un&#39;esecuzione garantita. I processi pianificati Sling garantiscono l’esecuzione e sono più adatti sia per gli ambienti cluster che per quelli non cluster.

Per ulteriori informazioni sulla gestione dei processi Sling in ambienti cluster, consultate [Apache Sling Eventing and Job Handling](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html) .

### Le API obsolete di AEM non devono essere utilizzate {#sonarqube-aem-deprecated}

**Chiave**: AMSCORE-553

**Tipo**: Odore di codice

**Gravità**: Minore

**Dal** momento: Versione 2020.5.0

La superficie dell’API AEM è soggetta a revisioni costanti per identificare le API per le quali l’utilizzo è scoraggiato e quindi considerato obsoleto.

In molti casi, queste API sono obsolete utilizzando l&#39;annotazione standard Java *@Deprecated* e, come tali, identificata da `squid:CallToDeprecatedMethod`.

Tuttavia, in alcuni casi un’API è obsoleta nel contesto di AEM ma potrebbe non essere obsoleta in altri contesti. Questa regola identifica questa seconda classe.

## Regole contenuto OakPAL {#oakpal-rules}

Di seguito sono riportati i controlli OakPAL eseguiti da Cloud Manager.

>[!NOTE]
>OakPAL è un framework sviluppato da un partner AEM (e vincitore di AEM Rockstar North America 2019) che convalida i pacchetti di contenuto utilizzando un repository Oak standalone.

### I pacchetti cliente non devono creare o modificare nodi in /libs {#oakpal-customer-package}

**Chiave**: BanningPaths

**Tipo**: Bug

**Gravità**: Blocco

**Dal** momento: Versione 2019.6.0

È stata una procedura consigliata di vecchia data che la struttura di contenuti /libs nell’archivio dei contenuti di AEM venga considerata di sola lettura dai clienti. La modifica di nodi e proprietà in */libs* comporta rischi significativi per gli aggiornamenti principali e secondari. Le modifiche a */libs* devono essere apportate solo da Adobe attraverso canali ufficiali.

### I pacchetti non devono contenere configurazioni OSGi duplicate {#oakpal-package-osgi}

**Chiave**: DuplicateOsgiConfigurations

**Tipo**: Bug

**Gravità**: Maggiore

**Dal** momento: Versione 2019.6.0

Un problema comune che si verifica in progetti complessi è rappresentato dalla configurazione ripetuta dello stesso componente OSGi. Ciò crea un&#39;ambiguità sulla configurazione che sarà operativa. Questa regola è &quot;in modalità di esecuzione&quot; in quanto identifica solo i problemi per i quali lo stesso componente è configurato più volte nella stessa modalità di esecuzione (o combinazione di modalità di esecuzione).

#### Codice non conforme {#non-compliant-code-osgi}

```+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### Codice conforme {#compliant-code-osgi}

```+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### Le cartelle di configurazione e installazione devono contenere solo nodi OSGi {#oakpal-config-install}

**Chiave**: ConfigAndInstallShouldOnlyContainOsgiNodes

**Tipo**: Bug

**Gravità**: Maggiore

**Dal** momento: Versione 2019.6.0

Per motivi di sicurezza, i percorsi contenenti */config/ e /install/* sono leggibili solo dagli utenti amministrativi in AEM e devono essere utilizzati solo per la configurazione OSGi e i bundle OSGi. Posizionando altri tipi di contenuto in percorsi che contengono questi segmenti, il comportamento dell&#39;applicazione varia involontariamente tra utenti amministrativi e non amministrativi.

Un problema comune è rappresentato dall’uso di nodi denominati `config` nelle finestre di dialogo dei componenti o quando si specifica la configurazione dell’editor Rich Text per la modifica in linea. Per risolvere questo problema, il nodo che ha commesso l&#39;errore deve essere rinominato in un nome conforme. Per la configurazione dell&#39;editor Rich Text, utilizzate la `configPath` proprietà sul `cq:inplaceEditing` nodo per specificare la nuova posizione.

#### Codice non conforme {#non-compliant-code-config-install}

```
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    + config [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

#### Codice conforme {#compliant-code-config-install}

```
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    ./configPath = inplaceEditingConfig (String)
    + inplaceEditingConfig [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

### I Pacchetti Non Devono Sovrapporsi {#oakpal-no-overlap}

**Chiave**: PackageOverlaps

**Tipo**: Bug

**Gravità**: Maggiore

**Dal** momento: Versione 2019.6.0

Simili ai *pacchetti Non devono contenere configurazioni OSGi duplicate* si tratta di un problema comune nei progetti complessi in cui lo stesso percorso nodo è scritto da più pacchetti di contenuto separati. Anche se è possibile utilizzare le dipendenze del pacchetto di contenuti per garantire un risultato coerente, è meglio evitare sovrapposizioni del tutto.

### La Modalità Di Authoring Predefinita Non Deve Essere Interfaccia Classica {#oakpal-default-authoring}

**Chiave**: ClassicUIAuthoringMode

**Tipo**: Odore di codice

**Gravità**: Minore

**Dal** momento: Versione 2020.5.0

La configurazione OSGi `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` definisce la modalità di authoring predefinita in AEM. Poiché l’interfaccia classica è obsoleta a partire da AEM 6.4, ora viene generato un problema quando la modalità di authoring predefinita è configurata per l’interfaccia classica.

### I Componenti Con Finestre Di Dialogo Devono Avere Finestre Di Dialogo Touch {#oakpal-components-dialogs}

**Chiave**: ComponentWithOnlyClassicUIDialog

**Tipo**: Odore di codice

**Gravità**: Minore

**Dal** momento: Versione 2020.5.0

I componenti AEM che dispongono di una finestra di dialogo dell’interfaccia classica devono sempre disporre di una finestra di dialogo dell’interfaccia utente touch per fornire un’esperienza di authoring ottimale e per essere compatibili con il modello di distribuzione del servizio cloud, in cui l’interfaccia classica non è supportata. Questa regola verifica i seguenti scenari:

* Un componente con una finestra di dialogo dell’interfaccia classica (ovvero un nodo secondario della finestra di dialogo) deve avere una finestra di dialogo dell’interfaccia utente touch corrispondente (ovvero un nodo `cq:dialog` secondario).
* Un componente con una finestra di dialogo per la progettazione dell’interfaccia classica (ad es. un nodo design_dialog) deve avere una finestra di dialogo corrispondente per la progettazione dell’interfaccia utente touch (ovvero un nodo `cq:design_dialog` secondario).
* Un componente con una finestra di dialogo per l’interfaccia classica e una finestra di dialogo per la progettazione dell’interfaccia classica deve avere una finestra di dialogo per l’interfaccia utente touch corrispondente e una finestra di dialogo per la progettazione dell’interfaccia touch corrispondente.

La documentazione Strumenti di modernizzazione AEM fornisce documentazione e strumenti per la conversione dei componenti dall’interfaccia classica all’interfaccia utente touch. Per ulteriori informazioni, consultate [Strumenti](https://opensource.adobe.com/aem-modernize-tools/pages/tools.html) di modernizzazione AEM.

### I pacchetti non devono mescolare contenuto variabile e immutabile {#oakpal-packages-immutable}

**Chiave**: ImmutableMeableMixedPackage

**Tipo**: Odore di codice

**Gravità**: Minore

**Dal** momento: Versione 2020.5.0

Per essere compatibile con il modello di distribuzione del servizio cloud, i singoli pacchetti di contenuto devono contenere contenuti per le aree immutabili dell&#39;archivio (ovvero, non `/apps and /libs, although /libs` devono essere modificati dal codice cliente e causeranno una violazione separata) o l&#39;area modificabile (ovvero tutto il resto), ma non entrambi. Ad esempio, un pacchetto che include entrambi `/apps/myco/components/text and /etc/clientlibs/myco` non è compatibile con il servizio cloud e causerà la segnalazione di un problema.

Per ulteriori informazioni, consultate Struttura [progetto](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) AEM.

### Gli Agenti Di Replica Inverti Non Devono Essere Utilizzati {#oakpal-reverse-replication}

**Chiave**: ReverseReplication

**Tipo**: Odore di codice

**Gravità**: Minore

**Dal** momento: Versione 2020.5.0

Il supporto per la replica inversa non è disponibile nelle distribuzioni del servizio cloud, come descritto nelle note [sulla versione: Rimozione degli agenti](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/release-notes/aem-cloud-changes.html#replication-agents)di replica.

I clienti che utilizzano la replica inversa devono contattare Adobe per trovare soluzioni alternative.

