---
title: Selettore risorse per [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]
description: Esempi per personalizzare il selettore risorse in base alle esigenze.
role: Admin, User
exl-id: 7a393a96-f2a2-4a25-922c-577271cafc57
source-git-commit: 9c1104f449dc2ec625926925ef8c95976f1faf3d
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 54%

---


# Esempi per utilizzare le proprietà del Selettore risorse {#usage-examples}

Puoi definire il selettore risorse [proprietà](/help/assets/asset-selector-properties.md) nel file **index.html** per personalizzare la visualizzazione del selettore risorse all&#39;interno dell&#39;applicazione.

## Esempio 1: Selettore risorse nella visualizzazione della barra

![rail-view-example](assets/rail-view-example-vanilla.png)

Se il valore di AssetSelector `rail` è impostato su `false` o non è menzionato nelle proprietà, per impostazione predefinita Asset Selector viene visualizzato nella visualizzazione modale. La proprietà `acvConfig` consente alcune configurazioni approfondite, come il trascinamento della selezione. Visita [abilita o disabilita il trascinamento della selezione](asset-selector-customization.md#enable-disable-drag-and-drop) per informazioni sull&#39;utilizzo della proprietà `acvConfig`.

<!--
### Example 2: Use selectedAssets property in addition to the path property

Use the `path` property to define the folder name that displays automatically when the Asset Selector is rendered. In addition, use the `selectedAssets` property to define the IDs for the assets that you need to select within the folder. Moreover, when you want to display assets that are pre-defined within the folder, you can use selectedAssets property.

   ![selected-assets-example](assets/selected-assets-example-vanilla.png)
-->

## Esempio 2: finestra popover dei metadati

Utilizza varie proprietà per definire i metadati di una risorsa da visualizzare mediante un’icona Info. La finestra popover Iinfo fornisce un insieme di informazioni sulla risorsa o sulla cartella, tra cui titolo, dimensioni, data di modifica, posizione e descrizione di una risorsa. Nell’esempio seguente, per visualizzare i metadati di una risorsa vengono utilizzate diverse proprietà, ad esempio: proprietà `repo:path` che specifica la posizione di una risorsa. <!--`repo` represents the repository from where the asset is showing, whereas, `path` represents the route from where the asset or folder is rendered.-->

![metadata-popover-example](assets/metadata-popover.png)

## Esempio 3: proprietà filtro personalizzata nella visualizzazione della barra

Oltre alla ricerca con facet, Assets Selector consente di personalizzare vari attributi per perfezionare la ricerca da [!DNL Adobe Experience Manager] come applicazione [!DNL Cloud Service]. Aggiungi il seguente codice per aggiungere filtri di ricerca personalizzati nell’applicazione. Nell’esempio seguente, la ricerca `Type Filter` che identifica il tipo di risorsa tra Immagini, Documenti o Video o il tipo di filtro aggiunto per la ricerca.

![custom-filter-example-vanilla](assets/custom-filter-example-vanilla.png)

<!--

## Customization after integrating Asset Selector 

### Custom metadata

Assets display panel shows the out of the box metadata that can be displayed in the info of the asset. In addition to this, [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] application allows configuration of the asset selector by adding custom metadata that is shown in info panel of the asset.
-->


>[!MORELIKETHIS]
>
>* [Personalizzazioni del Selettore risorse](/help/assets/asset-selector-customization.md)
>* [Caricamento selettore risorse](/help/assets/asset-selector-upload.md)
>* [Proprietà del Selettore risorse](/help/assets/asset-selector-properties.md)
>* [Integrare il Selettore risorse con Dynamic Media con funzionalità OpenAPI](/help/assets/integrate-asset-selector-dynamic-media-open-api.md)
