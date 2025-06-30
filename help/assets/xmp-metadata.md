---
title: Metadati XMP
description: Scopri lo standard dei metadati di XMP (Extensible Metadata Platform) per la gestione dei metadati. Viene utilizzato da Experience Manager come formato standardizzato per la creazione, l’elaborazione e l’interscambio di metadati.
contentOwner: AG
feature: Metadata
role: Admin, User
exl-id: fd9af408-d2a3-4c7a-9423-c4b69166f873
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 17%

---

# Metadati XMP {#xmp-metadata}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/xmp-writeback.html) |
| AEM as a Cloud Service | Questo articolo |

XMP (Extensible Metadata Platform) è lo standard di metadati utilizzato da Experience Manager Assets per la gestione di tutti i metadati. XMP fornisce un formato standard per la creazione, l&#39;elaborazione e lo scambio di metadati per un&#39;ampia gamma di applicazioni.

Oltre a offrire la codifica universale dei metadati che può essere incorporata in tutti i formati di file, XMP fornisce un [modello di contenuto](#xmp-core-concepts) avanzato ed è [supportato da Adobe](#advantages-of-xmp) e altre aziende, in modo che gli utenti di XMP in combinazione con [!DNL Assets] abbiano una piattaforma potente su cui basarsi.

## Panoramica ed ecosistema di XMP {#xmp-ecosystem}

[!DNL Assets] supporta in modo nativo lo standard dei metadati di XMP. XMP è uno standard per l&#39;elaborazione e l&#39;archiviazione di metadati standardizzati e proprietari in risorse digitali. XMP è progettato per essere lo standard comune che consente a più applicazioni di lavorare in modo efficace con i metadati.

I professionisti della produzione, ad esempio, utilizzano il supporto integrato di XMP nelle applicazioni Adobe per trasmettere informazioni in più formati di file. L&#39;archivio [!DNL Assets] estrae i metadati XMP e li utilizza per gestire il ciclo di vita dei contenuti e offre la possibilità di creare flussi di lavoro di automazione.

XMP standardizza il modo in cui i metadati vengono definiti, creati ed elaborati fornendo un modello di dati, un modello di archiviazione e schemi. Tutti questi concetti sono trattati in questa sezione.

Tutti i metadati legacy di EXIF, ID3 o Microsoft Office vengono automaticamente tradotti in XMP, che può essere esteso per supportare schemi di metadati specifici del cliente, ad esempio i cataloghi di prodotti.

I metadati in XMP sono costituiti da un set di proprietà. Queste proprietà sono sempre associate a una specifica entità definita risorsa, ovvero le proprietà riguardano la risorsa. Nel caso di XMP, la risorsa è sempre la risorsa.

XMP definisce un modello di [metadati](https://it.wikipedia.org/wiki/Metadato) che può essere usato con qualsiasi insieme definito di elementi di metadati. XMP definisce anche [schemi](https://en.wikipedia.org/wiki/XML_schema) specifici per le proprietà di base, utili per registrare la cronologia di una risorsa, in quanto passano attraverso più fasi di elaborazione: dalla fotografia, dalla [scansione](https://it.wikipedia.org/wiki/Scanner_(informatica)) o creazione come testo, fino ai passaggi di modifica delle foto (come [ritaglio](https://en.wikipedia.org/wiki/Cropping_%28image%29) o regolazione colore), fino all’assemblaggio in un’immagine definitiva. XMP consente a ogni programma software o dispositivo di aggiungere le proprie informazioni a una risorsa digitale, che possono quindi essere poi mantenute nel file digitale finale.

XMP è spesso serializzato e memorizzato utilizzando un sottoinsieme del [W3C](https://it.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://it.wikipedia.org/wiki/Resource_Description_Framework) (RDF), che a sua volta è espresso in [XML](https://it.wikipedia.org/wiki/XML).

### Vantaggi di XMP {#advantages-of-xmp}

XMP offre i seguenti vantaggi rispetto ad altri standard e schemi di codifica:

* I metadati basati su XMP sono molto potenti e granulari.
* XMP consente di avere più valori per una proprietà.
* XMP dispone di una codifica standardizzata che consente di scambiare facilmente i metadati.
* XMP è estensibile. Puoi aggiungere ulteriori informazioni alle risorse.

Lo standard XMP è progettato per essere estensibile e consente di aggiungere tipi personalizzati di metadati ai dati di XMP. EXIF, invece, no - ha un elenco fisso di proprietà che non possono essere estese.

>[!NOTE]
>
>XMP in genere non consente l’incorporamento di tipi di dati binari. Per inserire dati binari in XMP, ad esempio immagini di miniature, è necessario codificarli in un formato compatibile con XML, ad esempio `Base64`.

### Concetti di base di XMP {#xmp-core-concepts}

**Spazi dei nomi e schemi**

Uno schema di XMP è un insieme di nomi di proprietà in uno spazio dei nomi XML comune che include
il tipo di dati e le informazioni descrittive. Uno schema XMP è identificato dall&#39;URI dello spazio dei nomi XML. L’utilizzo degli spazi dei nomi evita conflitti tra proprietà in schemi diversi che hanno lo stesso nome ma un significato diverso.

Ad esempio, la proprietà **Creator** in due schemi progettati in modo indipendente potrebbe indicare la persona che ha creato la risorsa o l&#39;applicazione che ha creato la risorsa (ad esempio, Adobe Photoshop).

**Proprietà e valori di XMP**

XMP può includere proprietà da uno o più schemi. Ad esempio, un sottoinsieme tipico utilizzato da molte applicazioni Adobe potrebbe includere quanto segue:

* Schema di base Dublino: `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`
* Schema di base XMP: `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`
* Schema di XMP Rights Management: `xmpRights:WebStatement`, `xmpRights:Marked`
* Schema gestione supporti XMP: `xmpMM:DocumentID`

**Alternative linguistiche**

XMP consente di aggiungere una proprietà `xml:lang` alle proprietà di testo per specificare la lingua del testo.

## Write-back di XMP alle rappresentazioni {#xmp-writeback-to-renditions}

Questa funzionalità di writeback di XMP in [!DNL Adobe Experience Manager Assets] replica le modifiche ai metadati nelle rappresentazioni della risorsa originale.
Quando modifichi i metadati di una risorsa dall&#39;interno di [!DNL Assets] o durante il caricamento della risorsa, le modifiche vengono inizialmente memorizzate nel nodo metadati nella gerarchia della risorsa. La funzione di writeback consente di propagare le modifiche ai metadati a tutte le rappresentazioni o a rappresentazioni specifiche della risorsa. La funzionalità riscrive solo le proprietà dei metadati che utilizzano lo spazio dei nomi `jcr`, ovvero una proprietà denominata `dc:title` viene riscritta ma una proprietà denominata `mytitle` no.

Consideriamo ad esempio uno scenario in cui si modifica la proprietà [!UICONTROL Title] della risorsa con titolo `Classic Leather` in `Nylon`.

![metadati](assets/metadata.png)

In questo caso, [!DNL Assets] salva le modifiche alla proprietà **[!UICONTROL Title]** nel parametro `dc:title` per i metadati della risorsa memorizzati nella gerarchia della risorsa.

![metadati archiviati nel nodo della risorsa nell&#39;archivio](assets/metadata_stored.png)

>[!IMPORTANT]
>
>La funzionalità di writeback non è attivata per impostazione predefinita in [!DNL Assets]. Scopri come [abilitare il writeback dei metadati](#enable-xmp-writeback). MSM per risorse digitali non funziona se è abilitato il writeback dei metadati. Al writeback, l&#39;ereditarietà si interrompe.

### Abilita writeback di XMP {#enable-xmp-writeback}

Il flusso di lavoro [!UICONTROL Writeback di metadati DAM] viene utilizzato per eseguire il writeback dei metadati di una risorsa. Per abilitare il writeback, seguire uno dei tre metodi seguenti:

* Utilizza i moduli di avvio.
* Avvia manualmente il flusso di lavoro `DAM MetaData Writeback`.
* Configura il flusso di lavoro per la post-elaborazione.

Per utilizzare i moduli di avvio, effettua le seguenti operazioni:

1. Come amministratore, accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Moduli di avvio]**.
1. Selezionare il [!UICONTROL modulo di avvio] per il quale nella colonna **[!UICONTROL Flusso di lavoro]** viene visualizzato **[!UICONTROL Writeback di metadati DAM]**. Fare clic su **[!UICONTROL Proprietà]** nella barra degli strumenti.

   ![Selezionare il modulo di avvio del writeback dei metadati DAM per modificarne le proprietà e attivarlo](assets/launcher-properties-metadata-writeback1.png)

1. Selezionare **[!UICONTROL Attiva]** nella pagina **[!UICONTROL Proprietà modulo di avvio]**. Fai clic su **[!UICONTROL Salva e chiudi]**.

Per applicare manualmente il flusso di lavoro a una risorsa una sola volta, applica il flusso di lavoro [!UICONTROL Writeback di metadati DAM] dalla barra a sinistra.

Per applicare il flusso di lavoro a tutte le risorse caricate, aggiungi il flusso di lavoro a un profilo di post-elaborazione.

<!-- Commenting for now. Need to document how to enable metadata writeback. See CQDOC-17254.

### Enable XMP writeback {#enable-xmp-writeback}

To enable the metadata changes to be propagated to the renditions of the asset when uploading it, modify the **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration in Configuration Manager.

1. To open Configuration Manager, access `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration.
1. Select the **[!UICONTROL Propagate XMP]** option, and then save the changes.

### Enable XMP write-back for specific renditions {#enable-xmp-writeback-for-specific-renditions}

To let the XMP write-back feature propagate metadata changes to select renditions, specify these renditions to the [!UICONTROL XMP Writeback Process] workflow step of DAM Metadata WriteBack workflow. By default, this step is configured with the original rendition.

For the XMP write-back feature to propagate metadata to the rendition thumbnails 140.100.png and 319.319.png, perform these steps.

1. Select the Experience Manager logo, and then navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Workflow]** &gt; **[!UICONTROL Models]**.
1. From the Models page, open the **[!UICONTROL DAM Metadata Writeback]** workflow model.
1. In the **[!UICONTROL DAM Metadata Writeback]** properties page, open the **[!UICONTROL XMP Writeback Process]** step.
1. In the **[!UICONTROL Step Properties]** dialog box, select the **[!UICONTROL Process]** tab.
1. In the **[!UICONTROL Arguments]** box, add `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`, and then select **[!UICONTROL OK]**.

   ![step_properties](assets/step_properties.png)

1. Save the changes.
1. To regenerate the Pyramid TIFF (PTIFF) renditions for Dynamic Media images with the new attributes, add the **[!UICONTROL Dynamic Media Process Image Assets]** step to the DAM Metadata write-back workflow. PTIFF renditions are only created and stored locally in a Dynamic Media Hybrid implementation.

1. Save the workflow.

The metadata changes are propagated to the renditions renditions thumbnail.140.100.png and thumbnail.319.319.png of the asset, and not the others.
-->

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)
* [Pubblicare risorse in AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
