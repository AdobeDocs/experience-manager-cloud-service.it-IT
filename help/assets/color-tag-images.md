---
title: Tag colore per immagini
description: Experience Manager Assets consente di distinguere i colori in un’immagine e di applicarli automaticamente come tag. Puoi quindi utilizzare questi tag per cercare e filtrare le immagini.
exl-id: 3afa949b-ea1b-4b8e-ac94-06566e2c7147
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 8%

---

# Tag colore per immagini {#color-tag-images}

![Banner a colori](assets/banner-image.png)

Experience Manager Assets utilizza le funzionalità di intelligenza artificiale di Adobe Sensei per distinguere i colori in un’immagine e applicarli automaticamente come tag al momento dell’acquisizione. Questi tag consentono un’esperienza di ricerca avanzata, in base alla composizione del colore dell’immagine.

È possibile configurare il numero di colori (da 1 a 40) che vengono assegnati come tag in modo da poter cercare, in un secondo momento, le immagini in base a tali colori. Experience Manager Assets applica i tag in base alla copertura del colore in un’immagine. Puoi anche configurare il formato di visualizzazione per un tag colore.

La figura seguente illustra la sequenza di attività eseguite per configurare e gestire l’assegnazione di tag colore alle immagini in Experience Manager Assets:

![Applicazione di tag colore](assets/color-tagging-dfd.gif)

## Formati di file supportati {#supported-file-formats-color-tags}

| Formato file | Estensione | Tipo MIME | Spazio dei colori di ingresso | Dimensione massima del file di origine supportata | Risoluzione massima delle dimensioni dei file supportati |
|---|---|---|---|---|---|
| JPEG | .jpg, .jpeg | image/jpeg | sRGB | 15GB | 20000px X 20000px |
| PNG | .png | image/png | sRGB | 15GB | 20000px X 20000px |
| TIFF | .tif, .tiff | image/tiff | sRGB | 4 GB (limitati dalle specifiche del formato) | 20000px X 20000px |
| PSD | .psd | image/vnd.adobe.photoshop | sRGB | 2 GB (limitato dalle specifiche del formato) | 20000px X 20000px |
| GIF | .gif | image/gif | sRGB | 15GB | 20000px X 20000px |
| BMP | .bmp | image/bmp | sRGB | 4 GB (limitato dalle specifiche del formato) | 20000px X 20000px |

## Gestione delle proprietà di assegnazione tag colore {#manage-color-tagging-properties}

Per gestire le proprietà di assegnazione tag colore per le immagini:

1. Passa a **[!UICONTROL Strumenti > Risorse > Assegnazione tag colore]**.

   ![Proprietà dei tag colore](assets/color-tag-settings.png)

1. Specifica un formato di visualizzazione per il tag colore nel **[!UICONTROL Formato di visualizzazione]** campo . Le opzioni possibili includono il nome del colore, il RGB o il formato HEX.

1. Specifica il numero di colori a cui assegnare i tag per le immagini nella **[!UICONTROL Limite]** campo . Questi colori vengono visualizzati quando si visualizzano le proprietà di un&#39;immagine.  In questo campo è possibile definire un numero compreso tra uno e quaranta. Il valore predefinito per questo campo è dieci colori.

1. Specifica la percentuale minima di copertura del colore per includere un tag colore nei risultati della ricerca nel **[!UICONTROL Soglia copertura/posizione dominante %]** campo . Ad esempio, se la copertura del colore rosso in un’immagine è del 10% e si definisce il 9% in questo campo, l’immagine viene inclusa quando si cercano immagini con colore rosso. Tuttavia, se la copertura del colore rosso in un&#39;immagine è del 10% e si definisce l&#39;11% in questo campo, l&#39;immagine non viene inclusa quando si cercano immagini con colore rosso.

   In questo campo è possibile specificare un numero compreso tra cinque e cento. Il valore predefinito è undici.

   >[!NOTE]
   >
   >In questo campo, Adobe consiglia di utilizzare un valore prossimo al valore predefinito. L’impostazione di un valore di numero elevato impostato per questo campo (ad esempio, maggiore di 25) potrebbe restituire pochissimi risultati di ricerca. Analogamente, l’impostazione di un valore numerico basso (ad esempio, inferiore a 6) può restituire troppi risultati di ricerca, il che potrebbe non essere utile.

