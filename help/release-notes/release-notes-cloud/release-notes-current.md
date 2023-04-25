---
title: Note sulla versione corrente per  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione corrente per  [!DNL Adobe Experience Manager]  as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: eb42c39af65f1e10417d855e5ad476cafc97da45
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 33%

---

# Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note specifiche sulla versione corrente (più recente) di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti; per esempio, quelle del 2021, 2022 e così via.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

Data di rilascio di [!DNL Adobe Experience Manager] come [!DNL Cloud Service] la versione corrente della funzione (2023.2.0) è il 12 aprile 2023. Il prossimo rilascio di nuove funzioni (2023.4.0) è pianificato per il 18 maggio 2023.

## Video sulla versione {#release-video}

Per un riepilogo delle funzioni aggiunte nella versione 2023.2.0, guarda il video Panoramica sulla versione di febbraio 2023:

>[!VIDEO](https://video.tv.adobe.com/v/3416885/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni in [!DNL Experience Manager Sites] affittare {#prerelease-sites}

* Esporta frammenti di contenuto da AEM as a cloud service a Adobe target come offerte JSON.
* Il supporto per l’impaginazione e l’ordinamento di GraphQL, insieme ai miglioramenti apportati al caching interno, ora consente di migliorare le prestazioni delle applicazioni client disaccoppiate quando si recuperano set di contenuti di grandi dimensioni dalle AEM utilizzando query e filtri GraphQL complessi.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

* Nuovo supporto per protocollo (DASH - Dynamic Adaptive Streaming su HTTP) avviato per lo streaming adattivo nella distribuzione video Dynamic Media (con CMAF abilitato):
   * Lo streaming adattivo (DASH/HLS) garantisce una migliore esperienza di visualizzazione da parte dell&#39;utente finale per i video
   * DASH è il protocollo standard internazionale per lo streaming video adattivo ed è ampiamente adottato nel settore
   * Disponibile in NA, per l&#39;abilitazione tramite ticket di supporto, disponibile a breve in APAC, EMEA

* È stato aggiunto il supporto per le immagini WebP per estrarre automaticamente i metadati, generare miniature e rappresentazioni personalizzate. Per questi file sono ora supportate anche le funzionalità di Smart Tag e Smart Crop .

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni disponibili in [!DNL Forms] {#new-features-available-in-channel}

* **[Utilizza i componenti core di acquisizione dei dati per generare moduli adattivi](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it)**: [utilizza l’editor dei moduli adattivi](/help/forms/creating-adaptive-form-core-components.md) per creare moduli basati su componenti di acquisizione dei dati standardizzati (componenti core). Questi componenti forniscono funzionalità di personalizzazione e riducono i tempi di sviluppo e i costi di manutenzione per le esperienze di registrazione digitale.

* **[Supporto della pipeline front-end per lo stile basato su componenti adattativi Forms](/help/forms/using-themes-in-core-components.md)**: Utilizza temi standardizzati basati su BEM per Forms adattivo basato su componenti core distribuendoli con la pipeline di distribuzione Frontend per migliorare l’aspetto dei moduli e allinearli alle linee guida di progettazione approvate dal marchio della tua organizzazione.

* **[Genera documento di record per Forms adattivo basato su componenti core](/help/forms/generate-document-of-record-core-components.md)**: Crea un documento contenente i dati inviati per Adaptive Forms generato utilizzando i componenti core per l&#39;archiviazione o riferimento agli utenti finali, in stampa o in formato documento.

![https://www.aemcomponents.dev/](/help/forms/assets/sample-core-components-based-adaptive-form.png)

* **[Creazione efficiente di moduli con la funzione Salva un modulo adattivo come modello](/help/forms/template-editor.md#save-an-adaptive-form-as-template-saving-adaptive-form-as-template)**: Accelerare e standardizzare lo sviluppo dei moduli salvando i moduli approvati dal marchio esistenti come modelli di modulo da riutilizzare rapidamente.

* **[Collegare AEM Forms ai database supportati da JDBC](/help/forms/configure-data-sources.md#configure-relational-database-configure-relational-database)**: Collegati ai database aziendali direttamente da AEM Cloud Service utilizzando il protocollo JDBC, senza la necessità di esporli tramite REST API.

* **[Integrare con gli endpoint REST utilizzando Open API 3.0](/help/forms/configure-data-sources.md#configure-restful-services-open-api-specification-version-20-configure-restful-services-swagger-version30)**: Integrazione perfetta nei sistemi di record che supportano Open API 3.0 per memorizzare e recuperare i dati utilizzando modelli di dati dei moduli.

* **[Condividi un modulo adattivo per la revisione](/help/forms/create-reviews-forms.md)**: utilizza il meccanismo di revisione dei moduli adattivi per consentire a uno o più revisori di rivedere il modulo.


### Funzioni in [!DNL Forms] prerelease {#prerelease-features-forms}

* **[Inviare Forms adattivo a Microsoft SharePoint e Microsoft OneDrive](/help/forms/configuring-submit-actions.md)**: Migliorare l’agilità degli utenti aziendali per avviare rapidamente nuovi moduli e archiviare i dati inviati in strumenti quotidiani, ad esempio il sito Microsoft SharePoint o la cartella OneDrive.

![Inviare Forms adattivo a Microsoft SharePoint e Microsoft OneDrive](/help/forms/assets/onedrive-and-sharepoint.jpg)


## Programma di adozione precoce Forms headless {#forms-early-adopter}

Utilizza l’interfaccia adattiva headless per consentire agli sviluppatori di creare, pubblicare e gestire moduli interattivi a cui è possibile accedere e interagire tramite API, anziché tramite un’interfaccia utente grafica tradizionale. I moduli adattivi headless consentono di:

* creare moduli multicanale di alta qualità nel linguaggio di programmazione desiderato
* integrare i moduli in modo nativo nelle app desktop e mobili, nei siti web e nelle applicazioni di chat
* riutilizzare i componenti dell’interfaccia utente proprietari con le applicazioni dei moduli
* sfruttare la potenza di Adobe Experience Manager Forms

Puoi inviare un&#39;e-mail a aem-forms-headless@adobe.com dal tuo ID e-mail ufficiale per partecipare al programma di primo adozione.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui.](/help/implementing/cloud-manager/release-notes/current.md)

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
