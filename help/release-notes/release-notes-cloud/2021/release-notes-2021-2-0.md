---
title: Note sulla versione 2021.2.0 di [!DNL Adobe Experience Manager] as a Cloud Service.
description: "[!DNL Adobe Experience Manager] as a Cloud Service note sulla versione 2021.2.0."
exl-id: 88dac54b-cc12-44a0-b429-6e691221f806
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 32%

---


# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La sezione seguente illustra le note generali sulla versione di [!DNL Experience Manager] as a Cloud Service.

## Data di rilascio {#release-date}

La data di rilascio per [!DNL Adobe Experience Manager] as a Cloud Service 2021.2.0 è il 25 febbraio 2021.
La seguente versione (2021.3.0) sarà del 25 marzo 2021.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Gestione dei contenuti headless {#headless}

* **[API GraphQL per la distribuzione dei frammenti di contenuto](/help/headless/graphql-api/content-fragments.md)**: possibilità di eseguire query sui frammenti di contenuto utilizzando la sintassi GraphQL e gli schemi basati su modelli di frammenti di contenuto, per l&#39;output in formato JSON.

* **[Supporto dell&#39;autenticazione per le richieste API GraphQL](/help/headless/security/authentication.md)**: possibilità di autenticare le richieste API GraphQL con token di accesso per le API lato server.

* **[Componente RemotePage](/help/implementing/developing/hybrid/remote-page.md)**: è stato aggiunto il supporto per la visualizzazione e la modifica di SPA esterni all&#39;interno dell&#39;AEM tramite.

* **[Modifica di un SPA esterno all&#39;interno dell&#39;AEM](/help/implementing/developing/hybrid/editing-external-spa.md)**: è stata aggiunta la possibilità di caricare un&#39;applicazione indipendente a pagina singola in un&#39;istanza AEM, aggiungere sezioni di contenuto modificabili e abilitare l&#39;authoring.

* È stato migliorato l’output JSON dall’API di GraphQL, inclusa la possibilità di generare testo RTF in formato JSON e in diverse lingue.

* Supporto per la nidificazione dei modelli di frammenti di contenuto, per consentire la creazione di strutture di frammenti di contenuto nidificate tramite tipi di dati per riferimenti a frammenti di contenuto dedicati o riferimenti a frammenti di contenuto incorporati in campi di testo multiriga.

* Regole di convalida aggiuntive disponibili nei tipi di dati dei modelli di Frammento di contenuto, tra cui &quot;univoco&quot;, &quot;obbligatorio&quot; e &quot;traducibile&quot;.

* Possibilità di assegnare tag ai modelli per frammenti di contenuto e di creare frammenti di contenuto in una cartella con criteri per tag o percorsi.

* Miglioramenti a livello di utilizzo nell’editor dei frammenti di contenuto, comprese le azioni di pubblicazione e la visualizzazione del modello su cui si basa un frammento.

* Possibilità di visualizzare l’anteprima dell’output JSON direttamente nell’editor dei frammenti di contenuto.

<!--
### Progressive Web Apps (PWAs) {#pwa}

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/sites-console/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

## Novità in [!DNL Assets] {#what-is-new-assets}

* Assets può essere originato con [!DNL Experience Manager Assets Brand Portal]. Consente di approvvigionarsi di risorse dagli utenti dell’agenzia per nuove campagne di marketing, servizi fotografici e progetti.

* [!DNL Experience Manager Assets] come [!DNL Cloud Service] ha diritto ad avere un&#39;istanza [!DNL Brand Portal] preconfigurata. L&#39;utente [!DNL Cloud Manager] può attivare [!DNL Brand Portal] su [!DNL Experience Manager Assets] come [!DNL Cloud Service]. Vedere [attivare Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/brand-portal/configure-aem-assets-with-brand-portal.html).

* Le aziende possono ora trovare risorse utilizzando [!DNL Brand Portal]. La funzione Asset sourcing utilizza [!DNL Brand Portal] per aiutare i clienti a interagire con gli utenti dell&#39;agenzia per la creazione di risorse per nuove campagne di marketing, servizi fotografici e progetti. Vedi [origine risorse in [!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=it).

* Il report sull&#39;utilizzo di [!DNL Brand Portal] ora visualizza solo gli utenti attivi. Gli utenti inattivi non vengono più visualizzati. Gli utenti attivi sono quelli il cui account è assegnato a un profilo di prodotto in [!DNL Admin Console]. Consulta [[!DNL Brand Portal] report](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/admin-tools/brand-portal-reports.html).

* In [!DNL Brand Portal] viene introdotta una nuova impostazione di download che consente di creare cartelle separate per ogni risorsa durante il download di cartelle, raccolte e così via. Vedi [impostazioni download](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html).

## Correzioni di bug in [!DNL Assets] {#bug-fixes-assets}

* Quando sono selezionate più risorse per aggiornare le proprietà, a volte si verifica un errore o le proprietà di una risorsa deselezionata vengono aggiornate. (CQ-4316532)
* Quando si tenta di aprire [!UICONTROL Barra di ricerca amministrazione di Assets], la pagina rimane vuota e se si fa clic su [!UICONTROL Modifica] > [!UICONTROL Impostazioni] viene generato un errore. (CQ-4315079)
* Quando viene creata una nuova versione di una risorsa esistente dopo aver risolto il conflitto di denominazione, i metadati della risorsa originale vengono sovrascritti. (CQ-4313594)
* Quando viene stampata una risorsa con testo di annotazione lungo, il testo dell’annotazione viene ritagliato, anche se è disponibile dello spazio. (CQ-4314101)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novità {#what-is-new-commerce}

* Gestione dell’esperienza del prodotto: arricchisci le pagine dei cataloghi di prodotti singolarmente con Frammenti esperienza.

* Proprietà estese della console prodotti per mostrare Assets collegato e frammenti di esperienza, con azioni per passare rapidamente al contenuto associato.

* È stato rilasciato il sito di riferimento CIF Venia (24.02.2021), che include la versione più recente dei Componenti core CIF v1.8.0. Per ulteriori dettagli, consulta [Sito di riferimento per CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.24).

* È stata rilasciata la versione 1.8.0 dei Componenti core CIF. Per ulteriori dettagli, consulta [Componenti core CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.8.0).

## Cloud Manager {#cloud-manager}

### Data di pubblicazione {#release-date-cm}

La data di pubblicazione di Cloud Manager in AEM as a Cloud Service 2021.2.0 è il 11 febbraio 2021.

### Novità {#what-is-new-cloud-manager}


* Ora i clienti di Assets possono scegliere quando e dove distribuire l’istanza di Brand Portal in modalità self-service tramite l’interfaccia utente di Cloud Manager. Ora per un programma normale (non sandbox) con soluzione Assets è possibile eseguire il provisioning di Brand Portal nell’ambiente di produzione. Il provisioning può essere eseguito una sola volta nell’ambiente di produzione.

* L’archetipo del progetto AEM utilizzato nella creazione di progetti e sandbox è stato aggiornato alla versione 25.

* L’elenco delle API obsolete identificate durante il controllo del codice è stato perfezionato per includere classi e metodi obsoleti aggiuntivi rilevati nelle versioni più aggiornate dell’SDK di Cloud Service.

* Il profilo SonarQube per Cloud Manager è stato aggiornato per rimuovere la regola Sonar squid:S2142. Non entrerà più in conflitto con i controlli di interruzione del thread.

* Ora l’interfaccia utente di Cloud Manager informa l’utente che temporaneamente potrebbe non essere possibile aggiungere/aggiornare il nome di dominio in quanto all’ambiente associato è collegata una pipeline in esecuzione o attualmente in attesa del passaggio di approvazione.

* Le proprietà impostate nei file `pom.xml` del cliente con prefisso sonar vengono ora rimosse dinamicamente, per evitare errori di build e del controllo di qualità.

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

### Data di rilascio {#release-date-ctt-feb}

La data di pubblicazione dello strumento Content Transfer v1.2.2 è il 1° febbraio 2021.

### Novità dello strumento Content Transfer {#what-is-new-ctt}

* Nuove funzionalità e interfaccia utente aggiunte allo strumento Content Transfer (Trasferimento contenuti) - Strumento di mappatura utenti. Questa funzione mappa automaticamente utenti e gruppi esistenti ai loro ID di sistema Adobe Identity Management come parte dell’attività di migrazione dei contenuti.
Vedi [Utilizzo dello strumento di mappatura utente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) per ulteriori dettagli.
* Lo strumento Content Transfer (Trasferimento contenuti) ora esegue la migrazione di tutti i gruppi e gli utenti a cui si fa riferimento nel set di migrazione, inclusi gli elementi figlio.
* Gli utenti possono selezionare alcuni percorsi in `/etc` durante la creazione dei set di migrazione.

## Analisi delle best practice {#best-practices-analyzer}

### Data di pubblicazione {#release-date-bpa}

La data di rilascio di Best Practices Analyzer v2.1.2 è il 18 febbraio 2021.

### Novità di Best Practices Analyzer {#what-is-new-bpa}

* Possibilità di rilevare l’utilizzo dell’implementazione di AEM Forms e AEM Forms e di indicare le aree rilevanti per la migrazione ad AEM Forms as a Cloud Service.
* Possibilità di rilevare e segnalare l’utilizzo e il numero di componenti e modelli personalizzati.
* Possibilità di rilevare il tipo di archivio nodi e di archivio dati utilizzati.
* Possibilità di rilevare l’utilizzo di Dynamic Medie.
* Possibilità di rilevare la versione Java utilizzata.

## Strumenti di refactoring del codice {#code-refactoring-tools}

### Novità degli strumenti di refactoring del codice {#what-is-new-crt}

* È stata rilasciata la nuova versione del plug-in AIO-CLI. La versione più recente di questo plug-in include diverse correzioni di bug per Repository Modernizer.
Per ulteriori informazioni su questo plug-in, consulta [Esperienza unificata](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html#benefits).

### Correzioni di bug {#bug-fixes-crt}

* Sono state apportate diverse correzioni di bug in Repository Modernizer.
Per ulteriori dettagli, consulta [Risorsa GitHub: aem-cloud-service-source-migration](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).
