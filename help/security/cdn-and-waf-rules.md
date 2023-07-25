---
title: Configurazione delle regole CDN e WAF per filtrare il traffico
description: Utilizzare le regole CDN e Firewall applicazione Web per filtrare il traffico dannoso
source-git-commit: 579f2842a72c7da1c9d24772bdae354a943de40c
workflow-type: tm+mt
source-wordcount: '2360'
ht-degree: 2%

---


# Configurazione delle regole CDN e WAF per filtrare il traffico {#configuring-cdn-and-waf-rules-to-filter-traffic}

>[!NOTE]
>
>Questa funzione non è ancora disponibile al pubblico. Per aderire al programma di adozione anticipata in corso, invia un messaggio e-mail a **aemcs-waf-adopter@adobe.com**, incluso il nome dell’organizzazione e il contesto relativi al tuo interesse per la funzione.

Adobe tenta di mitigare gli attacchi contro i siti web dei clienti, ma può essere utile filtrare in modo proattivo le richieste che corrispondono a determinati modelli in modo che il traffico dannoso non raggiunga l’applicazione. I possibili approcci includono:

* Moduli di livello Apache come `mod_security`
* Configurazione delle regole distribuite nella rete CDN tramite la pipeline di configurazione di Cloud Manager.

Questo articolo descrive quest’ultimo approccio, che offre due categorie di regole:

1. **Regole CDN**: blocca o consenti le richieste in base alle proprietà e alle intestazioni di richiesta, inclusi IP, percorsi e agente utente. Queste regole possono essere configurate da tutti i clienti AEM as a Cloud Service
1. **WAF** (Web Application Firewall) regole: blocca le richieste che corrispondono a vari pattern noti per essere associati a traffico dannoso. Queste regole possono essere configurate dai clienti che concedono in licenza il componente aggiuntivo WAF; per informazioni, contatta il team del tuo account di Adobe. Si noti che non è richiesta alcuna licenza aggiuntiva durante il primo programma dell&#39;utente.

Queste regole possono essere distribuite ai tipi di ambiente cloud di sviluppo, staging e produzione, per i programmi di produzione (non sandbox). Il supporto per gli ambienti RDE sarà disponibile in futuro.

## Configurazione {#setup}

1. Innanzitutto, crea la seguente cartella e struttura di file nella cartella di livello principale in Git:

   ```
   config/
        cdn/
           cdn.yaml
           _config.yaml
   ```

1. `_config.yaml` descrive alcuni metadati sulla configurazione. Il parametro &quot;tipo&quot; deve essere impostato su &quot;CDN&quot; e la versione deve essere impostata sulla versione dello schema, attualmente &quot;1&quot;. Vedi lo snippet seguente:

   ```
   kind: "CDN"
   version: "1"
   ```

   <!-- Two properties -- `envType` and `envId` -- may be included to limit the scope of the rules. The envType property may have values "dev", "stage", or "prod", while the envId property is the environment (e.g., "53245"). This approach is useful if it is desired to have a single configuration pipeline, even if some environments have different rules. However, a different approach could be to have multiple configuration pipelines, each pointing to different repositories or git branches. -->

1. `cdn.yaml` deve includere un elenco di regole CDN e WAF, come descritto nelle sezioni seguenti
1. Per soddisfare le regole WAF, WAF deve essere abilitato in Cloud Manager, come descritto di seguito per gli scenari di programma nuovi ed esistenti. Si noti che per WAF deve essere acquistata una licenza separata.

   1. Per configurare WAF per un nuovo programma, selezionare **Protezione WAF-DDOS** casella di controllo in **Sicurezza** come mostrato di seguito. Continua seguendo i passaggi descritti in [Aggiungi programma di produzione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) per creare il programma

   1. Per configurare WAF su un programma esistente, selezionare **Modifica programma** seguendo i passaggi descritti nella sezione [Modifica dei programmi](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) documentazione. Quindi, nella **Sicurezza** della procedura guidata, è possibile deselezionare o selezionare l&#39;opzione WAF-DDOS in qualsiasi momento

