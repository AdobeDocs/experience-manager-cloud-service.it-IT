---
title: Integrare [!DNL AEM Assets] durante la creazione di contenuto per [!DNL Edge Delivery Services]
description: Scopri come integrare il [!DNL AEM Assets] con [!DNL Edge Delivery Services]. This integration enables you to integrate [!DNL AEM Assets]  [!DNL Microsoft Word] e [!DNL Google Docs], integrate [!DNL AEM Assets] con [!DNL Universal Editor], integrate [!DNL Dynamic Media]  [!DNL Edge Delivery Services], integrate [!DNL Dynamic Media with OpenAPI capabilities]  [!DNL Universal Editor] con e integrare [!DNL Dynamic Media with OpenAPI capabilities] con [!DNL Microsoft Word] e. [!DNL Google Docs]
tags: "AEM Assets""Edge Delivery Services""Dynamic Media""Dynamic Media with OpenAPI capabilities""Universal Editor""Edge Delivery Services with Universal Editor"
features: "How to use [!DNL  AEM Assets] with [!DNL Edge Delivery Services]""How to use [!DNL AEM Assets] with [!DNL Universal Editor]""How to use [!DNL Dynamic Media with OpenAPI capabilities] with [!DNL Edge Delivery Services]""How to use [!DNL Dynamic Media with OpenAPI capabilities] in [!DNL Universal Editor]""How to integrate [!DNL Universal Editor] with [!DNL Edge Delivery Services] and [!DNL AEM Assets]""How to use [!DNL Dynamic Media with OpenAPI capabilities] in document based authoring tools""How to use [!DNL AEM Assets] in [!DNL Microsoft word] and [!DNL Google docs]""How to use [!DNL Universal Editor] with [!DNL Edge Delivery Services]""How to use [!DNL Dynamic Media with OpenAPI capabilities] in [!DNL Microsoft word] and [!DNL Google docs]""How to use [!DNL Dynamic Media] for asset delivery in document based authoring tools and [!DNL Universal Editor]"
exl-id: e58db2ce-a55a-49b3-ae8e-709b5ea8d095
source-git-commit: 3d333fb7b6304c5e0d9898bd9fbd947e54d2e7e1
workflow-type: tm+mt
source-wordcount: 671
ht-degree: 6%

---


# Integrare [!DNL AEM Assets] durante la creazione di contenuto per [!DNL Edge Delivery Services] {#integrate-aem-assets-with-edge-delivery-services}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime e Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>Estensibilità dell’interfaccia utente</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Novità</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Abilitare Dynamic Media Prime e Ultimate</b></a>
        </td>
         <td>
            <a href="/help/assets/search-best-practices.md"><b>Best practice per la ricerca</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Best practice per i metadati</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funzionalità OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentazione di AEM Assets per sviluppatori</b></a>
        </td>
    </tr>
</table>

![Integrazione di AEM Assets con Universal Editor](/help/assets/assets/EDS2.png)

