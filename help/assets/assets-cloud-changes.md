---
title: Notevoli modifiche in Risorse Adobe Experience Manager come servizio cloud
description: Notevoli modifiche alle risorse Adobe Experience Manager nel servizio AEM Cloud rispetto ad Adobe Experience Manager 6.5.
translation-type: tm+mt
source-git-commit: 37ff6912837ba78c90526e8f8322b9002e9a4304

---


# Notable changes to Experience Manager Assets as a Cloud Service {#notable-changes}

Adobe Experience Manager come servizio Cloud offre molte nuove funzionalità e possibilità per gestire i progetti AEM. Tuttavia, esistono molte differenze tra Experience Manager Assets locale o in Adobe Managed Service rispetto a Experience Manager come servizio Cloud. In questo documento vengono evidenziate le differenze importanti per le funzionalità di Risorse. Per altre modifiche, vedi le [modifiche generiche a Experience Manager come servizio](/help/release-notes/aem-cloud-changes.md)Cloud.

Le principali differenze rispetto a Experience Manager 6.5 si trovano nelle seguenti aree:

* [Caricamento](#asset-ingestion)e assimilazione delle risorse.
* [Microservizi di risorse per l’elaborazione](#asset-microservices)cloud.
* [Rimozione dell’interfaccia classica](#classic-ui).

## Caricamento e caricamento delle risorse {#asset-ingestion}

Il caricamento delle risorse è stato ottimizzato per garantire l’efficienza operativa, ottimizzando l’assimilazione delle risorse e velocizzando i caricamenti. Sono state aggiornate le funzionalità dei prodotti (interfacce utente Web, client desktop). Tuttavia, questo potrebbe avere un impatto su alcune personalizzazioni esistenti.

* Experience Manager utilizza il principio di accesso binario diretto per caricare e scaricare e i microservizi di risorse per l’elaborazione delle risorse. Consultate [Panoramica sull’assimilazione](/help/assets/asset-microservices-overview.md)delle risorse.
   * Caricamento delle risorse [con accesso](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access)binario diretto.
   * Per informazioni tecniche, consultate Protocollo di caricamento binario [diretto e API](/help/assets/developer-reference-material-apis.md#overview-binary-upload).
* Il flusso di lavoro predefinito **[!UICONTROL DAM Asset Update]** incluso nelle versioni precedenti di AEM non è più disponibile. Al contrario, i microservizi delle risorse forniscono un servizio scalabile e facilmente disponibile che copre la maggior parte dell’elaborazione predefinita delle risorse (rappresentazioni, estrazione dei metadati, estrazione del testo per l’indicizzazione).
   * Consultate [Configurazione e utilizzo dei microservizi delle risorse](/help/assets/asset-microservices-configure-and-use.md)
   * Per impostare i passaggi del flusso di lavoro personalizzati nell&#39;elaborazione, è possibile utilizzare i flussi di lavoro [di](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) post-elaborazione.
* Assets that come in via Package Manager require manual reprocessing using the **[!UICONTROL Reprocess Asset]** action in the Assets interface.

Le rappresentazioni standard generate con i microservizi delle risorse vengono memorizzate in modo compatibile con le versioni precedenti nei nodi dell’archivio delle risorse (stesse convenzioni di denominazione).

## Sviluppare e testare microservizi per risorse {#asset-microservices}

I microservizi delle risorse forniscono un’elaborazione scalabile e resiliente delle risorse mediante i servizi cloud. Adobe gestisce i servizi cloud per una gestione ottimale dei diversi tipi di risorse e opzioni di elaborazione. I microservizi delle risorse consentono di evitare la necessità di strumenti e metodi di rendering di terze parti (come ImageMagick) e di semplificare le configurazioni, fornendo al contempo funzionalità pronte all’uso per i tipi di file più comuni. Ora puoi elaborare un&#39; [ampia gamma di tipi](/help/assets/file-format-support.md) di file che includono più formati out-of-the-box di quanto sia possibile con le versioni precedenti di Experience Manager. Ad esempio, l&#39;estrazione delle miniature dei formati PSD e PSB ora è possibile che soluzioni di terze parti come ImageMagick precedentemente richieste. Non è possibile utilizzare le configurazioni complesse di ImageMagick per la configurazione dei profili [!UICONTROL di] elaborazione. Utilizzate anche [!DNL Dynamic Media] per la transcodifica FFmpeg dei video.

Asset microservices è un servizio nativo basato su cloud che viene automaticamente fornito e collegato a Experience Manager nei programmi cliente e negli ambienti gestiti in Cloud Manager. Per estendere o personalizzare Experience Manager, gli sviluppatori possono utilizzare il contenuto o le risorse esistenti con rappresentazioni generate in un ambiente cloud, per testare e convalidare il codice utilizzando, visualizzando e scaricando le risorse.

Per eseguire una convalida end-to-end del codice e del processo, compresi l’assimilazione e l’elaborazione delle risorse, implementa le modifiche del codice in un ambiente di sviluppo cloud utilizzando [la pipeline](/help/implementing/cloud-manager/configure-pipeline.md) e verifica con l’esecuzione completa dell’elaborazione dei microservizi di risorse.

## Rimozione dell’interfaccia classica {#classic-ui}

L&#39;interfaccia classica non è più disponibile in Experience Manager come servizio Cloud. L’interfaccia standard è l’interfaccia touch.
