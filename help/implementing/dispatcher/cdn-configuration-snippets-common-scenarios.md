---
title: Snippet di configurazione CDN per scenari comuni
description: Modelli YAML pronti per la copia per le impostazioni CDN gestite da Adobe e CDN gestite dal cliente, tra cui autenticazione Edge, reindirizzamenti, variazione della cache, traffic shaping e limiti di velocità.
feature: Dispatcher
role: Admin
source-git-commit: ab43facbd4c34c92878e303acf2fef9cc127e28a
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---


# Snippet di configurazione CDN per scenari comuni {#cdn-configuration-snippets}

Questo articolo raccoglie i pattern pratici di `cdn.yaml` per AEM as a Cloud Service. Utilizzale insieme alla documentazione della funzione per [regole traffico CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md), [credenziali CDN gestite dal cliente](/help/implementing/dispatcher/cdn-credentials-authentication.md) e [regole filtro traffico, incluso WAF](/help/security/traffic-filter-rules-including-waf.md). Distribuisci snippet con una pipeline [config](/help/operations/config-pipeline.md) di Cloud Manager.

>[!NOTE]
>
>Sostituisci nomi host, percorsi, intervalli IP, chiavi e soglie con valori corrispondenti al tuo programma. Esegui il test delle modifiche in un ambiente non di produzione prima di promuoverle.

## CDN gestito dal cliente {#customer-managed-cdn}

### Impostazione dell&#39;autenticazione con chiave Edge solo per alcuni domini {#edge-auth-selected-hosts}

