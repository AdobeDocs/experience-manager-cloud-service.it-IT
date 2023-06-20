---
title: Ricerca e indicizzazione dei contenuti
description: Ricerca e indicizzazione dei contenuti
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '2481'
ht-degree: 74%

---

# Ricerca e indicizzazione dei contenuti {#indexing}

## Modifiche in AEM as a Cloud Service {#changes-in-aem-as-a-cloud-service}

Con AEM as a Cloud Service, Adobe si sta spostando da un modello AEM incentrato sull’istanza a una visualizzazione basata sul servizio con contenitori AEM n-x, guidata dalle pipeline CI/CD in Cloud Manager. Invece di configurare e mantenere gli indici su singole istanze di AEM, è necessario specificare la configurazione dell’indice prima di una distribuzione. I cambiamenti di configurazione nella produzione chiaramente infrangono i criteri CI/CD. Lo stesso vale per le modifiche dell’indice in quanto può influire sulla stabilità e sulle prestazioni del sistema se non specificamente testato e reindicizzato prima dell’introduzione nella produzione.

Di seguito è riportato un elenco delle modifiche principali rispetto ad AEM 6.5 e versioni precedenti:

1. Gli utenti non avranno più accesso al gestore degli indici di una singola istanza AEM per eseguire il debug, configurare o mantenere l’indicizzazione. Viene utilizzato solo per lo sviluppo locale e le distribuzioni on-premise.
1. Gli utenti non cambieranno gli indici su una singola istanza AEM né dovranno più preoccuparsi dei controlli di coerenza o della reindicizzazione.
1. In generale, le modifiche dell’indice vengono avviate prima di passare alla produzione per non aggirare i gateway di qualità nelle pipeline CI/CD di Cloud Manager e non influire sui KPI aziendali in produzione.
1. Tutte le metriche correlate, comprese le prestazioni di ricerca in produzione, sono disponibili per i clienti in fase di runtime per fornire una visione olistica degli argomenti di ricerca e indicizzazione.
1. I clienti possono impostare gli avvisi in base alle proprie esigenze.
1. Gli SRE monitorano lo stato di integrità del sistema 24/7 e intraprendono le azioni necessarie il più presto possibile.
1. La configurazione dell’indice viene modificata tramite le distribuzioni. Le modifiche alla definizione dell’indice sono configurate come altre modifiche al contenuto.
1. Ad alto livello sull&#39;AEM as a Cloud Service, con l&#39;introduzione della [modello di distribuzione continua](#index-management-using-rolling-deployments) esistono due set di indici: uno per la versione precedente e uno per la nuova versione.
1. I clienti possono vedere se il processo di indicizzazione è completo nella pagina di compilazione di Cloud Manager e ricevono una notifica quando la nuova versione è pronta per il traffico.

Limiti:

* Attualmente, la gestione degli indici su AEM as a Cloud Service è supportata solo per gli indici di tipo `lucene`.
* Sono supportati solo gli analizzatori standard (ovvero quelli forniti con il prodotto). Gli analizzatori personalizzati non sono supportati.
* Internamente, possono essere configurati e utilizzati per le query altri indici. Ad esempio, le query scritte rispetto all’indice `damAssetLucene` potrebbero, su Skyline, essere eseguite in base a una versione Elasticsearch di questo indice. Questa differenza generalmente non è visibile all’applicazione e all’utente, tuttavia alcuni strumenti come la funzionalità `explain` riferiranno un indice diverso. Per le differenze tra gli indici Lucene e gli indici Elastic, vedi [la documentazione Elastic in Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/query/elastic.html). I clienti non devono e non possono configurare direttamente gli indici di Elasticsearch.

## Guida all’uso {#how-to-use}

La definizione degli indici può comprendere i tre casi d’uso seguenti:

1. Aggiunta di una nuova definizione dell’indice del cliente.
1. Aggiornamento di una definizione di indice esistente. Ciò corrisponde effettivamente all’aggiunta di una nuova versione di una definizione di indice esistente.
1. Rimozione di un indice esistente ridondante o obsoleto.

