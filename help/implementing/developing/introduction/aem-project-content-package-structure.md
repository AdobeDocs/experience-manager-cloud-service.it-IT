---
title: Struttura dei progetti AEM
description: Scoprite come definire le strutture dei pacchetti per la distribuzione nel Cloud Service Adobe Experience Manager.
translation-type: tm+mt
source-git-commit: 1a282bdaca02f47d7936222da8522e74831a4572
workflow-type: tm+mt
source-wordcount: '2828'
ht-degree: 13%

---


# Struttura dei progetti AEM

>[!TIP]
>
>Acquisisci familiarità con il [AEM Project Archetype use](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/archetype/overview.html) di base e con il [FileVault Content Maven Plug-in](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/vlt-mavenplugin.html), in quanto questo articolo si basa su tali conoscenze e concetti.

Questo articolo illustra le modifiche necessarie per i progetti Adobe Experience Manager Maven AEM come Cloud Service compatibile, garantendo che rispettino la divisione dei contenuti mutabili e immutabili, che le dipendenze siano stabilite per creare distribuzioni deterministiche non in conflitto e che siano inserite in una struttura distribuibile.

AEM distribuzioni dell&#39;applicazione devono essere composte da un unico pacchetto AEM. Questo pacchetto deve contenere a sua volta sottopacchetti che comprendono tutto ciò che l&#39;applicazione richiede per funzionare, compreso il codice, la configurazione e qualsiasi contenuto di base di supporto.

AEM richiede una separazione di **contenuto** e **codice**, il che significa che un singolo pacchetto di contenuti **non può** essere distribuito **sia** su `/apps` che su aree scrivibili di runtime dell’archivio (ad esempio `/content`, `/conf`, `/home` o tutto il resto fuorché `/apps`). Al contrario, l’applicazione deve separare codice e contenuto in pacchetti discreti da distribuire in AEM.

La struttura del pacchetto descritta in questo documento è compatibile **sia** con le distribuzioni di sviluppo locali che con le distribuzioni di AEM Cloud Service.

