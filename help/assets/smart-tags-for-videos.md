---
title: Assegnare tag avanzati alle risorse video
description: Experience Manager aggiunge automaticamente tag avanzati contestuali e descrittivi ai video utilizzando  [!DNL Adobe AI].
feature: Smart Tags,Tagging
role: Admin,User
exl-id: 87d0eea2-83a1-4cfa-a4a5-425d0e8abba6
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 0%

---

# Assegnare tag avanzati alle risorse video {#video-smart-tags}

La crescente necessità di nuovi contenuti richiede uno sforzo manuale ridotto per offrire esperienze digitali coinvolgenti in tempi brevi. [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] supporta l&#39;assegnazione tag automatici alle risorse video tramite l&#39;intelligenza artificiale. Assegnare tag ai video manualmente può richiedere tempo. Tuttavia, la funzionalità di assegnazione tag avanzati video basata su [!DNL Adobe AI] utilizza modelli di intelligenza artificiale per analizzare i contenuti video e aggiungere tag alle risorse video. In questo modo gli utenti DAM hanno meno tempo per fornire esperienze avanzate ai propri clienti. Il servizio di apprendimento automatico di Adobe genera due set di tag per un video. Mentre, un set corrisponde a oggetti, scene e attributi in quel video; l&#39;altro set è relativo ad azioni come bere, correre e fare jogging.

L&#39;assegnazione tag video è attivata per impostazione predefinita in [!DNL Adobe Experience Manager] come [!DNL Cloud Service]. Tuttavia, puoi [rinunciare all&#39;assegnazione di tag avanzati video](#opt-out-video-smart-tagging) in una cartella. I video vengono contrassegnati automaticamente quando carichi nuovi video o li rielabora. [!DNL Experience Manager] crea anche le miniature ed estrae i metadati dei file video. Gli smart tag vengono visualizzati in ordine decrescente del relativo [punteggio di affidabilità](#confidence-score-video-tag) nella risorsa [!UICONTROL Proprietà].

## Applicazione di tag avanzati ai video al caricamento {#smart-tag-assets-on-ingestion}

