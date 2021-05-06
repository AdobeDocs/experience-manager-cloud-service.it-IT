---
title: Note sulla versione 2021.1.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: '[!DNL Adobe Experience Manager] as a Cloud Service - Note sulla versione 2021.1.0.'
exl-id: cd639736-6e3d-4b69-b8ae-11e4e6490535
translation-type: tm+mt
source-git-commit: b842f70bd53676d23229e24edb4a957ff7613824
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 5%

---


# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione per [!DNL Experience Manager] come Cloud Service.

## Data di rilascio {#release-date}

La data di rilascio per [!DNL Adobe Experience Manager] as a Cloud Service 2021.1.0 è il 3 febbraio 2021.
La versione seguente (2021.2.0) sarà del 25 febbraio 2021.

## [!DNL Adobe Experience Manager Sites] come Cloud Service  {#sites}

* **[API](/help/assets/content-fragments/assets-api-content-fragments.md)** HTTP per frammento di contenuto: Aggiungi la possibilità di aggiungere/aggiornare ed eliminare varianti di frammenti di contenuto utilizzando l’API HTTP.

* **[API GraphQL per la distribuzione](/help/assets/content-fragments/graphql-api-content-fragments.md)** di frammenti di contenuto: Possibilità di eseguire query sui frammenti di contenuto utilizzando la sintassi GraphQL e gli schemi basati su modelli di frammenti di contenuto per l’output in formato JSON.

* **[Supporto per l’autenticazione per le richieste](/help/assets/content-fragments/graphql-authentication-content-fragments.md)** API GraphQL: Possibilità di autenticare le richieste API GraphQL con token di accesso per le API lato server.

* Output JSON migliorato dall’API GraphQL, inclusa la possibilità di generare testo RTF in formato JSON e impostazioni internazionali.

* Supporto per la nidificazione di modelli di frammenti di contenuto per consentire la creazione di strutture di frammenti di contenuto nidificate tramite tipi di dati di riferimento a frammenti di contenuto dedicati o riferimenti a frammenti di contenuto in linea in campi di testo multilingue.

* Regole di convalida aggiuntive disponibili nei tipi di dati dei modelli di frammento di contenuto, inclusi &quot;univoci&quot;, &quot;obbligatori&quot; e &quot;traducibili&quot;.

* Possibilità di assegnare tag ai modelli di frammenti di contenuto e di creare frammenti di contenuto in una cartella con criteri basati su tag o percorsi.

* Miglioramenti a livello di usabilità nell’editor dei frammenti di contenuto, inclusa l’azione di pubblicazione e la visualizzazione del modello su cui si basa un frammento.

* Possibilità di visualizzare in anteprima l’output JSON direttamente nell’editor frammento di contenuto.


## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

* [!DNL Experience Manager] as a  [!DNL Cloud Service] estende la funzionalità Tag avanzati per supportare l’identificazione di parole chiave ed entità nelle risorse basate su testo. Il testo viene identificato, indicizzato e reso disponibile come metadati per migliorare l’esperienza di ricerca senza la necessità di alcuna configurazione. Consulta [Tag avanzati](/help/assets/smart-tags.md).

