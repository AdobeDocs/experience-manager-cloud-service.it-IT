---
title: Plug-in Maven del pacchetto di contenuti di Adobe
description: Utilizza il plug-in Maven del pacchetto di contenuti per distribuire le applicazioni AEM
exl-id: d631d6df-7507-4752-862b-9094af9759a0
source-git-commit: 278470482a582db7d88bfbe6f851eb3070afc0df
workflow-type: tm+mt
source-wordcount: '1844'
ht-degree: 5%

---

# Plug-in Maven del pacchetto di contenuti di Adobe {#adobe-content-package-maven-plugin}

Utilizza il plug-in Maven Adobe Content Package per integrare le attività di distribuzione e gestione dei pacchetti nei tuoi progetti Maven.

La distribuzione dei pacchetti costruiti da AEM viene eseguita dal plug-in Adobe Content Package Maven e consente l&#39;automazione delle attività normalmente eseguite utilizzando AEM [Gestione pacchetti:](/help/implementing/developing/tools/package-manager.md)

* Crea nuovi pacchetti da file nel file system.
* Installa e disinstalla i pacchetti su AEM.
* Crea pacchetti già definiti in AEM.
* Ottieni un elenco dei pacchetti installati in AEM.
* Rimuovi un pacchetto da AEM.

In questo documento viene descritto come utilizzare Maven per gestire queste attività. Tuttavia è anche importante capire [come sono strutturati AEM progetti e i relativi pacchetti.](#aem-project-structure)

>[!NOTE]
>
>La creazione del pacchetto è ora di proprietà della [Plug-in Maven pacchetto Apache Jackrabbit FileVault](https://jackrabbit.apache.org/filevault-package-maven-plugin/). La distribuzione dei pacchetti costruiti da AEM viene eseguita dal plug-in Maven Adobe Content Package come descritto qui.

## Pacchetti e struttura del progetto AEM {#aem-project-structure}

AEM as a Cloud Service aderisce alle best practice più recenti per la gestione dei pacchetti e la struttura del progetto, implementate dall’ultimo Archetipo di progetto AEM.

>[!TIP]
>
>Per ulteriori dettagli, consulta la sezione [AEM struttura del progetto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=it) articolo nella documentazione as a Cloud Service AEM nonché [Archetipo di progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) documentazione. Entrambi sono pienamente supportati per AEM 6.5.

## Ottenimento del plug-in Maven del pacchetto di contenuti {#obtaining-the-content-package-maven-plugin}

Il plug-in è disponibile dal [Archivio centrale Maven.](https://mvnrepository.com/artifact/com.day.jcr.vault/content-package-maven-plugin?repo=adobe-public)

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

Per consentire a Maven di scaricare il plug-in, utilizza il profilo fornito nella [Ottenimento del plug-in Maven del pacchetto di contenuti](#obtaining-the-content-package-maven-plugin) in questa pagina.

## Obiettivi del plugin Maven del pacchetto di contenuti {#goals-of-the-content-package-maven-plugin}

Gli obiettivi e i parametri dell’obiettivo forniti dal plug-in Content Package sono descritti nelle sezioni seguenti. I parametri descritti nella sezione Parametri comuni possono essere utilizzati per la maggior parte degli obiettivi. I parametri che si applicano a un obiettivo sono descritti nella sezione relativa a tale obiettivo.

### Prefisso plug-in {#plugin-prefix}

Il prefisso del plug-in è `content-package`. Utilizza questo prefisso per eseguire un obiettivo dalla riga di comando, come nell’esempio seguente:

```shell
mvn content-package:build
```

### Prefisso parametro {#parameter-prefix}

Se non diversamente indicato, gli obiettivi e i parametri del plug-in utilizzano il `vault` Prefisso, come nell’esempio seguente:

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

### Proxy {#proxies}

Obiettivi che utilizzano i proxy per AEM utilizzano la prima configurazione proxy valida trovata nelle impostazioni Maven. Se non viene trovata alcuna configurazione proxy, non viene utilizzato alcun proxy. Consulta la sezione `useProxy` nel [Parametri comuni](#common-parameters) sezione .

### Parametri comuni {#common-parameters}

I parametri nella tabella seguente sono comuni a tutti gli obiettivi, tranne quando indicati nella **Obiettivi** colonna.

| Nome | Tipo | Obbligatorio | Valore predefinito | Descrizione | Obiettivi |
|---|---|---|---|---|---|
| `failOnError` | `boolean` | No | `false` | Un valore di `true` causa il mancato funzionamento della build quando si verifica un errore. Un valore di `false` fa sì che la build ignori l’errore. | Tutti gli obiettivi tranne `package` |
| `name` | `String` | `build`: Sì, `install`: No, `rm`: Sì | `build`: Nessuna impostazione predefinita, `install`: Il valore del `artifactId` proprietà del progetto Maven | Nome del pacchetto su cui agire | Tutti gli obiettivi tranne `ls` |
| `password` | `String` | Sì | `admin` | Password utilizzata per l&#39;autenticazione con AEM | Tutti gli obiettivi tranne `package` |
| `serverId` | `String` | No | ID server da cui recuperare il nome utente e la password per l&#39;autenticazione | Tutti gli obiettivi tranne `package` |
| `targetURL` | `String` | Sì | `http://localhost:4502/crx/packmgr/service.jsp` | URL dell’API del servizio HTTP del gestore dei pacchetti AEM | Tutti gli obiettivi tranne `package` |
| `timeout` | `int` | No | `5` | Timeout di connessione per la comunicazione con il servizio di gestione pacchetti, in secondi | Tutti gli obiettivi tranne `package` |
| `useProxy` | `boolean` | No | `true` | Un valore di `true` fa sì che Maven utilizzi la prima configurazione proxy attiva trovata per delegare le richieste a Gestione pacchetti. | Tutti gli obiettivi tranne `package` |
| `userId` | `String` | Sì | `admin` | Nome utente con cui eseguire l&#39;autenticazione con AEM | Tutti gli obiettivi tranne `package` |
| `verbose` | `boolean` | No | `false` | Abilita o disabilita la registrazione dettagliata | Tutti gli obiettivi tranne `package` |

### build {#build}

Crea un pacchetto di contenuti già definito in un’istanza AEM.

>[!NOTE]
>
>Questo obiettivo non deve essere eseguito all’interno di un progetto Maven.

#### Parametri {#parameters}

Tutti i parametri per l’obiettivo di compilazione sono descritti nella sezione [Parametri comuni](#common-parameters) sezione .

### installare {#install}

Installa un pacchetto nella directory archivio. L’esecuzione di questo obiettivo non richiede un progetto Maven. L’obiettivo è associato al `install` fase del ciclo di vita della build Maven.

#### Parametri {#parameters-1}

Oltre ai seguenti parametri, consulta le descrizioni nel [Parametri comuni](#common-parameters) sezione .

| Nome | Tipo | Obbligatorio | Valore predefinito | Descrizione |
|---|---|---|---|---|
| `artifact` | `String` | No | Il valore del `artifactId` proprietà del progetto Maven | Una stringa del modulo `groupId:artifactId:version[:packaging]` |
| `artifactId` | `String` | No | Nessuno | ID dell&#39;artefatto da installare |
| `groupId` | `String` | No | Nessuno | La `groupId` dell&#39;artefatto da installare |
| `install` | `boolean` | No | `true` | Determina se rimuovere automaticamente dal pacchetto il pacchetto quando viene caricato |
| `localRepository` | `org.apache.maven.artifact.repository.ArtifactRepository` | No | Il valore del `localRepository` variabile di sistema | L’archivio Maven locale che non può essere configurato utilizzando la configurazione del plug-in come proprietà del sistema viene sempre utilizzato |
| `packageFile` | `java.io.File` | No | L’artefatto principale definito per il progetto Maven | Nome del file del pacchetto da installare |
| `packaging` | `String` | No | `zip` | Tipo di imballaggio dell&#39;artefatto da installare |
| `pomRemoteRepositories` | `java.util.List` | Sì | Il valore del `remoteArtifactRepositories` proprietà definita per il progetto Maven | Questo valore non può essere configurato utilizzando la configurazione del plug-in e deve essere specificato nel progetto. |
| `project` | `org.apache.maven.project.MavenProject` | Sì | Progetto per il quale è configurato il plug-in | Progetto Maven implicito perché il progetto contiene la configurazione del plug-in |
| `repositoryId` POM, `repoID` (riga di comando) | `String` | No | `temp` | ID dell’archivio da cui viene recuperato l’artefatto |
| `repositoryUrl` POM, `repoURL` (riga di comando) | `String` | No | Nessuno | URL dell’archivio da cui viene recuperato l’artefatto. |
| version | Stringa | No | Nessuno | Versione dell&#39;artefatto da installare |

### ls {#ls}

Elenca i pacchetti distribuiti in [Gestione pacchetti.](/help/implementing/developing/tools/package-manager.md)

#### Parametri {#parameters-2}

Tutti i parametri dell’obiettivo ls sono descritti nella sezione [Parametri comuni](#common-parameters) sezione .

### rm {#rm}

Rimuove un pacchetto da [Gestione pacchetti.](/help/implementing/developing/tools/package-manager.md)

#### Parametri {#parameters-3}

Tutti i parametri dell’obiettivo rm sono descritti nella sezione [Parametri comuni](#common-parameters) sezione .

### disinstallare {#uninstall}

Disinstalla un pacchetto. Il pacchetto rimane sul server nello stato disinstallato.

#### Parametri {#parameters-4}

Tutti i parametri dell&#39;obiettivo di disinstallazione sono descritti nel [Parametri comuni](#common-parameters) sezione .

### pacchetto {#package}

Crea un pacchetto di contenuti. La configurazione predefinita dell&#39;obiettivo del pacchetto include il contenuto della directory in cui vengono salvati i file compilati. L’esecuzione dell’obiettivo del pacchetto richiede che la fase di compilazione della build sia stata completata. L’obiettivo del pacchetto è associato alla fase del pacchetto del ciclo di vita della build Maven.

#### Parametri {#parameters-5}

Oltre ai seguenti parametri, consulta la descrizione del `name` nel [Parametri comuni](#common-parameters) sezione .

| Nome | Tipo | Obbligatorio | Valore predefinito | Descrizione |
|---|---|---|---|---|
| `archive` | `org.apache.maven.archiver.MavenArchiveConfiguration` | No | Nessuno | La configurazione di archivio da utilizzare |
| `builtContentDirectory` | `java.io.File` | Sì | Il valore della directory di output della build Maven | La directory che contiene il contenuto da includere nel pacchetto |
| `dependencies` | `java.util.List` | No | Nessuno |  |
| `embeddedTarget` | `java.lang.String` | No | Nessuno |  |
| `embeddeds` | `java.util.List` | No | Nessuno |  |
| `failOnMissingEmbed` | `boolean` | Sì | `false` | Un valore di `true` causa il mancato funzionamento della build quando un artefatto incorporato non viene trovato nelle dipendenze del progetto. Un valore di `false` fa sì che la build ignori tali errori. |
| `filterSource` | `java.io.File` | No | Nessuno | Questo parametro definisce un file che specifica l&#39;origine del filtro dell&#39;area di lavoro. I filtri specificati nella configurazione e inseriti tramite incorporamenti o pacchetti secondari vengono uniti con il contenuto del file. |
| `filters` | `com.day.jcr.vault.maven.pack.impl.DefaultWorkspaceFilter` | No | Nessuno | Questo parametro contiene elementi di filtro che definiscono il contenuto del pacchetto. Quando vengono eseguiti, i filtri sono inclusi nella `filter.xml` file. Consulta la sezione [Utilizzo dei filtri](#using-filters) di seguito. |
| `finalName` | `java.lang.String` | Sì | La `finalName` definito nel progetto Maven (fase di creazione) | Il nome del file ZIP del pacchetto generato, senza il `.zip` estensione file |
| `group` | `java.lang.String` | Sì | La `groupID` definito nel progetto Maven | La `groupId` del pacchetto di contenuti generato che fa parte del percorso di installazione di destinazione per il pacchetto di contenuti |
| `outputDirectory` | `java.io.File` | Sì | La directory di compilazione definita nel progetto Maven | Directory locale in cui viene salvato il pacchetto di contenuti |
| `prefix` | `java.lang.String` | No | Nessuno |  |
| `project` | `org.apache.maven.project.MavenProject` | Sì | Nessuno | Il progetto Maven |
| `properties` | `java.util.Map` | No | Nessuno | Questi parametri definiscono proprietà aggiuntive che è possibile impostare nel `properties.xml` file. Queste proprietà non possono sovrascrivere le seguenti proprietà predefinite: `group` (usare `group` parametro da impostare), `name` (usare `name` parametro da impostare), `version` (usare `version` parametro da impostare), `description` (dalla descrizione del progetto), `groupId` (`groupId` del descrittore del progetto Maven), `artifactId` (`artifactId` del descrittore del progetto Maven), `dependencies` (usare `dependencies` parametro da impostare), `createdBy` (il valore `user.name` proprietà del sistema), `created` (l&#39;ora attuale del sistema), `requiresRoot` (usare `requiresRoot` parametro da impostare), `packagePath` (generato automaticamente dal nome del gruppo e del pacchetto) |
| `requiresRoot` | `boolean` | Sì | false | Definisce se il pacchetto richiede la radice. Questo diventerà il `requiresRoot` proprietà `properties.xml` file. |
| `subPackages` | `java.util.List` | No | Nessuno |  |
| `version` | `java.lang.String` | Sì | Versione definita nel progetto Maven | Versione del pacchetto di contenuti |
| `workDirectory` | `java.io.File` | Sì | La directory definita nel progetto Maven (fase di creazione) | Directory contenente il contenuto da includere nel pacchetto |

#### Utilizzo dei filtri {#using-filters}

Utilizza l’elemento filters per definire il contenuto del pacchetto. I filtri vengono aggiunti alla variabile `workspaceFilter` nel `META-INF/vault/filter.xml` del pacchetto.

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

La `mode` l’elemento definisce in che modo il contenuto è interessato dall’archivio quando il pacchetto viene importato. È possibile utilizzare i seguenti valori:

* **Unione:** Viene aggiunto il contenuto del pacchetto che non è già presente nell’archivio. Il contenuto presente sia nel pacchetto che nell’archivio rimane invariato. Nessun contenuto viene rimosso dalla directory archivio.
* **Sostituisci:** Il contenuto del pacchetto che non si trova nell’archivio viene aggiunto all’archivio. Il contenuto nell’archivio viene sostituito con il contenuto corrispondente nel pacchetto. Il contenuto viene rimosso dall’archivio quando non esiste nel pacchetto.
* **Aggiorna:** Il contenuto del pacchetto che non si trova nell’archivio viene aggiunto all’archivio. Il contenuto nell’archivio viene sostituito con il contenuto corrispondente nel pacchetto. Il contenuto esistente viene rimosso dalla directory archivio.

Quando il filtro non contiene `mode` elemento, il valore predefinito di `replace` viene utilizzato.

### aiuto {#help}

#### Parametri {#parameters-6}

| Nome | Tipo | Obbligatorio | Valore predefinito | Descrizione |
|---|---|---|---|---|
| `detail` | `boolean` | No | `false` | Determina se visualizzare tutte le proprietà impostabili per ogni obiettivo |
| `goal` | `String` | No | Nessuno | Questi parametri definiscono il nome dell’obiettivo per il quale visualizzare la guida. Se non viene specificato alcun valore, viene visualizzata la guida per tutti gli obiettivi. |
| `indentSize` | `int` | No | `2` | Il numero di spazi da utilizzare per il rientro di ciascun livello (deve essere positivo se definito) |
| `lineLength` | `int` | No | `80` | La lunghezza massima di una linea di visualizzazione (deve essere positiva se definita) |

## Inclusione di un&#39;immagine miniatura o di un file di proprietà nel pacchetto {#including-a-thumbnail-image-or-properties-file-in-the-package}

Sostituisci i file di configurazione del pacchetto predefiniti per personalizzare le proprietà del pacchetto. Ad esempio, includi una miniatura per distinguere il pacchetto in [Gestione pacchetti.](/help/implementing/developing/tools/package-manager.md)

I file di origine possono trovarsi in qualsiasi punto del file system. Nel file POM, definisci le risorse di compilazione per copiare i file di origine nel `target/vault-work/META-INF` da includere nel pacchetto.

Il seguente codice POM aggiunge i file nel `META-INF` cartella dell&#39;origine del progetto nel pacchetto:

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

Il seguente codice POM aggiunge solo un&#39;immagine di miniatura al pacchetto. L’immagine della miniatura deve essere denominata `thumbnail.png`e deve trovarsi nella `META-INF/vault/definition` cartella del pacchetto. In questo esempio, il file di origine si trova nella `/src/main/content/META-INF/vault/definition` cartella del progetto:

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

## Utilizzo dell’Archetipo di progetto AEM per generare progetti AEM {#using-archetypes}

L’ultimo archetipo di progetto AEM implementa la struttura dei pacchetti con le best practice per le implementazioni on-premise e AMS ed è consigliato per tutti i progetti AEM.

>[!TIP]
>
>Per ulteriori dettagli, consulta la sezione [AEM struttura del progetto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) articolo nella documentazione as a Cloud Service AEM nonché [Archetipo di progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) documentazione. Entrambi sono pienamente supportati per AEM 6.5.
