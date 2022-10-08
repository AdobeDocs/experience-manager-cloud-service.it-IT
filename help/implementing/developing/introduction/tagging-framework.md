---
title: Framework di assegnazione tag AEM
description: Assegna tag ai contenuti e sfrutta l’infrastruttura di assegnazione tag AEM per organizzarli e suddividerli in categorie.
exl-id: 25418d44-aace-4e73-be1a-4b1902f40403
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '1570'
ht-degree: 0%

---

# Framework di assegnazione tag AEM {#aem-tagging-framework}

I tag consentono di classificare e organizzare i contenuti. I tag possono essere classificati in base a uno spazio dei nomi e a una tassonomia. Per informazioni dettagliate sull’utilizzo dei tag:

* Vedi [Utilizzo dei tag](/help/sites-cloud/authoring/features/tags.md) per informazioni sull’assegnazione tag ai contenuti come autore di contenuti.
* Per informazioni sulla creazione e la gestione dei tag, nonché sulla prospettiva di un amministratore, consulta Gestione dei tag .

Questo articolo si concentra sul framework sottostante che supporta l’assegnazione di tag in AEM e su come sfruttarlo come sviluppatore.

## Introduzione {#introduction}

Per assegnare tag ai contenuti e sfruttare l’infrastruttura di assegnazione tag AEM :

