---
title: Framework di assegnazione tag AEM
description: Assegna tag ai contenuti e utilizza l’infrastruttura di tag di AEM per suddividerli in categorie e organizzarli.
exl-id: 25418d44-aace-4e73-be1a-4b1902f40403
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1559'
ht-degree: 0%

---

# Framework di assegnazione tag di AEM {#aem-tagging-framework}

L’assegnazione tag consente di categorizzare e organizzare i contenuti. I tag possono essere classificati in base a uno spazio dei nomi e a una tassonomia. Per informazioni dettagliate sull’utilizzo dei tag:

* Per informazioni sull&#39;assegnazione di tag ai contenuti come autore di contenuti, vedere [Utilizzo dei tag](/help/sites-cloud/authoring/sites-console/tags.md).
* Per informazioni sulla creazione e la gestione dei tag e sulla modalità di applicazione dei tag di contenuto, consulta Amministrazione dei tag .

Questo articolo si concentra sul framework sottostante che supporta i tag in AEM e su come utilizzarlo come sviluppatore.

## Introduzione {#introduction}

Per assegnare tag ai contenuti e utilizzare l’infrastruttura di assegnazione tag di AEM:

* Il tag deve esistere come nodo di tipo [`cq:Tag`](#cq-tag-node-type) nel [nodo principale della tassonomia](#taxonomy-root-node).
* Il mixin `NodeType` deve essere incluso nel nodo del contenuto con tag [`cq:Taggable`](#taggable-content-cq-taggable-mixin).
* [`TagID`](#tagid) viene aggiunto alla proprietà [`cq:tags`](#cq-tags-property) del nodo di contenuto e viene risolto in un nodo di tipo [`cq:Tag`](#cq-tag-node-type).

## Tipo di nodo cq:Tag {#cq-tag-node-type}

La dichiarazione di un tag viene acquisita nell&#39;archivio in un nodo di tipo `cq:Tag.`

* Un tag può essere una parola semplice (ad esempio, `sky`) o rappresentare una tassonomia gerarchica (ad esempio, `fruit/apple`, che significa sia il frutto generico che la mela più specifica).
* I tag sono identificati da un `TagID` univoco.
* Un tag include metadati facoltativi, ad esempio un titolo, titoli localizzati e una descrizione. Il titolo deve essere visualizzato nelle interfacce utente anziché `TagID`, se presente.

Il framework dei tag limita inoltre l’utilizzo da parte di autori e visitatori del sito di soli tag specifici e predefiniti.

### Caratteristiche tag {#tag-characteristics}

* Il tipo di nodo è `cq:Tag`.
* Il nome del nodo è un componente di [`TagID`](#tagid).
* [`TagID`](#tagid) include sempre uno [spazio dei nomi](#tag-namespace).
* La proprietà `jcr:title` (il titolo da visualizzare nell&#39;interfaccia utente) è facoltativa.
* La proprietà `jcr:description` è facoltativa.
* Quando si contengono nodi figlio, viene indicato come [tag contenitore](#container-tags).
* Il tag viene archiviato nel repository sotto un percorso di base denominato [nodo principale della tassonomia](#taxonomy-root-node).

### ID tag {#tagid}

Un `TagID` identifica un percorso che viene risolto in un nodo di tag nell&#39;archivio.

In genere, `TagID` è una scorciatoia `TagID` che inizia con lo spazio dei nomi oppure può essere un `TagID` assoluto che inizia dal [nodo principale della tassonomia](#taxonomy-root-node).

Quando il contenuto viene taggato, se non esiste ancora, la proprietà [`cq:tags`](#cq-tags-property) viene aggiunta al nodo del contenuto e `TagID` al valore dell&#39;array `String` della proprietà.

`TagID` è costituito da un [namespace](#tag-namespace) seguito dal `TagID` locale. [I tag contenitore](#container-tags) contengono tag secondari che rappresentano un ordine gerarchico nella tassonomia. I tag secondari possono essere utilizzati per fare riferimento ai tag come qualsiasi `TagID` locale. Ad esempio, è possibile assegnare tag al contenuto con `fruit` anche se si tratta di un tag contenitore con tag secondari, ad esempio `fruit/apple` e `fruit/banana`.

### Nodo principale tassonomia {#taxonomy-root-node}

Il nodo principale della tassonomia è il percorso di base per tutti i tag nell’archivio. Il nodo principale della tassonomia deve essere *not* un nodo di tipo `cq:Tag`.

In AEM, il percorso di base è `/content/cq:tags` e il nodo principale è di tipo `cq:Folder`.

### Spazio dei nomi dei tag {#tag-namespace}

Gli spazi dei nomi consentono di raggruppare gli elementi. Il caso d’uso più tipico consiste nell’avere uno spazio dei nomi per sito (ad esempio, pubblico rispetto a interno) o per applicazione più grande (ad esempio, Sites o Assets), ma gli spazi dei nomi possono essere utilizzati per varie altre esigenze. Nell’interfaccia utente, gli spazi dei nomi vengono utilizzati per mostrare solo il sottoinsieme di tag (ovvero i tag di un determinato spazio dei nomi) applicabile al contenuto corrente.

Lo spazio dei nomi del tag è il primo livello della sottostruttura della tassonomia, ovvero il nodo immediatamente sotto il [nodo principale della tassonomia](#taxonomy-root-node). Uno spazio dei nomi è un nodo di tipo `cq:Tag` il cui elemento padre non è un tipo di nodo `cq:Tag`.

Tutti i tag hanno uno spazio dei nomi. Se non viene specificato alcuno spazio dei nomi, il tag viene assegnato allo spazio dei nomi predefinito, ovvero `TagID` `default`, ovvero `/content/cq:tags/default`. In questi casi, il valore predefinito è `Standard Tags`.

### Tag contenitore {#container-tags}

Un tag contenitore è un nodo di tipo `cq:Tag` contenente un numero e un tipo qualsiasi di nodi figlio, che consente di migliorare il modello di tag con metadati personalizzati.

Inoltre, i tag contenitore (o super-tag) in una tassonomia fungono da sommatoria di tutti i tag secondari. Ad esempio, anche il contenuto con tag `fruit/apple` è considerato con tag `fruit`. In altre parole, la ricerca del contenuto con tag `fruit` troverebbe anche il contenuto con tag `fruit/apple`.

### Risoluzione di TagID {#resolving-tagids}

Se l&#39;ID tag contiene i due punti (`:`), lo spazio dei nomi viene separato dal tag o dalla sottotassonomia, che vengono quindi separati con barre normali (`/`). Se l’ID tag non ha due punti, viene implicito lo spazio dei nomi predefinito.

La posizione standard e unica dei tag è inferiore a `/content/cq:tags`.

I tag che fanno riferimento a percorsi non esistenti o che non fanno riferimento a un nodo `cq:Tag` vengono considerati non validi e vengono ignorati.

Nella tabella seguente vengono illustrati alcuni `TagID` di esempio, i relativi elementi e il modo in cui `TagID` viene risolto in un percorso assoluto nell&#39;archivio:

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

* [I tag in lingue diverse](tagging-applications.md#tags-in-different-languages) descrivono l&#39;utilizzo delle API come sviluppatore
* Gestione dei tag in lingue diverse, per descrivere l’utilizzo della console Assegnazione tag come amministratore

### Controllo accesso {#access-control}

I tag esistono come nodi nell&#39;archivio nel nodo principale della tassonomia [](#taxonomy-root-node). È possibile consentire o negare agli autori e ai visitatori del sito la creazione di tag in un determinato spazio dei nomi impostando ACL appropriati nell’archivio.

Il rifiuto delle autorizzazioni di lettura per alcuni tag o spazi dei nomi controlla la possibilità di applicare tag a contenuto specifico.

Una pratica tipica include:

* Consente al gruppo/ruolo `tag-administrators` di accedere in scrittura a tutti gli spazi dei nomi (aggiungere/modificare in `/content/cq:tags`). Questo gruppo viene fornito con AEM pronto all’uso.
* Consente agli utenti/autori di accedere in lettura a tutti i namespace che dovrebbero essere leggibili (per lo più tutti).
* Consentire agli utenti/autori di accedere in scrittura agli spazi dei nomi in cui i tag devono essere liberamente definibili dagli utenti/autori (`add_node` in `/content/cq:tags/some_namespace`)

## Contenuto con tag : cq:Taggable Mixin {#taggable-content-cq-taggable-mixin}

Affinché gli sviluppatori di applicazioni possano associare tag a un tipo di contenuto, la registrazione del nodo ([CND](https://jackrabbit.apache.org/jcr/node-type-notation.html)) deve includere il mixin `cq:Taggable` o il mixin `cq:OwnerTaggable`.

Il mixin `cq:OwnerTaggable`, che eredita da `cq:Taggable`, ha lo scopo di indicare che il contenuto può essere classificato dal proprietario/autore. In AEM è solo un attributo del nodo `cq:PageContent`. Il mixin `cq:OwnerTaggable` non è richiesto dal framework di assegnazione tag.

>[!NOTE]
>
>Si consiglia di abilitare i tag solo nel nodo di livello superiore di un elemento di contenuto aggregato (o nel relativo nodo `jcr:content`). Alcuni esempi:
>
>* Pagine (`cq:Page`) in cui il nodo `jcr:content` è di tipo `cq:PageContent`, che include il mixin `cq:Taggable`.
>* Assets (`cq:Asset`) dove il nodo `jcr:content/metadata` ha sempre il mixin `cq:Taggable`.

### Notazione del tipo di nodo (CND) {#node-type-notation-cnd}

Le definizioni dei tipi di nodo esistono nell’archivio come file CND. La notazione CND è definita nella [documentazione JCR](https://jackrabbit.apache.org/jcr/node-type-notation.html).

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

La proprietà `cq:tags` è un array `String` utilizzato per memorizzare uno o più `TagID` quando vengono applicati al contenuto da autori o visitatori del sito. La proprietà ha un significato solo quando viene aggiunta a un nodo definito con il mixin [`cq:Taggable`](#taggable-content-cq-taggable-mixin).

>[!NOTE]
>
>Per utilizzare la funzionalità di assegnazione tag di AEM, le applicazioni sviluppate personalizzate non devono definire proprietà di tag diverse da `cq:tags`.

## Spostamento e unione di tag {#moving-and-merging-tags}

Di seguito è riportata una descrizione degli effetti nell’archivio durante lo spostamento o l’unione di tag tramite la console Assegnazione tag.

Quando il tag A viene spostato o unito al tag B in `/content/cq:tags`:

* Il tag A non viene eliminato e riceve una proprietà `cq:movedTo`.
   * `cq:movedTo` punti al tag B.
   * Questa proprietà indica che il tag A è stato spostato o unito al tag B.
   * Lo spostamento del tag B aggiorna di conseguenza questa proprietà.
   * Il tag A è quindi nascosto ed è mantenuto solo nell’archivio in modo da poter risolvere gli ID tag nei nodi di contenuto che puntano al tag A.
   * Il garbage collector dei tag rimuove tag come tag A una volta che nessun altro nodo di contenuto vi punta.
   * Un valore speciale per la proprietà `cq:movedTo` è `nirvana`, che viene applicato quando il tag viene eliminato ma non può essere rimosso dall&#39;archivio perché sono presenti tag secondari con un `cq:movedTo` che devono essere conservati.

     >[!NOTE]
     >
     >La proprietà `cq:movedTo` viene aggiunta al tag spostato o unito solo se viene soddisfatta una delle seguenti condizioni:
     >
     > 1. Il tag viene utilizzato nel contenuto (ovvero ha un riferimento). OR
     > 1. Il tag include elementi figlio già spostati.
     >
* Il tag B viene creato (in caso di spostamento) e riceve una proprietà `cq:backlinks`.
   * `cq:backlinks` mantiene i riferimenti nell&#39;altra direzione. In altre parole, mantiene un elenco di tutti i tag che sono stati spostati o uniti con il tag B.
   * Questa funzionalità è necessaria principalmente per mantenere aggiornate le proprietà `cq:movedTo` quando il tag B viene spostato/unito/eliminato o quando il tag B viene attivato, nel qual caso devono essere attivati anche tutti i relativi tag di backlink.

     >[!NOTE]
     >
     >La proprietà `cq:backlinks` viene aggiunta al tag spostato o unito solo se viene soddisfatta una delle seguenti condizioni:
     >
     > 1. Il tag viene utilizzato nel contenuto (ovvero ha un riferimento), oppure
     > 1. Il tag include elementi figlio già spostati.

La lettura di una proprietà `cq:tags` di un nodo di contenuto richiede la seguente risoluzione:

1. Se non viene trovata alcuna corrispondenza in `/content/cq:tags`, non verrà restituito alcun tag.
1. Se per il tag è impostata la proprietà `cq:movedTo`, viene seguito l&#39;ID del tag di riferimento.
   * Questo passaggio viene ripetuto se il tag seguito ha una proprietà `cq:movedTo`.
1. Se il tag seguito non ha una proprietà `cq:movedTo`, il tag verrà letto.

Per pubblicare la modifica quando un tag è stato spostato o unito, è necessario replicare il nodo `cq:Tag` e tutti i relativi collegamenti. Questa replica viene eseguita automaticamente quando il tag viene attivato nella console di amministrazione dei tag.

Gli aggiornamenti successivi alla proprietà `cq:tags` della pagina eliminano automaticamente i riferimenti precedenti. La pulizia viene attivata perché la risoluzione di un tag spostato tramite l’API restituisce il tag di destinazione, fornendo così l’ID del tag di destinazione.
