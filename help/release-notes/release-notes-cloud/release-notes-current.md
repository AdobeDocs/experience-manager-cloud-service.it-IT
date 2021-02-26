---
title: Note sulla versione corrente per  [!DNL Adobe Experience Manager] come Cloud Service.
description: Note sulla versione corrente per  [!DNL Adobe Experience Manager] come Cloud Service.
translation-type: tm+mt
source-git-commit: a93db92689928a900662a39b11bb5a7ea9724e62
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 4%

---


# Note sulla versione per [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

Nella sezione seguente sono riportate le note generali sulla versione relative a [!DNL Experience Manager] come Cloud Service.

## Data di rilascio {#release-date}

La data di rilascio per [!DNL Adobe Experience Manager] come Cloud Service 2021.2.0 è il 25 febbraio 2021.
La seguente release (2021.3.0) sarà del 25 marzo 2021.

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

## Novità in [!DNL Assets] {#what-is-new-assets}

* In [!DNL Brand Portal] viene introdotta una nuova impostazione di download che consente di creare una cartella separata per ogni risorsa quando si scaricano cartelle, raccolte e così via. vedere [impostazioni di download](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html).

<!-- TBD: refine this list of features and enh. for Feb release.

Customers using the Connected Assets feature can now easily view and track assets used on remote Sites instances. This affords customers a complete view of being used across all Sites powered pages, allowing for better tracking, management, and brand consistency.  -->

## Correzioni di bug in [!DNL Assets] {#bug-fixes-assets}

* Quando viene creata una nuova versione di una risorsa esistente dopo la risoluzione del conflitto di denominazione, i metadati della risorsa originale vengono sovrascritti. (CQ-4313594)
* Quando viene stampata una risorsa con testo di annotazione lungo, il testo dell’annotazione viene troncato, anche se è disponibile spazio. (CQ-4314101)
* Quando sono selezionate più risorse per aggiornare le proprietà, talvolta si verifica un errore o le proprietà di una risorsa deselezionata vengono aggiornate. (CQ-4316532)
* Quando si tenta di aprire la [!UICONTROL Barra di ricerca Amministratore risorse], la pagina rimane vuota e facendo clic su [!UICONTROL Edit] > [!UICONTROL Settings] viene generato un errore. (CQ-4315079)

## Cloud Manager {#cloud-manager}

### Data di rilascio {#release-date-cm}

La data di rilascio per Cloud Manager in AEM come Cloud Service 2021.2.0 è l’11 febbraio 2021.

### Novità {#what-is-new-cloud-manager}


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

## Strumento Content Transfer (Trasferimento contenuti) {#content-transfer-tool}

### Data di rilascio {#release-date-ctt}

La Data di rilascio per lo strumento di trasferimento dei contenuti v1.2.4 è il 10 febbraio 2021.

### Correzioni di bug {#bug-fixes-ctt}

* Quando si mappavano più utenti, alcuni ID IMS degli utenti venivano mappati in modo non corretto. Questo è stato corretto.

### Data di rilascio {#release-date-ctt-feb}

La Data di rilascio per lo strumento di trasferimento dei contenuti v1.2.2 è il 10 febbraio 2021.

### Novità in Content Transfer Tool {#what-is-new-ctt}

* Nuove funzionalità e interfaccia utente aggiunte a Content Transfer Tool - Strumento di mappatura utente. Questa funzione mappa automaticamente gli utenti e i gruppi esistenti al loro Adobe   ID di sistema Identity Management nell’ambito dell’attività di migrazione dei contenuti.
Per ulteriori informazioni, fare riferimento a [Utilizzo dello strumento di mappatura utente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html).
* Content Transfer Tool ora esegue la migrazione di tutti i gruppi e gli utenti a cui viene fatto riferimento nel set di migrazione, inclusi gli elementi figlio.
* Gli utenti possono selezionare alcuni percorsi in `/etc` al momento della creazione dei set di migrazione.

## Best practice Analyzer {#best-practices-analyzer}

### Data di rilascio {#release-date-bpa}

La data di rilascio per Best Practices Analyzer v2.1.2 è il 18 febbraio 2021.

### Novità in Best Practices Analyzer {#what-is-new-bpa}

* Possibilità di rilevare l&#39;utilizzo &#39;implementazione di AEM Forms e  AEM Forms e indicare le aree rilevanti per la migrazione  AEM Forms come Cloud Service.
* Possibilità di rilevare e segnalare l’utilizzo e il conteggio dei componenti e dei modelli personalizzati.
* Possibilità di rilevare il tipo di archivio nodi e di archivio dati utilizzato.
* Possibilità di rilevare l’utilizzo di Dynamic Media.
* Possibilità di rilevare la versione Java utilizzata.

## Strumenti di refactoring del codice {#code-refactoring-tools}

### Novità in Strumenti di refactoring del codice {#what-is-new-crt}

* Nuova versione del plugin AIO-CLI rilasciata. La versione più recente di questo plug-in include diverse correzioni di bug per Repository Modernizer.
Per ulteriori informazioni su questo plug-in, fare riferimento a [Unified Experience](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits).

### Correzioni di bug {#bug-fixes-crt}

* Diverse correzioni di bug eseguite su Repository Modernizer.
Fare riferimento a [Risorsa GitHub: aem-cloud-service-source-migration](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) per ulteriori dettagli.








