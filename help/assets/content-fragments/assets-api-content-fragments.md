---
title: Supporto per frammenti di contenuto di Adobe Experience Manager as a Cloud Service nell’API HTTP di Assets
description: Scopri il supporto per i frammenti di contenuto nell’API HTTP di Assets, un elemento importante della funzione di distribuzione headless di Adobe Experience Manager.
feature: Content Fragments, Assets HTTP API
exl-id: d72cc0c0-0641-4fd6-9f87-745af5f2c232
role: User, Admin
source-git-commit: f55299d7054a9e1f8e1356cb975dfeee162ec202
workflow-type: tm+mt
source-wordcount: '1856'
ht-degree: 14%

---

# Supporto dei frammenti di contenuto nell’API HTTP di AEM Assets {#content-fragments-support-in-aem-assets-http-api}

## Panoramica {#overview}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/extending/assets-api-content-fragments.html) |
| AEM as a Cloud Service | Questo articolo |

>[!CAUTION]
>
>Il supporto per i frammenti di contenuto nell&#39;API HTTP di Assets è ora [obsoleto](/help/release-notes/deprecated-removed-features.md).
>
>È stato sostituito da [Content Fragment Delivery con OpenAPI](/help/headless/aem-content-fragment-delivery-with-openapi.md) insieme a [Content Fragments and Content Fragment Models Management OpenAPI](/help/headless/content-fragment-openapis.md).

Scopri il supporto per i frammenti di contenuto nell’API HTTP di Assets, un elemento importante della funzione di consegna headless di Adobe Experience Manager (AEM).

>[!NOTE]
>
>Consulta [API di AEM per la distribuzione e la gestione strutturata dei contenuti](/help/headless/apis-headless-and-content-fragments.md) per una panoramica delle varie API disponibili e un confronto di alcuni dei concetti coinvolti.
>
>Sono disponibili anche [OpenAPI per frammenti di contenuto e modelli di frammenti di contenuto](/help/headless/content-fragment-openapis.md).

>[!NOTE]
>
>L&#39;[API HTTP di Assets](/help/assets/mac-api-assets.md) include:
>
>* API REST di Assets
>* incluso il supporto per i frammenti di contenuto
>
>L&#39;implementazione corrente dell&#39;API HTTP di Assets si basa sullo stile di architettura [REST](https://en.wikipedia.org/wiki/Representational_state_transfer).