>[!TIP]
>
>Le configurazioni descritte in questo documento sono fornite da [AEM Project Maven Archetype 24 o successivo](https://github.com/adobe/aem-project-archetype/releases).

## Aree variabile e immutabili del repository {#mutable-vs-immutable}

`/apps` e `/libs`**sono considerate aree immutabili di AEM poiché non possono essere modificate (create, aggiornate, eliminate) dopo l’avvio di AEM (ad es. in fase di runtime).** Eventuali tentativi di modifica di un’area immutabile in fase di runtime avranno esito negativo.

Tutti gli altri elementi presenti nella directory archivio, `/content`, `/conf`, `/var`, `/etc`, `/oak:index`, `/system`, `/tmp` ecc. sono tutte le aree **mutable**, il che significa che possono essere modificate in fase di esecuzione.

>[!WARNING]
>
>Come nelle versioni precedenti di AEM, `/libs` non deve essere modificato. Solo AEM codice prodotto può essere distribuito in `/libs`.

### Indici Oak {#oak-indexes}

Gli indici Oak (`/oak:index`) sono gestiti specificamente dal AEM come processo di distribuzione del Cloud Service. Questo perché Cloud Manager deve aspettare che un nuovo indice venga distribuito e riclassificato completamente prima di passare alla nuova immagine del codice.

Per questo motivo, sebbene gli indici Oak siano modificabili in fase di esecuzione, devono essere distribuiti come codice in modo che possano essere installati prima che siano installati pacchetti modificabili. Di conseguenza, le configurazioni `/oak:index` fanno parte del pacchetto di codice e non del pacchetto di contenuti [come descritto di seguito](#recommended-package-structure).

>[!TIP]
>
>Per ulteriori dettagli sull&#39;indicizzazione in AEM come Cloud Service, consultare il documento [Content Search and Indexing](/help/operations/indexing.md) (Ricerca e indicizzazione dei contenuti).

## Struttura pacchetto consigliata {#recommended-package-structure}

![ struttura pacchetto progetto Experience Manager](assets/content-package-organization.png)

Questo diagramma fornisce una panoramica della struttura di progetto consigliata e degli artifact di distribuzione del pacchetto.

La struttura di distribuzione dell&#39;applicazione consigliata è la seguente:

### Pacchetti di codice / Bundle OSGi

+ Il file Jar del bundle OSGi viene generato e incorporato direttamente in tutto il progetto.

+ Il pacchetto `ui.apps` contiene tutto il codice da distribuire e distribuisce solo in `/apps`. Gli elementi comuni del pacchetto `ui.apps` includono, tra l&#39;altro:
   + [Definizioni dei componenti e ](https://docs.adobe.com/content/help/it-IT/experience-manager-htl/using/overview.html) script HTL
      + `/apps/my-app/components`
   + JavaScript e CSS (tramite [librerie client](/help/implementing/developing/introduction/clientlibs.md))
      + `/apps/my-app/clientlibs`
   + [](/help/implementing/developing/introduction/overlays.md) Sovrapposizioni  `/libs`
      + `/apps/cq`, `/apps/dam/`, etc.
   + Configurazioni basate sul contesto di fallback
      + `/apps/settings`
   + ACL (autorizzazioni)
      + Qualsiasi `rep:policy` per qualsiasi percorso in `/apps`

+ Il pacchetto `ui.config` contiene tutte le [configurazioni OSGi](/help/implementing/deploying/configuring-osgi.md):
   + Cartella organizzativa contenente definizioni di configurazione OSGi specifiche della modalità di esecuzione
      + `/apps/my-app/osgiconfig`
   + Cartella di configurazione OSGi comune contenente configurazioni OSGi predefinite che si applicano a tutte le AEM di destinazione come destinazioni di distribuzione Cloud Service
      + `/apps/my-app/osgiconfig/config`
   + Esegui cartelle di configurazione OSGi specifiche della modalità che contengono configurazioni OSGi predefinite applicabili a tutti i AEM di destinazione come destinazioni di distribuzione Cloud Service
      + `/apps/my-app/osgiconfig/config.<author|publish>.<dev|stage|prod>`
   + Script di configurazione Repo Init OSGi
      + [Repo ](#repo-init) Inite è il metodo consigliato per distribuire (modificabile) contenuto che fa parte logicamente dell&#39;applicazione AEM. Le configurazioni di Repo Init OSGi devono trovarsi nella cartella `config.<runmode>` appropriata come indicato sopra e devono essere utilizzate per definire:
         + Strutture contenuto di base
         + Utenti
         + Utenti del servizio
         + Gruppi
         + ACL (autorizzazioni)

### Pacchetti di contenuti

+ Il pacchetto `ui.content` contiene tutto il contenuto e la configurazione. Il pacchetto di contenuti contiene tutte le definizioni dei nodi non presenti nei pacchetti `ui.apps` o `ui.config`, o in altre parole, in elementi non inclusi in `/apps` o `/oak:index`. Gli elementi comuni del pacchetto `ui.content` includono, tra l&#39;altro:
   + Configurazioni basate sul contesto
      + `/conf`
   + Strutture di contenuto complesse e necessarie (ad esempio Compilazione del contenuto che si basa e si estende oltre le strutture di contenuto della linea di base definite in Repo Init.)
      + `/content`,  `/content/dam`ecc.
   + Tassonomie di tag gestite
      + `/content/cq:tags`
   + Nodi legacy ecc. (Idealmente, migrare questi a posizioni diverse/ecc.)
      + `/etc`

### Pacchetti contenitore

+ Il pacchetto `all` è un pacchetto contenitore che include UNICAMENTE artefatti distribuibili, il file Jar del bundle OSGI, `ui.apps`, `ui.config` e `ui.content` pacchetti come embed. Il pacchetto `all` non deve avere **alcun contenuto o codice** proprio, ma deve delegare tutta la distribuzione al repository ai relativi pacchetti secondari o ai file Jar del bundle OSGi.

   I pacchetti ora sono inclusi utilizzando la configurazione incorporata del plug-in Maven [FileVault Package Maven](#embeddeds), anziché la configurazione `<subPackages>`.

   Per implementazioni complesse  Experience Manager, potrebbe essere utile creare più `ui.apps`, `ui.config` e `ui.content` progetti/pacchetti che rappresentano siti o locatari specifici in AEM. In questo caso, accertatevi che la divisione tra contenuto variabile e immutabile sia rispettata, e che i pacchetti di contenuto e i file Jar del bundle OSGi richiesti siano incorporati come pacchetti secondari nel pacchetto di contenuto contenitore `all`.

   Ad esempio, una struttura complessa di pacchetti di contenuto di distribuzione potrebbe avere l&#39;aspetto seguente:

   + `all` il pacchetto di contenuti incorpora i pacchetti seguenti, per creare un artefatto di distribuzione unico
      + `common.ui.apps` distribuisce il codice richiesto dal  **** sito A e dal sito B
      + `site-a.core` Bacheca OSGi necessaria per il sito A
      + `site-a.ui.apps` distribuisce il codice richiesto dal sito A
      + `site-a.ui.config` distribuisce le configurazioni OSGi richieste dal sito A
      + `site-a.ui.content` distribuisce il contenuto e la configurazione richiesti dal sito A
      + `site-b.core` Bacheca OSGi necessaria per il sito B
      + `site-b.ui.apps` distribuisce il codice richiesto dal sito B
      + `site-b.ui.config` distribuisce le configurazioni OSGi richieste dal sito B
      + `site-b.ui.content` distribuisce il contenuto e la configurazione richiesti dal sito B

### Pacchetti applicativi aggiuntivi{#extra-application-packages}

Se altri progetti AEM, anch&#39;essi costituiti da pacchetti di codice e contenuto propri, vengono utilizzati dalla distribuzione AEM, i loro pacchetti contenitore devono essere incorporati nel pacchetto `all` del progetto.

Ad esempio, un progetto AEM che include 2 applicazioni AEM fornitore potrebbe avere l&#39;aspetto seguente:

+ `all` il pacchetto di contenuti incorpora i pacchetti seguenti, per creare un artefatto di distribuzione unico
   + `core` Bacheca OSGi necessaria per l&#39;applicazione AEM
   + `ui.apps` distribuisce il codice richiesto dall&#39;applicazione AEM
   + `ui.config` distribuisce le configurazioni OSGi richieste dall&#39;applicazione AEM
   + `ui.content` distribuisce il contenuto e la configurazione richiesti dall&#39;applicazione AEM
   + `vendor-x.all` distribuisce tutto (codice e contenuto) richiesto dall&#39;applicazione X del fornitore
   + `vendor-y.all` distribuisce tutto (codice e contenuto) richiesto dall&#39;applicazione Y del fornitore

## Tipi di pacchetti {#package-types}

I pacchetti devono essere contrassegnati con il tipo di pacchetto dichiarato.

+ I pacchetti contenitore devono impostare `packageType` su `container`.
+ I pacchetti di codice (immutabili) devono impostare `packageType` su `application`.
+ I pacchetti di contenuto (modificabili) devono impostare `packageType` su `content`.

Per ulteriori informazioni vedere [Apache Jackrabbit FileVault - Package Maven Plugin documentation](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType) e [FileVault Maven configuration snippet](#marking-packages-for-deployment-by-adoube-cloud-manager) di seguito.

>[!TIP]
>
>Per un frammento completo, vedere la sezione [Snippet XML POM](#xml-package-types) sotto.

## Contrassegnazione dei pacchetti per la distribuzione da parte di  Adobe Cloud Manager {#marking-packages-for-deployment-by-adoube-cloud-manager}

Per impostazione predefinita, Adobe Cloud Manager raccoglie tutti i pacchetti prodotti dalla build Maven. Tuttavia, poiché il pacchetto contenitore (`all`) è l’unico artefatto di distribuzione che contiene tutti i pacchetti di codice e contenuto, è necessario assicurarsi che sia distribuito **solo** il pacchetto contenitore (`all`). Per questo motivo, gli altri pacchetti generati dalla build Maven devono essere contrassegnati con la configurazione FileVault Content Package Maven Plug-In di `<properties><cloudManagerTarget>none</cloudManageTarget></properties>`.

>[!TIP]
>
>Per un frammento completo, vedere la sezione [Snippet XML POM](#pom-xml-snippets) sotto.

## Repo Init{#repo-init}

Repo Init fornisce istruzioni, o script, che definiscono le strutture JCR, che vanno dalle strutture nodo comuni come le strutture delle cartelle, agli utenti, agli utenti del servizio, ai gruppi e alla definizione ACL.

I vantaggi principali di Repo Init sono i permessi impliciti per eseguire tutte le azioni definite dai loro script, e vengono richiamati in anticipo nel ciclo di vita della distribuzione, garantendo che tutte le strutture JCR necessarie siano presenti dal codice temporale.

Mentre gli script Repo Init stessi vivono nel progetto `ui.config` come script, possono e devono essere utilizzati per definire le seguenti strutture modificabili:

+ Strutture contenuto di base
+ Utenti del servizio
+ Utenti
+ Gruppi
+ ACL

Gli script Repo Init sono memorizzati come `scripts` voci di `RepositoryInitializer` configurazioni di fabbrica OSGi, e quindi possono essere implicitamente indirizzati dalla modalità di esecuzione, consentendo differenze tra gli script Repo Init di AEM Author e AEM Publish Services o anche tra ambienti (Dev, Stage e Prod).

Le configurazioni di Repo Init OSGi sono scritte meglio nel formato di configurazione [`.config` OSGi](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-config-1) in quanto supportano più righe, il che rappresenta un&#39;eccezione alle best practice relative all&#39;utilizzo di [`.cfg.json` per definire le configurazioni OSGi](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1).

Tenete presente che quando definite Utenti e Gruppi, solo i gruppi sono considerati parte dell’applicazione e che la funzione integrata deve essere definita qui. Gli utenti e i gruppi dell&#39;organizzazione devono essere ancora definiti in fase di esecuzione in AEM; ad esempio, se un flusso di lavoro personalizzato assegna il lavoro a un gruppo denominato, tale gruppo deve essere definito in tramite Repo Init nell&#39;applicazione AEM, tuttavia se il gruppo è semplicemente di tipo organizzativo, come &quot;Wendy&#39;s Team&quot; e &quot;Sean&#39;s Team&quot;, questi sono definiti e gestiti in fase di runtime in AEM.

>[!TIP]
>
>Gli script Repo Init *devono* essere definiti nel campo inline `scripts` e la configurazione `references` non funzionerà.

Il vocabolario completo per gli script Repo Init è disponibile nella [documentazione Apache Sling Repo Init](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

>[!TIP]
>
>Per un frammento completo, vedere la sezione [Repo Init Snippet](#snippet-repo-init) sotto.

## Pacchetto struttura archivio {#repository-structure-package}

I pacchetti di codice richiedono la configurazione del plug-in FileVault Maven per fare riferimento a un `<repositoryStructurePackage>` che applica la correttezza delle dipendenze strutturali (per garantire che un pacchetto di codice non venga installato su un altro). È possibile [creare un proprio pacchetto di struttura del repository per il progetto](repository-structure-package.md).

Questa operazione è **richiesta solo** per i pacchetti codice, ovvero per tutti i pacchetti contrassegnati con `<packageType>application</packageType>`.

Per informazioni su come creare un pacchetto di struttura del repository per l&#39;applicazione, vedere [Sviluppare un pacchetto di struttura del repository](repository-structure-package.md).

I pacchetti di contenuto (`<packageType>content</packageType>`) **non** richiedono questo pacchetto della struttura del repository.

>[!TIP]
>
>Per un frammento completo, vedere la sezione [Snippet XML POM](#xml-repository-structure-package) sotto.

## Incorporazione di pacchetti secondari nel pacchetto contenitore{#embeddeds}

I pacchetti di contenuto o codice vengono inseriti in una speciale cartella &quot;side-car&quot; e possono essere installati sia AEM autore che AEM pubblicazione, oppure entrambi, utilizzando la configurazione `<embeddeds>` del plug-in FileVault Maven. Tenere presente che la configurazione `<subPackages>` non deve essere utilizzata.

I casi d’uso più comuni includono:

+ ACL/autorizzazioni che differiscono tra AEM utenti autori e AEM utenti di pubblicazione
+ Configurazioni utilizzate per supportare le attività solo su AEM autore
+ Codice come le integrazioni con i sistemi di back-office, richiesto solo per l&#39;esecuzione su AEM autore

![Incorporazione di pacchetti](assets/embeddeds.png)

Per eseguire il targeting AEM autore, AEM pubblicazione o entrambi, il pacchetto è incorporato nel pacchetto contenitore `all` in una cartella speciale, nel formato seguente:

`/apps/<app-name>-packages/(content|application|container)/install(.author|.publish)?`

Suddividere la struttura delle cartelle in base a:

+ La cartella di primo livello **deve essere** `/apps`.
+ La cartella di secondo livello rappresenta l&#39;applicazione con `-packages` post-fisso sul nome della cartella. Spesso esiste una sola cartella di 2° livello in cui sono incorporati tutti i pacchetti secondari, tuttavia è possibile creare un numero qualsiasi di cartelle di 2° livello per rappresentare al meglio la struttura logica dell&#39;applicazione:
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`

   >[!WARNING]
   >
   >Per convenzione, le cartelle incorporate in un pacchetto secondario sono denominate con il suffisso `-packages`. In questo modo, il codice di distribuzione e i pacchetti di contenuto **non** vengono distribuiti nelle cartelle di destinazione di qualsiasi pacchetto secondario `/apps/<app-name>/...`, il che provoca un comportamento di installazione distruttivo e ciclico.

+ La cartella di terzo livello deve essere
   `application`,  `content` oppure  `container`
   + La cartella `application` contiene pacchetti di codice
   + La cartella `content` contiene pacchetti di contenuti
   + La cartella `container` contiene tutti i [pacchetti di applicazioni extra](#extra-application-packages) che possono essere inclusi dall&#39;applicazione AEM.
Il nome della cartella corrisponde ai [tipi di pacchetto](#package-types) dei pacchetti che contiene.
+ La cartella di quarto livello contiene i pacchetti secondari e deve corrispondere a una delle seguenti:
   + `install` per effettuare l’installazione **sia su** AEM Author che AEM Publish
   + `install.author` per eseguire l’installazione **solo** su AEM Author
   + `install.publish` per  **** eseguire l&#39;installazione solo su AEM pubblicazione Nota che solo  `install.author` e  `install.publish` sono destinazioni supportate. Altre modalità di esecuzione **non sono** supportate.

Ad esempio, una distribuzione che contiene AEM pacchetti specifici per l&#39;autore e la pubblicazione potrebbe avere l&#39;aspetto seguente:

+ `all` Il pacchetto contenitore incorpora i pacchetti seguenti, per creare un artefatto di distribuzione singolo
   + `ui.apps` incorporato in  `/apps/my-app-packages/application/install` distribuisce il codice sia AEM creazione che AEM pubblicazione
   + `ui.apps.author` incorporato nel codice  `/apps/my-app-packages/application/install.author` distribuisce solo AEM autore
   + `ui.content` incorporato in  `/apps/my-app-packages/content/install` distribuisce il contenuto e la configurazione sia per AEM creazione che per AEM pubblicazione
   + `ui.content.publish` incorporato in  `/apps/my-app-packages/content/install.publish` distribuisce contenuto e configurazione solo AEM pubblicazione

>[!TIP]
>
>Per un frammento completo, vedere la sezione [Snippet XML POM](#xml-embeddeds) sotto.

### Definizione filtro pacchetto contenitore {#container-package-filter-definition}

A causa dell&#39;incorporazione del codice e dei sottopacchetti di contenuto nel pacchetto contenitore, i percorsi di destinazione incorporati devono essere aggiunti alla `filter.xml` del progetto contenitore per garantire che i pacchetti incorporati siano inclusi nel pacchetto contenitore una volta creati.

È sufficiente aggiungere le `<filter root="/apps/<my-app>-packages"/>` voci per qualsiasi cartella di secondo livello che contiene pacchetti secondari da distribuire.

>[!TIP]
>
>Per un frammento completo, vedere la sezione [Snippet XML POM](#xml-container-package-filters) sotto.

## Incorporazione di pacchetti di terze parti {#embedding-3rd-party-packages}

Tutti i pacchetti devono essere disponibili tramite il [ Adobe  archivio degli artifact Maven pubblico](https://repo.adobe.com/nexus/content/groups/public/com/adobe/) o un archivio degli artifact di terze parti accessibile e accessibile al pubblico.

Se i pacchetti di terze parti si trovano nell’**archivio di artefatti Maven pubblico di Adobe**, per consentire ad Adobe Cloud Manager di risolvere gli artefatti non è necessario effettuare nessuna ulteriore configurazione.

Se i pacchetti di terze parti si trovano in un **archivio di artefatti Maven pubblico di terze parti**, tale archivio deve essere registrato nel `pom.xml` del progetto, per poi essere incorporato seguendo il metodo [descritto sopra](#embeddeds).

I connettori/applicazioni di terze parti devono essere incorporati utilizzando il pacchetto `all` come contenitore nel pacchetto contenitore del progetto (`all`).

L&#39;aggiunta di dipendenze Paradiso segue le pratiche standard di Maven, e l&#39;incorporazione di artefatti di terze parti (pacchetti di codice e di contenuto) sono [descritti sopra](#embedding-3rd-party-packages).

>[!TIP]
>
>Per un frammento completo, vedere la sezione [Snippet XML POM](#xml-3rd-party-maven-repositories) sotto.

## Dipendenze del pacchetto tra `ui.apps` da `ui.content` pacchetti {#package-dependencies}

Per garantire la corretta installazione dei pacchetti, si raccomanda di stabilire dipendenze tra pacchetti.

La regola generale è che i pacchetti che contengono contenuto variabile (`ui.content`) devono dipendere dal codice immutabile (`ui.apps`) che supporta il rendering e l&#39;uso del contenuto modificabile.

Un&#39;eccezione notevole a questa regola generale è rappresentata dal fatto che il pacchetto di codice immutabile (`ui.apps` o qualsiasi altro), __only__ contiene pacchetti OSGi. In tal caso, nessun pacchetto AEM deve dichiarare una dipendenza da esso. Questo perché i pacchetti di codice immutabili __solo__ contenenti bundle OSGi non sono registrati con AEM Package Manager, e quindi, qualsiasi pacchetto AEM a seconda di esso avrà una dipendenza non soddisfatta e non sarà possibile eseguire l&#39;installazione.

>[!TIP]
>
>Per un frammento completo, vedere la sezione [Snippet XML POM](#xml-package-dependencies) sotto.

I pattern comuni per le dipendenze dei pacchetti di contenuto sono:

### Dipendenze pacchetto di distribuzione semplice {#simple-deployment-package-dependencies}

Il semplice caso imposta il pacchetto di contenuti `ui.content` modificabile in modo che dipenda dal pacchetto di codice `ui.apps` immutabile.

+ `all` non ha dipendenze
   + `ui.apps` non ha dipendenze
   + `ui.content` dipende da  `ui.apps`

### Dipendenze complesse del pacchetto di distribuzione {#complex-deploxment-package-dependencies}

Le implementazioni complesse si espandono in base al caso semplice e impostano le dipendenze tra il contenuto mutabile corrispondente e i pacchetti di codice immutabili. Se necessario, è possibile stabilire dipendenze tra pacchetti di codice immutabili.

+ `all` non ha dipendenze
   + `common.ui.apps.common` non ha dipendenze
   + `site-a.ui.apps` dipende da  `common.ui.apps`
   + `site-a.ui.content` dipende da  `site-a.ui.apps`
   + `site-b.ui.apps` dipende da  `common.ui.apps`
   + `site-b.ui.content` dipende da  `site-b.ui.apps`

## Sviluppo locale e implementazione {#local-development-and-deployment}

Le strutture e l&#39;organizzazione del progetto descritte in questo articolo sono **AEM di sviluppo locale completamente compatibili**.

## Snippet XML POM {#pom-xml-snippets}

Di seguito sono riportati gli snippet di configurazione Maven `pom.xml` che possono essere aggiunti ai progetti Maven per allineare alle raccomandazioni di cui sopra.

### Tipi di pacchetti {#xml-package-types}

I pacchetti di codice e di contenuto, distribuiti come pacchetti secondari, devono dichiarare un pacchetto di tipo **applicazione** o **contenuto**, a seconda di ciò che contengono.

#### Tipi di pacchetti contenitore {#container-package-types}

Il contenitore `all/pom.xml` progetto **non dichiara** un `<packageType>`.

#### Tipi di pacchetti di codice (immutabile) {#immutable-package-types}

I pacchetti di codice devono impostare `packageType` su `application`.

In `ui.apps/pom.xml`, le direttive di configurazione `<packageType>application</packageType>` del plug-in `filevault-package-maven-plugin` dichiarano il tipo di pacchetto.

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
        <name>my-app.ui.apps</name>
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

In `ui.content/pom.xml`, la direttiva di configurazione della `<packageType>content</packageType>` del plug-in `filevault-package-maven-plugin` dichiara il tipo di pacchetto.

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
        <name>my-app.ui.content</name>
        <packageType>content</packageType>
        <accessControlHandling>merge</accessControlHandling>
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

### Contrassegnazione dei pacchetti per  distribuzione di Adobe Cloud Manager {#cloud-manager-target}

In ogni progetto che genera un pacchetto, **fatta eccezione** per il progetto contenitore (`all`), aggiungi `<cloudManagerTarget>none</cloudManagerTarget>` alla configurazione `<properties>`della dichiarazione del plug-in `filevault-package-maven-plugin`, in modo da assicurarti che **non siano** distribuiti da Adobe Cloud Manager. Il pacchetto contenitore (`all`) deve essere il singolo pacchetto distribuito tramite Cloud Manager, che a sua volta incorpora tutti i pacchetti di codice e contenuto richiesti.

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

Gli script Repo Init che contengono gli script Repo Init sono definiti nella configurazione `RepositoryInitializer` OSGi factory tramite la proprietà `scripts`. Poiché questi script sono stati definiti all&#39;interno delle configurazioni OSGi, è possibile definirli facilmente in modalità di esecuzione utilizzando la semantica `../config.<runmode>` di cartelle standard.

Poiché gli script sono in genere una dichiarazione su più righe, è più facile definirli nel file `.config` che nel formato `.cfg.json` basato su JSON.

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

La proprietà `scripts` OSGi contiene le direttive definite dal linguaggio Repo Init [Apache Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

### Pacchetto struttura archivio {#xml-repository-structure-package}

In `ui.apps/pom.xml` e in qualsiasi altro `pom.xml` che dichiara un pacchetto di codice (`<packageType>application</packageType>`), aggiungete la seguente configurazione di pacchetto struttura del repository al plug-in FileVault Maven. È possibile [creare un proprio pacchetto di struttura del repository per il progetto](repository-structure-package.md).

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

In `all/pom.xml`, aggiungere le seguenti `<embeddeds>` direttive alla dichiarazione del plug-in `filevault-package-maven-plugin`. Ricorda: **non** utilizzare la configurazione `<subPackages>`, in quanto includerà i pacchetti secondari in `/etc/packages` anziché in `/apps/my-app-packages/<application|content|container>/install(.author|.publish)?`.

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

          <!-- OSGi Bundle Jar file that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.core</artifactId>
              <type>jar</type>
              <target>/apps/my-app-packages/application/install</target>
          </embedded>

          <!-- Code package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.apps</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/application/install</target>
          </embedded>

           <!-- OSGi configuration code package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.config</artifactId>
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

          <!-- Include any other extra packages  -->
          <embedded>
              <groupId>com.vendor.x</groupId>
              <artifactId>vendor.plug-in.all</artifactId>
              <type>zip</type>
              <target>/apps/vendor-packages/container/install</target>
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

Se nelle destinazioni di incorporamento vengono utilizzati più `/apps/*-packages`, questi devono essere enumerati tutti in questo campo.

### Repository Maven di terze parti {#xml-3rd-party-maven-repositories}

>[!WARNING]
>
>L&#39;aggiunta di più repository Maven può estendere i tempi di creazione dei cibi mentre ulteriori repository Maven saranno controllati per dipendenze.

Nel progetto del reattore `pom.xml`, aggiungere le necessarie direttive di repository di Maven pubbliche di terze parti. La configurazione `<repository>` completa deve essere disponibile dal provider del repository di terze parti.

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

### Dipendenze del pacchetto tra `ui.apps` da `ui.content` pacchetti {#xml-package-dependencies}

In `ui.content/pom.xml`, aggiungere le seguenti `<dependencies>` direttive alla dichiarazione del plug-in `filevault-package-maven-plugin`.

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

In `all/pom.xml` aggiungere il plug-in `maven-clean-plugin` che pulirà la directory di destinazione prima delle build Maven.

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