---
title: Progetto di applicazione AEM - Cloud Service
description: Progetto di applicazione AEM - Cloud Service
translation-type: tm+mt
source-git-commit: 696014ea61c049e719c8c9fdccc2a85b087c2466
workflow-type: tm+mt
source-wordcount: '1549'
ht-degree: 9%

---


# Creazione di un progetto di applicazione AEM {#aem-application-project}

## Utilizzo della procedura guidata per creare un progetto di applicazione AEM {#using-wizard-to-create-an-aem-application-project}

Per aiutare a far iniziare i nuovi clienti, Cloud Manager è ora in grado di creare un progetto AEM minimo come punto di partenza. Questo processo si basa sul [**AEM Project Archetype**](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype).


Per creare un progetto di applicazione AEM in Cloud Manager, procedi come segue:

1. Una volta effettuato l’accesso a Cloud Manager e quando la configurazione del programma di base è completa, nella schermata **Panoramica** verrà visualizzato uno speciale invito all’azione, se l’archivio è vuoto.

   ![](assets/create-wizard1.png)

1. Per passare alla schermata **Create a Branch and Project (Crea un ramo e un progetto)**, fai clic su **Crea**.

   ![](assets/create-wizard2.png)

1. La sezione Creazione **progetto in corso** viene visualizzata nella schermata Panoramica ** programma.

   ![](assets/create-wizard3.png)

1. Una volta completata la creazione del programma, la sezione **Aggiungi ambiente** viene visualizzata nella pagina *Program Overview (Panoramica del programma)*.
   ![](assets/create-wizard4.png)

   Per informazioni su come aggiungere o gestire gli ambienti, fare riferimento a [Gestione degli ambienti](/help/implementing/cloud-manager/manage-environments.md) .

## Impostazione del progetto {#setting-up-your-project}

### Modifica dei dettagli di impostazione del progetto {#modifying-project-setup-details}

Per essere generati e distribuiti correttamente con Cloud Manager, i progetti AEM esistenti devono rispettare alcune regole di base:

* I progetti devono essere realizzati con Apache Maven.
* Nella directory principale dell’archivio Git deve essere presente un file *pom.xml* . Questo file *pom.xml* può fare riferimento a tutti i sottomoduli (che a loro volta possono avere altri sottomoduli, ecc.) se necessario.

* Potete aggiungere riferimenti ad altri archivi di artefatti Maven nei file *pom.xml* . L&#39;accesso agli archivi di artefatti protetti da [password è supportato se configurato](#password-protected-maven-repositories) . Tuttavia, l&#39;accesso ai repository di artifact protetti dalla rete non è supportato.
* I pacchetti di contenuto distribuibile vengono rilevati mediante la scansione dei file *zip* del pacchetto di contenuto contenuti contenuti in una directory denominata *target*. Un numero qualsiasi di sottomoduli può produrre pacchetti di contenuto.

* Gli artifact del Dispatcher distribuibile vengono rilevati mediante la scansione di file *zip* (ancora, contenuti in una directory denominata *target*) con directory denominate *conf* e *conf.d*.

* In presenza di più pacchetti di contenuto, l&#39;ordine delle distribuzioni dei pacchetti non è garantito. Se è necessario un ordine specifico, per definire l’ordine è possibile utilizzare le dipendenze del pacchetto di contenuto. I pacchetti possono essere [ignorati](#skipping-content-packages) dalla distribuzione.


## Dettagli ambiente di generazione {#build-environment-details}

Cloud Manager crea e verifica il codice utilizzando un ambiente di build specializzato. Questo ambiente ha i seguenti attributi:

* L&#39;ambiente di costruzione è basato su Linux, derivato da Ubuntu 18.04.
* Apache Maven 3.6.0 è installato.
* Le versioni Java installate sono Oracle JDK 8u202 e 11.0.2.
* Sono installati alcuni pacchetti di sistema aggiuntivi necessari:

   * bzip2
   * decomprimere
   * libpng
   * imagemagick
   * graphicsmagick

