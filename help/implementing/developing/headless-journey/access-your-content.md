---
title: Come accedere ai contenuti tramite API di consegna AEM
description: In questa parte del Percorso di sviluppatori AEM Headless, scopri come utilizzare le query GraphQL per accedere al contenuto dei frammenti di contenuto.
hide: true
hidefromtoc: true
index: false
exl-id: 5ef557ff-e299-4910-bf8c-81c5154ea03f
translation-type: tm+mt
source-git-commit: 7b04ae2bfa75fe3d3af13271efe567a5fc401f49
workflow-type: tm+mt
source-wordcount: '4636'
ht-degree: 1%

---

# Come accedere ai contenuti tramite le API di consegna AEM {#access-your-content}

>[!CAUTION]
>
>LAVORO IN CORSO - La creazione di questo documento è in corso e non deve essere inteso come completo o definitivo né deve essere utilizzato a fini di produzione.

In questa parte del [AEM Percorso di sviluppatori headless,](overview.md) puoi imparare a utilizzare le query GraphQL per accedere al contenuto dei frammenti di contenuto.

## La storia finora {#story-so-far}

Nel documento precedente del percorso AEM headless [Come modellare il contenuto](model-your-content.md) hai appreso le nozioni di base sulla modellazione dei dati in AEM, quindi ora devi capire come modellare la struttura del contenuto, quindi realizzare tale struttura utilizzando AEM Modelli di frammento di contenuto e Frammenti di contenuto:

