---
title: AEM Tagging Framework
description: Assegnare tag ai contenuti e sfruttare l’infrastruttura di tag AEM per suddividerli in categorie e organizzarli.
translation-type: tm+mt
source-git-commit: 4bf023068aa69fb6b69c6f2443703ea2bbbf7d42
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 0%

---


# Il AEM Tagging Framework {#aem-tagging-framework}

I tag consentono di classificare e organizzare il contenuto. I tag possono essere classificati da uno spazio dei nomi e una tassonomia. Per informazioni dettagliate sull’uso dei tag:

* Consultate [Utilizzo dei tag](/help/sites-cloud/authoring/features/tags.md) per informazioni sull’assegnazione di tag ai contenuti come autori di contenuti.
* Consultate Amministrazione dei tag per la prospettiva dell’amministratore sulla creazione e gestione dei tag, nonché per informazioni sui tag di contenuto applicati.

Questo articolo è incentrato sul framework sottostante che supporta l’assegnazione di tag in AEM e su come utilizzarlo come sviluppatore.

## Introduzione {#introduction}

Per assegnare tag ai contenuti e sfruttare l&#39;infrastruttura di tag AEM:

* Il tag deve essere un nodo di tipo [`cq:Tag`](#cq-tag-node-type) sotto il nodo principale della [tassonomia.](#taxonomy-root-node)
* Il nodo del contenuto con tag `NodeType` deve includere il [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin.
* Il nodo [`TagID`](#tagid) viene aggiunto alla [`cq:tags`](#cq-tags-property) proprietà del nodo di contenuto e viene risolto in un nodo di tipo [`cq:Tag`.](#cq-tag-node-type)

## cq:Tipo nodo tag {#cq-tag-node-type}

La dichiarazione di un tag viene acquisita nella directory archivio in un nodo di tipo `cq:Tag.`

* Un tag può essere una parola semplice (ad es. `sky`) o rappresentano una tassonomia gerarchica (ad es. `fruit/apple`, che significa sia il frutto generico che la mela più specifica).
* I tag sono identificati da un `TagID`elemento univoco.
* Un tag contiene metadati facoltativi quali un titolo, titoli localizzati e una descrizione. Il titolo deve essere visualizzato nelle interfacce utente invece che `TagID`, se presente.

Il framework di assegnazione tag consente inoltre di limitare gli autori e i visitatori del sito a utilizzare solo tag predefiniti specifici.

### Caratteristiche del tag {#tag-characteristics}

* Il tipo di nodo è `cq:Tag`.
* Il nome del nodo è un componente del [`TagID`.](#tagid)
* Include [`TagID`](#tagid) sempre uno [spazio nomi.](#tag-namespace)
* La `jcr:title` proprietà (Titolo da visualizzare nell’interfaccia utente) è facoltativa.
* The `jcr:description` property is optional.
* Quando contengono nodi secondari, viene definito tag [contenitore.](#container-tags)
* Il tag viene memorizzato nell&#39;archivio sotto un percorso di base denominato nodo principale della [tassonomia.](#taxonomy-root-node)

### ID tag {#tagid}

A `TagID` identifica un percorso che risolve un nodo di tag nella directory archivio.

In genere, `TagID` si tratta di una abbreviazione che `TagID` inizia con lo spazio dei nomi o può essere un valore assoluto a `TagID` partire dal nodo radice della [tassonomia.](#taxonomy-root-node)

Quando un contenuto è dotato di tag, se non esiste ancora, la [`cq:tags`](#cq-tags-property) proprietà viene aggiunta al nodo di contenuto e il contenuto `TagID` viene aggiunto al valore dell&#39; `String` array della proprietà.

Il campo `TagID` è costituito da uno [spazio dei nomi](#tag-namespace) seguito dal `TagID`nome locale. [I tag](#container-tags) del contenitore hanno dei tag secondari che rappresentano un ordine gerarchico nella tassonomia. I tag secondari possono essere utilizzati per fare riferimento ai tag come qualsiasi altro tag locale `TagID`. Ad esempio, `fruit` è consentito assegnare tag al contenuto, anche se si tratta di un tag contenitore con tag secondari, quali `fruit/apple` e `fruit/banana`.

### Nodo radice tassonomia {#taxonomy-root-node}

Il nodo principale della tassonomia è il percorso di base per tutti i tag presenti nella directory archivio. Il nodo principale della tassonomia *non* deve essere un nodo di tipo `cq:Tag`.

In AEM, il percorso di base è `/content/cq:tags` e il nodo principale è di tipo `cq:Folder`.

### Tag Namespace {#tag-namespace}

Gli spazi dei nomi consentono di raggruppare gli elementi. Il caso d’uso più tipico consiste nell’avere uno spazio nomi per sito (ad esempio pubblico o interno) o per applicazione più grande (ad esempio Siti o Risorse), ma gli spazi dei nomi possono essere utilizzati per varie altre esigenze. Gli spazi dei nomi vengono utilizzati nell&#39;interfaccia utente per mostrare solo il sottoinsieme di tag (cioè i tag di un determinato spazio dei nomi) applicabile al contenuto corrente.

Lo spazio dei nomi del tag è il primo livello nella struttura ad albero secondaria della tassonomia, ovvero il nodo immediatamente sotto il nodo principale della [tassonomia.](#taxonomy-root-node) Uno spazio dei nomi è un nodo di tipo `cq:Tag` il cui elemento principale non è un tipo di `cq:Tag` nodo.

Tutti i tag hanno uno spazio nomi. Se non viene specificato alcuno spazio dei nomi, il tag viene assegnato allo spazio dei nomi predefinito, ovvero `TagID` , `default`ad esempio `/content/cq:tags/default`.  In questi `Standard Tags`casi, per impostazione predefinita viene utilizzato il Titolo.

### Tag contenitore {#container-tags}

Un tag contenitore è un nodo di tipo `cq:Tag` contenente qualsiasi numero e tipo di nodi secondari, che consente di migliorare il modello di tag con metadati personalizzati.

Inoltre, i tag contenitore (o super-tag) in una tassonomia fungono da sottotitoli per tutti i tag secondari: ad esempio, il contenuto con `fruit/apple` cui è stato assegnato un tag viene considerato `fruit` anche come tag, ossia la ricerca di contenuto con cui è stato aggiunto un tag `fruit` potrebbe anche trovare il contenuto con cui è stato `fruit/apple`.

### Risoluzione degli ID tag {#resolving-tagids}

Se l&#39;ID del tag contiene due punti (`:`), i due punti separano lo spazio nomi dal tag o dalla sotto-tassonomia, che vengono quindi separati con le normali barre (`/`). Se l&#39;ID del tag non ha due punti, lo spazio dei nomi predefinito è implicito.

Di seguito è riportata la posizione standard e l’unica dei tag `/content/cq:tags`.

I tag che fanno riferimento a percorsi o percorsi non esistenti che non puntano a un `cq:Tag` nodo vengono considerati non validi e vengono ignorati.

Nella tabella seguente sono riportati alcuni esempi `TagID`e i relativi elementi, nonché il modo in cui la directory `TagID` risolve in un percorso assoluto nella directory archivio:

| `TagID` | Namespace | ID locale | Tag contenitore | Tag foglia | Percorso tag assoluto archivio |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`,`apple` | `braeburn` | `content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | (nessuno) | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | (nessuno) | (nessuno) | (nessuno) | `/content/cq:tags/dam` |
| `content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `content/cq:tags/category/car` |

### Localizzazione del titolo del tag {#localization-of-tag-title}

Quando il tag include la stringa del titolo opzionale `jcr:title`, è possibile localizzare il titolo per la visualizzazione aggiungendo la proprietà `jcr:title.<locale>`.

Per ulteriori dettagli, consulta:

* [Tag in diverse lingue,](tagging-applications.md#tags-in-different-languages) che descrive l&#39;utilizzo delle API come sviluppatore
* Gestione dei tag in diverse lingue, che descrive l’utilizzo della console Tagging come amministratore

### Controllo accesso {#access-control}

I tag esistono come nodi nel repository sotto il nodo principale della [tassonomia.](#taxonomy-root-node) È possibile consentire o negare agli autori e ai visitatori del sito di creare tag in un dato spazio nomi impostando ACL appropriati nell&#39;archivio.

La negazione delle autorizzazioni di lettura per alcuni tag o spazi di nomi consente di controllare la possibilità di applicare tag a contenuti specifici.

Una pratica tipica include:

* Consentire a gruppi/ruoli di accedere in scrittura a tutti gli spazi dei nomi (aggiungere/modificare in `tag-administrators` `/content/cq:tags`). Questo gruppo viene fornito con AEM out-of-the-box.
* Consentire a utenti/autori di accedere in lettura a tutti gli spazi dei nomi che dovrebbero essere leggibili (per lo più tutti).
* Consentire a utenti/autori di accedere in scrittura agli spazi dei nomi in cui i tag devono essere liberamente definibili da utenti/autori (`add_node` in `/content/cq:tags/some_namespace`)

## Contenuto variabile: cq:Mixin variabile {#taggable-content-cq-taggable-mixin}

Affinché gli sviluppatori di applicazioni possano allegare i tag a un tipo di contenuto, la registrazione del nodo ([CND](https://jackrabbit.apache.org/node-type-notation.html)) deve includere il `cq:Taggable` mixin o il `cq:OwnerTaggable` mixin.

Il `cq:OwnerTaggable` mixin, che eredita da `cq:Taggable`, ha lo scopo di indicare che il contenuto può essere classificato dal proprietario/autore. In AEM, è solo un attributo del `cq:PageContent` nodo. Il `cq:OwnerTaggable` mixin non è richiesto dal framework di assegnazione tag.

>[!NOTE]
>
>Si consiglia di abilitare solo i tag sul nodo di primo livello di un elemento di contenuto aggregato (o sul `jcr:content` nodo). Alcuni esempi:
>
>* Pagine (`cq:Page`) in cui il `jcr:content`nodo è di tipo `cq:PageContent`, che include il `cq:Taggable` mixin.
>* Risorse (`cq:Asset`) in cui il `jcr:content/metadata` nodo ha sempre il `cq:Taggable` mixin.


### Notazione tipo nodo (CND) {#node-type-notation-cnd}

Le definizioni dei tipi di nodo esistono nell&#39;archivio come file CND. La notazione CND è definita come parte della documentazione [JCR.](https://jackrabbit.apache.org/node-type-notation.html).

Le definizioni essenziali per i tipi di nodo inclusi in AEM sono le seguenti:

```xml
[cq:Tag] > mix:title, nt:base
    orderable
    - * (undefined) multiple
    - * (undefined)
    + * (nt:base) = cq:Tag version

[cq:Taggable]
    mixin
    - cq:tags (string) multiple

[cq:OwnerTaggable] > cq:Taggable
    mixin
```

## cq:tags, proprietà {#cq-tags-property}

La `cq:tags` proprietà è un `String` array utilizzato per memorizzare uno o più `TagID`elementi quando vengono applicati al contenuto da autori o visitatori del sito. La proprietà ha un significato solo quando viene aggiunta a un nodo definito con il [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin.

>[!NOTE]
>
>Per utilizzare AEM funzionalità di assegnazione tag, le applicazioni sviluppate personalizzate non devono definire proprietà di tag diverse da `cq:tags`.

## Spostamento e unione dei tag {#moving-and-merging-tags}

Di seguito è riportata una descrizione degli effetti presenti nell’archivio quando si spostano o si uniscono tag mediante la console Tagging.

Quando il tag A viene spostato o unito nel tag B in `/content/cq:tags`:

* Il tag A non viene eliminato e riceve una `cq:movedTo` proprietà.
   * `cq:movedTo` punta al tag B.
   * Questa proprietà indica che il tag A è stato spostato o unito nel tag B.
   * Se si sposta il tag B, questa proprietà verrà aggiornata di conseguenza.
   * Il tag A è quindi nascosto e viene conservato solo nell’archivio per risolvere gli ID tag nei nodi di contenuto che puntano al tag A.
   * Il raccoglitore di tag per elementi indesiderati rimuove i tag come tag A, a cui nessun altro nodo di contenuto punta.
   * Un valore speciale per la `cq:movedTo` proprietà è `nirvana`, che viene applicato quando il tag viene eliminato ma non può essere rimosso dall&#39;archivio perché esistono tag secondari con un tag `cq:movedTo` che deve essere mantenuto.

      >[!NOTE]
      >
      >La `cq:movedTo` proprietà viene aggiunta al tag spostato o unito solo se è soddisfatta una delle seguenti condizioni:
      >
      > 1. Il tag viene usato nel contenuto (ovvero ha un riferimento). OPPURE
      > 1. Nel tag sono presenti elementi figlio che sono già stati spostati.


* Il tag B viene creato (in caso di spostamento) e riceve una `cq:backlinks` proprietà.
   * `cq:backlinks` mantiene i riferimenti nella direzione opposta, ossia tiene un elenco di tutti i tag spostati o uniti al tag B.
   * Questo è richiesto per lo più per mantenere `cq:movedTo` le proprietà aggiornate quando il tag B viene spostato/unito/eliminato o quando il tag B è attivato, nel qual caso tutti i relativi tag backlink devono essere attivati.

      >[!NOTE]
      >
      >La `cq:backlinks` proprietà viene aggiunta al tag spostato o unito solo se è soddisfatta una delle seguenti condizioni:
      >
      > 1. Il tag viene usato nel contenuto (ovvero ha un riferimento). OPPURE
      > 1. Nel tag sono presenti elementi figlio che sono già stati spostati.


La lettura di una `cq:tags` proprietà di un nodo di contenuto comporta la risoluzione seguente:

1. Se non è presente alcuna corrispondenza in `/content/cq:tags`, non viene restituito alcun tag.
1. Se il tag ha una `cq:movedTo` proprietà impostata, viene seguito l&#39;ID del tag di riferimento.
   * Questo passaggio viene ripetuto purché il tag seguito abbia una `cq:movedTo` proprietà.
1. Se il tag seguito non ha una `cq:movedTo` proprietà, il tag viene letto.

Per pubblicare la modifica quando un tag è stato spostato o unito, è necessario replicare il `cq:Tag` nodo e tutti i relativi backlink. Questa operazione viene eseguita automaticamente quando il tag viene attivato nella console di amministrazione dei tag.

Gli aggiornamenti successivi alla `cq:tags` proprietà della pagina consentono di cancellare automaticamente i riferimenti precedenti. Questo viene attivato perché la risoluzione di un tag spostato attraverso l&#39;API restituisce il tag di destinazione, fornendo così l&#39;ID del tag di destinazione.
