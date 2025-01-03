---
title: Integrare AEM Assets durante la creazione di contenuti per Edge Delivery Services
description: Scopri come integrare AEM Assets con i Edge Delivery Services. Questa integrazione consente di integrare AEM Assets con Microsoft Word e Google Docs, integrare AEM Assets con Universal Editor, integrare Dynamic Media con funzionalità OpenAPI con Universal Editor e integrare Dynamic Media con funzionalità OpenAPI con Microsoft Word e Google Docs.
exl-id: e58db2ce-a55a-49b3-ae8e-709b5ea8d095
source-git-commit: f57edede03cf55110122c59f2874a5f40ffa9c76
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 3%

---

# Integrare AEM Assets durante la creazione di contenuti per Edge Delivery Services {#integrate-aem-assets-while-authoring-for-edge-delivery-services}

![EDS2](/help/assets/assets/EDS2.png)

[Edge Delivery Services](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/edge-delivery/overview) è un insieme componibile di servizi che consente un elevato grado di flessibilità nel modo in cui si creano e distribuiscono i contenuti sul sito Web. È possibile utilizzare sia la [gestione dei contenuti AEM](/help/sites-cloud/authoring/author-publish.md) che la [creazione di WYSIWYG utilizzando l&#39;editor universale e l&#39;authoring basato su documenti](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring).

Puoi modificare il contenuto in:

* [Documentazione di Microsoft Word o Google](#integrate-aem-assets-with-document-based-authoring-tools)

* [Editor universale](#integrate-aem-assets-with-universal-editor)

Dopo aver modificato il contenuto, puoi pubblicarlo in Edge Delivery Services.

## Integrazione di AEM Assets con i flussi di authoring basati su documenti per i Edge Delivery Services {#integrate-aem-assets-with-document-based-authoring-tools}

L’integrazione di AEM Assets con gli strumenti di authoring basato su documenti, come Microsoft Word o Google Docs, fornisce direttamente un selettore di risorse nell’editor. Utilizza questo selettore di risorse per accedere a AEM Assets e inserire nel documento le risorse approvate.

Se disponi già di un sito Web Edge Delivery Services, consulta [Plug-in AEM Assets](https://github.com/adobe-rnd/aem-assets-plugin/blob/main/README.md) per integrare AEM Assets con il progetto AEM esistente. Se non disponi di un sito web Edge Delivery Services, consulta le sezioni [Prerequisiti](#integrate-aem-assets-with-microsoft-word-and-google-docs) e [Integrazione di AEM Assets con l&#39;ambiente di authoring basato su documenti](#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs) di seguito.

### Prerequisiti{#integrate-aem-assets-with-microsoft-word-and-google-docs}

Prima di iniziare, accertati che l’ambiente di authoring basato su documenti sia pronto:

* È possibile integrare l’AEM con uno strumento di authoring basato su documenti per configurare l’ambiente di authoring. Consulta [Guida introduttiva - Esercitazione per sviluppatori](https://www.aem.live/developer/tutorial) per configurare l&#39;ambiente di authoring.

### Integrazione di AEM Assets con l’ambiente di authoring basato su documenti{#integrate-aem-assets-with-microsoft-word-or-google-docs-to-use-aem-assets-with-microsoft-word-or-google-docs}

Configura il plug-in Sidekick AEM Assets per utilizzare le risorse durante l’authoring dei contenuti nei documenti di Microsoft Word o Google.

* Consulta [Adobe Experience Manager Assets Sidekick Plugin](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-experience-manager-assets-for-website-authors) per informazioni su come accedere e utilizzare AEM Assets nei documenti di Microsoft Word o Google.
* Per informazioni dettagliate sulla configurazione, consulta [Configurazione del plug-in di Sidekick di Adobe Experience Manager Assets](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin).
  ![my-assets-sidebar](/help/assets/assets/my-assets-sidebar.png)

## Distribuire risorse tramite Dynamic Media con funzionalità OpenAPI {#integrate-Dynamic-Media-with-OpenAPI-capabilities-with-Microsoft-Word-Google-Docs-and-universal-editor}

Puoi anche utilizzare le risorse distribuite tramite DM con funzionalità OpenAPI. Offre numerosi vantaggi, tra cui:

* Accedi solo alle risorse approvate dal marchio (immagini, video, PDF e altri tipi di risorse) dai Cloud Service AEM Assets.
* Governance (riferimenti e copie della risorsa): per facilitare la propagazione automatica degli eventi del ciclo di vita delle risorse come scadenza, eliminazione e aggiornamenti.
* Rappresentazioni di immagini dinamiche e ritaglio avanzato.
* Ottimizzazione e distribuzione di contenuti multimediali avanzati, ad esempio streaming video adattivo pronto all’uso e distribuzione originale delle risorse per i PDF.
* Rapporto impression a livello di risorsa ([disponibilità limitata](/help/assets/manage-reports-assets-view.md#dynamic-media-delivery-reports)).

Per ulteriori dettagli sulle funzionalità, consulta la documentazione di [Dynamic Media con funzionalità OpenAPI](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview).

### Prerequisiti {#prerequisites-for-dm-with-openapi-capabilities-to-use-aem-assets}

Per utilizzare il riferimento della risorsa, è necessario disporre di:

* Adesione a un ambiente di Cloud Service Assets in cui è abilitato Dynamic Media con funzionalità Open API.
* Una licenza Dynamic Media.
* Il plug-in della barra laterale di AEM Assets è abilitato con il riferimento di copia per le risorse immagine. Per ulteriori dettagli, vedere [questo](https://www.aem.live/developer/configuring-aem-assets-sidekick-plugin#copymode) per l&#39;authoring basato su documenti e [questo](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview) per l&#39;authoring basato su Universal Editor.
* Assets che sono approvati. Le risorse approvate hanno `dam:status=Approved` tramite il backend o le azioni dell&#39;interfaccia utente dei Cloud Service di Assets.

### Utilizzare le risorse distribuite tramite Dynamic Media con funzionalità OpenAPI{#how-to-use-Dynamic-Media-with-OpenAPI-assets}

Per utilizzare le risorse distribuite tramite Dynamic Media con funzionalità OpenAPI durante la creazione dei contenuti, consulta:

* [Utilizzo dei riferimenti immagine](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-image-references-when-authoring-content)
* [Utilizzo di riferimenti video](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-video-references-when-authoring-content)
* [Utilizzo di riferimenti alle risorse per risorse non immagine e video quali PDF, file ZIP e altro ancora](https://www.aem.live/docs/aem-assets-sidekick-plugin#using-asset-references-for-pdf-zip-etc-when-authoring-content)

Guarda questo video per scoprire come distribuire le risorse utilizzando Dynamic Media con funzionalità OpenAPI.

>[!VIDEO](https://video.tv.adobe.com/v/3441155)

## Sito Edge Delivery Services di esempio{#example-of-an-Edge-Delivery-Services-site}

Vedi [Viaggi WKND](http://bit.ly/3DExLnf). Questo sito viene creato utilizzando le funzionalità di authoring basato su documenti dei Edge Delivery Services. Il contenuto del sito è stato creato in [Google Docs](https://drive.google.com/drive/folders/1HCCHRWp4HJIXW_cUv5cRDQ5DzzqiZsXT), utilizzando Dynamic Media con funzionalità OpenAPI per la distribuzione delle risorse. Una volta creato, il contenuto viene pubblicato direttamente dal documento. Per questa configurazione di authoring basato su documenti, tutti i file essenziali, le cartelle, le configurazioni, lo stile e i codici di funzionalità del sito Web sono archiviati in questo [archivio Git](https://github.com/hlxsites/franklin-assets-selector/tree/aem-dynamicmedia-demo/blocks).

## Integrazione di AEM Assets con flussi di authoring per Edge Delivery Services basati su Universal Editor {#integrate-aem-assets-with-universal-editor}

Configura l’Editor universale per l’integrazione con AEM Assets. Questa integrazione consente di utilizzare Dynamic Media con funzionalità OpenAPI per distribuire le risorse.

* Consulta [Configurazione nel sito Edge Delivery](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#configuration-in-edge-delivery-site) per aggiungere una funzione di selezione risorse personalizzata in Universal Editor. Il selettore di risorse personalizzato consente di inserire direttamente le risorse nel contenuto dell’Editor universale.
* Consulta [Panoramica dell&#39;estensione](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview) per scoprire come accedere ad AEM Assets e inserire le risorse durante la creazione in Universal Editor.
