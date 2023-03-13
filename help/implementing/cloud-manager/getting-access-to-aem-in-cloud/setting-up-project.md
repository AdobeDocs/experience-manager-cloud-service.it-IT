---
title: Configurazione del progetto
description: Scopri come creare progetti AEM con Maven e gli standard da osservare durante la creazione di un progetto personalizzato.
exl-id: 76af0171-8ed5-4fc7-b5d5-7da5a1a06fa8
source-git-commit: cc6565121a76f70b958aa9050485e0553371f3a3
workflow-type: tm+mt
source-wordcount: '1415'
ht-degree: 100%

---

# Configurazione del progetto {#project-setup}

Scopri come creare progetti AEM con Maven e gli standard da osservare durante la creazione di un progetto personalizzato.

## Dettagli della configurazione del progetto {#project-setup-details}

Per poter essere generati e distribuiti correttamente con Cloud Manager, i progetti AEM devono rispettare le seguenti linee guida:

* I progetti devono essere generati con [Apache Maven.](https://maven.apache.org)
* Nella radice dell’archivio Git deve essere presente un file `pom.xml`. Il file `pom.xml` può fare riferimento a tutti i moduli secondari (che a loro volta possono prevedere altri moduli secondari e così via) secondo necessità.
* Puoi aggiungere riferimenti ad altri archivi di artefatti Maven nel file `pom.xml`.
   * Quando configurato, l’accesso agli [archivi di artefatti protetti da password](#password-protected-maven-repositories) è supportato. Tuttavia, l’accesso agli archivi di artefatti protetti dalla rete non è supportato.
* I pacchetti di contenuti distribuibili vengono rilevati mediante l’analisi dei file `.zip` del pacchetto di contenuti, che si trovano in una directory denominata `target`.
   * I pacchetti di contenuti possono essere prodotti da qualsiasi modulo secondario.
* Gli artefatti dispatcher distribuibili vengono rilevati mediante l’analisi dei file `.zip` (presenti anche nella directory denominata `target`), le cui directory sono `conf` e `conf.d`.
* Se sono presenti più pacchetti di contenuti, l’ordinamento delle distribuzioni dei pacchetti non è garantito.
   * Se è necessario un ordine specifico, puoi definirlo con le dipendenze dei pacchetti di contenuti.
* I pacchetti possono essere [ignorati](#skipping-content-packages) durante la distribuzione.

## Attivazione dei profili Maven in Cloud Manager {#activating-maven-profiles-in-cloud-manager}

In alcuni casi limitati, potrebbe essere necessario modificare leggermente il processo di build durante l’esecuzione in Cloud Manager rispetto a quando viene eseguito dalle workstation di sviluppo. Per questi casi è possibile utilizzare i [profili Maven](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) per definire il modo in cui la build deve differire nei diversi ambienti, incluso Cloud Manager.

L’attivazione di un profilo Maven all’interno dell’ambiente di build di Cloud Manager deve essere eseguita cercando la [variabile di ambiente `CM_BUILD`.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) Analogamente, per un profilo destinato a essere utilizzato esclusivamente all’esterno dell’ambiente di build di Cloud Manager, è necessario verificare l’assenza di tale variabile.

Ad esempio, per inviare un semplice messaggio solo quando la build viene eseguita in Cloud Manager, effettua questa operazione.

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
>Per eseguire test di questo profilo da una workstation di sviluppo, è possibile abilitarlo nella riga di comando (con `-PcmBuild`) o nell’ambiente di sviluppo integrato (IDE).

Per inviare un semplice messaggio solo quando la build viene eseguita all’esterno di Cloud Manager, effettua questa operazione.

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

## Supporto dell’archivio Maven protetto da password {#password-protected-maven-repositories}

>[!NOTE]
>
>Gli artefatti di un archivio Maven protetto da password devono essere utilizzati con cautela, in quanto attualmente il codice distribuito tramite questo meccanismo non viene eseguito da tutte le [regole per la qualità del codice](/help/implementing/cloud-manager/custom-code-quality-rules.md) implementate nei gate di qualità di Cloud Manager. Per questo motivo, è consigliabile utilizzarlo esclusivamente in rari casi e solo per il codice non collegato a AEM. Si consiglia inoltre di distribuire le origini Java e l’intero codice sorgente del progetto insieme ai dati binari.

Per utilizzare un archivio Maven protetto da password in Cloud Manager:

1. Specifica la password (e facoltativamente il nome utente) come [variabile segreta della pipeline.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)
1. Fai riferimento al segreto all’interno del file denominato `.cloudmanager/maven/settings.xml` nell’archivio Git, che segue lo schema del [file delle impostazioni Maven](https://maven.apache.org/settings.html).

All’avvio del processo di build di Cloud Manager:

* L’elemento `<servers>` in questo file viene unito al file `settings.xml` predefinito fornito da Cloud Manager.
   * Gli ID server che iniziano con `adobe` e `cloud-manager` sono considerati riservati e non devono essere utilizzati per i server personalizzati.
   * Per gli ID server che non corrispondono a uno di questi prefissi o all’ID predefinito `central`, il mirroring non viene mai eseguito da Cloud Manager.
* Quando questo file è presente, si fa riferimento all’ID server da un `<repository>` e/o da un elemento del `<pluginRepository>` contenuto nel file `pom.xml`.
* In generale, questi elementi di `<repository>` e/o di `<pluginRepository>` sono contenuti in un [profilo specifico di Cloud Manager](#activating-maven-profiles-in-cloud-manager), anche se ciò non è strettamente necessario.

Supponiamo ad esempio che l’archivio si trovi nella posizione `https://repository.myco.com/maven2` e che il nome utente che Cloud Manager debba utilizzare sia `cloudmanager`, con password `secretword`. Effettua le seguenti operazioni.

1. Imposta la password come segreto nella pipeline.

   ```text
   $ aio cloudmanager:set-pipeline-variables PIPELINEID --secret CUSTOM_MYCO_REPOSITORY_PASSWORD secretword`
   ```

1. Fai riferimento al segreto dal file `.cloudmanager/maven/settings.xml`.

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <settings xmlns="https://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="https://maven.apache.org/SETTINGS/1.0.0 https://maven.apache.org/xsd/settings-1.0.0.xsd">
       <servers>
           <server>
               <id>myco-repository</id>
               <username>cloudmanager</username>
              <password>${env.CUSTOM_MYCO_REPOSITORY_PASSWORD}</password>
           </server>
       </servers>
   </settings>
   ```

1. Infine, fai riferimento all’ID server nel file `pom.xml`:

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

### Distribuzione delle origini {#deploying-sources}

È buona prassi distribuire le origini Java insieme ai dati binari in un archivio Maven.

Per eseguire l’operazione, configura il plug-in maven-source nel progetto.

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

### Distribuzione delle origini del progetto {#deploying-project-sources}

È buona prassi distribuire l’intera origine del progetto insieme ai dati binari in un archivio Maven. Questo permette di rigenerare l’artefatto in modo esatto.

Per eseguire l’operazione, configura il plug-in maven-assembly nel progetto.

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

## Ignorare i pacchetti di contenuti {#skipping-content-packages}

In Cloud Manager le build possono produrre qualsiasi numero di pacchetti di contenuti. Per diversi motivi può essere utile produrre un pacchetto di contenuti ma non distribuirlo. Un esempio potrebbe essere la creazione di pacchetti di contenuti utilizzati solo a scopi di test o che verranno ricompilati da un altro passaggio del processo di build, ovvero come pacchetti secondari di un altro pacchetto.

Per soddisfare questi scenari, Cloud Manager cercherà una proprietà denominata `cloudManagerTarget` tra le proprietà dei pacchetti di contenuti generati. Se questa proprietà è impostata su `none`, il pacchetto verrà ignorato e non distribuito.

Il meccanismo per impostare questa proprietà dipende dal modo in cui la build produce il pacchetto di contenuti. Ad esempio, con `filevault-maven-plugin` è possibile configurare il plug-in come indicato di seguito.

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

`content-package-maven-plugin` presenta una configurazione analoga.

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

## Riutilizzo degli artefatti di generazione {#build-artifact-reuse}

In molti casi, lo stesso codice viene distribuito in più ambienti AEM. Quando possibile, Cloud Manager evita di ricompilare la base di codice quando rileva che lo stesso commit Git viene utilizzato in più esecuzioni di pipeline full stack.

All’avvio di un’esecuzione, viene estratto il commit HEAD corrente per la pipeline del ramo. L’hash del commit è visibile nell’interfaccia utente e tramite l’API. Al termine della fase di build, gli artefatti risultanti vengono archiviati in base a tale hash di commit e possono essere riutilizzati nelle esecuzioni successive della pipeline.

Se si trovano nello stesso programma, i pacchetti vengono riutilizzati tra le pipeline. Durante la ricerca di pacchetti da poter riutilizzare, AEM ignora i rami e riutilizza gli artefatti tra rami.

In caso di un riutilizzo, i passaggi di build e qualità del codice vengono effettivamente sostituiti con i risultati dell’esecuzione originale. Il file di registro della fase di build elenca gli artefatti e le informazioni sull’esecuzione utilizzate per generarli originariamente.

Di seguito è riportato un esempio di tale output di registro.

```shell
The following build artifacts were reused from the prior execution 4 of pipeline 1 which used commit f6ac5e6943ba8bce8804086241ba28bd94909aef:
build/aem-guides-wknd.all-2021.1216.1101633.0000884042.zip (content-package)
build/aem-guides-wknd.dispatcher.cloud-2021.1216.1101633.0000884042.zip (dispatcher-configuration)
```

Il registro del passaggio di qualità del codice conterrà informazioni simili alle seguenti.

### Esempi {#example-reuse}

#### Esempio 1 {#example-1}

Ipotizza di utilizzare un programma con due pipeline di sviluppo:

* Pipeline 1 su ramo `foo`
* Pipeline 2 su ramo `bar`

Entrambi i rami presentano lo stesso ID commit.

1. L’esecuzione delle pipeline 1 genera i pacchetti normalmente.
1. L’esecuzione della pipeline 2 riutilizza i pacchetti creati dalla pipeline 1.

#### Esempio 2 {#example-2}

Ipotizza di utilizzare un programma con due rami:

* Ramo `foo`
* Ramo `bar`

Entrambi i rami presentano lo stesso ID commit.

1. Una pipeline di sviluppo genera ed esegue `foo`.
1. Successivamente una pipeline di produzione genera ed esegue `bar`.

In questo caso, l’artefatto di `foo` viene riutilizzato per la pipeline di produzione poiché è stato identificato lo stesso hash di commit.

### Disattivazione {#opting-out}

Se lo desideri, puoi disattivare il comportamento di riutilizzo per specifiche pipeline impostando la variabile di pipeline `CM_DISABLE_BUILD_REUSE` su `true`. Configurando questa variabile, l’hash di commit viene comunque estratto e gli artefatti risultanti vengono archiviati per un uso successivo. Tuttavia, gli eventuali artefatti archiviati in precedenza non vengono riutilizzati. Per comprendere questo comportamento, considera lo scenario seguente.

1. Viene creata una nuova pipeline.
1. La pipeline viene eseguita (esecuzione n. 1) e il commit HEAD corrente è `becdddb`. L’esecuzione ha esito positivo e gli artefatti risultanti vengono archiviati.
1. Viene impostata la variabile `CM_DISABLE_BUILD_REUSE`.
1. La pipeline viene rieseguita senza modificare il codice. Anche se sono presenti artefatti archiviati associati a `becdddb`, non vengono riutilizzati per via della variabile `CM_DISABLE_BUILD_REUSE`.
1. Il codice viene modificato e la pipeline eseguita. Il commit HEAD ora è `f6ac5e6`. L’esecuzione ha esito positivo e gli artefatti risultanti vengono archiviati.
1. La variabile `CM_DISABLE_BUILD_REUSE` viene eliminata.
1. La pipeline viene rieseguita senza modificare il codice. Poiché sono presenti artefatti archiviati associati a `f6ac5e6`, questi artefatti vengono riutilizzati.

### Avvertenze {#caveats}

* Gli artefatti di generazione non vengono riutilizzati in diversi programmi, indipendentemente dal fatto che l’hash di commit sia identico.
* Gli artefatti di generazione vengono riutilizzati all’interno dello stesso programma anche se il ramo e/o la pipeline sono diversi.
* La [gestione delle versioni Maven](/help/implementing/cloud-manager/managing-code/project-version-handling.md) sostituisce la versione del progetto esclusivamente nelle pipeline di produzione. Pertanto, se si utilizza lo stesso commit su una pipeline di distribuzione nell’ambiente di sviluppo e su una pipeline di produzione e la prima viene eseguita per prima, le versioni verranno distribuite nell’ambiente di staging e produzione senza essere modificate. Tuttavia, anche in questo caso verrà creato un tag.
* Se il recupero degli artefatti archiviati non ha esito positivo, la fase di build viene eseguita come se non fossero stati archiviati artefatti.
* Le variabili di pipeline diverse da `CM_DISABLE_BUILD_REUSE` non vengono considerate quando Cloud Manager opta per riutilizzare gli artefatti di generazione creati in precedenza.