* Riconosci i concetti e la terminologia relativi alla modellazione dei dati [a1/>.](#data-modeling)
* Scopri [perché è necessaria la modellazione dei dati per la distribuzione di contenuti headless](#data-modeling-for-aem-headless).
* Scopri [come realizzare questa struttura utilizzando AEM Modelli per frammenti di contenuto](#create-structure-content-fragment-models) (e crea contenuti con [Frammenti di contenuto](#use-content-to-author-content)).
* Comprendere [come modellare il contenuto](#getting-started-examples); principi con campioni di base.

Questo articolo si basa su questi elementi fondamentali per comprendere come accedere al contenuto headless esistente in AEM utilizzando l’API GraphQL di AEM.

* **Pubblico**: Principiante
* **Obiettivo**: Scopri come accedere al contenuto dei frammenti di contenuto utilizzando AEM query GraphQL:
   * Introduce GraphQL e l&#39;API GraphQL AEM.
   * Approfondisci i dettagli dell’API GraphQL AEM.
   * Osserva alcune query di esempio per vedere come funzionano le cose nella pratica.

## Vuoi accedere ai tuoi dati? {#so-youd-like-to-access-your-data}

Quindi...hai tutto questo contenuto, ben strutturato (in Frammenti di contenuto) e in attesa di alimentare la tua nuova app. La domanda è: come arrivarci?

Ciò di cui hai bisogno è un modo per eseguire il targeting di contenuti specifici, seleziona ciò che ti serve e restituiscilo all’app per un’ulteriore elaborazione.

Con Adobe Experience Manager (AEM) come Cloud Service, puoi accedere in modo selettivo ai frammenti di contenuto, utilizzando l’API GraphQL di AEM, per restituire solo il contenuto necessario. Ciò significa che è possibile realizzare una distribuzione headless di contenuti strutturati da utilizzare nelle applicazioni.

>[!NOTE]
>
>AEM GraphQL API è un’implementazione personalizzata, basata su GraphQL standard.

## GraphQL - Introduzione {#graphql-introduction}

GraphQL è una specifica open source che fornisce:

* linguaggio di query che consente di selezionare contenuto specifico da oggetti strutturati.
* un runtime per eseguire queste query con il contenuto strutturato.

GraphQL è un&#39;API tipizzata *fortemente*. Questo significa che il contenuto *tutto* deve essere chiaramente strutturato e organizzato per tipo, in modo che GraphQL *comprenda* cosa accedere e come. I campi dati sono definiti all’interno degli schemi GraphQL, che definiscono la struttura degli oggetti contenuto.

Gli endpoint GraphQL forniscono quindi i percorsi che rispondono alle query GraphQL.

Questo significa che l&#39;app può selezionare in modo preciso, affidabile ed efficiente i dati di cui ha bisogno, esattamente ciò di cui hai bisogno quando viene utilizzata con AEM.

>[!NOTE]
>
>Consulta *GraphQL*.org e *GraphQL*.com.

## AEM e GraphQL {#aem-graphql}

GraphQL viene utilizzato in varie posizioni in AEM; ad esempio:

* Commerce
   * Sono disponibili integrazioni GraphQL tra AEM e diverse soluzioni commerce di terze parti, utilizzate con gli hook di estensione forniti dai componenti core CIF.
* Frammenti di contenuto
   * Per questo caso d’uso è stata sviluppata un’API personalizzata.
   * Questa è l&#39;API GraphQL AEM.

>[!NOTE]
>
>Questo passaggio del Percorso Headless riguarda solo l’API GraphQL AEM e i frammenti di contenuto.

## AEM API GraphQL {#aem-graphql-api}

L’API GraphQL di AEM è una versione personalizzata dell’API GraphQL standard, appositamente configurata per consentire l’esecuzione di query (complesse) sui frammenti di contenuto.

I frammenti di contenuto vengono utilizzati, in quanto il contenuto è strutturato in base ai modelli di frammenti di contenuto . Questo soddisfa un requisito fondamentale di GraphQL.

* Un modello di frammento di contenuto è costituito da uno o più campi.
   * Ogni campo è definito in base a un tipo di dati.
* I modelli per frammenti di contenuto vengono utilizzati per generare gli schemi AEM GraphQL corrispondenti.

Per accedere effettivamente a GraphQL per AEM (e il contenuto) viene utilizzato un endpoint per fornire il percorso di accesso.

Il contenuto restituito, tramite l’API GraphQL di AEM, può quindi essere utilizzato dalle tue applicazioni.

>[!NOTE]
>
>L’implementazione AEM dell’API GraphQL si basa sulle librerie Java GraphQL.

### Casi d’uso per ambienti di authoring e pubblicazione {#use-cases-author-publish-environments}

I casi d’uso per l’API GraphQL AEM possono dipendere dal tipo di AEM come ambiente di Cloud Service:

* ambiente di pubblicazione; utilizzato per:
   * Dati query per l’applicazione JS (caso d’uso standard)

* Ambiente di authoring; utilizzato per:
   * Dati query per &quot;scopo di gestione del contenuto&quot;:
      * GraphQL in AEM as a Cloud Service è attualmente un&#39;API di sola lettura.
      * L’API REST può essere utilizzata per le operazioni CR(u)D.

## Frammenti di contenuto da utilizzare con AEM API GraphQL {#content-fragments-use-with-aem-graphql-api}

I frammenti di contenuto possono essere utilizzati come base per GraphQL per AEM schemi e query come:

* Consentono di progettare, creare, curare e pubblicare contenuti indipendenti dalla pagina.
* Si basano su un modello per frammenti di contenuto, che predefinisce la struttura per il frammento risultante per mezzo di tipi di dati definiti.
* È possibile ottenere livelli aggiuntivi di struttura con il tipo di dati Riferimento frammento, disponibile quando si definisce un modello.

### Modelli per frammenti di contenuto {#content-fragments-models}

Questi Modelli Di Frammento Di Contenuto:

* Vengono utilizzati per generare gli schemi una volta **Abilitato**.

* Fornisci i tipi di dati e i campi richiesti per GraphQL. Assicurano che la tua applicazione richieda solo ciò che è possibile e riceva ciò che è previsto.

* Il tipo di dati **Riferimenti frammento** può essere utilizzato nel modello per fare riferimento a un altro frammento di contenuto e quindi introdurre livelli aggiuntivi di struttura.

### Riferimenti a frammento {#fragment-references}

Il **Riferimento al frammento**:

* È di particolare interesse in combinazione con GraphQL.

* È un tipo di dati specifico che può essere utilizzato durante la definizione di un modello di frammento di contenuto.

* Fa riferimento a un altro frammento, a seconda di un modello di frammento di contenuto specifico.

* Consente di recuperare dati strutturati.

   * Quando è definito come **multifeed**, è possibile fare riferimento a più frammenti secondari (recuperati) dal frammento principale.

### Anteprima JSON {#json-preview}

Per facilitare la progettazione e lo sviluppo di modelli di frammenti di contenuto, puoi visualizzare in anteprima l’output JSON nell’Editor frammento di contenuto.

## Generazione dello schema GraphQL da frammenti di contenuto {#graphql-schema-generation-content-fragments}

GraphQL è un’API fortemente tipizzata, il che significa che i dati devono essere chiaramente strutturati e organizzati per tipo. La specifica GraphQL fornisce una serie di linee guida su come creare una solida API per l&#39;interrogazione dei dati su una determinata istanza. A questo scopo, un client deve recuperare lo schema, che contiene tutti i tipi necessari per una query.

Per i frammenti di contenuto, gli schemi GraphQL (struttura e tipi) si basano su **Modelli di frammento di contenuto abilitati** e i relativi tipi di dati.

>[!CAUTION]
>
>Tutti gli schemi GraphQL (derivati dai modelli di frammenti di contenuto che sono stati **abilitati**) sono leggibili tramite l’endpoint GraphQL.
>
>Ciò significa che devi assicurarti che non siano disponibili dati sensibili, in quanto potrebbero essere trapelati in questo modo; ad esempio, include informazioni che potrebbero essere presenti come nomi di campo nella definizione del modello.

Ad esempio, se un utente ha creato un modello per frammenti di contenuto denominato `Article`, AEM genera l’oggetto `article` di tipo `ArticleModel`. I campi all’interno di questo tipo corrispondono ai campi e ai tipi di dati definiti nel modello.

1. Un Modello Di Frammento Di Contenuto:

   ![Modello per frammento di contenuto da utilizzare con ](assets/graphqlapi-cfmodel.png "GraphQLContent Fragment Model per l’utilizzo con GraphQL")

1. Lo schema GraphQL corrispondente (output dalla documentazione automatica GraphiQL):
   ![Schema GraphQL basato su schema ](assets/graphqlapi-cfm-schema.png "ModelGraphQL per frammenti di contenuto basato su modello di frammento di contenuto")

   Questo indica che il tipo generato `ArticleModel` contiene diversi [campi](#fields).

   * Tre di essi sono stati controllati dall’utente: `author`, `main` e `referencearticle`.

   * Gli altri campi sono stati aggiunti automaticamente da AEM e rappresentano metodi utili per fornire informazioni su un determinato frammento di contenuto; in questo esempio, `_path`, `_metadata`, `_variations`. Questi [campi helper](#helper-fields) sono contrassegnati con un `_` precedente per distinguere tra ciò che è stato definito dall&#39;utente e ciò che è stato generato automaticamente.

1. Dopo che un utente crea un frammento di contenuto basato sul modello di articolo, può essere interrogato tramite GraphQL. Ad esempio, consulta l’articolo sulle query di esempio .md#graphql-sample-query) (basate su una struttura di frammento di contenuto di esempio da utilizzare con GraphQL.

In GraphQL per AEM, lo schema è flessibile. Ciò significa che viene generato automaticamente ogni volta che viene creato, aggiornato o eliminato un modello di frammento di contenuto. Le cache dello schema dati vengono aggiornate anche quando si aggiorna un modello di frammento di contenuto.

Il servizio GraphQL di Sites ascolta (in background) le modifiche apportate a un modello di frammento di contenuto. Quando vengono rilevati aggiornamenti, viene rigenerata solo la parte dello schema. Questa ottimizzazione consente di risparmiare tempo e di garantire stabilità.

Ad esempio, se:

1. Installa un pacchetto contenente `Content-Fragment-Model-1` e `Content-Fragment-Model-2`:

   1. Verranno generati i tipi GraphQL per `Model-1` e `Model-2`.

1. Quindi modifica `Content-Fragment-Model-2`:

   1. Verrà aggiornato solo il tipo `Model-2` GraphQL.

   1. `Model-1` rimarrà invariato.

>[!NOTE]
>
>Questo è importante da notare nel caso in cui desideri eseguire aggiornamenti in blocco sui modelli di frammenti di contenuto tramite l’api REST o in altro modo.

Lo schema viene gestito attraverso lo stesso endpoint delle query GraphQL, con il client che gestisce il fatto che lo schema viene chiamato con l&#39;estensione `GQLschema`. Ad esempio, l’esecuzione di una semplice richiesta `GET` su `/content/cq:graphql/global/endpoint.GQLschema` darà luogo all’output dello schema con il tipo di contenuto: `text/x-graphql-schema;charset=iso-8859-1`.

### Generazione schema - Modelli non pubblicati {#schema-generation-unpublished-models}

Quando i frammenti di contenuto sono nidificati, può accadere che un modello di frammento di contenuto principale venga pubblicato, ma non lo è un modello di riferimento.

>[!NOTE]
>
>L’interfaccia utente AEM impedisce che ciò accada, ma se la pubblicazione viene effettuata a livello di programmazione o con pacchetti di contenuto può verificarsi.

In questo caso, AEM genera uno schema *incompleto* per il modello di frammento di contenuto principale. Ciò significa che il Riferimento frammento, che dipende dal modello non pubblicato, viene rimosso dallo schema.

## AEM Endpoint GraphQL {#aem-graphql-endpoints}

<!--
need details/examples
-->

Un endpoint è il percorso utilizzato per accedere a GraphQL per AEM. Utilizzando questo percorso (o la tua app) puoi:

* accedere agli schemi GraphQL,
* invia le query GraphQL,
* ricevere le risposte (alle query GraphQL).

AEM consente:

* Endpoint globale disponibile per tutti i siti.
* Endpoint tenant - che è possibile configurare, specifici per un sito o un progetto specifico.

## Autorizzazioni  {#permissions}

Le autorizzazioni sono quelle necessarie per accedere ad Assets.

## Interfaccia GraphiQL AEM {#aem-graphiql-interface}

Per facilitare l’input diretto e il test delle query, è disponibile per l’utilizzo con AEM GraphQL un’implementazione dell’interfaccia standard GraphiQL . Questo può essere installato con AEM.

Offre funzioni quali evidenziazione della sintassi, completamento automatico, suggerimento automatico, nonché una cronologia e una documentazione online.

![Interfaccia ](assets/graphiql-interface.png "GraphiQL")

<!--
new page?
-->

## Utilizzo dell&#39;API GraphQL AEM {#using-aem-graphiql}

### Endpoint {#endpoints}

Il percorso dell&#39;archivio di GraphQL per AEM endpoint globale è:

`/content/cq:graphql/global/endpoint`

Per cui l’app può utilizzare il seguente percorso nell’URL della richiesta:

`/content/_cq_graphql/global/endpoint.json`

Per un endpoint tenant i percorsi sono paragonabili:

`/content/cq:graphql/your-tenant/endpoint`
`/content/_cq_graphql/your-tenant/endpoint.json`

Prima dell’utilizzo, tutti gli endpoint devono essere abilitati. Per abilitare un endpoint, globale o tenant, per GraphQL per AEM è necessario:

* Abilita l&#39;endpoint GraphQL
* Pubblicare l&#39;endpoint

>[!CAUTION]
>
>L’editor dei frammenti di contenuto può consentire a un frammento di contenuto di un tenant di fare riferimento a un frammento di contenuto di un altro tenant (tramite criteri).
>
>In tal caso, non tutto il contenuto sarà recuperabile utilizzando un endpoint specifico per il tenant.
>
>L’autore del contenuto deve controllare questo scenario; ad esempio, potrebbe essere utile considerare l’inserimento di modelli di frammenti di contenuto condivisi nel tenant globale.

### Abilitazione dell&#39;endpoint GraphQL {#enabling-graphql-endpoint}

Per abilitare un endpoint GraphQL è innanzitutto necessario disporre di una configurazione appropriata nel browser di configurazione.

>[!CAUTION]
>
>Se l’uso dei modelli di frammento di contenuto non è stato abilitato, l’opzione **Crea** non sarà disponibile.

Per abilitare l&#39;endpoint corrispondente:

1. Passa a **Strumenti**, **Siti**, quindi seleziona **GraphQL**.
1. Seleziona **Crea**.
1. Viene aperta la finestra di dialogo **Crea nuovo endpoint GraphQL** . Qui puoi specificare:
   * **Nome**: nome del punto finale; puoi immettere qualsiasi testo.
   * **Utilizza lo schema GraphQL fornito da**: utilizza il menu a discesa per selezionare il sito o il progetto richiesto.

   >[!NOTE]
   >
   >Nella finestra di dialogo viene visualizzato il seguente avviso:
   >
   >* *Se non vengono gestiti correttamente, gli endpoint GraphQL possono introdurre problemi di prestazioni e sicurezza dei dati. Dopo aver creato un endpoint, assicurati di impostare le autorizzazioni appropriate.*


1. Conferma con **Crea**.
1. La finestra di dialogo **Passaggi successivi** fornirà un collegamento diretto alla console Sicurezza per garantire che l’endpoint appena creato disponga delle autorizzazioni appropriate.

   >[!CAUTION]
   >
   >L’endpoint è accessibile a tutti. Questo può creare problemi di sicurezza, soprattutto per le istanze di pubblicazione, in quanto le query GraphQL possono imporre un carico pesante sul server.
   >
   >Puoi impostare ACL, appropriati al tuo caso d&#39;uso, sull&#39;endpoint.

### Pubblicazione dell&#39;endpoint GraphQL {#publishing-graphql-endpoint}

Seleziona il nuovo endpoint e **Pubblica** per renderlo completamente disponibile in tutti gli ambienti.

>[!CAUTION]
>
>L’endpoint è accessibile a tutti.
>
>Nelle istanze di pubblicazione questo può rappresentare un problema di sicurezza, in quanto le query GraphQL possono imporre un carico pesante sul server.
>
>Devi impostare ACL appropriati al tuo caso d&#39;uso sull&#39;endpoint.

### Installazione dell&#39;interfaccia AEM GraphiQL {#installing-graphiql-interface}

L&#39;interfaccia utente GraphiQL può essere installata su AEM con un pacchetto dedicato: il pacchetto [GraphiQL Content Package v0.0.6 (2021.3)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-graphql/graphiql-0.0.6.zip).

### Schemi AEM GraphQL {#aem-graphql-schemas}

Per accedere ai dati devi innanzitutto selezionare il tipo di modello per frammento di contenuto richiesto, rappresentato da uno schema GraphQL. AEM gli schemi GraphQL sono derivati dai modelli di frammenti di contenuto, per l’utilizzo nelle query GraphQL.

<!--
Confirm is the schema city or CityModel? -->

Se disponi di un modello di frammento di contenuto denominato `City`, sarà disponibile uno schema corrispondente denominato `city`. Puoi utilizzare la seguente query per elencare la `name` di tutti i frammenti di contenuto basati su questo modello.

```xml
query {
  cityList {
    items {
      name
    }
  }
}
```

Puoi utilizzare la seguente query per elencare i valori `name` e `description` di tutti i valori `types` per tutti gli schemi disponibili:

```xml
{
  __schema {
    types {
      name
      description
    }
  }
}
```

### AEM Campi GraphQL {#aem-graphql-fields}

Dopo aver selezionato lo schema necessario, potrai accedere a dati specifici rappresentati dai campi nello schema.

Nello schema sono presenti singoli campi, di due categorie di base:

* Campi generati.

   Una selezione di [Tipi di campo](#field-types) viene utilizzata per creare campi in base alla modalità di configurazione del modello di frammento di contenuto. I nomi dei campi sono ricavati dal campo **Nome proprietà** del **Tipo di dati**.

   * È inoltre disponibile la proprietà **Rendering come** da considerare, in quanto gli utenti possono configurare determinati tipi di dati; ad esempio, come testo a riga singola o come campo multiplo.

* GraphQL per AEM genera anche una serie di campi di supporto.

   Vengono utilizzati per identificare un frammento di contenuto o per ottenere ulteriori informazioni su un frammento di contenuto.

### Tipi di campi {#field-types}

GraphQL per AEM supporta un elenco di tipi. Sono rappresentati tutti i tipi di dati dei modelli di frammento di contenuto supportati e i corrispondenti tipi GraphQL:

| Modello per frammento di contenuto - Tipo di dati | Tipo GraphQL | Descrizione |
|--- |--- |--- |
| Testo a riga singola | Stringa, [Stringa] | Utilizzato per stringhe semplici come nomi di autore, nomi di posizione, ecc. |
| Testo a più righe | Stringa | Utilizzato per l’output di testo, ad esempio il corpo di un articolo |
| Numero | Mobile, [Mobile] | Utilizzato per visualizzare il numero a virgola mobile e i numeri regolari |
| Booleano | Booleano | Utilizzato per visualizzare le caselle di controllo → semplici istruzioni true/false |
| Data E Ora | Calendario | Utilizzato per visualizzare data e ora in formato ISO 8086. A seconda del tipo selezionato, sono disponibili tre aromi da utilizzare in AEM GraphQL: `onlyDate`, `onlyTime`, `dateTime` |
| Enumerazione | Stringa | Utilizzato per visualizzare un&#39;opzione da un elenco di opzioni definite durante la creazione del modello |
| Tag | [Stringa] | Utilizzato per visualizzare un elenco di stringhe che rappresentano tag utilizzati in AEM |
| Riferimento contenuto | Stringa | Utilizzato per visualizzare il percorso verso un’altra risorsa in AEM |
| Riferimento frammento | *Un tipo di modello* | Utilizzato per fare riferimento a un altro frammento di contenuto di un determinato tipo di modello, definito al momento della creazione del modello |

### Campi helper {#helper-fields}

Oltre ai tipi di dati per i campi generati dall’utente, GraphQL per AEM genera anche una serie di campi *helper* per facilitare l’identificazione di un frammento di contenuto o per fornire informazioni aggiuntive su un frammento di contenuto.

#### Percorso {#path}

Il campo percorso viene utilizzato come identificatore in GraphQL. Rappresenta il percorso della risorsa Frammento di contenuto all’interno dell’archivio AEM. Questo è l’identificatore di un frammento di contenuto, in quanto:

* è univoco all&#39;interno di AEM,
* può essere facilmente recuperato.

Il codice seguente visualizza i percorsi di tutti i frammenti di contenuto creati in base al modello di frammento di contenuto `Person`.

```xml
{
  personList {
    items {
      _path
    }
  }
}
```

Per recuperare un singolo frammento di contenuto di un tipo specifico, è necessario anche determinarne prima il percorso. ad esempio:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      firstName
      name
    }
  }
}
```

>[!NOTE]
>
>Vedere Query Di Esempio - Un Singolo Frammento Di Città Specifico.

#### Metadati {#metadata}

Tramite GraphQL, AEM espone anche i metadati di un frammento di contenuto. I metadati sono informazioni che descrivono un frammento di contenuto, ad esempio il titolo di un frammento di contenuto, il percorso delle miniature, la descrizione di un frammento di contenuto, la data di creazione, tra gli altri.

Poiché i metadati vengono generati tramite l’Editor di schema e in quanto tali non dispongono di una struttura specifica, il tipo `TypedMetaData` GraphQL è stato implementato per esporre i metadati di un frammento di contenuto. `TypedMetaData` espone le informazioni raggruppate per i seguenti tipi scalari:

| Campo |
|--- |
| `stringMetadata:[StringMetadata]!` |
| `stringArrayMetadata:[StringArrayMetadata]!` |
| `intMetadata:[IntMetadata]!` |
| `intArrayMetadata:[IntArrayMetadata]!` |
| `floatMetadata:[FloatMetadata]!` |
| `floatArrayMetadata:[FloatArrayMetadata]!` |
| `booleanMetadata:[BooleanMetadata]!` |
| `booleanArrayMetadata:[booleanArrayMetadata]!` |
| `calendarMetadata:[CalendarMetadata]!` |
| `calendarArrayMetadata:[CalendarArrayMetadata]!` |

Ogni tipo scalare rappresenta una coppia nome-valore singola o una matrice di coppie nome-valore, in cui il valore di tale coppia è del tipo in cui è stato raggruppato.

Ad esempio, se desideri recuperare il titolo di un frammento di contenuto, questa proprietà è una proprietà String , quindi eseguiamo una query per tutti i metadati stringa:

Per eseguire una query per i metadati:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      _metadata {
        stringMetadata {
          name
          value
        }
      }
    }
  }
}
```

Puoi visualizzare tutti i tipi di metadati GraphQL se visualizzi lo schema GraphQL generato. Tutti i tipi di modello hanno lo stesso `TypedMetaData`.

>[!NOTE]
>
>**Differenza tra i metadati normali e quelli dell&#39;array**
>Tieni presente che `StringMetadata` e `StringArrayMetadata` si riferiscono entrambi a ciò che è memorizzato nell’archivio e non a come lo recuperi.
>
>Ad esempio, chiamando il campo `stringMetadata` riceverai un array di tutti i metadati memorizzati nell&#39;archivio come `String` , e se richiami `stringArrayMetadata` riceverai un array di tutti i metadati memorizzati nell&#39;archivio come `String[]`.

>[!NOTE]
>
>Vedi Esempio di query per metadati - Elenco dei metadati per i premi denominati GB.

#### Varianti {#variations}

Il campo `_variations` è stato implementato per semplificare la query delle varianti di un frammento di contenuto. Esempio:

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

>[!NOTE]
>
>Consulta Query di esempio - Tutte le città con una variante denominata .

### AEM variabili GraphQL {#aem-graphql-variables}

Le variabili sono utili in qualsiasi tipo di programmazione o query, in quanto consentono di memorizzare valori diversi in un’unica posizione. Per AEM GraphQL questo significa che invece di dover scrivere una query separata per ogni valore, puoi scrivere la query per una variabile e il valore di questa variabile può cambiare come necessario.

GraphQL consente di inserire le variabili nella query.

>[!NOTE]
>
>Per ulteriori informazioni, consulta la documentazione GraphQL per le variabili .

Ad esempio, per ottenere tutti i frammenti di contenuto di tipo `Article` con una variante specifica, puoi specificare la variabile `variation` in GraphiQL. Tutte le istanze verranno recuperate in `GetArticlesByVariation`, quindi trasmesse per utilizzate in `articleList`.

![Variabili GraphQL ](assets/graphqlapi-variables.png "VariablesGraphQL")

```xml
### query
query GetArticlesByVariation($variation: String!) {
    articleList(variation: $variation) {
        items {
            _path
            author
        }
    }
}
 
### in query variables
{
    "variation": "uk"
}
```

### Direttive AEM GraphQL {#aem-graphql-directives}

In GraphQL è possibile modificare la query in base alle variabili, denominate Direttive GraphQL.

Ad esempio, è possibile includere il campo `adventurePrice` in una query per tutti i valori `AdventureModels`, in base a una variabile `includePrice`.

!![GraphQL Directives](assets/graphqlapi-sections.png &quot;GraphQL Guidelines&quot;)

```xml
### query
query GetAdventureByType($includePrice: Boolean!) {
  adventureList {
    items {
      adventureTitle
      adventurePrice @include(if: $includePrice)
    }
  }
}
 
### in query variables
{
    "includePrice": true
}
```

### Filtri GraphQL AEM {#aem-graphql-filters}

È inoltre possibile utilizzare il filtro nelle query GraphQL per restituire dati specifici.

Il filtro utilizza una sintassi basata su operatori logici ed espressioni.

Ad esempio, la seguente query (di base) filtra tutte le persone con un nome `Jobs` o `Smith`:

```xml
query {
  personList(filter: {
    name: {
      _logOp: OR
      _expressions: [
        {
          value: "Jobs"
        },
        {
          value: "Smith"
        }
      ]
    }
  }) {
    items {
      name
      firstName
    }
  }
}
```

Per ulteriori esempi, consulta:

* dettagli di GraphQL per le estensioni AEM

* Query di esempio con contenuto e struttura di esempio

### Estensioni AEM GraphQL {#aem-graphql-extensions}

Il funzionamento di base delle query con GraphQL per AEM rispettare la specifica GraphQL standard. Per le query GraphQL con AEM sono disponibili alcune estensioni:

* Se hai bisogno di un singolo risultato:
   * utilizzare il nome del modello; città

* Se si prevede un elenco di risultati:
   * aggiungere `List` al nome del modello; ad esempio, `cityList`
   * Consulta [Query di esempio - Tutte le informazioni su Tutte le città](#sample-all-information-all-cities)

* Se desideri utilizzare un operatore OR logico:
   * use ` _logOp: OR`
   * Vedere [Query di esempio - Tutte le persone con un nome &quot;Jobs&quot; o &quot;Smith&quot;](#sample-all-persons-jobs-smith)

* Esiste anche l&#39;AND logico, ma è (spesso) implicito

* È possibile eseguire query sui nomi di campo corrispondenti ai campi all’interno del modello di frammento di contenuto
   * Consulta [Query di esempio - Dettagli completi sull&#39;amministratore delegato e sui dipendenti di un&#39;azienda](#sample-full-details-company-ceos-employees)

* Oltre ai campi del modello, sono presenti alcuni campi generati dal sistema (preceduti dal carattere di sottolineatura):

   * Per il contenuto:

      * `_locale` : rivelare la lingua; basato su Language Manager
         * Consulta [Query di esempio per più frammenti di contenuto di una determinata impostazione internazionale](#sample-wknd-multiple-fragments-given-locale)
      * `_metadata` : per visualizzare i metadati del frammento
         * Consulta [Esempio di query per metadati - Elenco dei metadati per i premi denominati GB](#sample-metadata-awards-gb)
      * `_model` : consentire la query per un modello di frammento di contenuto (percorso e titolo)
         * Consulta [Query di esempio per un modello di frammento di contenuto da un modello](#sample-wknd-content-fragment-model-from-model)
      * `_path` : percorso del frammento di contenuto all’interno dell’archivio
         * Vedere [Query di esempio - Un singolo frammento di città specifico](#sample-single-specific-city-fragment)
      * `_reference` : rivelare riferimenti; inclusione di riferimenti in linea nell’Editor Rich Text
         * Consulta [Query di esempio per più frammenti di contenuto con riferimenti prerecuperati](#sample-wknd-multiple-fragments-prefetched-references)
      * `_variation` : per visualizzare varianti specifiche all’interno del frammento di contenuto
         * Consulta [Query di esempio - Tutte le città con una variante denominata](#sample-cities-named-variation)
   * e operazioni:

      * `_operator` : applicare operatori specifici;  `EQUALS`,  `EQUALS_NOT`,  `GREATER_EQUAL`,  `LOWER`,  `CONTAINS`,  `STARTS_WITH`
         * Vedere [Query di esempio - Tutte le persone che non hanno un nome di &quot;Jobs&quot;](#sample-all-persons-not-jobs)
         * Consulta [Query di esempio - Tutte le avventure in cui il `_path` inizia con un prefisso specifico](#sample-wknd-all-adventures-cycling-path-filter)
      * `_apply` : applicare condizioni specifiche; ad esempio,   `AT_LEAST_ONCE`
         * Vedere [Query di esempio - Filtro su una matrice con un elemento che deve verificarsi almeno una volta](#sample-array-item-occur-at-least-once)
      * `_ignoreCase` : per ignorare il caso durante la query
         * Vedere [Query di esempio - Tutte le città con SAN nel nome, indipendentemente dal caso](#sample-all-cities-san-ignore-case)









* I tipi di unione GraphQL sono supportati:

   * utilizza `... on`
      * Consulta [Query di esempio per un frammento di contenuto di un modello specifico con un riferimento di contenuto](#sample-wknd-fragment-specific-model-content-reference)

### Query persistenti (memorizzazione in cache) {#persisted-queries-caching}

Dopo aver preparato una query con una richiesta POST, può essere eseguita con una richiesta GET memorizzabile nella cache tramite cache HTTP o CDN.

Questo è necessario in quanto le query POST di solito non vengono memorizzate nella cache e se si utilizza GET con la query come parametro esiste un rischio significativo che il parametro diventi troppo grande per i servizi HTTP e gli intermediari.

Le query persistenti devono sempre utilizzare l’endpoint correlato alla configurazione appropriata (tenant); in modo che possano utilizzare una delle due opzioni, oppure entrambe:

* Configurazione globale ed endpoint
La query ha accesso a tutti i modelli di frammento di contenuto.
* Configurazioni e endpoint specifici del tenant
La creazione di una query persistente per una configurazione tenant specifica richiede un endpoint specifico per il tenant corrispondente (per fornire l’accesso ai relativi modelli di frammento di contenuto).
Ad esempio, per creare una query persistente specifica per il tenant WKND, è necessario creare in anticipo una configurazione tenant specifica per WKND corrispondente e un endpoint specifico per WKND.

>[!NOTE]
>
>Per ulteriori informazioni, consulta Abilita funzionalità frammento di contenuto nel browser di configurazione .
>
>È necessario abilitare le **query di persistenza GraphQL** per la configurazione tenant appropriata.

Ad esempio, se è presente una particolare query denominata `my-query` che utilizza un modello `my-model` dalla configurazione del tenant `my-conf`:

* Puoi creare una query utilizzando l’endpoint specifico `my-conf`, quindi la query verrà salvata come segue:
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* Puoi creare la stessa query utilizzando l’endpoint `global`, ma la query verrà salvata come segue:
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>Queste sono due query diverse - salvate in percorsi diversi.
>
>Usano lo stesso modello, ma attraverso endpoint diversi.

Di seguito sono riportati i passaggi necessari per mantenere una determinata query:

1. Prepara la query inserendola nel nuovo URL dell&#39;endpoint `/graphql/persist.json/<config>/<persisted-label>`.

   Ad esempio, crea una query persistente:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
       }
     }
   }'
   ```

1. A questo punto, controlla la risposta.

   Ad esempio, controlla il successo:

   ```xml
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. È quindi possibile riprodurre nuovamente la query persistente utilizzando GETing l&#39;URL `/graphql/execute.json/<shortPath>`.

   Ad esempio, utilizza la query persistente:

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. Aggiornare una query persistente tramite POSTing a un percorso di query già esistente.

   Ad esempio, utilizza la query persistente:

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
         referencearticle {
           _path
         }
       }
     }
   }'
   ```

1. Crea una query normale con wrapping.

   Esempio:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. Crea una query normale con wrapping con il controllo della cache.

   Esempio:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. Crea una query persistente con parametri:

   Esempio:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-parameters" \
       -d \
   'query GetAsGraphqlModelTestByPath($apath: String!, $withReference: Boolean = true) {
     articleByPath(_path: $apath) {
       item {
         _path
           author
           main {
           plaintext
           }
           referencearticle @include(if: $withReference) {
           _path
           }
         }
       }
     }'
   ```

1. Esecuzione di una query con parametri.

   Esempio:

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   
   $ curl -X GET \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   ```

1. Per eseguire la query al momento della pubblicazione, la struttura ad albero persistente correlata deve essere replicata

   * Utilizzo di un POST per la replica:

      ```xml
      $curl -X POST   http://localhost:4502/bin/replicate.json \
        -H 'authorization: Basic YWRtaW46YWRtaW4=' \
        -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
        -F cmd=activate
      ```

   * Utilizzando un pacchetto:
      1. Crea una nuova definizione di pacchetto.
      1. Includi la configurazione (ad esempio, `/conf/wknd/settings/graphql/persistentQueries`).
      1. Crea il pacchetto.
      1. Replicare il pacchetto.
   * Utilizzo dello strumento di replica/distribuzione.
      1. Passa allo strumento Distribuzione .
      1. Seleziona l’attivazione ad albero per la configurazione (ad esempio, `/conf/wknd/settings/graphql/persistentQueries`).
   * Utilizzo di un flusso di lavoro (tramite la configurazione del modulo di avvio del flusso di lavoro):
      1. Definisci una regola di avvio del flusso di lavoro per l’esecuzione di un modello di flusso di lavoro che replichi la configurazione su eventi diversi (ad esempio, crea, modifica, tra gli altri).



1. Quando la configurazione della query è attiva per la pubblicazione, si applicano gli stessi principi, utilizzando solo l’endpoint di pubblicazione.

   >[!NOTE]
   >
   >Per l&#39;accesso anonimo il sistema presuppone che l&#39;ACL consenta a &quot;tutti&quot; di avere accesso alla configurazione della query.
   >
   >In caso contrario, non potrà essere eseguito.

   >[!NOTE]
   >
   >Eventuali punti e virgola (&quot;;&quot;) negli URL devono essere codificati.
   >
   >Ad esempio, come nella richiesta di eseguire una query persistente:
   >
   >
   ```xml
   >curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   >```

### Query dell’endpoint GraphQL da un sito Web esterno {#query-graphql-endpoint-from-external-website}

Per accedere all’endpoint GraphQL da un sito Web esterno è necessario configurare i seguenti elementi:

* Filtro CORS
* Filtro di riferimento

#### Filtro CORS {#cors-filter}

>[!NOTE]
>
>Per una panoramica dettagliata dei criteri di condivisione delle risorse CORS in AEM vedere Comprendere la condivisione delle risorse tra le origini (Cross-Origin Resource Sharing, CORS).

Per accedere all’endpoint GraphQL, è necessario configurare un criterio CORS nell’archivio Git del cliente. Questo viene fatto aggiungendo un file di configurazione OSGi CORS appropriato per gli endpoint desiderati.

Questa configurazione deve specificare un&#39;origine del sito web attendibile `alloworigin` o `alloworiginregexp` per la quale è necessario concedere l&#39;accesso.

Ad esempio, per concedere l’accesso all’endpoint GraphQL e all’endpoint di query persistenti per `https://my.domain` puoi utilizzare:

```xml
{
  "supportscredentials":true,
  "supportedmethods":[
    "GET",
    "HEAD",
    "POST"
  ],
  "exposedheaders":[
    ""
  ],
  "alloworigin":[
    "https://my.domain"
  ],
  "maxage:Integer":1800,
  "alloworiginregexp":[
    ""
  ],
  "supportedheaders":[
    "Origin",
    "Accept",
    "X-Requested-With",
    "Content-Type",
    "Access-Control-Request-Method",
    "Access-Control-Request-Headers"
  ],
  "allowedpaths":[
    "/content/_cq_graphql/global/endpoint.json",
    "/graphql/execute.json/.*"
  ]
}
```

Se hai configurato un percorso personalizzato per l’endpoint, puoi utilizzarlo anche in `allowedpaths`.

#### Filtro referente {#referrer-filter}

Oltre alla configurazione CORS, è necessario configurare un filtro Referrer per consentire l’accesso da host di terze parti.

A questo scopo, aggiungi un file di configurazione OSGi Referrer Filter appropriato che:

* specifica un nome host del sito web fidato; `allow.hosts` o `allow.hosts.regexp`,
* concede l&#39;accesso per questo nome host.

Ad esempio, per concedere l’accesso alle richieste con il referente `my.domain` puoi:

```xml
{
    "allow.empty":false,
    "allow.hosts":[
      "my.domain"
    ],
    "allow.hosts.regexp":[
      ""
    ],
    "filter.methods":[
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp":[
      ""
    ]
}
```

>[!CAUTION]
>
>Spetta al cliente:
>
>* concedere solo l&#39;accesso ai domini trusted
>* assicurati che non siano esposte informazioni sensibili
>* non utilizzare una sintassi jolly [*]; entrambi disattiveranno l’accesso autenticato all’endpoint GraphQL e lo esporranno a tutto il mondo.


>[!CAUTION]
>
>Tutti gli schemi GraphQL (derivati dai modelli di frammenti di contenuto che sono stati **abilitati**) sono leggibili tramite l’endpoint GraphQL.
>
>Ciò significa che devi assicurarti che non siano disponibili dati sensibili, in quanto potrebbero essere trapelati in questo modo; ad esempio, include informazioni che potrebbero essere presenti come nomi di campo nella definizione del modello.

### Autenticazione AEM GraphQL {#aem-graphql-authentication}

Un caso d’uso principale per l’API GraphQL di Adobe Experience Manager as a Cloud Service (AEM) per la distribuzione dei frammenti di contenuto è quello di accettare query remote da applicazioni o servizi di terze parti. Queste query remote possono richiedere l’accesso alle API autenticate per garantire la distribuzione di contenuti headless.

>[!NOTE]
>
>Per i test e lo sviluppo è inoltre possibile accedere all’API GraphQL AEM direttamente tramite l’interfaccia di interfaccia GraphiQL .

Per l’autenticazione, il servizio di terze parti deve utilizzare un token di accesso, che può quindi essere utilizzato nella richiesta GraphQL.

#### Recupero di un token di accesso {#retrieving-access-token}

Per informazioni dettagliate, consulta Generazione di token di accesso per API lato server .

#### Utilizzo del token di accesso in una richiesta GraphQL {#use-access-token-in-graphql-request}

Affinché un servizio di terze parti possa connettersi a un&#39;istanza AEM, deve disporre di un *token di accesso*. Il servizio deve quindi aggiungere questo token all’intestazione `Authorization` nella richiesta di POST.

Ad esempio, un’intestazione di autorizzazione GraphQL:

```xml
Authorization: Bearer <access_token>
```

#### Requisiti delle autorizzazioni {#permission-requirements}

Tutte le richieste effettuate utilizzando il token di accesso saranno in realtà effettuate *dall&#39;account utente che ha generato il token*.

Ciò significa che devi verificare che l’account disponga delle autorizzazioni necessarie per eseguire le query GraphQL.

Puoi controllare questo usando GraphiQL sull&#39;istanza locale.

## Esempi di query GraphQL AEM {#samples-aem-graphql-queries}

Consulta Imparare a utilizzare GraphQL con AEM - Contenuto di esempio e query per una gamma completa di query di esempio.

<!--
## Code Samples for AEM GraphQL Queries {#code-samples-aem-graphql-queries}
-->

## Novità {#whats-next}

Ora che hai imparato ad accedere ai contenuti headless e ad eseguire query tramite l’API GraphQL di AEM, ora [scopri come utilizzare l’API REST per accedere e aggiornare il contenuto dei frammenti di contenuto](/help/implementing/developing/headless-journey/update-your-content.md).

## Risorse aggiuntive {#additional-resources}

* [GraphQL.org](https://graphql.org)
   * [Schemi](https://graphql.org/learn/schema/)
   * [Variabili](https://graphql.org/learn/queries/#variables)
   * [Librerie Java GraphQL](https://graphql.org/code/#java)
* [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)
* [Struttura dei frammenti di contenuto di esempio](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)
* [Imparare a utilizzare GraphQL con AEM - Contenuto di esempio e query](/help/assets/content-fragments/content-fragments-graphql-samples.md)
   * [Query Di Esempio - Un Singolo Frammento Di Città Specifico](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)
   * [Esempio di query per metadati - Elenco dei metadati per i riconoscimenti denominati GB](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb)
   * [Query di esempio - Tutte le città con una variante denominata](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation)
* [Abilitare la funzionalità dei frammenti di contenuto nel browser di configurazione](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)
* [Utilizzo di frammenti di contenuto](/help/assets/content-fragments/content-fragments.md)
   * [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md)
   * [Output JSON](/help/assets/content-fragments/content-fragments-json-preview.md)
* [Comprendere la condivisione delle risorse tra le origini (CORS, Cross-Origin Resource Sharing)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=en#understand-cross-origin-resource-sharing-(cors))
* [Generazione dei token di accesso per le API lato server](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)
* [Guida introduttiva a AEM headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)  - Una breve serie di esercitazioni video che offre una panoramica dell’utilizzo AEM funzioni headless, tra cui la modellazione dei dati e GraphQL.
