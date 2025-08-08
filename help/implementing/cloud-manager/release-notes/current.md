---
title: Note sulla versione 2025.8.0 di Cloud Manager
description: Scopri la versione 2025.8.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: c465542d5e89dbae0eb1c380ca1e7756d0beb2b6
workflow-type: tm+mt
source-wordcount: '1308'
ht-degree: 59%

---

# Note sulla versione 2025.8.0 di Cloud Manager in Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

Scopri la versione 2025.8.0 di Cloud Manager in AEM (Adobe Experience Manager) as a Cloud Service.

Consulta anche le [note sulla versione corrente di Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Date di pubblicazione {#release-date}

La versione 2025.8.0 di Cloud Manager in AEM as a Cloud Service è stata rilasciata il venerdì 7 agosto 2025.

La prossima versione è pianificata per il venerdì 4 settembre 2025.

## Novità {#what-is-new}

* **La licenza Edge Delivery Services può essere inclusa in un programma HIPAA in modo autonomo**

  Le organizzazioni che necessitano di assistenza sanitaria o di dati sensibili possono ora utilizzare Edge Delivery Services in modo autonomo, garantendo la conformità HIPAA ai severi standard normativi. <!-- CMGR-70016 -->

* **BYOG è ora disponibile per Edge Delivery Services**

  Cloud Manager ora consente di configurare archivi Git esterni, abilitando flussi di lavoro flessibili per la gestione del codice. <!--(CMGR‑69010, CMGR‑70988) --> Consente inoltre di estrarre il codice da un ramo scelto direttamente nell&#39;interfaccia utente di Cloud Manager, riducendo le attività manuali dell&#39;archivio. Vedi [Configurare il sito Edge Delivery per l&#39;utilizzo di un archivio Git esterno](/help/implementing/cloud-manager/edge-delivery/config-edge-delivery-site-with-byog.md) <!-- (CMGR‑68085)(CMGR-69015) --> <!-- KT: https://wiki.corp.adobe.com/display/DMSArchitecture/%5B2025%5D+Cloud+Manager+-+Bring+Your+Own+Git+with+EDS -->

* **Provisioning automatico per il nuovo componente aggiuntivo Forms**

  I clienti che utilizzano solo Sites hanno spesso bisogno di un modo leggero e a basso costo per creare moduli di marketing. Il nuovo componente aggiuntivo AEM Forms Sites soddisfa tale esigenza aggiungendo funzionalità Forms limitate a un programma Sites. Inoltre, crea un chiaro percorso di aggiornamento all’offerta completa di AEM Forms. <!-- (CMGR-64301) --> <!-- KT: CMGR Provisioning Support for AEM Forms Sites Add-On SKU https://wiki.corp.adobe.com/pages/viewpage.action?pageId=3578379797 -->

  Componente aggiuntivo:
   * Si collega a un programma Sites e viene distribuito insieme a esso, senza alcun programma Forms separato o diritto.
   * Sono indirizzati a casi di utilizzo semplici per moduli di marketing.
   * Viene visualizzato nell&#39;elenco **Soluzioni e componenti aggiuntivi** durante la creazione del programma di produzione o la modifica del programma di produzione, solo quando l&#39;organizzazione IMS dispone di licenze aggiuntive Forms disponibili.

     ![Componenti aggiuntivi per Forms](/help/implementing/cloud-manager/release-notes/assets/forms-add-on.png) *Il componente aggiuntivo per Forms può essere aggiunto al programma solo se le licenze dei componenti aggiuntivi per Forms sono disponibili nella tua organizzazione IMS.*

     ![Componente aggiuntivo Forms in soluzioni e componenti aggiuntivi durante la creazione di un programma di produzione](/help/implementing/cloud-manager/release-notes/assets/forms-add-on-creating-production-program.png) *Durante la creazione del programma, è possibile selezionare il componente aggiuntivo Forms nella soluzione Sites.*

     ![Componente aggiuntivo Forms durante la modifica di un programma di produzione](/help/implementing/cloud-manager/release-notes/assets/forms-add-on-editing-production-program.png) *In **Modifica programma**, selezionare il componente aggiuntivo Forms per il programma Sites, quindi eseguire la pipeline per attivarlo negli ambienti.*

     Per ulteriori informazioni, vedere [Creare un programma di produzione](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md).

## Programmi Beta {#private-beta-program}

Partecipa ai programmi beta di Cloud Manager per avere accesso esclusivo alle prossime funzionalità prima del rilascio generale.

Sono attualmente disponibili le seguenti opportunità:

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

* Ora puoi configurare un ambiente di test specializzato su una pipeline non di produzione tramite un flusso di lavoro più semplice e intuitivo. La configurazione semplificata accelera il completamento e riduce gli errori di configurazione.
* **Copia contenuto** è ora supportato in ambienti di test specializzati. È ora possibile eseguire **Copia contenuto** in modo sicuro in ambienti di test isolati che rispecchiano la produzione. <!-- (CMGR‑68900) -->

Consulta [Aggiungere un ambiente di test specializzato](/help/implementing/cloud-manager/specialized-test-environment.md).

![Finestra di dialogo Aggiungi ambiente con il pulsante di scelta Ambiente di test specializzato selezionato](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

Se ti interessa testare questa nuova funzione e condividere il tuo feedback, invia un’e-mail a [grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com) dall’indirizzo e-mail associato al tuo Adobe ID.


### Porta il tuo Git (BYOG) {#gitlab-bitbucket-azure-vsts}

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
| *Le impostazioni esistenti come gli elenchi `IP Allow` continuano a funzionare?* | Sì, gli elenchi `IP Allow` esistenti continuano a funzionare normalmente. Tuttavia, se l’archivio Git esterno è protetto da un firewall, gli [Indirizzi IP Adobe necessari devono essere aggiunti all’elenco consentiti](/help/implementing/cloud-manager/ip-allow-lists/introduction.md). |
| *Funzionano tutti gli URL dell’archivio GitLab? L’URL dell’archivio in uso segue il formato `https://gitlab_dedicated_url.com/path/repo-name.git`, che differisce dall’esempio riportato nella documentazione.* | Sì, è supportato qualsiasi archivio GitLab che supporta API V3 o V4, inclusi gli URL GitLab con hosting autonomo come quelli descritto in [Aggiungere archivi esterni in Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md) (`https://git-vendor-name.com/org-name/repo-name.git`). |


#### Gestisci token di accesso{#manage-access-tokens}

Utilizza **Gestisci token di accesso** in Cloud Manager per visualizzare, rinominare ed eliminare i token di accesso associati agli archivi BYOG esterni, ad esempio GitHub Enterprise, GitLab, Bitbucket e Azure DevOps.

Consulta [Gestisci token di accesso](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md).

<!-- If you are interested in testing this new feature and sharing your feedback, send an email to [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) from your email address associated with your Adobe ID. -->


### Aggiungere una pipeline di configurazione Edge Delivery {#add-eds-pipeline}

Le pipeline di configurazione sono ora supportate per i siti creati con Edge Delivery Services, espandendo questa funzionalità oltre i singoli ambienti di Cloud Service. È possibile utilizzare le **pipeline di configurazione** per gestire impostazioni quali le regole di filtro del traffico e le configurazioni del firewall per applicazioni web (WAF), se applicabile. Consulta le [configurazioni supportate](/help/operations/config-pipeline.md#configurations).

**Miglioramento recente**

* Le pipeline di Edge Delivery Services ora visualizzano **Configurazione** nella colonna **Codice distribuito**, consentendo l&#39;identificazione immediata delle distribuzioni di sola configurazione. <!-- CMGR‑69681 -->
* Cloud Manager mostra **Aggiungi pipeline Edge Delivery** quando un programma contiene almeno un sito Edge Delivery Services e un dominio mappato. In caso contrario, l’opzione risulta disabilitata e una descrizione comando spiega i requisiti mancanti. <!-- CMGR‑69680 -->
* Nella scheda **Edge Delivery** è visualizzato un nuovo widget **Edge Delivery pipeline** in cui sono elencati il nome, lo stato, l&#39;archivio e il ramo di ogni pipeline. <!-- (CMGR-69052) -->

  ![Widget pipeline Edge Delivery con nome pipeline, stato, repository e ramo](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-widget.png)

* Il pannello **Filtri** aggiunge una sezione **Tipo di consegna**; include le caselle di controllo **Consegna Edge** e **Consegna pubblicazione**. <!-- (CMGR-69682) -->

  ![Pannello dei filtri che mostra il nuovo tipo di consegna Edge e la consegna Publish](/help/implementing/cloud-manager/release-notes/assets/filter-delivery-type.png)

![Aggiungi pipeline Edge Delivery nell’elenco a discesa Aggiungi pipeline](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add.png) *Aggiunta di una pipeline Edge Delivery dalla pagina **Panoramica del programma**, scheda **Pipeline**.*

![Finestra di dialogo Aggiungi pipeline di Edge Delivery](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add-dialogbox.png) *Finestra di dialogo Aggiungi pipeline di Edge Delivery.*

Vedi [Aggiungi pipeline Edge Delivery](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md)

<!-- If you are interested in testing this new feature and sharing your feedback, send an email to [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com) from your email address associated with your Adobe ID. -->


## Correzioni di bug

* Le pipeline ora distribuiscono variabili solo alla configurazione del dominio Edge Delivery Services attivo, ignorando eventuali configurazioni rimosse durante la ricreazione della pipeline. <!-- (CMGR‑70039) -->
* L’esecuzione della pipeline ora viene avviata in modo affidabile; è stato risolto un problema che impediva l’avvio di alcune pipeline a causa di errori di gestione delle risorse interne. <!-- (CMGR‑58167) -->
* La copia del contenuto convalida le autorizzazioni di Cloud Manager e blocca l’avvio del sistema da parte di utenti che non dispongono dei diritti di Manager implementazione o Amministratore. <!-- (CMGR‑62097) -->


<!-- ## Known issues {#known-issues} -->

