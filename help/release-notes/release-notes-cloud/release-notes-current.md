---
title: Note sulla versione corrente per  [!DNL Adobe Experience Manager] come Cloud Service.
description: Note sulla versione corrente per  [!DNL Adobe Experience Manager] come Cloud Service.
translation-type: tm+mt
source-git-commit: f1a54ac3f995a6e8cc51f9ef16e14df6210a02cd
workflow-type: tm+mt
source-wordcount: '1108'
ht-degree: 4%

---


# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

Nella sezione seguente sono riportate le note generali sulla versione relative a [!DNL Experience Manager] come Cloud Service.

## Data di rilascio {#release-date}

La data di rilascio per [!DNL Adobe Experience Manager] come Cloud Service 2021.1.0 è il 3 febbraio 2021.
La seguente release (2021.2.0) sarà del 25 febbraio 2021.

## [!DNL Adobe Experience Manager Sites] come Cloud Service  {#sites}

### Gestione dei contenuti headless {#headless}

* **[API GraphQL per la distribuzione](/help/assets/content-fragments/graphql-api-content-fragments.md)** dei frammenti di contenuto: Possibilità di eseguire query sui frammenti di contenuto utilizzando la sintassi GraphQL e gli schemi basati su modelli di frammenti di contenuto, per l&#39;output in formato JSON.

