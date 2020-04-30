---
title: Struttura dei progetti AEM
description: Scopri come definire le strutture dei pacchetti per la distribuzione in Adobe Experience Manager Cloud Service.
translation-type: tm+mt
source-git-commit: ae04553b17fcb7b9660f709565faed791a0c930e

---


# Struttura dei progetti AEM

>[!TIP]
>
>Acquisisci familiarità con l&#39;utilizzo [di base di Project Archetype di](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/archetype/overview.html)AEM e con il plug-in [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/vlt-mavenplugin.html) FileVault Content Maven, man mano che questo articolo si basa su tali informazioni e concetti.

Questo articolo illustra le modifiche necessarie ai progetti Adobe Experience Manager Maven per essere compatibili con il servizio AEM Cloud, garantendo che rispettino la suddivisione di contenuti modificabili e immutabili; che siano stabilite dipendenze necessarie per creare distribuzioni deterministiche non conflittuali; e che siano raggruppati in una struttura distribuibile.

Le distribuzioni di applicazioni AEM devono essere composte da un unico pacchetto AEM. Questo pacchetto deve contenere a sua volta sottopacchetti che comprendono tutto ciò che l&#39;applicazione richiede per funzionare, compreso il codice, la configurazione e qualsiasi contenuto di base di supporto.

AEM richiede una separazione di **contenuto** e **codice**, il che significa che un singolo pacchetto di contenuti **non può** essere distribuito **sia** su `/apps` che su aree scrivibili di runtime dell’archivio (ad esempio `/content`, `/conf`, `/home` o tutto il resto fuorché `/apps`). Al contrario, l’applicazione deve separare codice e contenuto in pacchetti discreti da distribuire in AEM.

La struttura del pacchetto descritta in questo documento è compatibile **sia** con le distribuzioni di sviluppo locali che con le distribuzioni di AEM Cloud Service.

