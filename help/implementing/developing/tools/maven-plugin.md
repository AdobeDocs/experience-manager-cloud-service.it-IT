---
title: Plug-in  Adobe pacchetto contenuto
description: Utilizzate il plug-in Content Package Maven per distribuire AEM applicazioni
translation-type: tm+mt
source-git-commit: 2cdbbe9b8f6608cbdd299889be515d421e3d9ad3
workflow-type: tm+mt
source-wordcount: '1857'
ht-degree: 7%

---


# Plug-in  pacchetto di contenuti Adobe {#adobe-content-package-maven-plugin}

Utilizzate il plug-in  Adobe Content Package Maven per integrare le attività di distribuzione e gestione dei pacchetti nei vostri progetti Maven.

La distribuzione dei pacchetti costruiti da AEM viene eseguita dal plug-in  Content Package Maven del Adobe e consente l&#39;automazione delle attività normalmente eseguite tramite AEM Package Manager:

* Creare nuovi pacchetti da file nel file system.
* Installate e disinstallate i pacchetti in AEM.
* Creare pacchetti già definiti su AEM.
* Ottenete un elenco dei pacchetti installati in AEM.
* Rimuovete un pacchetto da AEM.

Questo documento descrive come utilizzare il Paradiso per gestire queste attività. Tuttavia è importante anche comprendere [come sono strutturati i progetti AEM e i relativi pacchetti.](#aem-project-structure)

>[!NOTE]
>
>La creazione del pacchetto è ora di proprietà del plug-in Maven pacchetto [Apache Jackrabbit FileVault](https://jackrabbit.apache.org/filevault-package-maven-plugin/). La distribuzione dei pacchetti costruiti da AEM viene eseguita dal plug-in  Content Package Maven, come descritto qui.

## Pacchetti e struttura AEM progetto {#aem-project-structure}

AEM 6.5 aderisce alle best practice più recenti per la gestione dei pacchetti e la struttura dei progetti, come implementato dall&#39;ultimo archivio dei progetti AEM sia per le implementazioni locali che per le implementazioni AMS.

>[!TIP]
>
>Per ulteriori dettagli, vedere l&#39;articolo [AEM Struttura del progetto](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) nella AEM come documentazione Cloud Service e la documentazione [AEM Project Archetype](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/archetype/overview.html). Entrambe sono completamente supportate per AEM 6.5.

## Come ottenere il plug-in Content Package Maven {#obtaining-the-content-package-maven-plugin}

Il plugin è disponibile dal [repository centrale di Maven.](https://mvnrepository.com/artifact/com.day.jcr.vault/content-package-maven-plugin?repo=adobe-public)

## Obiettivi e parametri del plug-in di Content Package Maven

Per utilizzare il plug-in Content Package Maven, aggiungete il seguente elemento plug-in all’interno dell’elemento build del file POM:

```xml
<plugin>
 <groupId>com.day.jcr.vault</groupId>
 <artifactId>content-package-maven-plugin</artifactId>
 <version>0.0.24</version>
 <configuration>
       <!-- parameters and values common to all goals, as required -->
 </configuration>
</plugin>
```

Per consentire a Maven di scaricare il plug-in, utilizzate il profilo fornito nella sezione [Acquisizione del plug-in di Content Package Maven](#obtaining-the-content-package-maven-plugin) in questa pagina.

## Obiettivi del plug-in Content Package Maven {#goals-of-the-content-package-maven-plugin}

Gli obiettivi e i parametri dell&#39;obiettivo forniti dal plug-in Content Package sono descritti nelle sezioni che seguono. I parametri descritti nella sezione Parametri comuni possono essere utilizzati per la maggior parte degli obiettivi. I parametri che si applicano a un obiettivo sono descritti nella sezione relativa a tale obiettivo.

### Prefisso plug-in {#plugin-prefix}

Il prefisso del plugin è `content-package`. Utilizzate questo prefisso per eseguire un obiettivo dalla riga di comando, come nell&#39;esempio seguente:

```shell
mvn content-package:build
```

### Prefisso parametro {#parameter-prefix}

Salvo diversa indicazione, gli obiettivi e i parametri del plugin usano il prefisso `vault`, come nell&#39;esempio seguente:

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

### Proxies {#proxies}

Obiettivi che utilizzano i proxy per AEM utilizzano la prima configurazione proxy valida trovata nelle impostazioni Maven. Se non viene trovata alcuna configurazione proxy, non viene utilizzato alcun proxy. Vedere il parametro `useProxy` nella sezione [Parametri comuni](#common-parameters).

### Parametri comuni {#common-parameters}

I parametri nella tabella seguente sono comuni a tutti gli obiettivi, tranne se indicati nella colonna **Obiettivi**.

| Nome | Tipo | Obbligatorio | Valore predefinito | Descrizione | Obiettivi |
|---|---|---|---|---|---|
| `failOnError` | `boolean` | No | `false` | Un valore di `true` causa il fallimento della build quando si verifica un errore. Un valore di `false` fa sì che la build ignori l&#39;errore. | Tutti gli obiettivi eccetto `package` |
| `name` | `String` | `build`: Sì,  `install`: No,  `rm`: Yes | `build`: Nessuna impostazione predefinita,  `install`: Il valore della  `artifactId` proprietà del progetto Maven | Nome del pacchetto su cui agire | Tutti gli obiettivi eccetto `ls` |
| `password` | `String` | Sì | `admin` | La password utilizzata per l&#39;autenticazione con AEM | Tutti gli obiettivi eccetto `package` |
| `serverId` | `String` | No | L&#39;ID server da cui recuperare il nome utente e la password per l&#39;autenticazione | Tutti gli obiettivi eccetto `package` |
| `targetURL` | `String` | Sì | `http://localhost:4502/crx/packmgr/service.jsp` | L&#39;URL dell&#39;API del servizio HTTP del gestore pacchetti AEM | Tutti gli obiettivi eccetto `package` |
| `timeout` | `int` | No | `5` | Timeout di connessione per la comunicazione con il servizio di gestione pacchetti, in secondi | Tutti gli obiettivi eccetto `package` |
| `useProxy` | `boolean` | No | `true` | Un valore di `true` fa in modo che Maven utilizzi la prima configurazione proxy attiva trovata per le richieste di proxy al Gestore pacchetti. | Tutti gli obiettivi eccetto `package` |
| `userId` | `String` | Sì | `admin` | Nome utente con cui autenticare AEM | Tutti gli obiettivi eccetto `package` |
| `verbose` | `boolean` | No | `false` | Abilita o disabilita la registrazione dettagliata | Tutti gli obiettivi eccetto `package` |

### build {#build}

Crea un pacchetto di contenuti già definito in un&#39;istanza AEM.

>[!NOTE]
>
>Questo obiettivo non deve essere eseguito all&#39;interno di un progetto Maven.

#### Parametri {#parameters}

Tutti i parametri per l&#39;obiettivo di compilazione sono descritti nella sezione [Parametri comuni](#common-parameters).

### install {#install}

Installa un pacchetto nella directory archivio. L&#39;esecuzione di questo obiettivo non richiede un progetto Maven. L&#39;obiettivo è legato alla fase `install` del ciclo di vita della build Maven.

#### Parametri {#parameters-1}

Oltre ai seguenti parametri, vedere le descrizioni nella sezione [Parametri comuni](#common-parameters).

| Nome | Tipo | Obbligatorio | Valore predefinito | Descrizione |
|---|---|---|---|---|---|
| `artifact` | `String` | No | Il valore della proprietà `artifactId` del progetto Maven | Una stringa del modulo `groupId:artifactId:version[:packaging]` |
| `artifactId` | `String` | No | Nessuno | ID dell&#39;artifact da installare |
| `groupId` | `String` | No | Nessuno | `groupId` dell&#39;artifact da installare |
| `install` | `boolean` | No | `true` | Determina se rimuovere automaticamente il pacchetto al momento del caricamento |
| `localRepository` | `org.apache.maven.artifact.repository.ArtifactRepository` | No | Il valore della variabile di sistema `localRepository` | Il repository locale Maven che non può essere configurato utilizzando la configurazione del plug-in come proprietà di sistema viene sempre utilizzato |
| `packageFile` | `java.io.File` | No | Il manufatto principale definito per il progetto Maven | Nome del file del pacchetto da installare |
| `packaging` | `String` | No | `zip` | Tipo di imballaggio dell&#39;artefatto da installare |
| `pomRemoteRepositories` | `java.util.List` | Sì | Il valore della proprietà `remoteArtifactRepositories` definita per il progetto Maven | Questo valore non può essere configurato con la configurazione del plug-in e deve essere specificato nel progetto. |
| `project` | `org.apache.maven.project.MavenProject` | Sì | Progetto per il quale è configurato il plug-in | Il progetto Maven che è implicito perché il progetto contiene la configurazione del plugin |
| `repositoryId` (POM),  `repoID` (riga di comando) | `String` | No | `temp` | ID del repository da cui viene recuperato l&#39;artifact |
| `repositoryUrl` (POM),  `repoURL` (riga di comando) | `String` | No | Nessuno | URL del repository da cui viene recuperato l&#39;artifact |
| version | Stringa | No | Nessuno | Versione dell&#39;artifact da installare |

### ls {#ls}

Elenca i pacchetti distribuiti in Gestione pacchetti.

#### Parametri {#parameters-2}

Tutti i parametri dell&#39;obiettivo ls sono descritti nella sezione [Parametri comuni](#common-parameters).

### rm {#rm}

Rimuove un pacchetto da Gestione pacchetti.

#### Parametri {#parameters-3}

Tutti i parametri dell&#39;obiettivo rm sono descritti nella sezione [Parametri comuni](#common-parameters).

### disinstallazione {#uninstall}

Disinstalla un pacchetto. Il pacchetto rimane sul server nello stato disinstallato.

#### Parametri {#parameters-4}

Tutti i parametri dell&#39;obiettivo di disinstallazione sono descritti nella sezione [Parametri comuni](#common-parameters).

### pacchetto {#package}

Crea un pacchetto di contenuti. La configurazione predefinita dell&#39;obiettivo del pacchetto include il contenuto della directory in cui vengono salvati i file compilati. L&#39;esecuzione dell&#39;obiettivo del pacchetto richiede il completamento della fase di compilazione. L&#39;obiettivo del pacchetto è legato alla fase del pacchetto del ciclo di vita della build Maven.

#### Parametri {#parameters-5}

Oltre ai seguenti parametri, vedere la descrizione del parametro `name` nella sezione [Parametri comuni](#common-parameters).

| Nome | Tipo | Obbligatorio | Valore predefinito | Descrizione |
|---|---|---|---|---|
| `archive` | `org.apache.maven.archiver.MavenArchiveConfiguration` | No | Nessuno | Configurazione dell&#39;archivio da utilizzare |
| `builtContentDirectory` | `java.io.File` | Sì | Il valore della directory di output della build Maven | La directory che contiene il contenuto da includere nel pacchetto |
| `dependencies` | `java.util.List` | No | Nessuno |  |
| `embeddedTarget` | `java.lang.String` | No | Nessuno |  |
| `embeddeds` | `java.util.List` | No | Nessuno |  |
| `failOnMissingEmbed` | `boolean` | Sì | `false` | Un valore di `true` causa la mancata riuscita della build quando un artifact incorporato non viene trovato nelle dipendenze del progetto. Un valore di `false` fa sì che la build ignori tali errori. |
| `filterSource` | `java.io.File` | No | Nessuno | Questo parametro definisce un file che specifica l’origine del filtro dell’area di lavoro. I filtri specificati nella configurazione e iniettati tramite incorporamenti o pacchetti secondari vengono uniti con il contenuto del file. |
| `filters` | `com.day.jcr.vault.maven.pack.impl.DefaultWorkspaceFilter` | No | Nessuno | Questo parametro contiene elementi di filtro che definiscono il contenuto del pacchetto. Una volta eseguiti, i filtri vengono inclusi nel file `filter.xml`. Vedere la sezione [Utilizzo dei filtri](#using-filters) di seguito. |
| `finalName` | `java.lang.String` | Sì | La `finalName` definita nel progetto Maven (fase di costruzione) | Il nome del file ZIP del pacchetto generato, senza l&#39;estensione del file `.zip` |
| `group` | `java.lang.String` | Sì | La `groupID` definita nel progetto Maven | La `groupId` del pacchetto di contenuto generato che fa parte del percorso di installazione di destinazione per il pacchetto di contenuto |
| `outputDirectory` | `java.io.File` | Sì | La directory di compilazione definita nel progetto Maven | La directory locale in cui viene salvato il pacchetto di contenuto |
| `prefix` | `java.lang.String` | No | Nessuno |  |
| `project` | `org.apache.maven.project.MavenProject` | Sì | Nessuno | Il progetto Maven |
| `properties` | `java.util.Map` | No | Nessuno | Questi parametri definiscono proprietà aggiuntive che è possibile impostare nel file `properties.xml`. Queste proprietà non possono sovrascrivere le seguenti proprietà predefinite: `group` (utilizzare il parametro `group` per impostare), `name` (utilizzare il parametro `name` per impostare), `version` (utilizzare il parametro `version` per impostare), `description` (impostato dalla descrizione del progetto), `groupId` (`groupId` del descrittore del progetto Maven), `artifactId` (`artifactId` descrittore di progetto Maven), `dependencies` (utilizzare il parametro `dependencies` per impostare), `createdBy` (il valore della proprietà di sistema `user.name`), `created` (l&#39;ora corrente del sistema), `requiresRoot` (utilizzare il parametro `requiresRoot` per impostare), `packagePath` (generato automaticamente dal nome del gruppo e del pacchetto) |
| `requiresRoot` | `boolean` | Sì | false | Definisce se il pacchetto richiede root. Questo diventerà la proprietà `requiresRoot` del file `properties.xml`. |
| `subPackages` | `java.util.List` | No | Nessuno |  |
| `version` | `java.lang.String` | Sì | La versione definita nel progetto Maven | Versione del pacchetto di contenuti |
| `workDirectory` | `java.io.File` | Sì | Directory definita nel progetto Maven (fase di costruzione) | La directory che contiene il contenuto da includere nel pacchetto |

#### Utilizzo dei filtri {#using-filters}

Utilizzate l&#39;elemento filter per definire il contenuto del pacchetto. I filtri vengono aggiunti all&#39;elemento `workspaceFilter` nel file `META-INF/vault/filter.xml` del pacchetto.

L&#39;esempio di filtro seguente mostra la struttura XML da utilizzare:

```xml
<filter>
   <root>/apps/myapp</root>
   <mode>merge</mode>
       <includes>
              <include>/apps/myapp/install/</include>
              <include>/apps/myapp/components</include>
       </includes>
       <excludes>
              <exclude>/apps/myapp/config/*</exclude>
       </excludes>
</filter>
```

##### Modalità di importazione {#import-mode}

L&#39;elemento `mode` definisce in che modo il contenuto viene influenzato dalla directory archivio quando viene importato il pacchetto. È possibile utilizzare i seguenti valori:

* **Unisci: viene aggiunto** il contenuto del pacchetto che non è già presente nella directory archivio. Il contenuto presente sia nel pacchetto che nell&#39;archivio rimane invariato. Nessun contenuto viene rimosso dalla directory archivio.
* **Sostituisci:** il contenuto del pacchetto che non si trova nella directory archivio viene aggiunto alla directory archivio. Il contenuto del repository viene sostituito con il contenuto corrispondente presente nel pacchetto. Il contenuto viene rimosso dalla directory archivio quando non esiste nel pacchetto.
* **Aggiornamento:** il contenuto del pacchetto che non si trova nella directory archivio viene aggiunto alla directory archivio. Il contenuto del repository viene sostituito con il contenuto corrispondente presente nel pacchetto. Il contenuto esistente viene rimosso dalla directory archivio.

Se il filtro non contiene alcun elemento `mode`, viene utilizzato il valore predefinito di `replace`.

### aiuto {#help}

#### Parametri {#parameters-6}

| Nome | Tipo | Obbligatorio | Valore predefinito | Descrizione |
|---|---|---|---|---|
| `detail` | `boolean` | No | `false` | Determina se visualizzare tutte le proprietà impostabili per ciascun obiettivo |
| `goal` | `String` | No | Nessuno | Questi parametri definiscono il nome dell&#39;obiettivo per il quale visualizzare la guida. Se non viene specificato alcun valore, viene visualizzata la guida per tutti gli obiettivi. |
| `indentSize` | `int` | No | `2` | Il numero di spazi da utilizzare per il rientro di ciascun livello (deve essere positivo se definito) |
| `lineLength` | `int` | No | `80` | La lunghezza massima di una linea di visualizzazione (deve essere positiva se definita) |

## Inclusione di un&#39;immagine miniatura o di un file di proprietà nel pacchetto {#including-a-thumbnail-image-or-properties-file-in-the-package}

Sostituite i file di configurazione del pacchetto predefiniti per personalizzare le proprietà del pacchetto. Ad esempio, includete una miniatura per distinguere il pacchetto in Gestione pacchetti e Condivisione pacchetti.

I file sorgente possono trovarsi ovunque nel file system. Nel file POM, definite le risorse di build per copiare i file sorgente in `target/vault-work/META-INF` per l&#39;inclusione nel pacchetto.

Il seguente codice POM aggiunge al pacchetto i file presenti nella cartella `META-INF` dell’origine del progetto:

```xml
<build>
    <resources>
        <!-- vault META-INF resources (thumbnail etc.) -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF</directory>
            <targetPath>../vault-work/META-INF</targetPath>
        </resource>
    </resources>
</build>
```

Il seguente codice POM aggiunge al pacchetto solo una miniatura. L&#39;immagine in miniatura deve essere denominata `thumbnail.png` e deve trovarsi nella cartella `META-INF/vault/definition` del pacchetto. In questo esempio, il file di origine si trova nella cartella `/src/main/content/META-INF/vault/definition` del progetto:

```xml
<build>
    <resources>
        <!-- thumbnail only -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF/vault/definition</directory>
            <targetPath>../vault-work/META-INF/vault/definition</targetPath>
        </resource>
    </resources>
</build>
```

## Utilizzo del tipo di archivio AEM progetto per generare AEM progetti {#using-archetypes}

L&#39;ultimo AEM Project Archetype implementa la struttura del pacchetto best practice sia per le implementazioni locali che per le implementazioni AMS ed è consigliato per tutti AEM progetti.

>[!TIP]
>
>Per ulteriori dettagli, vedere l&#39;articolo [AEM Struttura del progetto](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) nella AEM come documentazione Cloud Service e la documentazione [AEM Project Archetype](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/overview.html). Entrambe sono completamente supportate per AEM 6.5.
