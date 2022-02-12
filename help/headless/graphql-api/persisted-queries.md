---
title: Query GraphQL persistenti
description: Scopri come persistere le query GraphQL in Adobe Experience Manager per ottimizzare le prestazioni. Le query persistenti possono essere richieste dalle applicazioni client utilizzando il metodo HTTP GET e la risposta può essere memorizzata nella cache ai livelli dispatcher e CDN, migliorando in ultima analisi le prestazioni delle applicazioni client.
feature: Content Fragments,GraphQL API
source-git-commit: 0912cadeae13050c9cfc606d1c2b8f4236cd78ed
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 1%

---


# Query GraphQL persistenti {#persisted-queries-caching}

Le query persistenti sono query GraphQL create e memorizzate sul server AEM. Le query GraphQL standard vengono eseguite utilizzando richieste POST e la risposta non può essere facilmente memorizzata nella cache. Le query persistenti possono essere richieste con una richiesta GET da parte delle applicazioni client. La risposta di una richiesta GET può essere memorizzata nella cache ai livelli dispatcher e CDN, migliorando in ultima analisi le prestazioni dell’applicazione client richiedente.

Le query persistenti devono sempre utilizzare l&#39;endpoint correlato al [configurazione Sites appropriata](graphql-endpoint.md); in modo che possano utilizzare una delle due opzioni, oppure entrambe:

* Configurazione globale ed endpoint La query ha accesso a tutti i modelli di frammenti di contenuto.
* Configurazione o endpoint di Sites specifici La creazione di una query persistente per una configurazione di Sites specifica richiede un endpoint specifico per la configurazione di Sites corrispondente (per fornire accesso ai relativi modelli di frammenti di contenuto).
Ad esempio, per creare una query persistente specifica per la configurazione di WKND Sites, è necessario creare in anticipo una configurazione di Sites specifica per WKND corrispondente e un endpoint specifico per WKND.

>[!NOTE]
>
>Vedi [Abilitare la funzionalità dei frammenti di contenuto nel browser di configurazione](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser) per ulteriori dettagli.
>
>La **Query di persistenza GraphQL** deve essere abilitato per la configurazione Sites appropriata.

Ad esempio, se è presente una particolare query denominata `my-query`, che utilizza un modello `my-model` dalla configurazione Sites `my-conf`:

* Puoi creare una query utilizzando `my-conf` endpoint specifico, quindi la query verrà salvata come segue:
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* Puoi creare la stessa query utilizzando `global` endpoint, ma la query verrà salvata come segue:
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>Queste sono due query diverse - salvate in percorsi diversi.
>
>Usano lo stesso modello, ma attraverso endpoint diversi.

## Come persistere una query GraphQL

Si consiglia di persistere prima delle query in un ambiente di authoring AEM e poi [pubblicare la query](#publish-persisted-query) in un ambiente di pubblicazione AEM. Strumenti simili [Postman](https://www.postman.com/) o strumenti della riga di comando come [arricciare](https://curl.se/) può essere utilizzato.

Di seguito sono riportati i passaggi per persistere una determinata query utilizzando **arricciare** strumento della riga di comando:

1. Prepara la query inserendola nel nuovo URL dell’endpoint `/graphql/persist.json/<config>/<persisted-label>`.

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

1. È quindi possibile richiedere la query persistente tramite GETing l&#39;URL `/graphql/execute.json/<shortPath>`.

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

## Pubblicare una query persistente {#publish-persisted-query}

Le query persistenti possono essere pubblicate in un ambiente AEM Publish in cui possono essere richieste dalle applicazioni client. Per utilizzare una query persistente in fase di pubblicazione, la relativa struttura persistente deve essere replicata.

Esistono diversi approcci per pubblicare una query persistente:

* **Utilizzo di un POST per la replica**:

   ```xml
   $ curl -X POST   http://localhost:4502/bin/replicate.json \
   -H 'authorization: Basic YWRtaW46YWRtaW4=' \
   -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
   -F cmd=activate
   ```

* **Utilizzo di un pacchetto**:
   1. Crea una nuova definizione di pacchetto.
   1. Includi la configurazione (ad esempio, `/conf/wknd/settings/graphql/persistentQueries`).
   1. Crea il pacchetto.
   1. Replicare il pacchetto.

* **Utilizzo dello strumento di replica/distribuzione**:
   1. Passa allo strumento Distribuzione .
   1. Seleziona l’attivazione ad albero per la configurazione (ad esempio, `/conf/wknd/settings/graphql/persistentQueries`).

* **Utilizzo di un flusso di lavoro (tramite la configurazione del modulo di avvio del flusso di lavoro)**:
   1. Definisci una regola di avvio del flusso di lavoro per l’esecuzione di un modello di flusso di lavoro che replichi la configurazione su eventi diversi (ad esempio, crea, modifica, tra gli altri).

Una volta che la configurazione della query è in fase di pubblicazione, si applicano gli stessi principi di autenticazione, utilizzando solo l’endpoint di pubblicazione.

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
