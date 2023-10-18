---
title: Configurazione delle regole del filtro del traffico con le regole WAF
description: Utilizzare le regole di filtro del traffico con le regole WAF per filtrare il traffico
exl-id: 6a0248ad-1dee-4a3c-91e4-ddbabb28645c
source-git-commit: 9345ec974c9fbd525b12b53d20d98809cd72cb04
workflow-type: tm+mt
source-wordcount: '3810'
ht-degree: 1%

---

# Configurazione delle regole del filtro del traffico con le regole WAF per filtrare il traffico {#configuring-cdn-and-waf-rules-to-filter-traffic}

>[!NOTE]
>
>Questa funzione non è ancora disponibile al pubblico. Per aderire al programma di adozione anticipata in corso, invia un messaggio e-mail a **aemcs-waf-adopter@adobe.com**, incluso il nome dell’organizzazione e il contesto relativi al tuo interesse per la funzione.

Adobe tenta di mitigare gli attacchi contro i siti web dei clienti, ma può essere utile filtrare in modo proattivo il traffico che corrisponde a determinati modelli in modo che il traffico dannoso non raggiunga l’applicazione. I possibili approcci includono:

* Moduli di livello Apache come `mod_security`
* Configurazione delle regole del filtro del traffico distribuite nella rete CDN tramite la pipeline di configurazione di Cloud Manager

Questo articolo descrive l’approccio alle regole del filtro del traffico. La maggior parte di queste regole blocca o consente le richieste in base alle proprietà e alle intestazioni delle richieste, inclusi IP, percorsi e agente utente. Queste regole possono essere configurate da tutti i clienti AEM as a Cloud Service Sites e Forms.

I clienti che dispongono di una licenza per il componente aggiuntivo WAF (Web Application Firewall) possono anche configurare una categoria aggiuntiva di regole denominata &quot;regole del filtro del traffico WAF&quot; (o regole WAF in breve). Queste regole WAF bloccano le richieste che corrispondono a vari pattern noti per essere associati a traffico dannoso. Contatta il team del tuo account di Adobe per informazioni dettagliate sulla concessione della licenza per questa funzionalità in arrivo. Si noti che non è richiesta alcuna licenza aggiuntiva durante il primo programma dell&#39;utente.

Le regole del filtro del traffico possono essere distribuite a tutti i tipi di ambiente cloud (RDE, dev, stage, prod) nei programmi di produzione (non sandbox).

## Configurazione {#setup}

1. Innanzitutto, crea la seguente cartella e struttura di file nella cartella di livello principale in Git:

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

Il parametro &quot;tipo&quot; deve essere impostato su &quot;CDN&quot; e la versione deve essere impostata sulla versione dello schema, attualmente &quot;1&quot;. Vedi gli esempi di seguito.


<!-- Two properties -- `envType` and `envId` -- may be included to limit the scope of the rules. The envType property may have values "dev", "stage", or "prod", while the envId property is the environment (e.g., "53245"). This approach is useful if it is desired to have a single configuration pipeline, even if some environments have different rules. However, a different approach could be to have multiple configuration pipelines, each pointing to different repositories or git branches. -->

1. Per configurare le regole WAF, è necessario che WAF sia abilitato in Cloud Manager, come descritto di seguito per gli scenari di programma nuovi ed esistenti. Si noti che per WAF deve essere acquistata una licenza separata.

   1. Per configurare WAF per un nuovo programma, selezionare **Protezione WAF-DDOS** casella di controllo in **Sicurezza** come mostrato di seguito. Continua seguendo i passaggi descritti in [Aggiungi programma di produzione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) per creare il programma

   1. Per configurare WAF su un programma esistente, selezionare **Modifica programma** seguendo i passaggi descritti nella sezione [Modifica dei programmi](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) documentazione. Quindi, nella **Sicurezza** della procedura guidata, è possibile deselezionare o selezionare l&#39;opzione WAF-DDOS in qualsiasi momento

