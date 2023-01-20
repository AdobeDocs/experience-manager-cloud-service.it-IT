---
title: Test dell’interfaccia utente
description: I test personalizzati dell’interfaccia utente sono una funzionalità facoltativa che consente di creare ed eseguire automaticamente i test dell’interfaccia utente per le applicazioni personalizzate.
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
source-git-commit: 0ea7255f4dfc5c9f2e99cb144ef58152a2565822
workflow-type: tm+mt
source-wordcount: '1407'
ht-degree: 100%

---


# Test dell’interfaccia utente {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="Test dell’interfaccia utente"
>abstract="I test dell’interfaccia utente personalizzati sono una funzione facoltativa che consente di creare ed eseguire automaticamente i test dell’interfaccia utente per le applicazioni. I test dell’interfaccia utente sono test basati su Selenium inseriti in un’immagine Docker per consentire un’ampia scelta in termini di linguaggio e framework (come Java e Maven, Node e WebDriver.io o qualsiasi altro framework e tecnologia basati su Selenium)."

I test dell’interfaccia utente personalizzati sono una funzione facoltativa che consente di creare ed eseguire automaticamente i test dell’interfaccia utente per le applicazioni.

## Panoramica {#custom-ui-testing}

AEM fornisce una suite integrata di [gate di qualità di Cloud Manager](/help/implementing/cloud-manager/custom-code-quality-rules.md) per garantire una fluida esperienza di aggiornamento delle applicazioni personalizzate. In particolare, i gate di test IT già creano e automatizzano i test personalizzati utilizzando le API AEM.

I test dell’interfaccia utente sono test basati su Selenium inseriti in un’immagine Docker per consentire un’ampia scelta in termini di linguaggio e framework (come Java e Maven, Node e WebDriver.io o qualsiasi altro framework e tecnologia basati su Selenium). Inoltre, è possibile generare facilmente un progetto di test dell’interfaccia utente con l’[archetipo del progetto AEM.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it)

I test dell’interfaccia utente vengono eseguiti come parte di un gate di qualità specifico per ogni pipeline di Cloud Manager con il passaggio **[Test dell’interfaccia utente personalizzati** dedicato.](/help/implementing/cloud-manager/deploy-code.md) Tutti i test dell’interfaccia utente, compresi la regressione e le nuove funzionalità, consentono di rilevare e segnalare gli errori.

