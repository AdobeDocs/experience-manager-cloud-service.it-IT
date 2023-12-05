---
title: Framework di assegnazione tag AEM
description: Assegna tag ai contenuti e utilizza l’infrastruttura di tag AEM per suddividerli in categorie e organizzarli.
exl-id: 25418d44-aace-4e73-be1a-4b1902f40403
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '1562'
ht-degree: 0%

---

# Il quadro di riferimento per l&#39;assegnazione dei tag dell&#39;AEM {#aem-tagging-framework}

L’assegnazione tag consente di categorizzare e organizzare i contenuti. I tag possono essere classificati in base a uno spazio dei nomi e a una tassonomia. Per informazioni dettagliate sull’utilizzo dei tag:

* Consulta [Utilizzo dei tag](/help/sites-cloud/authoring/features/tags.md) per informazioni sull’assegnazione tag ai contenuti come autore di contenuti.
* Per informazioni sulla creazione e la gestione dei tag e sulla modalità di applicazione dei tag di contenuto, consulta Amministrazione dei tag .

Questo articolo si concentra sul framework sottostante che supporta l’assegnazione tag in AEM e su come utilizzarlo come sviluppatore.

## Introduzione {#introduction}

Per assegnare tag ai contenuti e utilizzare l&#39;infrastruttura dei tag AEM:

