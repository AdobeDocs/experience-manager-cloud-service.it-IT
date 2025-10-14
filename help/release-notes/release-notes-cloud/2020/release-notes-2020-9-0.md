---
title: Note sulla versione 2020.9.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: '[!DNL Adobe Experience Manager] note sulla versione 2020.9.0 di as a Cloud Service.'
exl-id: 2332512f-8c52-4569-a006-faa36a7670a1
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 14%

---

# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 {#release-notes}

La sezione seguente illustra le note generali sulla versione di [!DNL Experience Manager] as a Cloud Service 2020.9.0.

## Data di pubblicazione {#release-date}

La data di rilascio per [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 è il 24 settembre 2020.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Novità in [!DNL Sites] {#what-is-new-sites}

* L&#39;SDK di JavaScript per l&#39;editor di applicazioni a pagina singola (SPA) [&#x200B; è ora open source](/help/implementing/developing/hybrid/reference-materials.md).

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### Novità in [!DNL Assets] {#what-is-new-assets}

* La filigrana dei file immagine è supportata per le rappresentazioni generate con i microservizi per le risorse. Può essere configurato come profilo di elaborazione e utilizza un file PNG come filigrana. Consulta [applicare una filigrana alle risorse](/help/assets/watermark-assets.md).

* Miglioramenti in [!DNL Dynamic Media]

   * Publish selettivo: ora un team di marketing può accedere alle immagini con ritaglio avanzato [!DNL Dynamic Media] e alle rappresentazioni dinamiche sincronizzate con [!DNL Dynamic Media], in modo da creare materiali promozionali senza dover pubblicare tali risorse in [!DNL Dynamic Media] per la distribuzione globale. La pubblicazione di [!DNL Experience Manager] e [!DNL Dynamic Media] è scollegata e può avvenire separatamente. Vedi [pubblicazione selettiva](/help/assets/dynamic-media/selective-publishing.md).
   * Gli amministratori ora possono reimpostare la password di Cloud Service di [!DNL Dynamic Media] ricevuta al momento del provisioning. La reimpostazione può essere eseguita nell&#39;interfaccia utente di [!DNL Experience Manager], senza dover utilizzare l&#39;app desktop [!DNL Dynamic Media Classic].

* Per informazioni sui seguenti miglioramenti, vedere [Novità di Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=it).

   * Anteprima PDF avanzata con l’integrazione di Adobe Document Cloud View SDK.
   * Funzionalità di download con un solo clic.
   * Nuove configurazioni di amministrazione per l’esperienza di download.

<!--
### Bugs Fixed {#bugs-fixed-assets}

TBD: list of Assets aaCS bugs that are fixed.
-->

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* È stata rilasciata la versione 1.3.0 dei Componenti core CIF. Per ulteriori dettagli, consulta [Componenti core CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.3.0).

* È ora disponibile la funzionalità di anteprima con prodotti/categorie per i modelli di prodotto e categoria. Questo consente agli utenti aziendali e agli esperti di marketing dell’AEM di visualizzare i modelli di prodotto e categoria con dati reali.

* Ai prodotti e alle categorie sono state aggiunte delle proprietà di pagina per consentire agli utenti aziendali di visualizzare i dettagli associati all’ID di categoria o SKU del prodotto.

* È stata aggiunta una funzione di ordinamento alla console Prodotti che consente di ordinare i prodotti e le categorie in base agli attributi di nome o prezzo.

* Alla console Prodotti è stata aggiunta la funzionalità di ricerca dei prodotti.

### Correzioni di bug {#bug-fixes-commerce}

* Le configurazioni Commerce Cloud non rispettavano l’ereditarietà. Questo problema è stato risolto per garantire che la configurazione erediti i valori.

## Cloud Manager {#cloud-manager}

### Data di pubblicazione {#release-date-cm}

La data di pubblicazione di [!UICONTROL Cloud Manager] versione 2020.9.0 è il 3 settembre 2020.

### Novità {#what-is-new-cloud-manager}

* Audit del contenuto è stato rinominato in Audit dell’esperienza.
* Il processo di build è stato diviso in tre diversi comandi Maven.
* Se la clonazione dell’archivio Git genera errori, sono eseguiti fino a tre nuovi tentativi.

### Correzioni di bug {#bug-fixes-cm}

* La scheda Audit del contenuto mostrava erroneamente l’URL di base utilizzando il dominio di Author anziché di Publish.

## Cloud Readiness Analyzer {#cloud-readiness-analyzer}

Leggi questa sezione per scoprire le novità e gli aggiornamenti di Cloud Readiness Analyzer v1.1.0.

### Novità {#what-is-new-cra}

* Cloud Readiness Analyzer (Analisi di preparazione al cloud) dispone di una console di stato iniziale che visualizza un pulsante **Genera report** esplicito su cui l&#39;utente può fare clic per eseguire l&#39;analisi di preparazione al cloud.

* Durante l’esecuzione, l’interfaccia utente di Cloud Readiness Analyzer mostra lo stato di avanzamento. Vengono visualizzati gli elementi in fase di analisi e i risultati rilevati durante l&#39;esecuzione.

* Il rapporto di Cloud Readiness Analyzer presenta un riepilogo e il numero dei risultati sotto forma di tabella, organizzati in base al tipo di risultato e al livello di importanza. Facendo clic sul numero di quel risultato, si passa automaticamente alla posizione del risultato nel rapporto.

### Correzioni di bug {#cra-bug-fixes}

* In alcuni casi, il rapporto CRA non veniva aggiornato dopo l’aggiornamento forzato. Questo problema è stato risolto in questa versione.

## Strumento trasferimento contenuti {#content-transfer-tool}

Leggi questa sezione per scoprire le novità e gli aggiornamenti della versione 1.1.10 dello strumento Content Transfer.

### Novità {#what-is-new-ctt}

* Lo strumento Content Transfer supporta Azure Blob Store Data Store.

* L’interfaccia dello strumento Content Transfer dispone di una funzione di ricaricamento automatico che ricarica la pagina della panoramica ogni 30 secondi.

* Pulsante aggiunto all&#39;interfaccia utente CTT per recuperare facilmente *il token di accesso*.

* Messaggio di convalida descrittivo aggiunto per *URL* e *Nome set di migrazione*.

## Strumenti di refactoring del codice {#code-refactoring}

Leggi questa sezione per scoprire le novità e gli aggiornamenti di Strumenti di refactoring del codice.

### Novità {#what-is-new-refactoring}

* Il plug-in AIO-CLI supporta Repository Modernizer e consente agli utenti di eseguire lo strumento utilizzando il plug-in.

  Per ulteriori dettagli, consulta [Risorsa Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration).

* L’utility Repository Modernizer può essere utilizzata per ristrutturare i pacchetti di progetto esistenti in pacchetti compatibili con la struttura di progetto definita per AEM as a Cloud Service.

  Per ulteriori dettagli, vedi [Risorsa Git: Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).
