---
title: Ricerca e indicizzazione dei contenuti
description: Scopri la ricerca e l’indicizzazione dei contenuti in AEM as a Cloud Service.
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
feature: Operations
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '2442'
ht-degree: 29%

---

# Ricerca e indicizzazione dei contenuti {#indexing}

## Modifiche in AEM as a Cloud Service {#changes-in-aem-as-a-cloud-service}

Con AEM as a Cloud Service, Adobe si sta spostando da un modello AEM incentrato sull’istanza a una visualizzazione basata sul servizio con contenitori AEM n-x, guidata dalle pipeline CI/CD in Cloud Manager. Invece di configurare e mantenere gli indici su singole istanze di AEM, è necessario specificare la configurazione dell’indice prima di una distribuzione. I cambiamenti di configurazione nella produzione chiaramente infrangono i criteri CI/CD. Lo stesso vale per le modifiche dell’indice in quanto può influire sulla stabilità e sulle prestazioni del sistema se non specificamente testato e reindicizzato prima dell’introduzione nella produzione.

Di seguito è riportato un elenco delle modifiche principali rispetto ad AEM 6.5 e versioni precedenti:

1. Gli utenti non hanno più accesso al Gestore indice di una singola istanza AEM per eseguire il debug, configurare o mantenere l’indicizzazione. Viene utilizzato solo per lo sviluppo locale e le distribuzioni on-premise.
1. Gli utenti non modificano gli indici su una singola istanza AEM e non devono più preoccuparsi dei controlli di coerenza o della reindicizzazione.
1. In generale, le modifiche dell’indice vengono avviate prima di passare alla produzione per non aggirare i gateway di qualità nelle pipeline CI/CD di Cloud Manager e non influire sui KPI aziendali in produzione.
1. Tutte le metriche correlate, comprese le prestazioni di ricerca in produzione, sono disponibili per i clienti in fase di runtime per fornire una visione olistica degli argomenti di ricerca e indicizzazione.
1. I clienti possono impostare gli avvisi in base alle proprie esigenze.
1. Gli SRE monitorano lo stato di salute del sistema 24 ore su 24, 7 giorni su 7 e intervengono il prima possibile.
1. La configurazione dell’indice viene modificata tramite le distribuzioni. Le modifiche alla definizione dell’indice sono configurate come altre modifiche al contenuto.
1. Ad alto livello sull&#39;AEM as a Cloud Service, con l&#39;introduzione della [modello di distribuzione continua](#index-management-using-rolling-deployments), esistono due set di indici: uno per la versione precedente e uno per la nuova versione.
1. I clienti possono vedere se il processo di indicizzazione è stato completato nella pagina di build di Cloud Manager e ricevono una notifica quando la nuova versione è pronta per il traffico.

Limiti:

* Attualmente, la gestione degli indici su AEM as a Cloud Service è supportata solo per gli indici di tipo `lucene`.
* Sono supportati solo gli analizzatori standard (ovvero gli analizzatori forniti con il prodotto). Gli analizzatori personalizzati non sono supportati.
* Internamente, possono essere configurati e utilizzati per le query altri indici. Ad esempio, le query scritte rispetto all’indice `damAssetLucene` potrebbero, su Skyline, essere eseguite in base a una versione Elasticsearch di questo indice. Questa differenza generalmente non è visibile all’applicazione e all’utente, tuttavia, alcuni strumenti come `explain` La funzionalità segnala un indice diverso. Per le differenze tra gli indici Lucene e gli indici Elastic, vedi [la documentazione Elastic in Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/query/elastic.html). I clienti non devono e non possono configurare direttamente gli indici Elasticsearch.
* Ricerca per vettori di funzionalità simili (`useInSimilarity = true`) non è supportato.

