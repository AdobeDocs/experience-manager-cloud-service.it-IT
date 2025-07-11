---
title: Integra [!DNL AEM Assets] durante l'authoring del contenuto per [!DNL Edge Delivery Services]
description: Scopri come integrare  [!DNL AEM Assets] con [!DNL Edge Delivery Services]. This integration enables you to integrate [!DNL AEM Assets] con [!DNL Microsoft Word] e [!DNL Google Docs], integrate [!DNL AEM Assets] con [!DNL Universal Editor], integrate [!DNL Dynamic Media] con [!DNL Edge Delivery Services], integrate [!DNL Dynamic Media with OpenAPI capabilities] con [!DNL Universal Editor] e integrare [!DNL Dynamic Media with OpenAPI capabilities] con [!DNL Microsoft Word] e [!DNL Google Docs].
tags: AEM Assets, Edge Delivery Services, Dynamic Media, Dynamic Media with OpenAPI capabilities, Universal Editor, Edge Delivery Services with Universal Editor
exl-id: e58db2ce-a55a-49b3-ae8e-709b5ea8d095
source-git-commit: 79213bcfe5c5ccf7c60a31e6cb757f60a0ba87a7
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 0%

---


# Integra [!DNL AEM Assets] durante l&#39;authoring dei contenuti per [!DNL Edge Delivery Services] {#integrate-aem-assets-with-edge-delivery-services}

![Integrazione di AEM Assets con Universal Editor](/help/assets/assets/EDS2.png)

