---
title: Modifiche di rilievo in [!DNL Adobe Experience Manager Assets] come a [!DNL Cloud Service]
description: Modifiche di rilievo apportate a [!DNL Adobe Experience Manager Assets] in [!DNL Experience Manager] as a [!DNL Cloud Service] rispetto a [!DNL Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: 201abba4352362b1bb97b6a25bd84f95e8ed8483
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 5%

---


# Modifiche di rilievo apportate a [!DNL Experience Manager Assets] come a [!DNL Cloud Service] {#notable-changes}

[!DNL Adobe Experience Manager] as a  [!DNL Cloud Service] offre molte nuove funzioni e possibilità per gestire i progetti di Experience Manager. Ci sono molte differenze tra [!DNL Experience Manager Assets] on-premise o in hosting come Adobe Managed Service rispetto a [!DNL Experience Manager] come [!DNL Cloud Service]. Questo articolo evidenzia le differenze importanti per le funzionalità di .[!DNL Assets]

Le principali differenze rispetto all&#39; [Experience Manager] 6.5 riguardano le seguenti aree:

* [Acquisizione, caricamento ed elaborazione delle risorse](#asset-ingestion).
* [Microservizi per risorse per l’elaborazione](#asset-microservices) nativa per il cloud.
* [Rimozione dell’interfaccia classica](#classic-ui).

## Acquisizione ed elaborazione delle risorse {#asset-ingestion}

Il caricamento delle risorse è ottimizzato per l’efficienza, consentendo una migliore scalabilità dell’acquisizione, caricamenti più rapidi, elaborazione più rapida tramite i microservizi e ingestione in massa. Le funzionalità del prodotto (interfacce utente web, client desktop) vengono aggiornate. Inoltre, questo può influire su alcune personalizzazioni esistenti.

* [!DNL Experience Manager] utilizza il principio di accesso binario diretto per caricare e scaricare le risorse e utilizza i microservizi per le risorse per elaborare le risorse. Vedere [panoramica dei microservizi](/help/assets/asset-microservices-overview.md).
   * Caricamento delle risorse [con accesso binario diretto](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access).
   * Per informazioni tecniche, consulta [protocollo di caricamento binario diretto e API](/help/assets/developer-reference-material-apis.md#upload-binary).
   * Per un confronto dei metodi API disponibili per le operazioni CRUD di base, consulta [API e operazioni sulle risorse](/help/assets/developer-reference-material-apis.md#use-cases-and-apis).
* Il flusso di lavoro predefinito **[!UICONTROL DAM Asset Update]** incluso nelle versioni precedenti di non è più disponibile. [!DNL Experience Manager] Al contrario, i microservizi per le risorse forniscono un servizio scalabile e prontamente disponibile che copre la maggior parte dell’elaborazione delle risorse predefinita (rendering, estrazione dei metadati e estrazione del testo per l’indicizzazione).
   * Consulta [configurare e utilizzare i microservizi per le risorse](/help/assets/asset-microservices-configure-and-use.md)
   * Per personalizzare i passaggi del flusso di lavoro nell&#39;elaborazione, è possibile utilizzare [flussi di lavoro di post-elaborazione](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows).

Le rappresentazioni standard generate con i microservizi per le risorse vengono memorizzate in modo compatibile con le versioni precedenti nei nodi dell’archivio delle risorse, utilizzando le stesse convenzioni di denominazione.

## Sviluppare e testare i microservizi per le risorse {#asset-microservices}

I microservizi per le risorse forniscono un’elaborazione scalabile e flessibile delle risorse tramite Cloud Services. Adobe gestisce i servizi cloud per una gestione ottimale dei diversi tipi di risorse e opzioni di elaborazione. I microservizi per le risorse consentono di evitare la necessità di strumenti e metodi di rendering di terze parti (come ImageMagick) e di semplificare le configurazioni, fornendo al contempo funzionalità pronte all’uso per i tipi di file comuni. È ora possibile elaborare una [vasta gamma di tipi di file](/help/assets/file-format-support.md) che copre più formati pronti all&#39;uso rispetto a quanto è possibile con le versioni precedenti di Experience Manager. Ad esempio, è ora possibile estrarre le miniature dei formati PSD e PSB che in precedenza richiedevano soluzioni di terze parti come ImageMagick. Non è possibile utilizzare le configurazioni complesse di ImageMagick per la configurazione [!UICONTROL Profili di elaborazione]. Utilizza [!DNL Dynamic Media] per la transcodifica avanzata FFmpeg di video e utilizza i profili di elaborazione per [la transcodifica di base di video MP4](/help/assets/manage-video-assets.md#transcode-video).

I microservizi per le risorse sono un servizio nativo per il cloud, fornito automaticamente e collegato a [!DNL Experience Manager] nei programmi e negli ambienti cliente gestiti in Cloud Manager. Per estendere o personalizzare [!DNL Experience Manager], gli sviluppatori possono utilizzare il contenuto o le risorse esistenti con rendering generati in un ambiente cloud, per testare e convalidare il codice utilizzando, visualizzando, scaricando risorse.

Per eseguire una convalida end-to-end del codice e del processo, compresi l’inserimento e l’elaborazione delle risorse, implementa le modifiche al codice in un ambiente di sviluppo cloud utilizzando [la pipeline](/help/implementing/cloud-manager/configure-pipeline.md) e testa con la completa esecuzione dell’elaborazione dei microservizi per le risorse.


## Parità delle funzioni con [!DNL Experience Manager] 6.5 {#cloud-service-feature-status}

[!DNL Experience Manager] as a  [!DNL Cloud Service] introduce molte nuove funzioni e modi più efficaci per il funzionamento delle funzioni esistenti. Tuttavia, quando si passa da [!DNL Experience Manager] 6.5 a [!DNL Experience Manager] come [!DNL Cloud Service], è possibile notare che alcune funzioni funzionano in modo diverso, non sono disponibili o sono parzialmente disponibili. Di seguito è riportato un elenco di tali funzioni:

| Funzionalità o caso d’uso | Stato in [!DNL Experience Manager] come [!DNL Cloud Service] | Commenti |
|-----|-----|-----|
| [Rilevamento di risorse duplicato](/help/assets/manage-digital-assets.md#detect-duplicate-assets) | Funziona diversamente. | Vedi [come funzionava in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html). |
| [Rendering For Placement Only (FPO)](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/configure-aem-assets-for-asset-link.ug.html#configfporendition) | Funziona diversamente |  |
| Write-back metadati | Non supportato. | Consulta [write-back di metadati in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/xmp-writeback.html) |
| Elaborazione delle risorse caricate tramite Gestione pacchetti | Ha bisogno di intervento manuale. | Rielabora manualmente utilizzando l&#39;azione **[!UICONTROL Rielabora risorsa]** . |
| Rilevamento del tipo MIME | Non supportato. | Se carichi una risorsa digitale senza un’estensione o con un’estensione errata, potrebbe non essere elaborata come desiderato. Gli utenti possono comunque memorizzare i file binari senza un’estensione nel DAM. Vedi [Rilevamento del tipo MIME in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/detect-asset-mime-type-with-tika.html). |
| Generazione di attività secondarie per le attività composte | Non supportato. | I casi di utilizzo dipendenti non vengono soddisfatti. Ad esempio, è interessata l’annotazione di file PDF con più pagine. Consulta [creazione di risorse secondarie in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-linked-subassets.html#generate-subassets). |
| Home page | Non supportato. | Vedere [[!DNL Assets] Home Page experience in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-home-page.html) |
| Estrarre risorse dall’archivio ZIP | Non supportato. | Consulta [Estrazione ZIP in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.htmln#extractzip). |
| Interfaccia classica | Non supportato. | È disponibile solo l’interfaccia touch. |

>[!MORELIKETHIS]
>
>Le risorse seguenti sono disponibili per [!DNL Experience Manager] come [!DNL Cloud Service]:
>
>* [Introduzione](/help/overview/introduction.md)
>* [Novità e differenze](/help/overview/what-is-new-and-different.md)
>* [L&#39;architettura](/help/core-concepts/architecture.md)
>* [Modifiche di rilievo](/help/release-notes/aem-cloud-changes.md)
>* [Modifiche di rilievo [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
>* [Esercitazioni video](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html?lang=it)

