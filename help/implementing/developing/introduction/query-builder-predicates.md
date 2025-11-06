---
title: Riferimento predicato di Query Builder
description: Riferimento predicato per l’API Query Builder in AEM as a Cloud Service.
exl-id: 77118ef7-4d29-470d-9c4b-20537a408940
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2270'
ht-degree: 1%

---

# Riferimento predicato di Query Builder {#query-builder-predicate-reference}

## Generale {#general}

### radice {#root}

Gruppo di predicati radice. Supporta tutte le funzioni di un gruppo e consente di impostare parametri di query globali.

Il nome &quot;root&quot; non viene mai utilizzato in una query; è implicito.

#### Proprietà {#properties-18}

* **`p.offset`** - numero che indica l&#39;inizio della pagina dei risultati, ovvero il numero di elementi da saltare.
* **`p.limit`** - numero che indica le dimensioni della pagina.
* **`p.guessTotal`** - consigliato: evitare di calcolare il totale completo dei risultati, il che può essere costoso. Un numero che indica il totale massimo fino al quale contare (ad esempio, 1000, un numero che fornisce agli utenti un feedback sufficiente sulle dimensioni approssimative e sui numeri esatti per risultati più piccoli). Oppure `true` per contare solo il minimo necessario `p.offset` + `p.limit`.
* **`p.excerpt`** - se impostato su `true`, includere nel risultato un estratto di testo completo.
* **`p.indexTag`** - se impostato, includerà un&#39;opzione di tag di indice nella query (vedere [Tag di indice dell&#39;opzione di query](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#query-option-index-tag)).
* **`p.facetStrategy`** - Se è impostato su `oak`, Query Builder delegherà l&#39;estrazione del facet ad Oak (vedi [Facet](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#facets)).
* **`p.hits`** - (solo per il servlet JSON) seleziona il modo in cui gli hit vengono scritti come JSON, con questi standard (estensibili tramite il servizio ResultHitWriter).
   * **`simple`** - elementi minimi come `path`, `title`, `lastmodified`, `excerpt` (se impostati).
   * **`full`** - Rendering JSON sling del nodo, con `jcr:path` che indica il percorso dell&#39;hit. Per impostazione predefinita, elenca solo le proprietà dirette del nodo, include una struttura più profonda con `p.nodedepth=N`, dove 0 significa l&#39;intera sottostruttura infinita. Aggiungi `p.acls=true` per includere le autorizzazioni JCR della sessione corrente sull&#39;elemento risultato specificato (mappature: `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`).
   * **`selective`** - solo le proprietà specificate in `p.properties`, che è un elenco di percorsi relativi separato da spazi (utilizzare `+` negli URL). Se il percorso relativo ha una profondità `>1`, queste proprietà sono rappresentate come oggetti figlio. La proprietà speciale `jcr:path` include il percorso dell&#39;hit.

### gruppo {#group}

Questo predicato consente di creare condizioni nidificate. I gruppi possono contenere gruppi nidificati. Tutto ciò che si trova in una query di Query Builder è implicitamente in un gruppo radice, che può avere anche `p.or` e `p.not` parametri.

Di seguito è riportato un esempio per confrontare una delle due proprietà con un valore:

