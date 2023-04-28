---
title: Assegnare tag avanzati alle risorse video
description: Experience Manager aggiunge automaticamente tag avanzati contestuali e descrittivi ai video utilizzando [!DNL Adobe Sensei].
feature: Smart Tags,Tagging
role: Admin,User
exl-id: b59043c5-5df3-49a7-b4fc-da34c03649d7
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1213'
ht-degree: 2%

---

# Assegnare tag avanzati alle risorse video {#video-smart-tags}

La crescente necessità di nuovi contenuti richiede sforzi manuali ridotti per offrire esperienze digitali avvincenti in tempo reale. [!DNL Adobe Experience Manager] come [!DNL Cloud Service] supporta l’assegnazione automatica dei tag alle risorse video tramite l’intelligenza artificiale. L’assegnazione di tag ai video manualmente può richiedere molto tempo. Tuttavia, [!DNL Adobe Sensei] la funzione di assegnazione tag avanzati video è dotata di modelli di intelligenza artificiale per analizzare i contenuti video e aggiungere tag alle risorse video. In questo modo, gli utenti DAM possono dedicare più tempo alla distribuzione di esperienze avanzate ai propri clienti. Il servizio di machine learning di Adobe genera due set di tag per un video. Mentre, un set corrisponde a oggetti, scene e attributi in quel video; l&#39;altro insieme riguarda azioni come bere, correre e fare jogging.

