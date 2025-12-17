---
title: Test dell’interfaccia utente
description: I test personalizzati dell’interfaccia utente sono una funzionalità facoltativa che consente di creare ed eseguire automaticamente i test dell’interfaccia utente per le applicazioni personalizzate.
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 770318fd14e28c8406650eb563df36fe88227359
workflow-type: tm+mt
source-wordcount: '2662'
ht-degree: 53%

---


# Test dell’interfaccia utente {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="Test dell’interfaccia utente"
>abstract="I test dell’interfaccia utente personalizzati sono una funzione facoltativa che consente di creare ed eseguire automaticamente i test dell’interfaccia utente per le applicazioni. I test dell’interfaccia utente sono test basati su Selenium inseriti in un’immagine Docker per consentire un’ampia scelta in termini di linguaggio e framework. Come Java e Maven, Node e WebDriver.io o qualsiasi altro framework e tecnologia basati su Selenium."

I test dell’interfaccia utente personalizzati sono una funzione facoltativa che consente di creare ed eseguire automaticamente i test dell’interfaccia utente per le applicazioni.

## Panoramica {#custom-ui-testing}

AEM fornisce una suite integrata di [gate di qualità di Cloud Manager](/help/implementing/cloud-manager/custom-code-quality-rules.md) per garantire una fluida esperienza di aggiornamento delle applicazioni personalizzate. In particolare, i gate di test IT supportano già la creazione e automazione dei test personalizzati utilizzando le API di AEM.

I test dell’interfaccia utente sono inclusi in un’immagine Docker per consentire un’ampia scelta in termini di linguaggio e framework (come Cypress, Selenium, Java e Maven e JavaScript). Inoltre, un progetto di test dell&#39;interfaccia utente può essere facilmente generato utilizzando [Archetipo progetto AEM](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/developing/archetype/overview).

Adobe incoraggia l’utilizzo di Cypress, in quanto offre il ricaricamento in tempo reale e l’attesa automatica, che consente di risparmiare tempo e migliora la produttività durante il test. Cypress fornisce anche una sintassi semplice e intuitiva, che lo rende facile da imparare e utilizzare, anche per gli utenti che non conoscono ancora i test.

I test dell&#39;interfaccia utente vengono eseguiti come gate di qualità nel passaggio [**Test dell&#39;interfaccia utente personalizzati**](/help/implementing/cloud-manager/deploy-code.md), obbligatorio nelle [pipeline di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) e facoltativo nelle [pipeline non di produzione](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md). Tutti i test dell’interfaccia utente, compresi la regressione e le nuove funzionalità, consentono di rilevare e segnalare gli errori.

