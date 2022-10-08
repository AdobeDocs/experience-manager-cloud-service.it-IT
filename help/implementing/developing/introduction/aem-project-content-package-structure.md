---
title: Struttura dei progetti AEM
description: Scopri come definire le strutture dei pacchetti per la distribuzione in Adobe Experience Manager Cloud Service.
exl-id: 38f05723-5dad-417f-81ed-78a09880512a
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '2931'
ht-degree: 12%

---

# Struttura dei progetti AEM

>[!TIP]
>
>Acquisire familiarità con le funzioni di base [Utilizzo di AEM Project Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it)e [Plug-in Maven contenuto FileVault](/help/implementing/developing/tools/maven-plugin.md) come questo articolo si basa su questi insegnamenti e concetti.

Il presente articolo illustra le modifiche necessarie affinché i progetti Adobe Experience Manager Maven siano AEM compatibili con l’as a Cloud Service, garantendo che rispettino la suddivisione dei contenuti mutabili e immutabili, che le dipendenze siano stabilite per creare distribuzioni deterministiche non in conflitto e che siano inserite in una struttura distribuibile.

AEM implementazioni di applicazioni devono essere costituite da un singolo pacchetto AEM. Questo pacchetto deve a sua volta contenere pacchetti secondari che comprendono tutto ciò che l’applicazione deve funzionare, compresi il codice, la configurazione ed eventuali contenuti di base di supporto.

AEM richiede una separazione **content** e **codice**, che significa un unico pacchetto di contenuti **impossibile** distribuire **entrambi** `/apps` e aree scrivibili in fase di esecuzione (ad esempio, `/content`, `/conf`, `/home`o altro `/apps`) del repository. Al contrario, l’applicazione deve separare codice e contenuto in pacchetti discreti da distribuire in AEM.

La struttura del pacchetto descritta in questo documento è compatibile **sia** con le distribuzioni di sviluppo locali che con le distribuzioni di AEM Cloud Service.

