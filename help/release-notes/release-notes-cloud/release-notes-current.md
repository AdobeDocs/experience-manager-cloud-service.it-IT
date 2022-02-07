---
title: Note sulla versione corrente per  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Note sulla versione corrente per [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 5731337ff0edf5825860e6f76ed919b90402d88b
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 32%

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

Data di rilascio di [!DNL Adobe Experience Manager] come [!DNL Cloud Service] la versione corrente (2022.1.0) è il 3 febbraio 2022.
La seguente versione (2022.2.0) è del 24 febbraio 2022.

## Video sulla versione {#release-video}

Dai un&#39;occhiata al [Panoramica sulla versione di gennaio 2022](https://video.tv.adobe.com/v/340120) video per un riepilogo delle funzioni aggiunte nella versione 2022.1.0.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuove funzioni in [!DNL Assets] {#assets-features}

* [!DNL Dynamic Media] - È ora possibile utilizzare l’interfaccia Dynamic Media di AEM per configurare le impostazioni generali e le impostazioni di pubblicazione anziché passare attraverso l’applicazione desktop Dynamic Media Classic.

* [!DNL Dynamic Media] ora supporta l’acquisizione, l’anteprima, la riproduzione e la pubblicazione per i video MXF. L&#39;annotazione e il video acquistabile per i video MXF non sono ancora supportati.

* Dopo aver configurato una connessione tra le implementazioni remote di DAM e Sites, le risorse in DAM remoto sono rese disponibili nell’implementazione di Sites. È ora possibile [aggiornare, eliminare, rinominare e spostare le operazioni](/help/assets/use-assets-across-connected-assets-instances.md) sulle risorse o cartelle DAM remote. Gli aggiornamenti, con un certo ritardo, sono disponibili automaticamente nell’implementazione di Sites.

### Nuove funzioni nel [!DNL Assets] canale prerelease {#assets-prerelease-features}

* [!DNL AEM Dynamic Media] offre la flessibilità di [configura un account alias](../../assets/dynamic-media/dm-alias-account.md) nell’interfaccia utente di , garantendo in tal modo l’aggiornamento degli URL predefiniti di Dynamic Media e del codice di incorporamento del visualizzatore. Questo influisce positivamente sull’ottimizzazione SEO (Search Engine Optimization), per riflettere gli aggiornamenti apportati al contesto aziendale, ad esempio il rebranding.

* Ora puoi utilizzare la [!DNL Experience Manager Assets] interfaccia utente a:

   * Configura il rilevamento delle risorse duplicate in un archivio.

   * Configura l’aggiunta di watermark digitali alle immagini.

* Gli amministratori possono ora configurare il servizio e-mail per i download di grandi dimensioni. Consente agli utenti di [abilitare le notifiche e-mail per i download di grandi dimensioni](/help/assets/download-assets-from-aem.md#enable-email-notifications-for-large-downloads) dal [!DNL Experience Manager Assets] interfaccia. Al termine del processo di download, l’utente riceve una notifica e-mail contenente il collegamento di download della cartella zip archiviata.


* La [Gestisci pubblicazione](/help/assets/manage-publication.md) viene migliorata con un’interfaccia utente migliorata. Gli utenti possono pubblicare o annullare la pubblicazione dei contenuti da e verso la destinazione selezionata, [Aggiungi contenuto](/help/assets/manage-publication.md#add-content) all’elenco di pubblicazione dall’archivio DAM, [Includi impostazioni cartella](/help/assets/manage-publication.md#include-folder-settings) per pubblicare il contenuto delle cartelle selezionate e applicare i filtri, e [pianificazione della pubblicazione](/help/assets/manage-publication.md#publish-assets-later) a una data o un&#39;ora successiva.

### Correzioni di bug {#bug-fixes}

* Le risorse non elaborate senza rendering originale vengono inviate ad Asset compute per l’elaborazione durante la migrazione delle risorse da AEM on-premise a Cloud Services.

## [!DNL Experience Manager Forms] come [!DNL Cloud Service] {#forms}

### Novità in [!DNL Forms] {#what-is-new-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [API di comunicazione](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html?lang=it) consente di combinare un modello e dati XML per generare documenti di stampa in vari formati. Il servizio consente di generare documenti in modalità sincrona e batch. Le API consentono di creare applicazioni che permettono di:

   * Genera i documenti compilando i file modello con dati XML.
   * Generare moduli di in vari formati, compresi flussi di stampa PDF non interattivi.
   * Genera PDF di stampa da PDF modulo XFA.
   * Generare in blocco documenti PDF, PostScript, PCL e ZPL unendo più set di dati con modelli di origine.

* **Font personalizzati per documenti Record e PDF creati con API di comunicazione**: è ora possibile utilizzare font approvati dal marchio nei documenti PDF generati utilizzando le API di comunicazione per allinearli ai requisiti organizzativi.

### Nuove funzioni disponibili in [!DNL Forms] canale prerelease {#prerelease-features-forms}

* **[API Assembler](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/)**: API Assembler per combinare, ridisporre, integrare e ottenere informazioni sui documenti PDF.


## Componente aggiuntivo CIF {#cloud-services-cif}

### Novità {#what-is-new-cif}

* Componenti myAccount migliorati
* Il componente Product Recommendation supporta ulteriori tipi di pagina (home page, carrello acquisti, conferma ordine)
* **Lista dei desideri**
   * I visitatori registrati possono aggiungere prodotti a una lista dei desideri
   * La gestione della wishlist e dei suoi prodotti è possibile tramite myAccount
   * Il pulsante &quot;Aggiungi alla wishlist&quot; può essere abilitato/disabilitato a livello di componente tramite i criteri (ad esempio, product teaser, product detail)
   * Disponibile come componente core e nella AEM Venia Storefront

![Lista dei desideri](/help/assets/CIF/wishlist.png)

## Cloud Manager {#cloud-manager}

### Data di pubblicazione {#release-date-cm}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2022.01.0 è il 20 gennaio 2022. La prossima versione è prevista per il 10 febbraio 2022.

### Novità {#what-is-new-cm}

* Cloud Manager [evita di ricostruire la base di codice quando rileva che viene utilizzato lo stesso commit git](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) in più esecuzioni di pipeline full-stack.
* L&#39;accesso al registro dell&#39;ambiente AEM ora richiede **Gestione distribuzione** profilo di prodotto. Gli utenti senza questo profilo visualizzeranno un pulsante disabilitato nell’interfaccia utente.
* L’interfaccia utente non consente la configurazione della pipeline front-end per un programma in cui Sites non è abilitato come soluzione.
* Al momento della generazione di una password git, verrà visualizzata la data di scadenza.

### Correzioni di bug {#bug-fixes-cm}

* Sono state corrette le eccezioni Null al puntatore rilevate da alcune distribuzioni di pipeline front-end.
* È ora possibile aggiungere, aggiornare ed eliminare variabili di ambiente quando un ambiente esegue una versione obsoleta di AEM.
* Il passaggio dell’immagine della build non verrà più contrassegnato come ERRORE per le pipeline che hanno utilizzato il passaggio pianificato in alcuni rari casi.
* Per i programmi con un solo archivio, nella schermata di esecuzione della pipeline viene ora visualizzato il nome dell’archivio.

## Strumento Content Transfer (Trasferimento contenuti)  {#ctt-release}

### Data di pubblicazione {#release-date-ctt}

La data di rilascio dello strumento Content Transfer (Trasferimento contenuti) v1.8.6 è il 3 febbraio 2022.

### Novità {#what-is-new-ctt}

* Convalida del contenuto : gli utenti possono determinare in modo affidabile se tutti i contenuti estratti dallo strumento Content Transfer (Trasferimento contenuti) sono stati correttamente acquisiti nell’istanza di destinazione. Per utilizzare questa funzione, è necessario abilitarla nella `System Console` dell&#39;ambiente AEM sorgente. Fai riferimento a [Convalida dei trasferimenti di contenuto - Guida introduttiva](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html?lang=en#getting-started) per ulteriori dettagli.

### Correzioni di bug {#bug-fixes-ctt}

* Alcuni utenti non sono stati mappati perché la mappatura utente faceva distinzione tra maiuscole e minuscole. Questo problema è stato risolto. La mappatura utente non fa più distinzione tra maiuscole e minuscole.

## Analisi delle best practice {#bpa-release}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.24 è il 10 febbraio 2022.

### Novità {#what-is-new-bpa}

* Possibilità di rilevare e segnalare il numero di risorse con e senza tag avanzati.
* Possibilità di rilevare e creare rapporti sulla versione del componente core utilizzato.
* Possibilità di rilevare e creare rapporti sul tipo di livello di origine (Autore o Pubblicazione) in cui è stato eseguito BPA.

### Correzioni di bug {#bug-fixes-bpa}

* La logica di dimensionamento BPA è stata resa più rapida ed efficiente.
* In alcuni scenari, BPA non incrementa il conteggio analizzato al momento dell&#39;esecuzione. Questo problema è stato risolto.