[[!DNL Edge Delivery Services]](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/edge-delivery/overview) è un insieme componibile di servizi che consente un elevato grado di flessibilità nel modo in cui si creano e distribuiscono i contenuti sul sito Web. Puoi utilizzare sia la [gestione dei contenuti di AEM](/help/sites-cloud/authoring/author-publish.md) che la [creazione di WYSIWYG utilizzando  [!DNL Universal Editor] sia l&#39;authoring basato su documenti](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring).

Puoi modificare il contenuto in:

* [[!DNL Microsoft Word] o  [!DNL Google Docs]](#integrate-dynamic-media-with-edge-delivery-services)
* [[!DNL Universal Editor]](#integrate-aem-assets-with-universal-editor-UE)

Dopo aver modificato il contenuto, puoi pubblicarlo in Edge Delivery Services.

## Integrazione di [!DNL AEM Assets] con flussi di authoring basati su documenti per [!DNL Edge Delivery Services] {#integrate-dynamic-media-with-edge-delivery-services}

Quando [!DNL AEM Assets] si integra con gli strumenti di authoring basati su documenti, ad esempio [!DNL Microsoft Word] o [!DNL Google Docs], fornisce un selettore di risorse nello strumento di authoring. Utilizza questo selettore risorse per accedere a [!DNL AEM Assets] e inserire nel contenuto le risorse approvate.
Se disponi già di un sito Web [!DNL Edge Delivery Services], consulta la documentazione del [[!DNL AEM Assets] plugin](https://github.com/adobe-rnd/aem-assets-plugin/blob/main/README.md) per scoprire come integrare [!DNL AEM Assets] con il progetto [!DNL AEM] esistente.
Segui le seguenti [sezioni sui prerequisiti](#integrate-aem-assets-with-microsoft-word-and-google-docs) e [sull&#39;integrazione [!DNL AEM Assets] con l&#39;ambiente di authoring basato su documenti](#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs) se non disponi di un sito Web [!DNL Edge Delivery Services] per pubblicare il contenuto inclusivo [!DNL AEM Assets] creato con gli strumenti di authoring basati su documenti.

### Prerequisiti{#integrate-aem-assets-with-microsoft-word-and-google-docs}

Prima di iniziare, accertati che l’ambiente di authoring basato su documenti sia pronto:

* Integra [!DNL AEM] con uno strumento di authoring basato su documenti per configurare l&#39;ambiente di authoring. Consulta [Guida introduttiva - Esercitazione per sviluppatori](https://www.aem.live/developer/tutorial) per scoprire come configurare l&#39;ambiente di authoring.

### Integrazione di [!DNL AEM Assets] con l&#39;ambiente di authoring basato su documenti{#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs}

Configurare il plug-in di Sidekick [!DNL AEM Assets] per utilizzare le risorse durante l&#39;authoring dei contenuti in [!DNL Microsoft Word] o [!DNL Google Docs].

* Per informazioni su come accedere e utilizzare AEM Assets in Microsoft Word o Google Docs, vedere [[!DNL Adobe Experience Manager Assets Sidekick Plugin]](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-experience-manager-assets-for-website-authors).
* Per informazioni dettagliate sulla configurazione, vedere [Configurazione di [!DNL Adobe Experience Manager Assets Sidekick Plugin]](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin).
  ![utilizza dynamic media con funzionalità openAPI in ms word e google docs](/help/assets/assets/my-assets-sidebar.png)

## Consegna risorse tramite [!DNL Dynamic Media with OpenAPI capabilities] {#integrate-Dynamic-Media-with-OpenAPI-capabilities-with-Microsoft-Word-Google-Docs-and-universal-editor}

È inoltre possibile utilizzare le risorse consegnate tramite [!DNL Dynamic Media with OpenAPI capabilities]. Offre numerosi vantaggi, tra cui:

* Accedi solo alle risorse approvate dal marchio (immagini, video, PDF e altri tipi di risorse) da [!DNL AEM Assets Cloud Services].
* Governance (riferimenti e copie della risorsa): per facilitare la propagazione automatica degli eventi del ciclo di vita delle risorse come scadenza, eliminazione e aggiornamenti.
* Rappresentazioni di immagini dinamiche e ritaglio avanzato.
* Ottimizzazione e distribuzione di contenuti multimediali avanzati, ad esempio streaming video adattivo pronto all’uso e distribuzione di risorse originali per PDF.
<!--

* Asset-level impressions report ([limited availability](/help/assets/manage-reports-assets-view.md#dynamic-media-delivery-reports)).

-->

Per ulteriori dettagli sulle funzionalità, vedere la documentazione di [[!DNL Dynamic Media with OpenAPI capabilities]](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview).

### Prerequisiti {#dynamic-media-with-universal-editor-and-edge-delivery-services}

Per utilizzare il riferimento della risorsa, è necessario disporre di:

* Diritto a un ambiente Assets Cloud Service in cui è abilitato [!DNL Dynamic Media with Open API capabilities].
* Una licenza di [!DNL Dynamic Media].
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

Vedi [WKND Travel](https://aem-dynamicmedia-demo--dm--hlxsites.aem.live/travel-hospitality/wknd-trvl-home), un sito creato utilizzando le funzionalità di authoring basato su documenti di [!DNL Edge Delivery Services]. Il contenuto del sito è stato creato in [Google Docs](https://drive.google.com/drive/folders/1HCCHRWp4HJIXW_cUv5cRDQ5DzzqiZsXT) e [!DNL Dynamic Media with OpenAPI capabilities] è utilizzato per distribuire le risorse nel contenuto. Dopo l’authoring, il contenuto viene pubblicato direttamente dal documento. Esplora questo [archivio Git](https://github.com/hlxsites/franklin-assets-selector/tree/aem-dynamicmedia-demo/blocks) per informazioni su tutti i file, le cartelle, le configurazioni, lo stile e i codici di funzionalità essenziali del sito Web utilizzati per creare l&#39;impostazione di authoring basato su documenti per questo sito [!DNL Edge Delivery Services (EDS)].

## Integrazione di [!DNL AEM Assets] con flussi di authoring basati su [!DNL Universal Editor] per [!DNL Edge Delivery Services] {#integrate-aem-assets-with-universal-editor-UE}

Configura [!DNL Universal Editor] per l&#39;integrazione con [!DNL AEM Assets]. Questa integrazione consente di utilizzare [!DNL Dynamic Media with OpenAPI capabilities] per distribuire le risorse.

* Consulta [Configurazione in [!DNL Edge Delivery] Sito](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#configuration-in-edge-delivery-site) per scoprire come aggiungere una funzione di selezione risorse personalizzata in [!DNL Universal Editor]. Il selettore risorse personalizzato consente di inserire direttamente le risorse nel contenuto di [!DNL Universal Editor].
* Per informazioni su come accedere a [ e inserire le risorse durante la creazione in ](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview), consulta la [!DNL AEM Assets]Panoramica dell&#39;estensione[!DNL Universal Editor].