Problema: in una [rete CDN gestita dal cliente](/help/implementing/dispatcher/cdn.md#point-to-point-cdn), è necessario applicare l&#39;autenticazione per alcuni nomi host del cliente, mentre altri nomi host che raggiungono la pubblicazione dovrebbero rimanere disponibili senza tale intestazione (ad esempio durante il rollout o quando solo un dominio del marchio è posizionato dietro la rete CDN).

Soluzione: è necessaria l&#39;autenticazione `X-AEM-Edge-Key` solo quando il primo nome host da `X-Forwarded-Host` è uguale al nome host di destinazione (ad esempio `example.com`). La regola utilizza la proprietà di richiesta `forwardedDomain` per eseguire la corrispondenza ed esegue l&#39;azione `authenticate` sull&#39;autenticatore Edge. Sostituisci i nomi host, i nomi degli autenticatori e i segnaposto chiave per il programma.

```yaml
kind: "CDN"
version: "1"
data:
  authentication:
    authenticators:
      - name: edge-key-auth
        type: edge
        edgeKey1: ${{CDN_EDGEKEY_1}}
        edgeKey2: ${{CDN_EDGEKEY_2}}
    rules:
      - name: edge-key-auth-rule
        when: { reqProperty: forwardedDomain, equals: "example.com" }
        action:
          type: authenticate
          authenticator: edge-key-auth
```

### Impostazione dell’autenticazione della chiave Edge per le richieste non provenienti da IP VPN {#edge-auth-trusted-ips}

Problema: configurare l’autenticazione della chiave edge per BYOCDN ma consentire l’accesso diretto al dominio di pubblicazione solo per gli IP VPN

Soluzione: è necessaria l’autenticazione X-AEM-Edge-Key solo quando l’IP del client non è incluso nell’elenco degli IP VPN

```yaml
kind: "CDN"
version: "1"
data:
  authentication:
    authenticators:
      - name: edge-key-auth
        type: edge
        edgeKey1: ${{CDN_EDGEKEY_1}}
        edgeKey2: ${{CDN_EDGEKEY_2}}
    rules:
      - name: edge-key-auth-rule
        when: { reqProperty: clientIp, notIn: ["10.0.0.1", "11.0.0.0/24", "<other VPN IPs>"] }
        action:
          type: authenticate
          authenticator: edge-key-auth
```

## Reindirizzamenti {#redirects}

### Reindirizzamento dal dominio APEX a www {#apex-to-www}

```yaml
kind: "CDN"
version: "1"
data:
 redirects:
   rules:
     - name: non-www-to-www-redirect
       when:
         reqProperty: domain
         doesNotMatch: '^www\.'
       action:
         type: redirect
         status: 301
         location:
           join:
             format: 'https://www.%s%s'
             args:
               - reqProperty: domain
               - reqProperty: url
```

### Modifica della chiave della cache {#cache-key}

La rete CDN non espone un campo &quot;cache key&quot; separato. Poiché l&#39;URL partecipa alla memorizzazione in cache, è possibile dividere le voci della cache modificando l&#39;URL, ad esempio aggiungendo un parametro di query tramite una [trasformazione richiesta](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations).

```yaml
kind: "CDN"
version: "1"
data:
  requestTransformations:
    rules:
      - name: set-request-different-cache-curl
        when:
          allOf:
            - reqProperty: tier
              equals: publish
            - reqHeader: user-agent
              matches: curl
        actions:
          - type: set
            queryParam: cache
            value: 'curl'
```

### Reindirizzamento a un percorso normalizzato {#trailing-slash}

Invia un reindirizzamento permanente quando un browser richiede una barra finale al momento della pubblicazione, ad esempio da `https://www.example.com/path/` a `https://www.example.com/path`.

```yaml
kind: "CDN"
version: "1"
data:
  redirects:
    rules:
      - name: remove-trailing-slash
        when:
          allOf:
            - reqProperty: tier
              equals: publish
            - reqProperty: domain
              equals: www.example.com
            - reqProperty: originalPath
              matches: ^/(.+)/$
        action:
          type: redirect
          status: 301
          location:
            reqProperty: originalPath
            transform:
              - op: replace
                match: ^/(.+)/$
                replacement: https://www.example.com/\1
```

### Estrazione di informazioni da un cookie JSON {#json-cookie}

```yaml
kind: "CDN"
version: "1"
data:
  requestTransformations:
    rules:
      - name: options-response
        when: { reqProperty: tier, equals: publish }
        actions:
        - type: set
          reqHeader: x-mycookie-info
          value:
            reqCookie: mycookie
            transform: 
            - 'base64decode'
            - { op: 'replace', match: '"info":\s*"([^"]*)"', replacement: '\1'} 
```

## Configurazione tra origini {#cross-origin}

### Distribuzione delle richieste di OPTIONS dalla rete CDN {#options-from-cdn}

```yaml
kind: "CDN"
version: "1"
data:
  requestTransformations:
    rules:
      - name: options-response
        when:
          allOf: 
            - { reqProperty: path, like: /mypathi*  }
            - { reqProperty: method, equals: "OPTIONS" }
            - { reqHeader: Origin, equals: "https://example.com" }
        actions:
          - type: respond
            status: 200
            reason: "OK"
            headers:
              content-type: 'text/plain'
              access-control-allow-origin: { reqHeader: Origin }
              access-control-allow-methods: "*"
              access-control-allow-headers: "*"
```

## Filtri di traffico {#traffic-filters}

### Limitazione tariffa ASN {#rate-limit-asn}

Problema: i limiti di velocità per IP possono non rispettare un pattern DDoS (Distributed Denial-of-Service): ogni indirizzo rimane al di sotto della soglia, pertanto il traffico legittimo e abusivo si presenta simile a quello a livello IP.

Soluzione: conteggiare le richieste in base al nome di sistema autonomo (`clientAsName`) in modo che il limiter aggreghi gli host che condividono lo stesso nome di rete. Lo snippet scrive `clientAsName` in una proprietà di registro a ogni richiesta, quindi applica un limite di velocità all&#39;authoring e alla pubblicazione raggruppato per tale valore. Molti utenti possono condividere un ASN (ad esempio un ISP di grandi dimensioni o un’uscita VPN aziendale), quindi ottimizzare i limiti con attenzione e monitorare i registri CDN per i falsi positivi.

```yaml
kind: "CDN"
version: "1"
data:
  requestTransformations:
    rules:
      - name: log-on-request
        when: "*"
        actions:
          - type: set
            logProperty: client_as_name
            value:
              reqProperty: clientAsName
  trafficFilters:
    rules:
    - name: limit-requests-client-as-name
      when:
        reqProperty: tier
        matches: "author|publish"
      rateLimit:
        limit: 60
        window: 10
        penalty: 300
        count: all
        groupBy:
          - reqProperty: clientAsName
      action: block
```
