---
title: Riferimento predicato Query Builder
description: Riferimento predicato per l'API Query Builder.
translation-type: tm+mt
source-git-commit: 90b635cb31af910e08bdee7925cec0c7beb05318
workflow-type: tm+mt
source-wordcount: '2221'
ht-degree: 1%

---


# Riferimento predicato Query Builder {#query-builder-predicate-reference}

## Generale {#general}

### root {#root}

Questo è il gruppo di predicati radice. Supporta tutte le funzioni di un gruppo e consente di impostare parametri di query globali.

Il nome &quot;root&quot; non viene mai utilizzato in una query, è implicito.

#### Proprietà {#properties-18}

* **`p.offset`** - numero che indica l&#39;inizio della pagina dei risultati, ovvero quanti elementi saltare
* **`p.limit`** - numero che indica le dimensioni della pagina
* **`p.guessTotal`** - consigliato: evitare di calcolare l&#39;intero risultato complessivo che può essere costoso; un numero che indica il totale massimo da conteggiare fino a (ad esempio 1000, un numero che fornisce agli utenti un feedback sufficiente sulla dimensione approssimativa e sui numeri esatti per risultati più piccoli) o  `true` da conteggiare solo fino al minimo necessario  `p.offset` +  `p.limit`
* **`p.excerpt`** - se impostato su  `true`, includete un estratto di testo completo nel risultato
* **`p.hits`** - (solo per il servlet JSON) selezionate il modo in cui gli hit vengono scritti come JSON, con i seguenti standard (estensibili tramite il servizio ResultHitWriter):
   * **`simple`** - elementi minimi come  `path`,  `title`,  `lastmodified`,  `excerpt` (se impostati)
   * **`full`** - rendering JSON sling del nodo, con  `jcr:path` indicazione del percorso dell&#39;hit: per impostazione predefinita elenca solo le proprietà dirette del nodo, include una struttura ad albero più profonda con  `p.nodedepth=N`, con 0 che significa l&#39;intera sottostruttura infinita; aggiungere  `p.acls=true` per includere le autorizzazioni JCR della sessione corrente sull&#39;elemento risultato dato (mappature:  `create` =  `add_node`,  `modify` =  `set_property`,  `delete` =  `remove`)
   * **`selective`** - solo le proprietà specificate in  `p.properties`, che è un elenco di percorsi relativi separati da spazi (da usare  `+` in URL); se il percorso relativo ha una profondità,  `>1` questi saranno rappresentati come oggetti secondari; la  `jcr:path` proprietà speciale include il percorso dell&#39;hit

### gruppo {#group}

Questo predicato consente la creazione di condizioni nidificate. I gruppi possono contenere gruppi nidificati. Tutto in una query Query Builder si trova implicitamente in un gruppo radice, che può avere anche `p.or` e `p.not` parametri.

Di seguito è riportato un esempio di corrispondenza tra una delle due proprietà e un valore:

