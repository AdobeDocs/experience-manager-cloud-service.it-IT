---
title: Configurazione del traffico sulla rete CDN
description: Scopri come configurare il traffico CDN dichiarando regole e filtri in un file di configurazione e distribuendoli nella CDN utilizzando la pipeline di configurazione di Cloud Manager.
feature: Dispatcher
source-git-commit: 0a0c9aa68b192e8e2a612f50a58ba5f9057c862d
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 2%

---


# Configurazione del traffico sulla rete CDN {#cdn-configuring-cloud}

>[!NOTE]
>Questa funzione non è ancora disponibile al pubblico. Per partecipare al programma di adozione anticipata, invia un messaggio e-mail a `aemcs-cdn-config-adopter@adobe.com` e descrivi il tuo caso d’uso.

AEM as a Cloud Service offre una raccolta di funzioni configurabili in [CDN gestito da Adobe](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) che modificano la natura delle richieste in ingresso o delle risposte in uscita. Le seguenti regole, descritte in dettaglio in questa pagina, possono essere dichiarate per ottenere il seguente comportamento:

* [Richiedi trasformazioni](#request-transformations) : modifica gli aspetti delle richieste in entrata, tra cui intestazioni, percorsi e parametri.
* [Trasformazioni di risposta](#response-transformations) : modifica le intestazioni che stanno tornando al client (ad esempio, un browser web).
* [Redirector lato client](#client-side-redirectors) : attiva un reindirizzamento del browser.
* [Selettori di origine](#origin-selectors) : proxy a un back-end di origine diversa.

Nella rete CDN sono configurabili anche le regole del filtro del traffico (incluso WAF), che controllano il traffico consentito o negato dalla rete CDN. Questa funzione è già stata rilasciata e puoi saperne di più nel [Regole del filtro del traffico, incluse le regole WAF](/help/security/traffic-filter-rules-including-waf.md) pagina.

Inoltre, se la rete CDN non è in grado di contattare la relativa origine, puoi scrivere una regola che fa riferimento a una pagina di errore personalizzata con hosting autonomo (di cui viene quindi eseguito il rendering). Per saperne di più, leggi [Configurazione delle pagine di errore CDN](/help/implementing/dispatcher/cdn-error-pages.md) articolo.

Tutte queste regole, dichiarate in un file di configurazione nel controllo del codice sorgente, vengono distribuite utilizzando [Pipeline di configurazione di Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline). Tieni presente che la dimensione cumulativa del file di configurazione non può superare i 100 KB.

## Ordine di valutazione {#order-of-evaluation}

Dal punto di vista funzionale, le varie feature menzionate in precedenza vengono valutate nella seguente sequenza:

![immagine](/help/implementing/dispatcher/assets/order.png)

## Configurazione {#initial-setup}

Prima di configurare il traffico sulla rete CDN, è necessario effettuare le seguenti operazioni:

* Innanzitutto, crea questa cartella e struttura di file nella cartella di livello principale del progetto Git:

```
config/
     cdn.yaml
```

* In secondo luogo, `cdn.yaml` Il file di configurazione deve contenere sia i metadati che le regole descritte negli esempi seguenti.

## Richiedi trasformazioni {#request-transformations}

Le regole di trasformazione delle richieste consentono di modificare le richieste in ingresso. Le regole supportano l’impostazione, la disimpostazione e l’alterazione di percorsi, parametri di query e intestazioni (inclusi i cookie) in base a varie condizioni di corrispondenza, comprese le espressioni regolari. Puoi anche impostare le variabili, a cui è possibile fare riferimento in un secondo momento nella sequenza di valutazione.

I casi d’uso sono vari e includono la riscrittura degli URL per semplificare l’applicazione o mappare gli URL legacy.

Come accennato in precedenza, esiste un limite di dimensione per il file di configurazione, pertanto le organizzazioni con requisiti più grandi devono definire regole nel `apache/dispatcher` livello.

Esempio di configurazione:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["prod", "dev"]
data:  
  experimental_requestTransformations:
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
 
      - name: unset-header-rule
        when:
          reqProperty: path
          like: /unset-header
        actions:
          - type: unset
            reqHeader: x-some-header
 
      - name: set-query-param-rule
        when:
          reqProperty: path
          equals: /set-query-param
        actions:
          - type: set
            queryParam: someParam
            value: someValue
 
      - name: unset-query-param-rule
        when:
          reqProperty: path
          equals: /unset-query-param
        actions:
          - type: unset
            queryParam: someParam
 
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
 
      - name: set-req-cookie-rule
        when:
          reqProperty: path
          equals: /set-req-cookie
        actions:
          - type: set
            reqCookie: someParam
            value: someValue
 
      - name: unset-req-cookie-rule
        when:
          reqProperty: path
          equals: /unset-req-cookie
        actions:
          - type: unset
            reqCookie: someParam
 
      - name: set-variable-rule
        when:
          reqProperty: path
          equals: /set-variable
        actions:
          - type: set
            var: some_var_name
            value: some value
 
      - name: unset-variable-rule
        when:
          reqProperty: path
          equals: /unset-variable
        actions:
          - type: unset
            var: some_var_name
 
      - name: replace-segment
        when:
          reqProperty: path
          like: /replace-segment/*
        actions:
          - type: replace
            reqProperty: path
            match: /replace-segment/
            value: /segment-was-replaced/
 
      - name: replace-extension
        when:
          reqProperty: path
          like: /replace-extension/*.html
        actions:
          - type: replace
            reqProperty: path
            match: \.html
            value: ''
 
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
```

**Azioni**

Nella tabella seguente sono illustrate le azioni disponibili.

| Nome | Proprietà | Significato |
|-----------|--------------------------|-------------|
| **set** | reqHeader, value | Imposta un&#39;intestazione specificata su un valore specificato. |
|     | queryParam, value | Imposta un parametro di query specificato su un valore specificato. |
|     | reqCookie, value | Imposta un cookie specificato su un valore specificato. |
|     | var, value | Imposta una variabile specificata su un valore specificato. |
| **non impostato** | reqHeader | Rimuove un&#39;intestazione specificata. |
|         | queryParam | Rimuove un parametro di query specificato. |
|         | reqCookie | Rimuove un cookie specificato. |
|         | var | Rimuove una variabile specificata. |
|         | queryParamMatch | Rimuove tutti i parametri di query che corrispondono a un&#39;espressione regolare specificata. |
| **replace** | reqProperty, match, value | Sostituisce parte della proprietà della richiesta con un nuovo valore. Attualmente è supportata solo la proprietà &quot;path&quot;. |

### Variabili {#variables}

Puoi impostare le variabili durante la trasformazione della richiesta e quindi farvi riferimento in un secondo momento nella sequenza di valutazione. Consulta la [ordine di valutazione](#order-of-evaluation) per ulteriori dettagli.

Esempio di configurazione:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["prod", "dev"]
data:   
  experimental_requestTransformations:
    rules:
      - name: set-variable-rule
        when:
          reqProperty: path
          equals: /set-variable
        actions:
          - type: set
            var: some_var_name
            value: some_value
 
  experimental_responseTransformations:
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

## Trasformazioni di risposta {#response-transformations}

Le regole di trasformazione delle risposte consentono di impostare e annullare l’impostazione delle intestazioni delle risposte in uscita della rete CDN. Inoltre, consulta l’esempio precedente per un riferimento a una variabile precedentemente impostata in una regola di trasformazione della richiesta.

Esempio di configurazione:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["prod", "dev"]
data:
  experimental_responseTransformations:
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
```

**Azioni**

Nella tabella seguente sono illustrate le azioni disponibili.

| Nome | Proprietà | Significato |
|-----------|--------------------------|-------------|
| **set** | reqHeader, value | Imposta un&#39;intestazione specificata su un valore specificato nella risposta. |
| **non impostato** | respHeader | Rimuove un’intestazione specificata dalla risposta. |

## Selettori di origine {#origin-selectors}

Puoi sfruttare la rete CDN dell’AEM per indirizzare il traffico a diversi backend, incluse le applicazioni non basate su Adobi (ad esempio in base al percorso o al sottodominio).

Esempio di configurazione:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_originSelectors:
    rules:
      - name: example-com
        when: { reqProperty: path, like: /proxy-me* }
        action:
          type: selectOrigin
          originName: example-com
          # useCache: false
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
|     | useCache (facoltativo, il valore predefinito è true) | Segnala se utilizzare il caching per le richieste che corrispondono a questa regola. |

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

## Redirector lato client {#client-side-redirectors}

Puoi utilizzare le regole di reindirizzamento lato client per 301, 302 e reindirizzamenti lato client simili. Se una regola corrisponde, la rete CDN risponde con una riga di stato che include il codice di stato e il messaggio (ad esempio, HTTP/1.1 301 Spostato definitivamente), nonché l’intestazione della posizione impostata.

Sono consentite posizioni sia assolute che relative con valori fissi.

Esempio di configurazione:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_redirects:
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
| **reindirizzare** | luogo | Valore per l’intestazione &quot;Posizione&quot;. |
|     | stato (facoltativo, il valore predefinito è 301) | Stato HTTP da utilizzare nel messaggio di reindirizzamento: 301 per impostazione predefinita. I valori consentiti sono: 301, 302, 303, 307, 308. |
