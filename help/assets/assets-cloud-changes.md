---
title: Modifiche di rilievo in  [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service]
description: Modifiche di rilievo apportate a  [!DNL Adobe Experience Manager Assets] in [!DNL Experience Manager] as a [!DNL Cloud Service] as rispetto a [!DNL Adobe Experience Manager] 6.5.
feature: Release Information
role: User, Leader, Developer, Admin
exl-id: 93e7dbcd-016e-4ef2-a1cd-c554efb5ad34
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 9%

---

# Modifiche di rilievo apportate a [!DNL Experience Manager Assets] come [!DNL Cloud Service] {#notable-changes}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] offre molte nuove funzionalità e possibilità per gestire i tuoi progetti Experience Manager. Esistono molte differenze tra [!DNL Experience Manager Assets] on-premise o ospitato come Adobe Managed Service e [!DNL Experience Manager] come [!DNL Cloud Service]. Questo articolo evidenzia le differenze importanti per le funzionalità di [!DNL Assets].

Le principali differenze rispetto a [!DNL Experience Manager] 6.5 riguardano le seguenti aree:

* [Acquisizione, caricamento ed elaborazione delle risorse](#asset-ingestion).
* [Microservizi risorse per elaborazione nativa per il cloud](#asset-microservices).
* [Rimozione dell&#39;interfaccia classica](#classic-ui).

## Acquisizione, elaborazione e distribuzione delle risorse {#asset-ingestion-distribution}

Il caricamento delle risorse è ottimizzato per migliorarne l’efficienza, in quanto consente una migliore scalabilità dell’acquisizione, caricamenti più veloci, un’elaborazione più rapida tramite microservizi e l’acquisizione in blocco. Le funzionalità del prodotto (interfacce utente web, client desktop) sono state aggiornate. Inoltre, questi elementi possono influire su alcune personalizzazioni esistenti.

* [!DNL Experience Manager] utilizza il principio dell&#39;accesso binario diretto per caricare e scaricare le risorse e utilizza i microservizi per l&#39;elaborazione delle risorse. Visualizza una [panoramica dei microservizi](/help/assets/asset-microservices-overview.md).
   * Caricamento risorsa [&#x200B; con accesso binario diretto](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access).
   * Per informazioni tecniche, vedere [protocollo di caricamento binario diretto e API](/help/assets/developer-reference-material-apis.md#upload-binary).
   * Per un confronto tra i metodi API disponibili per le operazioni CRUD di base, vedi [API e operazioni su risorse](/help/assets/developer-reference-material-apis.md#use-cases-and-apis).
* Il flusso di lavoro predefinito **[!UICONTROL DAM Asset Update]** nelle versioni precedenti di [!DNL Experience Manager] non è più disponibile. Al contrario, i microservizi per le risorse forniscono un servizio scalabile e prontamente disponibile che copre la maggior parte dell’elaborazione delle risorse predefinita (rappresentazioni, estrazione dei metadati ed estrazione del testo per l’indicizzazione).
   * Consulta [configurare e utilizzare i microservizi per le risorse](/help/assets/asset-microservices-configure-and-use.md)
   * Per personalizzare i passaggi del flusso di lavoro nell&#39;elaborazione, è possibile utilizzare [flussi di lavoro di post-elaborazione](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows).

* I componenti del sito web che forniscono un file binario senza alcuna trasformazione possono utilizzare il download diretto. Per impostazione predefinita, il servlet GET di Sling viene aggiornato per abilitare questa funzionalità. I componenti del sito web che forniscono un binario con una certa trasformazione (ad esempio, ridimensionalo tramite un servlet) possono continuare a funzionare nello stato attuale.

Le rappresentazioni standard generate con i microservizi per le risorse vengono memorizzate in modo compatibile con le versioni precedenti nei nodi dell’archivio delle risorse utilizzando le stesse convenzioni di denominazione.

## Sviluppare e testare i microservizi per le risorse {#asset-microservices}

I microservizi per le risorse forniscono un’elaborazione scalabile e flessibile delle risorse utilizzando servizi cloud. Adobe gestisce i servizi cloud per una gestione ottimale dei diversi tipi di risorse e opzioni di elaborazione. I microservizi per le risorse consentono di evitare la necessità di metodi e strumenti di rendering di terze parti (come [!DNL ImageMagick]) e di semplificare le configurazioni, fornendo al contempo funzionalità predefinite per i tipi di file più comuni. Ora puoi elaborare una [vasta gamma di tipi di file](/help/assets/file-format-support.md) che copre più formati preconfigurati rispetto alle versioni precedenti di Experience Manager. Ad esempio, è ora possibile estrarre le miniature dei formati PSD e PSB che in precedenza richiedevano soluzioni di terze parti come [!DNL ImageMagick]. Impossibile utilizzare le configurazioni complesse di [!DNL ImageMagick] per la configurazione di [!UICONTROL Profili elaborazione]. Utilizza [!DNL Dynamic Media] per la transcodifica FFmpeg avanzata dei video e utilizza i profili di elaborazione per [la transcodifica di base dei video MP4](/help/assets/manage-video-assets.md#transcode-video).

Asset microservices è un servizio nativo per il cloud fornito automaticamente e collegato a [!DNL Experience Manager] nei programmi e negli ambienti del cliente gestiti in Cloud Manager. Per estendere o personalizzare [!DNL Experience Manager], gli sviluppatori possono utilizzare contenuto o risorse esistenti con rappresentazioni generate in un ambiente cloud. Questa funzionalità consente loro di testare e convalidare il codice utilizzando, visualizzando o scaricando le risorse.

Per eseguire una convalida end-to-end del codice e del processo, inclusa l&#39;acquisizione e l&#39;elaborazione delle risorse, distribuisci le modifiche al codice in un ambiente di sviluppo cloud utilizzando [la pipeline](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) ed esegui un test con l&#39;esecuzione completa dell&#39;elaborazione dei microservizi per le risorse.

## Parità di funzionalità con [!DNL Experience Manager] 6.5 {#cloud-service-feature-status}

[!DNL Experience Manager] as a [!DNL Cloud Service] introduce molte nuove funzionalità e modi più performanti per il funzionamento delle funzionalità esistenti. Tuttavia, quando si passa da [!DNL Experience Manager] 6.5 a [!DNL Experience Manager] come [!DNL Cloud Service], è possibile notare che alcune funzionalità funzionano in modo diverso, non sono disponibili o sono parzialmente disponibili. Di seguito è riportato un elenco di tali funzioni. Inoltre, vedere le [funzionalità obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

| Funzionalità o caso d’uso | Stato in [!DNL Experience Manager] come [!DNL Cloud Service] | Commenti |
|-----|-----|-----|
| [Rilevamento risorsa duplicato](/help/assets/detect-duplicate-assets.md) | Questo funziona diversamente | Vedi [come funzionava in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/managing/duplicate-detection). |
| [Rappresentazioni solo posizionamento](/help/assets/configure-fpo-renditions.md) | Questo funziona diversamente | I profili di elaborazione utilizzano i microservizi delle risorse per generare rappresentazioni FPO. In Experience Manager 6.5, era disponibile una soluzione di terze parti come [!DNL ImageMagick] per generare le rappresentazioni. |
| Writeback di metadati | Questo funziona diversamente | Disabilitata per impostazione predefinita. Se necessario, abilita il modulo di avvio del flusso di lavoro corrispondente. I microservizi per le risorse gestiscono il writeback. |
| Elaborazione delle risorse caricate tramite Gestione pacchetti | Questo richiede un intervento manuale | Rielabora manualmente utilizzando l&#39;azione **[!UICONTROL Rielabora risorsa]**. |
| Rilevamento tipo MIME | Non supportato. | Se carichi una risorsa digitale senza un’estensione o con un’estensione non corretta, questa potrebbe non essere elaborata come desiderato. Gli utenti possono comunque memorizzare i file binari senza un’estensione in DAM. Vedi [Rilevamento del tipo MIME in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/administer/detect-asset-mime-type-with-tika). |
| Generazione di risorse secondarie per risorse composte | Non supportato. | I casi d’uso dipendenti come le annotazioni potrebbero non essere soddisfatti. Consulta [creazione di risorse secondarie in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/managing/managing-linked-subassets#generate-subassets). L&#39;anteprima PDF di alcuni tipi di file è disponibile a partire dalla versione [2021.7.0](/help/release-notes/release-notes-cloud/release-notes-current.md). |
| Modificare le immagini | Non supportato | La modifica delle risorse non è supportata in Experience Manager as a Cloud Service. Consulta [Funzionamento in Experience Manager 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/managing/manage-assets#editing-images). |
| Home page | Non supportato | Consulta [[!DNL Assets] Esperienza pagina iniziale in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/using/assets-home-page) |
| Estrai risorse dall’archivio ZIP | Non supportato | Vedi [Estrazione ZIP in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/managing/manage-assets#extractzip). |
| Valutazioni Assets | Non supportato | Il widget di valutazione nell’editor schema metadati non è supportato. |
| Filtro di disposizione del contenuto | Non supportato | Un caso d&#39;uso comune di `ContentDispositionFilter` consiste nel consentire agli amministratori di configurare [!DNL Experience Manager] per distribuire i file HTML e aprire i file PDF in linea anziché scaricarli. Nelle istanze di pubblicazione, puoi gestire la disposizione utilizzando la configurazione di Dispatcher. Nelle istanze di authoring, Adobe sconsiglia di modificare l’intestazione Content Disposition. Vedi [Filtro eliminazione contenuti in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/security/content-disposition-filter). |
| Modello servizio fotografico per prodotto | Non supportato | Vedi [modello servizio fotografico per prodotto in [!DNL Experience Manager] 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/sites/authoring/projects/managing-product-information). |
| Traduzione intelligente | Non supportato | La traduzione intelligente non è supportata in [!DNL Experience Manager] come [!DNL Cloud Service]. |
| WebDAV | Non supportato | Per informazioni alternative, vedere [[!DNL Creative Cloud] integration](/help/assets/aem-cc-integration-best-practices.md) o [Developer reference material](/help/assets/developer-reference-material-apis.md). |
| Interfaccia classica | Non supportato | È disponibile solo un’interfaccia touch. |

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi di metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)
* [Pubblicare risorse in AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>Le risorse seguenti sono disponibili per [!DNL Experience Manager] come [!DNL Cloud Service]:
>
>* [Elenco delle funzionalità obsolete e rimosse](/help/release-notes/deprecated-removed-features.md)
>* [Introduzione](/help/overview/introduction.md)
>* [Novità e differenze](/help/overview/what-is-new-and-different.md)
>* [Architettura](/help/overview/architecture.md)
>* [Modifiche di rilievo](/help/release-notes/aem-cloud-changes.md)
>* [Modifiche di rilievo [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
>* [Esercitazioni video](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/overview)
