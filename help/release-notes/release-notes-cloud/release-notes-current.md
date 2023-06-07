---
title: Note sulla versione corrente per  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione corrente per  [!DNL Adobe Experience Manager]  as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 3a17f02b6544669e07adabfd4f50905eb6afd51e
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 41%

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

La data di rilascio di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] la versione corrente (2023.4.0) è il 7 giugno 2023. La prossima versione (2023.6.0) è prevista per il 29 giugno 2023.

## Video sulla versione {#release-video}

Dai un’occhiata al video Panoramica sulla versione di aprile 2023 per un riepilogo delle funzioni aggiunte alla versione 2023.4.0:

>[!VIDEO](https://video.tv.adobe.com/v/3418681/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni in [!DNL Experience Manager Sites] {#sites-features}

* Esporta frammenti di contenuto da AEM as a Cloud Service in Adobe Target come offerte JSON.
* Il supporto per la paginazione e l’ordinamento di GraphQL, insieme ai miglioramenti apportati alla memorizzazione nella cache interna, ora consente di migliorare le prestazioni delle applicazioni client separate quando si recuperano set di contenuti di grandi dimensioni da AEM utilizzando query e filtri GraphQL complessi.

### Nuove funzioni in [!DNL Experience Manager Sites] prelease {#prerelease-sites}

* Ora è possibile pubblicare i frammenti di contenuto e i relativi riferimenti in [Servizio di anteprima AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=en#access-preview-service) utilizzando [Console Frammenti di contenuto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=en), che consente agli utenti di visualizzare in anteprima l’esperienza finale su un’applicazione di anteprima separata prima della pubblicazione.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

* È stato aggiunto il supporto per le immagini WebP per estrarre automaticamente i metadati, generare miniature e rappresentazioni personalizzate. Per questi file è ora supportata anche la funzionalità Tag avanzati. Le funzionalità di Dynamic Media non sono supportate per WebP come formato di input.

* [Miglioramenti all’esperienza di ricerca](/help/assets/search-assets.md#aftersearch) - È ora possibile eseguire rapidamente le seguenti operazioni sulle risorse visualizzate nei risultati di ricerca:

   * Creare un flusso di lavoro
   * Crea una nuova versione
   * Correlare o non correlare le risorse

      Per eseguire queste operazioni, non è necessario passare alla posizione della risorsa e visualizzarne le proprietà.

* Miglioramenti apportati all’usabilità del facet di ricerca colore: il campo di input per i valori dei colori è ora modificabile e i risultati della ricerca vengono aggiornati solo quando esci dal selettore colore.

* Lancio del supporto per il nuovo protocollo (DASH - Dynamic Adaptive Streaming over HTTP) per lo streaming adattivo nella distribuzione video Dynamic Media (con CMAF abilitato):
   * Lo streaming adattivo (DASH/HLS) garantisce agli utenti finali una migliore esperienza di visualizzazione dei video
   * DASH è il protocollo standard internazionale per lo streaming video adattivo ed è ampiamente adottato nel settore
   * Disponibile in tutte le aree geografiche, da attivare tramite ticket di supporto

* Dynamic Media _Snapshot_ - Sperimentate immagini di prova o URL Dynamic Media per vedere l&#39;output di diversi modificatori di immagini e ottimizzazioni Smart Imaging per le dimensioni dei file (con distribuzione WebP e AVIF), la larghezza di banda della rete e le proporzioni pixel del dispositivo. Consulta [Snapshot Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html).

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni disponibili in [!DNL Forms] {#new-features-available-in-channel}

* **[Invio di moduli adattivi a Microsoft SharePoint e Microsoft OneDrive](/help/forms/configuring-submit-actions.md)**: migliora l’agilità degli utenti aziendali per inviare rapidamente nuovi moduli e archiviare i dati inviati in strumenti di uso quotidiano, ad esempio il sito Microsoft SharePoint o la cartella OneDrive.

![Invio di moduli adattivi a Microsoft SharePoint e Microsoft OneDrive](/help/forms/assets/onedrive-and-sharepoint.jpg)


### Funzioni nella versione prerelease di [!DNL Forms] {#prerelease-features-forms}

* Integrazione e conformità migliorate di Adobe Acrobat Sign: AEM Forms ora si integra con Adobe Acrobat Sign for Government, fornendo un livello avanzato di conformità e sicurezza per le firme elettroniche con l’invio di moduli adattivi per gli account associati alla pubblica amministrazione (dipartimenti e agenzie governative).

L’integrazione con Adobe Acrobat Sign for Government consente ai nostri partner e ai clienti governativi di utilizzare le firme elettroniche in Adaptive Forms per alcune delle linee di business più critiche e sensibili. Questo ulteriore livello di sicurezza assicura che tutte le firme elettroniche siano pienamente conformi alla conformità FedRAMP Moderate, garantendo ai nostri clienti governativi la massima tranquillità.

* Forms adattivo nell’editor di AEM Sites: ora puoi utilizzare l’editor di AEM Sites per creare e aggiungere rapidamente più moduli alle pagine dei siti. Questa funzionalità consente agli autori di contenuti di creare esperienze di acquisizione dati fluide all’interno delle pagine Sites utilizzando la potenza dei componenti per moduli adattivi, tra cui comportamento dinamico, convalide, integrazione dei dati, generazione di documenti di record e automazione dei processi aziendali. Operazioni disponibili:

   * Crea un modulo adattivo trascinando i componenti del modulo nel componente Contenitore adattivo Forms nell’editor di AEM Sites.
   * Utilizza l’Adaptive Forms Wizard (procedura guidata adattiva) nell’editor di AEM Sites per creare moduli indipendenti da qualsiasi pagina Sites, consentendoti di riutilizzare tali moduli su più pagine.
   * Aggiungere più moduli a una pagina Sites per semplificare l’esperienza utente e fornire maggiore flessibilità.

   >[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

* Migliorare la gestione degli errori con gestori degli errori personalizzati nell’editor delle regole: ora puoi richiamare una funzione personalizzata (utilizzando la libreria client) in risposta a un errore restituito da un servizio esterno e fornire una risposta personalizzata agli utenti finali o eseguire azioni specifiche per gli errori restituiti da un servizio. Ad esempio, puoi richiamare un flusso di lavoro personalizzato nel backend per codici di errore specifici o informare il cliente che il servizio non è disponibile.

Questo consente di migliorare la capacità complessiva di gestione degli errori introducendo risposte di errore basate su standard, compatibili con le versioni precedenti dei gestori degli errori OOTB, con maggiore flessibilità e controllo.

## Programma dei moduli adattivi headless per i primi utilizzatori {#forms-early-adopter}

Utilizza i moduli adattivi headless per consentire agli sviluppatori di creare, pubblicare e gestire moduli interattivi a cui è possibile accedere e con cui si può interagire tramite API, anziché tramite un’interfaccia utente grafica tradizionale. I moduli adattivi headless consentono di:

* creare moduli multi-canale di alta qualità nel linguaggio di programmazione desiderato
* integrare in modo nativo i moduli nelle app desktop e per dispositivi mobili, nei siti web e nelle applicazioni chat
* riutilizzare i componenti proprietari dell’interfaccia utente con le applicazioni di Forms
* sfruttare la potenza di Adobe Experience Manager Forms

Puoi inviare un’e-mail a `aem-forms-headless@adobe.com` dal tuo ID e-mail ufficiale per partecipare al programma early adopter.

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Novità {#what-is-new-foundation}

* Aree geografiche di pubblicazione aggiuntive: i clienti di Sites possono concedere in licenza fino a tre aree di pubblicazione, oltre all’area principale. Il traffico viene indirizzato ad altre farm di pubblicazione, il che si traduce in una latenza ridotta per alcune richieste e in una maggiore resilienza contro interruzioni regionali. Contatta il tuo Adobe Account Manager per informazioni sulle licenze [Aree geografiche di pubblicazione aggiuntive](/help/operations/additional-publish-regions.md) per i programmi.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui.](/help/implementing/cloud-manager/release-notes/current.md)

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
