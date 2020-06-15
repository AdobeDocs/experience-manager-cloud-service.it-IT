---
title: Ricerca e indicizzazione dei contenuti
description: Ricerca e indicizzazione dei contenuti
translation-type: tm+mt
source-git-commit: 5594792b84bdb5a0c72bfb6d034ca162529e4ab2
workflow-type: tm+mt
source-wordcount: '1450'
ht-degree: 3%

---


# Ricerca e indicizzazione dei contenuti {#indexing}

## Modifiche in AEM come servizio cloud {#changes-in-aem-as-a-cloud-service}

Con AEM come servizio cloud, Adobe si sta spostando da un modello incentrato sulle istanze di AEM a una vista basata sui servizi con contenitori AEM n-x, guidati dalle pipeline CI/CD in Cloud Manager. Anziché configurare e mantenere indici su singole istanze di AEM, è necessario specificare la configurazione dell&#39;indice prima di procedere alla distribuzione. I cambiamenti di configurazione nella produzione stanno chiaramente infrangendo i criteri CI/CD. Lo stesso vale per le modifiche dell&#39;indice, in quanto può influire sulla stabilità e sulle prestazioni del sistema se non specificato testato e reindicizzato prima di portarli in produzione.

Di seguito è riportato un elenco delle modifiche principali rispetto a AEM 6.5 e versioni precedenti:

1. Gli utenti non avranno più accesso a Index Manager di una singola istanza di AEM per eseguire il debug, configurare o gestire l&#39;indicizzazione. Viene utilizzato solo per lo sviluppo locale e le distribuzioni on-prem.

1. Gli utenti non modificheranno gli indici su una singola istanza di AEM né dovranno più preoccuparsi dei controlli di coerenza o della reindicizzazione.

1. In generale, le modifiche dell&#39;indice sono iniziate prima dell&#39;avvio della produzione per non eludere i gateway di qualità nelle pipeline CI/CD di Cloud Manager e non incidere sugli indicatori KPI aziendali nella produzione.

1. Tutte le metriche correlate, comprese le prestazioni di ricerca in produzione, saranno disponibili per i clienti in fase di esecuzione al fine di fornire la visualizzazione olistica sugli argomenti di ricerca e indicizzazione.

1. I clienti potranno impostare gli avvisi in base alle loro esigenze.

1. Gli SRE stanno monitorando lo stato di salute del sistema 24 ore su 24, 7 giorni su 7 e adotteranno le misure necessarie e il più presto possibile.

1. La configurazione dell&#39;indice viene modificata tramite distribuzioni. Le modifiche alla definizione dell&#39;indice sono configurate come altre modifiche al contenuto.

