---
title: Note sulla versione 2023.2.0 di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione 2023.2.0 di [!DNL Adobe Experience Manager]  as a Cloud Service.
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 97%

---


# Note sulla versione 2023.2.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione funzionale 2023.2.0 di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti; per esempio, quelle del 2021, 2022 e così via.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

La data di rilascio della versione corrente della funzione di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2023.2.0) è il 12 aprile 2023. La prossima versione (2023.4.0) è prevista per il 7 giugno 2023.

## Video sulla versione {#release-video}

Dai un’occhiata al video Panoramica sulla versione di febbraio 2023 per un riepilogo delle funzioni aggiunte nella versione 2023.2.0:

>[!VIDEO](https://video.tv.adobe.com/v/3416885/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni in [!DNL Experience Manager Sites] prerelease {#prerelease-sites}

* Esporta frammenti di contenuto da AEM as a Cloud Service in Adobe Target come offerte JSON.
* Il supporto per la paginazione e l’ordinamento di GraphQL, insieme ai miglioramenti apportati alla memorizzazione nella cache interna, ora consente di migliorare le prestazioni delle applicazioni client separate quando si recuperano set di contenuti di grandi dimensioni da AEM utilizzando query e filtri GraphQL complessi.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

* Lancio del supporto per il nuovo protocollo (DASH - Dynamic Adaptive Streaming over HTTP) per lo streaming adattivo nella distribuzione video Dynamic Media (con CMAF abilitato):
   * Lo streaming adattivo (DASH/HLS) garantisce agli utenti finali una migliore esperienza di visualizzazione dei video
   * DASH è il protocollo standard internazionale per lo streaming video adattivo ed è ampiamente adottato nel settore
   * Disponibile in NA, si abilita tramite ticket di supporto, disponibile a breve nella regione APAC (Asia-Pacifico) e nella regione EMEA (Europa, Medio Oriente, Africa)

* È stato aggiunto il supporto per le immagini WebP per estrarre automaticamente i metadati, generare miniature e rappresentazioni personalizzate. Per questi file sono ora supportate anche le funzionalità di Tag avanzati e Ritaglio avanzato.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni disponibili in [!DNL Forms] {#new-features-available-in-channel}

* **[Utilizza i componenti core di acquisizione dei dati per generare moduli adattivi](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it)**: [utilizza l’editor dei moduli adattivi](/help/forms/creating-adaptive-form-core-components.md) per creare moduli basati su componenti di acquisizione dei dati standardizzati (componenti core). Questi componenti forniscono funzionalità di personalizzazione e riducono i tempi di sviluppo e i costi di manutenzione per le esperienze di registrazione digitale.

* **[Supporto della pipeline di front-end per lo stile dei moduli adattivi basati su componenti core](/help/forms/using-themes-in-core-components.md)**: utilizza temi standardizzati basati su BEM per i moduli adattivi basati su componenti core, implementandoli con una pipeline di distribuzione di front-end per migliorare l’aspetto dei moduli e allinearli alle linee guida per la progettazione approvate dal marchio dell’organizzazione.

* **[Genera un documento di record per moduli adattivi basati su componenti core](/help/forms/generate-document-of-record-core-components.md)**: crea un documento di record contenente i dati inviati per i moduli adattivi, generato utilizzando i componenti core come archiviazione o riferimento per gli utenti finali, nel formato di stampa o in quello di documento.

![https://www.aemcomponents.dev/](/help/forms/assets/sample-core-components-based-adaptive-form.png)

* **[Creazione efficiente di moduli con la funzione “Salva un modulo adattivo come modello”](/help/forms/template-editor.md#save-an-adaptive-form-as-template-saving-adaptive-form-as-template)**: velocizza e uniforma lo sviluppo dei moduli salvando i moduli esistenti approvati dal marchio come modelli di modulo da riutilizzare rapidamente.

* **[Connessione di AEM Forms ai database supportati da JDBC](/help/forms/configure-data-sources.md#configure-relational-database-configure-relational-database)**: consente di connettersi ai database aziendali direttamente da AEM Cloud Service utilizzando il protocollo JDBC, senza la necessità di esporli tramite API REST.

* **[Integrazione con gli endpoint REST utilizzando Open API 3.0](/help/forms/configure-data-sources.md#configure-restful-services-open-api-specification-version-20-configure-restful-services-swagger-version30)**: integrazione perfetta nei sistemi di record che supportano Open API 3.0 per memorizzare e recuperare i dati utilizzando modelli di dati per moduli.

* **[Condividi un modulo adattivo per la revisione](/help/forms/create-reviews-forms.md)**: utilizza il meccanismo di revisione dei moduli adattivi per consentire a uno o più revisori di rivedere il modulo.


### Funzioni nella versione prerelease di [!DNL Forms] {#prerelease-features-forms}

* **[Invio di moduli adattivi a Microsoft SharePoint e Microsoft OneDrive](/help/forms/configuring-submit-actions.md)**: migliora l’agilità degli utenti aziendali per inviare rapidamente nuovi moduli e archiviare i dati inviati in strumenti di uso quotidiano, ad esempio il sito Microsoft SharePoint o la cartella OneDrive.

![Invio di moduli adattivi a Microsoft SharePoint e Microsoft OneDrive](/help/forms/assets/onedrive-and-sharepoint.jpg)


## Programma dei moduli adattivi headless per i primi utilizzatori {#forms-early-adopter}

Utilizza i moduli adattivi headless per consentire agli sviluppatori di creare, pubblicare e gestire moduli interattivi a cui è possibile accedere e con cui si può interagire tramite API, anziché tramite un’interfaccia utente grafica tradizionale. I moduli adattivi headless consentono di:

* creare moduli multi-canale di alta qualità nel linguaggio di programmazione desiderato
* integrare in modo nativo i moduli nelle app desktop e per dispositivi mobili, nei siti web e nelle applicazioni chat
* riutilizzare i componenti proprietari dell’interfaccia utente con le applicazioni di Forms
* sfrutta la potenza di Adobe Experience Manager Forms

È possibile inviare un’e-mail all’indirizzo aem-forms-headless@adobe.com dal proprio ID e-mail ufficiale per aderire al programma per i primi utilizzatori.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui.](/help/implementing/cloud-manager/release-notes/current.md)

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