```text
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

Concettualmente è `(1_property` O `2_property)`.

Di seguito è riportato un esempio per i gruppi nidificati:

```text
fulltext=Management
group.p.or=true
group.1_group.path=/content/wknd/ch/de
group.1_group.type=cq:Page
group.2_group.path=/content/dam/wknd
group.2_group.type=dam:Asset
```

Cerca il termine **Gestione** nelle pagine di `/content/wknd/ch/de` o nelle risorse di `/content/dam/wknd`.

Concettualmente, è `fulltext AND ( (path AND type) OR (path AND type) )`. Tali join OR richiedono indici validi per motivi di prestazioni.

#### Proprietà {#properties-6}

* **`p.or`** - se impostato su `true`, solo un predicato nel gruppo deve corrispondere. Il valore predefinito è `false`, il che significa che tutti devono corrispondere
* **`p.not`** - se impostato su `true`, nega il gruppo (impostazione predefinita: `false`)
* **`<predicate>`** - aggiunge predicati nidificati
* **`N_<predicate>`** - aggiunge più predicati nidificati contemporaneamente, come `1_property, 2_property, ...`

### orderby {#orderby}

Questo predicato consente di ordinare i risultati. Se è necessario ordinare per più proprietà, questo predicato deve essere aggiunto più volte utilizzando il prefisso numerico, ad esempio `1_orderby=first`, `2_oderby=second`.

#### Proprietà {#properties-13}

* **`orderby`** - Nome della proprietà JCR indicato da una @ iniziale, ad esempio `@jcr:lastModified` o `@jcr:content/jcr:title`, o da un altro predicato nella query, ad esempio `2_property`, su cui ordinare
* **`sort`** - direzione di ordinamento, `desc` per decrescente o `asc` per crescente (impostazione predefinita)
* **`case`** - se è impostato su `ignore`, l&#39;ordinamento non fa distinzione tra maiuscole e minuscole, ovvero `a` viene prima di `B`; se è vuoto o escluso, l&#39;ordinamento fa distinzione tra maiuscole e minuscole, ovvero `B` precede `a`

## Predicati {#predicates}

### boolproperty {#boolproperty}

Questo predicato corrisponde alle proprietà booleane JCR. Accetta solo i valori `true` e `false`. Se il valore è `false`, viene restituito se la proprietà ha il valore `false` o se non esiste affatto. Questo predicato è utile per verificare la presenza di flag booleani impostati solo se attivati.

Il parametro `operation` ereditato non ha alcun significato.

Questo predicato supporta l&#39;estrazione facet e fornisce bucket per ogni valore `true` o `false`, ma solo per le proprietà esistenti.

#### Proprietà {#properties}

* **`boolproperty`** - percorso relativo della proprietà, ad esempio `myFeatureEnabled` o `jcr:content/myFeatureEnabled`
* **`value`** - valore per cui controllare la proprietà, `true` o `false`

### contentfragment {#contentfragment}

Questo predicato limita il risultato ai frammenti di contenuto.

* Non supporta il filtro.
* Non supporta l’estrazione dei facet.

#### Proprietà {#properties-1}

* **`contentfragment`** - Può essere utilizzato con qualsiasi valore per controllare frammenti di contenuto.

### `dateComparison` {#datecomparison}

Questo predicato confronta due proprietà di data JCR tra loro. Può verificare se sono uguali, ineguali, maggiori o maggiori o uguali.

Un predicato di sola filtraggio e non può utilizzare un indice di ricerca.

#### Proprietà {#properties-2}

* **`property1`** - percorso della proprietà della prima data
* **`property2`** - percorso della seconda proprietà data
* **`operation`**
   * `=` per corrispondenza esatta (impostazione predefinita)
   * `!=` per confronto disuguaglianza
   * `>` per `property1` maggiore di `property2`
   * `>=` per `property1` maggiore o uguale a `property2`

### intervallo di date {#daterange}

Questo predicato confronta le proprietà della data JCR con un intervallo di data/ora. Utilizza ISO8601
formato per data e ora (`YYYY-MM-DDTHH:mm:ss.SSSZ`) e consente anche rappresentazioni parziali, come `YYYY-MM-DD`. In alternativa, la marca temporale può essere fornita come ora POSIX.

Puoi cercare qualsiasi cosa tra due marche temporali, qualsiasi cosa più recente o più vecchia di una determinata data e anche scegliere tra intervalli inclusivi e aperti.

Supporta l&#39;estrazione facet e fornisce i bucket `today`, `this week`, `this month`, `last 3 months`, `this year`, `last year` e `earlier than last year`.

Non supporta il filtro.

#### Proprietà {#properties-3}

* **`property`** - percorso relativo di una proprietà `DATE`, ad esempio `jcr:lastModified`
* **`lowerBound`** - data inferiore associata per verificare la proprietà, ad esempio `2014-10-01`
* **`lowerOperation`** - `>` (più recente) o `>=` (più recente), si applica a `lowerBound`. Il valore predefinito è `>`
* **`upperBound`** - limite superiore per verificare la proprietà, ad esempio `2014-10-01T12:15:00`
* **`upperOperation`** - `<` (più vecchio) o `<=` (più o meno), si applica a `upperBound`. Il valore predefinito è `<`
* **`timeZone`** - ID del fuso orario da utilizzare quando non viene fornito come stringa di data ISO-8601. Il fuso orario predefinito è quello del sistema.

### excludepaths {#excludepaths}

Questo predicato esclude i nodi dal risultato in cui il loro percorso corrisponde a un’espressione regolare.

Un predicato di sola filtraggio e non può utilizzare un indice di ricerca.

Non supporta l’estrazione dei facet.

#### Proprietà {#properties-4}

* **`excludepaths`** - espressione regolare corrispondente ai percorsi dei risultati, escludendo quelli corrispondenti dal risultato.

### full-text {#fulltext}

Cerca i termini nell&#39;indice full-text.

Non supporta il filtro.

Non supporta l’estrazione dei facet.

#### Proprietà {#properties-5}

* **`fulltext`** - termini di ricerca full-text
* **`relPath`**: il percorso relativo per la ricerca nella proprietà o nel sottonodo. Questa proprietà è facoltativa.

### hasPermission {#haspermission}

Questo predicato limita il risultato agli elementi in cui la sessione corrente dispone dei [privilegi JCR](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges) specificati.

Un predicato di sola filtraggio e non può utilizzare un indice di ricerca. Non supporta l’estrazione dei facet.

#### Proprietà {#properties-7}

* **`hasPermission`** - tutti i privilegi JCR separati da virgole che la sessione utente corrente deve avere per il nodo in questione. Ad esempio, `jcr:write`, `jcr:modifyAccessControl`

### lingua {#language}

Questo predicato trova le pagine AEM in una lingua specifica. Vengono esaminate sia la proprietà lingua della pagina che il percorso della pagina, che spesso include la lingua o le impostazioni locali in una struttura del sito principale.

Un predicato di sola filtraggio e non può utilizzare un indice di ricerca.

Supporta l’estrazione facet e fornisce bucket per ogni codice lingua univoco.

#### Proprietà {#properties-8}

* **`language`** - Codice lingua ISO, ad esempio `de`

### risorsa principale {#mainasset}

Questo predicato controlla se un nodo è una risorsa principale DAM e non una risorsa secondaria. In pratica, si tratta di ogni nodo non incluso in un nodo di risorse secondarie. Non verifica il tipo di nodo `dam:Asset`. Per utilizzare questo predicato, impostare `mainasset=true` o `mainasset=false`. Non sono presenti ulteriori proprietà.

Un predicato di sola filtraggio e non può utilizzare un indice di ricerca.

Supporta l’estrazione facet e fornisce due bucket per le risorse principali e secondarie.

#### Proprietà {#properties-9}

* **`mainasset`** - booleano, `true` per le risorse principali, `false` per le risorse secondarie

### memberOf {#memberof}

Questo predicato trova elementi che sono membri di una raccolta di risorse [sling specifica](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

Un predicato di sola filtraggio e non può utilizzare un indice di ricerca.

Non supporta l’estrazione dei facet.

#### Proprietà {#properties-10}

* **`memberOf`** - percorso della raccolta di risorse Sling

### nodename {#nodename}

Questo predicato corrisponde ai nomi dei nodi JCR.

Supporta l’estrazione facet e fornisce bucket per ogni nome di nodo univoco (nome file).

#### Proprietà {#properties-11}

* **`nodename`** - modello nome nodo che consente caratteri jolly: `*` = qualsiasi carattere o nessun carattere, `?` = qualsiasi carattere, `[abc]` = solo caratteri tra parentesi

### non scaduto {#notexpired}

Questo predicato corrisponde agli elementi controllando se una proprietà di data JCR è maggiore o uguale all’ora corrente del server. Può essere utilizzato per controllare un valore `expiresAt` e limitare i risultati solo ai valori non ancora scaduti (`notexpired=true`) o già scaduti (`notexpired=false`).

Non supporta il filtro.

Supporta l&#39;estrazione facet nello stesso modo del predicato [`daterange`](#daterange).

#### Proprietà {#properties-12}

* **`notexpired`** - valore booleano, `true` per non ancora scaduto (data nel futuro o uguale), `false` per scaduto (data nel passato) (obbligatorio)
* **`property`** - percorso relativo della proprietà `DATE` da verificare (obbligatorio)

### percorso {#path}

Questo predicato esegue ricerche all’interno di un determinato percorso.

Non supporta l’estrazione dei facet.

#### Proprietà {#properties-14}

* **`path`** - Definisce il pattern del percorso.
   * A seconda della proprietà `exact`, l&#39;intera sottostruttura corrisponde (come l&#39;aggiunta di `//*` in xpath, ma si noti che non include il percorso di base), oppure viene abbinato solo un percorso esatto, che può includere caratteri jolly (`*`).
      * Impostazione predefinita: `true`.
