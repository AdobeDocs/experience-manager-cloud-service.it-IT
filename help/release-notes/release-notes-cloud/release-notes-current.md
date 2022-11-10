---
title: Note sulla versione corrente per  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione corrente per  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 218f162bcf9eb9a4bd3097348dd7893a5160bed3
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 16%

---


# Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione per la versione corrente (più recente) di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti; per esempio, quelle del 2020, 2021 e così via.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

>[!CAUTION]
>
>**Periodo di esclusione manutenzione Black Friday e Christmas**
>
> Non verrà eseguita alcuna manutenzione automatica di AEMaaCS nei seguenti intervalli di tempo, a partire dalla mezzanotte (00:00) CET:
>
>* Lunedì 21 Novembre - Lunedì 5 Dicembre
>* Lunedì 19 dicembre - Martedì 3 gennaio
>
> Questi periodi coprono Black Friday, Cyber Monday, Natale e Capodanno.

## Data di pubblicazione {#release-date}

Data di rilascio di [!DNL Adobe Experience Manager] come [!DNL Cloud Service] il rilascio mensile attuale (2022.10.0) è il 10 novembre 2022. La prossima versione mensile (2023.1.0) è prevista per il 26 gennaio 2022.

## Video sulla versione {#release-video}

Guarda il video Panoramica sulla versione di ottobre 2022 per un riepilogo delle funzioni aggiunte nella versione 2022.10.0:

