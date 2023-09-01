---
title: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: a635a727e431a73086a860249e4f42d297882298
workflow-type: tm+mt
source-wordcount: '1750'
ht-degree: 17%

---

# Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note specifiche sulla versione corrente (più recente) di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio 2021 o 2022.
>
>Dai un’occhiata alla [roadmap delle versioni di Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=it) per informazioni sulle prossime attivazioni delle funzioni per [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

La data di rilascio di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] la versione corrente (2023.8.0) è il 31 agosto 2023. La prossima versione (2023.9.0) è prevista per il 28 settembre 2023.

## Video sulla versione {#release-video}

Dai un’occhiata al video Panoramica sulla versione di agosto 2023 per un riepilogo delle funzioni aggiunte alla versione 2023.8.0:

>[!VIDEO](https://video.tv.adobe.com/v/3423535/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuove funzioni in [!DNL Experience Manager Sites] {#sites-features}

* Il [Console Frammenti di contenuto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=it) ora consente agli utenti di visualizzare i tag e di effettuare ricerche per tag applicati come metadati ai frammenti di contenuto. Per usufruire di questa funzionalità, gli utenti non dovranno più passare all’interfaccia utente Assets, riducendo il passaggio da un contesto all’altro e migliorando l’efficienza.

  ![Assegnazione di tag nella console Frammenti di contenuto](/help/assets/content-fragments-console-tags.png)
* Il nuovo Editor frammento di contenuto è ora disponibile su AEM as a Cloud Service. Consente agli autori di contenuti di essere più produttivi semplificando le attività di authoring e riducendo la necessità di passare da un’app all’altra durante la modifica dei contenuti.
  ![Nuovo editor frammento di contenuto](/help/release-notes/assets/newCFEditor.png)

Il nuovo editor di frammenti di contenuto offre i seguenti vantaggi che non sono disponibili nell’editor originale:
* Salvataggio automatico per una maggiore efficienza nell&#39;authoring e per evitare la perdita accidentale di modifiche.
* Visualizzazione gerarchica di un frammento di contenuto e dei relativi riferimenti utilizzando la struttura ad albero Struttura per una navigazione rapida all’interno di un frammento con struttura profonda.
  ![Struttura nell’Editor frammenti di contenuto](/help/release-notes/assets/newCFEditor_StructureTree.png)

* Caricamento in linea delle risorse come riferimenti di contenuto senza doverlo prima caricare in Asset DAM
* Anteprima ad hoc dell’esperienza con rendering fornita dal frammento di contenuto, per aiutare gli autori a visualizzare l’aspetto dei contenuti nell’app front-end
* Pubblicazione con 1 clic e annullamento della pubblicazione del frammento di contenuto dall’editor
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

* **Importare risorse in blocco da origini dati**: gli amministratori ora dispongono di [possibilità di importare un numero elevato di risorse](/help/assets/bulk-import-assets-view.md) da un’origine dati ad AEM Assets. Gli amministratori non devono più caricare singole risorse o cartelle in AEM Assets. Le origini dati supportate per l’importazione in blocco includono Azure, AWS, Google Cloud e Dropbox.

  ![Importare risorse in blocco da un’origine dati](/help/release-notes/assets/bulk-import.png)

* **Strumenti di modifica delle immagini basati su Adobi Express**: facile e intuitivo [strumenti di modifica delle immagini basati su Adobi Express](/help/assets/edit-images-assets-view.md) disponibile direttamente in AEM Assets per aumentare il riutilizzo dei contenuti e velocizzarne la distribuzione.

  ![Editing di immagini con Adobi Express](/help/release-notes/assets/edit-adobe-express.png)

* **Flessibilità durante l&#39;inserimento di elementi nell&#39;area di lavoro Accesso rapido**: possibilità di selezionare e fissare gli elementi per te, per l’intera organizzazione o per un elenco di gruppi in modo che vengano visualizzati nel [Sezione Accesso rapido della mia area di lavoro](/help/assets/my-workspace-assets-view.md) in base alla selezione.

  ![Fissa elementi per gruppi](/help/release-notes/assets/pin-items-for-groups.png)

### Nuove funzioni nella visualizzazione Amministratore {#admin-view-features}

**Miglioramenti alla ricerca**

* Ora gli amministratori possono [configurare la dimensione batch delle risorse](/help/assets/search-assets.md#configure-asset-batch-size) che vengono visualizzati quando si esegue una ricerca. I risultati della ricerca delle risorse vengono visualizzati in multipli del numero di dimensioni del batch configurato quando scorri ulteriormente verso il basso per caricare i risultati. Puoi scegliere tra le dimensioni disponibili del batch (200, 500 e 1000 risorse). Impostando un numero di dimensioni batch più basso si ottengono tempi di risposta della ricerca più rapidi.

  ![Configurazione delle dimensioni batch delle risorse](/help/release-notes/assets/assets-batch-size-configuration.png)

* Experience Manager Assets ora include una nuova versione 9 di `damAssetLucene` indice. `damAssetLucene-9` modifica il comportamento del conteggio dei facet di query Oak in [non valuta più il controllo degli accessi sui conteggi facet](/help/assets/search-assets.md) restituito dall&#39;indice di ricerca sottostante, che determina tempi di risposta della ricerca più rapidi.

### Funzioni pre-release disponibili in [!DNL Experience Manager Assets] {#prerelease-features-assets}

* **Dynamic Medie**: [Supporto di tracce multi-sottotitolo e multi-audio per video in Dynamic Medie](/help/assets/dynamic-media/video.md#about-msma)- È ora possibile aggiungere facilmente più sottotitoli e tracce audio a un video principale. Grazie a questa funzionalità, i video sono accessibili a un pubblico globale. Puoi personalizzare un singolo video principale pubblicato per un pubblico globale in più lingue e rispettare le linee guida sull’accessibilità per diverse aree geografiche. Gli autori possono anche gestire i sottotitoli e le tracce audio da una singola scheda nell’interfaccia utente.

  ![Scheda Sottotitoli e tracce audio nella pagina Proprietà di una risorsa video selezionata.](/help/release-notes/assets/msma-aem-cs.png)*Scheda Sottotitoli e tracce audio nella pagina Proprietà di una risorsa video selezionata.*

* **Risorse**: possibilità di selezionare archivi ZIP gestiti in Experience Manager e [estrazione diretta dei file in Experience Manager](/help/assets/manage-digital-assets.md#extract-zip-archives) senza scaricarli.

  ![Fissa elementi per gruppi](/help/release-notes/assets/extract-archive.png)


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuove funzioni disponibili in [!DNL Forms] {#new-features-available-in-forms-channel}

* [**Supporto aziendale Google reCAPTCHA**](/help/forms/captcha-adaptive-forms.md): utilizza Google reCAPTCHA Enterprise in un modulo adattivo per fornire una protezione avanzata contro le attività fraudolente e lo spam, fornendo un’esperienza utente più sicura. Grazie all’analisi avanzata dei rischi e all’integrazione perfetta, gli utenti autentici possono inviare facilmente i moduli mentre i bot vengono bloccati in modo efficace.


### Funzioni pre-release disponibili in [!DNL Forms] {#pre-release-features-available-in-forms-channel}

* **Adobe Analytics con Experience Cloud Setup Automation per Forms**: ora puoi abilitare Adobe Analytics con Experience Cloud Setup Automation con un paio di pulsanti. Consente di collegare AEM Forms as a Cloud Service con i tag Experienci Platform e Adobe Analytics per acquisire e tenere traccia delle metriche delle prestazioni per i moduli pubblicati.

* **Modello di rapporto Adobe Analytics per Adaptive Forms**: Forms as a Cloud Service ora fornisce un rapporto Adobe Analytics OOTB. Consente di comprendere facilmente le prestazioni dei moduli. Le metriche a livello di modulo forniscono informazioni approfondite sulle prestazioni del modulo per più indicatori di prestazioni chiave (KPI, Key Performance Indicator), come rappresentazioni, visitatori, invii e tempo medio di riempimento. Monitorando il comportamento degli utenti e i feedback ricevuti, è possibile identificare le aree del modulo che causano confusione e guidare i miglioramenti alla progettazione e alle funzionalità del modulo.

  ![Report Adobe Analytics sul coinvolgimento degli utenti dei moduli adattivi](/help/forms/assets/forms-analytics-report.png)

* **[Frammento di modulo in Forms adattivo basato su componenti core](/help/forms/adaptive-form-fragments-core-components.md)**: puoi dire addio alla duplicazione, ottimizzare l’inventario digitale e migliorare la collaborazione migliorando l’esperienza di creazione dei moduli con i frammenti di modulo. Questi componenti riutilizzabili si integrano perfettamente in più moduli, semplificando la creazione di moduli coerenti e dall’aspetto professionale. I frammenti di modulo garantiscono riutilizzabilità, standardizzazione e coerenza del brand attraverso la funzionalità &quot;cambia una volta e riflette ovunque&quot;. Aumenta la manutenibilità e l’efficienza, poiché gli aggiornamenti apportati in un’unica posizione vengono propagati automaticamente in tutti i moduli che utilizzano questi frammenti.

* **[Passaggio del flusso di lavoro Adobe Sign migliorato](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)**: il passaggio del flusso di lavoro di Adobe Sign è stato migliorato per includere quanto segue:
   * **Autenticazione basata su documento ufficiale per Adobe Sign**: l’autenticazione basata su documento ufficiale di Adobe Acrobat Sign offre un ulteriore livello di verifica, consentendo agli utenti di autenticare la propria identità utilizzando gli ID governativi (patente di guida, carta d’identità, passaporto). Sfruttando i documenti di identificazione attendibili, questo miglioramento aggiunge un ulteriore livello di affidabilità al processo di firma, rendendolo ideale per scenari che richiedono maggiore sicurezza, conformità e convalida degli utenti.

   * **Audit Trail per documenti Adobe Sign**: utilizza la funzione Audit Trail per ottenere informazioni dettagliate sul ciclo di vita dei documenti Adobe Sign. Con Audit Trail è ora possibile mantenere un registro completo di tutte le azioni e interazioni relative ai documenti. Questo include dettagli quali chi ha visualizzato, modificato o firmato il documento, insieme ai timestamp di ogni evento. Questo miglioramento è fondamentale per mantenere la conformità, risolvere le controversie e garantire l’integrità degli accordi digitali.

   * **Nuovi ruoli per i destinatari del contratto oltre al solo firmatario**: Adobe Acrobat Sign può espandere i ruoli dei destinatari del contratto oltre al solo firmatario, per soddisfare meglio i requisiti del flusso di lavoro. Quando questa opzione è abilitata, ogni destinatario di un contratto ha il proprio ruolo configurabile singolarmente, con Firmatario come impostazione predefinita.

* **[Protect i tuoi documenti con le API Document Assurance (parte delle API di comunicazione)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: le API Document Assurance ti consentono di proteggere le informazioni riservate firmando e crittografando i documenti. Tramite la crittografia, il contenuto di un documento viene trasformato in un formato illeggibile, in modo che solo gli utenti autorizzati possano accedervi. Questo strato di protezione fortificato non solo protegge i dati preziosi da occhi non autorizzati, ma offre anche la massima tranquillità. Le API di firma consentono all’organizzazione di proteggere la sicurezza e la privacy dei documenti Adobe PDF che distribuisce e riceve. Questo servizio utilizza firme digitali e certificazione per garantire che solo i destinatari desiderati possano modificare i documenti.

* **Supporto del conteggio delle pagine nelle API di comunicazione**: ora, oltre a recuperare il documento tramite le API di comunicazione, puoi ricevere anche le preziose informazioni sul numero di pagine contenute all’interno del documento.

* **[Gestione degli errori con gestori degli errori personalizzati nell’editor di regole](/help/forms/add-custom-error-handler-adaptive-forms-core-components.md)**: ora puoi richiamare una funzione personalizzata in risposta a un errore restituito da un servizio esterno e fornire una risposta personalizzata agli utenti finali. Ad esempio, puoi richiamare un flusso di lavoro personalizzato nel back-end per codici di errore specifici o informare il cliente che il servizio non è disponibile.


### Programma dei moduli adattivi headless per i primi utilizzatori {#forms-early-adopter}

Utilizza i [moduli adattivi headless](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=it) per consentire a chi sviluppa di creare, pubblicare e gestire moduli interattivi a cui è possibile accedere e con cui si può interagire tramite API, anziché tramite un’interfaccia utente grafica tradizionale. I moduli adattivi headless consentono di:

* creare moduli multi-canale di alta qualità nel linguaggio di programmazione desiderato
* integrare in modo nativo i moduli nelle app desktop e per dispositivi mobili, nei siti web e nelle applicazioni chat
* riutilizzare i componenti proprietari dell’interfaccia utente con le applicazioni di Forms
* sfruttare la potenza di Adobe Experience Manager Forms

È possibile inviare un’e-mail a `aem-forms-headless@adobe.com` dal proprio ID e-mail ufficiale per aderire al programma per i primi utilizzatori.


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### Registri CDN {#cdn-logs}

Scarica i registri CDN da Cloud Manager, utile per ottimizzare il rapporto cache-hit e migliorare la visibilità nel flusso di distribuzione dei contenuti. [Informazioni su](/help/implementing/developing/introduction/logging.md#cdn-log) il formato di registro CDN. Questa funzione verrà gradualmente implementata dai primi di settembre.

### Programma per l’adozione anticipata delle regole CDN e WAF {#waf-early-adopter}

Filtra il traffico sulla rete CDN in base a:
* intestazioni e proprietà della richiesta (ad esempio, indirizzo IP)
* modelli di traffico noti per essere associati a traffico dannoso

Ti interessa provare questa funzione e condividere feedback? Invia un messaggio e-mail a **aemcs-waf-adopter@adobe.com** dal tuo ID e-mail ufficiale per ulteriori informazioni sul programma early adopter. Lo spazio è limitato.

Ulteriori informazioni sulla funzione nell’articolo [qui](/help/security/cdn-and-waf-rules.md).


## Note sulla versione di manutenzione {#maintenance}

Puoi trovare le ultime note sulla versione di manutenzione [qui](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

L’elenco completo dei rilasci mensili di Cloud Manager è disponibile [qui](/help/implementing/cloud-manager/release-notes/current.md).

## Strumenti di migrazione {#migration-tools}

L’elenco completo dei rilasci mensili degli strumenti di migrazione è disponibile [qui](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
