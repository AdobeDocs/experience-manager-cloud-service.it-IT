---
title: Ambiente build
description: Scopri l’ambiente di build di Cloud Manager e come crea e verifica il codice.
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
source-git-commit: c138f0be15550df85a2ec23b6b551ccba07996c8
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 1%

---

# Ambiente build {#build-environment}

Scopri l’ambiente di build di Cloud Manager e come crea e verifica il codice.

## Dettagli dell’ambiente di generazione {#build-environment-details}

Cloud Manager crea ed esegue il test del codice utilizzando un ambiente di build specializzato.

* L&#39;ambiente di creazione è basato su Linux, derivato da Ubuntu 18.04.
* Apache Maven 3.6.0 è installato.
* Le versioni Java installate sono Oracle JDK 8u202 e Oracle JDK 11.0.2.
* Per impostazione predefinita, la `JAVA_HOME` variabile di ambiente impostata su `/usr/lib/jvm/jdk1.8.0_202`  che contiene l&#39;Oracle JDK 8u202. Vedi [Versione JDK di esecuzione Maven alternativa](#alternate-maven-jdk-version) per ulteriori dettagli.
* Ci sono alcuni pacchetti di sistema aggiuntivi installati che sono necessari.

   * `bzip2`
   * `unzip`
   * `libpng`
   * `imagemagick`
   * `graphicsmagick`

