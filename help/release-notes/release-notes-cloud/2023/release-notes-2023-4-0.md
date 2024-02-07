---
title: Note sulla versione 2023.4.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione 2023.4.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: c34aedee-e45a-4e2a-ae7f-930bc0cc026f
source-git-commit: ecf4c06fd290d250c14386b3135250633b26c910
workflow-type: ht
source-wordcount: '1122'
ht-degree: 100%

---

# Note sulla versione 2023.4.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione funzionale 2023.4.0 di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2021 o 2022.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

La data di rilascio della versione funzionale corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2023.4.0) è il 7 giugno 2023. La prossima versione funzionale (2023.6.0) è pianificata per il 29 giugno 2023.

## Video sulla versione {#release-video}

Dai un’occhiata al video Panoramica sulla versione di aprile 2023 per un riepilogo delle funzioni aggiunte alla versione 2023.4.0:

>[!VIDEO](https://video.tv.adobe.com/v/3418681/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni in [!DNL Experience Manager Sites] {#sites-features}

* Esportare frammenti di contenuto da AEM as a Cloud Service a Adobe Target in formato JSON e creare offerte JSON corrispondenti in Target.
* Il supporto per la paginazione e l’ordinamento di GraphQL, insieme ai miglioramenti apportati alla memorizzazione nella cache interna, ora consente di migliorare le prestazioni delle applicazioni client separate quando si recuperano set di contenuti di grandi dimensioni da AEM utilizzando query e filtri GraphQL complessi.

### Nuove funzioni nella versione prerelease di [!DNL Experience Manager Sites] {#prerelease-sites}

* Ora è possibile pubblicare i frammenti di contenuto e i relativi riferimenti nel [Servizio di anteprima AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=it#access-preview-service) utilizzando la [Console Frammenti di contenuto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=it), che consente agli utenti di visualizzare in anteprima l’esperienza finale su un’applicazione di anteprima separata prima della pubblicazione.
* Le immagini possono essere ora ottimizzate dinamicamente per la distribuzione web in scenari headless utilizzando GraphQL di AEM. Nelle query GraphQL è possibile definire [Variabili di query](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/images.html?lang=it#query-variables) per consentire alle applicazioni client separate di richiedere a AEM immagini ottimizzate di conseguenza.
* I tag sulle [Varianti dei frammenti di contenuto](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-variations.html?lang=it) ora possono essere trasmessi in formato JSON utilizzando l’API per la distribuzione dei contenuti GraphQL di AEM.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

* È stato aggiunto il supporto per le immagini WebP per estrarre automaticamente i metadati, generare miniature e rappresentazioni personalizzate. Per questi file è ora supportata anche la funzionalità Tag avanzati. Le funzionalità di Dynamic Media non sono supportate per WebP come formato di immissione.

* [Miglioramenti all’esperienza di ricerca](/help/assets/search-assets.md#aftersearch): è ora possibile eseguire rapidamente le seguenti operazioni sulle risorse visualizzate nei risultati di ricerca:

   * Crea un flusso di lavoro
   * Crea una versione
   * Correla o non correla risorse

     Per eseguire queste operazioni, non è necessario passare alla posizione della risorsa e visualizzarne le proprietà.

* Miglioramenti apportati all’usabilità del facet di ricerca colore: il campo di inserimento per i valori dei colori è ora modificabile e i risultati della ricerca vengono aggiornati solo quando esci dal selettore colore.

* Lancio del supporto per il nuovo protocollo (DASH - Dynamic Adaptive Streaming over HTTP) per lo streaming adattivo nella distribuzione video Dynamic Media (con CMAF abilitato):
   * Lo streaming adattivo (DASH/HLS) garantisce agli utenti una migliore esperienza di visualizzazione dei video
   * DASH è il protocollo standard internazionale per lo streaming video adattivo ed è ampiamente adottato nel settore
   * Disponibile in tutte le aree geografiche, da abilitare tramite ticket di supporto

* Dynamic Media _Snapshot_: sperimenta immagini di test o URL Dynamic Media per visualizzare l’output di diversi modificatori di immagini e valutare le ottimizzazioni di Imaging avanzato per le dimensioni dei file (con distribuzione WebP e AVIF), la larghezza di banda della rete e le proporzioni dei pixel del dispositivo. Consulta [Dynamic Media Snapshot](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html?lang=it).

### Funzione nella versione prerelease di [!DNL Assets] {#prerelease-feature-assets}

* Dynamic Media: l’interfaccia utente di alcuni campi relativi a Ritaglio avanzato in un profilo immagine ora è aggiornata per riflettere le linee guida correnti per la definizione di un Ritaglio avanzato. Consulta [Opzioni di ritaglio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles.html?lang=it#crop-options).

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni disponibili in [!DNL Forms] {#new-features-available-in-channel}

* **[Invio di moduli adattivi a Microsoft® SharePoint e Microsoft® OneDrive](/help/forms/configuring-submit-actions.md)**: migliora l’agilità degli utenti aziendali per avviare rapidamente nuovi moduli e archiviare i dati inviati in strumenti di uso quotidiano, ad esempio il sito Microsoft® SharePoint o la cartella OneDrive.

### Funzioni nella versione prerelease di [!DNL Forms] {#prerelease-features-forms}

* [Moduli adattivi nell’Editor pagina di AEM](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md): ora è possibile utilizzare l’Editor pagina di AEM per creare e aggiungere rapidamente più moduli alle pagine del sito. Questa funzionalità consente agli autori di contenuti di creare esperienze di acquisizione dati fluide all’interno delle pagine di Sites utilizzando la potenza dei componenti per moduli adattivi, tra cui il comportamento dinamico, le convalide, l’integrazione dei dati, la generazione di documenti di record e l’automazione dei processi aziendali. Operazioni disponibili:

   * Creare un modulo adattivo trascinando i componenti del modulo nel componente Contenitore di moduli adattivi nell’editor di AEM Sites o nei Frammenti di esperienza.
   * Utilizzare la procedura guidata per moduli adattivi nell’editor di AEM Sites per creare moduli indipendenti da qualsiasi pagina di Sites e poter riutilizzare tali moduli su più pagine.
   * Aggiungere più moduli a una pagina di Sites per semplificare l’esperienza utente e fornire maggiore flessibilità.

     >[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

* [Adobe Acrobat Sign Solutions per la Pubblica amministrazione](/help/forms/adobe-sign-integration-adaptive-forms.md): AEM Forms ora si integra con Adobe Acrobat Sign Solutions per la Pubblica amministrazione. Questa integrazione fornisce un livello avanzato di conformità e sicurezza per le firme elettroniche con l’invio di moduli adattivi per gli account della pubblica amministrazione associati (dipartimenti e agenzie statali).

  L’integrazione con Adobe Acrobat Sign per la Pubblica amministrazione consente ai partner e ai clienti del settore pubblico di Adobe di utilizzare le firme elettroniche in moduli adattivi per alcune delle linee di business più critiche e sensibili. Questo ulteriore livello di sicurezza garantisce che tutte le firme elettroniche siano pienamente conformi alla conformità FedRAMP Moderate, garantendo ai clienti del settore pubblico di Adobe la massima tranquillità.

* Gestione avanzata degli errori con handler di errori personalizzati nell’editor di regole: ora è possibile richiamare una funzione personalizzata (utilizzando la libreria client) a fronte di un errore restituito da un servizio esterno e fornire una risposta personalizzata agli utenti finali. In alternativa, è possibile eseguire azioni specifiche per gli errori restituiti da un servizio. Ad esempio, puoi richiamare un flusso di lavoro personalizzato nel back-end per codici di errore specifici o informare il cliente che il servizio non è disponibile.

  Questa funzionalità consente di migliorare la capacità complessiva di gestione degli errori introducendo risposte di errore basate su standard compatibili con le versioni precedenti dei gestori degli errori OOTB, con maggiore flessibilità e controllo.

### Programma dei moduli adattivi headless per i primi utilizzatori {#forms-early-adopter}

Utilizza i moduli adattivi headless per consentire agli sviluppatori di creare, pubblicare e gestire moduli interattivi a cui è possibile accedere e con cui si può interagire tramite API, anziché tramite un’interfaccia utente grafica tradizionale. I moduli adattivi headless consentono di:

* creare moduli multi-canale di alta qualità nel linguaggio di programmazione desiderato
* integrare in modo nativo i moduli nelle app desktop e per dispositivi mobili, nei siti web e nelle applicazioni chat
* riutilizzare i componenti proprietari dell’interfaccia utente con le applicazioni di Forms
* sfruttare la potenza di Adobe Experience Manager Forms

È possibile inviare un’e-mail a `aem-forms-headless@adobe.com` dal proprio ID e-mail ufficiale per aderire al programma per i primi utilizzatori.

## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### Novità {#what-is-new-foundation}

* Aree geografiche di pubblicazione aggiuntive: i clienti di Sites possono concedere in licenza fino a tre aree di pubblicazione, oltre all’area geografica primaria. Il traffico viene indirizzato ad altre farm di pubblicazione con una minore latenza per determinate richieste e una maggiore resilienza contro interruzioni a livello regionale. Contatta l’Adobe Account Manager per informazioni sulle licenze per [Aree geografiche di pubblicazione aggiuntiva](/help/operations/additional-publish-regions.md) per i programmi.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui.](/help/implementing/cloud-manager/release-notes/current.md)

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
