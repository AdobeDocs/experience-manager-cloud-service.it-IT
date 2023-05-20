---
title: Note sulla versione 2020.9.0 di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: "[!DNL Adobe Experience Manager] Note sulla versione 2020.9.0 as a Cloud Service."
exl-id: 2332512f-8c52-4569-a006-faa36a7670a1
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 21%

---

# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 {#release-notes}

La sezione seguente illustra le note generali sulla versione di [!DNL Experience Manager] as a Cloud Service 2020.9.0.

## Data di pubblicazione {#release-date}

La data di rilascio per [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 è il 24 settembre 2020.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Novità in [!DNL Sites] {#what-is-new-sites}

* L’SDK JavaScript dell’editor di applicazioni a pagina singola (SPA) [è ora open source.](/help/implementing/developing/hybrid/reference-materials.md)

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### Novità in [!DNL Assets] {#what-is-new-assets}

* La filigrana dei file immagine è supportata per le rappresentazioni generate con i microservizi per le risorse. Può essere configurato come profilo di elaborazione e utilizza un file PNG come filigrana. Consulta [applicare una filigrana alle risorse](/help/assets/watermark-assets.md).

* Miglioramenti in [!DNL Dynamic Media]

   * Pubblicazione selettiva: ora un team di marketing può accedere [!DNL Dynamic Media] ritaglio avanzato delle immagini e delle rappresentazioni dinamiche sincronizzate con [!DNL Dynamic Media] in modo che possano creare materiali promozionali, senza dover pubblicare tali risorse su [!DNL Dynamic Media] per la distribuzione globale. [!DNL Experience Manager] e [!DNL Dynamic Media] la pubblicazione è scollegata e può avvenire separatamente. Consulta [pubblicazione selettiva](/help/assets/dynamic-media/selective-publishing.md).
   * Gli amministratori possono ora reimpostare [!DNL Dynamic Media] Password di Cloud Service ricevuta al momento del provisioning. Il ripristino può essere eseguito in [!DNL Experience Manager] senza dover utilizzare l&#39;interfaccia utente di [!DNL Dynamic Media Classic] app desktop.

* Per informazioni sui seguenti miglioramenti, consulta [novità di Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=it).

   * Anteprima PDF avanzata con l’integrazione di Adobe Document Cloud View SDK.
   * Funzionalità di download con un solo clic.
   * Nuove configurazioni di amministrazione per l’esperienza di download.

<!--
### Bugs Fixed {#bugs-fixed-assets}

TBD: list of Assets aaCS bugs that are fixed.
-->

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* È stata rilasciata la versione 1.3.0 dei componenti core CIF. Fai riferimento a [Componenti core CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.3.0) per ulteriori dettagli.

* È ora disponibile la funzionalità di anteprima con prodotti/categorie per i modelli di prodotto e categoria. Questo consente agli utenti aziendali e agli esperti di marketing dell’AEM di visualizzare i modelli di prodotto e categoria con dati reali.

* Ai prodotti e alle categorie sono state aggiunte delle proprietà di pagina per consentire agli utenti aziendali di visualizzare i dettagli associati all’ID di categoria o SKU del prodotto.

* È stata aggiunta una funzione di ordinamento alla console Prodotti che consente di ordinare i prodotti e le categorie in base agli attributi di nome o prezzo.

* Alla console Prodotti è stata aggiunta la funzionalità di ricerca dei prodotti.

### Correzioni di bug {#bug-fixes-commerce}

* Le configurazioni Commerce Cloud non rispettavano l’ereditarietà. Questo problema è stato risolto per garantire che la configurazione erediti i valori.

## Cloud Manager {#cloud-manager}

### Data di pubblicazione {#release-date-cm}

La data di rilascio per [!UICONTROL Cloud Manager] La versione 2020.9.0 di è il 3 settembre 2020.

### Novità {#what-is-new-cloud-manager}

* Audit del contenuto è stato rinominato in Audit dell’esperienza.
* Il processo di build è stato diviso in tre diversi comandi Maven.
* Se la clonazione dell’archivio Git genera errori, verranno eseguiti fino a tre nuovi tentativi.

### Correzioni di bug {#bug-fixes-cm}

* La scheda Audit del contenuto mostrava erroneamente l’URL di base utilizzando il dominio di Author anziché di Publish.

## Cloud Readiness Analyzer (Analisi di preparazione al cloud)  {#cloud-readiness-analyzer}

Leggi questa sezione per saperne di più sulle novità e sugli aggiornamenti di Cloud Readiness Analyzer v1.1.0.

### Novità {#what-is-new-cra}

* Cloud Readiness Analyzer (Analisi di preparazione al cloud) dispone di una console di stato iniziale che presenta un’intestazione **Genera report** per consentire all’utente di fare clic per eseguire lo strumento CRA.

* Durante l’esecuzione dell’interfaccia di Cloud Readiness Analyzer, viene visualizzato lo stato di avanzamento. Vengono visualizzati gli elementi in fase di analisi e i risultati rilevati durante l&#39;esecuzione.

* Il rapporto di Cloud Readiness Analyzer presenta un riepilogo e il numero dei risultati sotto forma di tabella, organizzati in base al tipo di risultato e al livello di importanza. Facendo clic sul numero di quel risultato, si passa automaticamente alla posizione del risultato nel rapporto.

### Correzioni di bug {#cra-bug-fixes}

* In alcuni casi, il rapporto CRA non veniva aggiornato dopo l’aggiornamento forzato. Questo problema è stato risolto in questa versione.

## Strumento trasferimento contenuti {#content-transfer-tool}

Leggi questa sezione per scoprire le novità e gli aggiornamenti della versione 1.1.10 dello strumento Content Transfer.

### Novità {#what-is-new-ctt}

* Lo strumento Content Transfer supporta Azure Blob Store Data Store.

* L’interfaccia dello strumento Content Transfer dispone di una funzione di ricaricamento automatico che ricarica la pagina della panoramica ogni 30 secondi.

* Pulsante aggiunto all&#39;interfaccia utente CTT per il recupero *Token di accesso* facilmente.

* Messaggio di convalida descrittivo aggiunto per *URL* e *Nome set di migrazione*.

## Strumenti di refactoring del codice {#code-refactoring}

Leggi questa sezione per scoprire le novità e gli aggiornamenti di Strumenti di refactoring del codice.

### Novità {#what-is-new-refactoring}

* Il plug-in AIO-CLI supporta Repository Modernizer e consente agli utenti di eseguire lo strumento utilizzando il plug-in.

   Fai riferimento a [Risorsa Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) per ulteriori dettagli.

* L’utility Repository Modernizer può essere utilizzata per ristrutturare i pacchetti di progetto esistenti in pacchetti compatibili con la struttura di progetto definita per AEM as a Cloud Service.

   Fai riferimento a [Risorsa Git: Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) per ulteriori dettagli.