* È ora supportato il formato di file MXF. Vedere [formati di file supportati](/help/assets/file-format-support.md#video-formats).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* Gestione dell&#39;esperienza del prodotto: Nuova scheda delle proprietà &quot;Commerce&quot; per Assets e Frammenti esperienza. Questa scheda ti consente di collegare prodotti/categorie a risorse e frammenti esperienza. La scheda mostra anche i dati in tempo reale per prodotti/categorie collegati e un collegamento per mostrare i dettagli nella console del prodotto.

* È stato rilasciato il sito di riferimento CIF Venia - 2021.02.02 che include la versione più recente dei componenti core CIF versione v1.7.0. Per ulteriori informazioni, consulta [CIF Venia Reference Site](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.02) .

* È stata rilasciata la versione 1.7.0 dei componenti core CIF. Per ulteriori informazioni, consulta [Componenti core CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.7.0) .

## Cloud Manager {#cloud-manager}

### Data di rilascio {#release-date-cm}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.1.0 è il 14 gennaio 2021.

### Correzioni di bug {#bug-fixes-cloud-manager}

* L’istanza Produzione di Assets può occasionalmente mostrare lo stato del Brand Portal nella pagina di dettaglio **Ambienti** come *In sospeso* senza consentire all’utente di eseguire alcuna azione.

* Quando si attiva una disattivazione da Cloud Manager, a volte veniva visualizzato un messaggio di errore anche quando la disattivazione è stata avviata correttamente.

* Sono stati risolti alcuni rari casi di errore durante la creazione o l’eliminazione dell’ambiente.

## Strumenti di refactoring del codice {#code-refactoring-tools}

### Novità in [!DNL Code Refactoring Tools] {#what-is-new-crt}

* È stata rilasciata la nuova versione del plug-in AIO-CLI. La versione più recente di questo plug-in include correzioni di bug per AEM Dispatcher Converter e Repository Modernizer e supporta anche una nuova utility - Index Converter. Per ulteriori informazioni su questo plug-in, consulta [Esperienza unificata](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) .

* Index Converter è un&#39;utilità che può essere utilizzata per trasformare le definizioni di indice OAK personalizzato di un cliente in AEM come definizioni di indici OAK compatibili con il Cloud Service. Per ulteriori informazioni, consulta [Convertitore indice](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter) .

* Nuova funzionalità aggiunta a [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) che crea un pacchetto separato `ui.config` per contenere tutte le configurazioni OSGi.

### Correzioni di bug {#crt-bug-fixes}

* Diverse correzioni di bug eseguite sugli strumenti AEM Dispatcher Converter e Repository Modernizer . Fai riferimento a [AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) e [Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).

## AEM come base di Cloud Service {#aem-as-a-cloud-service-foundation}

### Novità {#what-is-new-foundation}

* Chiamate API autenticate server-to-server : genera i token di accesso appropriati per effettuare chiamate API server-to-server autenticate tra le applicazioni esterne e AEM come ambienti di Cloud Service. Per saperne di più, leggi [la documentazione](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) o consulta l&#39; [tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication).

### SDK Build Analytics {#sdk-build-analyzers}

Il plug-in Maven AEM as a Cloud Service SDK Build Analyzer rileva i problemi in un progetto Maven, incluse le dipendenze mancanti. Offre agli sviluppatori l’opportunità di scoprire i problemi durante lo sviluppo locale, molto prima di distribuirli in ambienti Cloud con Cloud Manager.

Per questa versione sono stati aggiunti due nuovi analizzatori:

* analizzatore repoinit
* codice nativo del bundle

Per ulteriori informazioni, consulta la documentazione [qui](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing).

## Strumenti di transizione verso il cloud {#code-transition-tools}

### Data di rilascio {#release-date-ctt}

La data di rilascio dello strumento Content Transfer (Trasferimento contenuti) v1.2.2 è il 10 febbraio 2021.

### Novità in [!DNL Content Transfer Tool] {#what-is-new-ctt}

* Aggiunta di nuove funzionalità e interfaccia utente allo strumento Content Transfer (Trasferimento contenuti) - User Mapping Tool (Strumento di mappatura utenti). Questa funzione mappa automaticamente gli utenti e i gruppi esistenti ai loro ID di sistema Identity Management di Adobe come parte dell’attività di migrazione dei contenuti. Per ulteriori informazioni, consulta [Utilizzo dello strumento di mappatura utente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) .
* Lo strumento Content Transfer (Trasferimento contenuti) ora esegue la migrazione di tutti i gruppi e gli utenti a cui viene fatto riferimento nel set di migrazione, inclusi gli elementi figlio.
* Gli utenti possono selezionare determinati percorsi in `/etc` durante la creazione dei set di migrazione.
