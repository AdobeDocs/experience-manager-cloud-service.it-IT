---
title: 'Pacchetto per la struttura dell’archivio dei progetti AEM  '
description: I progetti Adobe Experience Manager as a Cloud Service Maven richiedono una definizione di sottopacchetto con struttura dell’archivio il cui unico scopo è quello di definire le radici dell’archivio JCR in cui vengono distribuiti i pacchetti secondari del codice del progetto.
exl-id: dec08410-d109-493d-bf9d-90e5556d18f0
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 9%

---

# Pacchetto per la struttura dell’archivio dei progetti AEM

I progetti Maven per Adobe Experience Manager as a Cloud Service richiedono una definizione di pacchetto secondario della struttura dell’archivio il cui unico scopo è quello di definire le radici dell’archivio JCR in cui vengono distribuiti i pacchetti secondari del codice del progetto. In questo modo l’installazione dei pacchetti in Experience Manager as a Cloud Service viene ordinata automaticamente dalle dipendenze delle risorse JCR. Le dipendenze mancanti possono portare a scenari in cui le sottostrutture sarebbero installate prima delle loro strutture padre e quindi rimosse inaspettatamente, interrompendo la distribuzione.

Se il pacchetto di codice viene distribuito in una posizione **non inclusa** nel pacchetto stesso, tutte le risorse precedenti (risorse JCR più vicine alla radice JCR) devono essere enumerate nel pacchetto della struttura dell’archivio per stabilire tali dipendenze.

![Pacchetto struttura archivio](./assets/repository-structure-packages.png)

Il pacchetto della struttura dell&#39;archivio definisce lo stato comune previsto di `/apps` che il validatore del pacchetto utilizza per determinare le aree &quot;sicure da potenziali conflitti&quot; in quanto sono radici standard.

I percorsi più tipici da includere nel pacchetto della struttura dell&#39;archivio sono:

+ `/apps` che è un nodo fornito dal sistema
+ `/apps/cq/...`, `/apps/dam/...`, `/apps/wcm/...`e `/apps/sling/...` che forniscono sovrapposizioni comuni `/libs`.
+ `/apps/settings` che è il percorso principale della configurazione in base al contesto condiviso

Tieni presente che questo pacchetto secondario **non ha** qualsiasi contenuto ed è costituito unicamente da un `pom.xml` definizione delle radici del filtro.

## Creazione del pacchetto della struttura dell’archivio

Per creare un pacchetto della struttura dell’archivio per il progetto Maven, crea un nuovo sottoprogetto Maven vuoto con le seguenti opzioni `pom.xml`, aggiornamento dei metadati del progetto per adattarli al progetto Maven principale.

Aggiorna `<filters>` per includere tutte le directory del percorso dell&#39;archivio JCR che i pacchetti di codice distribuiscono in.

Aggiungi questo nuovo sottoprogetto Maven ai progetti padre `<modules>` elenco.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <!-- ====================================================================== -->
    <!-- P A R E N T  P R O J E C T  D E S C R I P T I O N                      -->
    <!-- ====================================================================== -->
    <parent>
        <groupId>com.my-company</groupId>
        <artifactId>my-app</artifactId>
        <version>x.x.x</version>
        <relativePath>../pom.xml</relativePath>
    </parent>

    <!-- ====================================================================== -->
    <!-- P R O J E C T  D E S C R I P T I O N                                   -->
    <!-- ====================================================================== -->
    <artifactId>ui.apps.structure</artifactId>
    <packaging>content-package</packaging>
    <name>UI Apps Structure - Repository Structure Package for /apps</name>

    <description>
        Empty package that defines the structure of the Adobe Experience Manager repository the code packages in this project deploy into.
        Any roots in the code packages of this project should have their parent enumerated in the filters list below.
    </description>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.jackrabbit</groupId>
                <artifactId>filevault-package-maven-plugin</artifactId>
                <extensions>true</extensions>
                <properties>
                    <!-- Set Cloud Manager Target to none, else this package will be deployed and remove all defined filter roots -->
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
                <configuration>
                    <properties>
                        <!-- Set Cloud Manager Target to none, else this package will be deployed and remove all defined filter roots -->
                        <cloudManagerTarget>none</cloudManagerTarget>
                    </properties>
                    <filters>

                        <!-- /apps root -->
                        <filter><root>/apps</root></filter>

                        <!--
                        Examples of complex roots


                        Overlays of /libs typically require defining the overlayed structure, at each level here.

                        For example, adding a new section to the main AEM Tools navigation, necessitates the following rules:

                        <filter><root>/apps/cq</root></filter>
                        <filter><root>/apps/cq/core</root></filter>
                        <filter><root>/apps/cq/core/content</root></filter>
                        <filter><root>/apps/cq/core/content/nav/</root></filter>
                        <filter><root>/apps/cq/core/content/nav/tools</root></filter>


                        Any /apps level Context-aware configurations need to enumerated here. 
                        
                        For example, providing email templates under `/apps/settings/notification-templates/com.day.cq.replication` necessitates the following rules:

                        <filter><root>/apps/settings</root></filter>
                        <filter><root>/apps/settings/notification-templates</root></filter>
                        <filter><root>/apps/settings/notification-templates/com.day.cq.replication</root></filter>
                        -->

                    </filters>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

