---
title: Come aggiornare i contenuti tramite le API di AEM Assets
description: In questa parte del Percorso di sviluppatori AEM Headless, scopri come utilizzare l’API REST per accedere e aggiornare il contenuto dei frammenti di contenuto.
hide: true
hidefromtoc: true
index: false
exl-id: 8d133b78-ca36-4c3b-815d-392d41841b5c
translation-type: tm+mt
source-git-commit: 0c47dec1e96fc3137d17fc3033f05bf1ae278141
workflow-type: tm+mt
source-wordcount: '1657'
ht-degree: 3%

---

# Come aggiornare i contenuti tramite le API di AEM Assets {#update-your-content}

>[!CAUTION]
>
>LAVORO IN CORSO - La creazione di questo documento è in corso e non deve essere inteso come completo o definitivo né deve essere utilizzato a fini di produzione.

In questa parte del [AEM Percorso di sviluppatori headless,](overview.md) scopri come utilizzare l’API REST per accedere e aggiornare il contenuto dei frammenti di contenuto.

## La storia finora {#story-so-far}

Nel documento precedente del percorso AEM headless, [Come accedere ai contenuti tramite API di distribuzione AEM](access-your-content.md) hai imparato ad accedere ai contenuti headless in AEM tramite l’API GraphQL di AEM e ora dovresti:

* Comprendere ad alto livello GraphQL.
* Scopri come funziona l’API GraphQL di AEM.
* Comprendere alcune domande pratiche di esempio.

Questo articolo si basa su questi elementi fondamentali per comprendere come aggiornare il contenuto headless esistente in AEM tramite l’API REST.

## Obiettivo {#objective}

* **Pubblico**: Avanzate
* **Obiettivo**: Scopri come utilizzare l’API REST per accedere e aggiornare il contenuto dei frammenti di contenuto:
   * Introduzione all’API HTTP di AEM Assets.
   * È possibile introdurre e discutere il supporto per i frammenti di contenuto nell’API.
   * Illustrare i dettagli dell’API.

<!--
  * Look at sample code to see how things work in practice.
-->

## Perché è necessaria l’API HTTP delle risorse per il frammento di contenuto {#why-http-api}

Nella fase precedente del Percorso Headless hai appreso dell’utilizzo dell’API GraphQL di AEM per recuperare il contenuto utilizzando le query.

Allora perché è necessaria un&#39;altra API?

L’API HTTP di Assets consente di **leggere** il contenuto, ma consente anche di **creare**, **Aggiornare** e **Eliminare** contenuti - azioni non possibili con l’API GraphQL.

## API HTTP di Assets {#assets-http-api}

L’ [API HTTP Assets](/help/assets/mac-api-assets.md) include:

* API REST di Assets
* incluso il supporto per i frammenti di contenuto

L’implementazione corrente dell’API HTTP di Assets si basa sullo stile architettonico **REST** .

L’API REST di Assets consente agli sviluppatori di Adobe Experience Manager come Cloud Service di accedere ai contenuti (memorizzati in AEM) direttamente tramite l’API HTTP tramite le operazioni **CRUD** (Creazione, lettura, aggiornamento, eliminazione).

L’API ti consente di utilizzare Adobe Experience Manager come Cloud Service come CMS headless (Content Management System) fornendo servizi di contenuto a un’applicazione front-end JavaScript. O qualsiasi altra applicazione in grado di eseguire richieste HTTP e gestire risposte JSON.

Ad esempio, le applicazioni a pagina singola (SPA), basate su framework o personalizzate, richiedono il contenuto fornito tramite un’API, spesso in formato JSON.

Anche se AEM componenti core forniscono un’API molto completa, flessibile e personalizzabile che può servire le operazioni di lettura necessarie a questo scopo e il cui output JSON può essere personalizzato, richiedono AEM know-how WCM (Web Content Management) per l’implementazione, in quanto devono essere ospitati in pagine basate su modelli AEM dedicati. Non tutte le SPA organizzazioni di sviluppo hanno accesso diretto a tali conoscenze.

Questo è il momento in cui è possibile utilizzare l’API REST di Assets. Consente agli sviluppatori di accedere direttamente alle risorse (ad esempio, immagini e frammenti di contenuto) senza dover prima incorporarle in una pagina e consegnare il contenuto in formato JSON serializzato.

>[!NOTE]
>
>Non è possibile personalizzare l’output JSON dall’API REST di Assets.

L’API REST di Assets consente inoltre agli sviluppatori di modificare il contenuto creando nuove risorse, aggiornando o eliminando risorse esistenti, frammenti di contenuto e cartelle.

API REST di Assets:

* segue il principio HATEOAS
* implementa il formato SIREN

## Prerequisiti {#prerequisites}

L’API REST di Assets è disponibile per ogni installazione predefinita di una versione Adobe Experience Manager recente come Cloud Service.

## Concetti fondamentali {#key-concepts}

L’API REST di Assets offre l’accesso in stile REST alle risorse memorizzate all’interno di un’istanza AEM.

Utilizza l’ `/api/assets` endpoint e richiede il percorso della risorsa per accedervi (senza l’ `/content/dam` iniziale).

