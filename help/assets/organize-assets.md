---
title: Organizzazione delle risorse digitali
description: Organizza risorse digitali, immagini, file, cartelle e così via utilizzando Experience Manager.
contentOwner: AG
feature: Asset Management, Best Practices
role: User
exl-id: 6b3ce076-2dd9-47f6-9b68-4fa52bfedd42
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 6%

---

# Organizzazione delle risorse digitali {#organize-digital-assets}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/organize-assets.html?lang=en) |
| AEM as a Cloud Service | Questo articolo |

Tutte le risorse digitali, i metadati e il contenuto dei documenti di Microsoft® Office e PDF vengono estratti e resi ricercabili. La ricerca consente un filtro sofisticato sulle risorse e rispetta completamente le autorizzazioni appropriate. I metadati sono descritti in dettaglio in Metadati in Gestione delle risorse digitali.

[!DNL Experience Manager Assets] supporta più modalità di organizzazione del contenuto. Puoi organizzarli in modo gerarchico utilizzando le cartelle oppure in modo non ordinato e ad hoc, ad esempio i tag. Gli utenti possono modificare i tag nell’Editor risorse DAM in cui vengono visualizzate le risorse secondarie, le rappresentazioni e i metadati.

<!-- Commenting to pull down the existing content before applying changes wrt CQDOC-15930
## Create folders {#create-folders}

When organizing a collection of assets, for example, all *Nature* images, you can create folders to keep them together. You can use folders to categorize and organize your assets. [!DNL Assets] does not require you to organize assets in folders to work better.

>[!NOTE]
>
>Sharing an Assets folder (in Marketing Cloud) of the type `sling:OrderedFolder`, is not supported. If you want to share a folder, do not select Ordered when creating a folder.

1. Navigate to the place in your digital assets folder where you want to create a folder.
1. In the menu, click **[!UICONTROL Create]**. Select **[!UICONTROL New Folder]**.
1. In the **[!UICONTROL Title]** field, provide a folder name. By default, DAM uses the title that you provided as the folder name. Once the folder is created, you can override the default and specify another folder name.
1. Click **[!UICONTROL Create]**. Your folder is displayed in the digital assets folder.

## Add CUG properties to folders {#add-cug-properties-to-folders}

You can limit who can access certain folders in Assets by making the folder part of a closed user group (CUG). To make a folder part of a CUG:

1. In Assets, right-click the folder you want to add closed user group properties for and select **Properties**.  
1. Click the **CUG** tab.
1. Select the **Enabled** check box to make the folder and its assets available only to a closed user group.  
1. Browse to the login page, if there is one, to add that information. Add admitted groups by clicking **Add item**. If necessary, add the realm. Click **OK** to save your changes.

## Use tags to organize assets {#use-tags-to-organize-assets}

You can use folders or tags or both to organize assets. Adding tags to assets makes them easier to retrieve during a search. To add tags to an asset, follow these steps:

1. In the Digital Asset Manager, double-click the asset to open it.
1. In the **Tags** area, open the menu to reveal the available tags. Select tags as appropriate. To delete a tag, hover the pointer over the tag and click `X` to delete it.
1. Click **Save** to save any tags you added.

Date24/08/2021
-->

## Organizzare le risorse in cartelle {#organize-using-folders}

Il modo più semplice per organizzare le risorse consiste nel salvarle in cartelle. È simile all’organizzazione dei file nelle cartelle nel file system locale. Per ulteriori informazioni su come creare e gestire le cartelle, consulta [Gestire le risorse](manage-digital-assets.md). Il modo in cui denominate i file e le cartelle, organizzate le sottocartelle e gestite i file all’interno di queste cartelle può avere un impatto significativo sul modo in cui tali risorse vengono elaborate. Utilizzando strategie di denominazione di file e cartelle coerenti e appropriate, insieme a una buona pratica sui metadati, puoi sfruttare al massimo l’archivio delle risorse digitali.

* Di solito, l’archivio delle risorse digitali è sempre in crescita. Pertanto, è importante formalizzare l’uso dei metadati, la struttura delle cartelle e la denominazione dei file nelle prime fasi del ciclo di creazione dei contenuti.
* Utilizza le cartelle solo per imporre una struttura di archiviazione coerente per le risorse digitali. Questa coerenza aiuta il processo e gestisce meglio le risorse. Ad esempio, le risorse posizionate nei seguenti tipi di cartelle possono essere utili per separare le risorse:

   * **Cartelle di sviluppo**: contiene risorse digitali su cui si sta lavorando.
   * **Cartelle client**: contiene risorse digitali basate sui client o sui nomi dei progetti.
   * **Cartelle primarie**: contiene risorse digitali originali di origine.
   * **Cartelle di rendering**: contiene copie trasformate e copie delle risorse digitali originali di origine.
   * **Cartelle dimensioni file**: contiene risorse digitali basate su file di dimensioni piccole, medie o grandi.
   * **Cartelle di gestione temporanea**: contiene risorse digitali pronte per la pubblicazione live sul sito Web.
   * **Cartelle di tipo MIME**: contiene risorse digitali specifiche per i tipi MIME, ad esempio immagini, documenti e file multimediali.
   * **Archivia cartelle**: contiene risorse digitali ritirate.
   * **Cartelle basate sulla data**: contiene risorse digitali basate su una data di creazione o su una data dell&#39;ultima modifica.