* Il tag deve esistere come nodo di tipo [`cq:Tag`](#cq-tag-node-type) in [nodo principale della tassonomia.](#taxonomy-root-node)
* Il nodo del contenuto con tag `NodeType` deve includere [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin.
* La [`TagID`](#tagid) viene aggiunto al nodo del contenuto [`cq:tags`](#cq-tags-property) e risolve in un nodo di tipo [`cq:Tag`.](#cq-tag-node-type)

## cq:Tag Node Type {#cq-tag-node-type}

La dichiarazione di un tag viene acquisita nell’archivio in un nodo di tipo `cq:Tag.`

* Un tag può essere una parola semplice (ad esempio, `sky`) o rappresentano una tassonomia gerarchica (ad esempio, `fruit/apple`, che significa sia il frutto generico che la mela più specifica).
* I tag sono identificati da un `TagID`.
* Un tag contiene metadati facoltativi, ad esempio un titolo, titoli localizzati e una descrizione. Il titolo deve essere visualizzato nelle interfacce utente anziché nel `TagID`, se presente.

Il framework di assegnazione tag consente inoltre di limitare gli autori e i visitatori del sito a utilizzare solo tag predefiniti specifici.

### Caratteristiche del tag {#tag-characteristics}

* Il tipo di nodo è `cq:Tag`.
* Il nome del nodo è un componente del [`TagID`.](#tagid)
* La [`TagID`](#tagid) include sempre [spazio dei nomi.](#tag-namespace)
* La `jcr:title` (Titolo da visualizzare nell’interfaccia utente) è facoltativo.
* La `jcr:description` è facoltativo.
* Quando contengono nodi figlio, è indicato come [tag contenitore .](#container-tags)
* Il tag viene memorizzato nell’archivio sotto un percorso di base denominato [nodo principale della tassonomia.](#taxonomy-root-node)

### ID tag {#tagid}

A `TagID` identifica un percorso che si risolve in un nodo di tag nella directory archivio.

In genere, il `TagID` è una stenografia `TagID` a partire dallo spazio dei nomi o può essere un valore assoluto `TagID` a partire dal [nodo principale della tassonomia.](#taxonomy-root-node)

Quando il contenuto è contrassegnato, se non esiste ancora, la [`cq:tags`](#cq-tags-property) viene aggiunta al nodo del contenuto e il `TagID` viene aggiunto al `String` valore array.

La `TagID` è costituito da [namespace](#tag-namespace) seguito dal locale `TagID`. [Tag contenitore](#container-tags) dispongono di tag secondari che rappresentano un ordine gerarchico nella tassonomia. I tag secondari possono essere utilizzati per fare riferimento ai tag come qualsiasi altro tag locale `TagID`. Ad esempio, assegnare tag al contenuto con `fruit` è consentito, anche se si tratta di un tag contenitore con tag secondari, come `fruit/apple` e `fruit/banana`.

### Nodo principale tassonomia {#taxonomy-root-node}

Il nodo principale della tassonomia è il percorso di base per tutti i tag nel repository. Il nodo principale della tassonomia deve *not* essere un nodo di tipo `cq:Tag`.

In AEM, il percorso di base è `/content/cq:tags` e il nodo principale è di tipo `cq:Folder`.

### Spazio dei nomi tag {#tag-namespace}

I namespace consentono di raggruppare gli elementi. Il caso d’uso più tipico è quello di avere uno spazio dei nomi per sito (ad esempio pubblico o interno) o per applicazione più grande (ad esempio, Sites o Assets), ma i namespace possono essere utilizzati per varie altre esigenze. Nell’interfaccia utente i namespace vengono utilizzati per mostrare solo il sottoinsieme di tag (ovvero i tag di un determinato namespace) applicabile al contenuto corrente.

Lo spazio dei nomi del tag è il primo livello della sottostruttura della tassonomia, che è il nodo immediatamente sotto la [nodo principale della tassonomia.](#taxonomy-root-node) Uno spazio dei nomi è un nodo di tipo `cq:Tag` il cui genitore non è un `cq:Tag` tipo di nodo.

Tutti i tag hanno uno spazio dei nomi. Se non viene specificato alcun namespace, il tag viene assegnato allo spazio dei nomi predefinito, ovvero `TagID` `default`, vale a dire `/content/cq:tags/default`.  Per impostazione predefinita, il campo Titolo `Standard Tags`in tali casi.

### Tag contenitore {#container-tags}

Un tag contenitore è un nodo di tipo `cq:Tag` contenente qualsiasi numero e tipo di nodi figlio, che consente di migliorare il modello di tag con metadati personalizzati.

Inoltre, i tag contenitore (o super tag) in una tassonomia fungono da sotto-somma di tutti i tag secondari: ad esempio il contenuto con tag `fruit/apple` è considerato con tag `fruit` anche, ovvero la ricerca di contenuti con tag `fruit` troverà anche il contenuto con tag `fruit/apple`.

### Risoluzione degli ID tag {#resolving-tagids}

Se l&#39;ID del tag contiene due punti (`:`), separa lo spazio dei nomi dal tag o dalla tassonomia secondaria, che vengono poi separati con le normali barre (`/`). Se l’ID del tag non ha due punti, viene implicito il namespace predefinito.

Di seguito è riportata la posizione standard e l’unica posizione dei tag `/content/cq:tags`.

Tag che fanno riferimento a percorsi o percorsi non esistenti che non puntano a un `cq:Tag` i nodi sono considerati non validi e vengono ignorati.

Nella tabella seguente sono riportati alcuni esempi `TagID`s, i loro elementi e come `TagID` risolve in un percorso assoluto nell&#39;archivio:

| `TagID` | Namespace | ID locale | Tag contenitore | Tag foglia | Percorso tag assoluto archivio |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`,`apple` | `braeburn` | `content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | (nessuno) | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | (nessuno) | (nessuno) | (nessuno) | `/content/cq:tags/dam` |
| `content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `content/cq:tags/category/car` |

### Localizzazione del titolo del tag {#localization-of-tag-title}

Quando il tag include la stringa del titolo opzionale `jcr:title`, è possibile localizzare il titolo per la visualizzazione aggiungendo la proprietà `jcr:title.<locale>`.

Per maggiori dettagli vedi:

* [Tag in diverse lingue,](tagging-applications.md#tags-in-different-languages) che descrive l’utilizzo delle API come sviluppatore
* Gestione dei tag in diverse lingue, che descrive l’utilizzo della console Assegnazione tag come amministratore

### Controllo accesso {#access-control}

I tag esistono come nodi nell’archivio sotto [nodo principale della tassonomia.](#taxonomy-root-node) È possibile consentire o negare agli autori e ai visitatori del sito di creare tag in un dato spazio dei nomi impostando ACL appropriati nell’archivio.

Negare le autorizzazioni di lettura per alcuni tag o namespace controllerà la possibilità di applicare tag a contenuti specifici.

Una pratica tipica include:

* Consentire la `tag-administrators` accesso in scrittura di gruppo/ruolo a tutti i namespace (aggiungere/modificare in `/content/cq:tags`). Questo gruppo viene fornito con AEM preconfigurato.
* Consentire agli utenti/autori di accedere in lettura a tutti i namespace che dovrebbero essere leggibili per loro (per lo più tutti).
* Consentire a utenti/autori di accedere in scrittura a quei namespace in cui i tag devono essere liberamente definiti dagli utenti/autori (`add_node` sotto `/content/cq:tags/some_namespace`)

## Contenuto variabile : cq:Mixin taggabile {#taggable-content-cq-taggable-mixin}

Per consentire agli sviluppatori di applicazioni di allegare tag a un tipo di contenuto, la registrazione del nodo ([CND](https://jackrabbit.apache.org/node-type-notation.html)) deve includere `cq:Taggable` miscelazione o `cq:OwnerTaggable` mixin.

La `cq:OwnerTaggable` mixin, che eredita da `cq:Taggable`, indica che il contenuto può essere classificato dal proprietario/autore. In AEM, è solo un attributo del `cq:PageContent` nodo. La `cq:OwnerTaggable` il mixin non è richiesto dal framework di assegnazione tag.

>[!NOTE]
>
>Si consiglia di abilitare solo i tag sul nodo di primo livello di un elemento di contenuto aggregato (o sul relativo `jcr:content` node). Gli esempi includono:
>
>* Pagine (`cq:Page`) dove `jcr:content`il nodo è di tipo `cq:PageContent`, che include `cq:Taggable` mixin.
>* Risorse (`cq:Asset`) dove `jcr:content/metadata` il nodo ha sempre `cq:Taggable` mixin.


### Notazione del tipo di nodo (CND) {#node-type-notation-cnd}

Le definizioni dei tipi di nodo esistono nell’archivio come file CND. La notazione CND è definita come parte del [Documentazione JCR.](https://jackrabbit.apache.org/node-type-notation.html).

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

La `cq:tags` è una proprietà `String` array utilizzato per memorizzare uno o più `TagID`viene applicata al contenuto da autori o visitatori del sito. La proprietà ha un significato solo quando viene aggiunta a un nodo definito con [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin.

>[!NOTE]
>
>Per sfruttare AEM funzionalità di assegnazione tag, le applicazioni sviluppate personalizzate non devono definire proprietà di tag diverse da `cq:tags`.

## Spostamento e unione dei tag {#moving-and-merging-tags}

Di seguito è riportata una descrizione degli effetti nell’archivio durante lo spostamento o l’unione dei tag tramite la console Tagging .

Quando il tag A viene spostato o unito nel tag B in `/content/cq:tags`:

* Il tag A non viene eliminato e riceve un `cq:movedTo` proprietà.
   * `cq:movedTo` punta al tag B.
   * Questa proprietà significa che il tag A è stato spostato o unito nel tag B.
   * Lo spostamento del tag B comporterà l’aggiornamento di conseguenza di questa proprietà.
   * Il tag A è quindi nascosto e viene conservato solo nell’archivio per risolvere gli ID tag nei nodi di contenuto che puntano al tag A.
   * Il tag Garbage Collector rimuove i tag come tag A una volta nessun altro nodo di contenuto li punta.
   * Un valore speciale per `cq:movedTo` è `nirvana`, che viene applicata quando il tag viene eliminato ma non può essere rimosso dall’archivio perché sono presenti tag secondari con un `cq:movedTo` deve essere mantenuto.

      >[!NOTE]
      >
      >La `cq:movedTo` viene aggiunta al tag spostato o unito solo se viene soddisfatta una delle seguenti condizioni:
      >
      > 1. Il tag viene utilizzato nel contenuto (ovvero ha un riferimento). OPPURE
      > 1. Il tag include elementi secondari già spostati.

* Il tag B viene creato (in caso di spostamento) e riceve un `cq:backlinks` proprietà.
   * `cq:backlinks` mantiene i riferimenti nell’altra direzione, ovvero mantiene un elenco di tutti i tag spostati o uniti al tag B.
   * Questo è richiesto principalmente per mantenere `cq:movedTo` le proprietà sono aggiornate anche quando il tag B viene spostato/unito/eliminato o quando il tag B viene attivato, nel qual caso devono essere attivati anche tutti i suoi tag backlink.

      >[!NOTE]
      >
      >La `cq:backlinks` viene aggiunta al tag spostato o unito solo se viene soddisfatta una delle seguenti condizioni:
      >
      > 1. Il tag viene utilizzato nel contenuto (ovvero ha un riferimento). OPPURE
      > 1. Il tag include elementi secondari già spostati.


Lettura di un `cq:tags` la proprietà di un nodo di contenuto comporta la seguente risoluzione:

1. Se non c&#39;è alcuna corrispondenza in `/content/cq:tags`, non viene restituito alcun tag.
1. Se il tag ha un `cq:movedTo` impostato sulla proprietà , viene seguito l&#39;ID tag di riferimento.
   * Questo passaggio viene ripetuto purché il tag seguito abbia un `cq:movedTo` proprietà.
1. Se il tag seguito non ha un `cq:movedTo` , il tag viene letto.

Per pubblicare la modifica quando un tag è stato spostato o unito, l’ `cq:Tag` e tutti i relativi backlink devono essere replicati. Questa operazione viene eseguita automaticamente quando il tag viene attivato nella console di amministrazione dei tag.

Aggiornamenti successivi al `cq:tags` consente di pulire automaticamente i vecchi riferimenti. Questo viene attivato perché la risoluzione di un tag spostato attraverso l&#39;API restituisce il tag di destinazione, fornendo così l&#39;ID del tag di destinazione.
