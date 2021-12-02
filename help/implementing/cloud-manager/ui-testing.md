---
title: Test interfaccia utente - Cloud Services
description: Test interfaccia utente - Cloud Services
exl-id: 3009f8cc-da12-4e55-9bce-b564621966dd
source-git-commit: 02db915e114c2af8329eaddbb868045944a3574d
workflow-type: tm+mt
source-wordcount: '1617'
ht-degree: 1%

---

# Test dell&#39;interfaccia utente {#ui-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_uitesting"
>title="Test dell&#39;interfaccia utente"
>abstract="I test dell’interfaccia utente sono test basati su Selenium inseriti in un’immagine Docker per consentire un’ampia scelta in linguaggio e framework (come Java e Maven, Node e WebDriver.io o qualsiasi altro framework e tecnologia basati su Selenium). The Docker image can be created with standard tooling, but it must respect certain conventions during its execution. Quando si esegue l&#39;immagine Docker, viene eseguito automaticamente il provisioning di un server Selenium. Le convenzioni di runtime descritte di seguito consentono al codice di test di accedere sia al server Selenium che alle istanze AEM in fase di test."

UI tests are Selenium-based tests packaged in a Docker image in order to allow a wide choice in language and frameworks (such as Java and Maven, Node and WebDriver.io, or any other framework and technology built upon Selenium). The Docker image can be created with standard tooling, but it must respect certain conventions during its execution. Quando si esegue l&#39;immagine Docker, viene eseguito automaticamente il provisioning di un server Selenium. Le convenzioni di runtime descritte di seguito consentono al codice di test di accedere sia al server Selenium che alle istanze AEM in fase di test.

>[!NOTE]
> Per utilizzare i test dell’interfaccia utente descritti in questa pagina, è necessario aggiornare le pipeline di stage e produzione create prima del 10 febbraio 2021.
> Vedi [Pipeline CI-CD in Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) per informazioni sulla configurazione della pipeline.

## Test personalizzati dell&#39;interfaccia utente {#custom-ui-testing}

AEM fornisce ai suoi clienti una suite integrata di gate di qualità di Cloud Manager per garantire un aggiornamento fluido delle loro applicazioni. In particolare, i gate di test IT consentono già ai clienti di creare e automatizzare i propri test che utilizzano API AEM.

