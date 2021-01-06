---
title: Metadati XMP
description: Scoprite lo standard di metadati XMP (Extensible Metadata Platform) per la gestione dei metadati. Viene utilizzato da AEM come formato standard per la creazione, l’elaborazione e lo scambio di metadati.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 8110259a910c891a5bcf7507cfa9897603a45c91
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 18%

---


# Metadati XMP {#xmp-metadata}

XMP (Extensible Metadata Platform) è lo standard di metadati utilizzato da  AEM Assets per la gestione di tutti i metadati. XMP fornisce un formato standard per la creazione, l&#39;elaborazione e lo scambio di metadati per un&#39;ampia gamma di applicazioni.

Oltre a offrire una codifica universale dei metadati che può essere incorporata in tutti i formati di file, XMP fornisce un modello di contenuto [ricco](#xmp-core-concepts) ed è [supportato da  Adobe](#advantages-of-xmp) e da altre aziende, in modo che gli utenti di XMP in combinazione con  AEM Assets possano contare su una piattaforma potente su cui realizzare l&#39;integrazione.

## Panoramica XMP ed ecosistema {#xmp-ecosystem}

 AEM Assets supporta in modo nativo lo standard di metadati XMP. XMP è uno standard per l’elaborazione e l’archiviazione di metadati standardizzati e proprietari nelle risorse digitali. XMP è stato progettato per essere lo standard comune che consente a più applicazioni di lavorare in modo efficace con i metadati.

I professionisti della produzione, ad esempio, utilizzano il supporto XMP integrato in  applicazioni  Adobi per trasmettere informazioni in più formati di file. L&#39;archivio  AEM Assets estrae i metadati XMP e li utilizza per gestire il ciclo di vita del contenuto e offre la possibilità di creare flussi di lavoro di automazione.

XMP standardizzare la modalità di definizione, creazione ed elaborazione dei metadati fornendo un modello dati, un modello di storage e schemi. Tutti questi concetti sono trattati in questa sezione.

Tutti i metadati legacy di EXIF, ID3 o Microsoft Office vengono automaticamente convertiti in XMP, che possono essere estesi per supportare lo schema di metadati specifico del cliente, ad esempio i cataloghi di prodotti.

I metadati in XMP sono composti da un set di proprietà. Tali proprietà sono sempre associate a un&#39;entità specifica denominata risorsa; in altre parole, le proprietà sono &quot;informazioni&quot; sulla risorsa. Nel caso di XMP, la risorsa è sempre la risorsa.

XMP definisce un modello di [metadati](https://it.wikipedia.org/wiki/Metadato) che può essere usato con qualsiasi insieme definito di elementi di metadati. XMP definisce anche [schemi](https://en.wikipedia.org/wiki/XML_schema) specifici per le proprietà di base, utili per registrare la cronologia di una risorsa, in quanto passano attraverso più fasi di elaborazione: dalla fotografia, dalla [scansione](https://it.wikipedia.org/wiki/Scanner_(informatica)) o creazione come testo, fino ai passaggi di modifica delle foto (come [ritaglio](https://en.wikipedia.org/wiki/Cropping_%28image%29) o regolazione colore), fino all’assemblaggio in un’immagine definitiva. XMP consente a ogni programma software o dispositivo di aggiungere le proprie informazioni a una risorsa digitale, che possono quindi essere poi mantenute nel file digitale finale.

XMP è spesso serializzato e memorizzato utilizzando un sottoinsieme del [W3C](https://it.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://it.wikipedia.org/wiki/Resource_Description_Framework) (RDF), che a sua volta è espresso in [XML](https://it.wikipedia.org/wiki/XML).

### Vantaggi di XMP {#advantages-of-xmp}

XMP offre i seguenti vantaggi rispetto ad altri standard di codifica e schemi:

* I metadati basati su XMP sono molto potenti e granulari.
* XMP consente di avere più valori per una proprietà.
* XMP una codifica standard, che consente di scambiare facilmente i metadati.
* XMP è estensibile. Potete aggiungere ulteriori informazioni alle risorse.

Lo standard XMP è progettato per essere estensibile e consente di aggiungere tipi personalizzati di metadati ai dati XMP. EXIF, invece, non ha - ha un elenco fisso di proprietà che non può essere esteso.

>[!NOTE]
>
>XMP generalmente non consente l&#39;incorporazione di tipi di dati binari. Per trasmettere dati binari in XMP, ad esempio, immagini in miniatura, è necessario codificarli in un formato adatto a XML, ad esempio `Base64`.

### Concetti di base XMP {#xmp-core-concepts}

**Spazi dei nomi e schemi**

Uno schema XMP è un insieme di nomi di proprietà in uno spazio dei nomi XML comune che include
il tipo di dati e le informazioni descrittive. Uno schema XMP è identificato dal relativo URI dello spazio dei nomi XML. L&#39;utilizzo di spazi dei nomi evita conflitti tra proprietà in schemi diversi con lo stesso nome ma con un significato diverso.

Ad esempio, la proprietà **Creator** in due schemi progettati in modo indipendente potrebbe indicare la persona che ha creato la risorsa o l&#39;applicazione che ha creato la risorsa (ad esempio,  Adobe Photoshop).

**XMP proprietà e valori**

XMP possono includere proprietà di uno o più schemi. Ad esempio, un sottoinsieme tipico utilizzato da molte applicazioni  Adobe potrebbe includere i seguenti elementi:

* Schema di base Dublino: `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`
* XMP schema di base: `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`
* Schema di gestione dei diritti XMP: `xmpRights:WebStatement`, `xmpRights:Marked`
* XMP schema di gestione supporti: `xmpMM:DocumentID`

**Lingue alternative**

XMP consente di aggiungere una proprietà `xml:lang` alle proprietà di testo per specificare la lingua del testo.

## Write-back XMP per le rappresentazioni {#xmp-writeback-to-renditions}

Questa funzione di XMP di riscrittura in Adobe Experience Manager (AEM) Assets replica le modifiche apportate ai metadati delle risorse alle rappresentazioni della risorsa.

Quando modificate i metadati di una risorsa dall’interno  AEM Assets o durante il caricamento della risorsa, le modifiche vengono inizialmente memorizzate all’interno del nodo della risorsa in CRXDE.

La funzione di XMP writeback propaga le modifiche ai metadati a tutte le rappresentazioni o a specifiche della risorsa.

Considerate uno scenario in cui modificate la proprietà [!UICONTROL Title] della risorsa denominata `Classic Leather` in `Nylon`.

![metadati](assets/metadata.png)

In questo caso, l&#39;AEM Assets  salva le modifiche alla proprietà **[!UICONTROL Title]** nel parametro `dc:title` per i metadati delle risorse memorizzati nella gerarchia delle risorse.

![metadata_stored](assets/metadata_stored.png)

Tuttavia,  AEM Assets non propaga automaticamente le modifiche apportate ai metadati alle rappresentazioni di una risorsa.

La funzione di XMP remix consente di estendere le modifiche ai metadati a tutte le rappresentazioni o a specifiche della risorsa. Tuttavia, le modifiche non vengono memorizzate sotto il nodo di metadati nella gerarchia delle risorse. Questa funzione incorpora invece le modifiche apportate ai file binari per le rappresentazioni.

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

>[!MORELIKETHIS]
>
>* [XMP specifica per Adobe ](https://www.adobe.com/devnet/xmp.html)

