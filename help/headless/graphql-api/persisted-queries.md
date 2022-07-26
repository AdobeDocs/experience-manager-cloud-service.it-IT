---
title: Query GraphQL persistenti
description: Scopri come rendere persistenti le query GraphQL in Adobe Experience Manager as a Cloud Service per ottimizzare le prestazioni. Le query persistenti possono essere richieste dalle applicazioni client tramite il metodo HTTP GET e la risposta può essere memorizzata nella cache ai livelli dispatcher e CDN, migliorando in definitiva le prestazioni delle applicazioni client.
feature: Content Fragments,GraphQL API
exl-id: 080c0838-8504-47a9-a2a2-d12eadfea4c0
source-git-commit: 9bfb5bc4b340439fcc34e97f4e87d711805c0d82
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 47%

---

# Query GraphQL persistenti {#persisted-queries-caching}

Le query persistenti sono query GraphQL create e memorizzate sul server di Adobe Experience Manager (AEM) as a Cloud Service. Possono essere richiamate tramite una richiesta GET da parte delle applicazioni client. La risposta di una richiesta GET può essere memorizzata nella cache ai livelli dispatcher e CDN, migliorando in definitiva le prestazioni dell’applicazione client richiedente. In questo sono diverse dalle query GraphQL standard, che vengono eseguite utilizzando richieste POST in cui la risposta non può essere facilmente memorizzata nella cache.

