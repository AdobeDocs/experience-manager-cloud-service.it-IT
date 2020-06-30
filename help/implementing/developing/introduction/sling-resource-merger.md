---
title: Utilizzo di Sling Resource Merger in  Adobe Experience Manager come Cloud Service
description: Sling Resource Merger fornisce servizi per accedere e unire le risorse
translation-type: tm+mt
source-git-commit: 1a8a9781da7390d25ec687d46af8d8a976c069bc
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 1%

---


# Utilizzo di Sling Resource Merger in AEM come Cloud Service {#using-the-sling-resource-merger-in-aem}

## Scopo {#purpose}

Sling Resource Merger fornisce servizi per accedere e unire le risorse. Fornisce meccanismi di diff (differenziazione) per entrambi:

* **[Sovrapposizioni](/help/implementing/developing/introduction/overlays.md)**di risorse tramite i percorsi[di ricerca](/help/implementing/developing/introduction/overlays.md#configuring-the-search-paths)configurati.

* **Ignora** le finestre di dialogo dei componenti per l’interfaccia touch (`cq:dialog`), utilizzando la gerarchia dei tipi di risorse (tramite la proprietà `sling:resourceSuperType`).

Con Sling Resource Merger, le risorse e/o le proprietà di sovrapposizione/esclusione vengono unite con le risorse/proprietà originali:

* Il contenuto della definizione personalizzata ha una priorità maggiore rispetto a quello dell&#39;originale (ovvero *sovrapposizioni* o *sostituzioni* ).

* Se necessario, [le proprietà](#properties) definite nella personalizzazione indicano in che modo verrà utilizzato il contenuto unito dall&#39;originale.

<!-- Still links to reference material in 6.5 -->

>[!CAUTION]
>
>La Fusione risorse Sling e i metodi correlati possono essere utilizzati solo con [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). Ciò significa anche che è adatto solo per l’interfaccia touch standard; in particolare, le sostituzioni definite in questo modo sono applicabili solo alla finestra di dialogo attivata dal tocco di un componente.
>
>Le sovrapposizioni/sostituzioni per altre aree (compresi altri aspetti di un componente abilitato per il tocco) comportano la copia del nodo e della struttura appropriati dall’originale a dove verrà definita la personalizzazione.

### Obiettivi di AEM {#goals-for-aem}

Gli obiettivi per l’utilizzo di Sling Resource Merger in AEM sono:

* accertatevi che le modifiche alla personalizzazione non vengano effettuate in `/libs`.
* ridurre la struttura da cui viene replicata `/libs`.

   Quando si utilizza la Fusione risorse Sling si consiglia di non copiare l&#39;intera struttura da `/libs` perché ciò comporterebbe la conservazione di troppe informazioni nella personalizzazione (in genere `/apps`). Duplicare le informazioni aumenta inutilmente la possibilità di problemi quando il sistema viene aggiornato in qualsiasi modo.

>[!NOTE]
>
>Le sostituzioni non dipendono dai percorsi di ricerca, ma utilizzano la proprietà `sling:resourceSuperType` per creare la connessione.
>
>Tuttavia, le sostituzioni sono spesso definite in `/apps`, in quanto la best practice in AEM consiste nel definire le personalizzazioni in `/apps`; questo è perché non devi cambiare niente sotto `/libs`.

>[!CAUTION]
>
>Non ***devi*** cambiare nulla nel `/libs` percorso.
>
>Questo perché il contenuto di `/libs` viene sovrascritto al successivo aggiornamento dell’istanza (e potrebbe essere sovrascritto quando si applica un hotfix o un feature pack).
>
>Il metodo consigliato per la configurazione e altre modifiche è:
>
>1. Ricreare l&#39;elemento richiesto (ovvero come esiste in `/libs`) in `/apps`
   >
   >
1. Apportare modifiche all&#39;interno `/apps`

>



### Proprietà {#properties}

La fusione delle risorse fornisce le seguenti proprietà:

* `sling:hideProperties` ( `String` o `String[]`)

   Specifica la proprietà, o l&#39;elenco di proprietà, da nascondere.

   Il carattere jolly `*` nasconde tutto.

* `sling:hideResource` ( `Boolean`)

   Indica se le risorse devono essere completamente nascoste, inclusi i relativi elementi figlio.

* `sling:hideChildren` ( `String` o `String[]`)

   Contiene il nodo secondario, o elenco di nodi secondari, da nascondere. Le proprietà del nodo verranno mantenute.

   Il carattere jolly `*` nasconde tutto.

* `sling:orderBefore` ( `String`)

   Contiene il nome del nodo di pari livello al quale il nodo corrente deve essere posizionato davanti.

Queste proprietà influiscono sul modo in cui le risorse/proprietà (da `/libs`) corrispondenti/originali vengono utilizzate dalla sovrapposizione/sostituzione (spesso in `/apps`).

### Creazione della struttura {#creating-the-structure}

Per creare una sovrapposizione o una sostituzione, è necessario ricreare il nodo originale, con la struttura equivalente, sotto la destinazione (in genere `/apps`). Ad esempio:

* Sovrapposizione

   * La definizione della voce di navigazione per la console Siti, come illustrato nella barra laterale, è definita in:

      `/libs/cq/core/content/nav/sites/jcr:title`

   * Per sovrapporre questo, create il seguente nodo:

      `/apps/cq/core/content/nav/sites`

      Quindi aggiornate la proprietà `jcr:title` come necessario.

* Override

   * La definizione della finestra di dialogo touch per la console Testo è definita in:

      `/libs/foundation/components/text/cq:dialog`

   * Per ignorare questo problema, create il seguente nodo, ad esempio:

      `/apps/the-project/components/text/cq:dialog`

Per creare una di queste è sufficiente ricreare la struttura dell&#39;ossatura. Per semplificare la ricreazione della struttura, tutti i nodi intermedi possono essere di tipo `nt:unstructured` (non devono riflettere il tipo di nodo originale; ad esempio, in `/libs`).

Nell&#39;esempio di sovrapposizione riportato sopra, sono necessari i seguenti nodi:

```shell
/apps
  /cq
    /core
      /content
        /nav
          /sites
```

>[!NOTE]
>
>Quando si utilizza la funzione Sling Resource Merger (ovvero quando si utilizza l’interfaccia touch standard), si consiglia di non copiare l’intera struttura da `/libs` tale funzionalità, in quanto comporterebbe la memorizzazione di troppe informazioni `/apps`. Ciò può causare problemi quando il sistema viene aggiornato in qualsiasi modo.

### Use Cases {#use-cases}

Questi, insieme alle funzionalità standard, consentono di:

* **Aggiunta di una proprietà**

   La proprietà non esiste nella `/libs` definizione, ma è obbligatoria nella `/apps` sovrapposizione o nella sostituzione.

   1. Crea il nodo corrispondente all&#39;interno `/apps`
   1. Crea la nuova proprietà su questo nodo &quot;

* **Ridefinire una proprietà (proprietà non create automaticamente)**

   La proprietà è definita in `/libs`, ma è necessario un nuovo valore nella `/apps` sovrapposizione/sostituzione.

   1. Crea il nodo corrispondente all&#39;interno `/apps`
   1. Crea la proprietà corrispondente su questo nodo (sotto / `apps`)

      * La proprietà avrà una priorità in base alla configurazione di Sling Resource Resolver.
      * È supportata la modifica del tipo di proprietà.

         Se si utilizza un tipo di proprietà diverso da quello utilizzato in `/libs`, verrà utilizzato il tipo di proprietà definito.
   >[!NOTE]
   >
   >È supportata la modifica del tipo di proprietà.

* **Ridefinire una proprietà creata automaticamente**

   Per impostazione predefinita, le proprietà create automaticamente (come `jcr:primaryType`) non sono soggette a sovrapposizione/override per garantire che il tipo di nodo attualmente in uso `/libs` sia rispettato. Per imporre una sovrapposizione/sostituzione è necessario ricreare il nodo in `/apps`, nascondere esplicitamente la proprietà e ridefinirla:

   1. Crea il nodo corrispondente sotto `/apps` con quello desiderato `jcr:primaryType`
   1. Creare la proprietà `sling:hideProperties` su tale nodo, con il valore impostato su quello della proprietà creata automaticamente; ad esempio, `jcr:primaryType`

      Questa proprietà, definita in `/apps`, avrà ora priorità rispetto a quella definita in `/libs`

* **Ridefinire un nodo e i relativi elementi secondari**

   Il nodo e i relativi elementi secondari sono definiti in `/libs`, ma è necessaria una nuova configurazione nella `/apps` sovrapposizione/sostituzione.

   1. Combinare le azioni di:

      1. Nascondere gli elementi secondari di un nodo (mantenendo le proprietà del nodo)
      1. Ridefinire proprietà/proprietà

* **Nascondere una proprietà**

   La proprietà è definita in `/libs`, ma non è necessaria nella `/apps` sovrapposizione/sostituzione.

   1. Crea il nodo corrispondente all&#39;interno `/apps`
   1. Creare una proprietà `sling:hideProperties` di tipo `String` o `String[]`. Utilizzate questa opzione per specificare le proprietà da nascondere o ignorare. È inoltre possibile utilizzare i caratteri jolly. Ad esempio:

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **Nascondere un nodo e i relativi elementi secondari**

   Il nodo e i relativi elementi secondari sono definiti in `/libs`, ma non sono richiesti nella `/apps` sovrapposizione/sostituzione.

   1. Crea il nodo corrispondente in /apps
   1. Creare una proprietà `sling:hideResource`

      * tipo: `Boolean`
      * valore: `true`

* **Nascondere gli elementi secondari di un nodo (mantenendo le proprietà del nodo)**

   Il nodo, le relative proprietà e i relativi elementi secondari sono definiti in `/libs`. Il nodo e le relative proprietà sono obbligatori nella `/apps` sovrapposizione/sostituzione, ma alcuni o tutti i nodi secondari non sono richiesti nella `/apps` sovrapposizione/sostituzione.

   1. Crea il nodo corrispondente sotto `/apps`
   1. Creare la proprietà `sling:hideChildren`:

      * tipo: `String[]`
      * value: un elenco dei nodi secondari (come definito in `/libs`) da nascondere/ignorare

      Il carattere jolly &amp;ast; può essere utilizzato per nascondere/ignorare tutti i nodi figlio.


* **Riordinare i nodi**

   Il nodo e i relativi elementi di pari livello sono definiti in `/libs`. È necessaria una nuova posizione per ricreare il nodo nella `/apps` sovrapposizione/sostituzione, dove la nuova posizione viene definita in riferimento al nodo di pari livello appropriato in `/libs`.

   * Utilizzare la `sling:orderBefore` proprietà:

      1. Crea il nodo corrispondente sotto `/apps`
      1. Creare la proprietà `sling:orderBefore`:

         Indica il nodo (come in `/libs`) in cui il nodo corrente deve essere posizionato prima:

         * tipo: `String`
         * valore: `<before-SiblingName>`

### Richiamo di Sling Resource Merger dal codice {#invoking-the-sling-resource-merger-from-your-code}

Sling Resource Merger include due provider di risorse personalizzate, uno per le sovrapposizioni e l&#39;altro per le sostituzioni. Ognuno di questi può essere richiamato all&#39;interno del codice utilizzando un punto di montaggio:

>[!NOTE]
>
>Quando accedete alla risorsa, si consiglia di utilizzare il punto di montaggio appropriato.
>
>In questo modo viene richiamato Sling Resource Merger e viene restituita la risorsa completamente unita (riducendo la struttura da cui replicare `/libs`).

* Sovrapposizione:

   * finalità: unire risorse in base al percorso di ricerca
   * punto di montaggio: `/mnt/overlay`
   * usage: `mount point + relative path`
   * esempio:

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* Ignora:

   * finalità: unire le risorse in base al relativo super-type
   * punto di montaggio: `/mnt/overide`
   * usage: `mount point + absolute path`
   * esempio:

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

<!--
### Example of Usage {#example-of-usage}

Some examples are covered:

* Overlay:

    * [Customizing the Consoles](/help/sites-developing/customizing-consoles-touch.md)
    * [Customizing Page Authoring](/help/sites-developing/customizing-page-authoring-touch.md)

* Override:

    * [Configuring your Page Properties](/help/sites-developing/page-properties-views.md#configuring-your-page-properties)
-->
