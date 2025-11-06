---
title: Pacchetto per la struttura dell’archivio dei progetti AEM
description: I progetti Maven in Adobe Experience Manager as a Cloud Service richiedono una definizione di pacchetto secondario della struttura dell’archivio il cui unico scopo è quello di definire le directory principali dell’archivio JCR in cui vengono distribuiti i pacchetti secondari del codice del progetto.
exl-id: dec08410-d109-493d-bf9d-90e5556d18f0
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 2%

---

# Pacchetto per la struttura dell’archivio dei progetti AEM

I progetti Maven per Adobe Experience Manager as a Cloud Service richiedono una definizione di pacchetto secondario della struttura dell’archivio il cui unico scopo è quello di definire le directory principali dell’archivio JCR in cui vengono distribuiti i pacchetti secondari del codice del progetto. Questo metodo assicura che l’installazione dei pacchetti in Experience Manager as a Cloud Service venga ordinata automaticamente in base alle dipendenze delle risorse JCR. Le dipendenze mancanti possono portare a scenari in cui le sottostrutture verrebbero installate prima delle strutture padre e quindi rimosse in modo imprevisto, interrompendo la distribuzione.

Se il pacchetto di codice viene distribuito in una posizione **non coperta** dal pacchetto stesso, tutte le risorse precedenti (risorse JCR più vicine alla radice JCR) devono essere enumerate nel pacchetto della struttura dell&#39;archivio. Questo processo è necessario per stabilire tali dipendenze.

![Pacchetto struttura archivio](./assets/repository-structure-packages.png)

Il pacchetto della struttura dell&#39;archivio definisce lo stato comune previsto di `/apps` utilizzato dal modulo di convalida del pacchetto per determinare le aree &quot;al riparo da potenziali conflitti&quot; in quanto si tratta di directory principali standard.

I percorsi più tipici da includere nel pacchetto della struttura dell’archivio sono:

+ `/apps` che è un nodo fornito dal sistema
+ `/apps/cq/...`, `/apps/dam/...`, `/apps/wcm/...` e `/apps/sling/...` che forniscono sovrapposizioni comuni per `/libs`.
+ `/apps/settings` che è il percorso radice della configurazione in base al contesto condiviso

Il pacchetto secondario **non contiene** alcun contenuto ed è composto solo da `pom.xml` che definiscono le radici del filtro.

## Creazione del pacchetto della struttura dell’archivio

Per creare un pacchetto della struttura dell’archivio per il progetto Maven, crea un sottoprogetto Maven vuoto con il seguente `pom.xml`, aggiornando i metadati del progetto in modo che siano conformi al progetto Maven principale.

Aggiorna `<filters>` per includere tutti i percorsi radice dell&#39;archivio JCR nei pacchetti di codice distribuiti in.

Assicurarsi di aggiungere questo nuovo sottoprogetto Maven all&#39;elenco dei progetti principali `<modules>`.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/maven-v4_0_0.xsd">
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
                    <!-- Set Cloud Manager Target to none, else this package is deployed and remove all defined filter roots -->
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
                <configuration>
                    <properties>
                        <!-- Set Cloud Manager Target to none, else this package is deployed and remove all defined filter roots -->
                        <cloudManagerTarget>none</cloudManagerTarget>
                    </properties>
                    <filters>

                        <!-- /apps root -->
                        <filter><root>/apps</root></filter>

                        <!--
                        Examples of complex roots


                        Overlays of /libs typically require defining the overlay structure, at each level here.

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

Per utilizzare il pacchetto della struttura dell&#39;archivio, fare riferimento a esso tramite tutti i pacchetti di codice (i sottopacchetti che distribuiscono a `/apps`) progetti Maven tramite la configurazione del pacchetto di contenuti FileVault plug-in Maven `<repositoryStructurePackage>`.

In `ui.apps/pom.xml` e in qualsiasi altro pacchetto di codice `pom.xml`, aggiungere un riferimento alla configurazione del pacchetto di struttura dell&#39;archivio (#repository-structure-package) del progetto al plug-in Maven del pacchetto FileVault.

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

## Caso di utilizzo: pacchetto con più codici

Un caso d’uso meno comune e più complesso supporta la distribuzione di più pacchetti di codice che vengono installati nelle stesse aree dell’archivio JCR.

Ad esempio:

+ Il pacchetto di codice A viene distribuito in `/apps/a`
+ Il pacchetto di codice B viene distribuito in `/apps/a/b`

Se non viene stabilita una dipendenza a livello di pacchetto dal pacchetto di codice B nel pacchetto di codice A, il pacchetto di codice B può essere distribuito prima in `/apps/a`. Se viene seguito dal pacchetto di codice A, che viene distribuito in `/apps/a`, il risultato è la rimozione di `/apps/a/b` precedentemente installato.

In questo caso:

+ Il pacchetto di codice A deve definire un `<repositoryStructurePackage>` nel pacchetto della struttura dell&#39;archivio del progetto (che deve avere un filtro per `/apps`).
+ Il pacchetto di codice B deve definire un `<repositoryStructurePackage>` nel pacchetto di codice A, perché il pacchetto di codice B viene distribuito nello spazio condiviso dal pacchetto di codice A.

## Errori e debug

Se i pacchetti della struttura dell’archivio non sono configurati correttamente, alla build Maven viene segnalato un errore:

```
1 error(s) detected during dependency analysis.
Filter root's ancestor '/apps/some/path' is not covered by any of the specified dependencies.
```

Questo errore indica che il pacchetto del codice di interruzione non ha un `<repositoryStructurePackage>` che elenca `/apps/some/path` nel suo elenco di filtri.

## Risorse aggiuntive

+ [Plug-in Maven pacchetto contenuti FileVault](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
