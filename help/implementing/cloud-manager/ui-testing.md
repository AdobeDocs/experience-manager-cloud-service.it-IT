---
title: Test interfaccia utente - Cloud Services
description: Test interfaccia utente - Cloud Services
translation-type: tm+mt
source-git-commit: bf3fb5178bc2ae72e19ecc1de82b08fac5089ecf
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---


# Test interfaccia utente {#ui-testing}

>[!CAUTION]
>
>Questa funzione non è ancora disponibile.


I test dell&#39;interfaccia utente sono test basati su selenio inclusi in un&#39;immagine Docker per consentire un&#39;ampia scelta in linguaggio e framework (come Java e Maven, Node e WebDriver.io o qualsiasi altro framework e tecnologia basati su Selenium). L&#39;immagine Docker può essere creata con strumenti standard, ma deve rispettare alcune convenzioni durante la sua esecuzione. Quando si esegue l&#39;immagine Docker, viene automaticamente eseguito il provisioning di un server Selenium. Le convenzioni di runtime descritte di seguito consentono al codice di test di accedere sia al server di Selenium che alle istanze di AEM in fase di test.

## Creazione di test dell&#39;interfaccia utente {#building-ui-tests}

I test dell&#39;interfaccia utente sono generati da un contesto di creazione Docker generato da un progetto Maven. Cloud Manager utilizza il contesto di creazione Docker per generare un&#39;immagine Docker che contiene i test effettivi dell&#39;interfaccia utente. In sintesi, un progetto Maven genera un contesto di creazione Docker e il contesto di creazione Docker descrive come creare un&#39;immagine Docker contenente i test dell&#39;interfaccia utente.

Questa sezione descrive i passaggi necessari per aggiungere un progetto di test dell’interfaccia utente all’archivio. Se hai fretta o non hai requisiti speciali per il linguaggio di programmazione, il [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) può generare un progetto di test dell&#39;interfaccia utente.

### Generare un contesto di build Docker {#generate-docker-build-context}

Per generare un contesto di creazione Docker, è necessario un modulo Maven che:

- Genera un archivio contenente un `Dockerfile` e tutti gli altri file necessari per creare l&#39;immagine Docker con i test.
- Assegna tag all&#39;archivio con il classificatore `ui-test-docker-context`.

