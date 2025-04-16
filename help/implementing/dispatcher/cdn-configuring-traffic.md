---
title: Configurazione del traffico sulla rete CDN
description: Scopri come configurare i traffico della rete CDN dichiarando regole e filtri in un file di configurazione e distribuendoli nella rete CDN utilizzando una pipeline di configurazione di Cloud Manager.
feature: Dispatcher
exl-id: e0b3dc34-170a-47ec-8607-d3b351a8658e
role: Admin
source-git-commit: a43fdc3f9b9ef502eb0af232b1c6aedbab159f1f
workflow-type: tm+mt
source-wordcount: '1390'
ht-degree: 1%

---


# Configurazione del traffico sulla rete CDN {#cdn-configuring-cloud}

AEM come Cloud Service offre una raccolta di funzionalità configurabili a [livello di CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) gestita da Adobe Systems che modificano la natura delle richieste in entrata o delle risposte in uscita. The following rules, described in detail in this page, can be declared to achieve the following behavior:

* [Request transformations](#request-transformations) - modify aspects of incoming requests, including headers, paths and parameters.
* [Trasformazioni di](#response-transformations) risposta - modificare le intestazioni che sono sulla via del ritorno al client (ad esempio, un browser web).
* [Reindirizzamenti](#server-side-redirectors) lato server: attivano un reindirizzare browser.
* [Selettori di](#origin-selectors) origine: proxy per un backend di origine diverso.

Nella CDN sono inoltre configurabili le regole di Filtra del traffico (incluso WAF), che controllano quali traffico sono consentite o negate dalla CDN. Questa funzione è già stata rilasciata e puoi trovare ulteriori informazioni nella [pagina Regole del Filtra del traffico, incluse le regole](/help/security/traffic-filter-rules-including-waf.md) WAF.

Inoltre, se la rete CDN non è in grado di contattare la sua origine, è possibile scrivere un regola che fa riferimento a una pagina di errore personalizzata self-hosted (che viene quindi renderizzata). Scopri ulteriori informazioni su questo argomento leggendo l&#39;articolo [Configurazione delle pagine](/help/implementing/dispatcher/cdn-error-pages.md) di errore CDN.

Tutte queste regole, dichiarate in un file di configurazione nel controllo del codice sorgente, vengono distribuite utilizzando la pipeline](/help/operations/config-pipeline.md) di configurazione di Cloud Manager[. Tenere presente che la dimensione cumulativa del file di configurazione, incluse le regole di filtro traffico, non può superare i 100 KB.

## Ordine di valutazione {#order-of-evaluation}

Dal punto di vista funzionale, le varie caratteristiche menzionate in precedenza vengono valutate nella seguente sequenza:

![Ordine di valutazione](/help/implementing/dispatcher/assets/order.png)

## Configurazione {#initial-setup}

Prima di poter configurare traffico sulla rete CDN, è necessario effettuare le seguenti operazioni:

1. Crea un file denominato `cdn.yaml` o simile, facendo riferimento ai vari frammenti di configurazione nelle sezioni seguenti.

   Tutti gli snippet hanno queste proprietà comuni, descritte in [Pipeline](/help/operations/config-pipeline.md#common-syntax) di configurazione. Il `kind` valore della proprietà deve essere *CDN* e la `version` proprietà deve essere impostata su *1*.

   ```
   kind: "CDN"
   version: "1"
   metadata:
     envTypes: ["dev"]
   ```

1. Posizionare il file in una cartella di primo livello denominata *config* o simile, come descritto in [Pipeline di configurazione](/help/operations/config-pipeline.md#folder-structure).

1. Creare una pipeline di configurazione in Cloud Manager, come descritto in [Pipeline di configurazione](/help/operations/config-pipeline.md#managing-in-cloud-manager).

1. Distribuisci la configurazione.

## Sintassi delle regole {#configuration-syntax}

I tipi di regole nelle sezioni seguenti condividono una sintassi comune.

A una regola viene fatto riferimento tramite un nome, una &quot;clausola when&quot; condizionale e azioni.

La clausola when determina se una regola verrà valutata in base a proprietà quali dominio, percorso, stringhe di query, intestazioni e cookie. La sintassi è la stessa per tutti i tipi di regole. Per ulteriori dettagli, vedere la [sezione Struttura condizione](/help/security/traffic-filter-rules-including-waf.md#condition-structure) nell&#39;articolo Regole filtro traffico.

I dettagli del nodo delle azioni differiscono per tipo di regola e sono descritti nelle singole sezioni seguenti.

## Richiedi trasformazioni {#request-transformations}

Le regole di trasformazione delle richieste consentono di modificare le richieste in ingresso. Le regole supportano l’impostazione, la disimpostazione e l’alterazione di percorsi, parametri di query e intestazioni (inclusi i cookie) in base a varie condizioni di corrispondenza, comprese le espressioni regolari. Puoi anche impostare le variabili, a cui è possibile fare riferimento in un secondo momento nella sequenza di valutazione.

Use cases are varied and include URL rewrites for application simplification or mapping legacy URLs.

As mentioned earlier, there is a size limit to the configuration file so organizations with larger requirements should define rules in the `apache/dispatcher` layer.

Esempio di configurazione:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev", "stage", "prod"]
data:
  requestTransformations:
    removeMarketingParams: true
    rules:
      - name: set-header-rule
        when:
          reqProperty: path
          like: /set-header
        actions:
          - type: set
            reqHeader: x-some-header
            value: some value
      - name: set-header-with-reqproperty-rule
        when:
          reqProperty: path
          like: /set-header
        actions:
          - type: set
            reqHeader: x-some-header
            value: {reqProperty: path}
      - name: unset-header-rule
        when:
          reqProperty: path
          like: /unset-header
        actions:
          - type: unset
            reqHeader: x-some-header

      - name: unset-matching-query-params-rule
        when:
          reqProperty: path
          equals: /unset-matching-query-params
        actions:
          - type: unset
            queryParamMatch: ^removeMe_.*$

      - name: unset-all-query-params-except-exact-two-rule
        when:
          reqProperty: path
          equals: /unset-all-query-params-except-exact-two
        actions:
          - type: unset
            queryParamMatch: ^(?!leaveMe$|leaveMeToo$).*$

      - name: multi-action
        when:
          reqProperty: path
          like: /multi-action
        actions:
          - type: set
            reqHeader: x-header1
            value: body set by transformation rule
          - type: set
            reqHeader: x-header2
            value: '201'

      - name: replace-html
        when:
          reqProperty: path
          like: /mypath
        actions:
          - type: transform
            reqProperty: path
            op: replace
            match: \.html$
            replacement: ""
```

**Azioni**

Explained in the table below are the available actions.

| Nome | Proprietà | Significato |
|-----------|--------------------------|-------------|
| **set** | (reqProperty o reqHeader o queryParam o reqCookie), valore | Imposta un parametro richiesta specificato (supportata solo la proprietà &quot;path&quot;) o richiesta intestazione, parametro di query o cookie su un valore specificato, che può essere un valore letterale stringa o un parametro richiesta. |
|     | var, valore | Imposta la proprietà richiesta specificata su un valore specificato. |
| **Annullata** | reqProperty | Rimuove un parametro richiesta specificato (supportata solo la proprietà &quot;path&quot;) o richiesta intestazione, parametro di query o cookie a un determinato valore, che può essere un valore letterale stringa o un parametro richiesta. |
|         | var | Removes a specified variable. |
|         | queryParamMatch | Removes all query parameters that match a specified regular expression. |
|         | queryParamDoesNotMatch | Rimuove tutti i parametri di query che non corrispondono a un&#39;espressione regolare specificata. |
| **trasformazione** | op:replace, (reqProperty o reqHeader o queryParam o reqCookie o var), match, replace | Sostituisce parte del parametro di richiesta (supportata solo la proprietà &quot;path&quot;), dell’intestazione di richiesta, del parametro di query, del cookie o della variabile con un nuovo valore. |
|              | op:tolower, (reqProperty o reqHeader o queryParam o reqCookie o var) | Imposta sul valore minuscolo il parametro della richiesta (supportata solo la proprietà &quot;path&quot; ), l&#39;intestazione di richiesta, il parametro di query, il cookie o la variabile. |

Sostituisci azioni supportano i gruppi di acquisizione, come illustrato di seguito:

```
      - name: extract-country-code-from-path
        when:
          reqProperty: path
          matches: ^/([a-zA-Z]{2})(/.*|$)
        actions:
          - type: set
            var: country-code
            value:
              reqProperty: path
          - type: transform
            var: country-code
            op: replace
            match: ^/([a-zA-Z]{2})(/.*|$)
            replacement: \1
      - name: replace-jpg-with-jpeg
        when:
          reqProperty: path
          like: /mypath
        actions:
          - type: transform
            reqProperty: path
            op: replace
            match: (.*)(\.jpg)$
            replacement: "\1\.jpeg"
```

Le azioni possono essere concatenate. Ad esempio:

```
actions:
    - type: transform
      reqProperty: path
      op: replace
      match: \.html$
      replacement: ""
    - type: transform
      reqProperty: path
      op: tolower
```

### Variabili {#variables}

È possibile impostare le variabili durante la trasformazione richiesta e quindi farvi riferimento in un secondo momento nella sequenza di valutazione. Vedere l&#39;ordine [del diagramma di valutazione](#order-of-evaluation) per ulteriori dettagli.

Esempio di configurazione:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["prod", "dev"]
data:
  requestTransformations:
    rules:
      - name: set-variable-rule
        when:
          reqProperty: path
          equals: /set-variable
        actions:
          - type: set
            var: some_var_name
            value: some_value

  responseTransformations:
    rules:
      - name: set-response-header-while-variable
        when:
          var: some_var_name
          equals: some_value
        actions:
          - type: set
            respHeader: x-some-header
            value: some header value
```

## Trasformazioni delle risposte {#response-transformations}

Le regole di trasformazione delle risposte consentono di impostare e annullare le intestazioni delle risposte in uscita della rete CDN. Inoltre, vedi l&#39;esempio precedente per fare riferimento a una variabile precedentemente impostata in un regola di trasformazione richiesta. È inoltre possibile impostare il codice di stato della risposta.

Esempio di configurazione:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["prod", "dev"]
data:
  responseTransformations:
    rules:
      - name: set-response-header-rule
        when:
          reqProperty: path
          like: /set-response-header
        actions:
          - type: set
            value: value-set-by-resp-rule
            respHeader: x-resp-header

      - name: unset-response-header-rule
        when:
          reqProperty: path
          like: /unset-response-header
        actions:
          - type: unset
            respHeader: x-header1

      # Example: Multi-action on response header
      - name: multi-action-response-header-rule
        when:
          reqProperty: path
          like: /multi-action-response-header
        actions:
          - type: set
            respHeader: x-resp-header-1
            value: value-set-by-resp-rule-1
          - type: set
            respHeader: x-resp-header-2
            value: value-set-by-resp-rule-2
      # Example: setting status code
      - name: status-code-rule
        when:
          reqProperty: path
          like: status-code
        actions:
          - type: set
            respProperty: status
            value: '410'        
```

**Azioni**

Nella tabella seguente sono illustrate le azioni disponibili.

| Nome | Proprietà | Significato |
|-----------|--------------------------|-------------|
| **mettere** | reqHeader, valore | Imposta un&#39;intestazione specificata su un dato valore nella risposta. |
|          | respProperty, valore | Imposta una proprietà response. Supporta solo la proprietà &quot;status&quot; per impostare il codice di stato. |
| **Annullata** | respHeader | Rimuove un’intestazione specificata dalla risposta. |

## Selettori di origine {#origin-selectors}

Puoi sfruttare la rete CDN di AEM per indirizzare il traffico a diversi backend, incluse le applicazioni non Adobe (ad esempio in base al percorso o al sottodominio).

Esempio di configurazione:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  originSelectors:
    rules:
      - name: example-com
        when: { reqProperty: path, like: /proxy* }
        action:
          type: selectOrigin
          originName: example-com
          # skipCache: true
    origins:
      - name: example-com
        domain: www.example.com
        # ip: '1.1.1.1'
        # forwardHost: true
        # forwardCookie: true
        # forwardAuthorization: true
        # timeout: 20
```

**Azioni**

Nella tabella seguente è illustrata l’azione disponibile.

| Nome | Proprietà | Significato |
|-----------|--------------------------|-------------|
| **selectOrigin** | originName | Name of one of the defined origins. |
|     | skipCache (optional, default is false) | Flag whether to use caching for requests matching this rule. By default, responses will be cached according to the response caching header (e.g., Cache-Control or Expires) |

**Origins**

Le connessioni alle origini sono solo SSL e utilizzano la porta 443.

| Proprietà | Significato |
|------------------|--------------------------------------|
| **nome** | Nome a cui può fare riferimento &quot;action.originName&quot;. |
| **dominio** | Nome di dominio utilizzato per connettersi al back-end personalizzato. Viene utilizzato anche per l’SNI SSL e la convalida. |
| **ip** (facoltativo, supportato iv4 e ipv6) | Se fornito, viene utilizzato per connettersi al backend invece di &quot;dominio&quot;. Tuttavia, &quot;domain&quot; viene utilizzato per l’SNI SSL e la convalida. |
| **forwardHost** (facoltativo, il valore predefinito è false) | If set to true, then &quot;Host&quot; header from the client request will be passed to the backend, otherwise the &quot;domain&quot; value will be passed in the &quot;Host&quot; header. |
| **forwardCookie** (optional, default is false) | If set to true then the &quot;Cookie&quot; header from the client request will be passed to backend, otherwise the Cookie header is removed. |
| **forwardAuthorization** (optional, default is false) | If set to true then the &quot;Authorization&quot; header from the client request will be passed to the backend, otherwise the Authorization header is removed. |
| **timeout** (optional, in seconds, default is 60) | Numero di secondi in cui la rete CDN deve attendere che un server backend distribuisca il primo byte di un corpo di risposta HTTP. Questo valore viene utilizzato anche come timeout tra i byte per il server back-end. |

### Proxy a Edge Delivery Services {#proxying-to-edge-delivery}

Esistono scenari in cui i selettori di origine devono essere utilizzati per instradare il traffico attraverso AEM Publish ad AEM Edge Delivery Services:

* Alcuni contenuti vengono distribuiti da un dominio gestito da AEM Publish, mentre altri contenuti dello stesso dominio vengono distribuiti da Edge Delivery Services
* Il contenuto distribuito da Edge Delivery Services trarrebbe vantaggio dalle regole distribuite tramite la pipeline di configurazione, incluse le regole del filtro del traffico o le trasformazioni di richiesta/risposta

Ecco un esempio di origine selettore regola che può raggiungere questo obiettivo:

```
kind: CDN
version: '1'
data:
  originSelectors:
    rules:
      - name: select-edge-delivery-services-origin
        when:
          allOf:
            - reqProperty: tier
              equals: publish
            - reqProperty: domain
              equals: <Production Host>
            - reqProperty: path
              matches: "^(/scripts/.*|/styles/.*|/fonts/.*|/blocks/.*|/icons/.*|.*/media_.*|/favicon.ico)"
        action:
          type: selectOrigin
          originName: aem-live
    origins:
      - name: aem-live
        domain: main--repo--owner.aem.live
```

>[!NOTE]
> Poiché viene utilizzata la rete CDN gestita Adobe Systems, assicurarsi di configurare l&#39;invalidazione push in **modalità gestita**, seguendo la documentazione](https://www.aem.live/docs/byo-dns#setup-push-invalidation) di invalidazione push dell&#39;installazione di Edge Delivery Services[.


## Reindirizzamenti lato server {#server-side-redirectors}

È possibile utilizzare le regole di reindirizzare lato client per i reindirizzamenti lato client 301, 302 e simili. Se un regola corrisponde, la rete CDN risponde con una riga di stato che include il codice di stato e il messaggio (ad esempio, HTTP/1.1 301 spostato in modo permanente), nonché il set di intestazioni della posizione.

Sono consentite posizioni assolute e relative con valori fissi.

Be aware that the cumulative size of the configuration file, including traffic filter rules, cannot exceed 100KB.

Esempio di configurazione:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  redirects:
    rules:
      - name: redirect-absolute
        when: { reqProperty: path, equals: "/page.html" }
        action:
          type: redirect
          status: 301
          location: https://example.com/page
      - name: redirect-relative
        when: { reqProperty: path, equals: "/anotherpage.html" }
        action:
          type: redirect
          location: /anotherpage
```

| Nome | Proprietà | Significato |
|-----------|--------------------------|-------------|
| **reindirizzare** | luogo | Valore per l&#39;intestazione &quot;Location&quot;. |
|     | status (facoltativo, il valore predefinito è 301) | Stato HTTP da utilizzare nel messaggio reindirizzare, 301 Per impostazione predefinita, i valori consentiti sono: 301, 302, 303, 307, 308. |

Le posizioni di un reindirizzare possono essere letterali stringa (ad esempio, https://www.example.com/page) o il risultato di una proprietà (ad esempio, percorso) che viene facoltativamente trasformata, con la seguente sintassi:

```
redirects:
  rules:
    - name: country-code-redirect
      when: { reqProperty: path, like: "/" }
      action:
        type: redirect
        location:
          reqProperty: clientCountry
          transform:
            - op: replace
              match: '^(.*)$'
              replacement: 'https://www.example.com/\1/home'
            - op: tolower
    - name: www-redirect
      when: { reqProperty: domain, equals: "example.com" }
      action:
        type: redirect
        location:
          reqProperty: url
          transform:
            - op: replace
              match: '^/(.*)$'
              replacement: 'https://www.example.com/\1'
```
