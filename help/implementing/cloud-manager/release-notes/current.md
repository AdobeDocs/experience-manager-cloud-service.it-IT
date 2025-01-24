---
title: Note sulla versione 2025.1.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service
description: Ulteriori informazioni sulla versione 2025.1.0 di Cloud Manager in AEM as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 9850a52626c2bd80f7528931d23691dff1dd3eb2
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 10%

---

# Note sulla versione 2025.1.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/pages/viewpage.action?pageId=3389843928 -->

Ulteriori informazioni sulla versione 2025.1.0 di Cloud Manager in AEM (Adobe Experience Manager) as a Cloud Service.

>[!NOTE]
>
>Consulta le [note sulla versione corrente di Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Date di pubblicazione {#release-date}

La data di rilascio per Cloud Manager 2025.1.0 in AEM as a Cloud Service è mercoledì 22 gennaio 2025.

La prossima versione è pianificata per il venerdì 13 febbraio 2025.


## Novità {#what-is-new}

* **Regole di qualità del codice - Aggiornamento del server SonarQube:** il passaggio Qualità del codice di Cloud Manager inizierà a utilizzare SonarQube Server 9.9 con la versione 2025.2.0 di Cloud Manager, pianificata per giovedì 13 febbraio 2025.

  Per preparare, le regole SonarQube aggiornate sono ora disponibili in [Regole per la qualità del codice](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules).

  Puoi &quot;verificare anticipatamente&quot; le nuove regole impostando la seguente variabile di testo della pipeline:

  `CM_BUILD_IMAGE_OVERRIDE` = `self-service-build:sonar-99-upgrade-java17or21`

  Inoltre, impostare la variabile seguente per garantire che il passaggio di qualità del codice venga eseguito per lo stesso commit (normalmente ignorato per lo stesso `commitId`):

  `CM_DISABLE_BUILD_REUSE` = `true`

![Pagina Configurazione variabili](/help/implementing/cloud-manager/release-notes/assets/variables-config.png)

>[!NOTE]
>
>Adobe consiglia di creare una nuova pipeline CI/CD Code Quality, configurata sullo stesso ramo della pipeline di produzione principale. Imposta le variabili appropriate *prima* della versione del 13 febbraio 2025 per verificare che le nuove regole applicate non introducano blocchi.

* Supporto per la compilazione di **Java 17 e Java 21:** I clienti possono ora creare con Java 17 o Java 21, accedendo a miglioramenti delle prestazioni e a nuove funzioni del linguaggio. Per i passaggi di configurazione, incluso l&#39;aggiornamento delle versioni del progetto Maven e della libreria, consulta [Ambiente di build](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md). Quando la versione della build è impostata su Java 17 o Java 21, il runtime distribuito è Java 21.

   * **Abilitazione funzionalità**
      * Questa funzione verrà abilitata per tutti i clienti giovedì 13 febbraio 2025, in coincidenza con il rollout predefinito della nuova versione di SonarQube.
      * I clienti possono abilitarlo *immediatamente* impostando le due configurazioni di variabili descritte in precedenza per l&#39;aggiornamento della versione 9.9 di SonarQube.

   * **Distribuzione runtime Java 21**
      * Il runtime Java 21 viene distribuito durante la generazione con Java 17 o Java 21.
      * Il rollout graduale a tutti gli ambienti Cloud Manager inizia a febbraio per le sandbox e gli ambienti di sviluppo e si estende agli ambienti di produzione in aprile.
      * I clienti che creano con Java 11 e desiderano adottare il runtime Java 21 *precedente* possono contattare Adobe all&#39;indirizzo [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com).

* **&quot;Configurazioni CDN&quot; rinominate &quot;Mapping dominio&quot;:** Come parte dei miglioramenti dell&#39;interfaccia utente in AEM Cloud Manager, l&#39;etichetta &quot;Configurazioni CDN&quot; è ora rinominata &quot;Mapping dominio&quot;. Questa modifica migliora l’allineamento terminologico con la funzionalità. <!-- CMGR-64738 -->

  ![&quot;Configurazioni CDN&quot; rinominate &quot;Mapping dominio&quot; nell&#39;interfaccia utente](/help/implementing/cloud-manager/release-notes/assets/domain-mappings.png)

* **Effettuare il provisioning di un sito Edge Delivery con un clic:** Cloud Manager consente ora agli utenti con le autorizzazioni e le licenze appropriate di creare un sito Edge Delivery Services di esempio con un solo clic. Questo processo semplificato offre le seguenti funzionalità automatizzate:

   * **Integrazione GitHub**: crea automaticamente un archivio GitHub all&#39;interno di un&#39;organizzazione esistente, preconfigurato con un modello standard per i Edge Delivery Services.
   * **Installazione dell&#39;app di sincronizzazione del codice AEM** - Installa l&#39;applicazione di sincronizzazione del codice AEM nell&#39;archivio, garantendo la sincronizzazione e la distribuzione senza problemi.
   * **Configurazione del Collaboration dei contenuti** - Collega una cartella di Google Drive designata per l&#39;archiviazione dei contenuti, fornendo un ambiente collaborativo per la gestione dei contenuti.
   * **Pubblicazione dei contenuti** - Gli utenti possono ora pubblicare i contenuti per i siti con provisioning direttamente dall&#39;interfaccia utente di Cloud Manager, semplificando i flussi di lavoro e migliorando l&#39;efficienza.
   * **Collaboration avanzato** - La piattaforma consente agli utenti di aggiungere più collaboratori alla cartella di archiviazione dei contenuti di Google Drive, semplificando il lavoro di squadra e i contributi ai contenuti.

  Questi miglioramenti mirano a migliorare l’automazione, semplificare i processi di configurazione e migliorare la collaborazione per gli utenti dei Edge Delivery Services. <!-- CMGR-59362 -->

  ![Provisioning di un sito Edge Delivery](/help/implementing/cloud-manager/release-notes/assets/eds-one-click-60.png)

  ![Finestra di dialogo Provisioning sito Edge Delivery](/help/implementing/cloud-manager/release-notes/assets/eds-provision-60.png)

* **Supporto avanzato per i siti Edge Delivery Services:** Cloud Manager ora supporta l&#39;onboarding per i siti Edge Delivery Services più recenti. Questo aggiornamento include un refactoring completo della rete CDN e dello stack di consegna, che migliora la robustezza e la manutenibilità.

* **Aggiornamento anticipato del programma Adopter - Supporto della convalida PR per Bitbucket e GitLab:** Cloud Manager ora supporta la convalida della richiesta di pull (PR) per le versioni Cloud e self-hosted di Bitbucket e GitLab. Questa funzione consente ai clienti di testare le modifiche al codice in base alle soglie di qualità del codice di Adobe prima di unire una PR. Garantendo una qualità del codice più elevata prima dell’unione, questo miglioramento migliora in modo significativo la percentuale di modifiche del codice nelle pipeline di produzione, riducendo i tempi di commercializzazione e semplificando i flussi di lavoro di sviluppo.

* **Opzioni di filtro avanzate per le pipeline:** Cloud Manager ora include opzioni di filtro avanzate nella pagina Pipeline, che consentono di accedere rapidamente ai dati rilevanti e migliorare l&#39;efficienza della distribuzione. Alcune delle caratteristiche principali includono:

   * **Filtro con più criteri:** Affina i risultati della ricerca con filtri quali il nome della pipeline, l&#39;ambiente e il codice di distribuzione.
   * **Ricerca semplificata delle pipeline:** Individua facilmente pipeline specifiche per velocizzare la navigazione e migliorare la gestione del flusso di lavoro.

  Nel complesso, questi miglioramenti rendono la gestione e l’implementazione delle pipeline più efficienti e di facile utilizzo.

  ![Funzionalità filtri pipeline](/help/implementing/cloud-manager/release-notes/assets/pipeline-filters.png)

* **Configurazione CDN self-service per il servizio Edge Delivery:** I nuovi utenti che utilizzano il servizio Edge Delivery ora possono configurare la propria rete CDN in modo indipendente tramite Cloud Manager. Questo aggiornamento estende il supporto da `.hlx.page/live` al nuovo `.aem.page/live`, fornendo maggiore flessibilità e una configurazione semplificata per gli utenti.


<!-- ## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features. -->

<!-- ## Bug fixes -->




<!-- ## Known issues {#known-issues} -->
