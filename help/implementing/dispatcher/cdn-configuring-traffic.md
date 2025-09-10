---
title: Configurazione del traffico sulla rete CDN
description: Scopri come configurare il traffico CDN dichiarando regole e filtri in un file di configurazione e distribuendoli nella CDN utilizzando una pipeline di configurazione di Cloud Manager.
feature: Dispatcher
exl-id: e0b3dc34-170a-47ec-8607-d3b351a8658e
role: Admin
source-git-commit: b367e7d62596c33a4ba399008e856a97d12fb45b
workflow-type: tm+mt
source-wordcount: '1523'
ht-degree: 1%

---


# Configurazione del traffico sulla rete CDN {#cdn-configuring-cloud}

AEM as a Cloud Service offre una raccolta di funzionalità configurabili a livello di [CDN](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) gestita da Adobe che modificano la natura delle richieste in arrivo o delle risposte in uscita. Le seguenti regole, descritte in dettaglio in questa pagina, possono essere dichiarate per ottenere il seguente comportamento:

* [Trasformazioni richieste](#request-transformations) - Modifica gli aspetti delle richieste in arrivo, inclusi intestazioni, percorsi e parametri.
* [Trasformazioni di risposta](#response-transformations) - Modifica le intestazioni che stanno per essere inviate al client (ad esempio, un browser Web).
* [Reindirizzamenti lato server](#server-side-redirectors) - attiva un reindirizzamento del browser.
* [Selettori di origine](#origin-selectors) - proxy a un backend di origine diverso.

Nella rete CDN sono configurabili anche le regole del filtro del traffico (incluso WAF), che controllano il traffico consentito o negato dalla rete CDN. Questa funzionalità è già stata rilasciata ed è possibile ottenere ulteriori informazioni nella pagina [Regole filtro del traffico, incluse le regole di WAF](/help/security/traffic-filter-rules-including-waf.md).

Inoltre, se la rete CDN non è in grado di contattare la relativa origine, puoi scrivere una regola che fa riferimento a una pagina di errore personalizzata con hosting autonomo (di cui viene quindi eseguito il rendering). Ulteriori informazioni leggendo l&#39;articolo [Configurazione delle pagine di errore CDN](/help/implementing/dispatcher/cdn-error-pages.md).

Tutte queste regole, dichiarate in un file di configurazione nel controllo del codice sorgente, vengono distribuite tramite la pipeline [config](/help/operations/config-pipeline.md) di Cloud Manager. Tieni presente che la dimensione cumulativa del file di configurazione, incluse le regole del filtro del traffico, non può superare i 100 KB.

## Ordine di valutazione {#order-of-evaluation}

Dal punto di vista funzionale, le varie feature menzionate in precedenza vengono valutate nella seguente sequenza:

![Ordine di valutazione](/help/implementing/dispatcher/assets/order.png)

## Configurazione {#initial-setup}

Prima di configurare il traffico sulla rete CDN, è necessario effettuare le seguenti operazioni:

1. Creare un file denominato `cdn.yaml` o simile, facendo riferimento ai vari snippet di configurazione nelle sezioni seguenti.

   Tutti i frammenti hanno queste proprietà comuni, descritte in [Pipeline di configurazione](/help/operations/config-pipeline.md#common-syntax). Il valore della proprietà `kind` deve essere *CDN* e la proprietà `version` deve essere impostata su *1*.

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

La clausola &quot;when&quot; determina se una regola verrà valutata in base a proprietà quali dominio, percorso, stringhe di query, intestazioni e cookie. La sintassi è la stessa per tutti i tipi di regole. Per ulteriori dettagli, vedere la [sezione Struttura condizione](/help/security/traffic-filter-rules-including-waf.md#condition-structure) nell&#39;articolo Regole filtro traffico.

I dettagli del nodo delle azioni differiscono per tipo di regola e sono descritti nelle singole sezioni seguenti.

Nelle regole di configurazione è possibile fare riferimento a segreti definiti come variabili di ambiente (vedere [Segreti di configurazione](/help/implementing/dispatcher/cdn-credentials-authentication.md)).

## Richiedi trasformazioni {#request-transformations}

Le regole di trasformazione delle richieste consentono di modificare le richieste in ingresso. Le regole supportano l’impostazione, la disimpostazione e l’alterazione di percorsi, parametri di query e intestazioni (inclusi i cookie) in base a varie condizioni di corrispondenza, comprese le espressioni regolari. Puoi anche impostare le variabili, a cui è possibile fare riferimento in un secondo momento nella sequenza di valutazione.

I casi d’uso sono vari e includono la riscrittura degli URL per semplificare l’applicazione o mappare gli URL legacy.

Come indicato in precedenza, esiste un limite di dimensione per il file di configurazione, pertanto le organizzazioni con requisiti più grandi devono definire regole nel livello `apache/dispatcher`.

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
      - name: log-on-request
        when: "*"
        actions:
          - type: set
            logProperty: forwarded_host
            value:
              reqHeader: x-forwarded-host
```

**Azioni**

Nella tabella seguente sono illustrate le azioni disponibili.

| Nome | Proprietà | Significato |
|-----------|--------------------------|-------------|
| **set** | reqProperty, value | Imposta un parametro di richiesta specificato (è supportata solo la proprietà &quot;path&quot;) |
|     | reqHeader, value | Imposta un&#39;intestazione di richiesta specificata su un valore specificato. |
|     | queryParam, value | Imposta un parametro di query specificato su un valore specificato. |
|     | reqCookie, value | Imposta un cookie di richiesta specificato su un valore specificato. |
|     | logProperty, value | Imposta una proprietà di registro CDN specificata su un valore specificato. |
|     | var, value | Imposta una variabile specificata su un valore specificato. |
| **non impostato** | reqProperty | Rimuove un parametro di richiesta specificato (è supportata solo la proprietà &quot;path&quot;) |
|     | reqHeader, value | Rimuove un&#39;intestazione di richiesta specificata. |
|     | queryParam, value | Rimuove un parametro di query specificato. |
|     | reqCookie, value | Rimuove un cookie specificato. |
|     | logProperty, value | Rimuove una proprietà di registro CDN specificata. |
|     | var | Rimuove una variabile specificata. |
|     | queryParamMatch | Rimuove tutti i parametri di query che corrispondono a un&#39;espressione regolare specificata. |
|     | queryParamDoesNotMatch | Rimuove tutti i parametri di query che non corrispondono a un&#39;espressione regolare specificata. |
| **trasformazione** | op:replace, (reqProperty o reqHeader o queryParam o reqCookie o var), corrispondenza, sostituzione | Sostituisce parte del parametro di richiesta (supportata solo la proprietà &quot;path&quot;), dell’intestazione di richiesta, del parametro di query, del cookie o della variabile con un nuovo valore. |
|              | op:tolower, (reqProperty o reqHeader o queryParam o reqCookie o var) | Imposta sul valore minuscolo il parametro della richiesta (supportata solo la proprietà &quot;path&quot; ), l&#39;intestazione di richiesta, il parametro di query, il cookie o la variabile. |

Le azioni di sostituzione supportano i gruppi di acquisizione, come illustrato di seguito:

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

Le azioni possono essere concatenate tra loro. Ad esempio:

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

Puoi impostare le variabili durante la trasformazione della richiesta e quindi farvi riferimento in un secondo momento nella sequenza di valutazione. Per ulteriori dettagli, consulta il diagramma dell&#39;[ordine di valutazione](#order-of-evaluation).

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

### Proprietà registro {#logproperty}

Puoi aggiungere proprietà di registro personalizzate nei registri CDN utilizzando le trasformazioni di richiesta e risposta.

Esempio di configurazione:

```
requestTransformations:
  rules:
    - name: log-on-request
      when: "*"
      actions:
        - type: set
          logProperty: forwarded_host
          value:
            reqHeader: x-forwarded-host
responseTransformations:
  rules:
    - name: log-on-response
      when: '*'
      actions:
        - type: set
          logProperty: cache_control
          value:
            respHeader: cache-control
```

Esempio di registro:

```
{
"timestamp": "2025-03-26T09:20:01+0000",
"ttfb": 19,
"cli_ip": "147.160.230.112",
"cli_country": "CH",
"rid": "974e67f6",
"req_ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.3 Safari/605.1.15",
"host": "example.com",
"url": "/content/hello.png",
"method": "GET",
"res_ctype": "image/png",
"cache": "PASS",
"status": 200,
"res_age": 0,
"pop": "PAR",
"rules": "",
"forwarded_host": "example.com",
"cache_control": "max-age=300"
}
```

## Trasformazioni di risposta {#response-transformations}

Le regole di trasformazione della risposta consentono di impostare e annullare l’impostazione di intestazioni, cookie e stato delle risposte in uscita della rete CDN. Inoltre, consulta l’esempio precedente per un riferimento a una variabile precedentemente impostata in una regola di trasformazione della richiesta.

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
      - name: status-code-rule
        when:
          reqProperty: path
          like: status-code
        actions:
          - type: set
            respProperty: status
            value: '410'
      - name: set-response-cookie-with-attributes-as-object
        when: '*'
        actions:
          - type: set
            respCookie: first-name
            value: first-value
            attributes:
              expires: '2025-08-29T10:00:00'
              domain: example.com
              path: /some-path
              secure: true
              httpOnly: true
              extension: ANYTHING
      - name: unset-response-cookie
        when: '*'
        actions:
          - type: unset
            respCookie: third-name
```

**Azioni**

Nella tabella seguente sono illustrate le azioni disponibili.

| Nome | Proprietà | Significato |
|-----------|--------------------------|-------------|
| **set** | respProperty, value | Imposta una proprietà di risposta. Supporta solo la proprietà &quot;status&quot; per impostare il codice di stato. |
|     | respHeader, value | Imposta un&#39;intestazione di risposta specificata su un valore specificato. |
|     | respCookie, attributi (scadenza, dominio, percorso, protetto, httpOnly, estensione), valore | Imposta un cookie di richiesta specificato con attributi specifici a un determinato valore. |
|     | logProperty, value | Imposta una proprietà di registro CDN specificata su un valore specificato. |
|     | var, value | Imposta una variabile specificata su un valore specificato. |
| **non impostato** | respHeader | Rimuove un’intestazione specificata dalla risposta. |
|     | respCookie, value | Rimuove un cookie specificato. |
|     | logProperty, value | Rimuove una proprietà di registro CDN specificata. |
|     | var | Rimuove una variabile specificata. |

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
| **selectOrigin** | originName | Nome di una delle origini definite. |
|     | skipCache (facoltativo, il valore predefinito è false) | Segnala se utilizzare il caching per le richieste che corrispondono a questa regola. Per impostazione predefinita, le risposte vengono memorizzate nella cache in base all’intestazione di memorizzazione nella cache delle risposte (ad esempio, Cache-Control o Expires) |

**Origini**

Le connessioni alle origini sono solo SSL e utilizzano la porta 443.

| Proprietà | Significato |
|------------------|--------------------------------------|
| **nome** | Nome a cui può fare riferimento &quot;action.originName&quot;. |
| **dominio** | Nome di dominio utilizzato per connettersi al back-end personalizzato. Viene utilizzato anche per l’SNI SSL e la convalida. |
| **ip** (facoltativo, supportato iv4 e ipv6) | Se fornito, viene utilizzato per connettersi al backend invece di &quot;dominio&quot;. Tuttavia, &quot;domain&quot; viene utilizzato per l’SNI SSL e la convalida. |
| **forwardHost** (facoltativo, il valore predefinito è false) | Se è impostato su true, l’intestazione &quot;Host&quot; della richiesta client verrà passata al backend, altrimenti il valore &quot;dominio&quot; verrà passato nell’intestazione &quot;Host&quot;. |
| **forwardCookie** (facoltativo, il valore predefinito è false) | Se è impostato su true, l’intestazione &quot;Cookie&quot; della richiesta client verrà passata al backend, altrimenti l’intestazione Cookie viene rimossa. |
| **forwardAuthorization** (facoltativo, il valore predefinito è false) | Se è impostato su true, l’intestazione &quot;Authorization&quot; dalla richiesta del client verrà passata al backend, altrimenti l’intestazione Authorization viene rimossa. |
| **timeout** (facoltativo, in secondi, il valore predefinito è 60) | Numero di secondi in cui la rete CDN deve attendere che un server backend distribuisca il primo byte di un corpo di risposta HTTP. Questo valore viene utilizzato anche come timeout tra i byte per il server back-end. |

### Proxy a Edge Delivery Services {#proxying-to-edge-delivery}

Esistono scenari in cui i selettori di origine devono essere utilizzati per instradare il traffico attraverso AEM Publish ad AEM Edge Delivery Services:

* Alcuni contenuti vengono distribuiti da un dominio gestito da AEM Publish, mentre altri contenuti dello stesso dominio vengono distribuiti da Edge Delivery Services.
* Il contenuto distribuito da Edge Delivery Services trarrebbe vantaggio dalle regole distribuite tramite la pipeline di configurazione, incluse le regole del filtro del traffico o le trasformazioni di richiesta/risposta.
* La pipeline di configurazione di Edge Delivery consente di configurare le impostazioni CDN gestite da Adobe definendo regole quali `trafficFilters`, `originSelectors` e `redirects`. <!-- https://wiki.corp.adobe.com/pages/editpage.action?pageId=3610084282 -->

Di seguito è riportato un esempio di regola del selettore di origine che può eseguire questa operazione:

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
>
>Poiché viene utilizzata la rete CDN gestita di Adobe, assicurarsi di configurare l&#39;annullamento della validità push in modalità **gestita** seguendo la [documentazione sull&#39;annullamento della validità push di Edge Delivery Services](https://www.aem.live/docs/byo-dns#setup-push-invalidation).


## Reindirizzamenti lato server {#server-side-redirectors}

Puoi utilizzare le regole di reindirizzamento lato client per 301, 302 e reindirizzamenti lato client simili. Se una regola corrisponde, la rete CDN risponde con una riga di stato che include il codice di stato e il messaggio (ad esempio, HTTP/1.1 301 Spostato definitivamente), nonché l’intestazione della posizione impostata.

Sono consentite posizioni sia assolute che relative con valori fissi.

Tieni presente che la dimensione cumulativa del file di configurazione, incluse le regole del filtro del traffico, non può superare i 100 KB.

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
| **reindirizzamento** | luogo | Valore per l’intestazione &quot;Posizione&quot;. |
|     | stato (facoltativo, il valore predefinito è 301) | Stato HTTP da utilizzare nel messaggio di reindirizzamento: 301 per impostazione predefinita. I valori consentiti sono: 301, 302, 303, 307, 308. |

Le posizioni di un reindirizzamento possono essere valori letterali stringa (ad esempio, https://www.example.com/page) o il risultato di una proprietà (ad esempio, percorso) che viene facoltativamente trasformata con la seguente sintassi:

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
