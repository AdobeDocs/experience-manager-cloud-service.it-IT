---
title: Struttura dei progetti AEM
description: Scopri come definire le strutture dei pacchetti per la distribuzione nel Cloud Service Adobe Experience Manager.
translation-type: tm+mt
source-git-commit: f9a6dbec25b8154fda8069ff213aaaaa1d443ca1
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Struttura dei progetti AEM

>[!TIP]
>
>Acquisisci familiarità con l&#39;utilizzo di base di [AEM Project Archetype](https://docs.adobe.com/content/help/it/experience-manager-core-components/using/developing/archetype/overview.html) e con il [FileVault Content Maven Plug-in](/help/implementing/developing/tools/maven-plugin.md) in quanto questo articolo si basa su questi insegnamenti e concetti.

Questo articolo illustra le modifiche necessarie affinché i progetti Adobe Experience Manager Maven siano AEM come un Cloud Service compatibile, garantendo che rispettino la suddivisione di contenuti mutabili e immutabili, che le dipendenze siano stabilite per creare distribuzioni deterministiche non in conflitto e che siano inserite in una struttura distribuibile.

AEM implementazioni di applicazioni devono essere costituite da un singolo pacchetto AEM. Questo pacchetto deve a sua volta contenere pacchetti secondari che comprendono tutto ciò che l’applicazione deve funzionare, compresi il codice, la configurazione ed eventuali contenuti di base di supporto.

AEM richiede una separazione di **contenuto** e **codice**, il che significa che un singolo pacchetto di contenuti **non può** essere distribuito **sia** su `/apps` che su aree scrivibili di runtime dell’archivio (ad esempio `/content`, `/conf`, `/home` o tutto il resto fuorché `/apps`). Al contrario, l’applicazione deve separare codice e contenuto in pacchetti discreti da distribuire in AEM.

La struttura del pacchetto descritta in questo documento è compatibile **sia** con le distribuzioni di sviluppo locali che con le distribuzioni di AEM Cloud Service.

