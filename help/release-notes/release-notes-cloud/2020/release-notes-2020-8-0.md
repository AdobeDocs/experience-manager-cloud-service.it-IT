---
title: Note sulla versione 2020.8.0 di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: "[!DNL Adobe Experience Manager] Note sulla versione 2020.8.0 as a Cloud Service."
exl-id: 83413130-ae90-4419-bcf7-42fdc740452b
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 34%

---

# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0 {#release-notes}

La sezione seguente illustra le note generali sulla versione di Experience Manager as a Cloud Service 2020.8.0.


## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Novità in [!DNL Sites] {#what-is-new-sites}

* Possibilità di [ripristinare pagine e sottopagine (strutture ad albero pagina) in una versione precedente](/help/sites-cloud/authoring/features/page-versions.md#reinstating-versions).

* Possibilità di [creare lanci](/help/sites-cloud/authoring/launches/overview.md) nell’AEM [Editor SPA.](/help/implementing/developing/hybrid/introduction.md)


## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### Novità in [!DNL Assets] {#what-is-new-assets}

* La transcodifica video è ora supportata con i microservizi per le risorse. Una nuova sezione nella sezione [!UICONTROL Profili elaborazione] consente di impostare la velocità in bit e le dimensioni del video. Il formato di output è MP4 con codec H.264. Per ulteriori informazioni, consulta [gestire le risorse video](/help/assets/manage-video-assets.md#transcode-video). Per ulteriori opzioni di transcodifica e per la distribuzione di video, utilizza [!DNL Dynamic Media] componente aggiuntivo.

* Su nuovo [!DNL Experience Manager Assets] implementazioni, la funzionalità di assegnazione tag avanzati è ora configurata per impostazione predefinita. Non è necessario eseguire l’integrazione manuale con [!DNL Adobe Developer Console]. Nelle implementazioni esistenti, gli amministratori configurano l’integrazione dei tag avanzati come prima.

* Una nuova [esperienza di download delle risorse](/help/assets/download-assets-from-aem.md) consente,

   * Download asincrono per download di grandi dimensioni in modo che gli utenti non debbano attendere.
   * Una nuova API modulare per l’estensibilità degli sviluppatori.

* L’estrazione dei metadati per i microservizi per le risorse offre prestazioni migliorate. Aumenta la velocità effettiva di acquisizione complessiva delle risorse.

* Utilizza un profilo di elaborazione per generare metadati personalizzati utilizzando Compute Service. Consulta [Metadati personalizzati tramite profilo di elaborazione](/help/assets/manage-metadata.md#metadata-compute-service).

* Esperienza di download più semplice per gli utenti di Brand Portal che gli amministratori possono configurare. Consulta [panoramica sul download dell’esperienza](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html#download-configurations).

* Le anteprime dei documenti PDF nativi e ad alta fedeltà sono ora disponibili in Brand Portal. Consulta [panoramica del visualizzatore documenti](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html#doc-viewer).

* Ora puoi annullare la validità della rete CDN direttamente da [!DNL Dynamic Media] nell’AEM as a Cloud Service (anziché utilizzare [!DNL Dynamic Media Classic]). In questo modo le risorse più recenti vengono servite in pochi minuti anziché in alcune ore. Consulta [Annullamento della validità della CDN tramite Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md).

* Il supporto per l’accesso facilitato è stato aggiunto ai controlli dell’interfaccia utente, all’esperienza di navigazione, di navigazione e di ricerca in [!DNL Assets].

   * Se si preme il tasto Esc dopo aver selezionato [!UICONTROL Aggiungi rappresentazione] , lo stato attivo ritorna sulla barra degli strumenti. <!-- via CQ-4293594-->
   * Lo stato attivo sulla tastiera funziona come previsto quando si utilizza la casella combinata E-mail. <!-- via CQ-4286215 -->
   * Gli elementi delle fisarmoniche nella sezione dei filtri di ricerca sono interpretati come fisarmoniche standard espandibili. <!-- via CQ-4273103 -->
   * Quando si applica un tag a una risorsa, i tag vengono visualizzati nella finestra di dialogo come elementi della struttura. Gli attributi ARIA vengono applicati in modo appropriato agli elementi dell’albero per renderli ora accessibili. <!-- via CQ-4272964 -->

* [!DNL AEM Desktop app] È ora disponibile la versione 2.0.3 di. La compatibilità con [!DNL Experience Manager] 6.5.5 Service Pack e dispone di un elenco aggiornato di compatibilità del sistema operativo client. [!DNL Windows] 7 e [!DNL macOS] non sono supportate le versioni precedenti alla 10.14.

### Bug corretti in [!DNL Assets] {#bugs-fixed}

* L’opzione Relate (Relate) e unrelated (Annulla relazione) non risponde quando si fa clic per la prima volta. (CQ-4299022)
* Quando si scarica una risorsa, se si seleziona l’opzione per riceverla tramite e-mail, l’e-mail non viene inviata. (CQ-4299146)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* È ora disponibile la funzione Console del prodotto. Questo consente agli esperti di marketing/autori in AEM di visualizzare e navigare tra le categorie e i prodotti memorizzati nel back-end per l’e-commerce. È inoltre disponibile il supporto per proprietà, categorie e prodotti nella console Prodotti.

* Sono stati migliorati i selettori di prodotti e categorie per consentire agli addetti al marketing di selezionare un prodotto tramite SKU o di selezionare una categoria tramite l’ID categoria.

## Cloud Manager {#cloud-manager}

### Data di pubblicazione {#release-date-cm}

La data di rilascio per [!UICONTROL Cloud Manager] La versione 2020.8.0 di è del 6 agosto 2020.

### Novità {#what-is-new-cloud-manager}

* Audit del contenuto è una funzione abilitata nelle pipeline di produzione di Cloud Manager Sites. Ora la configurazione della pipeline di produzione per i programmi con Sites include una terza scheda denominata **Audit del contenuto**. Ogni volta che viene eseguita una pipeline di produzione, nella pipeline viene incluso un nuovo passaggio di audit del contenuto dopo i test funzionali personalizzati, che valuta il sito in base a una serie di dimensioni, tra cui prestazioni, SEO (Search Engine Optimization), accessibilità, best practice e PWA (app web progressiva).


  >[!NOTE]
  >Audit del contenuto è stato successivamente rinominato in Audit dell’esperienza.

  Per ulteriori informazioni, consulta [Test di audit dell’esperienza](/help/implementing/cloud-manager/experience-audit-testing.md).

* Ora gli ambienti creati di recente nei programmi Assets vengono configurati automaticamente con Smart Content Service.

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

* Per attivare il passaggio Audit del contenuto, gli utenti devono modificare la pipeline e, facoltativamente, aggiungere pagine. Se non viene aggiunta alcuna pagina, la pagina home viene sottoposta a controllo.

## Strumento trasferimento contenuti {#content-transfer-tool}

Leggi questa sezione per scoprire le novità e gli aggiornamenti della versione 1.0.4 dello strumento Content Transfer.

### Novità {#what-is-new-ctt}

* Lo strumento Content Transfer (Trasferimento contenuti) ora supporta il DataStore S3 condiviso.

### Correzioni di bug {#ctt-bug-fixes}

* Sono stati aggiunti timeout aggiuntivi per consentire allo strumento di completare le azioni.

* Talvolta nell’interfaccia utente della versione precedente veniva visualizzata un’estrazione riuscita, anche se il registro mostrava degli errori.

## Strumenti di refactoring del codice {#code-refactoring-tools}

Leggi questa sezione per scoprire le novità e gli aggiornamenti di Strumenti di refactoring del codice.

### Novità {#what-is-new-refactoring}

* Plug-in AIO-CLI rilasciato per unificare gli strumenti di refactoring del codice per consentire agli sviluppatori di richiamare ed eseguire strumenti di refactoring del codice da un’unica posizione. Fai riferimento a [Risorsa Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) per ulteriori dettagli.

* Il convertitore del Dispatcher AEM è stato esteso per supportare le conversioni delle configurazioni del Dispatcher Managed Services On-Premise e di Adobe in configurazioni del Dispatcher compatibili con AEM as a Cloud Service. Fai riferimento a [Risorsa Git: AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) per ulteriori dettagli.

* AEM Dispatcher Converter riscritto in ` node.js ` e integrato con il plug-in AIO-CLI.
