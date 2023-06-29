---
title: Plug-in Maven pacchetto di contenuti Adobe
description: Utilizza il plug-in Maven Content Package per distribuire le applicazioni AEM
exl-id: d631d6df-7507-4752-862b-9094af9759a0
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1838'
ht-degree: 6%

---

# Plug-in Maven pacchetto di contenuti Adobe {#adobe-content-package-maven-plugin}

Utilizza il plug-in Maven Adobe Content Package per integrare le attività di distribuzione e gestione dei pacchetti nei progetti Maven.

La distribuzione dei pacchetti costruiti all’AEM viene eseguita dal plug-in Maven per pacchetti di contenuti Adobi e consente l’automazione delle attività normalmente eseguite con l’AEM [Gestione pacchetti:](/help/implementing/developing/tools/package-manager.md)

* Creare nuovi pacchetti dai file nel file system.
* Installare e disinstallare pacchetti su AEM.
* Creare pacchetti già definiti in AEM.
* Ottieni un elenco dei pacchetti installati su AEM.
* Rimuovere un pacchetto dall’AEM.

Questo documento descrive come utilizzare Maven per gestire queste attività. Tuttavia è anche importante comprendere [la struttura dei progetti AEM e dei relativi pacchetti.](#aem-project-structure)

>[!NOTE]
>
>Pacchetto **creazione** è ora di proprietà di [Plug-in Maven pacchetto Apache Jackrabbit FileVault.](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
>* Il `content-package-maven-plugin` non supporta più la creazione di pacchetti dalla versione 1.0.2.
>* Questo articolo descrive **distribuzione** dei pacchetti costruiti per l’AEM viene eseguito dal plug-in Maven per il pacchetto di contenuti Adobe.

## Pacchetti e struttura del progetto AEM {#aem-project-structure}

AEM as a Cloud Service aderisce alle best practice più recenti per la gestione dei pacchetti e la struttura dei progetti, come implementato dal più recente Archetipo di progetto AEM.

>[!TIP]
>
>Per maggiori dettagli, vedi [Struttura dei progetti AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=it) nella documentazione as a Cloud Service dell&#39;AEM e nella [Archetipo progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) documentazione. Entrambi sono pienamente supportati per AEM 6.5.

## Ottenere il plug-in Maven del pacchetto di contenuti {#obtaining-the-content-package-maven-plugin}

Il plug-in è disponibile da [Archivio centrale Maven.](https://mvnrepository.com/artifact/com.day.jcr.vault/content-package-maven-plugin?repo=adobe-public)

## Obiettivi e parametri del plug-in Maven del pacchetto di contenuti

Per utilizzare il plug-in Maven per pacchetto di contenuti, aggiungi il seguente elemento plug-in all’interno dell’elemento di build del file POM:

```xml
<plugin>
 <groupId>com.day.jcr.vault</groupId>
 <artifactId>content-package-maven-plugin</artifactId>
 <version>1.0.4</version>
 <configuration>
       <!-- parameters and values common to all goals, as required -->
 </configuration>
</plugin>
```

Per consentire a Maven di scaricare il plug-in, utilizza il profilo fornito in [Ottenere il plug-in Maven del pacchetto di contenuti](#obtaining-the-content-package-maven-plugin) in questa pagina.

## Obiettivi del plug-in Maven per pacchetto di contenuti {#goals-of-the-content-package-maven-plugin}

Gli obiettivi e i parametri di obiettivo forniti dal plug-in Pacchetto di contenuti sono descritti nelle sezioni seguenti. I parametri descritti nella sezione Parametri comuni possono essere utilizzati per la maggior parte degli obiettivi. I parametri che si applicano a un obiettivo sono descritti nella sezione relativa a tale obiettivo.

### Prefisso plug-in {#plugin-prefix}

Il prefisso del plug-in è `content-package`. Utilizza questo prefisso per eseguire un obiettivo dalla riga di comando, come nell’esempio seguente:

```shell
mvn content-package:build
```

### Prefisso parametro {#parameter-prefix}

Se non diversamente specificato, gli obiettivi e i parametri del plug-in utilizzano `vault` come nell’esempio seguente:

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

### Proxy {#proxies}

Per gli obiettivi che utilizzano i proxy per l’AEM viene utilizzata la prima configurazione proxy valida trovata nelle impostazioni Maven. Se non viene trovata alcuna configurazione proxy, non viene utilizzato alcun proxy. Consulta la `useProxy` parametro in [Parametri comuni](#common-parameters) sezione.

### Parametri comuni {#common-parameters}

I parametri riportati nella tabella seguente sono comuni a tutti gli obiettivi, tranne quando indicato nella **Obiettivi** colonna.

| Nome | Tipo | Obbligatorio | Valore predefinito | Descrizione | Obiettivi |
|---|---|---|---|---|---|
| `failOnError` | `boolean` | No | `false` | Un valore di `true` causa un errore nella generazione. Un valore di `false` fa in modo che la build ignori l’errore. | Tutti gli obiettivi tranne `package` |
| `name` | `String` | `build`: Sì, `install`: No, `rm`: Sì | `build`: nessun valore predefinito, `install`: il valore della proprietà `artifactId` proprietà del progetto Maven | Nome del pacchetto su cui intervenire | Tutti gli obiettivi tranne `ls` |
| `password` | `String` | Sì | `admin` | Password utilizzata per l’autenticazione con AEM | Tutti gli obiettivi tranne `package` |
| `serverId` | `String` | No | ID server da cui recuperare il nome utente e la password per l&#39;autenticazione | Tutti gli obiettivi tranne `package` |
| `targetURL` | `String` | Sì | `http://localhost:4502/crx/packmgr/service.jsp` | URL dell’API del servizio HTTP del gestore di pacchetti AEM | Tutti gli obiettivi tranne `package` |
| `timeout` | `int` | No | `5` | Timeout di connessione per la comunicazione con il servizio Gestione pacchetti, in secondi | Tutti gli obiettivi tranne `package` |
| `useProxy` | `boolean` | No | `true` | Un valore di `true` fa in modo che Maven utilizzi la prima configurazione proxy attiva trovata per le richieste proxy al Gestione pacchetti. | Tutti gli obiettivi tranne `package` |
| `userId` | `String` | Sì | `admin` | Nome utente da autenticare con AEM | Tutti gli obiettivi tranne `package` |
| `verbose` | `boolean` | No | `false` | Abilita o disabilita la registrazione dettagliata | Tutti gli obiettivi tranne `package` |

### build {#build}

Genera un pacchetto di contenuti già definito in un’istanza AEM.

>[!NOTE]
>
>Questo obiettivo non deve essere eseguito all’interno di un progetto Maven.

#### Parametri {#parameters}

Tutti i parametri per l’obiettivo di build sono descritti in [Parametri comuni](#common-parameters) sezione.

### installare {#install}

Installa un pacchetto nel repository. L’esecuzione di questo obiettivo non richiede un progetto Maven. L’obiettivo è associato a `install` fase del ciclo di vita della build Maven.

#### Parametri {#parameters-1}

Oltre ai seguenti parametri, consulta le descrizioni in [Parametri comuni](#common-parameters) sezione.

| Nome | Tipo | Obbligatorio | Valore predefinito | Descrizione |
|---|---|---|---|---|
| `artifact` | `String` | No | Il valore della proprietà `artifactId` proprietà del progetto Maven | Una stringa del modulo `groupId:artifactId:version[:packaging]` |
| `artifactId` | `String` | No | Nessuno | ID dell’artefatto da installare |
| `groupId` | `String` | No | Nessuno | Il `groupId` dell’artefatto da installare |
| `install` | `boolean` | No | `true` | Determina se decomprimere automaticamente il pacchetto quando viene caricato |
| `localRepository` | `org.apache.maven.artifact.repository.ArtifactRepository` | No | Il valore della proprietà `localRepository` variabile di sistema | L’archivio Maven locale che non può essere configurato utilizzando la configurazione del plug-in in quanto viene sempre utilizzata la proprietà di sistema |
| `packageFile` | `java.io.File` | No | L’artefatto principale definito per il progetto Maven | Nome del file del pacchetto da installare |
| `packaging` | `String` | No | `zip` | Tipo di pacchetto dell&#39;artefatto da installare |
| `pomRemoteRepositories` | `java.util.List` | Sì | Il valore della proprietà `remoteArtifactRepositories` proprietà definita per il progetto Maven | Questo valore non può essere configurato utilizzando la configurazione del plug-in e deve essere specificato nel progetto. |
| `project` | `org.apache.maven.project.MavenProject` | Sì | Progetto per il quale è configurato il plug-in | Il progetto Maven che è implicito perché il progetto contiene la configurazione del plug-in. |
| `repositoryId` (POM) `repoID` (riga di comando) | `String` | No | `temp` | ID dell’archivio da cui viene recuperato l’artefatto |
| `repositoryUrl` (POM) `repoURL` (riga di comando) | `String` | No | Nessuno | URL dell’archivio da cui viene recuperato l’artefatto |
| version | Stringa | No | Nessuno | Versione dell&#39;artefatto da installare |

### ls {#ls}

Elenca i pacchetti distribuiti in [Gestione pacchetti](/help/implementing/developing/tools/package-manager.md).

#### Parametri {#parameters-2}

Tutti i parametri dell’obiettivo ls sono descritti in [Parametri comuni](#common-parameters) sezione.

### rm {#rm}

Rimuove un pacchetto da [Gestione pacchetti](/help/implementing/developing/tools/package-manager.md).

#### Parametri {#parameters-3}

Tutti i parametri dell&#39;obiettivo rm sono descritti nel [Parametri comuni](#common-parameters) sezione.

### disinstalla {#uninstall}

Disinstalla un pacchetto. Il pacchetto rimane nel server nello stato disinstallato.

#### Parametri {#parameters-4}

Tutti i parametri dell&#39;obiettivo di disinstallazione sono descritti in [Parametri comuni](#common-parameters) sezione.

### pacchetto {#package}

Crea un pacchetto di contenuti. La configurazione predefinita dell&#39;obiettivo del pacchetto include il contenuto della directory in cui vengono salvati i file compilati. L’esecuzione dell’obiettivo del pacchetto richiede che la fase di compilazione della build sia stata completata. L’obiettivo del pacchetto è associato alla fase del pacchetto del ciclo di vita della build Maven.

#### Parametri {#parameters-5}

Oltre ai seguenti parametri, consulta la descrizione della `name` parametro in [Parametri comuni](#common-parameters) sezione.

| Nome | Tipo | Obbligatorio | Valore predefinito | Descrizione |
|---|---|---|---|---|
| `archive` | `org.apache.maven.archiver.MavenArchiveConfiguration` | No | Nessuno | Configurazione archivio da utilizzare |
| `builtContentDirectory` | `java.io.File` | Sì | Valore della directory di output della build Maven | Directory contenente il contenuto da includere nel pacchetto |
| `dependencies` | `java.util.List` | No | Nessuno |  |
| `embeddedTarget` | `java.lang.String` | No | Nessuno |  |
| `embeddeds` | `java.util.List` | No | Nessuno |  |
| `failOnMissingEmbed` | `boolean` | Sì | `false` | Un valore di `true` genera un errore di compilazione quando un artefatto incorporato non viene trovato nelle dipendenze del progetto. Un valore di `false` fa in modo che la build ignori tali errori. |
| `filterSource` | `java.io.File` | No | Nessuno | Questo parametro definisce un file che specifica l&#39;origine del filtro del workspace. I filtri specificati nella configurazione e inseriti tramite incorporamenti o pacchetti secondari vengono uniti al contenuto del file. |
| `filters` | `com.day.jcr.vault.maven.pack.impl.DefaultWorkspaceFilter` | No | Nessuno | Questo parametro contiene elementi filtro che definiscono il contenuto del pacchetto. Quando vengono eseguiti, i filtri vengono inclusi nel `filter.xml` file. Consulta la [Utilizzo dei filtri](#using-filters) sezione successiva. |
| `finalName` | `java.lang.String` | Sì | Il `finalName` definito nel progetto Maven (fase di build) | Il nome del file ZIP del pacchetto generato, senza `.zip` estensione file |
| `group` | `java.lang.String` | Sì | Il `groupID` definito nel progetto Maven | Il `groupId` del pacchetto di contenuti generato che fa parte del percorso di installazione di destinazione per il pacchetto di contenuti |
| `outputDirectory` | `java.io.File` | Sì | La directory di build definita nel progetto Maven | Directory locale in cui viene salvato il pacchetto di contenuti |
| `prefix` | `java.lang.String` | No | Nessuno |  |
| `project` | `org.apache.maven.project.MavenProject` | Sì | Nessuno | Il progetto Maven |
| `properties` | `java.util.Map` | No | Nessuno | Questi parametri definiscono proprietà aggiuntive che è possibile impostare in `properties.xml` file. Queste proprietà non possono sovrascrivere le seguenti proprietà predefinite: `group` (utilizzare `group` parametro da impostare), `name` (utilizzare `name` parametro da impostare), `version` (utilizzare `version` parametro da impostare), `description` (ricavato dalla descrizione del progetto), `groupId` (`groupId` del descrittore di progetto Maven), `artifactId` (`artifactId` del descrittore di progetto Maven), `dependencies` (utilizzare `dependencies` parametro da impostare), `createdBy` (il valore del `user.name` proprietà di sistema), `created` (l&#39;ora di sistema corrente), `requiresRoot` (utilizzare `requiresRoot` parametro da impostare), `packagePath` (generato automaticamente dal nome del gruppo e del pacchetto) |
| `requiresRoot` | `boolean` | Sì | false | Definisce se il pacchetto richiede la radice. Diventa il `requiresRoot` proprietà del `properties.xml` file. |
| `subPackages` | `java.util.List` | No | Nessuno |  |
| `version` | `java.lang.String` | Sì | Versione definita nel progetto Maven | Versione del pacchetto di contenuti |
| `workDirectory` | `java.io.File` | Sì | La directory definita nel progetto Maven (fase di build) | Directory contenente il contenuto da includere nel pacchetto |

#### Utilizzo dei filtri {#using-filters}

Utilizza l’elemento filters per definire il contenuto del pacchetto. I filtri vengono aggiunti al `workspaceFilter` elemento nel `META-INF/vault/filter.xml` del pacchetto.

Nell&#39;esempio di filtro seguente viene illustrata la struttura XML da utilizzare:

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

Il `mode` definisce il modo in cui il contenuto viene influenzato dall’archivio quando il pacchetto viene importato. È possibile utilizzare i seguenti valori:

* **Unisci:** Vengono aggiunti contenuti nel pacchetto che non sono già presenti nell’archivio. Il contenuto presente sia nel pacchetto che nell’archivio rimane invariato. Nessun contenuto viene rimosso dall’archivio.
* **Sostituisci:** Il contenuto del pacchetto non presente nell’archivio viene aggiunto all’archivio. Il contenuto nell’archivio viene sostituito con il contenuto corrispondente nel pacchetto. Il contenuto viene rimosso dall’archivio quando non esiste nel pacchetto.
* **Aggiorna:** Il contenuto del pacchetto non presente nell’archivio viene aggiunto all’archivio. Il contenuto nell’archivio viene sostituito con il contenuto corrispondente nel pacchetto.

Se il filtro non contiene `mode` , il valore predefinito di `replace` viene utilizzato.

### Aiuto di  {#help}

#### Parametri {#parameters-6}

| Nome | Tipo | Obbligatorio | Valore predefinito | Descrizione |
|---|---|---|---|---|
| `detail` | `boolean` | No | `false` | Determina se visualizzare tutte le proprietà impostabili per ogni obiettivo |
| `goal` | `String` | No | Nessuno | Questi parametri definiscono il nome dell’obiettivo per il quale visualizzare la guida. Se non viene specificato alcun valore, viene visualizzata la guida per tutti gli obiettivi. |
| `indentSize` | `int` | No | `2` | Numero di spazi da utilizzare per il rientro di ciascun livello (se definito, deve essere positivo) |
| `lineLength` | `int` | No | `80` | Lunghezza massima di una linea di visualizzazione (deve essere positiva se definita) |

## Inclusione di un&#39;immagine di anteprima o di un file delle proprietà nel pacchetto {#including-a-thumbnail-image-or-properties-file-in-the-package}

Sostituire i file di configurazione del pacchetto predefiniti per personalizzare le proprietà del pacchetto. Ad esempio, includi una miniatura per distinguere il pacchetto in [Gestione pacchetti](/help/implementing/developing/tools/package-manager.md).

I file di origine possono trovarsi in qualsiasi punto del file system. Nel file POM, definisci le risorse di build per copiare i file sorgente in `target/vault-work/META-INF` da includere nel pacchetto.

Il codice POM seguente aggiunge i file nel `META-INF` cartella dell&#39;origine del progetto nel pacchetto:

```xml
<build>
    <resources>
        <!-- vault META-INF resources (thumbnail and so on) -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF</directory>
            <targetPath>../vault-work/META-INF</targetPath>
        </resource>
    </resources>
</build>
```

Il codice POM seguente aggiunge al pacchetto solo un&#39;immagine in miniatura. L&#39;immagine di anteprima deve essere denominata `thumbnail.png`, e deve trovarsi nel `META-INF/vault/definition` cartella del pacchetto. In questo esempio, il file di origine si trova nel `/src/main/content/META-INF/vault/definition` cartella del progetto:

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

## Utilizzo dell’archetipo del progetto AEM per generare progetti AEM {#using-archetypes}

L’archetipo del progetto AEM più recente implementa la struttura di pacchetti di best practice sia per le implementazioni on-premise che per quelle AMS ed è consigliato per tutti i progetti AEM.

>[!TIP]
>
>Per maggiori dettagli, vedi [Struttura dei progetti AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=it) nella documentazione as a Cloud Service dell&#39;AEM e nella [Archetipo progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) documentazione. Entrambi sono pienamente supportati per AEM 6.5.
