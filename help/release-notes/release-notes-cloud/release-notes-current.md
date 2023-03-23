---
title: Note sulla versione corrente per  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione corrente per  [!DNL Adobe Experience Manager]  as a Cloud Service.
mini-toc-levels: 1
source-git-commit: b47901d749712384506cf4eb03c099027933e95f
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 23%

---


# Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione della funzione per la versione corrente (più recente) di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti; per esempio, quelle del 2021, 2022 e così via.
>
>Dai un&#39;occhiata al [Roadmap sulle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it) per informazioni sulle prossime attivazioni delle funzioni di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

Data di rilascio di [!DNL Adobe Experience Manager] come [!DNL Cloud Service] la versione corrente delle funzioni (2023.1.0) è il 9 febbraio 2023. Il prossimo rilascio di nuove funzioni (2023.2.0) è pianificato per il 6 aprile 2023.

## Video sulla versione {#release-video}

Dai un’occhiata al video Panoramica sulla versione di gennaio 2023 per un riepilogo delle funzioni aggiunte alla versione 2023.1.0:

>[!VIDEO](https://video.tv.adobe.com/v/3413479/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni nella versione prerelease di [!DNL Sites] {#prerelease-features-sites}

* L’API di distribuzione dei contenuti GraphQL AEM ora supporta GraphQL [Paging](/help/headless/graphql-api/content-fragments.md#paging) e [Ordinamento](/help/headless/graphql-api/content-fragments.md#sorting), per rendere più efficiente il recupero e il rendering di set di contenuti di grandi dimensioni. L’impaginazione di GraphQL consente di migliorare il tempo di risposta delle query restituendo i risultati in sottoinsiemi anziché tutti contemporaneamente. L’ordinamento GraphQL consente di ordinare i set di contenuti in modo desiderato, facilitando l’elaborazione dei contenuti da parte di un’applicazione client.  Il tempo di risposta della query viene ulteriormente migliorato con Filtro ibrido nel motore GraphQL AEM. Il contenuto viene ora letto da JCR in set più piccoli che corrispondono ai filtri di query.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

* I rapporti di Assets ora includono la possibilità per gli amministratori di [generare rapporti di download delle risorse](/help/assets/asset-reports.md) dalla distribuzione as a Cloud Service di Experience Manager Assets. Questi dati consentono inoltre agli amministratori di ricavare informazioni dalle metriche di successo chiave al fine di misurare l’adozione di Assets all’interno della tua azienda e da parte dei clienti.

   ![Rappresentazione di PDF per altri formati](/help/release-notes/assets/choose_report.png)

* Experience Manager Assets adesso [supporta il token SAS](/help/assets/add-assets.md#asset-bulk-ingestor) oltre alla chiave di accesso per l’autenticazione durante la connessione all’origine dati Archiviazione BLOB di Azure per l’acquisizione delle risorse tramite lo strumento Importazione in blocco.

* È stata migliorata la gestione delle immagini CMYK in Asset compute, consentendo di generare ritaglio avanzato e tag avanzati per le immagini CMYK.

### Nuove funzioni nella versione prerelease di [!DNL Assets] {#prerelease-features-assets}

* Experience Manager Assets supporta ora [acquisizione su larga scala di risorse da Google Cloud Platform](/help/assets/add-assets.md#asset-bulk-ingestor) utilizzando lo strumento di importazione in blocco.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni disponibili in [!DNL Forms] {#new-features-available-in-channel}

* **[Passaggi del flusso di lavoro per generare documenti PDF non interattivi e output stampabile](/help/forms/aem-forms-workflow-step-reference.md)**: Automatizza la creazione di documenti PDF non interattivi e l&#39;output stampabile per i processi aziendali con AEM passaggi del flusso di lavoro, semplificando il processo di generazione dei documenti e risparmiando tempo.
* **[Utilizza le note a piè di pagina per fornire citazioni o informazioni aggiuntive in Adaptive Forms](/help/forms/footnotes-richtextsupport.md)**: Utilizzare le note a piè di pagina in un modulo adattivo per visualizzare le informazioni relative alla compilazione o all’utilizzo di un modulo. Puoi anche utilizzarlo per fornire informazioni parentetiche, autorizzazioni di copyright e altre informazioni utili.

### Nuove funzioni nella versione prerelease di [!DNL Forms] {#prerelease-features-forms}

* **[Utilizzare i componenti core di acquisizione dati per creare Forms adattivo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en)**: [Utilizza l’editor Forms adattivo](/help/forms/creating-adaptive-form-core-components.md) per creare moduli basati su componenti di acquisizione dati standardizzati (componenti core). Questi componenti offrono funzionalità di personalizzazione, tempi di sviluppo ridotti e costi di manutenzione inferiori per le esperienze di iscrizione digitale.
* **[Supporto della pipeline front-end per lo stile basato su componenti adattativi Forms](/help/forms/using-themes-in-core-components.md)**: Utilizza temi basati su BEM facilmente personalizzabili per Forms adattivo basato su componenti core distribuendoli con la pipeline di distribuzione Frontend per migliorare l’aspetto dei moduli.
* **[Genera documento di record per Forms adattivo basato su componenti core](/help/forms/generate-document-of-record-core-components.md)**: Crea un record per i moduli adattivi basati su componenti core all’invio per l’archiviazione a lungo termine, in formato cartaceo o nel formato del documento.

![https://www.aemcomponents.dev/](/help/forms/assets/sample-core-components-based-adaptive-form.png)

* **[Inviare Forms adattivo a Microsoft SharePoint e Microsoft OneDrive](/help/forms/configuring-submit-actions.md)**: Semplifica l’invio dei dati con la possibilità di inviare direttamente i dati del modulo adattivo a Microsoft SharePoint e Microsoft OneDrive. È possibile inviare sia dati basati su schema che dati privi di schema. Queste azioni di invio si aggiungono alle azioni di invio già disponibili.
* **[Creazione efficiente di moduli con la funzione Salva un modulo adattivo come modello](/help/forms/template-editor.md#save-an-adaptive-form-as-template-saving-adaptive-form-as-template)**: Semplifica il processo di creazione dei moduli salvando un modulo adattivo come modello e riutilizzando i modelli per il nuovo modulo adattivo.
* **[Collegare AEM Forms ai database supportati da JDBC](/help/forms/configure-data-sources.md#configure-relational-database-configure-relational-database)**: Collega facilmente il tuo modello dati AEM Forms ai database che supportano JDBC, consentendoti di leggere e scrivere i dati senza problemi.
* **[Integrare con gli endpoint REST utilizzando Open API 3.0](/help/forms/configure-data-sources.md#configure-restful-services-open-api-specification-version-20-configure-restful-services-swagger-version30)**: Collega i modelli di dati dei moduli as a Cloud Service di AEM Forms agli endpoint REST che supportano la versione 3.0 della specifica Open API, che consente di inviare e ricevere i dati con facilità.
* **[Condivisione di un modulo adattivo per la revisione](/help/forms/create-reviews-forms.md)**: Utilizza il meccanismo di revisione di Forms adattivo per consentire a uno o più revisori di rivedere il modulo.


## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* Gli autori possono arricchire dinamicamente gli elenchi di prodotti con Frammenti di esperienza (ad esempio, inserendo un banner tra le voci dei prodotti elencati).
* Il componente Elenco ora supporta le pagine o categorie di prodotti associate per mostrare in modo dinamico le pagine correlate.
* È stato aggiunto il supporto per i componenti Peregrine 12.5.
* È stato aggiunto il supporto per il caricamento dei prezzi lato client nei teaser e nei caroselli di prodotti.

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### Novità {#what-is-new-foundation}

* [Ambienti di sviluppo rapidi](/help/implementing/developing/introduction/rapid-development-environments.md) - Gli RDE consentono agli sviluppatori di risolvere rapidamente i problemi e di distribuire nuove funzionalità su AEM as a Cloud Service.

   Gli ambienti di sviluppo rapido sono un nuovo tipo di ambiente cloud inteso come modo rapido, coerente ed estensibile di convalidare tale codice che funziona localmente funziona anche come previsto nel cloud. Utilizzando gli strumenti della riga di comando, puoi &quot;sincronizzare&quot; rapidamente pacchetti di contenuto, bundle, file di contenuto, configurazione OSGI o configurazione del dispatcher all’RDE. Vedi questo in azione nel video seguente:

   >[!VIDEO](https://video.tv.adobe.com/v/3413508/?quality=12&learn=on)

   Dopo aver convalidato correttamente il codice nell’RDE, è consigliabile distribuirlo in un ambiente Cloud Dev per sfruttare i gate di qualità di Cloud Manager, prima di distribuirlo tramite la pipeline di produzione per gli ambienti di stage e produzione.

   Ogni programma include un RDE ed eventualmente un altro può essere concesso in licenza.

   >[!NOTE]
   >
   >Le RDE saranno gradualmente estese nelle prossime settimane; puoi inviare un’e-mail a aemcs-rde-support@adobe.com per passare all’inizio della riga.

* [Supporto esteso per token di accesso API lato server](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) - È ora possibile generare più credenziali, utile per gli scenari in cui le API hanno caratteristiche diverse. Ora è anche possibile revocare le credenziali in modo self-service.

## Note sulla versione di manutenzione {#maintenance}

Sono disponibili le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui.](/help/implementing/cloud-manager/release-notes/current.md)

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
