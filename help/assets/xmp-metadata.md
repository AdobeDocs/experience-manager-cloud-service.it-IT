---
title: Metadati XMP
description: Scoprite lo standard XMP (Extensible Metadata Platform) per la gestione dei metadati. Viene utilizzato da AEM come formato standard per la creazione, l’elaborazione e lo scambio di metadati.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Metadati XMP {#xmp-metadata}

XMP (Extensible Metadata Platform) è lo standard di metadati utilizzato da AEM Assets per la gestione di tutti i metadati. XMP fornisce un formato standard per la creazione, l&#39;elaborazione e lo scambio di metadati per un&#39;ampia gamma di applicazioni.

Oltre a offrire una codifica di metadati universale che può essere incorporata in tutti i formati di file, XMP offre un modello [di](#xmp-core-concepts) contenuto avanzato ed è [supportato da Adobe](#advantages-of-xmp) e da altre aziende, in modo che gli utenti di XMP, in combinazione con Risorse AEM, possano sfruttare una piattaforma potente.

## Panoramica XMP ed ecosistema {#xmp-ecosystem}

Risorse AEM supporta in modo nativo lo standard di metadati XMP. XMP è uno standard per l&#39;elaborazione e la memorizzazione di metadati standard e proprietari nelle risorse digitali. XMP è stato progettato per essere lo standard comune che consente a più applicazioni di lavorare in modo efficace con i metadati.

I professionisti della produzione, ad esempio, utilizzano il supporto XMP integrato nelle applicazioni Adobe per trasmettere informazioni in più formati di file. L’archivio di Risorse AEM estrae i metadati XMP e li utilizza per gestire il ciclo di vita del contenuto e offre la possibilità di creare flussi di lavoro di automazione.

XMP standardizza la modalità di definizione, creazione ed elaborazione dei metadati fornendo un modello dati, un modello di memorizzazione e schemi. Tutti questi concetti sono trattati in questa sezione.

Tutti i metadati legacy di EXIF, ID3 o Microsoft Office vengono automaticamente convertiti in XMP, che possono essere estesi per supportare lo schema di metadati specifico del cliente, ad esempio i cataloghi di prodotti.

I metadati in XMP sono costituiti da un set di proprietà. Tali proprietà sono sempre associate a un&#39;entità specifica denominata risorsa; in altre parole, le proprietà sono &quot;informazioni&quot; sulla risorsa. Nel caso di XMP, la risorsa è sempre la risorsa.

XMP definisce un modello di [metadati](https://en.wikipedia.org/wiki/Metadata) che può essere utilizzato con qualsiasi insieme definito di elementi di metadati. XMP definisce anche [schemi](https://en.wikipedia.org/wiki/XML_schema) specifici per le proprietà di base utili per registrare la cronologia di una risorsa, passando attraverso più fasi di elaborazione, dalla fotografia, dalla [scansione](https://en.wikipedia.org/wiki/Image_scanner)o creazione come testo, ai passaggi di modifica delle foto (come [ritaglio](https://en.wikipedia.org/wiki/Cropping_%28image%29) o regolazione del colore), all&#39;assemblaggio in un&#39;immagine finale. XMP consente a ogni programma software o dispositivo di aggiungere le proprie informazioni a una risorsa digitale, che può quindi essere mantenuta nel file digitale finale.

XMP è più comunemente serializzato e memorizzato utilizzando un sottoinsieme del [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF), che a sua volta è espresso in [XML](https://en.wikipedia.org/wiki/XML).

### Vantaggi di XMP {#advantages-of-xmp}

XMP presenta i seguenti vantaggi rispetto ad altri standard di codifica e schemi:

* I metadati basati su XMP sono molto potenti e granulari.
* XMP consente di avere più valori per una proprietà.
* XMP ha una codifica standard, che consente di scambiare facilmente i metadati.
* XMP è estensibile. Potete aggiungere ulteriori informazioni alle risorse.

Lo standard XMP è progettato per essere estensibile, consentendo di aggiungere tipi personalizzati di metadati ai dati XMP. EXIF, invece, non ha - ha un elenco fisso di proprietà che non può essere esteso.

>[!NOTE]
>
>XMP generalmente non consente l&#39;incorporamento di tipi di dati binari. Per poter includere dati binari in XMP, ad esempio immagini in miniatura, questi devono essere codificati in un formato XML adatto, ad esempio `Base64`.

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

Quando modificate i metadati di una risorsa da Risorse AEM o durante il caricamento di tale risorsa, le modifiche vengono inizialmente memorizzate nel nodo della risorsa in CRXDE.

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

1. Toccate/fate clic sul logo AEM, quindi accedete a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso]** di lavoro > **[!UICONTROL Modelli]**.
1. Dalla pagina Modelli, aprite il modello di flusso di lavoro **[!UICONTROL DAM Metadata Writeback]** .
1. Nella pagina delle proprietà Write **[!UICONTROL dei metadati]** DAM, aprite il passaggio **[!UICONTROL XMP Writeback Process]** .
1. Nella finestra di dialogo Proprietà **** passaggio, toccate/fate clic sulla scheda **[!UICONTROL Processo]** .
1. Nella casella **[!UICONTROL Argomenti]** , aggiungete `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`, quindi toccate o fate clic su **[!UICONTROL OK]**.

   ![step_properties](assets/step_properties.png)

1. Salva le modifiche.
1. Per rigenerare le rappresentazioni TIFF (PTIFF) piramidali per le immagini di elementi multimediali dinamici con i nuovi attributi, aggiungete il passaggio **[!UICONTROL Risorse]** immagine processo file multimediali dinamici al flusso di lavoro di riscrittura dei metadati DAM. Le rappresentazioni PTIFF vengono create e memorizzate solo localmente in un’implementazione Dynamic Media Hybrid.

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

AEM Assets supporta sia il filtro in blacklist che quello nella whitelist di proprietà/nodi per i metadati XMP letti dai binari delle risorse e memorizzati in JCR quando vengono assimilate le risorse.

Il filtro Blacklist consente di importare tutte le proprietà dei metadati XMP, ad eccezione delle proprietà specificate per l&#39;esclusione. Tuttavia, per i tipi di risorse come i file INDD con enormi quantità di metadati XMP (ad esempio, 1000 nodi con 10.000 proprietà), i nomi dei nodi da filtrare non sono sempre noti in anticipo. Se il filtraggio della blacklist consente di importare un gran numero di risorse con numerosi metadati XMP, l’istanza o il cluster AEM può incontrare problemi di stabilità, ad esempio code di osservazione bloccate.

Il filtro whitelist dei metadati XMP risolve questo problema consentendo di definire le proprietà XMP da importare. In questo modo, le altre proprietà XMP/sconosciute vengono ignorate. È possibile aggiungere alcune di queste proprietà al filtro blacklist per garantire la compatibilità con le versioni precedenti.

>[!NOTE]
>
>Il filtro funziona solo per le proprietà derivate da origini XMP nei file binari delle risorse. Per le proprietà derivate da origini non XMP, come i formati EXIF e IPTC, il filtro non funziona. Ad esempio, la data di creazione delle risorse è memorizzata nella proprietà denominata `CreateDate` in EXIF TIFF. AEM rileva questo valore nel campo di metadati denominato `exif:DateTimeOriginal`. Poiché l&#39;origine è un&#39;origine non XMP, il filtraggio non funziona su questa proprietà.

1. Per aprire Configuration Manager, accedere `https://[aem_server]:[port]/system/console/configMgr`.
1. Aprite la configurazione **[!UICONTROL Adobe CQ DAM XmpFilter]** .
1. Per applicare il filtro della whitelist, selezionate **[!UICONTROL Applica whitelist alle proprietà]** XMP e specificate le proprietà da importare nella casella Nomi XML **[!UICONTROL Whitelist per il filtro]** XMP.

1. Per filtrare le proprietà XMP in blacklist dopo aver applicato il filtro della whitelist, specificatele nella casella Nomi XML **[!UICONTROL in blacklist per il filtro]** XMP.

   >[!NOTE]
   >
   >L&#39;opzione **[!UICONTROL Applica lista nera alle proprietà]** XMP è selezionata per impostazione predefinita. In altre parole, il filtro della blacklist è attivato per impostazione predefinita. Per disattivare il filtro della blacklist, deselezionate l&#39;opzione **[!UICONTROL Applica lista nera alle proprietà]** XMP.

1. Salva le modifiche.

>[!MORELIKETHIS]
>
>* [Specifica XMP per Adobe](https://www.adobe.com/devnet/xmp.html)