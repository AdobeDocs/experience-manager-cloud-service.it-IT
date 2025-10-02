---
title: Note sulla versione 2020.8.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: '[!DNL Adobe Experience Manager] Note sulla versione 2020.8.0 di as a Cloud Service.'
exl-id: 83413130-ae90-4419-bcf7-42fdc740452b
feature: Release Information
role: Admin
source-git-commit: 2aea79d42ef9627a8fc758077a7ee012592888d7
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 34%

---

# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0 {#release-notes}

La sezione seguente illustra le note generali sulla versione di Experience Manager as a Cloud Service 2020.8.0.


## as a Cloud Service [!DNL Adobe Experience Manager Sites] {#sites}

### Novità in [!DNL Sites] {#what-is-new-sites}

* Possibilità di [ripristinare pagine e sottopagine (strutture ad albero pagina) in una versione precedente](/help/sites-cloud/authoring/sites-console/page-versions.md#reinstating-versions).

* Possibilità di [creare lanci](/help/sites-cloud/authoring/launches/overview.md) in AEM [SPA Editor](/help/implementing/developing/hybrid/introduction.md).


## as a Cloud Service [!DNL Adobe Experience Manager Assets] {#assets}

### Novità in [!DNL Assets] {#what-is-new-assets}

* La transcodifica video è ora supportata con i microservizi per le risorse. Una nuova sezione nella configurazione [!UICONTROL Profili elaborazione] consente di impostare la velocità in bit e le dimensioni del video. Il formato di output è MP4 con codec H.264. Per informazioni dettagliate, consulta [gestire le risorse video](/help/assets/manage-video-assets.md#transcode-video). Per ulteriori opzioni di transcodifica e per la distribuzione di video, utilizzare il componente aggiuntivo [!DNL Dynamic Media].

* Nelle nuove distribuzioni di [!DNL Experience Manager Assets], la funzionalità di assegnazione tag avanzati è ora configurata per impostazione predefinita. Non è necessario eseguire l&#39;integrazione manuale con [!DNL Adobe Developer Console]. Nelle implementazioni esistenti, gli amministratori configurano l’integrazione dei tag avanzati come prima.

* Una nuova esperienza di download di [risorse](/help/assets/download-assets-from-aem.md) consente,

   * Il download asincrono per i download di grandi dimensioni in modo che gli utenti non debbano attendere.
   * Una nuova API modulare per l’estensibilità degli sviluppatori.

* L’estrazione dei metadati per i microservizi per le risorse offre prestazioni migliorate. Aumenta la velocità effettiva di acquisizione complessiva delle risorse.

* Utilizza un profilo di elaborazione per generare metadati personalizzati utilizzando Compute Service. Vedi [Metadati personalizzati utilizzando il profilo di elaborazione](/help/assets/manage-metadata.md#metadata-compute-service).

* Esperienza di download più semplice per gli utenti di Brand Portal che gli amministratori possono configurare. Consulta [panoramica dell&#39;esperienza di download](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html#download-configurations).

* Le anteprime native e ad alta fedeltà dei documenti PDF sono ora disponibili in Brand Portal. Vedi [panoramica del visualizzatore di documenti](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html#doc-viewer).

* È ora possibile annullare la validità della rete CDN direttamente da [!DNL Dynamic Media] in AEM as a Cloud Service (anziché utilizzare [!DNL Dynamic Media Classic]). In questo modo le risorse più recenti vengono servite in pochi minuti anziché in alcune ore. Vedi [Annullamento della validità della CDN tramite Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md).

* Il supporto per l&#39;accesso facilitato è stato aggiunto ai controlli dell&#39;interfaccia utente, alla navigazione, alla navigazione e alla ricerca in [!DNL Assets].

   * Se si preme il tasto Esc dopo aver selezionato l&#39;opzione [!UICONTROL Aggiungi rappresentazione], viene visualizzata nuovamente la barra degli strumenti. <!-- via CQ-4293594-->
   * Lo stato attivo sulla tastiera funziona come previsto quando si utilizza la casella combinata E-mail. <!-- via CQ-4286215 -->
   * Gli elementi delle fisarmoniche nella sezione dei filtri di ricerca sono interpretati come fisarmoniche standard espandibili. <!-- via CQ-4273103 -->
   * Quando si applica un tag a una risorsa, i tag vengono visualizzati nella finestra di dialogo come elementi della struttura. Gli attributi ARIA vengono applicati in modo appropriato agli elementi dell’albero per renderli ora accessibili. <!-- via CQ-4272964 -->

* È ora disponibile la versione 2.0.3 di [!DNL AEM Desktop app]. Migliora la compatibilità con [!DNL Experience Manager] 6.5.5 Service Pack e dispone di un elenco aggiornato di compatibilità del sistema operativo client. [!DNL Windows] 7 e [!DNL macOS] versioni precedenti alla 10.14 non sono supportate.

### Bug corretti in [!DNL Assets] {#bugs-fixed}

* L’opzione Relate (Relate) e unrelated (Annulla relazione) non risponde quando si fa clic per la prima volta. (CQ-4299022)
* Quando si scarica una risorsa, se si seleziona l’opzione per riceverla tramite e-mail, l’e-mail non viene inviata. (CQ-4299146)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* È ora disponibile la funzione Console del prodotto. Questo consente agli esperti di marketing e agli autori in AEM di visualizzare e navigare tra le categorie e i prodotti memorizzati nel back-end per l’e-commerce. È inoltre disponibile il supporto per proprietà, categorie e prodotti nella console Prodotti.

* Sono stati migliorati i selettori di prodotti e categorie per consentire agli addetti al marketing di selezionare un prodotto tramite SKU o di selezionare una categoria tramite l’ID categoria.

## Cloud Manager {#cloud-manager}

### Data di pubblicazione {#release-date-cm}

La data di pubblicazione di [!UICONTROL Cloud Manager] versione 2020.8.0 è il 6 agosto 2020.

### Novità {#what-is-new-cloud-manager}

* Audit del contenuto è una funzione abilitata nelle pipeline di produzione di Cloud Manager Sites. Ora la configurazione della pipeline di produzione per i programmi con Sites include una terza scheda denominata **Audit del contenuto**. Ogni volta che viene eseguita una pipeline di produzione, nella pipeline viene incluso un nuovo passaggio di audit del contenuto dopo i test funzionali personalizzati, che valuta il sito in base a diverse dimensioni, tra cui prestazioni, SEO (Search Engine Optimization), accessibilità, best practice e PWA (app web progressiva).


  >[!NOTE]
  >Audit del contenuto è stato successivamente rinominato in Audit dell’esperienza.

  Per ulteriori informazioni, consulta [Test di audit dell’esperienza](/help/implementing/cloud-manager/reports/report-experience-audit.md).

* Ora gli ambienti creati di recente nei programmi Assets vengono configurati automaticamente con Smart Content Services.

* Gli ambienti sospesi possono essere riattivati dalla pagina **Panoramica** di Cloud Manager.

* La possibilità di eseguire controlli dell’esperienza sulle pagine è offerta da Google Lighthouse. Come parte della pipeline di Cloud Manager, è possibile controllare e convalidare fino a 25 pagine in base ai KPI dell’esperienza e visualizzare i punteggi nell’interfaccia utente di Cloud Manager.

### Correzioni di bug {#bug-fixes-cm}

* Alcuni plug-in di SonarQube superflui e indesiderati venivano eseguiti come parte del controllo di qualità del codice.

* Nella pagina di esecuzione della pipeline, il nome del ramo non era formattato correttamente.

* In alcuni casi, le esecuzioni completate della pipeline non venivano registrate correttamente come completate, impedendo in tal modo nuove esecuzioni.

* Talvolta le esecuzioni delle pipeline *si bloccavano* a causa di problemi di comunicazione interna.

* Al momento del provisioning di una nuova organizzazione, ad alcuni utenti con ruoli amministrativi diversi da Amministratore di sistema veniva erroneamente consentito l’accesso a Cloud Manager.

* In determinate condizioni, il processo di aggiornamento degli indici veniva avviato più volte in parallelo, causando un errore di distribuzione.

* Il suggerimento sulle schede del programma non era sempre corretto.

* L’interfaccia utente consentiva erroneamente di eseguire operazioni in un ambiente durante la sua eliminazione.

* Nella pagina **Panoramica** di Cloud Manager veniva riscontrata una mancata corrispondenza dei colori.

### Problemi noti {#known-issues-cm}

* Vengono incluse alcune pagine non valide che comportano l’abbassamento del punteggio medio dell’audit del contenuto rispetto al valore reale previsto.

* La scheda Audit del contenuto mostra erroneamente l’URL di base utilizzando il dominio di Author anziché di Publish.

* Per attivare il passaggio di audit del contenuto, gli utenti devono modificare la pipeline e, facoltativamente, aggiungere pagine. Se non si aggiunge alcuna pagina, viene sottoposta a audit la pagina Home.

## Strumento di trasferimento contenuti {#content-transfer-tool}

Leggi questa sezione per scoprire le novità e gli aggiornamenti della versione 1.0.4 dello strumento Content Transfer.

### Novità {#what-is-new-ctt}

* Lo strumento Content Transfer (Trasferimento contenuti) ora supporta il DataStore S3 condiviso.

### Correzioni di bug {#ctt-bug-fixes}

* Sono stati aggiunti timeout aggiuntivi per consentire allo strumento di completare le azioni.

* Talvolta nell’interfaccia utente della versione precedente veniva visualizzata un’estrazione riuscita, anche se il registro mostrava degli errori.

## Strumenti di refactoring del codice {#code-refactoring-tools}

Leggi questa sezione per scoprire le novità e gli aggiornamenti di Strumenti di refactoring del codice.

### Novità {#what-is-new-refactoring}

* Plug-in AIO-CLI rilasciato per unificare gli strumenti di refactoring del codice per consentire agli sviluppatori di richiamare ed eseguire strumenti di refactoring del codice da un’unica posizione. Per ulteriori dettagli, consulta [Risorsa Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration).

* AEM Dispatcher Converter esteso per supportare le conversioni delle configurazioni di Dispatcher Managed Services On-Premise e Adobe in configurazioni di Dispatcher compatibili con AEM as a Cloud Service. Per ulteriori dettagli, consulta [Risorsa Git: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter).

* AEM Dispatcher Converter riscritto in ` node.js ` e integrato con il plug-in AIO-CLI.
