---
title: Dettagli di configurazione del progetto
description: Dettagli configurazione progetto - Cloud Services
exl-id: 76af0171-8ed5-4fc7-b5d5-7da5a1a06fa8
source-git-commit: b9bb9e7b63a53ea1a6ce1e126285bb84c8351083
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 7%

---

# Configurazione del progetto {#project-setup-details}

## Modifica dei dettagli di configurazione del progetto {#modifying-project-setup-details}

Per poter essere generati e implementati correttamente con Cloud Manager, i progetti AEM esistenti devono rispettare alcune regole di base:

* I progetti devono essere generati utilizzando Apache Maven.
* Nella directory principale dell’archivio Git deve essere presente un file *pom.xml*. Questo file *pom.xml* può fare riferimento a tutti i sottomoduli (che a loro volta possono avere altri sottomoduli, ecc.) se necessario.

* Puoi aggiungere riferimenti ad altri archivi di artefatti Maven nei file *pom.xml*. L&#39;accesso a [archivi di artefatti protetti da password](#password-protected-maven-repositories) è supportato quando è configurato. Tuttavia, l&#39;accesso agli archivi di artefatti protetti dalla rete non è supportato.
* I pacchetti di contenuti distribuibili vengono rilevati eseguendo la scansione dei file *zip* contenuti in una directory denominata *target*. Un numero qualsiasi di sottomoduli può produrre pacchetti di contenuti.

* Gli artefatti distribuibili del Dispatcher vengono rilevati eseguendo la scansione di file *zip* (ancora una volta, contenuti in una directory denominata *target*) con directory denominate *conf* e *conf.d*.

* Se sono presenti più pacchetti di contenuto, l’ordine delle distribuzioni dei pacchetti non è garantito. Se è necessario un ordine specifico, le dipendenze del pacchetto di contenuti possono essere utilizzate per definire l’ordine. I pacchetti possono essere [ignorati](#skipping-content-packages) dalla distribuzione.


## Attivazione dei profili Maven in Cloud Manager {#activating-maven-profiles-in-cloud-manager}

In alcuni casi limitati, potrebbe essere necessario variare leggermente il processo di generazione quando si esegue in Cloud Manager rispetto a quando si esegue su workstation per sviluppatori. Per questi casi, [Profili Maven](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) può essere utilizzato per definire come la build deve essere diversa in ambienti diversi, incluso Cloud Manager.

L’attivazione di un profilo Maven nell’ambiente di build di Cloud Manager deve essere eseguita cercando la variabile di ambiente CM_BUILD descritta sopra. Al contrario, un profilo destinato a essere utilizzato solo al di fuori dell’ambiente di build di Cloud Manager deve essere fatto cercando l’assenza di questa variabile.

Ad esempio, se desideri inviare un messaggio semplice solo quando la build viene eseguita in Cloud Manager, effettua le seguenti operazioni:

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
>Per testare questo profilo su una workstation sviluppatore, puoi abilitarlo sulla riga di comando (con `-PcmBuild`) o nell’ambiente di sviluppo integrato (IDE).

E se desideri inviare un messaggio semplice solo quando la build viene eseguita al di fuori di Cloud Manager, effettua le seguenti operazioni:

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

## Supporto dell&#39;archivio Maven protetto da password {#password-protected-maven-repositories}

>[!NOTE]
>Gli artefatti provenienti da un archivio Maven protetto da password devono essere utilizzati con molta cautela, in quanto il codice distribuito tramite questo meccanismo attualmente non viene eseguito attraverso tutte le regole di qualità implementate nei Gates di qualità di Cloud Manager. Pertanto dovrebbe essere utilizzato solo in rari casi e per codice non legato a AEM. Si consiglia inoltre di distribuire le origini Java e l&#39;intero codice sorgente del progetto insieme al binario.

Per utilizzare un archivio Maven protetto da password da Cloud Manager, specifica la password (e facoltativamente il nome utente) come variabile di pipeline segreta e fai riferimento a tale segreto all’interno di un file denominato `.cloudmanager/maven/settings.xml` nell’archivio Git. Questo file segue lo schema [File impostazioni Maven](https://maven.apache.org/settings.html) . All’avvio del processo di compilazione di Cloud Manager, l’elemento `<servers>` in questo file verrà unito al file `settings.xml` predefinito fornito da Cloud Manager. Gli ID server che iniziano con `adobe` e `cloud-manager` sono considerati riservati e non devono essere utilizzati dai server personalizzati. Gli ID server **non** che corrispondono a uno di questi prefissi o l&#39;ID predefinito `central` non verranno mai rispecchiati da Cloud Manager. Con questo file attivo, all&#39;interno di un elemento `<repository>` e/o `<pluginRepository>` all&#39;interno del file `pom.xml` viene fatto riferimento all&#39;ID del server. In genere, questi elementi `<repository>` e/o `<pluginRepository>` sono contenuti all’interno di un profilo specifico di [Cloud Manager](#activating-maven-profiles-in-cloud-manager), anche se ciò non è strettamente necessario.

Ad esempio, supponiamo che l’archivio sia all’indirizzo https://repository.myco.com/maven2, che il nome utente Cloud Manager utilizzi sia `cloudmanager` e che la password sia `secretword`.

Innanzitutto, imposta la password come segreto sulla pipeline:

`$ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword`

Fai quindi riferimento a questo dal file `.cloudmanager/maven/settings.xml` :

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

Infine, fai riferimento all&#39;ID server all&#39;interno del file `pom.xml` :

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

È buona prassi distribuire le origini Java insieme al binario in un archivio Maven.

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

### Distribuzione di origini di progetto {#deploying-project-sources}

È buona prassi distribuire l’intera origine del progetto insieme al binario in un archivio Maven, in modo da ricreare l’artefatto esatto.

Configura il plug-in maven-assembly nel progetto:

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

## Ignora pacchetti di contenuto {#skipping-content-packages}

In Cloud Manager, le build possono produrre un numero qualsiasi di pacchetti di contenuto.
Per vari motivi, può essere opportuno creare un pacchetto di contenuti ma non distribuirlo. Ciò può essere utile, ad esempio, quando si creano pacchetti di contenuto utilizzati solo per il test o che verranno reimballati da un altro passaggio del processo di compilazione, ovvero come pacchetto secondario di un altro pacchetto.

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