>[!TIP]
>
>Per ulteriori dettagli sull’indicizzazione e le query Oak, inclusa una descrizione dettagliata delle funzioni di ricerca e indicizzazione avanzate, vedi [Documentazione di Apache Oak](https://jackrabbit.apache.org/oak/docs/query/query.html).


## Guida all’uso {#how-to-use}

Le definizioni degli indici possono essere suddivise in tre casi d’uso principali, come segue:

1. **Aggiungi** una nuova definizione di indice personalizzato.
2. **Aggiorna** una definizione di indice esistente aggiungendo una nuova versione.
3. **Rimuovi** una definizione di indice non più necessaria.

Per entrambi i punti 1 e 2 di cui sopra, devi creare una definizione dell’indice come parte della base di codice personalizzata nella rispettiva pianificazione della versione di Cloud Manager. Per ulteriori informazioni, vedere [Distribuzione a AEM as a Cloud Service](/help/implementing/deploying/overview.md) documentazione.

## Nomi indice {#index-names}

Una definizione di indice può rientrare in una delle seguenti categorie:

1. Indice preconfigurato. Ad esempio: `/oak:index/cqPageLucene-2` o `/oak:index/damAssetLucene-8`.

2. Personalizzazione di un indice OOTB. Questi sono indicati aggiungendo `-custom-` seguito da un identificatore numerico al nome originale dell’indice. Ad esempio: `/oak:index/damAssetLucene-8-custom-1`.

3. Indice completamente personalizzato: è possibile creare un indice completamente nuovo da zero. Il nome deve avere un prefisso per evitare conflitti di denominazione. Ad esempio: `/oak:index/acme.product-1-custom-2`, dove il prefisso è `acme.`

>[!NOTE]
>
>Introduzione di nuovi indici sul `dam:Asset` nodetype (in particolare gli indici full-text) è fortemente sconsigliato in quanto possono entrare in conflitto con le funzionalità dei prodotti OOTB e causare problemi funzionali e di prestazioni. In generale, l&#39;aggiunta di proprietà aggiuntive al `damAssetLucene-*` versione indice è il modo più appropriato per indicizzare le query sulla `dam:Asset` nodetype (queste modifiche verranno automaticamente unite in una nuova versione del prodotto dell’indice se viene successivamente rilasciato). In caso di dubbi, contatta il supporto Adobe per un consiglio.

## Preparazione della nuova definizione dell’indice {#preparing-the-new-index-definition}

>[!NOTE]
>
>Ad esempio, per personalizzare un indice predefinito: `damAssetLucene-8`, copia l’ultima definizione di indice preconfigurata da una *Ambiente Cloud Service* utilizzo di Gestione pacchetti CRX DE (`/crx/packmgr/`). Rinomina in `damAssetLucene-8-custom-1` (o versione successiva) e aggiungere le personalizzazioni nel file XML. In questo modo le configurazioni richieste non vengono rimosse inavvertitamente. Ad esempio, il `tika` nodo sotto `/oak:index/damAssetLucene-8/tika` è richiesto nell’indice personalizzato distribuito in un ambiente AEM Cloud Service, ma non esiste nell’SDK AEM locale.

Per le personalizzazioni di un indice OOTB, prepara un nuovo pacchetto contenente la definizione effettiva dell’indice che segue questo pattern di denominazione:

`<indexName>-<productVersion>-custom-<customVersion>`

Per un indice completamente personalizzato, prepara un nuovo pacchetto di definizione dell’indice che contiene la definizione dell’indice che segue questo pattern di denominazione:

`<prefix>.<indexName>-<productVersion>-custom-<customVersion>`

<!-- Alexandru: temporarily drafting this statement due to CQDOC-17701

The package from the above sample is built as `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`. -->

>[!NOTE]
>
>Qualsiasi pacchetto di contenuto contenente le definizioni degli indici deve avere le seguenti proprietà impostate nel file delle proprietà, situato in `<package_name>/META-INF/vault/properties.xml`:
>
> * `noIntermediateSaves=true`
>
> * `allowIndexDefinitions=true`

## Distribuzione di definizioni indice personalizzate {#deploying-custom-index-definitions}

Per illustrare la distribuzione di una versione personalizzata dell’indice predefinito `damAssetLucene-8`, ti forniremo una guida dettagliata. In questo esempio, lo rinomineremo `damAssetLucene-8-custom-1`. Il processo è quindi il seguente:

1. Crea una nuova cartella con il nome di indice aggiornato nel `ui.apps` directory:
   * Esempio: `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/`

2. Aggiungi un file di configurazione `.content.xml` con le configurazioni personalizzate all’interno della cartella creata. Di seguito è riportato un esempio di personalizzazione: Filename: `ui.apps/src/main/content/jcr_root/_oak_index/damAssetLucene-8-custom-1/.content.xml`

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

5. Assicurati che la configurazione sia conforme alle linee guida fornite in [Configurazione del progetto](#project-configuration) sezione. Apportare le modifiche necessarie di conseguenza.

## Configurazione del progetto

Si consiglia vivamente di utilizzare versione >= `1.3.2` del Coniglio di Giacca `filevault-package-maven-plugin`. Per incorporarlo nel progetto, segui questi passaggi:

1. Aggiornare la versione nel livello superiore `pom.xml`:

   ```xml
   <plugin>
       <groupId>org.apache.jackrabbit</groupId>
           <artifactId>filevault-package-maven-plugin</artifactId>
           ...
           <version>1.3.2</version>
       ...
   </plugin>
   ```

2. Aggiungi quanto segue al livello superiore `pom.xml`:

   ```xml
   <jackrabbit-packagetype>
       <options>   
           <immutableRootNodeNames>apps,libs,oak:index</immutableRootNodeNames>
       </options>
   </jackrabbit-packagetype>
   ```

   Di seguito è riportato un esempio del livello principale del progetto `pom.xml` il file con le configurazioni di cui sopra includeva:

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

3. In entrata `ui.apps/pom.xml` e `ui.apps.structure/pom.xml` è necessario abilitare `allowIndexDefinitions` e `noIntermediateSaves` opzioni in `filevault-package-maven-plugin`. Abilitazione `allowIndexDefinitions` consente definizioni di indice personalizzate, mentre `noIntermediateSaves` assicura che le configurazioni vengano aggiunte atomicamente.

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
>Per maggiori dettagli sulla struttura del pacchetto richiesta per l’AEM as a Cloud Service, vedi [Struttura dei progetti AEM](/help/implementing/developing/introduction/aem-project-content-package-structure.md).

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

Durante lo sviluppo o quando si utilizzano installazioni on-premise, gli indici possono essere aggiunti, rimossi o modificati in fase di runtime. Gli indici vengono utilizzati quando sono disponibili. Se un indice non è ancora utilizzato nella vecchia versione dell’applicazione, in genere viene generato durante un periodo di inattività pianificato. Lo stesso si verifica quando si rimuove un indice o si modifica un indice esistente. Quando si rimuove un indice, questo diventa non disponibile.

### Gestione degli indici con distribuzioni continue {#index-management-with-rolling-deployments}

Con le distribuzioni continue, non si verificano tempi di inattività. Per un certo periodo di tempo durante un aggiornamento, sia la vecchia versione (ad esempio, la versione 1) dell’applicazione che la nuova versione (versione 2) vengono eseguite contemporaneamente sullo stesso archivio. Se la versione 1 richiede la disponibilità di un determinato indice, questo non deve essere rimosso nella versione 2. L’indice deve essere rimosso in un secondo momento, ad esempio nella versione 3, che garantisce che la versione 1 dell’applicazione non è più in esecuzione. Inoltre, le applicazioni devono essere scritte in modo che la versione 1 funzioni bene, anche se la versione 2 è in esecuzione, e se sono disponibili indici della versione 2.

Al termine dell’aggiornamento alla nuova versione, i vecchi indici possono essere raccolti come rifiuti dal sistema. I vecchi indici potrebbero rimanere ancora per un po’ di tempo, per velocizzare i rollback (se dovesse essere necessario un rollback).

La tabella seguente mostra cinque definizioni di indice: l’indice `cqPageLucene` viene utilizzato in entrambe le versioni mentre l’indice `damAssetLucene-custom-1` viene utilizzato solo nella versione 2.

>[!NOTE]
>
>Il `<indexName>-custom-<customerVersionNumber>` è necessario affinché l’AEM as a Cloud Service possa contrassegnarlo come sostitutivo di un indice esistente.

| Indice | Indice predefinito | Uso nella versione 1 | Uso nella versione 2 |
|---|---|---|---|
| /oak:index/damAssetLucene | Sì | Sì | No |
| /oak:index/damAssetLucene-custom-1 | Sì (personalizzato) | No | Sì |
| /oak:index/acme.product-custom-1 | No | Sì | No |
| /oak:index/acme.product-custom-2 | No | No | Sì |
| /oak:index/cqPageLucene | Sì | Sì | Sì |

Il numero di versione è incrementato ogni volta che l’indice viene modificato. Per evitare che i nomi di indice personalizzati si scontrino con i nomi di indice del prodotto stesso, gli indici personalizzati e le modifiche agli indici predefiniti devono terminare con `-custom-<number>`.

### Modifiche agli indici predefiniti {#changes-to-out-of-the-box-indexes}

Dopo un Adobe cambia un indice predefinito come &quot;damAssetLucene&quot; o &quot;cqPageLucene&quot;, un nuovo indice denominato `damAssetLucene-2` o `cqPageLucene-2` viene creato. Oppure, se l’indice è già stato personalizzato, la definizione dell’indice personalizzato viene unita alle modifiche nell’indice predefinito, come mostrato di seguito. L’unione delle modifiche avviene automaticamente. Ciò significa che non è necessario eseguire alcuna operazione se un indice predefinito cambia. Tuttavia, è possibile personalizzare di nuovo l’indice in un secondo momento.

| Indice | Indice predefinito | Uso nella versione 2 | Uso nella versione 3 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | Sì (personalizzato) | Sì | No |
| /oak:index/damAssetLucene-2-custom-1 | Sì (unione automatica di damAssetLucene-custom-1 e damAssetLucene-2) | No | Sì |
| /oak:index/cqPageLucene | Sì | Sì | No |
| /oak:index/cqPageLucene-2 | Sì | No | Sì |

### Limitazioni attuali {#current-limitations}

La gestione degli indici è supportata solo per gli indici di tipo `lucene`, con `compatVersion` imposta su `2`. Internamente, possono essere configurati e utilizzati per le query altri indici, ad esempio indici Elasticsearch. Query scritte rispetto al `damAssetLucene` In caso di AEM as a Cloud Service, l&#39;indice potrebbe essere eseguito con una versione Elasticsearch di questo indice. Questa differenza è invisibile all’utente dell’applicazione, tuttavia alcuni strumenti come `explain` la funzione segnala un indice diverso. Per le differenze tra gli indici Lucene e Elasticsearch, consulta [la documentazione relativa agli Elasticsearch in Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/query/elastic.html). I clienti non possono e non devono configurare direttamente gli indici Elasticsearch.

Sono supportati solo gli analizzatori incorporati (ovvero, gli analizzatori forniti con il prodotto). Gli analizzatori personalizzati non sono supportati.

Per ottenere le migliori prestazioni operative, gli indici non dovrebbero essere eccessivamente grandi. La dimensione totale di tutti gli indici può essere utilizzata come guida. Se questa dimensione aumenta di oltre il 100% dopo l’aggiunta degli indici personalizzati e la regolazione degli indici standard in un ambiente di sviluppo, è necessario regolare le definizioni degli indici personalizzati. AEM as a Cloud Service può impedire la distribuzione di indici che influirebbero negativamente sulla stabilità e sulle prestazioni del sistema.

### Aggiunta di un indice {#adding-an-index}

Per aggiungere un indice completamente personalizzato denominato `/oak:index/acme.product-custom-1`, per essere utilizzato in una nuova versione dell’applicazione e successivamente, l’indice deve essere configurato come segue:

`acme.product-1-custom-1`

Questa configurazione funziona ponendo un identificatore personalizzato davanti al nome dell’indice, seguito da un punto (**`.`**). L’identificatore deve contenere da 2 a 5 caratteri.

Come sopra, questa configurazione assicura che l’indice sia utilizzato solo dalla nuova versione dell’applicazione.

### Modifica di un indice {#changing-an-index}

Quando viene modificato un indice esistente, è necessario aggiungere un nuovo indice con la modifica della definizione. Ad esempio, supponi che l’indice esistente `/oak:index/acme.product-custom-1` venga modificato. Il vecchio indice è memorizzato in `/oak:index/acme.product-custom-1` e il nuovo indice è memorizzato in `/oak:index/acme.product-custom-2`.

La vecchia versione dell’applicazione utilizza la seguente configurazione:

`/oak:index/acme.product-custom-1`

La nuova versione dell’applicazione utilizza la seguente configurazione (modificata):

`/oak:index/acme.product-custom-2`

>[!NOTE]
>
>Le definizioni degli indici su AEM as a Cloud Service potrebbero non corrispondere completamente a quelle su un’istanza di sviluppo locale. L’istanza di sviluppo non dispone di una configurazione Tika, mentre le istanze di AEM as a Cloud Service ne hanno una. Se personalizzi un indice con una configurazione Tika, mantieni la configurazione Tika.

### Annullamento di una modifica {#undoing-a-change}

A volte, è necessario annullare una modifica nella definizione di un indice. Ciò potrebbe verificarsi a causa di un errore involontario o perché la modifica non è più necessaria. Prendi, ad esempio, la definizione dell’indice `damAssetLucene-8-custom-3,` creato in modo errato ed è già stato distribuito. Di conseguenza, desideri ripristinare la precedente definizione dell’indice, `damAssetLucene-8-custom-2.` A questo scopo, devi introdurre un nuovo indice denominato `damAssetLucene-8-custom-4` che incorpora la definizione dell&#39;indice precedente, `damAssetLucene-8-custom-2.`

### Rimozione di un indice {#removing-an-index}

Ciò che segue si applica solo agli indici personalizzati. Gli indici di prodotto non possono essere rimossi poiché sono utilizzati da AEM.

Se un indice viene rimosso in una versione successiva dell’applicazione, puoi definire un indice vuoto (un indice vuoto che non viene mai utilizzato e non contiene dati) con un nuovo nome. Per questo esempio, puoi denominarlo `/oak:index/acme.product-custom-3`. Questo nome sostituisce l’indice `/oak:index/acme.product-custom-2`. Dopo `/oak:index/acme.product-custom-2` viene rimosso dal sistema, l’indice vuoto `/oak:index/acme.product-custom-3` possono quindi essere rimossi. Un esempio di tale indice vuoto è:

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

Apache Jackrabbit Oak consente configurazioni di indice flessibili per gestire in modo efficiente le query di ricerca. Gli indici sono particolarmente importanti per gli archivi più grandi. Assicurati che tutte le query siano supportate da un indice appropriato. Le query senza un indice appropriato possono leggere migliaia di nodi, che vengono quindi registrati come un avviso.

Consulta [questo documento](query-and-indexing-best-practices.md) per informazioni su come è possibile ottimizzare le query e gli indici.
