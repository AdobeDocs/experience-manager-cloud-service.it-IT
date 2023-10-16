---
title: Riferimento predicato di Query Builder
description: Riferimento predicato per l’API Query Builder in AEM as a Cloud Service.
exl-id: 77118ef7-4d29-470d-9c4b-20537a408940
source-git-commit: e10c39c1d7fa05b738dd8f25662617a3a9568f83
workflow-type: tm+mt
source-wordcount: '2295'
ht-degree: 2%

---

# Riferimento predicato di Query Builder {#query-builder-predicate-reference}

## Generale {#general}

### radice {#root}

Gruppo di predicati radice. Supporta tutte le funzioni di un gruppo e consente di impostare parametri di query globali.

Il nome &quot;root&quot; non viene mai utilizzato in una query; è implicito.

#### Proprietà {#properties-18}

* **`p.offset`** - numero che indica l&#39;inizio della pagina dei risultati, ovvero il numero di elementi da saltare.
* **`p.limit`** - numero che indica le dimensioni della pagina.
* **`p.guessTotal`** - consigliato: evita di calcolare il totale completo dei risultati, che può essere costoso. Un numero che indica il totale massimo fino a cui contare (ad esempio 1000, un numero che fornisce agli utenti un feedback sufficiente sulle dimensioni approssimative e numeri esatti per risultati più piccoli). Oppure `true` per contare solo fino al minimo necessario `p.offset` + `p.limit`.
* **`p.excerpt`** - se impostato su `true`, includi un estratto di testo completo nel risultato.
* **`p.indexTag`** : se impostato, includerà un’opzione tag di indice nella query (consulta [Tag indice opzione query](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#query-option-index-tag)).
* **`p.facetStrategy`** - se impostato su `oak`, Query Builder delegherà l’estrazione del facet a Oak (vedi [Facet](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#facets)).
* **`p.hits`** : (solo per il servlet JSON) seleziona il modo in cui gli hit vengono scritti come JSON, con questi standard (estensibili tramite il servizio ResultHitWriter).
   * **`simple`** - elementi minimi come `path`, `title`, `lastmodified`, `excerpt` (se impostato).
   * **`full`** : rendering JSON sling del nodo, con `jcr:path` che indica il percorso dell’hit. Per impostazione predefinita, elenca solo le proprietà dirette del nodo, includi una struttura più profonda con `p.nodedepth=N`, dove 0 indica l&#39;intero sottoalbero infinito. Aggiungi `p.acls=true` per includere le autorizzazioni JCR della sessione corrente sull’elemento risultato specificato (mappature: `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`).
   * **`selective`** - solo le proprietà specificate in `p.properties`, che è uno spazio separato (utilizzare `+` nell’elenco degli URL dei percorsi relativi. Se il percorso relativo ha una profondità `>1`, queste proprietà sono rappresentate come oggetti figlio. Lo speciale `jcr:path` La proprietà include il percorso dell&#39;hit.

### gruppo {#group}

Questo predicato consente di creare condizioni nidificate. I gruppi possono contenere gruppi nidificati. Tutto ciò che si trova in una query di Query Builder è implicitamente in un gruppo radice, che può avere `p.or` e `p.not` parametri.

Di seguito è riportato un esempio per confrontare una delle due proprietà con un valore:

```text
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

Concettualmente, è `(1_property` OPPURE `2_property)`.

Di seguito è riportato un esempio per i gruppi nidificati:

```text
fulltext=Management
group.p.or=true
group.1_group.path=/content/wknd/ch/de
group.1_group.type=cq:Page
group.2_group.path=/content/dam/wknd
group.2_group.type=dam:Asset
```

Cerca il termine **Gestione** nelle pagine di `/content/wknd/ch/de` o in risorse in `/content/dam/wknd`.

Concettualmente, è `fulltext AND ( (path AND type) OR (path AND type) )`. Tali join OR richiedono indici validi per motivi di prestazioni.

#### Proprietà {#properties-6}

* **`p.or`** - se impostato su `true`, solo un predicato nel gruppo deve corrispondere. Impostazione predefinita `false`, il che significa che tutti devono corrispondere
* **`p.not`** - se impostato su `true`, nega il gruppo (impostazione predefinita `false`)
* **`<predicate>`** - aggiunge predicati nidificati
* **`N_<predicate>`** : aggiunge più predicati nidificati della stessa ora, come `1_property, 2_property, ...`

### orderby {#orderby}

Questo predicato consente di ordinare i risultati. Se è necessario ordinare per più proprietà, questo predicato deve essere aggiunto più volte utilizzando il prefisso numerico, ad esempio `1_orderby=first`, `2_oderby=second`.

#### Proprietà {#properties-13}

* **`orderby`** - il nome della proprietà JCR indicato da una @ iniziale, ad esempio `@jcr:lastModified` o `@jcr:content/jcr:title`, o un altro predicato nella query, ad esempio `2_property`, su cui ordinare
* **`sort`** - direzione di ordinamento, `desc` per decrescente o `asc` per crescente (impostazione predefinita)
* **`case`** - se impostato su `ignore`, non fa distinzione tra maiuscole e minuscole, ovvero `a` precede `B`; se vuoto o escluso, l’ordinamento distingue tra maiuscole e minuscole, ovvero `B` precede `a`

## Predicati {#predicates}

### boolproperty {#boolproperty}

Questo predicato corrisponde alle proprietà booleane JCR. Accetta solo i valori `true` e `false`. Se il valore è `false`, corrisponde se la proprietà ha il valore `false`o se non esiste affatto. Questo predicato è utile per verificare la presenza di flag booleani impostati solo se attivati.

L&#39;ereditata `operation` Il parametro non ha alcun significato.

Questo predicato supporta l’estrazione dei facet e fornisce bucket per ciascuno `true` o `false` ma solo per le proprietà esistenti.

#### Proprietà {#properties}

* **`boolproperty`** : percorso relativo della proprietà, ad esempio `myFeatureEnabled` o `jcr:content/myFeatureEnabled`
* **`value`** - valore per cui verificare la proprietà, `true` o `false`

### contentfragment {#contentfragment}

Questo predicato limita il risultato ai frammenti di contenuto.

* Non supporta il filtro.
* Non supporta l’estrazione dei facet.

#### Proprietà {#properties-1}

* **`contentfragment`** : può essere utilizzato con qualsiasi valore per verificare la presenza di frammenti di contenuto.

### `dateComparison` {#datecomparison}

Questo predicato confronta due proprietà di data JCR tra loro. Può verificare se sono uguali, ineguali, maggiori o maggiori o uguali.

Un predicato di sola filtraggio e non può utilizzare un indice di ricerca.

#### Proprietà {#properties-2}

* **`property1`** : percorso della proprietà della prima data
* **`property2`** - percorso della seconda proprietà data
* **`operation`**
   * `=` per corrispondenza esatta (impostazione predefinita)
   * `!=` per confronto disuguaglianza
   * `>` per `property1` maggiore di `property2`
   * `>=` per `property1` maggiore o uguale a `property2`

### intervallo di date {#daterange}

Questo predicato confronta le proprietà della data JCR con un intervallo di data/ora. Utilizza il formato ISO8601 per data e ora (`YYYY-MM-DDTHH:mm:ss.SSSZ`) e consente anche rappresentazioni parziali, come `YYYY-MM-DD`. In alternativa, la marca temporale può essere fornita come ora POSIX.

Puoi cercare qualsiasi cosa tra due marche temporali, qualsiasi cosa più recente o più vecchia di una determinata data e anche scegliere tra intervalli inclusivi e aperti.

Supporta l’estrazione facet e fornisce bucket `today`, `this week`, `this month`, `last 3 months`, `this year`, `last year`, e `earlier than last year`.

Non supporta il filtro.

#### Proprietà {#properties-3}

* **`property`** - percorso relativo di un `DATE` proprietà, ad esempio `jcr:lastModified`
* **`lowerBound`** : data inferiore associata per verificare la proprietà, ad esempio `2014-10-01`
* **`lowerOperation`** - `>` (più recente) o `>=` (versione successiva o uguale a), si applica al `lowerBound`. Il valore predefinito è `>`
* **`upperBound`** : limite superiore per verificare la proprietà, ad esempio `2014-10-01T12:15:00`
* **`upperOperation`** - `<` (più vecchio) o `<=` (a partire da), si applica al `upperBound`. Il valore predefinito è `<`
* **`timeZone`** - ID del fuso orario da utilizzare quando non viene fornito come stringa di data ISO-8601. Il fuso orario predefinito è quello del sistema.

### excludepaths {#excludepaths}

Questo predicato esclude i nodi dal risultato in cui il loro percorso corrisponde a un’espressione regolare.

Un predicato di sola filtraggio e non può utilizzare un indice di ricerca.

Non supporta l’estrazione dei facet.

#### Proprietà {#properties-4}

* **`excludepaths`** : espressione regolare confrontata con i percorsi dei risultati, escludendo quelli corrispondenti dal risultato.

### full-text {#fulltext}

Cerca i termini nell&#39;indice full-text.

Non supporta il filtro.

Non supporta l’estrazione dei facet.

#### Proprietà {#properties-5}

* **`fulltext`** - i termini di ricerca full-text
* **`relPath`** : percorso relativo della ricerca nella proprietà o nel sottonodo. Questa proprietà è facoltativa.

### hasPermission {#haspermission}

Questo predicato limita il risultato agli elementi in cui la sessione corrente ha il [Privilegi JCR.](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

Un predicato di sola filtraggio e non può utilizzare un indice di ricerca. Non supporta l’estrazione dei facet.

#### Proprietà {#properties-7}

* **`hasPermission`** : tutti i privilegi JCR separati da virgole che la sessione utente corrente deve avere per il nodo in questione. Ad esempio, `jcr:write`, `jcr:modifyAccessControl`

### lingua {#language}

Questo predicato trova le pagine AEM in una lingua specifica. Vengono esaminate sia la proprietà lingua della pagina che il percorso della pagina, che spesso include la lingua o le impostazioni locali in una struttura del sito principale.

Un predicato di sola filtraggio e non può utilizzare un indice di ricerca.

Supporta l’estrazione facet e fornisce bucket per ogni codice lingua univoco.

#### Proprietà {#properties-8}

* **`language`** - codice della lingua ISO, ad esempio `de`

### risorsa principale {#mainasset}

Questo predicato controlla se un nodo è una risorsa principale DAM e non una risorsa secondaria. In pratica, si tratta di ogni nodo non incluso in un nodo di risorse secondarie. Non controlla la `dam:Asset` tipo di nodo. Per utilizzare questo predicato, imposta `mainasset=true` o `mainasset=false`. Non sono presenti ulteriori proprietà.

Un predicato di sola filtraggio e non può utilizzare un indice di ricerca.

Supporta l’estrazione facet e fornisce due bucket per le risorse principali e secondarie.

#### Proprietà {#properties-9}

* **`mainasset`** - booleano, `true` per le attività principali, `false` per le risorse secondarie

### memberOf {#memberof}

Questo predicato trova elementi che sono membri di un [raccolta di risorse sling](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

Un predicato di sola filtraggio e non può utilizzare un indice di ricerca.

Non supporta l’estrazione dei facet.

#### Proprietà {#properties-10}

* **`memberOf`** - percorso della raccolta di risorse Sling

### nodename {#nodename}

Questo predicato corrisponde ai nomi dei nodi JCR.

Supporta l’estrazione facet e fornisce bucket per ogni nome di nodo univoco (nome file).

#### Proprietà {#properties-11}

* **`nodename`** - pattern del nome del nodo che consente l’utilizzo di caratteri jolly: `*` = qualsiasi carattere o nessun carattere, `?` = qualsiasi carattere, `[abc]` = solo caratteri tra parentesi

### non scaduto {#notexpired}

Questo predicato corrisponde agli elementi controllando se una proprietà di data JCR è maggiore o uguale all’ora corrente del server. Può essere utilizzato per controllare un `expiresAt` e limita i risultati solo ai valori non ancora scaduti (`notexpired=true`) o che sono già scaduti (`notexpired=false`).

Non supporta il filtro.

Supporta l’estrazione delle sfaccettature allo stesso modo della [`daterange`](#daterange) predicato.

#### Proprietà {#properties-12}

* **`notexpired`** - booleano, `true` per non ancora scaduto (data futura o uguale), `false` per scaduto (data nel passato) (obbligatorio)
* **`property`** : percorso relativo del `DATE` proprietà da verificare (obbligatoria)

### percorso {#path}

Questo predicato esegue ricerche all’interno di un determinato percorso.

Non supporta l’estrazione dei facet.

#### Proprietà {#properties-14}

* **`path`** - Definisce il pattern del percorso.
   * A seconda della `exact` , l&#39;intera sottostruttura corrisponde (ad esempio, aggiungendo `//*` in xpath, ma si noti che non include il percorso di base), oppure viene abbinato solo un percorso esatto, che può includere caratteri jolly (`*`).
      * Impostazione predefinita `true`.
&lt;!— * Se il `self`viene eseguita la ricerca nell&#39;intera sottostruttura, incluso il nodo di base.—>
* **`exact`** - se `exact` è `true`, il percorso esatto deve corrispondere, ma può contenere caratteri jolly semplici (`*`), che corrispondono ai nomi, ma non `/`; se è `false` (impostazione predefinita) sono inclusi tutti i discendenti (facoltativo).
* **`flat`** - cerca solo gli elementi secondari diretti (ad esempio, aggiungendo `/*` in xpath) (utilizzato solo se `exact` non è true, facoltativo).
* **`self`** : esegue la ricerca nella sottostruttura ma include il nodo di base indicato come percorso (nessun carattere jolly).
   * *Nota importante*: è stato identificato un problema con `self` proprietà nell’implementazione corrente di query builder e il suo utilizzo nelle query potrebbe non produrre risultati di ricerca corretti. Modifica dell’implementazione corrente di `self` non è fattibile perché potrebbe interrompere le applicazioni esistenti che si basano su di essa. Grazie a questa funzionalità, `self` La proprietà è ora obsoleta. Si consiglia di evitare di utilizzarla.

### proprietà {#property}

Questo predicato corrisponde alle proprietà JCR e ai relativi valori.

Supporta l’estrazione dei facet e fornisce bucket per ogni valore di proprietà univoco nei risultati.

#### Proprietà {#properties-15}

* **`property`** : percorso relativo della proprietà, ad esempio `jcr:title`.
* **`value`** : valore di cui controllare la proprietà; segue il tipo di proprietà JCR per le conversioni di stringhe.
* **`N_value`** - utilizzare `1_value`, `2_value`, ... per verificare la presenza di più valori (combinati con `OR` per impostazione predefinita, con `AND` se `and=true`).
* **`and`** - impostato su `true` per combinare più valori (`N_value`) con `AND`
* **`operation`**
   * `equals` per corrispondenza esatta (impostazione predefinita).
   * `unequals` per il confronto delle disuguaglianze.
   * `like` per utilizzare `jcr:like` funzione xpath (opzionale).
   * `not` in caso di mancata corrispondenza (ad esempio, `not(@prop)` in xpath, il parametro value viene ignorato).
   * `exists` per verifica esistenza.
      * `true` la proprietà deve esistere.
      * `false` è uguale a `not` e è l’impostazione predefinita.
* **`depth`** - numero di livelli di caratteri jolly sotto i quali può esistere la proprietà o il percorso relativo (ad esempio, `property=size depth=2` assegni `node/size`, `node/*/size`, e `node/*/*/size`).

### rangeproperty {#rangeproperty}

Questo predicato corrisponde a una proprietà JCR rispetto a un intervallo. Si applica alle proprietà con tipi lineari come `LONG`, `DOUBLE`, e `DECIMAL`. Per `DATE`, vedere [`daterange`](#daterange) predicato con input in formato data ottimizzato.

È possibile definire un limite inferiore, superiore o entrambi. L’operazione (ad esempio minore di, minore di o uguale a) può essere specificata anche per i limiti inferiore e superiore singolarmente.

Non supporta l’estrazione dei facet.

#### Proprietà {#properties-16}

* **`property`** : percorso relativo della proprietà
* **`lowerBound`** : limite inferiore per verificare la proprietà
* **`lowerOperation`** - `>` (impostazione predefinita) oppure `>=`, si applica al `lowerValue`
* **`upperBound`** : limite superiore per verificare la proprietà
* **`upperOperation`** - `<` (impostazione predefinita) oppure `<=`, si applica al `lowerValue`
* **`decimal`** - `true` se la proprietà selezionata è di tipo Decimal

### relativedaterange {#relativedaterange}

Questo predicato corrisponde a `JCR DATE` proprietà rispetto a un intervallo di data/ora utilizzando gli offset temporali relativi all&#39;ora corrente del server. È possibile specificare `lowerBound` e `upperBound` utilizzando un valore in millisecondi o la sintassi Bugzilla `1s 2m 3h 4d 5w 6M 7y` (un secondo, due minuti, tre ore, quattro giorni, cinque settimane, sei mesi, sette anni) Prefisso con `-` per indicare un offset negativo prima dell&#39;ora corrente. Se si specifica solo `lowerBound` o `upperBound`, l’altro utilizza per impostazione predefinita `0`, che rappresenta l&#39;ora corrente.

Ad esempio:

* `upperBound=1h` (e no `lowerBound`a) seleziona qualsiasi elemento nell&#39;ora successiva
* `lowerBound=-1d` (e no `upperBound`a) seleziona qualsiasi elemento nelle ultime 24 ore
* `lowerBound=-6M` e `upperBound=-3M` seleziona qualsiasi elemento negli ultimi 3-6 mesi
* `lowerBound=-1500` e `upperBound=5500` seleziona un valore compreso tra 1500 e 5500 millisecondi in futuro
* `lowerBound=1d` e `upperBound=2d` seleziona qualsiasi elemento dopodomani

Non prende in considerazione anni bisestili e tutti i mesi sono 30 giorni.

Non supporta il filtro.

Supporta l’estrazione delle sfaccettature allo stesso modo della [`daterange`](#daterange) predicato.

#### Proprietà {#properties-17}

* **`upperBound`** - limite superiore di date in millisecondi o `1s 2m 3h 4d 5w 6M 7y` (un secondo, due minuti, tre ore, quattro giorni, cinque settimane, sei mesi, sette anni) rispetto al tempo del server corrente, utilizzare `-` per scostamento negativo
* **`lowerBound`** - limite di data inferiore in millisecondi o `1s 2m 3h 4d 5w 6M 7y` (un secondo, due minuti, tre ore, quattro giorni, cinque settimane, sei mesi, sette anni) rispetto al tempo del server corrente, utilizzare `-` per scostamento negativo

### savedquery {#savedquery}

Questo predicato include tutti i predicati di una query di Query Builder persistente nella query corrente come predicato di sottogruppo.

Non esegue una query aggiuntiva, ma estende la query corrente.

Le query possono essere rese persistenti a livello di programmazione utilizzando `QueryBuilder#storeQuery()`. Il formato può essere multiriga `String` proprietà o un `nt:file` nodo che contiene la query come file di testo in formato Java™ properties.

Non supporta l’estrazione dei facet per i predicati della query salvata.

#### Proprietà {#properties-19}

* **`savedquery`** : percorso della query salvata (`String` proprietà o `nt:file` node)

### simile {#similar}

Questo predicato è una ricerca per somiglianza utilizzando JCR XPath `rep:similar()`.

Non supporta il filtro e non supporta l’estrazione dei facet.

#### Proprietà {#properties-20}

* **`similar`** : percorso assoluto del nodo per il quale trovare nodi simili
* **`local`** - un percorso relativo a un nodo discendente oppure `.` per il nodo corrente (facoltativo, il valore predefinito è `.`)

### tag {#tag}

Questo predicato cerca contenuti con tag assegnati a uno o più tag, specificando i percorsi dei titoli dei tag.

Supporta l’estrazione facet e fornisce bucket per ogni tag univoco, utilizzando il percorso del titolo del tag corrente.

#### Proprietà {#properties-21}

* **`tag`** : percorso del titolo del tag da cercare, ad esempio `properties:orientation/landscape`
* **`N_value`** - utilizzare `1_value`, `2_value`, ... per verificare la presenza di più tag (combinati con `OR` per impostazione predefinita, con `AND` se `and=true`)
* **`property`** : proprietà (o percorso relativo della proprietà) da esaminare (impostazione predefinita `cq:tags`)

### tagid {#tagid}

Questo predicato cerca contenuti con tag assegnati a uno o più tag, specificando gli ID tag.

Supporta l’estrazione facet e fornisce bucket per ogni tag univoco, utilizzando il relativo ID tag corrente.

#### Proprietà {#properties-22}

* **`tagid`** : ID tag da cercare, ad esempio `properties:orientation/landscape`
* **`N_value`** - utilizzare `1_value`, `2_value`, ... per verificare la presenza di più ID tag (combinati con `OR` per impostazione predefinita, con `AND` se `and=true`)
* **`property`** : proprietà (o percorso relativo della proprietà) da esaminare (impostazione predefinita `cq:tags`)

### tagsearch {#tagsearch}

Questo predicato consente di cercare contenuto con uno o più tag, specificando parole chiave. Cerca prima i tag contenenti queste parole chiave nei loro titoli, quindi limita il risultato solo agli elementi con queste parole chiave.

Non supporta l’estrazione dei facet.

#### Proprietà {#Properties-1}

* **`tagsearch`** - parola chiave da cercare nei titoli dei tag
* **`property`** : proprietà (o percorso relativo della proprietà) da considerare (impostazione predefinita `cq:tags`)
* **`lang`** : per eseguire ricerche solo in un determinato titolo di tag localizzato (ad esempio, `de`)
* **`all`** : valore booleano per cercare l’intero testo completo del tag, ovvero tutti i titoli, le descrizioni e così via (ha la precedenza su `lang`)

### tipo {#type}

Questo predicato limita i risultati a un tipo di nodo JCR specifico, entrambi tipi di nodo primari o `mixin` tipi. Trova anche i sottotipi di quel tipo di nodo. Gli indici di ricerca dell’archivio devono coprire i tipi di nodo per un’esecuzione efficiente.

Supporta l’estrazione dei facet e fornisce bucket per ogni tipo univoco nei risultati.

#### Proprietà {#Properties-2}

* **`type`** - tipo di nodo o `mixin` nome da cercare, ad esempio `cq:Page`