1. Su AEM come servizio cloud, con l’introduzione del modello [di distribuzione](#index-management-using-blue-green-deployments) Blue-Green saranno disponibili due serie di indici: un set per la versione precedente (blu) e uno per la nuova versione (verde).

<!-- The version of the index that is used is configured using flags in the index definitions via the `useIfExist` flag. An index may be used in only one version of the application (for example only blue or only green), or in both versions. Detailed documentation is available at [Index Management using Blue-Green Deployments](#index-management-using-blue-green-deployments). -->

1. I clienti possono vedere se il processo di indicizzazione è completo nella pagina di build di Cloud Manager e riceveranno una notifica quando la nuova versione sarà pronta per il traffico.

1. Limitazioni: al momento, la gestione degli indici su AEM come servizio cloud è supportata solo per gli indici di tipo lucene.

<!-- ## Sizing Considerations {#sizing-considerations}

AEM as a Cloud Service comes with a default capacity model to provide sufficient performance for average web applications. This "average" measure relates to the repository size and even more relevant to the indexing size. If we have reasons to believe that we need extended capacity for a specific customer project, an evaluation with SREs and Engineering will take place to determine the required capacity settings.

AS NOTE: the above is internal for now.

-->

## Guida all’uso {#how-to-use}

La definizione degli indici può comprendere tre casi di utilizzo:

1. Aggiunta di una nuova definizione di indice cliente
1. Aggiornamento di una definizione di indice esistente. Ciò significa effettivamente aggiungere una nuova versione di una definizione di indice esistente
1. Rimozione di un indice esistente ridondante o obsoleto.

Per entrambi i punti 1 e 2 di cui sopra, devi creare una nuova definizione di indice come parte della tua base di codice personalizzata nella rispettiva pianificazione delle versioni di Cloud Manager. Per ulteriori informazioni, consulta [Distribuzione in AEM come documentazione](/help/implementing/deploying/overview.md)del servizio cloud.

### Preparazione della nuova definizione di indice {#preparing-the-new-index-definition}

È necessario preparare un nuovo pacchetto di definizione dell&#39;indice che contenga la definizione effettiva dell&#39;indice, seguendo questo pattern di denominazione:

`<indexName>[-<productVersion>]-custom-<customVersion>`

che poi deve andare sotto `ui.apps/src/main/content/jcr_root`. Le cartelle sub-root non sono supportate al momento.

<!-- need to review and link info on naming convention from https://wiki.corp.adobe.com/display/WEM/Merging+Customer+and+OOTB+Index+Changes?focusedCommentId=1784917629#comment-1784917629 -->

Il pacchetto del campione sopra riportato è costruito come `com.adobe.granite:new-index-content:zip:1.0.0-SNAPSHOT`.

### Distribuzione delle definizioni degli indici {#deploying-index-definitions}

>[!NOTE]
>
> C&#39;è un problema noto con Jackrabbit Filevault Maven Package Plugin versione **1.1.0** che non consente di aggiungere `oak:index` a moduli di `<packageType>application</packageType>`. Per risolvere il problema, utilizzate la versione **1.0.4**.

Le definizioni degli indici sono ora contrassegnate come personalizzate e con versione:

* La definizione di indice stessa (ad esempio `/oak:index/ntBaseLucene-custom-1`)

Pertanto, per distribuire un indice, la definizione (`/oak:index/definitionname`) dell&#39;indice deve essere distribuita tramite `ui.apps` Git e il processo di distribuzione di Cloud Manager.

Una volta aggiunta la nuova definizione di indice, la nuova applicazione deve essere distribuita tramite Cloud Manager. All&#39;avvio della distribuzione, vengono avviati due processi, responsabili dell&#39;aggiunta (e dell&#39;unione, se necessario) delle definizioni di indice a MongoDB e ad Azure Segment Store rispettivamente per l&#39;autore e la pubblicazione. I repository sottostanti vengono reindicizzati con le nuove definizioni di indice, prima che venga eseguito il passaggio Blu-Verde.

>[!TIP]
>
>Per ulteriori dettagli sulla struttura del pacchetto richiesta per AEM come servizio cloud, consultate il documento Struttura del progetto [AEM.](/help/implementing/developing/introduction/aem-project-content-package-structure.md)

## Gestione dell&#39;indice con le implementazioni Blue-Green {#index-management-using-blue-green-deployments}

### Che cos&#39;è la gestione dell&#39;indice {#what-is-index-management}

La gestione degli indici si occupa dell’aggiunta, della rimozione e della modifica degli indici. La modifica della *definizione* di un indice è rapida, ma l&#39;applicazione della modifica (spesso denominata &quot;creazione di un indice&quot; o, per gli indici esistenti, &quot;reindicizzazione&quot;) richiede tempo. Non è istantanea: per indicizzare i dati, è necessario eseguire la scansione del repository.

### Che cos&#39;è l&#39;implementazione blu-verde {#what-is-blue-green-deployment}

L&#39;implementazione Blue-Green può ridurre i tempi di inattività. Consente inoltre di azzerare i tempi di inattività e offre ripristini rapidi. La versione precedente dell’applicazione (blu) viene eseguita contemporaneamente alla nuova versione dell’applicazione (verde).

### Aree di sola lettura e di lettura/scrittura {#read-only-and-read-write-areas}

Alcune aree del repository (parti di sola lettura del repository) possono essere diverse nella vecchia versione (blu) e nella nuova versione (verde) dell&#39;applicazione. Le aree di sola lettura del repository sono in genere &quot;`/app`&quot; e &quot;`/libs`&quot;. Nell&#39;esempio seguente, il corsivo viene utilizzato per contrassegnare le aree di sola lettura, mentre il grassetto viene utilizzato per le aree di lettura/scrittura.

* **/**
* */apps (sola lettura)*
* **/content**
* */libs (sola lettura)*
* **/oak:index**
* **/oak:index/acme**
* **/jcr:system**
* **/system**
* **/var**

Le aree di lettura/scrittura dell&#39;archivio sono condivise tra tutte le versioni dell&#39;applicazione, mentre per ogni versione dell&#39;applicazione è presente un set specifico di `/apps` e `/libs`.

### Gestione degli indici senza implementazione blu-verde {#index-management-without-blue-green-deployment}

Durante lo sviluppo o quando si utilizzano installazioni locali, gli indici possono essere aggiunti, rimossi o modificati in fase di esecuzione. Gli indici vengono utilizzati non appena sono disponibili. Se un indice non deve ancora essere utilizzato nella vecchia versione dell&#39;applicazione, l&#39;indice viene generalmente generato durante un periodo di inattività pianificato. Lo stesso si verifica quando si rimuove un indice o si modifica un indice esistente. Quando si rimuove un indice, questo diventa non disponibile non appena viene rimosso.

### Gestione Dell&#39;Indice Con Implementazione Blu-Verde {#index-management-with-blue-green-deployment}

Con le installazioni blu-verde, non si verificano tempi di inattività. Tuttavia, per la gestione degli indici, ciò richiede che gli indici siano utilizzati solo da alcune versioni dell&#39;applicazione. Ad esempio, quando si aggiunge un indice nella versione 2 dell&#39;applicazione, non si desidera che venga ancora utilizzato dalla versione 1 dell&#39;applicazione. Il contrario si verifica quando un indice viene rimosso: un indice rimosso nella versione 2 è ancora necessario nella versione 1. Quando si modifica una definizione di indice, si desidera che la vecchia versione dell&#39;indice venga utilizzata solo per la versione 1 e che la nuova versione dell&#39;indice venga utilizzata solo per la versione 2.

Nella tabella seguente sono riportate 5 definizioni di indice: index `cqPageLucene` è utilizzato in entrambe le versioni, mentre index `damAssetLucene-custom-1` è utilizzato solo nella versione 2.

>[!NOTE]
>
> `<indexName>-custom-<customerVersionNumber>` è necessario che AEM come servizio cloud contrassegni questo tipo di sostituzione per un indice esistente.

| Indice | Indice out-of-the-box | Usa nella versione 1 | Usa nella versione 2 |
|---|---|---|---|
| /oak:index/damAssetLucene | Sì | Sì | No |
| /oak:index/damAssetLucene-custom-1 | Sì (personalizzato) | No | Sì |
| /oak:index/acmeProduct-custom-1 | No | Sì | No |
| /oak:index/acmeProduct-custom-2 | No | No | Sì |
| /oak:index/cqPageLucene | Sì | Sì | Sì |

Il numero di versione viene incrementato ogni volta che l&#39;indice viene modificato. Per evitare che i nomi di indice personalizzati si scontrino con i nomi di indice del prodotto stesso, è necessario terminare con gli indici personalizzati, così come apportare modifiche agli indici out-of-box `-custom-<number>`.

### Modifiche agli indici forniti {#changes-to-out-of-the-box-indexes}

Quando Adobe modifica un indice out-of-the-box come &quot;damAssetLucene&quot; o &quot;cqPageLucene&quot;, viene creato un nuovo indice denominato `damAssetLucene-2` o `cqPageLucene-2` oppure, se l&#39;indice è già stato personalizzato, la definizione dell&#39;indice personalizzata viene unita alle modifiche nell&#39;indice out-of-the-box, come mostrato di seguito. L&#39;unione delle modifiche avviene automaticamente. Ciò significa che non è necessario eseguire alcuna operazione in caso di modifica di un indice out-of-the-box. Tuttavia, è possibile personalizzare nuovamente l&#39;indice in un secondo momento.

| Indice | Indice out-of-the-box | Usa nella versione 2 | Usa nella versione 3 |
|---|---|---|---|
| /oak:index/damAssetLucene-custom-1 | Sì (personalizzato) | Sì | No |
| /oak:index/damAssetLucene-2-custom-1 | Sì (unito automaticamente da damAssetLucene-custom-1 e damAssetLucene-2) | No | Sì |
| /oak:index/cqPageLucene | Sì | Sì | No |
| /oak:index/cqPageLucene-2 | Sì | No | Sì |

### Limitazioni  {#limitations}

Al momento la gestione degli indici è supportata solo per gli indici di tipo `lucene`.

### Rimozione di un indice {#removing-an-index}

Se un indice deve essere rimosso in una versione successiva dell&#39;applicazione, è possibile definire un indice vuoto (un indice senza dati da indicizzare) con un nuovo nome. Ad esempio, potete denominarlo `/oak:index/acmeProduct-custom-3`. Questo sostituisce l&#39;indice `/oak:index/acmeProduct-custom-2`. Una volta `/oak:index/acmeProduct-custom-2` rimosso dal sistema, l&#39;indice vuoto `/oak:index/acmeProduct-custom-3` può essere rimosso.

### Aggiunta di un indice {#adding-an-index}

Per aggiungere un indice denominato &quot;/oak:index/acmeProduct-custom-1&quot; da utilizzare in una nuova versione dell’applicazione e successivamente, l’indice deve essere configurato come segue:

`/oak:index/acmeProduct-custom-1`

Come sopra, questo assicura che l&#39;indice sia utilizzato solo dalla nuova versione dell&#39;applicazione.

### Modifica di un indice {#changing-an-index}

Quando si modifica un indice esistente, è necessario aggiungere un nuovo indice con la nuova definizione di indice. Considerate ad esempio la modifica dell&#39;indice esistente &quot;/oak:index/acmeProduct-custom-1&quot;. Il vecchio indice è memorizzato in `/oak:index/acmeProduct-custom-1`e il nuovo indice è memorizzato in `/oak:index/acmeProduct-custom-2`.

La vecchia versione dell&#39;applicazione utilizza la seguente configurazione:

`/oak:index/acmeProduct-custom-1`

La nuova versione dell&#39;applicazione utilizza la seguente configurazione (modificata):

`/oak:index/acmeProduct-custom-2`