* Il tag deve esistere come nodo di tipo [`cq:Tag`](#cq-tag-node-type) sotto [nodo principale della tassonomia.](#taxonomy-root-node)
* Del nodo del contenuto con tag `NodeType` deve includere [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin.
* Il [`TagID`](#tagid) viene aggiunto al nodo del contenuto [`cq:tags`](#cq-tags-property) e viene risolto in un nodo di tipo [`cq:Tag`.](#cq-tag-node-type)

## cq:Tag Node Type {#cq-tag-node-type}

La dichiarazione di un tag viene acquisita nell’archivio in un nodo di tipo `cq:Tag.`

* Un tag può essere una parola semplice (ad esempio, `sky`) o rappresentano una tassonomia gerarchica (ad esempio, `fruit/apple`, vale a dire sia il frutto generico che la mela più specifica).
* I tag sono identificati da un `TagID`.
* Un tag include metadati facoltativi, ad esempio un titolo, titoli localizzati e una descrizione. Il titolo deve essere visualizzato nelle interfacce utente anziché nel `TagID`, se presente.

Il framework dei tag limita inoltre l’utilizzo da parte di autori e visitatori del sito di soli tag specifici e predefiniti.

### Caratteristiche tag {#tag-characteristics}

* Il tipo di nodo è `cq:Tag`.
* Il nome del nodo è un componente di [`TagID`.](#tagid)
* Il [`TagID`](#tagid) include sempre un [spazio dei nomi.](#tag-namespace)
* Il `jcr:title` (il Titolo da visualizzare nell&#39;interfaccia utente) è facoltativo.
* Il `jcr:description` proprietà è facoltativa.
* Quando si contengono nodi figlio, viene indicato come [tag contenitore.](#container-tags)
* Il tag viene memorizzato nell’archivio sotto un percorso di base denominato [nodo principale della tassonomia.](#taxonomy-root-node)

### ID tag {#tagid}

A `TagID` identifica un percorso che viene risolto in un nodo di tag nell’archivio.

In genere, il `TagID` è una stenografia `TagID` a partire dallo spazio dei nomi oppure può essere un valore assoluto `TagID` a partire dal [nodo principale della tassonomia.](#taxonomy-root-node)

Quando il contenuto viene taggato, se non esiste ancora, il [`cq:tags`](#cq-tags-property) viene aggiunta al nodo del contenuto e alla proprietà `TagID` viene aggiunto al di `String` valore dell’array.

Il `TagID` è costituito da un [namespace](#tag-namespace) seguito dal locale `TagID`. [Tag contenitore](#container-tags) dispongono di tag secondari che rappresentano un ordine gerarchico nella tassonomia. I tag secondari possono essere utilizzati per fare riferimento ai tag come qualsiasi tag locale `TagID`. Ad esempio, l’assegnazione di tag al contenuto con `fruit` è consentito, anche se si tratta di un tag contenitore con tag secondari, come `fruit/apple` e `fruit/banana`.

### Nodo principale tassonomia {#taxonomy-root-node}

Il nodo principale della tassonomia è il percorso di base per tutti i tag nell’archivio. Il nodo principale della tassonomia deve *non* essere un nodo di tipo `cq:Tag`.

Nell’AEM, il percorso di base è `/content/cq:tags` e il nodo principale è di tipo `cq:Folder`.

### Spazio dei nomi dei tag {#tag-namespace}

Gli spazi dei nomi consentono di raggruppare gli elementi. Il caso d’uso più tipico consiste nell’avere uno spazio dei nomi per sito (ad esempio, pubblico rispetto a interno) o per applicazione più grande (ad esempio, Sites o Assets), ma gli spazi dei nomi possono essere utilizzati per varie altre esigenze. Nell’interfaccia utente, gli spazi dei nomi vengono utilizzati per mostrare solo il sottoinsieme di tag (ovvero i tag di un determinato spazio dei nomi) applicabile al contenuto corrente.

Lo spazio dei nomi del tag è il primo livello della sottostruttura della tassonomia, che è il nodo immediatamente sotto il [nodo principale della tassonomia.](#taxonomy-root-node) Uno spazio dei nomi è un nodo di tipo `cq:Tag` il cui elemento padre non è un `cq:Tag` tipo di nodo.

Tutti i tag hanno uno spazio dei nomi. Se non viene specificato alcuno spazio dei nomi, il tag viene assegnato allo spazio dei nomi predefinito, che è `TagID` `default`, ovvero `/content/cq:tags/default`. Il titolo predefinito è `Standard Tags`in tali casi.

### Tag contenitore {#container-tags}

Un tag contenitore è un nodo di tipo `cq:Tag` contenente qualsiasi numero e tipo di nodi secondari, che consente di migliorare il modello di tag con metadati personalizzati.

Inoltre, i tag contenitore (o super-tag) in una tassonomia fungono da sommatoria di tutti i tag secondari. Ad esempio, contenuto con tag `fruit/apple` è considerato taggato con `fruit`Anche. In altre parole, la ricerca di contenuto con tag `fruit` troverebbe anche il contenuto taggato con `fruit/apple`.

### Risoluzione di TagID {#resolving-tagids}

Se l’ID tag contiene due punti (`:`), i due punti separano lo spazio dei nomi dal tag o dalla tassonomia secondaria, che vengono quindi separati con barre normali (`/`). Se l’ID tag non ha due punti, viene implicito lo spazio dei nomi predefinito.

Di seguito è riportata la posizione standard e unica dei tag `/content/cq:tags`.

Tag che fanno riferimento a percorsi non esistenti o che non puntano a un `cq:Tag` I nodi sono considerati non validi e vengono ignorati.

Nella tabella seguente sono riportati alcuni esempi `TagID`s, i relativi elementi e come `TagID` viene risolto in un percorso assoluto nel repository:

| `TagID` | Namespace | ID locale | Tag contenitore | Tag foglia | Percorso tag assoluto dell’archivio |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`,`apple` | `braeburn` | `content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | (nessuno) | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | (nessuno) | (nessuno) | (nessuno) | `/content/cq:tags/dam` |
| `content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `content/cq:tags/category/car` |

### Localizzazione del titolo del tag {#localization-of-tag-title}

Quando il tag include la stringa opzionale del titolo `jcr:title`, è possibile localizzare il titolo da visualizzare aggiungendo la proprietà `jcr:title.<locale>`.

Per ulteriori dettagli, vedi:

* [Tag in lingue diverse](tagging-applications.md#tags-in-different-languages) descrivere l’utilizzo delle API come sviluppatore
* Gestione dei tag in lingue diverse, per descrivere l’utilizzo della console Assegnazione tag come amministratore

### Controllo accesso {#access-control}

I tag esistono come nodi nell’archivio sotto [nodo principale della tassonomia.](#taxonomy-root-node) È possibile consentire o negare agli autori e ai visitatori del sito la creazione di tag in un determinato spazio dei nomi impostando ACL appropriati nell’archivio.

Il rifiuto delle autorizzazioni di lettura per alcuni tag o spazi dei nomi controlla la possibilità di applicare tag a contenuto specifico.

Una pratica tipica include:

* Consentire `tag-administrators` accesso in scrittura gruppo/ruolo a tutti gli spazi dei nomi (aggiungi/modifica in `/content/cq:tags`). Questo gruppo viene fornito con AEM preconfigurato.
* Consente agli utenti/autori di accedere in lettura a tutti i namespace che dovrebbero essere leggibili (per lo più tutti).
* Consentire agli utenti/autori di accedere in scrittura ai namespace in cui i tag dovrebbero essere liberamente definibili da parte di utenti/autori (`add_node` in `/content/cq:tags/some_namespace`)

## Contenuto assegnabile : cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

Per consentire agli sviluppatori di applicazioni di associare i tag a un tipo di contenuto, la registrazione del nodo ([CND](https://jackrabbit.apache.org/jcr/node-type-notation.html)) deve includere `cq:Taggable` mixin o `cq:OwnerTaggable` mixin.

Il `cq:OwnerTaggable` mixin, che eredita da `cq:Taggable`, ha lo scopo di indicare che il contenuto può essere classificato dal proprietario/autore. Nel AEM, è solo un attributo del `cq:PageContent` nodo. Il `cq:OwnerTaggable` Il mixin non è richiesto dal framework di assegnazione tag.

>[!NOTE]
>
>Si consiglia di abilitare i tag solo nel nodo di livello superiore di un elemento di contenuto aggregato (o nel relativo `jcr:content` nodo ). Alcuni esempi:
>
>* Pagine (`cq:Page`) in cui `jcr:content`il nodo è di tipo `cq:PageContent`, che include `cq:Taggable` mixin.
>* Risorse (`cq:Asset`) in cui `jcr:content/metadata` il nodo ha sempre `cq:Taggable` mixin.

### Notazione del tipo di nodo (CND) {#node-type-notation-cnd}

Le definizioni dei tipi di nodo esistono nell’archivio come file CND. La notazione CND è definita come parte della [Documentazione JCR](https://jackrabbit.apache.org/jcr/node-type-notation.html).

Le definizioni essenziali per i tipi di nodo inclusi nell’AEM sono le seguenti:

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

Il `cq:tags` la proprietà è un `String` array utilizzato per memorizzare uno o più `TagID`quando vengono applicati ai contenuti da autori o visitatori del sito. La proprietà ha un significato solo quando viene aggiunta a un nodo definito con [`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin.

>[!NOTE]
>
>Per utilizzare la funzionalità di assegnazione tag AEM, le applicazioni sviluppate personalizzate non devono definire proprietà di tag diverse da `cq:tags`.

## Spostamento e unione di tag {#moving-and-merging-tags}

Di seguito è riportata una descrizione degli effetti nell’archivio durante lo spostamento o l’unione di tag tramite la console Assegnazione tag.

Quando il tag A viene spostato o unito al tag B in `/content/cq:tags`:

* Il tag A non viene eliminato e riceve un `cq:movedTo` proprietà.
   * `cq:movedTo` punta al tag B.
   * Questa proprietà indica che il tag A è stato spostato o unito al tag B.
   * Lo spostamento del tag B aggiorna di conseguenza questa proprietà.
   * Il tag A è quindi nascosto ed è mantenuto solo nell’archivio in modo da poter risolvere gli ID tag nei nodi di contenuto che puntano al tag A.
   * Il garbage collector dei tag rimuove tag come tag A una volta che nessun altro nodo di contenuto vi punta.
   * Un valore speciale per `cq:movedTo` la proprietà è `nirvana`, applicato quando il tag viene eliminato ma non può essere rimosso dall’archivio perché sono presenti tag secondari con `cq:movedTo` questo deve essere mantenuto.

     >[!NOTE]
     >
     >Il `cq:movedTo` viene aggiunta al tag spostato o unito solo se viene soddisfatta una delle seguenti condizioni:
     >
     > 1. Il tag viene utilizzato nel contenuto (ovvero ha un riferimento). OPPURE
     > 1. Il tag include elementi figlio già spostati.
     >
* Il tag B viene creato (in caso di spostamento) e riceve `cq:backlinks` proprietà.
   * `cq:backlinks` mantiene i riferimenti nella direzione opposta. In altre parole, mantiene un elenco di tutti i tag che sono stati spostati o uniti con il tag B.
   * Questa funzionalità è richiesta principalmente per mantenere `cq:movedTo` proprietà aggiornate quando il tag B viene anche spostato/unito/eliminato o quando il tag B viene attivato, nel qual caso devono essere attivati anche tutti i relativi tag di backlink.

     >[!NOTE]
     >
     >Il `cq:backlinks` viene aggiunta al tag spostato o unito solo se viene soddisfatta una delle seguenti condizioni:
     >
     > 1. Il tag viene utilizzato nel contenuto (ovvero ha un riferimento), oppure
     > 1. Il tag include elementi figlio già spostati.

Lettura di un `cq:tags` La proprietà di un nodo di contenuto prevede la seguente risoluzione:

1. Se non viene trovata alcuna corrispondenza in `/content/cq:tags`, non viene restituito alcun tag.
1. Se il tag ha `cq:movedTo` impostata, viene seguito l’ID tag di riferimento.
   * Questo passaggio viene ripetuto purché il tag seguito abbia `cq:movedTo` proprietà.
1. Se il tag seguito non ha un `cq:movedTo` , il tag viene letto.

Per pubblicare la modifica quando un tag è stato spostato o unito, la `cq:Tag` e tutti i relativi backlink devono essere replicati. Questa replica viene eseguita automaticamente quando il tag viene attivato nella console di amministrazione dei tag.

Aggiornamenti successivi al `cq:tags` pulisci automaticamente i riferimenti precedenti. La pulizia viene attivata perché la risoluzione di un tag spostato tramite l’API restituisce il tag di destinazione, fornendo così l’ID del tag di destinazione.
