---
title: Creazione di tag nelle applicazioni AEM
description: Funzionamento programmatico con tag o estensione tag all'interno di un'applicazione AEM personalizzata
exl-id: a106dce1-5d51-406a-a563-4dea83987343
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 1%

---

# Creazione di tag nelle applicazioni AEM {#building-tagging-into-aem-applications}

Per lavorare in modo programmatico con i tag o per estendere i tag all&#39;interno di un&#39;applicazione di AEM personalizzata, in questo documento viene descritto l&#39;utilizzo del

* [API di assegnazione tag](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html)

che interagisce con

* [Framework di assegnazione tag](tagging-framework.md)

Per informazioni correlate sull’assegnazione tag:

* Vedi [Utilizzo dei tag](/help/sites-cloud/authoring/features/tags.md) per informazioni sull’assegnazione tag ai contenuti come autore di contenuti.
* Per informazioni sulla creazione e la gestione dei tag, nonché sulla prospettiva di un amministratore, consulta Gestione dei tag .

## Panoramica dell’API di assegnazione tag {#overview-of-the-tagging-api}

L&#39;attuazione [framework di assegnazione tag](tagging-framework.md) in AEM consente la gestione di tag e contenuti tag utilizzando l’API JCR. `TagManager` assicura che i tag immessi come valori nel `cq:tags` la proprietà string array non è duplicata, viene rimossa `TagID`s indica tag e aggiornamenti non esistenti `TagID`s per i tag spostati o uniti. `TagManager` utilizza un listener di osservazione JCR che ripristina eventuali modifiche errate. Le classi principali sono [com.day.cq.tagging](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html) pacchetto:

* `JcrTagManagerFactory` - restituisce un&#39;implementazione basata su JCR di un `TagManager`. È l’implementazione di riferimento dell’API di assegnazione tag.
* `TagManager` - consente di risolvere e creare tag in base a percorsi e nomi.
* `Tag` - definisce l’oggetto tag .

### Ottenere un TagManager basato su JCR {#getting-a-jcr-based-tagmanager}

Per recuperare un `TagManager` ad esempio, devi avere un JCR `Session` e di chiamare `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

Nel contesto Sling tipico puoi anche adattarti a un `TagManager` dal `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Recupero di un oggetto Tag {#retrieving-a-tag-object}

A `Tag` può essere recuperato tramite `TagManager`, risolvendo un tag esistente o creandone uno nuovo:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

Per l’implementazione basata su JCR, che mappa `Tags` su JCR `Nodes`, puoi utilizzare direttamente gli `adaptTo` se disponi della risorsa (ad esempio, `/content/cq:tags/default/my/tag`):

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
>Adattamento diretto da `Node` a `Tag` non è possibile, perché `Node` non implementa Sling `Adaptable.adaptTo(Class)` metodo .

### Ottenimento e impostazione dei tag {#getting-and-setting-tags}

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
>Il valore valido `RangeIterator` da utilizzare:
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

Il tag garbage Collector è un servizio di background che pulisce i tag nascosti e inutilizzati. I tag nascosti e non utilizzati sono tag sottostanti `/content/cq:tags` che hanno `cq:movedTo` e non vengono utilizzati in un nodo di contenuto. Hanno un conteggio di zero. Utilizzando questo processo di eliminazione pigra, il nodo del contenuto (ovvero `cq:tags` non è necessario aggiornare come parte dell&#39;operazione di spostamento o unione. I riferimenti nel `cq:tags` viene automaticamente aggiornata quando `cq:tags` viene aggiornata, ad esempio, tramite la finestra di dialogo delle proprietà della pagina.

Il Garbage Collector dei tag viene eseguito per impostazione predefinita una volta al giorno. Puoi configurarlo in:

`http://<host>:<port>/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector`

## Ricerca tag ed elenco tag {#tag-search-and-tag-listing}

La ricerca di tag e l’elenco dei tag funzionano come segue:

* La ricerca di `TagID` cerca i tag che hanno la proprietà `cq:movedTo` impostato su `TagID` e segue `cq:movedTo` `TagID`s.
* La ricerca del titolo del tag cerca solo i tag che non hanno un `cq:movedTo` proprietà.

## Tag in diverse lingue {#tags-in-different-languages}

Un tag `title` può essere definito in lingue diverse. Al nodo del tag viene quindi aggiunta una proprietà sensibile alla lingua. Questa proprietà ha il formato `jcr:title.<locale>`ad esempio, `jcr:title.fr` per la traduzione francese. `<locale>` deve essere una stringa internazionale ISO in minuscolo e utilizzare il carattere di sottolineatura (`_`) invece del trattino/trattino (`-`), ad esempio: `de_ch`.

Ad esempio quando **Animali** viene aggiunto al **Prodotti** page, il valore `stockphotography:animals` viene aggiunto alla proprietà `cq:tags` del nodo `/content/wknd/en/products/jcr:content`. La traduzione viene referenziata dal nodo del tag.

L’API lato server è localizzata `title`Metodi correlati:

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

In AEM, la lingua può essere ottenuta dalla lingua della pagina o dalla lingua dell’utente.

Per l’assegnazione tag, la localizzazione dipende dal contesto come tag `titles` può essere visualizzato nella lingua della pagina, nella lingua dell’utente o in qualsiasi altra lingua.

### Aggiunta di una nuova lingua alla finestra di dialogo Modifica tag {#adding-a-new-language-to-the-edit-tag-dialog}

La procedura seguente descrive come aggiungere una nuova lingua (ad esempio, il finlandese) al **Modifica tag** finestra di dialogo:

1. In **CRXDE**, modifica la proprietà multivalore `languages` del nodo `/content/cq:tags`.
1. Aggiungi `fi_fi`, che rappresenta le impostazioni internazionali finlandesi e salva le modifiche.

Il finlandese è ora disponibile nella finestra di dialogo dei tag delle proprietà della pagina e nel **Modifica tag** durante la modifica di un tag **Assegnazione tag** console.

>[!NOTE]
>
>La nuova lingua deve essere una delle lingue riconosciute AEM, cioè deve essere disponibile come nodo qui sotto `/libs/wcm/core/resources/languages`.
