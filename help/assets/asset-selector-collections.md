---
title: Selettore risorse per [!DNL Adobe Experience Manager]  as a  [!DNL Cloud Service]
description: Utilizza il Selettore risorse per cercare, trovare e recuperare i metadati e le rappresentazioni delle risorse all’interno dell’applicazione.
role: Admin,User
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 9%

---


# Raccolte selettore risorse {#asset-selector-collections}

| [Best practice per la ricerca](/help/assets/search-best-practices.md) | [Best practice per i metadati](/help/assets/metadata-best-practices.md) | [Hub di contenuti](/help/assets/product-overview.md) | [Dynamic Medie con funzionalità OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentazione per gli sviluppatori di AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Una raccolta è un insieme di risorse, cartelle o altre raccolte all’interno di Selettore risorse. Puoi utilizzare le raccolte per condividere le risorse tra i vari utenti. A differenza delle cartelle, una raccolta può includere risorse da posizioni diverse.

Le micro raccolte front-end in Asset Selector sono disponibili come funzionalità integrata in modalità di sola lettura. Recupera risorse e raccolte direttamente dall&#39;archivio [!DNL Experience Manager Assets] a cui hai accesso.

>[!NOTE]
>
>Assicurarsi di disporre delle autorizzazioni per accedere a un [!DNL Experience Manager Assets] [imsOrg](/help/assets/asset-selector-properties.md) e alle raccolte.

Le micro raccolte front-end in Asset Selector sono disponibili come funzionalità integrata in modalità di sola lettura. Recupera le risorse e le raccolte direttamente dall’archivio Experience Manager Assets a cui hai accesso ed eredita le proprietà delle cartelle pubbliche e private dall’archivio Experience Manager Assets. Ulteriori informazioni sulla [creazione di una raccolta pubblica o privata nella visualizzazione Assets](/help/assets/manage-collections-assets-view.md#create-collection).

Puoi visualizzare le raccolte in Asset Selector sia nella vista a barra che nella vista modale.

![Raccolte nella visualizzazione della barra](assets/collections-rail-modal-view.png)

<!--
Additionally, you can [customize](/help/assets/asset-selector-customization.md) the `featureSet` property to enable or disable collections in Asset Selector. See [enable or disable Collections tab](#enable-disable-collections-tab).-->

Inoltre, puoi anche personalizzare la selezione delle risorse nella scheda Raccolte. Per eseguire questa operazione, è possibile personalizzarla utilizzando `handleSelection`. Vedere [gestione della selezione di Assets mediante lo schema di oggetti](/help/assets/asset-selector-customization.md#handling-selection).

## Visualizza raccolte {#view-collections}

Il selettore risorse consente di visualizzare le raccolte in una ![vista a elenco](assets/do-not-localize/list-view.png) o in una ![vista a griglia](assets/do-not-localize/grid-view.png). Consulta [tipi di visualizzazione in Asset Selector](overview-asset-selector.md#types-of-view).

## Trascinare le risorse nella raccolta {#collection-drag-and-drop}

È possibile trascinare una risorsa nelle raccolte direttamente dalla vista [!DNL Assets as a Cloud Service] nell&#39;ambiente di authoring. A questo scopo, trascina la risorsa dalla scheda Assets all’area di lavoro Raccolte dell’applicazione Selettore risorse per creare applicazioni avanzate.

>[!NOTE]
>
>* Il trascinamento e il rilascio di una risorsa sono possibili solo nella vista a barra.
>* Puoi trascinare solo i file (risorse) e non le cartelle.

D&#39;altra parte, puoi anche [abilitare o disabilitare direttamente il trascinamento della selezione delle risorse nelle raccolte](asset-selector-customization.md#enable-disable-drag-and-drop).

## Disattiva la selezione delle risorse nelle raccolte {#disable-selection-collection}

La funzione Disattiva selezione viene utilizzata per nascondere o disabilitare la selezione delle risorse o cartelle. La casella di controllo di selezione viene nascosta dalla scheda o dalla risorsa, che ne impedisce la selezione. Vedere [disabilitare la selezione](/help/assets/asset-selector-customization.md#disable-selection).

## Abilitare o disabilitare la scheda Raccolte {#enable-disable-collections-tab}

Asset Selector (Selettore risorse) consente di personalizzare i componenti in base ai requisiti e all’usabilità. Per abilitare o disabilitare la scheda Raccolte in Asset Selector, è possibile utilizzare la proprietà `featureSet` nel modo seguente:

* **Abilita scheda Raccolte:** Per abilitare la scheda Raccolte, è necessario fornire `collections` come valore all&#39;array. Per impostazione predefinita, la scheda Raccolte è attivata per tutti gli utenti. Ad esempio `featureSet:["collections"]`
* **Disabilita scheda Raccolte:** Per disabilitare la scheda Raccolte, è necessario fornire un array vuoto come valore. Ad esempio `featureSet:[ ]`

>[!MORELIKETHIS]
>
>* [Personalizzazioni di Asset Selector](/help/assets/asset-selector-customization.md)
>* [Integrare Asset Selector con varie applicazioni](/help/assets/integrate-asset-selector.md)
>* [Proprietà selettore risorse](/help/assets/asset-selector-properties.md)