>[!TIP]
>
>Le configurazioni descritte in questo documento sono fornite da [AEM Project Maven Archetype 24 o successivo](https://github.com/adobe/aem-project-archetype/releases).

## Aree variabili e immutabili dell&#39;archivio {#mutable-vs-immutable}

`/apps` e `/libs`**sono considerate aree immutabili di AEM poiché non possono essere modificate (create, aggiornate, eliminate) dopo l’avvio di AEM (ad es. in fase di runtime).** Eventuali tentativi di modifica di un’area immutabile in fase di runtime avranno esito negativo.

Tutto il resto nell&#39;archivio, `/content`, `/conf`, `/var`, `/etc`, `/oak:index`, `/system`, `/tmp`, ecc. sono tutti **mutabile** aree, ovvero possono essere modificate in fase di runtime.

>[!WARNING]
>
>Come nelle versioni precedenti di AEM, `/libs` non devono essere modificate. È possibile distribuire solo AEM codice prodotto in `/libs`.

### Indici Oak {#oak-indexes}

Indici Oak (`/oak:index`) sono gestite in modo specifico dal processo di distribuzione as a Cloud Service AEM. Questo perché Cloud Manager deve attendere fino a quando non viene distribuito alcun nuovo indice e completamente reindicizzato prima di passare alla nuova immagine del codice.

Per questo motivo, anche se gli indici Oak sono modificabili in fase di esecuzione, devono essere distribuiti come codice in modo che possano essere installati prima che vengano installati pacchetti mutabili. Pertanto `/oak:index` Le configurazioni fanno parte del pacchetto di codice e non fanno parte del pacchetto di contenuti [come descritto di seguito](#recommended-package-structure).

>[!TIP]
>
>Per ulteriori dettagli sull&#39;indicizzazione in AEM as a Cloud Service, consulta il documento [Ricerca e indicizzazione dei contenuti](/help/operations/indexing.md).

## Struttura del pacchetto consigliata {#recommended-package-structure}

![Experience Manager struttura del pacchetto di progetto](assets/content-package-organization.png)

Questo diagramma fornisce una panoramica della struttura di progetto consigliata e degli artefatti di distribuzione dei pacchetti.

La struttura di distribuzione dell&#39;applicazione consigliata è la seguente:

### Pacchetti di codice / Bundle OSGi

+ Il file Jar del bundle OSGi viene generato e incorporato direttamente in tutto il progetto.

+ La `ui.apps` il pacchetto contiene tutto il codice da distribuire e distribuisce solo in `/apps`. Elementi comuni `ui.apps` Il pacchetto include, ma non è limitato a:
   + [Definizioni dei componenti e HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=it) script
      + `/apps/my-app/components`
   + JavaScript e CSS (tramite [Librerie client](/help/implementing/developing/introduction/clientlibs.md))
      + `/apps/my-app/clientlibs`
   + [Sovrapposizioni](/help/implementing/developing/introduction/overlays.md) di `/libs`
      + `/apps/cq`, `/apps/dam/`, ecc.
   + Configurazioni in base al contesto di fallback
      + `/apps/settings`
   + ACL (autorizzazioni)
      + Qualsiasi `rep:policy` per qualsiasi percorso `/apps`
   + [Script raggruppati precompilati](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/precompiled-bundled-scripts.html)

>[!NOTE]
>
>Lo stesso codice deve essere distribuito a tutti gli ambienti. Ciò è necessario per garantire un livello di convalide di affidabilità anche nell’ambiente stage. Per ulteriori informazioni, consulta la sezione su [Modalità di esecuzione](/help/implementing/deploying/overview.md#runmodes).


### Pacchetti di contenuti

+ La `ui.content` il pacchetto contiene tutto il contenuto e la configurazione. Il pacchetto di contenuti contiene tutte le definizioni dei nodi non incluse nella `ui.apps` o `ui.config` pacchetti, o in altre parole, qualsiasi cosa non in `/apps` o `/oak:index`. Elementi comuni `ui.content` Il pacchetto include, ma non è limitato a:
   + Configurazioni in base al contesto
      + `/conf`
   + Strutture di contenuto complesse e necessarie (ad esempio Compilazione del contenuto che si basa e si estende oltre le strutture di contenuto della linea di base definite in Repo Init.)
      + `/content`, `/content/dam`, ecc.
   + Tassonomie di assegnazione tag gestite
      + `/content/cq:tags`
   + Nodi legacy ecc (Idealmente, esegui la migrazione a posizioni diverse/ecc.)
      + `/etc`

### Pacchetti contenitore

+ La `all` pacchetto contenitore che include SOLO gli artefatti distribuibili, il file Jar del bundle OSGI, `ui.apps`, `ui.config` e `ui.content` pacchetti come incorporamenti. La `all` il pacchetto non deve avere **qualsiasi contenuto o codice** di per sé, ma delegare tutta la distribuzione all&#39;archivio ai relativi pacchetti secondari o file Jar del bundle OSGi.

   I pacchetti sono ora inclusi utilizzando Maven [Configurazione incorporamenti del plug-in Maven del pacchetto FileVault](#embeddeds), anziché `<subPackages>` configurazione.

   Per implementazioni Experienci Manager complesse, può essere utile creare più `ui.apps`, `ui.config` e `ui.content` progetti/pacchetti che rappresentano siti o tenant specifici in AEM. In questo caso, assicurati che la divisione tra contenuto variabile e immutabile sia rispettata e che i pacchetti di contenuto richiesti e i file Jar del bundle OSGi siano incorporati come pacchetti secondari nel `all` pacchetto di contenuto del contenitore.

   Ad esempio, una struttura complessa dei pacchetti di contenuto di distribuzione potrebbe avere un aspetto simile al seguente:

   + `all` il pacchetto di contenuti incorpora i seguenti pacchetti, per creare un singolo artefatto di distribuzione
      + `common.ui.apps` distribuisce il codice richiesto da **entrambi** sito A e sito B
      + `site-a.core` Jar del bundle OSGi richiesto dal sito A
      + `site-a.ui.apps` distribuisce il codice richiesto dal sito A
      + `site-a.ui.config` distribuisce le configurazioni OSGi richieste dal sito A
      + `site-a.ui.content` distribuisce il contenuto e la configurazione richiesti dal sito A
      + `site-b.core` Jar del bundle OSGi richiesto dal sito B
      + `site-b.ui.apps` distribuisce il codice richiesto dal sito B
      + `site-b.ui.config` distribuisce le configurazioni OSGi richieste dal sito B
      + `site-b.ui.content` distribuisce il contenuto e la configurazione richiesti dal sito B

+ La `ui.config` pacchetto contiene tutto [Configurazioni OSGi](/help/implementing/deploying/configuring-osgi.md):
   + È stato preso in considerazione il codice e appartiene ai bundle OSGi ma non contiene nodi di contenuto regolari. Così è contrassegnato come un pacchetto contenitore
   + Cartella organizzativa contenente definizioni di configurazione OSGi specifiche della modalità di esecuzione
      + `/apps/my-app/osgiconfig`
   + Cartella di configurazione OSGi comune contenente configurazioni OSGi predefinite che si applicano a tutte le destinazioni di distribuzione as a Cloud Service AEM target
      + `/apps/my-app/osgiconfig/config`
   + Cartelle di configurazione OSGi specifiche per la modalità di esecuzione che contengono configurazioni OSGi predefinite applicabili a tutte le destinazioni di distribuzione as a Cloud Service AEM target
      + `/apps/my-app/osgiconfig/config.<author|publish>.<dev|stage|prod>`
   + Script di configurazione OSGi di Repo Init
      + [Inizio repository](#repo-init) è il metodo consigliato per distribuire (variabile) contenuti che fanno parte logica dell’applicazione AEM. Le configurazioni Repo Init OSGi devono essere posizionate nelle posizioni appropriate `config.<runmode>` come descritto in precedenza e può essere utilizzato per definire:
         + Strutture di contenuto di base
         + Utenti
         + Utenti del servizio
         + Gruppi
         + ACL (autorizzazioni)

### Pacchetti applicativi aggiuntivi{#extra-application-packages}

Se la distribuzione AEM utilizza altri progetti AEM, che sono essi stessi costituiti da pacchetti di codice e contenuto propri, i relativi pacchetti contenitore devono essere incorporati nel `all` pacchetto.

Ad esempio, un progetto AEM che include 2 applicazioni AEM fornitori potrebbe avere un aspetto simile al seguente:

+ `all` il pacchetto di contenuti incorpora i seguenti pacchetti, per creare un singolo artefatto di distribuzione
   + `core` Jar del bundle OSGi richiesto dall&#39;applicazione AEM
   + `ui.apps` distribuisce il codice richiesto dall&#39;applicazione AEM
   + `ui.config` distribuisce le configurazioni OSGi richieste dall&#39;applicazione AEM
   + `ui.content` distribuisce il contenuto e la configurazione richiesti dall&#39;applicazione AEM
   + `vendor-x.all` distribuisce tutto (codice e contenuto) richiesto dall&#39;applicazione X del fornitore
   + `vendor-y.all` distribuisce tutti gli elementi (codice e contenuto) richiesti dall&#39;applicazione Y del fornitore

## Tipi di pacchetti {#package-types}

I pacchetti devono essere contrassegnati con il tipo di pacchetto dichiarato. I tipi di pacchetto consentono di chiarire lo scopo e la distribuzione di un pacchetto.

+ I pacchetti contenitore devono impostare i relativi `packageType` a `container`. I pacchetti contenitore non devono contenere nodi regolari. Sono consentiti solo bundle, configurazioni e pacchetti secondari OSGi. I contenitori in AEM as a Cloud Service non possono utilizzare [installare gli hook](https://jackrabbit.apache.org/filevault/installhooks.html).
+ I pacchetti di codice (immutabili) devono impostare i rispettivi `packageType` a `application`.
+ I pacchetti di contenuto (mutabili) devono impostare i relativi `packageType` a `content`.


Per ulteriori informazioni consulta [FileVault Apache Jackrabbit - Documentazione del plugin Maven](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType), [Tipi di pacchetti Apache Jackrabbit](https://jackrabbit.apache.org/filevault/packagetypes.html)e [Frammento di configurazione FileVault Maven](#marking-packages-for-deployment-by-adoube-cloud-manager) sotto.

>[!TIP]
>
>Consulta la sezione [Snippet XML POM](#xml-package-types) sezione seguente per un frammento completo.

## Contrassegno dei pacchetti per la distribuzione tramite Adobe Cloud Manager {#marking-packages-for-deployment-by-adoube-cloud-manager}

Per impostazione predefinita, Adobe Cloud Manager raccoglie tutti i pacchetti prodotti dalla build Maven. Tuttavia, poiché il pacchetto contenitore (`all`) è l’unico artefatto di distribuzione che contiene tutti i pacchetti di codice e contenuto, è necessario assicurarsi che sia distribuito **solo** il pacchetto contenitore (`all`). Per questo motivo, gli altri pacchetti generati dalla build Maven devono essere contrassegnati con la configurazione FileVault Content Package Maven Plug-In di `<properties><cloudManagerTarget>none</cloudManageTarget></properties>`.

>[!TIP]
>
>Consulta la sezione [Snippet XML POM](#pom-xml-snippets) sezione seguente per un frammento completo.

## Inizio repository{#repo-init}

Repo Init fornisce istruzioni, o script, che definiscono strutture JCR, che vanno dalle strutture di nodi comuni come strutture di cartelle, agli utenti, utente di servizio, gruppi e definizione ACL.

I vantaggi principali di Repo Init sono che dispongono di autorizzazioni implicite per eseguire tutte le azioni definite dai loro script e vengono richiamati all&#39;inizio del ciclo di vita dell&#39;implementazione, assicurando che tutte le strutture JCR necessarie esistano dal codice temporale.

Mentre gli script Repo Init stessi vivono nel `ui.config` possono e devono essere utilizzati come script per definire le seguenti strutture mutabili:

+ Strutture di contenuto di base
+ Utenti del servizio
+ Utenti
+ Gruppi
+ ACL

Gli script Repo Init sono memorizzati come `scripts` voci `RepositoryInitializer` Le configurazioni di fabbrica OSGi, e quindi, possono essere eseguite in modo implicito in modalità di esecuzione, consentendo differenze tra gli script Repo Init di AEM Author e AEM Publish Services o anche tra ambienti (Dev, Stage e Prod).

Le configurazioni OSGi di Repo Init sono meglio scritte nel [`.config` Formato di configurazione OSGi](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-config-1) in quanto supportano più righe, il che costituisce un&#39;eccezione alle best practice relative all&#39;utilizzo [`.cfg.json` per definire le configurazioni OSGi](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1).

Tieni presente che quando definisci Utenti e Gruppi, solo i gruppi vengono considerati parte dell’applicazione e che la relativa funzione deve essere integrata in questo campo. Gli utenti e i gruppi dell&#39;organizzazione devono ancora essere definiti in fase di runtime in AEM; ad esempio, se un flusso di lavoro personalizzato assegna il lavoro a un gruppo denominato, tale gruppo deve essere definito in tramite Repo Init nell&#39;applicazione AEM, tuttavia se il raggruppamento è puramente organizzativo, come &quot;Wendy&#39;s Team&quot; e &quot;Sean&#39;s Team&quot;, questi sono definiti al meglio e gestiti in fase di runtime in AEM.

>[!TIP]
>
>Script Repo Init *deve* essere definito in linea `scripts` e `references` la configurazione non funzionerà.

Il vocabolario completo per gli script Repo Init è disponibile sul sito [Documentazione di Apache Sling Repo Init](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

>[!TIP]
>
>Consulta la sezione [Snippet di informazioni repository](#snippet-repo-init) sezione seguente per un frammento completo.

## Pacchetto struttura archivio {#repository-structure-package}

I pacchetti di codice richiedono la configurazione del plug-in FileVault Maven per fare riferimento a un `<repositoryStructurePackage>` che applica la correttezza delle dipendenze strutturali (per garantire che un pacchetto di codice non si installi su un altro). È possibile [crea un pacchetto personalizzato per la struttura dell’archivio per il progetto](repository-structure-package.md).

Questa operazione è **richiesta solo** per i pacchetti codice, ovvero per tutti i pacchetti contrassegnati con `<packageType>application</packageType>`.

Per informazioni su come creare un pacchetto della struttura dell&#39;archivio per l&#39;applicazione, vedi [Sviluppare un pacchetto con la struttura dell’archivio](repository-structure-package.md).

Tieni presente che i pacchetti di contenuto (`<packageType>content</packageType>`) **non** richiede questo pacchetto della struttura dell&#39;archivio.

>[!TIP]
>
>Consulta la sezione [Snippet XML POM](#xml-repository-structure-package) sezione seguente per un frammento completo.

## Incorporazione di pacchetti secondari nel pacchetto contenitore{#embeddeds}

I pacchetti di contenuto o codice vengono inseriti in una cartella speciale &quot;side-car&quot; e possono essere destinati all&#39;installazione su AEM autore, AEM pubblicazione o entrambi, utilizzando il plug-in FileVault Maven `<embeddeds>` configurazione. Tieni presente che `<subPackages>` la configurazione non deve essere utilizzata.

I casi d’uso comuni includono:

+ ACL/autorizzazioni che differiscono tra gli utenti AEM autore e AEM utenti di pubblicazione
+ Configurazioni utilizzate per supportare attività solo su AEM autore
+ Codice come le integrazioni con i sistemi di back-office, necessario solo per l&#39;esecuzione su AEM autore

![Incorporazione di pacchetti](assets/embeddeds.png)

Per eseguire il targeting AEM autore, AEM pubblicazione o entrambi, il pacchetto è incorporato nel `all` pacchetto contenitore in una cartella-posizione speciale, nel seguente formato:

`/apps/<app-name>-packages/(content|application|container)/install(.author|.publish)?`

Scomposizione della struttura delle cartelle:

+ Cartella di primo livello **devono** `/apps`.
+ La cartella di secondo livello rappresenta l&#39;applicazione con `-packages` post-fisso al nome della cartella. Spesso esiste solo una singola cartella di 2° livello in cui sono incorporati tutti i pacchetti secondari, tuttavia è possibile creare un numero qualsiasi di cartelle di 2° livello per rappresentare al meglio la struttura logica dell&#39;applicazione:
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`

   >[!WARNING]
   >
   >Per convenzione, le cartelle incorporate in un pacchetto secondario sono denominate con il suffisso `-packages`. In questo modo, il codice di distribuzione e i pacchetti di contenuto **non** vengono distribuiti nelle cartelle di destinazione di qualsiasi pacchetto secondario `/apps/<app-name>/...`, il che provoca un comportamento di installazione distruttivo e ciclico.

+ La cartella di terzo livello deve essere
   `application`, `content` oppure `container`
   + La `application` cartella contiene pacchetti di codice
   + La `content` la cartella contiene pacchetti di contenuto
   + La `container` cartella contiene qualsiasi [pacchetti applicativi aggiuntivi](#extra-application-packages) che potrebbe essere incluso nell&#39;applicazione AEM.
Questo nome della cartella corrisponde al [tipi di pacchetto](#package-types) dei pacchetti che contiene.
+ La cartella di quarto livello contiene i pacchetti secondari e deve corrispondere a una delle seguenti:
   + `install` per effettuare l’installazione **sia su** AEM Author che AEM Publish
   + `install.author` per eseguire l’installazione **solo** su AEM Author
   + `install.publish` a **only** installa su AEM pubblica Nota che solo `install.author` e `install.publish` sono destinazioni supportate. Altre modalità di esecuzione **non sono** supportate.

Ad esempio, una distribuzione che contiene AEM pacchetti specifici per l’authoring e la pubblicazione può avere un aspetto simile al seguente:

+ `all` Il pacchetto contenitore incorpora i seguenti pacchetti, per creare un singolo artefatto di distribuzione
   + `ui.apps` incorporato in `/apps/my-app-packages/application/install` distribuisce il codice sia per l&#39;autore AEM che per AEM pubblicare
   + `ui.apps.author` incorporato in `/apps/my-app-packages/application/install.author` distribuisce il codice solo AEM autore
   + `ui.content` incorporato in `/apps/my-app-packages/content/install` distribuisce contenuti e configurazioni sia per AEM creazione che per AEM pubblicazione
   + `ui.content.publish` incorporato in `/apps/my-app-packages/content/install.publish` distribuisce contenuto e configurazione solo AEM pubblicazione

>[!TIP]
>
>Consulta la sezione [Snippet XML POM](#xml-embeddeds) sezione seguente per un frammento completo.

### Definizione del filtro del pacchetto contenitore {#container-package-filter-definition}

A causa dell’incorporazione del codice e dei pacchetti secondari del contenuto nel pacchetto contenitore, i percorsi di destinazione incorporati devono essere aggiunti al del progetto contenitore `filter.xml` per garantire che i pacchetti incorporati siano inclusi nel pacchetto contenitore quando generato.

Aggiungi semplicemente il `<filter root="/apps/<my-app>-packages"/>` voci per qualsiasi cartella di secondo livello che contiene pacchetti secondari da distribuire.

>[!TIP]
>
>Consulta la sezione [Snippet XML POM](#xml-container-package-filters) sezione seguente per un frammento completo.

## Incorporazione di pacchetti di terze parti {#embedding-3rd-party-packages}

Tutti i pacchetti devono essere disponibili tramite [Archivio degli artefatti Maven pubblico di Adobe](https://repo1.maven.org/maven2/com/adobe/) o un archivio di artefatti Maven di terze parti accessibile al pubblico.

Se i pacchetti di terze parti si trovano nell’**archivio di artefatti Maven pubblico di Adobe**, per consentire ad Adobe Cloud Manager di risolvere gli artefatti non è necessario effettuare nessuna ulteriore configurazione.

Se i pacchetti di terze parti si trovano in un **archivio di artefatti Maven pubblico di terze parti**, tale archivio deve essere registrato nel `pom.xml` del progetto, per poi essere incorporato seguendo il metodo [descritto sopra](#embeddeds).

Le applicazioni/i connettori di terze parti devono essere incorporati utilizzando `all` come contenitore nel contenitore del progetto (`all`).

L’aggiunta delle dipendenze Maven segue le pratiche Maven standard e l’incorporazione di artefatti di terze parti (pacchetti di codice e contenuto) è [sopra descritto](#embedding-3rd-party-packages).

>[!TIP]
>
>Consulta la sezione [Snippet XML POM](#xml-3rd-party-maven-repositories) sezione seguente per un frammento completo.

## Dipendenze del pacchetto tra `ui.apps` da `ui.content` Pacchetti {#package-dependencies}

Al fine di garantire la corretta installazione dei pacchetti, si raccomanda di stabilire dipendenze tra i pacchetti.

La regola generale è costituita dai pacchetti contenenti contenuto variabile (`ui.content`) deve dipendere dal codice immutabile (`ui.apps`) che supporta il rendering e l’utilizzo del contenuto modificabile.

Un&#39;eccezione notevole a questa regola generale è se il pacchetto di codice immutabile (`ui.apps` o qualsiasi altro), __only__ contiene i bundle OSGi. In tal caso, nessun pacchetto AEM deve dichiarare una dipendenza da esso. Questo perché i pacchetti di codice non possono essere modificati __only__ contenenti bundle OSGi non sono registrati con AEM [Gestione pacchetti,](/help/implementing/developing/tools/package-manager.md) e quindi, qualsiasi pacchetto AEM a seconda di esso avrà una dipendenza non soddisfatta e non riuscirà ad installarsi.

>[!TIP]
>
>Consulta la sezione [Snippet XML POM](#xml-package-dependencies) sezione seguente per un frammento completo.

I pattern comuni per le dipendenze dei pacchetti di contenuto sono:

### Dipendenze dei pacchetti di distribuzione semplici {#simple-deployment-package-dependencies}

Il caso semplice imposta la variabile `ui.content` pacchetto di contenuti modificabili a seconda del `ui.apps` pacchetto di codice immutabile.

+ `all` non ha dipendenze
   + `ui.apps` non ha dipendenze
   + `ui.content` dipende da `ui.apps`

### Dipendenze del pacchetto di distribuzione complesse {#complex-deploxment-package-dependencies}

Le implementazioni complesse si espandono in base al caso semplice e impostano le dipendenze tra il contenuto variabile corrispondente e i pacchetti di codice immutabili. Se necessario, le dipendenze possono essere stabilite anche tra pacchetti di codice immutabili.

+ `all` non ha dipendenze
   + `common.ui.apps.common` non ha dipendenze
   + `site-a.ui.apps` dipende da `common.ui.apps`
   + `site-a.ui.content` dipende da `site-a.ui.apps`
   + `site-b.ui.apps` dipende da `common.ui.apps`
   + `site-b.ui.content` dipende da `site-b.ui.apps`

## Sviluppo locale e distribuzione {#local-development-and-deployment}

Le strutture e l&#39;organizzazione del progetto di cui al presente articolo sono **completamente compatibile** AEM di sviluppo locale.

## Snippet XML POM {#pom-xml-snippets}

I seguenti sono Maven `pom.xml` snippet di configurazione che possono essere aggiunti ai progetti Maven per allinearli ai consigli di cui sopra.

### Tipi di pacchetti {#xml-package-types}

I pacchetti di codice e di contenuto, distribuiti come pacchetti secondari, devono dichiarare un pacchetto di tipo **applicazione** o **contenuto**, a seconda di ciò che contengono.

#### Tipi di pacchetti contenitore {#container-package-types}

Il contenitore `all/pom.xml` progetto **non** dichiarare `<packageType>`.

#### Tipi di pacchetti di codice (immutabile) {#immutable-package-types}

I pacchetti di codice devono impostare le `packageType` a `application`.

In `ui.apps/pom.xml`, `<packageType>application</packageType>` le direttive di configurazione della build `filevault-package-maven-plugin` la dichiarazione del plugin dichiara il suo tipo di pacchetto.

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

#### Tipi di pacchetti contenuto (variabile) {#mutable-package-types}

I pacchetti di contenuto devono impostare `packageType` a `content`.

In `ui.content/pom.xml`, `<packageType>content</packageType>` direttiva sulla configurazione della build `filevault-package-maven-plugin` la dichiarazione del plugin dichiara il suo tipo di pacchetto.

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

### Contrassegno dei pacchetti per l’implementazione di Adobe Cloud Manager {#cloud-manager-target}

In ogni progetto che genera un pacchetto, **fatta eccezione** per il progetto contenitore (`all`), aggiungi `<cloudManagerTarget>none</cloudManagerTarget>` alla configurazione `<properties>`della dichiarazione del plug-in `filevault-package-maven-plugin`, in modo da assicurarti che **non siano** distribuiti da Adobe Cloud Manager. Il contenitore (`all`) deve essere il singolo pacchetto distribuito tramite Cloud Manager, che a sua volta incorpora tutti i pacchetti di codice e contenuto richiesti.

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

### Inizio repository{#snippet-repo-init}

Gli script Repo Init contenenti gli script Repo Init sono definiti nella sezione `RepositoryInitializer` Configurazione di fabbrica OSGi tramite `scripts` proprietà. Tieni presente che, poiché questi script sono definiti nelle configurazioni OSGi, possono essere facilmente delimitati dalla modalità di esecuzione utilizzando il consueto `../config.<runmode>` semantica delle cartelle.

Poiché gli script sono in genere dichiarazioni su più righe, è più semplice definirli nel `.config` rispetto al file basato su JSON `.cfg.json` formato.

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

La `scripts` La proprietà OSGi contiene direttive definite dal [Lingua Repo Init di Apache Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

### Pacchetto struttura archivio {#xml-repository-structure-package}

In `ui.apps/pom.xml` e qualsiasi altro `pom.xml` che dichiara un pacchetto di codice (`<packageType>application</packageType>`), aggiungi la seguente configurazione del pacchetto della struttura dell&#39;archivio al plug-in FileVault Maven. È possibile [crea un pacchetto personalizzato per la struttura dell’archivio per il progetto](repository-structure-package.md).

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

In `all/pom.xml`, aggiungi quanto segue `<embeddeds>` direttiva `filevault-package-maven-plugin` dichiarazione del plugin. Ricorda, **non** utilizza `<subPackages>` , in quanto includerà i pacchetti secondari in `/etc/packages` piuttosto che `/apps/my-app-packages/<application|content|container>/install(.author|.publish)?`.

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

Se multipli `/apps/*-packages` sono utilizzati nei target incorporati, quindi tutti devono essere enumerati qui.

### Repository Maven di terze parti {#xml-3rd-party-maven-repositories}

>[!WARNING]
>
>L’aggiunta di più archivi Maven può estendere i tempi di creazione Maven, in quanto ulteriori archivi Maven saranno controllati per verificare la presenza di dipendenze.

Nel progetto del reattore `pom.xml`, aggiungi eventuali direttive di repository Maven pubbliche di terze parti necessarie. Il pieno `<repository>` la configurazione deve essere disponibile dal provider dell&#39;archivio di terze parti.

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

In `ui.content/pom.xml`, aggiungi quanto segue `<dependencies>` direttiva `filevault-package-maven-plugin` dichiarazione del plugin.

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

In `all/pom.xml` aggiungi le `maven-clean-plugin` plug-in che pulirà la directory di destinazione prima delle build Maven.

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
+ [Plug-in Maven pacchetto di contenuti FileVault](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
