---
title: Note sulla versione 2020.9.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: '[!DNL Adobe Experience Manager] come Cloud Service - Note sulla versione 2020.9.0.'
translation-type: tm+mt
source-git-commit: 701d9ff3c9553c28bce0ef417487facedb22373f
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 11%

---


# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 {#release-notes}

La sezione seguente illustra le note generali sulla versione relative a [!DNL Experience Manager] come Cloud Service 2020.9.0.

## Data di rilascio {#release-date}

La data di rilascio per [!DNL Adobe Experience Manager] come Cloud Service 2020.9.0 è il 24 settembre 2020.

## [!DNL Adobe Experience Manager Sites] come Cloud Service  {#sites}

### Novità in [!DNL Sites] {#what-is-new-sites}

* L&#39;SDK JavaScript per l&#39;applicazione di pagina singola (SPA) Editor [ora è open source.](/help/implementing/developing/hybrid/reference-materials.md)

## [!DNL Adobe Experience Manager Assets] come Cloud Service  {#assets}

### Novità in [!DNL Assets] {#what-is-new-assets}

* I file immagine con filigrana sono supportati per le rappresentazioni generate con i microservizi delle risorse. Può essere configurato come profilo di elaborazione e utilizza un file PNG come filigrana. Consultate [filigrana delle risorse](/help/assets/watermark-assets.md).

* Miglioramenti in [!DNL Dynamic Media]

   * Pubblicazione selettiva - È ora possibile per un team di marketing accedere alle [!DNL Dynamic Media] immagini di ritaglio avanzato e alle rappresentazioni dinamiche sincronizzate con [!DNL Dynamic Media] in modo che possano creare materiali promozionali, il tutto senza dover pubblicare tali risorse su [!DNL Dynamic Media] per la distribuzione globale. [!DNL Experience Manager] e la  [!DNL Dynamic Media] pubblicazione viene disaccoppiata e può avvenire separatamente a questo scopo. Consultate [pubblicazione selettiva](/help/assets/dynamic-media/selective-publishing.md).
   * Adesso, gli amministratori possono ripristinare la password di Cloud Service [!DNL Dynamic Media] ricevuta al momento del provisioning. La reimpostazione può essere eseguita nell&#39;interfaccia utente [!DNL Experience Manager], senza la necessità di utilizzare l&#39;app desktop [!DNL Dynamic Media Classic].

* Per informazioni sui seguenti miglioramenti, consultate [novità in Brand Portal](https://docs.adobe.com/content/help/it-IT/experience-manager-brand-portal/using/introduction/whats-new.html).

   * Anteprima PDF avanzata con integrazione con Adobe Document Cloud View SDK.
   * Funzionalità di download con un solo clic.
   * Nuove configurazioni di amministrazione per l&#39;esperienza di download.

<!--
### Bugs Fixed {#bugs-fixed-assets}

TBD: list of Assets aaCS bugs that are fixed.
-->

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* Componenti CIF di base rilasciati v1.3.0. Per ulteriori informazioni, consultare [CIF Core Components](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.3.0).

* È ora disponibile la funzionalità di anteprima con prodotti/categorie per i modelli di prodotto e categoria. Questo consente agli utenti aziendali o agli esperti di marketing di AEM di visualizzare i modelli di prodotto/categoria con dati reali.

* Pagina delle proprietà aggiunta a prodotti e categorie per consentire agli utenti aziendali di visualizzare i dettagli associati all’ID SKU/categoria del prodotto.

* Funzione di ordinamento aggiunta alla console prodotto per consentire l’ordinamento di prodotti/categorie in base al nome o agli attributi di prezzo.

* Funzionalità di ricerca prodotti aggiunta alla console prodotto.

### Correzioni di bug {#bug-fixes-commerce}

* Le configurazioni di Commerce Cloud non rispettavano l&#39;ereditarietà. È stato corretto per garantire che la configurazione erediti i valori.

## Cloud Manager {#cloud-manager}

### Data di rilascio {#release-date-cm}

La data di rilascio per [!UICONTROL Cloud Manager] Versione 2020.9.0 è il 3 settembre 2020.

### Novità {#what-is-new-cloud-manager}

* Content Audit è stato ribattezzato come Experience Audit (Audit esperienza).
* Il processo di costruzione è stato separato in tre diversi comandi Maven.
* Se il repository Git non viene clonato, verrà ripetuto fino a tre volte.

### Correzioni di bug {#bug-fixes-cm}

* La scheda Controllo contenuto visualizzava erroneamente l’URL di base utilizzando il dominio di creazione invece del dominio di pubblicazione.

## Cloud Readiness Analyzer (Analisi di preparazione al cloud) {#cloud-readiness-analyzer}

Leggi questa sezione per saperne di più sulle novità e sugli aggiornamenti di Cloud Readiness Analyzer v1.1.0.

### Novità {#what-is-new-cra}

* La console CRA (Cloud Readiness Analyzer) dispone di una console di stato iniziale che mostra un pulsante esplicito **Genera report** su cui l&#39;utente può fare clic per eseguire la CRA.

* L&#39;interfaccia utente CRA visualizza l&#39;avanzamento durante l&#39;esecuzione. Vengono visualizzati gli elementi analizzati e i risultati rilevati durante l&#39;esecuzione.

* Il rapporto CRA presenta un riepilogo e il numero dei risultati in un formato tabulare organizzato in base al tipo di ricerca e al livello di importanza. Facendo clic sul numero di risultati, si passa automaticamente alla posizione di tale ricerca nel rapporto.

### Correzioni di bug {#cra-bug-fixes}

* In alcuni casi, il rapporto CRA non veniva aggiornato dopo aver forzato un aggiornamento. Questo problema è stato risolto in questa versione.

## Strumento Content Transfer (Trasferimento contenuti) {#content-transfer-tool}

Seguite questa sezione per saperne di più sulle novità e sugli aggiornamenti di Content Transfer Tool Release v1.1.10.

### Novità {#what-is-new-ctt}

* Il Content Transfer Tool (CTT) supporta l&#39;archivio dati di Azure Blob Store.

* L&#39;interfaccia utente CTT dispone di una funzione di ricarica automatica che ricarica la pagina della panoramica ogni 30 secondi.

* Pulsante aggiunto all&#39;interfaccia utente CTT per recuperare facilmente *Token di accesso*.

* Messaggio di convalida descrittivo aggiunto per *URL* e *Nome set di migrazione*.

## Strumenti di refactoring del codice {#code-refactoring}

Segui questa sezione per saperne di più sulle novità e gli aggiornamenti per gli strumenti di refactoring del codice.

### Novità {#what-is-new-refactoring}

* Il plug-in AIO-CLI supporta Repository Modernizer e consente agli utenti di eseguire lo strumento utilizzando il plugin.

   Fare riferimento a [Risorse Git: aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) per ulteriori dettagli.

* L&#39;utility Repository Modernizer può essere utilizzata per ristrutturare i pacchetti di progetto esistenti in pacchetti compatibili con la struttura di progetto definita per AEM come Cloud Service.

   Fare riferimento a [Risorse Git: Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) per ulteriori dettagli.

