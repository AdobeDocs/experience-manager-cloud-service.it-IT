---
title: Note sulla versione 2020.9.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: '"[!DNL Adobe Experience Manager] Note sulla versione as a Cloud Service per 2020.9.0."'
exl-id: 2332512f-8c52-4569-a006-faa36a7670a1
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 13%

---

# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 {#release-notes}

La sezione seguente illustra le note generali sulla versione di [!DNL Experience Manager] as a Cloud Service 2020.9.0.

## Data di pubblicazione {#release-date}

Data di rilascio per [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 è il 24 settembre 2020.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Novità in [!DNL Sites] {#what-is-new-sites}

* L’SDK JavaScript dell’editor di applicazioni a pagina singola (SPA) [è ora open source.](/help/implementing/developing/hybrid/reference-materials.md)

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### Novità in [!DNL Assets] {#what-is-new-assets}

* I file immagine con filigrana sono supportati per le rappresentazioni generate con i microservizi per le risorse. Può essere configurato come profilo di elaborazione e utilizza un file PNG come filigrana. Vedi [filigrana le risorse](/help/assets/watermark-assets.md).

* Miglioramenti apportati a [!DNL Dynamic Media]

   * Pubblicazione selettiva : è ora possibile accedere a un team di marketing [!DNL Dynamic Media] immagini di ritaglio avanzato e rappresentazioni dinamiche sincronizzate con [!DNL Dynamic Media] in modo che possano creare materiale promozionale, il tutto senza la necessità di pubblicare tali risorse in [!DNL Dynamic Media] per la distribuzione globale. [!DNL Experience Manager] e [!DNL Dynamic Media] la pubblicazione è disaccoppiata e può avvenire separatamente a questo scopo. Vedi [pubblicazione selettiva](/help/assets/dynamic-media/selective-publishing.md).
   * Gli amministratori ora possono reimpostare [!DNL Dynamic Media] Password di Cloud Service ricevuta al momento del provisioning. La reimpostazione può essere eseguita in [!DNL Experience Manager] interfaccia utente, senza la necessità di utilizzare [!DNL Dynamic Media Classic] app desktop.

* Per informazioni sui seguenti miglioramenti, consulta [Novità in Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html).

   * Anteprima PDF migliorata con l’integrazione Adobe Document Cloud View SDK.
   * Funzionalità di download con un solo clic.
   * Nuove configurazioni di amministrazione per l&#39;esperienza di download.

<!--
### Bugs Fixed {#bugs-fixed-assets}

TBD: list of Assets aaCS bugs that are fixed.
-->

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* Componenti core CIF rilasciati v1.3.0. Fai riferimento a [Componenti core CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.3.0) per ulteriori dettagli.

* È ora disponibile la funzionalità di anteprima con prodotti/categorie per i modelli di prodotto e categoria. Questo consente agli utenti aziendali o agli esperti di marketing di AEM di visualizzare i modelli di prodotto/categoria con dati reali.

* È stata aggiunta una pagina delle proprietà ai prodotti e alle categorie per consentire agli utenti aziendali di visualizzare i dettagli associati al codice SKU del prodotto/ID categoria.

* È stata aggiunta una funzione di ordinamento alla console Prodotti per consentire l’ordinamento di prodotti/categorie in base agli attributi di nome o prezzo.

* Funzionalità di ricerca dei prodotti aggiunte alla console Prodotti.

### Correzioni di bug {#bug-fixes-commerce}

* Le configurazioni di Commerce Cloud non rispettavano l’ereditarietà. È stato corretto per garantire che la configurazione erediti i valori.

## Cloud Manager {#cloud-manager}

### Data di pubblicazione {#release-date-cm}

Data di rilascio per [!UICONTROL Cloud Manager] La versione 2020.9.0 è il 3 settembre 2020.

### Novità {#what-is-new-cloud-manager}

* La funzione Verifica del contenuto è stata rinominata Audit esperienze.
* Il processo di creazione è stato separato in tre diversi comandi Maven.
* Se non è possibile clonare l’archivio Git, verranno eseguiti fino a tre tentativi.

### Correzioni di bug {#bug-fixes-cm}

* La scheda Verifica del contenuto mostrava erroneamente l’URL di base utilizzando il dominio autore invece del dominio di pubblicazione.

## Cloud Readiness Analyzer (Analisi di preparazione al cloud)  {#cloud-readiness-analyzer}

Leggi questa sezione per saperne di più sulle novità e sugli aggiornamenti di Cloud Readiness Analyzer v1.1.0.

### Novità {#what-is-new-cra}

* Cloud Readiness Analyzer (Analisi di preparazione al cloud) dispone di una console di stato iniziale che presenta un **Genera report** per consentire all’utente di fare clic su per eseguire l’analisi dei dati CRA.

* L’interfaccia utente CRA mostra l’avanzamento durante l’esecuzione. Mostra gli elementi in corso di analisi e i risultati rilevati durante l’esecuzione.

* Il rapporto CRA presenta un riepilogo e il numero dei risultati in un formato tabulare organizzato in base al tipo di risultato e al livello di importanza. Se fai clic sul numero di risultati, scorri automaticamente fino alla posizione del risultato nel rapporto.

### Correzioni di bug {#cra-bug-fixes}

* In alcuni casi, il rapporto CRA non veniva aggiornato dopo aver forzato un aggiornamento. Questo problema è stato risolto in questa versione.

## Strumento Trasferimento contenuti {#content-transfer-tool}

Leggi questa sezione per scoprire le novità e gli aggiornamenti della versione 1.1.10 dello strumento Content Transfer (Trasferimento contenuti).

### Novità {#what-is-new-ctt}

* Lo strumento Content Transfer (CTT) supporta Azure Blob Store Data Store.

* L’interfaccia utente CTT dispone di una funzione di ricaricamento automatico che ricarica la pagina della panoramica ogni 30 secondi.

* Pulsante aggiunto all’interfaccia utente CTT da recuperare *Token di accesso* facilmente.

* È stato aggiunto un messaggio di convalida descrittivo per *URL* e *Nome set di migrazione*.

## Strumenti di refactoring del codice {#code-refactoring}

Leggi questa sezione per scoprire le novità e gli aggiornamenti di Strumenti di refactoring del codice.

### Novità {#what-is-new-refactoring}

* Il plug-in AIO-CLI supporta Repository Modernizer e consente agli utenti di eseguire lo strumento utilizzando il plug-in.

   Fai riferimento a [Risorsa Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) per ulteriori dettagli.

* L’utility Repository Modernizer può essere utilizzata per ristrutturare i pacchetti di progetto esistenti in pacchetti compatibili con la struttura di progetto definita per AEM as a Cloud Service.

   Fai riferimento a [Risorsa Git: Modernizzatore dell&#39;archivio](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) per ulteriori dettagli.
