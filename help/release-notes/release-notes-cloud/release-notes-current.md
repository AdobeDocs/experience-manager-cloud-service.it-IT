---
title: Note sulla versione 2020.8.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: '[!DNL Adobe Experience Manager] as a Cloud Service: note sulla versione 2020.8.0.'
translation-type: tm+mt
source-git-commit: e1bf1a42ff81352c4946a2e5e5c731255234d5f3
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 7%

---


# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0 {#release-notes}

La sezione seguente illustra le note generali sulla versione di Experience Manager as a Cloud Service 2020.8.0.

## Data di rilascio {#release-date}

The release date for [!DNL Experience Manager] as a Cloud Service 2020.8.0 is August 27, 2020.

## [!DNL Adobe Experience Manager Sites] come Cloud Service {#sites}

### What is new in [!DNL Sites] {#what-is-new-sites}

* Possibilità di [ripristinare pagine e sottopagine (strutture ad albero pagina) in una versione](/help/sites-cloud/authoring/features/page-versions.md#reinstating-versions)precedente.

* Possibilità di creare avvii in AEM SPA Editor.

## [!DNL Adobe Experience Manager Assets] come Cloud Service {#assets}

### What is new in [!DNL Assets] {#what-is-new-assets}

* La transcodifica video è ora supportata con i microservizi delle risorse, con una nuova sezione Video nella schermata Profili [!UICONTROL di] elaborazione che supporta la configurazione del bitrate e delle dimensioni video (il formato di output è MP4 con il codec H.264). Per informazioni dettagliate, consultate [Gestione delle risorse](/help/assets/manage-video-assets.md#transcode-video)video. Per ulteriori opzioni di transcodifica e per la distribuzione di video è possibile utilizzare il [!DNL Dynamic Media] componente aggiuntivo.

* Nelle nuove [!DNL Experience Manager Assets] distribuzioni, la funzionalità di smart tag è ora configurata per impostazione predefinita. Non è necessario effettuare l’integrazione manuale con [!DNL Adobe Developer Console]. Nelle distribuzioni esistenti, gli amministratori [configurano l&#39;integrazione](/help/assets/smart-tags-configuration.md#aio-integration) degli smart tag come prima.

* Una nuova esperienza [di download delle](/help/assets/download-assets-from-aem.md) risorse consente di:

   * Download asincrono per i download di grandi dimensioni in modo che gli utenti non debbano attendere.

   * Una nuova API modulare per l&#39;estensibilità degli sviluppatori.

* [!DNL Experience Manager] ha migliorato le prestazioni di estrazione dei metadati per i microservizi delle risorse. Aumenta il throughput complessivo di assimilazione delle risorse.

* Utilizzate il profilo di elaborazione per generare metadati personalizzati utilizzando Compute Service. Consultate Metadati [personalizzati con il profilo di elaborazione](/help/assets/manage-metadata.md#metadata-compute-service)

* Un’esperienza di download più semplice per gli utenti di Brand Portal che gli amministratori possono configurare. Consultate [Panoramica](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/whats-new.html#download-configurations)dell&#39;esperienza di download.

* Le anteprime dei documenti PDF native e ad alta fedeltà sono ora disponibili nel Brand Portal. Consultate Panoramica [del visualizzatore di](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/whats-new.html#doc-viewer)documenti.

* Ora potete annullare la validità della cache CDN (Content Delivery Network) direttamente da [!DNL Dynamic Media] in AEM come Cloud Service (anziché utilizzare [!DNL Dynamic Media Classic]) per garantire che le risorse più recenti vengano servite in pochi minuti invece che in poche ore. Consultate [Annullamento della validità della cache CDN per mezzo di elementi multimediali dinamici](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)

* Il supporto per l&#39;accessibilità è stato aggiunto ai controlli dell&#39;interfaccia utente, alla navigazione, alla navigazione e all&#39;esperienza di ricerca in [!DNL Assets].

   * Se si preme il tasto Escape dopo aver selezionato [!UICONTROL Aggiungi rappresentazione] , lo stato attivo ritorna alla barra degli strumenti. <!-- via CQ-4293594-->
   * Lo stato attivo della tastiera funziona come previsto quando si utilizza la casella combinata E-mail. <!-- via CQ-4286215 -->
   * Gli elementi Accordion nella sezione dei filtri di ricerca vengono interpretati come Accordi espandibili standard. <!-- via CQ-4273103 -->
   * Quando applicate un tag a una risorsa, nella finestra di dialogo vengono visualizzati i tag come elementi ad albero. Gli attributi ARIA vengono applicati correttamente agli elementi della struttura per renderli accessibili. <!-- via CQ-4272964 -->

* [!DNL AEM Desktop app] È ora disponibile la versione 2.0.3, che migliora la compatibilità con [!DNL AEM] 6.5.5 [!DNL Service Pack] e aggiorna l&#39;elenco di compatibilità del sistema operativo client (rimozione di [!DNL Windows] 7 e [!DNL MacOS] versioni precedenti alla 10.14).

### Bug corretti in [!DNL Assets] {#bugs-fixed}

* L&#39;opzione Relate (Collega) e Annulla relazione (scollega) non risponde quando si fa clic per la prima volta. (CQ-4299022)
* Quando scaricate una risorsa, se selezionate l’opzione per riceverla via e-mail, l’e-mail non viene inviata. (CQ-4299146)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* È ora disponibile la funzionalità della console prodotto. Questo consente agli esperti di marketing/autori di AEM di visualizzare e navigare tra le categorie e i prodotti memorizzati nel back-end del commercio. È stato inoltre fornito il supporto per le proprietà di categorie e prodotti nella console Prodotti.

* Sono stati migliorati i selettori prodotto e categoria per consentire agli addetti al marketing di selezionare il prodotto tramite SKU o di selezionare la categoria tramite l&#39;ID categoria.

## Cloud Manager {#cloud-manager}

### Data di rilascio {#release-date-cm}

The Release Date for [!UICONTROL Cloud Manager] Version 2020.8.0 is August 06, 2020.

### Novità {#what-is-new-cloud-manager}

* Content Audit è una funzione abilitata nelle pipeline di produzione di siti di Cloud Manager. La configurazione della pipeline di produzione per i programmi con Siti ora include una terza scheda denominata Controllo **** contenuto. Ogni volta che viene eseguita una pipeline di produzione, verrà inclusa una nuova fase di controllo dei contenuti nella pipeline dopo il test funzionale personalizzato che valuterà il sito rispetto a una serie di dimensioni, tra cui prestazioni, SEO (ottimizzazione motore di ricerca), accessibilità, best practice e PWA (app Web progressiva).

   Refer to [Content Audit Testing](/help/implementing/cloud-manager/experience-audit-testing.md) for more details.

* Gli ambienti creati di recente nei programmi Assets ora verranno configurati automaticamente con Smart Content Services.

* Gli ambienti con sospensione possono essere disattivati dalla pagina **Panoramica** di Cloud Manager.

* Possibilità di eseguire verifiche dell’esperienza sulle pagine, con tecnologia Google Lighthouse. Come parte della pipeline di Cloud Manager, è possibile controllare e convalidare fino a 25 pagine in base ai KPI dell&#39;esperienza e visualizzare i punteggi nell&#39;interfaccia di Cloud Manager.

### Correzioni di bug {#bug-fixes-cm}

* Alcuni plug-in SonarQube non necessari e indesiderati venivano eseguiti come parte della scansione Code Quality.

* Nella pagina di esecuzione della pipeline, il nome del ramo non era formattato correttamente.

* In alcuni casi, le esecuzioni completate della pipeline non sono state registrate come completate, impedendo così nuove esecuzioni della pipeline.

* Le esecuzioni delle tubazioni si *bloccavano* occasionalmente a causa di problemi di comunicazione interni.

* Al momento del provisioning di una nuova organizzazione, ad alcuni utenti con ruoli amministrativi diversi dagli amministratori di sistema veniva erroneamente concesso l&#39;accesso a Cloud Manager.

* In alcune condizioni, il processo di indicizzazione degli aggiornamenti è stato avviato più volte in parallelo e ciò ha comportato un errore di distribuzione.

* La descrizione comandi sulle schede del programma non era corretta in modo coerente.

* L&#39;interfaccia utente ha erroneamente consentito di tentare operazioni in un ambiente durante l&#39;eliminazione.

* C&#39;è stata una mancata corrispondenza di colore nella pagina **Panoramica** di Cloud Manager.

### Problemi noti {#known-issues-cm}

* Sono incluse pagine non valide che riportano il punteggio medio di controllo dei contenuti al di sotto di quanto dovrebbero essere.

* La scheda Controllo contenuto visualizza erroneamente l&#39;URL di base utilizzando il dominio dell&#39;autore invece del dominio di pubblicazione.

* Per attivare il passaggio Controllo contenuto, gli utenti devono modificare la pipeline e, facoltativamente, aggiungere pagine. Se non viene aggiunta alcuna pagina, la pagina iniziale verrà sottoposta a controllo.

## Strumento Content Transfer (Trasferimento contenuti) {#content-transfer-tool}

Seguite questa sezione per saperne di più sulle novità e gli aggiornamenti per Content Transfer Tool Release v1.0.4.

### Novità {#what-is-new-ctt}

* Content Transfer Tool ora supporta Shared S3 DataStore.

### Correzioni di bug {#ctt-bug-fixes}

* Timeout aggiuntivi aggiunti allo strumento per completare le azioni.

* L’interfaccia utente della versione precedente talvolta mostrava un’estrazione corretta anche se il registro presentava degli errori.

## Strumenti di refactoring del codice {#code-refactoring-tools}

Segui questa sezione per saperne di più sulle novità e gli aggiornamenti per gli strumenti di refactoring del codice.

### Novità {#what-is-new-refactoring}

* Plug-in AIO-CLI rilasciato per unificare gli strumenti di refactoring del codice per consentire agli sviluppatori di richiamare ed eseguire strumenti di refactoring del codice da un&#39;unica posizione. Fare riferimento a Risorse [Git: per maggiori informazioni, fai clic su aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) .

* AEM Dispatcher Converter esteso per supportare le conversioni delle configurazioni del dispatcher dei servizi gestiti in sede e Adobe in AEM come configurazioni del dispatcher Cloud Service compatibili con il . Fare riferimento a Risorse [Git: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) per ulteriori dettagli.

* AEM Dispatcher Converter riscritto ` node.js ` e integrato con il plugin AIO-CLI.