>[!NOTE]
>
>Per informazioni aggiornate sulle API Experience Manager, visita [API Adobe Experience Manager as a Cloud Service](https://developer.adobe.com/experience-cloud/experience-manager-apis/).

L&#39;[API REST di Assets](/help/assets/mac-api-assets.md) consente agli sviluppatori di Adobe Experience Manager as a Cloud Service di accedere ai contenuti (memorizzati in AEM) direttamente tramite l&#39;API HTTP, mediante operazioni CRUD (Create, Read, Update, Delete).

L’API consente di utilizzare Adobe Experience Manager as a Cloud Service come CMS (Content Management System) headless fornendo Content Services a un’applicazione front-end JavaScript. Oppure qualsiasi altra applicazione in grado di eseguire richieste HTTP e gestire risposte JSON.

Ad esempio, [le applicazioni a pagina singola (SPA)](/help/implementing/developing/hybrid/introduction.md), basate su framework o personalizzate, richiedono contenuto fornito tramite API HTTP, spesso in formato JSON.

Sebbene i [componenti core di AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) forniscano un&#39;API personalizzabile in grado di fornire le operazioni di lettura necessarie per questo scopo e il cui output JSON possa essere personalizzato, richiedono il know-how AEM WCM (Web Content Management) per l&#39;implementazione. Questo perché devono essere ospitate in pagine basate su modelli AEM dedicati. Non tutte le organizzazioni che si occupano di sviluppo di applicazioni a pagina singola hanno accesso diretto a tali conoscenze.

Qui è possibile utilizzare l’API REST di Assets. Consente agli sviluppatori di accedere direttamente alle risorse (ad esempio immagini e frammenti di contenuto), senza doverle incorporare in una pagina, e di distribuire il contenuto in formato JSON serializzato.

>[!NOTE]
>
>Non è possibile personalizzare l’output JSON dall’API REST di Assets.

L’API REST di Assets consente inoltre agli sviluppatori di modificare i contenuti creando, aggiornando o eliminando risorse, frammenti di contenuto e cartelle esistenti.

API REST di Assets:

* segue il principio [HATEOAS](https://en.wikipedia.org/wiki/HATEOAS)

* implementa il formato [SIREN](https://github.com/kevinswiber/siren)

## Prerequisiti {#prerequisites}

L’API REST di Assets è disponibile per ogni installazione predefinita di una versione di Adobe Experience Manager as a Cloud Service recente.

## Concetti fondamentali {#key-concepts}

L&#39;API REST di Assets offre l&#39;accesso in stile [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) alle risorse memorizzate all&#39;interno di un&#39;istanza di AEM.

Utilizza l&#39;endpoint `/api/assets` e richiede il percorso della risorsa per accedervi (senza `/content/dam` iniziale).

* Ciò significa che per accedere alla risorsa in:
   * `/content/dam/path/to/asset`
* Richiesta:
   * `/api/assets/path/to/asset`

Ad esempio, per accedere a `/content/dam/wknd/en/adventures/cycling-tuscany`, richiedi `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>
>l’accesso a:
>
>* `/api/assets` **non è** necessario l’uso del selettore `.model`.
>* `/content/path/to/page` **richiede** l’uso del selettore `.model`.

Il metodo HTTP determina l’operazione da eseguire:

* **GET**: per recuperare una rappresentazione JSON di una risorsa o di una cartella
* **POST** - per creare risorse o cartelle
* **PUT**: per aggiornare le proprietà di una risorsa o di una cartella
* **DELETE**: per eliminare una risorsa o una cartella

>[!NOTE]
>
>Il corpo della richiesta e/o i parametri URL possono essere utilizzati per configurare alcune di queste operazioni; ad esempio, definisci che una cartella o una risorsa debbano essere create da una richiesta **POST**.

Il formato esatto delle richieste supportate è definito nella documentazione di [Riferimento API](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference).

>[!NOTE]
>
>Sono disponibili anche [OpenAPI per frammenti di contenuto e modelli di frammenti di contenuto](/help/headless/content-fragment-openapis.md).

### Comportamento transazionale {#transactional-behavior}

Tutte le richieste sono atomiche.

Ciò significa che le richieste successive (`write`) non possono essere combinate in una singola transazione che potrebbe avere esito positivo o negativo come singola entità.

### API REST di AEM (Assets) rispetto ai componenti di AEM {#aem-assets-rest-api-versus-aem-components}

<table>
 <thead>
  <tr>
   <td>Aspetto</td>
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
   <td><p>È accessibile direttamente.</p> <p>Utilizza l'endpoint <code>/api/assets </code>, mappato a <code>/content/dam</code> (nell'archivio).</p> 
   <p>Un esempio di percorso sarà simile al seguente: <code>/api/assets/wknd/en/adventures/cycling-tuscany.json</code></p>
   </td>
    <td><p>Deve essere referenziato tramite un componente AEM in una pagina AEM.</p> <p>Utilizza il selettore <code>.model</code> per creare la rappresentazione JSON.</p> <p>Un esempio di percorso sarà simile al seguente:<br/> <code>/content/wknd/language-masters/en/adventures/cycling-tuscany.model.json</code></p> 
   </td>
  </tr>
  <tr>
   <td>Protezione</td>
   <td><p>Sono possibili più opzioni.</p> <p>OAuth è proposto; può essere configurato separatamente dalla configurazione standard.</p> </td>
   <td>Utilizza la configurazione standard di AEM.</td>
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

### Protezione {#security}

Se l’API REST di Assets viene utilizzata in un ambiente senza requisiti di autenticazione specifici, il filtro CORS di AEM deve essere configurato correttamente.

>[!NOTE]
>
>Per ulteriori informazioni, consulta:
>
>* [Spiegazione di CORS/AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html)
>* [Video: sviluppo per CORS con AEM (04:06)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/develop-for-cross-origin-resource-sharing.html)
>

Negli ambienti con requisiti di autenticazione specifici, si consiglia OAuth.

## Funzioni disponibili {#available-features}

I frammenti di contenuto sono un tipo specifico di risorsa. Vedere [Utilizzo dei frammenti di contenuto](/help/assets/content-fragments/content-fragments.md).

Per ulteriori informazioni sulle funzioni disponibili tramite l’API, consulta:

* [API REST di Assets](/help/assets/mac-api-assets.md)
* [Tipi di entità](/help/assets/content-fragments/assets-api-content-fragments.md#entity-types), in cui sono illustrate le caratteristiche specifiche di ciascun tipo supportato (relative ai frammenti di contenuto)

>[!NOTE]
>
>Sono disponibili anche [OpenAPI per frammenti di contenuto e modelli di frammenti di contenuto](/help/headless/content-fragment-openapis.md).

### Paging {#paging}

L’API REST di Assets supporta il paging (per le richieste GET) tramite i parametri URL:

* `offset` - numero della prima entità (figlio) da recuperare
* `limit` - Numero massimo di entità restituite

La risposta contiene informazioni di paging nella sezione `properties` dell&#39;output SIREN. Questa proprietà `srn:paging` contiene il numero totale di entità (figlio) ( `total`), l&#39;offset e il limite ( `offset`, `limit`) come specificato nella richiesta.

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

Le cartelle fungono da contenitori per risorse e altre cartelle. Riflettono la struttura dell’archivio dei contenuti di AEM.

L’API REST di Assets espone l’accesso alle proprietà di una cartella. Ad esempio, il nome e il titolo. Assets sono esposte come entità secondarie di cartelle e sottocartelle.

>[!NOTE]
>
>A seconda del tipo di risorsa delle risorse e cartelle secondarie, l’elenco delle entità secondarie può già contenere l’intero set di proprietà che definisce la rispettiva entità secondaria. In alternativa, è possibile esporre solo un set ridotto di proprietà per un&#39;entità in questo elenco di entità figlio.

### Risorse {#assets}

Se viene richiesta una risorsa, la risposta restituisce i relativi metadati, ad esempio titolo, nome e altre informazioni come definito dal rispettivo schema della risorsa.

I dati binari di una risorsa sono esposti come collegamento SIREN di tipo `content`.

Assets può avere più rappresentazioni. Queste sono in genere esposte come entità secondarie, ad eccezione di una rappresentazione di miniature esposta come collegamento di tipo `thumbnail` ( `rel="thumbnail"`).

### Frammenti di contenuto {#content-fragments}

Un [frammento di contenuto](/help/assets/content-fragments/content-fragments.md) è un tipo speciale di risorsa. Possono essere utilizzati per accedere a dati strutturati, tra cui testi, numeri, date.

Poiché esistono diverse differenze rispetto alle *risorse standard* (ad esempio immagini o audio), per gestirle sono applicabili alcune regole aggiuntive.

#### Rappresentazione {#representation}

Frammenti di contenuto:

* Non esporre dati binari.
* Sono contenute nell&#39;output JSON (all&#39;interno della proprietà `properties`).

* Sono anche considerati atomici. In altre parole, gli elementi e le varianti vengono esposti come parte delle proprietà del frammento, anziché come collegamenti o entità figlio. Questo consente un accesso efficiente al payload di un frammento.

#### Modelli di contenuto e frammenti di contenuto {#content-models-and-content-fragments}

Attualmente i modelli che definiscono la struttura di un frammento di contenuto non sono esposti tramite un’API HTTP. Pertanto, il *consumatore* deve conoscere almeno il modello di un frammento, anche se la maggior parte delle informazioni può essere dedotta dal payload; poiché i tipi di dati e così via fanno parte della definizione.

Per creare un frammento di contenuto, è necessario fornire il percorso (archivio interno) del modello.

#### Contenuto associato {#associated-content}

Il contenuto associato non è esposto.

## Utilizzo {#using}

L’utilizzo può variare a seconda che si utilizzi un ambiente AEM Author o Publish, oltre a un caso d’uso specifico.

* Si consiglia di associare la creazione a un&#39;istanza Autore ([e attualmente non è possibile replicare un frammento da pubblicare utilizzando questa API](/help/assets/content-fragments/assets-api-content-fragments.md#limitations)).
* La distribuzione è possibile da entrambi, in quanto AEM fornisce il contenuto richiesto solo in formato JSON.

   * L’archiviazione e la distribuzione da un’istanza di AEM Author devono essere sufficienti per le applicazioni di librerie multimediali dietro il firewall.

   * Per la distribuzione live sul web, si consiglia un’istanza AEM Publish.

>[!CAUTION]
>
>La configurazione di Dispatcher nelle istanze cloud di AEM potrebbe bloccare l&#39;accesso a `/api`.

>[!NOTE]
>
>Vedi il [riferimento API](/help/assets/content-fragments/assets-api-content-fragments.md#api-reference). In particolare, [API di Adobe Experience Manager Assets - Frammenti di contenuto](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/assets-api-content-fragments/index.html).
>
>Sono disponibili anche [OpenAPI per frammenti di contenuto e modelli di frammenti di contenuto](/help/headless/content-fragment-openapis.md).

## Limitazioni {#limitations}

Esistono alcune limitazioni:

* **I modelli per frammenti di contenuto non sono attualmente supportati**. Impossibile leggerli o crearli. Per poter creare o aggiornare un frammento di contenuto esistente, gli sviluppatori devono conoscere il percorso corretto del modello per frammenti di contenuto. Attualmente, l’unico metodo per ottenere una panoramica di questi è tramite l’interfaccia utente di amministrazione.
* **I riferimenti vengono ignorati**. Al momento non sono presenti controlli per verificare se viene fatto riferimento a un frammento di contenuto esistente. Pertanto, ad esempio, l’eliminazione di un frammento di contenuto potrebbe causare problemi in una pagina che contiene un riferimento al frammento di contenuto eliminato.
* **Tipo di dati JSON** L&#39;output REST API del tipo di dati *JSON* è *output basato su stringhe*.

## Codici di stato e messaggi di errore {#status-codes-and-error-messages}

I seguenti codici di stato possono essere visualizzati nelle circostanze pertinenti:

* **200** (OK)

  Restituito quando:

   * richiesta di un frammento di contenuto tramite `GET`
   * aggiornamento di un frammento di contenuto tramite `PUT` completato

* **201** (creato)

  Restituito quando:

   * creazione di un frammento di contenuto tramite `POST` completata

* **404** (non trovato)

  Restituito quando:

   * il frammento di contenuto richiesto non esiste

* **500** (errore interno del server)

  >[!NOTE]
  >
  >Questo errore viene restituito:
  >
  >* si è verificato un errore che non può essere identificato con un codice specifico
  >* quando il payload specificato non era valido

  Di seguito sono elencati gli scenari comuni in cui viene restituito questo stato di errore, insieme al messaggio di errore (monospazio) generato:

   * La cartella principale non esiste (quando si crea un frammento di contenuto tramite `POST`)
   * Non è stato fornito alcun modello per frammenti di contenuto (cq:model mancante), non può essere letto (a causa di un percorso non valido o di un problema di autorizzazione) o non è disponibile un modello per frammenti valido:

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
