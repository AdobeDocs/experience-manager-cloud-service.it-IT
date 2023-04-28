---
title: Organizzazione delle risorse digitali
description: Organizza le risorse digitali, le immagini, i file, le cartelle e così via tramite Experience Manager.
contentOwner: AG
feature: Asset Management, Search
role: User
exl-id: 6b3ce076-2dd9-47f6-9b68-4fa52bfedd42
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 3%

---

# Organizzazione delle risorse digitali {#organize-digital-assets}

Tutte le risorse digitali, i metadati e i contenuti dei documenti Microsoft® Office e PDF vengono estratti e resi ricercabili. La ricerca consente un filtraggio sofisticato delle risorse e rispetta completamente le autorizzazioni appropriate. I metadati sono descritti in dettaglio in Metadata in Digital Asset Management.

[!DNL Experience Manager Assets] supporta diversi modi per organizzare i contenuti. È possibile organizzarle in modo gerarchico utilizzando le cartelle oppure in modo non ordinato e ad hoc, ad esempio i tag. Gli utenti possono modificare i tag nell’editor risorse DAM in cui vengono visualizzate risorse secondarie, rappresentazioni e metadati.

<!-- Commenting to pull down the existing content before applying changes wrt CQDOC-15930
## Create folders {#create-folders}

When organizing a collection of assets, for example, all *Nature* images, you can create folders to keep them together. You can use folders to categorize and organize your assets. [!DNL Assets] does not require you to organize assets in folders to work better.

>[!NOTE]
>
>Sharing an Assets folder (in Marketing Cloud) of the type `sling:OrderedFolder`, is not supported. If you want to share a folder, do not select Ordered when creating a folder.

1. Navigate to the place in your digital assets folder where you want to create a new folder.
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

You can use folders or tags or both to organize assets. Adding tags to assets makes them more easy to retrieve during a search. To add tags to an asset, follow these steps:

1. In the Digital Asset Manager, double-click the asset to open it.
1. In the **Tags** area, open the menu to reveal the available tags. Select tags as appropriate. To delete a tag, hover the pointer over the tag and click `X` to delete it.
1. Click **Save** to save any tags you added.

Date24/08/2021
-->

## Organizzare le risorse nelle cartelle {#organize-using-folders}

Il modo più semplice per organizzare le risorse è quello di salvarle nelle cartelle. È simile all&#39;organizzazione di file in cartelle nel file system locale. Per ulteriori informazioni su come creare e gestire le cartelle, consulta [Gestire le risorse](manage-digital-assets.md). Le modalità di denominazione di file e cartelle, di organizzazione delle sottocartelle e di gestione dei file all’interno di queste cartelle possono avere un impatto significativo sulle modalità di elaborazione di tali risorse. Utilizzando strategie di denominazione dei file e delle cartelle coerenti e appropriate, oltre a buone pratiche in materia di metadati, puoi sfruttare al massimo l’archivio delle risorse digitali.

* Di solito, l’archivio delle risorse digitali cresce sempre. Pertanto, è importante formalizzare l’uso dei metadati, la struttura delle cartelle e la denominazione dei file all’inizio del ciclo di creazione dei contenuti.
* Utilizza solo le cartelle per imporre una struttura di archiviazione coerente per le risorse digitali. Questa coerenza consente di elaborare e gestire meglio le risorse. Ad esempio, le risorse posizionate nei seguenti tipi di cartelle possono essere utili per separare le risorse:

   * **Cartelle di sviluppo**: contiene risorse digitali su cui stai lavorando.
   * **Cartelle client**: contiene risorse digitali basate su client o nomi di progetto.
   * **Cartelle principali**: contiene risorse digitali originali di origine.
   * **Cartelle di rendering**: contiene rappresentazioni e copie delle risorse digitali originali di origine.
   * **Cartelle Dimensione file**: contiene risorse digitali basate su file di piccole, medie o grandi dimensioni.
   * **Cartelle di staging**: contiene risorse digitali pronte per la pubblicazione live sul sito web.
   * **Cartelle di tipo MIME**: contiene risorse digitali specifiche per i tipi MIME come immagini, documenti e elementi multimediali.
   * **Archiviare le cartelle**: contiene risorse digitali in pensione.
   * **Cartelle basate su data**: contiene risorse digitali in base a una data di creazione o a un’ultima data di modifica.

