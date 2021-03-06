---
title: Riferimento predicato di Query Builder
description: Riferimento predicato per l’API di Query Builder.
exl-id: 77118ef7-4d29-470d-9c4b-20537a408940
source-git-commit: c08e442e58a4ff36e89a213aa7b297b538ae3bab
workflow-type: tm+mt
source-wordcount: '2218'
ht-degree: 2%

---

# Riferimento predicato di Query Builder {#query-builder-predicate-reference}

## Generale {#general}

### root {#root}

Questo è il gruppo di predicati radice. Supporta tutte le funzionalità di un gruppo e consente di impostare parametri di query globali.

Il nome &quot;root&quot; non viene mai utilizzato in una query, è implicito.

#### Proprietà {#properties-18}

* **`p.offset`** - numero che indica l’inizio della pagina dei risultati, ovvero quanti elementi saltare
* **`p.limit`** - numero che indica le dimensioni della pagina
* **`p.guessTotal`** - consigliato: evitare di calcolare il totale del risultato complessivo che può essere costoso; un numero che indica il totale massimo da conteggiare fino a (ad esempio 1000, un numero che fornisce agli utenti un feedback sufficiente sulle dimensioni approssimative e sui numeri esatti per risultati più piccoli) o `true` per contare solo fino al minimo necessario `p.offset` + `p.limit`
* **`p.excerpt`** - se impostato su `true`, include estratto di testo completo nel risultato
* **`p.hits`** - (solo per il servlet JSON) seleziona il modo in cui gli hit vengono scritti come JSON, con quelli standard (estensibili tramite il servizio ResultHitWriter):
   * **`simple`** - elementi minimi come `path`, `title`, `lastmodified`, `excerpt` (se impostato)
   * **`full`** - rendering JSON sling del nodo, con `jcr:path` indica il percorso dell&#39;hit: per impostazione predefinita elenca solo le proprietà dirette del nodo, includi una struttura più profonda con `p.nodedepth=N`, con 0 che significa l&#39;intero sottoalbero infinito; add `p.acls=true` per includere le autorizzazioni JCR della sessione corrente sull&#39;elemento risultato dato (mappature: `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`)
   * **`selective`** - solo le proprietà specificate in `p.properties`, che è uno spazio separato (usa `+` in URL) elenco dei percorsi relativi; se il percorso relativo ha una profondità `>1` che saranno rappresentati come oggetti secondari; la speciale `jcr:path` include il percorso dell&#39;hit

### gruppo {#group}

Questo predicato consente di creare condizioni nidificate. I gruppi possono contenere gruppi nidificati. Tutto in una query Query Builder si trova implicitamente in un gruppo principale, che può avere `p.or` e `p.not` anche i parametri.

Di seguito è riportato un esempio di corrispondenza tra una delle due proprietà e un valore:

