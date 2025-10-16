---
title: Note sulla versione 2025.10.0 di Cloud Manager
description: Scopri la versione 2025.10.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 302248ade67683712bf1895fd8dfdd8853aae1ac
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 56%

---

# Note sulla versione 2025.10.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

Scopri la versione 2025.10.0 di Cloud Manager in AEM (Adobe Experience Manager) as a Cloud Service.

Consulta anche le [note sulla versione corrente di Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Date di pubblicazione {#release-date}

La versione 2025.10.0 di Cloud Manager in AEM as a Cloud Service è stata rilasciata il venerdì 2 ottobre 2025.

La prossima versione è pianificata per il venerdì 6 novembre 2025.

## Novità {#what-is-new}

* **Pipeline di distribuzione dedicate solo per la fase e solo per la produzione**

  Cloud Manager offre ora pipeline di distribuzione dedicate solo per lo staging e per la sola produzione, garantendo maggiore flessibilità per la gestione indipendente delle distribuzioni negli ambienti di staging e produzione. Consulta [Pipeline suddivise solo per staging e solo produzione](/help/implementing/cloud-manager/configuring-pipelines/stage-prod-only.md).

* **Servizio di valutazione dell&#39;integrità cloud di AEM**

  Adobe presenta AEM Cloud Health Assessment Service, uno strumento di controllo automatizzato e non invasivo che mantiene l’ambiente AEM as a Cloud Service ottimizzato, sicuro e allineato con le best practice.

  Questo servizio esegue le seguenti operazioni:

   * Esegue la scansione degli ambienti per individuare colli di bottiglia delle prestazioni, inefficienze e rischi potenziali.
   * Analizza le strutture dei contenuti (blueprint, Live Copy) e le configurazioni personalizzate.
   * Identifica le dipendenze obsolete (AEM SDK, librerie di terze parti).
   * Segnala i problemi di qualità del codice (annotazioni non corrette, modelli inefficienti).
   * Fornisce indicazioni actionable tramite dashboard come **Centro azioni**.
   * Supporta l’ottimizzazione proattiva tramite il rilevamento e la risoluzione tempestivi dei problemi.

  I team possono monitorare e migliorare continuamente gli ambienti AEM per garantire prestazioni più fluide, maggiore sicurezza e manutenibilità a lungo termine.

  Consulta [Valutazione dello stato per gli ambienti di produzione e staging](/help/implementing/cloud-manager/reports/report-health-assessment.md).

* **Supporto pipeline di configurazione**

  Le pipeline di configurazione sono ora supportate per i siti creati con Edge Delivery Services, espandendo questa funzionalità oltre i singoli ambienti Cloud Service. Puoi utilizzare **Pipeline di configurazione** per gestire impostazioni quali la configurazione CDN, incluse le regole del filtro del traffico e i selettori di origine. Consulta le [configurazioni supportate](/help/operations/config-pipeline.md#configurations).

  Le pipeline di configurazione di Edge Delivery supportano anche i segreti tramite le variabili della pipeline di Cloud Manager.

  Consulta [Aggiungere pipeline Edge Delivery](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md).

* **Finestra di dialogo di configurazione di Domain Mapping-CDN semplificata**

  Cloud Manager ha semplificato il flusso **Mappa dominio su CDN** per ridurre confusione e velocizzare la configurazione. La finestra di dialogo ora enfatizza **CDN gestita da Adobe** (con un badge &quot;Consigliato&quot;).

  ![Finestra di dialogo Mappa dominio su rete CDN con il pulsante di opzione CDN gestita da Adobe selezionato](/help/implementing/cloud-manager/assets/cdn/map-domain-to-cdn-dialog-box-adobe-managed-cdn.png).

  Vedere [Aggiungere un mapping di dominio](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md).

  La finestra di dialogo presenta anche un elenco di controllo singolo e conciso per la scheda **Altro provider CDN**, incentrato sul contenuto informativo con i seguenti elementi:

   * Puntare l&#39;origine CDN a `publish-p<PROGRAM_ID>-e<ENV_ID>.adobeaemcloud.com`.
   * Imposta **Host/SNI** per inoltrare l&#39;host originale.
   * Aggiungi `X-AEM-Edge-Key` (dopo la distribuzione della chiave in Cloud Manager).
   * Imposta `X-Forwarded-Host` sul tuo dominio rivolto al cliente.
   * Cancella altre intestazioni `X-Forwarded-*` prima di raggiungere AEM.

  ![Finestra di dialogo Mappa dominio su rete CDN con il pulsante di scelta Altro provider CDN selezionato](/help/implementing/cloud-manager/assets/cdn/map-domain-to-cdn-dialog-box-other-cdn-provider.png)

  <!-- (no redundant `Origin` field or "Learn more" clutter) -->Il piè di pagina allegato fornisce due collegamenti utili: configurazioni di esempio per le CDN principali e un collegamento alla documentazione completa. Un singolo pulsante di conferma-Ho configurato la rete CDN-completa il flusso.

  Vedi [CDN in AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md#point-to-point-CDN).

<!--
### Staging-Only and Production-Only Pipelines {#staging-production-only-pipelines}

Support for [staging-only and production-only pipelines](/help/implementing/cloud-manager/configuring-pipelines/stage-prod-only.md) has been introduced, enabling you to split full-stack production deployment pipelines into smaller, specialized deployments.

If you are interested in testing this new feature and sharing your feedback, send an email to  `Grp-cloudmanager_splitpipelines@adobe.com` from your email address associated with your Adobe ID. -->


## Programmi Beta {#private-beta-program}

Partecipa al programma Beta privato di Cloud Manager per ottenere un accesso esclusivo alle funzioni in arrivo prima del rilascio generale.

Sono attualmente disponibili le seguenti opportunità:
<!--
### Support for Custom Author Domains in Cloud Service

AEM Cloud Service is going to soon support one custom domain per Author environment.-->

### Estensibilità e personalizzazione di Experience Hub {#exp-hub-extensibility}

[Experience Hub](/help/experience-hub.md) funge da punto di ingresso ad AEM, personalizzato in base alle esigenze della tua organizzazione. Comunica ad Adobe le tue estensioni dell’interfaccia utente di AEM esistenti in modo che possano aiutarti ad abilitarle in Experience Hub con il minimo sforzo.

![Diagramma del flusso di lavoro di estensibilità e personalizzazione di Experience Hub](/help/implementing/cloud-manager/release-notes/assets/experience-hub-extensibility-customization.png)

Incorpora esperienze personalizzate in Experience Hub per estendere e personalizzare il dashboard della tua organizzazione. Oltre ai widget incorporati di Adobe, aggiungi quelli personalizzati utilizzando il framework [UI Extensibility](https://developer.adobe.com/uix/docs/). Crea app dell’interfaccia utente basate su JavaScript e mostrale agli utenti per soddisfare requisiti e flussi di lavoro specifici per le aziende.

Ti interessa la versione beta? Invia un&#39;e-mail a [beta_exphubextensibility@adobe.com](mailto:beta_exphubextensibility@adobe.com) con il tuo OrgID Adobe e una breve descrizione della personalizzazione che intendi creare.

### Build più veloci con il caching dei moduli {#quick-build-cm-pipelines}

Un nuovo modello di build compila solo i moduli modificati (anziché l’intero archivio) utilizzando la memorizzazione nella cache a livello di modulo per ridurre i tempi di build. Si applica alle pipeline di qualità del codice, full stack e solo stage.

![Finestra di dialogo Modifica pipeline non di produzione che mostra le due opzioni della strategia di compilazione, ovvero Build completa e Build avanzata](/help/implementing/cloud-manager/release-notes/assets/non-production-pipeline-edit.png) *Finestra di dialogo Modifica pipeline non di produzione che mostra le due opzioni della strategia di compilazione, ovvero Build completa e Build avanzata.*

Nella finestra di dialogo **Aggiungi/Modifica pipeline**, nella scheda **Codice Source**, una nuova sezione **Strategia di compilazione** consente di scegliere una delle seguenti opzioni di compilazione:

* **Build completa**: crea tutti i moduli nell&#39;archivio a ogni esecuzione.
* **Smart Build**: crea solo i moduli che sono cambiati dall&#39;ultimo commit, riducendo così il tempo di compilazione complessivo.

Puoi controllare quali pipeline utilizzano **Smart build**. Durante la versione beta, questa opzione viene visualizzata solo per le pipeline **Qualità codice** e **Distribuzione sviluppatore**.

Interessato? Invia un&#39;e-mail a [beta_quickbuild_cmpipelines@adobe.com](mailto:beta_quickbuild_cmpipelines@adobe.com) con il tuo ID organizzazione e l&#39;ID programma di Adobe.

<!-- You can deactivate incremental builds at the pipeline level by setting the property `CM_BUILD_DISABLE_MODULE_CACHING` to `true` (effective during the `BUILD` step). For how to add pipeline variables, see [Pipeline Variables in Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md).-->



### Rollback con un solo clic per le implementazioni di pipeline {#one-click-rollback}

Ripristino rapido a un’implementazione precedente se il codice di origine più recente del cliente non funziona come previsto: non è necessario eseguire nuovamente la pipeline completa o ripristinare manualmente i commit.<!--https://jira.corp.adobe.com/browse/CMGR-69556 -->

![Ripristina il codice di origine del cliente dalla scheda Ambienti](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed.png) *Nella scheda Ambienti precedente è visualizzata l’opzione **Ripristina**>**Codice precedente implementato**per un ambiente selezionato.*

![Finestra di dialogo Ripristina codice precedente implementato](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed-dialogbox.png)
*Nella finestra di dialogo **Ripristina codice precedente implementato**, controlla la versione attualmente implementata e quella che desideri ripristinare, quindi fai clic su **Conferma***.

![Ripristino dell’attivazione](/help/implementing/cloud-manager/release-notes/assets/restoring-previous-code-deployed-restoring.png)
*Cloud Manager ripristina l’ambiente alla versione precedente, mantiene intatti il contenuto e la configurazione e contrassegna l’ambiente **Ripristino**fino al completamento dell’implementazione.*

![Versione del codice di origine in uso](/help/implementing/cloud-manager/release-notes/assets/environments-view-details-sourcecodeversion.png) *La visualizzazione dei dettagli dell’ambiente, come illustrato in precedenza, mostra ora anche la versione del codice di origine attiva in uso.*

Se ti interessa testare questa nuova funzione e condividere il tuo feedback, invia un’e-mail a [restorecode@adobe.com](mailto:restorecode@adobe.com) dall’indirizzo e-mail associato al tuo Adobe ID.

Consulta [Ripristinare il codice precedente distribuito in AEM as a Cloud Service](/help/operations/restore-previous-code-deployed.md).

Consulta anche [Ripristino dei contenuti in AEM as a Cloud Service](/help/operations/restore.md).

### Ambiente di test specializzato {#specialized-test-environment}

Cloud Manager ora supporta l’aggiunta di un nuovo tipo di ambiente denominato **Ambiente di test specializzato**. L’ambiente è progettato per aiutare i team a convalidare le funzioni in condizioni prossime alla produzione prima della pubblicazione. Questo tipo di ambiente è diverso dagli ambienti *Produzione + Fase*, *Sviluppo* o *Sviluppo rapido* e offre uno spazio mirato per l’esecuzione di scenari di convalida avanzati.

**Miglioramenti recenti**

* Ora puoi configurare ambienti di test specializzati su una pipeline non di produzione tramite un flusso di lavoro più semplice e intuitivo. La configurazione semplificata accelera il completamento e riduce gli errori di configurazione.
* **Copia contenuto** è ora supportato in ambienti di test specializzati. È ora possibile eseguire **Copia contenuto** in modo sicuro in ambienti di test isolati che rispecchiano la produzione. <!-- (CMGR‑68900) -->

Consulta [Aggiungere un ambiente di test specializzato](/help/implementing/cloud-manager/specialized-test-environment.md).

![Finestra di dialogo Aggiungi ambiente con il pulsante di scelta Ambiente di test specializzato selezionato](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

>[!NOTE]
>
>Adobe ha chiuso le richieste di accesso in versione beta per gli ambienti di test specializzati, avendo raggiunto un numero sufficiente di partecipanti. La funzione è ora in preparazione per la disponibilità generale.

<!--
If you are interested in testing this new feature and sharing your feedback, send an email to [grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com) from your email address associated with your Adobe ID. -->


### Integra il tuo Git personale (BYOG) {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

Ora è possibile portare in Cloud Manager i propri archivi Git Azure DevOps, con supporto per i nuovi archivi Azure DevOps e gli archivi legacy VSTS (Visual Studio Team Services).

* Per chi usa Edge Delivery Services, l’archivio di cui è stato eseguito l’onboarding può essere utilizzato per sincronizzare e distribuire il codice del sito.
* Per chi usa AEM as a Cloud Service e Adobe Managed Services (AMS), l’archivio può essere collegato sia a pipeline full stack che front-end.

Verranno presto introdotti anche il supporto di ulteriori tipi di pipeline e la convalida di richieste pull tramite pipeline per la qualità del codice.

Consulta [Aggiungere archivi esterni in Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Finestra di dialogo Aggiungi archivio](/help/implementing/cloud-manager/release-notes/assets/azure-repo.png)

<!-- If you are interested in testing this new feature and sharing your feedback, send an email to [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) from your email address associated with your Adobe ID. Be sure to include which Git platform you want to use and whether you are on a private/public or enterprise repository structure. -->

**Domande frequenti su BYOG**

| Domanda | Risposta |
|---|---|
| *Come può un progetto tornare all’archivio Git gestito da Adobe, se necessario?* | Tornare indietro è semplice. [Aggiorna le pipeline](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) in modo che puntino all’archivio Adobe e rimuovi l’archivio esterno se non è più necessario. |
| *È possibile configurare archivi diversi per ambienti diversi (ad esempio, non di produzione o di produzione) per consentire prima il test in ambienti non di produzione?* | Sì, è possibile configurare archivi diversi per ambienti separati. Ad esempio, la pipeline di sviluppo o di qualità del codice può puntare a un archivio esterno mentre la pipeline di produzione rimane connessa all’archivio Adobe. Assicurati che il processo di sincronizzazione tra i due archivi rimanga attivo durante questa configurazione. |
| *Le impostazioni esistenti come gli elenchi `IP Allow` continuano a funzionare?* | Sì, gli elenchi `IP Allow` esistenti continuano a funzionare come di consueto. Tuttavia, se l’archivio Git esterno è protetto da un firewall, gli [Indirizzi IP Adobe necessari devono essere aggiunti all’elenco consentiti](/help/implementing/cloud-manager/ip-allow-lists/introduction.md). |
| *Funzionano tutti gli URL dell’archivio GitLab? L’URL dell’archivio in uso segue il formato `https://gitlab_dedicated_url.com/path/repo-name.git`, che differisce dall’esempio riportato nella documentazione.* | Sì, è supportato qualsiasi archivio GitLab che supporta API V3 o V4, inclusi gli URL GitLab con hosting autonomo come quelli descritto in [Aggiungere archivi esterni in Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md) (`https://git-vendor-name.com/org-name/repo-name.git`). |


#### Gestisci token di accesso{#manage-access-tokens}

Utilizza **Gestisci token di accesso** in Cloud Manager per visualizzare, rinominare ed eliminare i token di accesso associati agli archivi BYOG esterni, ad esempio GitHub Enterprise, GitLab, Bitbucket e Azure DevOps.

Consulta [Gestisci token di accesso](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md).

<!-- If you are interested in testing this new feature and sharing your feedback, send an email to [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) from your email address associated with your Adobe ID. -->


## Correzioni di bug {#bug-fixes}

Non vi sono correzioni di bug significativi nella versione di ottobre di Cloud Manager.


<!-- ## Known issues {#known-issues} -->

