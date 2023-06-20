---
title: Struttura dei progetti AEM
description: Scopri come definire le strutture dei pacchetti da implementare nel Cloud Service Adobe Experience Manager.
exl-id: 38f05723-5dad-417f-81ed-78a09880512a
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '2927'
ht-degree: 12%

---

# Struttura dei progetti AEM

>[!TIP]
>
>Acquisisci familiarità con le [Utilizzo di Archetipo progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it)e [Plug-in FileVault Content Maven](/help/implementing/developing/tools/maven-plugin.md) poiché questo articolo si basa su questi insegnamenti e concetti.

Questo articolo illustra le modifiche necessarie affinché i progetti Adobe Experience Manager Maven siano compatibili con l’AEM as a Cloud Service, garantendo che rispettino la suddivisione di contenuti mutabili e immutabili, che le dipendenze siano stabilite per creare distribuzioni deterministiche non in conflitto e che siano inserite in una struttura distribuibile.

Le implementazioni delle applicazioni AEM devono essere composte da un singolo pacchetto AEM. A sua volta, questo pacchetto deve contenere pacchetti secondari che comprendono tutto ciò che l’applicazione richiede per funzionare, inclusi il codice, la configurazione e qualsiasi contenuto della linea di base di supporto.

L&#39;AEM richiede una separazione di **contenuto** e **codice**, che significa un singolo pacchetto di contenuti **non può** distribuisci in **entrambi** `/apps` e aree scrivibili di runtime (ad esempio, `/content`, `/conf`, `/home`, o tutto ciò che non `/apps`) dell’archivio. Al contrario, l’applicazione deve separare codice e contenuto in pacchetti discreti da distribuire in AEM.

La struttura del pacchetto descritta in questo documento è compatibile **sia** con le distribuzioni di sviluppo locali che con le distribuzioni di AEM Cloud Service.