```text
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

Questo è concettualmente `(1_property` O `2_property)`.

Di seguito è riportato un esempio per i gruppi nidificati:

```text
fulltext=Management
group.p.or=true
group.1_group.path=/content/wknd/ch/de
group.1_group.type=cq:Page
group.2_group.path=/content/dam/wknd
group.2_group.type=dam:Asset
```

Cerca il termine **Gestione** all’interno di pagine in `/content/wknd/ch/de` o in attività `/content/dam/wknd`.

Questo è concettualmente `fulltext AND ( (path AND type) OR (path AND type) )`. Tieni presente che tali join OR necessitano di buoni indici per motivi di prestazioni.

#### Proprietà {#properties-6}

* **`p.or`** - se impostato su `true`, solo un predicato nel gruppo deve corrispondere. Questa impostazione predefinita `false`, ovvero tutti devono corrispondere
* **`p.not`** - se impostato su `true`nega il gruppo (impostazione predefinita `false`)
* **`<predicate>`** - aggiunge predicati nidificati
* **`N_<predicate>`** - aggiunge più predicati nidificati della stessa volta, come `1_property, 2_property, ...`

### ordine {#orderby}

Questo predicato consente di ordinare i risultati. Se l’ordinamento è richiesto da più proprietà, questo predicato deve essere aggiunto più volte utilizzando il prefisso del numero, ad esempio `1_orderby=first`, `2_oderby=second`.

#### Proprietà {#properties-13}

* **`orderby`** - nome della proprietà JCR indicato da una @ iniziale, ad esempio `@jcr:lastModified` o `@jcr:content/jcr:title`, o un altro predicato nella query, ad esempio `2_property`, su cui ordinare
* **`sort`** - ordinare la direzione `desc` per decrescente o `asc` per crescente (predefinito)
* **`case`** - se impostato su `ignore` farà sì che l’ordinamento non faccia distinzione tra maiuscole e minuscole, ovvero `a` viene prima `B`; se vuoto o mancante, l’ordinamento è sensibile a maiuscole e minuscole, ovvero `B` viene prima `a`

## Predicati {#predicates}

### boolproperty {#boolproperty}

Questo predicato corrisponde alle proprietà booleane JCR. Accetta solo i valori `true` e `false`. In caso di `false`, corrisponderà se la proprietà ha il valore `false` o se non esiste affatto. Questo può essere utile per verificare la presenza di flag booleani impostati solo quando sono abilitati.

L&#39;ereditato `operation` Il parametro non ha alcun significato.

Questo predicato supporta l’estrazione dei facet e fornisce bucket per ogni `true` o `false` ma solo per le proprietà esistenti.

#### Proprietà {#properties}

* **`boolproperty`** - percorso relativo alla proprietà, ad esempio `myFeatureEnabled` o `jcr:content/myFeatureEnabled`
* **`value`** - valore per il quale verificare la proprietà, `true` o `false`

### contentfragment {#contentfragment}

Questo predicato limita il risultato ai frammenti di contenuto.

* Non supporta il filtro.
* Non supporta l’estrazione dei facet.

#### Proprietà {#properties-1}

* **`contentfragment`** - Può essere utilizzato con qualsiasi valore per verificare la presenza di frammenti di contenuto.

### `dateComparison` {#datecomparison}

Questo predicato confronta due proprietà della data JCR tra loro. Può verificare se sono uguali, ineguali, maggiori o maggiori di o uguali.

Questo è un predicato di sola filtrazione e non può sfruttare un indice di ricerca.

#### Proprietà {#properties-2}

* **`property1`** - percorso della proprietà prima data
* **`property2`** - percorso della proprietà della seconda data
* **`operation`**
   * `=` per corrispondenza esatta (predefinito)
   * `!=` per il confronto delle disuguaglianze
   * `>` per `property1` maggiore di `property2`
   * `>=` per `property1` maggiore o uguale a `property2`

### daterange {#daterange}

Questo predicato corrisponde alle proprietà della data JCR rispetto a un intervallo data/ora. Questo utilizza il formato ISO8601 per date e ore (`YYYY-MM-DDTHH:mm:ss.SSSZ`) e consente anche rappresentazioni parziali, come `YYYY-MM-DD`. In alternativa, la marca temporale può essere fornita come ora POSIX.

Puoi cercare qualsiasi elemento tra due marche temporali, più recenti o più vecchie di una data specificata, e puoi anche scegliere tra intervalli inclusivi e aperti.

Supporta l’estrazione dei facet e fornisce bucket `today`, `this week`, `this month`, `last 3 months`, `this year`, `last year`e `earlier than last year`.

Non supporta il filtro.

#### Proprietà {#properties-3}

* **`property`** - percorso relativo a un `DATE` ad esempio `jcr:lastModified`
* **`lowerBound`** - data inferiore associata a controllare la proprietà per, ad esempio `2014-10-01`
* **`lowerOperation`** - `>` (più recente) o `>=` (a o più recente), si applica al `lowerBound`. Il valore predefinito è `>`
* **`upperBound`** - limite superiore per controllare la proprietà, ad esempio `2014-10-01T12:15:00`
* **`upperOperation`** - `<` (precedente) o `<=` (a partire da), si applica al `upperBound`. Il valore predefinito è `<`
* **`timeZone`** - ID del fuso orario da utilizzare quando non viene fornito come stringa di data ISO-8601. L’impostazione predefinita è il fuso orario predefinito del sistema.

### excludepaths {#excludepaths}

Questo predicato esclude i nodi dal risultato in cui il loro percorso corrisponde a un&#39;espressione regolare.

Questo è un predicato di sola filtrazione e non può sfruttare un indice di ricerca.

Non supporta l’estrazione dei facet.

#### Proprietà {#properties-4}

* **`excludepaths`** - espressione regolare confrontata con i percorsi dei risultati, esclusi quelli corrispondenti dal risultato.

### fulltext {#fulltext}

Questo predicato cerca i termini nell&#39;indice fulltext.

Non supporta il filtro.

Non supporta l’estrazione dei facet.

#### Proprietà {#properties-5}

* **`fulltext`** - i termini di ricerca a testo intero
* **`relPath`** - il percorso relativo da cercare nella proprietà o nel sottonodo. Questa proprietà è facoltativa.

### hasPermission {#haspermission}

Questo predicato limita il risultato agli elementi in cui la sessione corrente ha il [Privilegi JCR.](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

Questo è un predicato di sola filtrazione e non può sfruttare un indice di ricerca. Non supporta l’estrazione dei facet.

#### Proprietà {#properties-7}

* **`hasPermission`** - privilegi JCR separati da virgole che la sessione utente corrente deve avere ALL per il nodo in questione; per esempio `jcr:write`, `jcr:modifyAccessControl`

### language {#language}

Questo predicato trova AEM pagine in una lingua specifica. Osserva sia la proprietà della lingua della pagina che il percorso della pagina, che spesso include la lingua o le impostazioni internazionali in una struttura del sito di primo livello.

Questo è un predicato di sola filtrazione e non può sfruttare un indice di ricerca.

Supporta l’estrazione dei facet e fornisce bucket per ogni codice di lingua univoco.

#### Proprietà {#properties-8}

* **`language`** - Codice della lingua ISO, ad esempio `de`

### principale {#mainasset}

Questo predicato controlla se un nodo è una risorsa principale DAM e non una risorsa secondaria. In pratica si tratta di ogni nodo non all’interno di un nodo di risorse secondarie. Tieni presente che questo non controlla la `dam:Asset` tipo di nodo. Per utilizzare questo predicato, imposta semplicemente `mainasset=true` o `mainasset=false`. Non ci sono altre proprietà.

Questo è un predicato di sola filtrazione e non può sfruttare un indice di ricerca.

Supporta l’estrazione dei facet e fornisce due bucket per le risorse principali e secondarie.

#### Proprietà {#properties-9}

* **`mainasset`** - booleano, `true` per le attività principali, `false` per le attività secondarie

### MemberOf {#memberof}

Questo predicato individua gli elementi che sono membri di un [raccolta di risorse sling](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

Questo è un predicato di sola filtrazione e non può sfruttare un indice di ricerca.

Non supporta l’estrazione dei facet.

#### Proprietà {#properties-10}

* **`memberOf`** - percorso della raccolta di risorse Sling

### nodename {#nodename}

Questo predicato corrisponde ai nomi dei nodi JCR.

Supporta l’estrazione dei facet e fornisce bucket per ogni nome di nodo univoco (nome del file).

#### Proprietà {#properties-11}

* **`nodename`** - pattern di nome del nodo che consente l’utilizzo di caratteri jolly: `*` = qualsiasi o nessun carattere, `?` = qualsiasi carattere, `[abc]` = solo caratteri tra parentesi

### non scaduto {#notexpired}

Questo predicato corrisponde agli elementi controllando se una proprietà data JCR è maggiore o uguale all&#39;ora server corrente. Può essere utilizzato per controllare un `expiresAt` e limita i risultati solo a quelli non ancora scaduti (`notexpired=true`) o che sono già scaduti (`notexpired=false`).

Non supporta il filtro.

Supporta l’estrazione dei facet nello stesso modo della [`daterange`](#daterange) predicato.

#### Proprietà {#properties-12}

* **`notexpired`** - booleano, `true` non ancora scaduto (data futura o uguale), `false` per scaduto (data passata) (obbligatorio)
* **`property`** - percorso relativo `DATE` proprietà da controllare (obbligatorio)

### path {#path}

Questo predicato esegue ricerche all’interno di un determinato percorso.

Non supporta l’estrazione dei facet.

#### Proprietà {#properties-14}

* **`path`** - Definisce il pattern del percorso.
   * A seconda del `exact` l&#39;intera sottostruttura corrisponderà (come l&#39;aggiunta `//*` in xpath, ma nota che questo non include il percorso di base) o solo una corrispondenza esatta del percorso, che può includere caratteri jolly (`*`).
      * Impostazione predefinita `true`
   * Se la `self`viene impostata e viene eseguita la ricerca dell&#39;intero sottoalbero, incluso il nodo base.
