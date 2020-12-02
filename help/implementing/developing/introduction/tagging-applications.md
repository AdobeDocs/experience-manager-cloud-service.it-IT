---
title: Creazione di tag nelle applicazioni AEM
description: Operazioni a livello di programmazione con i tag o l'estensione di tag all'interno di un'applicazione AEM personalizzata
translation-type: tm+mt
source-git-commit: ce55065c3ae6a2350ed06811af76477df7c11291
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---


# Creazione di tag nelle applicazioni AEM {#building-tagging-into-aem-applications}

Per utilizzare in modo programmatico i tag o estenderli all&#39;interno di un&#39;applicazione AEM personalizzata, in questo documento viene descritto l&#39;utilizzo del

* [API di tag](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html)

che interagisce con il

* [Framework di tag](tagging-framework.md)

Per ulteriori informazioni sui tag:

* Per informazioni sull&#39;assegnazione di tag ai contenuti come autori di contenuti, consultate [Utilizzo di tag](/help/sites-cloud/authoring/features/tags.md).
* Consultate Amministrazione dei tag per la prospettiva dell’amministratore sulla creazione e gestione dei tag, nonché per informazioni sui tag di contenuto applicati.

## Panoramica dell&#39;API Tagging {#overview-of-the-tagging-api}

L&#39;implementazione del [framework di tag](tagging-framework.md) in AEM consente la gestione di tag e contenuti di tag mediante l&#39;API JCR. `TagManager` assicura che i tag immessi come valori nella proprietà della matrice di  `cq:tags` stringhe non vengano duplicati,  `TagID`che rimuoverà puntando a tag e aggiornamenti non esistenti  `TagID`per i tag spostati o uniti. `TagManager` utilizza un listener di osservazione JCR che ripristina le modifiche non corrette. Le classi principali si trovano nel pacchetto [com.day.cq.tagging](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/package-summary.html):

* `JcrTagManagerFactory` - restituisce un&#39;implementazione JCR di un  `TagManager`. È l’implementazione di riferimento dell’API Tagging.
* `TagManager` - consente di risolvere e creare tag in base a percorsi e nomi.
* `Tag` - definisce l&#39;oggetto tag.

### Ottenimento di un gestore di tag basato su JCR {#getting-a-jcr-based-tagmanager}

Per recuperare un&#39;istanza `TagManager`, è necessario disporre di un JCR `Session` e chiamare `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

Nel contesto Sling tipico è anche possibile adattarsi a un `TagManager` dal `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Recupero di un oggetto Tag {#retrieving-a-tag-object}

È possibile recuperare un `Tag` tramite `TagManager`, risolvendo un tag esistente o creandone uno nuovo:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

Per l&#39;implementazione basata su JCR, che esegue il mapping di `Tags` su JCR `Nodes`, è possibile utilizzare direttamente il meccanismo di Sling `adaptTo` se si dispone della risorsa (ad esempio, `/content/cq:tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

Mentre un tag può essere convertito solo da *una risorsa (non da un nodo), un tag può essere convertito in* un nodo e una risorsa:**

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>L&#39;adattamento diretto da `Node` a `Tag` non è possibile, perché `Node` non implementa il metodo Sling `Adaptable.adaptTo(Class)`.

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
>La `RangeIterator` valida da utilizzare è:
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

Il Garbage Collector tag è un servizio di sfondo che pulisce i tag nascosti e inutilizzati. I tag nascosti e inutilizzati sono tag inferiori a `/content/cq:tags` che hanno una proprietà `cq:movedTo` e non sono utilizzati su un nodo di contenuto. Hanno un conteggio pari a zero. Utilizzando questo processo di eliminazione pigra, il nodo di contenuto (ovvero la proprietà `cq:tags`) non deve essere aggiornato come parte dell&#39;operazione di spostamento o unione. I riferimenti nella proprietà `cq:tags` vengono aggiornati automaticamente quando la proprietà `cq:tags` viene aggiornata, ad esempio tramite la finestra di dialogo delle proprietà della pagina.

Per impostazione predefinita, il Garbage Collector tag viene eseguito una volta al giorno. È possibile configurare in:

`http://<host>:<port>/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector`

## Ricerca tag ed Elenco tag {#tag-search-and-tag-listing}

La ricerca di tag e l’elenco dei tag funzionano come segue:

* La ricerca di `TagID` cerca i tag per i quali la proprietà `cq:movedTo` è impostata su `TagID` e segue attraverso `cq:movedTo` `TagID`s.
* La ricerca del titolo del tag cerca solo i tag privi di proprietà `cq:movedTo`.

## Tag in diverse lingue {#tags-in-different-languages}

Un tag `title` può essere definito in diverse lingue. Al nodo del tag viene quindi aggiunta una proprietà sensibile alla lingua. Questa proprietà ha il formato `jcr:title.<locale>`, ad esempio `jcr:title.fr` per la traduzione in francese. `<locale>` deve essere una stringa di lingua ISO in lettere minuscole e utilizzare carattere di sottolineatura (`_`) invece di trattino/trattino (`-`), ad esempio:  `de_ch`.

Ad esempio, quando il tag **Animals** viene aggiunto alla pagina **Products**, il valore `stockphotography:animals` viene aggiunto alla proprietà `cq:tags` del nodo `/content/wknd/en/products/jcr:content`. Il nodo del tag fa riferimento alla traduzione.

L&#39;API lato server include metodi `title` localizzati:

* [`com.day.cq.tagging.Tag`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/Tag.html)
   * `getLocalizedTitle(Locale locale)`
   * `getLocalizedTitlePaths()`
   * `getLocalizedTitles()`
   * `getTitle(Locale locale)`
   * `getTitlePath(Locale locale)`
* [`com.day.cq.tagging.TagManager`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/TagManager.html)
   * `canCreateTagByTitle(String tagTitlePath, Locale locale)`
   * `createTagByTitle(String tagTitlePath, Locale locale)`
   * `resolveByTitle(String tagTitlePath, Locale locale)`

In AEM, la lingua può essere ottenuta dalla lingua della pagina o dalla lingua dell’utente.

Per i tag, la localizzazione dipende dal contesto in cui è possibile visualizzare il tag `titles` nella lingua della pagina, nella lingua dell’utente o in qualsiasi altra lingua.

### Aggiunta di una nuova lingua alla finestra di dialogo Modifica tag {#adding-a-new-language-to-the-edit-tag-dialog}

La procedura seguente descrive come aggiungere una nuova lingua (ad esempio il finlandese) alla finestra di dialogo **Modifica tag**:

1. In **CRXDE**, modificare la proprietà multi-valore `languages` del nodo `/content/cq:tags`.
1. Aggiungete `fi_fi`, che rappresenta l&#39;impostazione internazionale finlandese, e salvate le modifiche.

Il finlandese è ora disponibile nella finestra di dialogo dei tag delle proprietà della pagina e nella finestra di dialogo **Edit Tag** quando si modifica un tag nella console **Tagging**.

>[!NOTE]
>
>La nuova lingua deve essere una delle AEM lingue riconosciute, ovvero deve essere disponibile come nodo sotto `/libs/wcm/core/resources/languages`.
