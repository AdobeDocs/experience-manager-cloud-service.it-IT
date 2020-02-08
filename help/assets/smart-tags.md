---
title: Smart tag migliorati
description: Applica tag business contestuali e descrittivi utilizzando i servizi AI e ML di Adobe Sensei, per migliorare l'individuazione delle risorse e la velocità dei contenuti.
contentOwner: AG
translation-type: tm+mt
source-git-commit: dfa9b099eaf7f0d155986bbab7d56901876d98f6

---


# Applicazione di tag avanzati alle risorse {#smart-tag-assets}

## Panoramica dei tag avanzati {#overview-of-enhanced-smart-tags}

Le organizzazioni che si occupano di risorse digitali utilizzano sempre più vocabolario controllato dalla tassonomia nei metadati delle risorse. Comprende in sostanza un elenco di parole chiave utilizzate comunemente da dipendenti, partner e clienti per fare riferimento e cercare risorse digitali di una determinata classe. L’assegnazione di tag alle risorse con un vocabolario controllato dalla tassonomia ne consente l’identificazione e il recupero tramite ricerche basate sui tag.

Rispetto ai vocabolari di lingua naturale, l’assegnazione di tag alle risorse digitali in base alla tassonomia aziendale consente di allinearle al business di un’azienda e garantisce che le risorse più rilevanti vengano visualizzate nelle ricerche. Ad esempio, un produttore di auto può assegnare tag alle immagini di un&#39;auto con nomi di modelli in modo che vengano visualizzate solo immagini rilevanti quando vengono ricercate immagini di vari modelli per progettare una campagna promozionale.

In background, Smart Content Service utilizza il framework AI di [Adobe Sensei](https://www.adobe.com/sensei/experience-cloud-artificial-intelligence.html) per formare il suo algoritmo di riconoscimento delle immagini sulla struttura dei tag e la tassonomia aziendale. Questa funzione di content intelligence viene quindi utilizzata per applicare tag rilevanti a un altro set di risorse.

>[!NOTE]
>
>Smart Content Services è applicabile solo ai clienti Assets. Smart Content Service è disponibile per l&#39;acquisto come componente aggiuntivo per Experience Manager.

<!-- ![flowchart](assets/flowchart.gif) -->

## Gestione di smart tag e ricerche {#manage-smart-tags-and-searches}

Potete curare gli smart tag per rimuovere eventuali tag non accurati eventualmente assegnati alle immagini del vostro marchio, in modo da visualizzare solo i tag più rilevanti.

La moderazione degli smart tag consente inoltre di perfezionare le ricerche basate sui tag per le immagini, assicurando che l’immagine venga visualizzata nei risultati di ricerca per i tag più rilevanti. In sostanza, elimina la possibilità che immagini non collegate vengano visualizzate nei risultati della ricerca.

Potete anche assegnare un rango più alto a un tag per aumentarne la rilevanza rispetto a un’immagine. La promozione di un tag per un’immagine aumenta le probabilità che l’immagine venga visualizzata nei risultati di ricerca quando viene eseguita una ricerca in base al tag specifico.

1. Nella casella di ricerca Omnico, cercate le risorse basate su un tag.
1. Controllate i risultati della ricerca per identificare un’immagine che non vi interessa.
1. Selezionate l’immagine, quindi toccate o fate clic sull’icona **[!UICONTROL Gestisci tag]** nella barra degli strumenti.
1. Dalla pagina **[!UICONTROL Gestisci tag]** , ispezionate i tag. Se non desiderate che l’immagine venga cercata in base a un tag specifico, selezionate il tag e quindi fate clic o toccate l’icona Elimina dalla barra degli strumenti. In alternativa, toccate o fate clic `X` sul simbolo visualizzato accanto all’etichetta.
1. Per assegnare un rango più alto a un tag, selezionatelo e toccate o fate clic sull’icona di promozione nella barra degli strumenti. Il tag promosso viene spostato nella sezione **[!UICONTROL Tag]** .
1. Tocca o fai clic su **[!UICONTROL Salva]**, quindi su **[!UICONTROL OK]** per chiudere la finestra di dialogo Successo.
1. Passate alla pagina delle proprietà dell’immagine. Osservate che al tag promosso è stata assegnata un’elevata rilevanza e, di conseguenza, appare più alta nei risultati della ricerca.

### Comprendere i risultati della ricerca AEM con gli smart tag {#understandsearch}

Per impostazione predefinita, la ricerca AEM combina i termini di ricerca con una `AND` clausola. L&#39;utilizzo di smart tag non modifica questo comportamento predefinito. L&#39;utilizzo di smart tag aggiunge una `OR` clausola aggiuntiva per individuare qualsiasi termine di ricerca negli smart tag applicati. For example, consider searching for `woman running`. Per impostazione predefinita, le risorse con una sola parola chiave `woman` o una sola `running` parola chiave nei metadati non vengono visualizzate nei risultati della ricerca. Tuttavia, in una query di ricerca di questo tipo viene visualizzata una risorsa con `woman` o `running` tramite smart tag. Quindi i risultati della ricerca sono una combinazione di:

* risorse con `woman` e `running` parole chiave nei metadati.

* assets smart tag con una delle parole chiave.

I risultati della ricerca che corrispondono a tutti i termini di ricerca nei campi di metadati vengono visualizzati per primi, seguiti dai risultati della ricerca che corrispondono a qualsiasi termine di ricerca negli smart tag. Nell&#39;esempio precedente, l&#39;ordine approssimativo di visualizzazione dei risultati della ricerca è:

1. corrispondenze di `woman running` nei vari campi di metadati.
1. corrispondenze di `woman running` in smart tag.
1. corrispondenze di `woman` o di `running` in smart tag.

<!-- 

## Training the Smart Content Service {#training-the-smart-content-service}

For the Smart Content Service to recognize your business taxonomy, run it on a set of assets that already include tags that are relevant to your business. After training, the service can apply the same taxonomy on a similar set of assets.

You can train the service multiple times to improve its ability to apply relevant tags. After each training cycle, run a tagging workflow and check whether your assets are tagged appropriately.

You can train the Smart Content Service periodically or on requirement basis.

>[!NOTE]
>
>The training workflow runs on folders only.

### Periodic training {#periodic-training}

You can enable the Smart Content Service to train periodically on the assets and associated tags within a folder. Open the properties page of your asset folder, select **[!UICONTROL Enable Smart Tags]** under the **[!UICONTROL Details]** tab, and save the changes.

Once this option is selected for a folder, AEM runs a training workflow automatically to train the Smart Content Service on the folder assets and their tags. By default, the training workflow runs on a weekly basis at 12:30 AM on Saturdays.

### On-demand training {#on-demand-training}

You can train the Smart Content Service whenever required from the Workflow console.

1. Tap/click the AEM logo, and go to **[!UICONTROL Tools > Workflow > Models]**.
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL Smart Tags Training]** workflow and then tap/click **[!UICONTROL Start Workflow]** from the toolbar.
1. In the **[!UICONTROL Run Workflow]** dialog, browse to the payload folder that includes the tagged assets for training the service.
1. Specify a title for the workflow and a add a comment. Then, tap/click **[!UICONTROL Run]**. The assets and tags are submitted for training.

