---
title: Note sulla versione 2020.8.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: '[!DNL Adobe Experience Manager] as a Cloud Service - Note sulla versione 2020.8.0.'
exl-id: 83413130-ae90-4419-bcf7-42fdc740452b
translation-type: tm+mt
source-git-commit: 33e92b9cd19dd49dcdb6a8c8f30feccb755f615f
workflow-type: tm+mt
source-wordcount: '1050'
ht-degree: 7%

---

# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0 {#release-notes}

La sezione seguente illustra le note generali sulla versione di Experience Manager as a Cloud Service 2020.8.0.


## [!DNL Adobe Experience Manager Sites] come Cloud Service  {#sites}

### Novità in [!DNL Sites] {#what-is-new-sites}

* Possibilità di [ripristinare pagine e sottopagine (strutture ad albero pagina) a una versione precedente](/help/sites-cloud/authoring/features/page-versions.md#reinstating-versions).

* Possibilità di [creare lanci](/help/sites-cloud/authoring/launches/overview.md) in AEM [SPA Editor.](/help/implementing/developing/hybrid/introduction.md)


## [!DNL Adobe Experience Manager Assets] come Cloud Service  {#assets}

### Novità in [!DNL Assets] {#what-is-new-assets}

* La transcodifica video è ora supportata con i microservizi per le risorse. Una nuova sezione della configurazione [!UICONTROL Profili di elaborazione] consente di impostare il bit rate e le dimensioni del video. Il formato di uscita è MP4 con codec H.264. Per informazioni dettagliate, consulta [gestire le risorse video](/help/assets/manage-video-assets.md#transcode-video). Per ulteriori opzioni di transcodifica e per la distribuzione video, utilizza il componente aggiuntivo [!DNL Dynamic Media] .

* Nelle nuove implementazioni di [!DNL Experience Manager Assets] , la funzionalità di assegnazione tag avanzati è ora configurata per impostazione predefinita. Non è necessario eseguire l&#39;integrazione manuale con [!DNL Adobe Developer Console]. Sulle implementazioni esistenti, gli amministratori configurano l’integrazione di tag avanzati come in precedenza.

* Una nuova [esperienza di download delle risorse](/help/assets/download-assets-from-aem.md) consente:

   * Download asincrono per i download di grandi dimensioni in modo che gli utenti non debbano attendere.
   * Una nuova API modulare per l’estensibilità degli sviluppatori.

* L’estrazione dei metadati per i microservizi per le risorse offre prestazioni migliori. Aumenta il throughput complessivo di inserimento delle risorse.

* Utilizza un profilo di elaborazione per generare metadati personalizzati utilizzando Compute Service. Consulta [Metadati personalizzati utilizzando il profilo di elaborazione](/help/assets/manage-metadata.md#metadata-compute-service).

* Un’esperienza di download più semplice per gli utenti di Brand Portal che gli amministratori possono configurare. Consulta [scarica panoramica esperienza](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/whats-new.html#download-configurations).

* Le anteprime dei documenti PDF nativi e ad alta fedeltà sono ora disponibili in Brand Portal. Consulta [panoramica visualizzatore di documenti](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/whats-new.html#doc-viewer).

* Ora puoi annullare la validità della cache CDN (Content Delivery Network) direttamente da [!DNL Dynamic Media] in AEM come Cloud Service (anziché utilizzare [!DNL Dynamic Media Classic]). In questo modo le risorse più recenti vengono servite in pochi minuti anziché in ore. Consulta [Annullamento della validità della CDN tramite Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md).

* Il supporto per l’accessibilità è stato aggiunto ai controlli dell’interfaccia utente, all’esperienza di navigazione, navigazione e ricerca in [!DNL Assets].

   * Se si preme il tasto Esc dopo aver selezionato l&#39;opzione [!UICONTROL Aggiungi rappresentazione], lo stato attivo torna alla barra degli strumenti. <!-- via CQ-4293594-->
   * Lo stato attivo della tastiera funziona come previsto quando si utilizza la casella combinata e-mail. <!-- via CQ-4286215 -->
   * Gli elementi a soffietto nella sezione dei filtri di ricerca vengono interpretati come pannello a soffietto espandibile standard. <!-- via CQ-4273103 -->
   * Quando applicate un tag a una risorsa, nella finestra di dialogo i tag vengono visualizzati come elementi ad albero. Gli attributi ARIA vengono applicati in modo appropriato agli elementi della struttura per renderli accessibili ora. <!-- via CQ-4272964 -->

* [!DNL AEM Desktop app] È ora disponibile la versione 2.0.3 di . Migliora la compatibilità con [!DNL Experience Manager] Service Pack 6.5.5 e dispone di un elenco di compatibilità del sistema operativo client aggiornato. [!DNL Windows] 7 e  [!DNL macOS] versioni precedenti alla 10.14 non sono supportate.

### Bug corretti in [!DNL Assets] {#bugs-fixed}

* L’opzione Relate (Collega) e Unrelation (Annulla relazione) non risponde quando viene fatto clic per la prima volta. (CQ-4299022)
* Quando si scarica una risorsa, se si seleziona l’opzione per riceverla tramite e-mail, l’e-mail non viene inviata. (CQ-4299146)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* È ora disponibile la funzione Console del prodotto . Questo consente agli esperti di marketing/autori in AEM di visualizzare e navigare tra le categorie e i prodotti memorizzati nel back-end di Commerce. È inoltre disponibile il supporto per le proprietà di categorie e prodotti nella console Prodotti.

* Sono stati migliorati i selettori di prodotti e categorie per consentire agli addetti al marketing di selezionare un prodotto tramite SKU o di selezionare una categoria tramite ID categoria.

## Cloud Manager {#cloud-manager}

### Data di rilascio {#release-date-cm}

La data di rilascio per [!UICONTROL Cloud Manager] versione 2020.8.0 è il 6 agosto 2020.

### Novità {#what-is-new-cloud-manager}

* Verifica del contenuto è una funzione abilitata nelle pipeline di produzione di Cloud Manager Sites. La configurazione della pipeline di produzione per i programmi con Sites ora include una terza scheda denominata **Verifica del contenuto**. Ogni volta che viene eseguita una pipeline di produzione, nella pipeline verrà incluso un nuovo passaggio di Verifica del contenuto dopo un test funzionale personalizzato che valuterà il sito in base a una serie di dimensioni, tra cui prestazioni, SEO (Search Engine Optimization), accessibilità, best practice e PWA (Progressive Web App).


   >[!NOTE]
   >La funzione di audit del contenuto è stata successivamente rinominata in Audit esperienze.

   Per ulteriori informazioni, consulta [Test di audit esperienza](/help/implementing/cloud-manager/experience-audit-testing.md) .

* Gli ambienti creati di recente nei programmi Assets ora verranno configurati automaticamente con Smart Content Services.

* Gli ambienti sospesi possono essere disattivati dalla pagina **Panoramica** di Cloud Manager.

* Possibilità di eseguire controlli di esperienza sulle pagine, con tecnologia Google Lighthouse. Come parte della pipeline di Cloud Manager, è possibile controllare e convalidare fino a 25 pagine in base ai KPI di esperienza e visualizzare i punteggi nell’interfaccia utente di Cloud Manager.

### Correzioni di bug {#bug-fixes-cm}

* Alcuni plug-in SonarQube superflui e indesiderati venivano eseguiti come parte della scansione Code Quality.

* Nella pagina di esecuzione della pipeline, il nome del ramo non era formattato correttamente.

* In alcuni casi, le esecuzioni completate della pipeline non sono state registrate correttamente come completate, impedendo così nuove esecuzioni della pipeline.

* Le esecuzioni delle pipeline verrebbero occasionalmente bloccate a causa di problemi di comunicazione interni.**

* Al momento del provisioning di una nuova organizzazione, ad alcuni utenti con ruoli amministrativi diversi dagli amministratori di sistema è stato erroneamente concesso l’accesso a Cloud Manager.

* In determinate condizioni, il processo di indicizzazione dell&#39;aggiornamento è stato avviato più volte in parallelo, causando un errore di distribuzione.

* La descrizione comandi sulle schede del programma non era corretta in modo coerente.

* L&#39;interfaccia utente ha erroneamente consentito il tentativo di eseguire operazioni in un ambiente durante l&#39;eliminazione.

* C&#39;è stata una mancata corrispondenza dei colori nella pagina **Panoramica** di Cloud Manager.

### Problemi noti {#known-issues-cm}

* Sono incluse pagine non valide che riportano il punteggio medio di Verifica del contenuto al di sotto di quello che dovrebbe essere.

* La scheda Verifica del contenuto visualizza in modo errato l’URL di base utilizzando il dominio dell’autore invece del dominio di pubblicazione.

* Per attivare il passaggio Verifica contenuto, gli utenti devono modificare la pipeline e, facoltativamente, aggiungere pagine. Se non viene aggiunta alcuna pagina, la home page verrà sottoposta a controllo.

## Strumento Content Transfer (Trasferimento contenuti) {#content-transfer-tool}

Leggi questa sezione per scoprire le novità e gli aggiornamenti della versione 1.0.4 dello strumento Content Transfer (Trasferimento contenuti).

### Novità {#what-is-new-ctt}

* Lo strumento Content Transfer (Trasferimento contenuti) ora supporta Shared S3 DataStore.

### Correzioni di bug {#ctt-bug-fixes}

* Sono stati aggiunti timeout aggiuntivi per il completamento delle azioni da parte dello strumento.

* L’interfaccia utente della versione precedente talvolta mostrava l’estrazione corretta anche se il registro mostrava errori.

## Strumenti di refactoring del codice {#code-refactoring-tools}

Leggi questa sezione per scoprire le novità e gli aggiornamenti di Strumenti di refactoring del codice.

### Novità {#what-is-new-refactoring}

* Plug-in AIO-CLI rilasciato per unificare gli strumenti di refactoring del codice per consentire agli sviluppatori di richiamare ed eseguire gli strumenti di refactoring del codice da un’unica posizione. Fai riferimento a [Risorsa Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) per maggiori dettagli.

* AEM Dispatcher Converter esteso per supportare le conversioni delle configurazioni del Dispatcher On-Premise e Adobe Managed Services in AEM come configurazioni del Dispatcher compatibili con il Cloud Service. Fai riferimento a [Risorsa Git: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) per ulteriori dettagli.

* AEM Dispatcher Converter riscritto in ` node.js ` e integrato con il plug-in AIO-CLI.
