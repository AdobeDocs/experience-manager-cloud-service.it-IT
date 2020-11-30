---
title: Applicazione di tag avanzati alle risorse video
description: Le risorse video con tag avanzati automatizzano i tag delle risorse applicando tag contestuali e descrittivi tramite  servizi Adobe Sensei.
translation-type: tm+mt
source-git-commit: 68fe67617f0d63872f13427b3fbc7b58f2497aca
workflow-type: tm+mt
source-wordcount: '1284'
ht-degree: 0%

---


# Applicazione di tag avanzati alle risorse video {#video-smart-tags}

La crescente necessità di nuovi contenuti richiede un impegno manuale ridotto per offrire esperienze digitali coinvolgenti in tempi brevi. [!DNL Adobe Experience Manager] come Cloud Service, supporta l’assegnazione automatizzata di tag alle risorse video assistite da intelligenza artificiale. Assegnare manualmente i tag ai video può richiedere molto tempo. Tuttavia,  funzione di smart tag video basata su Adobe Sensei utilizza modelli di intelligenza artificiale per analizzare i contenuti video e aggiungere tag alle risorse video. In questo modo, gli utenti DAM possono dedicare meno tempo alla distribuzione di esperienze avanzate ai propri clienti.  Adobe  servizio di machine learning genera due set di tag per un video. Mentre, un set corrisponde a oggetti, scene e attributi nel video; l&#39;altro insieme riguarda azioni quali bere, correre e fare jogging.