```text
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

Questo è concettualmente `(1_property` OR `2_property)`.

Di seguito è riportato un esempio per i gruppi nidificati:

```text
fulltext=Management
group.p.or=true
group.1_group.path=/content/wknd/ch/de
group.1_group.type=cq:Page
group.2_group.path=/content/dam/wknd
group.2_group.type=dam:Asset
```

Viene ricercato il termine **Gestione** all&#39;interno delle pagine in `/content/wknd/ch/de` o nelle risorse in `/content/dam/wknd`.

Questo è concettualmente `fulltext AND ( (path AND type) OR (path AND type) )`. Tenere presente che tali join OR necessitano di buoni indici per motivi di prestazioni.

#### Proprietà {#properties-6}

* **`p.or`** - se impostato su  `true`, solo un predicato nel gruppo deve corrispondere. Questo valore predefinito è `false`, ovvero tutti devono corrispondere
* **`p.not`** - se impostato su  `true`, nega il gruppo (impostazione predefinita:  `false`)
* **`<predicate>`** - aggiunge i predicati nidificati
* **`N_<predicate>`** - aggiunge più predicati nidificati contemporaneamente, come  `1_property, 2_property, ...`

### orderby {#orderby}

Questo predicato consente di ordinare i risultati. Se l&#39;ordine è richiesto da più proprietà, questo predicato deve essere aggiunto più volte utilizzando il prefisso del numero, ad esempio `1_orderby=first`, `2_oderby=second`.

#### Proprietà {#properties-13}

* **`orderby`** - nome della proprietà JCR indicato da una @ iniziale, ad esempio  `@jcr:lastModified` o  `@jcr:content/jcr:title`, oppure da un altro predicato nella query, ad esempio  `2_property`, su cui ordinare
* **`sort`** - ordinare la direzione,  `desc` per la discesa o  `asc` per la crescente (impostazione predefinita)
* **`case`** - se impostato su  `ignore` renderà la selezione senza distinzione tra maiuscole e minuscole, il significato  `a` viene prima  `B`; se vuoto o lasciato fuori, l&#39;ordinamento distingue tra maiuscole e minuscole, il significato  `B` viene prima  `a`

## Predicati {#predicates}

### boolproperty {#boolproperty}

Questo predicato corrisponde alle proprietà booleane JCR. Accetta solo i valori `true` e `false`. In caso di `false`, la corrispondenza sarà valida se la proprietà ha il valore `false` o se non esiste affatto. Questa funzione può essere utile per verificare la presenza di flag booleani impostati solo se abilitati.

Il parametro `operation` ereditato non ha alcun significato.

Questo predicato supporta l&#39;estrazione dei facet e fornisce bucket per ciascun valore `true` o `false`, ma solo per le proprietà esistenti.

#### Proprietà {#properties}

* **`boolproperty`** - percorso relativo alla proprietà, ad esempio  `myFeatureEnabled` o  `jcr:content/myFeatureEnabled`
* **`value`** - valore per la verifica della proprietà,  `true` oppure  `false`

### content fragment {#contentfragment}

Questo predicato limita il risultato ai frammenti di contenuto.

* Non supporta i filtri.
* Non supporta l&#39;estrazione dei facet.

#### Proprietà {#properties-1}

* **`contentfragment`** - Può essere utilizzato con qualsiasi valore per verificare la presenza di frammenti di contenuto.

### `dateComparison` {#datecomparison}

Questo predicato mette a confronto due proprietà data JCR. Può verificare se sono uguali, diversi, maggiori o maggiori di o uguali.

Si tratta di un predicato di solo filtraggio e non può sfruttare un indice di ricerca.

#### Proprietà {#properties-2}

* **`property1`** - percorso della proprietà data first
* **`property2`** - percorso alla proprietà seconda data
* **`operation`**
   * `=` per corrispondenza esatta (predefinito)
   * `!=` per il confronto tra disuguaglianze
   * `>` per  `property1` maggiore di  `property2`
   * `>=` per  `property1` maggiore o uguale a  `property2`

### daterange {#daterange}

Questo predicato corrisponde alle proprietà data JCR rispetto a un intervallo data/ora. Viene utilizzato lo standard ISO8601
formato per date e ore (`YYYY-MM-DDTHH:mm:ss.SSSZ`) e consente anche rappresentazioni parziali, come `YYYY-MM-DD`. In alternativa, la marca temporale può essere fornita come ora POSIX.

Potete cercare qualsiasi elemento tra due marche temporali, qualsiasi data più recente o precedente, e scegliere anche tra intervalli inclusivi e aperti.

Supporta l&#39;estrazione dei facet e fornisce secchi `today`, `this week`, `this month`, `last 3 months`, `this year`, `last year` e `earlier than last year`.

Non supporta i filtri.

#### Proprietà {#properties-3}

* **`property`** - percorso relativo a una  `DATE` proprietà, ad esempio  `jcr:lastModified`
* **`lowerBound`** - data inferiore associata a check property per, ad esempio  `2014-10-01`
* **`lowerOperation`** -  `>` (più recente) o  `>=` (più recente o più recente), si applica al  `lowerBound`. Il valore predefinito è `>`
* **`upperBound`** - limite superiore per controllare la proprietà, ad esempio  `2014-10-01T12:15:00`
* **`upperOperation`** -  `<` (precedente) o  `<=` (precedente o precedente), si applica al  `upperBound`. Il valore predefinito è `<`
* **`timeZone`** - ID del fuso orario da utilizzare quando non viene specificato come stringa data ISO-8601. L&#39;impostazione predefinita è il fuso orario predefinito del sistema.

### esclude percorsi {#excludepaths}

Questo predicato esclude i nodi dal risultato in cui il percorso corrisponde a un&#39;espressione regolare.

Si tratta di un predicato di solo filtraggio e non può sfruttare un indice di ricerca.

Non supporta l&#39;estrazione dei facet.

#### Proprietà {#properties-4}

* **`excludepaths`** - espressione regolare confrontata con i percorsi dei risultati, esclusi quelli corrispondenti dal risultato.

### fulltext {#fulltext}

Questo predicato cerca i termini nell&#39;indice full-text.

Non supporta i filtri.

Non supporta l&#39;estrazione dei facet.

#### Proprietà {#properties-5}

* **`fulltext`** - i termini di ricerca full-text
* **`relPath`** - il percorso relativo da cercare nella proprietà o nel nodo secondario. Questa proprietà è facoltativa.

### hasPermission {#haspermission}

Questo predicato limita il risultato agli elementi in cui la sessione corrente dispone dei privilegi JCR [specificati.](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

Si tratta di un predicato di solo filtraggio e non può sfruttare un indice di ricerca. Non supporta l&#39;estrazione dei facet.

#### Proprietà {#properties-7}

* **`hasPermission`** - i privilegi JCR separati da virgola che la sessione utente corrente deve avere per il nodo in questione; ad esempio  `jcr:write`,  `jcr:modifyAccessControl`

### language {#language}

Questo predicato trova AEM pagine in una lingua specifica. Questo esamina sia la proprietà della lingua della pagina che il percorso della pagina, che spesso include la lingua o le impostazioni internazionali in una struttura del sito di livello principale.

Si tratta di un predicato di solo filtraggio e non può sfruttare un indice di ricerca.

Supporta l&#39;estrazione dei facet e fornisce bucket per ogni codice lingua univoco.

#### Proprietà {#properties-8}

* **`language`** - Codice della lingua ISO, ad esempio  `de`

### main asset {#mainasset}

Questo predicato verifica se un nodo è una risorsa principale DAM e non una risorsa secondaria. In pratica, si tratta di ogni nodo che non si trova all&#39;interno di un nodo di risorse secondarie. Tenere presente che questo non verifica il tipo di nodo `dam:Asset`. Per utilizzare questo predicato, è sufficiente impostare `mainasset=true` o `mainasset=false`. Non ci sono ulteriori proprietà.

Si tratta di un predicato di solo filtraggio e non può sfruttare un indice di ricerca.

Supporta l’estrazione dei facet e fornisce due bucket per le risorse principali e secondarie.

#### Proprietà {#properties-9}

* **`mainasset`** - booleano,  `true` per le risorse principali,  `false` per le risorse secondarie

### MemberOf {#memberof}

Questo predicato trova elementi che appartengono a una raccolta di risorse sling [specifica](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

Si tratta di un predicato di solo filtraggio e non può sfruttare un indice di ricerca.

Non supporta l&#39;estrazione dei facet.

#### Proprietà {#properties-10}

* **`memberOf`** - percorso della raccolta di risorse Sling

### nodename {#nodename}

Questo predicato corrisponde ai nomi dei nodi JCR.

Supporta l&#39;estrazione dei facet e fornisce bucket per ogni nome di nodo univoco (nome file).

#### Proprietà {#properties-11}

* **`nodename`** - pattern di nome nodo che consente i caratteri jolly:  `*` = qualsiasi o nessun carattere,  `?` = qualsiasi carattere,  `[abc]` = solo caratteri tra parentesi

### not expired {#notexpired}

Questo predicato corrisponde agli elementi controllando se una proprietà data JCR è maggiore o uguale all&#39;ora server corrente. Questo può essere utilizzato per verificare un valore `expiresAt` e limitare i risultati solo a quelli che non sono ancora scaduti (`notexpired=true`) o che sono già scaduti (`notexpired=false`).

Non supporta i filtri.

Supporta l&#39;estrazione dei facet nello stesso modo del predicato [`daterange`](#daterange).

#### Proprietà {#properties-12}

* **`notexpired`** - booleano,  `true` per non ancora scaduto (data in futuro o uguale),  `false` per scaduto (data in passato) (obbligatorio)
* **`property`** - percorso relativo alla  `DATE` proprietà da verificare (obbligatorio)

### path {#path}

Questo predicate esegue le ricerche all&#39;interno di un determinato percorso.

Non supporta l&#39;estrazione dei facet.

#### Proprietà {#properties-14}

* **`path`** - Definisce il pattern del percorso.
   * A seconda della proprietà `exact`, l&#39;intera sottostruttura corrisponderà (come aggiungere `//*` in xpath, ma si noti che non include il percorso di base) o solo una corrispondenza esatta del percorso, che può includere caratteri jolly (`*`).
      * Impostazione predefinita `true`
   * Se la proprietà `self`è impostata, verrà eseguita la ricerca nell&#39;intera sottostruttura, incluso il nodo di base.