* **`exact`** - se `exact` è `true`, il percorso esatto deve corrispondere, ma può contenere caratteri jolly semplici (`*`), che corrispondono ai nomi, ma non `/`; se `false` (impostazione predefinita) sono inclusi tutti i discendenti (facoltativo)
* **`flat`** - cerca solo gli elementi figlio diretti (come aggiungere `/*` in xpath) (utilizzato solo se `exact` non è true, facoltativo)
* **`self`** - esegue la ricerca nella sottostruttura ma include il nodo di base specificato come percorso (nessun carattere jolly)

### proprietà {#property}

Questo predicato corrisponde alle proprietà JCR e ai loro valori.

Supporta l’estrazione dei facet e fornisce bucket per ogni valore di proprietà univoco nei risultati.

#### Proprietà {#properties-15}

* **`property`** - percorso relativo alla proprietà, ad esempio `jcr:title`
* **`value`** - valore da controllare per la proprietà; segue il tipo di proprietà JCR in conversioni stringa
* **`N_value`** - uso `1_value`, `2_value`, ... per controllare più valori (combinati con `OR` per impostazione predefinita, con `AND` if `and=true`)
* **`and`** - impostare `true` per combinare più valori (`N_value`) con `AND`
* **`operation`**
   * `equals` per corrispondenza esatta (predefinito)
   * `unequals` per il confronto delle disuguaglianze
   * `like` per utilizzare `jcr:like` funzione xpath (opzionale)
   * `not` per nessuna corrispondenza (ad es. `not(@prop)` in xpath, il parametro del valore verrà ignorato)
   * `exists` verifica dell&#39;esistenza
      * `true` la proprietà deve esistere
      * `false` è uguale a `not` ed è l&#39;impostazione predefinita
