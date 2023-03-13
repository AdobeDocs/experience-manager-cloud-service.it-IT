---
title: Utilizzo di Sling Resource Merger in Adobe Experience Manager as a Cloud Service
description: Sling Resource Merger fornisce servizi per accedere e unire le risorse
exl-id: 5b6e5cb5-4c6c-4246-ba67-6b9f752867f5
source-git-commit: ac760e782f80ee82a9b0604ef64721405fc44ee4
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 2%

---

# Utilizzo di Sling Resource Merger in AEM as a Cloud Service {#using-the-sling-resource-merger-in-aem}

## Scopo {#purpose}

Sling Resource Merger fornisce servizi per accedere e unire le risorse. Fornisce meccanismi di differenze per entrambi:

* **[Sovrapposizioni](/help/implementing/developing/introduction/overlays.md)** delle risorse utilizzando [percorsi di ricerca](/help/implementing/developing/introduction/overlays.md#search-paths).

* **Sostituzioni** delle finestre di dialogo dei componenti per l’interfaccia touch (`cq:dialog`), utilizzando la gerarchia dei tipi di risorsa (tramite la proprietà `sling:resourceSuperType`).

Con Sling Resource Merger, le risorse e/o le proprietà di sovrapposizione/sostituzione vengono unite alle risorse/proprietà originali:

* Il contenuto della definizione personalizzata ha una priorità più alta rispetto a quella dell’originale (cioè *sovrapposizioni* o *sostituzioni* it).

* Se necessario, [proprietà](#properties) definito nella personalizzazione, indica come deve essere utilizzato il contenuto unito dall’originale.

>[!CAUTION]
>
>Sling Resource Merger e i metodi correlati possono essere utilizzati solo con l’interfaccia touch (l’unica disponibile per gli as a Cloud Service AEM).

### Obiettivi per l&#39;AEM {#goals-for-aem}

Gli obiettivi per utilizzare Sling Resource Merger in AEM sono i seguenti:

* assicurati che non vengano apportate modifiche di personalizzazione in `/libs`.
* ridurre la struttura da cui viene replicata `/libs`.

   Quando si utilizza Sling Resource Merger, non è consigliabile copiare l’intera struttura da `/libs` in quanto ciò comporterebbe la memorizzazione di troppe informazioni nella personalizzazione (in genere `/apps`). La duplicazione delle informazioni aumenta inutilmente la possibilità di problemi quando il sistema viene aggiornato in qualsiasi modo.

>[!CAUTION]
>
>Tu ***deve*** non modificare nulla in `/libs` percorso.
>
>Questo perché il contenuto di `/libs` può essere sovrascritto quando vengono applicati aggiornamenti all’istanza.
>
>* Le sovrapposizioni dipendono da [percorsi di ricerca](/help/implementing/developing/introduction/overlays.md#search-paths).
>
>* Le sostituzioni non dipendono dai percorsi di ricerca, utilizzano la proprietà `sling:resourceSuperType` per effettuare la connessione.
>
>Tuttavia, le sostituzioni sono spesso definite in `/apps`, come best practice in AEM as a Cloud Service è di definire le personalizzazioni in `/apps`; questo perché non è necessario modificare nulla in `/libs`.

### Proprietà {#properties}

La fusione delle risorse fornisce le seguenti proprietà:

* `sling:hideProperties` ( `String` oppure `String[]`)

   Specifica la proprietà o l&#39;elenco di proprietà da nascondere.

   Il carattere jolly `*` nasconde tutto.

* `sling:hideResource` ( `Boolean`)

   Indica se le risorse devono essere completamente nascoste, inclusi i relativi elementi secondari.

* `sling:hideChildren` ( `String` oppure `String[]`)

   Contiene il nodo figlio, o elenco di nodi figlio, da nascondere. Le proprietà del nodo verranno mantenute.

   Il carattere jolly `*` nasconde tutto.

* `sling:orderBefore` ( `String`)

   Contiene il nome del nodo di pari livello che deve essere posizionato davanti al nodo corrente.

Queste proprietà influiscono sul modo in cui le risorse/proprietà originali/corrispondenti (da `/libs`) vengono utilizzati dalla sovrapposizione/esclusione (spesso in `/apps`).

### Creazione della struttura {#creating-the-structure}

Per creare una sovrapposizione o una sostituzione è necessario ricreare il nodo originale, con la struttura equivalente, sotto la destinazione (in genere `/apps`). Esempio:

* Sovrapposizione

   * La definizione della voce di navigazione per la console Sites, come mostrato nella barra, è definita in:

      `/libs/cq/core/content/nav/sites/jcr:title`

   * Per sovrapporsi, crea il seguente nodo:

      `/apps/cq/core/content/nav/sites`

      Quindi aggiorna la proprietà `jcr:title` secondo necessità.

* Sostituisci

   * La definizione della finestra di dialogo touch per la console Testi è definita in:

      `/libs/foundation/components/text/cq:dialog`

   * Per evitare questo problema, crea il seguente nodo, ad esempio:

      `/apps/the-project/components/text/cq:dialog`

Per creare uno di questi elementi è sufficiente ricreare la struttura dell&#39;ossatura. Per semplificare la ricreazione della struttura, tutti i nodi intermedi possono essere di tipo `nt:unstructured` (non devono necessariamente riflettere il tipo di nodo originale; ad esempio, in `/libs`).

Nell’esempio di sovrapposizione precedente, sono necessari i seguenti nodi:

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
>Quando si utilizza Sling Resource Merger (ad esempio quando si tratta dell’interfaccia utente standard touch), non è consigliabile copiare l’intera struttura da `/libs` in quanto comporterebbe la memorizzazione di troppe informazioni `/apps`. Questo può causare problemi quando il sistema viene aggiornato in qualsiasi modo.

### Casi d’uso {#use-cases}

Queste funzionalità, insieme a quelle standard, consentono di:

* **Aggiungi una proprietà**

   La proprietà non esiste in `/libs` ma è richiesto nella sezione `/apps` sovrapposizione/sostituzione.

   1. Crea il nodo corrispondente in `/apps`
   1. Crea la nuova proprietà su questo nodo &quot;

* **Ridefinire una proprietà (proprietà non create automaticamente)**

   La proprietà è definita in `/libs`, ma è necessario un nuovo valore in `/apps` sovrapposizione/sostituzione.

   1. Crea il nodo corrispondente in `/apps`
   1. Crea la proprietà corrispondente su questo nodo (sotto / `apps`)

      * La proprietà avrà una priorità in base alla configurazione di Sling Resource Resolver.
      * È supportata la modifica del tipo di proprietà.

         Se utilizzi un tipo di proprietà diverso da quello utilizzato in `/libs`, verrà utilizzato il tipo di proprietà definito.
   >[!NOTE]
   >
   >È supportata la modifica del tipo di proprietà.

* **Ridefinire una proprietà creata automaticamente**

   Per impostazione predefinita, le proprietà create automaticamente (come `jcr:primaryType`) non sono soggetti a sovrapposizione/esclusione per garantire che il tipo di nodo attualmente in `/libs` è rispettato. Per imporre una sovrapposizione/esclusione è necessario ricreare il nodo in `/apps`, nasconde esplicitamente la proprietà e la ridefinisce:

   1. Crea il nodo corrispondente in `/apps` con il `jcr:primaryType`
   1. Creare la proprietà `sling:hideProperties` su tale nodo, con il valore impostato su quello della proprietà creata automaticamente; ad esempio, `jcr:primaryType`

      Questa proprietà, definita in `/apps`, avrà ora la priorità rispetto a quello definito in `/libs`

* **Ridefinire un nodo e i relativi elementi secondari**

   Il nodo e i relativi elementi secondari sono definiti in `/libs`, ma è necessaria una nuova configurazione in `/apps` sovrapposizione/sostituzione.

   1. Combina le azioni di:

      1. Nascondi elementi figlio di un nodo (mantenendo le proprietà del nodo)
      1. Ridefinisci la/le proprietà

* **Nascondere una proprietà**

   La proprietà è definita in `/libs`, ma non richiesto nella `/apps` sovrapposizione/sostituzione.

   1. Crea il nodo corrispondente in `/apps`
   1. Creare una proprietà `sling:hideProperties` di tipo `String` o `String[]`. Utilizzare questa opzione per specificare le proprietà da nascondere/ignorare. È inoltre possibile utilizzare i caratteri jolly. Esempio:

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **Nascondere un nodo e i relativi elementi figlio**

   Il nodo e i relativi elementi secondari sono definiti in `/libs`, ma non richiesto nella `/apps` sovrapposizione/sostituzione.

   1. Crea il nodo corrispondente in /apps
   1. Creare una proprietà `sling:hideResource`

      * tipo: `Boolean`
      * valore: `true`

* **Nascondi gli elementi secondari di un nodo (mantenendo le proprietà del nodo)**

   Il nodo, le relative proprietà e i relativi elementi secondari sono definiti in `/libs`. Il nodo e le relative proprietà sono necessari nel `/apps` overlay/override, ma alcuni o tutti i nodi secondari non sono necessari nel `/apps` sovrapposizione/sostituzione.

   1. Crea il nodo corrispondente in `/apps`
   1. Creare la proprietà `sling:hideChildren`:

      * tipo: `String[]`
      * value: un elenco dei nodi secondari (come definito in `/libs`) per nascondere/ignorare

      Il carattere jolly &amp;ast; può essere utilizzato per nascondere/ignorare tutti i nodi figlio.


* **Riordina nodi**

   Il nodo e i relativi elementi di pari livello sono definiti in `/libs`. È necessaria una nuova posizione in modo che il nodo venga ricreato in `/apps` overlay/override, in cui la nuova posizione viene definita in riferimento al nodo di pari livello appropriato in `/libs`.

   * Utilizza il `sling:orderBefore` proprietà:

      1. Crea il nodo corrispondente in `/apps`
      1. Creare la proprietà `sling:orderBefore`:

         Specifica il nodo (come in `/libs`) il nodo corrente deve essere posizionato prima di:

         * tipo: `String`
         * valore: `<before-SiblingName>`

### Richiamare Sling Resource Merger dal codice {#invoking-the-sling-resource-merger-from-your-code}

Sling Resource Merger include due provider di risorse personalizzati: uno per le sovrapposizioni e l’altro per le sostituzioni. Ognuna di queste può essere richiamata all’interno del codice utilizzando un punto di montaggio:

>[!NOTE]
>
>Quando si accede alla risorsa, si consiglia di utilizzare il punto di montaggio appropriato.
>
>In questo modo viene richiamato Sling Resource Merger e viene restituita la risorsa completamente unita, riducendo la struttura da cui replicare `/libs`).

* Sovrapposizione:

   * finalità: unire le risorse in base al relativo percorso di ricerca
   * punto di montaggio: `/mnt/overlay`
   * usage: `mount point + relative path`
   * esempio:

      * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* Sostituisci:

   * finalità: unire le risorse in base al loro super tipo
   * punto di montaggio: `/mnt/overide`
   * usage: `mount point + absolute path`
   * esempio:

      * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

