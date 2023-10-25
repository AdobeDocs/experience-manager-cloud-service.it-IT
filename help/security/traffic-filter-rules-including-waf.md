---
title: Regole del filtro del traffico, incluse le regole WAF
description: Configurazione delle regole del filtro del traffico, incluse le regole WAF (Web Application Firewall)
exl-id: 6a0248ad-1dee-4a3c-91e4-ddbabb28645c
source-git-commit: 221f6df73fe660c6f8dbf79affdccdd081ad3906
workflow-type: tm+mt
source-wordcount: '4210'
ht-degree: 1%

---


# Regole del filtro del traffico, incluse le regole WAF {#traffic-filter-rules-including-waf-rules}

>[!NOTE]
>
>Questa funzione non è ancora disponibile al pubblico. Per aderire al programma di adozione anticipata in corso, invia un messaggio e-mail a **aemcs-waf-adopter@adobe.com**, incluso il nome dell’organizzazione e il contesto relativi al tuo interesse per la funzione.

Le regole del filtro del traffico possono essere utilizzate per bloccare o consentire le richieste a livello CDN, il che può essere utile in scenari come:

* Limitazione dell’accesso a domini specifici al traffico interno dell’azienda, prima della pubblicazione di un nuovo sito
* Stabilire limiti di velocità in modo da essere meno suscettibili ad attacchi DDoS volumetrici
* Impedire che indirizzi IP dannosi eseguano il targeting delle pagine

Alcune di queste regole del filtro del traffico sono disponibili per tutti i clienti AEM as a Cloud Service Sites e Forms. Funzionano principalmente su proprietà di richiesta e intestazioni di richiesta, tra cui IP, nome host, percorso e agente utente.