>[!VIDEO](https://video.tv.adobe.com/v/3409801/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}


### Nuove funzioni in [!DNL Sites] {#sites-features}

* La [Scheda Personalizzazione per frammenti esperienza](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#personalization-experience-fragment) consente di creare specifiche di segmentazione per l’Editor frammento esperienza e la flessibilità necessaria per creare frammenti esperienza nidificati, in cui è possibile creare varianti di intestazioni e piè di pagina per più segmenti. Prima dell’avvio di questa funzione, la personalizzazione offerta da AEM è disponibile solo per le pagine del sito, ma non per i frammenti esperienza

* La [Console Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) ora consente agli utenti di gestire in modo efficiente i frammenti di contenuto tradotti. È stato fornito un accesso con 1 clic per visualizzare anche tutte le copie della lingua. Gli utenti possono inoltre filtrare la visualizzazione della tabella in base alle impostazioni internazionali di interesse.

![Lingue dei frammenti di contenuto](/help/release-notes/assets/cfconsole-languages.png)

* Riduci ulteriormente il tempo di caricamento delle pagine per i visitatori ottimizzando le impostazioni delle dimensioni delle immagini nei modelli. Per ulteriori informazioni sul componente immagine, visita [Componente WCM core](https://github.com/adobe/aem-core-wcm-components)

## [!DNL Experience Manager Assets] come [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

* Experience Manager Assets ora consente di caricare documenti in altri tipi di formati supportati e[ visualizzarli in anteprima utilizzando il visualizzatore di Document Cloud incluso](/help/assets/manage-pdf-documents.md). I tipi di formato supportati sono TXT, RTF, DOC, DOCX, PPT, PPTX, XLS e XLSX.

   ![Rendering di PDF per altri formati](/help/release-notes/assets/multi-page-other-formats.png)


### Nuove funzioni in [!DNL Assets] prerelease {#prerelease-features-assets}

* Experience Manager Assets ora utilizza un framework di intelligenza artificiale migliorato per i tag avanzati delle immagini. Questa intelligenza dei contenuti consente di migliorare la pertinenza e la precisione dei tag avanzati disponibili per tutte le risorse di immagini al momento dell’acquisizione. Inoltre, le informazioni sull’orientamento vengono compilate in `cq:tags`, che consente di ottenere risultati di ricerca migliori utilizzando il filtro Orientamento .

   Se siete interessati a partecipare alla Beta, [compilare il modulo](https://forms.office.com/pages/responsepage.aspx?id=Wht7-jR7h0OUrtLBeN7O4epXZrTVKKdJkUiHeolccf9UNEwyNEpHVEFaODdBNFZQSlFDREZQOVRRTy4u) entro il 14 novembre.

* Experience Manager Assets [supporta il token SAS](/help/assets/add-assets.md#asset-bulk-ingestor) oltre alla chiave di accesso per l’autenticazione durante la connessione all’origine dati Archiviazione BLOB di Azure per l’acquisizione delle risorse tramite lo strumento Importazione in blocco.

## [!DNL Experience Manager Forms] come [!DNL Cloud Service] {#forms}

### Nuove funzioni disponibili nel canale prerelease di [!DNL Forms] {#prerelease-features-forms}

* **Editor modelli Forms adattivo**: L’editor di modelli ti consente di predefinire la struttura e l’aspetto di base di Adaptive Forms di un’organizzazione. Questa versione apporta i seguenti miglioramenti all’editor modelli:
   * **[Modello dati modulo nell’editor modelli](/help/forms/creating-adaptive-form.md#edit-form-model-properties-of-an-adaptive-form-edit-form-model)**: È possibile associare uno schema Modello dati modulo a un modello Modulo adattivo nell’editor modelli. Consente di ridurre il tempo necessario per creare un modulo adattivo. L’opzione viene aggiunta anche all’editor di Forms adattivo per consentire agli utenti di selezionare o modificare il modello dati del modulo per i moduli esistenti.
   * **[Documento di record nell’editor modelli](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#document-of-record-support-in-adaptive-form-editor-dor-support-in-adaptiveform)**: È ora possibile standardizzare la generazione di documenti di record per tutti i moduli creati utilizzando un modello. Questo aiuta a migliorare la conformità e la standardizzazione per i requisiti dell&#39;organizzazione.

* **[Avvia la procedura guidata Moduli adattivi da una pagina AEM Sites](/help/forms/embed-adaptive-form-aem-sites.md)**: La pagina AEM Sites ha esteso il supporto per Adaptive Forms. È ora possibile creare un nuovo modulo adattivo o incorporarne uno esistente mentre si trova nella pagina AEM Sites.
* **[Modificare l’allineamento della visualizzazione per le caselle di controllo e il pulsante di scelta rapida in DoR](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#customize-the-branding-information-in-document-of-record-customize-the-branding-information-in-document-of-record)**: È ora possibile impostare l’allineamento desiderato (orizzontale, verticale, uguale a Forms adattivo) per le caselle di controllo e i pulsanti di scelta nel documento di record. Questa opzione determina il posizionamento delle opzioni di casella di controllo e pulsante di scelta nel documento di registrazione.

## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* Gli autori possono arricchire dinamicamente gli elenchi di prodotti con Frammenti esperienza (ad esempio: inserire banner tra gli elenchi dei prodotti).
* Il componente Elenco supporta ora le pagine di prodotti/categorie associate per mostrare in modo dinamico le pagine correlate.
* È stato aggiunto il supporto per i componenti Peregrine 12.5 .
* È stato aggiunto il supporto per il caricamento dei prezzi lato client nel teaser e nel carosello del prodotto.

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### Novità {#what-is-new-foundation}

* AEM as a Cloud Service (Author Service) è ora integrato con Unified Shell per migliorare l’esperienza utente e unificarla a tutte le altre applicazioni di Experience Cloud. Fai riferimento a AEM come a [Cloud Service sulla shell unificata](/help/overview/aem-cloud-service-on-unified-shell.md) per ulteriori dettagli.

* Come indicato in precedenza nelle note sulla versione, l’utilizzo della schermata di amministrazione dell’agente di replica o dell’API di replica per la distribuzione di pacchetti di contenuti di dimensioni superiori a 10 MB (nodi con proprietà, esclusi i binari) è obsoleto e verrà applicato nei prossimi giorni. Fai riferimento a [Gestisci pubblicazione](/help/operations/replication.md#manage-publication) o [Flusso di lavoro Pubblica albero del contenuto](/help/operations/replication.md#publish-content-tree-workflow) per gli approcci suggeriti per la replica di questi pacchetti di contenuti di grandi dimensioni.

* La configurazione del Dispatcher ora fa riferimento a un file che elenca i parametri comuni di query della campagna di marketing. I clienti possono scegliere di rimuovere il commento dai parametri rilevanti per loro, con conseguente miglioramento della memorizzazione in cache. Fai riferimento a [Parametri della campagna di marketing](/help/implementing/dispatcher/caching.md#marketing-parameters) per ulteriori dettagli.

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md).

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