La funzione di test dell’interfaccia utente personalizzata è una [funzionalità opzionale](#customer-opt-in) che consente ai nostri clienti di creare ed eseguire automaticamente i test dell’interfaccia utente per le loro applicazioni. I test dell’interfaccia utente sono test basati su Selenium inseriti in un’immagine Docker per consentire un’ampia scelta in linguaggio e framework (come Java e Maven, Node e WebDriver.io o qualsiasi altro framework e tecnologia basati su Selenium). Per ulteriori informazioni su come creare l’interfaccia utente e scrivere i test dell’interfaccia utente, consulta questo articolo. Inoltre, un progetto di test dell’interfaccia utente può essere facilmente generato utilizzando il AEM Project Archetype.

I clienti possono creare (tramite GIT) test personalizzati e suite di test per l’interfaccia utente. Il test dell’interfaccia utente viene eseguito come parte di un gate di qualità specifico per ogni pipeline di Cloud Manager con il relativo passaggio specifico e le relative informazioni sul feedback. Eventuali test dell’interfaccia utente, tra cui regressione e nuove funzionalità, consentiranno di rilevare gli errori e di segnalarli nel contesto del cliente.

I test dell’interfaccia utente del cliente vengono eseguiti automaticamente sulla pipeline di produzione nel passaggio &quot;Test personalizzati dell’interfaccia utente&quot;.

A differenza dei test funzionali personalizzati che sono test HTTP scritti in java, i test dell’interfaccia utente possono essere un’immagine docker con test scritti in qualsiasi lingua, purché rispettino le convenzioni definite in [Creazione di test dell’interfaccia utente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/ui-testing.html?lang=en#building-ui-tests).

>[!NOTE]
>Si consiglia di seguire la struttura e la lingua *(js e audio)* opportunamente fornito nel [Archetipo di progetto AEM](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/ui.tests) come punto di partenza.

### Opt-in del cliente {#customer-opt-in}

Per poter generare ed eseguire i test dell’interfaccia utente, i clienti devono &quot;effettuare l’opt-in&quot; aggiungendo un file al proprio archivio di codice, sotto il sottomodulo maven per i test dell’interfaccia (accanto al file pom.xml del sottomodulo dei test dell’interfaccia utente) e assicurarsi che questo file sia nella directory principale del predefinito `tar.gz` file.

*Nome file*: `testing.properties`

*Contenuto*: `ui-tests.version=1`

Se questo non è presente nella build `tar.gz` file, la build e le esecuzioni dei test dell’interfaccia utente verranno ignorate

Per aggiungere `testing.properties` aggiungi un `include` istruzione in `assembly-ui-test-docker-context.xml` file (nel sottomodulo di test dell’interfaccia utente). Se il progetto non include la riga, dovrai modificare questo file per abilitare il consenso al test dell’interfaccia utente. Se il file può avere una riga che consiglia di non modificare, si prega di ignorare quel consiglio.

    &quot;
    [..]
    &lt;includes>
    &lt;include>Dockerfile&lt;/include>
    &lt;include>wait-for-grid.sh&lt;/include>
    &lt;include>testing.properties&lt;/include> &lt;!>- modulo di test opt-in in Cloud Manager —>
    &lt;/includes>
    [..]
    &quot;

>[!NOTE]
>Le pipeline di produzione create prima del 10 febbraio 2021 dovranno essere aggiornate per poter utilizzare i test dell’interfaccia utente come descritto in questa sezione. In sostanza, l’utente deve modificare la pipeline di produzione e fare clic su **Salva** dall’interfaccia utente anche se non sono state apportate modifiche.
>Fai riferimento a [Configurazione della pipeline CI-CD](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager) per ulteriori informazioni sulla configurazione della pipeline.

## Creazione di test dell’interfaccia utente {#building-ui-tests}

I test dell’interfaccia utente si basano su un contesto di build Docker generato da un progetto Maven. Cloud Manager utilizza il contesto di creazione Docker per generare un’immagine Docker che contiene i test effettivi dell’interfaccia utente. In sintesi, un progetto Maven genera un contesto di creazione Docker e il contesto di creazione Docker descrive come creare un’immagine Docker contenente i test dell’interfaccia utente.

Questa sezione descrive i passaggi necessari per aggiungere un progetto di test dell’interfaccia utente all’archivio. Se hai fretta o non hai requisiti speciali per il linguaggio di programmazione, la [Archetipo di progetto AEM](https://github.com/adobe/aem-project-archetype) può generare un progetto di test dell’interfaccia utente .

### Generare un contesto di creazione Docker {#generate-docker-build-context}

Per generare un contesto di creazione Docker, è necessario un modulo Maven che:

- Produce un archivio contenente un `Dockerfile` e tutti gli altri file necessari per creare l&#39;immagine Docker con i test.
- Assegna tag all’archivio con la `ui-test-docker-context` classificatore.

Il modo più semplice per ottenere questo risultato è quello di configurare il [Plug-in assembly Maven](http://maven.apache.org/plugins/maven-assembly-plugin/) per creare l&#39;archivio contestuale della build Docker e assegnargli il classificatore corretto.

Puoi creare test dell’interfaccia utente con diverse tecnologie e framework, ma questa sezione presuppone che il progetto sia disposto in modo simile al seguente.

```
├── Dockerfile
├── assembly-ui-test-docker-context.xml
├── pom.xml
├── test-module
│   ├── package.json
│   ├── index.js
│   └── wdio.conf.js
└── wait-for-grid.sh
```

La `pom.xml` il file si occupa della build Maven. Aggiungi un’esecuzione al plugin Maven Assembly in modo simile al seguente.

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

Questa esecuzione indica al plugin Maven Assembly di creare un archivio in base alle istruzioni contenute in `assembly-ui-test-docker-context.xml`, chiamato un &quot;descrittore di assembly&quot; nel gergo del plugin. Il descrittore dell&#39;assembly elenca tutti i file che devono far parte dell&#39;archivio.

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

Il descrittore dell&#39;assieme indica al plug-in di creare un archivio di tipo `.tar.gz` e assegna le `ui-test-docker-context` classificatore. Inoltre, elenca i file che devono essere inclusi nell&#39;archivio:

- A `Dockerfile`, obbligatorio per la creazione dell’immagine Docker.
- La `wait-for-grid.sh` script, le cui finalità sono descritte di seguito.
- I test effettivi dell’interfaccia utente, implementati da un progetto Node.js in `test-module` cartella.

Il descrittore di assembly esclude inoltre alcuni file che potrebbero essere generati durante l&#39;esecuzione localmente dei test dell&#39;interfaccia utente. Questo garantisce un archivio più piccolo e build più veloci.

L’archivio contenente il contesto della build Docker viene automaticamente raccolto da Cloud Manager, che creerà l’immagine Docker contenente i test durante le pipeline di distribuzione. Alla fine, Cloud Manager eseguirà l’immagine Docker per eseguire i test dell’interfaccia utente rispetto all’applicazione.

La build deve produrre zero o un archivio. Se genera un archivio a zero, il passaggio di test viene superato per impostazione predefinita. Se la build produce più di un archivio, l&#39;archivio selezionato non è deterministico.

## Creazione di test dell’interfaccia utente {#writing-ui-tests}

Questa sezione descrive le convenzioni che l’immagine Docker contenente i test dell’interfaccia utente deve seguire. L’immagine Docker è creata in base al contesto della build Docker descritto nella sezione precedente.

### Variabili di ambiente {#environment-variables}

Le seguenti variabili di ambiente verranno passate all’immagine Docker in fase di esecuzione.

| Variabile | Esempi | Descrizione |
|---|---|---|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | URL del server Selenium |
| `SELENIUM_BROWSER` | `chrome`, `firefox` | The browser implementation used by the Selenium Server |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | URL dell’istanza di authoring AEM |
| `AEM_AUTHOR_USERNAME` | `admin` | Nome utente per accedere all’istanza di authoring AEM |
| `AEM_AUTHOR_PASSWORD` | `admin` | Password per accedere all&#39;istanza di authoring AEM |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | URL dell’istanza di pubblicazione AEM |
| `AEM_PUBLISH_USERNAME` | `admin` | Nome utente per accedere all&#39;istanza di pubblicazione AEM |
| `AEM_PUBLISH_PASSWORD` | `admin` | Password per accedere all&#39;istanza di pubblicazione AEM |
| `REPORTS_PATH` | `/usr/src/app/reports` | Percorso in cui salvare il report XML dei risultati del test |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | URL a cui deve essere caricato il file per renderlo accessibile a Selenium |

### In attesa che il selenio sia pronto {#waiting-for-selenium}

Prima dell&#39;avvio dei test, è responsabilità dell&#39;immagine Docker assicurarsi che il server Selenium sia in esecuzione. L&#39;attesa del servizio Selenium è un processo in due fasi:

1. Leggi l’URL del servizio Selenium dal `SELENIUM_BASE_URL` variabile di ambiente.
2. Sondaggio a intervalli regolari [endpoint di stato](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready) esposti dall’API Selenium.

Una volta che l&#39;endpoint di stato di Selenium risponde con una risposta positiva, i test possono finalmente iniziare.

### Generare i report di test {#generate-test-reports}

L’immagine Docker deve generare rapporti di test in formato JUnit XML e salvarli nel percorso specificato dalla variabile di ambiente `REPORTS_PATH`. Il formato JUnit XML è un formato diffuso per la generazione di rapporti sui risultati dei test. Se l’immagine Docker utilizza Java e Maven, entrambe le [Plug-in del surefire Maven](https://maven.apache.org/surefire/maven-surefire-plugin/) e [Plug-in Maven FailureSafe](https://maven.apache.org/surefire/maven-failsafe-plugin/). Se l&#39;immagine Docker è implementata con altri linguaggi di programmazione o runners di test, controlla la documentazione relativa agli strumenti selezionati per sapere come generare report JUnit XML.

### Caricare file {#upload-files}

A volte i test devono caricare i file nell&#39;applicazione sotto test. Al fine di mantenere flessibile la distribuzione di Selenium rispetto ai test, non è possibile caricare direttamente una risorsa direttamente in Selenium. Il caricamento di un file passa attraverso alcuni passaggi intermedi:

1. Carica il file all’URL specificato dal `UPLOAD_URL` variabile di ambiente. Il caricamento deve essere eseguito in una richiesta POST con un modulo multiparte. Il modulo multiparte deve avere un singolo campo di file. Equivale a `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`. Per informazioni su come eseguire una richiesta HTTP, consulta la documentazione e le librerie del linguaggio di programmazione utilizzato nell’immagine Docker .
2. Se il caricamento ha esito positivo, la richiesta restituisce un `200 OK` risposta del tipo `text/plain`. Il contenuto della risposta è un handle di file opaco. Puoi utilizzare questo handle al posto del percorso di un file in un `<input>` per testare il caricamento di file nell&#39;applicazione.