* Ciò significa che per accedere alla risorsa in:
   * `/content/dam/path/to/asset`
* È necessario richiedere:
   * `/api/assets/path/to/asset`

Ad esempio, per accedere a `/content/dam/wknd/en/adventures/cycling-tuscany`, richiedi `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>Accedere a:
>
>* `/api/assets` **non** richiede l’utilizzo del  `.model` selettore.
>* `/content/path/to/page` **** richiede l’utilizzo del  `.model` selettore.


Il metodo HTTP determina l&#39;operazione da eseguire:

* **GET** : per recuperare una rappresentazione JSON di una risorsa o di una cartella
* **POST** : per creare nuove risorse o cartelle
* **PUT** : per aggiornare le proprietà di una risorsa o di una cartella
* **DELETE** : per eliminare una risorsa o una cartella

>[!NOTE]
>
>Il corpo della richiesta e/o i parametri URL possono essere utilizzati per configurare alcune di queste operazioni; ad esempio, definisci che una cartella o una risorsa debba essere creata da una richiesta **POST**.

Il formato esatto delle richieste supportate è definito nella documentazione Riferimento API.

### Comportamento transazionale {#transactional-behavior}

Tutte le richieste sono atomiche.

Ciò significa che le richieste successive (`write`) non possono essere combinate in una singola transazione che potrebbe avere esito positivo o negativo come singola entità.

### API REST AEM (Assets) rispetto ai componenti AEM {#aem-assets-rest-api-versus-aem-components}

<table>
 <thead>
  <tr>
   <td>Aspetto</td>
   <td>API REST delle risorse<br/> </td>
   <td>AEM Componente<br/> (componenti che utilizzano modelli Sling)</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>Casi d’uso supportati</td>
   <td>Scopo generale.</td>
   <td><p>Ottimizzato per il consumo in applicazioni a pagina singola (SPA) o in qualsiasi altro contesto (che consuma contenuti).</p> <p>Può anche contenere informazioni sul layout.</p> </td>
  </tr>
  <tr>
   <td>Operazioni supportate</td>
   <td><p>Crea, Leggi, Aggiorna, Elimina.</p> <p>Con operazioni aggiuntive a seconda del tipo di entità.</p> </td>
   <td>Sola lettura.</td>
  </tr>
  <tr>
   <td>Accesso</td>
   <td><p>È accessibile direttamente.</p> <p>Utilizza l'endpoint <code>/api/assets </code>mappato a <code>/content/dam</code> (nel repository).</p> 
   <p>Un esempio di percorso potrebbe essere: <code>/api/assets/wknd/en/adventures/cycling-tuscany.json</code></p>
   </td>
    <td><p>Deve essere fatto riferimento tramite un componente AEM in una pagina AEM.</p> <p>Utilizza il selettore <code>.model</code> per creare la rappresentazione JSON.</p> <p>Un esempio di percorso potrebbe essere:<br/> <code>/content/wknd/language-masters/en/adventures/cycling-tuscany.model.json</code></p> 
   </td>
  </tr>
  <tr>
   <td>Sicurezza</td>
   <td><p>Sono possibili più opzioni.</p> <p>è proposta l’OAuth; può essere configurato separatamente dalla configurazione standard.</p> </td>
   <td>Utilizza AEM configurazione standard.</td>
  </tr>
  <tr>
   <td>Osservazioni architettoniche</td>
   <td><p>L'accesso in scrittura si rivolge in genere a un'istanza dell'autore.</p> <p>La lettura può anche essere diretta a un'istanza di pubblicazione.</p> </td>
   <td>Poiché questo approccio è di sola lettura, in genere viene utilizzato per le istanze di pubblicazione.</td>
  </tr>
  <tr>
   <td>Output</td>
   <td>Output SIREN basato su JSON: verboso, ma potente. Consente di spostarsi all’interno del contenuto.</td>
   <td>output proprietario basato su JSON; configurabile tramite modelli Sling. La navigazione nella struttura dei contenuti è difficile da implementare (ma non necessariamente impossibile).</td>
  </tr>
 </tbody>
</table>

### Sicurezza {#security}

Se l’API REST di Assets viene utilizzata in un ambiente senza requisiti di autenticazione specifici, AEM filtro CORS deve essere configurato correttamente.

>[!NOTE]
>
>Per ulteriori informazioni, consulta:
>
>* Spiegazione di CORS/AEM
>* Video: sviluppo per CORS con AEM

>



In ambienti con requisiti di autenticazione specifici, si consiglia OAuth.

## Funzioni disponibili {#available-features}

I frammenti di contenuto sono un tipo specifico di risorsa. Consulta Utilizzo dei frammenti di contenuto .

Per ulteriori informazioni sulle funzioni disponibili tramite API, consulta:

* API REST di Assets
* Tipi di entità, in cui vengono illustrate le funzioni specifiche di ciascun tipo supportato (in base ai frammenti di contenuto)

### Paging {#paging}

L’API REST di Assets supporta il paging (per richieste GET) tramite i parametri URL:

* `offset` - il numero della prima entità (figlio) da recuperare
* `limit` - il numero massimo di entità restituite

La risposta conterrà informazioni di paging come parte della sezione `properties` dell&#39;output SIREN. Questa proprietà `srn:paging` contiene il numero totale di entità (secondarie) ( `total`), l&#39;offset e il limite ( `offset`, `limit`) come specificato nella richiesta.

>[!NOTE]
>
>La paging viene in genere applicata alle entità contenitore (ovvero cartelle o risorse con rendering), in quanto si riferisce agli elementi secondari dell’entità richiesta.

#### Esempio: Paging {#example-paging}

`GET /api/assets.json?offset=2&limit=3`

```json
...
"properties": {
    ...
    "srn:paging": {
        "total": 7,
        "offset": 2,
        "limit": 3
    }
    ...
}
...
```

## Tipi di entità {#entity-types}

### Cartelle {#folders}

Le cartelle fungono da contenitori per risorse e altre cartelle. Essi riflettono la struttura dell’archivio dei contenuti AEM.

L’API REST di Assets espone l’accesso alle proprietà di una cartella; ad esempio nome, titolo, ecc. Le risorse vengono esposte come entità secondarie di cartelle e sottocartelle.

>[!NOTE]
>
>A seconda del tipo di risorsa delle risorse e delle cartelle secondarie, l’elenco delle entità figlio può già contenere l’intero set di proprietà che definisce la rispettiva entità figlio. In alternativa, solo un set ridotto di proprietà può essere esposto per un’entità in questo elenco di entità figlio.

### Assets {#assets}

Se viene richiesta una risorsa, la risposta restituirà i relativi metadati; quali titolo, nome e altre informazioni definite dal rispettivo schema di risorse.

I dati binari di una risorsa sono esposti come collegamento SIREN di tipo `content`.

Le risorse possono avere più rappresentazioni. Questi vengono generalmente esposti come entità secondarie, con un’eccezione rappresentata dal rendering delle miniature, che viene esposto come collegamento di tipo `thumbnail` ( `rel="thumbnail"`).

### Frammenti di contenuto {#content-fragments}

Un frammento di contenuto è un tipo speciale di risorsa. Possono essere utilizzati per accedere a dati strutturati, quali testi, numeri, date, ecc.

Poiché esistono diverse differenze tra le risorse *standard* (come immagini o audio), per gestirle è necessario applicare alcune regole aggiuntive.

#### Rappresentazione {#representation}

Frammenti di contenuto:

* Non esporre dati binari.
* Sono completamente contenute nell’output JSON (all’interno della proprietà `properties` ).

* Sono anche considerate atomiche, ovvero gli elementi e le varianti sono esposti come parte delle proprietà del frammento rispetto a come collegamenti o entità secondarie. Ciò consente un accesso efficiente al payload di un frammento.

#### Modelli di contenuto e frammenti di contenuto {#content-models-and-content-fragments}

Attualmente i modelli che definiscono la struttura di un frammento di contenuto non sono esposti tramite un’API HTTP. Pertanto il *consumatore* deve conoscere il modello di un frammento (almeno un minimo), anche se la maggior parte delle informazioni può essere dedotta dal payload; come tipi di dati, ecc. fanno parte della definizione.

Per creare un nuovo frammento di contenuto, è necessario fornire il percorso (archivio interno) del modello.

#### Contenuto associato {#associated-content}

Il contenuto associato non è attualmente esposto.

## Utilizzo dell’API REST di Assets {#using-aem-assets-rest-api}

Per informazioni dettagliate sull’utilizzo dell’API REST di AEM Assets, puoi fare riferimento a:

* API HTTP di Adobe Experience Manager Assets
* Supporto dei frammenti di contenuto nell’API HTTP di AEM Assets

## Novità {#whats-next}

Dopo aver completato questa parte del Percorso di sviluppatori AEM Headless, devi:

* Comprendere l’API HTTP di AEM Assets.
* Scopri in che modo i frammenti di contenuto sono supportati in questa API.

<!--
* Have experience with sample code and know how the API works in practice.
-->

Continua il tuo percorso AEM headless rivedendo il documento [Come mettere tutto insieme - La tua app e il tuo contenuto in AEM Headless](put-it-all-together.md) dove imparerai come prendere il tuo progetto AEM Headless e prepararlo per il lancio.

## Risorse aggiuntive {#additional-resources}

* [REST](https://en.wikipedia.org/wiki/Representational_state_transfer)
* [Principio delle HATEOAS](https://en.wikipedia.org/wiki/HATEOAS)
* [Formato SIREN](https://github.com/kevinswiber/siren)
* [API HTTP di Assets](/help/assets/mac-api-assets.md)
* [API REST per frammenti di contenuto](/help/assets/content-fragments/assets-api-content-fragments.md)
   * [Riferimento API](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference)
* [Utilizzo di frammenti di contenuto](/help/assets/content-fragments/content-fragments.md)
* [AEM Core Components](https://docs.adobe.com/content/help/it/experience-manager-core-components/using/introduction.html)
* [Spiegazione di CORS/AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
* [Video: sviluppo per CORS con AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)