Una sottocategoria delle regole del filtro del traffico richiede una licenza di protezione avanzata o una licenza di protezione WAF-DDoS Security. Queste potenti regole sono note come regole del filtro del traffico WAF (Web Application Firewall) (o regole WAF in breve) e hanno accesso al [Flag WAF](#waf-flags-list) descritto più avanti in questo articolo. I clienti di Sites e Forms possono contattare il proprio account team di Adobi per informazioni dettagliate sulla concessione in licenza di questa funzionalità avanzata.

Le regole del filtro del traffico possono essere distribuite tramite le pipeline di configurazione di Cloud Manager ai tipi di ambiente di sviluppo, di staging e di produzione nei programmi di produzione (non sandbox). Il supporto per gli RDE arriverà in futuro.

## Organizzazione di questo articolo {#how-organized}

Questo articolo è suddiviso nelle sezioni seguenti:

* **Panoramica sulla protezione del traffico:** Scopri come sei protetto dal traffico dannoso.
* **Processo consigliato per la configurazione delle regole:** Scopri una metodologia di alto livello per proteggere il tuo sito web.
* **Configurazione:** Scopri come impostare, configurare e distribuire le regole del filtro del traffico, incluse le regole WAF avanzate.
* **Sintassi delle regole:** Scopri come dichiarare le regole del filtro del traffico in `cdn.yaml` file di configurazione. Ciò include sia le regole del filtro del traffico disponibili per tutti i clienti Sites e Forms, sia la sottocategoria delle regole WAF per coloro che concedono in licenza tale funzionalità.
* **Esempi di regole:** Consulta alcuni esempi di regole dichiarate per iniziare.
* **Regole limite tasso:** Scopri come utilizzare le regole di limitazione della frequenza per proteggere il sito da attacchi di volumi elevati.
* **Registri CDN:** Scopri quali regole dichiarate e flag WAF corrispondono al tuo traffico.
* **Strumenti dashboard:** Analizza i registri CDN per trovare nuove regole per il filtro del traffico.
* **Esercitazione:** Conoscenza pratica della funzione, incluso come utilizzare gli strumenti del dashboard per dichiarare le regole corrette.
<!-- About the tutorial: sets the context for a linked tutorial, which gives you practical knowledge about the feature, including how to use dashboard tooling to declare the right rules. -->

## Panoramica sulla protezione del traffico {#traffic-protection-overview}

Nel panorama digitale attuale, il traffico dannoso è una minaccia sempre presente. Riconosciamo la gravità del rischio e offriamo diversi approcci per proteggere le applicazioni dei clienti e mitigare gli attacchi quando si verificano.

Al limite, la rete CDN gestita dall&#39;Adobe assorbe gli attacchi DDoS a livello di rete (livelli 3 e 4), inclusi gli attacchi di inondazione e riflessione/amplificazione.

Per impostazione predefinita, Adobe adotta misure per evitare il deterioramento delle prestazioni dovuto a picchi di traffico inaspettatamente elevato oltre una determinata soglia. Nel caso di un attacco DDoS che influisca sulla disponibilità del sito, i team operativi di Adobe vengono avvisati e adottano misure per mitigare gli effetti.

I clienti possono adottare misure proattive per mitigare gli attacchi a livello di applicazione (livello 7) configurando regole a vari livelli del flusso di distribuzione dei contenuti.

Ad esempio, a livello di Apache, i clienti possono configurare [modulo dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-access-to-content-filter) o [ModSecurity](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/modsecurity-crs-dos-attack-protection.html?lang=en) per limitare l’accesso a determinati contenuti.

Come descritto in questo articolo, le regole del filtro del traffico possono essere distribuite alla CDN utilizzando la pipeline di configurazione di Cloud Manager. Oltre alle regole del filtro del traffico basate sulla richiesta di traffico in base a proprietà come indirizzo IP, percorso e intestazioni, i clienti possono anche concedere in licenza una potente sottocategoria di regole del filtro del traffico chiamate regole WAF.

## Processo consigliato {#suggested-process}

Di seguito è riportato un processo end-to-end consigliato di alto livello per individuare le regole per il filtro del traffico corrette:

1. Configurare una pipeline di configurazione non di produzione e di produzione, come descritto in [Configurazione](#setup) sezione.
1. I clienti che hanno concesso in licenza la sottocategoria delle regole del filtro del traffico WAF devono abilitarle in Cloud Manager.
1. Leggi e prova l’esercitazione per comprendere concretamente come utilizzare le regole del filtro del traffico, incluse le regole WAF, se dispongono della licenza. Il tutorial illustra come distribuire le regole in un ambiente di sviluppo, simulare traffico dannoso e scaricare [Registri CDN](#cdn-logs)e analizzarli in [strumenti dashboard](#dashboard-tooling).
1. Copia le regole iniziali consigliate in `cdn.yaml` e implementa la configurazione nell’ambiente di produzione in modalità registro.
1. Dopo aver raccolto del traffico, analizza i risultati utilizzando [strumenti dashboard](#dashboard-tooling) per vedere se ci sono state corrispondenze. Cerca i falsi positivi e apporta le regolazioni necessarie, in ultima analisi abilitando le regole predefinite in modalità blocco.
1. Aggiungi regole personalizzate basate sull’analisi dei registri CDN, eseguendo prima un test con traffico simulato in ambienti di sviluppo, prima della distribuzione nell’ambiente di staging e produzione in modalità registro, quindi in modalità blocco.
1. Monitora il traffico su base continuativa, apportando modifiche alle regole man mano che il panorama delle minacce si evolve.

## Configurazione {#setup}

1. Innanzitutto, crea la cartella e la struttura di file seguenti nella cartella di livello principale del progetto in Git:

   ```
   config/
        cdn.yaml
   ```

1. `cdn.yaml` deve contenere metadati, nonché un elenco di regole dei filtri di traffico e regole WAF.

   ```
   kind: "CDN"
   version: "1"
   metadata:
     envTypes: ["dev"]
   data:
     trafficFilters:
       rules:
       # Block simple path
       - name: block-path
         when:
           allOf:
             - reqProperty: tier
               matches: "author|publish"
             - reqProperty: path
               equals: '/block/me'
         action: block
   ```

Il `kind` il parametro deve essere impostato su `CDN` e la versione deve essere impostata sulla versione dello schema, attualmente `1`. Vedi gli esempi di seguito.


<!-- Two properties -- `envType` and `envId` -- may be included to limit the scope of the rules. The envType property may have values "dev", "stage", or "prod", while the envId property is the environment (e.g., "53245"). This approach is useful if it is desired to have a single configuration pipeline, even if some environments have different rules. However, a different approach could be to have multiple configuration pipelines, each pointing to different repositories or git branches. -->

1. Per configurare le regole WAF, è necessario che WAF sia abilitato in Cloud Manager, come descritto di seguito per gli scenari di programma nuovi ed esistenti. Si noti che per WAF deve essere acquistata una licenza separata.

   1. Per configurare WAF per un nuovo programma, selezionare **Protezione WAF-DDOS** casella di controllo sulla **Sicurezza** scheda quando [aggiungi un programma di produzione.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)

   1. Per configurare WAF su un programma esistente: [modifica del programma](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) e il **Sicurezza** deselezionare o selezionare la scheda **WAF-DDOS** in qualsiasi momento.

1. Per tipi di ambiente diversi da RDE, crea una pipeline di configurazione della distribuzione di destinazione in Cloud Manager.

   * [Consulta questo documento per le pipeline di produzione.](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)
   * [Consulta questo documento per le pipeline non di produzione.](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)

Per gli RDE verrà utilizzata la riga di comando, ma al momento RDE non è supportato.

## Sintassi delle regole del filtro del traffico {#rules-syntax}

Puoi configurare `traffic filter rules` affinché corrisponda a pattern quali IP, agente utente, intestazioni di richiesta, nome host, geo e url.

I clienti che dispongono di una licenza per l&#39;offerta Sicurezza avanzata o Protezione WAF-DDoS possono anche configurare una categoria speciale di regole per il filtro del traffico denominata `WAF traffic filter rules` (o regole WAF in breve) che fanno riferimento a una o più [Flag WAF](#waf-flags-list).

Di seguito è riportato un esempio di un set di regole per il filtro del traffico, che include anche una regola WAF.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when: { reqProperty: path, equals: /block-me }
        action:
          type: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS]
```

Il formato delle regole del filtro del traffico nel `cdn.yaml` Il file è descritto di seguito. Vedi un po&#39; [altri esempi](#examples) in una sezione successiva, nonché in una sezione separata su [Regole di limite di tasso](#rate-limit-rules).


| **Proprietà** | **Regole filtro traffico più frequenti** | **Regole filtro traffico WAF** | **Tipo** | **Valore predefinito** | **Descrizione** |
|---|---|---|---|---|---|
| name | X | X | `string` | - | Nome regola (64 caratteri, può contenere solo caratteri alfanumerici e - ) |
| quando | X | X | `Condition` | - | La struttura di base è:<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>[Consulta Sintassi della struttura delle condizioni](#condition-structure) di seguito, che descrive i getter, i predicati e come combinare più condizioni. |
| azione | X | X | `Action` | log | log, allow, block, log o action object Il valore predefinito è log |
| rateLimit | X |   | `RateLimit` | non definito | Configurazione del limite di frequenza. La limitazione della frequenza è disabilitata se non definita.<br><br>Di seguito è riportata una sezione separata che descrive la sintassi rateLimit, con alcuni esempi. |

### Struttura della condizione {#condition-structure}

Una condizione può essere una condizione semplice o un gruppo di condizioni.

**Condizione semplice**

Una condizione semplice è composta da un getter e da un predicato.

```
{ <getter>: <value>, <predicate>: <value> }
```

**Condizioni gruppo**

Un gruppo di condizioni è composto da più condizioni semplici e/o di gruppo.

```
<allOf|anyOf>:
  - { <getter>: <value>, <predicate>: <value> }
  - { <getter>: <value>, <predicate>: <value> }
  - <allOf|anyOf>:
    - { <getter>: <value>, <predicate>: <value> }
```

| **Proprietà** | **Tipo** | **Significato** |
|---|---|---|
| **allOf** | `array[Condition]` | **e** operazione. true se tutte le condizioni elencate restituiscono true |
| **anyOf** | `array[Condition]` | **o** operazione. true se una qualsiasi delle condizioni elencate restituisce true |

**Recuperatore**

| **Proprietà** | **Tipo** | **Descrizione** |
|---|---|---|
| reqProperty | `string` | Proprietà richiesta.<br><br>Uno di: `path` , `queryString`, `method`, `tier`, `domain`, `clientIp`, `clientCountry`<br><br>La proprietà domain è una trasformazione in minuscolo dell’intestazione host della richiesta. È utile per i confronti tra stringhe, pertanto le corrispondenze non vengono perse a causa della distinzione tra maiuscole e minuscole.<br><br>Il `clientCountry` utilizza due codici di lettera visualizzati in [https://en.wikipedia.org/wiki/Regional_indicator_symbol](https://en.wikipedia.org/wiki/Regional_indicator_symbol) |
| reqHeader | `string` | Restituisce l’intestazione della richiesta con il nome specificato |
| queryParam | `string` | Restituisce il parametro di query con il nome specificato |
| reqCookie | `string` | Restituisce il cookie con il nome specificato |
| postParam | `string` | Restituisce il parametro con il nome specificato dal corpo. Funziona solo quando il corpo è di tipo contenuto `application/x-www-form-urlencoded` |

**Predicato**

| **Proprietà** | **Tipo** | **Significato** |
|---|---|---|
| **è uguale a** | `string` | true se il risultato del getter è uguale al valore specificato |
| **doesNotEqual** | `string` | true se il risultato del getter non è uguale al valore specificato |
| **mi piace** | `string` | true se il risultato del getter corrisponde al pattern specificato |
| **notLike** | `string` | true se il risultato del getter non corrisponde al pattern specificato |
| **matches** | `string` | true se il risultato del getter corrisponde a regex fornito |
| **doesNotMatch** | `string` | true se il risultato del getter non corrisponde al regex specificato |
| **in** | `array[string]` | true se l’elenco fornito contiene un risultato getter |
| **notIn** | `array[string]` | true se l’elenco fornito non contiene il risultato getter |
| **esiste** | `boolean` | true se è impostata su true e la proprietà esiste o se è impostata su false e la proprietà non esiste |

### Struttura azione {#action-structure}

Specificato da `action` può essere una stringa che specifica il tipo di azione (consenti, blocco, registro) e che assume i valori predefiniti per tutte le altre opzioni oppure un oggetto in cui il tipo di regola è definito tramite `type` campo obbligatorio insieme ad altre opzioni applicabili a quel tipo.

**Tipi di azioni**

Nella tabella seguente, che viene ordinata in base all’ordine di esecuzione delle azioni, le azioni hanno una priorità in base al loro tipo:

| **Nome** | **Proprietà consentite** | **Significato** |
|---|---|---|
| **consenti** | `wafFlags` (facoltativo) | se wafFlags non è presente, interrompe l&#39;ulteriore elaborazione della regola e passa alla risposta. Se wafFlags è presente, disabilita le protezioni WAF specificate e procede all&#39;ulteriore elaborazione delle regole. |
| **blocco** | `status, wafFlags` (facoltativo e reciprocamente esclusivo) | se wafFlags non è presente, restituisce un errore HTTP ignorando tutte le altre proprietà. Il codice di errore viene definito dalla proprietà status oppure viene impostato automaticamente su 406. Se wafFlags è presente, abilita le protezioni WAF specificate e procede all&#39;ulteriore elaborazione delle regole. |
| **log** | `wafFlags` (facoltativo) | registra il fatto che la regola è stata attivata, altrimenti non influisce sull’elaborazione. wafFlags non ha alcun effetto |

### Elenco flag WAF {#waf-flags-list}

Il `wafFlags` La proprietà, che può essere utilizzata nelle regole del filtro del traffico WAF su licenza, può fare riferimento a quanto segue:

| **ID contrassegno** | **Nome contrassegno** | **Descrizione** |
|---|---|---|
| SQLI | SQL Injection | SQL Injection è il tentativo di accedere a un&#39;applicazione o di ottenere informazioni con privilegi tramite l&#39;esecuzione di query arbitrarie nel database. |
| BACKDOOR | Backdoor | Un segnale backdoor è una richiesta che tenta di determinare se un file backdoor comune è presente sul sistema. |
| CMDEXE | Esecuzione comando | Esecuzione comando è il tentativo di ottenere il controllo o danneggiare un sistema di destinazione attraverso comandi arbitrari di sistema mediante l&#39;input dell&#39;utente. |
| XSS | Scripting tra siti | Per vulnerabilità cross-site scripting si intende il tentativo di dirottare l’account o la sessione di navigazione web di un utente attraverso codice JavaScript dannoso. |
| ATTRAVERSAMENTO | Directory Traversal | Directory Traversal è il tentativo di spostarsi tra le cartelle privilegiate all&#39;interno di un sistema nella speranza di ottenere informazioni riservate. |
| USERAGENT | Attrezzatura attacco | Attack Tooling è l&#39;uso di software automatizzato per identificare le vulnerabilità di sicurezza o per tentare di sfruttare una vulnerabilità scoperta. |
| LOG4J-JNDI | JNDI Log4J | Gli attacchi JNDI Log4J tentano di sfruttare il [Vulnerabilità Log4Shell](https://en.wikipedia.org/wiki/Log4Shell) presente nelle versioni Log4J precedenti alla 2.16.0 |
| BHH | Intestazioni hop non valide | Le intestazioni hop non valide indicano un tentativo di contrabbando HTTP tramite un&#39;intestazione di codifica di trasferimento (TE) o lunghezza dei contenuti (CL) non valida oppure tramite un&#39;intestazione TE e CL ben formata |
| PERCORSO ANOMALO | Percorso anormale | Percorso anormale indica che il percorso originale è diverso dal percorso normalizzato (ad esempio, `/foo/./bar` è normalizzato su `/foo/bar`) |
| DOUBLEENCODING | Doppia codifica | La doppia codifica verifica la tecnica di evasione dei caratteri HTML a doppia codifica |
| NOTUTF8 | Codifica non valida | Una codifica non valida può causare la conversione di caratteri dannosi da una richiesta a una risposta da parte del server, causando un rifiuto del servizio o XSS |
| ERRORE JSON | Errore di codifica JSON | Corpo della richiesta POST, PUT o PATCH specificato come contenente JSON nell’intestazione della richiesta &quot;Content-Type&quot;, ma contenente errori di analisi JSON. Questo è spesso correlato a un errore di programmazione o a una richiesta automatizzata o dannosa. |
| DATI NON VALIDI | Dati non validi nel corpo della richiesta | Corpo della richiesta POST, PUT o PATCH non valido in base all’intestazione della richiesta &quot;Content-Type&quot;. Ad esempio, se è specificata un’intestazione di richiesta &quot;Content-Type: application/x-www-form-urlencoded&quot; e contiene un corpo POST che è json. Spesso si tratta di un errore di programmazione, richiesta automatizzata o dannosa. Richiede l&#39;agente 3.2 o versione successiva. |
| SAN | Traffico IP dannoso | [SANS Internet Storm Center](https://isc.sans.edu/) elenco di indirizzi IP che sono stati segnalati come coinvolti in attività dannose |
| SIGSCI-IP | Effetto di rete | IP contrassegnato da SignalSciences: ogni volta che un IP viene contrassegnato a causa di un segnale dannoso da parte del motore decisionale, tale IP verrà propagato a tutti i clienti. Vengono quindi registrate le richieste successive dagli indirizzi IP che contengono un segnale aggiuntivo per la durata del flag |
| NO-CONTENT-TYPE | Intestazione di richiesta &quot;Content-Type&quot; mancante | Una richiesta POST, PUT o PATCH senza intestazione di richiesta &quot;Content-Type&quot;. Per impostazione predefinita, i server applicazioni devono assumere in questo caso &quot;Content-Type: text/plain; charset=us-ascii&quot;. In molte richieste automatizzate e dannose potrebbe mancare il &quot;Tipo di contenuto&quot;. |
| SOSTANTIVO | Nessun agente utente | Molte richieste automatizzate e dannose utilizzano agenti utente falsi o mancanti per rendere difficile identificare il tipo di dispositivo che effettua le richieste. |
| TORNODO | Traffico Tor | Tor è un software che nasconde l&#39;identità di un utente. Un picco nel traffico di Tor può indicare che un aggressore sta cercando di mascherare la sua posizione. |
| NULLBYTE | Byte Null | I byte Null non vengono in genere visualizzati in una richiesta e indicano che la richiesta è in formato non corretto e potenzialmente dannoso. |
| PRIVATEFILE | File privati | I file privati sono di solito di natura riservata, ad esempio un Apache `.htaccess` o un file di configurazione che potrebbe causare la perdita di informazioni riservate |
| SCANNER | Scanner | Identifica i servizi e gli strumenti di scansione più diffusi |
| RESPONSESPLIT | Suddivisione risposta HTTP | Identifica quando i caratteri CRLF vengono inviati come input all’applicazione per inserire le intestazioni nella risposta HTTP |
| XML-ERROR | Errore di codifica XML | Corpo della richiesta POST, PUT o PATCH specificato come contenente XML nell&#39;intestazione della richiesta &quot;Content-Type&quot;, ma contenente errori di analisi XML. Questo è spesso correlato a un errore di programmazione o a una richiesta automatizzata o dannosa. |

## Considerazioni {#considerations}

* Quando vengono create due regole in conflitto, le regole consentite avranno sempre la precedenza sulle regole del blocco. Ad esempio, se crei una regola per bloccare un percorso specifico e una regola per consentire un indirizzo IP specifico, le richieste provenienti da tale indirizzo IP sul percorso bloccato saranno consentite.

* Se una regola viene rilevata e bloccata, la rete CDN risponde con un `406` codice restituito.

* I file di configurazione non devono contenere segreti, in quanto potrebbero essere letti da chiunque abbia accesso all’archivio Git.

## Esempi di regole {#examples}

Di seguito sono riportati alcuni esempi di regole. Consulta la [sezione limite di tasso](#rules-with-rate-limits) ulteriori informazioni su esempi di regole relative ai limiti tariffari.

**Esempio 1**

Questa regola blocca le richieste provenienti da IP 192.168.1.1:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
     rules:
       - name: "block-request-from-ip"
         when: { reqProperty: clientIp, equals: "192.168.1.1" }
         action:
           type: block
```

**Esempio 2**

Questa regola blocca le richieste nel percorso `/helloworld` al momento della pubblicazione con un agente utente contenente Chrome:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "block-request-from-chrome-on-path-helloworld-for-publish-tier"
        when:
          allOf:
          - { reqProperty: path, equals: /helloworld }
          - { reqProperty: tier, equals: publish }
          - { reqHeader: user-agent, matches: '.*Chrome.*'  }
        action:
          type: block
```

**Esempio 3**

Questa regola blocca le richieste che contengono il parametro di query `foo`, ma consente ogni richiesta proveniente da IP 192.168.1.1:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "block-request-that-contains-query-parameter-foo"
        when: { queryParam: url-param, equals: foo }
        action:
          type: block
      - name: "allow-all-requests-from-ip"
        when: { reqProperty: clientIp, equals: 192.168.1.1 }
        action:
          type: allow
```

**Esempio 4**

Questa regola blocca le richieste al percorso `/block-me`, e blocca ogni richiesta che corrisponde a `SQLI` o `XSS` pattern. Questo esempio include le regole di filtro del traffico WAF, che fanno riferimento al `SQLI` e `XSS` [Flag WAF](#waf-flags-list), che richiedono una licenza separata.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when: { reqProperty: path, equals: /block-me }
        action:
          type: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS]
```

**Esempio 5**

Questa regola blocca l’accesso ai paesi OFAC:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: block-ofac-countries
        when:
          allOf:
            - reqProperty: tier
              matches: "author|publish"
            - reqProperty: clientCountry
              in:
                - SY
                - BY
                - MM
                - KP
                - IQ
                - CD
                - SD
                - IR
                - LR
                - ZW
                - CU
                - CI
        action: block
```

## Regole di limite di tasso {#rate-limits-rules}

A volte è auspicabile bloccare il traffico che corrisponde a una regola solo se la corrispondenza supera una determinata velocità nel tempo. Impostazione di un valore per `rateLimit` limita la frequenza delle richieste che corrispondono alla condizione della regola.

Le regole del limite di tasso non possono fare riferimento ai flag WAF. Sono disponibili per tutti i clienti Sites e Forms.

### struttura rateLimit {#ratelimit-structure}

| **Proprietà** | **Tipo** | **Predefiniti** | **SIGNIFICATO** |
|---|---|---|---|
| limit | numero intero da 10 a 10000 | obbligatorio | Frequenza richieste (per POP CDN) nelle richieste al secondo per le quali viene attivata la regola. |
| finestra | numero intero: 1, 10 o 60 | 10 | Finestra di campionamento in secondi per la quale viene calcolata la frequenza di richiesta. |
| penalità | numero intero compreso tra 60 e 3600 | 300 (5 minuti) | Un periodo in secondi per il quale le richieste corrispondenti vengono bloccate (arrotondato al minuto più vicino). |
| groupBy | array[Recuperatore] | nessuno | il contatore del limitatore di velocità verrà aggregato da un set di proprietà di richiesta (ad esempio clientIp). |

### Esempi {#ratelimiting-examples}

**Esempio 1**

Questa regola blocca un client per 5 m quando supera i 100 req/sec (per POP CDN) negli ultimi 60 sec:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
    - name: limit-requests-client-ip
      when:
        reqProperty: tier
        matches: "author|publish"
      rateLimit:
        limit: 60
        window: 10
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: block
```

**Esempio 2**

Blocca le richieste per gli anni 60 nel percorso /critical/resource quando supera i 100 req/sec (per POP CDN) negli ultimi 60 secondi:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: rate-limit-example
        when: { reqProperty: path, equals: /critical/resource }
        action:
          type: block
        rateLimit: { limit: 100, window: 60, penalty: 60 }
```

## Registri CDN {#cdn-logs}

AEM as a Cloud Service fornisce accesso ai registri CDN, utili per i casi d’uso, tra cui l’ottimizzazione del rapporto hit della cache e la configurazione delle regole CDN e WAF. I registri CDN vengono visualizzati in Cloud Manager **Scarica registri** durante la selezione del servizio Author o Publish.

I registri CDN possono subire un ritardo fino a 5 minuti.

Il `rules` La proprietà descrive le regole del filtro del traffico corrispondenti e presenta il seguente pattern:

```
"rules": "match=<matching-customer-named-rules-that-are-matched>,waf=<matching-WAF-rules>,action=<action_type>"
```

Ad esempio:

```
"rules": "match=Block-Traffic-under-private-folder,Enable-SQL-injection-everywhere,waf="SQLI,SANS",action=block"
```

Le regole si comportano nel modo seguente:

* Il nome della regola dichiarato dal cliente di qualsiasi regola corrispondente verrà elencato nell&#39;attributo matches.
* L’attributo action specifica se le regole hanno avuto l’effetto di bloccare, consentire o registrare.
* Se WAF è concesso in licenza e abilitato, l&#39;attributo waf elencherà tutte le regole waf rilevate, ad esempio SQLI; si noti che questo è indipendente dal nome dichiarato dal cliente, indipendentemente dal fatto che le regole waf siano elencate o meno nella configurazione.
* Se nessuna regola dichiarata dal cliente corrisponde e nessuna regola waf corrisponde, la proprietà dell&#39;attributo delle regole sarà vuota.

In generale, le regole corrispondenti vengono visualizzate nella voce di registro per tutte le richieste alla rete CDN, indipendentemente dal fatto che si tratti di un hit, di un superamento o di un mancato recapito della rete CDN. Tuttavia, le regole WAF vengono visualizzate nella voce di registro solo per le richieste alla rete CDN considerate mancanti o passate alla rete CDN, ma non per gli hit della rete CDN.

L’esempio seguente mostra un esempio `cdn.yaml` e due voci di registro CDN:


```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when: { reqProperty: path, equals: /block-me }
        action: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS ]
```

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cli_ip": "147.160.230.112",
"cli_country": "CH",
"rid": "974e67f6",
"req_ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.3 Safari/605.1.15",
"host": "example.com",
"url": "/block-me",
"method": "GET",
"res_ctype": "",
"cache": "PASS",
"status": 406,
"res_age": 0,
"pop": "PAR",
"rules": "match=path-rule,action=blocked"
}
```

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cli_ip": "147.160.230.112",
"cli_country": "CH",
"req_ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.3 Safari/605.1.15",
"rid": "974e67f6",
"host": "example.com",
"url": "/?sqli=%27%29%20UNION%20ALL%20SELECT%20NULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL--%20fAPK",
"method": "GET",
"res_ctype": "image/png",
"cache": "PASS",
"status": 406,
"res_age": 0,
"pop": "PAR",
"rules": "match=Enable-SQL-Injection-and-XSS-waf-rules-globally,waf=SQLI,action=blocked"
}
```

### Formato registro {#cdn-log-format}

Di seguito è riportato un elenco dei nomi dei campi utilizzati nei registri CDN, con una breve descrizione.

| **Nome campo** | **Descrizione** |
|---|---|
| *timestamp* | L’ora di inizio della richiesta, dopo la cessazione di TLS. |
| *ttfb* | Abbreviazione per *Tempo al primo byte*. L’intervallo di tempo tra la richiesta iniziata fino al punto prima che il corpo della risposta iniziasse a essere trasmesso in streaming. |
| *cli_ip* | Indirizzo IP del client. |
| *cli_country* | Due lettere [ISO 3166-1](https://en.wikipedia.org/wiki/ISO_3166-1) codice paese alfa-2 per il paese cliente. |
| *rid* | Il valore dell’intestazione della richiesta utilizzata per identificare in modo univoco la richiesta. |
| *req_ua* | L’agente utente responsabile di effettuare una determinata richiesta HTTP. |
| *host* | Autorità a cui è destinata la richiesta. |
| *url* | Il percorso completo, inclusi i parametri di query. |
| *metodo* | Metodo HTTP inviato dal client, ad esempio &quot;GET&quot; o &quot;POST&quot;. |
| *res_ctype* | Tipo di contenuto utilizzato per indicare il tipo di file multimediale originale della risorsa. |
| *cache* | Stato della cache. I valori possibili sono HIT, MISS o PASS |
| *stato* | Il codice di stato HTTP come valore intero. |
| *res_age* | Il tempo (in secondi) per cui una risposta è stata memorizzata nella cache (in tutti i nodi). |
| *pop* | Datacenter del server cache CDN. |
| *regole* | Nome di eventuali regole corrispondenti.<br><br>Indica anche se la corrispondenza ha prodotto un blocco. <br><br>Ad esempio, &quot;`match=Enable-SQL-Injection-and-XSS-waf-rules-globally,waf=SQLI,action=blocked`&quot;<br><br>Vuoto se non corrisponde alcuna regola. |

## Strumenti dashboard {#dashboard-tooling}

Adobe fornisce un meccanismo per scaricare gli strumenti del dashboard sul computer per acquisire i registri CDN scaricati tramite Cloud Manager. Con questo strumento, puoi analizzare il traffico per scoprire le regole del filtro del traffico da dichiarare, incluse le regole WAF.

Gli strumenti del dashboard possono essere clonati direttamente dal [AEMCS-CDN-Log-Analysis-ELK-Tool](https://github.com/adobe/AEMCS-CDN-Log-Analysis-ELK-Tool) Archivio Github.

[Guarda il tutorial](#tutorial) per istruzioni concrete su come utilizzare gli strumenti del dashboard.

## Tutorial {#tutorial}

Adobe fornisce un meccanismo per scaricare gli strumenti del dashboard sul computer per acquisire i registri CDN scaricati tramite Cloud Manager. Con questo strumento, puoi analizzare il traffico per scoprire le regole del filtro del traffico da dichiarare, incluse le regole WAF. Questa sezione fornisce innanzitutto alcune istruzioni per acquisire familiarità con gli strumenti del dashboard in un ambiente di sviluppo, seguite da indicazioni su come sfruttare tali conoscenze per creare regole in un ambiente di produzione.

Gli strumenti del dashboard possono essere clonati direttamente dal [AEMCS-CDN-Log-Analysis-ELK-Tool](https://github.com/adobe/AEMCS-CDN-Log-Analysis-ELK-Tool) Archivio GitHub.


### Introduzione agli strumenti del dashboard {#dashboard-getting-familiar}

1. Crea una pipeline di configurazione non di produzione di Cloud Manager, associata a un ambiente di sviluppo. Seleziona innanzitutto il **Pipeline di implementazione** opzione. Quindi seleziona **Distribuzione mirata**, Config, l’archivio, il ramo Git e imposta la posizione del codice su /config.

   ![Aggiungi implementazione di selezione pipeline non di produzione](/help/security/assets/waf-select-pipeline1.png)

   ![Aggiungi destinazione di selezione pipeline non di produzione](/help/security/assets/waf-select-pipeline2.png)

[Consulta questo documento per informazioni dettagliate sulla configurazione di pipeline non di produzione.](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)

1. Nel workspace, crea una configurazione di cartella a livello principale e aggiungi un file denominato `cdn.yaml`, in cui dichiarerai una regola semplice, impostandola in modalità registro anziché in modalità di blocco.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
    # Log request on simple path
    - name: log-rule-example
      when:
        allOf:
          - reqProperty: tier
            matches: "author|publish"
          - reqProperty: path
            equals: '/log/me'
      action: log
```

1. Apporta e invia le modifiche e distribuisci la configurazione utilizzando la pipeline di configurazione.

   ![Eseguire la pipeline di configurazione](/help/security/assets/waf-run-pipeline.png)

1. Una volta implementata la configurazione, prova ad accedere `https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me` utilizzando il browser web o con il comando curl di seguito. Dovresti ricevere una pagina di errore 404 in quanto tale pagina non esiste.

   ```
   curl -svo /dev/null https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me
   ```

1. Scarica i registri CDN da Cloud Manager e verifica che le regole corrispondano come previsto, con una proprietà delle regole corrispondente al nome della regola:

   ```
   "rules": "match=log-rule-example"
   ```

   ![Seleziona i registri di download](/help/security/assets/waf-download-logs1.png)

   ![Scaricare i registri](/help/security/assets/waf-download-logs2.png)

1. Carica l’immagine Docker con gli strumenti del dashboard e segui il file README per acquisire i registri CDN. Come illustrato nelle schermate seguenti, seleziona il periodo di tempo corretto, l’ambiente giusto e i filtri giusti.

   ![Seleziona l’ora dal dashboard](/help/security/assets/dashboard-select-time.png)

   ![Seleziona l’ambiente dal dashboard](/help/security/assets/dashboard-select-env.png)

1. Una volta applicati i filtri corretti, dovresti essere in grado di visualizzare una dashboard caricata con i dati previsti. Nella schermata seguente, l’esempio della regola di registro è stato attivato 3 volte nelle ultime 2 ore, dallo stesso IP che si trova in Irlanda, utilizzando un browser web e curl.

   ![Visualizzare i dati del dashboard di sviluppo](/help/security/assets/dashboard-see-data-logmode.png)
   ![Visualizza widget dati dashboard di sviluppo](/help/security/assets/dashboard-see-data-logmode2.png)

1. Ora modifica il file cdn.yaml in modo da attivare la regola in modalità di blocco per garantire che le pagine siano bloccate, come previsto. Quindi esegui il commit, invia e attiva la pipeline di configurazione come fatto in precedenza.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
    # Log request on simple path
    - name: log-rule-example
      when:
        allOf:
          - reqProperty: tier
            matches: "author|publish"
          - reqProperty: path
            equals: '/log/me'
      action: block
```

1. Una volta implementata la configurazione, prova ad accedere `https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me` utilizzando il browser web o con il comando curl di seguito. Dovresti ricevere una pagina di errore 406 che indica che la richiesta è stata bloccata.

   ```
   curl -svo /dev/null https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me
   ```

1. Ancora una volta, scarica i registri CDN in Cloud Manager (nota: l’esposizione delle nuove richieste nei registri CDN può richiedere fino a 5 minuti) e importali negli strumenti della dashboard, come abbiamo fatto in precedenza. Al termine, aggiorna la dashboard. Come puoi vedere nella schermata seguente, le richieste a `/log/me` sono bloccati dalla nostra regola.

   ![Visualizza dati dashboard di produzione](/help/security/assets/dashboard-see-data-blockmode.png)
   ![Visualizza dati dashboard di produzione](/help/security/assets/dashboard-see-data-blockmode2.png)

1. Se sono abilitati dei filtri del traffico WAF (questo richiederà una licenza aggiuntiva quando la funzione sarà GA), ripeti con una regola del filtro del traffico WAF, in modalità registro, e distribuisci le regole.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: log-waf-flags
        when:
          reqProperty: tier
          matches: "author|publish"
        action:
          type: log
          wafFlags:
              - SANS
              - SIGSCI-IP
              - TORNODE
              - NOUA
              - SCANNER
              - USERAGENT
              - PRIVATEFILE
              - ABNORMALPATH
              - TRAVERSAL
              - NULLBYTE
              - BACKDOOR
              - LOG4J-JNDI
              - SQLI
              - XSS
              - CODEINJECTION
              - CMDEXE
              - NO-CONTENT-TYPE
              - UTF8
```

1. Utilizza uno strumento come [nikto](https://github.com/sullo/nikto/tree/master) per generare richieste corrispondenti. Il comando seguente invierà circa 550 richieste dannose in meno di 1 minuto.

   ```
   ./nikto.pl -useragent "MyAgent (Demo/1.0)" -D V -Tuning 9 -ssl -h https://publish-pXXXXX-eYYYYY.adobeaemcloud.com
   ```

1. Scarica i registri CDN da Cloud Manager (la visualizzazione potrebbe richiedere fino a 5 minuti) e verifica che vengano visualizzate sia le regole dichiarate corrispondenti che i flag WAF.

   Come si può vedere, molte delle richieste prodotte da Nikto vengono segnalate dalla WAF come maligne. Possiamo vedere che Nikto ha provato a sfruttare le vulnerabilità CMDEXE, SQLI e NULLBYTE. Se ora modifichi l’azione da registro a blocco e riattivi una scansione utilizzando Nikto, tutte le richieste precedentemente segnalate verranno bloccate questa volta.

   ![Visualizza dati WAF](/help/security/assets/dashboard-see-data-waf.png)


   Tieni presente che ogni volta che una richiesta corrisponde a uno dei flag WAF, tali flag WAF verranno visualizzati, anche se non fanno parte della regola dichiarata; in questo modo sei sempre a conoscenza di traffico potenzialmente nuovo, per il quale non hai ancora dichiarato regole corrispondenti. Ad esempio:

   ```
   "rules": "match=log-waf-flags,waf=SQLI,action=blocked"
   ```

1. Ripeti con una regola che utilizza la limitazione della frequenza, in modalità registro. Come sempre, esegui il commit, invia e attiva la pipeline di configurazione per applicare la configurazione.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: limit-requests-client-ip
        when:
          reqProperty: tier
          matches: "author|publish"
        rateLimit:
          limit: 10
          window: 1
          penalty: 60
          groupBy:
            - reqProperty: clientIp
        action: log
```

1. Utilizza uno strumento come [Vegeta](https://github.com/tsenart/vegeta) per generare il traffico.

   ```
   echo "GET https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com" | vegeta attack -duration=5s | tee results.bin | vegeta report
   ```

1. Dopo aver eseguito lo strumento, puoi scaricare i registri CDN e acquisirli nel dashboard per verificare che la regola del limitatore di velocità sia stata attivata

   ![Visualizza dati WAF](/help/security/assets/waf-dashboard-ratelimiter-1.png)

   ![Visualizza dati WAF](/help/security/assets/waf-dashboard-ratelimiter-2.png)

   Come puoi vedere la nostra regola **limit-requests-client-ip** è stato attivato.

   Ora che conosci il funzionamento delle regole del filtro del traffico, puoi passare all’ambiente di produzione.

### Distribuzione di regole nell’ambiente di produzione {#dashboard-prod-env}

Assicurati di dichiarare inizialmente le regole in modalità registro per verificare che non vi siano falsi positivi, il che significa traffico legittimo che verrebbe bloccato in modo errato.

1. Crea una pipeline di configurazione di produzione associata all’ambiente di produzione.

1. Copia le regole consigliate di seguito nel tuo cdn.yaml. Puoi modificare le regole in base alle caratteristiche univoche del traffico live del tuo sito web. Esegui il commit, invia e attiva la pipeline di configurazione. Assicurati che le regole siano in modalità registro.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
    #  Block client for 5m when it exceeds 100 req/sec on a time window of 1sec
    - name: limit-requests-client-ip
      when:
        reqProperty: path
        like: '*'
      rateLimit:
        limit: 100
        window: 1
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: log
    # Block requests coming from OFAC countries
    - name: block-ofac-countries
      when:
        allOf:
          - { reqProperty: tier, equals: publish }
          - reqProperty: clientCountry
            in:
              - SY
              - BY
              - MM
              - KP
              - IQ
              - CD
              - SD
              - IR
              - LR
              - ZW
              - CU
              - CI
      action: log
    # Enable recommended WAF protections (only works if WAF is enabled for your environment)
    - name: block-waf-flags-globally
      when:
        reqProperty: tier
        matches: "author|publish"
      action:
        type: log
        wafFlags:
          - SANS
          - SIGSCI-IP
          - TORNODE
          - NOUA
          - SCANNER
          - USERAGENT
          - PRIVATEFILE
          - ABNORMALPATH
          - TRAVERSAL
          - NULLBYTE
          - BACKDOOR
          - LOG4J-JNDI
          - SQLI
          - XSS
          - CODEINJECTION
          - CMDEXE
          - NO-CONTENT-TYPE
          - UTF8
    # Disable protection against CMDEXE on /bin
    - name: allow-cdmexe-on-root-bin
      when:
        allOf:
          - reqProperty: tier
            matches: "author|publish"
          - reqProperty: path
            matches: "^/bin/.*"
      action:
        type: log
        wafFlags:
          - CMDEXE
```

1. Aggiungi eventuali regole aggiuntive per bloccare il traffico dannoso di cui potresti essere a conoscenza. Ad esempio, alcuni IP che hanno attaccato il tuo sito.

1. Dopo alcuni minuti, ore o giorni, a seconda del volume di traffico del sito, scarica i registri CDN da Cloud Manager e analizzali con la dashboard.

1. Di seguito sono riportate alcune considerazioni:
   1. Le regole dichiarate di corrispondenza del traffico vengono visualizzate nei grafici e nei registri delle richieste per verificare facilmente se le regole dichiarate vengono attivate.
   1. I flag WAF corrispondenti al traffico vengono visualizzati nei grafici e nei registri delle richieste, anche se non li hai registrati in una regola. In questo modo, sei sempre a conoscenza di traffico potenzialmente nuovo dannoso e puoi creare nuove regole, in base alle esigenze. Esaminare i flag WAF che non si riflettono nelle regole dichiarate e considerare la dichiarazione.
   1. Per le regole corrispondenti, esamina i registri di richiesta per verificare la presenza di falsi positivi e verifica se è possibile escluderli dalle regole. Ad esempio, potrebbero essere un falso positivo solo per determinati percorsi.

1. Imposta le regole appropriate per la modalità blocco e prendi in considerazione l’aggiunta di regole aggiuntive. Forse alcune delle regole dovrebbero rimanere in modalità registro mentre si analizza ulteriormente con più traffico.

1. Ridistribuisci la configurazione.

1. Eseguire iterazioni, analizzando frequentemente le dashboard.

