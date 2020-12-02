---
title: Dettagli configurazione progetto
description: Dettagli configurazione progetto - Cloud Services
translation-type: tm+mt
source-git-commit: 207d0742e8bf46065c7e20bec7d88b0776c246b2
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 7%

---


# Impostazione del progetto {#project-setup-details}

## Modifica dei dettagli di impostazione del progetto {#modifying-project-setup-details}

Per essere generati e distribuiti correttamente con Cloud Manager, i progetti AEM esistenti devono rispettare alcune regole di base:

* I progetti devono essere realizzati con Apache Maven.
* Nella directory principale dell&#39;archivio Git deve essere presente un file *pom.xml*. Questo file *pom.xml* può fare riferimento a tanti sottomoduli (che a loro volta possono avere altri sottomoduli, ecc.) se necessario.

* È possibile aggiungere riferimenti ad altri archivi di artefatti Maven nei file *pom.xml*. L&#39;accesso a [archivi di artefatti protetti da password](#password-protected-maven-repositories) è supportato se configurato. Tuttavia, l&#39;accesso ai repository di artifact protetti dalla rete non è supportato.
* I pacchetti di contenuto distribuibile vengono rilevati mediante la scansione dei file *zip* contenuti in una directory denominata *target*. Un numero qualsiasi di sottomoduli può produrre pacchetti di contenuti.

* Gli artifact del dispatcher distribuibile vengono rilevati mediante la scansione di file *zip* (ancora una volta, contenuti in una directory denominata *target*) con directory denominate *conf* e *conf.d*.

* In presenza di più pacchetti di contenuto, l&#39;ordine delle distribuzioni dei pacchetti non è garantito. Se è necessario un ordine specifico, per definire l’ordine è possibile utilizzare le dipendenze del pacchetto di contenuto. I pacchetti possono essere [ignorati](#skipping-content-packages) dalla distribuzione.


## Attivazione dei profili condivisi in Cloud Manager {#activating-maven-profiles-in-cloud-manager}

In alcuni casi limitati, potrebbe essere necessario variare leggermente il processo di creazione quando si esegue in Cloud Manager rispetto a quando viene eseguito su workstation sviluppatore. Per questi casi, è possibile utilizzare [Profili mobili](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) per definire in che modo la build deve essere diversa in ambienti diversi, incluso Cloud Manager.

L&#39;attivazione di un profilo Maven all&#39;interno dell&#39;ambiente di generazione di Cloud Manager deve essere eseguita ricercando la variabile di ambiente CM_BUILD descritta in precedenza. Al contrario, un profilo destinato ad essere utilizzato solo al di fuori dell&#39;ambiente di build di Cloud Manager dovrebbe essere fatto cercando l&#39;assenza di questa variabile.

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

## Supporto per l&#39;archivio protetto da password {#password-protected-maven-repositories}

>[!NOTE]
>Gli artefatti provenienti da un archivio Maven protetto da password dovrebbero essere utilizzati con molta cautela, in quanto il codice distribuito tramite questo meccanismo attualmente non viene eseguito tramite i gateway di qualità di Cloud Manager. Pertanto dovrebbe essere utilizzato solo in rari casi e per codici non legati a AEM. Si consiglia inoltre di distribuire le origini Java e l&#39;intero codice sorgente del progetto insieme al binario.

Per utilizzare un repository Maven protetto da password da Cloud Manager, specificate la password (e facoltativamente il nome utente) come segreto [Variabile pipeline](#pipeline-variables), quindi fate riferimento a tale segreto all&#39;interno di un file denominato `.cloudmanager/maven/settings.xml` nell&#39;archivio git. Questo file segue lo schema [Maven Settings File](https://maven.apache.org/settings.html). All&#39;avvio del processo di creazione di Cloud Manager, l&#39;elemento `<servers>` in questo file verrà unito al file `settings.xml` predefinito fornito da Cloud Manager. Gli ID server che iniziano con `adobe` e `cloud-manager` sono considerati riservati e non devono essere utilizzati dai server personalizzati. Gli ID server **non** corrispondenti a uno di questi prefissi oppure l&#39;ID predefinito `central` non verrà mai rispecchiato da Cloud Manager. Con questo file in posizione, all&#39;interno di un elemento `<repository>` e/o `<pluginRepository>` all&#39;interno del file `pom.xml` viene fatto riferimento all&#39;ID del server. In genere, questi elementi `<repository>` e/o `<pluginRepository>` sono contenuti all&#39;interno di un profilo specifico di [Cloud Manager](#activating-maven-profiles-in-cloud-manager), anche se ciò non è strettamente necessario.

Ad esempio, supponiamo che l&#39;archivio si trovi all&#39;indirizzo https://repository.myco.com/maven2, che il nome utente Cloud Manager utilizzi `cloudmanager` e che la password sia `secretword`.

In primo luogo, imposta la password come un segreto sulla pipeline:

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword`

Fate quindi riferimento al file `.cloudmanager/maven/settings.xml`:

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

Infine, fate riferimento all&#39;ID del server all&#39;interno del file `pom.xml`:

```xml
<profiles>
    <profile>
        <id>cmBuild</id>
        <activation>
                <property>
                    <name>env.CM_BUILD</name>
                </property>
        </activation>
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
    </profile>
</profiles>
```

### Distribuzione di origini {#deploying-sources}

È buona norma distribuire le origini Java insieme con il binario a un repository Maven.

Configura il plug-in maven-source nel tuo progetto:

```xml
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-source-plugin</artifactId>
            <executions>
                <execution>
                    <id>attach-sources</id>
                    <goals>
                        <goal>jar-no-fork</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
```

### Distribuzione di origini progetto {#deploying-project-sources}

È una buona prassi distribuire l&#39;intera origine del progetto insieme con il binario a un repository Maven - questo permette di ricostruire l&#39;esatto artefatto.

Configurate il plug-in di assemblaggio del vostro progetto:

```xml
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-assembly-plugin</artifactId>
            <executions>
                <execution>
                    <id>project-assembly</id>
                    <phase>package</phase>
                    <goals>
                        <goal>single</goal>
                    </goals>
                    <configuration>
                        <descriptorRefs>
                            <descriptorRef>project</descriptorRef>
                        </descriptorRefs>
                    </configuration>
                </execution>
            </executions>
        </plugin>
```

## Skipping Content Packages {#skipping-content-packages}

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