1. Per tipi di ambiente diversi da RDE, esegui la pipeline di configurazione di Cloud Manager, che può essere configurata come descritto di seguito.

   1. Dalla scheda pipeline nella home page di Cloud Manager, seleziona **Aggiungi pipeline di produzione** o **Aggiungi pipeline non di produzione** per avviare la procedura guidata aggiungi pipeline
   1. Seleziona **Pipeline di implementazione** nella scheda di configurazione

      ![Seleziona l’opzione Pipeline di distribuzione](/help/security/assets/deployment.png)

   1. Assegna un nome alla pipeline e seleziona i trigger di distribuzione, quindi seleziona **Continua**
   1. In **Codice sorgente** , seleziona **Distribuzione mirata**, quindi seleziona **Config**

      ![Seleziona implementazione di destinazione](/help/security/assets/target-deployment.png)

   1. Seleziona l’archivio e il ramo in base alle esigenze. Se esiste una pipeline di configurazione per l’ambiente selezionato, questa selezione viene disabilitata.

      ![Panoramica di una pipeline di configurazione](/help/security/assets/config-pipeline.png)

      >[!NOTE]
      >
      > Per configurare o eseguire queste pipeline, gli utenti devono aver effettuato l’accesso come Responsabile dell’implementazione.
      > Inoltre, puoi configurare ed eseguire una sola pipeline di configurazione per ogni ambiente.

   1. Imposta la posizione del codice in cui è memorizzata la configurazione radice (esempio: /config).
   1. Seleziona **Salva**. La nuova pipeline verrà visualizzata nella scheda della pipeline e potrà essere eseguita quando sei pronto.
   1. Per gli RDE verrà utilizzata la riga di comando, ma al momento RDE non è supportato.

## Sintassi delle regole del filtro del traffico {#rules-syntax}

Puoi configurare `traffic filter rules` affinché corrisponda a pattern quali IP, agente utente, intestazioni di richiesta, nome host, geo e url.

I clienti che dispongono di una licenza per l’offerta WAF possono anche configurare una categoria speciale di regole per il filtro del traffico denominate `WAF traffic filter rules` (o regole WAF in breve) che fanno riferimento a uno o più flag WAF, elencati nella sezione corrispondente riportata di seguito.

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

Il formato delle regole del filtro del traffico nel file cdn.yaml è descritto di seguito. Consulta alcuni esempi in una sezione successiva.


| **Proprietà** | **Regole filtro traffico più frequenti** | **Regole filtro traffico WAF** | **Tipo** | **Valore predefinito** | **Descrizione** |
|---|---|---|---|---|---|
| name | X | X | `string` | - | Nome regola (64 caratteri, può contenere solo caratteri alfanumerici e - ) |
| quando | X | X | `Condition` | - | La struttura di base è:<br><br>`{ <getter>: <value>, <predicate>: <value> }`<br><br>Vedi Sintassi della struttura delle condizioni di seguito, che descrive i getter, i predicati e come combinare più condizioni. |
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
| cookie | `string` | Restituisce il cookie con il nome specificato |

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

Il `wafFlags` la proprietà può includere quanto segue:

| **ID contrassegno** | **Nome contrassegno** | **Descrizione** |
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

* I file di configurazione non devono contenere segreti, in quanto potrebbero essere letti da chiunque abbia accesso all’archivio Git.

## Esempi di regole {#examples}

