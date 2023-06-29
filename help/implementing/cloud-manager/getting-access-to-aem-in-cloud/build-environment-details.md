---
title: Ambiente di build
description: Scopri l’ambiente di build di Cloud Manager e come genera e verifica il codice.
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '991'
ht-degree: 94%

---


# Ambiente di build {#build-environment}

Scopri l’ambiente di build di Cloud Manager e come genera e verifica il codice.

## Dettagli sull’ambiente di build {#build-environment-details}

Cloud Manager genera e verifica il codice mediante un ambiente di build specializzato.

* L’ambiente di build è basato su Linux, derivato da Ubuntu 18.04.
* Apache Maven 3.6.0 è installato.
* Le versioni Java installate sono Oracle JDK 8u202 e Oracle JDK 11.0.2.
* Per impostazione predefinita, la variabile di ambiente `JAVA_HOME` è impostata su `/usr/lib/jvm/jdk1.8.0_202`, che contiene Oracle JDK 8u202. Per ulteriori informazioni, consulta la sezione [Versione JDK alternativa per l’esecuzione Maven](#alternate-maven-jdk-version).
* È necessario installare anche alcuni pacchetti di sistema aggiuntivi.

   * `bzip2`
   * `unzip`
   * `libpng`
   * `imagemagick`
   * `graphicsmagick`

* Altri pacchetti possono essere installati al momento della generazione, come descritto nella sezione [Installazione di pacchetti di sistema aggiuntivi.](#installing-additional-system-packages)
* Ogni generazione viene svolta in un ambiente incontaminato; il contenitore della build non conserva nessuno stato tra le esecuzioni.
* Maven viene sempre eseguito con i tre comandi riportati di seguito.

* `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
* `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
* `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`
* Maven è configurato a livello di sistema con un file `settings.xml`, che include automaticamente l’archivio di artefatti pubblico di Adobe utilizzando un profilo denominato `adobe-public`. Per ulteriori informazioni, consulta [Archivio Maven pubblico di Adobe](https://repo1.maven.org/).

>[!NOTE]
>
>Sebbene Cloud Manager non definisca una versione specifica del `jacoco-maven-plugin`, la versione utilizzata deve essere `0.7.5.201505241946` o superiore.

### Utilizzo di una versione Java specifica {#using-java-support}

Per impostazione predefinita, i progetti sono generati dal processo di build di Cloud Manager utilizzando il JDK di Oracle 8. Chi desidera utilizzare un JDK alternativo ha due opzioni.

* [Usare le toolchain Maven.](#maven-toolchains)
* [Selezionare una versione JDK alternativa per l’intero processo di esecuzione Maven.](#alternate-maven-jdk-version)

#### Toolchain Maven {#maven-toolchains}

Il [plug-in Maven Toolchain](https://maven.apache.org/plugins/maven-toolchains-plugin/) consente di selezionare un JDK (o toolchain) specifico per i progetti da utilizzare nel contesto dei plug-in Maven compatibili con le toolchain. L’operazione viene eseguita nel file `pom.xml` del progetto specificando un fornitore e un valore per la versione.

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-toolchains-plugin</artifactId>
    <version>1.1</version>
    <executions>
        <execution>
            <goals>
                <goal>toolchain</goal>
            </goals>
        </execution>
    </executions>
    <configuration>
        <toolchains>
            <jdk>
                <version>11</version>
                <vendor>oracle</vendor>
            </jdk>
        </toolchains>
    </configuration>
</plugin>
```

Questo farà sì che tutti i plug-in Maven compatibili con le toolchain utilizzino Oracle JDK versione 11.

Quando si utilizza questo metodo, Maven continua a essere eseguito con il JDK predefinito (Oracle 8) e la variabile di ambiente `JAVA_HOME` non viene modificata. Pertanto, il controllo o l’applicazione della versione Java tramite plug-in come Apache Maven Enforcer non funziona. Non utilizzare questi plug-in.

Le combinazioni fornitore/versione attualmente disponibili sono:

| Fornitore | Versione |
|---|---|
| `oracle` | `8` |
| `oracle` | `11` |
| `sun` | `8` |
| `sun` | `11` |

Questa tabella si riferisce ai numeri di versione del prodotto. I numeri di build Java o i percorsi di installazione possono riflettere le precedenti convenzioni di versione Java, come 1.8 per Java 8.

>[!NOTE]
>
>A partire da aprile 2022, Oracle JDK diventa il JDK predefinito per lo sviluppo e il funzionamento delle applicazioni AEM. Il processo di build di Cloud Manager passa automaticamente all’utilizzo di JDK di Oracle, anche se nella toolchain Maven è selezionata esplicitamente un’opzione alternativa. Consulta le note sulla versione di aprile 2022.

#### Versione JDK alternativa per l’esecuzione Maven {#alternate-maven-jdk-version}

È inoltre possibile selezionare Java 8 o Java 11 come JDK per l’intera esecuzione Maven. A differenza delle opzioni toolchain, questa opzione modifica il JDK utilizzato per tutti i plug-in, a meno che non venga impostata anche la configurazione delle toolchain. In questo caso, la configurazione delle toolchain viene ancora applicata per i plug-in Maven compatibili con le toolchain. Di conseguenza, controllare e applicare la versione Java con il [plug-in Apache Maven Enforcer](https://maven.apache.org/enforcer/maven-enforcer-plugin/) funzionerà.

Per eseguire l’operazione, crea un file denominato `.cloudmanager/java-version` nel ramo dell’archivio Git utilizzato dalla pipeline. Questo file può avere contenuti della versione 11 o 8. Qualsiasi altro valore viene ignorato. Se si specifica 11, viene utilizzato Oracle 11 e la variabile di ambiente `JAVA_HOME` viene impostata su `/usr/lib/jvm/jdk-11.0.2`. Se si specifica 8, viene utilizzato Oracle 8 e la variabile di ambiente `JAVA_HOME` viene impostata su `/usr/lib/jvm/jdk1.8.0_202`.

## Variabili di ambiente {#environment-variables}

### Variabili di ambiente standard {#standard-environ-variables}

Potrebbe essere necessario variare il processo di build in base alle informazioni sul programma o sulla pipeline.

Ad esempio, se in fase di generazione la minimizzazione JavaScript viene eseguita tramite uno strumento come Gulp, potrebbe risultare utile utilizzare livelli di minimizzazione diversi per la build di un ambiente di sviluppo e per la build di un ambiente di staging e produzione.

Per supportare la funzione, Cloud Manager aggiunge le variabili di ambiente standard al contenitore della build per ogni esecuzione.

| Nome della variabile | Definizione |
|---|---|
| `CM_BUILD` | Sempre impostato su `true` |
| `BRANCH` | Ramo configurato per l’esecuzione |
| `CM_PIPELINE_ID` | Identificatore numerico della pipeline |
| `CM_PIPELINE_NAME` | Nome della pipeline |
| `CM_PROGRAM_ID` | Identificatore numerico del programma |
| `CM_PROGRAM_NAME` | Nome del programma |
| `ARTIFACTS_VERSION` | Per una pipeline di staging o di produzione, la versione sintetica generata da Cloud Manager |
| `CM_AEM_PRODUCT_VERSION` | Versione |

### Variabili delle pipeline {#pipeline-variables}

Il processo di build può dipendere da specifiche variabili di configurazione che sarebbe inopportuno inserire nell’archivio Git o che potrebbero dover essere modificate tra le esecuzioni della pipeline che utilizzano lo stesso ramo.

Cloud Manager consente di configurare queste variabili tramite l’API o l’interfaccia della riga di comando di Cloud Manager, in base alla pipeline. Le variabili possono essere archiviate come testo normale o crittografate quando inattive. In entrambi i casi, le variabili sono rese disponibili all’interno dell’ambiente di build come una variabile di ambiente a cui è possibile fare riferimento dal file `pom.xml` o da altri script della build.

Comando CLI per impostare una variabile.

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test
```

Comando per elencare le variabili.

```shell
$ aio cloudmanager:list-pipeline-variables PIPELINEID
```

I nomi delle variabili devono rispettare le seguenti convenzioni.

* Le variabili possono contenere solo caratteri alfanumerici e il carattere di sottolineatura (`_`).
* I nomi devono essere scritti in lettere maiuscole.
* È previsto un limite di 200 variabili per pipeline.
* Ogni nome deve avere una lunghezza inferiore a 100 caratteri.
* Ogni valore della variabile `string` deve avere una lunghezza inferiore a 2048 caratteri.
* Ogni valore della variabile di tipo `secretString` deve avere una lunghezza inferiore a 500 caratteri.

Per l’utilizzo in un file `pom.xml` Maven, in genere è utile associare queste variabili alle proprietà Maven scrivendo una sintassi simile a quella proposta di seguito.

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                <property>
                    <name>env.CM_BUILD</name>
                </property>
            </activation>
            <properties>
                <my.custom.property>${env.MY_CUSTOM_VARIABLE}</my.custom.property> 
            </properties>
        </profile>
```

## Installazione di pacchetti di sistema aggiuntivi {#installing-additional-system-packages}

Alcune build richiedono l’installazione di pacchetti di sistema aggiuntivi per l’operatività completa. Ad esempio, una build può richiamare uno script Python o Ruby e richiedere l’installazione dell’interprete di linguaggio appropriato. È possibile eseguire l’operazione chiamando [`exec-maven-plugin`](https://www.mojohaus.org/exec-maven-plugin/) in `pom.xml` per richiamare APT. Questa esecuzione deve generalmente essere integrata in un profilo Maven specifico per Cloud Manager. In questo esempio viene installato Python.

```xml
        <profile>
            <id>install-python</id>
            <activation>
                <property>
                        <name>env.CM_BUILD</name>
                </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <groupId>org.codehaus.mojo</groupId>
                        <artifactId>exec-maven-plugin</artifactId>
                        <version>1.6.0</version>
                        <executions>
                            <execution>
                                <id>apt-get-update</id>
                                <phase>validate</phase>
                                <goals>
                                    <goal>exec</goal>
                                </goals>
                                <configuration>
                                    <executable>apt-get</executable>
                                    <arguments>
                                        <argument>update</argument>
                                    </arguments>
                                </configuration>
                            </execution>
                            <execution>
                                <id>install-python</id>
                                <phase>validate</phase>
                                <goals>
                                    <goal>exec</goal>
                                </goals>
                                <configuration>
                                    <executable>apt-get</executable>
                                    <arguments>
                                        <argument>install</argument>
                                        <argument>-y</argument>
                                        <argument>--no-install-recommends</argument>
                                        <argument>python</argument>
                                    </arguments>
                                </configuration>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

Questa stessa tecnica può essere utilizzata per installare pacchetti per uno specifico linguaggio, ad esempio utilizzando `gem` per RubyGems o `pip` per i pacchetti Python.

>[!NOTE]
>
>Installando un pacchetto di sistema in questo modo, non lo si installa nell’ambiente di runtime utilizzato per l’esecuzione di Adobe Experience Manager. Se hai bisogno di installare un pacchetto di sistema nell’ambiente AEM, contatta il rappresentante Adobe.

>[!TIP]
>
>Per informazioni dettagliate sull’ambiente di build front-end, consulta [Sviluppo di siti con la pipeline front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md).
