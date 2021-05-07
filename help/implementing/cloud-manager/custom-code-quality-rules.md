---
title: Regole per la qualità del codice personalizzato - Cloud Services
description: Regole per la qualità del codice personalizzato - Cloud Services
exl-id: f40e5774-c76b-4c84-9d14-8e40ee6b775b
translation-type: tm+mt
source-git-commit: f6c700f82bc5a1a3edf05911a29a6e4d32dd3f72
workflow-type: tm+mt
source-wordcount: '3302'
ht-degree: 4%

---

# Regole per la qualità del codice personalizzato {#custom-code-quality-rules}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_customcodequalityrules"
>title="Regole per la qualità del codice personalizzato"
>abstract="Questa pagina descrive le regole di qualità del codice personalizzato eseguite da Cloud Manager create in base alle best practice di AEM Engineering."

Questa pagina descrive le regole di qualità del codice personalizzato eseguite da Cloud Manager create in base alle best practice di AEM Engineering.

>[!NOTE]
>I campioni di codice qui forniti hanno solo scopo illustrativo. Per informazioni sui concetti e sulle regole di qualità di SonarQube, consulta [Concetti](https://docs.sonarqube.org/7.4/user-guide/concepts/) .

## Regole SonarQube {#sonarqube-rules}

La sezione seguente evidenzia le regole SonarQube :

### Non utilizzare funzioni potenzialmente pericolose {#do-not-use-potentially-dangerous-functions}

**Chiave**: CQRules:CWE-676

**Tipo**: Vulnerabilità

**Gravità**: Maggiore

**Da**: Versione 2018.4.0

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

**Da**: Versione 2018.4.0

L&#39;utilizzo di una stringa di formato da un&#39;origine esterna (come un parametro di richiesta o contenuto generato dall&#39;utente) può generare può esporre un&#39;applicazione al rifiuto di attacchi del servizio. In alcune circostanze una stringa di formato può essere controllata esternamente, ma è consentita solo da fonti attendibili.

#### Codice non conforme {#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text"));
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### Le richieste HTTP devono sempre avere socket e timeout di connessione {#http-requests-should-always-have-socket-and-connect-timeouts}

**Chiave**: CQRules:ConnectionTimeoutMechanism

**Tipo**: Bug

**Gravità**: Critico

**Da**: Versione 2018.6.0

Durante l’esecuzione di richieste HTTP dall’interno di un’applicazione AEM, è fondamentale assicurarsi che siano configurati timeout appropriati al fine di evitare un consumo di thread inutile. Sfortunatamente, il comportamento predefinito sia del client HTTP predefinito di Java (java.net.HttpUrlConnection) che del client dei componenti HTTP Apache comunemente utilizzato non prevede mai il timeout, pertanto i timeout devono essere impostati in modo esplicito. Inoltre, come best practice, questi timeout non devono superare i 60 secondi.

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

### Le API del prodotto annotate con @ProviderType non devono essere implementate o estese dai clienti {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

**Chiave**: Dipendenze CQBP-84, CQBP-84

**Tipo**: Bug

**Gravità**: Critico

**Da**: Versione 2018.7.0

L’API AEM contiene interfacce e classi Java che devono essere utilizzate solo con il codice personalizzato, ma che non devono essere implementate. Ad esempio, l’interfaccia *com.day.cq.wcm.api.Page* è progettata per essere implementata ***solo da AEM***.

Quando a queste interfacce vengono aggiunti nuovi metodi, essi non influiscono sul codice esistente che utilizza tali interfacce e, di conseguenza, l’aggiunta di nuovi metodi ad esse è considerata retrocompatibile. Tuttavia, se il codice personalizzato ***implementa*** una di queste interfacce, crea al cliente un rischio di retrocompatibilità con le versioni precedenti.

Le interfacce (e le classi) che devono essere implementate solo da AEM vengono annotate con *org.osgi.annotation.versioning.ProviderType* (o, in alcuni casi, con un&#39;annotazione legacy simile *aQute.bnd.annotation.ProviderType*). Questa regola identifica i casi in cui tale interfaccia viene implementata (o una classe viene estesa) dal codice personalizzato.

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

**Da**: Versione 2018.4.0

Gli oggetti ResourceResolver ottenuti da ResourceResolverFactory utilizzano risorse di sistema. Sebbene esistano misure per recuperare queste risorse quando un ResourceResolver non è più in uso, è più efficiente chiudere in modo esplicito gli oggetti ResourceResolver aperti chiamando il metodo close() .

Un&#39;errata concezione relativamente comune è che gli oggetti ResourceResolver creati utilizzando una sessione JCR esistente non dovrebbero essere chiusi in modo esplicito o che così facendo chiuderà la sessione JCR sottostante. Ciò non accade - indipendentemente da come viene aperto un ResourceResolver, deve essere chiuso quando non viene più utilizzato. Poiché ResourceResolver implementa l&#39;interfaccia Closeable, è anche possibile utilizzare la sintassi try-with-resources invece di richiamare esplicitamente close().

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

**Chiave**: CQRules:CQBP-75

**Tipo**: Odore di codice

**Gravità**: Maggiore

**Da**: Versione 2018.4.0

Come descritto nella [documentazione Sling](http://sling.apache.org/documentation/the-sling-engine/servlets.html), i servlet di binding per percorsi sono scoraggiati. I servlet associati al percorso non possono utilizzare controlli di accesso JCR standard e, di conseguenza, richiedono un ulteriore rigore di sicurezza. Invece di utilizzare i servlet associati al percorso, si consiglia di creare nodi nell’archivio e registrare i servlet in base al tipo di risorsa.

#### Codice non conforme {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### Le eccezioni rilevate devono essere registrate o lanciate, ma non entrambe {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

**Chiave**: CQRules:CQBP-44—CatchAndOrLogOrThrow

**Tipo**: Odore di codice

**Gravità**: Minore

**Da**: Versione 2018.4.0

In generale, un&#39;eccezione dovrebbe essere registrata esattamente una volta. La registrazione di eccezioni più volte può causare confusione in quanto non è chiaro quante volte si è verificata un&#39;eccezione. Il modello più comune che porta a questo è la registrazione e il lancio di un&#39;eccezione colta.

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

### Evita di avere un’istruzione di registro immediatamente seguita da un’istruzione di tipo &quot;drill&quot; {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

**Chiave**: CQRules:CQBP-44—ConsecutivamenteLogAndThrow

**Tipo**: Odore di codice

**Gravità**: Minore

**Da**: Versione 2018.4.0

Un altro pattern comune da evitare è quello di registrare un messaggio e quindi lanciare immediatamente un’eccezione. Questo indica in genere che il messaggio di eccezione verrà duplicato nei file di log.

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

### Evita la registrazione a INFO quando gestisci le richieste GET o HEAD {#avoid-logging-at-info-when-handling-get-or-head-requests}

**Chiave**: CQRules:CQBP-44—LogInfoInGetOrHeadRequests

**Tipo**: Odore di codice

**Gravità**: Minore

In generale, il livello di log INFO deve essere utilizzato per delimitare azioni importanti e, per impostazione predefinita, AEM è configurato per il log al livello INFO o superiore. I metodi di GET e HEAD devono essere sempre di sola lettura e non costituiscono pertanto azioni importanti. È probabile che la registrazione a livello INFO in risposta alle richieste di GET o HEAD generi un notevole rumore di log, rendendo così più difficile identificare informazioni utili nei file di log. La registrazione durante la gestione delle richieste di GET o HEAD deve essere a livello di WARN o ERROR quando si è verificato un errore o a livello di DEBUG o di TRACE se è utile fornire informazioni più approfondite sulla risoluzione dei problemi.

>[!CAUTION]
>
>Questo non si applica alla registrazione del tipo access.log per ogni richiesta.

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

**Da**: Versione 2018.4.0

Come best practice, i messaggi di log devono fornire informazioni contestuali su dove si è verificata un’eccezione nell’applicazione. Anche se il contesto può essere determinato anche tramite l&#39;uso di tracce di stack, in generale il messaggio di log sarà più facile da leggere e comprendere. Di conseguenza, quando si registra un&#39;eccezione, è una cattiva prassi utilizzare il messaggio dell&#39;eccezione come messaggio di log - il messaggio di eccezione conterrà ciò che è andato storto, mentre il messaggio di log dovrebbe essere utilizzato per dire a un lettore di log cosa stava facendo l&#39;applicazione quando si è verificata l&#39;eccezione. Il messaggio di eccezione sarà ancora registrato; specificando il tuo messaggio i registri saranno più facili da comprendere.

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

### L&#39;accesso ai blocchi di blocco deve essere al livello WARN o ERROR {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

**Chiave**: CQRules:CQBP-44—WrongLogLevelInCatchBlock

**Tipo**: Odore di codice

**Gravità**: Minore

**Da**: Versione 2018.4.0

Come suggerisce il nome, le eccezioni Java devono sempre essere utilizzate in circostanze *eccezionali*. Di conseguenza, quando viene rilevata un&#39;eccezione, è importante assicurarsi che i messaggi di log siano registrati al livello appropriato, ovvero WARN o ERROR. In questo modo i messaggi verranno visualizzati correttamente nei registri.

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

### Non stampare tracce di stack nella console {#do-not-print-stack-traces-to-the-console}

**Chiave**: CQRules:CQBP-44—ExceptionPrintStackTrace

**Tipo**: Odore di codice

**Gravità**: Minore

**Da**: Versione 2018.4.0

Come accennato, il contesto è fondamentale per comprendere i messaggi di log. Se si utilizza Exception.printStackTrace(), **solo** la traccia dello stack viene trasmessa al flusso di errore standard, perdendo così tutto il contesto. Inoltre, in un&#39;applicazione multi-thread come AEM se vengono stampate più eccezioni utilizzando questo metodo in parallelo, le loro tracce di stack possono sovrapporsi e creare confusione significativa. Le eccezioni devono essere registrate solo tramite il framework di registrazione.

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

### Non trasmettere in uscita standard o errore standard {#do-not-output-to-standard-output-or-standard-error}

**Chiave**: CQRules:CQBP-44—LogLevelConsolePrinters

**Tipo**: Odore di codice

**Gravità**: Minore

**Da**: Versione 2018.4.0

L’accesso AEM deve sempre essere effettuato tramite il framework di registrazione (SLF4J). L’output diretto nei flussi di errore standard o standard perde le informazioni strutturali e contestuali fornite dal framework di registrazione e può, in alcuni casi, causare problemi di prestazioni.

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

**Chiave**: CQRules:CQBP-71

**Tipo**: Odore di codice

**Gravità**: Minore

**Da**: Versione 2018.4.0

In generale, i percorsi che iniziano con /libs e /apps non devono essere codificati in quanto i percorsi a cui si riferiscono sono generalmente memorizzati come percorsi relativi al percorso di ricerca Sling (che è impostato su /libs,/apps per impostazione predefinita). L&#39;utilizzo del percorso assoluto può presentare difetti sottili che appariranno solo successivamente nel ciclo di vita del progetto.

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

### Lo scheduler Sling non deve essere utilizzato {#sonarqube-sling-scheduler}

**Chiave**: CQRules:AMSCORE-554

**Tipo**: Compatibilità Cloud Service/odore del codice

**Gravità**: Minore

**Da**: Versione 2020.5.0

Lo strumento di pianificazione Sling non deve essere utilizzato per attività che richiedono un’esecuzione garantita. I processi pianificati Sling garantiscono l’esecuzione e sono più adatti sia per gli ambienti cluster che per quelli non cluster.

Per ulteriori informazioni sulla gestione dei processi Sling in ambienti cluster, consulta [Eventi Sling Apache e Gestione processi](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html) .

### AEM Le API obsolete non devono essere utilizzate {#sonarqube-aem-deprecated}

**Chiave**: AMSCORE-553

**Tipo**: Compatibilità Cloud Service/odore del codice

**Gravità**: Minore

**Da**: Versione 2020.5.0

La superficie dell’API AEM è soggetta a una revisione costante per identificare le API per le quali l’utilizzo è scoraggiato e quindi considerato obsoleto.

In molti casi, queste API sono obsolete utilizzando l’annotazione Java *@Deprecated* e, in quanto tali, identificata da `squid:CallToDeprecatedMethod` standard.

Tuttavia, in alcuni casi un’API è obsoleta nel contesto di AEM ma potrebbe non essere deprecata in altri contesti. Questa regola identifica questa seconda classe.

## Regole di contenuto OakPAL {#oakpal-rules}

Di seguito sono riportati i controlli OakPAL eseguiti da Cloud Manager.

>[!NOTE]
>OakPAL è un framework sviluppato da un partner AEM (e vincitore del 2019 AEM Rockstar Nord America) che convalida i pacchetti di contenuti utilizzando un archivio Oak indipendente.

### I pacchetti cliente non devono creare o modificare nodi sotto /libs {#oakpal-customer-package}

**Chiave**: PercorsiBanning

**Tipo**: Bug

**Gravità**: Blocco

**Da**: Versione 2019.6.0

È stata una best practice consolidata che la struttura di contenuti /libs nell’archivio dei contenuti AEM debba essere considerata di sola lettura dai clienti. La modifica di nodi e proprietà in */libs* crea rischi significativi per gli aggiornamenti principali e secondari. Le modifiche a */libs* devono essere effettuate solo per Adobe attraverso i canali ufficiali.

### I pacchetti non devono contenere configurazioni OSGi duplicate {#oakpal-package-osgi}

**Chiave**: DuplicateOsgiConfigurations

**Tipo**: Bug

**Gravità**: Maggiore

**Da**: Versione 2019.6.0

Un problema comune che si verifica in progetti complessi è che lo stesso componente OSGi è configurato più volte. Questo crea un’ambiguità riguardo alla configurazione utilizzabile. Questa regola è &quot;in base alla modalità di esecuzione&quot; in quanto identificherà solo i problemi in cui lo stesso componente è configurato più volte nella stessa modalità di esecuzione (o combinazione di modalità di esecuzione).

>[!NOTE]
>Questa regola produrrà problemi in cui la stessa configurazione, allo stesso percorso, è definita in più pacchetti, compresi i casi in cui lo stesso pacchetto è duplicato nell&#39;elenco complessivo dei pacchetti generati. Ad esempio, se la build produce pacchetti denominati `com.myco:com.myco.ui.apps` e `com.myco:com.myco.all` in cui `com.myco:com.myco.all` incorpora `com.myco:com.myco.ui.apps`, tutte le configurazioni in `com.myco:com.myco.ui.apps` verranno riportate come duplicati. In genere si tratta di un caso in cui non si seguono le [linee guida per la struttura del pacchetto di contenuti](/help/implementing/developing/introduction/aem-project-content-package-structure.md); in questo esempio specifico, al pacchetto `com.myco:com.myco.ui.apps` manca la proprietà `<cloudManagerTarget>none</cloudManagerTarget>` .

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

### Le cartelle di configurazione e installazione devono contenere solo i nodi OSGi {#oakpal-config-install}

**Chiave**: ConfigAndInstallShouldOnlyContainOsgiNodes

**Tipo**: Bug

**Gravità**: Maggiore

**Da**: Versione 2019.6.0

Per motivi di sicurezza, i percorsi contenenti */config/ e /install/* sono leggibili solo dagli utenti amministratori in AEM e devono essere utilizzati solo per la configurazione OSGi e i bundle OSGi. Posizionare altri tipi di contenuto in percorsi che contengono questi segmenti determina un comportamento dell’applicazione che varia involontariamente tra utenti amministrativi e non amministrativi.

Un problema comune è l’utilizzo di nodi denominati `config` nelle finestre di dialogo dei componenti o quando si specifica la configurazione dell’editor Rich Text per la modifica in linea. Per risolvere questo problema, il nodo che ha commesso l&#39;infrazione deve essere rinominato in un nome conforme. Per la configurazione dell’editor Rich Text, utilizza la proprietà `configPath` sul nodo `cq:inplaceEditing` per specificare la nuova posizione.

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

### I pacchetti non devono sovrapporsi {#oakpal-no-overlap}

**Chiave**: PackageOverlaps

**Tipo**: Bug

**Gravità**: Maggiore

**Da**: Versione 2019.6.0

Simile ai *Pacchetti non devono contenere configurazioni OSGi duplicate*, si tratta di un problema comune nei progetti complessi in cui lo stesso percorso nodo viene scritto da più pacchetti di contenuto separati. Quando si utilizzano le dipendenze dei pacchetti di contenuti per garantire un risultato coerente, è meglio evitare completamente sovrapposizioni.

### La modalità di authoring predefinita non deve essere un’interfaccia classica {#oakpal-default-authoring}

**Chiave**: ClassicUIAuthoringMode

**Tipo**: Compatibilità Cloud Service/odore del codice

**Gravità**: Minore

**Da**: Versione 2020.5.0

La configurazione OSGi `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` definisce la modalità di authoring predefinita all’interno di AEM. Poiché l’interfaccia utente classica è stata dichiarata obsoleta a partire dalla versione 6.4 di AEM, ora viene generato un problema quando la modalità di authoring predefinita è configurata nell’interfaccia classica.

### I componenti con finestre di dialogo devono avere finestre di dialogo dell&#39;interfaccia touch {#oakpal-components-dialogs}

**Chiave**: Finestra di dialogo ComponentWithOnlyClassicUID

**Tipo**: Compatibilità Cloud Service/odore del codice

**Gravità**: Minore

**Da**: Versione 2020.5.0

I componenti AEM che dispongono di una finestra di dialogo dell’interfaccia classica devono sempre avere una finestra di dialogo corrispondente per fornire un’esperienza di authoring ottimale ed essere compatibili con il modello di distribuzione del Cloud Service, dove l’interfaccia classica non è supportata. Questa regola verifica i seguenti scenari:

* Un componente con una finestra di dialogo dell’interfaccia classica (cioè un nodo figlio di finestra di dialogo) deve avere una finestra di dialogo corrispondente dell’interfaccia Touch (cioè, un nodo figlio `cq:dialog`).
* Un componente con una finestra di dialogo di progettazione dell’interfaccia classica (ad esempio un nodo design_dialog) deve avere una finestra di dialogo corrispondente per la progettazione dell’interfaccia Touch (cioè, un nodo figlio `cq:design_dialog`).
* Un componente con una finestra di dialogo di interfaccia classica e una finestra di dialogo di progettazione dell’interfaccia classica deve avere sia una finestra di dialogo corrispondente dell’interfaccia utente touch sia una finestra di dialogo corrispondente di progettazione dell’interfaccia touch.

La documentazione sugli strumenti di modernizzazione AEM fornisce documentazione e strumenti per la conversione dei componenti dall’interfaccia classica all’interfaccia utente touch. Per ulteriori informazioni, consulta [Strumenti di modernizzazione AEM](https://opensource.adobe.com/aem-modernize-tools/pages/tools.html) .

### I pacchetti non devono mixare contenuto variabile e immutabile {#oakpal-packages-immutable}

**Chiave**: ImmutableMeableMixedPackage

**Tipo**: Compatibilità Cloud Service/odore del codice

**Gravità**: Minore

**Da**: Versione 2020.5.0

Per essere compatibile con il modello di distribuzione del Cloud Service, i singoli pacchetti di contenuto devono contenere contenuto per le aree immutabili dell’archivio (ovvero, `/apps and /libs, although /libs` non deve essere modificato dal codice cliente e causerà una violazione separata) o l’area mutabile (ovvero tutto il resto), ma non entrambe. Ad esempio, un pacchetto che include sia `/apps/myco/components/text and /etc/clientlibs/myco` non è compatibile con il Cloud Service e causerà la segnalazione di un problema.

Per ulteriori informazioni, consulta [AEM Struttura del progetto](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) .

### Gli Agenti Di Replica Inversa Non Devono Essere Utilizzati {#oakpal-reverse-replication}

**Chiave**: ReverseReplication

**Tipo**: Compatibilità Cloud Service/odore del codice

**Gravità**: Minore

**Da**: Versione 2020.5.0

Il supporto per la replica inversa non è disponibile nelle distribuzioni di Cloud Service, come descritto in [Note sulla versione: Rimozione degli agenti di replica](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/release-notes/aem-cloud-changes.html#replication-agents).

I clienti che utilizzano la replica inversa devono contattare l&#39;Adobe per le soluzioni alternative.

### OakPAL - Le risorse contenute nelle librerie client abilitate per il proxy devono trovarsi in una cartella denominata risorse {#oakpal-resources-proxy}

**Chiave**: ClientlibProxyResource

**Tipo**: Bug

**Gravità**: Minore

**Da**: Versione 2021.2.0

AEM librerie client possono contenere risorse statiche come immagini e font. Come descritto in [Utilizzo di preprocessori](/help/implementing/developing/introduction/clientlibs.md#using-preprocessors), quando si utilizzano librerie client proxy, queste risorse statiche devono essere contenute in una cartella figlio denominata resources per poter essere effettivamente referenziate sulle istanze di pubblicazione.

#### Codice non conforme {#non-compliant-proxy-enabled}

```
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + images
        + myimage.jpg
```

#### Codice conforme {#compliant-proxy-enabled}

```
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + resources
        + myimage.jpg
```

### OakPAL - Utilizzo dei processi di workflow non compatibili del Cloud Service {#oakpal-usage-cloud-service}

**Chiave**: CloudServiceIncompatibleWorkflowProcess

**Tipo**: Bug

**Gravità**: Maggiore

**Da**: Versione 2021.2.0

Con il passaggio ai micro-servizi Asset per l’elaborazione delle risorse AEM Cloud Service, diversi processi del flusso di lavoro utilizzati nelle versioni on-premise e AMS di AEM sono diventati non supportati o non necessari. Lo strumento di migrazione all&#39;indirizzo [aem-cloud-migration](https://github.com/adobe/aem-cloud-migration) può essere utilizzato per aggiornare i modelli di flusso di lavoro durante AEM migrazione del Cloud Service.

### OakPAL - L&#39;utilizzo dei modelli statici è sconsigliato a favore dei modelli modificabili {#oakpal-static-template}

**Chiave**: StaticTemplateUsage

**Tipo**: Odore di codice

**Gravità**: Minore

**Da**: Versione 2021.2.0

Anche se l’utilizzo di modelli statici è sempre stato molto comune nei progetti AEM, i modelli modificabili sono altamente consigliati in quanto offrono la massima flessibilità e supportano funzionalità aggiuntive non presenti nei modelli statici. Ulteriori informazioni sono disponibili su [Modelli di pagina.](/help/implementing/developing/components/templates.md) La migrazione da modelli statici a modificabili può essere in gran parte automatizzata tramite gli  [AEM strumenti](https://opensource.adobe.com/aem-modernize-tools/) di modernizzazione.

### OakPAL - L&#39;utilizzo di componenti di base legacy è scoraggiato {#oakpal-usage-legacy}

**Chiave**: UsoComponenteLegacyFoundation

**Tipo**: Odore di codice

**Gravità**: Minore

**Da**: Versione 2021.2.0

I componenti di base legacy (ovvero i componenti in `/libs/foundation`) sono stati dichiarati obsoleti per diverse versioni AEM a favore dei componenti core WCM. L’utilizzo dei componenti di base legacy come base per i componenti personalizzati, sia per sovrapposizione che per ereditarietà, viene scoraggiato e deve essere convertito nel componente di base corrispondente. Questa conversione può essere facilitata dagli [AEM strumenti di modernizzazione](https://opensource.adobe.com/aem-modernize-tools/).

### OakPAL - Devono essere utilizzati solo i nomi e l&#39;ordinamento della modalità di esecuzione supportati {#oakpal-supported-runmodes}

**Chiave**: Modalità di esecuzione supportata

**Tipo**: Odore di codice

**Gravità**: Minore

**Da**: Versione 2021.2.0

AEM Cloud Service applica un criterio di denominazione rigoroso per i nomi in modalità runmode e un ordine rigoroso per tali modalità di esecuzione. L&#39;elenco delle modalità di esecuzione supportate può essere trovato su [Modalità di esecuzione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#runmodes) e qualsiasi deviazione da questo sarà identificato come un problema.

### OakPAL - I nodi di definizione dell&#39;indice di ricerca personalizzato devono essere figli diretti di /oak:index {#oakpal-custom-search}

**Chiave**: OakIndexLocation

**Tipo**: Odore di codice

**Gravità**: Minore

**Da**: Versione 2021.2.0

AEM Cloud Service richiede che le definizioni dell&#39;indice di ricerca personalizzata (cioè i nodi di tipo oak:QueryIndexDefinition) siano nodi figlio diretti di `/oak:index`. Gli indici in altre posizioni devono essere spostati per essere compatibili con AEM Cloud Service. Ulteriori informazioni sugli indici di ricerca sono disponibili su [Ricerca e indicizzazione dei contenuti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en).

### OakPAL - I nodi di definizione dell&#39;indice di ricerca personalizzato devono avere una versione compat di 2 {#oakpal-custom-search-compatVersion}

**Chiave**: IndexCompatVersion

**Tipo**: Odore di codice

**Gravità**: Minore

**Da**: Versione 2021.2.0

AEM Cloud Service richiede che la proprietà compatVersion sia impostata su 2 per le definizioni dell&#39;indice di ricerca personalizzata (ovvero i nodi di tipo oak:QueryIndexDefinition). Qualsiasi altro valore non è supportato dal Cloud Service AEM. Ulteriori informazioni sugli indici di ricerca sono disponibili su [Ricerca e indicizzazione dei contenuti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en).

### OakPAL - I nodi discendenti dei nodi di definizione dell&#39;indice di ricerca personalizzato devono essere di tipo nt:unstructured {#oakpal-descendent-nodes}

**Chiave**: IndexDescendantNodeType

**Tipo**: Odore di codice

**Gravità**: Minore

**Da**: Versione 2021.2.0

Difficile risolvere i problemi possono verificarsi quando si verifica un nodo di definizione dell&#39;indice di ricerca personalizzato con nodi figlio non ordinati. Per evitare questo problema, si consiglia che tutti i nodi discendenti di un nodo `oak:QueryIndexDefinition` siano di tipo nt:unstructured.

### OakPAL - I nodi di definizione dell&#39;indice di ricerca personalizzato devono contenere un nodo figlio denominato indexRules con elementi figlio {#oakpal-custom-search-index}

**Chiave**: IndexRulesNode

**Tipo**: Odore di codice

**Gravità**: Minore

**Da**: Versione 2021.2.0

Un nodo di definizione dell&#39;indice di ricerca personalizzato definito correttamente deve contenere un nodo figlio denominato indexRules che, a sua volta, deve avere almeno un figlio. Ulteriori informazioni sono disponibili su [Documentazione Oak](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

### OakPAL - I nodi di definizione dell&#39;indice di ricerca personalizzato devono seguire le convenzioni di denominazione {#oakpal-custom-search-definitions}

**Chiave**: NomeIndice

**Tipo**: Odore di codice

**Gravità**: Minore

**Da**: Versione 2021.2.0

AEM Cloud Service richiede che le definizioni degli indici di ricerca personalizzati (ovvero, i nodi di tipo `oak:QueryIndexDefinition`) siano denominati seguendo un pattern specifico descritto in [Ricerca e indicizzazione dei contenuti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#how-to-use).

### OakPAL - I nodi di definizione dell&#39;indice di ricerca personalizzato devono utilizzare il tipo di indice lucene {#oakpal-index-type-lucene}

**Chiave**: IndexType

**Tipo**: Odore di codice

**Gravità**: Minore

**Da**: Versione 2021.2.0

AEM Cloud Service richiede che le definizioni dell&#39;indice di ricerca personalizzata (cioè i nodi di tipo oak:QueryIndexDefinition) abbiano una proprietà type con il valore impostato su **lucene**. L&#39;indicizzazione utilizzando i tipi di indice legacy deve essere aggiornata prima della migrazione al Cloud Service AEM. Per ulteriori informazioni, consulta [Ricerca e indicizzazione dei contenuti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#how-to-use) .

### OakPAL - I nodi di definizione dell&#39;indice di ricerca personalizzato non devono contenere una proprietà denominata seed {#oakpal-property-name-seed}

**Chiave**: IndexSeedProperty

**Tipo**: Odore di codice

**Gravità**: Minore

**Da**: Versione 2021.2.0

AEM Cloud Service non consente alle definizioni degli indici di ricerca personalizzati (ovvero, nodi di tipo `oak:QueryIndexDefinition`) di contenere una proprietà denominata seed. L&#39;indicizzazione utilizzando questa proprietà deve essere aggiornata prima della migrazione al Cloud Service AEM. Per ulteriori informazioni, consulta [Ricerca e indicizzazione dei contenuti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#how-to-use) .

### OakPAL - I nodi di definizione dell&#39;indice di ricerca personalizzato non devono contenere una proprietà denominata reindex {#oakpal-reindex-property}

**Chiave**: IndexReindexProperty

**Tipo**: Odore di codice

**Gravità**: Minore

**Da**: Versione 2021.2.0

AEM Cloud Service non consente alle definizioni degli indici di ricerca personalizzati (ovvero, nodi di tipo `oak:QueryIndexDefinition`) di contenere una proprietà denominata reindex. L&#39;indicizzazione utilizzando questa proprietà deve essere aggiornata prima della migrazione al Cloud Service AEM. Per ulteriori informazioni, consulta [Ricerca e indicizzazione dei contenuti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#how-to-use) .
