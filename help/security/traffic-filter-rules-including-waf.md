---
title: Regole del filtro del traffico, incluse le regole WAF
description: Configurazione delle regole del filtro del traffico, incluse le regole del firewall delle applicazioni web (WAF).
exl-id: 6a0248ad-1dee-4a3c-91e4-ddbabb28645c
feature: Security
role: Admin
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: tm+mt
source-wordcount: '3937'
ht-degree: 98%

---


# Regole del filtro del traffico, incluse le regole WAF {#traffic-filter-rules-including-waf-rules}

Le regole del filtro del traffico possono essere utilizzate per bloccare o consentire le richieste a livello CDN, che potrebbe essere utile in scenari come:

* La limitazione dell’accesso a domini specifici al traffico interno dell’azienda, prima della pubblicazione di un nuovo sito
* Definizione dei limiti di frequenza per essere meno suscettibili ad attacchi DoS volumetrici
* La prevenzione del targeting delle tue pagine da parte di indirizzi IP dannosi

La maggior parte di queste regole del filtro del traffico è disponibile per tutta la clientela di Sites e Forms di AEM as a Cloud Service. Funzionano principalmente con proprietà di richiesta e intestazioni di richiesta, tra cui IP, nome host, percorso e agente utente.

Una sottocategoria delle regole del filtro del traffico richiede una licenza di sicurezza avanzata o una licenza di protezione WAF-DDoS. Queste potenti regole sono note come regole di filtro del traffico WAF (Web Application Firewall) (o regole WAF in breve) e hanno accesso ai [flag WAF](#waf-flags-list) descritti di seguito in questo articolo.

Le regole di filtro del traffico possono essere implementate nell’ambiente di sviluppo, di staging e di produzione nei programmi di produzione (non sandbox) tramite le pipeline di configurazione di Cloud Manager. Il supporto per gli ambienti di sviluppo rapido (RDE) verrà introdotto in futuro.

[Segui con un tutorial](#tutorial) per sviluppare rapidamente competenze concrete su questa funzione.

>[!NOTE]
>Per ulteriori opzioni relative alla configurazione del traffico sulla CDN, tra cui la modifica della richiesta/risposta, la dichiarazione dei reindirizzamenti e il proxy a un’origine non AEM, consulta l’articolo [Configurazione del traffico sulla CDN](/help/implementing/dispatcher/cdn-configuring-traffic.md).


## Struttura di questo articolo {#how-organized}

Questo articolo è suddiviso nelle sezioni seguenti:

* **Panoramica sulla protezione del traffico:** scopri in che modo sei protetto dal traffico dannoso.
* **Processo consigliato per la configurazione delle regole:** scopri una metodologia di alto livello per proteggere il sito web.
* **Configurazione:** scopri come impostare, configurare e distribuire le regole del filtro del traffico, incluse le regole WAF avanzate.
* **Sintassi delle regole:** scopri come dichiarare le regole del filtro del traffico nel file di configurazione `cdn.yaml`. Questa sezione include sia le regole del filtro del traffico disponibili per tutta la clientela di Sites e Forms, nonché la sottocategoria delle regole WAF per coloro che concedono in licenza tale funzionalità.
* **Esempi di regole:** per orientarti meglio, consulta alcuni esempi di regole dichiarate.
* **Regole dei limiti di frequenza:** scopri come utilizzare le regole dei limiti di frequenza per proteggere il sito da attacchi con volumi elevati.
* **Avvisi sulle regole del filtro del traffico:** configura gli avvisi da notificare quando le regole vengono attivate.
* **Avviso predefinito di picco nel traffico all’origine:** ricevi una notifica quando si verifica un sovraccarico di traffico all’origine indicativo di un attacco DDoS.
* **Registri CDN:** scopri quali regole dichiarate e contrassegni WAF corrispondono al tuo traffico.
* **Strumenti dashboard:** analizza i registri CDN per trovare nuove regole per il filtro del traffico.
* **Regole iniziali consigliate:** una serie di regole con cui iniziare.
* **Tutorial:** conoscenza pratica della funzione, incluso l’utilizzo degli strumenti della dashboard per dichiarare le regole corrette.

Adobe invita a fornire un feedback o a porre domande sulle regole del filtro del traffico inviando un’e-mail all’indirizzo **aemcs-waf-adopter@adobe.com**.

## Panoramica sulla protezione del traffico {#traffic-protection-overview}

Nel panorama digitale attuale, il traffico dannoso è una minaccia sempre presente. Adobe è consapevole della gravità del rischio e offre diverse strategie per proteggere le applicazioni della clientela e mitigare gli attacchi quando si verificano.

La rete CDN gestita da Adobe assorbe gli attacchi DoS a livello 
di rete (livelli 3 e 4) ai margini della stessa, inclusi gli attacchi di tipo flood e di riflessione/amplificazione.

Per impostazione predefinita, Adobe adotta misure per evitare la riduzione delle prestazioni dovuto a picchi di traffico estremamente elevato oltre una determinata soglia. Se si verifica un attacco DoS che influisce sulla disponibilità del sito, i team operativi di Adobe vengono avvisati e adottano le misure necessarie per attenuare l’impatto.

La clientela può adottare misure proattive per mitigare gli attacchi a livello di applicazione (livello 7), configurando regole a vari livelli del flusso di distribuzione dei contenuti.

Ad esempio, al livello Apache, è possibile configurare il [modulo Dispatcher](https://experienceleague.adobe.com/it/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration#configuring-access-to-content-filter) o [ModSecurity](https://experienceleague.adobe.com/it/docs/experience-manager-learn/foundation/security/modsecurity-crs-dos-attack-protection) per limitare l’accesso a determinati contenuti.

Come descritto in questo articolo, le regole di filtro del traffico possono essere distribuite alla rete CDN gestita da Adobe, utilizzando le [pipeline di configurazione di Cloud Manager.](/help/operations/config-pipeline.md) Oltre alle regole di filtro del traffico basate su proprietà come indirizzo IP, percorso e intestazioni, o alle regole basate sull’impostazione dei limiti di frequenza, è possibile anche ottenere una licenza per una potente sottocategoria di regole di filtro del traffico, chiamate regole WAF.

## Processo consigliato {#suggested-process}

Di seguito è riportato un processo end-to-end di alto livello consigliato per individuare le regole corrette per il filtro del traffico:

1. Configura le pipeline di configurazione di produzione e non di produzione, come descritto nella sezione [Configurazione](#setup).
1. Chi dispone della licenza per la sottocategoria delle regole del filtro del traffico WAF deve abilitarle in Cloud Manager.
1. Leggi e prova l’esercitazione per comprendere concretamente come utilizzare le regole del filtro del traffico, incluse le regole WAF, se disponi della licenza. Il tutorial illustra come distribuire le regole in un ambiente di sviluppo, simulare traffico dannoso, scaricare i [Registri CDN](#cdn-logs) e analizzarli negli [strumenti della dashboard](#dashboard-tooling).
1. Copia le regole iniziali consigliate in `cdn.yaml` e implementa la configurazione nell’ambiente di produzione in modalità registro.
1. Dopo aver raccolto alcuni dati di traffico, analizza i risultati utilizzando gli [strumenti della dashboard](#dashboard-tooling) per vedere se ci sono state corrispondenze. Cerca i falsi positivi e apporta le eventuali modifiche necessarie, in ultima analisi abilitando le regole iniziali in modalità blocco.
1. Aggiungi regole personalizzate basate sull’analisi dei registri CDN, eseguendo prima un test con traffico simulato in ambienti di sviluppo prima di distribuirlo negli ambienti di staging e produzione in modalità registro, quindi in modalità blocco.
1. Monitora costantemente il traffico e modifica le regole man mano che il panorama delle minacce evolve.

## Configurazione {#setup}

1. Crea un file `cdn.yaml` con un set di regole di filtro del traffico, incluse le regole WAF.

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

   Per una descrizione delle proprietà al di sopra del nodo `data`, vedere [Utilizzo delle pipeline di configurazione](/help/operations/config-pipeline.md#common-syntax). Il valore della proprietà `kind` deve essere impostato su *CDN* e la versione su `1`.


1. Se le regole WAF sono concesse in licenza, per gli scenari di programma nuovi ed esistenti, devi abilitare la funzione in Cloud Manager, come descritto di seguito.

   1. Per configurare WAF su un nuovo programma, seleziona la casella di controllo **Protezione WAF-DDOS** nella scheda **Sicurezza** quando [aggiungi un programma di produzione.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)

   1. Per configurare WAF su un programma esistente: [modifica il programma](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) e nella scheda **Sicurezza** deseleziona o seleziona l’opzione **WAF-DDOS** in qualsiasi momento.

1. Crea una pipeline di configurazione in Cloud Manager, come descritto nell’[articolo sulle pipeline di configurazione.](/help/operations/config-pipeline.md#managing-in-cloud-manager) La pipeline farà riferimento a una cartella `config` di primo livello con il file `cdn.yaml` posizionato in un punto qualsiasi al di sotto. Vedere [Utilizzo delle pipeline di configurazione](/help/operations/config-pipeline.md#folder-structure).

## Sintassi delle regole di filtro del traffico {#rules-syntax}

Puoi configurare le *regole di filtro del traffico* affinché corrispondano a pattern quali IP, agente utente, intestazioni di richiesta, nome host, geo e URL.

Ogni cliente che dispone di una licenza per l’offerta Sicurezza avanzata o Protezione WAF-DDoS può anche configurare una categoria speciale di *regole di filtro del traffico WAF* (o regole WAF in breve) che fa riferimento a uno o più [flag WAF](#waf-flags-list).

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
        when:
          allOf:
            - { reqProperty: path, equals: /block-me }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS]
```

Il formato delle regole per il filtro del traffico nel file `cdn.yaml` è descritto di seguito. Trovi alcuni [altri esempi](#examples) in una sezione successiva, nonché in una sezione separata su [Regole di limite di tasso](#rate-limit-rules).


| **Proprietà** | **Regole di filtro del traffico più frequenti** | **Regole di filtro del traffico WAF** | **Tipo** | **Valore predefinito** | **Descrizione** |
|---|---|---|---|---|---|
| nome | X | X | `string` | - | Nome regola (lunghezza 64 caratteri, può contenere solo caratteri alfanumerici e - ) |
| se | X | X | `Condition` | - | La struttura di base è: <br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>[Consulta Sintassi della struttura delle condizioni](#condition-structure) di seguito, che descrive i getter, i predicati e come combinare più condizioni. |
| azione | X | X | `Action` | registro | oggetto registro, consenti, blocca oppure Azione. Il valore predefinito è registro |
| rateLimit | X |   | `RateLimit` | non definito | Configurazione del limite di frequenza. Il limite di frequenza è disabilitato se non è definito.<br><br>Di seguito è riportata una sezione separata che descrive la sintassi di rateLimit con alcuni esempi. |

### Struttura della condizione {#condition-structure}

Una condizione può essere una condizione semplice o un gruppo di condizioni.

**Condizione semplice**

Una condizione semplice è composta da un getter e da un predicato.

```
{ <getter>: <value>, <predicate>: <value> }
```

**Gruppo di condizioni**

Un gruppo di condizioni è composto da più condizioni semplici e/o da condizioni di gruppo.

```
<allOf|anyOf>:
  - { <getter>: <value>, <predicate>: <value> }
  - { <getter>: <value>, <predicate>: <value> }
  - <allOf|anyOf>:
    - { <getter>: <value>, <predicate>: <value> }
```

| **Proprietà** | **Tipo** | **Significato** |
|---|---|---|
| **allOf** | `array[Condition]` | operazione **and**. true se tutte le condizioni elencate restituiscono true |
| **anyOf** | `array[Condition]` | operazione **or**. true se una qualsiasi delle condizioni elencate restituisce true |

**Getter**

| **Proprietà** | **Tipo** | **Descrizione** |
|---|---|---|
| reqProperty | `string` | Proprietà richiesta.<br><br>Una di:<br><ul><li>`path`: restituisce il percorso completo di un URL senza i parametri di query.</li><li>`queryString`: restituisce la parte di query di un URL</li><li>`method`: restituisce il metodo HTTP utilizzato nella richiesta.</li><li>`tier`: restituisce uno tra `author`, `preview` o `publish`.</li><li>`domain`: restituisce la proprietà del dominio (come definito nell’intestazione `Host`) in minuscolo</li><li>`clientIp`: restituisce l’IP del client.</li><li>`clientCountry`: restituisce un codice di due lettere ([simbolo indicatore regionale](https://en.wikipedia.org/wiki/Regional_indicator_symbol)) che identifica il paese in cui si trova il client.</li></ul> |
| reqHeader | `string` | Restituisce l’intestazione di richiesta con il nome specificato |
| queryParam | `string` | Restituisce il parametro di query con il nome specificato |
| reqCookie | `string` | Restituisce il cookie con il nome specificato |
| postParam | `string` | Restituisce il parametro pubblicazione con il nome specificato dal corpo della richiesta. Funziona solo quando il corpo è un tipo di contenuto `application/x-www-form-urlencoded` |

**Predicato**

| **Proprietà** | **Tipo** | **Significato** |
|---|---|---|
| **equals** | `string` | true se il risultato del getter è uguale al valore specificato |
| **doesNotEqual** | `string` | true se il risultato del getter non è uguale al valore specificato |
| **like** | `string` | true se il risultato del getter corrisponde al pattern specificato |
| **notLike** | `string` | true se il risultato del getter non corrisponde al pattern specificato |
| **matches** | `string` | true se il risultato del getter corrisponde al regex specificato |
| **doesNotMatch** | `string` | true se il risultato del getter non corrisponde al regex specificato |
| **in** | `array[string]` | true se l’elenco fornito contiene il risultato del getter |
| **notIn** | `array[string]` | true se l’elenco fornito non contiene il risultato del getter |
| **exists** | `boolean` | true se è impostato su true e la proprietà esiste o se è impostato su false e la proprietà non esiste |

**Note**

* La proprietà di richiesta `clientIp` può essere utilizzata solo con i seguenti predicati: `equals`, `doesNotEqual`, `in`, `notIn`. `clientIp` può essere confrontata anche con intervalli IP quando si utilizzano i predicati `in` e `notIn`. L’esempio seguente implementa una condizione per valutare se l’IP di un client è compreso nell’intervallo IP 192.168.0.0/24 (quindi tra 192.168.0.0 e 192.168.0.255):

```
when:
  reqProperty: clientIp
  in: [ "192.168.0.0/24" ]
```

* Adobe consiglia di utilizzare [regex101](https://regex101.com/) e [Fastly Fiddle](https://fiddle.fastly.dev/), quando si lavora con regex. Per ulteriori informazioni su come Fastly gestisce regex, consulta la documentazione di [fastly: espressioni regolari in Fastly VCL](https://www.fastly.com/documentation/reference/vcl/regex/#best-practices-and-common-mistakes).


### Struttura delle azioni {#action-structure}

Un’`action` può essere una stringa che specifica l’azione (consenti, blocca o registra) o un oggetto composto sia dal tipo di azione (consenti, blocca o registra) che da opzioni quali wafFlags e/o Stato.

**Tipi di azioni**

La priorità delle azioni dipende dal loro tipo; nella tabella seguente, le azioni sono elencate in base al rispettivo ordine di esecuzione:

| **Nome** | **Proprietà consentite** | **Significato** |
|---|---|---|
| **allow** | `wafFlags` (facoltativo), `alert` (facoltativo) | Se non sono presenti proprietà wafFlags, interrompe ulteriori elaborazioni di regole e passa alla risposta. Se sono presenti proprietà wafFlags, disabilita le protezioni WAF specificate e procede all’ulteriore elaborazione delle regole. <br>Se si specifica un avviso, viene inviata una notifica al Centro azioni se la regola viene attivata 10 volte in una finestra temporale di 5 minuti. Una volta attivato un avviso per una regola particolare, non verrà attivato nuovamente fino al giorno successivo (UTC). |
| **block** | `status, wafFlags` (facoltativo e reciprocamente esclusivo), `alert` (facoltativo) | Se non sono presenti proprietà wafFlags, restituisce un errore HTTP ignorando tutte le altre proprietà. Il codice di errore viene definito dalla proprietà dello stato oppure viene impostato sul codice predefinito 406. Se sono presenti proprietà wafFlags, abilita le protezioni WAF specificate e procede all’ulteriore elaborazione delle regole. <br>Se si specifica un avviso, viene inviata una notifica al Centro azioni se la regola viene attivata 10 volte in una finestra temporale di 5 minuti. Una volta attivato un avviso per una regola particolare, non verrà attivato nuovamente fino al giorno successivo (UTC). |
| **log** | `wafFlags` (facoltativo), `alert` (facoltativo) | Registra il fatto che la regola è stata attivata, non influisce sull’elaborazione in alcun modo. Eventuali proprietà wafFlags non hanno alcun effetto. <br>Se si specifica un avviso, viene inviata una notifica al Centro azioni se la regola viene attivata 10 volte in una finestra temporale di 5 minuti. Una volta attivato un avviso per una regola particolare, non verrà attivato nuovamente fino al giorno successivo (UTC). |

### Elenco contrassegni WAF {#waf-flags-list}

La proprietà `wafFlags`, che può essere utilizzata nelle regole del filtro del traffico WAF su licenza, può fare riferimento a quanto segue:

| **ID contrassegno** | **Nome contrassegno** | **Descrizione** |
|---|---|---|
| SQLI | SQL Injection | SQL Injection è il tentativo di accedere a un’applicazione o di ottenere informazioni con privilegi tramite l’esecuzione di query arbitrarie nel database. |
| BACKDOOR | Backdoor | Un segnale backdoor è una richiesta che tenta di determinare se un file backdoor comune è presente sul sistema. |
| CMDEXE | Command Execution | Command Execution è il tentativo di ottenere il controllo o danneggiare un sistema di destinazione attraverso comandi arbitrari di sistema mediante l’input dell’utente. |
| CMDEXE-NO-BIN | Esecuzione comando, tranne il `/bin/` | Garantisci lo stesso livello di protezione di `CMDEXE` durante la disabilitazione del falso positivo su `/bin` dovuta all’architettura di AEM. |
| XSS | Vulnerabilità cross-site scripting | Per vulnerabilità cross-site scripting si intende il tentativo di dirottare l’account o la sessione di navigazione web di un utente attraverso codice JavaScript dannoso. |
| TRAVERSAL | Directory Traversal | Directory Traversal è il tentativo di spostarsi tra le cartelle privilegiate all’interno di un sistema nella speranza di ottenere informazioni riservate. |
| USERAGENT | Attack Tooling | Attack Tooling è l’uso di un software automatizzato per identificare le vulnerabilità di sicurezza o per tentare di sfruttare una vulnerabilità scoperta. |
| LOG4J-JNDI | JNDI Log4J | Gli attacchi JNDI Log4J tentano di sfruttare la [vulnerabilità Log4Shell](https://en.wikipedia.org/wiki/Log4Shell) presente nelle versioni Log4J precedenti alla 2.16.0 |
| BHH | Intestazioni hop non valide | Le intestazioni hop non valide indicano un tentativo di smuggling dell’HTTP tramite un’intestazione di codifica di trasferimento (TE) o lunghezza dei contenuti (CL) non valida oppure tramite un’intestazione TE e CL corretta |
| CODEINJECTION | Code Injection | Code Injection è il tentativo di ottenere il controllo o danneggiare un sistema di destinazione attraverso comandi arbitrari di codice di applicazione tramite l’input dell’utente. |
| ABNORMALPATH | Percorso anomalo | Percorso anomalo indica che il percorso originale è diverso dal percorso normalizzato (ad esempio, `/foo/./bar` è normalizzato su `/foo/bar`) |
| DOUBLEENCODING | Doppia codifica | La doppia codifica verifica la tecnica di evasione dei caratteri HTML a doppia codifica |
| NOTUTF8 | Codifica non valida | Una codifica non valida può causare la conversione di caratteri dannosi da una richiesta a una risposta da parte del server, causando un rifiuto del servizio o XSS |
| JSON-ERROR | Errore di codifica JSON | Corpo della richiesta POST, PUT o PATCH specificato come contenente JSON nell’intestazione della richiesta “Content-Type”, ma contenente errori di analisi JSON. Questo è spesso correlato a un errore di programmazione o a una richiesta automatizzata o dannosa. |
| MALFORMED-DATA | Dati non validi nel corpo della richiesta | Corpo della richiesta POST, PUT o PATCH non valido in base all’intestazione della richiesta “Content-Type”. Ad esempio, se è specificata un’intestazione di richiesta “Content-Type: application/x-www-form-urlencoded” che contiene un corpo POST che è JSON. Spesso si tratta di un errore di programmazione, richiesta automatizzata o dannosa. Richiede l&#39;agente 3.2 o versione successiva. |
| SANS | Traffico IP dannoso | [SANS Internet Storm Center](https://isc.sans.edu/) elenco di indirizzi IP segnalati che hanno eseguito attività dannose. |
| NO-CONTENT-TYPE | Intestazione di richiesta “Content-Type” mancante | Una richiesta POST, PUT o PATCH senza intestazione di richiesta “Content-Type”. Per impostazione predefinita, i server delle applicazioni devono assumere in questo caso “Content-Type: text/plain; charset=us-ascii”. In molte richieste automatizzate e dannose potrebbe mancare “Content Type”. |
| NOUA | Nessun agente utente | Molte richieste automatizzate e dannose utilizzano agenti utente falsi o mancanti per rendere difficile identificare il tipo di dispositivo che effettua le richieste. |
| TORNODE | Traffico Tor | Tor è un software che nasconde l’identità di un utente. Un picco nel traffico Tor può indicare che un hacker sta cercando di mascherare la sua posizione. |
| NULLBYTE | Byte Null | I byte Null non vengono in genere visualizzati in una richiesta e indicano che la richiesta è in formato non corretto e potenzialmente dannoso. |
| PRIVATEFILE | File privati | I file privati sono di solito di natura riservata, ad esempio, un file `.htaccess` Apache o un file di configurazione, che potrebbero causare la perdita di informazioni riservate. |
| SCANNER | Scanner | Identifica i servizi e gli strumenti di scansione più diffusi. |
| RESPONSESPLIT | HTTP Response Splitting | Identifica quando i caratteri CRLF vengono inviati come input all’applicazione per inserire le intestazioni nella risposta HTTP. |
| XML-ERROR | Errore di codifica XML | Corpo della richiesta POST, PUT o PATCH specificato come contenente XML nell’intestazione della richiesta &quot;Content-Type&quot;, ma contenente errori di analisi XML. Questo è spesso correlato a un errore di programmazione o a una richiesta automatizzata o dannosa. |
| DATACENTER | Datacenter | Identifica la richiesta come proveniente da un provider di hosting noto. Questo tipo di traffico non è comunemente associato a un utente finale reale. |


## Considerazioni {#considerations}

* Quando vengono create due regole in conflitto, le regole consentite avranno sempre la precedenza sulle regole del blocco. Ad esempio, se crei una regola per bloccare un percorso specifico e una per consentire un indirizzo IP specifico, le richieste provenienti da tale indirizzo IP saranno consentite sul percorso bloccato.

* Se una regola viene rilevata e bloccata, il CDN risponde con un codice di restituzione `406`.

* I file di configurazione non devono contenere segreti, in quanto potrebbero essere letti da chiunque abbia accesso all’archivio Git.

* Gli elenchi di IP consentiti definiti in Cloud Manager hanno la precedenza sulle regole dei filtri di traffico.

* Le corrispondenze delle regole WAF vengono visualizzate solo nei registri CDN per CDN miss e pass, non per hit.

## Esempi di regole {#examples}

Di seguito sono riportati alcuni esempi di regole. Per esempi di regole del limite di frequenza, consulta la [sezione sul limite di frequenza](#rate-limit-rules) più in basso.

**Esempio 1**

Questa regola blocca le richieste provenienti da **IP 192.168.1.1**:

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

Questa regola blocca le richieste che contengono il parametro di query `foo` al momento della pubblicazione, ma consente ogni richiesta proveniente da IP 192.168.1.1:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "block-request-that-contains-query-parameter-foo"
        when:
          allOf:
            - { queryParam: url-param, equals: foo }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
      - name: "allow-all-requests-from-ip"
        when: { reqProperty: clientIp, equals: 192.168.1.1 }
        action:
          type: allow
```

**Esempio 4**

Questa regola blocca le richieste al percorso `/block-me` al momento della pubblicazione e blocca ogni richiesta che corrisponde a uno schema `SQLI` o `XSS`. Questo esempio include le regole di filtro del traffico WAF che fa riferimento ai [contrassegni WAF](#waf-flags-list) `SQLI` e `XSS` e richiede pertanto una licenza separata.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when:
          allOf:
            - { reqProperty: path, equals: /block-me }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
      - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
        when: { reqProperty: path, like: "*" }
        action:
          type: block
          wafFlags: [ SQLI, XSS]
```

**Esempio 5**

Questa regola blocca l’accesso ai Paesi OFAC:

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

## Regole del limite di frequenza

A volte è auspicabile bloccare il traffico, se supera una certa frequenza di richieste in arrivo, in base a una condizione specifica. L’impostazione di un valore per la proprietà `rateLimit` limita la frequenza delle richieste che corrispondono alla condizione della regola.

Le regole del limite di tasso non possono fare riferimento ai contrassegni WAF. Sono disponibili per tutti i clienti Sites e Forms.

I limiti di tasso vengono calcolati per POP CDN. Ad esempio, supponiamo che i POP a Montreal, Miami e Dublino registrino tassi di traffico rispettivamente di 80, 90 e 120 richieste al secondo. La regola del limite di frequenza è impostata su 100. In tal caso, sarebbe limitato solo il traffico verso Dublino.

I limiti di frequenza vengono valutati in base al traffico che raggiunge il limite, la sorgente o il numero di errori.

### Struttura rateLimit {#ratelimit-structure}

| **Proprietà** | **Tipo** | **Predefinito** | **SIGNIFICATO** |
|---|---|---|---|
| limite | numero intero da 10 a 10000 | obbligatorio | Frequenza di richiesta (per POP CDN) nelle richieste al secondo per le quali viene attivata la regola. |
| finestra | numero intero: 1, 10 o 60 | 10 | Finestra di campionamento in secondi per la quale viene calcolato il tasso di richiesta. La precisione dei contatori dipende dalle dimensioni della finestra (maggiore finestra, maggiore precisione). Ad esempio, ci si può aspettare una precisione del 50% per la finestra di 1 secondo e del 90% per la finestra di 60 secondi. |
| penalità | numero intero compreso tra 60 e 3600 | 300 (5 minuti) | Un periodo in secondi per il quale le richieste corrispondenti vengono bloccate (arrotondato al minuto più vicino). |
| numero | tutti, recuperi, errori | tutti | valutare in base al traffico del bordo (tutto), al traffico sorgente (recuperi) o al numero di errori (errori) |
| groupBy | array[Getter] | nessuno | il contatore del limitatore di frequenza verrà aggregato da un set di proprietà di richiesta (ad esempio clientIp). |

### Esempi {#ratelimiting-examples}

**Esempio 1**

Questa regola blocca un client per 5 millisecondi quando supera la media di 60 richieste/secondo (per POP CDN) negli ultimi 10 sec:

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
        count: all
        groupBy:
          - reqProperty: clientIp
      action: block
```

**Esempio 2**

Blocca le richieste per 60 secondi nel percorso /critical/resource quando supera la media di 100 richieste di origine al secondo (per POP CDN) in un periodo di tempo di dieci secondi:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: rate-limit-example
        when:
          allOf:
            - { reqProperty: path, equals: /critical/resource }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
        rateLimit: { limit: 100, window: 10, penalty: 60, count: fetches }
```

## Avvisi delle regole di filtro del traffico {#traffic-filter-rules-alerts}

Una regola può essere configurata per inviare una notifica al Centro azioni se viene attivata dieci volte in una finestra temporale di 5 minuti. Una regola di questo tipo avvisa quando si verificano determinati modelli di traffico in modo da poter adottare tutte le misure necessarie. Una volta attivato un avviso per una regola particolare, non verrà attivato nuovamente fino al giorno successivo (UTC).

Ulteriori informazioni sul [Centro azioni](/help/operations/actions-center.md), tra cui come configurare i profili di notifica richiesti per la ricezione di e-mail.

![Notifica Centro azioni](/help/security/assets/traffic-filter-rules-actions-center-alert.png)


La proprietà dell’avviso può essere applicata al nodo dell’azione per tutti i tipi di azione (consenti, blocco, registro).

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    rules:
      - name: "path-rule"
        when:
          allOf:
            - { reqProperty: path, equals: /block-me }
            - { reqProperty: tier, equals: publish }
        action:
          type: block
          alert: true
```

## Avviso predefinito di picco nel traffico all’origine {#traffic-spike-at-origin-alert}

Una notifica e-mail [Centro azioni](/help/operations/actions-center.md) verrà inviata quando viene rilevata una quantità significativa di traffico inviato all’origine, dove una soglia elevata di richieste proviene dallo stesso indirizzo IP, suggerendo quindi un attacco DDoS.

Se questa soglia viene raggiunta, Adobe bloccherà il traffico da tale indirizzo IP. Tuttavia si consiglia di adottare misure aggiuntive per proteggere l’origine, tra cui la configurazione delle regole del filtro del traffico del limite di frequenza e bloccare i picchi a soglie più basse. Per una procedura guidata, consulta [Tutorial sul blocco degli attacchi DoS e DDoS tramite le regole del traffico](#tutorial-blocking-DDoS-with-rules).

Questo avviso è attivato per impostazione predefinita, ma può essere disattivato utilizzando la proprietà *defaultTrafficAlerts* e impostandola su false. Una volta attivato, l’avviso non si riattiverà fino al giorno successivo (UTC).

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
   defaultTrafficAlerts: false
```

## Registri CDN {#cdn-logs}

AEM as a Cloud Service fornisce accesso ai registri CDN, utili per i casi d’uso tra cui l’ottimizzazione del rapporto hit della cache e la configurazione delle regole del filtro del traffico. I registri CDN vengono visualizzati nella finestra di dialogo di Cloud Manager **Scarica registri** durante la selezione del servizio di authoring o di pubblicazione.

I registri CDN possono subire un ritardo fino a 5 minuti.

La proprietà `rules` descrive le regole del filtro del traffico corrispondenti e presenta il seguente pattern:

```
"rules": "match=<matching-customer-named-rules-that-are-matched>,waf=<matching-WAF-rules>,action=<action_type>"
```

Ad esempio:

```
"rules": "match=Block-Traffic-under-private-folder,Enable-SQL-injection-everywhere,waf="SQLI,SANS",action=block"
```

Le regole si comportano nel modo seguente:

* Il nome delle regola dichiarato dal cliente di tutte le regole corrispondenti è elencato nell’attributo `match`.
* L’attributo `action` determina se le regole bloccano, consentono o registrano.
* Se WAF è concesso in licenza e abilitato, l’attributo `waf` elenca tutti i contrassegni WAF rilevati (ad esempio SQLI). Ciò è vero indipendentemente dal fatto che i flag WAF vengano elencati in una qualsiasi regola. Questo serve a ottenere informazioni dettagliate su possibili nuove regole da dichiarare.
* Se nessuna regola dichiarata dal cliente corrisponde e nessuna regola waf corrisponde, la proprietà `rules` è vuota.

Come indicato in precedenza, le corrispondenze delle regole WAF vengono visualizzate solo nei registri CDN per CDN miss e pass, non per hit.

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
| *marca temporale* | L’ora di inizio della richiesta, dopo la cessazione del TLS. |
| *ttfb* | Abbreviazione per *Time To First Byte*. L’intervallo di tempo compreso tra l’inizio della richiesta e il momento prima che il corpo della risposta inizi a essere trasmesso in streaming. |
| *cli_ip* | Indirizzo IP del client. |
| *cli_country* | Codice paese a due lettere [ISO 3166-1](https://en.wikipedia.org/wiki/ISO_3166-1) alfa-2 del paese client. |
| *rid* | Il valore dell’intestazione di richiesta utilizzato per identificare in modo univoco la richiesta. |
| *req_ua* | L’agente utente responsabile di effettuare una determinata richiesta HTTP. |
| *host* | Autorità a cui è destinata la richiesta. |
| *url* | Il percorso completo, inclusi i parametri di query. |
| *metodo* | Metodo HTTP inviato dal client, ad esempio “GET” o “POST”. |
| *res_ctype* | Tipo di contenuto utilizzato per indicare il tipo di file multimediale originale della risorsa. |
| *cache* | Stato della cache. I valori possibili sono HIT, MISS o PASS |
| *stato* | Il codice di stato HTTP come valore intero. |
| *res_age* | Il tempo (in secondi) in cui una risposta è stata memorizzata nella cache (in tutti i nodi). |
| *pop* | Centro dati del server cache CDN. |
| *regole* | Nome di eventuali regole corrispondenti.<br><br>Indica anche se la corrispondenza ha prodotto un blocco. <br><br>Ad esempio, &quot;`match=Enable-SQL-Injection-and-XSS-waf-rules-globally,waf=SQLI,action=blocked`&quot;<br><br>Vuoto se non corrisponde alcuna regola. |

## Strumenti dashboard {#dashboard-tooling}

Adobe fornisce un meccanismo per scaricare gli strumenti della dashboard sul computer per acquisire i registri CDN scaricati tramite Cloud Manager. Con questo strumento, puoi analizzare il traffico per scoprire le regole del filtro del traffico da dichiarare, incluse le regole WAF.

Gli strumenti della dashboard possono essere clonati direttamente dall’archivio GitHub [AEMCS-CDN-Log-Analysis-Tooling](https://github.com/adobe/AEMCS-CDN-Log-Analysis-Tooling).

I [tutorial](#tutorial) sono disponibili per istruzioni pratiche su come utilizzare gli strumenti della dashboard.

## Regole iniziali consigliate {#recommended-starter-rules}

Puoi copiare le regole consigliate di seguito nel tuo `cdn.yaml` per iniziare. Inizia in modalità registro, analizza il traffico e, quando il risultato è soddisfacente, passa alla modalità blocco. Puoi modificare le regole in base alle caratteristiche specifiche del traffico live del tuo sito Web.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev", "stage", "prod"]
data:
  trafficFilters:
    rules:
    #  Block client for 5m when it exceeds an average of 100 req/sec to origin on a time window of 10sec
    - name: limit-origin-requests-client-ip
      when:
        reqProperty: tier
        equals: 'publish'
      rateLimit:
        limit: 100
        window: 10
        count: fetches
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: log
    #  Block client for 5m when it exceeds an average of 500 req/sec on a time window of 10sec
    - name: limit-requests-client-ip
      when:
        reqProperty: tier
        equals: 'publish'
      rateLimit:
        limit: 500
        window: 10
        count: all
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: log
    # Block requests coming from OFAC countries
    - name: block-ofac-countries
      when:
        allOf:
          - { reqProperty: tier, in: ["author", "publish"] }
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
    # Enable recommended WAF protections (only works if WAF is licensed enabled for your environment)
    - name: block-waf-flags-globally
      when:
        reqProperty: tier
        in: ["author", "publish"]
      action:
        type: log
        wafFlags:
          - TRAVERSAL
          - CMDEXE-NO-BIN
          - XSS
          - LOG4J-JNDI
          - BACKDOOR
          - USERAGENT
          - SQLI
          - SANS
          - TORNODE
          - NOUA
          - SCANNER
          - PRIVATEFILE
          - NULLBYTE
```

## Tutorial {#tutorial}

Sono disponibili due tutorial.

### Protezione dei siti web con regole di filtro del traffico (comprese le regole WAF) {#tutorial-protecting-websites}

[Esercitati con un tutorial](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/security/traffic-filter-and-waf-rules/overview) per acquisire conoscenze pratiche e generali ed esperienza sulle regole per filtrare il traffico, incluse le regole WAF.

Il tutorial illustra i seguenti passaggi:

* Impostazione della pipeline di configurazione di Cloud Manager
* Utilizzo di strumenti per simulare traffico dannoso
* Dichiarazione delle regole per filtrare il traffico, incluse le regole WAF
* Analisi dei risultati con gli strumenti della dashboard
* Best practice

### Bloccare gli attacchi DoS e DDoS utilizzando le regole di filtro del traffico {#tutorial-blocking-DDoS-with-rules}

[Approfondimento su come bloccare](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/security/blocking-dos-attack-using-traffic-filter-rules) Attacchi Denial of Service (DoS) e Distributed Denial of Service (DDoS) che utilizzano regole di filtro del traffico con limite di velocità e altre strategie.

Il tutorial illustra i seguenti passaggi:

* come comprendere la protezione
* come ricevere avvisi quando i limiti di velocità vengono superati
* come analizzare i pattern di traffico utilizzando gli strumenti della dashboard per configurare le soglie per le regole di filtro del traffico con limite di velocità



