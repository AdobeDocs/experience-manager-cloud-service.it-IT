---
title: Ricerca e indicizzazione dei contenuti
description: Scopri la ricerca e l’indicizzazione dei contenuti in AEM as a Cloud Service.
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
feature: Operations
role: Admin
source-git-commit: 8d881caf5181e9c3cdc6dcb69f0deabc2d5eeed8
workflow-type: tm+mt
source-wordcount: '2918'
ht-degree: 17%

---

# Ricerca e indicizzazione dei contenuti {#indexing}

## Modifiche in AEM as a Cloud Service {#changes-in-aem-as-a-cloud-service}

Con AEM as a Cloud Service, Adobe si sta spostando da un modello AEM incentrato sull’istanza a una visualizzazione basata sul servizio con contenitori AEM n-x, guidata dalle pipeline CI/CD in Cloud Manager. Invece di configurare e mantenere gli indici su singole istanze di AEM, è necessario specificare la configurazione dell’indice prima di una distribuzione. I cambiamenti di configurazione nella produzione stanno interrompendo i criteri CI/CD. Lo stesso vale per le modifiche dell’indice, poiché può influire sulla stabilità e sulle prestazioni del sistema se non specificato, testato e reindicizzato prima di avviarlo alla produzione.

Di seguito è riportato un elenco delle modifiche principali rispetto ad AEM 6.5 e versioni precedenti:

1. Gli utenti non hanno più accesso al Gestore indice di una singola istanza AEM per eseguire il debug, configurare o mantenere l’indicizzazione. Viene utilizzato solo per lo sviluppo locale e le distribuzioni on-premise.
1. Gli utenti non modificano gli indici su una singola istanza di AEM e non devono più preoccuparsi dei controlli di coerenza o della reindicizzazione.
1. In generale, le modifiche dell’indice vengono avviate prima di passare alla produzione per non aggirare i gateway di qualità nelle pipeline CI/CD di Cloud Manager e non influire sui KPI aziendali in produzione.
1. Tutte le metriche correlate, comprese le prestazioni di ricerca in produzione, sono disponibili per i clienti in fase di runtime per fornire una visione olistica degli argomenti di ricerca e indicizzazione.
1. I clienti possono impostare gli avvisi in base alle proprie esigenze.
1. Gli SRE monitorano lo stato di salute del sistema 24 ore su 24, 7 giorni su 7 e intervengono il prima possibile.
1. La configurazione dell’indice viene modificata tramite le distribuzioni. Le modifiche alla definizione dell’indice sono configurate come altre modifiche al contenuto.
1. A un livello elevato in AEM as a Cloud Service, con l&#39;introduzione del [modello di distribuzione continua](#index-management-using-rolling-deployments), esistono due set di indici: uno per la versione precedente e uno per la nuova versione.
1. I clienti possono vedere se il processo di indicizzazione è completo nella pagina di build di Cloud Manager e riceve una notifica quando la nuova versione è pronta per il traffico.

Limiti:

* Attualmente, la gestione degli indici su AEM as a Cloud Service è supportata solo per gli indici di tipo `lucene`. Tutte le personalizzazioni dell&#39;indice devono essere di tipo `lucene`. La proprietà `async` può essere solo una delle seguenti: `[async]`, `[async,nrt]` o `[fulltext-async]`.
* Internamente, possono essere configurati e utilizzati per le query altri indici. È possibile, ad esempio, che le query scritte sull&#39;indice `damAssetLucene` vengano eseguite in AEM as a Cloud Service in base a una versione Elasticsearch dell&#39;indice. Questa differenza non è visibile all’utente. Tuttavia, alcuni strumenti come la funzionalità `explain` riportano un indice diverso. Per le differenze tra gli indici Lucene e gli indici Elastic, vedi [la documentazione Elastic in Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/query/elastic.html). I clienti non devono e non possono configurare direttamente gli indici di Elasticsearch.
* Sono supportati solo gli analizzatori standard (ovvero gli analizzatori forniti con il prodotto). Gli analizzatori personalizzati non sono supportati.
* La ricerca per vettori di funzionalità simili (`useInSimilarity = true`) non è supportata.