* Crea una directory di cartelle che non dovrebbero essere modificate in modo che qualsiasi personalizzazione o automazione continui a funzionare. Ad esempio, i profili di elaborazione assegnati continuano a funzionare.
* Se una risorsa è già pubblicata, puoi utilizzare [!DNL Experience Manager] per spostarla in un&#39;altra cartella e ripubblicarla dal nuovo percorso. La posizione originale della risorsa pubblicata è ancora disponibile insieme alla risorsa appena ripubblicata. La risorsa pubblicata originale, tuttavia, è *perduta* in [!DNL Experience Manager] e non può essere annullata. Pertanto, come best practice, devi prima annullare la pubblicazione di una risorsa e quindi spostarla in un’altra cartella.

## Organizzare le risorse utilizzando i tag {#use-tags-to-organize-assets}

L’aggiunta di tag alle risorse ne semplifica il recupero durante una ricerca, la creazione di raccolte utilizzando i risultati della ricerca, l’aumento della classificazione di ricerca per alcune risorse e l’applicazione di algoritmi di intelligenza artificiale di Adobe Sensei per l’individuazione delle risorse.

[!DNL Adobe Experience Manager Assets] utilizza un algoritmo di apprendimento automatico per creare tag altamente descrittivi che consentono di trovare la risorsa giusta con pochi clic. L’assegnazione tag avanzati utilizza Adobe Sensei, l’intelligenza artificiale e il framework di apprendimento automatico, che possono essere addestrati per riconoscere e applicare tag standard e specifici per l’azienda alle immagini. I tag avanzati possono inoltre identificare contenuti, singole parole o frasi e applicare automaticamente tag descrittivi alle risorse.

Di seguito è descritta la procedura per aggiungere tag a una risorsa:

1. Accedi a [!DNL Experience Manager Assets].
1. Fai clic su **[!UICONTROL Assets]** > **[!UICONTROL File]**, seleziona la risorsa e fai clic su **[!UICONTROL Proprietà]** per aprire le proprietà della risorsa.
1. Nella scheda **[!UICONTROL Base]**, fai clic sull&#39;icona della cartella nei metadati **[!UICONTROL Tag]**. Viene visualizzata una finestra popup.
1. Cerca o seleziona i tag appropriati dai tag esistenti in `cq-tags`. Puoi assegnare più tag alla risorsa.

   Puoi ordinare la struttura dei tag in ordine crescente o decrescente in base alla data **[!UICONTROL Name]** (ordine alfabetico), **[!UICONTROL Created]** o **[!UICONTROL Modified]**. Nell&#39;illustrazione seguente, la struttura dei tag è ordinata alfabeticamente in base al **[!UICONTROL Nome]**.

   ![add-tags](assets/add-tags-to-asset.png)

1. Fai clic su **Salva** per aggiornare le modifiche ai metadati della risorsa.

Per ulteriori informazioni, consulta i seguenti articoli:

* [Modificare i metadati delle risorse](meta-edit.md)
* [Tag avanzati in Assets](smart-tags.md)
* [Aggiungere il predicato tag al pannello di ricerca](/help/assets/search-facets.md#adding-a-tags-predicate)

## Organizza come raccolte {#organize-as-collections}

Con le raccolte di risorse in [!DNL Experience Manager Assets], è possibile semplificare la creazione, la modifica e la condivisione delle risorse tra gli utenti. Crea diversi tipi di raccolte in base al modo in cui le utilizzi, incluse le raccolte che contengono un elenco di riferimento statico di risorse, cartelle e raccolte e le raccolte che richiamano le risorse in base ai criteri di ricerca. Puoi creare raccolte con risorse da posizioni diverse e condividerle con più utenti con diversi livelli di accesso, visualizzazione e modifica dei privilegi.

Per ulteriori informazioni, vedere [gestire le raccolte](manage-collections.md)


## Utilizzare i profili per organizzare le risorse {#organize-to-use-profiles}

Un profilo di elaborazione contiene [!DNL Assets] comandi di elaborazione applicabili alle risorse caricate in cartelle predefinite. I profili vengono utilizzati per automatizzare l’elaborazione del contenuto di una cartella o delle risorse appena caricate. Puoi utilizzare i profili per organizzare meglio le risorse.

La standardizzazione dell’utilizzo dei metadati, della denominazione dei file e della struttura delle cartelle garantisce che, man mano che il pool di risorse digitali cresce, sia possibile applicare profili di elaborazione alle cartelle con maggiore precisione e coerenza.

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi di metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)
* [Pubblicare risorse in AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Utilizzare i microservizi delle risorse e i profili di elaborazione](asset-microservices-configure-and-use.md)
>* [Profili metadati](metadata-profiles.md)
>* [Profili video](/help/assets/dynamic-media/video-profiles.md)
>* [Profili immagine Dynamic Media](/help/assets/dynamic-media/image-profiles.md)