* Altri pacchetti possono essere installati in fase di creazione come descritto [di seguito](#installing-additional-system-packages).
* Ogni costruzione è fatta su un ambiente incontaminato; il contenitore di compilazione non mantiene alcuno stato tra le esecuzioni.
* Maven è sempre eseguito con il comando: *mvn —batch-mode clean org.jacoco:jacoco-maven-plugin:Preparare-agent package*
* Maven è configurato a livello di sistema con un file settings.xml che include automaticamente il repository **Artifact**  Adobe pubblico. Per ulteriori informazioni, consultate [archivio](https://repo.adobe.com/) Pubblico Paradiso in Adobe.

>[!NOTE]
>Anche se Cloud Manager non definisce una versione specifica di `jacoco-maven-plugin`, la versione utilizzata deve essere almeno `0.7.5.201505241946`.

### Utilizzo del supporto Java 11 {#using-java-support}

Cloud Manager ora supporta la creazione di progetti per i clienti con Java 8 e Java 11. Per impostazione predefinita, i progetti vengono creati utilizzando Java 8.

I clienti che desiderano utilizzare Java 11 nei loro progetti possono farlo utilizzando il plug-in [Apache Maven Toolchain](https://maven.apache.org/plugins/maven-toolchains-plugin/).

A questo scopo, nel file pom.xml aggiungete una `<plugin>` voce che si presenta così:

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

>[!NOTE]
>I valori del fornitore supportati sono `oracle` e `sun`.
>
>I valori di versione supportati sono `1.8`, `1.11`e `11`.

## Variabili di ambiente {#environment-variables}

### Variabili di ambiente standard {#standard-environ-variables}

In alcuni casi, i clienti trovano necessario variare il processo di creazione in base alle informazioni sul programma o sulla pipeline.

Ad esempio, se si sta effettuando una minificazione JavaScript in fase di creazione, attraverso uno strumento come gulp, potrebbe essere necessario utilizzare un livello di minificazione diverso quando si crea un ambiente di sviluppo anziché costruire per il palco e la produzione.

Per supportare questa funzione, Cloud Manager aggiunge queste variabili di ambiente standard al contenitore di build per ogni esecuzione.

| **Nome variabile** | **Definizione** |
|---|---|
| CM_BUILD | Sempre impostato su &quot;true&quot; |
| BRANCH | Il ramo configurato per l&#39;esecuzione |
| CM_PIPELINE_ID | Identificatore numerico della pipeline |
| CM_PIPELINE_NAME | Il nome della pipeline |
| CM_PROGRAM_ID | Identificatore numerico del programma |
| CM_PROGRAM_NAME | Nome del programma |
| ARTIFACTS_VERSION | Per una fase o una pipeline di produzione, la versione sintetica generata da Cloud Manager |
| CM_AEM_PRODUCT_VERSION | Nome della versione |

### Variabili pipeline {#pipeline-variables}

In alcuni casi, il processo di creazione di un cliente può dipendere da variabili di configurazione specifiche che non sarebbero adatte a essere inserite nell&#39;archivio Git o che dovrebbero variare tra le esecuzioni della pipeline che utilizzano lo stesso ramo.

Cloud Manager consente di configurare queste variabili tramite l&#39;API di Cloud Manager o l&#39;interfaccia CLI di Cloud Manager in base alla pipeline. Le variabili possono essere memorizzate come testo normale o cifrate a riposo. In entrambi i casi, le variabili sono rese disponibili all&#39;interno dell&#39;ambiente di creazione come variabile di ambiente a cui è possibile fare riferimento all&#39;interno del `pom.xml` file o di altri script di compilazione.

Per impostare una variabile utilizzando CLI, eseguire un comando come:

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --variable MY_CUSTOM_VARIABLE test`

È possibile elencare le variabili correnti:

`$ aio cloudmanager:list-pipeline-variables PIPELINEID`

I nomi delle variabili possono contenere solo caratteri alfanumerici e carattere di sottolineatura (_). Per convenzione, i nomi devono essere tutti maiuscoli. Esiste un limite di 200 variabili per pipeline, ogni nome deve essere inferiore a 100 caratteri e ogni valore deve essere inferiore a 2048 caratteri.

Se utilizzata all&#39;interno di un `Maven pom.xml` file, è generalmente utile mappare queste variabili alle proprietà Maven utilizzando una sintassi simile a quella riportata di seguito:

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


## Attivazione dei profili condivisi in Cloud Manager {#activating-maven-profiles-in-cloud-manager}

In alcuni casi limitati, potrebbe essere necessario variare leggermente il processo di creazione quando si esegue in Cloud Manager rispetto a quando viene eseguito su workstation sviluppatore. Per questi casi, [Maven Profiles](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) può essere utilizzato per definire in che modo la build deve essere diversa in ambienti diversi, incluso Cloud Manager.

L&#39;attivazione di un profilo Maven all&#39;interno dell&#39;ambiente di generazione di Cloud Manager deve essere eseguita ricercando la variabile di ambiente CM_BUILD descritta in precedenza. In alternativa, un profilo destinato a essere utilizzato solo al di fuori dell&#39;ambiente di build di Cloud Manager dovrebbe essere fatto cercando l&#39;assurdità di questa variabile.

Ad esempio, se desiderate inviare un messaggio semplice solo quando la build viene eseguita in Cloud Manager, effettuate le seguenti operazioni:

```xml
        <profile>
            <id>cmBuild</id>
            <activation>
                  <property>
                        <name>env.CM_BUILD</name>
                  </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <artifactId>maven-antrun-plugin</artifactId>
                        <version>1.8</version>
                        <executions>
                            <execution>
                                <phase>initialize</phase>
                                <configuration>
                                    <target>
                                        <echo>I'm running inside Cloud Manager!</echo>
                                    </target>
                                </configuration>
                                <goals>
                                    <goal>run</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

>[!NOTE]
>
>Per testare questo profilo su una workstation sviluppatore, è possibile attivarlo sulla riga di comando (con `-PcmBuild`) o nell&#39;ambiente di sviluppo integrato (IDE).

Se desideri inviare un messaggio semplice solo quando la build viene eseguita al di fuori di Cloud Manager, effettua le seguenti operazioni:

```xml
        <profile>
            <id>notCMBuild</id>
            <activation>
                  <property>
                        <name>!env.CM_BUILD</name>
                  </property>
            </activation>
            <build>
                <plugins>
                    <plugin>
                        <artifactId>maven-antrun-plugin</artifactId>
                        <version>1.8</version>
                        <executions>
                            <execution>
                                <phase>initialize</phase>
                                <configuration>
                                    <target>
                                        <echo>I'm running outside Cloud Manager!</echo>
                                    </target>
                                </configuration>
                                <goals>
                                    <goal>run</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
```

## Supporto dell&#39;archivio protetto da password {#password-protected-maven-repositories}

Per utilizzare un repository Maven protetto da password da Cloud Manager, specificate la password (e facoltativamente il nome utente) come variabile [](#pipeline-variables) pipeline segreta e fate riferimento a tale segreto all&#39;interno di un file denominato `.cloudmanager/maven/settings.xml` nel repository Git. Questo file segue lo schema [Maven Settings File](https://maven.apache.org/settings.html) . All&#39;avvio del processo di build di Cloud Manager, l&#39; `<servers>` elemento in questo file verrà unito al `settings.xml` file predefinito fornito da Cloud Manager. Gli ID server che iniziano con `adobe` e `cloud-manager` sono considerati riservati e non devono essere utilizzati dai server personalizzati. Gli ID server **che non** corrispondono a uno di questi prefissi o l&#39;ID predefinito non `central` verrà mai eseguito il mirroring da Cloud Manager. Con questo file in posizione, all&#39;ID del server viene fatto riferimento dall&#39;interno di un elemento `<repository>` e/o `<pluginRepository>` all&#39;interno del `pom.xml` file. In genere, questi `<repository>` e/o `<pluginRepository>` elementi sono contenuti all&#39;interno di un profilo [specifico di](#activating-maven-profiles-in-cloud-manager)Cloud Manager, anche se ciò non è strettamente necessario.

Ad esempio, supponiamo che il repository si trovi all&#39;indirizzo https://repository.myco.com/maven2, che il nome utente Cloud Manager debba utilizzare sia `cloudmanager` e la password sia `secretword`.

In primo luogo, imposta la password come un segreto sulla pipeline:

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword`

Fate quindi riferimento a questo dal `.cloudmanager/maven/settings.xml` file:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">
    <servers>
        <server>
            <id>myco-repository</id>
            <username>cloudmanager</username>
            <password>${env.CUSTOM_MYCO_REPOSITORY_PASSWORD}</password>
        </server>
    </servers>
</settings>
```

Infine, fate riferimento all&#39;ID del server all&#39;interno del `pom.xml` file:

```xml
<profiles>
    <profile>
        <id>cmBuild</id>
        <activation>
                <property>
                    <name>env.CM_BUILD</name>
                </property>
        </activation>
        <build>
            <repositories>
                <repository>
                    <id>myco-repository</id>
                    <name>MyCo Releases</name>
                    <url>https://repository.myco.com/maven2</url>
                    <snapshots>
                        <enabled>false</enabled>
                    </snapshots>
                    <releases>
                        <enabled>true</enabled>
                    </releases>
                </repository>
            </repositories>
            <pluginRepositories>
                <pluginRepository>
                    <id>myco-repository</id>
                    <name>MyCo Releases</name>
                    <url>https://repository.myco.com/maven2</url>
                    <snapshots>
                        <enabled>false</enabled>
                    </snapshots>
                    <releases>
                        <enabled>true</enabled>
                    </releases>
                </pluginRepository>
            </pluginRepositories>
        </build>
    </profile>
</profiles>
```

## Installazione di pacchetti di sistema aggiuntivi {#installing-additional-system-packages}

Alcune build richiedono l&#39;installazione di pacchetti di sistema aggiuntivi per funzionare completamente. Ad esempio, una build può richiamare uno script Python o ruby e, di conseguenza, deve disporre di un interprete lingua appropriato installato. Questo può essere fatto chiamando [exec-maven-plugin](https://www.mojohaus.org/exec-maven-plugin/) per richiamare APT. In genere, questa esecuzione deve essere racchiusa in un profilo Maven specifico per Cloud Manager. Ad esempio, per installare python:

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

Questa stessa tecnica può essere utilizzata per installare pacchetti specifici per la lingua, ad esempio per `gem` RubyGems o `pip` per Python Packages.

>[!NOTE]
>
>L&#39;installazione di un pacchetto di sistema in questo modo **non** lo installa nell&#39;ambiente di runtime utilizzato per eseguire Adobe Experience Manager. Se avete bisogno di installare un pacchetto di sistema nell&#39;ambiente AEM, contattate il rappresentante  Adobe.

## Skiping Content Packages {#skipping-content-packages}

In Cloud Manager, le build possono generare un numero qualsiasi di pacchetti di contenuto.
Per diversi motivi, può essere utile produrre un pacchetto di contenuti ma non distribuirlo. Questo può essere utile, ad esempio, quando si creano pacchetti di contenuto utilizzati solo per il test o che verranno reinseriti in un pacchetto da un altro passaggio del processo di creazione, ovvero come pacchetto secondario di un altro pacchetto.

Per soddisfare questi scenari, Cloud Manager cercherà una proprietà denominata ***cloudManagerTarget*** tra le proprietà dei pacchetti di contenuto incorporati. Se questa proprietà è impostata su none, il pacchetto verrà ignorato e non distribuito. Il meccanismo per impostare questa proprietà dipende dal modo in cui la build produce il pacchetto di contenuto. Ad esempio, con filevault-maven-plugin si configura il plugin come segue:

```xml
        <plugin>
            <groupId>org.apache.jackrabbit</groupId>
            <artifactId>filevault-package-maven-plugin</artifactId>
            <extensions>true</extensions>
            <configuration>
                <properties>
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
        <!-- other configuration -->
            </configuration>
        </plugin>
```

Con content-package-maven-plugin è simile:

```xml
        <plugin>
            <groupId>com.day.jcr.vault</groupId>
            <artifactId>content-package-maven-plugin</artifactId>
            <extensions>true</extensions>
            <configuration>
                <properties>
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
        <!-- other configuration -->
            </configuration>
        </plugin>
```

## Risorse aggiuntive {#additional-resources}

Per informazioni sull&#39;utilizzo di Cloud Manager nel Cloud Service, consulta le sezioni seguenti:

* [Gestione degli ambienti](/help/implementing/cloud-manager/manage-environments.md)
* [Configurare la pipeline CI-CD](/help/implementing/cloud-manager/configure-pipeline.md)
* [Implementazione del codice](/help/implementing/cloud-manager/deploy-code.md)
* [Risultati dei test](/help/implementing/developing/introduction/understand-test-results.md)