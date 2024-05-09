---
title: Modifiche di rilievo apportate a [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service]
description: Modifiche di rilievo apportate [!DNL Adobe Experience Manager Assets] in [!DNL Experience Manager] as a [!DNL Cloud Service] rispetto a [!DNL Adobe Experience Manager] 6.5
feature: Release Information
role: User,Leader,Architect,Admin
exl-id: 93e7dbcd-016e-4ef2-a1cd-c554efb5ad34
source-git-commit: f7f60036088a2332644ce87f4a1be9bae3af1c5e
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 9%

---

# Modifiche di rilievo apportate [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#notable-changes}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] offre molte nuove funzioni e possibilità per gestire i progetti Experience Manager. Ci sono molte differenze tra [!DNL Experience Manager Assets] on-premise o in hosting come Adobe Managed Service rispetto a [!DNL Experience Manager] as a [!DNL Cloud Service]. Questo articolo evidenzia le differenze importanti per [!DNL Assets] funzionalità.

Le principali differenze rispetto a [!DNL Experience Manager] 6.5 si situano nei seguenti settori:

* [Acquisizione, caricamento ed elaborazione delle risorse](#asset-ingestion).
* [Microservizi per risorse per elaborazione nativa per il cloud](#asset-microservices).
* [Rimozione dell’interfaccia classica](#classic-ui).

## Acquisizione, elaborazione e distribuzione delle risorse {#asset-ingestion-distribution}

Il caricamento delle risorse è ottimizzato per migliorarne l’efficienza, in quanto consente una migliore scalabilità dell’acquisizione, caricamenti più veloci, un’elaborazione più rapida tramite microservizi e l’acquisizione in blocco. Le funzionalità del prodotto (interfacce utente web, client desktop) sono state aggiornate. Inoltre, questo potrebbe influire su alcune personalizzazioni esistenti.

* [!DNL Experience Manager] utilizza il principio dell’accesso binario diretto per caricare e scaricare le risorse, mentre per elaborare le risorse utilizza i microservizi per le risorse. Consulta [panoramica dei microservizi](/help/assets/asset-microservices-overview.md).
   * Caricamento risorse [con accesso binario diretto](/help/assets/asset-microservices-overview.md#asset-upload-with-direct-binary-access).
   * Per informazioni di carattere tecnico, consultare [protocollo di caricamento binario diretto e API](/help/assets/developer-reference-material-apis.md#upload-binary).
   * Per un confronto dei metodi API disponibili per le operazioni CRUD di base, vedi [API e operazioni sulle risorse](/help/assets/developer-reference-material-apis.md#use-cases-and-apis).
* Il flusso di lavoro predefinito **[!UICONTROL Aggiornamento risorse DAM]** nelle versioni precedenti di [!DNL Experience Manager] non è più disponibile. Al contrario, i microservizi per le risorse forniscono un servizio scalabile e prontamente disponibile che copre la maggior parte dell’elaborazione delle risorse predefinita (rappresentazioni, estrazione dei metadati ed estrazione del testo per l’indicizzazione).
   * Consulta [configurare e utilizzare i microservizi per le risorse](/help/assets/asset-microservices-configure-and-use.md)
   * Per personalizzare i passaggi del flusso di lavoro nell’elaborazione, [flussi di lavoro di post-elaborazione](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) possono essere utilizzati.

* I componenti del sito web che forniscono un file binario senza alcuna trasformazione possono utilizzare il download diretto. Il servlet di GET Sling viene aggiornato per consentire agli sviluppatori di farlo per impostazione predefinita. I componenti del sito web che forniscono un binario con una certa trasformazione (ad esempio, ridimensionalo tramite un servlet) possono continuare a funzionare nello stato attuale.

Le rappresentazioni standard generate con i microservizi per le risorse vengono memorizzate in modo compatibile con le versioni precedenti nei nodi dell’archivio delle risorse utilizzando le stesse convenzioni di denominazione.

## Sviluppare e testare i microservizi per le risorse {#asset-microservices}

I microservizi per le risorse forniscono un’elaborazione scalabile e flessibile delle risorse utilizzando servizi cloud. Adobe gestisce i servizi cloud per una gestione ottimale dei diversi tipi di risorse e opzioni di elaborazione. I microservizi per le risorse aiutano a evitare la necessità di strumenti e metodi di rendering di terze parti (come [!DNL ImageMagick]) e semplificano le configurazioni, fornendo al tempo stesso funzionalità predefinite per i tipi di file più comuni. Ora puoi elaborare una [ampia gamma di tipi di file](/help/assets/file-format-support.md) coprono un maggior numero di formati predefiniti rispetto alle versioni precedenti di Experience Manager. Ad esempio, è ora possibile estrarre le miniature dei formati PSD e PSB che in precedenza richiedevano soluzioni di terze parti, come [!DNL ImageMagick]. Non è possibile utilizzare le configurazioni complesse di [!DNL ImageMagick] per [!UICONTROL Profili elaborazione] configurazione. Utilizzare [!DNL Dynamic Media] per la transcodifica FFmpeg avanzata dei video e utilizza i profili di elaborazione per [transcodifica di base di video MP4](/help/assets/manage-video-assets.md#transcode-video).

Asset microservices è un servizio nativo per il cloud fornito automaticamente e collegato via cavo a [!DNL Experience Manager] nei programmi e negli ambienti del cliente gestiti in Cloud Manager. Per estendere o personalizzare [!DNL Experience Manager], gli sviluppatori possono utilizzare il contenuto o le risorse esistenti con rappresentazioni generate in un ambiente cloud per testare e convalidare il codice utilizzando, visualizzando e scaricando le risorse.

Per eseguire una convalida end-to-end del codice e del processo, inclusi l’acquisizione e l’elaborazione delle risorse, distribuisci le modifiche del codice in un ambiente di sviluppo cloud utilizzando [la pipeline](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) e testare con l’esecuzione completa dell’elaborazione dei microservizi per le risorse.

## Parità di funzioni con [!DNL Experience Manager] 6,5 {#cloud-service-feature-status}

[!DNL Experience Manager] as a [!DNL Cloud Service] introduce molte nuove funzioni e modi più performanti per far funzionare le funzioni esistenti. Tuttavia, quando si passa da [!DNL Experience Manager] Da 6.5 a [!DNL Experience Manager] as a [!DNL Cloud Service]Tuttavia, è possibile notare che alcune funzioni funzionano diversamente, non sono disponibili o sono parzialmente disponibili. Di seguito è riportato un elenco di tali funzioni. Inoltre, consulta [funzioni obsolete e rimosse](/help/release-notes/deprecated-removed-features.md).

| Funzionalità o caso d’uso | Stato in [!DNL Experience Manager] as a [!DNL Cloud Service] | Commenti |
|-----|-----|-----|
| [Rilevamento di risorse duplicate](/help/assets/detect-duplicate-assets.md) | Funziona diversamente | Consulta [come funzionava in [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/duplicate-detection.html). |
| [Copie trasformate solo per posizionamento (FPO)](/help/assets/configure-fpo-renditions.md) | Funziona diversamente | I profili di elaborazione utilizzano i microservizi delle risorse per generare rappresentazioni FPO. Nell&#39;Experience Manager 6.5, una soluzione di terze parti come [!DNL ImageMagick] era disponibile per generare le rappresentazioni. |
| Writeback di metadati | Funziona diversamente | Disabilitata per impostazione predefinita. Se necessario, abilita il modulo di avvio del flusso di lavoro corrispondente. Il writeback viene gestito dai microservizi delle risorse. |
| Elaborazione delle risorse caricate tramite Gestione pacchetti | Necessità di intervento manuale | Rielabora manualmente utilizzando **[!UICONTROL Rielabora risorsa]** azione. |
| Rilevamento tipo MIME | Non supportato. | Se carichi una risorsa digitale senza un’estensione o con un’estensione non corretta, questa potrebbe non essere elaborata come desiderato. Gli utenti possono comunque memorizzare i file binari senza un’estensione in DAM. Consulta [Rilevamento del tipo MIME in [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/detect-asset-mime-type-with-tika.html). |
| Generazione di risorse secondarie per risorse composte | Non supportato. | I casi d’uso dipendenti come le annotazioni potrebbero non essere soddisfatti. Consulta [creazione di risorse secondarie in [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/managing-linked-subassets.html#generate-subassets). L’anteprima PDF di alcuni tipi di file è disponibile a partire da [Versione 2021.7.0](/help/release-notes/release-notes-cloud/release-notes-current.md). |
| Modificare le immagini | Non supportato | La modifica delle risorse non è supportata in Experience Manager as a Cloud Service. Consulta [come ha funzionato nell&#39;Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#editing-images). |
| Home page | Non supportato | Consulta [[!DNL Assets] Esperienza della pagina Home in [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-home-page.html) |
| Estrai risorse dall’archivio ZIP | Non supportato | Consulta [Estrazione ZIP in [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#extractzip). |
| Valutazioni risorse | Non supportato | Il widget di valutazione nell’editor schema metadati non è supportato. |
| Filtro di disposizione del contenuto | Non supportato | Un caso d’uso comune di `ContentDispositionFilter` consente agli amministratori di configurare [!DNL Experience Manager] per distribuire i file HTML e aprire i file PDF in linea anziché scaricarli. Nelle istanze Publish, puoi gestire la disposizione utilizzando la configurazione di Dispatcher. Nelle istanze Autore, Adobe non consiglia di modificare l’intestazione Disposizione contenuto. Consulta [Filtro eliminazione contenuto in [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/content-disposition-filter.html). |
| Modello servizio fotografico per prodotto | Non supportato | Consulta [modello servizio fotografico per prodotto in [!DNL Experience Manager] 6,5](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/projects/managing-product-information.html). |
| Traduzione intelligente | Non supportato | [Traduzione intelligente](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/translation/smart-translation-search-feature-video-use.html) non è supportato in [!DNL Experience Manager] as a [!DNL Cloud Service]. |
| WebDAV | Non supportato | Per delle alternative, vedi [[!DNL Creative Cloud] integrazione](/help/assets/aem-cc-integration-best-practices.md) o [Materiale di riferimento per sviluppatori](/help/assets/developer-reference-material-apis.md). |
| Interfaccia classica | Non supportato | È disponibile solo l’interfaccia touch. |

**Consulta anche**

* [Traduci risorse](translate-assets.md)
* [API HTTP di Assets](mac-api-assets.md)
* [Formati di file supportati dalle risorse](file-format-support.md)
* [Cerca risorse](search-assets.md)
* [Risorse collegate](use-assets-across-connected-assets-instances.md)
* [Rapporti sulle risorse](asset-reports.md)
* [Schemi metadati](metadata-schemas.md)
* [Scaricare le risorse](download-assets-from-aem.md)
* [Gestire i metadati](manage-metadata.md)
* [Facet di ricerca](search-facets.md)
* [Gestire le raccolte](manage-collections.md)
* [Importazione in blocco dei metadati](metadata-import-export.md)
* [Pubblicare risorse in AEM e Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>Sono disponibili le seguenti risorse per [!DNL Experience Manager] as a [!DNL Cloud Service]:
>
>* [Elenco delle funzioni obsolete e rimosse](/help/release-notes/deprecated-removed-features.md)
>* [Introduzione](/help/overview/introduction.md)
>* [Novità e differenze](/help/overview/what-is-new-and-different.md)
>* [Architettura](/help/overview/architecture.md)
>* [Modifiche di rilievo](/help/release-notes/aem-cloud-changes.md)
>* [Modifiche di rilievo [!DNL Sites]](/help/sites-cloud/sites-cloud-changes.md)
>* [Tutorial video](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html?lang=it)
