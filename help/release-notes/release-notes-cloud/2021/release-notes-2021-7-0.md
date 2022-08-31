---
title: Note sulla versione 2021.7.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Note sulla versione 2021.7.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: 848f6a29-2e0f-4976-8ed7-6b7f69408c1b
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '1316'
ht-degree: 12%

---

# Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione per la versione corrente (più recente) di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti; per esempio, per quelli del 2020, 2021 e così via.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

Data di rilascio di [!DNL Adobe Experience Manager] come [!DNL Cloud Service] la versione corrente (2021.7.0) è il 29 luglio 2021.
La versione seguente (2021.8.0) è del 26 agosto 2021.

## Video sulla versione {#release-video}

Dai un&#39;occhiata al [Panoramica sulla versione di luglio 2021](https://video.tv.adobe.com/v/335580) video per un riepilogo delle funzioni aggiunte.

## Experience Manager Foundation as a Cloud Service {#foundation}

### Novità {#what-is-new-foundation}

* Configurazione più flessibile del dispatcher: I progetti possono essere organizzati più facilmente. Ad esempio, ora puoi includere più file di regole di riscrittura che riflettono la struttura del sito. [Scopri](/help/implementing/dispatcher/disp-overview.md#validation-debug) questa modalità flessibile, tra cui come strutturare la configurazione del dispatcher per sfruttarla al meglio.
* L’interfaccia utente di replica ad albero nella scheda &quot;Distribute&quot; dell’agente di replica deve essere considerata obsoleta ed è prevista la rimozione dopo il 30 settembre. [Scopri](/help/operations/replication.md#tree-activation) strategie di replica alternative.
* Bundle `org.apache.sling.datasource-1.0.4.jar` per il supporto per l’origine dati Sling è stato rimosso, perché presenta funzionalità obsolete e non è utilizzato dai clienti.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

* Funzionalità di automazione dei contenuti [!DNL Experience Manager Assets] sfruttare [!DNL Adobe Creative Cloud] API per automatizzare la produzione di risorse su larga scala. Migliora la velocità dei contenuti riducendo notevolmente il tempo impiegato e le iterazioni necessarie per creare varianti della stessa risorsa. La funzionalità non richiede alcuna programmazione e funziona dall’interno di DAM. Vedi [generare varianti di risorse utilizzando l’integrazione con Creative Cloud](/help/assets/cc-api-integration.md).

* [!DNL Experience Manager Assets] include [!DNL Document Cloud] Visualizzatore PDF per visualizzare in anteprima i documenti PDF in modo nativo. Questa funzione consente agli utenti di visualizzare in anteprima i file PDF multipagina senza alcuna elaborazione o conversione di file. Questa funzione migliora la parità con [!DNL Experience Manager] 6.5. I controlli disponibili nel visualizzatore includono zoom, navigazione nelle pagine, sganciare i controlli e visualizzarli a schermo intero. Gli utenti visualizzano anche l’anteprima e passano alle pagine e ai segnalibri. Sono supportati i commenti sul file stesso e in una versione futura verranno aggiunti commenti e annotazioni sul contenuto del file PDF.

   ![Anteprima dei file PDF in [!DNL Experience Manager] utilizzo di PDF Viewer](/help/assets/assets/preview-pdf-file-viewer.png)

* La funzionalità di download di Linkshare utilizza download asincroni che aumentano la velocità di download. Vedi [Scaricare le risorse condivise tramite la condivisione dei collegamenti](/help/assets/download-assets-from-aem.md#link-share-download).

   ![Scarica casella in entrata](/help/assets/assets/download-inbox.png)

* Le impostazioni di visualizzazione vengono migliorate per consentire agli utenti di scegliere una vista predefinita e un parametro di ordinamento predefinito.

   ![Imposta la visualizzazione predefinita in [!UICONTROL Visualizza impostazioni]](/help/assets/assets/view-settings-for-defaults.png)

* Gli utenti possono cercare e filtrare le cartelle in base ai predicati delle proprietà.

   ![Filtrare le cartelle di ricerca utilizzando i predicati di ricerca](/help/assets/assets/search-folders-via-predicates.png)

### Nuove funzioni disponibili in [!DNL Assets] canale prerelease {#assets-prerelease-features}

<!-- TBD: Not sure about GA of these enh. Shall check with the team.

* A user experience enhancements displays the number of assets present in a folder. For more than 1000 assets in a folder, [!DNL Assets] displays 1000+.

  ![Number of assets in a folder are displayed on the interface](/help/assets/assets/browse-folder-number-of-assets.png)

* You can directly apply a metadata schemas to a folder in its [!UICONTROL Properties].

  ![Add metadata schema from folder properties](/help/assets/assets/metadata-schema-folder-properties.png)
-->

* Quando condividi risorse digitali come collegamento, gli utenti possono copiare l’URL negli Appunti. Questo miglioramento consente di condividere le risorse in modo più rapido e conveniente.

### Bug fissati in [!DNL Assets] {#assets-bugs-fixed}

API `com.day.cq.dam.api.collection.SmartCollection` non è disponibile in [!DNL Experience Manager] come [!DNL Cloud Service]. (CQ-4326322)

## [!DNL Experience Manager Forms] come [!DNL Cloud Service] {#forms}

### Novità in [!DNL Forms] {#what-is-new-forms}

* Ora puoi utilizzare il servizio Automated forms conversion per [convertire i PDF forms in francese, tedesco e spagnolo](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?#language-specific-meta-model) ai moduli adattivi.
* È stato aggiunto un pannello separato all’editor modelli per visualizzare gli errori relativi ai componenti per moduli adattivi. Consente di consolidare tutti gli errori dei moduli adattivi in un&#39;unica posizione e di ridurre i tempi di risoluzione.

### Nuove funzioni disponibili nel canale prerelease di [!DNL Forms] {#beta-features-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [API di comunicazione](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html) consente di combinare modelli XDP e dati XML per generare documenti di stampa in vari formati. Il servizio consente di generare documenti in modalità sincrona. Le API consentono di creare applicazioni che permettono di:
   * Generare i documenti compilando i file modello con dati XML.
   * Generare moduli di output in vari formati, compresi flussi di stampa PDF non interattivi.
   * Generare file PDF di stampa da un modulo XFA PDF e Adobe Acrobat Form.

* **Esternalizzatore dati variabile**: È possibile salvare i dati delle variabili AEM flusso di lavoro su un sistema di storage esterno gestito dalla propria organizzazione.

* **Documento di record basato su Acroform**: È inoltre possibile [utilizzare Adobe Acrobat Form PDF (Acroform PDF)](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/generate-document-of-record-for-non-xfa-based-adaptive-forms.html) come modello per il modello di modulo Document of Record oltre a basato su XFA.

* **Connettore dell’archivio dati di Microsoft Azure**: Ora puoi [collega il modello dati del modulo all’archiviazione di Microsoft Azure](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-azure-storage.html). Consente di recuperare e archiviare dati adattivi del modulo in Microsoft Azure Storage as a BLOB.

## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* Componenti core CIF v2
   * Configurazioni semplificate e migliorate per URL PDP/PLP e SEO
   * Indicatore visivo per i dati di prodotto in fase di creazione in modalità per una migliore visibilità delle imminenti modifiche
   * Nuovo componente mappa del sito per le pagine di contenuto e di e-commerce

* Supporto per [Raccomandazione di prodotto Adobe Commerce Sensei, basata su Adobe Sensei](https://business.adobe.com/products/magento/product-recommendations.html) in AEM Storefront utilizzando consigli predefiniti o al volo creati

## [!DNL Experience Manager Screens] come [!DNL Cloud Service] {#screens}

### Correzioni di bug {#bug-fixes-screens}

* Le impostazioni di Content Provider vengono ora convalidate durante la creazione o l’aggiornamento.

* Tutte le visualizzazioni presentano la colonna delle cartelle.

* È possibile espandere la struttura del contenuto Screens.

* `bulk-offline-update-service` Mancavano tutte le autorizzazioni per alcuni ambienti.

* È stato aggiornato il collegamento dell’Aiuto per far corrispondere la nuova documentazione cloud di screens.

* È ora possibile annullare l&#39;assegnazione delle playlist e impedire la rimozione delle playlist con i lettori assegnati.

* Il lettore ora scarica di nuovo le risorse quando la cache &quot;ALL&quot; viene cancellata.

* Se la *Ora di fine* è impostato per il giorno successivo.

* `Back&Forward` ora funziona nell’interfaccia as a Cloud Service di Screens.

* Impossibile creare in precedenza tag con lo stesso nome ma con spazi dei nomi diversi.

## XML Documentation per Experience Manager as a Cloud Service {#xml-documentation}

### Novità {#what-is-new-xml-documentation}

XML Documentation, ad Experience Manager as a Cloud Service, è generalmente disponibile. Consente ad Experienci Manager clienti as a Cloud Service di acquistare XML Documentation e di importare, creare, gestire e distribuire contenuti tecnici su più canali, incluso Experience Manager Sites.

## Cloud Manager {#cloud-manager}

Questa sezione illustra le note sulla versione di Cloud Manager in AEM as a Cloud Service 2021.7.0.

### Data di pubblicazione {#release-cm-july}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.7.0 è il 15 luglio 2021.
La prossima versione è prevista per il 12 agosto 2021.

### Novità {#what-is-new-cm-july}

* I clienti ora possono utilizzare Azul 8 e 11 JDK per i processi di creazione di Cloud Manager e possono scegliere di utilizzare uno di questi JDK per i plug-in Maven compatibili con toolchain *o* l’intera esecuzione del processo Maven.

* L&#39;IP in uscita verrà ora registrato nel file di registro dei passaggi della build.

* Gli ambienti di stage e produzione che eseguono versioni precedenti di AEM ora segnalano lo stato **Aggiornamento disponibile**.

* Il numero massimo di certificati SSL supportati è aumentato a 20 per programma.

* Il numero massimo di domini configurabili è aumentato a 500 per ambiente.

* La **Gestisci Git** i pulsanti sono stati rinominati in **Accedere alle informazioni Git** e la finestra di dialogo è stata visivamente aggiornata.

* La versione di AEM Project Archetype utilizzata da Cloud Manager è stata aggiornata alla versione 28.

### Correzioni di bug {#bug-fixes-cm-july}

* In alcune situazioni, l’opzione Anteprima non era disponibile durante il binding di un Elenco consentiti IP a un ambiente.

* La navigazione manuale alla pagina dei dettagli di esecuzione per un’esecuzione non esistente non mostrava un errore, ma solo una schermata di caricamento infinita.

* Il messaggio di errore visualizzato quando è stato raggiunto il numero massimo di certificati SSL non è stato utile.

* In alcune circostanze, potrebbe esserci una discrepanza nella versione di rilascio mostrata nella scheda della pipeline sul **Panoramica** pagina.

* Aggiunta guidata programma non corretta: il nome non può essere modificato dopo la creazione.

### Problemi noti {#known-issues-cm-july}

I clienti che passano all&#39;uso di Azul JDK dovrebbero essere consapevoli che non tutte le applicazioni esistenti si compileranno senza errori su Azul JDK. Si consiglia vivamente di eseguire il test localmente prima di passare a un altro metodo.

## Cloud Acceleration Manager {#cam}

### Data di pubblicazione {#release-date-july-cam}

La data di rilascio di Cloud Acceleration Manager è il 15 luglio 2021.

### Novità {#what-is-new-cam}

Cloud Acceleration Manager è un&#39;applicazione basata su cloud progettata per guidare i team IT durante l&#39;intero percorso di transizione, dalla pianificazione al Cloud Service. Imposta i team per una migrazione di successo con best practice, suggerimenti, documentazione e strumenti consigliati da Adobe per aiutarti in ogni fase del percorso a AEM come Cloud Service. Ulteriori informazioni [qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=en).

>[!NOTE]
>
> Controlla questo [Video dimostrativo di Cloud Acceleration Manager](https://video.tv.adobe.com/v/335547).
