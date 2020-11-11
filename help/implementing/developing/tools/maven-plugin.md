---
title: Plug-in  Adobe pacchetto contenuto
description: Utilizzate il plug-in Content Package Maven per distribuire AEM applicazioni
translation-type: tm+mt
source-git-commit: 2cdbbe9b8f6608cbdd299889be515d421e3d9ad3
workflow-type: tm+mt
source-wordcount: '1857'
ht-degree: 7%

---


# Plug-in  Adobe pacchetto contenuto {#adobe-content-package-maven-plugin}

Utilizzate il plug-in  Adobe Content Package Maven per integrare le attività di distribuzione e gestione dei pacchetti nei vostri progetti Maven.

La distribuzione dei pacchetti costruiti da AEM viene eseguita dal plug-in  Content Package Maven del Adobe e consente l&#39;automazione delle attività normalmente eseguite tramite AEM Package Manager:

* Creare nuovi pacchetti da file nel file system.
* Installate e disinstallate i pacchetti in AEM.
* Creare pacchetti già definiti su AEM.
* Ottenete un elenco dei pacchetti installati in AEM.
* Rimuovete un pacchetto da AEM.

Questo documento descrive come utilizzare il Paradiso per gestire queste attività. Tuttavia è importante anche comprendere [come sono strutturati AEM progetti e i loro pacchetti.](#aem-project-structure)

>[!NOTE]
>
>La creazione del pacchetto è ora di proprietà del plug-in [Maven pacchetto](https://jackrabbit.apache.org/filevault-package-maven-plugin/)Apache Jackrabbit FileVault. La distribuzione dei pacchetti costruiti da AEM viene eseguita dal plug-in  Content Package Maven, come descritto qui.

## Pacchetti e struttura AEM progetto {#aem-project-structure}

AEM 6.5 aderisce alle best practice più recenti per la gestione dei pacchetti e la struttura dei progetti, come implementato dall&#39;ultimo archivio dei progetti AEM sia per le implementazioni locali che per le implementazioni AMS.

>[!TIP]
>
>Per ulteriori dettagli, consultate l&#39;articolo [AEM Struttura](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) del progetto nella AEM come documentazione Cloud Service e la documentazione [AEM Project Archetype](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/archetype/overview.html) . Entrambe sono completamente supportate per AEM 6.5.

## Come ottenere il plug-in Contenuti Package Maven {#obtaining-the-content-package-maven-plugin}

Il plugin è disponibile dal repository [Maven Central.](https://mvnrepository.com/artifact/com.day.jcr.vault/content-package-maven-plugin?repo=adobe-public)

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

Per consentire a Maven di scaricare il plug-in, utilizzate il profilo fornito nella sezione [Acquisizione del plug-in](#obtaining-the-content-package-maven-plugin) di Content Package Maven in questa pagina.

## Obiettivi del plugin di Content Package Maven {#goals-of-the-content-package-maven-plugin}

Gli obiettivi e i parametri dell&#39;obiettivo forniti dal plug-in Content Package sono descritti nelle sezioni che seguono. I parametri descritti nella sezione Parametri comuni possono essere utilizzati per la maggior parte degli obiettivi. I parametri che si applicano a un obiettivo sono descritti nella sezione relativa a tale obiettivo.

### Prefisso plug-in {#plugin-prefix}

Il prefisso del plugin è `content-package`. Utilizzate questo prefisso per eseguire un obiettivo dalla riga di comando, come nell&#39;esempio seguente:

```shell
mvn content-package:build
```

### Prefisso parametro {#parameter-prefix}

Se non diversamente specificato, gli obiettivi e i parametri del plugin usano il `vault` prefisso, come nell&#39;esempio seguente:

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

### Proxy {#proxies}

Obiettivi che utilizzano i proxy per AEM utilizzano la prima configurazione proxy valida trovata nelle impostazioni Maven. Se non viene trovata alcuna configurazione proxy, non viene utilizzato alcun proxy. Vedete il `useProxy` parametro nella sezione Parametri [comuni](#common-parameters) .

### Parametri comuni {#common-parameters}

I parametri riportati nella tabella seguente sono comuni a tutti gli obiettivi, tranne se indicati nella colonna **Obiettivi** .

| Nome | Tipo | Obbligatorio | Valore predefinito | Descrizione | Obiettivi |
|---|---|---|---|---|---|
| `failOnError` | `boolean` | No | `false` | Un valore di `true` causa il fallimento della build in caso di errore. Un valore di `false` fa sì che la build ignori l&#39;errore. | Tutti gli obiettivi tranne `package` |
| `name` | `String` | `build`: Sì, `install`: No, `rm`: Yes | `build`: Nessuna impostazione predefinita, `install`: Il valore della `artifactId` proprietà del progetto Maven | Nome del pacchetto su cui agire | Tutti gli obiettivi tranne `ls` |
| `password` | `String` | Sì | `admin` | La password utilizzata per l&#39;autenticazione con AEM | Tutti gli obiettivi tranne `package` |
| `serverId` | `String` | No | L&#39;ID server da cui recuperare il nome utente e la password per l&#39;autenticazione | Tutti gli obiettivi tranne `package` |
| `targetURL` | `String` | Sì | `http://localhost:4502/crx/packmgr/service.jsp` | L&#39;URL dell&#39;API del servizio HTTP del gestore pacchetti AEM | Tutti gli obiettivi tranne `package` |
| `timeout` | `int` | No | `5` | Timeout di connessione per la comunicazione con il servizio di gestione pacchetti, in secondi | Tutti gli obiettivi tranne `package` |
| `useProxy` | `boolean` | No | `true` | Un valore che `true` fa sì che Maven utilizzi la prima configurazione proxy attiva trovata per le richieste proxy al Gestore pacchetti. | Tutti gli obiettivi tranne `package` |
| `userId` | `String` | Sì | `admin` | Nome utente con cui autenticare AEM | Tutti gli obiettivi tranne `package` |
| `verbose` | `boolean` | No | `false` | Abilita o disabilita la registrazione dettagliata | Tutti gli obiettivi tranne `package` |

### build {#build}

Crea un pacchetto di contenuti già definito in un&#39;istanza AEM.

>[!NOTE]
>
>Questo obiettivo non deve essere eseguito all&#39;interno di un progetto Maven.

#### Parametri {#parameters}

Tutti i parametri per l&#39;obiettivo di compilazione sono descritti nella sezione Parametri [](#common-parameters) comuni.

### install {#install}

Installa un pacchetto nella directory archivio. L&#39;esecuzione di questo obiettivo non richiede un progetto Maven. L&#39;obiettivo è legato alla `install` fase del ciclo di vita della costruzione Maven.

#### Parametri {#parameters-1}

Oltre ai seguenti parametri, vedete le descrizioni nella sezione Parametri [comuni](#common-parameters) .

| Nome | Tipo | Obbligatorio | Valore predefinito | Descrizione |
|---|---|---|---|---|---|
| `artifact` | `String` | No | Il valore della `artifactId` proprietà del progetto Maven | Una stringa del modulo `groupId:artifactId:version[:packaging]` |
| `artifactId` | `String` | No | Nessuno | ID dell&#39;artifact da installare |
| `groupId` | `String` | No | Nessuno | L&#39; `groupId` artifact da installare |
| `install` | `boolean` | No | `true` | Determina se rimuovere automaticamente il pacchetto al momento del caricamento |
| `localRepository` | `org.apache.maven.artifact.repository.ArtifactRepository` | No | Il valore della variabile di `localRepository` sistema | Il repository locale Maven che non può essere configurato utilizzando la configurazione del plug-in come proprietà di sistema viene sempre utilizzato |
| `packageFile` | `java.io.File` | No | Il manufatto principale definito per il progetto Maven | Nome del file del pacchetto da installare |
| `packaging` | `String` | No | `zip` | Tipo di imballaggio dell&#39;artefatto da installare |
| `pomRemoteRepositories` | `java.util.List` | Sì | Il valore della `remoteArtifactRepositories` proprietà definita per il progetto Maven | Questo valore non può essere configurato con la configurazione del plug-in e deve essere specificato nel progetto. |
| `project` | `org.apache.maven.project.MavenProject` | Sì | Progetto per il quale è configurato il plug-in | Il progetto Maven che è implicito perché il progetto contiene la configurazione del plugin |
| `repositoryId` (POM), `repoID` (riga di comando) | `String` | No | `temp` | ID del repository da cui viene recuperato l&#39;artifact |
| `repositoryUrl` (POM), `repoURL` (riga di comando) | `String` | No | Nessuno | URL del repository da cui viene recuperato l&#39;artifact |
| version | Stringa | No | Nessuno | Versione dell&#39;artifact da installare |

### ls {#ls}

Elenca i pacchetti distribuiti in Gestione pacchetti.

#### Parametri {#parameters-2}

Tutti i parametri dell&#39;obiettivo ls sono descritti nella sezione Parametri [](#common-parameters) comuni.

### rm {#rm}

Rimuove un pacchetto da Gestione pacchetti.

#### Parametri {#parameters-3}

Tutti i parametri dell&#39;obiettivo rm sono descritti nella sezione Parametri [](#common-parameters) comuni.

### uninstall {#uninstall}

Disinstalla un pacchetto. Il pacchetto rimane sul server nello stato disinstallato.

#### Parametri {#parameters-4}

Tutti i parametri dell&#39;obiettivo di disinstallazione sono descritti nella sezione Parametri [](#common-parameters) comuni.

### package {#package}

Crea un pacchetto di contenuti. La configurazione predefinita dell&#39;obiettivo del pacchetto include il contenuto della directory in cui vengono salvati i file compilati. L&#39;esecuzione dell&#39;obiettivo del pacchetto richiede il completamento della fase di compilazione. L&#39;obiettivo del pacchetto è legato alla fase del pacchetto del ciclo di vita della build Maven.

#### Parametri {#parameters-5}

Oltre ai seguenti parametri, vedete la descrizione del `name` parametro nella sezione Parametri [comuni](#common-parameters) .

| Nome | Tipo | Obbligatorio | Valore predefinito | Descrizione |
|---|---|---|---|---|
| `archive` | `org.apache.maven.archiver.MavenArchiveConfiguration` | No | Nessuno | Configurazione dell&#39;archivio da utilizzare |
| `builtContentDirectory` | `java.io.File` | Sì | Il valore della directory di output della build Maven | La directory che contiene il contenuto da includere nel pacchetto |
| `dependencies` | `java.util.List` | No | Nessuno |  |
| `embeddedTarget` | `java.lang.String` | No | Nessuno |  |
| `embeddeds` | `java.util.List` | No | Nessuno |  |
| `failOnMissingEmbed` | `boolean` | Sì | `false` | Un valore di `true` fa sì che la build non riesca quando un artefatto incorporato non viene trovato nelle dipendenze del progetto. Un valore di `false` fa sì che la build ignori tali errori. |
| `filterSource` | `java.io.File` | No | Nessuno | Questo parametro definisce un file che specifica l’origine del filtro dell’area di lavoro. I filtri specificati nella configurazione e iniettati tramite incorporamenti o pacchetti secondari vengono uniti con il contenuto del file. |
| `filters` | `com.day.jcr.vault.maven.pack.impl.DefaultWorkspaceFilter` | No | Nessuno | Questo parametro contiene elementi di filtro che definiscono il contenuto del pacchetto. Una volta eseguiti, i filtri vengono inclusi nel `filter.xml` file. Vedere la sezione [Utilizzo dei filtri](#using-filters) di seguito. |
| `finalName` | `java.lang.String` | Sì | La `finalName` definizione del progetto Maven (fase di costruzione) | Il nome del file ZIP del pacchetto generato, senza l&#39;estensione del `.zip` file |
| `group` | `java.lang.String` | Sì | La `groupID` definizione nel progetto Maven | Il pacchetto `groupId` di contenuto generato che fa parte del percorso di installazione di destinazione per il pacchetto di contenuto |
| `outputDirectory` | `java.io.File` | Sì | La directory di compilazione definita nel progetto Maven | La directory locale in cui viene salvato il pacchetto di contenuto |
| `prefix` | `java.lang.String` | No | Nessuno |  |
| `project` | `org.apache.maven.project.MavenProject` | Sì | Nessuno | Il progetto Maven |
| `properties` | `java.util.Map` | No | Nessuno | Questi parametri definiscono proprietà aggiuntive che è possibile impostare nel `properties.xml` file. Queste proprietà non possono sovrascrivere le seguenti proprietà predefinite: `group` (usare `group` parametro per impostare), `name` (usare `name` parametro per impostare), `version` (usare `version` parametro per impostare), `description` (impostato dalla descrizione del progetto), ( `groupId` del descrittore del progetto Maven), (del descrittore del progetto Maven),  (usare il parametro per impostare),  (il valore della proprietà del sistema ),  (l&#39;ora del sistema corrente),`groupId` `artifactId``artifactId` `dependencies` `dependencies` `createdBy` `user.name` `created` `requiresRoot` `requiresRoot` `packagePath` generato automaticamente dal gruppo e dal nome del pacchetto) |
| `requiresRoot` | `boolean` | Sì | false | Definisce se il pacchetto richiede root. Questo diventerà la `requiresRoot` proprietà del `properties.xml` file. |
| `subPackages` | `java.util.List` | No | Nessuno |  |
| `version` | `java.lang.String` | Sì | La versione definita nel progetto Maven | Versione del pacchetto di contenuti |
| `workDirectory` | `java.io.File` | Sì | Directory definita nel progetto Maven (fase di costruzione) | La directory che contiene il contenuto da includere nel pacchetto |

#### Utilizzo dei filtri {#using-filters}

Utilizzate l&#39;elemento filter per definire il contenuto del pacchetto. I filtri vengono aggiunti all&#39; `workspaceFilter` elemento nel `META-INF/vault/filter.xml` file del pacchetto.

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

L&#39; `mode` elemento definisce in che modo il contenuto del repository viene influenzato quando il pacchetto viene importato. È possibile utilizzare i seguenti valori:

* **Unisci:** Viene aggiunto il contenuto del pacchetto che non è già presente nella directory archivio. Il contenuto presente sia nel pacchetto che nell&#39;archivio rimane invariato. Nessun contenuto viene rimosso dalla directory archivio.
* **Sostituisci:** Il contenuto del pacchetto che non si trova nella directory archivio viene aggiunto alla directory archivio. Il contenuto del repository viene sostituito con il contenuto corrispondente presente nel pacchetto. Il contenuto viene rimosso dalla directory archivio quando non esiste nel pacchetto.
* **Aggiorna:** Il contenuto del pacchetto che non si trova nella directory archivio viene aggiunto alla directory archivio. Il contenuto del repository viene sostituito con il contenuto corrispondente presente nel pacchetto. Il contenuto esistente viene rimosso dalla directory archivio.

Se il filtro non contiene `mode` elementi, viene utilizzato il valore predefinito di `replace` .

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

I file sorgente possono trovarsi ovunque nel file system. Nel file POM, definite le risorse di build per copiare i file sorgente nel file `target/vault-work/META-INF` da includere nel pacchetto.

Il seguente codice POM aggiunge al pacchetto i file presenti nella `META-INF` cartella dell’origine del progetto:

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

Il seguente codice POM aggiunge al pacchetto solo una miniatura. L’immagine in miniatura deve essere denominata `thumbnail.png`e deve trovarsi nella `META-INF/vault/definition` cartella del pacchetto. In questo esempio, il file di origine si trova nella `/src/main/content/META-INF/vault/definition` cartella del progetto:

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
>Per ulteriori dettagli, consultate l&#39;articolo [AEM Struttura](https://docs.adobe.com/content/help/it-IT/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) del progetto nella AEM come documentazione Cloud Service e la documentazione [AEM Project Archetype](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/archetype/overview.html) . Entrambe sono completamente supportate per AEM 6.5.
