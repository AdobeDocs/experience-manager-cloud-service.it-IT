---
title: Metadati XMP
description: Scopri lo standard di metadati XMP (Extensible Metadata Platform) per la gestione dei metadati. Viene utilizzato da AEM come formato standard per la creazione, l'elaborazione e lo scambio di metadati.
contentOwner: AG
translation-type: tm+mt
source-git-commit: c3da535db4bf2b0f71e338f542d388437d6c1623
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 16%

---


# Metadati XMP {#xmp-metadata}

XMP (Extensible Metadata Platform) è lo standard di metadati utilizzato da AEM Assets per la gestione di tutti i metadati. XMP fornisce un formato standard per la creazione, l&#39;elaborazione e lo scambio di metadati per un&#39;ampia varietà di applicazioni.

Oltre ad offrire una codifica universale dei metadati che può essere incorporata in tutti i formati di file, XMP fornisce un [modello di contenuto ](#xmp-core-concepts) e è [supportato da Adobe](#advantages-of-xmp) e da altre aziende, in modo che gli utenti di XMP in combinazione con AEM Assets abbiano una piattaforma potente su cui basarsi.

## Panoramica XMP ed ecosistema {#xmp-ecosystem}

AEM Assets supporta in modo nativo lo standard di metadati XMP. XMP è uno standard per l’elaborazione e l’archiviazione di metadati standardizzati e proprietari nelle risorse digitali. XMP è stato progettato per essere lo standard comune che consente a più applicazioni di lavorare in modo efficace con i metadati.

I professionisti della produzione, ad esempio, utilizzano il supporto integrato XMP all&#39;interno delle applicazioni Adobe per trasmettere informazioni in più formati di file. L’archivio AEM Assets estrae i metadati XMP e li utilizza per gestire il ciclo di vita dei contenuti e offre la possibilità di creare flussi di lavoro di automazione.

XMP standardizza il modo in cui i metadati vengono definiti, creati ed elaborati fornendo un modello di dati, un modello di archiviazione e schemi. Tutti questi concetti sono trattati in questa sezione.

Tutti i metadati legacy di EXIF, ID3 o Microsoft Office vengono automaticamente tradotti in XMP, che possono essere estesi per supportare lo schema di metadati specifico del cliente, ad esempio i cataloghi di prodotti.

I metadati in XMP sono costituiti da un insieme di proprietà. Tali proprietà sono sempre associate a una specifica entità indicata come risorsa; in altre parole, le proprietà riguardano la risorsa. Nel caso di XMP, la risorsa è sempre la risorsa.

XMP definisce un modello di [metadati](https://it.wikipedia.org/wiki/Metadato) che può essere usato con qualsiasi insieme definito di elementi di metadati. XMP definisce anche [schemi](https://en.wikipedia.org/wiki/XML_schema) specifici per le proprietà di base, utili per registrare la cronologia di una risorsa, in quanto passano attraverso più fasi di elaborazione: dalla fotografia, dalla [scansione](https://it.wikipedia.org/wiki/Scanner_(informatica)) o creazione come testo, fino ai passaggi di modifica delle foto (come [ritaglio](https://en.wikipedia.org/wiki/Cropping_%28image%29) o regolazione colore), fino all’assemblaggio in un’immagine definitiva. XMP consente a ogni programma software o dispositivo di aggiungere le proprie informazioni a una risorsa digitale, che possono quindi essere poi mantenute nel file digitale finale.

XMP è spesso serializzato e memorizzato utilizzando un sottoinsieme del [W3C](https://it.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://it.wikipedia.org/wiki/Resource_Description_Framework) (RDF), che a sua volta è espresso in [XML](https://it.wikipedia.org/wiki/XML).

### Vantaggi di XMP {#advantages-of-xmp}

XMP presenta i seguenti vantaggi rispetto ad altri standard di codifica e schemi:

* I metadati basati su XMP sono molto potenti e precisi.
* XMP consente di avere più valori per una proprietà.
* XMP codifica standard, che consente di scambiare facilmente i metadati.
* XMP estensibile. Puoi aggiungere ulteriori informazioni alle risorse.

Lo standard XMP è progettato per essere estensibile e consente di aggiungere tipi personalizzati di metadati ai dati di XMP. EXIF, d&#39;altro canto, no - ha un elenco fisso di proprietà che non può essere esteso.

>[!NOTE]
>
>XMP generalmente non consente l&#39;incorporazione di tipi di dati binari. Per trasportare i dati binari in XMP, ad esempio, le immagini in miniatura, devono essere codificati in un formato compatibile con XML come `Base64`.

### Concetti di base XMP {#xmp-core-concepts}

**Namespace e schemi**

Uno schema XMP è un insieme di nomi di proprietà in uno spazio dei nomi XML comune che include
il tipo di dati e le informazioni descrittive. Uno schema XMP è identificato dal relativo URI dello spazio dei nomi XML. L’utilizzo di spazi dei nomi evita conflitti tra proprietà in schemi diversi con lo stesso nome ma con un significato diverso.

Ad esempio, la proprietà **Creatore** in due schemi progettati in modo indipendente potrebbe indicare la persona che ha creato la risorsa o l’applicazione che ha creato la risorsa (ad esempio, Adobe Photoshop).

**Proprietà e valori XMP**

XMP possono includere proprietà di uno o più schemi. Ad esempio, un sottoinsieme tipico utilizzato da molte applicazioni di Adobe potrebbe includere quanto segue:

* Schema di base Dublino: `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`
* Schema di base XMP: `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`
* Schema di gestione dei diritti XMP: `xmpRights:WebStatement`, `xmpRights:Marked`
* XMP schema di gestione file multimediali: `xmpMM:DocumentID`

**Alternative linguistiche**

XMP consente di aggiungere una proprietà `xml:lang` alle proprietà di testo per specificare la lingua del testo.

## Write-back XMP per le rappresentazioni {#xmp-writeback-to-renditions}

Questa funzione di XMP write-back in [!DNL Adobe Experience Manager Assets] replica le modifiche ai metadati alle rappresentazioni della risorsa originale.
Quando modifichi i metadati di una risorsa dall’interno di Assets o durante il caricamento della risorsa, le modifiche vengono inizialmente memorizzate nel nodo di metadati nella gerarchia delle risorse.

La funzione di XMP write-back consente di propagare le modifiche ai metadati a tutte le rappresentazioni o a specifiche della risorsa. La funzione riscrive solo le proprietà dei metadati che utilizzano lo spazio dei nomi `jcr`, ovvero viene riscritta una proprietà denominata `dc:title` ma non una proprietà denominata `mytitle`.

Ad esempio, considera uno scenario in cui modifichi la proprietà [!UICONTROL Title] della risorsa denominata `Classic Leather` in `Nylon`.

![Metadati](assets/metadata.png)

In questo caso, [!DNL Assets] salva le modifiche alla proprietà **[!UICONTROL Title]** nel parametro `dc:title` per i metadati delle risorse memorizzati nella gerarchia delle risorse.

![metadati memorizzati nel nodo risorsa nell’archivio](assets/metadata_stored.png)

>[!NOTE]
>
>La funzione di ripristino non è abilitata per impostazione predefinita in [!DNL Assets]. Scopri come [abilitare il writeback dei metadati](#enable-xmp-writeback).

### Abilita XMP writeback {#enable-xmp-writeback}

[!UICONTROL Il flusso di lavoro ] Writebackeraggio metadati DAM viene utilizzato per riscrivere i metadati di una risorsa. Per abilitare il write-back, segui questi passaggi:

1. In qualità di amministratore, accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Moduli di avvio]**.
1. Seleziona il [!UICONTROL Launcher] per il quale la colonna **[!UICONTROL Flusso di lavoro]** visualizza **[!UICONTROL Writeback di metadati DAM]**. Fai clic su **[!UICONTROL Proprietà]** nella barra degli strumenti.

   ![Seleziona DAM metadata writeback launcher per modificarne le proprietà e attivarlo](assets/launcher-properties-metadata-writeback1.png)

1. Seleziona **[!UICONTROL Attiva]** nella pagina **[!UICONTROL Proprietà di avvio]** . Fai clic su **[!UICONTROL Salva e chiudi]**.

Per applicare questo flusso di lavoro a una risorsa una sola volta, applica il flusso di lavoro [!UICONTROL Writeback di metadati DAM] dalla barra a sinistra. Per applicare il flusso di lavoro a tutte le risorse caricate, aggiungi il flusso di lavoro a un profilo di post-elaborazione.

<!-- Commenting for now. Need to document how to enable metadata writeback. See CQDOC-17254.

### Enable XMP writeback {#enable-xmp-writeback}
-->

<!-- asgupta, Engg: Need attention here to update the configuration manager changes. -->

<!-- 
To enable the metadata changes to be propagated to the renditions of the asset when uploading it, modify the **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration in Configuration Manager.

1. To open Configuration Manager, access `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration.
1. Select the **[!UICONTROL Propagate XMP]** option, and then save the changes.

### Enable XMP write-back for specific renditions {#enable-xmp-writeback-for-specific-renditions}

To let the XMP write-back feature propagate metadata changes to select renditions, specify these renditions to the [!UICONTROL XMP Writeback Process] workflow step of DAM Metadata WriteBack workflow. By default, this step is configured with the original rendition.

For the XMP write-back feature to propagate metadata to the rendition thumbnails 140.100.png and 319.319.png, perform these steps.

1. Tap/click the AEM logo, and then navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Workflow]** &gt; **[!UICONTROL Models]**.
1. From the Models page, open the **[!UICONTROL DAM Metadata Writeback]** workflow model.
1. In the **[!UICONTROL DAM Metadata Writeback]** properties page, open the **[!UICONTROL XMP Writeback Process]** step.
1. In the **[!UICONTROL Step Properties]** dialog box, tap/click the **[!UICONTROL Process]** tab.
1. In the **[!UICONTROL Arguments]** box, add `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`, and then tap/click **[!UICONTROL OK]**.

   ![step_properties](assets/step_properties.png)

1. Save the changes.
1. To regenerate the Pyramid TIFF (PTIFF) renditions for Dynamic Media images with the new attributes, add the **[!UICONTROL Dynamic Media Process Image Assets]** step to the DAM Metadata write-back workflow. PTIFF renditions are only created and stored locally in a Dynamic Media Hybrid implementation.

1. Save the workflow.

The metadata changes are propagated to the renditions renditions thumbnail.140.100.png and thumbnail.319.319.png of the asset, and not the others.
-->
