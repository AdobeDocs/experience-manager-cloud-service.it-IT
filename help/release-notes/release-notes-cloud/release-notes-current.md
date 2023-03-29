---
title: Note sulla versione corrente per  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione corrente per  [!DNL Adobe Experience Manager]  as a Cloud Service.
mini-toc-levels: 1
source-git-commit: b47901d749712384506cf4eb03c099027933e95f
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 99%

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

La data di rilascio della versione corrente (2023.1.0) di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] è il 9 febbraio 2023. Il prossimo rilascio di nuove funzioni (2023.2.0) è pianificato per il 6 aprile 2023.

## Video sulla versione {#release-video}

Dai un’occhiata al video Panoramica sulla versione di gennaio 2023 per un riepilogo delle funzioni aggiunte alla versione 2023.1.0:

>[!VIDEO](https://video.tv.adobe.com/v/3413479/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni nella versione prerelease di [!DNL Sites] {#prerelease-features-sites}

* L’API di distribuzione dei contenuti AEM GraphQL ora supporta il [paging](/help/headless/graphql-api/content-fragments.md#paging) e l’[ordinamento](/help/headless/graphql-api/content-fragments.md#sorting) GraphQL per rendere più efficiente il recupero e il rendering di set di contenuti di grandi dimensioni. L’impaginazione GraphQL consente di migliorare i tempi di risposta delle query perché restituisce i risultati in sottoinsiemi, anziché in una sola volta. L’ordinamento GraphQL consente di inserire i set di contenuti nell’ordine desiderato, semplificando l’elaborazione del contenuto da parte dell’applicazione client.  Il tempo di risposta alle query è stato ulteriormente migliorato con il filtro ibrido nel motore GraphQL dell’AEM. Il contenuto viene ora letto da JCR in set più piccoli che corrispondono ai filtri di query.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

* I rapporti sulle risorse ora consentono agli amministratori di [generare rapporti sul download delle risorse](/help/assets/asset-reports.md) dalla distribuzione as a Cloud Service di Experience Manager Assets. Questi dati consentono inoltre agli amministratori di derivare informazioni da metriche di successo chiave per misurare il livello di adozione delle risorse all’interno dell’azienda e da parte dei clienti.

   ![Rendering di PDF per altri formati](/help/release-notes/assets/choose_report.png)

* Experience Manager Assets adesso [supporta il token SAS](/help/assets/add-assets.md#asset-bulk-ingestor) oltre alla chiave di accesso per l’autenticazione durante la connessione all’origine dati Archiviazione BLOB di Azure per l’acquisizione delle risorse tramite lo strumento Importazione in blocco.

* È stata migliorata la gestione delle immagini CMYK in Asset Compute, consentendo di generare un ritaglio avanzato e tag avanzati per le immagini CMYK.

### Nuove funzioni nella versione prerelease di [!DNL Assets] {#prerelease-features-assets}

* Experience Manager Assets ora supporta l’[acquisizione di risorse su larga scala da Google Cloud Platform](/help/assets/add-assets.md#asset-bulk-ingestor) attraverso lo strumento Importazione in blocco.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni disponibili in [!DNL Forms] {#new-features-available-in-channel}

* **[Passaggi del flusso di lavoro per generare documenti PDF non interattivi e output stampabile](/help/forms/aem-forms-workflow-step-reference.md)**: con le fasi del flusso di lavoro AEM, è possibile automatizzare la creazione di documenti PDF non interattivi e l’output stampabile per i processi aziendali, semplificando il processo di generazione dei documenti e risparmiando tempo.
* **[Utilizza le note a piè di pagina per fornire citazioni o informazioni aggiuntive nei moduli adattivi](/help/forms/footnotes-richtextsupport.md)**: utilizza le note a piè di pagina di un modulo adattivo per visualizzare le informazioni su come completare o utilizzare un modulo. È inoltre possibile utilizzarle per fornire informazioni non fondamentali, autorizzazioni di copyright e altre informazioni utili.

### Nuove funzioni nella versione prerelease di [!DNL Forms] {#prerelease-features-forms}

* **[Utilizza i componenti core di acquisizione dei dati per generare moduli adattivi](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it)**: [utilizza l’editor dei moduli adattivi](/help/forms/creating-adaptive-form-core-components.md) per creare moduli basati su componenti di acquisizione dei dati standardizzati (componenti core). Questi componenti forniscono funzionalità di personalizzazione e riducono i tempi di sviluppo e i costi di manutenzione per le esperienze di registrazione digitale.
* **[Supporto della pipeline di front-end per lo stile dei moduli adattivi basati su componenti core](/help/forms/using-themes-in-core-components.md)**: utilizza temi facilmente personalizzabili basati su BEM per moduli adattivi basati su componenti core, implementandoli con una pipeline di distribuzione di front-end per migliorarne l’aspetto
* **[Genera un documento di record per moduli adattivi basati su componenti core](/help/forms/generate-document-of-record-core-components.md)**: crea un record per un modulo adattivo basato su componenti core all’invio per l’archiviazione a lungo termine, nel formato di stampa o in quello del documento.

![https://www.aemcomponents.dev/](/help/forms/assets/sample-core-components-based-adaptive-form.png)

* **[Invia moduli adattivi a Microsoft SharePoint e Microsoft OneDrive](/help/forms/configuring-submit-actions.md)**: semplifica l’invio dei dati con la possibilità di inviare direttamente i dati del modulo adattivo sia a Microsoft SharePoint che a Microsoft OneDrive. Puoi inviare dati basati su schema e senza schema. Queste azioni di invio si aggiungono a quelle già disponibili.
* **[Creazione efficiente di moduli con la funzione Salva un modulo adattivo come modello](/help/forms/template-editor.md#save-an-adaptive-form-as-template-saving-adaptive-form-as-template)**: semplifica il processo di creazione dei moduli salvando un modulo adattivo come modello e riutilizzando i modelli per il modulo adattivo successivo.
* **[Collega AEM Forms ai database supportati da JDBC](/help/forms/configure-data-sources.md#configure-relational-database-configure-relational-database)**: collega facilmente il modello dati di AEM Forms ai database che supportano JDBC per poter leggere e scrivere i dati in modo semplice.
* **[Integra con gli endpoint REST utilizzando Open API 3.0](/help/forms/configure-data-sources.md#configure-restful-services-open-api-specification-version-20-configure-restful-services-swagger-version30)**: collega i modelli di dati dei moduli as a Cloud Service di AEM Forms agli endpoint REST che supportano la versione 3.0 della specifica Open API per inviare e ricevere dati con facilità.
* **[Condividi un modulo adattivo per la revisione](/help/forms/create-reviews-forms.md)**: utilizza il meccanismo di revisione dei moduli adattivi per consentire a uno o più revisori di rivedere il modulo.


## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* Gli autori possono arricchire dinamicamente gli elenchi di prodotti con Frammenti di esperienza (ad esempio, inserendo un banner tra le voci dei prodotti elencati).
* Il componente Elenco ora supporta le pagine o categorie di prodotti associate per mostrare in modo dinamico le pagine correlate.
* È stato aggiunto il supporto per i componenti Peregrine 12.5.
* È stato aggiunto il supporto per il caricamento dei prezzi lato client nei teaser e nei caroselli di prodotti.

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### Novità {#what-is-new-foundation}

* [Ambienti di sviluppo rapido](/help/implementing/developing/introduction/rapid-development-environments.md) - Gli RDE consentono agli sviluppatori di risolvere i problemi rapidamente e di implementare nuove funzioni su AEM as a Cloud Service.

   Gli ambienti di sviluppo rapido sono un nuovo tipo di ambiente cloud concepito come un modo rapido, coerente ed estensibile di assicurarsi che un codice che funziona localmente funzioni anche come previsto nel cloud. Grazie agli strumenti della riga di comando, puoi “sincronizzare” rapidamente pacchetti di contenuti, bundle, file di contenuti, configurazione OSGI o configurazione del dispatcher con RDE. Per una dimostrazione pratica, guarda il video seguente:

   >[!VIDEO](https://video.tv.adobe.com/v/3413508/?quality=12&learn=on)

   Dopo aver convalidato correttamente il codice nell’RDE, si consiglia di distribuirlo in un ambiente di sviluppo cloud per sfruttare i gate di qualità di Cloud Manager, prima di distribuirlo agli ambienti di staging e produzione tramite la pipeline di produzione.

   Ogni programma include un RDE e, facoltativamente, è possibile concedere in licenza più programmi.

   >[!NOTE]
   >
   >Gli RDE verranno implementati gradualmente nelle prossime settimane; puoi inviare un’e-mail a aemcs-rde-support@adobe.com per posizionarti in cima alla lista.

* [Supporto esteso per i token di accesso per le API lato server](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md): è ora possibile generare più credenziali, che ti saranno d’aiuto negli scenari in cui le API hanno caratteristiche diverse. Ora è inoltre possibile revocare le credenziali in modo autonomo.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui.](/help/implementing/cloud-manager/release-notes/current.md)

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
