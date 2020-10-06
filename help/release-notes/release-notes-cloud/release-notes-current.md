---
title: Note sulla versione 2020.9.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: '[!DNL Adobe Experience Manager] as a Cloud Service: note sulla versione 2020.9.0.'
translation-type: tm+mt
source-git-commit: 5fb87f82c092552aa5e1c4b569399ec0bbc0da3b
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 12%

---


# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 {#release-notes}

The following section outlines the general Release Notes for [!DNL Experience Manager] as a Cloud Service 2020.9.0.

## Data di rilascio {#release-date}

The Release Date for [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 is September 24, 2020.

## [!DNL Adobe Experience Manager Sites] come Cloud Service {#sites}

### What is new in [!DNL Sites] {#what-is-new-sites}

* L’SDK JavaScript per l’editor di applicazioni a pagina singola (SPA) [è ora open source.](/help/implementing/developing/spa/reference-materials.md)

## [!DNL Adobe Experience Manager Assets] come Cloud Service {#assets}

### What is new in [!DNL Assets] {#what-is-new-assets}

* I file immagine con filigrana sono supportati per le rappresentazioni generate con i microservizi delle risorse. Può essere configurato come profilo di elaborazione e utilizza un file PNG come filigrana. Consultate [Filigrana delle risorse](/help/assets/watermark-assets.md).

* Miglioramenti in [!DNL Dynamic Media]

   * Pubblicazione selettiva - È ora possibile per un team di marketing accedere a immagini di ritaglio [!DNL Dynamic Media] smart e rappresentazioni dinamiche sincronizzate per [!DNL Dynamic Media] creare materiali promozionali, il tutto senza dover pubblicare tali risorse [!DNL Dynamic Media] per la distribuzione globale. [!DNL Experience Manager] e la [!DNL Dynamic Media] pubblicazione viene disaccoppiata e può avvenire separatamente per ottenere questo risultato. Consultate Pubblicazione [](/help/assets/dynamic-media/selective-publishing.md)selettiva.
   * Adesso, gli amministratori possono ripristinare la password [!DNL Dynamic Media] del Cloud Service ricevuta al momento del provisioning. Il ripristino può essere eseguito nell&#39;interfaccia [!DNL Experience Manager] utente, senza la necessità di utilizzare l&#39;app [!DNL Dynamic Media Classic] desktop.

* Per informazioni sui seguenti miglioramenti, consulta [le novità di Brand Portal](https://docs.adobe.com/content/help/it-IT/experience-manager-brand-portal/using/introduction/whats-new.html).

   * Anteprima PDF avanzata con integrazione con Adobe Document Cloud View SDK.
   * Funzionalità di download con un solo clic.
   * Nuove configurazioni di amministrazione per l&#39;esperienza di download.

<!--
### Bugs Fixed {#bugs-fixed-assets}

TBD: list of Assets aaCS bugs that are fixed.
-->

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* Componenti CIF di base rilasciati v1.3.0. Per ulteriori informazioni, consulta Componenti [di base](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.3.0) CIF.

* È ora disponibile la funzionalità di anteprima con prodotti/categorie per i modelli di prodotto e categoria. Questo consente agli utenti aziendali o agli esperti di marketing di AEM di visualizzare i modelli di prodotto/categoria con dati reali.

* Pagina delle proprietà aggiunta a prodotti e categorie per consentire agli utenti aziendali di visualizzare i dettagli associati all’ID SKU/categoria del prodotto.

* Funzione di ordinamento aggiunta alla console prodotto per consentire l’ordinamento di prodotti/categorie in base al nome o agli attributi di prezzo.

* Funzionalità di ricerca prodotti aggiunta alla console prodotto.

### Correzioni di bug {#bug-fixes-commerce}

* Le configurazioni di Commerce Cloud non rispettavano l&#39;ereditarietà. È stato corretto per garantire che la configurazione erediti i valori.

## Cloud Manager {#cloud-manager}

### Data di rilascio {#release-date-cm}

The Release Date for [!UICONTROL Cloud Manager] Version 2020.9.0 is September 03, 2020.

### Novità {#what-is-new-cloud-manager}

* Content Audit è stato ribattezzato come Experience Audit (Audit esperienza).
* Il processo di costruzione è stato separato in tre diversi comandi Maven.
* Se il repository Git non viene clonato, verrà ripetuto fino a tre volte.

### Correzioni di bug {#bug-fixes-cm}

* La scheda Controllo contenuto visualizzava erroneamente l’URL di base utilizzando il dominio di creazione invece del dominio di pubblicazione.

## Cloud Readiness Analyzer (Analisi di preparazione al cloud) {#cloud-readiness-analyzer}

Leggi questa sezione per saperne di più sulle novità e sugli aggiornamenti di Cloud Readiness Analyzer v1.1.0.

### Novità {#what-is-new-cra}

* La console CRA (Cloud Readiness Analyzer) dispone di una console di stato iniziale che consente di visualizzare un pulsante **Genera report** esplicito su cui l&#39;utente può fare clic per eseguire la CRA.

* L&#39;interfaccia utente CRA visualizza l&#39;avanzamento durante l&#39;esecuzione. Vengono visualizzati gli elementi analizzati e i risultati rilevati durante l&#39;esecuzione.

* Il rapporto CRA presenta un riepilogo e il numero dei risultati in un formato tabulare organizzato in base al tipo di ricerca e al livello di importanza. Facendo clic sul numero di risultati, si passa automaticamente alla posizione di tale ricerca nel rapporto.

### Correzioni di bug {#cra-bug-fixes}

* In alcuni casi, il rapporto CRA non veniva aggiornato dopo aver forzato un aggiornamento. Questo problema è stato risolto in questa versione.

## Strumento Content Transfer (Trasferimento contenuti) {#content-transfer-tool}

Seguite questa sezione per saperne di più sulle novità e sugli aggiornamenti di Content Transfer Tool Release v1.1.10.

### Novità {#what-is-new-ctt}

* Il Content Transfer Tool (CTT) supporta l&#39;archivio dati di Azure Blob Store.

* L&#39;interfaccia utente CTT dispone di una funzione di ricarica automatica che ricarica la pagina della panoramica ogni 30 secondi.

* Pulsante aggiunto all&#39;interfaccia utente CTT per recuperare facilmente il token *di* accesso.

* È stato aggiunto un messaggio di convalida descrittivo per il nome dell&#39; *URL* e del set di *migrazione*.

## Strumenti di refactoring del codice {#code-refactoring}

Segui questa sezione per saperne di più sulle novità e gli aggiornamenti per gli strumenti di refactoring del codice.

### Novità {#what-is-new-refactoring}

[Repository Modernizer](/help/move-to-cloud-service/refactoring-tools/repo-modernizer.md) è un&#39;utility sviluppata per ristrutturare i pacchetti di progetto esistenti separando il contenuto e il codice in pacchetti discreti per essere compatibile con la struttura di progetto definita per Adobe Experience Manager come Cloud Service.

* Il plug-in AIO-CLI supporta Repository Modernizer e consente agli utenti di eseguire lo strumento utilizzando il plugin.

   Fare riferimento a Risorse [Git: per maggiori informazioni, fai clic su aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration) .

* L&#39;utility Repository Modernizer può essere utilizzata per ristrutturare i pacchetti di progetto esistenti in pacchetti compatibili con la struttura di progetto definita per AEM come Cloud Service.

   Fare riferimento a Risorse [Git: Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) per ulteriori dettagli.