I formati di file video (e i relativi codec) supportati per l’assegnazione di smart tag sono MP4 (H264/AVC), MKV (H264/AVC), MOV (H264/AVC, Motion JPEG), AVI (index4), FLV (H264/AVC, vp6f) e WMV 2). Inoltre, la funzione consente di aggiungere tag ai video fino a 300 MB. I tag automatici delle risorse video vengono utilizzati come elaborazione standard delle risorse (insieme alla creazione di miniature ed estrazione di metadati) dopo il caricamento di un video o quando viene attivata una nuova elaborazione. Gli smart tag vengono visualizzati in ordine decrescente rispetto al punteggio [di](#confidence-score-video-tag) confidenza ottenuto in [!UICONTROL Proprietà]risorsa. Per impostazione predefinita, l’assegnazione di tag video è abilitata in [!DNL Adobe Experience Manager] come Cloud Service. Tuttavia, potete [scegliere di non applicare tag](#opt-out-video-smart-tagging) video avanzati a una cartella.

## Applicazione di tag avanzati ai video durante il caricamento {#smart-tag-assets-on-ingestion}

Quando [caricate le risorse](add-assets.md#upload-assets) video [!DNL Adobe Experience Manager] come Cloud Service, i video vengono ![elaborati](assets/do-not-localize/assetprocessing.png). Al termine dell&#39;elaborazione, consultate la scheda [!UICONTROL Base] della pagina [!UICONTROL Proprietà] risorsa. I tag avanzati vengono aggiunti automaticamente al video sotto [!UICONTROL Smart Tags].  Asset compute Service utilizza  Adobe Sensei per creare questi smart tag.

![I tag avanzati vengono aggiunti ai video e visualizzati nella scheda Base delle proprietà della risorsa](assets/smart-tags-added-to-videos.png)

Gli smart tag applicati vengono ordinati in ordine decrescente in base al punteggio [di](#confidence-score-video-tag)attendibilità, combinati per i tag oggetto e azione, all&#39;interno dei tag [!UICONTROL avanzati].

>[!IMPORTANT]
>
>Si consiglia di esaminare questi tag generati automaticamente per assicurarsi che siano conformi al marchio e ai relativi valori.

## Assegnazione di tag avanzati ai video esistenti in DAM {#smart-tag-existing-videos}

Le risorse video già esistenti in DAM non dispongono di tag avanzati automaticamente. Per generare tag avanzati per le risorse, è necessario [!UICONTROL rielaborare le risorse] manualmente.

Per applicare tag smart alle risorse video o alle cartelle (comprese le sottocartelle) già presenti nell’archivio delle risorse, effettuate le seguenti operazioni:

1. Selezionate il [!DNL Adobe Experience Manager] logo, quindi selezionate le risorse dalla pagina di [!UICONTROL navigazione] .

1. Selezionate [!UICONTROL File] per visualizzare l’interfaccia Risorse.

1. Passate alla cartella alla quale desiderate applicare gli smart tag.

1. Selezionate l’intera cartella o specifiche risorse video.

1. Selezionate l&#39;icona ![Rielabora risorse](assets/do-not-localize/reprocess-assets-icon.png) Icona [!UICONTROL Rielabora risorse] e selezionate l&#39;opzione [!UICONTROL Elaborazione] completa.

![Rielaborare le risorse per aggiungere tag ai video nell&#39;archivio DAM esistente](assets/reprocess.gif)

Al termine del processo, andate alla pagina [!UICONTROL Proprietà] di qualsiasi risorsa video all’interno della cartella. I tag aggiunti automaticamente vengono visualizzati nella sezione Tag  avanzati della scheda [!UICONTROL Base] . Questi smart tag applicati vengono ordinati in ordine decrescente in base al punteggio [](#confidence-score-video-tag)di attendibilità.

## Cercare video con tag {#search-smart-tagged-videos}

Per cercare le risorse video in base agli smart tag generati automaticamente, usate [Omnisearch](search-assets.md#search-assets-in-aem):

1. Selezionate l’icona ![di](assets/do-not-localize/search_icon.png) ricerca dell’iconadi ricerca per visualizzare il campo Omnisearch.

1. Specificate un tag, nel campo Omnisearch, che non è stato aggiunto in modo esplicito a un video.

1. Consente di effettuare ricerche in base al tag .

I risultati della ricerca visualizzano le risorse video in base al tag specificato.

I risultati della ricerca sono una combinazione di risorse video con parole chiave ricercate nei metadati e risorse video con tag avanzati associati alle parole chiave cercate. Tuttavia, i risultati di ricerca che corrispondono a tutti i termini di ricerca nei campi di metadati vengono visualizzati per primi, seguiti dai risultati di ricerca che corrispondono a qualsiasi termine di ricerca negli smart tag. Per ulteriori informazioni, consultate [ [!DNL Experience Manager] Comprendere i risultati di ricerca con gli smart tag](smart-tags.md#understandsearch).

## Smart tag video moderati {#moderate-video-smart-tags}

[!DNL Adobe Experience Manager] consente di gestire gli smart tag per:

* rimuovete i tag non accurati assegnati ai video del vostro marchio.

* potete perfezionare le ricerche di video in base ai tag, accertandovi che il video venga visualizzato nei risultati di ricerca per i tag più rilevanti. Pertanto, elimina le possibilità che video non correlati vengano visualizzati nei risultati della ricerca.

* assegnate un rango più alto a un tag per aumentarne la pertinenza rispetto a un video. La promozione di un tag per un video aumenta le probabilità che il video venga visualizzato nei risultati della ricerca quando viene eseguita una ricerca in base a tale tag.

Per ulteriori informazioni su come moderare gli smart tag per le risorse, consultate [Gestire gli smart tag](smart-tags.md#manage-smart-tags-and-searches).

![Smart tag video moderati](assets/manage-video-smart-tags.png)

>[!NOTE]
>
>Eventuali tag moderati tramite i passaggi di [Manage smart tag](smart-tags.md#manage-smart-tags-and-searches) non vengono ricordati durante la rielaborazione della risorsa. Il set di tag originale viene visualizzato di nuovo.

## Rifiuto dell’assegnazione di tag video avanzati {#opt-out-video-smart-tagging}

L’applicazione automatizzata di tag ai video avviene in parallelo ad altre attività di elaborazione delle risorse, come la creazione di miniature ed estrazione di metadati. Può richiedere molto tempo. Per accelerare l’elaborazione delle risorse potete rinunciare all’assegnazione di tag video avanzati al caricamento a livello di cartella.

Per rifiutare la generazione automatica di smart tag video per le risorse caricate in una cartella specifica:

1. Aprite la scheda Elaborazione  risorse in [!UICONTROL Proprietà]cartella.

1. Nel menu [!UICONTROL Tag avanzati per video] , l&#39;opzione [!UICONTROL Ereditato] è selezionata per impostazione predefinita e lo smart tag video è attivato.

   Quando l&#39;opzione [!UICONTROL Ereditato] è selezionata, anche il percorso della cartella ereditata è visibile insieme alle informazioni sia che sia impostato su [!UICONTROL Abilita] o [!UICONTROL Disattiva].

   ![Disabilita tag video avanzati](assets/disable-video-tagging.png)

1. Selezionate [!UICONTROL Disattiva] per rifiutare l’assegnazione di smart tag ai video caricati nella cartella.

>[!IMPORTANT]
>
>Se avete rinunciato a assegnare tag ai video presenti in una cartella al momento del caricamento e desiderate aggiungere tag avanzati ai video dopo il caricamento, **[!UICONTROL Attivate i tag avanzati per i video]** dalla scheda Elaborazione [!UICONTROL delle] risorse della cartella [!UICONTROL Proprietà] e utilizzate l’opzione [ Rielabora risorsa](#smart-tag-existing-videos) per aggiungere tag avanzati al video.

## Punteggio di confidenza {#confidence-score-video-tag}

[!DNL Adobe Experience Manager] applica una soglia di confidenza minima per gli smart tag di oggetto e azione per evitare di avere troppi tag per ciascuna risorsa video, il che rallenta l’indicizzazione. I risultati della ricerca delle risorse vengono classificati in base ai punteggi di attendibilità, che in genere migliorano i risultati della ricerca oltre a quanto suggerisce un’ispezione dei tag assegnati di qualsiasi risorsa video. I tag non accurati hanno spesso dei punteggi di confidenza bassi, pertanto vengono raramente visualizzati nella parte superiore dell’elenco dei tag avanzati per le risorse.

La soglia predefinita per i tag azione e oggetto in [!DNL Adobe Experience Manager] è 0,7 (il valore deve essere compreso tra 0 e 1). Se alcune risorse video non dispongono di tag specifici, significa che l’algoritmo è sicuro di meno del 70% nei tag previsti. La soglia predefinita potrebbe non essere sempre ottimale per tutti gli utenti. È quindi possibile modificare il valore del punteggio di confidenza nella configurazione OSGI.

Per aggiungere la configurazione OSGI del punteggio di confidenza al progetto distribuito [!DNL Adobe Experience Manager] come Cloud Service tramite Cloud Manager:

* Nel [!DNL Adobe Experience Manager] progetto (`ui.config` a partire da Archetype 24, o in precedenza `ui.apps`) la configurazione `config.author` OSGi, includete un file di configurazione denominato `com.adobe.cq.assetcompute.impl.senseisdk.SenseiSdkImpl.cfg.json` con i seguenti contenuti:

```json
{
  "minVideoActionConfidenceScore":0.5,
  "minVideoObjectConfidenceScore":0.5,
}
```

>[!NOTE]
>
>Ai tag manuali viene assegnata una confidenza del 100% (massima affidabilità). Di conseguenza, se sono presenti risorse video con tag manuali corrispondenti alla query di ricerca, queste vengono visualizzate prima di smart tag corrispondenti alla query di ricerca.

## Limitazioni  {#video-smart-tagging-limitations}

* Non è ancora supportata la formazione di Smart Tag Service (o Enhanced Smart Tags) per l’assegnazione di tag alle risorse video.

* L’avanzamento dei tag non viene visualizzato.

* Solo i video di dimensioni non superiori a 300 MB sono adatti per l’assegnazione di tag. Il servizio  Adobe Sensei consente di aggiungere tag ai video che soddisfano questi criteri e di ignorare l’assegnazione di tag ad altri video in una cartella.

* Solo i video in questi formati di file (e codec supportati): MP4 (H264/AVC), MKV (H264/AVC), MOV (H264/AVC, Motion JPEG), AVI (index4), FLV (H264/AVC, vp6f) e WMV (WMV2)—può essere taggato.

>[!MORELIKETHIS]
>
>* [Gestione di smart tag e ricerche di risorse](smart-tags.md#manage-smart-tags-and-searches)
>* [Servizio Smart Tag per formazione e tag delle immagini](smart-tags.md)

