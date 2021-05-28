---
title: Plug-in Maven del pacchetto di contenuti di Adobe
description: Utilizza il plug-in Maven del pacchetto di contenuti per distribuire le applicazioni AEM
exl-id: d631d6df-7507-4752-862b-9094af9759a0
source-git-commit: ac64ca485391d843c0ebefcf86e80b4015b72b2f
workflow-type: tm+mt
source-wordcount: '1847'
ht-degree: 5%

---

# Plug-in Maven del pacchetto di contenuti di Adobe {#adobe-content-package-maven-plugin}

Utilizza il plug-in Maven Adobe Content Package per integrare le attività di distribuzione e gestione dei pacchetti nei tuoi progetti Maven.

La distribuzione dei pacchetti costruiti da AEM viene eseguita dal plug-in Adobe Content Package Maven e consente l&#39;automazione delle attività normalmente eseguite utilizzando AEM Package Manager:

* Crea nuovi pacchetti da file nel file system.
* Installa e disinstalla i pacchetti su AEM.
* Crea pacchetti già definiti in AEM.
* Ottieni un elenco dei pacchetti installati in AEM.
* Rimuovi un pacchetto da AEM.

In questo documento viene descritto come utilizzare Maven per gestire queste attività. Tuttavia è importante anche comprendere [come sono strutturati i progetti AEM e i relativi pacchetti.](#aem-project-structure)

>[!NOTE]
>
>La creazione del pacchetto è ora di proprietà del plug-in Maven [Apache Jackrabbit FileVault Package](https://jackrabbit.apache.org/filevault-package-maven-plugin/). La distribuzione dei pacchetti costruiti da AEM viene eseguita dal plug-in Maven Adobe Content Package come descritto qui.

## Pacchetti e struttura del progetto AEM {#aem-project-structure}

AEM come Cloud Service aderisce alle best practice più recenti per la gestione dei pacchetti e la struttura del progetto, implementate dall’ultimo Archetype di progetto AEM.

>[!TIP]
>
>Per ulteriori dettagli, consulta l’articolo [AEM Struttura del progetto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) nella AEM come documentazione di Cloud Service e la documentazione [AEM Archetipo di progetto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) . Entrambi sono pienamente supportati per AEM 6.5.

## Ottenimento del plug-in Maven del pacchetto di contenuti {#obtaining-the-content-package-maven-plugin}

Il plug-in è disponibile dal [Repository centrale Maven.](https://mvnrepository.com/artifact/com.day.jcr.vault/content-package-maven-plugin?repo=adobe-public)

## Obiettivi e parametri del plug-in Maven del pacchetto di contenuti

Per utilizzare il plug-in Maven del pacchetto di contenuti, aggiungi il seguente elemento plug-in all’interno dell’elemento build del file POM:

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

Per consentire a Maven di scaricare il plug-in, utilizza il profilo fornito nella sezione [Ottenimento del plug-in Maven del pacchetto di contenuti](#obtaining-the-content-package-maven-plugin) in questa pagina.

## Obiettivi del plug-in Maven del pacchetto di contenuti {#goals-of-the-content-package-maven-plugin}

Gli obiettivi e i parametri dell’obiettivo forniti dal plug-in Content Package sono descritti nelle sezioni seguenti. I parametri descritti nella sezione Parametri comuni possono essere utilizzati per la maggior parte degli obiettivi. I parametri che si applicano a un obiettivo sono descritti nella sezione relativa a tale obiettivo.

### Prefisso plug-in {#plugin-prefix}

Il prefisso del plug-in è `content-package`. Utilizza questo prefisso per eseguire un obiettivo dalla riga di comando, come nell’esempio seguente:

```shell
mvn content-package:build
```

### Prefisso parametro {#parameter-prefix}

Salvo diversa indicazione, gli obiettivi e i parametri del plug-in utilizzano il prefisso `vault` , come nell’esempio seguente:

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

### Proxy {#proxies}

Obiettivi che utilizzano i proxy per AEM utilizzano la prima configurazione proxy valida trovata nelle impostazioni Maven. Se non viene trovata alcuna configurazione proxy, non viene utilizzato alcun proxy. Vedere il parametro `useProxy` nella sezione [Parametri comuni](#common-parameters) .

### Parametri comuni {#common-parameters}

I parametri nella tabella seguente sono comuni a tutti gli obiettivi, tranne quando indicati nella colonna **Obiettivi** .

| Nome | Tipo | Obbligatorio | Valore predefinito | Descrizione | Obiettivi |
|---|---|---|---|---|---|
| `failOnError` | `boolean` | No | `false` | Un valore di `true` causa il mancato funzionamento della build quando si verifica un errore. Un valore di `false` fa sì che la build ignori l&#39;errore. | Tutti gli obiettivi eccetto `package` |
| `name` | `String` | `build`: Sì,  `install`: No,  `rm`: Sì | `build`: Nessun valore predefinito,  `install`: Valore della  `artifactId` proprietà del progetto Maven | Nome del pacchetto su cui agire | Tutti gli obiettivi eccetto `ls` |
| `password` | `String` | Sì | `admin` | Password utilizzata per l&#39;autenticazione con AEM | Tutti gli obiettivi eccetto `package` |
| `serverId` | `String` | No | ID server da cui recuperare il nome utente e la password per l&#39;autenticazione | Tutti gli obiettivi eccetto `package` |
| `targetURL` | `String` | Sì | `http://localhost:4502/crx/packmgr/service.jsp` | URL dell’API del servizio HTTP del gestore dei pacchetti AEM | Tutti gli obiettivi eccetto `package` |
| `timeout` | `int` | No | `5` | Timeout di connessione per la comunicazione con il servizio di gestione pacchetti, in secondi | Tutti gli obiettivi eccetto `package` |
| `useProxy` | `boolean` | No | `true` | Un valore di `true` fa sì che Maven utilizzi la prima configurazione proxy attiva trovata per inviare richieste proxy a Gestione pacchetti. | Tutti gli obiettivi eccetto `package` |
| `userId` | `String` | Sì | `admin` | Nome utente con cui eseguire l&#39;autenticazione con AEM | Tutti gli obiettivi eccetto `package` |
| `verbose` | `boolean` | No | `false` | Abilita o disabilita la registrazione dettagliata | Tutti gli obiettivi eccetto `package` |

### build {#build}

Crea un pacchetto di contenuti già definito in un’istanza AEM.

>[!NOTE]
>
>Questo obiettivo non deve essere eseguito all’interno di un progetto Maven.

#### Parametri {#parameters}

Tutti i parametri per l&#39;obiettivo di compilazione sono descritti nella sezione [Parametri comuni](#common-parameters) .

### installare {#install}

Installa un pacchetto nella directory archivio. L’esecuzione di questo obiettivo non richiede un progetto Maven. L’obiettivo è associato alla fase `install` del ciclo di vita della build Maven.

#### Parametri {#parameters-1}

Oltre ai seguenti parametri, consulta le descrizioni nella sezione [Parametri comuni](#common-parameters) .

| Nome | Tipo | Obbligatorio | Valore predefinito | Descrizione |
|---|---|---|---|---|---|
| `artifact` | `String` | No | Valore della proprietà `artifactId` del progetto Maven | Una stringa del modulo `groupId:artifactId:version[:packaging]` |
| `artifactId` | `String` | No | Nessuna | ID dell&#39;artefatto da installare |
| `groupId` | `String` | No | Nessuna | `groupId` dell&#39;artefatto da installare |
| `install` | `boolean` | No | `true` | Determina se rimuovere automaticamente dal pacchetto il pacchetto quando viene caricato |
| `localRepository` | `org.apache.maven.artifact.repository.ArtifactRepository` | No | Valore della variabile di sistema `localRepository` | L’archivio Maven locale che non può essere configurato utilizzando la configurazione del plug-in come proprietà del sistema viene sempre utilizzato |
| `packageFile` | `java.io.File` | No | L’artefatto principale definito per il progetto Maven | Nome del file del pacchetto da installare |
| `packaging` | `String` | No | `zip` | Tipo di imballaggio dell&#39;artefatto da installare |
| `pomRemoteRepositories` | `java.util.List` | Sì | Valore della proprietà `remoteArtifactRepositories` definita per il progetto Maven | Questo valore non può essere configurato utilizzando la configurazione del plug-in e deve essere specificato nel progetto. |
| `project` | `org.apache.maven.project.MavenProject` | Sì | Progetto per il quale è configurato il plug-in | Progetto Maven implicito perché il progetto contiene la configurazione del plug-in |
| `repositoryId` (POM),  `repoID` (riga di comando) | `String` | No | `temp` | ID dell’archivio da cui viene recuperato l’artefatto |
| `repositoryUrl` (POM),  `repoURL` (riga di comando) | `String` | No | Nessuna | URL dell’archivio da cui viene recuperato l’artefatto. |
| version | Stringa | No | Nessuna | Versione dell&#39;artefatto da installare |

### ls {#ls}

Elenca i pacchetti distribuiti in Gestione pacchetti.

#### Parametri {#parameters-2}

Tutti i parametri dell&#39;obiettivo ls sono descritti nella sezione [Parametri comuni](#common-parameters) .

### rm {#rm}

Rimuove un pacchetto da Gestione pacchetti.

#### Parametri {#parameters-3}

Tutti i parametri dell&#39;obiettivo rm sono descritti nella sezione [Parametri comuni](#common-parameters) .

### disinstallare {#uninstall}

Disinstalla un pacchetto. Il pacchetto rimane sul server nello stato disinstallato.

#### Parametri {#parameters-4}

Tutti i parametri dell&#39;obiettivo di disinstallazione sono descritti nella sezione [Parametri comuni](#common-parameters) .

### pacchetto {#package}

Crea un pacchetto di contenuti. La configurazione predefinita dell&#39;obiettivo del pacchetto include il contenuto della directory in cui vengono salvati i file compilati. L’esecuzione dell’obiettivo del pacchetto richiede che la fase di compilazione della build sia stata completata. L’obiettivo del pacchetto è associato alla fase del pacchetto del ciclo di vita della build Maven.

#### Parametri {#parameters-5}

Oltre ai seguenti parametri, vedi la descrizione del parametro `name` nella sezione [Parametri comuni](#common-parameters) .

| Nome | Tipo | Obbligatorio | Valore predefinito | Descrizione |
|---|---|---|---|---|
| `archive` | `org.apache.maven.archiver.MavenArchiveConfiguration` | No | Nessuna | La configurazione di archivio da utilizzare |
| `builtContentDirectory` | `java.io.File` | Sì | Il valore della directory di output della build Maven | La directory che contiene il contenuto da includere nel pacchetto |
| `dependencies` | `java.util.List` | No | Nessuna |  |
| `embeddedTarget` | `java.lang.String` | No | Nessuna |  |
| `embeddeds` | `java.util.List` | No | Nessuna |  |
| `failOnMissingEmbed` | `boolean` | Sì | `false` | Un valore di `true` causa il mancato funzionamento della build quando un artefatto incorporato non viene trovato nelle dipendenze del progetto. Un valore di `false` fa sì che la build ignori tali errori. |
| `filterSource` | `java.io.File` | No | Nessuna | Questo parametro definisce un file che specifica l&#39;origine del filtro dell&#39;area di lavoro. I filtri specificati nella configurazione e inseriti tramite incorporamenti o pacchetti secondari vengono uniti con il contenuto del file. |
| `filters` | `com.day.jcr.vault.maven.pack.impl.DefaultWorkspaceFilter` | No | Nessuna | Questo parametro contiene elementi di filtro che definiscono il contenuto del pacchetto. Quando eseguito, i filtri sono inclusi nel file `filter.xml`. Consulta la sezione [Utilizzo dei filtri](#using-filters) di seguito. |
| `finalName` | `java.lang.String` | Sì | La `finalName` definita nel progetto Maven (fase di creazione) | Il nome del file ZIP del pacchetto generato, senza l&#39;estensione del file `.zip` |
| `group` | `java.lang.String` | Sì | Il `groupID` definito nel progetto Maven | La `groupId` del pacchetto di contenuti generati che fa parte del percorso di installazione di destinazione per il pacchetto di contenuti |
| `outputDirectory` | `java.io.File` | Sì | La directory di compilazione definita nel progetto Maven | Directory locale in cui viene salvato il pacchetto di contenuti |
| `prefix` | `java.lang.String` | No | Nessuna |  |
| `project` | `org.apache.maven.project.MavenProject` | Sì | Nessuna | Il progetto Maven |
| `properties` | `java.util.Map` | No | Nessuna | Questi parametri definiscono proprietà aggiuntive che è possibile impostare nel file `properties.xml` . Queste proprietà non possono sovrascrivere le seguenti proprietà predefinite: `group` (usare il parametro `group` per impostare), `name` (usare il parametro `name` per impostare), `version` (usare il parametro `version` per impostare), `description` (impostato dalla descrizione del progetto), `groupId` (`groupId` del descrittore del progetto Maven), `artifactId` (`artifactId`) Descrittore di progetto Maven), `dependencies` (utilizza il parametro `dependencies` per impostare ), `createdBy` (il valore della proprietà di sistema `user.name`), `created` (l&#39;ora di sistema corrente), `requiresRoot` (utilizza il parametro `requiresRoot` per impostare), `packagePath` (generato automaticamente dal nome del gruppo e del pacchetto) |
| `requiresRoot` | `boolean` | Sì | false | Definisce se il pacchetto richiede la radice. Questo diventerà la proprietà `requiresRoot` del file `properties.xml`. |
| `subPackages` | `java.util.List` | No | Nessuna |  |
| `version` | `java.lang.String` | Sì | Versione definita nel progetto Maven | Versione del pacchetto di contenuti |
| `workDirectory` | `java.io.File` | Sì | La directory definita nel progetto Maven (fase di creazione) | Directory contenente il contenuto da includere nel pacchetto |

#### Utilizzo dei filtri {#using-filters}

Utilizza l’elemento filters per definire il contenuto del pacchetto. I filtri vengono aggiunti all&#39;elemento `workspaceFilter` nel file `META-INF/vault/filter.xml` del pacchetto.

L’esempio di filtro seguente mostra la struttura XML da utilizzare:

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

L’elemento `mode` definisce in che modo il contenuto è interessato dall’archivio quando il pacchetto viene importato. È possibile utilizzare i seguenti valori:

* **Unione:** viene aggiunto il contenuto del pacchetto che non è già presente nella directory archivio. Il contenuto presente sia nel pacchetto che nell’archivio rimane invariato. Nessun contenuto viene rimosso dalla directory archivio.
* **Sostituisci:** il contenuto del pacchetto che non si trova nella directory archivio viene aggiunto alla directory archivio. Il contenuto nell’archivio viene sostituito con il contenuto corrispondente nel pacchetto. Il contenuto viene rimosso dall’archivio quando non esiste nel pacchetto.
* **Aggiornamento:** il contenuto del pacchetto che non si trova nella directory archivio viene aggiunto alla directory archivio. Il contenuto nell’archivio viene sostituito con il contenuto corrispondente nel pacchetto. Il contenuto esistente viene rimosso dalla directory archivio.

Quando il filtro non contiene elementi `mode`, viene utilizzato il valore predefinito `replace`.

### aiuto {#help}

#### Parametri {#parameters-6}

| Nome | Tipo | Obbligatorio | Valore predefinito | Descrizione |
|---|---|---|---|---|
| `detail` | `boolean` | No | `false` | Determina se visualizzare tutte le proprietà impostabili per ogni obiettivo |
| `goal` | `String` | No | Nessuna | Questi parametri definiscono il nome dell’obiettivo per il quale visualizzare la guida. Se non viene specificato alcun valore, viene visualizzata la guida per tutti gli obiettivi. |
| `indentSize` | `int` | No | `2` | Il numero di spazi da utilizzare per il rientro di ciascun livello (deve essere positivo se definito) |
| `lineLength` | `int` | No | `80` | La lunghezza massima di una linea di visualizzazione (deve essere positiva se definita) |

## Inclusione di un&#39;immagine miniatura o di un file di proprietà nel pacchetto {#including-a-thumbnail-image-or-properties-file-in-the-package}

Sostituisci i file di configurazione del pacchetto predefiniti per personalizzare le proprietà del pacchetto. Ad esempio, includi un’immagine di miniatura per distinguere il pacchetto in Gestione pacchetti e Condivisione pacchetti.

I file di origine possono trovarsi in qualsiasi punto del file system. Nel file POM, definisci le risorse di build per copiare i file di origine in `target/vault-work/META-INF` da includere nel pacchetto.

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

Il seguente codice POM aggiunge solo un&#39;immagine di miniatura al pacchetto. L&#39;immagine miniatura deve essere denominata `thumbnail.png` e deve trovarsi nella cartella `META-INF/vault/definition` del pacchetto. In questo esempio, il file di origine si trova nella cartella `/src/main/content/META-INF/vault/definition` del progetto:

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

## Utilizzo dell&#39;Archetipo di progetto AEM per generare progetti AEM {#using-archetypes}

L’ultimo archetipo di progetto AEM implementa la struttura dei pacchetti con le best practice per le implementazioni on-premise e AMS ed è consigliato per tutti i progetti AEM.

>[!TIP]
>
>Per ulteriori dettagli, consulta l’articolo [AEM Struttura del progetto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) nella AEM come documentazione di Cloud Service e la documentazione [AEM Archetipo di progetto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) . Entrambi sono pienamente supportati per AEM 6.5.
