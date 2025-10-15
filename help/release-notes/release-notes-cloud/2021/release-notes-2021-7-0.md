---
title: Note sulla versione 2021.7.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione 2021.7.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: 848f6a29-2e0f-4976-8ed7-6b7f69408c1b
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1292'
ht-degree: 30%

---

# Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione per la versione corrente (più recente) di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti, ad esempio quelle del 2020 e 2021.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

La data di rilascio della versione corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2021.7.0) è il venerdì 29 luglio 2021.
La seguente versione (2021.8.0) è del venerdì 26 agosto 2021.

## Video sulla versione {#release-video}

Dai un&#39;occhiata al video Panoramica sulla versione di [luglio 2021](https://video.tv.adobe.com/v/335580) per un riepilogo delle funzioni aggiunte.

## Experience Manager di base as a Cloud Service {#foundation}

### Novità {#what-is-new-foundation}

* Configurazione più flessibile di Dispatcher: i progetti possono essere organizzati più facilmente. Ad esempio, ora puoi includere più file di regole di riscrittura che riflettono la struttura del sito. [Scopri](/help/implementing/dispatcher/disp-overview.md#validation-debug) questa modalità flessibile, tra cui come strutturare la configurazione di Dispatcher in modo da poterne usufruire.
* L’interfaccia utente di replica ad albero nella scheda &quot;Distribuisci&quot; dell’agente di replica deve essere considerata obsoleta e rimossa dopo il 30 settembre 2021. [Scopri](/help/operations/replication.md#tree-activation) strategie di replica alternative.
* Il bundle `org.apache.sling.datasource-1.0.4.jar` per il supporto dell&#39;origine dati Sling è stato rimosso perché presenta funzionalità obsolete e non è più utilizzato dai clienti.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

* La funzionalità di automazione dei contenuti consente a [!DNL Experience Manager Assets] di utilizzare le API [!DNL Adobe Creative Cloud] per automatizzare la produzione delle risorse su larga scala. Migliora la velocità dei contenuti riducendo notevolmente il tempo impiegato e le iterazioni necessarie per creare varianti della stessa risorsa. La funzionalità non richiede alcuna programmazione e funziona dall’interno di DAM. Consulta [generare varianti di risorse utilizzando l&#39;integrazione Creative Cloud](/help/assets/cc-api-integration.md).

* [!DNL Experience Manager Assets] include [!DNL Document Cloud] visualizzatore PDF per visualizzare in anteprima i documenti PDF in modo nativo. Questa funzione consente agli utenti di visualizzare in anteprima i file di PDF con più pagine senza alcuna elaborazione o conversione di file. Questa funzionalità migliora la parità con [!DNL Experience Manager] 6.5. I controlli disponibili nel visualizzatore includono lo zoom, la navigazione alle pagine, la disancora dei controlli e la visualizzazione a schermo intero. Gli utenti possono anche visualizzare in anteprima e passare a pagine e segnalibri. Sono supportati i commenti sul file stesso. I commenti e le annotazioni sul contenuto del file PDF sono pianificati per una versione futura.

  ![Anteprima dei file PDF in [!DNL Experience Manager] tramite Visualizzatore PDF](/help/assets/assets/preview-pdf-file-viewer.png)

* La funzionalità di download tramite condivisione di collegamenti utilizza download asincroni, più veloci. Per ulteriori informazioni, consulta [Scaricare le risorse condivise utilizzando la condivisione dei collegamenti](/help/assets/download-assets-from-aem.md#link-share-download).

  ![Scarica casella in entrata](/help/assets/assets/download-inbox.png)

* Le impostazioni di visualizzazione sono migliorate e consentono agli utenti di scegliere una vista e un parametro di ordinamento predefiniti.

  ![Imposta visualizzazione predefinita in [!UICONTROL Impostazioni visualizzazione]](/help/assets/assets/view-settings-for-defaults.png)

* Gli utenti possono cercare e filtrare le cartelle in base ai predicati delle proprietà.

  ![Filtrare le cartelle di ricerca utilizzando i predicati di ricerca](/help/assets/assets/search-folders-via-predicates.png)

### Nuove funzioni disponibili nel canale prerelease [!DNL Assets] {#assets-prerelease-features}

<!-- TBD: Not sure about GA of these enh. Shall check with the team.

* A user experience enhancements displays the number of assets present in a folder. For more than 1000 assets in a folder, [!DNL Assets] displays 1000+.

  ![Number of assets in a folder are displayed on the interface](/help/assets/assets/browse-folder-number-of-assets.png)

* You can directly apply a metadata schemas to a folder in its [!UICONTROL Properties].

  ![Add metadata schema from folder properties](/help/assets/assets/metadata-schema-folder-properties.png)
-->

* Quando condividi risorse digitali come collegamento, gli utenti possono copiare l’URL negli Appunti. Questo miglioramento consente di condividere le risorse in modo più rapido e conveniente.

### Bug corretti in [!DNL Assets] {#assets-bugs-fixed}

API `com.day.cq.dam.api.collection.SmartCollection` non disponibile in [!DNL Experience Manager] come [!DNL Cloud Service]. (CQ-4326322)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Novità in [!DNL Forms] {#what-is-new-forms}

* È ora possibile utilizzare il servizio di Automated forms conversion per [convertire i PDF forms in francese, tedesco e spagnolo](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=it&#language-specific-meta-model) in moduli adattivi.
* È stato aggiunto un pannello separato all’editor modelli per visualizzare gli errori relativi ai componenti dei moduli adattivi. Consente di consolidare tutti gli errori dei moduli adattivi in un’unica posizione e di ridurre i tempi di risoluzione.

### Nuove funzioni disponibili nel canale pre-release di [!DNL Forms] {#beta-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [API di comunicazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html?lang=it) consente di combinare modelli XDP e dati XML per generare documenti di stampa in vari formati. Il servizio consente di generare documenti in modalità sincrona. Le API consentono di creare applicazioni che permettono di:
   * Generare i documenti compilando i file modello con dati XML.
   * Generare moduli di output in vari formati, compresi flussi di stampa PDF non interattivi.
   * Generare file PDF di stampa da un modulo XFA PDF e di Adobe Acrobat Form.

* **Esternalizzazione dei dati delle variabili**: puoi salvare i dati delle variabili del flusso di lavoro AEM su un sistema di archiviazione esterno gestito dalla tua organizzazione.

* **Documento di record basato su Acroform**: puoi anche [utilizzare Adobe Acrobat Form PDF (Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms.html?lang=it) come modello per documento record oltre al modello di modulo basato su XFA.

* **Connettore per l&#39;archivio dati Microsoft® Azure**: è ora possibile [collegare il modello dati dei moduli al sistema di archiviazione Microsoft® Azure](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-azure-storage.html?lang=it). Consente di recuperare e archiviare i dati dei moduli adattivi come BLOB nell’archiviazione di Microsoft® Azure.

## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* Componenti core CIF v2
   * Configurazioni semplificate e migliorate per URL PDP/PLP e SEO
   * Indicatore visivo per i dati di prodotto in staging in modalità di authoring per una migliore visibilità delle modifiche imminenti
   * Nuovo componente sitemap per contenuti e pagine commerce

* Supporto per [Adobe Commerce Sensei Product Recommendations, basato su Adobe Sensei](https://business.adobe.com/it/products/magento/product-recommendations.html) in AEM Storefront utilizzando consigli predefiniti o creati al volo

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

### Correzioni di bug {#bug-fixes-screens}

* Le impostazioni del provider di contenuti ora vengono convalidate durante la creazione o l’aggiornamento.

* Tutte le viste di visualizzazione hanno la colonna delle cartelle.

* È possibile espandere Struttura contenuto di Screens.

* A `bulk-offline-update-service` mancavano tutte le autorizzazioni per alcuni ambienti.

* È stato aggiornato il collegamento dell’Aiuto in modo che corrisponda alla nuova documentazione cloud Screens.

* Annulla l’assegnazione delle playlist e non consentire la rimozione delle playlist quando ai lettori sono assegnati, ora funziona.

* Il lettore ora scarica nuovamente Assets quando la cache &quot;ALL&quot; viene cancellata.

* La pianificazione ripetuta ora funziona, se *Ora di fine* è impostato per il giorno successivo.

* `Back&Forward` ora funziona nell&#39;interfaccia utente di Screens as a Cloud Service.

* Non è stato possibile creare in precedenza tag con lo stesso nome ma diversi spazi dei nomi.

## XML Documentation, ad Experience Manager, as a Cloud Service {#xml-documentation}

### Novità {#what-is-new-xml-documentation}

XML Documentation, ad Experience Manager as a Cloud Service, è generalmente disponibile. Consente ai clienti di Experience Manager as a Cloud Service di acquistare un componente aggiuntivo XML Documentation per importare, creare, gestire e distribuire contenuti tecnici su più canali, incluso Experience Manager Sites.

## Cloud Manager {#cloud-manager}

Questa sezione illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.7.0.

### Data di rilascio {#release-cm-july}

La data di pubblicazione di Cloud Manager in AEM as a Cloud Service 2021.7.0 è il 15 luglio 2021.
La prossima versione è pianificata per il 12 agosto 2021.

### Novità {#what-is-new-cm-july}

* I clienti ora possono utilizzare i JDK di Azul 8 e 11 per i processi di build Cloud Manager e possono scegliere di utilizzare uno di questi JDK per i plug-in Maven compatibili con le toolchain *o* per l’intera esecuzione del processo Maven.

* L’IP in uscita è ora registrato nel file di registro della fase di build.

* Negli ambienti di stage e produzione con versioni precedenti di AEM viene ora segnalato lo stato **Aggiornamento disponibile**.

* Il numero massimo di certificati SSL supportati è aumentato a 20 per programma.

* Il numero massimo di domini configurabili è aumentato a 500 per ambiente.

* Il pulsante **Gestisci Git** è stato rinominato **Accedi a informazioni Git** e la finestra di dialogo è stata aggiornata visivamente.

* L’archetipo del progetto AEM utilizzato da Cloud Manager è stato aggiornato alla versione 28.

### Correzioni di bug {#bug-fixes-cm-july}

* In alcune situazioni, l’opzione Anteprima non era disponibile quando si associava un inserisco nell&#39;elenco Consentiti IP a un ambiente.

* La navigazione manuale alla pagina dei dettagli sull’esecuzione di un’esecuzione non esistente non mostrava un errore, ma solo una schermata di caricamento infinita.

* Il messaggio di errore visualizzato quando è stato raggiunto il numero massimo di certificati SSL non è stato utile.

* In alcune circostanze era presente una discrepanza nella versione mostrata nella scheda della pipeline della pagina **Panoramica**.

* La procedura guidata per l’aggiunta di un programma indicava erroneamente che il nome non poteva essere modificato dopo la creazione.

### Problemi noti {#known-issues-cm-july}

I clienti che passano all’utilizzo dei JDK di Azul devono sapere che non tutte le applicazioni esistenti vengono compilate senza errori sul JDK di Azul. L’Adobe consiglia di eseguire il test a livello locale prima di cambiare.

## Cloud Acceleration Manager {#cam}

### Data di rilascio {#release-date-july-cam}

La data di rilascio per Cloud Acceleration Manager è il 15 luglio 2021.

### Novità {#what-is-new-cam}

Cloud Acceleration Manager è un’applicazione basata su cloud progettata per guidare i team IT durante l’intero percorso di transizione, dalla pianificazione al Cloud Service. Prepara il tuo team per una migrazione di successo con best practice, suggerimenti, documentazione e strumenti consigliati dagli Adobi per ogni fase del percorso al Cloud Service AEM. Ulteriori informazioni [qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=it).

>[!NOTE]
>
> Guarda questo [video dimostrativo su Cloud Acceleration Manager](https://video.tv.adobe.com/v/335547).
