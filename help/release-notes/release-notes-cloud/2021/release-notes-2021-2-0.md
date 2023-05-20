---
title: Note sulla versione 2021.2.0 di [!DNL Adobe Experience Manager]  as a Cloud Service.
description: "[!DNL Adobe Experience Manager] Note sulla versione 2021.2.0 as a Cloud Service."
exl-id: 88dac54b-cc12-44a0-b429-6e691221f806
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 35%

---


# Note sulla versione di [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione di [!DNL Experience Manager] as a Cloud Service.

## Data di pubblicazione {#release-date}

La data di rilascio per [!DNL Adobe Experience Manager] La versione 2021.2.0 di as a Cloud Service è il 25 febbraio 2021.
La seguente versione (2021.3.0) sarà del 25 marzo 2021.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Gestione dei contenuti headless {#headless}

* **[API GraphQL per la distribuzione dei frammenti di contenuto](/help/headless/graphql-api/content-fragments.md)**: possibilità di eseguire query sui frammenti di contenuto utilizzando la sintassi GraphQL e sugli schemi basati su modelli di frammenti di contenuto, per l’output in formato JSON.

* **[Supporto dell’autenticazione per le richieste API di GraphQL](/help/headless/security/authentication.md)**: possibilità di autenticare le richieste API di GraphQL con token di accesso per le API lato server.

* **[Componente RemotePage](/help/implementing/developing/hybrid/remote-page.md)**: è stato aggiunto il supporto per la visualizzazione e la modifica di SPA esterni all’interno dell’AEM tramite.

* **[Modifica di un SPA esterno all’interno dell’AEM](/help/implementing/developing/hybrid/editing-external-spa.md)**: è stata aggiunta la possibilità di caricare un’applicazione indipendente a pagina singola in un’istanza AEM, aggiungere sezioni di contenuto modificabili e abilitare l’authoring.

* È stato migliorato l’output JSON dall’API di GraphQL, inclusa la possibilità di generare testo RTF in formato JSON e in diverse lingue.

* Supporto per la nidificazione dei modelli di frammenti di contenuto, per consentire la creazione di strutture di frammenti di contenuto nidificate tramite tipi di dati per riferimenti a frammenti di contenuto dedicati o riferimenti a frammenti di contenuto incorporati in campi di testo multiriga.

* Regole di convalida aggiuntive disponibili nei tipi di dati dei modelli di Frammento di contenuto, tra cui &quot;univoco&quot;, &quot;obbligatorio&quot; e &quot;traducibile&quot;.

* Possibilità di assegnare tag ai modelli per frammenti di contenuto e di creare frammenti di contenuto in una cartella con criteri per tag o percorsi.

* Miglioramenti a livello di utilizzo nell’editor dei frammenti di contenuto, comprese le azioni di pubblicazione e la visualizzazione del modello su cui si basa un frammento.

* Possibilità di visualizzare l’anteprima dell’output JSON direttamente nell’editor dei frammenti di contenuto.

<!--
### Progressive Web Apps (PWAs) {#pwa}

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/features/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

## Novità in [!DNL Assets] {#what-is-new-assets}

* Le risorse possono essere originate tramite [!DNL Experience Manager Assets Brand Portal]. Consente di approvvigionarsi di risorse dagli utenti dell’agenzia per nuove campagne di marketing, servizi fotografici e progetti.

* [!DNL Experience Manager Assets] as a [!DNL Cloud Service] ha il diritto di disporre di un [!DNL Brand Portal] dell&#39;istanza. Il [!DNL Cloud Manager] l&#39;utente può attivare [!DNL Brand Portal] il [!DNL Experience Manager Assets] as a [!DNL Cloud Service]. Consulta [attivare Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/brand-portal/configure-aem-assets-with-brand-portal.html?lang=it).

* Ora le aziende possono reperire le risorse tramite [!DNL Brand Portal]. La funzione Asset sourcing sfrutta [!DNL Brand Portal] per aiutare i clienti a interagire con gli utenti dell’agenzia e reperire risorse per nuove campagne di marketing, servizi fotografici e progetti. Consulta [asset sourcing in [!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=it).

* Il [!DNL Brand Portal] il rapporto di utilizzo ora visualizza solo gli utenti attivi. Gli utenti inattivi non vengono più visualizzati. Gli utenti attivi sono quelli il cui account è assegnato a un profilo di prodotto in [!DNL Admin Console]. Consulta [[!DNL Brand Portal] rapporti](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/admin-tools/brand-portal-reports.html).

* In entrata [!DNL Brand Portal], viene introdotta una nuova impostazione di download che consente di creare cartelle separate per ogni risorsa durante il download di cartelle, raccolte e così via. Consulta [impostazioni di download](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html).

## Correzioni di bug in [!DNL Assets] {#bug-fixes-assets}

* Quando sono selezionate più risorse per aggiornare le proprietà, a volte si verifica un errore o le proprietà di una risorsa deselezionata vengono aggiornate. (CQ-4316532)
* Quando si tenta di aprire [!UICONTROL Barra di ricerca amministrazione risorse], la pagina rimane vuota e si fa clic su [!UICONTROL Modifica] > [!UICONTROL Impostazioni] genera un errore. (CQ-4315079)
* Quando viene creata una nuova versione di una risorsa esistente dopo aver risolto il conflitto di denominazione, i metadati della risorsa originale vengono sovrascritti. (CQ-4313594)
* Quando viene stampata una risorsa con testo di annotazione lungo, il testo dell’annotazione viene ritagliato, anche se è disponibile dello spazio. (CQ-4314101)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* Gestione dell’esperienza del prodotto: arricchisci le pagine dei cataloghi di prodotti singolarmente con Frammenti esperienza.

* Proprietà estese della console prodotti per visualizzare le risorse collegate e i frammenti di esperienza, con azioni per passare rapidamente al contenuto associato.

* È stato rilasciato il sito di riferimento CIF Venia (24.02.2021), che include la versione più recente dei Componenti Core CIF 1.8.0. Fai riferimento a [Sito di riferimento CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.24) per ulteriori dettagli.

* È stata rilasciata la versione 1.8.0 dei componenti core CIF. Fai riferimento a [Componenti core CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.8.0) per ulteriori dettagli.

## Cloud Manager {#cloud-manager}

### Data di pubblicazione {#release-date-cm}

La data di pubblicazione di Cloud Manager in AEM as a Cloud Service 2021.2.0 è il 11 febbraio 2021.

### Novità {#what-is-new-cloud-manager}


* Ora i clienti di Assets possono scegliere quando e dove distribuire l’istanza di Brand Portal in modalità self-service tramite l’interfaccia utente di Cloud Manager. Ora per un programma normale (non sandbox) con soluzione Assets è possibile eseguire il provisioning di Brand Portal nell’ambiente di produzione. Il provisioning può essere eseguito una sola volta nell’ambiente di produzione.

* L’archetipo del progetto AEM utilizzato nella creazione di progetti e sandbox è stato aggiornato alla versione 25.

* L’elenco delle API obsolete identificate durante il controllo del codice è stato perfezionato per includere classi e metodi obsoleti aggiuntivi rilevati nelle versioni più aggiornate dell’SDK di Cloud Service.

* Il profilo SonarQube per Cloud Manager è stato aggiornato per rimuovere la regola Sonar squid:S2142. Non entrerà più in conflitto con i controlli di interruzione del thread.

* Ora l’interfaccia utente di Cloud Manager informa l’utente che temporaneamente potrebbe non essere possibile aggiungere/aggiornare il nome di dominio in quanto all’ambiente associato è collegata una pipeline in esecuzione o attualmente in attesa del passaggio di approvazione.

* Ora le proprietà impostate nei file `pom.xml` del cliente con prefisso sonar vengono rimosse dinamicamente per evitare errori di build e del controllo di qualità.

* Ora l’interfaccia utente di Cloud Manager informa l’utente che temporaneamente potrebbe non essere possibile selezionare un certificato SSL se questo è in uso da un nome di dominio attualmente in fase di distribuzione.

* Sono state aggiunte ulteriori regole per la qualità del codice per risolvere i problemi relativi alla compatibilità con Cloud Service.

### Correzioni di bug {#bug-fixes-cloud-manager}

* La corrispondenza tra certificato SSL e nome di dominio non fa più distinzione tra maiuscole e minuscole.

* Ora l’interfaccia utente di Cloud Manager informa l’utente con un messaggio di errore appropriato nel caso in cui le chiavi private del certificato non rientrino nel limite di 2048 bit.

* Ora l’interfaccia utente di Cloud Manager informa l’utente che temporaneamente potrebbe non essere possibile selezionare un certificato SSL se questo è in uso da un nome di dominio attualmente in fase di distribuzione.

* In alcuni casi, un problema interno causa il blocco dell’eliminazione dell’ambiente.

* Alcuni problemi della pipeline venivano erroneamente segnalati come errori della pipeline.

## Strumento Trasferimento contenuti {#content-transfer-tool}

### Data di pubblicazione {#release-date-ctt}

La data di pubblicazione dello strumento Content Transfer v1.2.4 è il 10 febbraio 2021.

### Correzioni di bug {#bug-fixes-ctt}

* Quando si mappavano più utenti, gli ID IMS di alcuni utenti non venivano mappati correttamente. Questo problema è stato risolto.

### Data di pubblicazione {#release-date-ctt-feb}

La data di pubblicazione dello strumento Content Transfer v1.2.2 è il 01 febbraio 2021.

### Novità dello strumento Content Transfer {#what-is-new-ctt}

* Nuove funzionalità e interfaccia utente aggiunte allo strumento Content Transfer (Trasferimento contenuti) - Strumento di mappatura utenti. Questa funzione mappa automaticamente utenti e gruppi esistenti ai loro ID di sistema Adobe Identity Management come parte dell’attività di migrazione dei contenuti.
Fai riferimento a [Utilizzo dello strumento di mappatura utenti](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=it) per ulteriori dettagli.
* Lo strumento Content Transfer (Trasferimento contenuti) ora esegue la migrazione di tutti i gruppi e gli utenti a cui si fa riferimento nel set di migrazione, inclusi gli elementi figlio.
* Gli utenti possono selezionare alcuni percorsi in `/etc` durante la creazione dei set di migrazione.

## Analisi delle best practice {#best-practices-analyzer}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.2 è il 18 febbraio 2021.

### Novità di Best Practices Analyzer {#what-is-new-bpa}

* Possibilità di rilevare l’utilizzo dell’implementazione di AEM Forms e AEM Forms e di indicare le aree rilevanti per la migrazione ad AEM Forms as a Cloud Service.
* Possibilità di rilevare e segnalare l’utilizzo e il numero di componenti e modelli personalizzati.
* Possibilità di rilevare il tipo di archivio nodi e di archivio dati utilizzati.
* Possibilità di rilevare l’utilizzo di Dynamic Media.
* Possibilità di rilevare la versione Java utilizzata.

## Strumenti di refactoring del codice {#code-refactoring-tools}

### Novità degli strumenti di refactoring del codice {#what-is-new-crt}

* È stata rilasciata la nuova versione del plug-in AIO-CLI. La versione più recente di questo plug-in include diverse correzioni di bug per Repository Modernizer.
Fai riferimento a [Esperienza unificata](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) per ulteriori informazioni su questo plug-in.

### Correzioni di bug {#bug-fixes-crt}

* Sono state apportate diverse correzioni di bug in Repository Modernizer.
Fai riferimento a [Risorsa GitHub: aem-cloud-service-source-migration](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) per ulteriori dettagli.
