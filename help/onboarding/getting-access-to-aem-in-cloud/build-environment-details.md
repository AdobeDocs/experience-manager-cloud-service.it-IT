---
title: Dettagli dell’ambiente di generazione
description: Dettagli dell’ambiente di creazione - Cloud Services
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
source-git-commit: 558cd516a89d9012e96fb0b783d0df3eecfda73d
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 0%

---

# Informazioni sull’ambiente di creazione {#understanding-build-environment}

## Dettagli dell’ambiente di generazione {#build-environment-details}

Cloud Manager crea ed esegue il test del codice utilizzando un ambiente di build specializzato. Questo ambiente ha i seguenti attributi:

* L&#39;ambiente di creazione è basato su Linux, derivato da Ubuntu 18.04.
* Apache Maven 3.6.0 è installato.
* Le versioni Java installate sono Oracle JDK 8u202, Azul Zulu 8u292, Oracle JDK 11.0.2 e Azul Zulu 11.0.11.
* Sono installati alcuni pacchetti di sistema aggiuntivi necessari:

   * bzip2
   * decomprimere
   * libpng
   * immaginemagick
   * graphicsmagick

* Altri pacchetti possono essere installati in fase di creazione come descritto [sotto](#installing-additional-system-packages).
* Ogni costruzione è fatta su un ambiente incontaminato; il contenitore build non mantiene nessuno stato tra le esecuzioni.
* Maven viene sempre eseguito con i tre comandi seguenti:

   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent packageco-maven-plugin:prepare-agent package`
* Maven è configurato a livello di sistema con un file settings.xml che include automaticamente l’archivio dell’Adobe pubblico **Artifact** utilizzando un profilo denominato `adobe-public`. (Per ulteriori informazioni, consulta [Adobe Public Maven Repository](https://repo.adobe.com/) .

>[!NOTE]
>Anche se Cloud Manager non definisce una versione specifica di `jacoco-maven-plugin`, la versione utilizzata deve essere almeno `0.7.5.201505241946`.

### Utilizzo di una versione Java specifica {#using-java-support}

Per impostazione predefinita, i progetti sono generati dal processo di creazione di Cloud Manager utilizzando il JDK di Oracle 8. I clienti che desiderano utilizzare un JDK alternativo hanno due opzioni: Maven Toolchain e selezione di una versione JDK alternativa per l&#39;intero processo di esecuzione Maven.

#### Catene di strumenti Maven {#maven-toolchains}

Il [Plug-in Maven Toolchain](https://maven.apache.org/plugins/maven-toolchains-plugin/) consente ai progetti di selezionare un JDK specifico (o *toolchain*) da utilizzare nel contesto dei plug-in Maven consapevoli delle catene degli strumenti. Questo viene fatto nel file `pom.xml` del progetto specificando un valore di fornitore e versione. Una sezione di esempio nel file `pom.xml` è:

```
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

Quando si utilizza questo metodo, Maven stesso viene comunque eseguito utilizzando il JDK predefinito (Oracle 8). Pertanto, il controllo o l’applicazione della versione Java tramite plug-in come Apache Maven Enforcer Plugin non funziona e tali plug-in non devono essere utilizzati.

Le combinazioni fornitore/versione attualmente disponibili sono:

* oracle 1.8
* oracle 1.11
* oracle 11
* Sole 1.8
* sole 1.11
* sole 11
* azul 1.8
* azul 1,11
* azul 8

#### Versione JDK di esecuzione Maven alternativa {#alternate-maven-jdk-version}

È anche possibile selezionare Azul 8 o Azul 11 come JDK per l&#39;intera esecuzione Maven. A differenza delle opzioni delle catene degli strumenti, questo cambia il JDK utilizzato per tutti i plugin a meno che la configurazione delle catene degli utensili non sia impostata anche nel qual caso la configurazione delle catene degli utensili viene ancora applicata per i plugin Maven consapevoli delle catene degli utensili. Di conseguenza, il controllo e l&#39;applicazione della versione Java utilizzando il [plugin Apache Maven Enforcer](https://maven.apache.org/enforcer/maven-enforcer-plugin/) funzionerà.

A questo scopo, crea un file denominato `.cloudmanager/java-version` nel ramo dell’archivio Git utilizzato dalla pipeline. Questo file può avere il contenuto 11 o 8. Qualsiasi altro valore viene ignorato. Se è specificato 11, viene utilizzato Azul 11. Se si specifica 8, viene utilizzato Azul 8.

>[!NOTE]
>In una versione futura di Cloud Manager, attualmente stimata a ottobre 2021, il JDK predefinito verrà modificato e il valore predefinito sarà Azul 11. I progetti non compatibili con Java 11 devono creare questo file con il contenuto 8 il prima possibile per evitare che siano interessati da questo passaggio.


## Variabili di ambiente {#environment-variables}

### Variabili di ambiente standard {#standard-environ-variables}

In alcuni casi, i clienti trovano necessario variare il processo di creazione in base alle informazioni sul programma o sulla pipeline.

Ad esempio, se si esegue la minimizzazione JavaScript in fase di creazione, tramite uno strumento come gulp, potrebbe essere utile utilizzare un livello di minimizzazione diverso durante la creazione di un ambiente di sviluppo, anziché per la creazione di stage e produzione.

Per supportare questa funzione, Cloud Manager aggiunge queste variabili di ambiente standard al contenitore di build per ogni esecuzione.

| **Nome della variabile** | **Definizione** |
|---|---|
| CM_BUILD | Imposta sempre su &quot;true&quot; |
| BRANCH | Il ramo configurato per l’esecuzione |
| CM_PIPELINE_ID | Identificatore numerico della pipeline |
| CM_PIPELINE_NAME | Nome della pipeline |
| CM_PROGRAM_ID | Identificatore numerico del programma |
| CM_PROGRAM_NAME | Nome del programma |
| ARTIFACTS_VERSION | Per una fase o una pipeline di produzione, la versione sintetica generata da Cloud Manager |
| CM_AEM_PRODUCT_VERSION | Nome del rilascio |

### Variabili di pipeline {#pipeline-variables}

In alcuni casi, il processo di creazione di un cliente può dipendere da specifiche variabili di configurazione che non sarebbero appropriate per l’inserimento nell’archivio Git o dovrebbero variare tra le esecuzioni della pipeline che utilizzano lo stesso ramo.

Cloud Manager consente di configurare queste variabili tramite l’API di Cloud Manager o l’CLI di Cloud Manager in base alla pipeline. Le variabili possono essere memorizzate come testo normale o cifrate a riposo. In entrambi i casi, le variabili sono rese disponibili all&#39;interno dell&#39;ambiente di creazione come variabile di ambiente a cui è possibile fare riferimento all&#39;interno del file `pom.xml` o di altri script di compilazione.

Per impostare una variabile utilizzando CLI, esegui un comando simile al seguente:

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test`

È possibile elencare le variabili correnti:

`$ aio cloudmanager:list-pipeline-variables PIPELINEID`

I nomi delle variabili possono contenere solo caratteri alfanumerici e carattere di sottolineatura (_). Per convenzione, i nomi devono essere tutti maiuscoli. Esiste un limite di 200 variabili per pipeline, ogni nome deve essere inferiore a 100 caratteri e ogni valore deve essere inferiore a 2048 caratteri nel caso di variabili di tipo stringa e a 500 caratteri nel caso di variabili di tipo secretString.

Quando viene utilizzato all&#39;interno di un file `Maven pom.xml`, è in genere utile mappare queste variabili alle proprietà Maven utilizzando una sintassi simile alla seguente:

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

Alcune build richiedono l&#39;installazione di pacchetti di sistema aggiuntivi per funzionare completamente. Ad esempio, una build può richiamare uno script Python o ruby e, di conseguenza, deve disporre di un interprete di lingua appropriato installato. A tale scopo, è necessario chiamare [exec-maven-plugin](https://www.mojohaus.org/exec-maven-plugin/) per richiamare APT. Questa esecuzione deve generalmente essere racchiusa in un profilo Maven specifico per Cloud Manager. Ad esempio, per installare python:

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
>L&#39;installazione di un pacchetto di sistema in questo modo **non** lo installa nell&#39;ambiente di runtime utilizzato per l&#39;esecuzione di Adobe Experience Manager. Se hai bisogno di installare un pacchetto di sistema nell’ambiente AEM, contatta il tuo rappresentante Adobe.