* **`exact`** - se  `exact` è  `true`, il percorso esatto deve corrispondere, ma può contenere caratteri jolly semplici (`*`), che corrispondono ai nomi, ma non  `/`; se è  `false` (predefinito), tutti i discendenti sono inclusi (facoltativo)
* **`flat`** - esegue la ricerca solo negli elementi figlio diretti (come l&#39;aggiunta  `/*` in xpath) (utilizzato solo se non  `exact` è vero, facoltativo)
* **`self`** - esegue la ricerca nella sottostruttura, ma include il nodo di base specificato come percorso (nessun carattere jolly)

### proprietà {#property}

Questo predicato corrisponde alle proprietà JCR e ai relativi valori.

Supporta l&#39;estrazione dei facet e fornisce bucket per ogni valore di proprietà univoco nei risultati.

#### Proprietà {#properties-15}

* **`property`** - percorso relativo alla proprietà, ad esempio  `jcr:title`
* **`value`** - valore per controllare la proprietà; segue il tipo di proprietà JCR in conversioni stringa
* **`N_value`** - uso  `1_value`,  `2_value`, ... per controllare più valori (combinati con  `OR` per impostazione predefinita, con  `AND` if  `and=true`)
* **`and`** - impostato  `true` per combinare più valori (`N_value`con)  `AND`
* **`operation`**
   * `equals` per corrispondenza esatta (predefinito)
   * `unequals` per il confronto tra disuguaglianze
   * `like` per l&#39;utilizzo della funzione  `jcr:like` xpath (facoltativo)
   * `not` per nessuna corrispondenza (ad es.  `not(@prop)` in xpath, il valore param verrà ignorato)
   * `exists` verifica dell&#39;esistenza
      * `true` la proprietà deve esistere
      * `false` è uguale a  `not` ed è il valore predefinito
* **`depth`** - numero di livelli di caratteri jolly al di sotto dei quali può esistere il percorso proprietà/relativo (ad esempio,  `property=size depth=2` controllerà  `node/size`e  `node/*/size` e  `node/*/*/size`)

### rangeproperty {#rangeproperty}

Questo predicato corrisponde a una proprietà JCR rispetto a un intervallo. Ciò si applica alle proprietà con tipi lineari quali `LONG`, `DOUBLE` e `DECIMAL`. Per `DATE`, vedere il predicato [`daterange`](#daterange) con formato data ottimizzato.

È possibile definire un limite inferiore, un limite superiore o entrambi. L&#39;operazione (ad es. minore o minore di o uguale a) può essere specificata anche per i singoli rilegati inferiori e superiori.

Non supporta l&#39;estrazione dei facet.

#### Proprietà {#properties-16}

* **`property`** - percorso relativo alla proprietà
* **`lowerBound`** - associato inferiore alla proprietà check
* **`lowerOperation`** -  `>` (predefinito) o  `>=`, si applica al  `lowerValue`
* **`upperBound`** - associato superiore alla proprietà check
* **`upperOperation`** -  `<` (predefinito) o  `<=`, si applica al  `lowerValue`
* **`decimal`** -  `true` se la proprietà selezionata è di tipo Decimale

### relativedaterange {#relativedaterange}

Questo predicato corrisponde alle proprietà `JCR DATE` rispetto a un intervallo di data/ora utilizzando gli offset relativi all&#39;ora del server corrente. È possibile specificare `lowerBound` e `upperBound` utilizzando un valore in millisecondi o la sintassi di Bugzilla `1s 2m 3h 4d 5w 6M 7y` (un secondo, due minuti, tre ore, quattro giorni, cinque settimane, sei mesi, sette anni). Prefisso con `-` per indicare un offset negativo prima del tempo corrente. Se si specifica solo `lowerBound` o `upperBound`, per impostazione predefinita l&#39;altro valore è `0`, che rappresenta l&#39;ora corrente.

Esempio:

* `upperBound=1h` (e no  `lowerBound`) seleziona qualsiasi elemento nell&#39;ora successiva
* `lowerBound=-1d` (e no  `upperBound`) seleziona qualsiasi elemento nelle ultime 24 ore
* `lowerBound=-6M` e  `upperBound=-3M` seleziona qualsiasi cosa negli ultimi 3-6 mesi
* `lowerBound=-1500` e  `upperBound=5500` seleziona qualsiasi cosa compresa tra 1500 millisecondi e 5500 millisecondi nel futuro
* `lowerBound=1d` e  `upperBound=2d` seleziona qualsiasi cosa dopodomani

Si noti che non prende in considerazione anni bisestili e che tutti i mesi sono 30 giorni.

Non supporta i filtri.

Supporta l&#39;estrazione dei facet nello stesso modo del predicato [`daterange`](#daterange).

#### Proprietà {#properties-17}

* **`upperBound`** - data superiore in millisecondi o  `1s 2m 3h 4d 5w 6M 7y` (un secondo, due minuti, tre ore, quattro giorni, cinque settimane, sei mesi, sette anni) rispetto all&#39;ora del server corrente, utilizzo  `-` per offset negativo
* **`lowerBound`** - data più bassa in millisecondi o  `1s 2m 3h 4d 5w 6M 7y` (un secondo, due minuti, tre ore, quattro giorni, cinque settimane, sei mesi, sette anni) rispetto all&#39;ora del server corrente, utilizzo  `-` per offset negativo

### savedquery {#savedquery}

Questo predicato include tutti i predicati di una query Query Builder persistente nella query corrente come un predicato di sottogruppo.

Si noti che questo non eseguirà una query supplementare ma estenderà la query corrente.

Le query possono essere persistenti a livello di programmazione utilizzando `QueryBuilder#storeQuery()`. Il formato può essere una proprietà multi-riga `String` o un nodo `nt:file` che contiene la query come file di testo in formato delle proprietà Java.

Non supporta l&#39;estrazione facet per i predicati della query salvata.

#### Proprietà {#properties-19}

* **`savedquery`** - percorso della query salvata (`String` proprietà o  `nt:file` nodo)

### simili {#similar}

Questo predicato è una ricerca per similarità utilizzando l&#39;espressione `rep:similar()` dell&#39;XPath JCR.

Non supporta il filtraggio e non supporta l&#39;estrazione dei facet.

#### Proprietà {#properties-20}

* **`similar`** - percorso assoluto del nodo per il quale trovare nodi simili
* **`local`** - un percorso relativo a un nodo discendente o  `.` per il nodo corrente (facoltativo, il valore predefinito è  `.`)

### tag {#tag}

Questo predicato cerca il contenuto con uno o più tag, specificando i percorsi del titolo dei tag.

Supporta l&#39;estrazione dei facet e fornisce secchi per ogni tag univoco, utilizzando il percorso del titolo del tag corrente.

#### Proprietà {#properties-21}

* **`tag`** - percorso del titolo del tag da cercare, ad esempio  `properties:orientation/landscape`
* **`N_value`** - uso  `1_value`,  `2_value`, ... per controllare più tag (combinati con  `OR` per impostazione predefinita, con  `AND` if  `and=true`)
* **`property`** - proprietà (o percorso relativo alla proprietà) da esaminare (impostazione predefinita  `cq:tags`)

### tagid {#tagid}

Questo predicato cerca il contenuto con uno o più tag, specificando ID di tag.

Supporta l&#39;estrazione dei facet e fornisce bucket per ogni tag univoco, utilizzando l&#39;ID del tag corrente.

#### Proprietà {#properties-22}

* **`tagid`** - ID tag da cercare, ad esempio  `properties:orientation/landscape`
* **`N_value`** - uso  `1_value`,  `2_value`, ... per verificare la presenza di ID tag multipli (combinati con  `OR` per impostazione predefinita, con  `AND` if  `and=true`)
* **`property`** - proprietà (o percorso relativo alla proprietà) da esaminare (impostazione predefinita  `cq:tags`)

### tagsearch {#tagsearch}

Questo predicato cerca il contenuto con uno o più tag, specificando le parole chiave. In questo modo, i tag che contengono queste parole chiave nei loro titoli verranno prima cercati, quindi il risultato verrà limitato solo agli elementi ai quali è stato assegnato il tag.

Non supporta l&#39;estrazione dei facet.

#### Proprietà {#Properties-1}

* **`tagsearch`** - parola chiave da cercare nei titoli dei tag
* **`property`** - proprietà (o percorso relativo alla proprietà) da considerare (impostazione predefinita  `cq:tags`)
* **`lang`** - per eseguire la ricerca solo in un determinato titolo di tag localizzato (ad es.  `de`)
* **`all`** - valore booleano per cercare il testo completo dell&#39;intero tag, ad esempio tutti i titoli, la descrizione ecc. (ha precedenza su `lang`)

### tipo {#type}

Questo predicato limita i risultati a un tipo di nodo JCR specifico, sia i tipi di nodo primario che i tipi di mixin. Verranno inoltre individuati sottotipi di tale tipo di nodo. Gli indici di ricerca del repository devono coprire i tipi di nodo per un&#39;esecuzione efficiente.

Supporta l&#39;estrazione dei facet e fornisce bucket per ogni tipo univoco nei risultati.

#### Proprietà {#Properties-2}

* **`type`** - tipo di nodo o nome di mixaggio da cercare, ad esempio  `cq:Page`
