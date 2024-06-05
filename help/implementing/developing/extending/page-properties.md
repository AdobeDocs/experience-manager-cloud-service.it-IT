---
title: Personalizzazione delle visualizzazioni delle proprietà di pagina
description: Scopri come le proprietà della pagina vengono visualizzate e modificate dagli autori.
exl-id: 363b3c2d-f965-485f-bdae-2ea5b4cecb83
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# Personalizzazione delle visualizzazioni delle proprietà di pagina{#customizing-views-of-page-properties}

Ogni pagina ha un set di [proprietà](/help/sites-cloud/authoring/sites-console/page-properties.md) che possono essere visualizzate e modificate dagli utenti. Alcune sono necessarie durante la creazione della pagina (crea visualizzazione), altre possono essere visualizzate e modificate (modifica visualizzazione) in una fase successiva. Queste proprietà di pagina vengono definite e rese disponibili dalla finestra di dialogo (`cq:dialog`) del componente pagina appropriato.

Lo stato predefinito per ogni proprietà di pagina è:

* Nascosto nella vista di creazione (ad esempio, **Crea pagina** procedura guidata)

* Disponibile nella vista di modifica (ad esempio, **Visualizza proprietà**)

I campi devono essere configurati in modo specifico se è necessaria una modifica. Questa operazione viene eseguita utilizzando le proprietà del nodo appropriate:

* Proprietà di pagina da rendere disponibile nella visualizzazione di creazione (ad esempio, **Crea pagina** procedura guidata):

   * Nome: `cq:showOnCreate`
   * Tipo: `Boolean`

* Proprietà di pagina da rendere disponibile nella visualizzazione di modifica, ad esempio **Visualizza**/**Modifica**  **Proprietà** opzione:

   * Nome: `cq:hideOnEdit`
   * Tipo: `Boolean`

>[!TIP]
>
>Consulta la [Tutorial sull’estensione delle proprietà di pagina](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html) guida alla personalizzazione delle proprietà di pagina.

## Configurazione delle proprietà della pagina {#configuring-your-page-properties}

Puoi anche configurare i campi disponibili configurando la finestra di dialogo del componente Pagina e applicando le proprietà del nodo appropriate.

Ad esempio, per impostazione predefinita [**Crea pagina** procedura guidata](/help/sites-cloud/authoring/sites-console/creating-pages.md#creating-a-new-page) mostra i campi raggruppati in **Altri titoli e descrizioni**. Per nasconderli, configura:

1. Creare il componente Pagina in `/apps`.
1. Creare una sostituzione (tramite *finestra di dialogo* fornite da [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md)) per `basic` del componente Pagina, ad esempio:

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

1. Imposta il `path` proprietà su `basic` per puntare alla sostituzione della scheda di base (vedi anche il passaggio successivo). Ad esempio:

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. Creare un override di `basic` - `moretitles` nel percorso corrispondente; ad esempio:

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. Applica la proprietà del nodo appropriata:

   * **Nome**: `cq:showOnCreate`
   * **Tipo**: `Boolean`
   * **Valore**: `false`

   Il **Altri titoli e descrizioni** non verrà più visualizzata nella sezione **Crea pagina** procedura guidata.

>[!NOTE]
>
>Durante la configurazione delle proprietà di pagina da utilizzare con le Live Copy, consulta [Estensione di Multi Site Manager](/help/implementing/developing/extending/msm.md#configuring-msm-locks-on-page-properties) per ulteriori dettagli.

## Configurazione di esempio delle proprietà di pagina {#sample-configuration-of-page-properties}

In questo esempio viene illustrata la tecnica della finestra di dialogo [Sling Resource Merger](/help/implementing/developing/introduction/sling-resource-merger.md) compreso l&#39;uso di [`sling:orderBefore`](/help/implementing/developing/introduction/sling-resource-merger.md#properties). Illustra inoltre l’utilizzo di entrambi `cq:showOnCreate` e `cq:hideOnEdit`.

Puoi trovare il codice di questa pagina su [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog).
