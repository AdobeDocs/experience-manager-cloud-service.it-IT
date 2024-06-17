---
title: Supporto dei frammenti di contenuto di Adobe Experience Manager as a Cloud Service nell’API Assets HTTP
description: Scopri il supporto per i frammenti di contenuto nell’API Assets HTTP di, un elemento importante della funzione di distribuzione headless di Adobe Experience Manager.
feature: Content Fragments, Assets HTTP API
exl-id: d72cc0c0-0641-4fd6-9f87-745af5f2c232
role: User, Admin
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '1804'
ht-degree: 14%

---

# Supporto per frammenti di contenuto nell’API HTTP di AEM Assets {#content-fragments-support-in-aem-assets-http-api}

## Panoramica {#overview}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/extending/assets-api-content-fragments.html) |
| AEM as a Cloud Service | Questo articolo |

Scopri il supporto per i frammenti di contenuto nell’API Assets HTTP di, un’importante componente della funzione di distribuzione headless di Adobe Experience Manager (AEM).

>[!NOTE]
>
>Sono disponibili anche [OpenAPI per frammenti di contenuto e modelli di frammenti di contenuto](/help/headless/content-fragment-openapis.md).

>[!NOTE]
>
>Il [API HTTP di Assets](/help/assets/mac-api-assets.md) comprende:
>
>* API REST di Assets
>* incluso il supporto per i frammenti di contenuto
>
>L’implementazione corrente dell’API Assets HTTP si basa sulla [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) stile architettonico.