L’assegnazione tag video è abilitata per impostazione predefinita in [!DNL Adobe Experience Manager] come [!DNL Cloud Service]. Tuttavia, puoi [rinuncia all’assegnazione tag avanzati video](#opt-out-video-smart-tagging) su una cartella. I video vengono contrassegnati automaticamente quando carichi nuovi video o ne rielabori quelli esistenti. [!DNL Experience Manager] crea inoltre le miniature ed estrae i metadati dei file video. Gli smart tag vengono visualizzati in ordine decrescente [punteggio di affidabilità](#confidence-score-video-tag) nella risorsa [!UICONTROL Proprietà].

## Video con tag avanzati al caricamento {#smart-tag-assets-on-ingestion}

Quando [caricare le risorse video](add-assets.md#upload-assets) a [!DNL Adobe Experience Manager] come [!DNL Cloud Service], i video vengono elaborati. Al termine dell’elaborazione, vedi [!UICONTROL Base] scheda della risorsa [!UICONTROL Proprietà] pagina. I tag avanzati vengono aggiunti automaticamente al video in [!UICONTROL Tag avanzati]. I microservizi per le risorse sfruttano [!DNL Adobe Sensei] per creare questi tag avanzati.

![I tag avanzati vengono aggiunti ai video e visualizzati nella scheda Base delle proprietà della risorsa](assets/smart-tags-added-to-videos.png)

Gli smart tag applicati vengono ordinati in ordine decrescente in base a [punteggio di affidabilità](#confidence-score-video-tag), combinato per i tag oggetto e azione all&#39;interno di [!UICONTROL Tag avanzati].

>[!IMPORTANT]
>
>Si consiglia di esaminare questi tag generati automaticamente per assicurarsi che siano conformi al marchio e ai relativi valori.

## Assegnazione di tag avanzati ai video esistenti in DAM {#smart-tag-existing-videos}

Le risorse video già esistenti in DAM non vengono contrassegnate automaticamente con tag avanzati. Devi [!UICONTROL Rielaborazione delle risorse] per generare manualmente tag avanzati.

Per assegnare tag avanzati alle risorse video o alle cartelle (comprese le sottocartelle) di risorse già esistenti nell’archivio delle risorse, procedi come segue:

1. Seleziona la [!DNL Adobe Experience Manager] , quindi seleziona le risorse dal [!UICONTROL Navigazione] pagina.

1. Seleziona [!UICONTROL File] per visualizzare l’interfaccia Assets.

1. Passa alla cartella alla quale desideri applicare gli smart tag.

1. Seleziona l’intera cartella o le risorse video specifiche.

1. Seleziona ![Icona Rielabora risorse](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL Rielaborazione delle risorse] e seleziona la [!UICONTROL Processo completo] opzione .

<!-- TBD: Limit size -->

![Rielaborazione delle risorse per aggiungere tag ai video dell’archivio DAM esistente](assets/reprocess.gif)

Al termine del processo, passa alla [!UICONTROL Proprietà] di qualsiasi risorsa video all’interno della cartella. I tag aggiunti automaticamente vengono visualizzati in [!UICONTROL Tag avanzati] sezione [!UICONTROL Base] scheda . Questi tag avanzati applicati sono ordinati in ordine decrescente di [punteggio di affidabilità](#confidence-score-video-tag).

## Cercare video con tag {#search-smart-tagged-videos}

Per cercare le risorse video in base agli smart tag generati automaticamente, utilizza [Omnisearch](search-assets.md#search-assets-in-aem):

1. Seleziona l’icona di ricerca ![icona di ricerca](assets/do-not-localize/search_icon.png) per visualizzare il campo Omnisearch .

1. Specifica un tag nel campo Omnisearch che non è stato aggiunto in modo esplicito a un video.

1. Cerca in base al tag .

I risultati della ricerca visualizzano le risorse video in base al tag specificato.

I risultati della ricerca sono una combinazione di risorse video con parole chiave cercate nei metadati e risorse video con tag avanzati con le parole chiave cercate. Tuttavia, i risultati di ricerca che corrispondono a tutti i termini di ricerca nei campi di metadati vengono visualizzati per primi, seguiti dai risultati di ricerca che corrispondono a qualsiasi termine di ricerca negli smart tag. Per ulteriori informazioni, consulta [Comprendere [!DNL Experience Manager] risultati di ricerca con tag avanzati](smart-tags.md#understand-search).

## Tag video moderati {#moderate-video-smart-tags}

[!DNL Adobe Experience Manager] consente di curare gli smart tag in:

* rimuovi i tag imprecisi assegnati ai video del tuo marchio.

* perfeziona le ricerche basate su tag per i video assicurando che il video venga visualizzato nei risultati di ricerca per i tag più rilevanti. Pertanto, elimina le possibilità che i video non correlati vengano visualizzati nei risultati della ricerca.

* assegna un rango più alto a un tag per aumentarne la pertinenza rispetto a un video. La promozione di un tag per un video aumenta le possibilità che il video venga visualizzato nei risultati della ricerca quando viene eseguita una ricerca basata su tale tag.

Per ulteriori informazioni su come moderare gli smart tag per le risorse, consulta [Gestire tag avanzati](smart-tags.md#manage-smart-tags-and-searches).

![Tag video moderati](assets/manage-video-smart-tags.png)

>[!NOTE]
>
>Qualsiasi tag moderato utilizzando i passaggi descritti in [Gestire tag avanzati](smart-tags.md#manage-smart-tags-and-searches) non vengono ricordati al momento della rielaborazione della risorsa. Viene nuovamente visualizzato il set di tag originale.

## Rinuncia all’assegnazione tag avanzati video {#opt-out-video-smart-tagging}

Poiché l’assegnazione tag automatizzata dei video viene eseguita in parallelo ad altre attività di elaborazione delle risorse, come la creazione di miniature e l’estrazione dei metadati, può richiedere molto tempo. Per accelerare l’elaborazione delle risorse, puoi rinunciare all’assegnazione tag avanzati video al caricamento a livello di cartella.

Per rifiutare la generazione automatica di tag avanzati video per le risorse caricate in una cartella specifica:

1. Apri [!UICONTROL Elaborazione delle risorse] scheda nella cartella [!UICONTROL Proprietà].

1. In [!UICONTROL Tag avanzati per video] menu, [!UICONTROL Ereditato] l’opzione è selezionata per impostazione predefinita e lo smart tag video è abilitato.

   Quando il [!UICONTROL Ereditato] selezionata, il percorso della cartella ereditata è visibile insieme alle informazioni relative all&#39;impostazione su [!UICONTROL Abilita] o [!UICONTROL Disattiva].

   ![Disabilita assegnazione tag video avanzati](assets/disable-video-tagging.png)

1. Seleziona [!UICONTROL Disattiva] per rinunciare all’assegnazione tag avanzati dei video caricati nella cartella.

>[!IMPORTANT]
>
>Se hai rinunciato a assegnare tag ai video in una cartella al momento del caricamento e desideri assegnare tag avanzati ai video dopo il caricamento, allora **[!UICONTROL Abilita tag avanzati per video]** da [!UICONTROL Elaborazione delle risorse] scheda della cartella [!UICONTROL Proprietà] e l&#39;uso [[!UICONTROL Rielabora risorsa] opzione](#smart-tag-existing-videos) per aggiungere tag avanzati al video.

## Punteggio di affidabilità {#confidence-score-video-tag}

[!DNL Adobe Experience Manager] applica una soglia minima di affidabilità per gli smart tag oggetto e azione per evitare di avere troppi tag per ogni risorsa video, il che rallenta l’indicizzazione. I risultati della ricerca delle risorse vengono classificati in base ai punteggi di affidabilità, che in genere migliorano i risultati della ricerca oltre a quanto suggerisce un’ispezione dei tag assegnati di qualsiasi risorsa video. I tag errati hanno spesso punteggi di affidabilità bassi, quindi raramente compaiono nella parte superiore dell’elenco dei tag avanzati per le risorse.

La soglia predefinita per i tag azione e oggetto in [!DNL Adobe Experience Manager] è 0,7 (deve essere un valore compreso tra 0 e 1). Se alcune risorse video non sono contrassegnate da un tag specifico, significa che l’algoritmo è meno del 70% sicuro dei tag previsti. La soglia predefinita potrebbe non essere sempre ottimale per tutti gli utenti. È quindi possibile modificare il valore del punteggio di affidabilità nella configurazione OSGI.

Per aggiungere il punteggio di affidabilità alla configurazione OSGI al progetto distribuito in [!DNL Adobe Experience Manager] come [!DNL Cloud Service] attraverso [!DNL Cloud Manager]:

* In [!DNL Adobe Experience Manager] progetto (`ui.config` da Archetype 24, o `ui.apps`) `config.author` Configurazione OSGi, includere un file di configurazione denominato `com.adobe.cq.assetcompute.impl.senseisdk.SenseiSdkImpl.cfg.json` con i seguenti contenuti:

```json
{
  "minVideoActionConfidenceScore":0.5,
  "minVideoObjectConfidenceScore":0.5,
}
```

>[!NOTE]
>
>Ai tag manuali viene assegnata un’affidabilità del 100% (massima affidabilità). Pertanto, se sono presenti risorse video con tag manuali corrispondenti alla query di ricerca, queste vengono visualizzate prima di tag avanzati corrispondenti alla query di ricerca.

## Limitazioni {#video-smart-tagging-limitations}

* Non puoi addestrare il servizio che applica tag avanzati ai video utilizzando uno specifico video. Funziona con il valore predefinito [!DNL Adobe Sensei] impostazioni.

* L’avanzamento dei tag non viene visualizzato.

* Solo i video di dimensioni inferiori a 300 MB nelle dimensioni del file sono con tag automatici. La [!DNL Adobe Sensei] Il servizio ignora i file video di dimensioni maggiori.

* Solo i video nei formati di file e nei codec supportati menzionati in [Tag avanzati](/help/assets/smart-tags.md#smart-tags-supported-file-formats) sono taggati.

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cercare risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi di metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco di metadati](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* [Gestione di tag avanzati e ricerche delle risorse](smart-tags.md#manage-smart-tags-and-searches)
>* [Addestra il servizio di tag avanzati e assegna tag alle tue immagini](smart-tags.md)