>[!TIP]
>
>Per ulteriori dettagli sull&#39;indicizzazione e sulle query di Oak, inclusa una descrizione dettagliata delle funzioni di ricerca e indicizzazione avanzate, vedi la [documentazione di Apache Oak](https://jackrabbit.apache.org/oak/docs/query/query.html).


## Guida all’uso {#how-to-use}

Le definizioni degli indici possono essere suddivise in tre casi d’uso principali, come segue:

1. **Aggiungi** una nuova definizione di indice personalizzato.
2. **Aggiorna** una definizione di indice esistente aggiungendo una nuova versione.
3. **Rimuovi** una definizione di indice non più necessaria.

Per entrambi i punti 1 e 2 di cui sopra, devi creare una definizione dell’indice come parte della base di codice personalizzato nella rispettiva pianificazione delle versioni di Cloud Manager. Per ulteriori informazioni, vedere la documentazione [Distribuzione in AEM as a Cloud Service](/help/implementing/deploying/overview.md).

## Nomi indice {#index-names}

Una definizione di indice può rientrare in una delle seguenti categorie:

1. Indice preconfigurato. Si tratta di indici predefiniti forniti da AEM. Ad esempio: `/oak:index/cqPageLucene-2` o `/oak:index/damAssetLucene-8`.

2. Personalizzazione di un indice OOTB. Per personalizzare un indice OOTB, aggiungere `-custom-` seguito da un numero. `/oak:index/damAssetLucene-8-custom-1` è la personalizzazione dell&#39;indice OOTB `/oak:index/damAssetLucene-8`. Una personalizzazione è in genere una copia dell’indice OOTB, oltre a proprietà aggiuntive che devono essere indicizzate.

3. Indice completamente personalizzato: puoi creare un indice completamente nuovo da zero. Questi indici devono terminare con `-custom-` e un numero di versione. Inoltre, per evitare conflitti di denominazione, utilizza un prefisso nel nome dell’indice. Ad esempio: `/oak:index/acme.product-1-custom-2`, dove `acme.` è il prefisso.

>[!NOTE]
>
>L&#39;introduzione di nuovi indici sul tipo di nodo `dam:Asset` (in particolare gli indici full-text) è fortemente sconsigliata in quanto possono entrare in conflitto con le funzionalità dei prodotti OOTB, causando problemi funzionali e di prestazioni. Il modo più appropriato per indicizzare le query sul tipo di nodo `dam:Asset` consiste invece nel personalizzare l&#39;indice `damAssetLucene-*` aggiungendo le proprietà aggiuntive. Queste modifiche verranno automaticamente unite a una nuova versione del prodotto nelle versioni successive. In caso di dubbi, contatta il supporto Adobe per un consiglio.

## Preparazione della nuova definizione dell’indice {#preparing-the-new-index-definition}

>[!NOTE]
>
>Durante la personalizzazione di un indice predefinito, ad esempio `damAssetLucene-8`, copiare l&#39;ultima definizione di indice preconfigurato da un *ambiente Cloud Service* utilizzando Gestione pacchetti CRX DE (`/crx/packmgr/`). Rinominalo in `damAssetLucene-8-custom-1` (o versione successiva) e aggiungi le tue personalizzazioni nel file XML. Se l&#39;indice nell&#39;ambiente cloud è di tipo `elasticsearch`, sono necessarie ulteriori modifiche: modificare la proprietà `type` in `lucene`, modificare la proprietà `async` in `[async,nrt]` e modificare la proprietà `similarityTags` in `true`. In questo modo le configurazioni richieste non vengono rimosse inavvertitamente. Ad esempio, il nodo `tika` in `/oak:index/damAssetLucene-8/tika` è richiesto nell&#39;indice personalizzato distribuito in un ambiente AEM Cloud Service, ma non esiste nell&#39;SDK AEM locale.

Per le personalizzazioni di un indice OOTB, prepara un nuovo pacchetto contenente la definizione di indice personalizzata. Il nome dell’indice deve seguire il pattern di denominazione:

`<indexName>-<productVersion>-custom-<customVersion>`

Per un indice completamente personalizzato, prepara un nuovo pacchetto di definizione dell’indice che contiene la definizione dell’indice che segue questo pattern di denominazione:

`<prefix>.<indexName>-<productVersion>-custom-<customVersion>`