* **`depth`** - numero di livelli di caratteri jolly al di sotto dei quali può esistere la proprietà/percorso relativo (ad esempio, `property=size depth=2` controllerà `node/size`, `node/*/size` e `node/*/*/size`)

### rangeproperty {#rangeproperty}

Questo predicato corrisponde a una proprietà JCR rispetto a un intervallo. Questo vale per le proprietà con tipi lineari quali `LONG`, `DOUBLE` e `DECIMAL`. Per `DATE` per favore, vedi [`daterange`](#daterange) predicato con input del formato data ottimizzato.

È possibile definire un limite inferiore, un limite superiore o entrambi. L&#39;operazione (ad esempio minore o minore o uguale a) può essere specificata anche singolarmente per i limiti inferiore e superiore.

Non supporta l’estrazione dei facet.

#### Proprietà {#properties-16}

* **`property`** - percorso relativo alla proprietà
* **`lowerBound`** - limite inferiore alla proprietà check
* **`lowerOperation`** - `>` (predefinito) o `>=`, si applica al `lowerValue`
* **`upperBound`** - limite superiore alla proprietà check
* **`upperOperation`** - `<` (predefinito) o `<=`, si applica al `lowerValue`
* **`decimal`** - `true` se la proprietà selezionata è di tipo Decimal

### relativa {#relativedaterange}

Questa corrispondenza del predicato `JCR DATE` proprietà rispetto a un intervallo data/ora che utilizza scostamenti di tempo relativi all&#39;ora del server corrente. Puoi specificare `lowerBound` e `upperBound` utilizzando un valore di millisecondi o la sintassi Bugzilla `1s 2m 3h 4d 5w 6M 7y` (un secondo, due minuti, tre ore, quattro giorni, cinque settimane, sei mesi, sette anni). Prefisso con `-` per indicare un offset negativo prima del tempo corrente. Se specifichi solo `lowerBound` o `upperBound`, l’altro viene impostato come impostazione predefinita su `0`, che rappresenta l&#39;ora corrente.

Ad esempio:

* `upperBound=1h` (e no) `lowerBound`) seleziona qualsiasi elemento nell&#39;ora successiva
* `lowerBound=-1d` (e no) `upperBound`) seleziona qualsiasi elemento nelle ultime 24 ore
* `lowerBound=-6M` e `upperBound=-3M` seleziona qualsiasi elemento negli ultimi 3-6 mesi
* `lowerBound=-1500` e `upperBound=5500` seleziona qualsiasi cosa tra i 1500 millisecondi e i 5500 millisecondi futuri
* `lowerBound=1d` e `upperBound=2d` seleziona qualsiasi cosa dopodomani

Si noti che non prende in considerazione anni bisestili e tutti i mesi sono 30 giorni.

Non supporta il filtro.

