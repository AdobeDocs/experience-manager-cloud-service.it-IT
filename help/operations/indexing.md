---
title: Ricerca e indicizzazione dei contenuti
description: Ricerca e indicizzazione dei contenuti
exl-id: 4fe5375c-1c84-44e7-9f78-1ac18fc6ea6b
source-git-commit: eae25dc48a7cd5d257e23b515f497588a13917ea
workflow-type: tm+mt
source-wordcount: '1780'
ht-degree: 2%

---

# Ricerca e indicizzazione dei contenuti {#indexing}

## Modifiche in AEM come Cloud Service {#changes-in-aem-as-a-cloud-service}

Con AEM come Cloud Service, l’Adobe si sta spostando da un modello AEM incentrato sull’istanza a una visualizzazione basata sui servizi con contenitori AEM n-x, guidato da pipeline CI/CD in Cloud Manager. Invece di configurare e mantenere gli indici su singole istanze di AEM, è necessario specificare la configurazione dell&#39;indice prima di una distribuzione. I cambiamenti di configurazione nella produzione stanno chiaramente interrompendo i criteri CI/CD. Lo stesso vale per le modifiche dell&#39;indice in quanto può influire sulla stabilità e sulle prestazioni del sistema se non specificato testato e reindicizzato prima di introdurli nella produzione.

Di seguito è riportato un elenco delle modifiche principali rispetto a AEM 6.5 e versioni precedenti:

1. Gli utenti non avranno più accesso a Index Manager di una singola istanza AEM per eseguire il debug, configurare o mantenere l&#39;indicizzazione. Viene utilizzato solo per lo sviluppo locale e le distribuzioni on-premise.

1. Gli utenti non cambieranno gli indici su una singola istanza AEM né dovranno più preoccuparsi dei controlli di coerenza o della reindicizzazione.

1. In generale, le modifiche dell’indice vengono avviate prima di passare alla produzione per non aggirare i gateway di qualità nelle pipeline CI/CD di Cloud Manager e non influire sui KPI aziendali in produzione.

1. Tutte le metriche correlate, comprese le prestazioni di ricerca in produzione, saranno disponibili per i clienti in fase di runtime al fine di fornire una visione olistica sugli argomenti di ricerca e indicizzazione.

1. I clienti potranno impostare gli avvisi in base alle proprie esigenze.

1. Gli SRE monitorano lo stato di salute del sistema 24/7 e intraprenderanno le azioni necessarie e il più presto possibile.

1. La configurazione dell’indice viene modificata tramite le distribuzioni. Le modifiche alla definizione dell’indice sono configurate come altre modifiche al contenuto.

1. A un livello elevato su AEM come Cloud Service, con l&#39;introduzione del [modello di distribuzione Blue-Green](#index-management-using-blue-green-deployments) esisteranno due set di indici: un set per la versione precedente (blu) e uno per la nuova versione (verde).

1. I clienti possono vedere se il processo di indicizzazione è completo nella pagina di compilazione di Cloud Manager e riceveranno una notifica quando la nuova versione è pronta per il traffico.

1. Limitazioni: attualmente, la gestione degli indici su AEM come Cloud Service è supportata solo per gli indici di tipo lucene.

## Guida all’uso {#how-to-use}

La definizione degli indici può comprendere i tre casi d’uso seguenti:

1. Aggiunta di una nuova definizione dell&#39;indice del cliente
1. Aggiornamento di una definizione di indice esistente. Ciò significa effettivamente aggiungere una nuova versione di una definizione di indice esistente
1. Rimozione di un indice esistente ridondante o obsoleto.

Per entrambi i punti 1 e 2 di cui sopra, devi creare una nuova definizione dell’indice come parte della base di codice personalizzata nella rispettiva pianificazione della versione di Cloud Manager. Per ulteriori informazioni, consulta la sezione [Distribuzione di AEM come documentazione di Cloud Service](/help/implementing/deploying/overview.md).

### Preparazione della nuova definizione dell&#39;indice {#preparing-the-new-index-definition}

