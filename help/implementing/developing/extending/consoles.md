---
title: Personalizzazione delle console
description: Scopri le diverse opzioni fornite da AEM per personalizzare le console dell’istanza di authoring.
exl-id: 832f9a86-07c4-4229-a0dc-8ad50a8195b0
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# Personalizzazione delle console {#customizing-consoles}

AEM fornisce opzioni per personalizzare le console (e la funzionalità di [authoring delle pagine](/help/implementing/developing/extending/page-authoring.md)) dell&#39;istanza di authoring.

## Clientlibs {#clientlibs}

Le clientlibs consentono di estendere l’implementazione predefinita per offrire nuove funzionalità, riutilizzando al contempo funzioni, oggetti e metodi standard. Quando si esegue la personalizzazione con clientlibs, è possibile creare la propria clientlib in `/apps.`. Ad esempio, può contenere il codice necessario per il componente personalizzato.

Vedi [Utilizzo delle librerie lato client in AEM as a Cloud Service](/help/implementing/developing/introduction/clientlibs.md).

## Sovrapposizioni {#overlays}

Le sovrapposizioni si basano sulle definizioni dei nodi e consentono di sovrapporre la funzionalità standard disponibile in `/libs` con la funzionalità personalizzata in `/apps`. Durante la creazione di una sovrapposizione, non è necessaria una copia 1:1 dell&#39;originale, in quanto [Sling resource merger](/help/implementing/developing/introduction/sling-resource-merger.md) consente l&#39;ereditarietà.

Le sovrapposizioni possono essere utilizzate in molti modi per estendere le console AEM. Nelle sezioni seguenti vengono forniti diversi esempi.

Vedi anche [Sovrapposizioni per Adobe Experience Manager as a Cloud Service](/help/implementing/developing/introduction/overlays.md).

>[!TIP]
>
>Se ti interessano le opzioni per personalizzare l&#39;esperienza di authoring, consulta [Personalizzazione dell&#39;authoring delle pagine](/help/implementing/developing/extending/page-authoring.md).

## Personalizzazione della vista predefinita per una console {#customizing-the-default-view-for-a-console}

Puoi personalizzare la vista predefinita (colonna, scheda, elenco) per una console:

* È possibile riordinare le viste sovrapponendo la voce richiesta in:

   * `/libs/wcm/core/content/sites/jcr:content/views`

   * La prima voce è quella predefinita.

   * I nodi disponibili sono correlati alle opzioni di visualizzazione disponibili:

      * `column`
      * `card`
      * `list`

* Ad esempio, in una sovrapposizione per un elenco:

   * `/apps/wcm/core/content/sites/jcr:content/views/list`

   * Definisci la seguente proprietà:

      * **Nome**: `sling:orderBefore`
      * **Tipo**: `String`
      * **Valore**: `column`

### Aggiungere una nuova azione alla barra degli strumenti {#add-a-new-action-to-the-toolbar}

Puoi creare componenti personalizzati e includere le librerie client corrispondenti per le azioni personalizzate.

* Ad esempio, potrebbe essere utile creare un&#39;azione **Promuovi a social media** in:

   * `/apps/wcm/core/clientlibs/sites/js/socialmedia.js`

   * Questa può quindi essere collegata a un elemento della barra degli strumenti nella console:

   * `/apps/<yourProject>/admin/ext/launches`

   * Ad esempio, in modalità di selezione:

   * `content/jcr:content/body/content/header/items/selection/items/socialmedia`

### Limitare un&#39;azione della barra degli strumenti a un gruppo specifico {#restrict-a-toolbar-action-to-a-specific-group}

Puoi utilizzare una condizione di rendering personalizzata per sovrapporre l’azione standard e imporre condizioni specifiche che devono essere soddisfatte prima che venga eseguito il rendering.

Ad esempio, potrebbe essere utile creare un componente per controllare le condizioni di rendering in base a un gruppo:

* `/apps/myapp/components/renderconditions/group`

Per applicare questi elementi all&#39;azione **Crea sito** nella console Sites:

* `/libs/wcm/core/content/sites`

1. Crea la sovrapposizione:

   * `/apps/wcm/core/content/sites`

1. Quindi aggiungi la condizione di rendering per l’azione:

   * `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

Utilizzando le proprietà in questo nodo è possibile definire il `groups` consentito per eseguire l&#39;azione specifica, ad esempio `administrators`

### Personalizzazione delle colonne nella vista a elenco {#customizing-columns-in-list-view}

Per personalizzare le colonne nella vista a elenco:

1. Sovrapponi l’elenco delle colonne disponibili.

   * Sul nodo:

     `/apps/wcm/core/content/common/availablecolumns`

1. Aggiungi le nuove colonne o rimuovi quelle esistenti.

Per inserire dati aggiuntivi, è necessario scrivere un [PageInfoProvider](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageInfoProvider.html) con una proprietà `pageInfoProviderType`.

>[!NOTE]
>
>Questa funzione è ottimizzata per le colonne di campi di testo. Per altri tipi di dati è possibile sovrapporre `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` in `/apps`.

### Filtrare le risorse {#filtering-resources}

Quando utilizzi una console, un utente deve spesso selezionare tra risorse quali pagine, componenti o risorse. Può assumere la forma di un elenco dal quale l’autore deve scegliere un elemento.

Per mantenere l’elenco a una dimensione ragionevole e pertinente al caso d’uso, un filtro può essere implementato sotto forma di predicato personalizzato. Per ulteriori informazioni, vedere [Personalizzazione dell&#39;authoring delle pagine](/help/implementing/developing/extending/page-authoring.md#filtering-resources).