1. Per tipi di ambiente diversi da RDE, esegui la pipeline di configurazione di Cloud Manager, che può essere configurata come descritto di seguito.

   1. Dalla scheda pipeline nella home page di Cloud Manager, seleziona **Aggiungi pipeline di produzione** o **Aggiungi pipeline non di produzione** per avviare la procedura guidata aggiungi pipeline
   1. Seleziona **Pipeline di implementazione** nella scheda di configurazione

      ![Seleziona l’opzione Pipeline di distribuzione](/help/security/assets/deployment.png)

   1. Assegna un nome alla pipeline e seleziona i trigger di distribuzione, quindi seleziona **Continua**
   1. In **Codice sorgente** , seleziona **Distribuzione mirata**, quindi seleziona **Config**

      ![Seleziona distribuzione di destinazione](/help/security/assets/target-deployment.png)

   1. Seleziona l’archivio e il ramo in base alle esigenze. Se esiste una pipeline di configurazione per l’ambiente selezionato, questa selezione viene disabilitata.

      ![Panoramica di una pipeline di configurazione](/help/security/assets/config-pipeline.png)

      >[!NOTE]
      >
      >Puoi configurare ed eseguire una sola pipeline di configurazione per ogni ambiente.

   1. Seleziona **Salva**. La nuova pipeline verrà visualizzata nella scheda della pipeline e potrà essere eseguita quando sei pronto.
   1. Per RDE verrà utilizzata la riga di comando, ma al momento RDE non è supportato.

## Sintassi delle regole {#rules-syntax}

Il formato delle regole è descritto di seguito, seguito da alcuni esempi in una sezione successiva.

| **Proprietà** | **Regole CDN** | **Regole WAF** | **Tipo** | **Valore predefinito** | **Descrizione** |
|---|---|---|---|---|---|
| name | X | X | `string` | - | Nome regola (64 caratteri, può contenere solo caratteri alfanumerici e - ) |
| quando | X | X | `Condition` | - | La struttura di base è:<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>Vedi Sintassi della struttura delle condizioni di seguito, che descrive i getter, i predicati e come combinare più condizioni. |
| azione | X | X | `Enum` | registro (regole CDN) | Per le regole CDN: consenti, blocca, registra. Il valore predefinito è log.<br><br>Per le regole WAF: `enableWafRules`, `disableWafRules`, log. Nessun valore predefinito. |
| rateLimit | X |   | `RateLimit` | non definito | Configurazione del limite di frequenza. La limitazione della frequenza è disabilitata se non definita.<br><br>Di seguito è riportata una sezione separata che descrive la sintassi rateLimit, con alcuni esempi. |
| wafRules |   | X | `array[Enum]` | - | Elenco delle regole WAF da abilitare o disabilitare.<br><br>Alcuni esempi includono SQLI e XSS. Per un elenco completo, vedere l&#39;elenco delle regole waf riportato di seguito. |

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

| **Proprietà** | **Tipo** | **Descrizione** |
|---|---|---|
| **allOf** | `array[Condition]` | **e** operazione. true se tutte le condizioni elencate restituiscono true |
| **anyOf** | `array[Condition]` | **o** operazione. true se una qualsiasi delle condizioni elencate restituisce true |

**Recuperatore**