1. Fai clic su **[!UICONTROL Salva]**.


   >[!VIDEO](https://video.tv.adobe.com/v/340108)


### Disabilita assegnazione tag colore {#disable-color-tagging}

Per impostazione predefinita, l’assegnazione tag colore per le immagini è abilitata. È possibile disattivare l’assegnazione tag colore a livello di cartella. Tutte le cartelle secondarie ereditano le proprietà di assegnazione tag colore dalla cartella principale.

Per disabilitare l’assegnazione tag colore a livello di cartella:

1. Passa a **[!UICONTROL Adobe Experience Manager > Risorse > File]**.

1. Seleziona la cartella e fai clic su **[!UICONTROL Proprietà]**.

1. In **[!UICONTROL Elaborazione delle risorse]** , passa alla **[!UICONTROL Tag del colore per le immagini]** cartella. Selezionare uno dei seguenti valori dall’elenco a discesa:

   * Ereditato : la cartella eredita le opzioni di attivazione o disattivazione dalla cartella principale.

   * Abilita - Abilita l’assegnazione tag colore per la cartella selezionata.

   * Disabilita - Disattiva l&#39;assegnazione tag colore per la cartella selezionata.

   ![Impostazioni di assegnazione tag colore](assets/color-tags-folder.png)

## Configurare lo schema metadati per aggiungere il componente tag di colore avanzati {#configure-metadata-schema}

Gli schemi di metadati contengono campi specifici per informazioni specifiche da compilare. Contiene inoltre informazioni sul layout per visualizzare i campi di metadati in modo semplice e intuitivo. Le proprietà dei metadati includono titolo, descrizione, tipi MIME, tag e altro ancora. È possibile utilizzare [!UICONTROL Forms schema metadati] per modificare gli schemi esistenti o aggiungere schemi di metadati personalizzati.

>[!NOTE]
>
>Il campo Tag colore avanzato è disponibile nello schema metadati predefinito. Se si utilizza uno schema di metadati personalizzato, configurare lo schema per aggiungere un campo smart color tag.

Per aggiungere il componente Tag avanzati all’Editor modulo schema metadati:

1. Passa a **[!UICONTROL Strumenti > Risorse > Schemi di metadati]**.

1. Seleziona il nome dello schema e fai clic su **[!UICONTROL Modifica]**.

1. Trascina **[!UICONTROL Tag a colori avanzati]** dal **[!UICONTROL Crea modulo]** nella scheda **[!UICONTROL Editor moduli schema metadati]**.

1. Fai clic sul pulsante **[!UICONTROL Campo tag colore avanzato]** in **[!UICONTROL Editor moduli schema metadati]**.

1. Specifica un valore appropriato nella **[!UICONTROL Etichetta campo]** nel campo **[!UICONTROL Impostazioni]**  scheda .

1. Fai clic su **[!UICONTROL Salva]**.

   >[!VIDEO](https://video.tv.adobe.com/v/340124)

## Tag di colore per le immagini esistenti in DAM {#color-tags-existing-images}

Le immagini già esistenti in DAM non vengono taggate automaticamente in base al colore. Devi [!UICONTROL Rielaborazione delle risorse] per generare manualmente i tag colore.

Per colorare le immagini o le cartelle (comprese le sottocartelle) di risorse già esistenti nell’archivio delle risorse, effettua le seguenti operazioni:

1. Seleziona la [!DNL Adobe Experience Manager] , quindi seleziona le risorse dal [!UICONTROL Navigazione] pagina.

1. Seleziona [!UICONTROL File] per visualizzare l’interfaccia Assets.

1. Passa alla cartella alla quale desideri applicare i tag colore.

1. Seleziona l’intera cartella o le immagini specifiche.

1. Seleziona ![Icona Rielabora risorse](assets/do-not-localize/reprocess-assets-icon.png) [!UICONTROL Rielaborazione delle risorse] e seleziona la [!UICONTROL Processo completo] opzione .

Al termine del processo, passa alla [!UICONTROL Proprietà] di qualsiasi immagine all’interno della cartella. I tag aggiunti automaticamente vengono visualizzati in [!UICONTROL Tag a colori avanzati] sezione [!UICONTROL Base] scheda .


## Visualizzare tag di colore avanzati per le immagini {#view-color-tags}

Per visualizzare i tag colore avanzati per le immagini:

1. Passa a **[!UICONTROL Adobe Experience Manager > Risorse > File]**.

1. Fai clic sulla cartella appropriata e seleziona l’immagine.

1. Seleziona **[!UICONTROL Proprietà]** e visualizza i tag nel **[!UICONTROL Tag a colori avanzati]** campo .

   ![Visualizza tag colore](assets/view-color-tags.png)

   Passa il mouse su un tag colore per visualizzare il **[!UICONTROL Soglia copertura/posizione dominante %]** di un colore in un&#39;immagine.

## Configurare il predicato colore di AEM Assets {#configure-search-predicate}

Puoi configurare il filtro di ricerca per le immagini. Puoi quindi basare i criteri di ricerca su un colore specifico per filtrare i risultati.

>[!NOTE]
>
>Configura il predicato colore di AEM Assets solo se non utilizzi il modulo di ricerca predefinito.

Per configurare il filtro di ricerca, crea un predicato Colore risorsa utilizzando la barra di ricerca amministrazione risorse.

Per configurare il filtro di ricerca:

1. Passa a **[!UICONTROL Strumenti > Generale > Cerca in Forms]**.

1. Seleziona **[!UICONTROL Barra di ricerca amministrazione risorse]** e fai clic su **[!UICONTROL Modifica]**.

1. Trascina **[!UICONTROL Predicato colore risorsa]** dal **[!UICONTROL Seleziona predicato]** nella scheda **[!UICONTROL Editor moduli di ricerca]**.

1. Specifica un valore appropriato nella **[!UICONTROL Etichetta campo]** nel campo **[!UICONTROL Impostazioni]**  scheda .

1. Fai clic su **[!UICONTROL Fine]** per salvare le impostazioni.

   >[!VIDEO](https://video.tv.adobe.com/v/340110)

## Ricerca di immagini in base ai colori {#search-images-based-on-colors}

>[!VIDEO](https://video.tv.adobe.com/v/340761)

Dopo aver configurato tutte le proprietà di assegnazione tag colore e [configurazione del predicato a colori delle risorse](#search-images-based-on-colors), puoi cercare le immagini in base a un colore come filtro.

Per cercare le immagini in base ai colori:

1. Passa a **[!UICONTROL Risorse > File]**.

1. Seleziona **[!UICONTROL Filtro]** dall’elenco a discesa.
   ![Filtrare le risorse](assets/filter-assets.png)

1. Seleziona la [Predicato colore AEM Assets](#configure-search-predicate).

1. Trascinare il selettore colore per selezionare il colore appropriato. Il colore selezionato viene visualizzato nel campo di sola lettura disponibile sotto il selettore colore. È possibile selezionare RGB o HEX come formato di visualizzazione per il colore.

   ![Selettore colore](assets/color-picker-color-tags.png)

   È possibile filtrare le immagini in base alla selezione di un colore. Le immagini che hanno il colore selezionato come tag per i colori avanzati e al di sopra del [Soglia copertura/dominio %](#manage-color-tagging-settings) nel riquadro a destra.

1. Fai clic su x nella barra di ricerca per cancellare il filtro.

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
