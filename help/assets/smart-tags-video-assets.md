---
title: Assegnare tag avanzati alle risorse video
description: Experience Manager aggiunge automaticamente tag avanzati contestuali e descrittivi ai video utilizzando [!DNL Adobe Sensei].
feature: Tag avanzati, assegnazione tag
role: Amministratore, Business Practices
translation-type: tm+mt
source-git-commit: 8093f6cec446223af58515fd8c91afa5940f9402
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 0%

---


# Assegnare tag avanzati alle risorse video {#video-smart-tags}

La crescente necessità di nuovi contenuti richiede sforzi manuali ridotti per offrire esperienze digitali avvincenti in tempo reale. [!DNL Adobe Experience Manager] as a  [!DNL Cloud Service] supporta l’assegnazione automatica dei tag alle risorse video tramite l’intelligenza artificiale. L’assegnazione di tag ai video manualmente può richiedere molto tempo. Tuttavia, la funzione di assegnazione tag avanzati video basata su [!DNL Adobe Sensei] utilizza modelli di intelligenza artificiale per analizzare i contenuti video e aggiungere tag alle risorse video. In questo modo, gli utenti DAM possono dedicare più tempo alla distribuzione di esperienze avanzate ai propri clienti. Il servizio di machine learning di Adobe genera due set di tag per un video. Mentre, un set corrisponde a oggetti, scene e attributi in quel video; l&#39;altro insieme riguarda azioni come bere, correre e fare jogging.

