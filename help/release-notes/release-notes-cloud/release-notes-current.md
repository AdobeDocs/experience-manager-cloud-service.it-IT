---
title: Note sulla versione 2020.9.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: '[!DNL Adobe Experience Manager] as a Cloud Service: note sulla versione 2020.9.0.'
translation-type: tm+mt
source-git-commit: 9bb087cb0570a1f3bbffb989a9399d3274f9c5e1
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 22%

---


# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service 2020.9.0 {#release-notes}

La sezione seguente illustra le note generali sulla versione di Experience Manager as a Cloud Service 2020.9.0.

## [!DNL Adobe Experience Manager Sites] come Cloud Service {#sites}

### What is new in [!DNL Sites] {#what-is-new-sites}

* L’SDK Javascript per l’editor di applicazioni per pagina singola (SPA) ora [è open source.](/help/implementing/developing/spa/reference-materials.md)

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

