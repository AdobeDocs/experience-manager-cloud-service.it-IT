---
title: Note sulla versione 2023.8.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione 2023.8.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: a0ffa6cf-64ae-468c-93f4-ac6805ef907e
feature: Release Information
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1691'
ht-degree: 100%

---

# Note sulla versione 2023.8.0 di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note sulla versione funzionale 2023.8.0 di [!DNL Experience Manager] as a Cloud Service.

## Data di rilascio {#release-date}

La data di rilascio della versione corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2023.8.0) è il 31 agosto 2023. La prossima versione funzionale (2023.9.0) è pianificata per il 28 settembre 2023.

## Video sulla versione {#release-video}

Dai un’occhiata al video Panoramica sulla versione di agosto 2023 per un riepilogo delle funzioni aggiunte alla versione 2023.8.0:

>[!VIDEO](https://video.tv.adobe.com/v/3423535/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni in [!DNL Experience Manager Sites] {#sites-features}

* La [Console Frammenti di contenuto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=it) ora consente agli utenti di visualizzare i tag e di effettuare ricerche per tag applicati come metadati ai frammenti di contenuto. Per usufruire di questa funzionalità, gli utenti non dovranno più passare all’interfaccia utente Assets, riducendo così i passaggi da un contesto all’altro e migliorando l’efficienza.

  ![Assegnazione di tag nella console Frammenti di contenuto](/help/assets/content-fragments-console-tags.png)
* Il nuovo Editor frammento di contenuto è ora disponibile su AEM as a Cloud Service. Consente agli autori di contenuti di essere più produttivi, semplificando le attività di authoring e riducendo la necessità di passare da un’app all’altra durante la modifica dei contenuti.
  ![Nuovo Editor frammento di contenuto](/help/release-notes/assets/newCFEditor.png)

Il nuovo Editor frammento di contenuto offre i seguenti vantaggi che non sono disponibili nell’editor originale:

* Salvataggio automatico per una maggiore efficienza nell’authoring e per evitare la perdita accidentale di modifiche.
* Visualizzazione gerarchica di un frammento di contenuto e dei relativi riferimenti utilizzando la Struttura per una navigazione rapida all’interno di un frammento profondamente strutturato.
  ![Struttura nell’Editor frammento di contenuto](/help/release-notes/assets/newCFEditor_StructureTree.png)

* Caricamento in linea delle risorse come riferimenti di contenuto senza doverlo prima caricare in Asset DAM
* Anteprima ad hoc dell’esperienza con rendering fornita dal frammento di contenuto per aiutare gli autori a visualizzare l’aspetto dei contenuti nell’app front-end
* Pubblicazione con un solo clic e annullamento della pubblicazione del frammento di contenuto dall’editor
* Visualizzazione e accesso alle copie per lingua durante la modifica di un frammento di contenuto
  ![Copie per lingua nell’Editor frammento di contenuto](/help/release-notes/assets/newCFEditor_LanguageCopies.PNG)

* Visualizzazione delle versioni per tenere traccia della timeline di un frammento di contenuto

  ![Versioni nell’Editor frammento di contenuto](/help/release-notes/assets/newCFEditor_Versionhistory.PNG)

* Visualizzazione dei riferimenti principali per aiutare gli autori a comprendere l’impatto delle modifiche

  ![Riferimenti principali nell’Editor frammento di contenuto](/help/release-notes/assets/newCFEditor_Parentreferences.PNG)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni nella Vista risorse {#assets-view-features}

<!--

**Assign metadata form to a folder**

You can now assign metadata form to a specific folder within your Assets Essentials deployment. All assets in the folder, including assets in the sub-folders, then display properties defined in the assigned metadata form.

![assign metadata form to a folder](/help/release-notes/assets/assign-to-folder.png)

-->

* **Importazione in blocco da origini dati**: gli amministratori adesso [possono importare un numero elevato di risorse](/help/assets/bulk-import-assets-view.md) da un’origine dati ad AEM Assets. Gli amministratori non devono più caricare singole risorse o cartelle in AEM Assets. Le origini dati supportate per l’importazione in blocco includono Azure, AWS, Google Cloud e Dropbox.

  ![Importazione in blocco da un’origine dati](/help/release-notes/assets/bulk-import.png)

* **Strumenti di editing delle immagini gestiti da Adobe Express**: strumenti di editing delle immagini semplici e intuitivi[ gestiti da Adobe Express](/help/assets/edit-images-assets-view.md) disponibili direttamente in AEM Assets per aumentare il riutilizzo dei contenuti e velocizzarne la creazione.

  ![Editing di immagini con Adobe Express](/help/release-notes/assets/edit-adobe-express.png)

* **Flessibilità nel fissare elementi per Accesso rapido in La mia area di lavoro**: possibilità di selezionare e fissare gli elementi per l’utente, per l’intera organizzazione o per un elenco di gruppi in modo che vengano visualizzati nella [sezione Accesso rapido di La mia area di lavoro](/help/assets/my-workspace-assets-view.md) in base alla selezione.

  ![Fissa elementi per gruppi](/help/release-notes/assets/pin-items-for-groups.png)

### Nuove funzioni nella vista Amministratore {#admin-view-features}

**Miglioramenti alla ricerca**

* Ora gli amministratori possono [configurare la dimensione in batch delle risorse](/help/assets/search-assets.md#configure-asset-batch-size) che vengono visualizzate quando si esegue una ricerca. I risultati della ricerca delle risorse vengono visualizzati in multipli del numero di dimensioni in batch configurato durante l’ulteriore scorrimento verso il basso per caricare i risultati. È possibile scegliere tra le dimensioni in batch disponibili (200, 500 e 1000 risorse). Impostando un numero di dimensioni in batch più basso si ottengono tempi di risposta della ricerca più rapidi.

  ![Configurazione delle dimensioni in batch delle risorse](/help/release-notes/assets/assets-batch-size-configuration.png)

* Experience Manager Assets ora include una nuova version 9 dell’indice `damAssetLucene`. `damAssetLucene-9` modifica il comportamento del conteggio dei facet di query Oak in [ senza valutare il controllo degli accessi sui conteggi facet](/help/assets/search-assets.md) restituito dall’indice di ricerca sottostante, che determina tempi di risposta della ricerca più rapidi.

### Funzioni pre-release disponibili in [!DNL Experience Manager Assets] {#prerelease-features-assets}

* **Dynamic Media**: [supporto di tracce con più didascalie e multi-audio per video in Dynamic Media](/help/assets/dynamic-media/video.md#about-msma): è ora possibile aggiungere facilmente più didascalie e tracce audio a un video principale. Grazie a questa funzionalità, i video sono accessibili a un pubblico globale. È possibile personalizzare un singolo video principale pubblicato per un pubblico globale in più lingue e rispettare le linee guida sull’accessibilità per diverse aree geografiche. Gli autori possono gestire anche le didascalie e le tracce audio da una singola scheda nell’interfaccia utente.

  ![Scheda Didascalie e Tracce audio nella pagina Proprietà di una risorsa video selezionata.](/help/release-notes/assets/msma-aem-cs.png)*Scheda Didascalie e Tracce audio nella pagina delle Proprietà di una risorsa video selezionata.*

* **Risorse**: possibilità di selezionare archivi ZIP gestiti in Experience Manager ed [estrazione diretta dei file in Experience Manager](/help/assets/manage-digital-assets.md#extract-zip-archives), senza scaricarli.

  ![Fissa elementi per gruppi](/help/release-notes/assets/extract-archive.png)


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni disponibili in [!DNL Forms] {#new-features-available-in-forms-channel}

* [**Supporto reCAPTCHA di Google Enterprise**](/help/forms/captcha-adaptive-forms.md): utilizza Google reCAPTCHA Enterprise in un modulo adattivo per fornire una protezione avanzata contro le attività fraudolente e lo spam, fornendo un’esperienza utente più sicura. Grazie all’analisi avanzata dei rischi e all’integrazione diretta, gli utenti autentici possono inviare facilmente i moduli mentre i bot vengono bloccati in modo efficace.


### Funzioni pre-release disponibili in [!DNL Forms] {#pre-release-features-available-in-forms-channel}

* **Adobe Analytics con Configurazione dell’automazione di Experience Cloud per Forms**: ora è possibile abilitare Adobe Analytics con la configurazione dell’automazione di Experience grazie a un paio di pulsanti. Consente di collegare AEM Forms as a Cloud Service con i tag Experience Platform e Adobe Analytics per acquisire e tenere traccia delle metriche di prestazione per i moduli pubblicati.

* **Modello di rapporto di Adobe Analytics per moduli adattivi**: Forms as a Cloud Service ora fornisce un rapporto OOTB di Adobe Analytics. Consente di comprendere facilmente le prestazioni dei moduli. Le metriche a livello di modulo forniscono informazioni approfondite sulle prestazioni del modulo per più indicatori di prestazioni chiave (KPI, Key Performance Indicator), come rappresentazioni, visitatori, invii e tempo medio di riempimento. Monitorando il comportamento degli utenti e i feedback ricevuti, è possibile identificare le aree del modulo che creano confusione e promuovere i miglioramenti alla progettazione e alle funzionalità del modulo.

  ![Rapporti di Adobe Analytics sul coinvolgimento dell’utente nei moduli adattivi](/help/forms/assets/forms-analytics-report.png)

* **[Frammento di modulo in moduli adattivi basati su componenti core](/help/forms/adaptive-form-fragments-core-components.md)**: elimina la duplicazione, ottimizza l’inventario digitale e migliora la collaborazione migliorando l’esperienza di creazione dei moduli con i Frammenti di modulo. Questi componenti riutilizzabili si integrano perfettamente in più moduli, semplificando la creazione di moduli coerenti e dall’aspetto professionale. I Frammenti di modulo garantiscono riutilizzabilità, standardizzazione e coerenza del brand attraverso la funzionalità “cambia una volta e rifletti ovunque”. Migliora la manutenzione e l’efficienza, poiché gli aggiornamenti apportati in un’unica posizione vengono propagati automaticamente in tutti i moduli che utilizzano questi frammenti.

* **[Passaggio del flusso di lavoro Adobe Sign migliorato](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)**: il passaggio del flusso di lavoro di Adobe Sign è stato migliorato per includere quanto segue:
   * **Autenticazione basata su ID della Pubblica amministrazione per Adobe Sign**: l’autenticazione basata su ID della Pubblica amministrazione di Adobe Acrobat Sign offre un ulteriore livello di verifica, consentendo agli utenti di autenticare la propria identità utilizzando gli ID della pubblica amministrazione (patente di guida, carta d’identità, passaporto). Utilizzando documenti di identificazione attendibili, questo miglioramento aggiunge un ulteriore livello di affidabilità al processo di firma, rendendolo ideale per scenari che richiedono maggiore sicurezza, conformità e convalida degli utenti.

   * **Audit Trail per documenti di Adobe Sign**: utilizzo della funzione Audit Trail per ottenere informazioni dettagliate sul ciclo di vita dei documenti di Adobe Sign. Con l’Audit Trail è ora possibile mantenere un record completo di tutte le azioni e interazioni relative ai documenti. Tali azioni e interazioni includono dettagli quali visualizzazioni, modifiche o firme del documento, nonché le marche temporali di ciascun evento. Questo miglioramento è fondamentale per mantenere la conformità, risolvere le controversie e garantire l’integrità degli accordi digitali.

   * **Nuovi ruoli per i destinatari dell’accordo oltre al solo firmatario**: al fine di soddisfare meglio i requisiti del flusso di lavoro, Adobe Acrobat Sign può espandere i ruoli dei destinatari dell’accordo oltre al solo firmatario. Quando questa opzione è abilitata, ogni destinatario di un accordo può configurare il proprio ruolo singolarmente, in cui il Firmatario è l’impostazione predefinita.

* **[Proteggere i documenti con le API Document Assurance (parte delle API di comunicazione)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: le API Document Assurance consentono di proteggere le informazioni riservate firmando e crittografando i documenti. Tramite la crittografia, il contenuto di un documento viene trasformato in un formato illeggibile, in modo che solo gli utenti autorizzati possano accedervi. Questo strato di protezione fortificato non solo protegge i dati preziosi da persone non autorizzate, ma offre anche la massima tranquillità. Le API di firma consentono all’organizzazione di proteggere la sicurezza e la privacy dei documenti Adobe PDF che distribuisce e riceve. Questo servizio utilizza firme digitali e certificazione per garantire che solo i destinatari desiderati possano modificare i documenti.

* **Supporto del conteggio delle pagine nelle API di comunicazione**: ora, oltre a recuperare il documento tramite le API di comunicazione, è possibile ricevere anche le preziose informazioni sul numero di pagine contenute all’interno del documento.

* **[Gestione degli errori con handler degli errori personalizzati nell’editor delle regole](/help/forms/add-custom-error-handler-adaptive-forms-core-components.md)**: ora è possibile richiamare una funzione personalizzata a fronte di un errore restituito da un servizio esterno e fornire una risposta personalizzata agli utenti finali. Ad esempio, puoi richiamare un flusso di lavoro personalizzato nel back-end per codici di errore specifici o informare il cliente che il servizio non è disponibile.


### Programma dei moduli adattivi headless per i primi utilizzatori {#forms-early-adopter}

Utilizza i [moduli adattivi headless](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=it) per consentire a chi sviluppa di creare, pubblicare e gestire moduli interattivi a cui è possibile accedere e con cui si può interagire tramite API, anziché tramite un’interfaccia utente grafica tradizionale. I moduli adattivi headless consentono di:

* creare moduli multi-canale di alta qualità nel linguaggio di programmazione desiderato
* integrare in modo nativo i moduli nelle app desktop e per dispositivi mobili, nei siti web e nelle applicazioni chat
* riutilizzare i componenti proprietari dell’interfaccia utente con le applicazioni di Forms
* sfruttare la potenza di Adobe Experience Manager Forms

È possibile inviare un’e-mail a `aem-forms-headless@adobe.com` dal proprio ID e-mail ufficiale per aderire al programma per i primi utilizzatori.


## Elementi di base di [!DNL Experience Manager] as a [!DNL Cloud Service] {#foundation}

### Registri CDN {#cdn-logs}

Scarica i registri CDN da Cloud Manager, utili per ottimizzare il rapporto hit della cache e migliorare la visibilità nel flusso di distribuzione dei contenuti. [Ulteriori informazioni](/help/implementing/developing/introduction/logging.md#cdn-log) sul formato del registro CDN. Questa funzione verrà gradualmente implementata dai primi di settembre.

### Programma per i primi utilizzatori delle regole CDN e WAF {#waf-early-adopter}

Filtra il traffico sulla rete CDN in base a:

* intestazioni e proprietà delle richieste (ad esempio, indirizzo IP)
* modelli di traffico noti associati a traffico dannoso

Ti interessa provare questa funzione e condividere con noi un tuo feedback? Invia un messaggio e-mail a **aemcs-waf-adopter@adobe.com** dal tuo ID e-mail ufficiale per ulteriori informazioni sul programma per i primi utilizzatori. Lo spazio è limitato.

Ulteriori informazioni sulla funzione nell’articolo sono disponibili [qui](/help/security/traffic-filter-rules-including-waf.md).


## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes/current.md).

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