Supporta l’estrazione dei facet nello stesso modo della [`daterange`](#daterange) predicato.

#### Proprietà {#properties-17}

* **`upperBound`** - data massima in millisecondi o `1s 2m 3h 4d 5w 6M 7y` (un secondo, due minuti, tre ore, quattro giorni, cinque settimane, sei mesi, sette anni) rispetto all&#39;ora del server corrente, utilizza `-` per offset negativo
* **`lowerBound`** - data limite in millisecondi o `1s 2m 3h 4d 5w 6M 7y` (un secondo, due minuti, tre ore, quattro giorni, cinque settimane, sei mesi, sette anni) rispetto all&#39;ora del server corrente, utilizza `-` per offset negativo

### savedquery {#savedquery}

Questo predicato include tutti i predicati di una query Query Builder persistente nella query corrente come predicato di sottogruppo.

Tieni presente che questa operazione non esegue una query aggiuntiva ma estende la query corrente.

Le query possono essere mantenute a livello di programmazione utilizzando `QueryBuilder#storeQuery()`. Il formato può essere di più righe `String` proprietà o `nt:file` nodo che contiene la query come file di testo in formato proprietà Java.

Non supporta l’estrazione dei facet per i predicati della query salvata.

#### Proprietà {#properties-19}

* **`savedquery`** - percorso della query salvata (`String` proprietà o `nt:file` nodo)

### simile {#similar}

Questo predicato è una ricerca per similarità utilizzando JCR XPath `rep:similar()`.

Non supporta il filtro e non supporta l’estrazione dei facet.

#### Proprietà {#properties-20}

* **`similar`** - percorso assoluto del nodo per il quale trovare nodi simili
* **`local`** - un percorso relativo a un nodo discendente o `.` per il nodo corrente (facoltativo, il valore predefinito è `.`)

### tag {#tag}

Questo predicato cerca il contenuto con uno o più tag, specificando i percorsi del titolo del tag.

Supporta l’estrazione dei facet e fornisce bucket per ogni tag univoco, utilizzando il percorso del titolo del tag corrente.

#### Proprietà {#properties-21}

* **`tag`** - percorso del titolo del tag da cercare, ad esempio `properties:orientation/landscape`
* **`N_value`** - uso `1_value`, `2_value`, ... per controllare più tag (combinati con `OR` per impostazione predefinita, con `AND` if `and=true`)
* **`property`** - proprietà (o percorso relativo alla proprietà) da esaminare (impostazione predefinita) `cq:tags`)

### tagid {#tagid}

Questo predicato cerca il contenuto con tag di uno o più tag, specificando ID di tag.

Supporta l’estrazione dei facet e fornisce bucket per ogni tag univoco, utilizzando il loro ID tag corrente.

#### Proprietà {#properties-22}

* **`tagid`** - ID tag da cercare, ad esempio `properties:orientation/landscape`
* **`N_value`** - uso `1_value`, `2_value`, ... per verificare la presenza di più ID tag (combinati con `OR` per impostazione predefinita, con `AND` if `and=true`)
* **`property`** - proprietà (o percorso relativo alla proprietà) da esaminare (impostazione predefinita) `cq:tags`)

### tagsearch {#tagsearch}

Questo predicato cerca il contenuto con uno o più tag, specificando le parole chiave. In questo modo si cercherà innanzitutto i tag contenenti queste parole chiave nei loro titoli, quindi si limiterà il risultato solo agli elementi con tag.

Non supporta l’estrazione dei facet.

#### Proprietà {#Properties-1}

* **`tagsearch`** - parola chiave da cercare nei titoli dei tag
* **`property`** - proprietà (o percorso relativo alla proprietà) da considerare (impostazione predefinita) `cq:tags`)
* **`lang`** - per cercare solo un titolo di tag localizzato (ad es. `de`)
* **`all`** - valore booleano per cercare l’intero tag fulltext, ovvero tutti i titoli, la descrizione, ecc. (ha la precedenza su `lang`)

### tipo {#type}

Questo predicato limita i risultati a uno specifico tipo di nodo JCR, sia i tipi di nodo primario che i tipi di mixin. Verranno inoltre trovati sottotipi di quel tipo di nodo. Gli indici di ricerca del repository devono coprire i tipi di nodo per un&#39;esecuzione efficiente.

Supporta l’estrazione dei facet e fornisce bucket per ogni tipo univoco nei risultati.

#### Proprietà {#Properties-2}

* **`type`** - tipo di nodo o nome mixin da cercare, ad esempio `cq:Page`
