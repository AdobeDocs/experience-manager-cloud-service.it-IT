---
title: Query GraphQL persistenti
description: Scopri come rendere persistenti le query GraphQL in Adobe Experience Manager as a Cloud Service per ottimizzare le prestazioni. Le query persistenti possono essere richieste dalle applicazioni client tramite il metodo HTTP GET e la risposta può essere memorizzata nella cache ai livelli dispatcher e CDN, migliorando in definitiva le prestazioni delle applicazioni client.
feature: Content Fragments,GraphQL API
exl-id: 080c0838-8504-47a9-a2a2-d12eadfea4c0
source-git-commit: 0cac51564468c414866d29c8f0be82f77625eaeb
workflow-type: tm+mt
source-wordcount: '1541'
ht-degree: 73%

---

# Query GraphQL persistenti {#persisted-queries-caching}

Le query persistenti sono query GraphQL create e memorizzate sul server di Adobe Experience Manager (AEM) as a Cloud Service. Possono essere richiamate tramite una richiesta GET da parte delle applicazioni client. La risposta di una richiesta GET può essere memorizzata nella cache ai livelli dispatcher e CDN, migliorando in definitiva le prestazioni dell’applicazione client richiedente. In questo sono diverse dalle query GraphQL standard, che vengono eseguite utilizzando richieste POST in cui la risposta non può essere facilmente memorizzata nella cache.

