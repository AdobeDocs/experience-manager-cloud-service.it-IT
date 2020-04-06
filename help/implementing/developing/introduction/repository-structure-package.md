---
title: 'Sviluppare un pacchetto con la struttura dell’archivio   '
description: Adobe Experience Manager come progetto Cloud Service Maven richiede una definizione del sottopacchetto della struttura dell'archivio il cui unico scopo è definire le radici dell'archivio JCR in cui vengono distribuiti i sottopacchetti Codice del progetto.
translation-type: tm+mt
source-git-commit: 46d556fdf28267a08e5021f613fbbea75872ef21

---


# Sviluppare un pacchetto con la struttura dell’archivio

I progetti Maven per Adobe Experience Manager come servizio Cloud richiedono una definizione di sottopacchetto della struttura del repository il cui unico scopo è definire le radici del repository JCR in cui vengono distribuiti i sottopacchetti di codice del progetto. In questo modo, l&#39;installazione dei pacchetti in Experience Manager come servizio Cloud viene ordinata automaticamente dalle dipendenze delle risorse JCR. Le dipendenze mancanti potrebbero causare l&#39;installazione di sottostrutture in anticipo rispetto alle strutture padre e, di conseguenza, la rimozione imprevista, interrompendo la distribuzione.

Se il pacchetto di codice viene distribuito in una posizione **non inclusa** nel pacchetto stesso, tutte le risorse precedenti (risorse JCR più vicine alla radice JCR) devono essere enumerate nel pacchetto della struttura dell’archivio per stabilire tali dipendenze.

![Pacchetto struttura archivio](./assets/repository-structure-packages.png)

Il pacchetto della struttura dell&#39;archivio definisce lo stato comune previsto per `/apps` il quale il validatore del pacchetto utilizza per determinare le aree &quot;sicure da potenziali conflitti&quot; in quanto sono radici standard.

I percorsi più comuni da includere nel pacchetto della struttura del repository sono:

+ `/apps` che è un nodo fornito dal sistema
+ `/apps/cq/...`, `/apps/dam/...`, `/apps/wcm/...`e `/apps/sling/...` che forniscono sovrapposizioni comuni per `/libs`.
+ `/apps/settings` che è il percorso principale di configurazione basato sul contesto condiviso

Tenete presente che questo sottopacchetto **non contiene** alcun contenuto ed è composto esclusivamente da una `pom.xml` definizione delle radici del filtro.

## Creazione del pacchetto struttura archivio

Per creare un pacchetto di struttura del repository per il progetto Maven, create un nuovo progetto secondario Maven vuoto, con quanto segue, `pom.xml`aggiornando i metadati del progetto in modo che siano conformi al progetto Maven principale.

Aggiornate il file `<filters>` in modo da includere tutte le directory del percorso del repository JCR, ovvero le directory di origine distribuite dai pacchetti di codice.

Accertatevi di aggiungere il nuovo sottoprogetto Maven all&#39;elenco dei progetti padre `<modules>` .

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
    <artifactId>my-app.repository-structure</artifactId>
    <packaging>content-package</packaging>
    <name>My App - Adobe Experience Manager Repository Structure Package</name>

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
                <configuration>
                    <properties>
                        <!-- Set Cloud Manager Target to none, else this package will be deployed and remove all defined filter roots -->
                        <cloudManagerTarget>none</cloudManagerTarget>
                    </properties>
                    <filters>

                        <!-- /apps root -->
                        <filter><root>/apps</root></filter>

                        <!-- Common overlay roots -->
                        <filter><root>/apps/sling</root></filter>
                        <filter><root>/apps/cq</root></filter>
                        <filter><root>/apps/dam</root></filter>
                        <filter><root>/apps/wcm</root></filter>

                        <!-- Immutable context-aware configurations -->
                        <filter><root>/apps/settings</root></filter>

                    </filters>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

## Riferimento al pacchetto della struttura dell&#39;archivio

Per utilizzare il pacchetto della struttura del repository, farvi riferimento tramite tutti i pacchetti di codice (i pacchetti secondari che distribuiscono a `/apps`) progetti Maven tramite la configurazione dei plug-in Maven del pacchetto di contenuti FileVault `<repositoryStructurePackage>` .

Nei pacchetti `ui.apps/pom.xml`e altri pacchetti `pom.xml`di codice, aggiungete un riferimento alla configurazione della struttura del repository del progetto (#repository-structure-package) al plug-in Maven del pacchetto FileVault.

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
              <artifactId>my-app.repository-structure</artifactId>
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
        <artifactId>my-app.repository-structure</artifactId>
        <version>${project.version}</version>
        <type>zip</type>
    </dependency>
    ...
</dependencies>
```

## Caso di utilizzo per più codici

Un caso d’uso meno comune e più complesso supporta la distribuzione di più pacchetti di codice che si installano nelle stesse aree dell’archivio JCR.

Esempio:

+ Il pacchetto di codice A si distribuisce in `/apps/a`
+ Il pacchetto di codice B si distribuisce in `/apps/a/b`

Se una dipendenza a livello di pacchetto non viene stabilita dal pacchetto di codice B nel pacchetto di codice A, il pacchetto di codice B può essere implementato prima in `/apps/a`, seguito dal pacchetto di codice B, che si distribuisce in `/apps/a`, con conseguente rimozione dell&#39;installazione precedente `/apps/a/b`.

In questo caso:

+ Il pacchetto di codice A deve definire un pacchetto `<repositoryStructurePackage>` `/apps`sulla struttura del repository del progetto (per il quale deve essere presente un filtro).
+ Il pacchetto di codice B deve definire un pacchetto `<repositoryStructurePackage>` di codice A, perché il pacchetto di codice B viene distribuito nello spazio condiviso dal pacchetto di codice A.

## Errori e debug

Se i pacchetti della struttura dell&#39;archivio non sono configurati correttamente, in Maven build verrà segnalato un errore:

```
1 error(s) detected during dependency analysis.
Filter root's ancestor '/apps/some/path' is not covered by any of the specified dependencies.
```

Indica che il pacchetto di codice di interruzione non dispone di un `<repositoryStructurePackage>` elenco `/apps/some/path` nel relativo elenco di filtri.

## Risorse aggiuntive

+ [FileVault Content Package Maven Plug-in](http://jackrabbit.apache.org/filevault-package-maven-plugin/)