>[!NOTE]
>
>Se personalizzi un indice preconfigurato, ad esempio `damAssetLucene-6`, copia l&#39;ultima definizione dell&#39;indice preconfigurata da un *ambiente di Cloud Service* e aggiungi le tue personalizzazioni in alto, questo assicura che le configurazioni richieste non vengano rimosse inavvertitamente. Ad esempio, il nodo `tika` sotto `/oak:index/damAssetLucene-6/tika` è un nodo obbligatorio che deve far parte anche dell&#39;indice personalizzato e non esiste nell&#39;SDK di Cloud.

È necessario preparare un nuovo pacchetto di definizione dell&#39;indice che contiene la definizione effettiva dell&#39;indice, seguendo questo pattern di denominazione:

`<indexName>[-<productVersion>]-custom-<customVersion>`

che deve quindi andare sotto `ui.apps/src/main/content/jcr_root`. Le cartelle secondarie non sono supportate al momento.

Il pacchetto del campione di cui sopra è costruito come `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`.

>[!NOTE]
>
>Qualsiasi pacchetto di contenuto contenente le definizioni degli indici deve avere la seguente proprietà impostata nel file delle proprietà del pacchetto di contenuto, che si trova in `/META-INF/vault/properties.xml`:
>
>`noIntermediateSaves=true`

### Distribuzione delle definizioni degli indici {#deploying-index-definitions}

>[!NOTE]
>
>C&#39;è un problema noto con la versione del plug-in pacchetto Maven Jackrabbit Filevault **1.1.0** che non consente di aggiungere `oak:index` ai moduli di `<packageType>application</packageType>`. Per risolvere il problema, utilizza la versione **1.0.4**.

Le definizioni degli indici sono ora contrassegnate come personalizzate e con versione:

* La definizione stessa dell&#39;indice (ad esempio `/oak:index/ntBaseLucene-custom-1`)

Pertanto, per distribuire un indice, la definizione dell’indice (`/oak:index/definitionname`) deve essere fornita tramite `ui.apps` tramite Git e il processo di distribuzione di Cloud Manager.

Una volta aggiunta la nuova definizione dell’indice, la nuova applicazione deve essere distribuita tramite Cloud Manager. All’avvio della distribuzione vengono avviati due processi, responsabili dell’aggiunta (e dell’unione, se necessario) delle definizioni dell’indice a MongoDB e Azure Segment Store rispettivamente per l’authoring e la pubblicazione. Gli archivi sottostanti vengono reindicizzati con le nuove definizioni dell&#39;indice, prima che si verifichi lo switch Blue-Green.

>[!TIP]
>
>Per ulteriori dettagli sulla struttura del pacchetto richiesta per AEM come Cloud Service, vedere il documento [AEM Struttura del progetto.](/help/implementing/developing/introduction/aem-project-content-package-structure.md)

## Gestione dell&#39;indice utilizzando le implementazioni Blue-Green {#index-management-using-blue-green-deployments}

### Gestione dell&#39;indice {#what-is-index-management}

La gestione degli indici riguarda l’aggiunta, la rimozione e la modifica degli indici. Modificare la *definizione* di un indice è veloce, ma l&#39;applicazione della modifica (spesso denominata &quot;creazione di un indice&quot; o, per gli indici esistenti, &quot;reindicizzazione&quot;) richiede tempo. Non è istantaneo: l’archivio deve essere analizzato per individuare i dati da indicizzare.

### Implementazione Blue-Green {#what-is-blue-green-deployment}

L&#39;implementazione Blue-Green può ridurre i tempi di inattività. Consente inoltre di eseguire senza tempi di inattività gli aggiornamenti e offre rapidi rollback. La vecchia versione dell&#39;applicazione (blu) viene eseguita contemporaneamente alla nuova versione dell&#39;applicazione (verde).

### Aree di sola lettura e di lettura/scrittura {#read-only-and-read-write-areas}

Alcune aree dell’archivio (parti di sola lettura dell’archivio) possono essere diverse nella vecchia versione (blu) e nella nuova versione (verde) dell’applicazione. Le aree di sola lettura dell&#39;archivio sono in genere &quot;`/app`&quot; e &quot;`/libs`&quot;. Nell’esempio seguente, il corsivo viene utilizzato per contrassegnare le aree di sola lettura, mentre il grassetto viene utilizzato per le aree di lettura/scrittura.