>[!NOTE]
>
>Si consiglia di effettuare query persistenti. Consulta [Tecniche consigliate per le query GraphQL (Dispatcher)](/help/headless/graphql-api/content-fragments.md#graphql-query-best-practices) per informazioni dettagliate e la relativa configurazione di Dispatcher.

La [IDE GraphiQL](/help/headless/graphql-api/graphiql-ide.md) è disponibile in AEM per sviluppare, testare e mantenere le query GraphQL, prima del [trasferimento all’ambiente di produzione](#transfer-persisted-query-production). Per i casi che richiedono personalizzazione (ad esempio, quando [personalizzazione della cache](/help/headless/graphql-api/graphiql-ide.md#caching-persisted-queries)) puoi utilizzare l’API; vedi l’esempio cURL fornito in [Come persistere una query GraphQL](#how-to-persist-query).

## Query ed endpoint persistenti {#persisted-queries-and-endpoints}

Le query persistenti devono sempre utilizzare l’endpoint correlato alla [configurazione Sites adeguata](graphql-endpoint.md) in modo che possano utilizzare una delle due opzioni seguenti, oppure entrambe:

* Configurazione globale ed endpoint
La query ha accesso a tutti i modelli per frammenti di contenuto.
* Configurazione/i di Sites ed endpoint specifici 
La creazione di una query persistente per una configurazione di Sites specifica richiede un endpoint specifico per la configurazione di Sites corrispondente (in modo da fornire accesso ai relativi modelli per frammenti di contenuto).
Ad esempio, per creare una query persistente per la configurazione di Sites WKND, è necessario aver già creato una configurazione di Sites specifica per WKND corrispondente e un endpoint specifico per WKND.

>[!NOTE]
>
>Per ulteriori dettagli, vedi [Abilitare la funzionalità Frammenti di contenuto nel browser configurazioni](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser).
>
>Per la configurazione di Sites appropriata, è necessario abilitare **query GraphQL persistenti**.

Ad esempio, se vi è una particolare query denominata `my-query`, che utilizza un modello `my-model` della configurazione Sites `my-conf`:

* Puoi creare una query utilizzando l’endpoint `my-conf` specifico. La query viene salvata come segue:
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* Puoi creare la stessa query utilizzando l’endpoint `global`, ma in questo caso la query viene salvata come segue:
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>Si tratta di due query diverse, salvate in percorsi diversi.
>
>Utilizzano lo stesso modello, ma tramite endpoint diversi.

## Rendere persistente una query GraphQL {#how-to-persist-query}

Si consiglia di creare le query persistenti in un ambiente di authoring AEM per poi [trasferire la query](#transfer-persisted-query-production) nell’ambiente di pubblicazione AEM di produzione, per l’utilizzo da parte delle applicazioni.

Esistono diversi metodi per le query persistenti, tra cui:

* IDE GraphiQL: vedi [Salvataggio delle query persistenti](/help/headless/graphql-api/graphiql-ide.md#saving-persisted-queries) (metodo preferito)
* cURL - vedi l&#39;esempio seguente
* Altri strumenti, tra cui [Postman](https://www.postman.com/)

L’IDE GraphiQL è il metodo **preferito** per le query persistenti. Per persistere una determinata query utilizzando **cURL** strumento della riga di comando:

1. Prepara la query inserendola mediante il metodo PUT nel nuovo URL dell’endpoint `/graphql/persist.json/<config>/<persisted-label>`.

   Ad esempio, crea una query persistente:

   ```shell
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

1. A questo punto, verifica la risposta.

   Ad esempio, verifica se l’operazione è riuscita:

   ```json
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. Puoi quindi richiedere la query persistente utilizzando il metodo GET per l’URL `/graphql/execute.json/<shortPath>`.

   Ad esempio, utilizza la query persistente:

   ```shell
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. Per aggiorna una query persistente, utilizza il metodo POST per un percorso di query già esistente.

   Ad esempio, utilizza la query persistente:

   ```shell
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

1. Crea una query normale racchiusa.

   Esempio:

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. Crea una query normale racchiusa con il controllo della cache.

   Esempio:

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. Crea una query persistente con parametri:

   Esempio:

   ```shell
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


## Come eseguire una query persistente {#execute-persisted-query}

Per eseguire una query persistente, un’applicazione client invia una richiesta GET utilizzando la seguente sintassi:

```
GET <AEM_HOST>/graphql/execute.json/<PERSISTENT_PATH>
```

dove `PERSISTENT_PATH` è un percorso abbreviato in cui viene salvata la query persistente.

1. Ad esempio `wknd` è il nome della configurazione e `plain-article-query` è il nome della query persistente. Per eseguire la query:

   ```shell
   $ curl -X GET \
       https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/plain-article-query
   ```

1. Esegui una query con parametri.

   >[!NOTE]
   >
   > Le variabili e i valori della query devono essere correttamente [codificati](#encoding-query-url) durante l’esecuzione di una query persistente.

   Esempio:

   ```xml
   $ curl -X GET \
       "https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/plain-article-query-parameters%3Bapath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fmagazine%2Falaska-adventure%2Falaskan-adventures%3BwithReference%3Dfalse
   ```

   Per ulteriori dettagli, consulta la sezione sulle [variabili di query](#query-variables).

## Utilizzo delle variabili di query {#query-variables}

Le variabili di query possono essere utilizzate con le query persistenti. Le variabili di query aggiunte alla richiesta devono essere precedute da un punto e virgola (`;`) e devono utilizzare il nome e il valore della variabile. Se si utilizzano più variabili, queste devono essere separate da un punto e virgola.

Il pattern si presenta come segue:

```
<AEM_HOST>/graphql/execute.json/<PERSISTENT_QUERY_PATH>;variable1=value1;variable2=value2
```

Ad esempio, la seguente query contiene una variabile `activity` per filtrare un elenco in base a un valore di attività:

```graphql
query getAdventuresByActivity($activity: String!) {
      adventureList (filter: {
        adventureActivity: {
          _expressions: [
            {
              value: $activity
            }
          ]
        }
      }){
        items {
          _path
        adventureTitle
        adventurePrice
        adventureTripLength
      }
    }
  }
```

Questa query può essere resa persistente in un percorso `wknd/adventures-by-activity`. Per chiamare la query persistente dove `activity=Camping`, la richiesta sarà simile alla seguente:

```
<AEM_HOST>/graphql/execute.json/wknd/adventures-by-activity%3Bactivity%3DCamping
```

Tieni presente che `%3B` è la codifica UTF-8 per `;` e `%3D` è la codifica per `=`. Affinché la query persistente possa essere eseguita, le variabili della query ed eventuali caratteri speciali devono essere [codificati correttamente](#encoding-query-url).

## Memorizzazione in cache delle query persistenti {#caching-persisted-queries}

Le query persistenti sono consigliate in quanto possono essere memorizzate nella cache [Dispatcher](/help/headless/deployment/dispatcher.md) e i livelli CDN (Content Delivery Network), migliorando in ultima analisi le prestazioni dell’applicazione client richiedente.

Per impostazione predefinita, AEM la cache viene annullata in base alla definizione TTL (Time To Live). Questi TTL possono essere definiti dai seguenti parametri. Questi parametri sono accessibili con vari mezzi, con variazioni dei nomi in base al meccanismo utilizzato:

| Tipo di cache | [Intestazione HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control)  | cURL  | Configurazione OSGi  | Cloud Manager |
|--- |--- |--- |--- |--- |
| Browser | `max-age` | `cache-control : max-age` | `cacheControlMaxAge` | `graphqlCacheControl` |
| CDN | `s-maxage` | `surrogate-control : max-age` | `surrogateControlMaxAge` | `graphqlSurrogateControl` | 60 |
| CDN | `stale-while-revalidate` | `surrogate-control : stale-while-revalidate ` | `surrogateControlStaleWhileRevalidate` | `graphqlStaleWhileRevalidate` |
| CDN | `stale-if-error` | `surrogate-control : stale-if-error` | `surrogateControlStaleIfError` | `graphqlStaleIfError` |

{style="table-layout:auto"}

### Istanze di authoring {#author-instances}

Per le istanze dell’autore, i valori predefiniti sono:

* `max-age`  : 60
* `s-maxage` : 60
* `stale-while-revalidate` : 86400
* `stale-if-error` : 86400

Questi:

* non può essere sovrascritto:
   * con una configurazione OSGi
* può essere sovrascritto:
   * da una richiesta che definisce le impostazioni dell’intestazione HTTP utilizzando cURL; deve includere impostazioni adeguate per `cache-control` e/o `surrogate-control`; per esempi, consulta [Gestione della cache a livello di query persistente](#cache-persisted-query-level)
   * se specifichi i valori nella **Intestazioni** dialogo [IDE GraphiQL](#http-cache-headers-graphiql-ide)

### Pubblicare istanze {#publish-instances}

Per le istanze di pubblicazione i valori predefiniti sono:

* `max-age`  : 60
* `s-maxage` : 7200
* `stale-while-revalidate` : 86400
* `stale-if-error` : 86400

Questi possono essere sovrascritti:

* [da GraphQL IDE](#http-cache-headers-graphiql-ide)

* [a livello di query persistente](#cache-persisted-query-level); questo comporta la pubblicazione della query per AEM utilizzando cURL nell’interfaccia della riga di comando e la pubblicazione della query persistente.

* [con variabili di Cloud Manager](#cache-cloud-manager-variables)

* [con una configurazione OSGi](#cache-osgi-configration)

### Gestione delle intestazioni della cache HTTP nell’IDE GraphiQL {#http-cache-headers-graphiql-ide}

GraphiQL IDE: vedi [Salvataggio delle query persistenti](/help/headless/graphql-api/graphiql-ide.md#managing-cache)

### Gestione della cache a livello di query persistente {#cache-persisted-query-level}

Ciò comporta la pubblicazione della query per AEM l’utilizzo di cURL nell’interfaccia della riga di comando.

Per un esempio del metodo PUT (create):

```bash
curl -u admin:admin -X PUT \
--url "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
--header "Content-Type: application/json" \
--data '{ "query": "{articleList { items { _path author } } }", "cache-control": { "max-age": 300 }, "surrogate-control": {"max-age":600, "stale-while-revalidate":1000, "stale-if-error":1000} }'
```

Per un esempio del metodo POST (update):

```bash
curl -u admin:admin -X POST \
--url "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
--header "Content-Type: application/json" \
--data '{ "query": "{articleList { items { _path author } } }", "cache-control": { "max-age": 300 }, "surrogate-control": {"max-age":600, "stale-while-revalidate":1000, "stale-if-error":1000} }'
```

`cache-control` può essere impostato al momento della creazione (PUT) o successivamente (ad esempio, tramite una richiesta POST). Il controllo cache è facoltativo quando si crea la query persistente, in quanto AEM può fornire il valore predefinito. Vedi [Come persistere una query GraphQL](#how-to-persist-query), per un esempio di persistenza di una query utilizzando cURL.

### Gestione della cache con le variabili di Cloud Manager {#cache-cloud-manager-variables}

[Variabili dell’ambiente di Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) può essere definito con Cloud Manager per definire i valori richiesti:

| Nome | Valore | Servizio applicato | Tipo |
|--- |--- |--- |--- |
| `graphqlStaleIfError` | 86400 | *se del caso* | *se del caso* |
| `graphqlSurrogateControl` | 600 | *se del caso* | *se del caso* |

{style="table-layout:auto"}

### Gestione della cache con una configurazione OSGi {#cache-osgi-configration}

Per gestire la cache a livello globale, puoi [configurare le impostazioni OSGi](/help/implementing/deploying/configuring-osgi.md) per **Configurazione del servizio query permanente**.

>[!NOTE]
>
>La configurazione OSGi è appropriata solo per le istanze di pubblicazione. La configurazione esiste sulle istanze dell’autore, ma viene ignorata.

Configurazione OSGi predefinita per le istanze di pubblicazione:

* legge le variabili di Cloud Manager se disponibili:

   | Proprietà di configurazione OSGi | legge questo | Variabile Cloud Manager |
   |--- |--- |--- |
   | `cacheControlMaxAge` | letture | `graphqlCacheControl` |
   | `surrogateControlMaxAge` | letture | `graphqlSurrogateControl` |
   | `surrogateControlStaleWhileRevalidate` | letture | `graphqlStaleWhileRevalidate` |
   | `surrogateControlStaleIfError` | letture | `graphqlStaleIfError` |

   {style="table-layout:auto"}

* e, se non disponibile, la configurazione OSGi utilizza il [valori predefiniti per le istanze di pubblicazione](#publish-instances).

## Codifica dell’URL della query per l’utilizzo da parte di un’app {#encoding-query-url}

Per poter essere utilizzati da un’applicazione, eventuali caratteri speciali utilizzati per creare variabili di query (come punto e virgola (`;`), segno di uguale (`=`), barra `/`) deve essere convertito nella codifica UTF-8 corrispondente.

Esempio:

```xml
curl -X GET \ "https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/adventure-by-path%3BadventurePath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fadventures%2Fbali-surf-camp%2Fbali-surf-camp"
```

L’URL può essere suddiviso nelle seguenti parti:

| Parte URL | Descrizione |
|----------| -------------|
| `/graphql/execute.json` | Endpoint di query persistente |
| `/wknd/adventure-by-path` | Percorso query persistente |
| `%3B` | Codice per `;` |
| `adventurePath` | Variabile query |
| `%3D` | Codice per `=` |
| `%2F` | Codice per `/` |
| `%2Fcontent%2Fdam...` | Percorso codificato del frammento di contenuto |

Come testo normale, l’URI della richiesta si presenta così:

```plaintext
/graphql/execute.json/wknd/adventure-by-path;adventurePath=/content/dam/wknd/en/adventures/bali-surf-camp/bali-surf-camp
```

Per utilizzare una query persistente in un’app client, è necessario utilizzare l’SDK client AEM headless per [JavaScript](https://github.com/adobe/aem-headless-client-js), [Java](https://github.com/adobe/aem-headless-client-java) oppure [NodeJS](https://github.com/adobe/aem-headless-client-nodejs). L’SDK client headless codificherà automaticamente tutte le variabili di query in modo appropriato nella richiesta.

## Trasferimento di una query persistente all’ambiente di produzione  {#transfer-persisted-query-production}

Le query persistenti devono sempre essere create su un servizio AEM Author e quindi pubblicate (replicate) in un servizio AEM Publish. Spesso, le query persistenti vengono create e testate in ambienti inferiori, come ambienti locali o di sviluppo. È quindi necessario promuovere le query persistenti in ambienti di livello superiore, rendendole infine disponibili in un ambiente AEM Publish di produzione affinché possano essere utilizzate da parte delle applicazioni client.

### Query persistenti nei pacchetti

È possibile integrare le query persistenti in [pacchetti AEM](/help/implementing/developing/tools/package-manager.md). I pacchetti AEM possono quindi essere scaricati e installati in ambienti diversi. I pacchetti AEM possono essere replicati anche da un ambiente AEM Author ad ambienti AEM Publish.

Per creare un pacchetto:

1. Passa a **Strumenti** > **Implementazione** > **Pacchetti**.
1. Per creare un nuovo pacchetto, tocca **Crea pacchetto**. Viene visualizzata una finestra di dialogo per la definizione del pacchetto.
1. Nella finestra di dialogo Definizione pacchetto, nella sezione **Generale** inserisci un **Nome**, ad esempio “wknd-persistent-queries”.
1. Immetti un numero di versione, ad esempio a “1.0”.
1. Nella sezione **Filtri**, aggiungi un nuovo **Filtro**. Utilizza Trova percorso per selezionare la cartella `persistentQueries` sotto la configurazione. Ad esempio, per la configurazione `wknd` il percorso completo sarà `/conf/wknd/settings/graphql/persistentQueries`.
1. Tocca **Salva** per salvare la definizione del nuovo pacchetto e chiudere la finestra di dialogo.
1. Tocca **Genera** nella definizione del pacchetto appena creata.

Dopo aver generato il pacchetto puoi:

* **Scaricare** il pacchetto e ricaricalo in un altro ambiente.
* **Replicare** il pacchetto toccando **Altro** > **Replica**. Il pacchetto verrà replicato nell’ambiente AEM Publish collegato.

<!--
1. Using replication/distribution tool:
   1. Go to the Distribution tool.
   1. Select tree activation for the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).

* Using a workflow (via workflow launcher configuration):
  1. Define a workflow launcher rule for executing a workflow model that would replicate the configuration on different events (for example, create, modify, amongst others).
-->