>[!NOTE]
>
>Si consiglia di effettuare query persistenti. Vedi [Tecniche consigliate per le query GraphQL (Dispatcher)](/help/headless/graphql-api/content-fragments.md#graphql-query-best-practices) per informazioni dettagliate e la relativa configurazione di Dispatcher.

La [IDE GraphiQL](/help/headless/graphql-api/graphiql-ide.md) è disponibile in AEM per sviluppare, testare e mantenere le query GraphQL, prima di [trasferimento all&#39;ambiente di produzione](#transfer-persisted-query-production). Per i casi che richiedono personalizzazione (come la [personalizzazione della cache](/help/headless/graphql-api/graphiql-ide.md#caching-persisted-queries)) puoi utilizzare l’API; vedi l’esempio curl fornito in [Persistenza di una query GraphQL](#how-to-persist-query).

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
>La **Query persistenti GraphQL** deve essere abilitato per la configurazione Sites appropriata.

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

* IDE GraphiQL - vedi [Salvataggio delle query persistenti](/help/headless/graphql-api/graphiql-ide.md#saving-persisted-queries) (metodo preferito)
* curl: vedi l’esempio seguente
* Altri strumenti, tra cui [Postman](https://www.postman.com/)

L&#39;IDE GraphiQL è il **preferito** metodo per query persistenti. Per persistere una determinata query utilizzando **arricciare** strumento della riga di comando:

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

Per eseguire una query persistente, un&#39;applicazione client invia una richiesta GET utilizzando la seguente sintassi:

```
GET <AEM_HOST>/graphql/execute.json/<PERSISTENT_PATH>
```

Dove `PERSISTENT_PATH` è un percorso abbreviato in cui viene salvata la query persistente.

1. Esempio `wknd` è il nome della configurazione e `plain-article-query` è il nome della query persistente. Per eseguire la query:

   ```shell
   $ curl -X GET \
       https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/plain-article-query
   ```

1. Esegui una query con parametri.

   >[!NOTE]
   >
   > Le variabili e i valori della query devono essere correttamente [codificato](#encoding-query-url) durante l&#39;esecuzione di una query persistente.

   Esempio:

   ```xml
   $ curl -X GET \
       "https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/plain-article-query-parameters%3Bapath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fmagazine%2Falaska-adventure%2Falaskan-adventures%3BwithReference%3Dfalse
   ```

   Consulta la sezione [variabili di query](#query-variables) per ulteriori dettagli.

## Utilizzo delle variabili di query {#query-variables}

Le variabili di query possono essere utilizzate con le query persistenti. Le variabili della query vengono aggiunte alla richiesta con un punto e virgola (`;`) utilizzando il nome e il valore della variabile. Le variabili multiple sono separate da punto e virgola.

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

Questa query può essere persistente in un percorso `wknd/adventures-by-activity`. Per chiamare la query persistente dove `activity=Camping` la richiesta sarà simile alla seguente:

```
<AEM_HOST>/graphql/execute.json/wknd/adventures-by-activity%3Bactivity%3DCamping
```

Tieni presente che `%3B` è la codifica UTF-8 per `;` e `%3D` è la codifica per `=`. Le variabili della query e gli eventuali caratteri speciali devono essere [codificato correttamente](#encoding-query-url) per eseguire la query persistente.

## Memorizzazione in cache delle query persistenti {#caching-persisted-queries}

Le query persistenti sono consigliate in quanto possono essere memorizzate nella cache dei livelli dispatcher e CDN, migliorando in ultima analisi le prestazioni dell’applicazione client richiedente.

Per impostazione predefinita, AEM la cache CDN (Content Delivery Network) in base a un valore predefinito Time To Live (TTL).

Questo valore è impostato su:

* 7200 secondi, TTL predefinito per Dispatcher e CDN; noto anche come *cache condivise*
   * impostazione predefinita: s-maxage=7200
* 60, TTL predefinito per il client (ad esempio, un browser)
   * impostazione predefinita: maxage=60

Se desideri modificare il TTL per la query GraphLQ, la query deve essere:

* persistente dopo la gestione del [Intestazioni HTTP Cache - dall’IDE GraphQL](#http-cache-headers)
* persistente utilizzando [Metodo API](#cache-api).

### Gestione delle intestazioni della cache HTTP in GraphQL  {#http-cache-headers-graphql}

IDE GraphiQL - vedi [Salvataggio delle query persistenti](/help/headless/graphql-api/graphiql-ide.md#managing-cache)

### Gestione della cache dall’API {#cache-api}

Ciò comporta la pubblicazione della query per AEM utilizzando CURL nell’interfaccia per riga di comando.

Esempio:

```xml
curl -X PUT \
    -H 'authorization: Basic YWRtaW46YWRtaW4=' \
    -H "Content-Type: application/json" \
    "https://publish-p123-e456.adobeaemcloud.com/graphql/persist.json/wknd/plain-article-query-max-age" \
    -d \
'{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
```

`cache-control` può essere impostato al momento della creazione (PUT) o successivamente (ad esempio, tramite una richiesta POST). Il controllo cache è facoltativo quando si crea la query persistente, in quanto AEM può fornire il valore predefinito. Vedi [Come rendere persistente una query GraphQL](/help/headless/graphql-api/persisted-queries.md#how-to-persist-query), per un esempio di persistenza di query utilizzando CURL.

## Codifica dell’URL della query per l’utilizzo da parte di un’app {#encoding-query-url}

Per l&#39;uso da parte di un&#39;applicazione, qualsiasi carattere speciale utilizzato per la costruzione di variabili di query (ovvero punto e virgola (`;`), segno di uguale (`=`), barre `/`) deve essere convertito per utilizzare la codifica UTF-8 corrispondente.

Esempio:

```xml
curl -X GET \ "https://publish-p123-e456.adobeaemcloud.com/graphql/execute.json/wknd/adventure-by-path%3BadventurePath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fadventures%2Fbali-surf-camp%2Fbali-surf-camp"
```

L’URL può essere suddiviso nelle seguenti parti:

| Parte URL | Descrizione |
|----------| -------------|
| `/graphql/execute.json` | Endpoint query persistente |
| `/wknd/adventure-by-path` | Percorso query persistente |
| `%3B` | Codifica di `;` |
| `adventurePath` | Variabile query |
| `%3D` | Codifica di `=` |
| `%2F` | Codifica di `/` |
| `%2Fcontent%2Fdam...` | Percorso codificato del frammento di contenuto |

In testo normale, l’URI della richiesta ha il seguente aspetto:

```plaintext
/graphql/execute.json/wknd/adventure-by-path;adventurePath=/content/dam/wknd/en/adventures/bali-surf-camp/bali-surf-camp
```

Per utilizzare una query persistente in un’app client, è necessario utilizzare l’SDK client headless AEM per [JavaScript](https://github.com/adobe/aem-headless-client-js), [Java](https://github.com/adobe/aem-headless-client-java)oppure [NodeJS](https://github.com/adobe/aem-headless-client-nodejs). L’SDK del client headless codificherà automaticamente tutte le variabili di query in modo appropriato nella richiesta.

## Trasferimento di una query persistente all’ambiente di produzione  {#transfer-persisted-query-production}

Le query persistenti devono sempre essere create su un servizio AEM Author e quindi pubblicate (replicate) in un servizio AEM Publish. Spesso, le query persistenti vengono create e testate in ambienti inferiori, come gli ambienti locali o di sviluppo. È quindi necessario promuovere le query persistenti in ambienti di livello superiore, rendendole infine disponibili in un ambiente di produzione AEM Publish per l’utilizzo da parte delle applicazioni client.

### Query persistenti del pacchetto

Le query persistenti possono essere incorporate in [Pacchetti AEM](/help/implementing/developing/tools/package-manager.md). AEM I pacchetti possono quindi essere scaricati e installati in ambienti diversi. AEM pacchetti possono essere replicati anche da un ambiente AEM Author agli ambienti AEM Publish.

Per creare un pacchetto:

1. Passa a **Strumenti** > **Distribuzione** > **Pacchetti**.
1. Crea un nuovo pacchetto toccando **Crea pacchetto**. Viene visualizzata una finestra di dialogo per la definizione del pacchetto.
1. Nella finestra di dialogo Definizione pacchetto, in **Generale** inserire un **Nome** come &quot;query wknd-persistenti&quot;.
1. Immettere un numero di versione simile a &quot;1.0&quot;.
1. Sotto **Filtri** aggiungi una nuova **Filtro**. Utilizza il Finder del percorso per selezionare il `persistentQueries` sotto la configurazione. Ad esempio, per `wknd` configurazione del percorso completo `/conf/wknd/settings/graphql/persistentQueries`.
1. Tocca **Salva** per salvare la nuova definizione del pacchetto e chiudere la finestra di dialogo.
1. Tocca **Crea** nella definizione del pacchetto appena creata.

Dopo aver generato il pacchetto puoi:

* **Scarica** il pacchetto e ricaricalo in un ambiente diverso.
* **Replicare** il pacchetto toccando **Altro** > **Replicare**. Questo replicherà il pacchetto all’ambiente di pubblicazione AEM connesso.

<!--
1. Using replication/distribution tool:
   1. Go to the Distribution tool.
   1. Select tree activation for the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).

* Using a workflow (via workflow launcher configuration):
  1. Define a workflow launcher rule for executing a workflow model that would replicate the configuration on different events (for example, create, modify, amongst others).
-->