* Crea una directory di cartelle che non è probabile modificare in modo che qualsiasi personalizzazione o automazione continui a funzionare. Ad esempio, i profili di elaborazione assegnati continuano a funzionare.
* Se una risorsa è già stata pubblicata, puoi utilizzare [!DNL Experience Manager] per spostare la risorsa in un’altra cartella e ripubblicarla dalla nuova posizione. La posizione originale della risorsa pubblicata è ancora disponibile insieme alla nuova risorsa ripubblicata. La risorsa pubblicata originale, tuttavia, è *smarrito* a [!DNL Experience Manager] e non può essere annullata la pubblicazione. Di conseguenza, come best practice, prima annulla la pubblicazione di una risorsa e poi spostala in un’altra cartella.

## Organizzare le risorse utilizzando i tag {#use-tags-to-organize-assets}

L’aggiunta di tag alle risorse li rende più facili da recuperare durante una ricerca, creare raccolte utilizzando i risultati della ricerca, aumentare la classificazione della ricerca per alcune risorse e applicare gli algoritmi AI di Adobe Sensei per l’individuazione delle risorse.

[!DNL Adobe Experience Manager Assets] utilizza un algoritmo di apprendimento automatico per creare tag altamente descrittivi che consentono di trovare la risorsa giusta in pochi clic. L’assegnazione tag avanzati utilizza Adobe Sensei, l’intelligenza artificiale e il framework di apprendimento automatico, che possono essere addestrati a riconoscere e applicare tag standard e specifici per il business alle immagini. I tag avanzati possono inoltre identificare contenuti, singole parole o frasi e applicare automaticamente tag descrittivi alle risorse.

Di seguito sono riportati i passaggi per aggiungere tag a una risorsa:

1. Accedi a [!DNL Experience Manager Assets].
1. Fai clic su **[!UICONTROL Risorse]** > **[!UICONTROL File]**, seleziona la risorsa e fai clic su **[!UICONTROL Proprietà]** per aprire le proprietà della risorsa.
1. In **[!UICONTROL Base]** , fai clic sull’icona della cartella in **[!UICONTROL Tag]** metadati. Viene visualizzata una finestra a comparsa.
1. Cerca o seleziona i tag appropriati dai tag esistenti in `cq-tags`. Puoi assegnare più tag alla risorsa.

   Puoi ordinare la struttura dei tag in ordine crescente o decrescente in base a **[!UICONTROL Nome]** (ordine alfabetico), **[!UICONTROL Creato]** data, oppure **[!UICONTROL Modificato]** data. Nell’illustrazione seguente, la struttura dei tag viene ordinata in ordine alfabetico in base alla variabile **[!UICONTROL Nome]**.

   ![add-tags](assets/add-tags-to-asset.png)

1. Fai clic su **Salva** per aggiornare le modifiche ai metadati della risorsa.

Per ulteriori informazioni, consulta i seguenti articoli:

* [Modificare i metadati delle risorse](meta-edit.md)
* [Tag avanzati nelle risorse](smart-tags.md)
* [Aggiungi un predicato tag al pannello di ricerca](/help/assets/search-facets.md/#adding-a-tags-predicate)

## Organizza come raccolte {#organize-as-collections}

Con le raccolte di risorse in [!DNL Experience Manager Assets], puoi semplificare la possibilità di creare, modificare e condividere risorse tra gli utenti. Crea diversi tipi di raccolte in base al modo in cui le utilizzi, incluse le raccolte che contengono un elenco di riferimento statico di risorse, cartelle e raccolte e le raccolte che richiamano le risorse in base ai criteri di ricerca. Puoi creare raccolte con risorse da posizioni diverse e condividerle con più utenti con diversi livelli di accesso, visualizzazione e modifica.

Per ulteriori informazioni, consulta [gestire le raccolte](manage-collections.md)


## Utilizzare i profili per organizzare le risorse {#organize-to-use-profiles}

Un profilo di elaborazione contiene [!DNL Assets] elaborazione di comandi applicabili alle risorse caricate in cartelle predefinite. I profili vengono utilizzati per automatizzare l’elaborazione del contenuto di una cartella o di risorse appena caricate. Puoi utilizzare i profili per organizzare meglio le risorse.

La standardizzazione dell’utilizzo dei metadati, della denominazione dei file e della struttura delle cartelle consente di applicare profili di elaborazione alle cartelle con maggiore precisione e coerenza man mano che cresce il pool di risorse digitali.

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
>* [Utilizzare i microservizi delle risorse e i profili di elaborazione](asset-microservices-configure-and-use.md)
>* [Profili metadati](metadata-profiles.md)
>* [Profili video](/help/assets/dynamic-media/video-profiles.md)
>* [Profili immagine Dynamic Media](/help/assets/dynamic-media/image-profiles.md)