## Riferimento al pacchetto della struttura dell’archivio

Per utilizzare il pacchetto della struttura dell&#39;archivio, fai riferimento a esso tramite tutti i pacchetti di codice (i pacchetti secondari che si distribuiscono per `/apps`) Progetti Maven tramite il pacchetto di contenuti FileVault Maven plug-in `<repositoryStructurePackage>` configurazione.

In `ui.apps/pom.xml`e qualsiasi altro pacchetto di codice `pom.xml`s, aggiungi un riferimento alla configurazione del pacchetto della struttura dell&#39;archivio del progetto (#repository-structure-package) al plug-in Maven del pacchetto FileVault.

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        ...
        <repositoryStructurePackages>
          <repositoryStructurePackage>
              <groupId>${project.groupId}</groupId>
              <artifactId>ui.apps.structure</artifactId>
              <version>${project.version}</version>
          </repositoryStructurePackage>
        </repositoryStructurePackages>
      </configuration>
    </plugin>
    ...
</build>
<dependencies>
    <!-- Add the dependency for the repository structure package so it resolves -->
    <dependency>
        <groupId>${project.groupId}</groupId>
        <artifactId>ui.apps.structure</artifactId>
        <version>${project.version}</version>
        <type>zip</type>
    </dependency>
    ...
</dependencies>
```

## Caso di utilizzo di pacchetti multicodice

Un caso d’uso meno comune e più complesso supporta la distribuzione di più pacchetti di codice che si installano nelle stesse aree dell’archivio JCR.

Ad esempio:

+ Il pacchetto di codice A viene distribuito in `/apps/a`
+ Il pacchetto di codice B viene distribuito in `/apps/a/b`

Se una dipendenza a livello di pacchetto non è stabilita dal pacchetto di codice B sul pacchetto di codice A, il pacchetto di codice B può essere distribuito prima in `/apps/a`, seguito dal pacchetto di codice B, che distribuisce in `/apps/a`, con conseguente rimozione dell&#39;installazione precedente `/apps/a/b`.

In questo caso:

+ Il pacchetto di codice A deve definire un `<repositoryStructurePackage>` sul pacchetto della struttura dell’archivio del progetto (che deve avere un filtro per `/apps`).
+ Il pacchetto di codice B deve definire un `<repositoryStructurePackage>` sul pacchetto di codice A, perché il pacchetto di codice B viene distribuito nello spazio condiviso dal pacchetto di codice A.

## Errori e debug

Se i pacchetti della struttura dell&#39;archivio non sono configurati correttamente, in Maven verrà segnalato un errore:

```
1 error(s) detected during dependency analysis.
Filter root's ancestor '/apps/some/path' is not covered by any of the specified dependencies.
```

Questo indica che il pacchetto di codice di interruzione non ha un `<repositoryStructurePackage>` elenchi `/apps/some/path` nell’elenco dei filtri.

## Risorse aggiuntive

+ [Plug-in Maven pacchetto di contenuti FileVault](http://jackrabbit.apache.org/filevault-package-maven-plugin/)