Di seguito sono riportati alcuni esempi di regole. Consulta la [sezione limite di tasso](#rules-with-rate-limits) ulteriori dettagli per esempi di limitazione delle aliquote.

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
         when: { reqProperty: clientIp, equals: "192.168.1.1" }
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

Questa regola blocca le richieste al percorso /block-me e ogni richiesta che corrisponde a un modello SQLI o XSS:

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

## Regole con limiti di tariffa {#rules-with-rate-limits}

A volte è auspicabile bloccare il traffico che corrisponde a una regola solo se la corrispondenza supera una determinata velocità nel tempo. Impostazione di un valore per `rateLimit` limita la frequenza delle richieste che corrispondono alla condizione della regola.

### struttura rateLimit {#ratelimit-structure}

| **Proprietà** | **Tipo** | **Predefiniti** | **SIGNIFICATO** |
|---|---|---|---|
| limit | numero intero da 10 a 10000 | obbligatorio | Frequenza delle richieste al secondo per le quali viene attivata la regola. |
| finestra | numero intero: 1, 10 o 60 | 10 | Finestra di campionamento in secondi per la quale viene calcolata la frequenza di richiesta. |
| penalità | numero intero compreso tra 60 e 3600 | 300 (5 minuti) | Un periodo in secondi per il quale le richieste corrispondenti vengono bloccate (arrotondato al minuto più vicino). |
| groupBy | array[Recuperatore] | nessuno | il contatore del limitatore di velocità verrà aggregato da un set di proprietà di richiesta (ad esempio clientIp). |

### Esempi {#ratelimiting-examples}

**Esempio 1**

Questa regola blocca un client per 5 m quando supera i 100 req/sec negli ultimi 60 sec:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  trafficFilters:
    - name: limit-requests-client-ip
      when:
        - reqProperty: tier
        - matches: "author|publish"
      rateLimit:
        limit: 60
        window: 10
        penalty: 300
        groupBy:
          - reqProperty: clientIp
      action: block
```

**Esempio 2**

Blocca richieste per 60 secondi nel percorso /critical/resource quando supera i 100 richieste/sec negli ultimi 60 secondi:

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

La proprietà &quot;rules&quot; descrive le regole del filtro di traffico corrispondenti e ha il seguente pattern:

```
"rules": "match=<matching-customer-named-rules-that-are-matched>,waf=<matching-WAF-rules>,action=<action_type>"
```

Ad esempio:

```
"rules": "match=Block-Traffic-under-private-folder,Enable-SQL-injection-everywhere,waf="SQLI,SANS",action=block"
```

Le regole si comportano nel modo seguente:

* il nome della regola dichiarato dal cliente di qualsiasi regola corrispondente verrà elencato nell&#39;attributo matches.
* l’attributo action specifica se le regole hanno avuto l’effetto di bloccare, consentire o registrare.
* se WAF è concesso in licenza e abilitato, l&#39;attributo waf elencherà tutte le regole waf rilevate, ad esempio SQLI; si noti che questo è indipendente dal nome dichiarato dal cliente, indipendentemente dal fatto che le regole waf siano elencate o meno nella configurazione.
* se nessuna regola dichiarata dal cliente corrisponde e nessuna regola waf corrisponde, la proprietà dell&#39;attributo rules sarà vuota.

In generale, le regole corrispondenti vengono visualizzate nella voce di registro per tutte le richieste alla rete CDN, indipendentemente dal fatto che si tratti di un hit, di un superamento o di un mancato recapito della rete CDN. Tuttavia, le regole WAF vengono visualizzate nella voce di registro solo per le richieste alla rete CDN considerate mancanti o passate alla rete CDN, ma non per gli hit della rete CDN.

L’esempio seguente mostra un esempio di cdn.yaml e due voci di registro CDN:


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

## Tutorial sugli strumenti del dashboard  {#dashboard-tooling}

Adobe fornisce un meccanismo per scaricare gli strumenti del dashboard sul computer per acquisire i registri CDN scaricati tramite Cloud Manager. Con questo strumento, puoi analizzare il traffico per scoprire le regole del filtro del traffico da dichiarare, incluse le regole WAF. Questa sezione fornisce innanzitutto alcune istruzioni per acquisire familiarità con gli strumenti del dashboard in un ambiente di sviluppo, seguite da indicazioni su come sfruttare tali conoscenze per creare regole in un ambiente di produzione.

I clienti che utilizzano anticipatamente le Regole del filtro del traffico devono richiedere un file zip della dashboard, contenente un file README che descrive come caricare il contenitore Docker e acquisire i registri CDN.


### Introduzione agli strumenti del dashboard {#dashboard-getting-familiar}

1. Crea una pipeline di configurazione non di produzione di Cloud Manager, associata a un ambiente di sviluppo. Seleziona innanzitutto l’opzione Pipeline di implementazione. Quindi seleziona Distribuzione mirata, Config, l’archivio, il ramo Git e imposta la posizione del codice su /config.

   ![Aggiungi implementazione di selezione pipeline non di produzione](/help/security/assets/waf-select-pipeline1.png)

   ![Aggiungi destinazione di selezione pipeline non di produzione](/help/security/assets/waf-select-pipeline2.png)


1. Nel workspace, crea una configurazione di cartella a livello principale e aggiungi un file denominato cdn.yaml, in cui dichiarerai una regola semplice, impostandola in modalità registro anziché in modalità di blocco.

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

1. Una volta implementata la configurazione, prova ad accedere a https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me utilizzando il browser web o con il comando curl seguente. Dovresti ricevere una pagina di errore 404 in quanto tale pagina non esiste.

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

1. Una volta implementata la configurazione, prova ad accedere a https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me utilizzando il browser web o con il comando curl seguente. Dovresti ricevere una pagina di errore 406 che indica che la richiesta è stata bloccata.

   ```
   curl -svo /dev/null https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com/log/me
   ```

1. Ancora una volta, scarica i registri CDN in Cloud Manager (nota: l’esposizione delle nuove richieste nei registri CDN può richiedere fino a 5 minuti) e importali negli strumenti della dashboard, come abbiamo fatto in precedenza. Al termine, aggiorna la dashboard. Come puoi vedere nella schermata seguente, le richieste a /log/me sono bloccate dalla nostra regola.

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
   echo "GET https://publish-pXXXXX-eYYYYYY.adobeaemcloud.com" | vegeta attack -duration=5s
   ```

1. Dopo aver eseguito lo strumento, puoi scaricare i registri CDN e acquisirli nel dashboard per verificare che la regola del limitatore di velocità sia stata attivata

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
      action: block
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
        action: block
        # Enable recommended WAF protections (only works if WAF is enabled for your environment)
        - name: block-waf-flags-globally
          when:
            reqProperty: tier
            matches: "author|publish"
          action:
            type: block
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
            type: allow
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

1. Ridistribuisci la configurazione

1. Eseguire iterazioni, analizzando frequentemente le dashboard.