| **Proprietà** | **Tipo** | **Descrizione** |
|---|---|---|
| reqProperty | `string` | Proprietà richiesta.<br><br>Uno di: `path` , `queryString`, `method`, `tier`, `domain`, `clientIp`, `clientCountry`<br><br>La proprietà domain è una trasformazione in minuscolo dell’intestazione host della richiesta. È utile per i confronti tra stringhe, pertanto le corrispondenze non vengono perse a causa della distinzione tra maiuscole e minuscole.<br><br>Il `clientCountry` utilizza due codici di lettera visualizzati in [https://en.wikipedia.org/wiki/Regional_indicator_symbol](https://en.wikipedia.org/wiki/Regional_indicator_symbol) |
| reqHeader | `string` | Restituisce l’intestazione della richiesta con il nome specificato |
| queryParam | `string` | Restituisce il parametro di query con il nome specificato |
| cookie | `string` | Restituisce il cookie con il nome specificato |

**Predicato**

| **Proprietà** | **Tipo** | **Descrizione** |
|---|---|---|
| **è uguale a** | `string` | true se il risultato del getter è uguale al valore specificato |
| **doesNotEqual** | `string` | true se il risultato del getter non è uguale al valore specificato |
| **mi piace** | `string` | true se il risultato del getter corrisponde al pattern specificato |
| **notLike** | `string` | true se il risultato del getter non corrisponde al pattern specificato |
| **matches** | `string` | true se il risultato del getter corrisponde a regex fornito |
| **doesNotMatch** | `string` | true se il risultato del getter non corrisponde al regex specificato |
| **in** | `array[string]` | true se l’elenco fornito contiene un risultato getter |
| **notIn** | `array[string]` | true se l’elenco fornito non contiene il risultato getter |

**Elenco wafRules**

Il `wafRules` La proprietà può includere le seguenti regole:

| **ID regola** | **Nome regola** | **Descrizione** |
|---|---|---|
| SQLI | SQL Injection | SQL Injection è il tentativo di accedere a un&#39;applicazione o di ottenere informazioni con privilegi tramite l&#39;esecuzione di query arbitrarie nel database. |
| BACKDOOR | Backdoor | Un segnale backdoor è una richiesta che tenta di determinare se un file backdoor comune è presente sul sistema. |
| CMDEXE | Esecuzione comando | Esecuzione comando è il tentativo di ottenere il controllo o danneggiare un sistema di destinazione attraverso comandi arbitrari di sistema mediante l&#39;input dell&#39;utente. |
| XSS | Scripting tra siti | Per vulnerabilità cross-site scripting si intende il tentativo di dirottare l’account o la sessione di navigazione web di un utente attraverso codice JavaScript dannoso. |
| ATTRAVERSAMENTO | Directory Traversal | Directory Traversal è il tentativo di spostarsi tra le cartelle privilegiate all&#39;interno di un sistema nella speranza di ottenere informazioni riservate. |
| USERAGENT | Attrezzatura attacco | Attack Tooling è l&#39;uso di software automatizzato per identificare le vulnerabilità di sicurezza o per tentare di sfruttare una vulnerabilità scoperta. |
| LOG4J-JNDI | JNDI Log4J | Gli attacchi JNDI Log4J tentano di sfruttare il [Vulnerabilità Log4Shell](https://en.wikipedia.org/wiki/Log4Shell) presente nelle versioni Log4J precedenti alla 2.16.0 |
| AWS SSRF | AWS-SSRF | SSRF (Server Side Request Forgery) è una richiesta che tenta di inviare richieste effettuate dall’applicazione web a sistemi interni di destinazione. Gli attacchi SSRF di AWS utilizzano SSRF per ottenere le chiavi di Amazon Web Services (AWS) e ottenere l’accesso ai bucket S3 e ai relativi dati. |
| BHH | Intestazioni hop non valide | Le intestazioni hop non valide indicano un tentativo di contrabbando HTTP tramite un&#39;intestazione di codifica di trasferimento (TE) o lunghezza dei contenuti (CL) non valida oppure tramite un&#39;intestazione TE e CL ben formata |
| PERCORSO ANOMALO | Percorso anormale | Percorso anormale indica che il percorso originale è diverso dal percorso normalizzato (ad esempio, `/foo/./bar` è normalizzato su `/foo/bar`) |
| COMPRESSO | Compressione rilevata | Il corpo della richiesta POST è compresso e non può essere esaminato. Ad esempio, se è specificata un’intestazione di richiesta &quot;Content-Encoding: gzip&quot; e il corpo del POST non è un testo normale. |
| DOUBLEENCODING | Doppia codifica | La doppia codifica verifica la tecnica di evasione dei caratteri HTML a doppia codifica |
| FORCEFULBROWSING | Esplorazione forzata | La navigazione forzata è il tentativo non riuscito di accedere alle pagine di amministrazione |
| NOTUTF8 | Codifica non valida | Una codifica non valida può causare la conversione di caratteri dannosi da una richiesta a una risposta da parte del server, causando un rifiuto del servizio o XSS |
| ERRORE JSON | Errore di codifica JSON | Corpo della richiesta POST, PUT o PATCH specificato come contenente JSON nell’intestazione della richiesta &quot;Content-Type&quot;, ma contenente errori di analisi JSON. Questo è spesso correlato a un errore di programmazione o a una richiesta automatizzata o dannosa. |
| DATI NON VALIDI | Dati non validi nel corpo della richiesta | Corpo della richiesta POST, PUT o PATCH non valido in base all’intestazione della richiesta &quot;Content-Type&quot;. Ad esempio, se è specificata un’intestazione di richiesta &quot;Content-Type: application/x-www-form-urlencoded&quot; e contiene un corpo POST che è json. Spesso si tratta di un errore di programmazione, richiesta automatizzata o dannosa. Richiede l&#39;agente 3.2 o versione successiva. |
| SAN | Traffico IP dannoso | [SANS Internet Storm Center](https://isc.sans.edu/) elenco di indirizzi IP che sono stati segnalati come coinvolti in attività dannose |
| SIGSCI-IP | Effetto di rete | IP contrassegnato da SignalSciences: ogni volta che un IP viene contrassegnato a causa di un segnale dannoso da parte del motore decisionale, tale IP verrà propagato a tutti i clienti. Vengono quindi registrate le richieste successive dagli indirizzi IP che contengono un segnale aggiuntivo per la durata del flag |
| NO-CONTENT-TYPE | Intestazione di richiesta &quot;Content-Type&quot; mancante | Una richiesta POST, PUT o PATCH senza intestazione di richiesta &quot;Content-Type&quot;. Per impostazione predefinita, i server applicazioni devono assumere in questo caso &quot;Content-Type: text/plain; charset=us-ascii&quot;. In molte richieste automatizzate e dannose potrebbe mancare il &quot;Tipo di contenuto&quot;. |
| SOSTANTIVO | Nessun agente utente | Molte richieste automatizzate e dannose utilizzano agenti utente falsi o mancanti per rendere difficile identificare il tipo di dispositivo che effettua le richieste. |
| TORNODO | Traffico Tor | Tor è un software che nasconde l&#39;identità di un utente. Un picco nel traffico di Tor può indicare che un aggressore sta cercando di mascherare la sua posizione. |
| DATACENTER | Traffico datacenter | Il traffico del centro dati è traffico non organico proveniente da provider di hosting identificati. Questo tipo di traffico non è comunemente associato a un utente finale reale. |
| NULLBYTE | Byte Null | I byte Null non vengono in genere visualizzati in una richiesta e indicano che la richiesta è in formato non corretto e potenzialmente dannoso. |
| IMPOSTORE | Impostazione SearchBot | L&#39;impostore del bot di ricerca è qualcuno che finge di essere un bot di ricerca Google o Bing, ma che non è legittimo. Nota: non dipende da una risposta di per sé, ma deve essere risolta prima nel cloud, pertanto non deve essere utilizzata in una regola preliminare. |
| PRIVATEFILE | File privati | I file privati sono di solito di natura riservata, ad esempio un Apache `.htaccess` o un file di configurazione che potrebbe causare la perdita di informazioni riservate |
| SCANNER | Scanner | Identifica i servizi e gli strumenti di scansione più diffusi |
| RESPONSESPLIT | Suddivisione risposta HTTP | Identifica quando i caratteri CRLF vengono inviati come input all’applicazione per inserire le intestazioni nella risposta HTTP |
| XML-ERROR | Errore di codifica XML | Corpo della richiesta POST, PUT o PATCH specificato come contenente XML nell&#39;intestazione della richiesta &quot;Content-Type&quot;, ma contenente errori di analisi XML. Questo è spesso correlato a un errore di programmazione o a una richiesta automatizzata o dannosa. |

## Considerazioni {#considerations}

* Quando vengono create due regole in conflitto, le regole consentite avranno sempre la precedenza sulle regole del blocco. Ad esempio, se crei una regola per bloccare un percorso specifico e una regola per consentire un indirizzo IP specifico, le richieste provenienti da tale indirizzo IP sul percorso bloccato saranno consentite.

* Se una regola viene rilevata e bloccata, la rete CDN risponde con un `406` codice restituito.

## Esempi {#examples}

Di seguito sono riportati alcuni esempi di regole. Consulta la [sezione limite di tasso](#rules-with-rate-limits) ulteriori dettagli per esempi di limitazione delle aliquote.

**Esempio 1**

Questa regola blocca le richieste provenienti da IP 192.168.1.1:

```
data:
  rules:
    - name: "block-request-from-ip"
      when: { reqProperty: clientIp, equals: "192.168.1.1" }
      action: block
```

**Esempio 2**

Questa regola blocca le richieste nel percorso `/helloworld` al momento della pubblicazione con un agente utente contenente Chrome:

```
data:
  rules:
    - name: "block-request-from-chrome-on-path-helloworld-for-publish-tier"
      when:
        allOf:
          - { reqProperty: path, equals: /helloworld }
          - { reqProperty: tier, equals: publish }
          - { reqHeader: user-agent, matches: '.*Chrome.*'  }
      action: block
```

**Esempio 3**

Questa regola blocca le richieste che contengono il parametro di query `foo`, ma consente ogni richiesta proveniente da IP 192.168.1.1:

```
data:
  rules:
    - name: "block-request-that-contains-query-parameter-foo"
      when: { queryParam: url-param, equals: foo }
      action: block
    - name: "allow-all-requests-from-ip"
      when: { reqProperty: clientIp, equals: 192.168.1.1 }
      action: allow
```

**Esempio 4**

Questa regola blocca le richieste al percorso /block-me e ogni richiesta che corrisponde a un modello SQLI o XSS:

```
data:
  rules:
    - name: "path-rule"
      when: { reqProperty: path, equals: /block-me }
      action: block

    - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
      when: { reqProperty: path, like: "*" }
      action: enableWafRules
      wafRules:
        - SQLI
        - XSS
```

## Regole con limiti di tariffa {#rules-with-rate-limits}

A volte è auspicabile bloccare il traffico che corrisponde a una regola solo se la corrispondenza supera una determinata velocità nel tempo. Impostazione di un valore per `rateLimit` limita la frequenza delle richieste che corrispondono alla condizione della regola.

### struttura rateLimit {#ratelimit-structure}

| **Proprietà** | **Tipo** | **Valore predefinito** | **Descrizione** |
|---|---|---|---|
| limit | numero intero compreso tra 10 e 10000 | obbligatorio | Frequenza di richieste al secondo per le quali viene attivata la regola |
| finestra | numero intero: 1, 10 o 60 | 10 | Finestra di campionamento in secondi per la quale viene calcolata la frequenza di richiesta |
| penalità | numero intero compreso tra 60 e 3600 | 300 (5 minuti) | Un periodo in secondi per il quale le richieste corrispondenti vengono bloccate (arrotondato al minuto più vicino) |

### Esempi {#ratelimiting-examples}

Esempio 1: quando la frequenza di richieste supera le 100 richieste al secondo negli ultimi 60 secondi, blocca `/critical/resource` per 60 secondi

```
- name: rate-limit-example
  when: { reqProperty: /critical/resource }
  action: block
  rateLimit: { limit: 100, window: 60, penalty: 60 }
```

Esempio 2: quando la frequenza di richieste supera le 10 richieste al secondo in 10 secondi, blocca la risorsa per 300 secondi:

```
- name: rate-limit-using-defaults
  when: { reqProperty: /critical/resource }
  action: block
  rateLimit:
    limit: 10
```

## Registri CDN {#cdn-logs}

AEM as a Cloud Service fornisce accesso ai registri CDN, utili per i casi d’uso, tra cui l’ottimizzazione del rapporto hit della cache e la configurazione delle regole CDN e WAF. I registri CDN vengono visualizzati in Cloud Manager **Scarica registri** durante la selezione del servizio Author o Publish.

Il nome della regola viene visualizzato nella proprietà rules se la richiesta corrisponde alla regola, anche se l’azione è &quot;allow&quot; e pertanto il traffico non è bloccato.

Le regole CDN corrispondenti vengono visualizzate nella voce di registro per tutte le richieste alla CDN, indipendentemente dal fatto che si tratti di un hit, di un passaggio o di un mancato recapito della CDN. Tuttavia, le regole WAF vengono visualizzate nella voce di registro solo per le richieste alla rete CDN considerate mancanti o passate alla rete CDN, ma non per gli hit della rete CDN.

L’esempio seguente mostra un esempio `cdn.yaml` e due voci di registro CDN, con valori non vuoti nella proprietà rules a causa di richieste bloccate che corrispondono rispettivamente alla regola CDN e alla regola WAF.


```
data:
  rules:
    - name: "path-rule"
      when: { reqProperty: path, equals: /block-me }
      action: block

    - name: "Enable-SQL-Injection-and-XSS-waf-rules-globally"
      when: { reqProperty: path, like: "*" }
      action: enableWafRules
      wafRules:
        - SQLI
        - XSS
```

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cip": "147.160.230.112",
"rid": "974e67f6",
"host": "example.com",
"url": "/block-me",
"req_mthd": "GET",
"res_type": "",
"cache": "PASS",
"res_status": 406,
"res_bsize": 3362,
"server": "PAR",
"rules": "cdn=path-rule;waf=;action=blocked"
}
```

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cip": "147.160.230.112",
"rid": "974e67f6",
"host": "example.com",
"url": "/?sqli=%27%29%20UNION%20ALL%20SELECT%20NULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL%2CNULL--%20fAPK",
"req_mthd": "GET",
"res_type": "",
"cache": "PASS",
"res_status": 406,
"res_bsize": 3362,
"server": "PAR",
"rules": "cdn=;waf=SQLI;action=blocked"
}
```

### Formato registro {#cdn-log-format}

Di seguito è riportato un elenco dei nomi dei campi utilizzati nei registri CDN, con una breve descrizione.

| **Nome campo** | **Descrizione** |
|---|---|
| *timestamp* | Ora di inizio della richiesta, dopo la chiusura di TLS |
| *ttfb* | Abbreviazione per *Tempo al primo byte*. L’intervallo di tempo tra la richiesta iniziata fino al punto prima che il corpo della risposta iniziasse a essere trasmesso in streaming. |
| *cip* | Indirizzo IP del client. |
| *rid* | Il valore dell’intestazione della richiesta utilizzata per identificare in modo univoco la richiesta. |
| *host* | Autorità a cui è destinata la richiesta. |
| *url* | Il percorso completo, inclusi i parametri di query. |
| *req_mthd* | Metodo HTTP inviato dal client, ad esempio &quot;GET&quot; o &quot;POST&quot;. |
| *res_type* | Tipo di contenuto utilizzato per indicare il tipo di file multimediale originale della risorsa |
| *cache* | Stato della cache. I valori possibili sono HIT, MISS o PASS |
| *res_status* | Il codice di stato HTTP come valore intero. |
| *res_bsize* | Byte del corpo inviati al client nella risposta. |
| *server* | Datacenter del server cache CDN. |
| *regole* | Il nome di qualsiasi regola corrispondente, sia per le regole CDN che per quelle waf.<br><br>Le regole CDN corrispondenti vengono visualizzate nella voce di registro per tutte le richieste alla CDN, indipendentemente dal fatto che si tratti di un hit, di un passaggio o di un mancato recapito della CDN.<br><br>Indica anche se la corrispondenza ha prodotto un blocco. <br><br>Ad esempio, &quot;`cdn=;waf=SQLI;action=blocked`&quot;<br><br>Vuoto se non corrisponde alcuna regola. |