Per entrambi i punti 1 e 2 di cui sopra, devi creare una nuova definizione dell’indice come parte della base di codice personalizzato nella rispettiva pianificazione della versione di Cloud Manager. Per ulteriori informazioni, consulta la [documentazione sulla distribuzione di AEM as a Cloud Service](/help/implementing/deploying/overview.md).

## Nomi indice {#index-names}

Una definizione di indice può essere:

1. Un indice preconfigurato. Un esempio è `/oak:index/cqPageLucene-2`.
1. Una personalizzazione di un indice preconfigurato. Tali personalizzazioni sono definite dal cliente. Un esempio è `/oak:index/cqPageLucene-2-custom-1`.
1. Un indice completamente personalizzato. Un esempio è `/oak:index/acme.product-1-custom-2`. Per evitare conflitti di denominazione, è necessario che gli indici completamente personalizzati abbiano un prefisso, ad esempio, `acme.`

Tieni presente che sia la personalizzazione di un indice predefinito sia gli indici completamente personalizzati devono contenere `-custom-`. Solo gli indici completamente personalizzati devono iniziare con un prefisso.

## Preparazione della nuova definizione dell’indice {#preparing-the-new-index-definition}

>[!NOTE]
>
>Per personalizzare un indice preconfigurato, ad esempio `damAssetLucene-6`, copia l’ultima definizione di indice preconfigurato da un *ambiente Cloud Service* utilizzando Gestione pacchetti CRX DE (`/crx/packmgr/`). Quindi rinomina la configurazione, ad esempio `damAssetLucene-6-custom-1`, e aggiungi le tue personalizzazioni in alto. In questo modo le configurazioni richieste non vengono rimosse inavvertitamente. Ad esempio, il nodo `tika` sotto `/oak:index/damAssetLucene-6/tika` è richiesto nell’indice personalizzato del servizio cloud. Non esiste nell’SDK di Cloud.

È necessario preparare un nuovo pacchetto di definizione dell’indice che contiene la definizione effettiva, seguendo questo pattern di denominazione:

`<indexName>[-<productVersion>]-custom-<customVersion>`

che poi deve andare sotto `ui.apps/src/main/content/jcr_root`. Tutte le definizioni di indice personalizzate e rielaborate devono essere memorizzate in `/oak:index`.

Il filtro per il pacchetto deve essere impostato in modo da mantenere gli indici esistenti (preconfigurati). Nel file `ui.apps/src/main/content/META-INF/vault/filter.xml`, ogni indice personalizzato deve essere elencato, ad esempio come `<filter root="/oak:index/damAssetLucene-6-custom-1"/>`. Se la versione dell’indice viene successivamente modificata, è necessario regolare il filtro.

<!-- Alexandru: temporarily drafting this statement due to CQDOC-17701

The package from the above sample is built as `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`. -->

>[!NOTE]
>
>Qualsiasi pacchetto di contenuto con le definizioni degli indici deve avere la seguente proprietà impostata nel file delle proprietà, situato in `/META-INF/vault/properties.xml`:
>
>`noIntermediateSaves=true`

## Distribuzione delle definizioni degli indici {#deploying-index-definitions}

Le definizioni degli indici sono ora contrassegnate con “custom” e con il numero della versione:

* La definizione stessa dell’indice (ad esempio `/oak:index/ntBaseLucene-custom-1`)

Per distribuire un indice personalizzato, la definizione dell’indice (`/oak:index/definitionname`) deve essere consegnata tramite `ui.apps` da Git e il processo di implementazione di Cloud Manager. Nel filtro FileVault, ad esempio, `ui.apps/src/main/content/META-INF/vault/filter.xml`, elenca singolarmente ogni indice personalizzato, ad esempio `<filter root="/oak:index/damAssetLucene-7-custom-1"/>`. La definizione di indice personalizzato verrà quindi memorizzata nel file `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-7-custom-1/.content.xml`, come segue:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:oak="https://jackrabbit.apache.org/oak/ns/1.0" xmlns:dam="http://www.day.com/dam/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0" xmlns:rep="internal"
        jcr:primaryType="oak:QueryIndexDefinition"
        async="[async,nrt]"
        compatVersion="{Long}2"
        ...
        </indexRules>
        <tika jcr:primaryType="nt:unstructured">
            <config.xml jcr:primaryType="nt:file"/>
        </tika>