Quando [carichi risorse video](add-assets.md#upload-assets) in [!DNL Adobe Experience Manager] come [!DNL Cloud Service], i video vengono elaborati. Al termine dell&#39;elaborazione, vedere la scheda [!UICONTROL Base] della risorsa [!UICONTROL Proprietà]. Gli smart tag vengono aggiunti automaticamente al video in [!UICONTROL Smart tag]. I microservizi per le risorse sfruttano [!DNL Adobe AI] per creare questi tag avanzati.

![I tag avanzati vengono aggiunti ai video e visualizzati nella scheda Base delle Proprietà della risorsa](assets/smart-tags-added-to-videos.png)

Gli smart tag applicati vengono ordinati in ordine decrescente di [punteggio di affidabilità](#confidence-score-video-tag), combinati per i tag oggetto e azione, all&#39;interno di [!UICONTROL Smart tag].

>[!IMPORTANT]
>
>Ti consigliamo di rivedere questi tag generati automaticamente per assicurarti che siano conformi al tuo marchio e ai suoi valori.

## Applicazione di tag avanzati ai video esistenti in DAM {#smart-tag-existing-videos}

Le risorse video esistenti in DAM non vengono contrassegnate automaticamente con tag avanzati. È necessario [!UICONTROL Rielaborare Assets] manualmente per generare tag avanzati.

Per assegnare tag avanzati alle risorse video o alle cartelle (comprese le sottocartelle) di risorse già esistenti nell’archivio delle risorse, effettua le seguenti operazioni:

1. Seleziona il logo [!DNL Adobe Experience Manager], quindi seleziona le risorse dalla pagina [!UICONTROL Navigazione].

1. Seleziona [!UICONTROL File] per visualizzare l&#39;interfaccia di Assets.

1. Passare alla cartella alla quale si desidera applicare gli smart tag.

1. Seleziona l’intera cartella o specifiche risorse video.

1. Seleziona ![Icona Rielabora risorse](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL Icona Rielabora Assets] e seleziona l&#39;opzione [!UICONTROL Elabora completamente].

<!-- TBD: Limit size -->

![Rielabora risorse per aggiungere tag ai video dell&#39;archivio DAM esistente](assets/reprocess.gif)

Al termine del processo, passa alla pagina [!UICONTROL Proprietà] di qualsiasi risorsa video all&#39;interno della cartella. I tag aggiunti automaticamente sono visualizzati nella sezione [!UICONTROL Tag avanzati] della scheda [!UICONTROL Base]. Questi smart tag applicati sono ordinati in ordine decrescente di [punteggio di affidabilità](#confidence-score-video-tag).

## Cerca video con tag {#search-smart-tagged-videos}

Per cercare le risorse video in base agli smart tag generati automaticamente, utilizza [Omnisearch](search-assets.md#search-assets-in-aem):

1. Seleziona l&#39;icona di ricerca ![icona di ricerca](assets/do-not-localize/search_icon.png) per visualizzare il campo Omnisearch.

1. Specifica un tag, nel campo Omnisearch, che non è stato aggiunto in modo esplicito a un video.

1. Cerca in base al tag.

I risultati della ricerca mostrano le risorse video in base al tag specificato.

I risultati della ricerca sono una combinazione di risorse video con parole chiave cercate nei metadati e risorse video con tag avanzati con le parole chiave cercate. Tuttavia, i risultati della ricerca che corrispondono a tutti i termini di ricerca nei campi di metadati vengono visualizzati per primi, seguiti dai risultati della ricerca che corrispondono a qualsiasi termine di ricerca nei tag avanzati. Per ulteriori informazioni, consulta [Comprendere [!DNL Experience Manager] i risultati della ricerca con smart tag](smart-tags.md#understand-search).

## Modera tag avanzati video {#moderate-video-smart-tags}

[!DNL Adobe Experience Manager] consente di curare gli smart tag per:

* rimuovi i tag inesatti assegnati ai video del tuo marchio.

* perfeziona le ricerche di video basate su tag garantendo che il video venga visualizzato nei risultati di ricerca dei tag più rilevanti. Di conseguenza, elimina la possibilità che video non correlati vengano visualizzati nei risultati di ricerca.

* assegna una classificazione più alta a un tag per aumentarne la rilevanza rispetto a un video. La promozione di un tag per un video aumenta le possibilità che il video appaia nei risultati di ricerca quando viene eseguita una ricerca in base a tale tag.

Per ulteriori informazioni su come moderare i tag avanzati per le risorse, consulta [Gestione tag avanzati](smart-tags.md#manage-smart-tags-and-searches).

![Modera smart tag video](assets/manage-video-smart-tags.png)

>[!NOTE]
>
>Tutti i tag moderati utilizzando i passaggi in [Gestione smart tag](smart-tags.md#manage-smart-tags-and-searches) non vengono ricordati durante la rielaborazione della risorsa. Il set originale di tag viene nuovamente visualizzato.

## Rinuncia all’assegnazione tag avanzati video {#opt-out-video-smart-tagging}

Poiché l’assegnazione tag automatica dei video viene eseguita in parallelo ad altre attività di elaborazione delle risorse, come la creazione di miniature e l’estrazione di metadati, può richiedere tempo. Per accelerare l’elaborazione delle risorse, puoi rinunciare all’applicazione di tag avanzati video al caricamento a livello di cartella.

Per rinunciare alla generazione automatizzata di tag video avanzati per le risorse caricate in una cartella specifica:

1. Apri la scheda [!UICONTROL Elaborazione risorse] nella cartella [!UICONTROL Proprietà].

1. Nel menu [!UICONTROL Tag avanzati per video], l&#39;opzione [!UICONTROL Ereditato] è selezionata per impostazione predefinita e lo smart tag video è abilitato.

   Quando l&#39;opzione [!UICONTROL Ereditato] è selezionata, il percorso della cartella ereditata è visibile insieme all&#39;informazione se è impostato su [!UICONTROL Abilita] o [!UICONTROL Disabilita].

   ![Disattiva assegnazione tag avanzati video](assets/disable-video-tagging.png)

1. Seleziona [!UICONTROL Disattiva] per rifiutare l&#39;assegnazione di tag avanzati ai video caricati nella cartella.

>[!IMPORTANT]
>
>Se hai rinunciato a assegnare tag ai video in una cartella al momento del caricamento e desideri assegnarvi tag avanzati dopo il caricamento, **[!UICONTROL Abilita tag avanzati per video]** dalla scheda [!UICONTROL Elaborazione risorse] della cartella [!UICONTROL Proprietà] e utilizza l&#39;opzione [[!UICONTROL Rielabora risorsa] per aggiungere tag avanzati al video.](#smart-tag-existing-videos)

## Punteggio di affidabilità {#confidence-score-video-tag}

[!DNL Adobe Experience Manager] applica una soglia minima di affidabilità per i tag avanzati di oggetti e azioni per evitare di avere troppi tag per ogni risorsa video, rallentando così l&#39;indicizzazione. I risultati della ricerca delle risorse vengono classificati in base ai punteggi di affidabilità, che in genere migliorano i risultati della ricerca oltre a quanto suggerisce un’ispezione dei tag assegnati a qualsiasi risorsa video. I tag imprecisi hanno spesso punteggi di affidabilità bassi, pertanto raramente vengono visualizzati nella parte superiore dell’elenco Tag avanzati per le risorse.

La soglia predefinita per i tag azione e oggetto in [!DNL Adobe Experience Manager] è 0,7 (deve essere un valore compreso tra 0 e 1). Se alcune risorse video non sono taggate da un tag specifico, ciò indica che l’algoritmo ha un’affidabilità inferiore al 70% nei tag previsti. La soglia predefinita potrebbe non essere sempre ottimale per tutti gli utenti. Puoi quindi modificare il valore del punteggio di affidabilità nella configurazione OSGI.

Per aggiungere la configurazione OSGI del punteggio di affidabilità al progetto distribuito a [!DNL Adobe Experience Manager] come [!DNL Cloud Service] tramite [!DNL Cloud Manager]:

* Nel progetto [!DNL Adobe Experience Manager] (`ui.config` da Archetipo 24 o in precedenza `ui.apps`) la configurazione OSGi `config.author`, includi un file di configurazione denominato `com.adobe.cq.assetcompute.impl.aisdk.AISdkImpl.cfg.json` con il seguente contenuto:

```json
{
  "minVideoActionConfidenceScore":0.5,
  "minVideoObjectConfidenceScore":0.5,
}
```

>[!NOTE]
>
>Ai tag manuali viene assegnata un’affidabilità del 100% (affidabilità massima). Pertanto, se esistono risorse video con tag manuali che corrispondono alla query di ricerca, vengono visualizzate prima dei tag avanzati che corrispondono alla query di ricerca.

## Limitazioni {#video-smart-tagging-limitations}

* Non puoi addestrare il servizio che applica Tag avanzati ai video utilizzando video specifici. Funziona con le impostazioni predefinite di [!DNL Adobe AI].

* L’avanzamento dell’assegnazione tag non viene visualizzato.

* Solo i video di dimensioni inferiori a 300 MB vengono etichettati automaticamente. Il servizio [!DNL Adobe AI] ignora i file video di dimensioni maggiori.

* Solo i video nei formati di file e i codec supportati menzionati in [Tag avanzati](/help/assets/smart-tags.md#smart-tags-supported-file-formats) sono taggati.

>[!MORELIKETHIS]
>
>* [Gestione di tag avanzati e ricerche di risorse](smart-tags.md#manage-smart-tags-and-searches)
>* [Addestra il servizio di tag avanzati e assegna tag alle immagini](smart-tags.md)