L’assegnazione tag video è abilitata per impostazione predefinita in [!DNL Adobe Experience Manager] come [!DNL Cloud Service]. Tuttavia, puoi [rinunciare all’assegnazione tag avanzati video](#opt-out-video-smart-tagging) in una cartella. I video vengono contrassegnati automaticamente quando carichi nuovi video o ne rielabori quelli esistenti. [!DNL Experience Manager] crea inoltre le miniature ed estrae i metadati dei file video. Gli smart tag vengono visualizzati in ordine decrescente in base al loro [punteggio di affidabilità](#confidence-score-video-tag) nella risorsa [!UICONTROL Proprietà].

## Video con tag avanzati al caricamento {#smart-tag-assets-on-ingestion}

Quando [carichi risorse video](add-assets.md#upload-assets) in [!DNL Adobe Experience Manager] come [!DNL Cloud Service], i video vengono elaborati. Al termine dell’elaborazione, consulta la scheda [!UICONTROL Base] della pagina della risorsa [!UICONTROL Proprietà] . I tag avanzati vengono aggiunti automaticamente al video in [!UICONTROL Tag avanzati]. I microservizi per le risorse sfruttano [!DNL Adobe Sensei] per creare questi tag avanzati.

![I tag avanzati vengono aggiunti ai video e visualizzati nella scheda Base delle proprietà della risorsa](assets/smart-tags-added-to-videos.png)

Gli smart tag applicati sono ordinati in ordine decrescente in [punteggio di affidabilità](#confidence-score-video-tag), combinati per i tag oggetto e azione, all&#39;interno di [!UICONTROL Tag avanzati].

>[!IMPORTANT]
>
>Si consiglia di esaminare questi tag generati automaticamente per assicurarsi che siano conformi al marchio e ai relativi valori.

## Assegnazione di tag avanzati ai video esistenti in DAM {#smart-tag-existing-videos}

Le risorse video già esistenti in DAM non vengono contrassegnate automaticamente con tag avanzati. Devi [!UICONTROL rielaborare manualmente le risorse] per generare tag avanzati per tali risorse.

Per assegnare tag avanzati alle risorse video o alle cartelle (comprese le sottocartelle) di risorse già esistenti nell’archivio delle risorse, procedi come segue:

1. Seleziona il logo [!DNL Adobe Experience Manager], quindi seleziona le risorse dalla pagina [!UICONTROL Navigazione].

1. Seleziona [!UICONTROL File] per visualizzare l’interfaccia Assets.

1. Passa alla cartella alla quale desideri applicare gli smart tag.

1. Seleziona l’intera cartella o le risorse video specifiche.

1. Seleziona l&#39;icona ![Rielabora risorse](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL Rielabora risorse] e seleziona l&#39;opzione [!UICONTROL Processo completo].

<!-- TBD: Limit size -->

![Rielaborazione delle risorse per aggiungere tag ai video dell’archivio DAM esistente](assets/reprocess.gif)

Al termine del processo, passa alla pagina [!UICONTROL Proprietà] di qualsiasi risorsa video all’interno della cartella. I tag aggiunti automaticamente vengono visualizzati nella sezione [!UICONTROL Tag avanzati] della scheda [!UICONTROL Base] . Questi tag avanzati applicati sono ordinati in ordine decrescente in [punteggio di affidabilità](#confidence-score-video-tag).

## Cerca video con tag {#search-smart-tagged-videos}

Per cercare le risorse video in base agli smart tag generati automaticamente, utilizza [Omnisearch](search-assets.md#search-assets-in-aem):

1. Seleziona l’icona di ricerca ![icona di ricerca](assets/do-not-localize/search_icon.png) per visualizzare il campo Omnisearch.

1. Specifica un tag nel campo Omnisearch che non è stato aggiunto in modo esplicito a un video.

1. Cerca in base al tag .

I risultati della ricerca visualizzano le risorse video in base al tag specificato.

I risultati della ricerca sono una combinazione di risorse video con parole chiave cercate nei metadati e risorse video con tag avanzati con le parole chiave cercate. Tuttavia, i risultati di ricerca che corrispondono a tutti i termini di ricerca nei campi di metadati vengono visualizzati per primi, seguiti dai risultati di ricerca che corrispondono a qualsiasi termine di ricerca negli smart tag. Per ulteriori informazioni, consulta [Comprendere [!DNL Experience Manager] i risultati della ricerca con tag avanzati](smart-tags.md#understandsearch).

## Tag video avanzati moderati {#moderate-video-smart-tags}

[!DNL Adobe Experience Manager] consente di curare gli smart tag in:

* rimuovi i tag imprecisi assegnati ai video del tuo marchio.

* perfeziona le ricerche basate su tag per i video assicurando che il video venga visualizzato nei risultati di ricerca per i tag più rilevanti. Pertanto, elimina le possibilità che i video non correlati vengano visualizzati nei risultati della ricerca.

* assegna un rango più alto a un tag per aumentarne la pertinenza rispetto a un video. La promozione di un tag per un video aumenta le possibilità che il video venga visualizzato nei risultati della ricerca quando viene eseguita una ricerca basata su tale tag.

Per ulteriori informazioni su come moderare gli smart tag per le risorse, consulta [Gestire gli smart tag](smart-tags.md#manage-smart-tags-and-searches).

![Tag video moderati](assets/manage-video-smart-tags.png)

>[!NOTE]
>
>Eventuali tag sottoposti a moderazione tramite i passaggi descritti in [Gestione tag avanzati](smart-tags.md#manage-smart-tags-and-searches) non vengono ricordati durante la rielaborazione della risorsa. Viene nuovamente visualizzato il set di tag originale.

## Rinuncia all’assegnazione tag avanzati video {#opt-out-video-smart-tagging}

Poiché l’assegnazione tag automatizzata dei video viene eseguita in parallelo ad altre attività di elaborazione delle risorse, come la creazione di miniature e l’estrazione dei metadati, può richiedere molto tempo. Per accelerare l’elaborazione delle risorse, puoi rinunciare all’assegnazione tag avanzati video al caricamento a livello di cartella.

Per rifiutare la generazione automatica di tag avanzati video per le risorse caricate in una cartella specifica:

1. Apri la scheda [!UICONTROL Elaborazione risorse] nella cartella [!UICONTROL Proprietà].

1. Nel menu [!UICONTROL Tag avanzati per video], l’opzione [!UICONTROL Ereditato] è selezionata per impostazione predefinita e lo smart tag video è attivato.

   Quando l&#39;opzione [!UICONTROL Ereditato] è selezionata, anche il percorso della cartella ereditato è visibile insieme alle informazioni se è impostato su [!UICONTROL Abilita] o [!UICONTROL Disabilita].

   ![Disabilita assegnazione tag video avanzati](assets/disable-video-tagging.png)

1. Seleziona [!UICONTROL Disabilita] per rinunciare all’assegnazione tag avanzati ai video caricati nella cartella.

>[!IMPORTANT]
>
>Se hai rinunciato a assegnare tag ai video in una cartella al momento del caricamento e desideri assegnare tag avanzati ai video dopo il caricamento, seleziona l’opzione **[!UICONTROL Abilita tag avanzati per video]** dalla scheda [!UICONTROL Elaborazione risorse] della cartella [!UICONTROL Proprietà] e utilizza l’opzione [[!UICONTROL Rielabora risorsa]](#smart-tag-existing-videos) per aggiungere tag avanzati il video.

## Punteggio di affidabilità {#confidence-score-video-tag}

[!DNL Adobe Experience Manager] applica una soglia minima di affidabilità per gli smart tag oggetto e azione per evitare di avere troppi tag per ogni risorsa video, il che rallenta l’indicizzazione. I risultati della ricerca delle risorse vengono classificati in base ai punteggi di affidabilità, che in genere migliorano i risultati della ricerca oltre a quanto suggerisce un’ispezione dei tag assegnati di qualsiasi risorsa video. I tag errati hanno spesso punteggi di affidabilità bassi, quindi raramente compaiono nella parte superiore dell’elenco dei tag avanzati per le risorse.

La soglia predefinita per i tag azione e oggetto in [!DNL Adobe Experience Manager] è 0,7 (deve essere un valore compreso tra 0 e 1). Se alcune risorse video non sono contrassegnate da un tag specifico, significa che l’algoritmo è meno del 70% sicuro dei tag previsti. La soglia predefinita potrebbe non essere sempre ottimale per tutti gli utenti. È quindi possibile modificare il valore del punteggio di affidabilità nella configurazione OSGI.

Per aggiungere la configurazione OSGI del punteggio di affidabilità al progetto distribuito in [!DNL Adobe Experience Manager] come [!DNL Cloud Service] fino a [!DNL Cloud Manager]:

* Nel progetto [!DNL Adobe Experience Manager] (`ui.config` da Archetype 24 o in precedenza `ui.apps`) la configurazione `config.author` OSGi, includi un file di configurazione denominato `com.adobe.cq.assetcompute.impl.senseisdk.SenseiSdkImpl.cfg.json` con il seguente contenuto:

```json
{
  "minVideoActionConfidenceScore":0.5,
  "minVideoObjectConfidenceScore":0.5,
}
```

>[!NOTE]
>
>Ai tag manuali viene assegnata un’affidabilità del 100% (massima affidabilità). Pertanto, se sono presenti risorse video con tag manuali corrispondenti alla query di ricerca, queste vengono visualizzate prima di tag avanzati corrispondenti alla query di ricerca.

## Limitazioni  {#video-smart-tagging-limitations}

* Non puoi addestrare il servizio che applica tag avanzati ai video utilizzando uno specifico video. Funziona con le impostazioni [!DNL Adobe Sensei] predefinite.

* L’avanzamento dei tag non viene visualizzato.

* Solo i video di dimensioni inferiori a 300 MB nelle dimensioni del file sono con tag automatici. Il servizio [!DNL Adobe Sensei] ignora i file video di dimensioni maggiori.

* Solo i video nei formati di file e nei codec supportati menzionati in [Tag avanzati](/help/assets/smart-tags.md#smart-tags-supported-file-formats) sono taggati.

>[!MORELIKETHIS]
>
>* [Gestione di tag avanzati e ricerche delle risorse](smart-tags.md#manage-smart-tags-and-searches)
>* [Addestra il servizio di tag avanzati e assegna tag alle tue immagini](smart-tags.md)

