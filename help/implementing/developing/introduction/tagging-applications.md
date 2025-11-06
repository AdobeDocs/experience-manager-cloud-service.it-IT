---
title: Creazione di tag nelle applicazioni AEM
description: Utilizzare i tag a livello di programmazione o estenderli all’interno di un’applicazione AEM personalizzata
exl-id: a106dce1-5d51-406a-a563-4dea83987343
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 1%

---

# Creazione di tag nelle applicazioni AEM {#building-tagging-into-aem-applications}

Ai fini dell’utilizzo a livello di programmazione dei tag o dell’estensione dei tag all’interno di un’applicazione AEM personalizzata, questo documento descrive l’utilizzo di

* [API di assegnazione tag](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html)

che interagisce con

* [Framework di tag](tagging-framework.md)

Per informazioni correlate sull’assegnazione tag:

* Per informazioni sull&#39;assegnazione di tag ai contenuti come autore di contenuti, vedere [Utilizzo dei tag](/help/sites-cloud/authoring/sites-console/tags.md).
* Per informazioni sulla creazione e la gestione dei tag e sulla modalità di applicazione dei tag di contenuto, consulta Amministrazione dei tag .

## Panoramica dell’API di assegnazione tag {#overview-of-the-tagging-api}

L&#39;implementazione del [framework dei tag](tagging-framework.md) in AEM consente la gestione di tag e contenuti di tag tramite l&#39;API JCR. `TagManager` garantisce che i tag immessi come valori nella proprietà dell&#39;array di stringhe `cq:tags` non siano duplicati. Rimuove `TagID` che puntano a tag non esistenti e aggiorna `TagID` per i tag spostati o uniti. `TagManager` utilizza un listener di osservazione JCR che ripristina eventuali modifiche non corrette. Le classi principali si trovano nel pacchetto [com.day.cq.tagging](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/package-summary.html):

* `JcrTagManagerFactory` - restituisce un&#39;implementazione basata su JCR di un `TagManager`. È l’implementazione di riferimento dell’API di assegnazione tag.
* `TagManager` - consente di risolvere e creare tag in base a percorsi e nomi.
* `Tag` - definisce l&#39;oggetto tag.

### Ottenere un TagManager basato su JCR {#getting-a-jcr-based-tagmanager}

Per recuperare un&#39;istanza `TagManager`, è necessario disporre di un JCR `Session` e chiamare `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

Nel contesto Sling tipico è inoltre possibile adattarsi a un `TagManager` da `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Recupero di un oggetto Tag {#retrieving-a-tag-object}

È possibile recuperare `Tag` tramite `TagManager`, risolvendo un tag esistente o creandone uno:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

Per l&#39;implementazione basata su JCR, che mappa `Tags` su JCR `Nodes`, puoi utilizzare direttamente il meccanismo `adaptTo` di Sling se disponi della risorsa (ad esempio, `/content/cq:tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

Mentre un tag può essere convertito solo *da* risorsa (non nodo), un tag può essere convertito *in* sia nodo che risorsa:

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>L&#39;adattamento diretto da `Node` a `Tag` non è possibile perché `Node` non implementa il metodo Sling `Adaptable.adaptTo(Class)`.

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
>`RangeIterator` valido da utilizzare:
>
>`com.day.cq.commons.RangeIterator`

### Eliminazione dei tag {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### Replica dei tag {#replicating-tags}

È possibile utilizzare il servizio di replica (`Replicator`) con i tag perché i tag sono di tipo `nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## Tag Garbage Collector {#the-tag-garbage-collector}

Il garbage collector dei tag è un servizio in background che consente di pulire i tag nascosti e non utilizzati. I tag nascosti e inutilizzati sono tag al di sotto di `/content/cq:tags` che hanno una proprietà `cq:movedTo` e non sono utilizzati in un nodo di contenuto. Hanno un conteggio di zero. Utilizzando questo processo di eliminazione lenta, non è necessario aggiornare il nodo del contenuto (ovvero la proprietà `cq:tags`) come parte dell&#39;operazione di spostamento o unione. I riferimenti nella proprietà `cq:tags` vengono aggiornati automaticamente quando la proprietà `cq:tags` viene aggiornata, ad esempio tramite la finestra di dialogo delle proprietà della pagina.

Il garbage collector dei tag viene eseguito per impostazione predefinita una volta al giorno. Può essere configurato in:

`http://<host>:<port>/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector`

## Ricerca di tag ed elenco di tag {#tag-search-and-tag-listing}

La ricerca dei tag e l’elenco dei tag funzionano come segue:

* La ricerca di `TagID` cerca i tag con la proprietà `cq:movedTo` impostata su `TagID` e segue i `cq:movedTo` `TagID`.
* La ricerca del titolo del tag esegue la ricerca solo nei tag che non hanno una proprietà `cq:movedTo`.

## Tag in lingue diverse {#tags-in-different-languages}

È possibile definire un tag `title` in lingue diverse. Al nodo del tag viene quindi aggiunta una proprietà sensibile alla lingua. Questa proprietà ha il formato `jcr:title.<locale>`, ad esempio `jcr:title.fr` per la traduzione francese. `<locale>` deve essere una stringa delle impostazioni internazionali ISO minuscole e utilizzare il carattere di sottolineatura (`_`) invece del trattino (`-`), ad esempio: `de_ch`.

Ad esempio, quando il tag **Animals** viene aggiunto alla pagina **Products**, il valore `stockphotography:animals` viene aggiunto alla proprietà `cq:tags` del nodo `/content/wknd/en/products/jcr:content`. Viene fatto riferimento alla traduzione dal nodo del tag.

L&#39;API lato server ha localizzato `title` metodi correlati:

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

Per i tag, la localizzazione dipende dal contesto, in quanto il tag `titles` può essere visualizzato nella lingua della pagina, nella lingua dell&#39;utente o in qualsiasi altra lingua.

### Aggiunta di una nuova lingua alla finestra di dialogo Modifica tag {#adding-a-new-language-to-the-edit-tag-dialog}

La procedura seguente descrive come aggiungere una nuova lingua (ad esempio, finlandese) alla finestra di dialogo **Modifica tag**:

1. In **CRXDE**, modificare la proprietà multivalore `languages` del nodo `/content/cq:tags`.
1. Aggiungere `fi_fi`, che rappresenta la lingua finlandese, e salvare le modifiche.

Il finlandese è ora disponibile nella finestra di dialogo dei tag delle proprietà della pagina e nella finestra di dialogo **Modifica tag** quando si modifica un tag nella console **Assegnazione tag**.

>[!NOTE]
>
>La nuova lingua deve essere una delle lingue riconosciute da AEM. Deve quindi essere disponibile come nodo sotto `/libs/wcm/core/resources/languages`.