>[!TIP]
>
>Le configurazioni descritte in questo documento sono fornite da [AEM Project Maven Archetype 24 o versioni successive](https://github.com/adobe/aem-project-archetype/releases).

## Aree variabili e immutabili dell&#39;archivio {#mutable-vs-immutable}

`/apps` e `/libs`**sono considerate aree immutabili di AEM poiché non possono essere modificate (create, aggiornate, eliminate) dopo l’avvio di AEM (ad es. in fase di runtime).** Eventuali tentativi di modifica di un’area immutabile in fase di runtime avranno esito negativo.

Tutto il resto nel repository, `/content`, `/conf`, `/var`, `/etc`, `/oak:index`, `/system`, `/tmp`, ecc. sono tutte le aree **mutabili**, il che significa che possono essere modificate in fase di runtime.

>[!WARNING]
>
>Come nelle versioni precedenti di AEM, `/libs` non deve essere modificato. Solo AEM codice prodotto può essere distribuito su `/libs`.

### Indici Oak {#oak-indexes}

Gli indici Oak (`/oak:index`) sono gestiti specificamente dal AEM come processo di distribuzione del Cloud Service. Questo perché Cloud Manager deve attendere fino a quando non viene distribuito alcun nuovo indice e completamente reindicizzato prima di passare alla nuova immagine del codice.

Per questo motivo, anche se gli indici Oak sono modificabili in fase di esecuzione, devono essere distribuiti come codice in modo che possano essere installati prima che vengano installati pacchetti mutabili. Pertanto le configurazioni `/oak:index` fanno parte del pacchetto di codice e non del pacchetto di contenuti [come descritto di seguito](#recommended-package-structure).

>[!TIP]
>
>Per ulteriori dettagli sull&#39;indicizzazione in AEM come Cloud Service, consulta il documento [Ricerca e indicizzazione dei contenuti](/help/operations/indexing.md).

## Struttura del pacchetto consigliata {#recommended-package-structure}

![Experience Manager struttura del pacchetto di progetto](assets/content-package-organization.png)

Questo diagramma fornisce una panoramica della struttura di progetto consigliata e degli artefatti di distribuzione dei pacchetti.

La struttura di distribuzione dell&#39;applicazione consigliata è la seguente:

### Pacchetti di codice / Bundle OSGi

+ Il file Jar del bundle OSGi viene generato e incorporato direttamente in tutto il progetto.

+ Il pacchetto `ui.apps` contiene tutto il codice da distribuire e viene distribuito solo su `/apps`. Gli elementi comuni del pacchetto `ui.apps` includono, tra l&#39;altro:
   + [Definizioni dei componenti e ](https://docs.adobe.com/content/help/it-IT/experience-manager-htl/using/overview.html) script HTL
      + `/apps/my-app/components`
   + JavaScript e CSS (tramite [Librerie client](/help/implementing/developing/introduction/clientlibs.md))
      + `/apps/my-app/clientlibs`
   + [](/help/implementing/developing/introduction/overlays.md) Sovrapposizioni  `/libs`
      + `/apps/cq`, `/apps/dam/`, etc.
   + Configurazioni in base al contesto di fallback
      + `/apps/settings`
   + ACL (autorizzazioni)
      + Qualsiasi `rep:policy` per qualsiasi percorso sotto `/apps`

+ Il pacchetto `ui.config` contiene tutte le configurazioni [OSGi](/help/implementing/deploying/configuring-osgi.md):
   + Cartella organizzativa contenente definizioni di configurazione OSGi specifiche della modalità di esecuzione
      + `/apps/my-app/osgiconfig`
   + Cartella di configurazione OSGi comune contenente configurazioni OSGi predefinite che si applicano a tutti i AEM di destinazione come destinazioni di distribuzione di Cloud Service
      + `/apps/my-app/osgiconfig/config`
   + Esegui cartelle di configurazione OSGi specifiche per la modalità che contengono configurazioni OSGi predefinite applicabili a tutti i AEM di destinazione come destinazioni di distribuzione Cloud Service
      + `/apps/my-app/osgiconfig/config.<author|publish>.<dev|stage|prod>`
   + Script di configurazione OSGi di Repo Init
      + [Repo ](#repo-init) Initis è il modo consigliato per distribuire contenuto (mutabile) che fa parte logicamente dell&#39;applicazione AEM. Le configurazioni Repo Init OSGi devono trovarsi nella cartella `config.<runmode>` appropriata come descritto sopra e devono essere utilizzate per definire:
         + Strutture di contenuto di base
         + Utenti
         + Utenti del servizio
         + Gruppi
         + ACL (autorizzazioni)


### Pacchetti di contenuti

+ Il pacchetto `ui.content` contiene tutto il contenuto e la configurazione. Il pacchetto di contenuti contiene tutte le definizioni dei nodi che non sono presenti nei pacchetti `ui.apps` o `ui.config` o in altre parole, in elementi diversi da `/apps` o `/oak:index`. Gli elementi comuni del pacchetto `ui.content` includono, tra l&#39;altro:
   + Configurazioni in base al contesto
      + `/conf`
   + Strutture di contenuto complesse e necessarie (ad esempio Compilazione del contenuto che si basa e si estende oltre le strutture di contenuto della linea di base definite in Repo Init.)
      + `/content`,  `/content/dam`, ecc.
   + Tassonomie di assegnazione tag gestite
      + `/content/cq:tags`
   + Nodi legacy ecc (Idealmente, esegui la migrazione a posizioni diverse/ecc.)
      + `/etc`

### Pacchetti contenitore

+ Il pacchetto `all` è un pacchetto contenitore che include SOLO gli artefatti distribuibili, il file Jar del bundle OSGI, `ui.apps`, `ui.config` e i pacchetti `ui.content` come incorporamenti. Il pacchetto `all` non deve avere **alcun contenuto o codice** proprio, ma deve delegare tutta la distribuzione all&#39;archivio ai relativi pacchetti secondari o file Jar del bundle OSGi.

   I pacchetti sono ora inclusi utilizzando la configurazione incorporata del plug-in Maven [FileVault Package Maven](#embeddeds) anziché la configurazione `<subPackages>`.

   Per implementazioni Experienci Manager complesse, può essere opportuno creare più progetti/pacchetti `ui.apps`, `ui.config` e `ui.content` che rappresentano siti o tenant specifici in AEM. In questo caso, assicurati che la divisione tra contenuto variabile e immutabile sia rispettata e che i pacchetti di contenuto richiesti e i file Jar del bundle OSGi siano incorporati come pacchetti secondari nel pacchetto di contenuto contenitore `all` .

   Ad esempio, una struttura complessa dei pacchetti di contenuto di distribuzione potrebbe avere un aspetto simile al seguente:

   + `all` il pacchetto di contenuti incorpora i seguenti pacchetti, per creare un singolo artefatto di distribuzione
      + `common.ui.apps` distribuisce il codice richiesto sia dal  **** sito A che dal sito B
      + `site-a.core` Jar del bundle OSGi richiesto dal sito A
      + `site-a.ui.apps` distribuisce il codice richiesto dal sito A
      + `site-a.ui.config` distribuisce le configurazioni OSGi richieste dal sito A
      + `site-a.ui.content` distribuisce il contenuto e la configurazione richiesti dal sito A
      + `site-b.core` Jar del bundle OSGi richiesto dal sito B
      + `site-b.ui.apps` distribuisce il codice richiesto dal sito B
      + `site-b.ui.config` distribuisce le configurazioni OSGi richieste dal sito B
      + `site-b.ui.content` distribuisce il contenuto e la configurazione richiesti dal sito B

### Pacchetti applicativi aggiuntivi{#extra-application-packages}

Se la distribuzione AEM utilizza altri progetti AEM, che sono essi stessi costituiti da pacchetti di codice e contenuto propri, i relativi pacchetti contenitore devono essere incorporati nel pacchetto `all` del progetto.

Ad esempio, un progetto AEM che include 2 applicazioni AEM fornitori potrebbe avere un aspetto simile al seguente:

+ `all` il pacchetto di contenuti incorpora i seguenti pacchetti, per creare un singolo artefatto di distribuzione
   + `core` Jar del bundle OSGi richiesto dall&#39;applicazione AEM
   + `ui.apps` distribuisce il codice richiesto dall&#39;applicazione AEM
   + `ui.config` distribuisce le configurazioni OSGi richieste dall&#39;applicazione AEM
   + `ui.content` distribuisce il contenuto e la configurazione richiesti dall&#39;applicazione AEM
   + `vendor-x.all` distribuisce tutto (codice e contenuto) richiesto dall&#39;applicazione X del fornitore
   + `vendor-y.all` distribuisce tutti gli elementi (codice e contenuto) richiesti dall&#39;applicazione Y del fornitore

## Tipi di pacchetti {#package-types}

I pacchetti devono essere contrassegnati con il tipo di pacchetto dichiarato.

+ I pacchetti contenitore devono impostare i rispettivi `packageType` su `container`. I pacchetti contenitore non devono contenere direttamente i bundle OSGi, le configurazioni OSGi e non possono utilizzare [gli hook di installazione](http://jackrabbit.apache.org/filevault/installhooks.html).
+ I pacchetti di codice (immutabili) devono impostare i rispettivi `packageType` su `application`.
+ I pacchetti di contenuto (modificabili) devono impostare i rispettivi `packageType` su `content`.


Per ulteriori informazioni, consulta [Apache Jackrabbit FileVault - Package Maven Plugin documentation](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType) e il [frammento di configurazione FileVault Maven](#marking-packages-for-deployment-by-adoube-cloud-manager) qui sotto.

>[!TIP]
>
>Per un frammento completo, consulta la sezione [Frammenti XML POM](#xml-package-types) di seguito.

## Contrassegno dei pacchetti per la distribuzione tramite Adobe Cloud Manager {#marking-packages-for-deployment-by-adoube-cloud-manager}

Per impostazione predefinita, Adobe Cloud Manager raccoglie tutti i pacchetti prodotti dalla build Maven. Tuttavia, poiché il pacchetto contenitore (`all`) è l’unico artefatto di distribuzione che contiene tutti i pacchetti di codice e contenuto, è necessario assicurarsi che sia distribuito **solo** il pacchetto contenitore (`all`). Per questo motivo, gli altri pacchetti generati dalla build Maven devono essere contrassegnati con la configurazione FileVault Content Package Maven Plug-In di `<properties><cloudManagerTarget>none</cloudManageTarget></properties>`.

>[!TIP]
>
>Per un frammento completo, consulta la sezione [Frammenti XML POM](#pom-xml-snippets) di seguito.

## Repo Init{#repo-init}

Repo Init fornisce istruzioni, o script, che definiscono strutture JCR, che vanno dalle strutture di nodi comuni come strutture di cartelle, agli utenti, utente di servizio, gruppi e definizione ACL.

I vantaggi principali di Repo Init sono che dispongono di autorizzazioni implicite per eseguire tutte le azioni definite dai loro script e vengono richiamati all&#39;inizio del ciclo di vita dell&#39;implementazione, assicurando che tutte le strutture JCR necessarie esistano dal codice temporale.

Mentre gli script Repo Init stessi vivono nel progetto `ui.config` come script, possono e devono essere utilizzati per definire le seguenti strutture modificabili:

+ Strutture di contenuto di base
+ Utenti del servizio
+ Utenti
+ Gruppi
+ ACL

Gli script Repo Init vengono memorizzati come voci `scripts` di `RepositoryInitializer` configurazioni di fabbrica OSGi e possono quindi essere implicitamente indirizzati dalla modalità di esecuzione, consentendo differenze tra gli script Repo Init di AEM Author e AEM Publish Services o anche tra ambienti (Dev, Stage e Prod).

Le configurazioni OSGi di Repo Init sono meglio scritte nel formato di configurazione [`.config` OSGi](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-config-1) in quanto supportano le più righe, il che rappresenta un&#39;eccezione alle best practice relative all&#39;utilizzo di [`.cfg.json` per definire le configurazioni OSGi](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1).

Tieni presente che quando definisci Utenti e Gruppi, solo i gruppi vengono considerati parte dell’applicazione e che la relativa funzione deve essere integrata in questo campo. Gli utenti e i gruppi dell&#39;organizzazione devono ancora essere definiti in fase di runtime in AEM; ad esempio, se un flusso di lavoro personalizzato assegna il lavoro a un gruppo denominato, tale gruppo deve essere definito in tramite Repo Init nell&#39;applicazione AEM, tuttavia se il raggruppamento è puramente organizzativo, come &quot;Wendy&#39;s Team&quot; e &quot;Sean&#39;s Team&quot;, questi sono definiti al meglio e gestiti in fase di runtime in AEM.

>[!TIP]
>
>Gli script Repo Init *devono* essere definiti nel campo inline `scripts` e la configurazione `references` non funzionerà.

Il vocabolario completo per gli script Repo Init è disponibile nella documentazione [Apache Sling Repo Init](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

>[!TIP]
>
>Per un frammento completo, consulta la sezione [Repo Init Snippets](#snippet-repo-init) di seguito.

## Pacchetto struttura archivio {#repository-structure-package}

I pacchetti di codice richiedono la configurazione del plug-in FileVault Maven per fare riferimento a un `<repositoryStructurePackage>` che impone la correttezza delle dipendenze strutturali (per garantire che un pacchetto di codice non si installi su un altro). Puoi [creare un pacchetto di struttura dell&#39;archivio personalizzato per il progetto](repository-structure-package.md).

Questa operazione è **richiesta solo** per i pacchetti codice, ovvero per tutti i pacchetti contrassegnati con `<packageType>application</packageType>`.

Per informazioni su come creare un pacchetto della struttura dell&#39;archivio per l&#39;applicazione, consulta [Sviluppare un pacchetto della struttura dell&#39;archivio](repository-structure-package.md).

Tieni presente che i pacchetti di contenuto (`<packageType>content</packageType>`) **non** richiedono questo pacchetto di struttura dell’archivio.

>[!TIP]
>
>Per un frammento completo, consulta la sezione [Frammenti XML POM](#xml-repository-structure-package) di seguito.

## Incorporazione di pacchetti secondari nel pacchetto contenitore{#embeddeds}

I pacchetti di contenuto o codice vengono inseriti in una cartella speciale &quot;side-car&quot; e possono essere destinati all&#39;installazione su AEM autore, AEM pubblicazione o entrambi, utilizzando la configurazione `<embeddeds>` del plug-in FileVault Maven. Tieni presente che la configurazione `<subPackages>` non deve essere utilizzata.

I casi d’uso comuni includono:

+ ACL/autorizzazioni che differiscono tra gli utenti AEM autore e AEM utenti di pubblicazione
+ Configurazioni utilizzate per supportare attività solo su AEM autore
+ Codice come le integrazioni con i sistemi di back-office, necessario solo per l&#39;esecuzione su AEM autore

![Incorporazione di pacchetti](assets/embeddeds.png)

Per eseguire il targeting AEM autore, AEM pubblicazione o entrambi, il pacchetto è incorporato nel pacchetto contenitore `all` in una cartella-posizione speciale, nel seguente formato:

`/apps/<app-name>-packages/(content|application|container)/install(.author|.publish)?`

Scomposizione della struttura delle cartelle:

+ La cartella di primo livello **deve essere** `/apps`.
+ La cartella di secondo livello rappresenta l&#39;applicazione con `-packages` post-fisso sul nome della cartella. Spesso esiste solo una singola cartella di 2° livello in cui sono incorporati tutti i pacchetti secondari, tuttavia è possibile creare un numero qualsiasi di cartelle di 2° livello per rappresentare al meglio la struttura logica dell&#39;applicazione:
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`

   >[!WARNING]
   >
   >Per convenzione, le cartelle incorporate in un pacchetto secondario sono denominate con il suffisso `-packages`. In questo modo, il codice di distribuzione e i pacchetti di contenuto **non** vengono distribuiti nelle cartelle di destinazione di qualsiasi pacchetto secondario `/apps/<app-name>/...`, il che provoca un comportamento di installazione distruttivo e ciclico.

+ La cartella di terzo livello deve essere
   `application`,  `content` o  `container`
   + La cartella `application` contiene pacchetti di codice
   + La cartella `content` contiene pacchetti di contenuto
   + La cartella `container` contiene tutti i [pacchetti applicativi aggiuntivi](#extra-application-packages) che possono essere inclusi dall&#39;applicazione AEM.
Questo nome della cartella corrisponde ai [tipi di pacchetto](#package-types) dei pacchetti che contiene.
+ La cartella di quarto livello contiene i pacchetti secondari e deve corrispondere a una delle seguenti:
   + `install` per effettuare l’installazione **sia su** AEM Author che AEM Publish
   + `install.author` per eseguire l’installazione **solo** su AEM Author
   + `install.publish` per  **** eseguire l&#39;installazione solo su AEM pubblicazione Nota che solo  `install.author` e  `install.publish` sono destinazioni supportate. Altre modalità di esecuzione **non sono** supportate.

Ad esempio, una distribuzione che contiene AEM pacchetti specifici per l’authoring e la pubblicazione può avere un aspetto simile al seguente:

+ `all` Il pacchetto contenitore incorpora i seguenti pacchetti, per creare un singolo artefatto di distribuzione
   + `ui.apps` incorporato in  `/apps/my-app-packages/application/install` distribuisce il codice sia per l’authoring AEM che per la pubblicazione AEM
   + `ui.apps.author` incorporato in  `/apps/my-app-packages/application/install.author` distribuisce il codice solo AEM autore
   + `ui.content` incorporato in  `/apps/my-app-packages/content/install` distribuisce contenuti e configurazioni sia per l’authoring AEM che per la pubblicazione AEM
   + `ui.content.publish` incorporato in  `/apps/my-app-packages/content/install.publish` distribuisce contenuto e configurazione per AEM solo pubblicazione

>[!TIP]
>
>Per un frammento completo, consulta la sezione [Frammenti XML POM](#xml-embeddeds) di seguito.

### Definizione del filtro del pacchetto contenitore {#container-package-filter-definition}

A causa dell’incorporazione del codice e dei pacchetti secondari del contenuto nel pacchetto contenitore, i percorsi di destinazione incorporati devono essere aggiunti al `filter.xml` del progetto contenitore per garantire che i pacchetti incorporati siano inclusi nel pacchetto contenitore quando generato.

È sufficiente aggiungere le voci `<filter root="/apps/<my-app>-packages"/>` per tutte le cartelle di secondo livello che contengono pacchetti secondari da distribuire.

>[!TIP]
>
>Per un frammento completo, consulta la sezione [Frammenti XML POM](#xml-container-package-filters) di seguito.

## Incorporazione di pacchetti di terze parti {#embedding-3rd-party-packages}

Tutti i pacchetti devono essere disponibili tramite l’ [archivio degli artefatti Maven pubblico di Adobe](https://repo.adobe.com/nexus/content/groups/public/com/adobe/) o un archivio degli artefatti Maven di terze parti accessibile al pubblico e di riferimento.

Se i pacchetti di terze parti si trovano nell’**archivio di artefatti Maven pubblico di Adobe**, per consentire ad Adobe Cloud Manager di risolvere gli artefatti non è necessario effettuare nessuna ulteriore configurazione.

Se i pacchetti di terze parti si trovano in un **archivio di artefatti Maven pubblico di terze parti**, tale archivio deve essere registrato nel `pom.xml` del progetto, per poi essere incorporato seguendo il metodo [descritto sopra](#embeddeds).

I connettori/applicazioni di terze parti devono essere incorporati utilizzando il relativo pacchetto `all` come contenitore nel pacchetto contenitore del progetto (`all`).

L’aggiunta delle dipendenze Maven segue le pratiche Maven standard e l’incorporazione di artefatti di terze parti (pacchetti di codice e contenuto) è [descritta sopra](#embedding-3rd-party-packages).

>[!TIP]
>
>Per un frammento completo, consulta la sezione [Frammenti XML POM](#xml-3rd-party-maven-repositories) di seguito.

## Dipendenze del pacchetto tra `ui.apps` da `ui.content` Pacchetti {#package-dependencies}

Al fine di garantire la corretta installazione dei pacchetti, si raccomanda di stabilire dipendenze tra i pacchetti.

La regola generale è che i pacchetti contenenti contenuto variabile (`ui.content`) devono dipendere dal codice immutabile (`ui.apps`) che supporta il rendering e l’utilizzo del contenuto modificabile.

Un&#39;eccezione notevole a questa regola generale è se il pacchetto di codice immutabile (`ui.apps` o qualsiasi altro), __solo__ contiene i bundle OSGi. In tal caso, nessun pacchetto AEM deve dichiarare una dipendenza da esso. Questo perché i pacchetti di codice immutabili __solo__ contenenti bundle OSGi non sono registrati con AEM Package Manager, e quindi, qualsiasi pacchetto AEM a seconda di esso avrà una dipendenza non soddisfatta e non sarà possibile installarlo.

>[!TIP]
>
>Per un frammento completo, consulta la sezione [Frammenti XML POM](#xml-package-dependencies) di seguito.

I pattern comuni per le dipendenze dei pacchetti di contenuto sono:

### Dipendenze semplici del pacchetto di distribuzione {#simple-deployment-package-dependencies}

Il caso semplice imposta il pacchetto di contenuto variabile `ui.content` in modo che dipenda dal pacchetto di codice immutabile `ui.apps` .

+ `all` non ha dipendenze
   + `ui.apps` non ha dipendenze
   + `ui.content` dipende da  `ui.apps`

### Dipendenze del pacchetto di distribuzione complesse {#complex-deploxment-package-dependencies}

Le implementazioni complesse si espandono in base al caso semplice e impostano le dipendenze tra il contenuto variabile corrispondente e i pacchetti di codice immutabili. Se necessario, le dipendenze possono essere stabilite anche tra pacchetti di codice immutabili.

+ `all` non ha dipendenze
   + `common.ui.apps.common` non ha dipendenze
   + `site-a.ui.apps` dipende da  `common.ui.apps`
   + `site-a.ui.content` dipende da  `site-a.ui.apps`
   + `site-b.ui.apps` dipende da  `common.ui.apps`
   + `site-b.ui.content` dipende da  `site-b.ui.apps`

## Sviluppo locale e distribuzione {#local-development-and-deployment}

Le strutture e l&#39;organizzazione del progetto descritte in questo articolo sono **istanze di sviluppo locale completamente compatibili** AEM.

## Snippet XML POM {#pom-xml-snippets}

Di seguito sono riportati i snippet di configurazione Maven `pom.xml` che possono essere aggiunti ai progetti Maven per allinearli alle raccomandazioni di cui sopra.

### Tipi di pacchetti {#xml-package-types}

I pacchetti di codice e di contenuto, distribuiti come pacchetti secondari, devono dichiarare un pacchetto di tipo **applicazione** o **contenuto**, a seconda di ciò che contengono.

#### Tipi di pacchetti contenitore {#container-package-types}

Il progetto contenitore `all/pom.xml` **non** dichiara un `<packageType>`.

#### Tipi di pacchetti di codice (immutabile) {#immutable-package-types}

I pacchetti di codice devono impostare i rispettivi `packageType` su `application`.

Nelle `ui.apps/pom.xml`, le direttive di configurazione della build `<packageType>application</packageType>` della dichiarazione del plug-in `filevault-package-maven-plugin` dichiarano il tipo di pacchetto.

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

#### Tipi di pacchetti contenuti (variabili) {#mutable-package-types}

I pacchetti di contenuto devono impostare i rispettivi `packageType` su `content`.

Nella `ui.content/pom.xml`, la direttiva di configurazione della build `<packageType>content</packageType>` della dichiarazione del plug-in `filevault-package-maven-plugin` dichiara il tipo di pacchetto.

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

### Contrassegno dei pacchetti per la distribuzione di Adobe Cloud Manager {#cloud-manager-target}

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

Gli script Repo Init che contengono gli script Repo Init sono definiti nella configurazione di fabbrica `RepositoryInitializer` OSGi tramite la proprietà `scripts` . Tieni presente che questi script definiti nelle configurazioni OSGi, possono essere facilmente delimitati dalla modalità di esecuzione utilizzando la semantica di cartelle `../config.<runmode>` usuale.

Poiché gli script sono in genere dichiarazioni su più righe, è più facile definirli nel file `.config` rispetto al formato `.cfg.json` basato su JSON.

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

La proprietà `scripts` OSGi contiene direttive definite dalla lingua Repo Init di [Apache Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

### Pacchetto struttura archivio {#xml-repository-structure-package}

Nel `ui.apps/pom.xml` e in qualsiasi altro `pom.xml` che dichiara un pacchetto di codice (`<packageType>application</packageType>`), aggiungi la seguente configurazione del pacchetto della struttura dell&#39;archivio al plug-in FileVault Maven. Puoi [creare un pacchetto di struttura dell&#39;archivio personalizzato per il progetto](repository-structure-package.md).

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

In `all/pom.xml`, aggiungi le seguenti `<embeddeds>` direttive alla dichiarazione del plug-in `filevault-package-maven-plugin`. Ricorda che **non** utilizza la configurazione `<subPackages>`, in quanto includerà i pacchetti secondari in `/etc/packages` anziché `/apps/my-app-packages/<application|content|container>/install(.author|.publish)?`.

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

### Definizione del filtro del pacchetto contenitore {#xml-container-package-filters}

Nel `filter.xml` `all` del progetto (`all/src/main/content/jcr_root/META-INF/vault/definition/filter.xml`), **includi** tutte le cartelle `-packages` che contengono pacchetti secondari da distribuire:

```xml
<filter root="/apps/my-app-packages"/>
```

Se nelle destinazioni di incorporamento vengono utilizzati più `/apps/*-packages`, è necessario enumerarli tutti qui.

### Repository Maven di terze parti {#xml-3rd-party-maven-repositories}

>[!WARNING]
>
>L’aggiunta di più archivi Maven può estendere i tempi di creazione Maven, in quanto ulteriori archivi Maven saranno controllati per verificare la presenza di dipendenze.

Nel progetto di reattore `pom.xml`, aggiungi tutte le necessarie direttive di repository Maven pubbliche di terze parti. La configurazione `<repository>` completa deve essere disponibile dal provider di archivio di terze parti.

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

### Dipendenze del pacchetto tra `ui.apps` da `ui.content` Pacchetti {#xml-package-dependencies}

In `ui.content/pom.xml`, aggiungi le seguenti `<dependencies>` direttive alla dichiarazione del plug-in `filevault-package-maven-plugin`.

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

In `all/pom.xml` aggiungi il plug-in `maven-clean-plugin` che pulirà la directory di destinazione prima delle build Maven.

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

+ [Gestione dei pacchetti con Maven](/help/implementing/developing/tools/maven-plugin.md)
+ [Plug-in Maven pacchetto di contenuti FileVault](http://jackrabbit.apache.org/filevault-package-maven-plugin/)
