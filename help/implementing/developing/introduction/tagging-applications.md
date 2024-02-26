---
title: Creazione di tag nelle applicazioni AEM
description: Utilizzare i tag a livello di programmazione o estenderli all’interno di un’applicazione AEM personalizzata
exl-id: a106dce1-5d51-406a-a563-4dea83987343
source-git-commit: f6162dcbc5b7937d55922e8c963a402697110329
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 1%

---

# Creazione di tag nelle applicazioni AEM {#building-tagging-into-aem-applications}

Per utilizzare i tag a livello di programmazione o per estendere i tag all&#39;interno di un&#39;applicazione AEM personalizzata, in questo documento viene descritto l&#39;utilizzo di

* [API di assegnazione tag](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html)

che interagisce con

* [Framework di tag](tagging-framework.md)

Per informazioni correlate sull’assegnazione tag:

* Consulta [Utilizzo dei tag](/help/sites-cloud/authoring/sites-console/tags.md) per informazioni sull’assegnazione tag ai contenuti come autore di contenuti.
* Per informazioni sulla creazione e la gestione dei tag e sulla modalità di applicazione dei tag di contenuto, consulta Amministrazione dei tag .

## Panoramica dell’API di assegnazione tag {#overview-of-the-tagging-api}

L&#39;attuazione del [framework di assegnazione tag](tagging-framework.md) in AEM consente la gestione di tag e contenuti tag utilizzando l’API JCR. `TagManager` garantisce che i tag immessi come valori sul `cq:tags` la proprietà di array di stringhe non è duplicata, rimuove `TagID`s che rimanda a tag e aggiornamenti non esistenti `TagID`s per i tag spostati o uniti. `TagManager` utilizza un listener di osservazione JCR che ripristina eventuali modifiche non corrette. Le classi principali sono [com.day.cq.tagging](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html) pacchetto:

* `JcrTagManagerFactory` - restituisce un’implementazione basata su JCR di un `TagManager`. È l’implementazione di riferimento dell’API di assegnazione tag.
* `TagManager` : consente di risolvere e creare tag in base a percorsi e nomi.
* `Tag` : definisce l’oggetto tag.

### Ottenere un TagManager basato su JCR {#getting-a-jcr-based-tagmanager}

