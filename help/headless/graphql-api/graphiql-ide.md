---
title: Utilizzo dell’IDE GraphiQL in AEM
description: Scopri come utilizzare l’IDE GraphiQL in Adobe Experience Manager.
feature: Content Fragments,GraphQL API
exl-id: be2ebd1b-e492-4d77-b6ef-ffdea9a9c775
source-git-commit: a2e36e296749c79040c9687bbd88288d8977086d
workflow-type: ht
source-wordcount: '964'
ht-degree: 100%

---

# Utilizzo dell’IDE GraphiQL {#graphiql-ide}

Un’implementazione dell’IDE [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) standard è disponibile con l’API GraphQL di Adobe Experience Manager (AEM) as a Cloud Service.

>[!NOTE]
>
>Alcune delle funzionalità di questa caratteristica sono disponibili nel canale prerelease. In particolare, funzionalità relative alle query persistenti.
> 
>Consulta la sezione [Documentazione sul canale prerelease](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=it#enable-prerelease) per informazioni su come abilitare la funzione per il tuo ambiente.

>[!NOTE]
>
>GraphiQL è incluso in AEM, ma per impostazione predefinita è abilitato solo sugli ambienti `dev-authors`.

>[!NOTE]
>Prima di utilizzare l’IDE GraphiQL, devi avere [configurato gli endpoint](/help/headless/graphql-api/graphql-endpoint.md) nel [browser delle configurazioni](/help/assets/content-fragments/content-fragments-configuration-browser.md).


Lo strumento **GraphiQL** consente di testare ed eseguire il debug delle query GraphQL consentendoti di:
* selezionare l’**Endpoint** appropriato per la configurazione Sites da utilizzare per le query;
* inserire direttamente nuove query;
* creare e accedere a **[query persistenti](/help/headless/graphql-api/persisted-queries.md)**;
* eseguire le query per visualizzare immediatamente i risultati;
* gestire **variabili di query**;
* salvare e gestire **query persistenti**;
* pubblicare o annullare la pubblicazione di **query persistenti** (a/da `dev-publish`);
* vedere la **cronologia** delle query precedenti;
* utilizzare **Esplora documentazione** per accedere alla documentazione, per scoprire e comprendere i metodi disponibili.

Esempio:

* `http://localhost:4502/aem/graphiql.html`

![Interfaccia di GraphiQL](assets/cfm-graphiql-interface.png "Interfaccia di GraphiQL")

Puoi utilizzare GraphiQL nel sistema di authoring dell’ambiente di sviluppo in modo che possano essere richieste dall’applicazione client utilizzando richieste GET e pubblicando query. Per l’utilizzo in produzione, devi quindi [spostare le query nell’ambiente di produzione](/help/headless/graphql-api/persisted-queries.md#transfer-persisted-query-production). Inizialmente devi spostarle nell’istanza Author dell’ambiente di produzione per convalidare i contenuti appena creati con le query, e infine nell’istanza Publish di produzione per l’utilizzo live.

## Selezione dell’endpoint {#selecting-endpoint}

Come primo passo è necessario selezionare l’**[endpoint](/help/headless/graphql-api/graphql-endpoint.md)** da utilizzare per le query. L’endpoint è appropriato per la configurazione Sites che desideri utilizzare per le query.

È disponibile dall’elenco a discesa in alto a destra.

## Creazione e persistenza di una nuova query {#creating-new-query}

Puoi inserire la nuova query nell’editor, che si trova nel pannello centrale a sinistra, direttamente sotto il logo GraphiQL.

>[!NOTE]
>
>Se hai già selezionato una query persistente, ed è visualizzata nel pannello editor, seleziona `+` (accanto a **query persistenti**) per svuotare l’editor approntandolo per la nuova query.

A questo punto è sufficiente iniziare a digitare. L’editor, inoltre:

* mostra ulteriori informazioni sugli elementi al passaggio del mouse;
* fornisce funzioni quali evidenziazione della sintassi, completamento automatico e suggerimento automatico.

>[!NOTE]
>
>Le query GraphQL in genere iniziano con un carattere `{`.
>
>Le righe che iniziano con `#` vengono ignorate.

Utilizza **Salva con nome** per rendere persistente la nuova query.

## Aggiornamento della query persistente {#updating-persisted-query}

Seleziona la query da aggiornare dall’elenco nel pannello delle **query persistenti** (a sinistra).

La query viene visualizzata nel pannello dell’editor. Apporta le modifiche necessarie, quindi utilizza **Salva** per confermare gli aggiornamenti della query persistente.

## Esecuzione delle query {#running-queries}

Puoi eseguire immediatamente una nuova query oppure caricare ed eseguire una query persistente. Per caricare una query persistente, selezionala dall’elenco: la query viene visualizzata nel pannello dell’editor.

In entrambi i casi, la query visualizzata nel pannello dell’editor è quella che verrà eseguita quando:

* tocchi o fai clic sull’icona **Esegui query**;
* utilizzi la scelta rapida di tastiera `Control-Enter`.

## Variabili di query {#query-variables}

<!-- more details needed here? -->

L’IDE GraphiQL consente inoltre di gestire le [variabili di query](/help/headless/graphql-api/content-fragments.md#graphql-variables).

Esempio:

![Variabili GraphQL](assets/cfm-graphqlapi-03.png "Variabili GraphQL")

## Pubblicazione di query persistenti (dev-publish) {#publishing-persisted-queries}

Dopo aver selezionato la query persistente dall’elenco (pannello a sinistra), puoi utilizzare le azioni **Pubblica** e **Annulla pubblicazione**. Questo le attiverà nell’istanza Pubblish dell’ambiente di sviluppo (`dev-publish`) per un facile accesso da parte delle applicazioni durante il test.

>[!NOTE]
>
>La definizione della cache della query persistente `Time To Live` {&quot;cache-control&quot;:&quot;parametro&quot;:valore} ha un valore predefinito di 2 ore (7200 secondi).

## Memorizzazione in cache delle query persistenti {#caching-persisted-queries}

AEM renderà non valida la cache CDN (Content Delivery Network) in base a un valore Time To Live (TTL) predefinito.

Questo valore è impostato su:

* 7200 secondi, TTL predefinito per Dispatcher e CDN; noto anche come *cache condivise*
   * impostazione predefinita: s-maxage=7200
* 60, TTL predefinito per il client (ad esempio, un browser)
   * impostazione predefinita: maxage=60

Le query AEM GraphQL persistenti con l’interfaccia utente GraphiQL utilizzeranno il valore TTL predefinito al momento dell’esecuzione. Se desideri modificare il TTL per la query GraphLQ, la query deve essere resa persistente utilizzando il metodo API. Ciò comporta la pubblicazione della query per AEM utilizzando CURL nell’interfaccia per riga di comando.

Esempio:

```xml
curl -X PUT \
    -H 'authorization: Basic YWRtaW46YWRtaW4=' \
    -H "Content-Type: application/json" \
    "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
    -d \
'{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
```

`cache-control` può essere impostato al momento della creazione (PUT) o successivamente (ad esempio, tramite una richiesta POST). Il controllo cache è facoltativo quando si crea la query persistente, in quanto AEM può fornire il valore predefinito. Vedi [Come rendere persistente una query GraphQL](/help/headless/graphql-api/persisted-queries.md#how-to-persist-query), per un esempio di persistenza di query utilizzando CURL.

## Copiare l’URL per accedere direttamente alla query {#copy-url}

L’opzione **Copia URL** consente di simulare una query copiando l’URL utilizzato per accedere direttamente alla query persistente e visualizzare i risultati. Questa può quindi essere utilizzata per i test; ad esempio, accedendo in un browser:

<!--
  >[!NOTE]
  >
  >The URL will need [encoding before using programmatically](/help/headless/graphql-api/persisted-queries.md#encoding-query-url).
  >
  >The target environment might need adjusting, depending on your requirements.
-->

Esempio:

`http://localhost:4502/graphql/execute.json/global/article-list-01`

Utilizzando questo URL in un browser, puoi confermare i risultati:

![GraphiQL - Copia URL](assets/cfm-graphiql-copy-url.png "GraphiQL - Copia URL")

L’opzione **Copia URL** è accessibile tramite i tre punti verticali a destra del nome della query persistente (pannello a sinistra):

![GraphiQL - Copia URL](assets/cfm-graphiql-persisted-query-options.png "GraphiQL - Copia URL")

## Eliminazione delle query persistenti {#deleting-persisted-queries}

L’opzione **Elimina** è anch’essa accessibile tramite i tre punti verticali a destra del nome della query persistente (pannello a sinistra).

<!-- what happens if you try to delete something that is still published? -->


## Installazione della query persistente nell’ambiente di produzione {#installing-persisted-query-production}

Dopo aver sviluppato e testato la query persistente con GraphiQL, occorre [trasferirla all’ambiente di produzione](/help/headless/graphql-api/persisted-queries.md#transfer-persisted-query-production) in modo che possa essere utilizzata dalle applicazioni.

## Scelte rapide da tastiera {#keyboard-shortcuts}

Nell’IDE è disponibile una selezione di scelte rapide da tastiera per accedere direttamente alle icone di azione:

* Migliora query: `Shift-Control-P`
* Unisci query: `Shift-Control-M`
* Esegui query: `Control-Enter`
* Completamento automatico: `Control-Space`

>[!NOTE]
>
>Su alcune tastiere il tasto `Control` è etichettato come `Ctrl`.
