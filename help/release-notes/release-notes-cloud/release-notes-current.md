---
title: Note sulla versione corrente per  [!DNL Adobe Experience Manager] come Cloud Service.
description: Note sulla versione corrente per  [!DNL Adobe Experience Manager] come Cloud Service.
translation-type: tm+mt
source-git-commit: 429d1710af30f85174f69ed111140b2e4fb5ab0f
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 5%

---


# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

Nella sezione seguente sono riportate le note generali sulla versione relative a [!DNL Experience Manager] come Cloud Service.

## Data di rilascio {#release-date}

La data di rilascio per [!DNL Adobe Experience Manager] come Cloud Service 2021.1.0 è il 3 febbraio 2021.
La seguente release (2021.2.0) sarà del 25 febbraio 2021.

## [!DNL Adobe Experience Manager Sites] come Cloud Service  {#sites}

* **[API GraphQL per la distribuzione](/help/assets/content-fragments/graphql-api-content-fragments.md)** dei frammenti di contenuto: Possibilità di eseguire query sui frammenti di contenuto utilizzando la sintassi GraphQL e gli schemi basati su modelli di frammenti di contenuto, per l&#39;output in formato JSON.

* **[Supporto dell&#39;autenticazione per le richieste](/help/assets/content-fragments/graphql-authentication-content-fragments.md)** API GraphQL: Possibilità di autenticare le richieste API GraphQL con token di accesso per le API lato server.

* È stato migliorato l&#39;output JSON dall&#39;API GraphQL, inclusa la possibilità di restituire testo RTF in formato JSON e nelle impostazioni internazionali.

* Supporto per la nidificazione di modelli di frammenti di contenuto per consentire la creazione di strutture di frammenti di contenuto nidificate tramite tipi di dati Riferimento frammento di contenuto dedicati o riferimenti a frammenti di contenuto in linea in campi di testo multiriga.

* Regole di convalida aggiuntive disponibili nei tipi di dati del modello di frammento di contenuto, inclusi &quot;univoci&quot;, &quot;obbligatori&quot; e &quot;traducibili&quot;.

* Possibilità di assegnare tag ai modelli di frammenti di contenuto e di creare frammenti di contenuto in una cartella con criteri per tag o percorsi.

* Miglioramenti a livello di usabilità nell’editor dei frammenti di contenuto, comprese le azioni di pubblicazione e la visualizzazione del modello su cui si basa un frammento.

* Possibilità di visualizzare l&#39;anteprima dell&#39;output JSON direttamente nell&#39;editor frammento di contenuto.


## [!DNL Adobe Experience Manager Assets] come  [!DNL Cloud Service] {#assets}

* [!DNL Experience Manager] come  [!DNL Cloud Service] estensione della funzionalità Smart Tags per l’identificazione di parole chiave ed entità in risorse basate su testo. Il testo viene identificato, indicizzato e reso disponibile come metadati per migliorare l’esperienza di ricerca senza bisogno di alcuna configurazione. Vedere [Tag avanzati](/help/assets/smart-tags.md).

* È ora supportato il formato di file MXF. Vedere [formati di file supportati](/help/assets/file-format-support.md#video-formats).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* Product Experience Management: Nuova scheda &quot;Commerce&quot; per risorse e frammenti esperienza. Questa scheda consente di collegare prodotti/categorie a risorse e frammenti esperienza. La scheda mostra anche i dati in tempo reale per prodotti/categorie collegati e un collegamento per visualizzare i dettagli nella console del prodotto.

* Sito di riferimento CIF Venia rilasciato - 2021.02.02 che include l&#39;ultima versione CIF Core Components v1.7.0. Per ulteriori informazioni, fare riferimento a [CIF Venia Reference Site](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.02).

* Componenti CIF di base rilasciati v1.7.0. Per ulteriori informazioni, consultare [CIF Core Components](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.7.0).

## Cloud Manager {#cloud-manager}

### Data di rilascio {#release-date-cm}

La data di rilascio per Cloud Manager in AEM come Cloud Service 2021.1.0 è il 14 gennaio 2021.

### Correzioni di bug {#bug-fixes-cloud-manager}

* In alcuni casi, l&#39;istanza Produzione risorse può mostrare lo stato del Portale marchio nella pagina di dettaglio **Ambienti** come *In sospeso*, senza consentire all&#39;utente di eseguire alcuna azione.

* Quando si attiva la disattivazione da Cloud Manager, talvolta veniva visualizzato un messaggio di errore anche quando la disattivazione veniva avviata correttamente.

* Sono stati risolti rari casi di errori nella creazione o eliminazione dell&#39;ambiente.

## AEM come base di Cloud Service {#aem-as-a-cloud-service-foundation}

### Novità {#what-is-new-foundation}

* Chiamate API autenticate da server a server - Generate i token di accesso appropriati per effettuare chiamate API da server a server autenticate tra le applicazioni esterne e AEM come ambienti di Cloud Service. Per saperne di più, leggi [la documentazione](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) o consulta l&#39; [tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication).

### SDK Build Analytics {#sdk-build-analyzers}

Il AEM come Cloud Service SDK Build Analyzer Maven Plugin rileva i problemi in un progetto maven, comprese le dipendenze mancanti. Offre agli sviluppatori l&#39;opportunità di individuare i problemi durante lo sviluppo locale, ben prima di distribuirli in ambienti Cloud con Cloud Manager.

Per questa versione sono stati aggiunti due nuovi analizzatori:

* analizzatore repoinit
* bundle-nativecode

Per ulteriori informazioni, consultare la documentazione [qui](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing).

## Strumenti di transizione verso il cloud {#code-transition-tools}

### Data di rilascio {#release-date-ctt}

La Data di rilascio per lo strumento di trasferimento dei contenuti v1.2.2 è il 10 febbraio 2021.

### Novità in [!DNL Content Transfer Tool] {#what-is-new-ctt}

* Nuove funzionalità e interfaccia utente aggiunte a Content Transfer Tool - Strumento di mappatura utente. Questa funzione mappa automaticamente gli utenti e i gruppi esistenti al loro Adobe   ID di sistema Identity Management nell’ambito dell’attività di migrazione dei contenuti. Per ulteriori informazioni, fare riferimento a [Utilizzo dello strumento di mappatura utente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html).
* Content Transfer Tool ora esegue la migrazione di tutti i gruppi e gli utenti a cui viene fatto riferimento nel set di migrazione, inclusi gli elementi figlio.
* Gli utenti possono selezionare alcuni percorsi in `/etc` al momento della creazione dei set di migrazione.
