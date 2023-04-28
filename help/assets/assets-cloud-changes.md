---
title: Modifiche di rilievo in [!DNL Adobe Experience Manager Assets] come [!DNL Cloud Service]
description: Modifiche di rilievo apportate a [!DNL Adobe Experience Manager Assets] in [!DNL Experience Manager] come [!DNL Cloud Service] rispetto a [!DNL Adobe Experience Manager] 6.5.
feature: Release Information
role: User,Leader,Architect,Admin
exl-id: 93e7dbcd-016e-4ef2-a1cd-c554efb5ad34
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 10%

---

# Modifiche di rilievo apportate a [!DNL Experience Manager Assets] come [!DNL Cloud Service] {#notable-changes}

[!DNL Adobe Experience Manager] come [!DNL Cloud Service] offre molte nuove funzioni e possibilità per gestire i progetti di Experience Manager. Ci sono molte differenze tra [!DNL Experience Manager Assets] on-premise o ospitato come Adobe Managed Service rispetto a [!DNL Experience Manager] come [!DNL Cloud Service]. Questo articolo evidenzia le differenze importanti per [!DNL Assets] funzionalità.

Le principali differenze rispetto a [!DNL Experience Manager] 6.5:

* [Acquisizione, caricamento ed elaborazione delle risorse](#asset-ingestion).
* [Microservizi per risorse per l’elaborazione nativa per il cloud](#asset-microservices).
* [Rimozione dell’interfaccia classica](#classic-ui).

## Acquisizione, elaborazione e distribuzione di risorse {#asset-ingestion-distribution}

Il caricamento delle risorse è ottimizzato per l’efficienza, consentendo una migliore scalabilità dell’acquisizione, caricamenti più rapidi, elaborazione più rapida tramite i microservizi e ingestione in massa. Le funzionalità del prodotto (interfacce utente web, client desktop) vengono aggiornate. Inoltre, questo può influire su alcune personalizzazioni esistenti.

* [!DNL Experience Manager] utilizza il principio di accesso binario diretto per caricare e scaricare le risorse e utilizza i microservizi per le risorse per elaborare le risorse. Vedi [panoramica dei microservizi](/help/assets/asset-microservices-overview.md).
   * Caricamento risorsa [con accesso binario diretto](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access).
   * Per informazioni tecniche, consulta [protocollo di caricamento binario diretto e API](/help/assets/developer-reference-material-apis.md#upload-binary).
   * Per un confronto dei metodi API disponibili per le operazioni CRUD di base, vedi [API e operazioni su risorse](/help/assets/developer-reference-material-apis.md#use-cases-and-apis).
* Il flusso di lavoro predefinito **[!UICONTROL DAM Asset Update]** incluso nelle versioni precedenti di non è più disponibile. [!DNL Experience Manager] Al contrario, i microservizi per le risorse forniscono un servizio scalabile e prontamente disponibile che copre la maggior parte dell’elaborazione delle risorse predefinita (rendering, estrazione dei metadati e estrazione del testo per l’indicizzazione).
   * Vedi [configurare e utilizzare i microservizi per le risorse](/help/assets/asset-microservices-configure-and-use.md)
   * Per personalizzare i passaggi del flusso di lavoro nell’elaborazione, [flussi di lavoro di post-elaborazione](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) può essere utilizzato.

* I componenti del sito web che forniscono un file binario senza alcuna trasformazione possono utilizzare il download diretto. Il servlet Sling GET viene aggiornato per consentire agli sviluppatori di eseguire questa operazione per impostazione predefinita. I componenti del sito web che forniscono un binario con alcune trasformazioni (ad esempio, ridimensionarlo tramite un servlet) possono continuare a funzionare così com’è.

Le rappresentazioni standard generate con i microservizi per le risorse vengono memorizzate in modo compatibile con le versioni precedenti nei nodi dell’archivio delle risorse, utilizzando le stesse convenzioni di denominazione.

## Sviluppare e testare microservizi per le risorse {#asset-microservices}

I microservizi per le risorse forniscono un’elaborazione scalabile e flessibile delle risorse utilizzando servizi cloud. Adobe gestisce i servizi cloud per una gestione ottimale dei diversi tipi di risorse e opzioni di elaborazione. I microservizi per le risorse aiutano a evitare la necessità di strumenti e metodi di rendering di terze parti (come [!DNL ImageMagick]) e semplifica le configurazioni, fornendo al contempo funzionalità pronte all’uso per i tipi di file più comuni. È ora possibile elaborare un [ampia gamma di tipi di file](/help/assets/file-format-support.md) con più formati pronti all’uso rispetto alle versioni precedenti di Experience Manager. Ad esempio, l’estrazione delle miniature dei formati PSD e PSB è ora possibile con soluzioni di terze parti precedentemente richieste, come [!DNL ImageMagick]. Non puoi utilizzare le configurazioni complesse di [!DNL ImageMagick] per [!UICONTROL Profili di elaborazione] configurazione. Utilizzo [!DNL Dynamic Media] per la transcodifica avanzata FFmpeg di video e l’utilizzo dei profili di elaborazione per [transcodifica di base dei video MP4](/help/assets/manage-video-assets.md#transcode-video).

I microservizi per le risorse sono un servizio nativo per il cloud, dotato di provisioning automatico e collegamento a [!DNL Experience Manager] nei programmi e negli ambienti dei clienti gestiti in Cloud Manager. Per estendere o personalizzare [!DNL Experience Manager], gli sviluppatori possono utilizzare il contenuto o le risorse esistenti con rendering generati in un ambiente cloud, per testare e convalidare il codice utilizzando, visualizzando, scaricando risorse.

Per eseguire una convalida end-to-end del codice e del processo, compresi l’inserimento e l’elaborazione delle risorse, distribuisci le modifiche al codice in un ambiente di sviluppo cloud utilizzando [la conduttura](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) test con l’esecuzione completa dell’elaborazione dei microservizi per le risorse.

## Parità delle funzioni con [!DNL Experience Manager] 6,5 {#cloud-service-feature-status}

[!DNL Experience Manager] come [!DNL Cloud Service] introduce molte nuove funzioni e modalità più efficaci per il funzionamento delle funzioni esistenti. Tuttavia, quando si passa da [!DNL Experience Manager] da 6,5 a [!DNL Experience Manager] come [!DNL Cloud Service], alcune funzioni funzionano in modo diverso, non sono disponibili o sono parzialmente disponibili. Di seguito è riportato un elenco di tali funzioni. Inoltre, consulta la sezione [funzioni obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

| Funzionalità o caso d’uso | Stato in [!DNL Experience Manager] come [!DNL Cloud Service] | Commenti |
|-----|-----|-----|
| [Rilevamento di risorse duplicato](/help/assets/manage-digital-assets.md#detect-duplicate-assets) | Funziona diversamente | Vedi [come funzionava [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html). |
| [Rendering For Placement Only (FPO)](/help/assets/configure-fpo-renditions.md) | Funziona diversamente | I profili di elaborazione utilizzano i microservizi delle risorse per generare rappresentazioni FPO. All&#39;Experience Manager 6.5, una soluzione di terze parti come [!DNL ImageMagick] era disponibile per generare le rappresentazioni. |
| Write-back metadati | Funziona diversamente | Opzione disattivata per impostazione predefinita. Abilita il modulo di avvio del flusso di lavoro corrispondente, se necessario. Il write-back viene gestito dai microservizi per le risorse. |
| Elaborazione delle risorse caricate tramite Gestione pacchetti | Necessità di intervento manuale | Rielaborazione manuale utilizzando **[!UICONTROL Rielabora risorsa]** azione. |
| Rilevamento del tipo MIME | Non supportato. | Se carichi una risorsa digitale senza un’estensione o con un’estensione errata, potrebbe non essere elaborata come desiderato. Gli utenti possono comunque memorizzare i file binari senza un’estensione nel DAM. Vedi [Rilevamento del tipo MIME in [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/detect-asset-mime-type-with-tika.html). |
| Generazione di attività secondarie per una risorsa composta | Non supportato. | I casi d’uso dipendenti come le annotazioni potrebbero non essere soddisfatti. Vedi [creazione di risorse secondarie in [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-linked-subassets.html#generate-subassets). È disponibile l’anteprima di alcuni tipi di file di PDF all’avvio [Versione 2021.7.0](/help/release-notes/release-notes-cloud/release-notes-current.md). |
| Modificare le immagini | Non supportato | La modifica delle risorse non è supportata nell’Experience Manager as a Cloud Service. Vedi [come ha funzionato in Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#editing-images). |
| Home page | Non supportato | Vedi [[!DNL Assets] Home Page experience in [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-home-page.html) |
| Estrarre risorse dall’archivio ZIP | Non supportato | Vedi [Estrazione ZIP in [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#extractzip). |
| Valutazioni delle risorse | Non supportato | Il widget di valutazione nell&#39;editor dello schema metadati non è supportato. |
| Filtro per la disposizione dei contenuti | Non supportato | Un caso d’uso comune di `ContentDispositionFilter` consente agli amministratori di configurare [!DNL Experience Manager] per distribuire i file HTML e aprire i file PDF in linea invece di scaricarli. Nelle istanze di pubblicazione, puoi gestire la disposizione utilizzando la configurazione di Dispatcher. Nelle istanze di authoring, Adobe non consiglia di modificare l’intestazione Content Disposition (Disposizione contenuto). Vedi [Filtro di disposizione dei contenuti in [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/content-disposition-filter.html). |
| Modello di servizio fotografico per prodotto | Non supportato | Vedi [modello di servizio fotografico del prodotto in [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/projects/managing-product-information.html). |
| Traduzione intelligente | Non supportato | [Traduzione intelligente](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/translation/smart-translation-search-feature-video-use.html) non è supportato in [!DNL Experience Manager] come [!DNL Cloud Service]. |
| WebDAV | Non supportato | Per le alternative, vedi [[!DNL Creative Cloud] integrazione](/help/assets/aem-cc-integration-best-practices.md) o [Materiale di riferimento per sviluppatori](/help/assets/developer-reference-material-apis.md). |
| Interfaccia classica | Non supportato | È disponibile solo l’interfaccia utente touch. |

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cercare risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi di metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco di metadati](metadata-import-export.md)

>[!MORELIKETHIS]
>
>Sono disponibili le seguenti risorse per [!DNL Experience Manager] come [!DNL Cloud Service]:
>
>* [Elenco delle funzioni obsolete e rimosse](/help/release-notes/deprecated-removed-features.md)
>* [Introduzione](/help/overview/introduction.md)
>* [Novità e differenze](/help/overview/what-is-new-and-different.md)
>* [L&#39;architettura](/help/overview/architecture.md)
>* [Modifiche di rilievo](/help/release-notes/aem-cloud-changes.md)
>* [Modifiche di rilievo [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
>* [Esercitazioni video](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html?lang=it)

