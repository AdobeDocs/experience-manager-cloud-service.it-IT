---
title: Note sulla versione 2023.6.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2023.6.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
source-git-commit: 2d10d03e478bff5a162c620c41ceac38a6d7911a
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 42%

---


# Note sulla versione 2023.6.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione funzionale 2023.6.0 di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2021 o 2022.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

La data di rilascio della versione funzionale corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2023.6.0) è il 29 giugno 2023. La prossima versione (2023.7.0) è prevista per il 27 luglio 2023.

## Video sulla versione {#release-video}

Dai un’occhiata al video Panoramica sulla versione di giugno 2023 per un riepilogo delle funzioni aggiunte alla versione 2023.6.0:

>[!VIDEO](https://video.tv.adobe.com/v/3420971/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni in [!DNL Experience Manager Sites] {#sites-features}

* Ora è possibile pubblicare i frammenti di contenuto e i relativi riferimenti nel [Servizio di anteprima AEM](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) utilizzando la [Console Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/content-fragments-console.md), che consente agli utenti di visualizzare in anteprima l’esperienza finale su un’applicazione di anteprima separata prima della pubblicazione.

![Anteprima nella console Frammenti di contenuto](/help/assets/content-fragments-console-preview.png)

* Le immagini possono ora essere ottimizzate dinamicamente per la distribuzione web in scenari headless utilizzando AEM GraphQL. [Variabili di query](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/images.html?lang=en#query-variables) può essere definito nelle query GraphQL per consentire alle applicazioni client disaccoppiate di richiedere all’AEM immagini ottimizzate di conseguenza.
* Tag su [Varianti dei frammenti di contenuto](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-variations.html?lang=en) ora può essere inviato in formato JSON utilizzando l’API di distribuzione dei contenuti GraphQL dell’AEM.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

**Disponibilità della vista Nuove risorse**

Il [nuova vista Risorse](/help/assets/assets-view-introduction.md) è ora disponibile in Experience Manager Assets. La visualizzazione Assets offre un’interfaccia utente semplificata che semplifica la gestione, l’individuazione e la distribuzione delle risorse digitali. L’esperienza è destinata ai creativi, ai consumatori di risorse di sola lettura e agli utenti DAM più leggeri.

![Gestione dei tag](/help/assets/assets/my-workspace.png)

**Miglioramenti all’esperienza di ricerca**

Experience Manager Assets ora ti consente di fare di più dall’interfaccia utente dei risultati della ricerca: ora puoi:

* [Eseguire ricerche nel percorso del repository corrente](/help/assets/search-assets.md) per impostazione predefinita, anziché cercare la parola chiave nell&#39;intero archivio.

* [Passa alla posizione della cartella](/help/assets/search-assets.md#aftersearch) per le risorse visualizzate nei risultati di ricerca.

**Anteprime miniature per risorse 3D**

[!DNL Experience Manager Assets] ora genera [anteprime di miniature per i formati di file 3D più comuni](/help/assets/file-format-support.md) tra cui gLB, USDz, FBX, 3DS, OBJ e SBSAR. Quando questi file vengono caricati, per impostazione predefinita vengono generate automaticamente le miniature.

**Configurazione condivisione collegamenti**

Una nuova esperienza utente migliorata per [creazione di condivisioni di collegamenti](/help/assets/share-assets.md) insieme a un nuovissimo set di configurazioni che consentono agli amministratori di personalizzare il comportamento predefinito di questa funzionalità per i tuoi utenti.

![Gestione dei tag](/help/assets/assets/config-email-service.png)

**Dynamic Medie: aggiornamento dei campi relativi al ritaglio avanzato nel profilo immagine**

L’interfaccia utente di alcuni campi relativi a Ritaglio avanzato in un profilo immagine ora è aggiornata per riflettere le linee guida correnti per la definizione di un Ritaglio avanzato. Consulta [Opzioni di ritaglio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles.html?lang=it#crop-options).

### Nuove funzioni nella vista Risorse {#assets-view-features}

**Assegnazione di tag gerarchici alle risorse per velocizzare l’esperienza di ricerca**

Le liste piatte di vocabolari controllati diventano ingestibili nel tempo. La vista Risorse ora supporta [struttura gerarchica dei tag](/help/assets/tagging-management-assets-view.md), che facilita l’applicazione di metadati rilevanti, la classificazione delle risorse, il supporto della ricerca, il riutilizzo dei tag, il miglioramento della reperibilità di informazioni e così via.

![Gestione dei tag](/help/assets/assets/tags-hierarchy.png)

**Aggiungi file, cartelle e raccolte per un accesso rapido**

Ora puoi [fissaggio di file, cartelle e raccolte per un accesso più rapido](/help/assets/my-workspace-assets-view.md) a questi elementi quando ne hai bisogno in un secondo momento. Gli elementi bloccati vengono visualizzati nel **Accesso rapido** sezione di My Workspace. È possibile accedervi utilizzando l&#39;area di lavoro personale anziché passare alla posizione in cui sono stati salvati nel repository.

![Attività nell’area di lavoro](/help/assets/assets/quick-access.png)

**Filtrare le risorse nella cartella Cestino**

La vista Risorse ora consente di: [filtrare le risorse disponibili nella cartella Cestino](/help/assets/navigate-assets-view.md). Puoi applicare filtri standard o personalizzati per cercare le risorse appropriate all’interno della cartella Cestino per ripristinarle o eliminarle definitivamente.

**Anteprime miniature per risorse 3D**

La vista Risorse genera ora anteprime di miniature per i formati di file 3D più comuni, tra cui gLB, USDz, FBX, 3DS, OBJ e SBSAR. Quando questi file vengono caricati nella vista Risorse, per impostazione predefinita il sistema genera automaticamente le miniature.

![Attività nell’area di lavoro](/help/assets/assets/3d-preview.png)

**Visualizza i termini più cercati**

La vista Risorse ora supporta [visualizzazione dei termini più ricercati nell’implementazione](/help/assets/my-workspace-assets-view.md) utilizzando **Approfondimenti** sezione di My Workspace. Puoi anche passare a Insights dettagliato per visualizzare le ricerche principali negli ultimi 30 giorni o 12 mesi.

![Attività nell’area di lavoro](/help/assets/assets/insights-top-searches.png)

**Miglioramenti al modulo metadati**

La vista Risorse ora consente di: [aggiungere componenti di proprietà di testo con più valori e elenco a discesa](/help/assets/metadata-assets-view.md#property-components) ai moduli di metadati.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni disponibili in [!DNL Forms] {#new-features-available-in-channel}

* [Moduli adattivi nell’Editor pagina di AEM](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md): ora è possibile utilizzare l’Editor pagina di AEM per creare e aggiungere rapidamente più moduli alle pagine del sito. Questa funzionalità consente agli autori di contenuti di creare esperienze di acquisizione dati fluide all’interno delle pagine di Sites utilizzando la potenza dei componenti per moduli adattivi, tra cui il comportamento dinamico, le convalide, l’integrazione dei dati, la generazione di documenti di record e l’automazione dei processi aziendali. Operazioni disponibili:

   * Creare un modulo adattivo trascinando i componenti del modulo nel componente Contenitore di moduli adattivi nell’editor di AEM Sites o nei Frammenti di esperienza.
   * Utilizzare la procedura guidata per moduli adattivi nell’editor di AEM Sites per creare moduli indipendenti da qualsiasi pagina di Sites e poter riutilizzare tali moduli su più pagine.
   * Aggiungere più moduli a una pagina di Sites per semplificare l’esperienza utente e fornire maggiore flessibilità.

     >[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

* [Adobe Acrobat Sign Solutions for Government](/help/forms/adobe-sign-integration-adaptive-forms.md): AEM Forms ora si integra con Adobe Acrobat Sign Solutions for Government. Questa integrazione fornisce un livello avanzato di conformità e sicurezza per le firme elettroniche con l’invio di moduli adattivi per gli account della pubblica amministrazione associati (dipartimenti e agenzie statali).

  L’integrazione con Adobe Acrobat Sign Solutions for Government consente ai partner e ai clienti governativi di Adobe di utilizzare le firme elettroniche in Adaptive Forms per alcune delle linee di business più critiche e sensibili. Questo ulteriore livello di sicurezza garantisce che tutte le firme elettroniche siano pienamente conformi alla conformità FedRAMP Moderate, garantendo ai clienti del settore pubblico di Adobe la massima tranquillità.

* [Gestione avanzata degli errori con gestori di errori personalizzati nell’editor di regole](/help/forms/add-custom-error-handler-adaptive-forms.md): ora puoi richiamare una funzione personalizzata (utilizzando la libreria client) in risposta a un errore restituito da un servizio esterno e fornire una risposta personalizzata agli utenti finali. In alternativa, è possibile eseguire azioni specifiche per gli errori restituiti da un servizio. Ad esempio, puoi richiamare un flusso di lavoro personalizzato nel back-end per codici di errore specifici o informare il cliente che il servizio non è disponibile.

  Questa funzionalità consente di migliorare la capacità complessiva di gestione degli errori introducendo risposte di errore basate su standard compatibili con le versioni precedenti dei gestori degli errori OOTB, con maggiore flessibilità e controllo.

* [Metodi di autenticazione migliorati per il modello dati modulo](/help/forms/configure-data-sources.md): maggiore sicurezza grazie all’introduzione dell’autenticazione basata sulle credenziali client per la connessione di AEM Forms con origini dati compatibili. Questo miglioramento elimina la necessità di rappresentazione o accesso da parte dell’utente, rafforzando la protezione dei dati.

* [Forms adattivo con sezioni ripetibili](/help/forms/create-forms-repeatable-sections.md): ora puoi effettuare [Accordion](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html), [Procedura guidata](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html), [Pannello](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html), e [Schede orizzontali](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html) componenti in un modulo adattivo basato su Componenti core per creare sezioni ripetibili.

  >[!VIDEO](https://video.tv.adobe.com/v/3421052/adaptive-forms-repeatable-sections-repeat-sections/?quality=12&learn=on)

  Queste sezioni ripetibili consentono di fornire un numero illimitato di voci senza un numero di campi fisso. È utile quando le istanze di dati richieste sono sconosciute in anticipo. Gli utenti di Forms possono aggiungere o rimuovere facilmente sezioni, rendendo i moduli adattabili a scenari di immissione dati diversi e semplificando la raccolta di più occorrenze degli stessi dati.

* **[Invio di moduli adattivi a Microsoft® SharePoint e Microsoft® OneDrive](/help/forms/configuring-submit-actions.md)**: migliora l’agilità degli utenti aziendali per avviare rapidamente nuovi moduli e archiviare i dati inviati in strumenti di uso quotidiano, ad esempio il sito Microsoft® SharePoint o la cartella OneDrive.

### Programma dei moduli adattivi headless per i primi utilizzatori {#forms-early-adopter}

Utilizzare [Forms adattivo headless](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) per consentire agli sviluppatori di creare, pubblicare e gestire moduli interattivi a cui è possibile accedere e con cui interagire tramite API, anziché tramite un’interfaccia utente grafica tradizionale. I moduli adattivi headless consentono di:

* creare moduli multi-canale di alta qualità nel linguaggio di programmazione desiderato
* integrare in modo nativo i moduli nelle app desktop e per dispositivi mobili, nei siti web e nelle applicazioni chat
* riutilizzare i componenti proprietari dell’interfaccia utente con le applicazioni di Forms
* sfruttare la potenza di Adobe Experience Manager Forms

È possibile inviare un’e-mail a `aem-forms-headless@adobe.com` dal proprio ID e-mail ufficiale per aderire al programma per i primi utilizzatori.

## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes/current.md).

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