&lt;!—   * Se la proprietà `self` è impostata, viene eseguita la ricerca nell&#39;intera sottostruttura, incluso il nodo di base.—>
* **`exact`** - se `exact` è `true`, il percorso esatto deve corrispondere, ma può contenere caratteri jolly semplici (`*`) che corrispondono ai nomi, ma non `/`; se è `false` (impostazione predefinita) tutti i discendenti sono inclusi (facoltativo).
* **`flat`** - esegue la ricerca solo negli elementi figlio diretti (come l&#39;aggiunta di `/*` in xpath) (utilizzato solo se `exact` non è true, facoltativo).
* **`self`** - esegue la ricerca nella sottostruttura ma include il nodo di base indicato come percorso (senza caratteri jolly).
   * *Nota importante*: è stato identificato un problema con la proprietà `self` nell&#39;implementazione corrente di Query Builder e il suo utilizzo nelle query potrebbe non produrre risultati di ricerca corretti. La modifica dell&#39;implementazione corrente della proprietà `self` non è inoltre possibile perché potrebbe interrompere le applicazioni esistenti che si basano su di essa. A causa di questa funzionalità, la proprietà `self` è ora obsoleta. Si consiglia di evitare di utilizzarla.

### proprietà {#property}

Questo predicato corrisponde alle proprietà JCR e ai relativi valori.

Supporta l’estrazione dei facet e fornisce bucket per ogni valore di proprietà univoco nei risultati.

#### Proprietà {#properties-15}

* **`property`**: percorso relativo della proprietà, ad esempio `jcr:title`.
* **`value`** - valore di cui controllare la proprietà; segue il tipo di proprietà JCR per le conversioni di stringhe.
* **`N_value`** - utilizzare `1_value`, `2_value`, ... per verificare la presenza di più valori (combinati con `OR` per impostazione predefinita, con `AND` se `and=true`).
* **`and`** - impostato su `true` per la combinazione di più valori (`N_value`) con `AND`
* **`operation`**
   * `equals` per corrispondenza esatta (impostazione predefinita).
   * `unequals` per confronto disuguaglianza.
   * `like` per l&#39;utilizzo della funzione xpath `jcr:like` (facoltativo).
   * `not` senza corrispondenza (ad esempio, `not(@prop)` in xpath, il parametro value viene ignorato).
   * `exists` per verifica esistenza.
      * `true` la proprietà deve esistere.
      * `false` è uguale a `not` ed è il valore predefinito.
* **`depth`** - numero di livelli di caratteri jolly sotto i quali può esistere la proprietà o il percorso relativo (ad esempio, `property=size depth=2` controlla `node/size`, `node/*/size` e `node/*/*/size`).

### rangeproperty {#rangeproperty}

Questo predicato corrisponde a una proprietà JCR rispetto a un intervallo. Si applica alle proprietà con tipi lineari come `LONG`, `DOUBLE` e `DECIMAL`. Per `DATE`, vedere il predicato [`daterange`](#daterange) con input in formato data ottimizzato.

È possibile definire un limite inferiore, superiore o entrambi. L’operazione (ad esempio minore di, minore di o uguale a) può essere specificata anche per i limiti inferiore e superiore singolarmente.

Non supporta l’estrazione dei facet.

#### Proprietà {#properties-16}

* **`property`** - percorso relativo della proprietà
* **`lowerBound`** - limite inferiore per controllare la proprietà
* **`lowerOperation`** - `>` (impostazione predefinita) o `>=`, si applica a `lowerValue`
* **`upperBound`** - limite superiore per verificare la proprietà
* **`upperOperation`** - `<` (impostazione predefinita) o `<=`, si applica a `lowerValue`
* **`decimal`** - `true` se la proprietà selezionata è di tipo Decimal

### relativedaterange {#relativedaterange}

Questo predicato corrisponde alle proprietà `JCR DATE` rispetto a un intervallo di data/ora utilizzando scostamenti di tempo relativi all&#39;ora corrente del server. È possibile specificare `lowerBound` e `upperBound` utilizzando un valore di millisecondi o la sintassi Bugzilla `1s 2m 3h 4d 5w 6M 7y` (un secondo, due minuti, tre ore, quattro giorni, cinque settimane, sei mesi, sette anni). Aggiungi il prefisso `-` per indicare uno scostamento negativo prima dell&#39;ora corrente. Se si specifica solo `lowerBound` o `upperBound`, l&#39;altro valore predefinito è `0`, che rappresenta l&#39;ora corrente.

Ad esempio:

* `upperBound=1h` (e nessun `lowerBound`) seleziona qualcosa nell&#39;ora successiva
* `lowerBound=-1d` (e nessun `upperBound`) seleziona qualsiasi elemento nelle ultime 24 ore
* `lowerBound=-6M` e `upperBound=-3M` seleziona qualsiasi elemento negli ultimi 3-6 mesi
* `lowerBound=-1500` e `upperBound=5500` seleziona qualsiasi elemento che abbia tra i 1500 millisecondi e i 5500 millisecondi nel futuro
* `lowerBound=1d` e `upperBound=2d` seleziona qualsiasi elemento dopodomani

Non prende in considerazione anni bisestili e tutti i mesi sono 30 giorni.

Non supporta il filtro.

Supporta l&#39;estrazione facet nello stesso modo del predicato [`daterange`](#daterange).

#### Proprietà {#properties-17}

* **`upperBound`** - limite di date superiore in millisecondi o `1s 2m 3h 4d 5w 6M 7y` (un secondo, due minuti, tre ore, quattro giorni, cinque settimane, sei mesi, sette anni) rispetto al tempo server corrente. Utilizzare `-` per offset negativo
* **`lowerBound`** - limite data inferiore in millisecondi o `1s 2m 3h 4d 5w 6M 7y` (un secondo, due minuti, tre ore, quattro giorni, cinque settimane, sei mesi, sette anni) rispetto al tempo server corrente. Utilizzare `-` per offset negativo

### savedquery {#savedquery}

Questo predicato include tutti i predicati di una query di Query Builder persistente nella query corrente come predicato di sottogruppo.

Non esegue una query aggiuntiva, ma estende la query corrente.

Le query possono essere rese persistenti a livello di programmazione utilizzando `QueryBuilder#storeQuery()`. Il formato può essere una proprietà `String` su più righe o un nodo `nt:file` che contiene la query come file di testo in formato proprietà Java™.

Non supporta l’estrazione dei facet per i predicati della query salvata.

#### Proprietà {#properties-19}

* **`savedquery`** - percorso della query salvata (`String` proprietà o `nt:file` nodo)

### simile {#similar}

Questo predicato è una ricerca per similarità utilizzando JCR XPath `rep:similar()`.

Non supporta il filtro e non supporta l’estrazione dei facet.

#### Proprietà {#properties-20}

* **`similar`** - percorso assoluto del nodo per il quale trovare nodi simili
* **`local`** - Percorso relativo di un nodo discendente o `.` per il nodo corrente (facoltativo, il valore predefinito è `.`)

### tag {#tag}

Questo predicato cerca contenuti con tag assegnati a uno o più tag, specificando i percorsi dei titoli dei tag.

Supporta l’estrazione facet e fornisce bucket per ogni tag univoco, utilizzando il percorso del titolo del tag corrente.

#### Proprietà {#properties-21}

* **`tag`** - percorso titolo tag da cercare, ad esempio `properties:orientation/landscape`
* **`N_value`** - utilizzare `1_value`, `2_value`, ... per verificare la presenza di più tag (combinati con `OR` per impostazione predefinita, con `AND` se `and=true`)
* **`property`** - proprietà (o percorso relativo della proprietà) da esaminare (impostazione predefinita `cq:tags`)

### tagid {#tagid}

Questo predicato cerca contenuti con tag assegnati a uno o più tag, specificando gli ID tag.

Supporta l’estrazione facet e fornisce bucket per ogni tag univoco, utilizzando il relativo ID tag corrente.

#### Proprietà {#properties-22}

* **`tagid`** - ID tag da cercare, ad esempio `properties:orientation/landscape`
* **`N_value`** - utilizzare `1_value`, `2_value`, ... per verificare la presenza di più ID tag (combinati con `OR` per impostazione predefinita, con `AND` se `and=true`)
* **`property`** - proprietà (o percorso relativo della proprietà) da esaminare (impostazione predefinita `cq:tags`)

### tagsearch {#tagsearch}

Questo predicato consente di cercare contenuto con uno o più tag, specificando parole chiave. Cerca prima i tag contenenti queste parole chiave nei loro titoli, quindi limita il risultato solo agli elementi con queste parole chiave.

Non supporta l’estrazione dei facet.

#### Proprietà {#Properties-1}

* **`tagsearch`** - parola chiave da cercare nei titoli dei tag
* **`property`** - proprietà (o percorso relativo della proprietà) da considerare (impostazione predefinita `cq:tags`)
* **`lang`** - per cercare solo in un determinato titolo di tag localizzato (ad esempio, `de`)
* **`all`** - valore booleano per cercare l&#39;intero testo completo del tag, ovvero tutti i titoli, le descrizioni e così via (ha la precedenza su `lang`)

### tipo {#type}

Questo predicato limita i risultati a un tipo di nodo JCR specifico, sia di tipo di nodo primario che di tipo `mixin`. Trova anche i sottotipi di quel tipo di nodo. Gli indici di ricerca dell’archivio devono coprire i tipi di nodo per un’esecuzione efficiente.

Supporta l’estrazione dei facet e fornisce bucket per ogni tipo univoco nei risultati.

#### Proprietà {#Properties-2}

* **`type`** - tipo di nodo o nome `mixin` da cercare, ad esempio `cq:Page`
