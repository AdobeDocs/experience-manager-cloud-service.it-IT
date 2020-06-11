---
title: Metadati XMP
description: Scoprite lo standard di metadati XMP (Extensible Metadata Platform) per la gestione dei metadati. Viene utilizzato da AEM come formato standard per la creazione, l’elaborazione e lo scambio di metadati.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 496ad0831d20eb7653a3c5727999a2abc5728ec7
workflow-type: tm+mt
source-wordcount: '1483'
ht-degree: 16%

---


# Metadati XMP {#xmp-metadata}

XMP (Extensible Metadata Platform) è lo standard di metadati utilizzato da AEM Assets per la gestione di tutti i metadati. XMP fornisce un formato standard per la creazione, l&#39;elaborazione e lo scambio di metadati per un&#39;ampia gamma di applicazioni.

Oltre a offrire una codifica di metadati universale che può essere incorporata in tutti i formati di file, XMP offre un modello [di](#xmp-core-concepts) contenuto avanzato ed è [supportato da Adobe](#advantages-of-xmp) e da altre aziende, in modo che gli utenti di XMP, in combinazione con Risorse AEM, abbiano a disposizione una piattaforma potente su cui costruire.

## Panoramica XMP ed ecosistema {#xmp-ecosystem}

Risorse AEM supporta in modo nativo lo standard di metadati XMP. XMP è uno standard per l&#39;elaborazione e la memorizzazione di metadati standard e proprietari nelle risorse digitali. XMP è stato progettato per essere lo standard comune che consente a più applicazioni di lavorare in modo efficace con i metadati.

I professionisti della produzione, ad esempio, utilizzano il supporto XMP integrato nelle applicazioni Adobe per trasmettere informazioni in più formati di file. L’archivio di Risorse AEM estrae i metadati XMP e li utilizza per gestire il ciclo di vita del contenuto e offre la possibilità di creare flussi di lavoro di automazione.

XMP standardizza la modalità di definizione, creazione ed elaborazione dei metadati fornendo un modello dati, un modello di memorizzazione e schemi. Tutti questi concetti sono trattati in questa sezione.

Tutti i metadati legacy di EXIF, ID3 o Microsoft Office vengono automaticamente convertiti in XMP, che possono essere estesi per supportare lo schema di metadati specifico del cliente, ad esempio i cataloghi di prodotti.

I metadati in XMP sono costituiti da un set di proprietà. Tali proprietà sono sempre associate a un&#39;entità specifica denominata risorsa; in altre parole, le proprietà sono &quot;informazioni&quot; sulla risorsa. Nel caso di XMP, la risorsa è sempre la risorsa.

XMP definisce un modello di [metadati](https://it.wikipedia.org/wiki/Metadato) che può essere usato con qualsiasi insieme definito di elementi di metadati. XMP definisce anche [schemi](https://en.wikipedia.org/wiki/XML_schema) specifici per le proprietà di base, utili per registrare la cronologia di una risorsa, in quanto passano attraverso più fasi di elaborazione: dalla fotografia, dalla [scansione](https://it.wikipedia.org/wiki/Scanner_(informatica)) o creazione come testo, fino ai passaggi di modifica delle foto (come [ritaglio](https://en.wikipedia.org/wiki/Cropping_%28image%29) o regolazione colore), fino all’assemblaggio in un’immagine definitiva. XMP consente a ogni programma software o dispositivo di aggiungere le proprie informazioni a una risorsa digitale, che possono quindi essere poi mantenute nel file digitale finale.

XMP è spesso serializzato e memorizzato utilizzando un sottoinsieme del [W3C](https://it.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://it.wikipedia.org/wiki/Resource_Description_Framework) (RDF), che a sua volta è espresso in [XML](https://it.wikipedia.org/wiki/XML).

### Vantaggi di XMP {#advantages-of-xmp}

XMP presenta i seguenti vantaggi rispetto ad altri standard di codifica e schemi:

* I metadati basati su XMP sono molto potenti e granulari.
* XMP consente di avere più valori per una proprietà.
* XMP ha una codifica standard, che consente di scambiare facilmente i metadati.
* XMP è estensibile. Potete aggiungere ulteriori informazioni alle risorse.

Lo standard XMP è progettato per essere estensibile, consentendo di aggiungere tipi personalizzati di metadati ai dati XMP. EXIF, invece, non ha - ha un elenco fisso di proprietà che non può essere esteso.

>[!NOTE]
>
>XMP generalmente non consente l&#39;incorporamento di tipi di dati binari. Per poter includere dati binari in XMP, ad esempio immagini in miniatura, questi devono essere codificati in un formato adatto a XML, ad esempio `Base64`.

### Concetti di base XMP {#xmp-core-concepts}

**Spazi dei nomi e schemi**

Uno schema XMP è un insieme di nomi di proprietà in uno spazio nomi XML comune che include il tipo di dati e informazioni descrittive. Uno schema XMP è identificato dal relativo URI dello spazio dei nomi XML. L&#39;utilizzo di spazi dei nomi evita conflitti tra proprietà in schemi diversi con lo stesso nome ma con un significato diverso.

Ad esempio, la proprietà **Creatore** in due schemi progettati in modo indipendente potrebbe indicare la persona che ha creato la risorsa o l’applicazione che ha creato la risorsa (ad esempio, Adobe Photoshop).

**Proprietà e valori XMP**

XMP può includere proprietà di uno o più schemi. Ad esempio, un sottoinsieme tipico utilizzato da molte applicazioni Adobe potrebbe includere i seguenti elementi:

* Schema di base Dublino: `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`
* Schema di base XMP: `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`
* Schema di gestione diritti XMP: `xmpRights:WebStatement`, `xmpRights:Marked`
* Schema di gestione file multimediali XMP: `xmpMM:DocumentID`

**Lingue alternative**

XMP consente di aggiungere una `xml:lang` proprietà alle proprietà di testo per specificare la lingua del testo.

## Write-back XMP per le rappresentazioni {#xmp-writeback-to-renditions}

Questa funzione di riscrittura XMP in Risorse Adobe Experience Manager (AEM) replica le modifiche apportate ai metadati delle risorse alle rappresentazioni della risorsa.

Quando modificate i metadati di una risorsa da Risorse AEM o durante il caricamento di tale risorsa, le modifiche vengono inizialmente memorizzate all’interno del nodo della risorsa in CRXDE.

La funzione di riscrittura XMP propaga le modifiche ai metadati a tutte le rappresentazioni o a specifiche della risorsa.

Considerate uno scenario in cui modificate la proprietà [!UICONTROL Titolo] della risorsa `Classic Leather` con titolo `Nylon`.

![metadati](assets/metadata.png)

In questo caso, Risorse AEM salva le modifiche alla proprietà **[!UICONTROL Titolo]** nel `dc:title` parametro per i metadati delle risorse memorizzati nella gerarchia delle risorse.

![metadata_stored](assets/metadata_stored.png)

Tuttavia, Risorse AEM non propaga automaticamente le modifiche ai metadati apportate alle rappresentazioni di una risorsa.

La funzione di riscrittura XMP consente di estendere le modifiche ai metadati a tutte le rappresentazioni o a specifiche della risorsa. Tuttavia, le modifiche non vengono memorizzate sotto il nodo di metadati nella gerarchia delle risorse. Questa funzione incorpora invece le modifiche apportate ai file binari per le rappresentazioni.

### Abilita riscrittura XMP {#enable-xmp-writeback}

<!-- asgupta, Engg: Need attention here to update the configuration manager changes.
-->

Per abilitare la propagazione delle modifiche ai metadati alle rappresentazioni della risorsa al momento del caricamento, modificate la configurazione di **[!UICONTROL Adobe CQ DAM Rendition Maker]** in Configuration Manager.

1. Per aprire Configuration Manager, accedere `https://[aem_server]:[port]/system/console/configMgr`.
1. Aprite la configurazione di **[!UICONTROL Adobe CQ DAM Rendition Maker]** .
1. Selezionate l&#39;opzione **[!UICONTROL Propaga XMP]** , quindi salvate le modifiche.

### Abilita riscrittura XMP per rappresentazioni specifiche {#enable-xmp-writeback-for-specific-renditions}

Per consentire alla funzione di riscrittura XMP di estendere le modifiche ai metadati per selezionare le rappresentazioni, specificate queste rappresentazioni nel passaggio del flusso di lavoro del processo [!UICONTROL di riscrittura dei metadati] XMP del flusso di lavoro di riscrittura dei metadati DAM. Per impostazione predefinita, questo passaggio è configurato con la rappresentazione originale.

Per estendere i metadati alle miniature di rappresentazione 140.100.png e 319.319.png, effettuate le seguenti operazioni.

1. Tocca/fai clic sul logo AEM, quindi vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
1. Dalla pagina Modelli, aprite il modello di flusso di lavoro **[!UICONTROL DAM Metadata Writeback]** .
1. Nella pagina delle proprietà **[!UICONTROL Writeback di metadati DAM]**, apri il passaggio **[!UICONTROL Processo write-back XMPs]**.
1. Nella finestra di dialogo **[!UICONTROL Proprietà passaggio]**, tocca/fai clic sulla scheda **[!UICONTROL Processo]**.
1. Nella casella **[!UICONTROL Argomenti]** , aggiungete `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`, quindi toccate o fate clic su **[!UICONTROL OK]**.

   ![step_properties](assets/step_properties.png)

1. Salva le modifiche.
1. Per rigenerare le rappresentazioni TIFF piramidali (PTIFF) delle immagini Dynamic Media con i nuovi attributi, aggiungi il passaggio **[!UICONTROL Risorse di immagine di processo di elementi multimediali dinamici]** al flusso di lavoro immagine processo file multimediali dinamici al flusso di lavoro Writeback di metadati DAM. Le rappresentazioni PTIFF vengono create e memorizzate solo localmente in un’implementazione Dynamic Media Hybrid.

1. Salvare il flusso di lavoro.

Le modifiche ai metadati vengono propagate alle miniature delle rappresentazioni.140.100.png e thumbnail.319.319.png della risorsa, e non agli altri.

<!--
>[!NOTE]
>
>For XMP writeback issues in 64 bit Linux, see [How to enable XMP write-back on 64-bit RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>For more information about supported platforms, see [XMP metadata write-back prerequisites](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).
-->

### Filtrare i metadati XMP {#filtering-xmp-metadata}

AEM Assets supporta il filtro di proprietà/nodi per i metadati XMP letti dai file binari delle risorse e memorizzati in JCR quando le risorse vengono assimilate. Il filtraggio è possibile tramite un elenco bloccato e un elenco consentito.

Il filtraggio mediante un elenco bloccato consente di importare tutte le proprietà dei metadati XMP, ad eccezione delle proprietà specificate per l&#39;esclusione. Tuttavia, per i tipi di risorse come i file INDD con enormi quantità di metadati XMP (ad esempio, 1000 nodi con 10.000 proprietà), i nomi dei nodi da filtrare non sono sempre noti in anticipo. Se il filtro applicato a un elenco bloccato consente l’importazione di un gran numero di risorse con numerosi metadati XMP, l’istanza o il cluster di AEM può rilevare problemi di stabilità, ad esempio code di osservazione bloccate.

Il filtro dei metadati XMP tramite l&#39;elenco consentito risolve il problema consentendo di definire le proprietà XMP da importare. In questo modo, le altre proprietà XMP/sconosciute vengono ignorate. Per compatibilità con le versioni precedenti, potete aggiungere alcune di queste proprietà al filtro che utilizza un elenco bloccato.

>[!NOTE]
>
>Il filtro funziona solo per le proprietà derivate da origini XMP nei file binari delle risorse. Per le proprietà derivate da origini non XMP, come i formati EXIF e IPTC, il filtro non funziona. Ad esempio, la data di creazione delle risorse è memorizzata nella proprietà denominata `CreateDate` in EXIF TIFF. AEM rileva questo valore nel campo di metadati denominato `exif:DateTimeOriginal`. Poiché l&#39;origine è un&#39;origine non XMP, il filtraggio non funziona su questa proprietà.

1. Per aprire Configuration Manager, accedere `https://[aem_server]:[port]/system/console/configMgr`.
1. Aprite la configurazione **[!UICONTROL Adobe CQ DAM XmpFilter]** .
1. To apply filtering via an allowed list, select **[!UICONTROL Apply Whitelist to XMP Properties]**, and specify the properties to be imported in the **[!UICONTROL Whitelisted XML Names for XMP filtering]** box.

1. To filter out blocked XMP properties after applying filtering via allowed list, specify them in the **[!UICONTROL Blacklisted XML Names for XMP filtering]** box.

   >[!NOTE]
   >
   >L&#39;opzione **[!UICONTROL Applica lista nera alle proprietà]** XMP è selezionata per impostazione predefinita. In altre parole, il filtraggio utilizzando un elenco bloccato è attivato per impostazione predefinita. Per disattivare tale filtro, deselezionate l&#39;opzione **[!UICONTROL Applica lista nera alle proprietà]** XMP.

1. Salva le modifiche.

>[!MORELIKETHIS]
>
>* [Specifica XMP per Adobe](https://www.adobe.com/devnet/xmp.html)

