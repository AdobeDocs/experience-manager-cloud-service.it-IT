---
title: Note sulla versione 2025.1.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service
description: Ulteriori informazioni sulla versione 2025.1.0 di Cloud Manager in AEM as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 613a5602706d4d0d63fce7a20bf52660d9a9d335
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 93%

---

# Note sulla versione 2025.1.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/pages/viewpage.action?pageId=3389843928 -->

Ulteriori informazioni sulla versione 2025.1.0 di Cloud Manager in AEM (Adobe Experience Manager) as a Cloud Service.

>[!NOTE]
>
>Consulta le [note sulla versione corrente di Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Date di pubblicazione {#release-date}

La data di pubblicazione per Cloud Manager 2025.1.0 in AEM as a Cloud Service è il 22 gennaio 2025.

La prossima pubblicazione è pianificata per il 13 febbraio 2025.


## Novità {#what-is-new}

* **Regole di qualità del codice - Aggiornamento del server SonarQube:** il passaggio Qualità del codice di Cloud Manager inizierà a utilizzare SonarQube Server 9.9 con la versione 2025.2.0 di Cloud Manager, pianificata per il 13 febbraio 2025.

  Per prepararti, le regole SonarQube aggiornate sono ora disponibili in [Regole di qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules).

  Puoi “verificare in anticipo” le nuove regole impostando la seguente variabile di testo della pipeline:

  `CM_BUILD_IMAGE_OVERRIDE` = `self-service-build:sonar-99-upgrade-java17or21`

  Inoltre, imposta la variabile seguente per garantire che il passaggio di qualità del codice venga eseguito per lo stesso commit (normalmente ignorato per lo stesso `commitId`):

  `CM_DISABLE_BUILD_REUSE` = `true`

![Pagina Configurazione variabili](/help/implementing/cloud-manager/release-notes/assets/variables-config.png)

>[!NOTE]
>
>Adobe consiglia di creare una nuova pipeline CI/CD per la qualità del codice, configurata sullo stesso ramo della pipeline di produzione principale. Imposta le variabili appropriate *prima* della versione del 13 febbraio 2025 per convalidare che le nuove regole applicate non introducano blocchi.

* **Supporto per la build di Java 17 e Java 21:** la clientela adesso può generare con Java 17 o Java 21, accedendo a miglioramenti delle prestazioni e a nuove funzioni del linguaggio. Per i passaggi di configurazione, incluso l’aggiornamento delle versioni del progetto Maven e della libreria, consulta [Ambiente di build](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md). Quando la versione della build è impostata su Java 17 o Java 21, il runtime distribuito è Java 21.

   * **Abilitazione della funzione**
      * Questa funzione verrà abilitata per tutta la clientela giovedì 13 febbraio 2025, in coincidenza con il rollout predefinito della nuova versione di SonarQube.
      * La clientela può abilitarlo *immediatamente* impostando le due configurazioni di variabili descritte in precedenza per l’aggiornamento alla versione 9.9 di SonarQube.

   * **Distribuzione runtime Java 21**
      * Il runtime di Java 21 viene distribuito durante la generazione con Java 17 o Java 21.
      * Il rollout graduale a tutti gli ambienti Cloud Manager inizia a febbraio per le sandbox e gli ambienti di sviluppo e verrà esteso agli ambienti di produzione ad aprile.
      * La clientela che genera con Java 11 e desidera adottare il runtime di Java 21 *precedente* può contattare Adobe all’indirizzo [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com).

* **“Configurazioni CDN” rinominate “Mappature di dominio”:** come parte dei miglioramenti dell’interfaccia utente in AEM Cloud Manager, l’etichetta “Configurazioni CDN” è ora rinominata “Mappature di dominio”. Questa modifica migliora l’allineamento terminologico con la funzionalità. <!-- CMGR-64738 -->

  ![“Configurazioni CDN” rinominate “Mappature di dominio” nell’interfaccia utente](/help/implementing/cloud-manager/release-notes/assets/domain-mappings.png)

* **Provisioning di un sito Edge Delivery con un clic:** Cloud Manager consente ora agli utenti con le autorizzazioni e le licenze appropriate di creare un sito Edge Delivery Services di esempio con un solo clic. Questo processo semplificato offre le seguenti funzionalità automatizzate:

   * **Integrazione GitHub**: crea automaticamente, all’interno di un’organizzazione esistente, un archivio GitHub preconfigurato con un modello standard per Edge Delivery Services.
   * **Installazione dell’app di sincronizzazione del codice AEM**: installa l’applicazione di sincronizzazione del codice AEM nell’archivio, garantendo la sincronizzazione e la distribuzione senza problemi.
   * **Configurazione della collaborazione sui contenuti:** collega una cartella di Google Drive designata per l’archiviazione dei contenuti, fornendo un ambiente collaborativo per la relativa gestione.
   * **Pubblicazione dei contenuti**: gli utenti possono ora pubblicare i contenuti per i siti con provisioning direttamente dall’interfaccia utente di Cloud Manager, semplificando i flussi di lavoro e migliorando l’efficienza.
   * **Collaborazione avanzata**: la piattaforma consente agli utenti di aggiungere più collaboratori alla cartella di archiviazione dei contenuti di Google Drive, semplificando il lavoro di squadra e i contributi ai contenuti.

  Questi miglioramenti mirano ad aumentare l’automazione, semplificare i processi di configurazione e valorizzare la collaborazione degli utenti di Edge Delivery Services. <!-- CMGR-59362 -->

  ![Provisioning di un sito Edge Delivery](/help/implementing/cloud-manager/release-notes/assets/eds-one-click-60.png)

  ![Finestra di dialogo Provisioning del sito Edge Delivery](/help/implementing/cloud-manager/release-notes/assets/eds-provision-60.png)

* **Supporto avanzato per i siti Edge Delivery Services:** Cloud Manager ora supporta l’onboarding dei siti Edge Delivery Services più recenti. Questo aggiornamento include un refactoring completo della rete CDN e dello stack di consegna, migliorando la robustezza e la manutenibilità.

* **Opzioni di filtro avanzate per le pipeline:** Cloud Manager ora nella pagina Pipeline include opzioni di filtro avanzate, che consentono di accedere rapidamente ai dati rilevanti e di migliorare l’efficienza della distribuzione. Alcune delle caratteristiche principali includono:

   * **Filtro con più criteri:** affina i risultati della ricerca con filtri quali il nome della pipeline, l’ambiente e il codice di distribuzione.
   * **Ricerca semplificata delle pipeline:** individua facilmente pipeline specifiche per velocizzare la navigazione e migliorare la gestione del flusso di lavoro.

  Nel complesso, questi miglioramenti rendono la gestione e l’implementazione delle pipeline più efficienti e di facile utilizzo.

  ![Funzionalità filtri pipeline](/help/implementing/cloud-manager/release-notes/assets/pipeline-filters.png)

* **Configurazione CDN self-service per il servizio Edge Delivery:** i nuovi utenti che utilizzano il servizio Edge Delivery ora possono configurare la propria rete CDN in modo indipendente tramite Cloud Manager. Questo aggiornamento estende il supporto da `.hlx.page/live` al nuovo `.aem.page/live`, fornendo maggiore flessibilità e una configurazione semplificata per gli utenti.

## Programma per i primi utilizzatori {#early-adoption}

Partecipa al programma per i primi utilizzatori di Cloud Manger e concediti la possibilità di testare le prossime funzionalità.

* **Aggiornamento del programma per i primi utilizzatori, supporto della convalida PR per Bitbucket e GitLab:** Cloud Manager ora supporta la convalida della richiesta di pull (PR) per le versioni Cloud e self-hosted di Bitbucket e GitLab. Questa funzionalità consente ai clienti di testare le modifiche al codice in base alle soglie di qualità del codice di Adobe prima di unire una PR. Garantendo una qualità del codice più elevata prima dell’unione, questo miglioramento aumenta in modo significativo la percentuale di modifiche del codice nelle pipeline di produzione, riducendo i tempi di commercializzazione e semplificando i flussi di lavoro di sviluppo.

  Per ulteriori informazioni su “Bring Your Own Git”, ora con supporto per GitLab e Bitbucket, e per iscriverti come primo utilizzatore, consulta le [note sulla versione di ottobre 2024 di Cloud Manager](/help/implementing/cloud-manager/release-notes/2024/2024-10-0.md##gitlab-bitbucket).

* **Ambiente di test avanzato:** soluzione appositamente progettata per colmare il divario tra sviluppo e produzione. Personalizzato per le esigenze aziendali, questo ambiente replica le specifiche a livello di produzione per supportare test di accettazione utente (UAT) accurati e valutazioni approfondite delle prestazioni.

  Se ti interessa partecipare al programma Early Adopter, [completa questo modulo](https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Furldefense.com%2Fv3%2F__https%3A%2Fwww.feedbackprogram.adobe.com%2Fh%2Fs%2F6N425LYG1jQ1Nc0F20Zllt__%3B!!OgNkHJCYlf_CHg!fIp-QrZ9si3kcUIjRCniEzqAAa8FcU1iN34SGQFtlcQ36eUQXOZWbDHP7oZajqddgpuOMAVL5CQpkZ6ths76Qks8%24&amp;data=05%7C02%7Cpanchapa%40adobe.it%7Cf81bcaa4b20544f1818b08dccd07c78c%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638610680502164019%7CUnknown%7CTWFpbGZsb3d8eyJoiMC4wLjAwMDAiLCJQIjoiV2luMzIi LCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=aGo6zz2ldPrta4lpvo3CLNENR5ghHDDCPbG1adUaNZQ%3D&amp;reserv=0) e invia un&#39;e-mail a [earlyadopter_cs_advtestenvironment@adobe.com](mailto:earlyadopter_cs_advtestenvironment@adobe.com) con il tuo `OrgID`.



<!-- ## Bug fixes -->




<!-- ## Known issues {#known-issues} -->