* Altri pacchetti possono essere installati in fase di creazione come descritto nella sezione [Installazione di pacchetti di sistema aggiuntivi.](#installing-additional-system-packages)
* Ogni costruzione è fatta su un ambiente incontaminato; il contenitore build non mantiene nessuno stato tra le esecuzioni.
* Maven viene sempre eseguito con i tre comandi seguenti.

* `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
* `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
* `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`
* Maven è configurato a livello di sistema con un `settings.xml` file , che include automaticamente l’archivio degli artefatti dell’Adobe pubblico utilizzando un profilo denominato `adobe-public`. (Vedi [Archivio Maven pubblico di Adobe](https://repo1.maven.org/) per ulteriori dettagli).

>[!NOTE]
>
>Anche se Cloud Manager non definisce una versione specifica del `jacoco-maven-plugin`, la versione utilizzata deve essere almeno `0.7.5.201505241946`.

### Utilizzo di una versione Java specifica {#using-java-support}

Per impostazione predefinita, i progetti sono generati dal processo di creazione di Cloud Manager utilizzando il JDK di Oracle 8. I clienti che desiderano utilizzare un JDK alternativo hanno due opzioni.

* [Usa le catene degli strumenti Maven.](#maven-toolchains)
* [Seleziona una versione JDK alternativa per l’intero processo di esecuzione Maven.](#alternate-maven-jdk-version)

#### Catene di strumenti Maven {#maven-toolchains}

La [Plug-in catene di strumenti Maven](https://maven.apache.org/plugins/maven-toolchains-plugin/) consente ai progetti di selezionare un JDK specifico (o toolchain) da utilizzare nel contesto dei plug-in Maven consapevoli delle catene di strumenti. Questo viene fatto nel `pom.xml` specificando un valore di fornitore e di versione.

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

Questo farà sì che tutti i plug-in Maven consapevoli delle catene di strumenti utilizzino l’Oracle JDK, versione 11.

Quando si utilizza questo metodo, Maven stesso viene comunque eseguito utilizzando il JDK predefinito (Oracle 8) e il `JAVA_HOME`  la variabile di ambiente non viene modificata. Pertanto, il controllo o l’applicazione della versione Java tramite plug-in come Apache Maven Enforcer Plugin non funziona e tali plug-in non devono essere utilizzati.

Le combinazioni fornitore/versione attualmente disponibili sono:

| Produttore | Versione |
|---|---|
| `oracle` | `1.8` |
| `oracle` | `1.11` |
| `oracle` | `11` |
| `sun` | `1.8` |
| `sun` | `1.11` |
| `sun` | `11` |

>[!NOTE]
>
>A partire da aprile 2022, Oracle JDK sarà il JDK predefinito per lo sviluppo e il funzionamento delle applicazioni AEM. Il processo di creazione di Cloud Manager passa automaticamente a utilizzando Oracle JDK, anche se nella toolchain Maven è selezionata esplicitamente un’opzione alternativa. Per ulteriori informazioni, consulta le note sulla versione di aprile pubblicate .

#### Versione JDK di esecuzione Maven alternativa {#alternate-maven-jdk-version}

È anche possibile selezionare Java 8 o Java 11 come JDK per l&#39;intera esecuzione Maven. A differenza delle opzioni delle catene degli strumenti, questo cambia il JDK utilizzato per tutti i plugin a meno che la configurazione delle catene degli utensili non sia impostata anche nel qual caso la configurazione delle catene degli utensili viene ancora applicata per i plugin Maven consapevoli delle catene degli utensili. Di conseguenza, verifica e applica la versione Java utilizzando il [Plug-in applicazione Apache Maven](https://maven.apache.org/enforcer/maven-enforcer-plugin/) funzionerà.

A questo scopo, crea un file denominato `.cloudmanager/java-version` nel ramo dell’archivio git utilizzato dalla pipeline. Questo file può avere il contenuto 11 o 8. Qualsiasi altro valore viene ignorato. Se è specificato 11, si utilizza l&#39;Oracle 11 e la `JAVA_HOME` variabile di ambiente impostata su `/usr/lib/jvm/jdk-11.0.2`. Se si specifica 8, si utilizza l&#39;Oracle 8 e la `JAVA_HOME` variabile di ambiente impostata su `/usr/lib/jvm/jdk1.8.0_202`.

## Variabili di ambiente {#environment-variables}

### Variabili di ambiente standard {#standard-environ-variables}

Potrebbe essere necessario variare il processo di creazione in base alle informazioni sul programma o sulla pipeline.

Ad esempio, se la minimizzazione JavaScript in fase di creazione viene eseguita tramite uno strumento come il gulp, potrebbe essere utile utilizzare un livello di minimizzazione diverso durante la creazione di un ambiente di sviluppo rispetto alla creazione di uno staging e produzione.

Per supportare questa funzione, Cloud Manager aggiunge queste variabili di ambiente standard al contenitore di build per ogni esecuzione.

| Nome della variabile | Definizione |
|---|---|
| `CM_BUILD` | Sempre impostato su `true` |
| `BRANCH` | Il ramo configurato per l’esecuzione |
| `CM_PIPELINE_ID` | Identificatore numerico della pipeline |
| `CM_PIPELINE_NAME` | Nome della pipeline |
| `CM_PROGRAM_ID` | Identificatore numerico del programma |
| `CM_PROGRAM_NAME` | Nome del programma |
| `ARTIFACTS_VERSION` | Per una fase o una pipeline di produzione, la versione sintetica generata da Cloud Manager |
| `CM_AEM_PRODUCT_VERSION` | Versione della versione |

### Variabili di pipeline {#pipeline-variables}

Il processo di creazione può dipendere da specifiche variabili di configurazione che non sarebbe opportuno inserire nell’archivio Git oppure potrebbe essere necessario modificarle tra le esecuzioni della pipeline che utilizzano lo stesso ramo.

Cloud Manager consente di configurare queste variabili tramite l’API di Cloud Manager o l’CLI di Cloud Manager in base alla pipeline. Le variabili possono essere memorizzate come testo normale o cifrate a riposo. In entrambi i casi, le variabili sono rese disponibili all&#39;interno dell&#39;ambiente di creazione come variabile di ambiente a cui è possibile fare riferimento dall&#39;interno del `pom.xml` file o altri script di build.

Questo comando CLI imposta una variabile.

```shell
$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test
```

Questo comando elenca le variabili.

```shell
$ aio cloudmanager:list-pipeline-variables PIPELINEID
```

I nomi delle variabili devono rispettare le convenzioni seguenti.

* Le variabili possono contenere solo caratteri alfanumerici e il carattere di sottolineatura (`_`).
* I nomi devono essere maiuscoli.
* Esiste un limite di 200 variabili per pipeline.
* Ogni nome deve contenere meno di 100 caratteri.
* Ogni `string` Il valore della variabile deve essere minore di 2048 caratteri.
* Ogni `secretString` Il valore della variabile di tipo deve essere inferiore a 500 caratteri.

Quando viene utilizzato all&#39;interno di un Maven `pom.xml` tipicamente è utile mappare queste variabili alle proprietà Maven utilizzando una sintassi simile a questa.

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

Alcune build richiedono l&#39;installazione di pacchetti di sistema aggiuntivi per funzionare completamente. Ad esempio, una build può richiamare uno script Python o Ruby e dovrà disporre di un interprete di lingua appropriato installato. Questa operazione può essere eseguita chiamando il [`exec-maven-plugin`](https://www.mojohaus.org/exec-maven-plugin/) nel tuo `pom.xml` per richiamare APT. Questa esecuzione deve generalmente essere racchiusa in un profilo Maven specifico per Cloud Manager. In questo esempio viene installato Python.

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

Questa stessa tecnica può essere utilizzata per installare pacchetti specifici per la lingua, ad esempio utilizzando `gem` per RubyGems o `pip` per pacchetti Python.

>[!NOTE]
>
>L&#39;installazione di un pacchetto di sistema in questo modo non lo installa nell&#39;ambiente di runtime utilizzato per l&#39;esecuzione di Adobe Experience Manager. Se hai bisogno di un pacchetto di sistema installato nell’ambiente AEM, contatta il tuo rappresentante Adobe.
