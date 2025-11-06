---
title: Plug-in Maven pacchetto contenuti Adobe
description: Utilizza il plug-in Maven Content Package per distribuire le applicazioni AEM.
exl-id: d631d6df-7507-4752-862b-9094af9759a0
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 4%

---

# Plug-in Maven pacchetto contenuti Adobe {#adobe-content-package-maven-plugin}

Utilizza il plug-in Adobe Content Package Maven per integrare le attività di distribuzione e gestione dei pacchetti nei progetti Maven.

La distribuzione dei pacchetti costruiti in AEM viene eseguita dal plug-in Maven di Adobe Content Package e consente l&#39;automazione delle attività normalmente eseguite con AEM [Gestione pacchetti](/help/implementing/developing/tools/package-manager.md)

* Creare nuovi pacchetti dai file nel file system.
* Installare e disinstallare pacchetti su AEM.
* Genera pacchetti già definiti in AEM.
* Ottieni un elenco dei pacchetti installati in AEM.
* Rimuovere un pacchetto da AEM.

Questo documento descrive come utilizzare Maven per gestire queste attività. Tuttavia è anche importante comprendere [la struttura dei progetti AEM e dei relativi pacchetti](#aem-project-structure).

>[!NOTE]
>
>Utilizza sempre le versioni più recenti di questi plug-in.

>[!NOTE]
>
>Il pacchetto **creation** è ora di proprietà del [plug-in Apache Jackrabbit FileVault Package Maven](https://jackrabbit.apache.org/filevault-package-maven-plugin/).
>
>Questo articolo descrive la **distribuzione** dei pacchetti costruiti in AEM come eseguito dal plug-in Maven del pacchetto di contenuti di Adobe.

## Pacchetti e struttura del progetto AEM {#aem-project-structure}

AEM as a Cloud Service aderisce alle best practice più recenti per la gestione dei pacchetti e la struttura del progetto, come implementato dal più recente Archetipo progetto AEM.

>[!TIP]
>
>Consulta l&#39;articolo [Struttura del progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=it) nella documentazione di AEM as a Cloud Service e la documentazione [Archetipo del progetto AEM](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/developing/archetype/overview). Entrambi sono completamente supportati per AEM 6.5.

## Ottenere il plug-in Maven del pacchetto di contenuti {#obtaining-the-content-package-maven-plugin}

Il plug-in è disponibile dall&#39;[archivio centrale Maven](https://mvnrepository.com/artifact/com.day.jcr.vault/content-package-maven-plugin?repo=adobe-public).

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

Per consentire a Maven di scaricare il plug-in, utilizza il profilo fornito nella sezione [Ottenere il plug-in Maven del pacchetto di contenuti](#obtaining-the-content-package-maven-plugin) in questa pagina.

## Obiettivi del plug-in Maven per pacchetto di contenuti {#goals-of-the-content-package-maven-plugin}

Gli obiettivi e i parametri di obiettivo forniti dal plug-in Pacchetto di contenuti sono descritti nelle sezioni seguenti. I parametri descritti nella sezione Parametri comuni possono essere utilizzati per la maggior parte degli obiettivi. I parametri che si applicano a un obiettivo sono descritti nella sezione relativa a tale obiettivo.

### Prefisso plug-in {#plugin-prefix}

Il prefisso del plug-in è `content-package`. Utilizza questo prefisso per eseguire un obiettivo dalla riga di comando, come nell’esempio seguente:

```shell
mvn content-package:build
```

### Prefisso parametro {#parameter-prefix}

Se non diversamente specificato, gli obiettivi e i parametri del plug-in utilizzano il prefisso `vault`, come nell&#39;esempio seguente:

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

### Proxy {#proxies}

Per gli obiettivi che utilizzano i proxy per AEM, viene utilizzata la prima configurazione proxy valida trovata nelle impostazioni Maven. Se non viene trovata alcuna configurazione proxy, non viene utilizzato alcun proxy. Vedi il parametro `useProxy` nella sezione [Parametri comuni](#common-parameters).

### Parametri comuni {#common-parameters}

I parametri nella tabella seguente sono comuni a tutti gli obiettivi, tranne quando indicato nella colonna **Obiettivi**.

| Nome | Tipo | Obbligatorio | Valore predefinito | Descrizione | Obiettivi |
|---|---|---|---|---|---|
| `failOnError` | `boolean` | No | `false` | Un valore di `true` causa un errore di compilazione. Il valore `false` fa sì che la build ignori l&#39;errore. | Tutti gli obiettivi tranne `package` |
| `name` | `String` | `build`: Sì, `install`: No, `rm`: Sì | `build`: nessun valore predefinito, `install`: il valore della proprietà `artifactId` del progetto Maven | Nome del pacchetto su cui intervenire | Tutti gli obiettivi tranne `ls` |
| `password` | `String` | Sì | `admin` | Password utilizzata per l’autenticazione con AEM | Tutti gli obiettivi tranne `package` |
| `serverId` | `String` | No | ID server da cui recuperare il nome utente e la password per l&#39;autenticazione | Tutti gli obiettivi tranne `package` |
| `targetURL` | `String` | Sì | `http://localhost:4502/crx/packmgr/service.jsp` | URL dell’API del servizio HTTP del gestore pacchetti di AEM | Tutti gli obiettivi tranne `package` |
| `timeout` | `int` | No | `5` | Timeout di connessione per la comunicazione con il servizio Gestione pacchetti, in secondi | Tutti gli obiettivi tranne `package` |
| `useProxy` | `boolean` | No | `true` | Il valore `true` fa in modo che Maven utilizzi la prima configurazione proxy attiva trovata per le richieste proxy al gestore di pacchetti. | Tutti gli obiettivi tranne `package` |
| `userId` | `String` | Sì | `admin` | Nome utente da autenticare con AEM | Tutti gli obiettivi tranne `package` |
| `verbose` | `boolean` | No | `false` | Abilita o disabilita la registrazione dettagliata | Tutti gli obiettivi tranne `package` |

### build {#build}

Genera un pacchetto di contenuti già definito in un’istanza di AEM.

>[!NOTE]
>
>Questo obiettivo non deve essere eseguito all’interno di un progetto Maven.

#### Parametri {#parameters}

Tutti i parametri per l&#39;obiettivo di compilazione sono descritti nella sezione [Parametri comuni](#common-parameters).

### installare {#install}

Installa un pacchetto nel repository. L’esecuzione di questo obiettivo non richiede un progetto Maven. L&#39;obiettivo è associato alla fase `install` del ciclo di vita della build Maven.

#### Parametri {#parameters-1}

Oltre ai seguenti parametri, vedere le descrizioni nella sezione [Parametri comuni](#common-parameters).

| Nome | Tipo | Obbligatorio | Valore predefinito | Descrizione |
|---|---|---|---|---|
| `artifact` | `String` | No | Valore della proprietà `artifactId` del progetto Maven | Una stringa del modulo `groupId:artifactId:version[:packaging]` |
| `artifactId` | `String` | No | Nessuna | ID dell’artefatto da installare |
| `groupId` | `String` | No | Nessuna | `groupId` dell&#39;artefatto da installare |
| `install` | `boolean` | No | `true` | Determina se decomprimere automaticamente il pacchetto quando viene caricato |
| `localRepository` | `org.apache.maven.artifact.repository.ArtifactRepository` | No | Valore della variabile di sistema `localRepository` | L’archivio Maven locale che non può essere configurato utilizzando la configurazione del plug-in in quanto viene sempre utilizzata la proprietà di sistema |
| `packageFile` | `java.io.File` | No | L’artefatto principale definito per il progetto Maven | Nome del file del pacchetto da installare |
| `packaging` | `String` | No | `zip` | Tipo di pacchetto dell&#39;artefatto da installare |
| `pomRemoteRepositories` | `java.util.List` | Sì | Valore della proprietà `remoteArtifactRepositories` definita per il progetto Maven | Questo valore non può essere configurato utilizzando la configurazione del plug-in e deve essere specificato nel progetto. |
| `project` | `org.apache.maven.project.MavenProject` | Sì | Progetto per il quale è configurato il plug-in | Il progetto Maven che è implicito perché il progetto contiene la configurazione del plug-in. |
| `repositoryId` (POM), `repoID` (riga di comando) | `String` | No | `temp` | ID dell’archivio da cui viene recuperato l’artefatto |
| `repositoryUrl` (POM), `repoURL` (riga di comando) | `String` | No | Nessuna | URL dell’archivio da cui viene recuperato l’artefatto |
| version | Stringa | No | Nessuna | Versione dell&#39;artefatto da installare |

### ls {#ls}

Elenca i pacchetti distribuiti in [Gestione pacchetti](/help/implementing/developing/tools/package-manager.md).

#### Parametri {#parameters-2}

Tutti i parametri dell&#39;obiettivo ls sono descritti nella sezione [Parametri comuni](#common-parameters).

### rm {#rm}

Rimuove un pacchetto da [Gestione pacchetti](/help/implementing/developing/tools/package-manager.md).

#### Parametri {#parameters-3}

Tutti i parametri dell&#39;obiettivo rm sono descritti nella sezione [Parametri comuni](#common-parameters).

### disinstalla {#uninstall}

Disinstalla un pacchetto. Il pacchetto rimane nel server nello stato disinstallato.

#### Parametri {#parameters-4}

Tutti i parametri dell&#39;obiettivo di disinstallazione sono descritti nella sezione [Parametri comuni](#common-parameters).


### aiuto {#help}

#### Parametri {#parameters-6}

| Nome | Tipo | Obbligatorio | Valore predefinito | Descrizione |
|---|---|---|---|---|
| `detail` | `boolean` | No | `false` | Determina se visualizzare tutte le proprietà impostabili per ogni obiettivo |
| `goal` | `String` | No | Nessuna | Questi parametri definiscono il nome dell’obiettivo per il quale visualizzare la guida. Se non viene specificato alcun valore, viene visualizzata la guida per tutti gli obiettivi. |
| `indentSize` | `int` | No | `2` | Numero di spazi da utilizzare per il rientro di ciascun livello (se definito, deve essere positivo) |
| `lineLength` | `int` | No | `80` | Lunghezza massima di una linea di visualizzazione (deve essere positiva se definita) |

## Inclusione di un&#39;immagine di anteprima o di un file delle proprietà nel pacchetto {#including-a-thumbnail-image-or-properties-file-in-the-package}

Sostituire i file di configurazione del pacchetto predefiniti per personalizzare le proprietà del pacchetto. Ad esempio, includere un&#39;immagine di anteprima per distinguere il pacchetto in [Gestione pacchetti](/help/implementing/developing/tools/package-manager.md).

I file di origine possono trovarsi in qualsiasi punto del file system. Nel file POM, definire le risorse di compilazione per copiare i file di origine in `target/vault-work/META-INF` per l&#39;inclusione nel pacchetto.

Il codice POM seguente aggiunge i file nella cartella `META-INF` dell&#39;origine del progetto al pacchetto:

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

Il codice POM seguente aggiunge al pacchetto solo un&#39;immagine in miniatura. L&#39;immagine miniatura deve essere denominata `thumbnail.png` e deve trovarsi nella cartella `META-INF/vault/definition` del pacchetto. In questo esempio, il file di origine si trova nella cartella `/src/main/content/META-INF/vault/definition` del progetto:

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

## Utilizzo di Archetipo progetto AEM per generare progetti AEM {#using-archetypes}

La versione più recente di Archetipo progetto AEM implementa la struttura di pacchetti basata su best practice per le implementazioni on-premise e AMS ed è consigliata per tutti i progetti AEM.

>[!TIP]
>
>Consulta l&#39;articolo [Struttura del progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html?lang=it) nella documentazione di AEM as a Cloud Service e la documentazione [Archetipo del progetto AEM](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/developing/archetype/overview). Entrambi sono completamente supportati per AEM 6.5.