Per recuperare un `TagManager` istanza, è necessario disporre di un JCR `Session` e chiamare `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

Nel tipico contesto Sling puoi anche adattarti a una `TagManager` dal `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Recupero di un oggetto Tag {#retrieving-a-tag-object}

A `Tag` possono essere recuperati tramite `TagManager`, risolvendo un tag esistente o creandone uno:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

Per l’implementazione basata su JCR, che mappa `Tags` su JCR `Nodes`, puoi utilizzare direttamente Sling `adaptTo` se si dispone della risorsa (ad esempio, `/content/cq:tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

Mentre un tag può essere convertito solo *da* una risorsa (non un nodo), un tag può essere convertito *a* sia un nodo che una risorsa:

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>Adattamento diretto da `Node` a `Tag` non è possibile, perché `Node` non implementa Sling `Adaptable.adaptTo(Class)` metodo.

### Recupero e impostazione dei tag {#getting-and-setting-tags}

```java
// Getting the tags of a Resource:
Tag[] tags = tagManager.getTags(resource);

// Setting tags to a Resource:
tagManager.setTags(resource, tags);
```

### Ricerca di tag {#searching-for-tags}

```java
// Searching for the Resource objects that are tagged with the tag object:
Iterator<Resource> it = tag.find();

// Retrieving the usage count of the tag object:
long count = tag.getCount();

// Searching for the Resource objects that are tagged with the tagID String:
 RangeIterator<Resource> it = tagManager.find(tagID);
```

>[!NOTE]
>
>Il valore `RangeIterator` da utilizzare è:
>
>`com.day.cq.commons.RangeIterator`

### Eliminazione dei tag {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### Replica dei tag {#replicating-tags}

È possibile utilizzare il servizio di replica (`Replicator`) con tag perché i tag sono di tipo `nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## Tag Garbage Collector {#the-tag-garbage-collector}

Il garbage collector dei tag è un servizio in background che consente di pulire i tag nascosti e non utilizzati. Di seguito sono riportati i tag nascosti e non utilizzati `/content/cq:tags` che hanno un `cq:movedTo` e non vengono utilizzati in un nodo di contenuto. Hanno un conteggio di zero. Utilizzando questo processo di eliminazione lenta, il nodo del contenuto (ovvero `cq:tags` ) non deve essere aggiornata come parte dell’operazione di spostamento o unione. I riferimenti in `cq:tags` vengono aggiornate automaticamente quando `cq:tags` viene aggiornata, ad esempio, tramite la finestra di dialogo proprietà pagina.

Il garbage collector dei tag viene eseguito per impostazione predefinita una volta al giorno. Può essere configurato in:

`http://<host>:<port>/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector`

## Ricerca di tag ed elenco di tag {#tag-search-and-tag-listing}

La ricerca dei tag e l’elenco dei tag funzionano come segue:

* La ricerca di `TagID` cerca i tag che hanno la proprietà `cq:movedTo` imposta su `TagID` e segue attraverso `cq:movedTo` `TagID`s.
* La ricerca del titolo del tag consente di cercare solo i tag che non hanno un `cq:movedTo` proprietà.

## Tag in lingue diverse {#tags-in-different-languages}

Un tag `title` possono essere definiti in diverse lingue. Al nodo del tag viene quindi aggiunta una proprietà sensibile alla lingua. Questa proprietà ha il formato `jcr:title.<locale>`ad esempio: `jcr:title.fr` per la traduzione francese. `<locale>` deve essere una stringa internazionale ISO minuscola e utilizzare il carattere di sottolineatura (`_`) invece del trattino (`-`), ad esempio: `de_ch`.

Ad esempio, quando **Animali** viene aggiunto al tag **Prodotti** pagina, il valore `stockphotography:animals` viene aggiunto alla proprietà `cq:tags` del nodo `/content/wknd/en/products/jcr:content`. Viene fatto riferimento alla traduzione dal nodo del tag.

L’API lato server ha localizzato `title`Metodi relativi a:

* [`com.day.cq.tagging.Tag`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/Tag.html)
   * `getLocalizedTitle(Locale locale)`
   * `getLocalizedTitlePaths()`
   * `getLocalizedTitles()`
   * `getTitle(Locale locale)`
   * `getTitlePath(Locale locale)`
* [`com.day.cq.tagging.TagManager`](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/TagManager.html)
   * `canCreateTagByTitle(String tagTitlePath, Locale locale)`
   * `createTagByTitle(String tagTitlePath, Locale locale)`
   * `resolveByTitle(String tagTitlePath, Locale locale)`

In AEM, la lingua può essere ottenuta o dalla lingua della pagina o dalla lingua dell’utente.

Per i tag, la localizzazione dipende dal contesto come tag `titles` può essere visualizzata nella lingua della pagina, nella lingua dell’utente o in qualsiasi altra lingua.

### Aggiunta di una nuova lingua alla finestra di dialogo Modifica tag {#adding-a-new-language-to-the-edit-tag-dialog}

Nella procedura seguente viene descritto come aggiungere una nuova lingua, ad esempio il finlandese, al **Modifica tag** finestra di dialogo:

1. In entrata **CRXDE**, modifica la proprietà con più valori `languages` del nodo `/content/cq:tags`.
1. Aggiungi `fi_fi`, che rappresenta la lingua finlandese, e salva le modifiche.

Il finlandese è ora disponibile nella finestra di dialogo dei tag delle proprietà della pagina e nel **Modifica tag** durante la modifica di un tag in **Assegnazione tag** console.

>[!NOTE]
>
>La nuova lingua deve essere una delle lingue riconosciute dall&#39;AEM. In altre parole, deve essere disponibile come nodo sotto `/libs/wcm/core/resources/languages`.