>[!TIP]
>
>Le configurazioni descritte in questo documento sono fornite da [AEM Project Maven Archetype 21 o versione successiva](https://github.com/adobe/aem-project-archetype/releases).

## Aree variabile e immutabili del repository {#mutable-vs-immutable}

`/apps` e `/libs` sono considerate aree **immutabili** di AEM poiché non possono essere modificate (create, aggiornate, eliminate) dopo l’avvio di AEM (ad es. in fase di runtime). Qualsiasi tentativo di modifica di un’area immutabile in fase di runtime avrà esito negativo.

Tutto il resto nella directory archivio, `/content`, `/conf`, `/var`, `/etc`, `/oak:index`, `/system`, `/tmp`ecc. sono tutte aree **mutabili** , ovvero possono essere modificate in fase di esecuzione.

>[!WARNING]
>
> Come nelle versioni precedenti di AEM, non `/libs` deve essere modificato. Solo il codice prodotto AEM può essere distribuito a `/libs`.

## Struttura pacchetto consigliata {#recommended-package-structure}

![Struttura del pacchetto di progetti Experience Manager](assets/content-package-organization.png)

Questo diagramma fornisce una panoramica della struttura di progetto consigliata e degli artifact di distribuzione del pacchetto.

La struttura di distribuzione dell&#39;applicazione consigliata è la seguente:

+ Il `ui.apps` pacchetto, o pacchetto di codice, contiene tutto il codice da distribuire e da distribuire solo a `/apps`. Gli elementi comuni del `ui.apps` pacchetto includono, tra l&#39;altro:
   + Pacchetti OSGi
      + `/apps/my-app/install`
   + Configurazioni OSGi
      + `/apps/my-app/config`
   + Script HTL
      + `/apps/my-app/components`
   + JavaScript e CSS (tramite librerie client)
      + `/apps/my-app/clientlibs`
   + Sovrapposizioni di /libs
      + `/apps/cq`, `/apps/dam/`, etc.
   + Configurazioni basate sul contesto di fallback
      + `/apps/settings`
   + ACL (autorizzazioni)
      + Qualsiasi `rep:policy` percorso in `/apps`
   + Direttive di configurazione di Repo Init OSGi (e script di accompagnamento)
      + [Repo Init](#repo-init) è il metodo consigliato per distribuire (modificabile) contenuto che fa parte logicamente dell’applicazione AEM. Repo Init deve essere utilizzato per definire:
         + Strutture contenuto di base
            + `/conf/my-app`
            + `/content/my-app`
            + `/content/dam/my-app`
         + Utenti
         + Utenti del servizio
         + Gruppi
         + ACL (autorizzazioni)
            + Qualsiasi `rep:policy` per qualsiasi percorso (mutabile o immutabile)
+ Il `ui.apps` pacchetto, o pacchetto di codice, contiene tutto il codice da distribuire e da distribuire solo a `/apps`. Gli elementi comuni del `ui.apps` pacchetto includono, tra l&#39;altro: <!-- GRANITE-29128 -->
   + Configurazioni basate sul contesto
      + `/conf`
   + Strutture di contenuto complesse e necessarie (ad esempio Compilazione del contenuto che si basa e si estende oltre le strutture di contenuto della linea di base definite in Repo Init.
      + `/content`, `/content/dam`, etc.
   + Tassonomie di tag gestite
      + `/content/cq:tags`
   + Indici Oak
      + `/oak:index`
   + Etc nodi legacy
      + `/etc`
+ Il pacchetto contenitore `all` include SOLO i pacchetti `ui.apps` e `ui.content` come incorporamenti. Il pacchetto `all` non deve avere **alcun contenuto** proprio, ma deve delegare l’intera distribuzione all’archivio ai relativi pacchetti secondari.

   I pacchetti ora sono inclusi utilizzando la configurazione [incorporata del plug-in Maven](#embeddeds)FileVault, anziché la `<subPackages>` configurazione.

   Per implementazioni complesse di Experience Manager, potrebbe essere utile creare più `ui.apps` progetti/pacchetti e `ui.content` pacchetti che rappresentano siti o tenant specifici in AEM. In questo caso, accertatevi che la divisione tra contenuto variabile e immutabile sia rispettata, e che i pacchetti di contenuto richiesti vengano aggiunti come pacchetti secondari nel pacchetto di contenuto `all` contenitore.

   Ad esempio, una struttura complessa di pacchetti di contenuto di distribuzione potrebbe avere l&#39;aspetto seguente:

   + `all` il pacchetto di contenuti incorpora i pacchetti seguenti, per creare un artefatto di distribuzione unico
      + `ui.apps.common` distribuisce il codice richiesto **sia** dal sito A che dal sito B
      + `ui.apps.site-a` distribuisce il codice richiesto dal sito A
      + `ui.content.site-a` distribuisce il contenuto e la configurazione richiesti dal sito A
      + `ui.apps.site-b` distribuisce il codice richiesto dal sito B
      + `ui.content.site-b` distribuisce il contenuto e la configurazione richiesti dal sito B

## Tipi di pacchetti {#package-types}

I pacchetti devono essere contrassegnati con il tipo di pacchetto dichiarato.

+ I pacchetti contenitore non devono avere un `packageType` set.
+ I pacchetti di codice (immutabili) devono impostare `packageType` su `application`.
+ I pacchetti di contenuto (modificabili) devono impostare `packageType` su `content`.

Per ulteriori informazioni vedere [Apache Jackrabbit FileVault - Package Maven Plugin documentazione](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType) e lo snippet di configurazione [FileVault Maven](#marking-packages-for-deployment-by-adoube-cloud-manager) di seguito.

>[!TIP]
>
>Per un frammento completo, consulta la sezione Snippet [XML](#xml-package-types) POM di seguito.

## Contrassegnazione dei pacchetti per la distribuzione da parte di Adobe Cloud Manager {#marking-packages-for-deployment-by-adoube-cloud-manager}

Per impostazione predefinita, Adobe Cloud Manager raccoglie tutti i pacchetti prodotti dalla build Maven. Tuttavia, poiché il pacchetto contenitore (`all`) è l’unico artefatto di distribuzione che contiene tutti i pacchetti di codice e contenuto, è necessario assicurarsi che sia distribuito **solo** il pacchetto contenitore (`all`). Per questo motivo, gli altri pacchetti generati dalla build Maven devono essere contrassegnati con la configurazione FileVault Content Package Maven Plug-In di `<properties><cloudManagerTarget>none</cloudManageTarget></properties>`.

>[!TIP]
>
>Per un frammento completo, consulta la sezione Snippet [XML](#pom-xml-snippets) POM di seguito.

## Repo Init{#repo-init}

Repo Init fornisce istruzioni, o script, che definiscono le strutture JCR, che vanno dalle strutture nodo comuni come le strutture delle cartelle, agli utenti, agli utenti del servizio, ai gruppi e alla definizione ACL.

I vantaggi principali di Repo Init sono i permessi impliciti per eseguire tutte le azioni definite dai loro script, e vengono richiamati in anticipo nel ciclo di vita della distribuzione, garantendo che tutte le strutture JCR necessarie siano presenti dal codice temporale.

Mentre gli script Repo Init stessi vivono nel `ui.apps` progetto come script, possono e devono essere utilizzati per definire le seguenti strutture modificabili:

+ Strutture contenuto di base
   + Examples: `/content/my-app`, `/content/dam/my-app`, `/conf/my-app/settings`
+ Utenti del servizio
+ Utenti
+ Gruppi
+ ACL

Gli script Repo Init sono memorizzati come `scripts` voci delle configurazioni di fabbrica `RepositoryInitializer` OSGi e possono quindi essere implicitamente indirizzati dalla modalità di esecuzione, consentendo differenze tra gli script Repo Init di AEM Author e AEM Publish Services o persino tra Envs (Dev, Stage e Prod).

Tenete presente che quando definite Utenti e Gruppi, solo i gruppi sono considerati parte dell’applicazione e che la funzione integrata deve essere definita qui. Gli utenti e i gruppi dell&#39;organizzazione devono essere ancora definiti in fase di runtime in AEM; ad esempio, se un flusso di lavoro personalizzato assegna il lavoro a un gruppo denominato, tale gruppo deve essere definito in tramite Repo Init nell’applicazione AEM, tuttavia se il gruppo è semplicemente di tipo organizzativo, ad esempio &quot;Il team di Wendy&quot; e &quot;Il team di Sean&quot;, questi sono definiti e gestiti al momento dell’esecuzione in AEM.

>[!TIP]
>
>Gli script Repo Init *devono* essere definiti nel campo in linea `scripts` , e la `references` configurazione non funzionerà.

Il vocabolario completo per gli script Repo Init è disponibile nella documentazione [di](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language)Apache Sling Repo Init.

>[!TIP]
>
>Per un frammento completo, consulta la sezione [Repo Init Snippet](#snippet-repo-init) di seguito.

## Pacchetto struttura archivio {#repository-structure-package}

I pacchetti di codice richiedono la configurazione del plug-in FileVault Maven per fare riferimento a una configurazione `<repositoryStructurePackage>` che applica la correttezza delle dipendenze strutturali (per garantire che un pacchetto di codice non venga installato su un altro). Potete [creare un pacchetto di struttura del repository personalizzato per il progetto](repository-structure-package.md).

Questa operazione è **richiesta solo** per i pacchetti codice, ovvero per tutti i pacchetti contrassegnati con `<packageType>application</packageType>`.

Per informazioni su come creare un pacchetto di struttura del repository per l&#39;applicazione, vedere [Sviluppo di un pacchetto](repository-structure-package.md)di struttura del repository.

I pacchetti di contenuto (`<packageType>content</packageType>`) **non** richiedono questo pacchetto struttura archivio.

>[!TIP]
>
>Per un frammento completo, consulta la sezione Snippet [XML](#xml-repository-structure-package) POM di seguito.

## Incorporazione di pacchetti secondari nel pacchetto contenitore{#embeddeds}

I pacchetti di contenuto o codice vengono inseriti in una speciale cartella &quot;side-car&quot; e possono essere installati sia sull&#39;autore AEM che sulla pubblicazione AEM, o su entrambi, utilizzando la `<embeddeds>` configurazione del plug-in FileVault Maven. Notate che la `<subPackages>` configurazione non deve essere utilizzata.

I casi d’uso più comuni includono:

+ ACL/autorizzazioni che differiscono tra gli utenti di AEM Author e gli utenti di AEM Publish
+ Configurazioni utilizzate per supportare attività solo su autori AEM
+ Codice come le integrazioni con i sistemi di back-office, richiesto solo per l’esecuzione su AEM Author

![Incorporazione di pacchetti](assets/embeddeds.png)

Per l’authoring AEM, la pubblicazione AEM o entrambi, il pacchetto è incorporato nel pacchetto `all` contenitore in una cartella speciale, nel seguente formato:

`/apps/<app-name>-packages/(content|application)/install(.author|.publish)?`

Suddividere la struttura delle cartelle in base a:

+ La cartella di primo livello **deve essere** `/apps`.
+ La cartella di secondo livello rappresenta l’applicazione con `-packages` post-fisso sul nome della cartella. Spesso esiste una sola cartella di 2° livello in cui sono incorporati tutti i pacchetti secondari, tuttavia è possibile creare un numero qualsiasi di cartelle di 2° livello per rappresentare al meglio la struttura logica dell&#39;applicazione:
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`
   >[!WARNING]
   >
   >Per convenzione, le cartelle incorporate in un pacchetto secondario sono denominate con il suffisso `-packages`. In questo modo, il codice di distribuzione e i pacchetti di contenuto **non** vengono distribuiti nelle cartelle di destinazione di qualsiasi pacchetto secondario `/apps/<app-name>/...`, il che provoca un comportamento di installazione distruttivo e ciclico.

+ La cartella di terzo livello deve essere
   `application` o `content`
   + La `application` cartella contiene pacchetti di codice
   + La `content` cartella balla i pacchetti di contenutoQuesto nome di cartella deve corrispondere ai tipi [di](#package-types) pacchetto dei pacchetti che contiene.
+ La cartella di quarto livello contiene i pacchetti secondari e deve corrispondere a una delle seguenti:
   + `install` per effettuare l’installazione **sia su** AEM Author che AEM Publish
   + `install.author` per eseguire l’installazione **solo** su AEM Author
   + `install.publish` per eseguire l&#39;installazione **solo** su AEM publishNotate che solo `install.author` e `install.publish` sono destinazioni supportate. Altre modalità di esecuzione **non sono** supportate.

Ad esempio, una distribuzione che contiene pacchetti specifici per l&#39;authoring e la pubblicazione di AEM potrebbe avere l&#39;aspetto seguente:

+ `all` Il pacchetto contenitore incorpora i pacchetti seguenti, per creare un artefatto di distribuzione singolo
   + `ui.apps` incorporato nella `/apps/my-app-packages/application/install` distribuzione del codice sia per l’autore che per la pubblicazione AEM
   + `ui.apps.author` incorporato in `/apps/my-app-packages/application/install.author` distribuisce il codice solo all’autore di AEM
   + `ui.content` incorporato nella `/apps/my-app-packages/content/install` distribuzione del contenuto e della configurazione sia per l’authoring che per la pubblicazione AEM
   + `ui.content.publish` incorporato nella `/apps/my-app-packages/content/install.publish` distribuzione di contenuto e configurazione solo per AEM Publish

>[!TIP]
>
>Per un frammento completo, consulta la sezione Snippet [XML](#xml-embeddeds) POM di seguito.

### Definizione filtro pacchetto contenitore {#container-package-filter-definition}

A causa dell&#39;incorporazione del codice e dei sottopacchetti di contenuto nel pacchetto contenitore, i percorsi di destinazione incorporati devono essere aggiunti al progetto contenitore `filter.xml` per garantire che i pacchetti incorporati siano inclusi nel pacchetto contenitore una volta creati.

È sufficiente aggiungere le `<filter root="/apps/<my-app>-packages"/>` voci per qualsiasi cartella di secondo livello che contiene pacchetti secondari da distribuire.

>[!TIP]
>
>Per un frammento completo, consulta la sezione Snippet [XML](#xml-container-package-filters) POM di seguito.

## Incorporazione di pacchetti di terze parti {#embedding-3rd-party-packages}

Tutti i pacchetti devono essere disponibili tramite l&#39;archivio [degli artifact Maven pubblico di](https://repo.adobe.com/nexus/content/groups/public/com/adobe/) Adobe o un archivio degli artifact di terze parti accessibile e accessibile al pubblico.

Se i pacchetti di terze parti si trovano nell’**archivio di artefatti Maven pubblico di Adobe**, per consentire ad Adobe Cloud Manager di risolvere gli artefatti non è necessario effettuare nessuna ulteriore configurazione.

Se i pacchetti di terze parti si trovano in un **archivio di artefatti Maven pubblico di terze parti**, tale archivio deve essere registrato nel `pom.xml` del progetto, per poi essere incorporato seguendo il metodo [descritto sopra](#embeddeds). Se l’applicazione/connettore di terze parti richiede pacchetti di codice e di contenuto, ciascuno di essi deve essere incorporato nelle posizioni corrette del pacchetto contenitore (`all`).

L&#39;aggiunta di dipendenze di Paradiso segue le pratiche standard di Maven, e l&#39;incorporazione di artefatti di terze parti (pacchetti di codice e di contenuto) è [descritta sopra](#embedding-3rd-party-packages).

>[!TIP]
>
>Per un frammento completo, consulta la sezione Snippet [XML](#xml-3rd-party-maven-repositories) POM di seguito.

## Dipendenze del pacchetto tra `ui.apps` i pacchetti `ui.content` dei pacchetti {#package-dependencies}

Per garantire la corretta installazione dei pacchetti, si raccomanda di stabilire dipendenze tra pacchetti.

La regola generale è che i pacchetti che contengono contenuto variabile (`ui.content`) devono dipendere dal contenuto immutabile (`ui.apps`) che supporta il rendering e l&#39;uso del contenuto modificabile.

>[!TIP]
>
>Per un frammento completo, consulta la sezione Snippet [XML](#xml-package-dependencies) POM di seguito.

I pattern comuni per le dipendenze dei pacchetti di contenuto sono:

### Dipendenze semplici del pacchetto di distribuzione {#simple-deployment-package-dependencies}

Il semplice caso imposta il pacchetto di contenuti `ui.content` modificabile in modo che dipenda dal pacchetto di codice `ui.apps` immutabile.

+ `all` non ha dipendenze
   + `ui.apps` non ha dipendenze
   + `ui.content` dipende da `ui.apps`

### Dipendenze complesse del pacchetto di distribuzione {#complex-deploxment-package-dependencies}

Le implementazioni complesse si espandono in base al caso semplice e impostano le dipendenze tra il contenuto mutabile corrispondente e i pacchetti di codice immutabili. Se necessario, è possibile stabilire dipendenze tra pacchetti di codice immutabili.

+ `all` non ha dipendenze
   + `ui.apps.common` non ha dipendenze
   + `ui.apps.site-a` dipende da `ui.apps.common`
   + `ui.content.site-a` dipende da `ui.apps.site-a`
   + `ui.apps.site-b` dipende da `ui.apps.common`
   + `ui.content.site-b` dipende da `ui.apps.site-b`

## Sviluppo locale e implementazione {#local-development-and-deployment}

Le strutture e l&#39;organizzazione del progetto descritte in questo articolo sono **completamente compatibili** con le istanze di AEM per lo sviluppo locale.

## Snippet XML POM {#pom-xml-snippets}

Di seguito sono riportati alcuni snippet di `pom.xml` configurazione Maven che possono essere aggiunti ai progetti Maven per allineare le raccomandazioni di cui sopra.

### Tipi di pacchetti {#xml-package-types}

I pacchetti di codice e di contenuto, distribuiti come pacchetti secondari, devono dichiarare un pacchetto di tipo **applicazione** o **contenuto**, a seconda di ciò che contengono.

#### Tipi di pacchetti contenitore {#container-package-types}

Il `all/pom.xml` progetto contenitore **non** dichiara un `<packageType>`.

#### Tipi di pacchetti di codice (immutabili) {#immutable-package-types}

I pacchetti di codice devono impostare `packageType` su `application`.

Nelle `ui.apps/pom.xml`, le direttive di configurazione della `<packageType>application</packageType>` build della dichiarazione del `filevault-package-maven-plugin` plug-in dichiarano il tipo di pacchetto.

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        <group>${project.groupId}</group>
        <name>${my-app.ui.apps}</name>
        <packageType>application</packageType>
        <accessControlHandling>merge</accessControlHandling>
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

#### Tipi di pacchetti di contenuto (variabile) {#mutable-package-types}

I pacchetti di contenuto devono impostare `packageType` su `content`.

Nella `ui.content/pom.xml`, la direttiva di configurazione della `<packageType>content</packageType>` build della dichiarazione del `filevault-package-maven-plugin` plugin dichiara il suo tipo di pacchetto.

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        <group>${project.groupId}</group>
        <name>${my-app.ui.content}</name>
        <packageType>content</packageType>
        <accessControlHandling>merge</accessControlHandling>
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

### Contrassegnazione dei pacchetti per la distribuzione di Adobe Cloud Manager {#cloud-manager-target}

In ogni progetto che genera un pacchetto, **fatta eccezione** per il progetto contenitore (`all`), aggiungi `<cloudManagerTarget>none</cloudManagerTarget>` alla configurazione `<properties>`della dichiarazione del plug-in `filevault-package-maven-plugin`, in modo da assicurarti che **non siano** distribuiti da Adobe Cloud Manager. Il pacchetto contenitore (`all`) deve essere il singolo pacchetto distribuito tramite Cloud Manager, che a sua volta incorpora tutti i pacchetti richiesti di codice e contenuto.

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
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

### Repo Init{#snippet-repo-init}

Gli script Repo Init che contengono gli script Repo Init sono definiti nella configurazione di fabbrica `RepositoryInitializer` OSGi tramite la `scripts` proprietà. Poiché questi script sono stati definiti nelle configurazioni OSGi, possono essere facilmente individuati in modalità di esecuzione utilizzando la semantica `../config.<runmode>` delle cartelle standard.

Poiché in genere gli script sono dichiarazioni su più righe, è più semplice definirle nel `.config` file rispetto al formato di base XML `sling:OsgiConfig` .

`/apps/my-app/config.author/org.apache.sling.jcr.repoinit.RepositoryInitializer-author.config`

```plain
scripts=["
    create service user my-data-reader-service

    set ACL on /var/my-data
        allow jcr:read for my-data-reader-service
    end

    create path (sling:Folder) /conf/my-app/settings
"]
```

La proprietà `scripts` OSGi contiene le direttive definite dalla lingua [Repo Init di](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language)Apache Sling.

### Pacchetto struttura archivio {#xml-repository-structure-package}

In `ui.apps/pom.xml` e in qualsiasi altro `pom.xml` che dichiara un pacchetto di codice (`<packageType>application</packageType>`), aggiungete la seguente configurazione di pacchetto struttura del repository al plug-in FileVault Maven. Potete [creare un pacchetto di struttura del repository personalizzato per il progetto](repository-structure-package.md).

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
```

### Incorporazione di pacchetti secondari nel pacchetto contenitore {#xml-embeddeds}

In `all/pom.xml`, aggiungete le seguenti `<embeddeds>` direttive alla dichiarazione del `filevault-package-maven-plugin` plugin. Ricordate, **non** utilizzate la `<subPackages>` configurazione, perché includerà i pacchetti secondari in `/etc/packages` piuttosto che `/apps/my-app-packages/<application|content>/install(.author|.publish)?`.

```xml
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <embeddeds>

          <!-- Include the application's ui.apps and ui.content packages -->
          <!-- Ensure the artifactIds are correct -->

          <!-- Code package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.apps</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/application/install</target>
          </embedded>

          <!-- Code package that deploys ONLY to AEM Author -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.apps.author</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/application/install.author</target>
          </embedded>

          <!-- Content package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.content</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/content/install</target>
          </embedded>

          <!-- Content package that deploys ONLY to AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.content.publish-only</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/content/install.publish</target>
          </embedded>

          <!-- Include any other extra packages such as AEM WCM Core Components -->
          <embedded>
              <groupId>com.adobe.cq</groupId>
              <!-- Not to be confused; WCM Core Components' Code package's artifact is named `.content` -->
              <artifactId>core.wcm.components.content</artifactId>
              <type>zip</type>
              <target>/apps/vendor-packages/application/install</target>
          </embedded>

          <embedded>
              <groupId>com.adobe.cq</groupId>
              <!-- Not to be confused; WCM Core Components' Content package's artifact is named `.conf` -->
              <artifactId>core.wcm.components.conf</artifactId>
              <type>zip</type>
              <target>/apps/vendor-packages/content/install</target>
          </embedded>
      <embeddeds>
  </configuration>
</plugin>
...
```

### Definizione filtro pacchetto contenitore {#xml-container-package-filters}

Nel `filter.xml` `all` del progetto (`all/src/main/content/jcr_root/META-INF/vault/definition/filter.xml`), **includi** tutte le cartelle `-packages` che contengono pacchetti secondari da distribuire:

```xml
<filter root="/apps/my-app-packages"/>
```

Se nelle destinazioni di incorporamento `/apps/*-packages` vengono utilizzati più elementi, questi devono essere elencati qui.

### Repository Maven di terze parti {#xml-3rd-party-maven-repositories}

>[!WARNING]
> L&#39;aggiunta di più repository Maven può estendere i tempi di creazione dei cibi mentre ulteriori repository Maven saranno controllati per le dipendenze.

Nel progetto del reattore `pom.xml`, aggiungere tutte le necessarie direttive del repository di Maven pubbliche di terze parti. La `<repository>` configurazione completa dovrebbe essere disponibile dal provider del repository di terze parti.

```xml
<repositories>
  ...
  <repository>
      <id>3rd-party-repository</id>
      <name>Public 3rd Party Repository</name>
      <url>https://repo.3rdparty.example.com/...</url>
      <releases>
          <enabled>true</enabled>
          <updatePolicy>never</updatePolicy>
      </releases>
      <snapshots>
          <enabled>false</enabled>
      </snapshots>
  </repository>
  ...
</repositories>
```

### Dipendenze del pacchetto tra `ui.apps` i pacchetti `ui.content` dei pacchetti {#xml-package-dependencies}

In `ui.content/pom.xml`, aggiungete le seguenti `<dependencies>` direttive alla dichiarazione del `filevault-package-maven-plugin` plugin.

```xml
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <dependencies>
        <!-- Declare the content package dependency in the ui.content/pom.xml on the ui.apps project -->
        <dependency>
            <groupId${project.groupId}</groupId>
            <artifactId>my-app.ui.apps</artifactId>
            <version>${project.version}</version>
        </dependency>
      </dependencies>
    ...
  </configuration>
</plugin>
...
```

### Pulizia della cartella di destinazione del progetto contenitore {#xml-clean-container-package}

In `all/pom.xml` aggiungere il `maven-clean-plugin` plug-in che pulirà la directory di destinazione prima delle build Maven.

```xml
<plugins>
  ...
  <plugin>
    <artifactId>maven-clean-plugin</artifactId>
    <executions>
      <execution>
        <id>auto-clean</id>
        <!-- Run at the beginning of the build rather than the default, which is after the build is done -->
        <phase>initialize</phase>
        <goals>
          <goal>clean</goal>
        </goals>
      </execution>
    </executions>
  </plugin>
  ...
</plugins>
```

## Risorse aggiuntive {#additional-resources}

+ [Gestione dei pacchetti con il cielo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/vlt-mavenplugin.html)
+ [FileVault Content Package Maven Plug-in](http://jackrabbit.apache.org/filevault-package-maven-plugin/)