---
title: Utilizzo dell’IDE GraphiQL in AEM
description: Scopri come utilizzare l’IDE GraphiQL in Adobe Experience Manager.
feature: Content Fragments,GraphQL API
exl-id: be2ebd1b-e492-4d77-b6ef-ffdea9a9c775
source-git-commit: dfcad7aab9dda7341de3dc4975eaba9bdfbd9780
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 4%

---

# Utilizzo dell’IDE GraphiQL {#graphiql-ide}

Attuazione dello standard [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) L’IDE è disponibile per l’utilizzo con l’API GraphQL di Adobe Experience Manager (AEM) as a Cloud Service.

>[!NOTE]
>
>Alcune delle funzionalità di questa funzione sono disponibili nel canale prerelease. In particolare, funzionalità relative alle query persistenti.
> 
>Consulta la sezione [Documentazione sul canale prerelease](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#enable-prerelease) per informazioni su come abilitare la funzione per il tuo ambiente.

>[!NOTE]
>
>GraphiQL è incluso in AEM, ma per impostazione predefinita è abilitato solo su `dev-authors` ambienti.

>[!NOTE]
>Devi avere [configurato gli endpoint](/help/headless/graphql-api/graphql-endpoint.md) in [browser di configurazione](/help/assets/content-fragments/content-fragments-configuration-browser.md) prima di utilizzare l&#39;IDE GraphiQL.


La **GraphiQL** strumento consente di testare ed eseguire il debug delle query GraphQL abilitando:
* seleziona la **Endpoint** appropriata alla configurazione Sites che desideri utilizzare per le query
* inserire direttamente nuove query
* creazione e accesso, **[Query persistenti](/help/headless/graphql-api/persisted-queries.md)**
* esegui le query per visualizzare immediatamente i risultati
* gestire **Variabili di query**
* salva e gestisci **Query persistenti**
* pubblicare o annullare la pubblicazione, **Query persistenti** (a/da `dev-publish`)
* vedi **Cronologia** delle query precedenti
* utilizza **Esplora documentazione** accedere alla documentazione; informazioni sui metodi disponibili.

Ad esempio:

* `http://localhost:4502/content/graphiql.html`

![Interfaccia di GraphiQL](assets/cfm-graphiql-interface.png "Interfaccia di GraphiQL")

Puoi utilizzare GraphiQL nel sistema di authoring di sviluppo in modo che possano essere richieste dall’applicazione client utilizzando richieste GET e pubblicando query. Per l&#39;utilizzo in produzione, devi quindi [spostare le query nell&#39;ambiente di produzione](/help/headless/graphql-api/persisted-queries.md#transfer-persisted-query-production). Inizialmente all’autore di produzione per la convalida dei contenuti appena creati con le query e infine alla pubblicazione di produzione per il consumo live.

## Selezione dell&#39;endpoint {#selecting-endpoint}

Come primo passo è necessario selezionare il **[Endpoint](/help/headless/graphql-api/graphql-endpoint.md)** che si desidera utilizzare per le query. L’endpoint è appropriato per la configurazione Sites che desideri utilizzare per le query.

È disponibile dall’elenco a discesa in alto a destra.

## Creazione e persistenza di una nuova query {#creating-new-query}

Puoi inserire la nuova query nell’editor, che si trova nel pannello centrale a sinistra, direttamente sotto il logo GraphiQL.

>[!NOTE]
>
>Se hai già selezionato una query persistente e la visualizzazione nel pannello editor, seleziona `+` (accanto a **Query persistenti**) per svuotare l’editor pronto per la nuova query.

Basta iniziare a digitare, anche l&#39;editor:

* utilizza il passaggio del mouse per visualizzare ulteriori informazioni sugli elementi
* fornisce funzioni quali evidenziazione della sintassi, completamento automatico e suggerimento automatico

>[!NOTE]
>
>Le query GraphQL in genere iniziano con un `{` carattere.
>
>Linee che iniziano con una `#` vengono ignorati.

Utilizzo **Salva con nome** per mantenere la nuova query.

## Aggiornamento della query persistente {#updating-persisted-query}

Seleziona la query da aggiornare dall’elenco nel **Query persistenti** pannello (a sinistra).

La query verrà visualizzata nel pannello dell’editor. Apporta le modifiche necessarie, quindi utilizza **Salva** per eseguire il commit degli aggiornamenti della query persistente.

## Query in esecuzione {#running-queries}

È possibile eseguire immediatamente una nuova query oppure caricare ed eseguire una query persistente. Per caricare una query persistente, selezionala dall’elenco; la query verrà visualizzata nel pannello dell’editor.

In entrambi i casi, la query visualizzata nel pannello dell’editor è la query che verrà eseguita quando:

* tocca o fai clic sul pulsante **Esegui query** icona
* utilizzare la combinazione di tastiera `Control-Enter`

## Variabili di query {#query-variables}

<!-- more details needed here? -->

L&#39;IDE GraphiQL consente inoltre di gestire il tuo [Variabili di query](/help/headless/graphql-api/content-fragments.md#graphql-variables).

Ad esempio:

![Variabili GraphQL](assets/cfm-graphqlapi-03.png "Variabili GraphQL")

## Pubblicazione di query persistenti (dev-publish) {#publishing-persisted-queries}

Dopo aver selezionato la query persistente dall’elenco (pannello a sinistra), puoi utilizzare la **Pubblica** e **Annulla pubblicazione** azioni. Questo li attiverà nell&#39;ambiente di pubblicazione di sviluppo (`dev-publish`) per un facile accesso da parte delle applicazioni durante il test.

>[!NOTE]
>
>Definizione della cache della query persistente `Time To Live` {&quot;cache-control&quot;:&quot;parameter&quot;:value} ha un valore predefinito di 2 ore (7200 secondi).

## Memorizzazione in cache delle query persistenti {#caching-persisted-queries}

AEM la cache CDN (Content Delivery Network) in base a un valore predefinito Time To Live (TTL).

Questo valore è impostato su:

* 7200 secondi è il TTL predefinito per Dispatcher e CDN; noto anche come *cache condivise*
   * predefinito: s-maxage=7200
* 60 è il TTL predefinito per il client (ad esempio, un browser)
   * predefinito: maxage=60

AEM le query GraphQL persistenti con l’interfaccia utente GraphiQL utilizzeranno il TTL predefinito al momento dell’esecuzione. Se desideri modificare il TTL per la query GraphLQ, la query deve essere mantenuta utilizzando il metodo API. Ciò comporta la pubblicazione della query per AEM utilizzando CURL nell’interfaccia della riga di comando.

Ad esempio:

```xml
curl -X PUT \
    -H 'authorization: Basic YWRtaW46YWRtaW4=' \
    -H "Content-Type: application/json" \
    "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
    -d \
'{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
```

La `cache-control` può essere impostato al momento della creazione (PUT) o successivamente (ad esempio, tramite una richiesta di POST). Il controllo cache è facoltativo quando si crea la query persistente, in quanto AEM può fornire il valore predefinito. Vedi [Come persistere una query GraphQL](/help/headless/graphql-api/persisted-queries.md#how-to-persist-query), per un esempio di persistenza di una query utilizzando curl.

## Copia URL per accedere direttamente alla query {#copy-url}

La **Copia URL** consente di simulare una query, copiando l’URL utilizzato per accedere direttamente alla query persistente e visualizzare i risultati. Questo può quindi essere utilizzato per le prove; ad esempio, accedendo in un browser:

<!--
  >[!NOTE]
  >
  >The URL will need [encoding before using programmatically](/help/headless/graphql-api/persisted-queries.md#encoding-query-url).
  >
  >The target environment might need adjusting, depending on your requirements.
-->

Ad esempio:

`http://localhost:4502/graphql/execute.json/global/article-list-01`

Utilizzando questo URL in un browser, puoi confermare i risultati:

![GraphiQL - Copia URL](assets/cfm-graphiql-copy-url.png "GraphiQL - Copia URL")

La **Copia URL** è accessibile tramite i tre punti verticali a destra del nome della query persistente (pannello a sinistra):

![GraphiQL - Copia URL](assets/cfm-graphiql-persisted-query-options.png "GraphiQL - Copia URL")

## Eliminazione delle query persistenti {#deleting-persisted-queries}

La **Elimina** è accessibile anche tramite i tre punti verticali a destra del nome della query persistente (pannello a sinistra).

<!-- what happens if you try to delete something that is still published? -->


## Installazione della query persistente in produzione {#installing-persisted-query-production}

Dopo aver sviluppato e testato la query persistente con GraphiQL, l&#39;obiettivo finale è quello di [trasferirlo all&#39;ambiente di produzione](/help/headless/graphql-api/persisted-queries.md#transfer-persisted-query-production) da utilizzare nelle applicazioni.

## Scelte rapide da tastiera {#keyboard-shortcuts}

Nell’IDE è disponibile una selezione di scelte rapide da tastiera per accedere direttamente alle icone delle azioni:

* Specifica query:  `Shift-Control-P`
* Query di unione:  `Shift-Control-M`
* Esegui query:  `Control-Enter`
* Completamento automatico:  `Control-Space`

>[!NOTE]
>
>Su alcune tastiere il `Control` key è etichettato come `Ctrl`.