>[!NOTE]
>
>Once the assets in a folder are processed for training, only the modified assets are processed in subsequent training cycles.

### Viewing training reports {#viewing-training-reports}

To check whether the Smart Content Service is trained on your tags in the training set of assets, review the training workflow report from the Reports console.

1. Tap/click the AEM logo, and go to **[!UICONTROL Tools > Assets > Reports]**.
1. In the **[!UICONTROL Asset Reports]** page, tap/click **[!UICONTROL Create]**.
1. Select the **[!UICONTROL Smart Tags Training]** report, and then tap/click **[!UICONTROL Next]** from the toolbar.
1. Specify a title and description for the report. Under **[!UICONTROL Schedule Report]**, leave the **[!UICONTROL Now]** option selected. If you want to schedule the report for later, select **[!UICONTROL Later]** and specify a date and time. Then, tap/click **[!UICONTROL Create]** from the toolbar.
1. In the **[!UICONTROL Asset Reports]** page, select the report you generated. To view the report, tap/click the **[!UICONTROL View]** icon from the toolbar.
1. Review the details of the report.

   The report displays the training status for the tags you trained. The green color in the **[!UICONTROL Training Status]** column indicates that the Smart Content Service is trained for the tag. Yellow color indicates that the service is not completely trained for a particular tag. In this case, add more images with the particular tag and run the training workflow to train the service completely on the tag.

   If you do not see your tags in this report, run the training workflow again for these tags.

1. To download the report, select it from the list, and tap/click the **[!UICONTROL Download]** icon from the toolbar. The report downloads as an Excel file.

## Tagging assets automatically {#tagging-assets-automatically}

After you have trained the Smart Content Service, you can trigger the tagging workflow to automatically apply appropriate tags on a different set of similar assets.

You can run the tagging workflow periodically or whenever required.

>[!NOTE]
>
>The tagging workflow runs on both assets and folders.

### Periodic tagging {#periodic-tagging}

You can enable the Smart Content Service to periodically tag assets within a folder. Open the properties page of your asset folder, select **[!UICONTROL Enable Smart Tags]** under the **[!UICONTROL Details]** tab, and save the changes.