Come indicato nelle sezioni delle limitazioni, `type` della definizione dell&#39;indice personalizzato deve essere sempre impostato su `lucene` anche se la definizione dell&#39;indice estratto utilizzando Gestione pacchetti è di un tipo diverso (ad esempio `elasticsearch`).
È inoltre necessario modificare la proprietà `async` se la definizione dell&#39;indice estratto è impostata su `elastic-async`. La proprietà `async` deve essere impostata su uno dei seguenti valori: `[async]`, `[async,nrt]` o `[fulltext-async]` per la definizione dell&#39;indice personalizzato.

<!-- Alexandru: temporarily drafting this statement due to CQDOC-17701

The package from the above sample is built as `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`. -->

>[!NOTE]
>
>Qualsiasi pacchetto di contenuto contenente definizioni di indice deve avere le seguenti proprietà impostate nel file `properties.xml` del pacchetto di contenuto. `properties.xml` viene creato per impostazione predefinita in un nuovo pacchetto e si trova in `<package_name>/META-INF/vault/properties.xml`:
>
> * `noIntermediateSaves=true`
>
> * `allowIndexDefinitions=true`

## Distribuzione di definizioni indice personalizzate {#deploying-custom-index-definitions}

Per illustrare la distribuzione di una versione personalizzata dell&#39;indice predefinito `damAssetLucene-8`, verrà fornita una guida dettagliata. In questo esempio verrà rinominato `damAssetLucene-8-custom-1`. Il processo è quindi il seguente:

1. Creare una nuova cartella con il nome di indice aggiornato nella directory `ui.apps`:
   * Esempio: `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/`

2. Aggiungere un file di configurazione `.content.xml` con le configurazioni personalizzate nella cartella creata. Di seguito è riportato un esempio di personalizzazione:
Nome file: `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/.content.xml`

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:dam="http://www.day.com/dam/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0" xmlns:oak="http://jackrabbit.apache.org/oak/ns/1.0" xmlns:rep="internal"
       jcr:mixinTypes="[rep:AccessControllable]"
       jcr:primaryType="oak:QueryIndexDefinition"
       async="[async,nrt]"
       compatVersion="{Long}2"
       evaluatePathRestrictions="{Boolean}true"
       includedPaths="[/content/dam]"
       maxFieldLength="{Long}100000"
       type="lucene">
       <facets
           jcr:primaryType="nt:unstructured"
           secure="statistical"
           topChildren="100"/>
       <indexRules jcr:primaryType="nt:unstructured">
           <dam:Asset jcr:primaryType="nt:unstructured">
               <properties jcr:primaryType="nt:unstructured">
                   <cqTags
                       jcr:primaryType="nt:unstructured"
                       name="jcr:content/metadata/cq:tags"
                       nodeScopeIndex="{Boolean}true"
                       propertyIndex="{Boolean}true"
                       useInSpellcheck="{Boolean}true"
                       useInSuggest="{Boolean}true"/>
               </properties>
           </dam:Asset>
       </indexRules>
       <tika jcr:primaryType="nt:folder">
           <config.xml jcr:primaryType="nt:file"/>
       </tika>
   </jcr:root>
   ```

3. Aggiungere una voce al filtro FileVault in `ui.apps/src/main/content/META-INF/vault/filter.xml`:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <workspaceFilter version="1.0">
       ...
       <filter root="/oak:index/damAssetLucene-8-custom-1"/> 
   </workspaceFilter>
   ```

4. Aggiungi un file di configurazione per Apache Tika in: `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/tika/config.xml`:

   ```xml
   <properties>
       <detectors>
           <detector class="org.apache.tika.detect.TypeDetector"/>
       </detectors>
       <parsers>
           <parser class="org.apache.tika.parser.DefaultParser">
           <mime>text/plain</mime>
           </parser>
       </parsers>
       <service-loader initializableProblemHandler="ignore" dynamic="true"/>
   </properties>
   ```