A differenza dei test funzionali personalizzati, che sono test HTTP scritti in Java, i test dell’interfaccia utente possono essere un’immagine Docker. I test possono essere scritti in qualsiasi lingua, purché rispettino le convenzioni definite nella sezione [Generazione dei test dell&#39;interfaccia utente](#building-ui-tests).

>[!TIP]
>
>Adobe consiglia di utilizzare Cypress per i test dell’interfaccia utente, seguendo il codice fornito nell’[Archivio degli esempi di test di AEM](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-cypress).
> 
>Adobe fornisce anche esempi di moduli di test dell’interfaccia utente basati su JavaScript con WebdriverIO (consulta [Archetipo progetto AEM](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)) e Java con WebDriver (consulta [Archivio degli esempi di test AEM](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver)).

## Introduzione ai test dell’interfaccia utente {#get-started-ui-tests}

In questa sezione vengono descritti i passaggi necessari per configurare i test dell’interfaccia utente per l’esecuzione in Cloud Manager.

1. Decidi il framework di test da utilizzare.

   * Per Cypress (impostazione predefinita), utilizza il codice di esempio dell&#39;archivio [AEM Test Samples](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-cypress) oppure il codice di esempio generato automaticamente nella cartella `ui.tests` dell&#39;archivio Cloud Manager.

   * Per Playwright, utilizza il codice di esempio dall&#39;[archivio degli esempi di test di AEM](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-playwright).

   * Per Webdriver.IO, utilizzare il codice di esempio dell&#39;archivio [AEM Test Samples](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-wdio).

   * Per Selenium WebDriver, utilizzare il codice di esempio dell&#39;archivio [AEM Test Samples](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-selenium-webdriver).

   * Per altri linguaggi di programmazione, consulta la sezione [Creazione dei test dell’interfaccia utente](#building-ui-tests) di questo documento per configurare il progetto di test.

1. Assicurati che i test dell’interfaccia utente siano attivati come secondo la sezione [Consenso del cliente](#customer-opt-in) di questo documento.

1. Sviluppa gli esempi di test e [eseguili in locale](#run-ui-tests-locally).

1. Salvare il codice nell’archivio di Cloud Manager ed eseguire una pipeline di Cloud Manager.

## Creazione dei test dell’interfaccia utente {#building-ui-tests}

Un progetto Maven genera un contesto di build Docker. Questo contesto build di Docker descrive come creare un’immagine Docker contenente i test dell’interfaccia utente che Cloud Manager utilizza per generare un’immagine Docker contenente i test effettivi dell’interfaccia utente.

In questa sezione vengono descritti i passaggi necessari per aggiungere un progetto di test dell’interfaccia utente all’archivio.

>[!TIP]
>
>L’[archetipo progetto AEM](https://github.com/adobe/aem-project-archetype), se non disponi di requisiti speciali per il linguaggio di programmazione, può generare un progetto di test dell’interfaccia utente che è conforme alla seguente descrizione.

### Generare un contesto di build Docker {#generate-docker-build-context}

Per generare un contesto build Docker è necessario un modulo Maven che:

* Produca un archivio contenente un `Dockerfile` e tutti gli altri file necessari per generare un’immagine Docker con i testi.
* Aggiunga all’archivio il tag con il classificatore `ui-test-docker-context`.

Il modo più semplice consiste nel configurare il [plug-in Maven Assembly](https://maven.apache.org/plugins/maven-assembly-plugin/) per creare l&#39;archivio di contesto di build Docker e assegnare a questo il classificatore corretto.

Puoi creare i test dell’interfaccia utente con diverse tecnologie e framework, ma questa sezione presuppone che il progetto sia simile al seguente.

```text
├── Dockerfile
├── assembly-ui-test-docker-context.xml
├── pom.xml
├── test-module
│   ├── package.json
│   ├── index.js
│   └── wdio.conf.js
└── wait-for-grid.sh
```

Il file `pom.xml` si occupa della build Maven. Aggiungi un’esecuzione simile alla seguente al plug-in Maven Assembly.

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-assembly-plugin</artifactId>
    <configuration>
        <descriptors>
            <descriptor>${project.basedir}/assembly-ui-test-docker-context.xml</descriptor>
        </descriptors>
        <tarLongFileMode>gnu</tarLongFileMode>
    </configuration>
    <executions>
        <execution>
            <id>make-assembly</id>
            <phase>package</phase>
            <goals>
                <goal>single</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

Questa esecuzione indica al plug-in Maven Assembly di creare un archivio in base alle istruzioni contenute in `assembly-ui-test-docker-context.xml`, che prende il nome di **descrittore assembly** nel gergo del plug-in. Il descrittore assembly elenca tutti i file che devono far parte dell’archivio.

```xml
<assembly>
    <id>ui-test-docker-context</id>
    <includeBaseDirectory>false</includeBaseDirectory>
    <formats>
        <format>tar.gz</format>
    </formats>
    <fileSets>
        <fileSet>
            <directory>${basedir}</directory>
            <includes>
                <include>Dockerfile</include>
                <include>wait-for-grid.sh</include>
            </includes>
        </fileSet>
        <fileSet>
            <directory>${basedir}/test-module</directory>
            <excludes>
                <exclude>node/**</exclude>
                <exclude>node_modules/**</exclude>
                <exclude>reports/**</exclude>
            </excludes>
        </fileSet>
    </fileSets>
</assembly>
```

Il descrittore assembly fornisce al plug-in istruzioni per creare un archivio di tipo `.tar.gz` e assegna a questo il classificatore `ui-test-docker-context`. Inoltre, elenca i file che devono essere inclusi nell’archivio, inclusi i seguenti:

* Un `Dockerfile`, obbligatorio per la generazione dell’immagine Docker
* Lo script `wait-for-grid.sh`, le cui finalità sono descritte di seguito
* I test effettivi dell’interfaccia utente, implementati da un progetto Node.js nella cartella `test-module`

Il descrittore assembly esclude inoltre alcuni file che potrebbero essere generati durante l’esecuzione locale dei test dell’interfaccia utente. Questo garantisce un archivio di dimensioni minori e generazioni più veloci.

Cloud Manager raccoglie automaticamente l’archivio del contesto di build Docker e crea l’immagine di test durante le pipeline di distribuzione. Alla fine, Cloud Manager esegue l’immagine Docker per eseguire i test dell’interfaccia utente per l’applicazione.

La generazione deve produrre zero archivi o un unico archivio. Se non produce archivi, il passaggio di test viene superato per impostazione predefinita. Se la generazione produce più di un archivio, l’archivio selezionato non è deterministico.

### Consenso del cliente {#customer-opt-in}

Affinché a Cloud Manager possa generare ed eseguire i test dell’interfaccia utente, devi fornire il consenso esplicito alla funzione aggiungendo un file all’archivio.

* Il nome file deve essere `testing.properties`.
* Il contenuto del file deve essere `ui-tests.version=1`.
* Il file deve trovarsi nel modulo secondario Maven per i test dell’interfaccia utente accanto al file `pom.xml` del modulo secondario dei test dell’interfaccia utente.
* Il file deve trovarsi nella radice del file `tar.gz` integrato.

Se il file non è presente, la build e le esecuzioni dei test dell’interfaccia utente vengono ignorate.

Per includere un file `testing.properties` nell’artefatto della build, aggiungi un’istruzione `include` nel file `assembly-ui-test-docker-context.xml`.

```xml
[...]
<includes>
    <include>Dockerfile</include>
    <include>wait-for-grid.sh</include>
    <include>testing.properties</include> <!-- opt-in test module in Cloud Manager -->
</includes>
[...]
```

>[!IMPORTANT]
>
>Se il progetto non include questa riga, modifica il file per fornire il consenso esplicito ai test dell’interfaccia utente.
>
>Il file può contenere una riga con la dicitura *DO NOT MODIFY*. Si tratta semplicemente di un avviso legacy proveniente da modelli/esempi precedenti e *non* ti impedisce di apportare le modifiche di consenso necessarie per i test dell&#39;interfaccia utente di Cloud Manager. Puoi ignorare l&#39;avviso; puoi modificare `assembly-ui-test-docker-context.xml` e `pom.xml` nel *tuo progetto* seguendo i passaggi di consenso (ad esempio, per includere `testing.properties`).

Se utilizzi gli esempi forniti da Adobe:

* Per la cartella `ui.tests` basata su JavaScript generata in base all’[archetipo progetto AEM](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests), puoi eseguire il comando seguente per aggiungere la configurazione richiesta.

  ```shell
  echo "ui-tests.version=1" > testing.properties
  
  if ! grep -q "testing.properties" "assembly-ui-test-docker-context.xml"; then
    awk -v line='                <include>testing.properties</include>' '/<include>wait-for-grid.sh<\/include>/ { printf "%s\n%s\n", $0, line; next }; 1' assembly-ui-test-docker-context.xml > assembly-ui-test-docker-context.xml.new && mv assembly-ui-test-docker-context.xml.new assembly-ui-test-docker-context.xml
  fi
  ```

* Gli esempi di test Cypress e Java Selenium forniti da Adobe dispongono già del flag Opt-in impostato.

## Scrittura dei test dell’interfaccia utente {#writing-ui-tests}

Questa sezione descrive le convenzioni da seguire per l’immagine Docker contenente i test dell’interfaccia utente. L’immagine Docker viene generata in base al contesto di build Docker descritto nella sezione precedente.

### Variabili di ambiente {#environment-variables}

In fase di esecuzione, all’immagine Docker vengono passate le seguenti variabili di ambiente a seconda del framework.

>[!NOTE]
>
> Questi valori vengono impostati automaticamente durante l’esecuzione della pipeline; non è necessario impostarli manualmente come variabili della pipeline.

| Variabile | Esempi | Descrizione | Test del framework |
|----------------------------|----------------------------------|----------------------------------------------------------------------------------------------------|---------------------|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | URL del server Selenium | Solo Selenium |
| `SELENIUM_BROWSER` | `chrome` | Implementazione del browser utilizzata dal server Selenium | Solo Selenium |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | URL dell’istanza di AEM Author | Tutti |
| `AEM_AUTHOR_USERNAME` | `admin` | Nome utente per accedere all’istanza Autore AEM | Tutti |
| `AEM_AUTHOR_PASSWORD` | `admin` | Password per accedere all’istanza di AEM Author | Tutti |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | URL dell’istanza AEM Publishing | Tutti* |
| `AEM_PUBLISH_USERNAME` | `admin` | Nome utente per accedere all’istanza di pubblicazione di AEM | Tutti* |
| `AEM_PUBLISH_PASSWORD` | `admin` | Password per accedere all’istanza di pubblicazione di AEM | Tutti* |
| `REPORTS_PATH` | `/usr/src/app/reports` | Percorso in cui deve essere salvato il report XML dei risultati del test | Tutti |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | URL in cui caricare il file per renderli accessibili al framework di test | Tutti |
| `PROXY_HOST` | `proxy-host` | Nome host del proxy HTTP interno che deve essere utilizzato dal framework di test | Tutti tranne Selenio |
| `PROXY_HTTPS_PORT` | `8071` | Porta di attesa del server proxy per le connessioni HTTPS (può essere vuota) | Tutti tranne Selenio |
| `PROXY_HTTP_PORT` | `8070` | Porta di attesa del server proxy per le connessioni HTTP (può essere vuota) | Tutti tranne Selenio |
| `PROXY_CA_PATH` | `/path/to/root_ca.pem` | Percorso del certificato CA che deve essere utilizzato dal framework di test | Tutti tranne Selenio |
| `PROXY_OBSERVABILITY_PORT` | `8081` | Porta HTTP `healthcheck` del server proxy | Tutti tranne Selenio |
| `PROXY_RETRY_ATTEMPTS` | `12` | Numero consigliato di tentativi durante l&#39;attesa della disponibilità del server proxy | Tutti tranne Selenio |
| `PROXY_RETRY_DELAY` | `5` | Ritardo consigliato tra i tentativi durante l’attesa della disponibilità del server proxy | Tutti tranne Selenio |

`* these values will be empty if there is no publish instance`

Gli esempi di test di Adobe forniscono funzioni di supporto per accedere ai parametri di configurazione:

Cypress: utilizza la funzione standard `Cypress.env('VARIABLE_NAME')`
<!-- BOTH URLs are 404 JavaScript: See the [`lib/config.js`](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests.wdio/test-module/lib/config.js) module
* Java: See the [`Config`](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/Config.java) class -->

### Generare rapporti sui test {#generate-test-reports}

L’immagine Docker deve generare rapporti sui test in formato JUnit XML e salvarli nel percorso specificato dalla variabile di ambiente `REPORTS_PATH`. Il formato JUnit XML è ampiamente utilizzato per la generazione di rapporti sui risultati dei test. Se l’immagine Docker utilizza Java e Maven, i moduli di test standard come [Maven Surefire Plug-in](https://maven.apache.org/surefire/maven-surefire-plugin/) e [Maven Failsafe Plug-in](https://maven.apache.org/surefire/maven-failsafe-plugin/) possono generare tali rapporti in modo preconfigurato.

Se implementi l’immagine Docker con altri linguaggi di programmazione o esecuzione di test, consulta la documentazione relativa agli strumenti scelti per sapere come generare rapporti JUnit XML.

>[!NOTE]
>
>Il risultato della fase di test dell’interfaccia utente viene valutato solo in base ai rapporti dei test. Assicurati di generare un rapporto conforme all’esecuzione del test.
>
>Utilizza le asserzioni invece di registrare un errore in STDERR o di restituire un codice di uscita diverso da zero; in caso contrario, la pipeline di distribuzione potrebbe procedere normalmente.
>
>Se durante l&#39;esecuzione dei test è stato utilizzato un proxy HTTP, i risultati includono un file `request.log`.

### Prerequisiti {#prerequisites}

* I test in Cloud Manager sono eseguiti utilizzando un utente amministratore tecnico.

>[!NOTE]
>
>Per eseguire i test funzionali dal computer locale, crea un utente con autorizzazioni di tipo amministratore per ottenere lo stesso comportamento.

* L&#39;infrastruttura a contenitori per il test funzionale è limitata dai seguenti vincoli:

| Tipo | Valore | Descrizione |
|----------------------|-------|-----------------------------------------------------------------------|
| CPU | 2.0 | Quantità di tempo CPU riservato per esecuzione del test. |
| Memoria | 1Gi | Quantità di memoria allocata al test. Il valore è espresso in gibibiti. |
| Timeout | 30 min | Durata dell’esecuzione del test. |
| Durata consigliata | 15 min | Adobe consiglia di mantenere i test entro questo limite di tempo. |

* Se l’istanza di authoring/pubblicazione di destinazione è protetta dall’inserire nell&#39;elenco Consentiti di IP, è necessario inserire nell&#39;elenco Consentiti l’infrastruttura di test dell’interfaccia utente della pipeline oppure i test dell’interfaccia utente possono non riuscire con 403 Forbidden (Non consentito).
Vedi anche [Errore del test dell&#39;interfaccia utente in AEMaaCS a causa di un&#39;Inserire nell&#39;elenco Consentiti del IP &#x200B;](https://experienceleague.adobe.com/it/docs/experience-cloud-kcs/kbarticles/ka-26654#) e [Introduzione ai Inserisce nell&#39;elenco Consentiti di IP](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

>[!NOTE]
>
> Se hai bisogno di più risorse, crea un caso di assistenza clienti e descrivi il tuo caso d’uso; Adobe esamina la tua richiesta e fornisce assistenza appropriata.

## Dettagli specifici per Selenium

>[!NOTE]
>
>Questa sezione si applica solo quando Selenium è l’infrastruttura per i test scelta.

### Attendere che Selenium sia pronto {#waiting-for-selenium}

Prima dell’avvio dei test, l’immagine Docker verifica che il server Selenium sia in esecuzione. L’attesa del servizio Selenium è un processo a due fasi.

1. È possibile leggere l’URL del servizio Selenium dalla variabile di ambiente `SELENIUM_BASE_URL`.
1. Esegui il polling a intervalli regolari dell&#39;endpoint di stato [&#128279;](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready) esposto dall&#39;API Selenium.

Dopo aver ricevuto una risposta positiva dall’endpoint di stato di Selenium è possibile avviare i test.

Gli esempi di test dell&#39;interfaccia utente di Adobe utilizzano `wait-for-grid.sh`. Viene eseguito all’avvio del Docker e avvia i test solo dopo che la griglia è pronta.


### Acquisire schermate e video {#capture-screenshots}

L’immagine Docker può generare un output di test aggiuntivo (ad esempio schermate o video) e salvarlo nel percorso specificato dalla variabile di ambiente `REPORTS_PATH`. Qualsiasi file trovato sotto `REPORTS_PATH` è incluso nell’archivio dei risultati del test.

Gli esempi di test forniti da Adobe per impostazione predefinita creano screenshot per tutti i test non riusciti.

Puoi utilizzare le funzioni di assistenza per creare screenshot tramite i test.

<!-- BOTH URLS ARE 404
* JavaScript: [takeScreenshot command](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/commons.js)
* Java: [Commands](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/Commands.java) -->

Se durante l&#39;esecuzione di un test dell&#39;interfaccia utente viene creato un archivio dei risultati del test, è possibile scaricarlo da Cloud Manager facendo clic sul pulsante `Download Details` nel passaggio [**Test dell&#39;interfaccia utente personalizzati**](/help/implementing/cloud-manager/deploy-code.md).

### Carica file {#upload-files}

I test a volte richiedono il caricamento di file nell’applicazione sottoposta a test. Per mantenere flessibile la distribuzione di Selenium rispetto ai test, non è possibile caricare una risorsa direttamente in Selenium. Per caricare un file è necessario seguire la procedura riportata di seguito.

1. Carica il file nell’URL specificato dalla variabile di ambiente `UPLOAD_URL`.
   * Il caricamento deve essere eseguito in un’unica richiesta POST con modulo multipart.
   * Il modulo multipart deve presentare un singolo campo di file.
   * Equivalente a `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`.
   * Per informazioni su come eseguire una tale richiesta HTTP, consulta la documentazione e le librerie del linguaggio di programmazione utilizzato nell’immagine Docker.

   <!-- BOTH URLS ARE 404
   * The Adobe test samples provide helper functions for uploading files:
     * JavaScript: See the [getFileHandleForUpload](https://github.com/adobe/aem-project-archetype/blob/develop/src/main/archetype/ui.tests/test-module/lib/wdio.commands.js) command.
     * Java: See the [FileHandler](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/test-module/src/main/java/com/adobe/cq/cloud/testing/ui/java/ui/tests/lib/FileHandler.java) class. -->

1. Se il caricamento ha esito positivo, la richiesta restituisce una risposta `200 OK` di tipo `text/plain`.
   * Il contenuto della risposta è un handle di file opaco.
   * È possibile utilizzare questo handle al posto del percorso file in un elemento `<input>` per i test del caricamento dei file nell’applicazione.

## Dettagli specifici di Cypress

>[!NOTE]
>
>Questa sezione si applica solo quando Cypress è l’infrastruttura di test scelta.

### Configurare il proxy HTTP

Il punto di ingresso del contenitore Docker deve verificare il valore della variabile di ambiente `PROXY_HOST`.

Se questo valore è vuoto, non sono necessari passaggi aggiuntivi e i test devono essere eseguiti senza utilizzare un proxy HTTP.

Se non è vuoto, lo script entrypoint deve:

1. Configurare una connessione proxy HTTP per l&#39;esecuzione dei test dell&#39;interfaccia utente esportando la variabile di ambiente `HTTP_PROXY` creata utilizzando i valori seguenti:
   * Host proxy, fornito dalla variabile `PROXY_HOST`
   * Porta proxy, fornita dalla variabile `PROXY_HTTPS_PORT` o `PROXY_HTTP_PORT` (viene utilizzata la variabile con un valore non vuoto)
2. Impostare il certificato CA utilizzato per la connessione al proxy HTTP. La sua posizione è fornita dalla variabile `PROXY_CA_PATH`.
   * Esporta variabile di ambiente `NODE_EXTRA_CA_CERTS`.
3. Attendi che il proxy HTTP sia pronto.
   * Per verificare l&#39;idoneità, è possibile utilizzare le variabili di ambiente `PROXY_HOST`, `PROXY_OBSERVABILITY_PORT`, `PROXY_RETRY_ATTEMPTS` e `PROXY_RETRY_DELAY`.
   * È possibile verificare utilizzando una richiesta cURL, assicurandosi di installare cURL in `Dockerfile`.

Un esempio di implementazione è disponibile nel punto di ingresso del modulo di test Cypress Sample su [GitHub](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-cypress/test-module/run.sh).

## Dettagli specifici del playwright

>[!NOTE]
>
> Questa sezione si applica solo quando `Playwright` è l&#39;infrastruttura di test scelta.

### Configurare il proxy HTTP

>[!NOTE]
>
> Negli esempi presentati, Adobe presuppone che Chrome sia utilizzato come browser del progetto.

Analogamente a Cypress, i test devono utilizzare il proxy HTTP se viene fornita una variabile di ambiente `PROXY_HOST` non vuota.

In tal caso, è necessario apportare le seguenti modifiche.

#### Dockerfile

Installa cURL e `libnss3-tools`, che fornisce `certutil.`

```dockerfile
RUN apt -y update \
    && apt -y --no-install-recommends install curl libnss3-tools \
    && rm -rf /var/lib/apt/lists/*
```

#### Script Entrypoint

Includere uno script di base che, nel caso in cui venga fornita la variabile di ambiente `PROXY_HOST`, esegua le operazioni seguenti:

1. Esporta variabili relative al proxy come `HTTP_PROXY` e `NODE_EXTRA_CA_CERTS`
2. Utilizzare `certutil` per installare il certificato CA proxy per Chromium™.
3. Attendi che il proxy HTTP sia pronto (o esci in caso di errore).

Esempio di implementazione:

```bash
# setup proxy environment variables and CA certificate
if [ -n "${PROXY_HOST:-}" ]; then
  if [ -n "${PROXY_HTTPS_PORT:-}" ]; then
    export HTTP_PROXY="https://${PROXY_HOST}:${PROXY_HTTPS_PORT}"
  elif [ -n "${PROXY_HTTP_PORT:-}" ]; then
    export HTTP_PROXY="http://${PROXY_HOST}:${PROXY_HTTP_PORT}"
  fi
  if [ -n "${PROXY_CA_PATH:-}" ]; then
    echo "installing certificate"
    mkdir -p $HOME/.pki/nssdb
    certutil -d sql:$HOME/.pki/nssdb -A -t "CT,c,c" -n "EaaS Client Proxy Root" -i $PROXY_CA_PATH
    export NODE_EXTRA_CA_CERTS=${PROXY_CA_PATH}
  fi
  if [ -n "${PROXY_OBSERVABILITY_PORT:-}" ] && [ -n "${HTTP_PROXY:-}" ]; then
    echo "waiting for proxy"
    curl --silent  --retry ${PROXY_RETRY_ATTEMPTS:-3} --retry-connrefused --retry-delay ${PROXY_RETRY_DELAY:-10} \
      --proxy ${HTTP_PROXY} --proxy-cacert ${PROXY_CA_PATH:-""} \
      ${PROXY_HOST}:${PROXY_OBSERVABILITY_PORT}
    if [ $? -ne 0 ]; then
      echo "proxy is not ready"
      exit 1
    fi
  fi
fi
```

#### Configurazione playwright

Modificare la configurazione del playwright (ad esempio in `playwright.config.js`) per utilizzare un proxy nel caso in cui sia impostata la variabile di ambiente `HTTP_PROXY`.

Esempio di implementazione:

```javascript
const proxyServer = process.env.HTTP_PROXY || ''
```

```javascript
// enable proxy if set
if (proxyServer !== '') {
 cfg.use.proxy = {
  server: proxyServer,
 }
}
```

>[!NOTE]
>
> Un esempio di implementazione si trova nel modulo di prova di esempio Playwright su [GitHub](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-playwright).


## Eseguire i test dell’interfaccia utente localmente {#run-ui-tests-locally}

Prima di attivare i test dell&#39;interfaccia utente in una pipeline di Cloud Manager, Adobe consiglia di eseguire i test dell&#39;interfaccia utente in locale con [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md). In alternativa, esegui su un’istanza AEM as a Cloud Service effettiva.

### Campione di prova Cypress {#cypress-sample}

1. Apri una shell e passa alla cartella `ui.tests/test-module` nell’archivio

1. Installa Cypress e altri prerequisiti

   ```shell
   npm install
   ```

1. Imposta le variabili di ambiente necessarie per l’esecuzione dei test

   ```shell
   export AEM_AUTHOR_URL=https://author-<program-id>-<environment-id>.adobeaemcloud.com
   export AEM_AUTHOR_USERNAME=<user>
   export AEM_AUTHOR_PASSWORD=<password>
   export AEM_PUBLISH_URL=https://publish-<program-id>-<environment-id>.adobeaemcloud.com
   export AEM_PUBLISH_USERNAME=<user>
   export AEM_PUBLISH_PASSWORD=<password>
   export REPORTS_PATH=target/
   ```

1. Esegui i test con uno dei seguenti comandi

   ```shell
   npm test              # Using default Cypress browser
   npm run test-chrome   # Using Google Chrome browser
   npm run test-firefox  # Using Firefox browser
   ```

>[!NOTE]
>
>I file di registro vengono archiviati nella cartella `target/` dell’archivio.
>
>Per informazioni dettagliate, vedere l&#39;[archivio degli esempi di test di AEM](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-cypress/test-module/README.md).

### Esempio di test di JavaScript WebdriverIO {#javascript-sample}

1. Apri una shell e passa alla cartella `ui.tests` nell’archivio.

1. Esegui il seguente comando per avviare i test utilizzando Maven.

   ```shell
   mvn verify -Pui-tests-local-execution \
    -DAEM_AUTHOR_URL=https://author-<program-id>-<environment-id>.adobeaemcloud.com \
    -DAEM_AUTHOR_USERNAME=<user> \
    -DAEM_AUTHOR_PASSWORD=<password> \
    -DAEM_PUBLISH_URL=https://publish-<program-id>-<environment-id>.adobeaemcloud.com \
    -DAEM_PUBLISH_USERNAME=<user> \
    -DAEM_PUBLISH_PASSWORD=<password>
   ```

>[!NOTE]
>
>* Questo comando avvia un’istanza Selenium indipendente ed esegue i test su di essa.
>* I file di registro vengono archiviati nella cartella `target/reports` dell’archivio.
>* È necessario assicurarsi che la macchina esegua la versione più recente di Chrome perché il test scarica automaticamente l’ultima versione di ChromeDriver per eseguire il test.
>
>Per informazioni dettagliate, vedere l&#39;[archivio degli esempi di test di AEM](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-wdio).

### Esempio di prova di Playwright {#playwright-sample}

1. Apri una shell e passa alla cartella `ui.tests` nell’archivio

1. Esegui il comando seguente per creare un’immagine docker con Maven

   ```shell
   mvn clean package -Pui-tests-docker-build
   ```

1. Esegui il comando seguente per avviare i test utilizzando Maven

   ```shell
   mvn verify -Pui-tests-docker-execution \
    -DAEM_AUTHOR_URL=https://author-<program-id>-<environment-id>.adobeaemcloud.com \
    -DAEM_AUTHOR_USERNAME=<user> \
    -DAEM_AUTHOR_PASSWORD=<password> \
    -DAEM_PUBLISH_URL=https://publish-<program-id>-<environment-id>.adobeaemcloud.com \
    -DAEM_PUBLISH_USERNAME=<user> \
    -DAEM_PUBLISH_PASSWORD=<password>
   ```

>[!NOTE]
>
>I file di registro vengono archiviati nella cartella `target/` dell’archivio.
>
>Per informazioni dettagliate, vedere l&#39;[archivio degli esempi di test di AEM](https://github.com/adobe/aem-test-samples/tree/aem-cloud/ui-playwright).


### Esempio di test Java Selenium WebDriver {#java-sample}

1. Apri una shell e passa alla cartella `ui.tests/test-module` nell’archivio

1. Esegui i comandi seguenti per avviare i test utilizzando Maven

   ```shell
   # Start selenium docker image
   # we mount /tmp/shared as a shared volume that will be used between selenium and the test module for uploads
   docker run -d -p 4444:4444 -v /tmp/shared:/tmp/shared selenium/standalone-chromium:latest
   
   # Run the tests using the previously started Selenium instance
   mvn verify -Pui-tests-local-execution -DSELENIUM_BASE_URL=http://<server>:4444
   ```

>[!NOTE]
>
>I file di registro vengono archiviati nella cartella `target/reports` dell’archivio.
>
>Per informazioni dettagliate, vedere l&#39;[archivio degli esempi di test di AEM](https://github.com/adobe/aem-test-samples/blob/aem-cloud/ui-selenium-webdriver/README.md).