>[!TIP]
>
>Le configurazioni descritte in questo documento sono fornite da [Progetto AEM Maven Archetipo 24 o successivo](https://github.com/adobe/aem-project-archetype/releases).

## Aree variabili e immutabili dell’archivio {#mutable-vs-immutable}

`/apps` e `/libs`**sono considerate aree immutabili di AEM poiché non possono essere modificate (create, aggiornate, eliminate) dopo l’avvio di AEM (ad es. in fase di runtime).** Eventuali tentativi di modifica di un’area immutabile in fase di runtime avranno esito negativo.

Tutto il resto nell’archivio, `/content`, `/conf`, `/var`, `/etc`, `/oak:index`, `/system`, `/tmp`, ecc. sono tutti **mutabile** , ovvero possono essere modificate in fase di runtime.

>[!WARNING]
>
>Come nelle versioni precedenti dell’AEM, `/libs` non devono essere modificati. Solo il codice prodotto AEM può distribuire a `/libs`.

### Indici Oak {#oak-indexes}

Indici Oak (`/oak:index`) sono gestite in modo specifico dal processo di implementazione as a Cloud Service dell&#39;AEM. Questo perché Cloud Manager deve attendere che venga distribuito e completamente reindicizzato un nuovo indice prima di passare alla nuova immagine del codice.

Per questo motivo, anche se gli indici Oak sono mutabili in fase di esecuzione, devono essere distribuiti come codice in modo che possano essere installati prima di qualsiasi pacchetto mutabile. Pertanto `/oak:index` Le configurazioni fanno parte del pacchetto di codice e non del pacchetto di contenuto [come descritto di seguito](#recommended-package-structure).

>[!TIP]
>
>Per ulteriori dettagli sull’indicizzazione in AEM as a Cloud Service, consulta il documento [Ricerca e indicizzazione dei contenuti](/help/operations/indexing.md).

## Struttura consigliata dei pacchetti {#recommended-package-structure}

![Experience Manager struttura del pacchetto del progetto](assets/content-package-organization.png)

Questo diagramma fornisce una panoramica della struttura di progetto e degli artefatti di distribuzione dei pacchetti consigliati.

La struttura consigliata per la distribuzione delle applicazioni è la seguente:

### Pacchetti codice/Bundle OSGi

+ Il file Jar del bundle OSGi viene generato e incorporato direttamente nel progetto all.

+ Il `ui.apps` contiene tutto il codice da distribuire e distribuisce solo in `/apps`. Elementi comuni della `ui.apps` Il pacchetto include, tra l’altro:
   + [Definizioni dei componenti e HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=it) script
      + `/apps/my-app/components`
   + JavaScript e CSS (tramite [Librerie client](/help/implementing/developing/introduction/clientlibs.md))
      + `/apps/my-app/clientlibs`
   + [Sovrapposizioni](/help/implementing/developing/introduction/overlays.md) di `/libs`
      + `/apps/cq`, `/apps/dam/`, ecc.
   + Configurazioni in base al contesto di fallback
      + `/apps/settings`
   + ACL (autorizzazioni)
      + Qualsiasi `rep:policy` per qualsiasi percorso in `/apps`
   + [Script in bundle precompilati](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/precompiled-bundled-scripts.html)

>[!NOTE]
>
>Lo stesso codice deve essere distribuito in tutti gli ambienti. Questo codice è necessario per garantire un livello di affidabilità delle convalide anche nell’ambiente stage in produzione. Per ulteriori informazioni, consulta la sezione su [Modalità di esecuzione](/help/implementing/deploying/overview.md#runmodes).


### Pacchetti di contenuti

+ Il `ui.content` Il pacchetto contiene tutto il contenuto e la configurazione. Il pacchetto di contenuti contiene tutte le definizioni di nodi non presenti nel `ui.apps` o `ui.config` o, in altre parole, qualsiasi cosa non contenuta in `/apps` o `/oak:index`. Elementi comuni della `ui.content` Il pacchetto include, tra l’altro:
   + Configurazioni in base al contesto
      + `/conf`
   + Strutture di contenuto complesse richieste (ad esempio Creazione di contenuti che si basano su ed estendono oltre le strutture di contenuto della linea di base definite in Repo Init.)
      + `/content`, `/content/dam`, ecc.
   + Tassonomie di assegnazione tag gestite
      + `/content/cq:tags`
   + Nodi etc legacy (idealmente, migrali in posizioni non/etc)
      + `/etc`

### Pacchetti contenitore

+ Il `all` è un pacchetto contenitore che include SOLO artefatti distribuibili, il file JAR del bundle OSGI, `ui.apps`, `ui.config` e `ui.content` pacchetti come incorporamenti. Il `all` il pacchetto non deve avere **qualsiasi contenuto o codice** di propria iniziativa, ma delega l’intera distribuzione all’archivio ai relativi pacchetti secondari o file Jar del bundle OSGi.

  I pacchetti sono ora inclusi utilizzando Maven [Configurazione incorporata del plug-in FileVault Package Maven](#embeddeds), anziché `<subPackages>` configurazione.

  Per implementazioni di Experienci Manager complesse, può essere opportuno creare più `ui.apps`, `ui.config` e `ui.content` progetti/pacchetti che rappresentano siti o tenant specifici in AEM. In tal caso, assicurati che venga rispettata la suddivisione tra contenuto mutabile e immutabile e che i pacchetti di contenuti richiesti e i file Jar del bundle OSGi siano incorporati come pacchetti secondari nel `all` pacchetto di contenuti del contenitore.

  Ad esempio, una struttura complessa del pacchetto di contenuti di distribuzione potrebbe essere simile alla seguente:

   + `all` il pacchetto di contenuto incorpora i seguenti pacchetti, per creare un singolo artefatto di distribuzione
      + `common.ui.apps` distribuisce il codice richiesto da **entrambi** sito A e sito B
      + `site-a.core` JAR del bundle OSGi richiesto dal sito A
      + `site-a.ui.apps` distribuisce il codice richiesto dal sito A
      + `site-a.ui.config` distribuisce le configurazioni OSGi richieste dal sito A
      + `site-a.ui.content` distribuisce il contenuto e la configurazione richiesti dal sito A
      + `site-b.core` JAR bundle OSGi richiesto dal sito B
      + `site-b.ui.apps` distribuisce il codice richiesto dal sito B
      + `site-b.ui.config` distribuisce le configurazioni OSGi richieste dal sito B
      + `site-b.ui.content` distribuisce il contenuto e la configurazione richiesti dal sito B

+ Il `ui.config` il pacchetto contiene tutti [Configurazioni OSGi](/help/implementing/deploying/configuring-osgi.md):
   + Considerato codice e appartiene ai bundle OSGi, ma non contiene nodi di contenuto regolari. In questo modo viene contrassegnato come pacchetto contenitore
   + Cartella organizzativa contenente le definizioni di configurazione OSGi specifiche per la modalità di esecuzione
      + `/apps/my-app/osgiconfig`
   + Cartella di configurazione OSGi comune contenente le configurazioni OSGi predefinite applicabili a tutte le destinazioni di distribuzione as a Cloud Service AEM di destinazione
      + `/apps/my-app/osgiconfig/config`
   + Eseguire cartelle di configurazione OSGi specifiche per la modalità che contengono configurazioni OSGi predefinite applicabili a tutte le destinazioni di distribuzione as a Cloud Service da AEM di destinazione
      + `/apps/my-app/osgiconfig/config.<author|publish>.<dev|stage|prod>`
   + Script di configurazione OSGi Repo iniziale
      + [Repo iniziale](#repo-init) è il metodo consigliato per distribuire il contenuto (mutabile) che fa logicamente parte dell’applicazione AEM. Le configurazioni OSGi Repo Init devono essere posizionate nel punto appropriato `config.<runmode>` come descritto in precedenza e può essere utilizzato per definire:
         + Strutture di contenuto della linea di base
         + Utenti
         + Utenti del servizio
         + Gruppi
         + ACL (autorizzazioni)

### Pacchetti di applicazioni aggiuntivi{#extra-application-packages}

Se altri progetti AEM, a loro volta costituiti da pacchetti di codice e contenuti propri, vengono utilizzati dall’implementazione dell’AEM, i pacchetti contenitore devono essere incorporati nel `all` pacchetto.

Ad esempio, un progetto AEM che include due applicazioni AEM di fornitori diversi potrebbe essere simile al seguente:

+ `all` il pacchetto di contenuto incorpora i seguenti pacchetti, per creare un singolo artefatto di distribuzione
   + `core` JAR del bundle OSGi richiesto dall’applicazione AEM
   + `ui.apps` distribuisce il codice richiesto dall’applicazione AEM
   + `ui.config` implementa le configurazioni OSGi richieste dall’applicazione AEM
   + `ui.content` implementa il contenuto e la configurazione richiesti dall’applicazione AEM
   + `vendor-x.all` distribuisce tutto il necessario (codice e contenuto) per l’applicazione X del fornitore
   + `vendor-y.all` distribuisce tutto il necessario (codice e contenuto) per l’applicazione Y del fornitore

## Tipi di pacchetti {#package-types}

I pacchetti devono essere contrassegnati con il relativo tipo di pacchetto dichiarato. I tipi di pacchetto aiutano a chiarire lo scopo e la distribuzione di un pacchetto.

+ I pacchetti contenitore devono impostare i `packageType` a `container`. I pacchetti contenitore non devono contenere nodi regolari. Sono consentiti solo bundle, configurazioni e pacchetti secondari OSGi. I contenitori in AEM as a Cloud Service non possono essere utilizzati [installare gli hook](https://jackrabbit.apache.org/filevault/installhooks.html).
+ I pacchetti di codice (immutabili) devono impostare i propri `packageType` a `application`.
+ I pacchetti di contenuti (mutabili) devono impostare i propri `packageType` a `content`.


Per ulteriori informazioni, consulta [Apache Jackrabbit FileVault - Documentazione del plug-in Package Maven](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType), [Tipi di pacchetti Apache Jackrabbit](https://jackrabbit.apache.org/filevault/packagetypes.html)e [Frammento configurazione FileVault Maven](#marking-packages-for-deployment-by-adoube-cloud-manager) di seguito.

>[!TIP]
>
>Consulta la [Frammenti XML POM](#xml-package-types) per uno snippet completo.

## Contrassegno dei pacchetti per la distribuzione da parte di Adobe Cloud Manager {#marking-packages-for-deployment-by-adoube-cloud-manager}

Per impostazione predefinita, Adobe Cloud Manager raccoglie tutti i pacchetti prodotti dalla build Maven. Tuttavia, poiché il pacchetto contenitore (`all`) è l’unico artefatto di distribuzione che contiene tutti i pacchetti di codice e contenuto, è necessario assicurarsi che sia distribuito **solo** il pacchetto contenitore (`all`). Per questo motivo, gli altri pacchetti generati dalla build Maven devono essere contrassegnati con la configurazione FileVault Content Package Maven Plug-In di `<properties><cloudManagerTarget>none</cloudManageTarget></properties>`.

>[!TIP]
>
>Consulta la [Frammenti XML POM](#pom-xml-snippets) per uno snippet completo.

## Repo iniziale{#repo-init}

Repo Init fornisce istruzioni, o script, per definire le strutture JCR, che vanno dalle strutture di nodi comuni come le strutture di cartelle a utenti, utenti del servizio, gruppi e definizioni ACL.

I vantaggi principali di Repo Init sono la presenza di autorizzazioni implicite per eseguire tutte le azioni definite dagli script e il richiamo all’inizio del ciclo di vita della distribuzione, che garantisce l’esistenza di tutte le strutture JCR richieste al momento dell’esecuzione del codice temporale.

Mentre gli script Repo Init stessi vivono nel `ui.config` progetto come script, possono e devono essere utilizzati per definire le seguenti strutture mutabili:

+ Strutture di contenuto della linea di base
+ Utenti del servizio
+ Utenti
+ Gruppi
+ ACL

Gli script di inizializzazione dell’archivio sono memorizzati come `scripts` voci di `RepositoryInitializer` Le configurazioni di fabbrica OSGi, e quindi, possono essere impostate come destinazione implicita dalla modalità di esecuzione, consentendo differenze tra gli script Repo Init di AEM Author e AEM Publish Services oppure tra ambienti (Dev, Stage e Prod).

Le configurazioni OSGi di Repo Init vengono scritte in modo ottimale in [`.config` Formato di configurazione OSGi](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-config-1) in quanto supportano più righe, il che rappresenta un’eccezione alle best practice per l’utilizzo di [`.cfg.json` per definire le configurazioni OSGi](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1).

Tieni presente che, quando definisci Utenti e Gruppi, solo i gruppi sono considerati parte dell’applicazione e devono essere qui definiti come parte integrante della sua funzione. Utenti e gruppi dell’organizzazione devono essere ancora definiti in fase di runtime in AEM; ad esempio, se un flusso di lavoro personalizzato assegna il lavoro a un gruppo denominato, tale gruppo deve essere definito tramite Repo Init nell’applicazione AEM, tuttavia se il raggruppamento è puramente organizzativo, come &quot;Team di Wendy&quot; e &quot;Team di Sean&quot;, è meglio definirli e gestirli in fase di runtime in AEM.

>[!TIP]
>
>Script di inizializzazione archivio *deve* essere definito in linea `scripts` e `references` la configurazione non funzionerà.

Il vocabolario completo per gli script Repo Init è disponibile sul sito [Documentazione di avvio dell’archivio Sling Apache](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

>[!TIP]
>
>Consulta la [Snippet di inizializzazione archivio](#snippet-repo-init) per uno snippet completo.

## Pacchetto struttura archivio {#repository-structure-package}

I pacchetti di codice richiedono la configurazione del plug-in FileVault Maven per fare riferimento a un `<repositoryStructurePackage>` che impone la correttezza delle dipendenze strutturali (per garantire che un pacchetto di codice non venga installato su un altro). È possibile [creare un pacchetto con la struttura dell’archivio personalizzato per il progetto](repository-structure-package.md).

Questa operazione è **richiesta solo** per i pacchetti codice, ovvero per tutti i pacchetti contrassegnati con `<packageType>application</packageType>`.

Per informazioni su come creare un pacchetto di struttura dell’archivio per l’applicazione, consulta [Sviluppare un pacchetto con la struttura dell’archivio](repository-structure-package.md).

Tieni presente che i pacchetti di contenuti (`<packageType>content</packageType>`) **non** richiede questo pacchetto con struttura dell’archivio.

>[!TIP]
>
>Consulta la [Frammenti XML POM](#xml-repository-structure-package) per uno snippet completo.

## Incorporazione di pacchetti secondari nel pacchetto contenitore{#embeddeds}

I pacchetti di contenuto o codice vengono inseriti in una speciale cartella &quot;side-car&quot; e possono essere destinati all’installazione su AEM Author, AEM Publish o entrambi, utilizzando il plug-in FileVault Maven `<embeddeds>` configurazione. Tieni presente che `<subPackages>` non deve essere utilizzata.

I casi d’uso comuni includono:

+ ACL/autorizzazioni che differiscono tra gli utenti autori AEM e gli utenti pubblicazione AEM
+ Configurazioni utilizzate per supportare attività solo sull’autore AEM
+ Codice come le integrazioni con sistemi di back-office, necessario solo per l’esecuzione sull’autore AEM

![Incorporazione di pacchetti](assets/embeddeds.png)

Per eseguire il targeting dell’autore dell’AEM, della pubblicazione dell’AEM o di entrambi, il pacchetto è incorporato nel `all` pacchetto contenitore in una posizione cartella speciale, nel formato seguente:

`/apps/<app-name>-packages/(content|application|container)/install(.author|.publish)?`

Suddivisione di questa struttura di cartelle:

+ Cartella di primo livello **deve essere** `/apps`.
+ La cartella di secondo livello rappresenta l&#39;applicazione con `-packages` dopo il nome della cartella. Spesso esiste una sola cartella di secondo livello in cui sono incorporati tutti i pacchetti secondari. Tuttavia, è possibile creare un numero qualsiasi di cartelle di secondo livello per rappresentare al meglio la struttura logica dell’applicazione:
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`

  >[!WARNING]
  >
  >Per convenzione, le cartelle incorporate in un pacchetto secondario sono denominate con il suffisso `-packages`. In questo modo, il codice di distribuzione e i pacchetti di contenuto **non** vengono distribuiti nelle cartelle di destinazione di qualsiasi pacchetto secondario `/apps/<app-name>/...`, il che provoca un comportamento di installazione distruttivo e ciclico.

+ La cartella di terzo livello deve essere
  `application`, `content` oppure `container`
   + Il `application` la cartella contiene pacchetti di codice
   + Il `content` la cartella contiene i pacchetti di contenuti
   + Il `container` cartella contiene qualsiasi [pacchetti applicativi aggiuntivi](#extra-application-packages) che potrebbero essere incluse nella domanda AEM.
Questo nome di cartella corrisponde al [tipi di pacchetti](#package-types) delle confezioni in esso contenute.
+ La cartella di quarto livello contiene i pacchetti secondari e deve corrispondere a una delle seguenti:
   + `install` per effettuare l’installazione **sia su** AEM Author che AEM Publish
   + `install.author` per eseguire l’installazione **solo** su AEM Author
   + `install.publish` a **solo** installare su pubblicazione AEM Nota che solo `install.author` e `install.publish` sono destinazioni supportate. Altre modalità di esecuzione **non sono** supportate.

Ad esempio, una distribuzione che contiene pacchetti specifici per l’authoring e la pubblicazione di AEM può avere un aspetto simile al seguente:

+ `all` Il pacchetto contenitore incorpora i seguenti pacchetti, per creare un singolo artefatto di distribuzione
   + `ui.apps` incorporato in `/apps/my-app-packages/application/install` distribuisce il codice sia all’istanza di authoring AEM che a quella di pubblicazione AEM
   + `ui.apps.author` incorporato in `/apps/my-app-packages/application/install.author` distribuisce il codice solo all’autore AEM
   + `ui.content` incorporato in `/apps/my-app-packages/content/install` distribuisce contenuti e configurazione sia all’autore AEM che alla pubblicazione AEM
   + `ui.content.publish` incorporato in `/apps/my-app-packages/content/install.publish` distribuisce contenuti e configurazione solo per la pubblicazione AEM

>[!TIP]
>
>Consulta la [Frammenti XML POM](#xml-embeddeds) per uno snippet completo.

### Definizione filtro del pacchetto contenitore {#container-package-filter-definition}

A causa dell’incorporamento del codice e dei pacchetti secondari di contenuto nel pacchetto contenitore, i percorsi di destinazione incorporati devono essere aggiunti al progetto contenitore `filter.xml` per garantire che i pacchetti incorporati siano inclusi nel pacchetto contenitore quando generato.

Aggiungi semplicemente il `<filter root="/apps/<my-app>-packages"/>` voci per le cartelle di secondo livello che contengono pacchetti secondari da distribuire.

>[!TIP]
>
>Consulta la [Frammenti XML POM](#xml-container-package-filters) per uno snippet completo.

## Incorporazione di pacchetti di terze parti {#embedding-3rd-party-packages}

Tutti i pacchetti devono essere disponibili tramite [Archivio di artefatti Maven pubblico di Adobe](https://repo1.maven.org/maven2/com/adobe/) o un archivio di artefatti Maven pubblico e di terze parti accessibile.

Se i pacchetti di terze parti si trovano nell’**archivio di artefatti Maven pubblico di Adobe**, per consentire ad Adobe Cloud Manager di risolvere gli artefatti non è necessario effettuare nessuna ulteriore configurazione.

Se i pacchetti di terze parti si trovano in un **archivio di artefatti Maven pubblico di terze parti**, tale archivio deve essere registrato nel `pom.xml` del progetto, per poi essere incorporato seguendo il metodo [descritto sopra](#embeddeds).

I connettori/applicazioni di terze parti devono essere incorporati utilizzando `all` come contenitore nel contenitore del progetto (`all`).

L’aggiunta di dipendenze Maven segue le pratiche Maven standard e l’incorporamento di artefatti di terze parti (pacchetti di codice e contenuti) sono [descritto sopra](#embedding-3rd-party-packages).

>[!TIP]
>
>Consulta la [Frammenti XML POM](#xml-3rd-party-maven-repositories) per uno snippet completo.

## Dipendenze dei pacchetti tra `ui.apps` da `ui.content` Pacchetti {#package-dependencies}

Per garantire la corretta installazione dei pacchetti, si consiglia di stabilire le dipendenze tra i pacchetti.

La regola generale è costituita dai pacchetti contenenti contenuto mutabile (`ui.content`) deve dipendere dal codice immutabile (`ui.apps`) che supporta il rendering e l’utilizzo del contenuto mutabile.

Un&#39;eccezione rilevante a questa regola generale è se il pacchetto di codice immutabile (`ui.apps` o altro), __solo__ contiene i bundle OSGi. In tal caso, nessun pacchetto AEM dovrebbe dichiarare una dipendenza da esso. Questo perché i pacchetti di codice non modificabili __solo__ I bundle OSGi che li contengono non sono registrati con AEM [Gestione pacchetti,](/help/implementing/developing/tools/package-manager.md) di conseguenza, qualsiasi pacchetto AEM che dipenda da esso avrà una dipendenza insoddisfatta e non potrà essere installato.

>[!TIP]
>
>Consulta la [Frammenti XML POM](#xml-package-dependencies) per uno snippet completo.

I pattern comuni per le dipendenze dei pacchetti di contenuti sono:

### Dipendenze dei pacchetti di distribuzione semplici {#simple-deployment-package-dependencies}

Il caso semplice imposta il `ui.content` pacchetto di contenuti modificabili a seconda del `ui.apps` pacchetto di codice immutabile.

+ `all` non ha dipendenze
   + `ui.apps` non ha dipendenze
   + `ui.content` dipende da `ui.apps`

### Dipendenze dei pacchetti di distribuzione complesse {#complex-deploxment-package-dependencies}

Le distribuzioni complesse si espandono in base al caso semplice e impostano le dipendenze tra il contenuto mutabile corrispondente e i pacchetti di codice immutabile. Se necessario, è possibile stabilire le dipendenze anche tra pacchetti di codice immutabili.

+ `all` non ha dipendenze
   + `common.ui.apps.common` non ha dipendenze
   + `site-a.ui.apps` dipende da `common.ui.apps`
   + `site-a.ui.content` dipende da `site-a.ui.apps`
   + `site-b.ui.apps` dipende da `common.ui.apps`
   + `site-b.ui.content` dipende da `site-b.ui.apps`

## Sviluppo e distribuzione locali {#local-development-and-deployment}

Le strutture e l&#39;organizzazione del progetto descritte in questo articolo sono **completamente compatibile** sviluppo locale istanze AEM.

## Frammenti XML POM {#pom-xml-snippets}

Di seguito sono riportati i file Maven `pom.xml` snippet di configurazione che possono essere aggiunti ai progetti Maven per allinearli ai consigli di cui sopra.

### Tipi di pacchetti {#xml-package-types}

I pacchetti di codice e di contenuto, distribuiti come pacchetti secondari, devono dichiarare un pacchetto di tipo **applicazione** o **contenuto**, a seconda di ciò che contengono.

#### Tipi di pacchetti contenitore {#container-package-types}

Il contenitore `all/pom.xml` progetto **non** dichiarare un `<packageType>`.

#### Tipi di pacchetti codice (immutabili) {#immutable-package-types}

I pacchetti di codice devono impostare i relativi `packageType` a `application`.

In `ui.apps/pom.xml`, il `<packageType>application</packageType>` direttive di configurazione della build di `filevault-package-maven-plugin` dichiarazione del plug-in che dichiara il tipo di pacchetto.

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

#### Tipi di pacchetti di contenuti (mutabili) {#mutable-package-types}

I pacchetti di contenuti devono impostare le rispettive `packageType` a `content`.

In `ui.content/pom.xml`, il `<packageType>content</packageType>` direttiva di configurazione della build del `filevault-package-maven-plugin` dichiarazione del plug-in che dichiara il tipo di pacchetto.

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

In ogni progetto che genera un pacchetto, **fatta eccezione** per il progetto contenitore (`all`), aggiungi `<cloudManagerTarget>none</cloudManagerTarget>` alla configurazione `<properties>`della dichiarazione del plug-in `filevault-package-maven-plugin`, in modo da assicurarti che **non siano** distribuiti da Adobe Cloud Manager. Il contenitore (`all`) deve essere il singolo pacchetto distribuito tramite Cloud Manager, che a sua volta incorpora tutti i pacchetti richiesti di codice e contenuto.

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

### Repo iniziale{#snippet-repo-init}

Gli script Repo Init che contengono gli script Repo Init sono definiti in `RepositoryInitializer` Configurazione di fabbrica OSGi tramite `scripts` proprietà. Poiché questi script sono definiti nelle configurazioni OSGi, possono essere facilmente delimitati dalla modalità di esecuzione utilizzando la `../config.<runmode>` semantica delle cartelle.

Poiché gli script sono in genere dichiarazioni su più righe, è più semplice definirli nella `.config` basato su JSON `.cfg.json` formato.

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

Il `scripts` La proprietà OSGi contiene le direttive definite dalla [Lingua iniziale dell’archivio Apache Sling](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

### Pacchetto struttura archivio {#xml-repository-structure-package}

In `ui.apps/pom.xml` e qualsiasi altro `pom.xml` che dichiara un pacchetto di codice (`<packageType>application</packageType>`), aggiungi la seguente configurazione del pacchetto della struttura dell’archivio al plug-in FileVault Maven. È possibile [creare un pacchetto con la struttura dell’archivio personalizzato per il progetto](repository-structure-package.md).

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

In `all/pom.xml`, aggiungi quanto segue `<embeddeds>` direttive al `filevault-package-maven-plugin` dichiarazione plugin. Ricorda: **non** utilizzare il `<subPackages>` , in quanto include i pacchetti secondari in `/etc/packages` anziché `/apps/my-app-packages/<application|content|container>/install(.author|.publish)?`.

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

### Definizione filtro del pacchetto contenitore {#xml-container-package-filters}

Nel `filter.xml` `all` del progetto (`all/src/main/content/jcr_root/META-INF/vault/definition/filter.xml`), **includi** tutte le cartelle `-packages` che contengono pacchetti secondari da distribuire:

```xml
<filter root="/apps/my-app-packages"/>
```

Se più `/apps/*-packages` sono utilizzati nelle destinazioni incorporate, quindi devono essere elencati tutti qui.

### Archivi Maven di terze parti {#xml-3rd-party-maven-repositories}

>[!WARNING]
>
>L’aggiunta di più archivi Maven può estendere i tempi di build Maven man mano che vengono verificati ulteriori archivi Maven per le dipendenze.

Nel progetto del reattore `pom.xml`, aggiungi eventuali direttive dell’archivio Maven pubblico di terze parti necessarie. Il valore completo `<repository>` La configurazione di deve essere disponibile dal provider dell’archivio di terze parti.

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

### Dipendenze dei pacchetti tra `ui.apps` da `ui.content` Pacchetti {#xml-package-dependencies}

In `ui.content/pom.xml`, aggiungi quanto segue `<dependencies>` direttive al `filevault-package-maven-plugin` dichiarazione plugin.

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

In `all/pom.xml` aggiungi `maven-clean-plugin` plug-in per la pulizia della directory di destinazione prima della generazione di una build Maven.

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

+ [Gestione dei pacchetti tramite Maven](/help/implementing/developing/tools/maven-plugin.md)
+ [Plug-in Maven pacchetto contenuti FileVault](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