5. Assicurati che la configurazione sia conforme alle linee guida fornite nella sezione [Configurazione del progetto](#project-configuration). Apportare le modifiche necessarie di conseguenza.

## Configurazione del progetto

Si consiglia vivamente di utilizzare la versione >= `1.3.2` del Jackrabbit `filevault-package-maven-plugin`. Per incorporarlo nel progetto, segui questi passaggi:

1. Aggiorna la versione nel livello principale `pom.xml`:

   ```xml
   <plugin>
       <groupId>org.apache.jackrabbit</groupId>
           <artifactId>filevault-package-maven-plugin</artifactId>
           ...
           <version>1.3.2</version>
       ...
   </plugin>
   ```

2. Aggiungi quanto segue al livello principale `pom.xml`:

   ```xml
   <jackrabbit-packagetype>
       <options>   
           <immutableRootNodeNames>apps,libs,oak:index</immutableRootNodeNames>
       </options>
   </jackrabbit-packagetype>
   ```

   Di seguito è riportato un esempio del file `pom.xml` di primo livello del progetto con le configurazioni sopra indicate:

   Nome file: `pom.xml`

   ```xml
   <plugin>
       <groupId>org.apache.jackrabbit</groupId>
           <artifactId>filevault-package-maven-plugin</artifactId>
           ...
           <version>1.3.2</version>
           <configuration>
               ...
               <validatorsSettings>
                   <jackrabbit-packagetype>
                       <options>
                           <immutableRootNodeNames>apps,libs,oak:index</immutableRootNodeNames>
                       </options>
                   </jackrabbit-packagetype>
                   ...
               ...
   </plugin>
   ```

3. In `ui.apps/pom.xml` e `ui.apps.structure/pom.xml`, è necessario abilitare le opzioni `allowIndexDefinitions` e `noIntermediateSaves` in `filevault-package-maven-plugin`. L&#39;abilitazione di `allowIndexDefinitions` consente definizioni di indice personalizzate, mentre `noIntermediateSaves` garantisce che le configurazioni vengano aggiunte atomicamente.

   Nomi file: `ui.apps/pom.xml` e `ui.apps.structure/pom.xml`

   ```xml
   <plugin>
       <groupId>org.apache.jackrabbit</groupId>
           <artifactId>filevault-package-maven-plugin</artifactId>
           <configuration>
               <allowIndexDefinitions>true</allowIndexDefinitions>
               <properties>
                   <cloudManagerTarget>none</cloudManagerTarget>
                   <noIntermediateSaves>true</noIntermediateSaves>
               </properties>
       ...
   </plugin>
   ```

4. Aggiungi un filtro per `/oak:index` in `ui.apps.structure/pom.xml`:

   ```xml
   <filters>
       ...
       <filter><root>/oak:index</root></filter>
   </filters>
   ```

Dopo aver aggiunto la nuova definizione dell’indice, distribuisci la nuova applicazione utilizzando Cloud Manager. Questa distribuzione avvia due processi, responsabili dell’aggiunta (e dell’unione, se necessario) delle definizioni dell’indice a MongoDB e Azure Segment Store rispettivamente per l’authoring e la pubblicazione. Prima dello switch, gli archivi sottostanti vengono reindicizzati con le definizioni di indice aggiornate.

>[!TIP]
>
>Per ulteriori dettagli sulla struttura del pacchetto richiesta per AEM as a Cloud Service, vedi [Struttura del progetto AEM](/help/implementing/developing/introduction/aem-project-content-package-structure.md).

## Gestione dell’indice tramite distribuzioni continue {#index-management-using-rolling-deployments}

### Gestione dell’indice {#what-is-index-management}

La gestione degli indici riguarda l’aggiunta, la rimozione e la modifica degli indici. La modifica della *definizione* di un indice è veloce, ma la sua applicazione (spesso chiamata “creazione di un indice”, o, per gli indici esistenti, “reindicizzazione”) richiede tempo. Non è istantaneo: l’archivio deve essere analizzato per individuare i dati da indicizzare.

### Cosa sono le distribuzioni continue {#what-are-rolling-deployments}

Una distribuzione continua consente di eseguire senza tempi di inattività gli aggiornamenti e offre rapidi rollback. La vecchia versione dell&#39;applicazione viene eseguita contemporaneamente alla nuova versione dell&#39;applicazione.

### Aree di sola lettura e di lettura/scrittura {#read-only-and-read-write-areas}

Alcune aree dell’archivio (parti di sola lettura dell’archivio) possono essere diverse nella vecchia e nella nuova versione dell’applicazione. Le aree di sola lettura dell&#39;archivio sono in genere `/app` e `/libs`. Nell’esempio seguente, il corsivo viene utilizzato per contrassegnare le aree di sola lettura, mentre il grassetto viene utilizzato per le aree di lettura/scrittura.

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

Durante lo sviluppo o quando si utilizzano installazioni on-premise, gli indici possono essere aggiunti, rimossi o modificati in fase di runtime. Gli indici vengono utilizzati quando sono disponibili. Se un indice non è ancora utilizzato nella vecchia versione dell’applicazione, in genere viene generato durante un periodo di inattività pianificato. Lo stesso si verifica quando si rimuove un indice o si modifica un indice esistente. Quando si rimuove un indice, questo diventa non disponibile.

### Gestione degli indici con distribuzioni continue {#index-management-with-rolling-deployments}

Con le distribuzioni continue, non si verificano tempi di inattività. Per un certo periodo di tempo durante un aggiornamento, sia la vecchia versione (ad esempio, la versione 1) dell’applicazione che la nuova versione (versione 2) vengono eseguite contemporaneamente sullo stesso archivio. Se la versione 1 richiede la disponibilità di un determinato indice, questo non deve essere rimosso nella versione 2. L’indice deve essere rimosso in un secondo momento, ad esempio nella versione 3, che garantisce che la versione 1 dell’applicazione non è più in esecuzione. Inoltre, le applicazioni devono essere scritte in modo che la versione 1 funzioni bene, anche se la versione 2 è in esecuzione, e se sono disponibili indici della versione 2.

Al termine dell’aggiornamento alla nuova versione, i vecchi indici possono essere raccolti come rifiuti dal sistema. I vecchi indici in genere rimangono per una settimana, per velocizzare i rollback (se dovesse essere necessario un rollback).

La tabella seguente mostra cinque definizioni di indice: l’indice `cqPageLucene` viene utilizzato in entrambe le versioni mentre l’indice `damAssetLucene-custom-1` viene utilizzato solo nella versione 2.

>[!NOTE]
>
>`<indexName>-custom-<customerVersionNumber>` è necessario affinché AEM as a Cloud Service possa contrassegnarlo come sostitutivo di un indice esistente.

| Indice | Indice predefinito | Uso nella versione 1 | Uso nella versione 2 |
|---|---|---|---|
| /oak:index/damAssetLucene-8 | Sì | Sì | No |
| /oak:index/damAssetLucene-8-custom-1 | Sì (personalizzato) | No | Sì |
| /oak:index/acme.product-1-custom-1 | No | Sì | No |
| /oak:index/acme.product-1-custom-2 | No | No | Sì |
| /oak:index/cqPageLucene-2 | Sì | Sì | Sì |

Il numero di versione è incrementato ogni volta che l’indice viene modificato. Per evitare che i nomi di indice personalizzati si scontrino con i nomi di indice del prodotto stesso, gli indici personalizzati e le modifiche agli indici predefiniti devono terminare con `-custom-<number>`.

### Modifiche agli indici predefiniti {#changes-to-out-of-the-box-indexes}

Dopo che Adobe ha modificato un indice predefinito come `damAssetLucene` o `cqPageLucene`, viene creato un nuovo indice denominato `damAssetLucene-2` o `cqPageLucene-2`. Oppure, se l’indice è già stato personalizzato, la definizione dell’indice personalizzato viene unita alle modifiche nell’indice predefinito, come mostrato di seguito. L’unione delle modifiche avviene automaticamente. Ciò significa che non è necessario eseguire alcuna operazione se un indice predefinito cambia. Tuttavia, è possibile personalizzare di nuovo l’indice in un secondo momento. In questo caso, è importante utilizzare la versione più recente (unita) come linea di base.

| Indice | Indice predefinito | Uso nella versione 2 | Uso nella versione 3 |
|---|---|---|---|
| /oak:index/damAssetLucene-1-custom-1 | Sì (personalizzato) | Sì | No |
| /oak:index/damAssetLucene-2-custom-1 | Sì (unione automatica di damAssetLucene-1-custom-1 e damAssetLucene-2) | No | Sì |
| /oak:index/cqPageLucene-1 | Sì | Sì | No |
| /oak:index/cqPageLucene-2 | Sì | No | Sì |

È importante notare che gli ambienti potrebbero trovarsi su diverse versioni di AEM. Ad esempio: l&#39;ambiente `dev` è nella versione `X+1` mentre stage e prod sono ancora nella versione `X` e sono in attesa di essere aggiornati alla versione `X+1` dopo l&#39;esecuzione dei test richiesti in `dev`. Se la versione `X+1` include una versione più recente di un indice di prodotto che è stata personalizzata ed è necessaria una nuova personalizzazione di tale indice, la tabella seguente spiegherà quali versioni devono essere impostate sugli ambienti basati sulla versione di AEM:

| Ambiente (versione di AEM) | Versione indice prodotto | Versione indice personalizzata esistente | Nuova versione dell’indice personalizzato |
|-----------------------------------|-----------------------|-------------------------------|----------------------------|
| Sviluppo (X+1) | damAssetLucene-11 | damAssetLucene-11-custom-1 | damAssetLucene-11-custom-2 |
| Fase (X) | damAssetLucene-10 | damAssetLucene-10-custom-1 | damAssetLucene-10-custom-2 |
| Prod (X) | damAssetLucene-10 | damAssetLucene-10-custom-1 | damAssetLucene-10-custom-2 |


### Limitazioni attuali {#current-limitations}

La gestione degli indici è supportata solo per gli indici di tipo `lucene`, con `compatVersion` impostato su `2`. Internamente, possono essere configurati e utilizzati per le query altri indici, ad esempio gli indici Elasticsearch. In AEM as a Cloud Service, le query scritte sull&#39;indice `damAssetLucene` potrebbero essere eseguite su una versione Elasticsearch di questo indice. Questa differenza è invisibile all&#39;utente dell&#39;applicazione, tuttavia alcuni strumenti come la funzionalità `explain` segnalano un indice diverso. Per le differenze tra gli indici Lucene e Elasticsearch, consulta [la documentazione di Elasticsearch in Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/query/elastic.html). I clienti non possono e non devono configurare direttamente gli indici Elasticsearch.

Sono supportati solo gli analizzatori incorporati (ovvero, gli analizzatori forniti con il prodotto). Gli analizzatori personalizzati non sono supportati.

Al momento, l&#39;indicizzazione del contenuto di `/oak:index` non è supportata.

Per ottenere le migliori prestazioni operative, gli indici non dovrebbero essere eccessivamente grandi. La dimensione totale di tutti gli indici può essere utilizzata come guida. Se questa dimensione aumenta di oltre il 100% dopo l’aggiunta degli indici personalizzati e la regolazione degli indici standard in un ambiente di sviluppo, è necessario regolare le definizioni degli indici personalizzati. AEM as a Cloud Service può impedire la distribuzione o la rimozione di indici che influirebbero negativamente sulla stabilità e sulle prestazioni del sistema.

### Aggiunta di un indice {#adding-an-index}

Per aggiungere un indice completamente personalizzato denominato `/oak:index/acme.product-1-custom-1`, da utilizzare in una nuova versione dell&#39;applicazione e successivamente, è necessario configurare l&#39;indice come segue:

`acme.product-1-custom-1`

Questa configurazione funziona ponendo un identificatore personalizzato davanti al nome dell&#39;indice, seguito da un punto (**`.`**). L’identificatore deve contenere da 2 a 5 caratteri.

Come sopra, questa configurazione assicura che l’indice sia utilizzato solo dalla nuova versione dell’applicazione.

### Modifica di un indice {#changing-an-index}

Quando viene modificato un indice esistente, è necessario aggiungere un nuovo indice con la modifica della definizione. Ad esempio, supponi che l’indice esistente `/oak:index/acme.product-1-custom-1` venga modificato. Il vecchio indice è memorizzato in `/oak:index/acme.product-1-custom-1` e il nuovo indice è memorizzato in `/oak:index/acme.product-1-custom-2`.

La vecchia versione dell’applicazione utilizza la seguente configurazione:

`/oak:index/acme.product-1-custom-1`

La nuova versione dell’applicazione utilizza la seguente configurazione (modificata):

`/oak:index/acme.product-1-custom-2`

>[!NOTE]
>
>Le definizioni degli indici su AEM as a Cloud Service potrebbero non corrispondere completamente a quelle su un’istanza di sviluppo locale. L’istanza di sviluppo non dispone di una configurazione Tika, mentre le istanze di AEM as a Cloud Service ne hanno una. Se personalizzi un indice con una configurazione Tika, mantieni la configurazione Tika.

### Annullamento di una modifica {#undoing-a-change}

A volte, è necessario annullare una modifica in una definizione di indice, ad esempio a causa di un errore o perché la modifica non è più necessaria. Se ad esempio la definizione dell&#39;indice `damAssetLucene-8-custom-3` contiene un errore, è possibile ripristinare la definizione precedente, `damAssetLucene-8-custom-2`. A tale scopo, creare un nuovo indice denominato `damAssetLucene-8-custom-4` che sia una copia dell&#39;indice precedente, `damAssetLucene-8-custom-2.`

### Rimozione di un indice {#removing-an-index}

Ciò che segue si applica solo alle personalizzazioni degli indici predefiniti e agli indici completamente personalizzati. Tieni presente che gli indici OOTB originali non possono essere rimossi, in quanto sono utilizzati da AEM.

Per garantire l’integrità e la stabilità del sistema, una volta implementate, le definizioni degli indici dovrebbero essere trattate come immutabili. Se devi rimuovere un indice personalizzato o una personalizzazione, crea una nuova versione di tale indice con una definizione che simuli efficacemente la rimozione
(vedi gli esempi di seguito).

Una volta distribuita una nuova versione di un indice, la versione precedente dello stesso indice non verrà più utilizzata dalle query.
La versione precedente non verrà eliminata immediatamente dall’ambiente,
ma diventerà idoneo per la raccolta di rifiuti tramite un meccanismo di pulizia che viene eseguito periodicamente.
Dopo un periodo di tolleranza progettato per consentire il recupero in caso di errori
(attualmente, 7 giorni a partire dalla rimozione dell’indicizzazione, ma soggetti a modifiche),
questo meccanismo di pulizia eliminerà i dati di indice non utilizzati,
e disabilita o rimuove la versione precedente dell’indice dall’ambiente.

Di seguito vengono descritti i due casi possibili: rimozione delle personalizzazioni di un indice OOTB e rimozione di un indice completamente personalizzato.

#### Rimozione delle personalizzazioni di un indice predefinito

Segui i passaggi descritti in [Annullamento di una modifica](#undoing-a-change-undoing-a-change) utilizzando le definizioni dell&#39;indice OOTB come nuova versione. Ad esempio, se `damAssetLucene-8-custom-3` è già stato distribuito, ma non sono più necessarie le personalizzazioni e si desidera tornare all&#39;indice predefinito `damAssetLucene-8`, è necessario aggiungere un indice `damAssetLucene-8-custom-4` che contiene la definizione dell&#39;indice di `damAssetLucene-8`.

#### Rimozione di un indice completamente personalizzato

Segui i passaggi descritti in [Annullamento di una modifica](#undoing-a-change-undoing-a-change) utilizzando un indice fittizio come nuova versione. Un indice fittizio non viene mai utilizzato per le query e non contiene dati, pertanto l’effetto è lo stesso di un indice inesistente. In questo esempio è possibile denominarlo `/oak:index/acme.product-1-custom-3`. Questo nome sostituisce l&#39;indice `/oak:index/acme.product-1-custom-2`. Un esempio di tale indice fittizio è:

```xml
<acme.product-1-custom-3
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
</acme.product-1-custom-3>
```

## Ottimizzazioni di indici e query {#index-query-optimizations}

Apache Jackrabbit Oak consente configurazioni di indice flessibili per gestire in modo efficiente le query di ricerca. Gli indici sono particolarmente importanti per gli archivi più grandi. Assicurati che tutte le query siano supportate da un indice appropriato. Le query senza un indice appropriato possono leggere migliaia di nodi, che vengono quindi registrati come un avviso.

Consulta [questo documento](query-and-indexing-best-practices.md) per informazioni su come è possibile ottimizzare le query e gli indici.