Il modo più semplice per ottenere questo è configurare il [Maven Assembly Plugin](http://maven.apache.org/plugins/maven-assembly-plugin/) per creare l&#39;archivio contestuale della build Docker e assegnarvi il classificatore giusto.

È possibile creare test dell&#39;interfaccia utente con tecnologie e framework diversi, ma questa sezione presuppone che il progetto sia disposto in modo simile a quello descritto di seguito.

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

Il file `pom.xml` si occupa della build Maven. Aggiungere un&#39;esecuzione al plug-in dell&#39;assieme Maven simile a quanto segue.

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

Questa esecuzione indica al plug-in di assemblaggio Maven di creare un archivio basato sulle istruzioni contenute in `assembly-ui-test-docker-context.xml`, denominato &quot;descrittore di assembly&quot; nel gergo del plugin. Il descrittore dell&#39;assembly elenca tutti i file che devono far parte dell&#39;archivio.

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

Il descrittore dell&#39;assembly indica al plug-in di creare un archivio di tipo `.tar.gz` e gli assegna il `ui-test-docker-context` classificatore. Inoltre, elenca i file che devono essere inclusi nell&#39;archivio:

- A `Dockerfile`, obbligatorio per la creazione dell&#39;immagine Docker.
- Lo script `wait-for-grid.sh`, le cui finalità sono descritte di seguito.
- I test dell&#39;interfaccia utente effettivi, implementati da un progetto Node.js nella cartella `test-module`.

Il descrittore dell&#39;assembly esclude inoltre alcuni file che potrebbero essere generati durante l&#39;esecuzione localmente dei test dell&#39;interfaccia utente. Questo garantisce un archivio più piccolo e build più veloci.

L&#39;archivio contenente il contesto di creazione Docker viene prelevato automaticamente da Cloud Manager, che genererà l&#39;immagine Docker contenente i test durante le pipeline di distribuzione. Alla fine, Cloud Manager eseguirà l&#39;immagine Docker per eseguire i test dell&#39;interfaccia utente sull&#39;applicazione.

## Test dell&#39;interfaccia utente di scrittura {#writing-ui-tests}

Questa sezione descrive le convenzioni che l&#39;immagine Docker contenente i test dell&#39;interfaccia utente deve seguire. L&#39;immagine Docker è ricavata dal contesto di creazione Docker descritto nella sezione precedente.

### Variabili di ambiente {#environment-variables}

Le seguenti variabili di ambiente verranno trasmesse all&#39;immagine Docker in fase di esecuzione.

| Variabile | Esempi | Descrizione |
|---|---|---|
| `SELENIUM_BASE_URL` | `http://my-ip:4444` | URL del server selenio |
| `SELENIUM_BROWSER` | `chrome`, `firefox` | Implementazione del browser utilizzata dal server selenio |
| `AEM_AUTHOR_URL` | `http://my-ip:4502/context-path` | URL dell’istanza di creazione AEM |
| `AEM_AUTHOR_USERNAME` | `admin` | Nome utente per accedere all’istanza di creazione AEM |
| `AEM_AUTHOR_PASSWORD` | `admin` | La password per accedere all&#39;istanza di creazione AEM |
| `AEM_PUBLISH_URL` | `http://my-ip:4503/context-path` | URL dell’istanza di pubblicazione AEM |
| `AEM_PUBLISH_USERNAME` | `admin` | Il nome utente per accedere all’istanza di pubblicazione AEM |
| `AEM_PUBLISH_PASSWORD` | `admin` | La password per accedere all’istanza di pubblicazione AEM |
| `REPORTS_PATH` | `/usr/src/app/reports` | Percorso in cui salvare il rapporto XML dei risultati del test |
| `UPLOAD_URL` | `http://upload-host:9090/upload` | URL in cui deve essere caricato il file per renderlo accessibile a Selenium |

### In attesa che il selenio sia pronto {#waiting-for-selenium}

Prima dell&#39;inizio dei test, è responsabilità dell&#39;immagine Docker assicurarsi che il server Selenium sia attivo e funzionante. L&#39;attesa del servizio Selenium è un processo in due fasi:

1. Leggere l&#39;URL del servizio Selenium dalla variabile di ambiente `SELENIUM_BASE_URL`.
2. Sondaggio a intervalli regolari sull&#39;endpoint [stato](https://github.com/SeleniumHQ/docker-selenium/#waiting-for-the-grid-to-be-ready) esposto dall&#39;API Selenium.

Una volta che l&#39;endpoint di stato del selenio risponde con una risposta positiva, i test possono finalmente avviarsi.

### Generare i report di test {#generate-test-reports}

L&#39;immagine Docker deve generare rapporti di prova in formato JUnit XML e salvarli nel percorso specificato dalla variabile di ambiente `REPORTS_PATH`. Il formato JUnit XML è un formato diffuso per la generazione di rapporti sui risultati dei test. Se l&#39;immagine Docker utilizza Java e Maven, sia il [Maven Surefire Plugin](https://maven.apache.org/surefire/maven-surefire-plugin/) che il [Maven FailedSafe Plugin](https://maven.apache.org/surefire/maven-failsafe-plugin/). Se l&#39;immagine Docker è implementata con altri linguaggi di programmazione o con altri corridori di test, controlla la documentazione relativa agli strumenti selezionati per sapere come generare i rapporti JUnit XML.

### Caricare i file (#upload-files)

Talvolta, i test devono caricare i file nell’applicazione in fase di test. Per mantenere la flessibilità nella distribuzione del selenio rispetto ai test, non è possibile caricare direttamente una risorsa direttamente in selenio. Al contrario, il caricamento di un file passa attraverso alcuni passaggi intermedi:

1. Caricate il file nell&#39;URL specificato dalla variabile di ambiente `UPLOAD_URL`. Il caricamento deve essere eseguito in una richiesta POST con un modulo multiparte. Il modulo multiparte deve avere un singolo campo di file. Equivale a `curl -X POST ${UPLOAD_URL} -F "data=@file.txt"`. Consulta la documentazione e le librerie del linguaggio di programmazione utilizzato nell&#39;immagine Docker per sapere come eseguire tale richiesta HTTP.
2. Se il caricamento ha esito positivo, la richiesta restituisce una risposta `200 OK` di tipo `text/plain`. Il contenuto della risposta è un handle di file opaco. Potete usare questa maniglia al posto del percorso di un file in un elemento `<input>` per testare i caricamenti di file nell&#39;applicazione.