>[!NOTE]
>
>Per informazioni aggiornate sulle API di Experience Manager, visita anche [API di Adobe Experience Manager as a Cloud Service](https://developer.adobe.com/experience-cloud/experience-manager-apis/).

Il [API REST di Assets](/help/assets/mac-api-assets.md) consente agli sviluppatori di Adobe Experience Manager as a Cloud Service di accedere ai contenuti (memorizzati nell’AEM) direttamente tramite l’API HTTP, mediante operazioni CRUD (Create, Read, Update, Delete).

L’API consente di utilizzare Adobe Experience Manager as a Cloud Service come CMS (Content Management System) headless fornendo Content Services a un’applicazione front-end JavaScript. Oppure qualsiasi altra applicazione in grado di eseguire richieste HTTP e gestire risposte JSON.

Ad esempio: [Applicazioni a pagina singola (SPA)](/help/implementing/developing/hybrid/introduction.md), basati su framework o personalizzati, richiedono contenuti forniti tramite l’API HTTP, spesso in formato JSON.

Mentre [Componenti core AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) fornisce un’API personalizzabile che può servire alle operazioni di lettura necessarie a questo scopo e il cui output JSON può essere personalizzato richiede il know-how WCM (Web Content Management) dell’AEM per l’implementazione. Questo perché devono essere ospitate in pagine basate su modelli AEM dedicati. Non tutte le organizzazioni per lo sviluppo dell&#39;SPA hanno accesso diretto a tali conoscenze.

Qui è possibile utilizzare l’API REST di Assets. Consente agli sviluppatori di accedere direttamente alle risorse (ad esempio immagini e frammenti di contenuto), senza doverle incorporare in una pagina, e di distribuire il contenuto in formato JSON serializzato.

>[!NOTE]
>
>Non è possibile personalizzare l’output JSON dall’API REST di Assets.

L’API REST di Assets consente inoltre agli sviluppatori di modificare i contenuti creando, aggiornando o eliminando risorse, frammenti di contenuto e cartelle esistenti.

API REST di Assets:

* segue la [Principio HATEOAS](https://en.wikipedia.org/wiki/HATEOAS)

* implementa [Formato Sirena](https://github.com/kevinswiber/siren)

## Prerequisiti {#prerequisites}

L’API REST di Assets è disponibile per ogni installazione predefinita di una versione di Adobe Experience Manager as a Cloud Service recente.

## Concetti fondamentali {#key-concepts}

Le offerte API REST di Assets [REST](https://en.wikipedia.org/wiki/Representational_state_transfer)accesso in stile alle risorse memorizzate all’interno di un’istanza AEM.

Utilizza il `/api/assets` e richiede il percorso della risorsa per accedervi (senza l&#39;opzione `/content/dam`).

* Ciò significa che per accedere alla risorsa in:
   * `/content/dam/path/to/asset`
* Richiesta:
   * `/api/assets/path/to/asset`

Ad esempio, per accedere a `/content/dam/wknd/en/adventures/cycling-tuscany`, richiedi `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>l’accesso a:
>
>* `/api/assets` **non è** necessario l’uso del selettore `.model`.
>* `/content/path/to/page` **richiede** l’uso del selettore `.model`.

Il metodo HTTP determina l’operazione da eseguire:

* **GET**: per recuperare una rappresentazione JSON di una risorsa o di una cartella
* **POST** : per creare risorse o cartelle
* **PUT**: per aggiornare le proprietà di una risorsa o di una cartella
* **DELETE**: per eliminare una risorsa o una cartella

>[!NOTE]
>
>Il corpo della richiesta e/o i parametri URL possono essere utilizzati per configurare alcune di queste operazioni; ad esempio, definisci che una cartella o una risorsa debbano essere create da una richiesta **POST**.

Il formato esatto delle richieste supportate è definito nel [Riferimento API](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference) documentazione.

>[!NOTE]
>
>Sono disponibili anche [OpenAPI per frammenti di contenuto e modelli di frammenti di contenuto](/help/headless/content-fragment-openapis.md).

### Comportamento transazionale {#transactional-behavior}

Tutte le richieste sono atomiche.

Ciò significa che il successivo (`write`) non possono essere combinate in una singola transazione che potrebbe avere esito positivo o negativo come singola entità.

### API REST di AEM (Assets) e componenti AEM {#aem-assets-rest-api-versus-aem-components}

<table>
 <thead>
  <tr>
   <td>Formato</td>
   <td>API REST di Assets<br/> </td>
   <td>Componente AEM<br/> (componenti che utilizzano modelli Sling)</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>Casi d’uso supportati</td>
   <td>Obiettivo generale.</td>
   <td><p>Ottimizzato per l’utilizzo in un contesto di applicazione a pagina singola (SPA) o in qualsiasi altro contesto (che consuma contenuti).</p> <p>Può anche contenere informazioni di layout.</p> </td>
  </tr>
  <tr>
   <td>Operazioni supportate</td>
   <td><p>Crea, Leggi, Aggiorna, Elimina.</p> <p>Con operazioni aggiuntive, a seconda del tipo di entità.</p> </td>
   <td>Sola lettura.</td>
  </tr>
  <tr>
   <td>Accesso</td>
   <td><p>È accessibile direttamente.</p> <p>Utilizza il <code>/api/assets </code>endpoint, mappato a <code>/content/dam</code> (nell’archivio).</p> 
   <p>Un esempio di percorso sarà simile al seguente: <code>/api/assets/wknd/en/adventures/cycling-tuscany.json</code></p>
   </td>
    <td><p>Deve essere referenziato tramite un componente AEM in una pagina AEM.</p> <p>Utilizza il <code>.model</code> per creare la rappresentazione JSON.</p> <p>Un esempio di percorso sarà simile al seguente:<br/> <code>/content/wknd/language-masters/en/adventures/cycling-tuscany.model.json</code></p> 
   </td>
  </tr>
  <tr>
   <td>Sicurezza</td>
   <td><p>Sono possibili più opzioni.</p> <p>OAuth è proposto; può essere configurato separatamente dalla configurazione standard.</p> </td>
   <td>Utilizza la configurazione standard dell’AEM.</td>
  </tr>
  <tr>
   <td>Osservazioni di architettura</td>
   <td><p>L'accesso in scrittura è in genere indirizzato a un'istanza Autore.</p> <p>La lettura può anche essere indirizzata a un’istanza Publish.</p> </td>
   <td>Poiché questo approccio è di sola lettura, in genere viene utilizzato per le istanze Publish.</td>
  </tr>
  <tr>
   <td>Output</td>
   <td>Output SIREN basato su JSON: dettagliato, ma potente. Consente di navigare all’interno del contenuto.</td>
   <td>Output proprietario basato su JSON; configurabile tramite modelli Sling. Navigare nella struttura del contenuto è difficile da implementare (ma non necessariamente impossibile).</td>
  </tr>
 </tbody>
</table>

### Sicurezza {#security}

Se l’API REST di Assets viene utilizzata in un ambiente senza requisiti di autenticazione specifici, il filtro AEM CORS deve essere configurato correttamente.

>[!NOTE]
>
>Per ulteriori informazioni, consulta:
>
>* [Spiegazione di CORS/AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html)
>* [Video: Sviluppo per CORS con AEM (04:06)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/develop-for-cross-origin-resource-sharing.html)
>

Negli ambienti con requisiti di autenticazione specifici, si consiglia OAuth.

## Funzioni disponibili {#available-features}

I frammenti di contenuto sono un tipo specifico di risorsa, vedi [Utilizzo dei frammenti di contenuto](/help/assets/content-fragments/content-fragments.md).

Per ulteriori informazioni sulle funzioni disponibili tramite l’API, consulta:

* Il [API REST di Assets](/help/assets/mac-api-assets.md)
* [Tipi di entità](/help/assets/content-fragments/assets-api-content-fragments.md#entity-types), in cui sono spiegate le funzioni specifiche di ciascun tipo supportato (come pertinenti ai frammenti di contenuto)

>[!NOTE]
>
>Sono disponibili anche [OpenAPI per frammenti di contenuto e modelli di frammenti di contenuto](/help/headless/content-fragment-openapis.md).

### Paging {#paging}

L’API REST di Assets supporta il paging (per le richieste GET) tramite i parametri URL:

* `offset` - il numero della prima entità (figlio) da recuperare
* `limit` - il numero massimo di entità restituite

La risposta contiene informazioni di paging come parte del `properties` sezione dell&#39;output SIREN. Questo `srn:paging` contiene il numero totale di entità (figlio) ( `total`), l&#39;offset e il limite ( `offset`, `limit`) come specificato nella richiesta.

>[!NOTE]
>
>Il paging viene in genere applicato alle entità contenitore (ovvero cartelle o risorse con rappresentazioni), in quanto si riferisce agli elementi figlio dell’entità richiesta.

#### Esempio: paging {#example-paging}

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

Le cartelle fungono da contenitori per risorse e altre cartelle. Riflettono la struttura dell’archivio dei contenuti dell’AEM.

L’API REST di Assets espone l’accesso alle proprietà di una cartella. Ad esempio, il nome e il titolo. Le risorse vengono esposte come entità secondarie di cartelle e sottocartelle.

>[!NOTE]
>
>A seconda del tipo di risorsa delle risorse e cartelle secondarie, l’elenco delle entità secondarie può già contenere l’intero set di proprietà che definisce la rispettiva entità secondaria. In alternativa, è possibile esporre solo un set ridotto di proprietà per un&#39;entità in questo elenco di entità figlio.

### Risorse {#assets}

Se viene richiesta una risorsa, la risposta restituisce i relativi metadati, ad esempio titolo, nome e altre informazioni come definito dal rispettivo schema della risorsa.

I dati binari di una risorsa vengono esposti come collegamento SIREN di tipo `content`.

Le risorse possono avere più rappresentazioni. In genere vengono esposte come entità secondarie, ad eccezione della rappresentazione di una miniatura esposta come collegamento di tipo `thumbnail` ( `rel="thumbnail"`).

### Frammenti di contenuto {#content-fragments}

A [frammento di contenuto](/help/assets/content-fragments/content-fragments.md) è un tipo speciale di risorsa. Possono essere utilizzati per accedere a dati strutturati, tra cui testi, numeri, date.

Poiché esistono diverse differenze *standard* risorse (come immagini o audio), si applicano alcune regole aggiuntive per la loro gestione.

#### Rappresentazione {#representation}

Frammenti di contenuto:

* Non esporre dati binari.
* Sono contenuti nell’output JSON (all’interno del `properties` proprietà ).

* Sono anche considerati atomici. In altre parole, gli elementi e le varianti vengono esposti come parte delle proprietà del frammento, anziché come collegamenti o entità figlio. Questo consente un accesso efficiente al payload di un frammento.

#### Modelli di contenuto e frammenti di contenuto {#content-models-and-content-fragments}

Attualmente i modelli che definiscono la struttura di un frammento di contenuto non sono esposti tramite un’API HTTP. Pertanto, la *consumer* deve conoscere il modello di un frammento (almeno un minimo), anche se la maggior parte delle informazioni può essere dedotta dal payload; poiché i tipi di dati, e così via, fanno parte della definizione.

Per creare un frammento di contenuto, è necessario fornire il percorso (archivio interno) del modello.

#### Contenuto associato {#associated-content}

Il contenuto associato non è esposto.

## Utilizzando {#using}

L’utilizzo può variare a seconda che si utilizzi un ambiente di authoring o pubblicazione AEM, insieme a un caso d’uso specifico.

* Si consiglia di associare la creazione a un&#39;istanza Autore ([e attualmente non è possibile replicare un frammento da pubblicare utilizzando questa API](/help/assets/content-fragments/assets-api-content-fragments.md#limitations)).
* La distribuzione è possibile da entrambi, in quanto AEM fornisce il contenuto richiesto solo in formato JSON.

   * L’archiviazione e la distribuzione da un’istanza di authoring AEM devono essere sufficienti per le applicazioni di librerie multimediali dietro il firewall.

   * Per la distribuzione live sul web, si consiglia un’istanza di pubblicazione dell’AEM.

>[!CAUTION]
>
>La configurazione del Dispatcher sulle istanze cloud AEM potrebbe bloccare l’accesso a `/api`.

>[!NOTE]
>
>Consulta la [Riferimento API](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference). In particolare, [API di Adobe Experience Manager Assets - Frammenti di contenuto](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/assets-api-content-fragments/index.html).
>
>Sono disponibili anche [OpenAPI per frammenti di contenuto e modelli di frammenti di contenuto](/help/headless/content-fragment-openapis.md).

## Limitazioni {#limitations}

Esistono alcune limitazioni:

* **I modelli per frammenti di contenuto non sono attualmente supportati**: non possono essere letti o creati. Per poter creare o aggiornare un frammento di contenuto esistente, gli sviluppatori devono conoscere il percorso corretto del modello per frammenti di contenuto. Attualmente, l’unico metodo per ottenere una panoramica di questi è tramite l’interfaccia utente di amministrazione.
* **I riferimenti vengono ignorati**. Al momento non sono presenti controlli per verificare se viene fatto riferimento a un frammento di contenuto esistente. Pertanto, ad esempio, l’eliminazione di un frammento di contenuto potrebbe causare problemi in una pagina che contiene un riferimento al frammento di contenuto eliminato.
* **Tipo di dati JSON** L’output REST API di *Tipo di dati JSON* è *output basato su stringhe*.

## Codici di stato e messaggi di errore {#status-codes-and-error-messages}

I seguenti codici di stato possono essere visualizzati nelle circostanze pertinenti:

* **200** (OK)

  Restituito quando:

   * richiesta di un frammento di contenuto tramite `GET`
   * aggiornamento di un frammento di contenuto tramite `PUT`

* **201** (Creato)

  Restituito quando:

   * creazione di un frammento di contenuto tramite `POST`

* **404** (Non trovato)

  Restituito quando:

   * il frammento di contenuto richiesto non esiste

* **500** (Errore interno del server)

  >[!NOTE]
  >
  >Questo errore viene restituito:
  >
  >* si è verificato un errore che non può essere identificato con un codice specifico
  >* quando il payload specificato non era valido

  Di seguito sono elencati gli scenari comuni in cui viene restituito questo stato di errore, insieme al messaggio di errore (monospazio) generato:

   * La cartella principale non esiste (quando si crea un frammento di contenuto tramite `POST`)
   * Non è stato fornito alcun modello per frammenti di contenuto (cq:model è mancante), non può essere letto (a causa di un percorso non valido o di un problema di autorizzazione) o non è disponibile alcun modello per frammenti valido:

      * `No content fragment model specified`
      * `Cannot create a resource of given model '/foo/bar/qux'`

   * Impossibile creare il frammento di contenuto (potrebbe trattarsi di un problema di autorizzazione):

      * `Could not create content fragment`

   * Impossibile aggiornare il titolo e/o la descrizione:

      * `Could not set value on content fragment`

   * Impossibile impostare i metadati:

      * `Could not set metadata on content fragment`

   * Impossibile trovare o aggiornare l’elemento di contenuto

      * `Could not update content element`
      * `Could not update fragment data of element`

  I messaggi di errore dettagliati vengono restituiti nel modo seguente:

  ```xml
  {
    "class": "core/response",
    "properties": {
      "path": "/api/assets/foo/bar/qux",
      "location": "/api/assets/foo/bar/qux.json",
      "parentLocation": "/api/assets/foo/bar.json",
      "status.code": 500,
      "status.message": "...{error message}.."
    }
  }
  ```

## Riferimento API {#api-reference}

Consulta qui per riferimenti API dettagliati:

* [API di Adobe Experience Manager Assets - Frammenti di contenuto](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/assets-api-content-fragments/index.html)

* [API HTTP di Assets](/help/assets/mac-api-assets.md)

   * [Funzioni disponibili](/help/assets/mac-api-assets.md#available-features)

* Sono disponibili anche [OpenAPI per frammenti di contenuto e modelli di frammenti di contenuto](/help/headless/content-fragment-openapis.md).

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni, consulta:

* [Documentazione API HTTP di Assets](/help/assets/mac-api-assets.md)
* [Sessione AEM Gem: OAuth](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/gems2014/aem-oauth-server-functionality-in-aem.html)
