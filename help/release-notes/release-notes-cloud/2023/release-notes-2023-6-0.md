---
title: Note sulla versione 2023.6.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione 2023.6.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 29cf9548-e413-4e4f-b233-d6bb04918b22
source-git-commit: ecf4c06fd290d250c14386b3135250633b26c910
workflow-type: tm+mt
source-wordcount: '1357'
ht-degree: 95%

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

La data di rilascio della versione funzionale corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2023.6.0) è il 29 giugno 2023. La successiva versione funzionale (2023.7.0) è pianificata per il 27 luglio 2023.

## Video sulla versione {#release-video}

Dai un’occhiata al video Panoramica sulla versione di giugno 2023 per un riepilogo delle funzioni aggiunte alla versione 2023.6.0:

>[!VIDEO](https://video.tv.adobe.com/v/3420971/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni in [!DNL Experience Manager Sites] {#sites-features}

* Ora è possibile pubblicare i frammenti di contenuto e i relativi riferimenti nel [Servizio di anteprima AEM](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) utilizzando la [Console Frammenti di contenuto](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console), che consente agli utenti di visualizzare in anteprima l’esperienza finale su un’applicazione di anteprima separata prima della pubblicazione.

![Anteprima nella console Frammenti di contenuto](/help/assets/content-fragments-console-preview.png)

* Le immagini possono essere ora ottimizzate dinamicamente per la distribuzione web in scenari headless utilizzando GraphQL di AEM. Nelle query GraphQL è possibile definire [Variabili di query](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/images.html#query-variables) per consentire alle applicazioni client separate di richiedere a AEM immagini ottimizzate di conseguenza.
* I tag sulle [Varianti dei frammenti di contenuto](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-variations.html) ora possono essere trasmessi in formato JSON utilizzando l’API per la distribuzione dei contenuti GraphQL di AEM.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

**Disponibilità della nuova vista Risorse**

La [nuova vista Risorse](/help/assets/assets-view-introduction.md) è ora disponibile in Experience Manager Assets. L’interfaccia utente semplificata della vista Risorse agevola la gestione, l’individuazione e la distribuzione delle risorse digitali. L’esperienza è destinata ai creativi, a chi utilizza le risorse di sola lettura e agli utenti di DAM più leggeri.

![Gestione dei tag](/help/assets/assets/my-workspace.png)

**Miglioramenti all’esperienza di ricerca**

Experience Manager Assets ora consente di fare di più dall’interfaccia utente dei risultati di ricerca: ora puoi:

* [Eseguire ricerche nel percorso dell’archivio corrente](/help/assets/search-assets.md) per impostazione predefinita, anziché cercare la parola chiave nell’intero archivio.

* [Passare alla posizione della cartella](/help/assets/search-assets.md#aftersearch) per le risorse visualizzate nei risultati di ricerca.

**Anteprime delle miniature per risorse 3D**

[!DNL Experience Manager Assets] ora genera [anteprime di miniature per i formati di file 3D più comuni](/help/assets/file-format-support.md), tra cui gLB, USDz, FBX, 3DS, OBJ e SBSAR. Quando questi file vengono caricati, per impostazione predefinita vengono generate automaticamente le miniature.

**Configurazione della condivisione di collegamenti**

Una nuova esperienza utente migliorata per [creare condivisioni di collegamenti](/help/assets/share-assets.md) e un nuovo set di configurazioni consentono agli amministratori di personalizzare il comportamento predefinito di questa funzionalità per gli utenti.

![Gestione dei tag](/help/assets/assets/config-email-service.png)

**Dynamic Media: aggiornamento dei campi relativi al ritaglio avanzato in un profilo immagine**

L’interfaccia utente di alcuni campi relativi a Ritaglio avanzato in un profilo immagine è stata aggiornata per riflettere le linee guida correnti utili alla definizione di un Ritaglio avanzato. Consulta [Opzioni di ritaglio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles.html#crop-options).

### Nuove funzioni nella Vista risorse {#assets-view-features}

**Assegnazione tag gerarchica alle risorse per un’esperienza di ricerca più veloce**

Gli elenchi semplici dei vocabolari controllati diventano ingestibili nel tempo. La Vista risorse ora supporta la [struttura gerarchica dell’assegnazione tag](/help/assets/tagging-management-assets-view.md), che semplifica l’applicazione di metadati rilevanti, la classificazione delle risorse, il supporto della ricerca, il riutilizzo dei tag, il miglioramento della reperibilità e così via.

![Gestione dell’assegnazione tag](/help/assets/assets/tags-hierarchy.png)

**Fissare file, cartelle e raccolte per un accesso rapido**

È ora possibile [fissare file, cartelle e raccolte per accedervi più rapidamente](/help/assets/my-workspace-assets-view.md) quando se ne avrà bisogno. Gli elementi fissati vengono visualizzati nella sezione **Accesso rapido** dell’area di lavoro personale. È possibile accedervi utilizzando l’area di lavoro personale anziché passare alla posizione in cui sono stati salvati nell’archivio.

![Attività nell’area di lavoro](/help/assets/assets/quick-access.png)

**Filtrare le risorse nella cartella Cestino**

La Vista risorse ora consente di [filtrare le risorse disponibili nella cartella Cestino](/help/assets/navigate-assets-view.md). Puoi applicare filtri standard o personalizzati per cercare le risorse appropriate all’interno della cartella Cestino per ripristinarle o eliminarle definitivamente.

**Anteprime delle miniature per risorse 3D**

La Vista risorse genera ora anteprime di miniature per i formati di file 3D più comuni, tra cui gLB, USDz, FBX, 3DS, OBJ e SBSAR. Quando questi file vengono caricati nella Vista risorse, per impostazione predefinita le miniature vengono generate automaticamente dal sistema.

![Attività nell’area di lavoro](/help/assets/assets/3d-preview.png)

**Visualizzare i termini più cercati**

La Vista risorse ora supporta la [visualizzazione dei termini più ricercati nella distribuzione](/help/assets/my-workspace-assets-view.md) utilizzando la sezione **Approfondimenti** dell’area di lavoro personale. Puoi anche passare alla sezione Approfondimenti per visualizzare le ricerche principali degli ultimi 30 giorni o 12 mesi.

![Attività nell’area di lavoro](/help/assets/assets/insights-top-searches.png)

**Miglioramenti al modulo metadati**

La Vista risorse ora consente di [aggiungere componenti di proprietà di testo multi-valore ed elenchi a discesa](/help/assets/metadata-assets-view.md#property-components) ai moduli metadati.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni disponibili in [!DNL Forms] {#new-features-available-in-channel}

* [Moduli adattivi nell’Editor pagina di AEM](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md): ora è possibile utilizzare l’Editor pagina di AEM per creare e aggiungere rapidamente più moduli alle pagine del sito. Questa funzionalità consente agli autori di contenuti di creare esperienze di acquisizione dati fluide all’interno delle pagine di Sites utilizzando la potenza dei componenti per moduli adattivi, tra cui il comportamento dinamico, le convalide, l’integrazione dei dati, la generazione di documenti di record e l’automazione dei processi aziendali. Operazioni disponibili:

   * Creare un modulo adattivo trascinando i componenti del modulo nel componente Contenitore di moduli adattivi nell’editor di AEM Sites o nei Frammenti di esperienza.
   * Utilizzare la procedura guidata per moduli adattivi nell’editor di AEM Sites per creare moduli indipendenti da qualsiasi pagina di Sites e poter riutilizzare tali moduli su più pagine.
   * Aggiungere più moduli a una pagina di Sites per semplificare l’esperienza utente e fornire maggiore flessibilità.

     >[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

* [Adobe Acrobat Sign Solutions per la Pubblica amministrazione](/help/forms/adobe-sign-integration-adaptive-forms.md): AEM Forms ora si integra con Adobe Acrobat Sign Solutions per la Pubblica amministrazione. Questa integrazione fornisce un livello avanzato di conformità e sicurezza per le firme elettroniche con l’invio di moduli adattivi per gli account della pubblica amministrazione associati (dipartimenti e agenzie statali).

  L’integrazione con Adobe Acrobat Sign Solutions per la Pubblica amministrazione consente ai partner e ai clienti del settore pubblico di Adobe di utilizzare le firme elettroniche in moduli adattivi per alcune delle linee di business più critiche e sensibili. Questo ulteriore livello di sicurezza garantisce che tutte le firme elettroniche siano pienamente conformi alla conformità FedRAMP Moderate, garantendo ai clienti del settore pubblico di Adobe la massima tranquillità.

* [Gestione avanzata degli errori con handler di errori personalizzati nell’editor delle regole](/help/forms/add-custom-error-handler-adaptive-forms.md): ora puoi richiamare una funzione personalizzata (utilizzando la libreria client) a fronte di un errore restituito da un servizio esterno e fornire una risposta personalizzata agli utenti finali. In alternativa, è possibile eseguire azioni specifiche per gli errori restituiti da un servizio. Ad esempio, puoi richiamare un flusso di lavoro personalizzato nel back-end per codici di errore specifici o informare il cliente che il servizio non è disponibile.

  Questa funzionalità consente di migliorare la capacità complessiva di gestione degli errori introducendo risposte di errore basate su standard compatibili con le versioni precedenti dei gestori degli errori OOTB, con maggiore flessibilità e controllo.

* [Metodi di autenticazione migliorati per il modello dati modulo](/help/forms/configure-data-sources.md): maggiore sicurezza grazie all’introduzione dell’autenticazione basata sulle credenziali client per la connessione di AEM Forms con origini dati compatibili. Questo miglioramento elimina la necessità di rappresentazione o accesso da parte dell’utente, rafforzando la protezione dei dati.

* [Forms adattivo con sezioni ripetibili](/help/forms/create-forms-repeatable-sections.md): ora puoi effettuare [Accordion](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html?lang=it), [Procedura guidata](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html?lang=it), [Pannello](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html?lang=it), e [Schede orizzontali](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html?lang=it) componenti in un modulo adattivo basato su Componenti core per creare sezioni ripetibili.

  >[!VIDEO](https://video.tv.adobe.com/v/3421052/adaptive-forms-repeatable-sections-repeat-sections/?quality=12&learn=on)

  Queste sezioni ripetibili consentono di fornire un numero illimitato di voci senza un numero di campi fisso. È utile quando le istanze di dati richieste non sono note in anticipo. Gli utenti di Forms possono aggiungere o rimuovere facilmente le sezioni, rendendo i moduli adattabili a scenari di immissione dati diversi e semplificando la raccolta di più occorrenze degli stessi dati.

* **[Invio di moduli adattivi a Microsoft® SharePoint e Microsoft® OneDrive](/help/forms/configuring-submit-actions.md)**: migliora l’agilità degli utenti aziendali per avviare rapidamente nuovi moduli e archiviare i dati inviati in strumenti di uso quotidiano, ad esempio il sito Microsoft® SharePoint o la cartella OneDrive.

### Programma dei moduli adattivi headless per i primi utilizzatori {#forms-early-adopter}

Utilizza i [moduli adattivi headless](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=it) per consentire a chi sviluppa di creare, pubblicare e gestire moduli interattivi a cui è possibile accedere e con cui si può interagire tramite API, anziché tramite un’interfaccia utente grafica tradizionale. I moduli adattivi headless consentono di:

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
