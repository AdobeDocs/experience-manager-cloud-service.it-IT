---
title: Assegna tag automatici alle risorse con  [!DNL Adobe Sensei] servizio avanzato
description: Assegna tag alle risorse con un servizio artificialmente intelligente che applica tag aziendali contestuali e descrittivi.
feature: Smart Tags,Tagging
role: Admin,User
exl-id: a2abc48b-5586-421c-936b-ef4f896d78b7
source-git-commit: 03cbcf098e0640705aa2a69a8fa605ab1e8cbb06
workflow-type: tm+mt
source-wordcount: '2082'
ht-degree: 1%

---

# Tag avanzati per AEM Assets {#using-smart-tags}

Le organizzazioni possiedono numerose risorse digitali, e questo numero continua a crescere rapidamente. La ricerca di una risorsa specifica in un numero così elevato di dati rappresenta una sfida significativa. Per risolvere questo problema, `metadata` e `tags` vengono utilizzati per migliorare la ricercabilità delle risorse digitali. Le organizzazioni utilizzano vocabolari controllati dalla tassonomia nei metadati delle risorse. In genere si tratta di elenchi di parole chiave utilizzati da dipendenti, partner e clienti per fare riferimento e individuare le risorse digitali.

I tag avanzati sono parole chiave che non solo compaiono nel testo, ma che descrivono meglio la risorsa. L’assegnazione dei tag alle risorse tramite un vocabolario controllato dalla tassonomia consente di identificarle e recuperarle facilmente tramite la ricerca.

Ad esempio, le parole disposte alfabeticamente in un dizionario sono più facili da trovare rispetto a quelle sparse casualmente. L’assegnazione tag ha uno scopo simile. Organizza le risorse in base alla tassonomia aziendale, garantendo che quelle più rilevanti appaiano nei risultati di ricerca. Ad esempio, un produttore di automobili può taggare le immagini dell’auto con i nomi dei modelli, in modo che vengano visualizzate solo le immagini pertinenti durante la progettazione di una campagna promozionale. Che si tratti di assegnare tag a &quot;corridori&quot; o &quot;scarpe da corsa&quot;, gli utenti non devono preoccuparsi di errori di battitura, variazioni di ortografia o termini di ricerca alternativi: i tag avanzati li riconoscono tutti.