* **/**
* */apps (sola lettura)*
* **/content**
* */libs (sola lettura)*
* **/oak:index**
* **/oak:index/acme.**
* **/jcr:system**
* **/system**
* **/var**

Le aree di lettura-scrittura dell&#39;archivio sono condivise tra tutte le versioni dell&#39;applicazione, mentre per ogni versione dell&#39;applicazione, esiste un set specifico di `/apps` e `/libs`.

### Gestione dell&#39;indice senza implementazione Blue-Green {#index-management-without-blue-green-deployment}

Durante lo sviluppo o quando si utilizzano installazioni locali, gli indici possono essere aggiunti, rimossi o modificati in fase di runtime. Gli indici vengono utilizzati non appena sono disponibili. Se un indice non deve ancora essere utilizzato nella vecchia versione dell&#39;applicazione, l&#39;indice viene generalmente generato durante un downtime pianificato. Lo stesso si verifica quando si rimuove un indice o si modifica un indice esistente. Quando si rimuove un indice, questo diventa non disponibile non appena viene rimosso.

### Gestione degli indici con implementazione Blue-Green {#index-management-with-blue-green-deployment}

Con le implementazioni blu-verde, non si verificano tempi di inattività. Tuttavia, per la gestione degli indici, ciò richiede che gli indici siano utilizzati solo da alcune versioni dell&#39;applicazione. Ad esempio, quando si aggiunge un indice nella versione 2 dell&#39;applicazione, non è ancora necessario utilizzarlo nella versione 1 dell&#39;applicazione. Il contrario si verifica quando un indice viene rimosso: un indice rimosso nella versione 2 è ancora necessario nella versione 1. Quando si modifica una definizione di indice, si desidera che la vecchia versione dell&#39;indice venga utilizzata solo per la versione 1 e che la nuova versione dell&#39;indice venga utilizzata solo per la versione 2.

La tabella seguente mostra cinque definizioni di indice: index `cqPageLucene` viene utilizzato in entrambe le versioni, mentre index `damAssetLucene-custom-1` è utilizzato solo nella versione 2.

>[!NOTE]
>
>`<indexName>-custom-<customerVersionNumber>` è necessario per AEM come Cloud Service per contrassegnare questo come sostitutivo di un indice esistente.

| Indice | Indice predefinito | Usa nella versione 1 | Usa nella versione 2 |
|---|---|---|---|
| /oak:index/damAssetLucene | Sì | Sì | No |
| /oak:index/damAssetLucene-custom-1 | Sì (personalizzato) | No | Sì |
| /oak:index/acme.product-custom-1 | No | Sì | No |
| /oak:index/acme.product-custom-2 | No | No | Sì |
| /oak:index/cqPageLucene | Sì | Sì | Sì |

Il numero di versione viene incrementato ogni volta che l’indice viene modificato. Per evitare che i nomi di indice personalizzati si scontrino con i nomi di indice del prodotto stesso, gli indici personalizzati e le modifiche agli indici predefiniti devono terminare con `-custom-<number>`.

### Modifiche agli indici predefiniti {#changes-to-out-of-the-box-indexes}

Una volta che l&#39;Adobe cambia un indice predefinito come &quot;damAssetLucene&quot; o &quot;cqPageLucene&quot;, viene creato un nuovo indice denominato `damAssetLucene-2` o `cqPageLucene-2` oppure, se l&#39;indice è già stato personalizzato, la definizione dell&#39;indice personalizzato viene unita con le modifiche nell&#39;indice predefinito, come mostrato di seguito. L&#39;unione delle modifiche avviene automaticamente. Ciò significa che non è necessario eseguire alcuna operazione se un indice predefinito cambia. Tuttavia, è possibile personalizzare di nuovo l&#39;indice in un secondo momento.