[[!DNL Edge Delivery Services]](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/edge-delivery/overview) è un insieme componibile di servizi che consente un elevato grado di flessibilità nel modo in cui si creano e distribuiscono i contenuti sul sito Web. Puoi utilizzare sia la [gestione dei contenuti di AEM](/help/sites-cloud/authoring/author-publish.md) che la [creazione di WYSIWYG utilizzando  [!DNL Universal Editor] sia l&#39;authoring basato su documenti](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring).

Puoi modificare contenuto in:

* [[!DNL Microsoft Word] o [!DNL Google Docs]](#integrate-dynamic-media-with-edge-delivery-services)
* [[!DNL Universal Editor]](#integrate-aem-assets-with-universal-editor-UE)

Dopo aver modificato il contenuto, è possibile pubblicare a Servizi di distribuzione Edge.

## Integrazione [!DNL AEM Assets] con flussi di authoring basati su documenti per [!DNL Edge Delivery Services] {#integrate-dynamic-media-with-edge-delivery-services}

Quando [!DNL AEM Assets] si integra con gli strumenti di authoring basati su documenti, ad esempio [!DNL Microsoft Word] o [!DNL Google Docs], fornisce un selettore di risorse nello strumento di authoring. Utilizza questo selettore risorse per accedere a [!DNL AEM Assets] e inserire nel contenuto le risorse approvate.
Se disponi già di un sito Web [!DNL Edge Delivery Services], consulta la documentazione del [[!DNL AEM Assets] plugin](https://github.com/adobe-rnd/aem-assets-plugin/blob/main/README.md) per scoprire come integrare [!DNL AEM Assets] con il progetto [!DNL AEM] esistente.
Segui le seguenti [sezioni sui prerequisiti](#integrate-aem-assets-with-microsoft-word-and-google-docs) e [sull&#39;integrazione [!DNL AEM Assets] con l&#39;ambiente di authoring basato su documenti](#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs) se non disponi di un sito Web [!DNL Edge Delivery Services] per pubblicare il contenuto inclusivo [!DNL AEM Assets] creato con gli strumenti di authoring basati su documenti.

### Prerequisiti{#integrate-aem-assets-with-microsoft-word-and-google-docs}

Prima di iniziare, assicurati che il tuo ambiente di authoring basato su documenti sia pronto:

* Esegui l&#39;integrazione [!DNL AEM] con un strumento di authoring basato su documenti per impostare il ambiente di authoring. Per informazioni su come configurare il ambiente di authoring, consulta [Guida introduttiva - Esercitazione](https://www.aem.live/developer/tutorial) per sviluppatori.

### Integrazione [!DNL AEM Assets] con l&#39;ambiente di authoring basato su documenti{#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs}

Configurare il plug-in di Sidekick [!DNL AEM Assets] per utilizzare le risorse durante l&#39;authoring dei contenuti in [!DNL Microsoft Word] o [!DNL Google Docs].

* Per informazioni su come accedere e utilizzare AEM Assets in Microsoft Word o Google Docs, vedere [[!DNL Adobe Experience Manager Assets Sidekick Plugin]](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-experience-manager-assets-for-website-authors).
* Per informazioni dettagliate sulla configurazione, vedere [Configurazione di [!DNL Adobe Experience Manager Assets Sidekick Plugin]](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin).
  ![utilizza dynamic media con funzionalità openAPI in ms word e google docs](/help/assets/assets/my-assets-sidebar.png)

## Consegna risorse tramite [!DNL Dynamic Media with OpenAPI capabilities] {#integrate-Dynamic-Media-with-OpenAPI-capabilities-with-Microsoft-Word-Google-Docs-and-universal-editor}

È inoltre possibile utilizzare le risorse consegnate tramite [!DNL Dynamic Media with OpenAPI capabilities]. Offre molti vantaggi come:

* Accesso solo a risorse approvati da marchio (immagini, video, PDF e altri tipi di risorsa) da [!DNL AEM Assets Cloud Services].
* Governance (riferimenti o copie del risorsa), che facilita la propagazione automatica degli eventi del ciclo di vita risorsa like scadenza, eliminazione e aggiornamenti.
* Rappresentazioni dinamiche delle immagini e Smart Ritaglio.
* Ottimizzazione e distribuzione di media avanzate, ad esempio streaming video adattivo pronto all&#39;uso e distribuzione risorsa originale per PDF.
* Rapporto impression a livello di risorsa ([disponibilità limitata](/help/assets/manage-reports-assets-view.md#dynamic-media-delivery-reports)).

Per ulteriori dettagli sulle funzionalità, consulta [[!DNL Dynamic Media with OpenAPI capabilities]](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview) la documentazione.

### Prerequisiti {#dynamic-media-with-universal-editor-and-edge-delivery-services}

Per utilizzare risorsa riferimento, è necessario disporre di:

* Abilitazione a un ambiente Cloud Service Assets in cui [!DNL Dynamic Media with Open API capabilities] è abilitata.
* Una [!DNL Dynamic Media] licenza.
* [!DNL AEM Assets sidekick plugin] abilitato con riferimento di copia per le risorse immagine abilitate. Per ulteriori dettagli, consulta [questa documentazione](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin#copymode) per l&#39;authoring basato su documenti e [questa documentazione](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview) per l&#39;authoring basato su Universal Editor.
* Assets che sono approvati. Le risorse approvate hanno `dam:status=Approved` tramite il backend o le azioni dell&#39;interfaccia utente di Assets Cloud Services.

### Utilizzare le risorse consegnate tramite [!DNL Dynamic Media with OpenAPI capabilities]{#Using-Dynamic-Media-with-edge-delivery-services}

Selezionare i collegamenti seguenti per scoprire come utilizzare [!DNL Dynamic Media with OpenAPI capabilities] per distribuire immagini, video e altri tipi di risorse nel contenuto:

* [Aggiungi immagini al contenuto](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-image-references-when-authoring-content)
* [Aggiungi video al contenuto](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-video-references-when-authoring-content)
* [Aggiungi al contenuto risorse non di immagine e video quali PDF, file ZIP e altro ancora](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-asset-references-for-pdf-zip-etc-when-authoring-content)

Guarda questo video per scoprire come distribuire le risorse nel contenuto utilizzando Dynamic Media con funzionalità OpenAPI.

>[!VIDEO](https://video.tv.adobe.com/v/3441155)

## Sito [!DNL Edge Delivery Services] di esempio{#dynamic-media-with-google-docs-and-ms-word}

Vedi [WKND Travel](http://bit.ly/3DExLnf), un sito creato utilizzando le funzionalità di authoring basato su documenti di [!DNL Edge Delivery Services]. Il contenuto del sito viene creato in [Google Documenti](https://drive.google.com/drive/folders/1HCCHRWp4HJIXW_cUv5cRDQ5DzzqiZsXT) e [!DNL Dynamic Media with OpenAPI capabilities] viene utilizzato per fornire risorse in contenuto. Dopo la creazione, il contenuto viene pubblicato direttamente dal documento. Esplora questo [archivio](https://github.com/hlxsites/franklin-assets-selector/tree/aem-dynamicmedia-demo/blocks) Git per conoscere tutti i file, le cartelle, le configurazioni, lo stile e i codici di funzionalità del sito Web essenziali utilizzati per creare l&#39;impostazione di authoring basato su documenti per questo [!DNL Edge Delivery Services (EDS)] sito.

## Integrazione [!DNL AEM Assets] con [!DNL Universal Editor] flussi di authoring basati per [!DNL Edge Delivery Services] {#integrate-aem-assets-with-universal-editor-UE}

Impostare l&#39;impostazione per [!DNL Universal Editor] integrare con [!DNL AEM Assets]. Questa integrazione consente di utilizzare [!DNL Dynamic Media with OpenAPI capabilities] per distribuire le risorse.

* Consulta [Configurazione in [!DNL Edge Delivery] Sito](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#configuration-in-edge-delivery-site) per scoprire come aggiungere una funzione di selezione risorse personalizzata in [!DNL Universal Editor]. Il selettore risorse personalizzato consente di inserire direttamente le risorse nel contenuto di [!DNL Universal Editor].
* Per informazioni su come accedere a [!DNL AEM Assets] e inserire le risorse durante la creazione in [!DNL Universal Editor], consulta la [Panoramica dell&#39;estensione](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview).