In background, la funzionalità utilizza il framework artificialmente intelligente di [Adobe Sensei](https://business.adobe.com/products/sensei/adobe-sensei.html) applica automaticamente Tag avanzati alle risorse caricate, per impostazione predefinita, insieme al testo allineato alla tassonomia aziendale.

## Prerequisiti e configurazione {#smart-tags-prereqs-config}

Il provisioning di Tag avanzati viene eseguito automaticamente per [!DNL Adobe Experience Manager] come [!DNL Cloud Service] e pertanto non è richiesta alcuna configurazione.

## Flusso di lavoro per tag avanzati {#smart-tags-workflow}

L&#39;assegnazione tag avanzati basati su [!DNL Adobe Sensei] utilizza modelli di intelligenza artificiale per analizzare il contenuto e aggiungere tag alle risorse. In questo modo, gli utenti DAM possono ridurre i tempi necessari per fornire esperienze avanzate ai propri clienti. I tag avanzati vengono visualizzati in ordine decrescente del relativo [punteggio di affidabilità](#confidence-score) nelle proprietà della risorsa.

* **Risorse basate su immagini**
Per le immagini, i tag avanzati si basano su un aspetto visivo. Le immagini in molti formati vengono taggate utilizzando i servizi per contenuti avanzati. I tag avanzati vengono applicati ai [tipi di file supportati](#supported-file-formats) che generano copie trasformate in formato JPG e PNG.

  <!-- ![Image Smart Tag](assets/image-smart-tag.png)-->

* **Risorse basate su video**
Per le risorse basate su video, l&#39;assegnazione tag è abilitata per impostazione predefinita in [!DNL Adobe Experience Manager] come [!DNL Cloud Service]. Allo stesso modo, i tag basati su immagini e testo vengono assegnati automaticamente anche ai video quando caricano nuovi video o li rielaborano. [!DNL Adobe Sensei] genera due set di tag per un video: un set corrisponde a oggetti, scene e attributi del video, mentre l&#39;altro set è relativo ad azioni quali bere, correre e fare jogging. Controlla anche [rinuncia ai tag avanzati video](#opt-out-video-smart-tagging).

* **Risorse basate su testo**
Per le risorse supportate, [!DNL Experience Manager] estrae già il testo, che viene quindi indicizzato e utilizzato per cercare le risorse. Tuttavia, i tag avanzati basati sulle parole chiave nel testo forniscono un facet di ricerca dedicato, strutturato e con priorità più elevata. Quest’ultimo consente di migliorare l’individuazione delle risorse rispetto a un indice di ricerca.
Per le risorse basate su testo, l’efficacia dei tag avanzati non dipende dalla quantità di testo nella risorsa, ma dalle parole chiave o entità pertinenti presenti nel testo della risorsa.

  ![Tipi di tag avanzati](assets/smart-tags-types.png)

I tag avanzati sono implementati in AEM Assets utilizzando il seguente flusso di lavoro:

1. Crea o carica una risorsa in AEM. I tag predefiniti vengono generati per Assets basati su immagini, video e testo.

1. Se scopri che non sono generati tag specifici, puoi addestrare di conseguenza i tag di tipo immagine. Consulta [Apprendimento dei tag avanzati](/help/assets/smart-tags-training.md).

## Formati di file supportati per tag avanzati {#supported-file-formats}

| Immagini (tipi MIME) | Risorse basate su testo (formati di file) | Risorse video (formati di file e codec) |
|----|-----|------|
| image/jpeg | CSV | MP4 (H264/AVC) |
| image/tiff | DOC | MKV (H264/AVC) |
| image/png | DOCX | MOV (H264/AVC, Motion JPEG) |
| image/bmp | HTML | AVI (indeo4) |
| image/gif | PDF | FLV (H264/AVC, vp6f) |
| image/pjpeg | PPT | WMV (WMV2) |
| image/x-portable-anymap | PPTX |  |
| image/x-portable-bitmap | RTF |  |
| image/x-portable-graymap | SRT |  |
| image/x-portable-pixmap | TXT |  |
| image/x-rgb | VTT |  |
| image/x-xbitmap | |  |
| image/x-xpixmap | |  |
| image/x-icon |  |  |
| image/photoshop |  |  |
| image/x-photoshop |  |  |
| image/psd |  |  |
| image/vnd.adobe.photoshop |  |  |

## Preparazione di una risorsa per l’assegnazione di tag avanzati predefiniti

Quando [carichi le risorse](add-assets.md#upload-assets) in [!DNL Adobe Experience Manager] come [!DNL Cloud Service], le risorse caricate vengono elaborate. Al termine dell&#39;elaborazione, vedere la scheda [!UICONTROL Base] della risorsa [!UICONTROL Proprietà]. I tag avanzati vengono aggiunti automaticamente alle risorse in [!UICONTROL Tag avanzati]. I microservizi per le risorse utilizzano [!DNL Adobe Sensei] per creare questi tag avanzati.

![I tag avanzati vengono aggiunti ai video e visualizzati nella scheda Base delle Proprietà della risorsa](assets/smart-tags-added-to-videos.png)

<!--
The applied smart tags are sorted in descending order of [confidence score](#confidence-score), combined for object and action tags, within [!UICONTROL Smart Tags].
-->

>[!IMPORTANT]
>
>Ti consigliamo di rivedere questi tag generati automaticamente per assicurarti che siano conformi al tuo marchio e ai suoi valori.

## Assets senza tag in DAM {#smart-tag-existing-assets}

Le risorse esistenti o precedenti in DAM non vengono contrassegnate automaticamente con tag avanzati. Devi [Rielaborare](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/about-image-video-profiles.html?lang=en#adjusting-load) Assets manualmente per generare tag avanzati per loro. Al termine del processo, passa alla pagina [!UICONTROL Proprietà] di qualsiasi risorsa all&#39;interno della cartella. I tag aggiunti automaticamente sono visualizzati nella sezione [!UICONTROL Tag avanzati] della scheda [!UICONTROL Base]. Questi tag avanzati applicati sono ordinati in ordine decrescente di [punteggio di affidabilità](#confidence-score).

<!--
To smart tag assets, or folders (including subfolders) of assets that exist in assets repository, follow these steps:

1. Select the [!DNL Adobe Experience Manager] logo and then select assets from the [!UICONTROL Navigation] page.

1. Select [!UICONTROL Files] to display the Assets interface.

1. Navigate to the folder to which you want to apply Smart Tags.

1. Select the assets and click ![Reprocess assets icon](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL Reprocess Assets] icon and select the [!UICONTROL Full Process] option.

![Reprocess assets to add tags to videos existing DAM repository](assets/reprocess.gif)-->

## Punteggio di affidabilità {#confidence-score}

I risultati della ricerca delle risorse vengono classificati in base ai punteggi di affidabilità, che in genere migliorano i risultati della ricerca oltre a quanto suggerisce un’ispezione dei tag assegnati a qualsiasi risorsa. I tag imprecisi hanno spesso punteggi di affidabilità bassi, pertanto raramente vengono visualizzati nella parte superiore dell’elenco Tag avanzati per le risorse.
<!--
[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] applies a minimum confidence threshold for object and action-smart tags to avoid having too many tags for each asset, which slows down indexing. 

The default threshold for action and object tags in [!DNL Adobe Experience Manager] for an image is 0.5 and for video it is 0.7 (should be value from 0 through 1). If some assets are not tagged by a specific tag, then it indicates that the algorithm is less than 70% confident in the predicted tags. The default threshold might not always be optimal for all the users. You can, therefore, change the confidence score value in OSGI configuration.

To add the confidence score OSGI configuration to the project deployed to [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] through [!DNL Cloud Manager]:

In the [!DNL Adobe Experience Manager] project (`ui.config` since Archetype 24, or previously `ui.apps`) the `config.author` OSGi configuration, include a config file named `com.adobe.cq.assetcompute.impl.senseisdk.SenseiSdkImpl.cfg.json` with the following contents:

```json
{
  "minVideoActionConfidenceScore":0.5,
  "minVideoObjectConfidenceScore":0.5,
}
```
-->

>[!NOTE]
>
>Ai tag manuali viene assegnata un’affidabilità del 100% (affidabilità massima). Pertanto, se esistono risorse con tag manuali che corrispondono alla query di ricerca, questi vengono visualizzati prima dei Tag avanzati che corrispondono alla query di ricerca.

## Modera tag avanzati {#moderate-smart-tags}

[!DNL Adobe Experience Manager] come [!DNL Cloud Service] ti consente di curare i tag avanzati in:

* rimuovi i tag non accurati assegnati alle risorse del tuo marchio.

* perfeziona le ricerche di risorse basate su tag garantendo che la risorsa sia visualizzata nei risultati di ricerca dei tag più rilevanti. Di conseguenza, elimina la possibilità che risorse non correlate vengano visualizzate nei risultati di ricerca.

* assegna una classificazione più alta a un tag per aumentarne la rilevanza rispetto a una risorsa. La promozione di un tag per una risorsa aumenta le possibilità che una particolare risorsa venga visualizzata nei risultati di ricerca quando viene eseguita una ricerca in base a tale tag.

Per ulteriori informazioni su come moderare i tag avanzati per le risorse, consulta [Gestione tag avanzati](smart-tags.md#manage-smart-tags-and-searches).

![Modera tag avanzati video](assets/manage-video-smart-tags.png)

>[!NOTE]
>
>Tutti i tag moderati utilizzando i passaggi in [Gestisci tag avanzati](smart-tags.md#manage-smart-tags-and-searches) non vengono ricordati durante la rielaborazione della risorsa. Vengono visualizzati di nuovo i set di tag originali.

## Gestire tag avanzati e ricerche di risorse {#manage-smart-tags-and-searches}

Puoi curare i tag avanzati per rimuovere eventuali tag non accurati assegnati alle risorse del tuo marchio, in modo che vengano visualizzati solo i tag più rilevanti.

La moderazione dei tag avanzati consente inoltre di perfezionare le ricerche di risorse basate su tag, garantendo che le risorse vengano visualizzate nei risultati di ricerca per i tag più rilevanti. In sostanza, aiuta a eliminare la possibilità che risorse non correlate vengano visualizzate nei risultati di ricerca.

Puoi anche assegnare una classificazione più alta a un tag per aumentarne la rilevanza per la risorsa. La promozione di un tag per una risorsa aumenta le possibilità che la risorsa appaia nei risultati di ricerca quando viene eseguita una ricerca in base a tale tag.

Per moderare i tag avanzati delle risorse digitali:

1. Nel campo di ricerca, cerca le risorse digitali in base a un tag.

1. Per identificare le risorse digitali che non trovi rilevanti per la ricerca, controlla i risultati della ricerca.

1. Seleziona una risorsa, quindi seleziona ![Icona Gestisci tag](assets/do-not-localize/manage-tags-icon.png) dalla barra degli strumenti.

1. Nella pagina **[!UICONTROL Gestisci tag]**, controlla i tag. Se non desideri che la risorsa venga cercata in base a un tag specifico, seleziona il tag e fai clic sull&#39;![icona Elimina](assets/do-not-localize/delete-icon.svg) nella barra degli strumenti. In alternativa, seleziona ![icona chiudi](assets/do-not-localize/close_icon.svg) accanto all&#39;etichetta.

1. Per assegnare una classificazione superiore a un tag, selezionare il tag e selezionare ![Icona Promuovi](assets/do-not-localize/promote-icon.svg) dalla barra degli strumenti. Il tag promosso è stato spostato nella sezione **[!UICONTROL Tag]**.

1. Seleziona **[!UICONTROL Salva]**, quindi seleziona **[!UICONTROL OK]** per chiudere la finestra di dialogo [!UICONTROL Operazione riuscita].

1. Passa alla pagina [!UICONTROL Proprietà] della risorsa. Tieni presente che al tag promosso viene assegnata una rilevanza elevata e, pertanto, viene visualizzato più in alto nei risultati di ricerca.

### Comprendere i risultati della ricerca di [!DNL Experience Manager] con tag avanzati {#understand-search}

Per impostazione predefinita, [!DNL Experience Manager] combina i termini di ricerca con una clausola `AND` o `OR` per trovare i termini di ricerca nei tag avanzati applicati. L’utilizzo di Tag avanzati non modifica questo comportamento predefinito. Ad esempio, provare a cercare `woman running`. Assets con solo `woman` o solo `running` parola chiave nei metadati non viene visualizzata nei risultati della ricerca per impostazione predefinita. Tuttavia, una risorsa con tag `woman` o `running` tramite Tag avanzati viene visualizzata in tale query di ricerca. I risultati della ricerca sono quindi una combinazione di:

* Assets con `woman` e `running` parole chiave nei metadati.

* Smart tag di Assets con una delle parole chiave.

I risultati della ricerca che corrispondono a tutti i termini di ricerca nei campi di metadati vengono visualizzati per primi, seguiti dai risultati della ricerca che corrispondono a qualsiasi termine di ricerca nei tag avanzati. Nell’esempio precedente, l’ordine approssimativo di visualizzazione dei risultati della ricerca è:

1. corrispondenze di `woman running` nei vari campi di metadati.
1. corrispondenze di `woman running` in Tag avanzati.
1. corrisponde a `woman` o `running` in Tag avanzati.

## Rinuncia all’assegnazione tag avanzati {#opt-out-smart-tagging}

Poiché l’assegnazione tag automatica delle risorse viene eseguita in parallelo ad altre attività di elaborazione delle risorse, come la creazione di miniature e l’estrazione di metadati, può richiedere molto tempo. Per accelerare l’elaborazione delle risorse, puoi rinunciare all’assegnazione tag avanzati al caricamento a livello di cartella. Per rinunciare alla generazione automatizzata di tag avanzati per le risorse caricate in una cartella specifica:

1. Apri la scheda [!UICONTROL Elaborazione risorse] nella cartella [!UICONTROL Proprietà].
1. Nel menu [!UICONTROL Tag avanzati per video], ad esempio, l&#39;opzione [!UICONTROL Ereditato] è selezionata per impostazione predefinita e lo smart tag video è abilitato.

   Quando l&#39;opzione [!UICONTROL Ereditato] è selezionata, il percorso della cartella ereditata è visibile insieme all&#39;informazione se è impostato su [!UICONTROL Abilita] o [!UICONTROL Disabilita].

   ![Disattiva assegnazione tag avanzati](assets/disable-tagging.png)

1. Seleziona [!UICONTROL Disattiva] per rifiutare l&#39;assegnazione di tag avanzati caricati nella cartella.

1. Allo stesso modo, puoi rinunciare all&#39;assegnazione di tag avanzati per [!UICONTROL Tag avanzati per testo], [!UICONTROL Tag avanzati per immagine] e [!UICONTROL Tag colori per immagini].

>[!IMPORTANT]
>
>Se al momento del caricamento hai rinunciato a assegnare tag a una cartella e desideri assegnarvi tag avanzati dopo il caricamento, **[!UICONTROL Abilita tag avanzati]** dalla scheda [!UICONTROL Elaborazione risorse] della cartella [!UICONTROL Proprietà] e utilizza l&#39;opzione [[!UICONTROL Rielabora risorse]](#smart-tag-existing-assets) per aggiungere tag avanzati alle risorse.

<!--
## Benefits of Smart Tags to your assets {#benefits-of-smart-tags}

Following are the benefits of using Smart Tags in your AEM Assets:
*  Makes an asset searchable.
*  Smart Tags are generated automatically to your assets, thus, it minimizes your effort to perform tagging manually.
*  It allows the usage of the same vocabulary, tag structure, and taxonomy so that you need not to worry about tagging if by chance you miss tagging at first.
*  Whether you are tagging "runners" or "running" shoes, you do not need to worry about typos, wrong spellings, or alternative search terms as Smart Tags know it already!
*  Helps your assets to become organized and categorized.
-->

## Limitazioni e best practice relative ai tag avanzati {#limitations-best-practices-smart-tags}

Questi modelli non sono sempre perfetti per identificare i tag. La versione corrente dei tag avanzati presenta le seguenti limitazioni:

* Incapacità di riconoscere le sottili differenze nelle immagini. Ad esempio, magliette o magliette.
* Impossibilità di identificare i tag in base a modelli o parti di un’immagine di dimensioni ridotte. Ad esempio, i logo sulle camicie.
* I tag non gestiti si riferiscono a:

   * Aspetti astratti e non visivi. Ad esempio, l’anno o la stagione di rilascio di un prodotto, l’umore o l’emozione evocati da un’immagine e una connotazione soggettiva di un video.
   * Differenze visive precise in prodotti come camicie con e senza colletto o logo di prodotto incorporati nei prodotti.

* Solo i video di dimensioni inferiori a 300 MB vengono etichettati automaticamente. Il servizio [!DNL Adobe Sensei] ignora i file video di dimensioni maggiori.
* Per cercare file con tag avanzati (regolari o avanzati), utilizzare la ricerca [!DNL Assets] (ricerca full-text). Non esiste un predicato di ricerca separato per i tag avanzati.
* Rispetto ai tag generali, le risorse con tag utilizzati nella tassonomia aziendale sono più facili da identificare e recuperare mediante ricerche basate su tag.

## Domande frequenti{#faq-smart-tags}

+++**In che modo i tag avanzati migliorano l&#39;esperienza di ricerca di una risorsa?**

[!DNL Adobe] Sensei assegna automaticamente i tag alle risorse dopo averle caricate. Il processo automatizzato viene eseguito così rapidamente nel backend che, al termine del caricamento, dopo alcuni secondi verranno visualizzati i tag aggiunti alle risorse.

+++

+++**Cosa succede se l&#39;elenco dei tag avanzati non è accurato o mostra tag indesiderati?**

Un tag inesatto o indesiderato può essere rimosso dall’elenco. Ad esempio, in qualità di rivenditore di automobili, potresti voler rimuovere il tag &quot;danneggiato&quot; dall’elenco.

+++

+++**Come assegnare la priorità alle risorse contenenti gli stessi tag?**

Sì, puoi assegnare la priorità alle risorse contenenti gli stessi tag. Puoi promuovere un tag nell’elenco Tag avanzati di una risorsa per eseguire la definizione delle priorità. La promozione di un tag consente di assegnare la priorità alle immagini visualizzate nei risultati di ricerca per quel particolare tag.

+++

+++**L&#39;applicazione dei tag avanzati è limitata a una cartella specifica?**

I tag avanzati sono configurabili e possono essere applicati a qualsiasi cartella all’interno di DAM.

+++

+++**Come posso sapere che l&#39;assegnazione tag richiede formazione?**

Consulta [Determinazione dei requisiti per l&#39;apprendimento dei tag avanzati](/help/assets/smart-tags-training.md#smart-tag-training-requirement).

+++

+++**Quali sono i formati di file supportati per l&#39;assegnazione di tag a una risorsa?**

Consulta [Formati di file supportati](#supported-file-formats).

+++

+++**In quale lingua vengono generati gli smart tag?**

I tag avanzati vengono generati solo in lingua inglese. Possono essere tradotte in altre lingue traducendo l’intera risorsa, inclusi i metadati.

+++

+++**Non si desidera più utilizzare l&#39;assegnazione tag avanzati.**

Puoi [rinunciare all&#39;assegnazione tag avanzati](#opt-out-smart-tagging) in qualsiasi momento desideri interrompere.

+++
