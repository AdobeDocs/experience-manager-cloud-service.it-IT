---
title: Query GraphQL persistenti
description: Scopri come persistere le query GraphQL in Adobe Experience Manager as a Cloud Service per ottimizzare le prestazioni. Le query persistenti possono essere richieste dalle applicazioni client tramite il metodo HTTP GET e la risposta può essere memorizzata nella cache ai livelli dispatcher e CDN, migliorando in definitiva le prestazioni delle applicazioni client.
feature: Content Fragments,GraphQL API
exl-id: 080c0838-8504-47a9-a2a2-d12eadfea4c0
source-git-commit: dfcad7aab9dda7341de3dc4975eaba9bdfbd9780
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 54%

---

# Query GraphQL persistenti {#persisted-queries-caching}

Le query persistenti sono query GraphQL create e memorizzate sul server as a Cloud Service di Adobe Experience Manager (AEM). Possono essere richiesti con una richiesta GET da parte delle applicazioni client. La risposta di una richiesta GET può essere memorizzata nella cache ai livelli dispatcher e CDN, migliorando in definitiva le prestazioni dell’applicazione client richiedente. Ciò è diverso dalle query GraphQL standard, che vengono eseguite utilizzando richieste POST in cui la risposta non può essere facilmente memorizzata nella cache.

La [IDE GraphiQL](/help/headless/graphql-api/graphiql-ide.md) è disponibile in AEM (per impostazione predefinita, `dev-author`) per sviluppare, testare e mantenere le query GraphQL, prima di [trasferimento all&#39;ambiente di produzione](#transfer-persisted-query-production). Per i casi che richiedono personalizzazione (ad esempio, quando [personalizzazione della cache](/help/headless/graphql-api/graphiql-ide.md#caching-persisted-queries)) puoi utilizzare l’API; vedi l’esempio curl fornito in [Come persistere una query GraphQL](#how-to-persist-query).

## Query ed endpoint persistenti {#persisted-queries-and-endpoints}

Le query persistenti devono sempre utilizzare l’endpoint correlato alla [configurazione Sites adeguata](graphql-endpoint.md) in modo che possano utilizzare una delle due opzioni seguenti, oppure entrambe:

* Configurazione globale ed endpoint
La query ha accesso a tutti i modelli per frammenti di contenuto.
* Configurazione/i di Sites ed endpoint specifici 
La creazione di una query persistente per una configurazione di Sites specifica richiede un endpoint specifico per la configurazione di Sites corrispondente (in modo da fornire accesso ai relativi modelli per frammenti di contenuto).
Ad esempio, per creare una query persistente per la configurazione di Sites WKND, è necessario aver già creato una configurazione di Sites specifica per WKND corrispondente e un endpoint specifico per WKND.

>[!NOTE]
>
>Per ulteriori dettagli, vedi [Abilitare la funzionalità Frammenti di contenuto nel browser configurazioni](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser).
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

Si consiglia di persistere prima delle query in un ambiente di authoring AEM e poi [trasferire la query](#transfer-persisted-query-production) nell&#39;ambiente di produzione AEM pubblicazione, per l&#39;utilizzo da parte delle applicazioni.

Esistono diversi metodi per le query persistenti, tra cui:

* IDE GraphiQL - vedi [Salvataggio delle query persistenti](/help/headless/graphql-api/graphiql-ide.md##saving-persisted-queries)
* curl - vedi l&#39;esempio seguente
* Altri strumenti, compresi [Postman](https://www.postman.com/)

Di seguito sono riportati i passaggi per rendere persistente una determinata query utilizzando lo strumento per riga di comando **cURL**:

1. Prepara la query inserendola mediante il metodo PUT nel nuovo URL dell’endpoint `/graphql/persist.json/<config>/<persisted-label>`.

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

1. A questo punto, verifica la risposta.

   Ad esempio, verifica se l’operazione è riuscita:

   ```xml
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

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. Per aggiorna una query persistente, utilizza il metodo POST per un percorso di query già esistente.

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

1. Crea una query normale racchiusa.

   Esempio:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. Crea una query normale racchiusa con il controllo della cache.

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

1. Esegui una query con parametri.

   Esempio:

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   
   $ curl -X GET \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   ```

## Trasferimento di una query persistente all’ambiente di produzione  {#transfer-persisted-query-production}

In ultima analisi, la query persistente deve trovarsi nell’ambiente di pubblicazione di produzione (di AEM as a Cloud Service), dove può essere richiesta dalle applicazioni client. Per utilizzare una query persistente nell&#39;ambiente di pubblicazione di produzione, la relativa struttura persistente deve essere replicata:

* inizialmente all’autore di produzione per la convalida dei contenuti appena creati con le query,
* poi infine alla produzione pubblicare per il consumo in diretta

Esistono diversi approcci per trasferire la query persistente:

1. Utilizzo di un pacchetto:
   1. Crea una nuova definizione di pacchetto.
   1. Includi la configurazione (ad esempio, `/conf/wknd/settings/graphql/persistentQueries`).
   1. Crea il pacchetto.
   1. Trasferisci il pacchetto (download/caricamento o replica).
   1. Installa il pacchetto.

1. Utilizzo del metodo POST per la replica:

   ```xml
   $ curl -X POST   http://localhost:4502/bin/replicate.json \
   -H 'authorization: Basic YWRtaW46YWRtaW4=' \
   -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
   -F cmd=activate
   ```

<!--
1. Using replication/distribution tool:
   1. Go to the Distribution tool.
   1. Select tree activation for the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).

* Using a workflow (via workflow launcher configuration):
  1. Define a workflow launcher rule for executing a workflow model that would replicate the configuration on different events (for example, create, modify, amongst others).
-->

Una volta che la configurazione della query è nell’ambiente di pubblicazione in produzione, si applicano gli stessi principi di autenticazione, utilizzando solo l’endpoint di pubblicazione.

>[!NOTE]
>
>Per l’accesso anonimo il sistema presuppone che l’ACL consenta a “tutti” l’accesso alla configurazione della query.
>
>In caso contrario, non potrà essere eseguito.

## Codifica dell’URL della query per l’utilizzo da parte di un’app {#encoding-query-url}

Per l’utilizzo da parte di un’applicazione, è necessario codificare tutti i punti e virgola (&quot;;&quot;) negli URL.

Ad esempio, nella richiesta di esecuzione di una query persistente:

```xml
curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
```

Per utilizzare una query persistente in un’app client, è necessario utilizzare l’SDK del client headless AEM [Client AEM headless per JavaScript](https://github.com/adobe/aem-headless-client-js).