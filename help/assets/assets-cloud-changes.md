---
title: Modifiche principali in [!DNL Adobe Experience Manager Assets] come a [!DNL Cloud Service]
description: Notevoli modifiche a [!DNL Adobe Experience Manager Assets] in [!DNL Experience Manager] as a [!DNL Cloud Service] rispetto a [!DNL Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: 3e7613aa50e69e2c9789df4f2fb429ab74654110
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 3%

---


# Modifiche notevoli a [!DNL Experience Manager Assets] come [!DNL Cloud Service] {#notable-changes}

[!DNL Adobe Experience Manager] come  [!DNL Cloud Service] offre molte nuove funzionalità e possibilità per gestire i progetti di Experience Manager . Ci sono molte differenze tra [!DNL Experience Manager Assets] locale o ospitato come servizio gestito  Adobe rispetto a [!DNL Experience Manager] come [!DNL Cloud Service]. Questo articolo evidenzia le differenze importanti per le funzionalità [!DNL Assets].

Le principali differenze rispetto al Experience Manager [] 6.5 si trovano nelle seguenti aree:

* [Caricamento, caricamento ed elaborazione](#asset-ingestion) delle risorse.
* [Microservizi di risorse per l’elaborazione](#asset-microservices) nativa cloud.
* [Rimozione dell’interfaccia classica](#classic-ui).

## Caricamento ed elaborazione delle risorse {#asset-ingestion}

Il caricamento delle risorse è ottimizzato per garantire l’efficienza operativa, migliorando il ridimensionamento dell’assimilazione, caricamenti più rapidi, elaborazione più rapida mediante microservizi e assimilazione in massa. Le funzionalità dei prodotti (interfacce utente Web, client desktop) vengono aggiornate. Inoltre, questo potrebbe avere un impatto su alcune personalizzazioni esistenti.

* [!DNL Experience Manager] utilizza il principio di accesso binario diretto per caricare e scaricare le risorse e utilizza i microservizi delle risorse per elaborare le risorse. Vedere [panoramica dei microservizi](/help/assets/asset-microservices-overview.md).
   * Caricamento risorse [con accesso binario diretto](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access).
   * Per informazioni tecniche, consultate [protocollo di caricamento binario diretto e API](/help/assets/developer-reference-material-apis.md#upload-binary).
   * Per un confronto dei metodi API disponibili per le operazioni CRUD di base, consultate [API e operazioni di risorse](/help/assets/developer-reference-material-apis.md#use-cases-and-apis).
* Il flusso di lavoro predefinito **[!UICONTROL DAM Asset Update]** incluso nelle versioni precedenti di non è più disponibile. [!DNL Experience Manager] Al contrario, i microservizi delle risorse forniscono un servizio scalabile e facilmente disponibile che copre la maggior parte dell’elaborazione predefinita delle risorse (rappresentazioni, estrazione dei metadati ed estrazione del testo per l’indicizzazione).
   * Vedere [configurare e utilizzare i microservizi delle risorse](/help/assets/asset-microservices-configure-and-use.md)
   * Per impostare dei passaggi personalizzati per l&#39;elaborazione, è possibile utilizzare i [flussi di lavoro di post-elaborazione](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows).
* Write-back metadati non supportato. Vedere [Write-back di metadati in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/xmp-writeback.html).
* Le risorse caricate tramite Gestione pacchetti richiedono una rielaborazione manuale tramite l&#39;azione **[!UICONTROL Rielabora risorsa]** nell&#39;interfaccia utente [!DNL Assets].
* [!DNL Assets] non rileva automaticamente il tipo MIME delle risorse caricate. Una risorsa digitale senza estensione o con estensione errata non viene elaborata come desiderato. Ad esempio, quando caricate tali risorse, alla risorsa potrebbe non verificarsi nulla o potrebbe essere applicato un profilo di elaborazione errato. Gli utenti possono comunque archiviare i file binari senza estensione in DAM. Vedere [Rilevamento del tipo MIME in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/detect-asset-mime-type-with-tika.html).
* [!DNL Assets] L&#39;esperienza Pagina iniziale non è disponibile. Vedere [[!DNL Assets] Home Page experience in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-home-page.html).
* Il rilevamento di risorse duplicate funziona diversamente rispetto a [come funzionava in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html).
* Le rappresentazioni Solo posizionamento (FPO) vengono generate in modo diverso rispetto alle versioni precedenti di [!DNL Experience Manager]. Vedere [rappresentazione FPO per [!DNL Experience Manager] come a [!DNL Cloud Service]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/configure-aem-assets-for-asset-link.ug.html).

Le rappresentazioni standard generate con i microservizi delle risorse vengono memorizzate in modo compatibile con le versioni precedenti nei nodi dell’archivio delle risorse, utilizzando le stesse convenzioni di denominazione.

## Sviluppare e testare i microservizi delle risorse {#asset-microservices}

I microservizi delle risorse forniscono un’elaborazione scalabile e resiliente delle risorse mediante i servizi cloud.  Adobe gestisce i servizi cloud per una gestione ottimale dei diversi tipi di risorse e opzioni di elaborazione. I microservizi delle risorse consentono di evitare la necessità di strumenti e metodi di rendering di terze parti (come ImageMagick) e di semplificare le configurazioni, fornendo al contempo funzionalità pronte all’uso per i tipi di file più comuni. È ora possibile elaborare un [ampio intervallo di tipi di file](/help/assets/file-format-support.md) che include più formati out-of-the-box rispetto a quanto è possibile con le versioni precedenti di  Experience Manager. Ad esempio, l&#39;estrazione delle miniature dei formati PSD e PSB ora è possibile che soluzioni di terze parti come ImageMagick precedentemente richieste. Non è possibile utilizzare le configurazioni complesse di ImageMagick per la configurazione [!UICONTROL Profili di elaborazione]. Utilizzate [!DNL Dynamic Media] per la transcodifica avanzata di FFmpeg di video e utilizzate i profili di elaborazione per la [transcodifica di base di video MP4](/help/assets/manage-video-assets.md#transcode-video).

Asset microservices è un servizio nativo basato su cloud che viene automaticamente fornito e collegato a [!DNL Experience Manager] nei programmi cliente e negli ambienti gestiti in Cloud Manager. Per estendere o personalizzare [!DNL Experience Manager], gli sviluppatori possono utilizzare il contenuto o le risorse esistenti con rappresentazioni generate in un ambiente cloud, per testare e convalidare il codice utilizzando, visualizzando e scaricando le risorse.

Per eseguire una convalida end-to-end del codice e del processo, compresi l’assimilazione e l’elaborazione delle risorse, implementate le modifiche del codice in un ambiente di sviluppo cloud utilizzando [la pipeline](/help/implementing/cloud-manager/configure-pipeline.md) e verificate con l’esecuzione completa dell’elaborazione dei microservizi di risorse.

## Rimozione dell’interfaccia classica {#classic-ui}

L&#39;interfaccia classica non è più disponibile in [!DNL Experience Manager] come [!DNL Cloud Service]. È disponibile solo l’interfaccia touch.

>[!MORELIKETHIS]
>
>Le risorse seguenti sono disponibili per [!DNL Experience Manager] come [!DNL Cloud Service]:
>
>* [Introduzione](/help/overview/introduction.md)
>* [Novità e differenze](/help/overview/what-is-new-and-different.md)
>* [L&#39;architettura](/help/core-concepts/architecture.md)
>* [Modifiche principali](/help/release-notes/aem-cloud-changes.md)
>* [Modifiche principali [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
>* [Esercitazioni video](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)