A differenza dei test funzionali personalizzati, che rappresentano test HTTP scritti in Java, i test dell’interfaccia utente possono essere un’immagine Docker con test scritti in qualsiasi linguaggio, purché rispettino le convenzioni definite nella sezione [Generazione dei test dell’interfaccia utente.](#building-ui-tests)

>[!TIP]
>
>Adobe consiglia di seguire la struttura e il linguaggio (JavaScript e WDIO) forniti nell’[archetipo del progetto AEM.](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests)

### Consenso del cliente {#customer-opt-in}

Affinché Cloud Manager possa generare ed eseguire i test dell’interfaccia utente, l’utente deve fornire il consenso esplicito alla funzione aggiungendo un file all’archivio.

* Il nome file deve essere `testing.properties`.
* Il contenuto del file deve essere `ui-tests.version=1`.
* Il file deve trovarsi nel modulo secondario Maven per i test dell’interfaccia utente accanto al file `pom.xml` del modulo secondario dei test dell’interfaccia utente.
* Il file deve trovarsi nella radice del file `tar.gz` integrato.

Se il file non è presente, la build e le esecuzioni dei test dell’interfaccia utente verranno ignorate.

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

>[!NOTE]
>
>Se il progetto non include questa riga, devi modificare il file per fornire il consenso esplicito ai test dell’interfaccia utente.
>
>Il file può contenere una riga che consiglia di non modificarla. Questo è dovuto all’aver introdotto la riga nel progetto prima che fosse stato introdotto il consenso per i test dell’interfaccia utente; i client non dovevano modificare il file. Puoi tranquillamente ignorarla.

## Creazione dei test dell’interfaccia utente {#building-ui-tests}

Un progetto Maven genera un contesto di build Docker. Tale contesto di build Docker descrive come creare un’immagine Docker contenente i test dell’interfaccia utente che gli utenti di Cloud Manager possono utilizzare per generare un’immagine Docker contenente i test effettivi dell’interfaccia utente.

In questa sezione vengono descritti i passaggi necessari per aggiungere un progetto di test dell’interfaccia utente all’archivio.

>[!TIP]
>
>Se non hai requisiti speciali per il linguaggio di programmazione, l’[archetipo del progetto AEM](https://github.com/adobe/aem-project-archetype) può generare un progetto di test dell’interfaccia utente automaticamente.

### Generare un contesto di build Docker {#generate-docker-build-context}

Per generare un contesto di build Docker è necessario un modulo Maven che:

* Produca un archivio contenente un `Dockerfile` e tutti gli altri file necessari per generare un’immagine Docker con i testi.
* Aggiunga all’archivio il tag con il classificatore `ui-test-docker-context`.

Il modo più semplice per eseguire l’operazione è configurare il [plug-in Maven Assembly](https://maven.apache.org/plugins/maven-assembly-plugin/) per creare l’archivio di contesto di build Docker e assegnare a questo il classificatore corretto.

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

Il descrittore assembly fornisce al plug-in istruzioni per creare un archivio di tipo `.tar.gz` e assegna a questo il classificatore `ui-test-docker-context`. Inoltre, elenca i file che devono essere inclusi nell’archivio, compresi quelli riportati di seguito.

* Un `Dockerfile`, obbligatorio per la generazione dell’immagine Docker
* Lo script `wait-for-grid.sh`, le cui finalità sono descritte di seguito
* I test effettivi dell’interfaccia utente, implementati da un progetto Node.js nella cartella `test-module`

Il descrittore assembly esclude inoltre alcuni file che potrebbero essere generati durante l’esecuzione locale dei test dell’interfaccia utente. Questo garantisce un archivio di dimensioni minori e generazioni più veloci.

L’archivio contenente il contesto di build Docker viene automaticamente selezionato da Cloud Manager, che crea l’immagine Docker contenente i test durante le pipeline di distribuzione. Infine, Cloud Manager esegue l’immagine Docker per eseguire i test dell’interfaccia utente per l’applicazione.

La generazione deve produrre zero archivi o un unico archivio. Se non produce archivi, il passaggio di test viene superato per impostazione predefinita. Se la generazione produce più di un archivio, l’archivio selezionato non è deterministico.

## Scrittura dei test dell’interfaccia utente {#writing-ui-tests}

Questa sezione descrive le convenzioni da seguire per l’immagine Docker contenente i test dell’interfaccia utente. L’immagine Docker viene generata in base al contesto di build Docker descritto nella sezione precedente.

### Variabili di ambiente {#environment-variables}

In fase di runtime, vengono passate all’immagine Docker le seguenti variabili di ambiente.

| Variabile | Esempi | Descrizione |
|---|---|---|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | URL del server Selenium |
| `SELENIUM_BROWSER` | `chrome` | Implementazione del browser utilizzata dal server Selenium |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | URL dell’istanza di AEM Author |
| `AEM_AUTHOR_USERNAME` | `admin` | Nome utente per accedere all’istanza di AEM Author |
| `AEM_AUTHOR_PASSWORD` | `admin` | Password per accedere all’istanza di AEM Author |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | URL dell’istanza di AEM Publish |
| `AEM_PUBLISH_USERNAME` | `admin` | Nome utente per accedere nell’istanza di AEM Publish |
| `AEM_PUBLISH_PASSWORD` | `admin` | Password per accedere all’istanza di AEM Publish |
| `REPORTS_PATH` | `/usr/src/app/reports` | Percorso in cui salvare il rapporto XML con i risultati del test |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | URL in cui caricare i file per renderli accessibili a Selenium |

### Attesa del servizio Selenium {#waiting-for-selenium}

Prima dell’avvio dei test, l’immagine Docker verifica che il server Selenium sia in esecuzione. L’attesa del servizio Selenium è un processo a due fasi.

1. È possibile leggere l’URL del servizio Selenium dalla variabile di ambiente `SELENIUM_BASE_URL`.
1. Utilizza il polling a intervalli regolari dell’[endpoint di stato](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready) esposto dall’API Selenium.

Dopo aver ricevuto una risposta positiva dall’endpoint di stato di Selenium è possibile avviare i test.

### Generazione dei rapporti sui test {#generate-test-reports}

L’immagine Docker deve generare rapporti sui test in formato JUnit XML e salvarli nel percorso specificato dalla variabile di ambiente `REPORTS_PATH`. Il formato JUnit XML è ampiamente utilizzato per la generazione di rapporti sui risultati dei test. Se l’immagine Docker utilizza Java e Maven, i moduli di test standard come [Maven Surefire Plug-in](https://maven.apache.org/surefire/maven-surefire-plugin/) e [Maven Failsafe Plug-in](https://maven.apache.org/surefire/maven-failsafe-plugin/) possono generare tali rapporti in modo preconfigurato.

Se implementi l’immagine Docker con altri linguaggi di programmazione o esecuzione di test, consulta la documentazione relativa agli strumenti scelti per sapere come generare rapporti JUnit XML.

### Acquisire schermate e video {#capture-screenshots}

L’immagine Docker può generare un output di test aggiuntivo (ad esempio schermate, video) e salvarli nel percorso specificato dalla variabile di ambiente `REPORTS_PATH`. Qualsiasi file trovato sotto `REPORTS_PATH` è incluso nell’archivio dei risultati del test.

Se durante l’esecuzione di un test dell’interfaccia utente è stato creato un archivio dei risultati del test, il file di registro del test contiene alla fine un riferimento alla posizione dell’archivio dei risultati del test.

```
[...]

===============================================================
The detailed test results can be downloaded from the URL below.
Note: the link will expire after 60 days

    https://results-host/test-results.zip

===============================================================
```

### Caricamento dei file {#upload-files}

I test a volte richiedono il caricamento di file nell’applicazione sottoposta a test. Al fine di mantenere la distribuzione di Selenium flessibile rispetto ai test, non è possibile caricare direttamente una risorsa in Selenium. Per caricare un file è necessario seguire la procedura riportata di seguito.

1. Carica il file nell’URL specificato dalla variabile di ambiente `UPLOAD_URL`.
   * Il caricamento deve essere eseguito in un’unica richiesta POST con modulo multipart.
   * Il modulo multipart deve presentare un singolo campo di file.
   * Questo equivale a `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`.
   * Per informazioni su come eseguire una tale richiesta HTTP, consulta la documentazione e le librerie del linguaggio di programmazione utilizzato nell’immagine Docker.
1. Se il caricamento ha esito positivo, la richiesta restituisce una risposta `200 OK` di tipo `text/plain`.
   * Il contenuto della risposta è un handle di file opaco.
   * È possibile utilizzare questo handle al posto del percorso file in un elemento `<input>` per i test del caricamento dei file nell’applicazione.