Once this option is selected for a folder, the Smart Content Service automatically tags the assets within the folder. By default, the tagging workflow runs every day at 12:00 AM.

### On-demand tagging {#on-demand-tagging}

You can trigger the tagging workflow from the following to instantly tag your assets:

* Workflow console
* Timeline

>[!NOTE]
>
>If you run the tagging workflow from the timeline, you can apply tags on a maximum of 15 assets at a time.

#### Tagging assets from the Workflow console {#tagging-assets-from-the-workflow-console}

1. Tap/click the AEM logo, and go to **[!UICONTROL Tools > Workflow > Models]**.
1. From the **[!UICONTROL Workflow Models]** page, select the **[!UICONTROL DAM Smart Tags Assets]** workflow and then tap/click **[!UICONTROL Start Workflow]** from the toolbar.
1. In the **[!UICONTROL Run Workflow]** dialog, browse to the payload folder containing assets on which you want to apply your tags automatically.
1. Specify a title for the workflow and an optional comment. Then, tap/click **[!UICONTROL Run]**.

Navigate to the asset folder and review the tags to verify whether the Smart Content Service tagged your assets properly. For details, see [Managing Smart Tags](manage-smart-tags.md).

#### Tagging assets from the timeline {#tagging-assets-from-the-timeline}

1. From the Assets user interface, select the folder containing assets or specific assets to which you want to apply smart tags.
1. Tap/click the GlobalNav icon and open the timeline.
1. Tap/click the arrow at the bottom, and then tap/click **[!UICONTROL Start Workflow]**.
1. Select the **[!UICONTROL DAM Smart Tag Assets]** workflow, and specify a title for the workflow.
1. Tap/click **[!UICONTROL Start]**. The workflow applies your tags on assets. Navigate to the asset folder and review the tags to verify whether the Smart Content Service tagged your assets properly. For details, see [Managing Smart Tags](manage-smart-tags.md).

>[!NOTE]
>
>In the subsequent tagging cycles, only the modified assets are tagged again with newly-trained tags.
>
>However, even unaltered assets are tagged if the gap between the last and current tagging cycles for the tagging workflow exceeds 24 hours.
>
>For periodic tagging workflows, unaltered assets are tagged when the gap exceeds 6 months.


## Smart Content Service Training Guidelines {#smart-content-service-training-guidelines}

To be able to effectively tag your brand images, the Smart Content Service requires that the training images conform to certain guidelines. For best results, images in your training set should conform to the following guidelines:

**Quantity and size:** Minimum 30 images per tag. Minimum of 500 pixels on the longer side.

**Coherence**: Images for a tag should be visually similar.

For example, it is not a good idea to tag all of these images as `my-party` (for training) because they are not visually similar.

![Illustrative images to exemplify the guidelines for training](assets/do-not-localize/coherence.png)

**Coverage**: There should be sufficient variety in the images in the training. The idea is to supply a few but reasonably diverse examples so that AEM learns to focus on the right things. If you're applying the same tag on visually dissimilar images, include at least five examples of each kind.

For example, for the tag *model-down-pose*, include more training images similar to the highlighted image below for the service to identify similar images more accurately during tagging.

![Illustrative images to exemplify the guidelines for training](assets/do-not-localize/coverage_1.png)

**Distraction/obstruction**: The service trains better on images that have less distraction (prominent backgrounds, unrelated accompaniments, such as objects/persons with the main subject).

For example, for the tag *casual-shoe*, the second image is not a good training candidate.

![Illustrative images to exemplify the guidelines for training](assets/do-not-localize/distraction.png)

**Completeness:** If an image qualifies for more than one tag, add all applicable tags before including the image for training. For example, for tags, such as *raincoat* and *model-side-view*, add both the tags on the eligible asset before including it for training.

![Illustrative images to exemplify the guidelines for training](assets/do-not-localize/completeness.png)

### Training limitations {#limitations}

Enhanced smart tags are based on learning models of brand images and their tags. These models are not always perfect at identifying tags. The current version of the Smart Content Service has the following limitations:

* Inability to recognize subtle differences in images. For example, slim versus regular fitted shirts.
* Inability to identify tags based on tiny patterns/parts of an image. For example, logos on T-shirts.
* Tagging is supported in the locales that AEM is supported in. For a list of languages, see [Smart Content Services release notes](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/smart-content-service-release-notes.html).

To search for assets with smart tags (regular or enhanced), use the Assets Omnisearch (full-text search). There is no separate search predicate for smart tags. 

>[!NOTE]
>
>The ability of the Smart Content Service to train on your tags and apply them on other images depends on the quality of images you use for training. 
>
>For best results, Adobe recommends that you use visually similar images to train the service for each tag.

-->