</jcr:root>
```

L’esempio precedente contiene una configurazione per Apache Tika. Il file di configurazione Tika verrebbe memorizzato in `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-7-custom-1/tika/config.xml`.

### Configurazione del progetto

A seconda della versione del plug-in del pacchetto Maven Jackrabbit Filevault, è necessaria un’ulteriore configurazione del progetto. Quando si utilizza il plug-in del pacchetto Maven Jackrabbit Filevault versione **1.1.6.** o successiva, il file `pom.xml` deve contenere la seguente sezione nella configurazione del plug-in per `filevault-package-maven-plugin`, in `configuration/validatorsSettings` (appena prima di `jackrabbit-nodetypes`):

```xml
<jackrabbit-packagetype>
    <options>
        <immutableRootNodeNames>apps,libs,oak:index</immutableRootNodeNames>
    </options>
</jackrabbit-packagetype>
```

Inoltre, in questo caso la versione di `vault-validation` deve essere aggiornata a una versione più recente:

```xml
<dependency>
    <groupId>org.apache.jackrabbit.vault</groupId>
    <artifactId>vault-validation</artifactId>
    <version>3.5.6</version>
</dependency>
```

Quindi, in `ui.apps.structure/pom.xml` e `ui.apps/pom.xml`, nella configurazione di `filevault-package-maven-plugin` devono essere abilitati sia `allowIndexDefinitions` che `noIntermediateSaves`. L’opzione `noIntermediateSaves` assicura che le configurazioni dell’indice vengano aggiunte atomicamente.

```xml
<groupId>org.apache.jackrabbit</groupId>
    <artifactId>filevault-package-maven-plugin</artifactId>
    <configuration>
        <allowIndexDefinitions>true</allowIndexDefinitions>
        <properties>
            <cloudManagerTarget>none</cloudManagerTarget>
            <noIntermediateSaves>true</noIntermediateSaves>
        </properties>
    ...
```

In `ui.apps.structure/pom.xml`, la sezione `filters` per questo plug-in deve contenere una radice di filtro come segue:

```xml
<filter><root>/oak:index</root></filter>
```

Una volta aggiunta la nuova definizione dell’indice, la nuova applicazione deve essere distribuita tramite Cloud Manager. Al momento della distribuzione, vengono avviati due processi responsabili dell’aggiunta (e dell’unione, se necessario) delle definizioni dell’indice a MongoDB e Azure Segment Store rispettivamente per l’authoring e la pubblicazione. Gli archivi sottostanti vengono reindicizzati con le nuove definizioni dell’indice, prima che lo switch venga implementato.

### NOTA

Nel caso in cui si osservi il seguente errore nella convalida di filevault <br>
`[ERROR] ValidationViolation: "jackrabbit-nodetypes: Mandatory child node missing: jcr:content [nt:base] inside node with types [nt:file]"` <br>
A questo punto, puoi seguire uno dei seguenti passaggi per risolvere il problema: <br>
1. Effettua il downgrade di filevault alla versione 1.0.4 e aggiungi quanto segue al pom di livello principale:

```xml
<allowIndexDefinitions>true</allowIndexDefinitions>
```

Di seguito è riportato un esempio di dove posizionare la configurazione precedente nel pom.

```xml
<plugin>
    <groupId>org.apache.jackrabbit</groupId>
    <artifactId>filevault-package-maven-plugin</artifactId>
    <configuration>
        <properties>
        ...
        </properties>
        ...
        <allowIndexDefinitions>true</allowIndexDefinitions>
        <repositoryStructurePackages>
        ...
        </repositoryStructurePackages>
        <dependencies>
        ...
        </dependencies>
    </configuration>
</plugin>
```

1. Disattiva convalida tipo di nodo. Imposta la seguente proprietà nella sezione jackrabbit-nodetypes della configurazione del plug-in filevault:

```xml
<isDisabled>true</isDisabled>
```

Di seguito è riportato un esempio di dove posizionare la configurazione precedente nel pom.

```xml
<plugin>
    <groupId>org.apache.jackrabbit</groupId>
    <artifactId>filevault-package-maven-plugin</artifactId>
    ...
    <configuration>
    ...
        <validatorsSettings>
        ...
            <jackrabbit-nodetypes>
                <isDisabled>true</isDisabled>
            </jackrabbit-nodetypes>
        </validatorsSettings>
    </configuration>