| Indice | Indice predefinito | Usa nella versione 2 | Usa nella versione 3 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | Sì (personalizzato) | Sì | No |
| /oak:index/damAssetLucene-2-custom-1 | Sì (unito automaticamente da damAssetLucene-custom-1 e damAssetLucene-2) | No | Sì |
| /oak:index/cqPageLucene | Sì | Sì | No |
| /oak:index/cqPageLucene-2 | Sì | No | Sì |

### Limitazioni correnti {#current-limitations}

La gestione degli indici è attualmente supportata solo per gli indici di tipo `lucene`.

### Aggiunta di un indice {#adding-an-index}

Per aggiungere un indice denominato `/oak:index/acme.product-custom-1` da utilizzare in una nuova versione dell&#39;applicazione e successivamente, l&#39;indice deve essere configurato come segue:

`acme.product-1-custom-1`

Questo funziona anteponendo un identificatore personalizzato al nome dell&#39;indice, seguito da un punto (**`.`**). La lunghezza dell&#39;identificatore deve essere compresa tra 2 e 5 caratteri.

Come sopra, questo assicura che l&#39;indice sia utilizzato solo dalla nuova versione dell&#39;applicazione.

### Modifica di un indice {#changing-an-index}

Quando viene modificato un indice esistente, è necessario aggiungere un nuovo indice con la modifica della definizione dell&#39;indice. Ad esempio, considera che l&#39;indice esistente `/oak:index/acme.product-custom-1` sia modificato. Il vecchio indice viene memorizzato in `/oak:index/acme.product-custom-1` e il nuovo indice viene memorizzato in `/oak:index/acme.product-custom-2`.

La vecchia versione dell&#39;applicazione utilizza la seguente configurazione:

`/oak:index/acme.product-custom-1`

La nuova versione dell’applicazione utilizza la seguente configurazione (modificata):

`/oak:index/acme.product-custom-2`

>[!NOTE]
>
>Le definizioni degli indici su AEM come Cloud Service potrebbero non corrispondere completamente alle definizioni degli indici su un&#39;istanza di sviluppo locale. L&#39;istanza di sviluppo non ha una configurazione Tika, mentre AEM come istanze di Cloud Service ne ha una. Se si personalizza un indice con una configurazione Tika, si prega di mantenere la configurazione Tika.

### Annullamento di una modifica {#undoing-a-change}

A volte, è necessario ripristinare una modifica nella definizione di un indice. Le ragioni potrebbero essere che un cambiamento è stato fatto per errore, o che non è più necessario un cambiamento. Ad esempio, la definizione dell&#39;indice `damAssetLucene-8-custom-3` è stata creata per errore ed è già distribuita. Per questo motivo, potrebbe essere utile ripristinare la precedente definizione dell&#39;indice `damAssetLucene-8-custom-2`. A questo scopo, devi aggiungere un nuovo indice denominato `damAssetLucene-8-custom-4` che contiene la definizione dell&#39;indice precedente, `damAssetLucene-8-custom-2`.

### Rimozione di un indice {#removing-an-index}

Il seguente si applica solo agli indici personalizzati. Gli indici di prodotto non possono essere rimossi in quanto sono utilizzati da AEM.

Se un indice deve essere rimosso in una versione successiva dell&#39;applicazione, è possibile definire un indice vuoto (un indice vuoto che non viene mai utilizzato e non contiene dati) con un nuovo nome. Ai fini di questo esempio, è possibile denominarlo `/oak:index/acme.product-custom-3`. Questo sostituisce l&#39;indice `/oak:index/acme.product-custom-2`. Una volta rimosso `/oak:index/acme.product-custom-2` dal sistema, è possibile rimuovere anche l&#39;indice vuoto `/oak:index/acme.product-custom-3`. Un esempio di tale indice vuoto è:

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

Se non è più necessario avere una personalizzazione di un indice predefinito, è necessario copiare la definizione di indice preconfigurata. Ad esempio, se hai già distribuito `damAssetLucene-8-custom-3` ma non hai più bisogno delle personalizzazioni e desideri tornare all&#39;indice predefinito `damAssetLucene-8` , devi aggiungere un indice `damAssetLucene-8-custom-4` che contenga la definizione dell&#39;indice di `damAssetLucene-8`.
