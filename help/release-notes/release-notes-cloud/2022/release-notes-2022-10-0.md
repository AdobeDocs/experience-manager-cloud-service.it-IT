---
title: Note sulla versione 2022.10.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2022.10.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 8fce7c50-f322-4bcf-bd76-390faedfd5b7
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 79%

---

# Note sulla versione 2022.10.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione 2022.10.0 di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti; per esempio, quelle del 2020, 2021 e così via.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

La data di rilascio della versione mensile corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2022.10.0) è il 10 novembre 2022. La prossima versione mensile (2023.1.0) è prevista per il 9 febbraio 2023.

## Video sulla versione {#release-video}

Dai un’occhiata al video di panoramica sulla versione di ottobre 2022 per un riepilogo delle funzioni aggiunte alla versione 2022.10.0:

>[!VIDEO](https://video.tv.adobe.com/v/3409801/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}


### Nuove funzioni in [!DNL Sites] {#sites-features}

* Il [Scheda Personalizzazione per frammenti esperienza](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#personalization-experience-fragment) consente di specificare la segmentazione nell’Editor frammento di esperienza e la flessibilità necessaria per creare frammenti di esperienza nidificati, con cui è possibile creare varianti di intestazioni e piè di pagina per più segmenti. Prima dell’introduzione di questa funzione, la funzionalità di personalizzazione di AEM era disponibile solo per le pagine del sito, ma non per i frammenti esperienza.

* La [Console Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) ora consente agli utenti di gestire in modo efficiente i frammenti di contenuto tradotti. Inoltre, è possibile accedere con 1 solo clic per visualizzare tutte le copie delle varie lingue. Gli utenti possono anche filtrare la visualizzazione a tabella in base alla lingua che desiderano.

![Lingue dei frammenti di contenuto](/help/release-notes/assets/cfconsole-languages.png)

* Riduci ulteriormente il tempo di caricamento delle pagine per i visitatori ottimizzando le impostazioni delle dimensioni delle immagini nei modelli. Per ulteriori informazioni sul componente immagine, visita [Componente WCM Core](https://github.com/adobe/aem-core-wcm-components).

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

* Experience Manager Assets ora consente di caricare documenti in altri tipi di formati supportati e[visualizzali in anteprima utilizzando il visualizzatore di Document Cloud incluso](/help/assets/manage-pdf-documents.md). I tipi di formato supportati sono TXT, RTF, DOC, DOCX, PPT, PPTX, XLS e XLSX.

  ![Rappresentazione di PDF per altri formati](/help/release-notes/assets/multi-page-other-formats.png)


### Nuove funzioni nella versione prerelease di [!DNL Assets] {#prerelease-features-assets}

* Experience Manager Assets ora utilizza un framework di intelligenza artificiale migliorato per i tag avanzati delle immagini. Offre un livello di intelligence sui contenuti che migliora la pertinenza e la precisione dei tag avanzati per tutte le risorse di immagini al momento della loro acquisizione. Inoltre, le informazioni sull’orientamento vengono inserite in `cq:tags` e quindi utilizzate per ottenere risultati di ricerca migliori mediante il filtro Orientamento.

  Se ti interessa partecipare alla versione beta, [compila questo modulo](https://forms.office.com/pages/responsepage.aspx?id=Wht7-jR7h0OUrtLBeN7O4epXZrTVKKdJkUiHeolccf9UNEwyNEpHVEFaODdBNFZQSlFDREZQOVRRTy4u) entro il 14 novembre.

* Experience Manager Assets adesso [supporta il token SAS](/help/assets/add-assets.md#asset-bulk-ingestor) oltre alla chiave di accesso per l’autenticazione durante la connessione all’origine dati Archiviazione BLOB di Azure per l’acquisizione delle risorse tramite lo strumento Importazione in blocco.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni disponibili nel canale prerelease di [!DNL Forms] {#prerelease-features-forms}

* **Editor modelli per Forms adattivo**: l’editor di modelli ti consente di predefinire la struttura e l’aspetto di base del Forms adattivo di un’organizzazione. Questa versione apporta i seguenti miglioramenti all’editor di modelli:
   * **[Modello per dati modulo nell’editor modelli](/help/forms/creating-adaptive-form.md#edit-form-model-properties-of-an-adaptive-form-edit-form-model)**: è possibile associare uno schema Modello dati modulo a un modello per moduli adattivi nell’editor modelli. Questo consente di velocizzare la creazione di un modulo adattivo. La stessa opzione è stata aggiunta anche all’editor di moduli adattivi per consentire agli utenti di selezionare o cambiare il modello di dati per i moduli esistenti.
   * **[Documento di record nell’editor modelli](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform)**: ora è possibile standardizzare la generazione di documenti di record per tutti i moduli creati utilizzando un modello. Questo aiuta a migliorare la conformità e la standardizzazione in base ai requisiti dell’organizzazione.

* **[Avviare la procedura guidata Moduli adattivi da una pagina AEM Sites](/help/forms/embed-adaptive-form-aem-sites.md)**: il supporto per moduli adattivi è stato esteso alla pagina di AEM Sites. È ora possibile creare un nuovo modulo adattivo o incorporarne uno esistente direttamente nella pagina di AEM Sites.
* **[Modificare l’allineamento della visualizzazione per caselle di controllo e pulsanti di scelta in DoR](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#customize-the-branding-information-in-document-of-record-customize-the-branding-information-in-document-of-record)**: ora è possibile impostare l’allineamento desiderato (Orizzontale, Verticale, Come moduli adattivi) per le caselle di controllo e i pulsanti di scelta nel documento di record. Questa opzione determina il posizionamento delle opzioni di caselle di controllo e pulsanti di scelta nel documento di record.

## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* Gli autori possono arricchire dinamicamente gli elenchi di prodotti con Frammenti di esperienza (ad esempio, inserendo un banner tra le voci dei prodotti elencati).
* Il componente Elenco ora supporta le pagine o categorie di prodotti associate per mostrare in modo dinamico le pagine correlate.
* È stato aggiunto il supporto per i componenti Peregrine 12.5.
* È stato aggiunto il supporto per il caricamento dei prezzi lato client nei teaser e nei caroselli di prodotti.

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### Novità {#what-is-new-foundation}

* AEM as a Cloud Service (servizio di authoring) è ora integrato con Unified Shell per migliorare l’esperienza utente e per coerenza con tutte le altre applicazioni di Experience Cloud. Vedi AEM as a [Cloud Service su Unified Shell](/help/overview/aem-cloud-service-on-unified-shell.md) per ulteriori dettagli.

* Come indicato in precedenza nelle note sulla versione, l’utilizzo della schermata di amministrazione dell’agente di replica o dell’API di replica per la distribuzione di pacchetti di contenuto di dimensioni superiori a 10 MB (nodi con proprietà, esclusi i binari) ora è obsoleto e viene applicato. Consulta [Gestisci pubblicazione](/help/operations/replication.md#manage-publication) o [Flusso di lavoro per la pubblicazione della struttura dei contenuti](/help/operations/replication.md#publish-content-tree-workflow) per suggerimenti su come replicare questi pacchetti di contenuti di grandi dimensioni.

* La configurazione del Dispatcher ora fa riferimento a un file in cui sono elencati i parametri comuni di query per campagne di marketing. I clienti possono scegliere di rimuovere la notazione di commento dai parametri di cui hanno bisogno, con conseguente miglioramento della memorizzazione in cache. Consulta [Parametri della campagna di marketing](/help/implementing/dispatcher/caching.md#marketing-parameters) per ulteriori dettagli.

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes/current.md).

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