</plugin>
```

>[!TIP]
>
>Per ulteriori dettagli sulla struttura del pacchetto richiesta per AEM as a Cloud Service, vedi il documento [struttura del progetto AEM.](/help/implementing/developing/introduction/aem-project-content-package-structure.md)

## Gestione dell’indice tramite distribuzioni continue {#index-management-using-rolling-deployments}

### Gestione dell’indice {#what-is-index-management}

La gestione degli indici riguarda l’aggiunta, la rimozione e la modifica degli indici. La modifica della *definizione* di un indice è veloce, ma la sua applicazione (spesso chiamata “creazione di un indice”, o, per gli indici esistenti, “reindicizzazione”) richiede tempo. Non è istantaneo: l’archivio deve essere analizzato per individuare i dati da indicizzare.

### Cosa sono le distribuzioni continue {#what-are-rolling-deployments}

Una distribuzione continua può ridurre i tempi di inattività. Consente inoltre di eseguire senza tempi di inattività gli aggiornamenti e offre rapidi rollback. La vecchia versione dell&#39;applicazione viene eseguita contemporaneamente alla nuova versione dell&#39;applicazione.

### Aree di sola lettura e di lettura/scrittura {#read-only-and-read-write-areas}

Alcune aree dell’archivio (parti di sola lettura dell’archivio) possono essere diverse nella vecchia e nella nuova versione dell’applicazione. Le aree di sola lettura dell’archivio sono in genere `/app` e `/libs`. Nell’esempio seguente, il corsivo viene utilizzato per contrassegnare le aree di sola lettura, mentre il grassetto viene utilizzato per le aree di lettura/scrittura.

* **/**
* */apps (sola lettura)*
* **/content**
* */libs (sola lettura)*
* **/oak:index**
* **/oak:index/acme.**
* **/jcr:system**
* **/system**
* **/var**

Le aree di lettura-scrittura dell’archivio sono condivise tra tutte le versioni dell’applicazione, mentre per ogni versione dell’applicazione, esiste un set specifico di `/apps` e `/libs`.

### Gestione degli indici senza distribuzioni continue {#index-management-without-rolling-deployments}

Durante lo sviluppo o quando si utilizzano installazioni locali, gli indici possono essere aggiunti, rimossi o modificati in fase di runtime. Gli indici vengono utilizzati non appena sono disponibili. Se un indice non deve ancora essere utilizzato nella vecchia versione dell’applicazione, viene generalmente generato durante un downtime pianificato. Lo stesso si verifica quando si rimuove un indice o si modifica un indice esistente. Quando si rimuove un indice, questo diventa non disponibile non appena viene rimosso.

### Gestione degli indici con distribuzioni continue {#index-management-with-rolling-deployments}

Con le distribuzioni continue, non si verificano tempi di inattività. Per un certo periodo di tempo durante un aggiornamento, sia la vecchia versione (ad esempio, la versione 1) dell’applicazione che la nuova versione (versione 2) vengono eseguite contemporaneamente sullo stesso archivio. Se la versione 1 richiede la disponibilità di un determinato indice, questo non deve essere rimosso nella versione 2. L’indice deve essere rimosso in un secondo momento, ad esempio nella versione 3, che garantisce che la versione 1 dell’applicazione non è più in esecuzione. Inoltre, le applicazioni devono essere scritte in modo che la versione 1 funzioni bene, anche se la versione 2 è in esecuzione, e se sono disponibili indici della versione 2.

Al termine dell’aggiornamento alla nuova versione, i vecchi indici possono essere raccolti come rifiuti dal sistema. I vecchi indici potrebbero rimanere ancora per un po’ di tempo, per velocizzare i rollback (se dovesse essere necessario un rollback).

La tabella seguente mostra cinque definizioni di indice: l’indice `cqPageLucene` viene utilizzato in entrambe le versioni mentre l’indice `damAssetLucene-custom-1` viene utilizzato solo nella versione 2.

>[!NOTE]
>
>`<indexName>-custom-<customerVersionNumber>` è necessario perché AEM as a Cloud Service possa contrassegnarlo come sostitutivo di un indice esistente.

| Indice | Indice predefinito | Uso nella versione 1 | Uso nella versione 2 |
|---|---|---|---|
| /oak:index/damAssetLucene | Sì | Sì | No |
| /oak:index/damAssetLucene-custom-1 | Sì (personalizzato) | No | Sì |
| /oak:index/acme.product-custom-1 | No | Sì | No |
| /oak:index/acme.product-custom-2 | No | No | Sì |
| /oak:index/cqPageLucene | Sì | Sì | Sì |

Il numero di versione è incrementato ogni volta che l’indice viene modificato. Per evitare che i nomi di indice personalizzati si scontrino con i nomi di indice del prodotto stesso, gli indici personalizzati e le modifiche agli indici predefiniti devono terminare con `-custom-<number>`.

### Modifiche agli indici predefiniti {#changes-to-out-of-the-box-indexes}

Quando Adobe cambia un indice predefinito come “damAssetLucene” o “cqPageLucene”, viene creato un nuovo indice denominato `damAssetLucene-2` o `cqPageLucene-2` oppure, se l’indice è già stato personalizzato, la sua definizione viene unita alle modifiche nell’indice predefinito, come mostrato di seguito. L’unione delle modifiche avviene automaticamente. Ciò significa che non è necessario eseguire alcuna operazione se un indice predefinito cambia. Tuttavia, è possibile personalizzare di nuovo l’indice in un secondo momento.

| Indice | Indice predefinito | Uso nella versione 2 | Uso nella versione 3 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | Sì (personalizzato) | Sì | No |
| /oak:index/damAssetLucene-2-custom-1 | Sì (unione automatica di damAssetLucene-custom-1 e damAssetLucene-2) | No | Sì |
| /oak:index/cqPageLucene | Sì | Sì | No |
| /oak:index/cqPageLucene-2 | Sì | No | Sì |

### Limitazioni attuali {#current-limitations}

La gestione degli indici è attualmente supportata solo per gli indici di tipo `lucene`, con `compatVersion` imposta su `2`. Internamente, possono essere configurati e utilizzati per le query altri indici, ad esempio gli indici Elasticsearch. Query scritte rispetto al `damAssetLucene` su AEM as a Cloud Service, l&#39;indice potrebbe infatti essere eseguito su una versione Elasticsearch di questo indice. Questa differenza è invisibile all&#39;utente finale dell&#39;applicazione, tuttavia alcuni strumenti come `explain` La funzionalità riporterà un indice diverso. Per le differenze tra gli indici Lucene e Elasticsearch, consulta [la documentazione relativa agli Elasticsearch in Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/query/elastic.html). I clienti non possono e non devono configurare direttamente gli indici Elasticsearch.

Sono supportati solo gli analizzatori incorporati (ovvero quelli forniti con il prodotto). Gli analizzatori personalizzati non sono supportati.

Per ottenere le migliori prestazioni operative, gli indici non dovrebbero essere eccessivamente grandi. La dimensione totale di tutti gli indici può essere utilizzata come guida: se aumenta di oltre il 100% dopo l’aggiunta degli indici personalizzati e la regolazione degli indici standard in un ambiente di sviluppo, è necessario regolare le definizioni degli indici personalizzati. AEM as a Cloud Service può impedire la distribuzione di indici che influirebbero negativamente sulla stabilità e sulle prestazioni del sistema.

### Aggiunta di un indice {#adding-an-index}

Per aggiungere un indice completamente personalizzato denominato `/oak:index/acme.product-custom-1` da utilizzare in una nuova versione dell’applicazione e successivamente, deve essere configurato come segue:

`acme.product-1-custom-1`

Questo funziona ponendo un identificatore personalizzato davanti al nome dell’indice, seguito da un punto (**`.`**). La lunghezza dell’identificatore deve essere compresa tra 2 e 5 caratteri.

Come sopra, questo assicura che l’indice sia utilizzato solo dalla nuova versione dell’applicazione.

### Modifica di un indice {#changing-an-index}

Quando viene modificato un indice esistente, è necessario aggiungere un nuovo indice con la modifica della definizione. Ad esempio, supponi che l’indice esistente `/oak:index/acme.product-custom-1` venga modificato. Il vecchio indice è memorizzato in `/oak:index/acme.product-custom-1` e il nuovo indice è memorizzato in `/oak:index/acme.product-custom-2`.

La vecchia versione dell’applicazione utilizza la seguente configurazione:

`/oak:index/acme.product-custom-1`

La nuova versione dell’applicazione utilizza la seguente configurazione (modificata):

`/oak:index/acme.product-custom-2`

>[!NOTE]
>
>Le definizioni degli indici su AEM as a Cloud Service potrebbero non corrispondere completamente a quelle su un’istanza di sviluppo locale. L’istanza di sviluppo non dispone di una configurazione Tika, mentre istanze di AEM as a Cloud Service ne hanno una. Se si personalizza un indice con una configurazione Tika, si prega di mantenere tale configurazione.

### Annullamento di una modifica {#undoing-a-change}

A volte, è necessario ripristinare una modifica nella definizione di un indice. Questo può avvenire perché un cambiamento è stato fatto per errore o non è più necessario. Ad esempio, la definizione dell’indice `damAssetLucene-8-custom-3` è stata creata per errore ed è già distribuita. Per questo motivo, potrebbe essere utile ripristinare la precedente definizione dell’indice `damAssetLucene-8-custom-2`. A questo scopo, devi aggiungere un nuovo indice denominato `damAssetLucene-8-custom-4` che contiene la definizione dell’indice precedente, `damAssetLucene-8-custom-2`.

### Rimozione di un indice {#removing-an-index}

Ciò che segue si applica solo agli indici personalizzati. Gli indici di prodotto non possono essere rimossi poiché sono utilizzati da AEM.

Se un indice deve essere rimosso in una versione successiva dell’applicazione, puoi definire un indice vuoto (un indice vuoto che non viene mai utilizzato e non contiene dati) con un nuovo nome. Ai fini di questo esempio, puoi denominarlo `/oak:index/acme.product-custom-3`. Questo sostituisce l’indice `/oak:index/acme.product-custom-2`. Dopo che `/oak:index/acme.product-custom-2` è stato rimosso dal sistema, può essere rimosso anche l’indice vuoto `/oak:index/acme.product-custom-3`. Un esempio di tale indice vuoto è:

```xml
<acme.product-custom-3
        jcr:primaryType="oak:QueryIndexDefinition"
        async="async"
        compatVersion="2"
        includedPaths="/dummy"
        queryPaths="/dummy"
        type="lucene">
        <indexRules jcr:primaryType="nt:unstructured">
            <rep:root jcr:primaryType="nt:unstructured">
                <properties jcr:primaryType="nt:unstructured">
                    <dummy
                        jcr:primaryType="nt:unstructured"
                        name="dummy"
                        propertyIndex="{Boolean}true"/>
                </properties>
            </rep:root>
        </indexRules>
</acme.product-custom-3>
```

Se non è più necessario avere una personalizzazione di un indice predefinito, è necessario copiare la definizione di indice preconfigurata. Ad esempio, se hai già distribuito `damAssetLucene-8-custom-3`, ma non sono più necessarie le personalizzazioni e desideri tornare all’indice predefinito `damAssetLucene-8`, devi aggiungere un indice `damAssetLucene-8-custom-4` che contiene la definizione dell’indice di `damAssetLucene-8`.

## Ottimizzazioni di indici e query {#index-query-optimizations}

Apache Jackrabbit Oak consente configurazioni di indice flessibili per gestire in modo efficiente le query di ricerca. Gli indici sono particolarmente importanti per gli archivi più grandi. Assicurati che tutte le query siano supportate da un indice appropriato. Le query senza un indice appropriato possono leggere migliaia di nodi, pertanto viene registrata un’avvertenza.

Per informazioni su come è possibile ottimizzare le query e gli indici, consulta [questo documento](query-and-indexing-best-practices.md).
