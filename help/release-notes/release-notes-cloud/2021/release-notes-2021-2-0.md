---
title: Note sulla versione 2021.2.0 di  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: "[!DNL Adobe Experience Manager] Note sulla versione as a Cloud Service per 2021.2.0."
exl-id: 88dac54b-cc12-44a0-b429-6e691221f806
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 8%

---


# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione di [!DNL Experience Manager] as a Cloud Service.

## Data di pubblicazione {#release-date}

Data di rilascio per [!DNL Adobe Experience Manager] as a Cloud Service 2021.2.0 è il 25 febbraio 2021.
La versione seguente (2021.3.0) sarà del 25 marzo 2021.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Gestione dei contenuti headless {#headless}

* **[API GraphQL per la distribuzione di frammenti di contenuto](/help/headless/graphql-api/content-fragments.md)**: Possibilità di eseguire query sui frammenti di contenuto utilizzando la sintassi GraphQL e gli schemi basati su modelli di frammenti di contenuto per l’output in formato JSON.

* **[Supporto per l’autenticazione per le richieste API GraphQL](/help/headless/security/authentication.md)**: Possibilità di autenticare le richieste API GraphQL con token di accesso per le API lato server.

* **[Componente RemotePage](/help/implementing/developing/hybrid/remote-page.md)**: È stato aggiunto il supporto per la visualizzazione e la modifica di SPA esterni in AEM utilizzando.

* **[Modifica di un SPA esterno in AEM](/help/implementing/developing/hybrid/editing-external-spa.md)**: È stata aggiunta la possibilità di caricare un’applicazione a pagina singola autonoma in un’istanza AEM, aggiungere sezioni di contenuto modificabili e abilitare l’authoring.

* Output JSON migliorato dall’API GraphQL, inclusa la possibilità di generare testo RTF in formato JSON e impostazioni internazionali.

* Supporto per la nidificazione di modelli di frammenti di contenuto per consentire la creazione di strutture di frammenti di contenuto nidificate tramite tipi di dati di riferimento a frammenti di contenuto dedicati o riferimenti a frammenti di contenuto in linea in campi di testo multilingue.

* Regole di convalida aggiuntive disponibili nei tipi di dati dei modelli di frammento di contenuto, inclusi &quot;univoci&quot;, &quot;obbligatori&quot; e &quot;traducibili&quot;.

* Possibilità di assegnare tag ai modelli di frammenti di contenuto e di creare frammenti di contenuto in una cartella con criteri basati su tag o percorsi.

* Miglioramenti a livello di usabilità nell’editor dei frammenti di contenuto, inclusa l’azione di pubblicazione e la visualizzazione del modello su cui si basa un frammento.

* Possibilità di visualizzare in anteprima l’output JSON direttamente nell’editor frammento di contenuto.

<!--
### Progressive Web Apps (PWAs) {#pwa}

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/features/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

## Novità in [!DNL Assets] {#what-is-new-assets}

* Le risorse possono essere reperite utilizzando [!DNL Experience Manager Assets Brand Portal]. Consente di reperire risorse dagli utenti dell’agenzia per nuove campagne di marketing, fototiri e progetti.

* [!DNL Experience Manager Assets] come [!DNL Cloud Service] ha il diritto di disporre di un [!DNL Brand Portal] istanza. La [!DNL Cloud Manager] l&#39;utente può attivare [!DNL Brand Portal] su [!DNL Experience Manager Assets] come [!DNL Cloud Service]. Vedi [attivare Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/brand-portal/configure-aem-assets-with-brand-portal.html?lang=it).

* Ora le aziende possono reperire risorse utilizzando [!DNL Brand Portal]. Utilizzo della funzione Asset sourcing [!DNL Brand Portal] per aiutare i clienti a interagire con gli utenti dell’agenzia per reperire risorse per nuove campagne di marketing, scatti fotografici e progetti. Vedi [determinazione delle risorse in [!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=it).

* La [!DNL Brand Portal] il rapporto di utilizzo ora visualizza solo gli utenti attivi. Gli utenti inattivi non vengono visualizzati ora. Gli utenti attivi sono quelli il cui account è assegnato a un profilo di prodotto nel [!DNL Admin Console]. Vedi [[!DNL Brand Portal] rapporti](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/admin-tools/brand-portal-reports.html).

* In [!DNL Brand Portal], viene introdotta una nuova impostazione di download che consente di creare una cartella separata per ogni risorsa durante il download di cartelle, raccolte e così via. Vedi [scarica impostazioni](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html).

## Correzioni di bug in [!DNL Assets] {#bug-fixes-assets}

* Quando selezioni più risorse per aggiornare le proprietà, a volte si verifica un errore o le proprietà di una risorsa deselezionata vengono aggiornate. (CQ-4316532)
* Quando si tenta di aprire [!UICONTROL Barra di ricerca amministrazione risorse], la pagina rimane vuota e facendo clic su [!UICONTROL Modifica] > [!UICONTROL Impostazioni] genera un errore. (CQ-4315079)
* Quando viene creata una nuova versione di una risorsa esistente dopo la risoluzione del conflitto di denominazione, i metadati della risorsa originale vengono sovrascritti. (CQ-4313594)
* Quando viene stampata una risorsa con testo di annotazione lungo, il testo dell’annotazione viene troncato, anche se è disponibile spazio. (CQ-4314101)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* Gestione dell&#39;esperienza del prodotto: Arricchisci le pagine dei cataloghi di prodotti singolarmente con Frammenti esperienza.

* Proprietà estese della console prodotti per visualizzare le risorse collegate e i frammenti esperienza, con l’azione di passare rapidamente al contenuto associato.

* Sito di riferimento CIF Venia rilasciato: 2021.02.24 che include la versione più recente dei componenti core CIF versione v1.8.0. Fai riferimento a [Sito di riferimento CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.24) per ulteriori dettagli.

* È stata rilasciata la versione 1.8.0 dei componenti core CIF. Fai riferimento a [Componenti core CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.8.0) per ulteriori dettagli.

## Cloud Manager {#cloud-manager}

### Data di pubblicazione {#release-date-cm}

La data di rilascio di Cloud Manager in AEM as a Cloud Service 2021.2.0 è l’11 febbraio 2021.

### Novità {#what-is-new-cloud-manager}


* I clienti di Assets ora potranno scegliere quando e dove implementare la propria istanza Brand Portal in modalità self-service tramite l’interfaccia utente di Cloud Manager. Per un programma normale (non sandbox) con soluzione Assets, ora è possibile eseguire il provisioning di Brand Portal nell’ambiente Produzione. Il provisioning può essere eseguito una sola volta nell’ambiente di produzione.

* L’Archetipo di progetto AEM utilizzato nella creazione di progetti e sandbox è stato aggiornato alla versione 25.

* L’elenco delle API obsolete identificate durante la scansione del codice è stato perfezionato per includere classi e metodi aggiuntivi obsoleti nelle ultime versioni dell’SDK di Cloud Service.

* Profilo SonarQube per Cloud Manager aggiornato per rimuovere Sonar rule squid:S2142. Questo non entrerà più in conflitto con i controlli di interruzione del thread.

* L’interfaccia utente di Cloud Manager informa l’utente che potrebbe non essere temporaneamente in grado di aggiungere/aggiornare il nome di dominio perché all’ambiente associato è collegata una pipeline in esecuzione o attualmente in attesa del passaggio di approvazione.

* Proprietà impostate nel cliente `pom.xml` i file con prefisso sonar vengono ora rimossi dinamicamente per evitare errori di creazione e di scansione della qualità.

* L’interfaccia utente di Cloud Manager informa l’utente che potrebbe non essere temporaneamente in grado di selezionare un certificato SSL se è utilizzato da un nome di dominio attualmente distribuito.

* Sono state aggiunte regole aggiuntive per la qualità del codice per risolvere i problemi relativi alla compatibilità dei Cloud Service.

### Correzioni di bug {#bug-fixes-cloud-manager}

* La corrispondenza del certificato SSL rispetto a un nome di dominio non fa più distinzione tra maiuscole e minuscole.

* L’interfaccia utente di Cloud Manager ora informa un utente se le chiavi private del certificato non soddisfano il limite di 2048 bit con un messaggio di errore appropriato.

* L’interfaccia utente di Cloud Manager informa l’utente che potrebbe non essere temporaneamente in grado di selezionare un certificato SSL se è utilizzato da un nome di dominio attualmente distribuito.

* In alcuni casi, un problema interno può causare il blocco dell’eliminazione dell’ambiente.

* Alcuni errori di pipeline non sono stati segnalati correttamente come errori di pipeline.

## Strumento Trasferimento contenuti {#content-transfer-tool}

### Data di pubblicazione {#release-date-ctt}

La data di pubblicazione dello strumento Content Transfer v1.2.4 è il 10 febbraio 2021.

### Correzioni di bug {#bug-fixes-ctt}

* Quando si mappavano più utenti, alcuni ID IMS di alcuni utenti venivano mappati in modo errato. Questo problema è stato risolto.

### Data di pubblicazione {#release-date-ctt-feb}

La data di pubblicazione dello strumento Content Transfer v1.2.2 è il 01 febbraio 2021.

### Novità nello strumento Content Transfer (Trasferimento contenuti) {#what-is-new-ctt}

* Aggiunta di nuove funzionalità e interfaccia utente allo strumento Content Transfer (Trasferimento contenuti) - User Mapping Tool (Strumento di mappatura utenti). Questa funzione mappa automaticamente gli utenti e i gruppi esistenti ai loro ID di sistema Identity Management di Adobe come parte dell’attività di migrazione dei contenuti.
Fai riferimento a [Utilizzo dello strumento di mappatura utente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) per ulteriori dettagli.
* Lo strumento Content Transfer (Trasferimento contenuti) ora esegue la migrazione di tutti i gruppi e gli utenti a cui viene fatto riferimento nel set di migrazione, inclusi gli elementi figlio.
* Gli utenti possono selezionare determinati percorsi in `/etc` durante la creazione di set di migrazione.

## Analisi delle best practice {#best-practices-analyzer}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.2 è il 18 febbraio 2021.

### Novità di Best Practices Analyzer {#what-is-new-bpa}

* Possibilità di rilevare l’utilizzo dell’implementazione di AEM Forms e AEM Forms e indicare le aree rilevanti per la migrazione ad AEM Forms as a Cloud Service.
* Possibilità di rilevare e generare rapporti sull’utilizzo e il conteggio dei componenti e dei modelli personalizzati.
* Possibilità di rilevare il tipo di archivio nodi e archivio dati utilizzati.
* Possibilità di rilevare l’utilizzo di Dynamic Media.
* Possibilità di rilevare la versione Java utilizzata.

## Strumenti di refactoring del codice {#code-refactoring-tools}

### Novità degli strumenti di refactoring del codice {#what-is-new-crt}

* È stata rilasciata la nuova versione del plug-in AIO-CLI. La versione più recente di questo plug-in include diverse correzioni di bug per Repository Modernizer.
Fai riferimento a [Esperienza unificata](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) per ulteriori informazioni su questo plug-in.

### Correzioni di bug {#bug-fixes-crt}

* Diverse correzioni di bug eseguite su Repository Modernizer.
Fai riferimento a [Risorsa GitHub: aem-cloud-service-source-migration](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) per ulteriori dettagli.