* **[Supporto dell&#39;autenticazione per le richieste](/help/assets/content-fragments/graphql-authentication-content-fragments.md)** API GraphQL: Possibilità di autenticare le richieste API GraphQL con token di accesso per le API lato server.

* **[Il componente](/help/implementing/developing/hybrid/remote-page.md)** RemotePage: È stato aggiunto il supporto per la visualizzazione e la modifica di SPA esterni all&#39;interno AEM.

* **[Modifica di una SPA esterna all&#39;interno di AEM](/help/implementing/developing/hybrid/editing-external-spa.md)**: È stata aggiunta la possibilità di caricare un’applicazione indipendente a pagina singola in un’istanza AEM, aggiungere sezioni di contenuto modificabili e abilitare l’authoring.

* È stato migliorato l&#39;output JSON dall&#39;API GraphQL, inclusa la possibilità di restituire testo RTF in formato JSON e nelle impostazioni internazionali.

* Supporto per la nidificazione di modelli di frammenti di contenuto per consentire la creazione di strutture di frammenti di contenuto nidificate tramite tipi di dati Riferimento frammento di contenuto dedicati o riferimenti a frammenti di contenuto in linea in campi di testo multiriga.

* Regole di convalida aggiuntive disponibili nei tipi di dati del modello di frammento di contenuto, inclusi &quot;univoci&quot;, &quot;obbligatori&quot; e &quot;traducibili&quot;.

* Possibilità di assegnare tag ai modelli di frammenti di contenuto e di creare frammenti di contenuto in una cartella con criteri per tag o percorsi.

* Miglioramenti a livello di usabilità nell’editor dei frammenti di contenuto, comprese le azioni di pubblicazione e la visualizzazione del modello su cui si basa un frammento.

* Possibilità di visualizzare l&#39;anteprima dell&#39;output JSON direttamente nell&#39;editor frammento di contenuto.

<!--
### Progressive Web Apps (PWAs) {#pwa}

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/features/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

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

La data di rilascio per Cloud Manager in AEM come Cloud Service 2021.2.0 è l’11 febbraio 2021.

### Novità {#what-is-new-cloud-manager}

* La pipeline di produzione di Cloud Manager ora include funzionalità di test dell&#39;interfaccia utente personalizzata.

* I clienti delle risorse potranno ora scegliere quando e dove distribuire l’istanza del Portale marchio in modo self-service tramite l’interfaccia utente di Cloud Manager. Per un normale programma (non sandbox) con soluzione Assets, ora è possibile effettuare il provisioning di Brand Portal nell&#39;ambiente Production. Il provisioning può essere eseguito solo una volta nell&#39;ambiente di produzione.

* Il tipo di archivio AEM progetto utilizzato nella creazione di progetti e sandbox è stato aggiornato alla versione 25.

* L&#39;elenco delle API obsolete identificate durante la scansione del codice è stato ridefinito in modo da includere classi e metodi aggiuntivi obsoleti nelle versioni SDK dell&#39;Cloud Service più recente.

* Profilo SonarQube per Cloud Manager aggiornato per rimuovere Sonar rule squid:S2142. Ciò non entrerà più in conflitto con i controlli di Interruzione del thread.

* L&#39;interfaccia utente di Cloud Manager informa l&#39;utente che potrebbe non essere temporaneamente in grado di aggiungere/aggiornare il nome di dominio perché nell&#39;ambiente associato è collegata una pipeline in esecuzione o al momento in attesa del passaggio di approvazione.

* Le proprietà impostate nei file `pom.xml` del cliente con il prefisso sonar verranno ora rimosse in modo dinamico per evitare errori di creazione e scansione di qualità.

* L&#39;interfaccia utente di Cloud Manager informa l&#39;utente che potrebbe non essere temporaneamente in grado di selezionare un certificato SSL se è in uso da un nome di dominio attualmente distribuito.

* Sono state aggiunte ulteriori regole sulla qualità del codice per i problemi di compatibilità del Cloud Service.

### Correzioni di bug {#bug-fixes-cloud-manager}

* La corrispondenza del certificato SSL rispetto a un nome di dominio non fa più distinzione tra maiuscole e minuscole.

* L&#39;interfaccia utente di Cloud Manager ora informa un utente se le chiavi private del certificato non soddisfano il limite di 2048 bit con un messaggio di errore appropriato.

* L&#39;interfaccia utente di Cloud Manager informa l&#39;utente che potrebbe non essere temporaneamente in grado di selezionare un certificato SSL se è in uso da un nome di dominio attualmente distribuito.

* In alcuni casi, un problema interno potrebbe causare il blocco dell&#39;eliminazione dell&#39;ambiente.

* Alcuni guasti della pipeline sono stati erroneamente riportati come errori della pipeline.

## AEM come base di Cloud Service {#aem-as-a-cloud-service-foundation}

### Novità {#what-is-new-foundation}

* Chiamate API autenticate da server a server - Generate i token di accesso appropriati per effettuare chiamate API da server a server autenticate tra le applicazioni esterne e AEM come ambienti di Cloud Service. Per saperne di più, leggi [la documentazione](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) o consulta l&#39; [tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/overview.html?lang=en#authentication).

### SDK Build Analytics {#sdk-build-analyzers}

Il AEM come Cloud Service SDK Build Analyzer Maven Plugin rileva i problemi in un progetto maven, comprese le dipendenze mancanti. Offre agli sviluppatori l&#39;opportunità di individuare i problemi durante lo sviluppo locale, ben prima di distribuirli in ambienti Cloud con Cloud Manager.

Per questa versione sono stati aggiunti due nuovi analizzatori:

* analizzatore repoinit
* bundle-nativecode

Per ulteriori informazioni, consultare la documentazione [qui](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing).

## Strumento Content Transfer (Trasferimento contenuti) {#content-transfer-tool}

### Data di rilascio {#release-date-ctt}

La Data di rilascio per lo strumento di trasferimento dei contenuti v1.2.4 è il 10 febbraio 2021.

### Correzioni di bug {#bug-fixes-ctt}

* Quando si mappavano più utenti, alcuni ID IMS degli utenti venivano mappati in modo non corretto. Questo è stato corretto.

### Data di rilascio {#release-date-ctt-feb}

La Data di rilascio per lo strumento di trasferimento dei contenuti v1.2.2 è il 10 febbraio 2021.

### Novità in [!DNL Content Transfer Tool] {#what-is-new-ctt}

* Nuove funzionalità e interfaccia utente aggiunte a Content Transfer Tool - Strumento di mappatura utente. Questa funzione mappa automaticamente gli utenti e i gruppi esistenti al loro Adobe   ID di sistema Identity Management nell’ambito dell’attività di migrazione dei contenuti. Per ulteriori informazioni, fare riferimento a [Utilizzo dello strumento di mappatura utente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html).
* Content Transfer Tool ora esegue la migrazione di tutti i gruppi e gli utenti a cui viene fatto riferimento nel set di migrazione, inclusi gli elementi figlio.
* Gli utenti possono selezionare alcuni percorsi in `/etc` al momento della creazione dei set di migrazione.

## Best practice Analyzer {#best-practices-analyzer}

### Data di rilascio {#release-date-bpa}

La data di rilascio per Best Practices Analyzer v2.1.0 è l&#39;11 febbraio 2021.

### Novità in [!DNL Best-Practices-Analyzer] {#what-is-new-bpa}

* Possibilità di rilevare l&#39;utilizzo &#39;implementazione di AEM Forms e  AEM Forms e indicare le aree rilevanti per la migrazione  AEM Forms come Cloud Service.
* Possibilità di rilevare e segnalare l’utilizzo e il conteggio dei componenti e dei modelli personalizzati.
* Possibilità di rilevare il tipo di archivio nodi e di archivio dati utilizzato.
* Possibilità di rilevare l’utilizzo di Dynamic Media.
* Possibilità di rilevare la versione Java utilizzata.







