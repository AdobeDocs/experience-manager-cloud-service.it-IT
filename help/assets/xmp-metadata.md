---
title: Metadati XMP
description: Scoprite lo standard di metadati XMP (Extensible Metadata Platform) per la gestione dei metadati. Viene utilizzato da AEM come formato standard per la creazione, l’elaborazione e lo scambio di metadati.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0c915b32d676ff225cbe276be075d3ae1a865f11
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 21%

---


# Metadati XMP {#xmp-metadata}

XMP (Extensible Metadata Platform) è lo standard di metadati utilizzato da  AEM Assets per la gestione di tutti i metadati. XMP fornisce un formato standard per la creazione, l&#39;elaborazione e lo scambio di metadati per un&#39;ampia gamma di applicazioni.

Oltre a offrire una codifica universale dei metadati che può essere incorporata in tutti i formati di file, XMP fornisce un modello [di](#xmp-core-concepts) contenuto avanzato ed è [supportato da  Adobe](#advantages-of-xmp) e da altre aziende, in modo che gli utenti di XMP in combinazione con  AEM Assets abbiano una piattaforma potente su cui costruire.

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
>XMP generalmente non consente l&#39;incorporazione di tipi di dati binari. Per trasmettere dati binari in XMP, ad esempio, immagini in miniatura, è necessario codificarli in un formato XML adatto, ad esempio `Base64`.

### Concetti XMP {#xmp-core-concepts}

**Spazi dei nomi e schemi**

Uno schema XMP è un insieme di nomi di proprietà in uno spazio nomi XML comune che include il tipo di dati e informazioni descrittive. Uno schema XMP è identificato dal relativo URI dello spazio dei nomi XML. L&#39;utilizzo di spazi dei nomi evita conflitti tra proprietà in schemi diversi con lo stesso nome ma con un significato diverso.

Ad esempio, la proprietà **Creatore** in due schemi progettati in modo indipendente potrebbe indicare la persona che ha creato la risorsa o l’applicazione che ha creato la risorsa (ad esempio,  Adobe Photoshop).

**XMP proprietà e valori**

XMP possono includere proprietà di uno o più schemi. Ad esempio, un sottoinsieme tipico utilizzato da molte applicazioni  Adobe potrebbe includere i seguenti elementi:

* Schema di base Dublino: `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`
* XMP schema di base: `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`
* Schema di gestione dei diritti XMP: `xmpRights:WebStatement`, `xmpRights:Marked`
* XMP schema di gestione supporti: `xmpMM:DocumentID`

**Lingue alternative**

XMP consente di aggiungere una `xml:lang` proprietà alle proprietà di testo per specificare la lingua del testo.

## Write-back XMP per le rappresentazioni {#xmp-writeback-to-renditions}

Questa XMP funzione di riscrittura in Adobe Experience Manager (AEM) Assets replica le modifiche apportate ai metadati delle risorse alle rappresentazioni della risorsa.

Quando modificate i metadati di una risorsa dall’interno  AEM Assets o durante il caricamento della risorsa, le modifiche vengono inizialmente memorizzate all’interno del nodo della risorsa in CRXDE.

La funzione di XMP riscrittura propaga le modifiche ai metadati a tutte le rappresentazioni o a specifiche della risorsa.

Considerate uno scenario in cui modificate la proprietà [!UICONTROL Titolo] della risorsa `Classic Leather` con titolo `Nylon`.

![metadati](assets/metadata.png)

In questo caso, l’AEM Assets  salva le modifiche alla proprietà **[!UICONTROL Titolo]** nel `dc:title` parametro per i metadati delle risorse memorizzati nella gerarchia delle risorse.

![metadata_stored](assets/metadata_stored.png)

Tuttavia,  AEM Assets non propaga automaticamente le modifiche apportate ai metadati alle rappresentazioni di una risorsa.

La funzione di XMP riscrittura consente di estendere le modifiche ai metadati a tutte le rappresentazioni o a determinate rappresentazioni della risorsa. Tuttavia, le modifiche non vengono memorizzate sotto il nodo di metadati nella gerarchia delle risorse. Questa funzione incorpora invece le modifiche apportate ai file binari per le rappresentazioni.

### Abilita XMP riscrittura {#enable-xmp-writeback}

<!-- asgupta, Engg: Need attention here to update the configuration manager changes.
-->

Per abilitare la propagazione delle modifiche ai metadati alle rappresentazioni della risorsa al momento del caricamento, modificate la configurazione **[!UICONTROL Adobe CQ DAM Rendition Maker]** in Configuration Manager.

1. Per aprire Configuration Manager, accedere `https://[aem_server]:[port]/system/console/configMgr`.
1. Apri la configurazione **[!UICONTROL Adobe CQ DAM Rendition Maker]** .
1. Selezionate l’opzione **[!UICONTROL Propaga XMP]** , quindi salvate le modifiche.

### Abilita XMP riscrittura per rappresentazioni specifiche {#enable-xmp-writeback-for-specific-renditions}

Per consentire alla funzione di XMP di riscrittura di diffondere le modifiche ai metadati per selezionare le rappresentazioni, specificate queste rappresentazioni nel passaggio del flusso di lavoro [!UICONTROL XMP WriteBack del processo] di WriteBack dei metadati DAM. Per impostazione predefinita, questo passaggio è configurato con la rappresentazione originale.

Per estendere i metadati alle miniature delle rappresentazioni 140.100.png e 319.319.png XMP funzione di riscrittura, effettuate le seguenti operazioni.

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

>[!MORELIKETHIS]
>
>* [XMP specifica per Adobe](https://www.adobe.com/devnet/xmp.html)

