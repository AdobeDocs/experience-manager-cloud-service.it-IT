---
title: Personalizzazione delle visualizzazioni delle proprietà pagina
description: Scopri come le proprietà della pagina vengono visualizzate e modificate dagli autori.
exl-id: 363b3c2d-f965-485f-bdae-2ea5b4cecb83
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 3%

---

# Personalizzazione delle visualizzazioni delle proprietà pagina{#customizing-views-of-page-properties}

Ogni pagina ha un set di [proprietà](/help/sites-cloud/authoring/sites-console/page-properties.md) che possono essere visualizzate e modificate dagli utenti. Alcune sono necessarie durante la creazione della pagina (crea visualizzazione), altre possono essere visualizzate e modificate (modifica visualizzazione) in una fase successiva. Queste proprietà di pagina vengono definite e rese disponibili dalla finestra di dialogo (`cq:dialog`) del componente pagina appropriato.

Lo stato predefinito per ogni proprietà di pagina è:

* Nascosto nella visualizzazione di creazione (ad esempio, **Creazione guidata pagina**)

* Disponibile nella visualizzazione di modifica (ad esempio, **Visualizza proprietà**)

I campi devono essere configurati in modo specifico se è necessaria una modifica. Questa operazione viene eseguita utilizzando le proprietà del nodo appropriate:

* Proprietà di pagina da rendere disponibile nella visualizzazione di creazione (ad esempio, **Creazione guidata pagina**):

   * Nome: `cq:showOnCreate`
   * Tipo: `Boolean`

* Proprietà di pagina da rendere disponibile nella visualizzazione di modifica, ad esempio l&#39;opzione **Visualizza**/**Modifica** **Proprietà**:

   * Nome: `cq:hideOnEdit`
   * Tipo: `Boolean`

>[!TIP]
>
>Per una guida alla personalizzazione delle proprietà di pagina, consulta il [tutorial Estensione delle proprietà di pagina](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html).

## Configurazione delle proprietà della pagina {#configuring-your-page-properties}

Puoi anche configurare i campi disponibili configurando la finestra di dialogo del componente Pagina e applicando le proprietà del nodo appropriate.

Per impostazione predefinita, ad esempio, la procedura guidata [**Crea pagina**](/help/sites-cloud/authoring/sites-console/creating-pages.md#creating-a-new-page) mostra i campi raggruppati in **Altri titoli e descrizioni**. Per nasconderli, configura:

1. Crea il componente Pagina in `/apps`.
1. Crea una sostituzione (utilizzando *dialog diff* fornito da [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md)) per la sezione `basic` del componente pagina, ad esempio:

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

1. Impostare la proprietà `path` su `basic` per puntare all&#39;override della scheda di base (vedere anche il passaggio successivo). Ad esempio:

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. Creare una sostituzione della sezione `basic` - `moretitles` nel percorso corrispondente, ad esempio:

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. Applica la proprietà del nodo appropriata:

   * **Nome**: `cq:showOnCreate`
   * **Tipo**: `Boolean`
   * **Valore**: `false`

   La sezione **Altri titoli e descrizioni** non verrà più visualizzata nella procedura guidata **Crea pagina**.

>[!NOTE]
>
>Durante la configurazione delle proprietà di pagina da utilizzare con Live Copy, vedi [Estensione di Multi Site Manager](/help/implementing/developing/extending/msm.md#configuring-msm-locks-on-page-properties) per ulteriori dettagli.

## Configurazione di esempio delle proprietà di pagina {#sample-configuration-of-page-properties}

In questo esempio viene illustrata la tecnica di dialogo diff di [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md), incluso l&#39;utilizzo di [`sling:orderBefore`](/help/implementing/developing/introduction/sling-resource-merger.md#properties). Illustra inoltre l&#39;utilizzo di `cq:showOnCreate` e `cq:hideOnEdit`.

Puoi trovare il codice di questa pagina in [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog).
