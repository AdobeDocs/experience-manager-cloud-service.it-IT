---
title: Notevoli modifiche in Risorse Adobe Experience Manager come a [!DNL Cloud Service]
description: Notevoli modifiche alle risorse Adobe Experience Manager in AEM [!DNL Cloud Service] rispetto ad Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: 5be8ab734306ad1442804b3f030a56be1d3b5dfa
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 8%

---


# Notevoli modifiche a  risorse Experience Manager come [!DNL Cloud Service] {#notable-changes}

Adobe Experience Manager come [!DNL Cloud Service] offre molte nuove funzionalità e possibilità per gestire i progetti AEM. Tuttavia, esistono molte differenze tra  risorse di Experience Manager locali o in  servizio gestito del Adobe rispetto a  Experience Manager come [!DNL Cloud Service]. In questo documento vengono evidenziate le differenze importanti per le funzionalità di Risorse.

Le principali differenze rispetto a Experience Manager 6.5 riguardano i seguenti aspetti:

* [Caricamento](#asset-ingestion) e assimilazione delle risorse.
* [Microservizi di risorse per l’elaborazione](#asset-microservices) nativa cloud.
* [Rimozione dell’interfaccia classica](#classic-ui).

>[!NOTE]
>
>In questo documento vengono evidenziate le modifiche rilevanti apportate  AEM Assets. Per le modifiche generali  Experience Manager come [!DNL Cloud Service] e altri moduli, vedete:
>
>* [Introduzione ad Adobe Experience Manager as a [!DNL Cloud Service]](/help/overview/introduction.md)
>* Una [Panoramica delle AEM come a [!DNL Cloud Service] - Novità e cosa è diverso](/help/overview/what-is-new-and-different.md)
>* [Architettura](/help/core-concepts/architecture.md) di Adobe Experience Manager as a [!DNL Cloud Service]
>* [Notevoli modifiche a AEM come [!DNL Cloud Service] (Note sulla versione)](/help/release-notes/aem-cloud-changes.md)
>* [Notevoli modifiche a  AEM Sites come [!DNL Cloud Service]](/help/sites-cloud/sites-cloud-changes.md)
>* [Adobe Experience Manager come  [!DNL Cloud Service] esercitazioni](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)


## Caricamento e caricamento di risorse {#asset-ingestion}

Il caricamento delle risorse è stato ottimizzato per garantire l’efficienza operativa, ottimizzando l’assimilazione delle risorse e velocizzando i caricamenti. Sono state aggiornate le funzionalità dei prodotti (interfacce utente Web, client desktop). Tuttavia, questo potrebbe avere un impatto su alcune personalizzazioni esistenti.

*  Experience Manager utilizza il principio di accesso binario diretto per caricare e scaricare e per elaborare le risorse, Consultate [panoramica dell&#39;assimilazione delle risorse](/help/assets/asset-microservices-overview.md).
   * Caricamento risorse [con accesso binario diretto](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access).
   * Per informazioni tecniche, consultate [protocollo di caricamento binario diretto e API](/help/assets/developer-reference-material-apis.md#upload-binary).
* Il flusso di lavoro predefinito **[!UICONTROL DAM Asset Update]** incluso nelle versioni precedenti di AEM non è più disponibile. Al contrario, i microservizi delle risorse forniscono un servizio scalabile e facilmente disponibile che copre la maggior parte dell’elaborazione predefinita delle risorse (rappresentazioni, estrazione dei metadati, estrazione del testo per l’indicizzazione).
   * Vedere [configurazione e utilizzo di asset microservices](/help/assets/asset-microservices-configure-and-use.md)
   * Per impostare dei passaggi personalizzati per l&#39;elaborazione, è possibile utilizzare i [flussi di lavoro di post-elaborazione](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows).
* Per le risorse incluse in Gestione pacchetti è necessaria la rielaborazione manuale tramite l&#39;azione **[!UICONTROL Rielabora risorsa]** nell&#39;interfaccia Risorse.

Le rappresentazioni standard generate con i microservizi delle risorse vengono memorizzate in modo compatibile con le versioni precedenti nei nodi dell’archivio delle risorse (stesse convenzioni di denominazione).

## Sviluppare e testare i microservizi delle risorse {#asset-microservices}

I microservizi delle risorse forniscono un’elaborazione scalabile e resiliente delle risorse mediante i servizi cloud.  Adobe gestisce i servizi cloud per una gestione ottimale dei diversi tipi di risorse e opzioni di elaborazione. I microservizi delle risorse consentono di evitare la necessità di strumenti e metodi di rendering di terze parti (come ImageMagick) e di semplificare le configurazioni, fornendo al contempo funzionalità pronte all’uso per i tipi di file più comuni. È ora possibile elaborare un [ampio intervallo di tipi di file](/help/assets/file-format-support.md) che include più formati out-of-the-box rispetto a quanto è possibile con le versioni precedenti di  Experience Manager. Ad esempio, l&#39;estrazione delle miniature dei formati PSD e PSB ora è possibile che soluzioni di terze parti come ImageMagick precedentemente richieste. Non è possibile utilizzare le configurazioni complesse di ImageMagick per la configurazione [!UICONTROL Profili di elaborazione]. Utilizzate [!DNL Dynamic Media] per la transcodifica FFmpeg di video e utilizzate i profili di elaborazione per la [transcodifica di base di video MP4](/help/assets/manage-video-assets.md#transcode-video).

Asset microservices è un servizio nativo basato su cloud che viene automaticamente fornito e collegato a  Experience Manager nei programmi cliente e negli ambienti gestiti in Cloud Manager. Per estendere o personalizzare  Experience Manager, gli sviluppatori possono utilizzare il contenuto o le risorse esistenti con rappresentazioni generate in un ambiente cloud, per testare e convalidare il codice utilizzando, visualizzando e scaricando le risorse.

Per eseguire una convalida end-to-end del codice e del processo, compresi l’assimilazione e l’elaborazione delle risorse, implementate le modifiche del codice in un ambiente di sviluppo cloud utilizzando [la pipeline](/help/implementing/cloud-manager/configure-pipeline.md) e verificate con l’esecuzione completa dell’elaborazione dei microservizi di risorse.

## Rimozione dell’interfaccia classica {#classic-ui}

L&#39;interfaccia classica non è più disponibile in  Experience Manager come [!DNL Cloud Service]. L’interfaccia standard è l’interfaccia touch.
