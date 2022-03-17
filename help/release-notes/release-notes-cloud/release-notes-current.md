---
title: Note sulla versione corrente per  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: c497424271ea960d22a30b4a6c66432935ec820d
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 84%

---


# Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione per la versione corrente (più recente) di [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Da qui puoi passare alle note sulla versione delle versioni precedenti; per esempio, quelle del 2020, 2021 e così via.

>[!NOTE]
>
>Consulta [Ultimi aggiornamenti della documentazione](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=it) per informazioni dettagliate sugli aggiornamenti della documentazione non direttamente correlati a una versione.

## Data di pubblicazione {#release-date}

La data di rilascio della versione corrente di [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] (2022.1.0) è il 3 febbraio 2022.
La versione seguente (2022.3.0) è del 31 marzo 2022.

## Video sulla versione {#release-video}

Dai un’occhiata al video [Panoramica sulla versione di gennaio 2022](https://video.tv.adobe.com/v/340120) per un riepilogo delle funzioni aggiunte alla versione 2022.1.0.

## Adobe Experience Manager Sites as a Cloud Service {#sites}

* Il pulsante **[Abilita pipeline front-end](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md)** è disponibile nella barra **Sito** della console Sites per i siti che utilizzano la v2 del componente core pagina. Questo pulsante configura il sito per caricare i temi distribuiti con la pipeline front-end sopra le librerie client esistenti.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

* [!DNL Dynamic Media] - È ora possibile utilizzare l’interfaccia Dynamic Media di AEM per configurare le impostazioni generali e le impostazioni di pubblicazione anziché passare attraverso l’applicazione desktop Dynamic Media Classic.

* [!DNL Dynamic Media] ora supporta l’acquisizione, l’anteprima, la riproduzione e la pubblicazione per i video MXF. L&#39;annotazione e il video acquistabile per i video MXF non sono ancora supportati.

* Dopo aver configurato una connessione tra le implementazioni remote di DAM e Sites, le risorse in DAM remoto sono rese disponibili nell’implementazione di Sites. È ora possibile [aggiornare, eliminare, rinominare e spostare le operazioni](/help/assets/use-assets-across-connected-assets-instances.md) sulle risorse o cartelle DAM remote. Gli aggiornamenti, con un certo ritardo, sono disponibili automaticamente nell’implementazione di Sites.

### Nuove funzioni nel canale prerelease [!DNL Assets] {#assets-prerelease-features}

* [!DNL AEM Dynamic Media] offre la flessibilità di [configurare un account alias](../../assets/dynamic-media/dm-alias-account.md) nell’interfaccia utente, garantendo in tal modo l’aggiornamento degli URL predefiniti di Dynamic Media e del codice di incorporamento del visualizzatore. Questo è particolarmente utile ai fini dell’ottimizzazione SEO (Search Engine Optimization), per riflettere eventuali aggiornamenti apportati al contesto aziendale, ad esempio in caso di rebranding.

* Ora puoi utilizzare l’interfaccia utente di [!DNL Experience Manager Assets] per:

   * Configura il rilevamento delle risorse duplicate in un archivio.

   * Configura l’aggiunta di watermark digitali alle immagini.

* Gli amministratori possono ora configurare il servizio e-mail per i download di grandi dimensioni. Consente agli utenti di [abilitare le notifiche e-mail per i download di grandi dimensioni](/help/assets/download-assets-from-aem.md#enable-email-notifications-for-large-downloads) dall’interfaccia [!DNL Experience Manager Assets]. Al termine del processo di download, l’utente riceve una notifica e-mail contenente il collegamento di download della cartella zip archiviata.


* La funzione [Gestisci pubblicazione](/help/assets/manage-publication.md) viene migliorata con un’interfaccia utente migliorata. Gli utenti possono pubblicare o annullare la pubblicazione dei contenuti da e verso la destinazione selezionata, [Aggiungi contenuto](/help/assets/manage-publication.md#add-content) all’elenco di pubblicazione dall’archivio DAM, [Includi impostazioni cartella](/help/assets/manage-publication.md#include-folder-settings) per pubblicare il contenuto delle cartelle selezionate e applicare i filtri, e [pianifica la pubblicazione](/help/assets/manage-publication.md#publish-assets-later) a una data o un’ora successiva.

### Correzioni di bug {#bug-fixes}

* Le risorse non elaborate senza rendering originale vengono inviate ad Asset Compute per l’elaborazione durante la migrazione delle risorse da AEM on-premise a Cloud Services.

## [!DNL Experience Manager Forms] come [!DNL Cloud Service] {#forms}

### Novità in [!DNL Forms] {#what-is-new-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [API di comunicazione](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html?lang=it) consente di combinare un modello e dati XML per generare documenti di stampa in vari formati. Il servizio consente di generare documenti in modalità sincrona e batch. Le API consentono di creare applicazioni che permettono di:

   * Generare i documenti compilando i file modello con dati XML.
   * Genera moduli in vari formati, compresi flussi di stampa PDF non interattivi.
   * Genera PDF di stampa da PDF modulo XFA.
   * Genera in blocco documenti PDF, PostScript, PCL e ZPL unendo più set di dati con modelli di origine.

* **Font personalizzati per documenti Record e PDF creati con API di comunicazione**: ora puoi utilizzare i font approvati dal marchio nei documenti PDF generati utilizzando le API di comunicazione per allinearli ai requisiti organizzativi.

### Nuove funzioni disponibili in [!DNL Forms] canale prerelease {#prerelease-features-forms}

* **[Assemblatore API](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/)**: Assemblatore API per combinare, ridisporre, integrare e ottenere informazioni sui documenti PDF.


## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* Componenti myAccount migliorati
* Il componente Consiglio di prodotto supporta ulteriori tipi di pagina (pagina home, carrello acquisti, conferma ordine)
* **Lista dei desideri**
   * I visitatori registrati possono aggiungere prodotti a una lista dei desideri
   * È possibile gestire la lista dei desideri e i prodotti contenuti tramite myAccount
   * Il pulsante “Aggiungi alla lista dei desideri” può essere abilitato/disabilitato a livello di componente tramite i criteri (ad esempio, teaser di prodotto, dettaglio di prodotto)
   * Disponibile come componente core e in AEM Venia Storefront

![Lista dei desideri](/help/assets/CIF/wishlist.png)

## Cloud Manager {#cloud-manager}

### Data di pubblicazione {#release-date-cm}

La data di pubblicazione di Cloud Manager in AEM as a Cloud Service 2022.01.0 è il 20 gennaio 2022. La prossima versione è prevista per il 10 febbraio 2022.

### Novità {#what-is-new-cm}

* Cloud Manager [evita di ricostruire la base di codice quando rileva che viene utilizzato lo stesso commit git](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) in più esecuzioni di pipeline full-stack.
* L’accesso al registro dell’ambiente AEM ora richiede il profilo di prodotto **Gestione distribuzione**. Gli utenti senza questo profilo visualizzeranno un pulsante disabilitato nell’interfaccia utente.
* L’interfaccia utente non consente la configurazione della pipeline front-end per un programma in cui Sites non è abilitato come soluzione.
* Al momento della generazione di una password git, verrà visualizzata la data di scadenza.

### Correzioni di bug {#bug-fixes-cm}

* Sono state corrette le eccezioni Null al puntatore rilevate da alcune distribuzioni di pipeline front-end.
* È ora possibile aggiungere, aggiornare ed eliminare variabili di ambiente quando un ambiente esegue una versione obsoleta di AEM.
* Il passaggio dell’immagine della build non verrà più contrassegnato come ERRORE per le pipeline che hanno utilizzato il passaggio pianificato in alcuni rari casi.
* Per i programmi con un solo archivio, nella schermata di esecuzione della pipeline viene ora visualizzato il nome dell’archivio.

## Strumento Trasferimento contenuti {#ctt-release}

### Data di pubblicazione {#release-date-ctt}

La data di pubblicazione dello strumento Trasferimento contenuti v1.8.6 è il 3 febbraio 2022.

### Novità {#what-is-new-ctt}

* Convalida del contenuto: gli utenti possono determinare in modo affidabile se tutti i contenuti estratti dallo strumento Trasferimento contenuti sono stati correttamente acquisiti nell’istanza di destinazione. Per utilizzare questa funzione, è necessario abilitarla nella `System Console` dell’ambiente AEM sorgente. Fai riferimento a [Guida introduttiva alla convalida dei trasferimenti di contenuto](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html?lang=it#getting-started) per ulteriori dettagli.

### Correzioni di bug {#bug-fixes-ctt}

* Alcuni utenti non venivano mappati perché la mappatura utente faceva distinzione tra maiuscole e minuscole. Questo problema è stato risolto. La mappatura utente non fa più distinzione tra maiuscole e minuscole.

## Analisi delle best practice {#bpa-release}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.26 è il 16 marzo 2022.

### Novità {#what-is-new-bpa}

* Possibilità di rilevare le risorse non elaborate. Se vengono rilevate risorse non elaborate, queste risorse devono essere impostate su elaborate o devono essere rimosse dal set di migrazione durante il trasferimento del contenuto per evitare problemi durante l’assimilazione del contenuto.
* Possibilità di rilevare se il contenuto ha più di 1000 URL personalizzati. L’utilizzo di un numero elevato di URL personalizzati non è una best practice in quanto carica un carico sui server Dispatcher e Publish .
* Possibilità di identificare i problemi relativi alle definizioni degli indici Oak e di rilevare le incompatibilità con AEM as a Cloud Service.
* Possibilità di rilevare e creare rapporti sull’utilizzo delle configurazioni di Externalizer. In AEM configurazioni as a Cloud Service di Externalizer sono impostate da Cloud Manager, pertanto le configurazioni esistenti di Externalizer devono essere reimpostate per mantenere la compatibilità.

### Correzioni di bug {#bug-fixes-bpa}

* In alcuni scenari, l&#39;esecuzione di BPA non è riuscita a causa di un errore di asserzione generato da FormsSelectiveFeaturesAnalysis. Questo problema è stato risolto.
* BPA riferiva i risultati relativi al modello WRK come PRINCIPALE invece che CRITICO. Questo problema è stato risolto.
* BPA segnalava erroneamente i risultati relativi alle definizioni dell&#39;indice OAK in ui.apps come CRITICAL. Questo problema è stato risolto
