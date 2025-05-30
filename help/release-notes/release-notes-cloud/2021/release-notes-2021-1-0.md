---
title: Note sulla versione 2021.1.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: '[!DNL Adobe Experience Manager] as a Cloud Service note sulla versione 2021.1.0.'
exl-id: cd639736-6e3d-4b69-b8ae-11e4e6490535
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 21%

---


# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione di [!DNL Experience Manager] as a Cloud Service.

## Data di pubblicazione {#release-date}

La data di rilascio per [!DNL Adobe Experience Manager] as a Cloud Service 2021.1.0 è il 3 febbraio 2021.
La seguente versione (2021.2.0) sarà del 25 febbraio 2021.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* **[API HTTP per frammenti di contenuto](/help/assets/content-fragments/assets-api-content-fragments.md)**: è stata aggiunta la possibilità di aggiungere/aggiornare ed eliminare varianti di frammenti di contenuto mediante API HTTP.

* **[API GraphQL per la distribuzione dei frammenti di contenuto](/help/headless/graphql-api/content-fragments.md)**: possibilità di eseguire query sui frammenti di contenuto utilizzando la sintassi GraphQL e gli schemi basati su modelli di frammenti di contenuto, per l&#39;output in formato JSON.

* **[Supporto dell&#39;autenticazione per le richieste API GraphQL](/help/headless/security/authentication.md)**: possibilità di autenticare le richieste API GraphQL con token di accesso per le API lato server.

* È stato migliorato l’output JSON dall’API di GraphQL, inclusa la possibilità di generare testo RTF in formato JSON e in diverse lingue.

* Supporto per la nidificazione dei modelli di frammenti di contenuto, per consentire la creazione di strutture di frammenti di contenuto nidificate tramite tipi di dati per riferimenti a frammenti di contenuto dedicati o riferimenti a frammenti di contenuto incorporati in campi di testo multiriga.

* Regole di convalida aggiuntive disponibili nei tipi di dati dei modelli di Frammento di contenuto, tra cui &quot;univoco&quot;, &quot;obbligatorio&quot; e &quot;traducibile&quot;.

* Possibilità di assegnare tag ai modelli per frammenti di contenuto e di creare frammenti di contenuto in una cartella con criteri per tag o percorsi.

* Miglioramenti a livello di utilizzo nell’editor dei frammenti di contenuto, comprese le azioni di pubblicazione e la visualizzazione del modello su cui si basa un frammento.

* Possibilità di visualizzare l’anteprima dell’output JSON direttamente nell’editor dei frammenti di contenuto.


## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* [!DNL Experience Manager] as a [!DNL Cloud Service] estende la funzionalità Tag avanzati per supportare l&#39;identificazione di parole chiave ed entità in risorse basate su testo. Il testo viene identificato, indicizzato e reso disponibile come metadati per migliorare l’esperienza di ricerca senza bisogno di alcuna configurazione. Vedi [Tag avanzati](/help/assets/smart-tags.md).

* È ora supportato il formato di file MXF. Consulta [formati di file supportati](/help/assets/file-format-support.md#video-formats).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* Gestione dell’esperienza del prodotto: nuova scheda delle proprietà &quot;Commerce&quot; per Assets e Frammenti esperienza. Questa scheda ti consente di collegare prodotti e categorie ad Assets e a Frammenti di esperienza. La scheda mostra anche i dati in tempo reale per i prodotti e le categorie collegati e un collegamento per visualizzare i dettagli nella console del prodotto.

* È stato rilasciato il sito di riferimento CIF Venia (2021.02.02), che include la versione più recente dei Componenti core CIF v1.7.0. Per ulteriori dettagli, consulta [Sito di riferimento per CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.02).

* È stata rilasciata la versione 1.7.0 dei Componenti core CIF. Per ulteriori dettagli, consulta [Componenti core CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.7.0).

## Cloud Manager {#cloud-manager}

### Data di pubblicazione {#release-date-cm}

La data di pubblicazione di Cloud Manager in AEM as a Cloud Service 2021.1.0 è il 14 gennaio 2021.

### Correzioni di bug {#bug-fixes-cloud-manager}

* L’istanza di produzione di Assets a volte riporta lo stato di Brand Portal nella pagina dei dettagli **Ambienti** come *In sospeso*, senza consentire all’utente di svolgere ulteriori azioni.

* Durante una riattivazione da Cloud Manager, a volte veniva visualizzato un messaggio di errore anche quando la riattivazione veniva avviata correttamente.

* Sono stati risolti alcuni rari casi di errore durante la creazione o l’eliminazione dell’ambiente.

## Strumenti di refactoring del codice {#code-refactoring-tools}

### Novità in [!DNL Code Refactoring Tools] {#what-is-new-crt}

* È stata rilasciata la nuova versione del plug-in AIO-CLI. La versione più recente di questo plug-in include correzioni di bug per AEM Dispatcher Converter e Repository Modernizer e supporta anche una nuova utility - Index Converter. Per ulteriori informazioni su questo plug-in, consulta [Esperienza unificata](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=it#benefits).

* Index Converter è un’utility che può essere utilizzata per trasformare le definizioni dell’indice OAK personalizzato di un cliente in definizioni dell’indice OAK compatibili con AEM as a Cloud Service. Per ulteriori dettagli, vedere [Index Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter).

* È stata aggiunta una nuova funzionalità a [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) che crea un pacchetto separato `ui.config` contenente tutte le configurazioni OSGi.

### Correzioni di bug {#crt-bug-fixes}

* Sono state apportate diverse correzioni di bug agli strumenti AEM Dispatcher Converter e Repository Modernizer. Vedere [AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) e [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).

## AEM as a Cloud Service Foundation {#aem-as-a-cloud-service-foundation}

### Novità {#what-is-new-foundation}

* Chiamate API autenticate server-to-server: genera i token di accesso appropriati per effettuare chiamate API autenticate server-to-server tra le applicazioni esterne e gli ambienti AEM as a Cloud Service. Ulteriori informazioni leggendo [la documentazione](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) o consultando la [esercitazione](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=it#authentication).

### SDK Build Analyzer {#sdk-build-analyzers}

Il plug-in Maven SDK Build Analyzer per AEM as a Cloud Service rileva i problemi in un progetto Maven, incluse eventuali dipendenze mancanti. Offre agli sviluppatori l’opportunità di individuare i problemi durante lo sviluppo locale, molto prima che vengano distribuiti in ambienti Cloud con Cloud Manager.

Per questa versione sono stati aggiunti due nuovi analizzatori:

* repoinit analyzer
* bundle-nativecode

Per ulteriori informazioni, consulta la [documentazione](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=it#developing).

## Strumenti di transizione verso il cloud {#code-transition-tools}

### Data di pubblicazione {#release-date-ctt}

La data di pubblicazione dello strumento Content Transfer v1.2.2 è il 1° febbraio 2021.

### Novità in [!DNL Content Transfer Tool] {#what-is-new-ctt}

* Nuove funzionalità e interfaccia utente aggiunte allo strumento Content Transfer (Trasferimento contenuti) - Strumento di mappatura utenti. Questa funzione mappa automaticamente utenti e gruppi esistenti ai loro ID di sistema di Adobe Identity Management come parte dell’attività di migrazione dei contenuti. Vedi [Utilizzo dello strumento di mappatura utente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=it) per ulteriori dettagli.
* Lo strumento Content Transfer (Trasferimento contenuti) ora esegue la migrazione di tutti i gruppi e gli utenti a cui si fa riferimento nel set di migrazione, inclusi gli elementi figlio.
* Gli utenti possono selezionare alcuni percorsi in `/etc` durante la creazione dei set di migrazione.
