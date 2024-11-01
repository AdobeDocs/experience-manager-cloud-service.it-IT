---
title: Ambiente di build di Cloud Manager
description: Scopri l’ambiente di build di Cloud Manager e come genera e verifica il codice.
exl-id: a4e19c59-ef2c-4683-a1be-3ec6c0d2f435
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f5f7830ac6d7f5b65203b12bb1775e64379c7d14
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 58%

---


# Ambiente di build {#build-environment}

Scopri l’ambiente di build di Cloud Manager e come genera e verifica il codice.

## Dettagli dell’ambiente di build {#build-environment-details}

Cloud Manager genera e verifica il codice mediante un ambiente di build specializzato.

* L’ambiente di build è basato su Linux, derivato da Ubuntu 22.04.
* Apache Maven 3.9.4 è installato.
   * Adobe consiglia agli utenti di [aggiornare i loro archivi Maven per utilizzare HTTPS invece di HTTP](#https-maven).
* Le versioni Java installate sono Oracle JDK 11.0.22 e Oracle JDK 8u401.
* **IMPORTANTE**: per impostazione predefinita, la variabile di ambiente `JAVA_HOME` è impostata su `/usr/lib/jvm/jdk1.8.0_401`, che contiene Oracle JDK 8u401. *_Questa impostazione predefinita deve essere sostituita per i progetti AEM Cloud che utilizzano JDK 11_*. Per ulteriori dettagli, consulta la sezione [Impostazione della versione JDK di Maven](#alternate-maven-jdk-version).
* È necessario installare anche alcuni pacchetti di sistema aggiuntivi.
   * `bzip2`
   * `unzip`
   * `libpng`
   * `imagemagick`
   * `graphicsmagick`
* Altri pacchetti possono essere installati in fase di build come descritto nella sezione [Installazione di pacchetti di sistema aggiuntivi](#installing-additional-system-packages).
* Ogni build viene eseguita in un ambiente pulito, con il contenitore di build che non mantiene alcuno stato tra le esecuzioni.
* Maven viene sempre eseguito con i tre comandi riportati di seguito.
   * `mvn --batch-mode org.apache.maven.plugins:maven-dependency-plugin:3.1.2:resolve-plugins`
   * `mvn --batch-mode org.apache.maven.plugins:maven-clean-plugin:3.1.0:clean -Dmaven.clean.failOnError=false`
   * `mvn --batch-mode org.jacoco:jacoco-maven-plugin:prepare-agent package`
* Maven è configurato a livello di sistema con un file `settings.xml`, che include automaticamente l’archivio di artefatti pubblico di Adobe utilizzando un profilo denominato `adobe-public`. Per ulteriori informazioni, consulta [Archivio Maven pubblico di Adobe](https://repo1.maven.org/).

>[!NOTE]
>
>Sebbene Cloud Manager non definisca una versione specifica del `jacoco-maven-plugin`, la versione utilizzata deve essere `0.7.5.201505241946` o superiore.

## Archivi Maven HTTPS {#https-maven}

Cloud Manager [versione 2023.10.0](/help/implementing/cloud-manager/release-notes/2023/2023-10-0.md) ha iniziato un aggiornamento continuo dell’ambiente di build (completandolo con la versione 2023.12.0), che includeva un aggiornamento a Maven 3.8.8. Come modifica significativa introdotta in Maven 3.8.1 è stato apportato un miglioramento della sicurezza volto a mitigare potenziali vulnerabilità. In particolare, Maven ora disabilita tutte le corrispondenze `http://*` non sicure per impostazione predefinita, come descritto nelle [note sulla versione di Maven](https://maven.apache.org/docs/3.8.1/release-notes.html#cve-2021-26291).

Come risultato di questo miglioramento sulla sicurezza, alcuni utenti potrebbero riscontrare problemi durante la fase di build, in particolare durante il download di artefatti dagli archivi Maven che utilizzano connessioni HTTP non sicure.

Per garantire un’esperienza fluida con la versione aggiornata, Adobe consiglia agli utenti di aggiornare gli archivi Maven per utilizzare HTTPS invece di HTTP. Questo adeguamento è in linea con la crescente tendenza del settore verso protocolli di comunicazione sicuri e contribuisce a mantenere un processo di creazione sicuro e affidabile.

### Utilizza una versione Java specifica {#using-java-support}

Per impostazione predefinita, il processo di compilazione Cloud Manager utilizza il JDK Oracle 8 per generare i progetti, ma i clienti AEM Cloud Service devono impostare la versione JDK di esecuzione Maven su `11`.

#### Impostare la versione JDK di Maven {#alternate-maven-jdk-version}

Adobe consiglia di impostare la versione JDK per l’intera esecuzione Maven su `11` in un file `.cloudmanager/java-version`.

A questo scopo, crea un file denominato `.cloudmanager/java-version` nel ramo dell’archivio Git utilizzato dalla pipeline. Modificare il file in modo che contenga solo il testo, `11`. Anche se Cloud Manager accetta il valore `8`, questa versione non è più supportata per i progetti AEM Cloud Service. Qualsiasi altro valore viene ignorato. Quando si specifica `11`, viene utilizzato l&#39;Oracle 11 e la variabile di ambiente `JAVA_HOME` è impostata su `/usr/lib/jvm/jdk-11.0.22`.

## Variabili di ambiente - standard {#environment-variables}

Potrebbe essere necessario variare il processo di build in base alle informazioni sul programma o sulla pipeline.

Ad esempio, se la minimizzazione di JavaScript si verifica in fase di build utilizzando uno strumento come gulp, è possibile preferire diversi livelli di minimizzazione per vari ambienti. Una build di sviluppo potrebbe utilizzare un livello di minimizzazione più leggero rispetto alla staging e alla produzione.

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

## Variabili di ambiente - pipeline {#pipeline-variables}

Il processo di build potrebbe richiedere variabili di configurazione specifiche che non devono essere memorizzate nell’archivio Git. Inoltre, potrebbe essere necessario regolare queste variabili tra le esecuzioni della pipeline che utilizzano lo stesso ramo.

Per ulteriori informazioni, vedi anche [Configurare le variabili di pipeline](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md).

## Installare pacchetti di sistema aggiuntivi {#installing-additional-system-packages}

Alcune build richiedono pacchetti di sistema aggiuntivi per funzionare completamente. Ad esempio, una build può richiamare uno script Python o Ruby e deve disporre di un interprete del linguaggio appropriato installato. È possibile gestire questo processo di installazione chiamando [`exec-maven-plugin`](https://www.mojohaus.org/exec-maven-plugin/) in `pom.xml` per richiamare APT. Questa esecuzione deve generalmente essere integrata in un profilo Maven specifico per Cloud Manager. In questo esempio viene installato Python.

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
>Per informazioni dettagliate sull’ambiente di creazione front-end, consulta il documento [Sviluppo di siti con la pipeline front-end](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md).
